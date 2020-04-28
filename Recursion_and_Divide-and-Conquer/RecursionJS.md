# Recursion Interview Question

A recursive method is a method that will call itself. Recursive methods can be used to repeat a method over and over again until
certain conditions are met and much more. A recursive case is the line of code in which you call the method. 
You must create a working recursive case for these methods in order to make them function as needed.

## Example Problem
  The method below is an incomplete recursive method that has the goal of printing N as even integers between 1-N.  
  
    public static int Rec(int n) {
    if(n==0){
    return 1;
    }
    if(n%2==0){
    System.out.print(n);
    }
    $$$$$
    }
    return 5;
    }
 
  The method is incomplete and is not recursive.
  The recursive case should be added at the $ to satisfy the goal.
  
      if(n<100){
      return Rec(n+1);
      }
  
  This recursive case completes the method by calling itself with N being 1 integer higher than the previous time it called itself.
  The if statement checks too see if N is less than 100. bn 
  
  ## Real Problem
  
 The next problem will be the same concept as the previous but with a more complicated goal.
 The goal of this method is to figure out which of 2 growing variables will reach the variable MaxNum first.
 The line with the $$$$$ indicates where the Recursive case fits in.
 
 This method has 2 int variables you will return in the recursion.
 N grows exponentially by 2 and X grows 35 by each iteration.
  
    public static int Rec2(int n,int x) {
    int MaxNum;
    MaxNum = 400;
    if(n==0){
    return Rec2(1,x);
    }
    if(x==0){
    return Rec2(n,x);
    }
    $$$$$
    if(n>MaxNum||x>MaxNum){
    if(n>x){
    System.out.println("N reached the number first");
    }
    else{
    System.out.println("X reached the number first");
    }
    }
	  return MaxNum;
    }

### __Solution below__
## The Solution

    if(n<MaxNum||x<MaxNum){
    return Rec2(n*2,x+35);
    }
    
   MaxNum is the variable that you are comparing to our N and X variable. 
   You must make a conditional statement that checks if either variable has surpassed MaxNum.
   So if the conditions specify that X or Y have not surpassed the number, you use recursion to return the two variables.
   But each return, you must multiply or add the given number in the instructions in order for X or Y to eventually meet the conditional that will tell us which one reached MaxNum first.
   The given change to X/N each iteration, and MaxNums value could be replaced in this method to figure out the race between any two equations to any number.
   
   All recursive cases must have a conditional. The conditional stops the program from never ending, and endlessly calling itself. 
   It is almost like a loop counter, but you have more freedom. What variables you must use to reach this conition would be given to you
   usually when told the purpose of the method. 
   
   So if you are ever tasked with creating a recursive method, firstly create a conditional that will loop until the goal has been reached. 
   And secondly you must increment you counter / counters in a way where they will eventually meet the wanted condition.
   
   ## Illustration of the Problem
   [logo]: https://github.com/JohnnyShanahan/Geocaris-Home/blob/master/Screenshot_13.png "Logo Title Text 2" 
   ![alt text][logo]
   ## Complexity
   
   
   ## Code implentation
   Recursion can be used for a lot of things. 
   It can be used to create a single method that can reverse the letter structure of a word of any size. 
   It can create methods that compare sets of different numbers over changing amounts of time. It allows you to loop an entire method
   with ever changing variables. It can be very useful in handfuls of programming situiations that require change over certain iterations. 
   
   ## Final Review Question
   
   
   

      
  
