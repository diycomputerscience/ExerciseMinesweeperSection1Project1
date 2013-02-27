<h1>Section 1 - Project 1</h1>

<h2>Overview</h2>

This is the first activity of this course. The purpose of the activity is to become familiar with the development environment that we will use in this course. It consists of:

 - The IDE (Eclipse)
 - The directory structure of the project
 - JUnit the unit testing infrastructure
 

We have given you an almost blank Eclipse project. It has two files - README.md, and a class called ```PleaseDelete```, which as the name suggests should be deleted once you import the project into your workspace.

<h2>Steps For This Activity</h2>
 1. Start the Eclipse IDE
 1. Create a workspace for this course (call it anything)
 1. Create a new source folder called 'test' for [unit tests](http://en.wikipedia.org/wiki/Unit_testing). Creating a 'test' directory for unit tests, is a fairly standard convention in a Java project.
 1. Using Eclipse, create a JUnit 4.0 test case called ```com.diycomputerscience.minesweeper.SquareTest``` in the 'test' folder. The 'test' folder is for unit test classes and the 'src' folder is for production code.
 1. Copy and paste the code shown below in _code sample 1_ into ```SquareTest```.
 1. You will notice a compilation error in the code. You need to fix that error.
 1. Now that the error is fixed and the code compiles, we can now start thinking about the API of the ```Square``` class. Ask yourself these basic questions: 
    1. _What should a Square class know about itself ?_  
    1. _What services should a Square class offer to the rest of the world ?_ . 
    We will answer these questions iteratively. Since we are making a Minesweeper game, the first thing a Square should know about itself is if it is a mine. Add a ```boolean``` attribute ```mine``` and accessor methods to get and set it's value. We normally do not test accessor methods, so we will not do anything to the test case as yet.
 1. Create a no-args (default) constructor for ```Square```.
 1. We still do not have anything to test, so the test case will fail. That is ok for now.

<h2>Stuff You Should Notice While Doing The Project</h2>
 1. Coding conventions used for class and method names.
 1. Coding conventions used for the accessor methods in the class ```Square```.
 1. Similarity in packages that ```Square``` and ```SquareTest``` belong to.
 1. How Eclipse displays results of a test case

<h2>Learning Outcomes</h2>
 1. How to create a source folder in Eclipse
 1. How to create a new class in Eclipse
 1. How to create a JUnit 4.0 test case in Eclipse
 1. How to run a test case
 1. How to create an attribute and it's accessors
 1. How to create a no-arg constructor for a class 


<h2>Code Samples</h2>

    package com.diycomputerscience.minesweeper;

    import static org.junit.Assert.*;

    import org.junit.After;
    import org.junit.Before;
    import org.junit.Test;

    public class SquareTest {
	
        private Square square;

        @Before	
        public void setUp() throws Exception {
        	this.square = new Square();
        }

        @After
        public void tearDown() throws Exception {
            this.square = null;
        }

        @Test
        public void testInitialSquareState() throws Exception {
            assertEquals(Square.SquareState.COVERED, this.square.getState());
        }
	
        @Test
        public void testUncoverCoveredSquare() throws Exception {
            this.square.uncover();
            assertEquals(Square.SquareState.UNCOVERED, this.square.getState());
        }

        @Test
        public void testUncoverUncoveredSquare() throws Exception {
            this.square.uncover();
            this.square.uncover();
            assertEquals(Square.SquareState.UNCOVERED, this.square.getState());
        }
	
        @Test
        public void testMarkCoveredSquare() throws Exception {
            this.square.mark();
            assertEquals(Square.SquareState.MARKED, this.square.getState());
        }
	
        @Test
        public void testMarkUncoveredSquare() throws Exception {
            this.square.uncover();
            this.square.mark();
            assertEquals(Square.SquareState.UNCOVERED, this.square.getState());
        }
	
        @Test
        public void testUncoverMarkedSquareWhichIsNotAMine() throws Exception {
            this.square.mark();
            this.square.uncover();		
            assertEquals(Square.SquareState.MARKED, this.square.getState());
        }
	
        @Test
        public void testUncoverMarkedSquareWhichIsAAMine() throws Exception {
            this.square.setMine(true);
            this.square.mark();
            this.square.uncover();		
            assertEquals(Square.SquareState.MARKED, this.square.getState());
        }
	
        @Test
        public void testMarkMarkedSquare() throws Exception {
            this.square.mark();
            this.square.mark();
            assertEquals(Square.SquareState.COVERED, this.square.getState());
        }
	
        @Test(expected=UncoveredMineException.class)
        public void testUncoverMine() throws Exception {
            this.square.setMine(true);
            this.square.uncover();
        }
	
    }


**_Code Sample 1_**