# sumAssignment
package com.company;

import java.util.*;
import java.io.*;
public class Main {

    private static final int MAX= 100;

    public static void main(String[] args) {
	// write your code here
        // find the smallest square subarray with a su as close to " " as possible
        //the smallest sub array to be considered is 2x2
        // File Format (each line)
        //<# rows/columns> <value>... <value>
        //ie. 2 -5 4 3 -3



        String userFileName = "matrix.txt";
        int someInteger = 0;
        int arr_[][] = null;


        //display sum, starting position and sub array to screen

        //System.out.println("");
       // System.out.println("Please type in the file name\n");

        // create a variable s of type scanner to process input from "System.in"
       // Scanner scanSystemIn = new Scanner(System.in);

        // Use the Scanner "s" to get the "next" input from "System.in"
       // userFileName = scanSystemIn.next();

        // Display the user input now stored in "userInput"
      //  System.out.println("\nThe user input: " + userFileName);


        // ---------------------------------------------
        // This is where we "try" to process the file
        //

        int bound = 0;
        int row = 0;

        try {
            // --------------------------------
            // create file, and scanner objects
            // - file object is called tempfilenums.txt and is in your project directory
            //   that is the same folder as the iml file
            //

            File userFile = new File(userFileName);
            Scanner scanUserFile = new Scanner(userFile);

            // ---------------------------------------------
            // Reads in values from the file in a for loop
            //

            for (int i = 0; i < MAX; i++) {
                if (i == 0 && scanUserFile.hasNextInt()) {
                    bound = scanUserFile.nextInt();

                    arr_ = new int[bound][bound];


                    for(int indx =0; indx < MAX; indx ++) {


                        // ---------------------------------------------
                        // The scanner checks if there is another integer and prints it
                        // if there is
                        //

                        if (scanUserFile.hasNext()) {
                            someInteger = scanUserFile.nextInt();
                            if (indx>5) {
                                indx = 0;
                                row +=1;
                                arr_[indx][row] = someInteger;
                            }

                            System.out.print(" " + someInteger);

                        } else {
                            // ---------------------------------------------
                            // The scanner detected no other integers
                            // - closes the scanner for the file
                            // - breaks out of the for loop
                            //
                            System.out.print("\n\nDataFileFILE has been completely READ");
                            scanUserFile.close();

                            // A break statement allows us to exit the loop before we have reach the end
                            break;
                        }
                    }



                } }




            System.out.println();
            for (int i = 0; i< bound; i++) {
                for (int j= 0; j < bound; j++) {
                    System.out.print ("i:" + i + " j:" + j + " " + arr_[i][j]);
                    System.out.println();
                }

            }


            // ---------------------------------------------
            // If the file cannot be found then an exception (error) is generated (thrown) that we have to
            // deal with (catch).
            // - we print "e" the exception, and
            // - show the user where it was using the "exceptions" stack trace information
            //

        } catch (FileNotFoundException e) {
            System.out.println(e);
            e.printStackTrace();
        }





























    }// end main method
}// end main class
