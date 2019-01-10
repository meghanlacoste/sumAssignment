# sumAssignment
package com.company;

import java.util.*;
import java.io.*;
public class Main {


    // maximum numbers stored in the array
    private static final int MAX= 500;
    private static final int INVALID = -100;


    // this function compares the numbers stored in a 2d array and returns the
    // the absolute value closest to zero

    /*
    public static int getClosestValue(int[][] numbers) {

        // creates a new int variable minValue with the value of the
        // initial value of the array
        int minValue = Math.abs(numbers[0][0]);

        // loops over all indexes in the int array
        for (int j = 0; j < numbers.length; j++) {

            for (int i = 0; i < numbers[j].length; i++) {

                // if the absolute value stored is less than the current minValue
                // then that becomes the new minValue
                if ( Math.abs(numbers[j][i]) < minValue ) {
                    minValue = numbers[j][i];
                }
            }
        }
        return minValue ;
    }
     */

    public static int getClosestValue(int[] numbers) {

        // creates a new int variable minValue with the value of the
        // initial value of the array
        int minValue = Math.abs(numbers[0]);

        // loops over all indexes in the int array
        for (int i = 0; i < numbers.length; i++) {

                if ( Math.abs(numbers[i]) < minValue ) {
                    minValue = numbers[i];
                }
            }

        return minValue ;
    }



    public static void main(String[] args) {

        //----------------------------------------------------------------------------------------------------
        // Requirements:
        // find the smallest square sub-array with a sum as close to 0 as possible
        //the smallest sub array to be considered is 2x2
        // File Format (each line)
        //<# rows/columns> <value>... <value>
        //ie. 2 -5 4 3 -3
        //display sum, starting position and sub array to screen
        //----------------------------------------------------------------------------------------------------


        //DECLARE/ INITIALIZE VARIABLES
        String userFileName;
        int someInteger = 0;
        int arr_[][] = null;
        boolean exit = false;

        // Loops through the process so long that the user has not selected exit
        while (!exit){

            System.out.println("");
            System.out.println("Please type in the file name\n");

            //create a variable s of type scanner to process input from "System.in"
            Scanner scanSystemIn = new Scanner(System.in);

            // Use the Scanner "s" to get the "next" input from "System.in"
            userFileName = scanSystemIn.next();

            // Display the user input now stored in "userInput"
            System.out.println("\nThe user input: " + userFileName);


            // ---------------------------------------------
            //  "try" to process the file
            //


            // let n represent the dimensions of the square matrix (n x n)
            int n = 0;


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
                    if (scanUserFile.hasNextInt()) {

                        // sets 'n' - the dimensions of the 2D array to be the first value in the file
                        if (i == 0) {

                            n = scanUserFile.nextInt();

                            arr_ = new int[n][n];

                        } else {

                            // stores the values in the file in the 2D array

                            for (int row = 0; row < n; row++) {

                                for (int column = 0; column < n; column++)

                                    arr_[row][column] = scanUserFile.nextInt();
                            }
                        }

                    }


                    else {
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


                System.out.println("\n==================================================================================\n");


                // Prints the original matrix to the screen
                System.out.println("Original Matrix");


                int itemsOnLine = 0;
                for (int i = 0; i< n; i++) {

                    for (int j= 0; j < n; j++) {
                        itemsOnLine++;
                        // System.out.print ("i:" + i + " j:" + j + " " + arr_[i][j]);
                        System.out.print(arr_[i][j] + " ");
                        if (itemsOnLine==n){
                            System.out.println();
                            itemsOnLine =0;
                        }
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



            System.out.println("\n==================================================================================\n");



            int sum;

            // creates a new 2d array which will store the sums of the various subarrays

          //  int arr_sum [][]= new int [n-1][n-1];
            int arr_sum [][]= new int [MAX][4];

            for (int i= 0; i < MAX; i++){
                for (int j=0; j< 4; j++){
                    arr_sum[i][j] = INVALID;
                }
            }

            // the dimensions of the sub-arrays are (side x side)
            // where the side length has to be less than the dimensions of the original matrix 'n'
            // and no less than 2 so that individual elements are not considered

            for (int i=0; i < MAX; i ++){

                for (int side = n-1; side >= 2; side --) {


                    for (int r = 0 ; r <= n-side; r ++){

                        for (int c = 0; c <= n-side; c ++){


                            sum = 0;

                            // for each starting position in the array [ r : c ]
                            // this for-loop adds all the other values that can be contained in each
                            // sub-array;
                            // the
                            for (int m = 0; m < side ; m++ ){

                                for (int x = 0; x < side; x ++){

                                    sum += arr_[r+m][c+x];

                                }

                            }

                            // stores the sum of the sub-array in the same position of the subarray
                            // in the original matrix
                            //arr_sum[r][c] = sum;
                            arr_sum[i][0]= side;
                            arr_sum [i][1] = r;
                            arr_sum [i][2] = c;
                            arr_sum [i][3] = sum;

                        }


                    }

                }
            }



            int temp_array [] = new int [MAX];
            for (int i  = 0; i < MAX; i++){
                if (arr_sum[i][3]!= INVALID) {

                    temp_array[i] = arr_sum[i][3];


                }
            }

            getClosestValue(temp_array);



            for (int i = 0; i < n-1; i++){
                for (int j = 0; j < n-1; j++){

                    if (arr_sum[i][j] == getClosestValue(temp_array)){

                        System.out.print( "Sum: " + getClosestValue(temp_array) + "  Position: [" + i + " : " + j + "] Sub-Array: [ " );

                        for (int side = n-1; side >= 2; side --) {

                            sum = 0;

                            for (int m = 0; m < side; m++) {

                                for (int x = 0; x < side; x++) {

                                    //   System.out.println(" m:" + m + " x: " + x + " " +  arr_[r+m][c+x] );
                                    sum += arr_[i + m][j + x];

                                }

                                if (sum == getClosestValue(temp_array)) {
                                    for (int t = 0; t < side; t++) {

                                        for (int s = 0; s < side; s++) {

                                            //   System.out.println(" m:" + m + " x: " + x + " " +  arr_[r+m][c+x] );
                                            System.out.print(arr_[i + t][j + s] + " ");

                                        }
                                    }
                                    break;
                                }
                            }
                        }

                        System.out.print("]\n");
                    }
                }

            }

            System.out.print("\n\n-------------------------------------------------------------\n");

            String userIn;
            System.out.println("");
            System.out.println("Do you have any more files to process? Enter 'exit' if you are done. To continue, enter any other character \n");

            Scanner scan= new Scanner (System.in);
            userIn  = scan.next();



            if(userIn.equalsIgnoreCase("exit") ) {

                System.out.println("\n\n Process Complete");
                 exit = true;

            }






        }







    }// end main method
        }// end main class
