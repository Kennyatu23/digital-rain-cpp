
## DigitalRain C++
---

----

## INTRODUCTION 
Welcome to my github blog for my year 4 digital rain project using Modern C++. The project brief was to design and execute code to simulate the "Matrix" style effect,
where characters fall down the console screen like Digital rain. Within this blog I hope to demonstrate my on going progress with explaination of my code used. The blog
will be broken down into sections to show the design and test, problem solving, insight into modern C++ and explain the algorithms used. 

## Design & Test
This project was designed using modern C++ (released 2011) which supports object orientated programming. Object orientated programming is 
a style of programming based on the concept of objects. Objects are intances of classes which contain the attributes(data) and methods(functions)
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
has two arguments.Function is declared here in class named DigitalRain. This is where the work is done by function.

![image](https://github.com/user-attachments/assets/42006980-25b9-4fcb-b488-17e28b7305fb)




In the code I have added a constructor for better code practice for initialising screen height and screen width. Also I 
have included a short delay which gives the look of the falling character by pausing the program for set time (milliseconds).
I have also included a new header libraries for time related code. 

![image](https://github.com/user-attachments/assets/b0659ce0-54c4-431f-9a43-79062de201e8)

![image](https://github.com/user-attachments/assets/47bae286-76d9-429d-be2d-7f0c54adac88)


main.cpp file

#include <chrono>			// Time related library



<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/ScreenshotRandom15032025.png" width="400" height="300">


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/ScreenshotRandom2.png" width="400" height="300">




Added Random columns code to main.cpp file only and the header library for rand() and seed random number generator.
![image](https://github.com/user-attachments/assets/75b569ba-c8e8-42e3-a4c1-0e0ca89a4c8f)


#include <cstdlib>                      // for rand() and srand() :: Random number generator

#include <ctime>                        // time seed for randomness

int main()
{
	std::srand(std::time(0));          // Seed random number generator


		while (1) {  
			                /*Random column Positions*/
                    int x = std::rand() % maxCol;  //Random column for the first character
		    int x1 = std::rand() % maxCol;  //Random column for the second  character


All the above snips are from the beginning of the project. It was just to try show the project at the very beginning. I didnt document the beginning very well
but I plan to go into more detail with the final finished code for the project digital rain and give a clearer understanding of what the code is doing.
-----------

-----------

In my main.cpp file (source file), I included standard library headers and my custom DigitalRain.h file. This links the code from DigitalRain.h to main.cpp, allowing access to the functions and classes defined in that header.
Here in my main.cpp, I set the console width (columns), height (rows), and the number of falling characters. These values control the size of the display and how many characters fall at once, shaping how the digital rain effect looks on screen.

I also declared two variables maxCol (width) maxRow and (height). These are used to store the maximum number of rows and columns which helps control the size of the screen. maxRow and maxCol (in main.cpp) are passed into the constructor in the DigitalRain class in DigitalRain.cpp and are used to set up the screen. I also pass maxRow and maxCol into the GenerateRain method in DigitalRain.cpp. This lets the method know the size of the screen so it can generate falling characters within the row and column limits I set.

I created the rain object of the DigitalRain class because you need to create an object to access the class’s member functions and variables. In C++, you cannot directly use the DigitalRain class methods or variables unless you create an object (like rain) of that class. The rain object allows me to use the DigitalRain constructor to set up the screen size by passing in the width and height.
After creating the rain object, I call the GenerateRain() method. Since GenerateRain() is part of the DigitalRain class, I need the rain object to access and run the method.

<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/SetHeightTerminalDigiRain.png" width="400" height="300">


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigiRainFalling2.png" width="400" height="300">


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigiRainFalling3.png" width="400" height="300">





<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/MemberFunction.png" width="600" height="300">


I added this snip of code to show a change I've made. I've removed rain.(object) from "rain.GotoXY". I had to create an object (instance) of the DigitalRain class because I had the logic to generate the rain effect in 
main.cpp outside the  DigitalRain class and i needed the object rain to access the methods (functions). Now that I have the logic moved to the DigitalRain class as part of the GenerateRain() member function, it can directly call all the other functions in the class (e.g GotoXY(), SetGreenText()) without needing to go through the object.  

