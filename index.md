---
layout: post
title: A Project in Modern C++
tags: cpp coding project
categories: demo
---

This is my first paragraph...

Welcome to my blog. This is my year 4 project for C++. We have to create and test a digital rain like the matrix.

## This is a Heading

This is a paragraph. Add an empty line to start a new paragraph.


Font can be *Italic* or **Bold**.

Code can be highlighted with 'backticks'.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list:

- vectors
- algorithms
- iterators

- 

You can add an impage that has been uploaded to the repository in a /docs/assets/images folder.

<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigitalRain.png" width="400" height="300">

main.cpp code for above image:

'#include <iostream>				// cerr, endl
#include <stdexcept>			// out_of_range
#include "DigitalRain.h"		// DigitalRain  need double quotes when class we create ourselves
#include <chrono>				// Time related library
#include <thread>				// Sleep
//#include "TestDigitalRain"	// Test Function

int TestSystemColours()
{
	std::system("COLOR 1F");    // Color blue background bright white text

	return 0;
}

int main()
{

	DigitalRain rain;  // Class(Digitalrain) Object(rain)

	while (1) {
		int x = 3;	   // starting column of character (X)
		int y = 1;	   // starting row of character (top of screen would be 0) (Y)
		//int maxRow = rain.screenHeight;

		int x1 = 6;    // starting column of character (X)
		int y1 = 1;	   // starting row of character (top of screen would be 0) (Y)
		
		int maxRow = rain.screenHeight;
		
		for (int row = y; row <= maxRow; row++) {

			rain.GotoXY(x, row);
			rain.SetGreenText();   // Set green text color
			std::cout << "!";      // THis line prints out character !!!!!!! in the terminal

			rain.GotoXY(x1, row);
			std::cout << "#";      // THis line prints out character ####### in the terminal
			std::this_thread::sleep_for(std::chrono::milliseconds(100));      //This short delay gives the look of falling character by pausing the program for set time (milliseconds)

			// Clears screen and reset y positions when reaching bottom
			if (row >= maxRow) {
				rain.ClearScreen();
				row = 1;               // Resets row position at end of each run

			}

		}
	}

	return 0;                  // returns nothing
}'
