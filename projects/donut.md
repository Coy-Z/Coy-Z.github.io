---
layout: default
title: Donut
permalink: /projects/donut/
---

# Donut

The task in this project was to develop a program that displays a rotating donut in console, using ascii characters.
On this webpage, I have used javascript to render the program to work in the webpage.

You can download the raw C++ file <a href="/files/Donut.cpp/">here</a>. However the code is displayed below.

```
{
// This project aims to program a rotating torus animation using ascii characters.

// Coy Zhu - 07/2024

// Include packages and define constants
#include <iostream>
#include <cmath>
#include <Eigen/Dense>
#include <string>
#include <cstdlib>
#include <vector>
#include <chrono>
#include <thread>
#include <array>
#include <omp.h>


#define screen_width 100
#define screen_height 100
#define R1 1
#define R2 2.0
#define z1 4
#define PI 3.14159265358979323846
constexpr double z0 = screen_width * z1 * 3 / (8 * (R1 + R2));


// Define structures
struct vector_scalar {
	std::vector<double> vector;
	double scalar;
};

// Define projection function
vector_scalar point_projection(double x, double y, double z) {
	double X, Y, ooz;

	X = x * z0 / (z + z1);
	Y = y * z0 / (z + z1);
	ooz = 1 / z;
	std::vector<double> r1 = { X,Y };

	vector_scalar r1ooz = { r1, ooz };

	return r1ooz;
}

// Define the pixel function
std::vector<double> position(double theta, double phi, double A, double B) {
	double X, Y, Z;

	// Pre-calculating trig values
	double cosphi, sinphi, costheta, sintheta, cosA, sinA, cosB, sinB;
	cosphi = cos(phi);
	sinphi = sin(phi);
	costheta = cos(theta);
	sintheta = sin(theta);
	cosA = cos(A);
	sinA = sin(A);
	cosB = cos(B);
	sinB = sin(B);

	// Calculating the position components
	X = (R2 + R1 * costheta) * (cosphi * cosA + sinphi * sinA * sinB) + R1 * sintheta * sinA * cosB;
	Y = (R2 + R1 * costheta) * (sinphi * cosA * sinB - cosphi * sinA) + R1 * sintheta * cosA * cosB;
	Z = (R2 + R1 * costheta) * sinphi * cosB - R1 * sintheta * sinB;

	// Assigning components to a vector r
	std::vector<double> r = { X,Y,Z };
	return r;
}

// Illumination
double illumination(double theta, double phi, double A, double B) {
	double Nx, Ny, Nz, L;

	// Pre-calculating trig values
	double cosphi, sinphi, costheta, sintheta, cosA, sinA, cosB, sinB;
	cosphi = cos(phi);
	sinphi = sin(phi);
	costheta = cos(theta);
	sintheta = sin(theta);
	cosA = cos(A);
	sinA = sin(A);
	cosB = cos(B);
	sinB = sin(B);

	// Calculating the surface normal components
	Nx = cosA * cosphi * costheta + sinA * cosB * sintheta + sinA * sinB * costheta * sinphi;
	Ny = cosA * cosB * sintheta - sinA * cosphi * costheta + cosA * sinB * costheta * sinphi;
	Nz = cosB * costheta * sinphi - sinB * sintheta;

	// Assigning components to vector n
	Eigen::Vector3d n = { Nx, Ny, Nz };

	// Dot product n with the source direction for an illumination index
	Eigen::Vector3d src = { 0,-1,1 };
	L = n.dot(src);
	L /= sqrt(2);
	return L + 1;
}

// Frame Rendering
void frame(double A, double B) {
	// Local variable declarations
	std::vector<double> r, r1;
	double ooz, L, theta, phi;
	vector_scalar r1ooz;

	// Initialise output and buffer arrays, where the buffer is to double buffer the output, reducing frame lag
	//static char output[screen_width][screen_height];
	//memset(output, ' ', sizeof output);
	static std::array<std::array<char, screen_width>, screen_height> output;
	std::memset(output.data(), ' ', sizeof(char) * screen_width * screen_height);

	// Potential double buffering
	/*char buffer[screen_width][screen_height];
	memset(buffer, ' ', sizeof output);*/

	// Initialise Z buffer to determine whether the point would be visible to us or not
	//double z_buffer[screen_width][screen_height] = { 0 };
	std::array<std::array<double, screen_width>, screen_height> z_buffer;
	std::memset(z_buffer.data(), 0, sizeof(double) * screen_width * screen_height);


	// Loop over theta and phi for the full toroid surface and calculate illumination values, storing results in buffer
	#pragma omp parallel for collapse(2)
	for (double theta = 0; theta < 2 * PI; theta += 0.05) {
		for (double phi = 0; phi < 2 * PI; phi += 0.01) {
			r = position(theta, phi, A, B);
			r1ooz = point_projection(r[0], r[1], r[2]);
			r1 = r1ooz.vector;
			ooz = r1ooz.scalar;
			int xp, yp;
			xp = round(screen_width / 2 + r1[0]);
			yp = round(screen_height / 2 + r1[1]);
			if (xp >= 0 && xp < screen_width && yp >= 0 && yp < screen_height) {
				L = illumination(theta, phi, A, B);
				if (L > 0 && ooz > z_buffer[xp][yp]) {
					z_buffer[xp][yp] = ooz;
					int index = round(L * 5.5);
					output[xp][yp] = ".,:;!-~=*#$@"[index];
				}
			}
		}
	}
	// Display frame
	std::cout << "\033cls";
	for (int j = 0; j < screen_height; j++) {
		for (int i = 0; i < screen_width; i++) {
			std::cout << output[i][j];
		}
		std::cout << std::endl;
	}
	// Could add double buffering
}

// Main
int main() {
	double A, B;
	A = 0;
	B = 0;
	while (true) {
		frame(A, B);
		std::this_thread::sleep_for(std::chrono::milliseconds(1));
		A += 0.2;
		B += 0.3;
	}
}
}
```

