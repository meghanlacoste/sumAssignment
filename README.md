# sumAssignment
package com.company;

import java.util.*;
import java.io.*;
public class Main {

    private static final int MAX= 100;



    public static int getClosestValue(int[][] numbers) {
        int minValue = Math.abs(numbers[0][0]);

        for (int j = 0; j < numbers.length; j++) {

            for (int i = 0; i < numbers[j].length; i++) {

                if ( Math.abs(numbers[j][i]) < minValue ) {
                    minValue = numbers[j][i];
                }
            }
        }
        return minValue ;
    }

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


        // let n represent the dimensions of the square matrix (n x n)
        int n = 0;
        //int row = 0;

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
                    if (i == 0) {

                        n = scanUserFile.nextInt();

                        arr_ = new int[n][n];

                    } else {

                        for (int row = 0; row < n; row++) {

                            for (int column = i - 1; column < n; column++)

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

            System.out.println("Original Matrix");


            int itemsOnLine = 0;
            for (int i = 0; i< n; i++) {

                for (int j= 0; j < n; j++) {
                    itemsOnLine++;
                    // System.out.print ("i:" + i + " j:" + j + " " + arr_[i][j]);
                    System.out.print(arr_[i][j] + " ");
                    if (itemsOnLine==5){
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

/*
 int sum =0;
        int arr_sum [][]= new int [n-1][n-1];


        // creates new array that:
        //stores the closest sum to zero in the first column [n][0]
        // stores the index row of the starting position in [n][1]
        //stores the index column of the starting position in [n][2]
        // stores the dimensions of the submatrix in [n][3]

        System.out.println("==================================================================================\n");

        int arr_closest [][] = new int [n][3];

 */

        System.out.println("\n==================================================================================\n");


        //for (int sideLength = 5; sideLength >= 2; sideLength --){
            int sum =0;
            int counter=0;
            int arr_sum [][]= new int [n-1][n-1];

            int arr_closest [][] = new int [n][1];

        for (int side = n-1; side >= 2; side --) {

            for (int r = 0 ; r <= n-side; r ++){

                for (int c = 0; c <= n-side; c ++){

                        //sum =  arr_[r][c];
                    sum =0;

                        for (int m = 0; m < side ; m++ ){

                            for (int x = 0; x < side; x ++){

                             //   System.out.println(" m:" + m + " x: " + x + " " +  arr_[r+m][c+x] );
                                sum += arr_[r+m][c+x];

                            }
                          //  System.out.println( "sum " + sum);
                           // sum += arr_[r][c+m] + arr_[r+m][c] + arr_[r+m][c+m];
                           // System.out.println("m " + m + " sum " + sum);

                        }

                    //System.out.println("side length " + side + " r:" + r + " c:"+  c + " sum:" + sum);

                    arr_sum[r][c] = sum;


                    }


                }

            }


        for (int i = 0; i < n-1; i++){
           for (int j = 0; j < n-1; j++){

               if (arr_sum[i][j] == getClosestValue(arr_sum)){

                   //Sum: 1, Position: [0:0] Sub-Array: [ 42 32 -73 0 ]
                   System.out.print( "Sum :" + getClosestValue(arr_sum) + "  Position [" + i + " : " + j + "] Sub-Array: [ " );

                   for (int side = n-1; side >= 2; side --) {

                            sum = 0;

                               for (int m = 0; m < side; m++) {

                                   for (int x = 0; x < side; x++) {

                                       //   System.out.println(" m:" + m + " x: " + x + " " +  arr_[r+m][c+x] );
                                       sum += arr_[i + m][j + x];

                                   }

                                   if (sum == getClosestValue(arr_sum)) {
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

                           System.out.print("]");
                       }
                   }

            }

            System.out.print("\n\n-------------------------------------------------------------\n");



            // NEXT STEP: FIND A WAY HOW TO TRACK THE SIDE LENGTH OF THE SUB ARRAYS.




        }// end main method
        }// end main class
