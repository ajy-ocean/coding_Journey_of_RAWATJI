# Numbers Related Java Programs

### Index
* [Write a Java Program to reverse a number](#1-write-a-java-program-to-reverse-a-number)
* [Write a Java Program to swap two numbers using the third variable](#2-write-a-java-program-to-swap-two-numbers-using-the-third-variable)
* [Write a Java Program to swap two numbers without using the third variable](#3-write-a-java-program-to-swap-two-numbers-without-using-the-third-variable)
* [Write a Java Program to find whether a number is prime or not](#4-write-a-java-program-to-find-whether-a-number-is-prime-or-not)
* [Write a Java Program to find whether a number is palindrome or not](#5-write-a-java-program-to-find-whether-a-number-is-palindrome-or-not)
* [Write a Java Program for the Fibonacci series](#6-write-a-java-program-for-the-fibonacci-series)
* [Write a Java Program to find the Largest, second-largest, smallest & second-smallest number in an array](#7-write-a-java-program-to-find-the-largest-second-largest-smallest--second-smallest-number-in-an-array)
* [Write a Java Program to find whether a number is Armstrong or not](#8-write-a-java-program-to-find-whether-a-number-is-armstrong-or-not)


#### 1. Write a Java Program to reverse a number.

* Method 1

```java

package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter a number:- ");
		int number = scanner.nextInt();
		StringBuilder str = new StringBuilder();
		str.append(number);
		str.reverse();
		Integer reverseNumber = Integer.parseInt(str.toString());
		/*  
			You can perform all the actions in one line like this....
			int reverseNumber = Integer.parseInt(stringBuilder.append(number).reverse().toString());
		*/
		System.out.println("Reverse:- " + reverseNumber);
	}
}
```
* Method 2

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter a number:- ");
		int number = scanner.nextInt();
		
		System.out.println("Before:- " + number);
		int remainder;
		int reverse = 0;
		while(number != 0) {
			remainder = number % 10;
			reverse = (reverse * 10) + remainder;
			number = number / 10;
		}
		System.out.println("After:- " + reverse);
	}
}
```


#### 2. Write a Java Program to swap two numbers using the third variable.

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter First Number:- ");
		int firstNumber = scanner.nextInt();
		System.out.print("Enter Second Number:- ");
		int secondNumber = scanner.nextInt();
		System.out.println("Before swapping the numbers:- " + " First Number = " + firstNumber + " Second Number = " + secondNumber);

		int temp = firstNumber;
		firstNumber = secondNumber;
		secondNumber = temp;

		System.out.println("After swapping the numbers:- " + " First Number = " + firstNumber + " Second Number = " + secondNumber);
	}
}
```

#### 3. Write a Java Program to swap two numbers without using the third variable.

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter First Number:- ");
		int firstNumber = scanner.nextInt();
		System.out.print("Enter Second Number:- ");
		int secondNumber = scanner.nextInt();
		System.out.println("Before swapping the numbers:- " + " First Number = " + firstNumber + " Second Number = " + secondNumber);

		// firstNumber now contains the total of firstNumber & secondNumber
		firstNumber = firstNumber + secondNumber;

		/*
		 * Here we have subtracted the secondNumber from firstNumber i.e (firstNumber +
		 * secondNumber) Since firstNumber contains the total value so if we subtract
		 * secondNumber from the total value we will get firstNumber
		 */
		secondNumber = firstNumber - secondNumber;

		/*
		 * Here we want the value of secondNumber in firstNumber so to get the value of
		 * secondNumber We need to subtract the value of firstNumber from total Since
		 * firstNumber contains the total value and secondNumber contains the
		 * firstNumber value So we subtract secondNumber from firstNumber
		 */
		firstNumber = firstNumber - secondNumber;

		System.out.println("After swapping the numbers:- " + " First Number = " + firstNumber + " Second Number = " + secondNumber);
	}
}
```

#### 4. Write a Java Program to find whether a number is prime or not.

* Method 1

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter a number to check if it is a prime number or not");
		int number = scanner.nextInt();
		int counter = 0;
		for(int i = 1; i <= number; i++) {
			if(number % i == 0) {
				counter++;
			}
		}
		if(counter == 2) {
			System.out.println(number + " is a PRIME NUMBER");
		}else {
			System.out.println(number + " is a NOT PRIME NUMBER");
		}
	}
}
```

* Method 2

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		int temp, num;
        boolean isPrime = true;
        System.out.println("Enter a number");
        Scanner in = new Scanner(System.in);
        num = in.nextInt();
        in.close();
        for (int i = 2; i <= num/2; i++) {
            temp = num%i;
            if (temp == 0) {
                isPrime = false;
                break;
            }
        }
        if(isPrime) 
            System.out.println(num + " number is prime");
            else
                System.out.println(num + " number is not a prime");
             
	}
}
```

#### 5. Write a Java Program to find whether a number is palindrome or not.

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter a number to check if it is a palindrome or not");
		String userInput = scanner.nextLine();
		System.out.println("Original Number:- " + userInput);

		int reverseNumber = Integer.parseInt(new StringBuilder().append(userInput).reverse().toString());
		System.out.println("Reverse Number:- " + reverseNumber);

		if (Integer.parseInt(userInput) == reverseNumber) {
			System.out.println(userInput + " is a PALINDROME NUMBER");
		} else {
			System.out.println(userInput + " is NOT a PALINDROME NUMBER");
		}
	}
}
```

#### 6. Write a Java Program for the Fibonacci series.

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		// 0 1 1 2 3 5 8 13.......
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter the range to calculate FIBONACCI SERIES:-");
		int rangeOfFibonaccci = scanner.nextInt();

		int firstTerm = 0;
		int secondTerm = 1;
		for (int i = 1; i <= rangeOfFibonaccci; i++) {
			System.out.print(firstTerm + " ");
			int sumOfTerms = firstTerm + secondTerm;
			firstTerm = secondTerm;
			secondTerm = sumOfTerms;
		}
	}
}
```

#### 7. Write a Java Program to find the Largest, second-largest, smallest & second-smallest number in an array.

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		System.out.println("Enter any 5 numbers");
		Scanner scanner = new Scanner(System.in);
		int[] numbers = new int[5];

		for (int i = 0; i < numbers.length; i++) {
			numbers[i] = scanner.nextInt();
		}

		System.out.print("The given numbers are:- ");
		for (int getNumbers : numbers) {
			System.out.print(getNumbers + " ");
		}

		System.out.println();

		/* Largest & Second Largest */
		int largest = Integer.MIN_VALUE;
		int secondLargest = Integer.MIN_VALUE;
		for (int i = 0; i < numbers.length; i++) {
			if (numbers[i] > largest) {
				secondLargest = largest;
				largest = numbers[i];
			} else if (numbers[i] > secondLargest) {
				secondLargest = numbers[i];
			}
		}

		System.out.println("The Largest Number in the given array is:- " + largest);
		System.out.println("The Second Largest Number in the given array is:- " + secondLargest);

		System.out.println("=======================================================");

		/* Smallest & Second Smallest */
		int smallest = Integer.MAX_VALUE;
		int secondSmallest = Integer.MAX_VALUE;
		for (int i = 0; i < numbers.length; i++) {
			if (numbers[i] < smallest) {
				secondSmallest = smallest;
				smallest = numbers[i];
			} else if (numbers[i] < secondSmallest && numbers[i] != smallest) {
				secondSmallest = numbers[i];
			}
		}

		System.out.println("The Smallest Number in the given array is:- " + smallest);
		System.out.println("The Second Smallest Number in the given array is:- " + secondSmallest);
	}
}
```

#### 8. Write a Java Program to find whether a number is Armstrong or not.

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter a number to check if it is an ARMSTRONG NUMBER OR NOT");
		int number = scanner.nextInt();
		int temp = number;

		int remainder;
		int armstrong = 0;
		while (number != 0) {
			// Remainder
			remainder = number % 10;
			// Logic for armstrong
			armstrong = (remainder * remainder * remainder) + armstrong;
			// divide
			number = number / 10;
		}
		
		if(armstrong == temp) {
			System.out.println(temp + " is an ARMSTRONG NUMBER");
		}else {
			System.out.println(temp + " is NOT an ARMSTRONG NUMBER");
		}
	}
}
```