# Java Programs

* [Number Related Programs](#number-related-programs)
* [String Related Programs](#string-relatd-programs)
* Collection Framework Related
	* [List Related Programs](#list-related-programs)
	* [Map Related Programs](#map-related-programs)

### Number Related Programs

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

---
---

### String Relatd Programs

#### 1. Write a Java Program to reverse a string without using String inbuilt function. 

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter your name:- ");
		String name = scanner.nextLine();
		StringBuilder strBd = new StringBuilder();
		strBd.append(name);
		strBd.reverse();
		System.out.print("Reverse:- " + strBd);

		/*
		 * You can do all this in a single line like this
		 * StringBuilder stringBuilder = new StringBuilder();
		 * System.out.println("Reverse:- " + stringBuilder.append(name).reverse());
		 */
		
		/*
		 * If you need to store it in a string variable
		 * String reverseName = stringBuilder.append(name).reverse().toString();
		 * System.out.println("Reverse:- " + reverseName);
		 */		
	}
}
```

#### 2. Write a Java Program to reverse a string without using String inbuilt function reverse().

* Method 1

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter the string to be reversed (Befor Reverse)");
		String beforeReverse = scanner.nextLine();
		int lastIndex = beforeReverse.length() - 1;
		String afterReverse = "";
		for (int i = lastIndex; i >= 0; i--) {
			afterReverse = afterReverse + beforeReverse.charAt(i);
			// We can write the above line as this also
			/* afterReverse += beforeReverse.charAt(i); */
		}
		System.out.println("String after reversed");
		System.out.println(afterReverse);

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
		System.out.print("Enter your name:- ");
		String name = scanner.nextLine();
		char[] nameCharArray = name.toCharArray();
		int lastIndex = nameCharArray.length - 1;
		for (int i = lastIndex; i >= 0; i--) {
			System.out.print(nameCharArray[i]);
		}
	}
}
```

* Method 3

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.print("Enter your name:- ");
		String name = scanner.nextLine();
		String[] nameStringArray = name.split("");
		int lastIndex = nameStringArray.length - 1;
		for(int i = lastIndex; i >= 0; i--) {
			System.out.print(nameStringArray[i]);
		}
	}
}
```

#### 3. Write a Java Program to find whether a string is palindrome or not.

```java
package practice;

import java.util.Scanner;

public class RandomPractice {

	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("Enter a word to check if it is a palindrome or not");
		String word = scanner.nextLine();

		String reverse = "";
		int lastIndex = word.length() - 1;
		for (int i = lastIndex; i >= 0; i--) {
			reverse += word.charAt(i);
		}
		
		System.out.println("The given word:- " + word);
		System.out.println("The reverse word:- " + reverse);

		if (word.equals(reverse)) {
			System.out.println("The given word is a PALINDROME WORD");
		}
		else {
			System.out.println("The given word is NOT a PALINDROME WORKD");
		}
	}
}
```

#### 4. Write a Java Program to find the duplicate words in a string.

```java
package practice;

import java.util.HashMap;

public class RandomPractice {

	public static void main(String[] args) {
		String str = "Frank Ocean is the best singer My Favourite Frank Ocean album is Blonde";
		String[] arrayOfString = str.split(" ");

		HashMap<String, Integer> map = new HashMap<String, Integer>();
		for (int i = 0; i < arrayOfString.length; i++) {
			if (map.containsKey(arrayOfString[i])) {
				int count = map.get(arrayOfString[i]);
				map.put(arrayOfString[i], count + 1);
			} else {
				map.put(arrayOfString[i], 1);
			}
		}
		System.out.println(map);
		
		// Duplicate values logic
		for (String key : map.keySet()) {
			if (map.get(key) > 1) {
				System.out.println("Duplicate value: " + key + " = " + map.get(key));
			}
		}
	}
}
```

#### 5. Write a Java Program to find the duplicate characters in a string.

```java
package practice;

public class RandomPractice {

	public static void main(String[] args) {
		String word = "Automation";
		char[] charArrayOfWords = word.toCharArray();
		int count = 0;

		for (int i = 0; i < word.length(); i++) {
			for (int j = i + 1; j < word.length(); j++) {
				if (charArrayOfWords[i] == charArrayOfWords[j]) {
					System.out.println("Duplicate character:- " + charArrayOfWords[j]);
					count++;
					break;
				}
			}
		}
		System.out.println("Total Number of Duplicate words:- " + count);
	}
}
```

#### 6. Write a Java Program to remove all white spaces from a string with using replace().

```java
package practice;

public class RandomPractice {

	public static void main(String[] args) {
		String name = "Ajay Rawat";
		System.out.println("Before:- " + name);
		System.out.println("After:- " + name.replaceAll("\\s", ""));
	}
}
```

#### 7. Write a Java Program to remove all white spaces from a string without using replace().

```java
package practice;

public class RandomPractice {

	public static void main(String[] args) {
		String words = "Ajay Rawat This is America";
		System.out.println("Before:- " + words);
		
		char[] charOfWords = words.toCharArray();
		StringBuilder stringBuider = new StringBuilder();
		
		for(int i = 0; i < charOfWords.length; i++) {
			if(charOfWords[i] != ' ' && charOfWords[i] != '\t') {
				stringBuider.append(charOfWords[i]);
			}
		}
		System.out.println("After:- " + stringBuider);
	}
}
```
---
---

## Collection Related

### List Related Programs

#### 1. Write a Java Program to iterate ArrayList using for-loop, while-loop, and advance for-loop.

```java
package practice;

import java.util.ArrayList;
import java.util.Iterator;

public class RandomPractice {

	public static void main(String[] args) {
		ArrayList<Integer> arrayList = new ArrayList<Integer>();
		arrayList.add(10);
		arrayList.add(20);
		arrayList.add(30);
		System.out.println("ArrayList size:- " + arrayList.size());
		
		System.out.println("Traversing ArrayList Using While Loop");
		System.out.println("==============================");
		Iterator itr = arrayList.iterator();
		while(itr.hasNext()) {
			System.out.println(itr.next());
		}
		
		System.out.println("Traversing ArrayList Using For Each Loop");
		System.out.println("==============================");
		for(Integer list : arrayList) {
			System.out.println(list);
		}
		
		System.out.println("Traversing ArrayList Using For Loop");
		System.out.println("==============================");
		for(int i = 0; i < arrayList.size(); i++) {
			System.out.println(arrayList.get(i));
		}
	}
}
```

### Map Related Programs

#### 1. Write a Java Program to count the number of words in a string using HashMap.

```java
package practice;

import java.util.HashMap;

public class RandomPractice {

	public static void main(String[] args) {
		String str = "This is done by Ajay Ajay is a Java Developer and this is his work";
		String[] arrayOfString = str.split(" ");

		HashMap<String, Integer> map = new HashMap<String, Integer>();
		for (int i = 0; i < arrayOfString.length; i++) {
			if (map.containsKey(arrayOfString[i])) {
				int count = map.get(arrayOfString[i]);
				map.put(arrayOfString[i], count + 1);
			} else {
				map.put(arrayOfString[i], 1)	;
			}
		}
		System.out.println(map);
	}
}
```

#### 2. Write a Java Program to iterate HashMap using While and advance for loop.

```java
package practice;

import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class RandomPractice {

	public static void main(String[] args) {

		HashMap<Integer, String> hm = new HashMap<Integer, String>();
		hm.put(1, "Ajay");
		hm.put(2, "NilKant");
		hm.put(3, "Panchi");
		hm.put(4, "Arjun idli");
		System.out.println("HashMap Size:- " + hm.size());

		System.out.println("While loop:- ");
		System.out.println("===============");
		Iterator itr = hm.entrySet().iterator();
		while (itr.hasNext()) {
			Map.Entry mapEntry = (Map.Entry) itr.next();
			System.out.println("Key:- " + mapEntry.getKey() + " Value:- " + mapEntry.getValue());
		}
		
		System.out.println("For Each loop");
		System.out.println("==============");
		for(Map.Entry mapEntry : hm.entrySet()) {
			System.out.println("Key:- " + mapEntry.getKey() + " Value:- " + mapEntry.getValue());
		}
	}
}
```

