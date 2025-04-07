
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




<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/MemberFunction.png" width="600" height="300">


I added this snip of code to show a change I've made. I've removed rain.(object) from "rain.GotoXY". I had to create an object (instance) of the DigitalRain class because I had the logic to generate the rain effect in 
main.cpp outside the  DigitalRain class and i needed the object rain to access the methods (functions). Now that I have the logic moved to the DigitalRain class as part of the GenerateRain() member function, it can directly call all the other functions in the class (e.g GotoXY(), SetGreenText()) without needing to go through the object. 

--------

--------
The code below is from the DigitalRain.cpp file. This is the source file where the actual code for the DigitalRain class methods (functions) is written. The class and its functions are declared in the DigitalRain.h header file, the real code (logic) for what the methods (functions) do is written here.


![image](https://github.com/user-attachments/assets/493531d5-6deb-4341-90a7-0a552bfe6a1e)

This is the constructor method. The constructor runs automatically when the object of the DigitalRain class is created. The rain object in main.cpp is what triggers the constructor to run. The constructor takes in the screen's width and height as arguments and stores them in screenWidth and screenHeight to set the screen size for the digital rain effect.

rainPositions is the name of the vector declared in the .h file. The line rainPositions.resize(width, 0); in the constructor resizes the vector to match the number of columns on the console (width). The initial value of each element in the vector is set to 0, which means each column starts at position 0 on the console.


This is the vector declared in the digitalrain.h (header) file. The reason to use a vector is that I need to track the position of each character in the rain effect across multiple columns. Since the number of columns depends on screenWidth, a vector makes it easy to store a varying number of values because a vector is a dynamic array that can change its size as needed.
![image](https://github.com/user-attachments/assets/493531d5-6deb-4341-90a7-0a552bfe6a1e)

---------

---------

Here I used a Getter. This method (function) returns the value of screenWidth. The const keyword means the method won’t change any class variables. It allows access the current value of screenWidth without modifying it. The getter provides controlled access to a private variable, this ensures it can be read safely without being modified directly. It helps maintain encapsulation, consistency, and makes it easier to make future changes without affecting other parts of the program.

![image](https://github.com/user-attachments/assets/ac9c5482-5d5c-4399-ba00-a3b6dcda70cd)

---------

---------

The GotoXY function is declared in the DigitalRain.h header file. This moves the console cursor to a specific position on the screen using two integer arguments, x (columns) and y (rows). It defines a COORD structure to store these positions, sets the X and Y values with the passed arguments, and then uses SetConsoleCursorPosition with GetStdHandle(STD_OUTPUT_HANDLE) to move the cursor to the new position in the console.
The COORD structure is a data type in Windows used to store the coordinates X (for the column position) and Y (for the row position), used to specify the location of something, in this program used to for the console cursor.
![image](https://github.com/user-attachments/assets/c4f24a1e-5fae-43a7-9b44-f85ab2609441)

----------

----------

This method uses the std::system("CLS") command to clear the console. It runs the "CLS" command, which is a built-in command in the operating system that clears all the text currently displayed in the console window.
![image](https://github.com/user-attachments/assets/08c49227-f620-41c6-be2b-c48bd1cb4971)

------------

------------

This is the The GenerateRain method which creates the falling characters effect in the console. The method starts by randomly setting the column position of each character (rain column) using std::rand() % maxCol inside the first loop. The rainPositions[i] stores each column’s random position.

It then enters an infinite loop (while (1)) to continuously generate the rain effect. For each row (from 1 to maxRow), it moves each character to a new position by updating rainPositions[i] and uses GotoXY to position the cursor at that spot. The text color is set to green using SetGreenText(), and it alternates between printing "1" and "0" characters (if (i % 2 == 0)).
The std::this_thread::sleep_for(std::chrono::milliseconds(100)) creates a short delay, making the characters appear to "fall" down the screen by pausing the program for 100 milliseconds between each update.
![image](https://github.com/user-attachments/assets/42ac5b3d-1eaa-49b7-a3b0-435549b8e0f5)

These are some images of the digital rain effect I was able to achieve.

<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/SetHeightTerminalDigiRain.png" width="400" height="300">


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigiRainFalling2.png" width="400" height="300">


<img src="https://raw.githubusercontent.com/Kennyatu23/digital-rain-cpp/main/docs/assets/images/DigiRainFalling3.png" width="400" height="300">


