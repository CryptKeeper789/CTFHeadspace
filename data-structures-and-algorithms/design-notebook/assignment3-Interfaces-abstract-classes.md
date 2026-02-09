# Design Notebook
**Rin Allen**
**Assignment #3**
## Problem Statement

This program reads athlete information from a file and creates a polymorphic array 
of Athlete objects. The program then performs three tasks: First, it displays all 
athletes along with their disciplines and speeds. Second, it identifies which athletes 
can swim, stores them in an ArrayList, and displays their swimming information. 
Finally, it simulates a bike race by comparing bike speeds and displays the winner.

## Understandings

#### What I know
- After reading through chapter 13 I have a pretty solid understanding of the similarities and differences on abstract classes and interfaces. 
- I know I need to code to the interfaces NOT the instances of the sub classes. Particularly with the bikeRace method and the findSwimmers method.
- I know I want to code the classes and interfaces first before stressing about main. 
- I know I want to use a "find max value" algorithm for bikeRace which should be fairly easy. 
#### What I Don't Know
- I have not ever worked with an ArrayList so I'm going to review the end of chapter 11 for more information. 
- I need to review casting to ensure I use the proper syntax for it. 
## Sketch 
![[assignment3-flow-sketch.png]]
![[assignment3-hier-sketch.png]]

## Pseudocode 

###  For Main
<pre>
//Create Polymorphic Athlete a.k.a sweatSquad
open Athlete.txt file for reading
read the first line and assign to sweatSquadSize
allocate memory for Athlete [] array named sweatSquad
for loop each index in sweatSquad
    create String type and read from file to assign value
    read from file double assigned to variable bikeSpeed 
    read from file double assigned to variable runSpeed
    read from file double assigned to variable swimSpeed
    read from file String  assigned to variable name
    if type equals ignore case "Aquathlete" then 
        assign the sweatSquad[i] a new object child for
         **Aquathlete**
    else if type equals
        assign the type to the correct child class
    repeat for all athlete subclass types
close input

//Display sweatSquad Array
call displayAthletes()

//Find which athletes are Swimmers
call findSwimmers and assign the Array list object to a 
reference variable swimmers 
for loop through the swimmers ArrayList size
	if athlete is an instanceof Swimmer
		display swimmer's  name, type, and (Swimmer) casted swimSpeed 
		using getters. 

//Simulate a bike race
call bikeRace() and assign Athlete object to reference 
variable fastestBiker
Display fastest biker's name, type, and casted (Biker) bike speed. 
//end of main
</pre>
### For bikeRace
<pre>
create a maxSpeedBiker Athlete ref. variable initialize to null
create a maxSpeed double variable initialize to 0
for each index of the incoming athlete array starting at 0
	if instanceOf Biker
		if athlete in array at index i's has a bikeSpeed that is greater than maxSpeed
			Assign that athlete to maxSpeedBiker
			Assign that speed to maxSpeed
return maxSpeedBiker
</pre>

## Lessons Learned 

-  I made a silly move and put the keyword "abstract" in the wrong order when constructing the Athlete class. I was annoyed with IntelliJ for a good minute before I realized my error. 
- My brain slightly overheated thinking of how to do the bikeRace for loop. I kept wanting to initialize the maxSpeedBiker to the Althete at index 0 but you cant do that because athlete at index 0 may not be an instance of biker and therefore may not have bikeSpeed to check. 
	- I instead initialized maxSpeedBiker to a null value and assigned maxSpeed to 0 to start the comparison. 
- 

