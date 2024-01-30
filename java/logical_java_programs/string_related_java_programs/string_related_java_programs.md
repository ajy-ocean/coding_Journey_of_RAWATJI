# String Related Java Programs

* [Write a Java Program to reverse a string without using String inbuilt function](#1-write-a-java-program-to-reverse-a-string-without-using-string-inbuilt-function)
* [Write a Java Program to reverse a string without using String inbuilt function reverse()](#2-write-a-java-program-to-reverse-a-string-without-using-string-inbuilt-function-reverse)
* [Write a Java Program to find whether a string is palindrome or not](#3-write-a-java-program-to-find-whether-a-string-is-palindrome-or-not)
* [Write a Java Program to find the duplicate words in a string](#4-write-a-java-program-to-find-the-duplicate-words-in-a-string)
* [Write a Java Program to find the duplicate characters in a string](#5-write-a-java-program-to-find-the-duplicate-characters-in-a-string)
* [Write a Java Program to remove all white spaces from a string with using replace()](#6-write-a-java-program-to-remove-all-white-spaces-from-a-string-with-using-replace)
* [Write a Java Program to remove all white spaces from a string without using replace()](#7-write-a-java-program-to-remove-all-white-spaces-from-a-string-without-using-replace)

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