
## DigitalRain C++
---

----

## INTRODUCTION 
Welcome to my github blog for my year 4 digital rain project using Modern C++. The project brief was to design and execute code to simulate the "Matrix" style effect,
where characters fall down the console screen like Digital rain. Within this blog I hope to demonstrate my on going progress with explaination of my code used. The blog
will be broken down into sections to show the design and test, problem solving, insight into modern C++ and explain the algorithms used. 

## Design & Test
This project was designed using modern C++ (released 2011) which supports object orientated programming. Object orientated programming is 
a style of programming based on the concept of objects. Objects are intances of classes which contain the attributes(data) and methods(fuctions)
which manipulates the data stored in the object.

In my design I started by creating a class called DigitalRain. I made the class public so it could be shared with the other files where nesscessary.
For this class I created an object (instance) called rain which I used to pass two parameters (width,height). I created a constructor for my DigitalRain
class. The constructor initialises the object rain. I set the width (columns), height (rows) to constants. The console is broken down into rows and columns.
I also set the number of charactors I wanted falling to constants. I used a vector called rainPositions to store the current position of the rain columns.
I created methods for setting the text to green, to clear the screen, generate the rain, for setting the cursor position to x (columns) or y (rows). I was 
to try and run some tests but I ran out of time to get to that stage. Also the code is distributed between different files sucgh as .h (header files)  and .cpp
(source files). Using header and source files is better for orgainising code. Makes code easier to read, maintain and makes code more efficient when compiling.

- Classes: User_defined data types that work as blueprints for creating objects. A class defines the attributes (data members) and methods (functions) that describe 
           the behavior and data of the objects created from it.
- Objects: Instances of a class, created with specific data. They can represent things from the real world or just ideas or concepts. When a class is defined,
           it only describes how an object should be, but no object exists.
- Methods: Are functions which define the actions or behaviors of an object (what object it can do). They are written inside a class and describe the specific
           tasks the object can perform.
- Attributes: Represent the state of an object. In other words, they are the characteristics that make each object unique. Objects store data in ther attributes.
              Class attributes are shared by all objects of that class and are defined in the class template.

- Constructor: Special type of method in a class that is automatically called when you create an object. It's used to set up the object, like giving it starting values.
- Vector: A collection of things of the same type int, floats, char or user defined (custom data types). Implemented as a class template and not a built in type.
  
- .cpp files: Source file which contains the implementation of the methods that were declared in the corresponding header file (.h). Where the actual code for the program  
              logic is witten.Basically contains the method definitions, where you wrtie how things work and are linked to header files.
- .h files: Header file which contains declarations of methods (functions), classes, varibles and constants but not actual code (implementation). Works as an interface for
            the code, lets other files know what methods and classes are availible. Has the declarations, has no actual code of what methods do and is shared between files. 
   
   
 


A bullet list:

- algorithms
  
- some code example and explain

- 
- iterators

- 
## Algorithm
Hyperlinks look like this: [GitHub Help](https://help.github.com/).
You can add an impage that has been uploaded to the repository in a /docs/assets/images folder.


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigitalRain.png" width="400" height="300">

This image is the output of the first piece of code I implemented. The code shows the class DigitalRain and the object rain which I created.
You can see I have set the cursor to start at column (x) position three and the row (y) to one. This starts the cursor three positions
in from the side of the console and one position down from top of the console.

main.cpp code for above image::
'int main()
{

	DigitalRain rain;          // Class(Digitalrain) Object(rain)

	while (1) {
		int x = 3;	   // starting column of character (X)
		int y = 1;	   // starting row of character (top of screen would be 0) (Y)
		//int maxRow = rain.screenHeight;

		int x1 = 6;       // starting column of character (X)
		int y1 = 1;	  // starting row of character (top of screen would be 0) (Y)
		
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


Below is the source file for the above image. You can see the header files (libraries) included. For example the input/output stream library
#include <iostream>. 
DigitalRain.cpp file for above image::

'#include <iostream>		// cout, endl, fixed

#include <string>		// string

#include "DigitalRain.h"	// Digital rain

#include <windows.h>		// SetConsoleCursorPosition

Function Named GotoXY is a function to place the cursor at a particular point on the terminal using the x(columns) and y(rows) axis
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



In the code I have added a constructor for better code practice for initialising screen height and screen width. Also I 
have included ashort delay which gives the look of the falling character by pausing the program for set time (milliseconds).
I have also included a new header libraries for time related code. 

main.cpp file

#include <chrono>			// Time related library


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

<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/SetHeightTerminalDigiRain.png" width="400" height="300">


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigiRainFalling2.png" width="400" height="300">


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigiRainFalling3.png" width="400" height="300">





<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/MemberFunction.png" width="600" height="300">


I added this snip of code to show a change I've made. I've removed rain.(instance) from rain.GotoXY. I had to create an instance or object of the class Digital rain when I had this logic to generate the rain effect in 
main.cpp as the logic was outside the class DigitalRain and i needed the object rain to access the functions in DigitalRain class. Now I have the logic moved to the DigitalRain class the GenerateRain has now become a member fuction it can directly call all the other functions in the DigitalRain class (e.g GotoXY(), SetGreenText()).  

