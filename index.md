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

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

main.cpp code for above image::

'#include <iostream>			// cerr, endl

#include <stdexcept>			// out_of_range

#include "DigitalRain.h"		// DigitalRain  need double quotes when class we create ourselves

#include <chrono>			// Time related library

#include <thread>			// Sleep


int main()
{

	DigitalRain rain;  // Class(Digitalrain) Object(rain)

	while (1) {
		int x = 3;	   // starting column of character (X)
		int y = 1;	   // starting row of character (top of screen would be 0) (Y)
		//int maxRow = rain.screenHeight;

		int x1 = 6;     // starting column of character (X)
		int y1 = 1;	// starting row of character (top of screen would be 0) (Y)
		
		int maxRow = rain.screenHeight;
		
		for (int row = y; row <= maxRow; row++) {

			rain.GotoXY(x, row);
			rain.SetGreenText();   // Set green text color
			std::cout << "!";      // THis line prints out character !!!!!!! in the terminal

			rain.GotoXY(x1, row);
			std::cout << "#";      // THis line prints out character ####### in the terminal
			std::this_thread::sleep_for(std::chrono::milliseconds(100));       //This short delay gives the look of falling character by pausing the program for set time(milliseconds)

			// Clears screen and reset y positions when reaching bottom
			if (row >= maxRow) {
				rain.ClearScreen();
				row = 1;        // Resets row position at end of each run

			}

		}
	}

	return 0;                  // returns nothing
}'



DigitalRain.cpp file for above image::


'#include <iostream>		// cout, endl, fixed

#include <string>		// string

#include "DigitalRain.h"	// Programmer

#include "TestDigitalRain.h"	// Test functions

#include <windows.h>		// SetConsoleCursorPosition

Function Named GotoXY is a function to palce the cursor at a particular point on the terminal using x and y axis
has two arguments
  Function is declared here in class named DigitalRain This is where the work is done by function 


void DigitalRain::GotoXY(int x, int y)       // Class funciton Name with two arguments(varibles type int)


{

	COORD coord;
	coord.X = x;
 
	coord.Y = y;
	SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
}

void DigitalRain::SetGreenText() {

	// Get the console handle
 
	HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
 
	// Set the text color to green (10 is green text with black background)
 
	SetConsoleTextAttribute(hConsole, 10);
}

/* Function to clear Screen*/

void DigitalRain::ClearScreen()

{ 

	std::system("CLS");
 
}'

DigitalRain.h for above  2 column 2 Character image::

/*************************Part of an include Guard Used in C++ to prevent multiple inclusions of the same header.**********************
#ifndef DIGITALRAIN_H:
This checks if the macro DIGITALRAIN_H has not been defined yet.
If it hasn’t, the code inside the guard will be processed.
If it has already been defined, the code is skipped, preventing redefinition errors.
#define DIGITALRAIN_H:
If the code inside the #ifndef is processed, this line defines the macro DIGITALRAIN_H so 
that any subsequent inclusion of this file will skip it.

Avoids Multiple Inclusions: Prevents multiple inclusions of the same header file, which can cause redefinition errors.
for example, if multiple files include DigitalRain.h, the compiler might try to process the same function declarations 
multiple times, leading to errors.
Efficiency: Skipping the already-included file can save compilation time.
*/


'#ifndef DIGITALRAIN_H

#define DIGITALRAIN_H

#include <iostream>		// Library ostream

#include <string>		// Library string

#include <vector>		// Library vector

#include <chrono>       // Library chrono (time related operations)

#include <windows.h>    // Library provides functions, macros, and data types 


/* Class is created "DigitalRain" and made public so it can be shared with other files (.h .cpp)*/
class DigitalRain

{

public:

    int screenWidth = 70;
    int screenHeight = 50;

    /* Public methods for other functionality */
    void GotoXY(int x, int y);     // Function prototype declaration informers compiler of the type of function arguments and return types if any
    void ClearScreen();            // Function prototype declaration for clear 
    void SetGreenText();           // Function to set green text color
   

    

private:

    std::vector<int> rainPositions;      // Stores current positions of each rain column
   
};

#endif

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In the code I have added a constructor for better code practice for initialising screen height and screen width This is the updated code::

main.cpp file


'#include <iostream>			// cerr, endl

#include <stdexcept>			// out_of_range

#include "DigitalRain.h"		// DigitalRain  need double quotes when class we create ourselves

#include <chrono>			// Time related library

#include <thread>			// Sleep

//#include "TestDigitalRain"	// Test Function

int TestSystemColours()

{

	std::system("COLOR 1F");    // Color blue background bright white text

	return 0;
 
}

int main()

{

	

		DigitalRain rain(70, 50);     // Class(Digitalrain) Object(rain) with width=70, height=50 
		

		int x = 3;	   // starting column of character (X)
		int y = 1;	   // starting row of character (top of screen would be 0) (Y)
		int x1 = 6;        // starting column of character (X)
		int y1 = 1;	   // starting row of character (top of screen would be 0) (Y)

		int maxRow = rain.GetScreenHeight();
		int maxCol = rain.GetScreenWidth();

		while (1) {	

		for (int row = y; row <= maxRow; row++)
		{
			rain.GotoXY(x, row);
			rain.SetGreenText();   // Set green text color
			std::cout << "!";      // THis line prints out character !!!!!!! in the terminal

			rain.GotoXY(x1, row);
			std::cout << "#";                                                 // THis line prints out character !!!!!!! in the terminal
			std::this_thread::sleep_for(std::chrono::milliseconds(100));      //This short delay gives the look of falling character by pausing the program for set time (milliseconds)


			if (row >= maxRow) {
				rain.ClearScreen();
				y = 1;

			}

		}
	}

	return 0;                  // returns nothing
}'

<DigitalRain.cpp file

'#include <iostream>				// cout, endl, fixed

#include <string>				// string

#include "DigitalRain.h"		        // Programmer

#include "TestDigitalRain.h"	                // Test functions

#include <windows.h>			        // SetConsoleCursorPosition

/*Function Named GotoXY is a function to palce the cursor at a particular point on the terminal using x and y axis
  has two arguments
  Function is declared here in class named DigitalRain This is where the work is done by function */


DigitalRain::DigitalRain(int width, int height) {

	screenWidth = width; // initialises the screenwidth with value passed from 'width'
	screenHeight = height; // initialises the screenheight with value passed from 'height'
}
// Getter for screen width
int DigitalRain::GetScreenWidth() const {
	return screenWidth;
}

// Getter for screen height
int DigitalRain::GetScreenHeight() const {
	return screenHeight;
}

void DigitalRain::GotoXY(int x, int y)               // Class funciton Name with two arguments/varibles type int
{
	COORD coord;
	coord.X = x;
	coord.Y = y;
	SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), coord);
}

void DigitalRain::SetGreenText() {
	// Get the console handle
	HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
	// Set the text color to green (10 is green text with black background)
	SetConsoleTextAttribute(hConsole, 10);
}

/* Function to clear Screen*/
void DigitalRain::ClearScreen() 
{ 
	std::system("CLS"); 
}'

DigitalRain.h file

'#ifndef DIGITALRAIN_H

#define DIGITALRAIN_H

#include <iostream>		// Library ostream

#include <string>		// Library string

#include <vector>		// Library vector

#include <chrono>               // Library chrono (time related operations)

#include <windows.h>            // Library provides functions, macros, and data types 


/* Class is created "DigitalRain" and made public so it can be shared with other files (.h .cpp)*/
class DigitalRain {
public:

    DigitalRain(int width, int height); //Constructor to initialise screen dimensions

    int GetScreenWidth() const;       // Getter for Screen width
    int GetScreenHeight() const;      // Getter for Screen height
    

    /* Public methods for other functionality */
    void GotoXY(int x, int y);     // Function prototype declaration informers compiler of the type of function arguments and return types if any
    void ClearScreen();            // Function prototype declaration for clear 
    void SetGreenText();           // Function to set green text color
    

    

private:
    /* Private member Varibles */
    int screenWidth;         //varible for screen width
    int screenHeight;        // varible for screen height

    std::vector<int> rainPositions;      // Stores current positions of each rain column
    


};



#endif'


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/ScreenshotRandom15032025.png" width="400" height="300">

<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/ScreenshotRandom2.png" width="400" height="300">

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Added Random columns code to main.cpp file only

'#include <iostream>			// cerr(Charactor error), endl(endline)

#include <stdexcept>			// out_of_range

#include "DigitalRain.h"		// DigitalRain  need double quotes when class we create ourselves

#include <chrono>			// Time related library functions

#include <thread>			// Sleep function

#include <cstdlib>              // for rand() and srand() :: Random number generator

#include <ctime>                // time seed for randomness

//#include "TestDigitalRain"	// Test Function

int TestSystemColours()
{
	std::system("COLOR 1F");    // Color blue background bright white text

	return 0;
}

int main()
{
	std::srand(std::time(0));          // Seed random number generator
	

	DigitalRain rain(70, 50);  // Class(Digitalrain) Object(rain) with width=70, height=50 

		int maxRow = rain.GetScreenHeight();  // Getting the screen height
		int maxCol = rain.GetScreenWidth();   // Getting the screen width


		while (1) {  
			                /*Random column Positions*/
                    int x = std::rand() % maxCol;  //Random column for the first character
		    int x1 = std::rand() % maxCol;  //Random column for the second  character

                    int y = 1;	   // Starting row for both character (top of screen would be 0) (Y)


		for (int row = y; row <= maxRow; row++)
		{
			rain.GotoXY(x, row);   // Move to the character position
			rain.SetGreenText();   // Set green text color
			std::cout << "!";      // Print out character ! in the terminal

			rain.GotoXY(x1, row);
			std::cout << "#";      // Prints out character # in the terminal
			std::this_thread::sleep_for(std::chrono::milliseconds(100));      //This short delay gives the look of falling character by pausing the program for set time (milliseconds)


			if (row == maxRow) {
				rain.ClearScreen();
				//y = 1;

			}

		}
	}

	return 0;                  // returns nothing
}'




