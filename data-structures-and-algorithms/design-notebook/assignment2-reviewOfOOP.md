# Design Notebook
**Rin Allen**
**Assignment #2**
## Problem Statement
The program opens and reads a text file to build a polymorphic array of turtle objects. It then displays each turtle along with its attributes and an overridden method describing the threats to its survival. Next, the program creates a tour object for 2025 and passes in the turtle array. Finally, it displays which turtles participated in the 2025 tour and how many miles each one traveled.
## Understandings

#### What I know
- How to create a parent class with child classes that have a is-a relationship.
- How to overload constructors, override methods, and create getters/setters. 
- To make instance variables private.
#### What I Don't Know
- I don't have opening and reading from a file memorized so this will be a good review. Honestly I may need to make flash cards about file handling. 
- Everything else about this assignment i'm pretty comfortable with, just need to make sure I pay close attention to the "must dos" and to not make any assumptions. 
## Sketch 
![[design-notebook-assignment2-turtle-sketch.png]]
## Pseudocode for Main

> **Note to TA:** Obsidian (where I create and store my design notebook) uses the markdown language. Markdown doesn't allow for indentation using `tab` so this is why I used bullets in my last assignment. If you prefer I can embed HTML so the indentation transfers that way. Please advise on your preference on my design notebook. 👀
 
<pre>
//Create Polymorphic Turtle Array a.k.a turtleSquad
open SeaTurtle.txt file for reading
read the first line and assign to turtleSquadSize
allocate memory for SeaTurtle [] array named turtleSquad
for loop each index in turtleSquad
    create String type and read from file to assign value
    read from file double milesTraveled
    read from file int daysTracked
    read from file int tourYear
    read from file String name
    if type equals ignore case "leatherback" then 
        assign the turtleSquad[i] a new object child 
    else if type equals
        assign the type 
    repeat as needed

//Display turtleSquad Array
Print the title of the tracked turtles and the columns
for loop each index in turtleSquad
    display all the attributes of the turtle with getters
    display threatToSurvival()

//Create TourDeTurtles Object and Display
create new TourDeTurtle object tour2025
call setupTour() passing in turtleSquad array
display tour using tour2025.displayTourDetails()
//end of main
</pre>
## Lessons Learned 

-  It wasn't clicking in my noggin that I could literally type in the `type` straight into the constructor. It took me some googling to realize I did not need a String variable. Intellij wouldn't let me put anything before the super call anyway. 
- I forgot to put an index count for filling the turtles to track array's index. 
	- I put `i` instead and it messed things up because as `i` incremented due to the tour date not being 2025 it caused indexes to be skipped in the turtles to track array. 
- How to embed HTML in Obsidian.

> **Note to TA:** Prepare yourself. The code on the coming pages have been pasted into a web based code printer so that its easier for you to read (you're welcome). Unfortunately, this means I cannot remove the watermark on the top of the pages. So fear not! There is no cheating! this is my code, just formatted using jaredpetersen.com/codeprinter/

![[design-notebook-proof-not-cheating.png]]