# Design Notebook
**Corinne Allen**
**Assignment #1**
## Problem Statement
The program will perform 5 tasks. 
- Task #1 
	- Create a random number generation. It will generate 20 random numbers between 10 and 40. Then it will place each value into an array as well as display the value. 
- Task #2 
	- Perform computations on the array. It will compute and display **sum, average, median, largest value** and **number of times the largest value appears in the array** Sorting the array will help with the task of finding the median and largest value and its occurrences. 
- Task #3 
	- Using a 2D array. It will create a 2D array with 4 rows and 5 columns. It will place the values in the 1D array into the 2D array, row by row. It will print each value from within the 2D array. 
- Task #4 
	- It will write and read to a file. It will create and open a file for writing. It will then iterate through the 2D array and write the values to the file in increasing order, each on its own line. Finally it will close the file. 
- Task #5 
	- is reading from a file. It will reopen the file for reading. It will read each value from the file and display it in the console.
## Understandings

#### What I know
- How a normal array works (1D).
- All the proper syntax for the Java language.
- How to use for loops to manipulate arrays and receive a desired value. (manually, not through for each loops, honestly don't even know how those work. Hopefully we learn at some point)
- How to generate a random number using the equation Mrs. Gonzalez provided in the assignment instructions. 

#### What I Don't Know
- I've never used 2D arrays before.
	- There's 2D array information in canvas so I'll check that out, and I'll look up the array type in chapter 8 if I'm still struggling. 
- I don't particularly remember much about dealing with files.
	- I will read through chapter 11 and check out the canvas review material to get a solid understanding on how to perform file actions in Java.
- I'm unfamiliar with InjelliJ. 
	- I know its not required but it's super aesthetic, and I've heard good things, so I'm going to use eclipse for this assignment then copy over my code to Intellij to play with it a bit. 

## Sketch 
> **Note to TA:** The example design notebook said I may include its sketch in my notebook, so I'm doing a replica of what Mrs. Gonzalez gave us. I use my iPad and stylus because its easier on my carpel tunnel.

![[sketch-notes.png]]
![[sketch-assignment1.png]]
## Pseudocode for Main
#### //Task #1: Fill array with 20 random values
Create an array to hold 20 values
for 20 iterations
- Generate a random value between 10 and 40
- Place the value into the array
- Display the random value on the console
end of for loop

#### //Task #2 Computing and displaying computations
//compute sum
sum = 0 
for ea. array value (not using a for each loop) (array.length)
- sum = sum + current array value
end of for loop

//compute average
avg = sum/number of array values
display sum and average

//compute median
Use Arrays.sort to organize array values
middle1 = [array.length / 2] (because there's an even amount of values)
middle2 = array1D[(array.length / 2) - 1]
median = (middle1 + middle2 / 2.0)
display median

//compute largest value
max = array1D[0]
for ea. array value starting at index 1 (int i = 1)
- if value is larger than max
	- max = value
display max

//# of times max occurs
count = 0
for ea. array value 
- if value is max 
	- count ++
display count
#### //Task #3 Using a 2D array
//create a 2D array and place the values from the 1D array into the 2D array. Print ea. value from
//within the 2D array

Create a array2D with 4 rows and 5 columns
final numRows = 4
final numCols = 5
index for 1D array = 0
for ea. row
- for ea. column
	- array2D[row],[col] = array1D[index]
	- increment index
- end col
end row

#### //Task #4: Create and open a file for writing. 
// Iterate through 2D array writing the values to a file in increasing order.

Create a file named **assignment1.txt**
Open file for writing
for ea. row (0 to NUM_ROWS)
- for ea. column (0 to NUM_COLS)
	- Write value in 2D array at [row], [column] to the file on it's own line
- end column for loop
end row for loop
Close file

#### Task #5: Open file for reading
//Obtain values from file and display in increasing order

Reopen file for reading
read the first line
display 2D array in a for loop //to match the example output
for 20 iteration
- read value from file and display on console
end for
Close file

print file path to console //to match example output

## Lessons Learned 

-  I learned the different Java code to create and open a file, write to it, and read from it to the console. 
- How 2D arrays are organized, how to create them, and how to manipulate nested loops to fill them properly. 
- That Intellij's debugger is amazing. 
- That I can use Obsidian as my Design notebook and upload it to my GitHub, via git bash, as a portfolio. (yay free storage) 
- I got refreshed on some basic syntax, and loops logic that I was a little rusty on. 