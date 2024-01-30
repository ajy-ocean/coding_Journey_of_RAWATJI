# Patterns

### Index
* [Pattern Logic](#pattern-logic)
* [Star related Pattern Programs](#star-related-pattern-programs)
* [Number related Pattern Program](#number-related-pattern-program)

### Pattern Logic
![Pattern Program Logic](/java/logical_java_programs/pattern_related_java_programs/img/Pattern_Program_Logic.png)

### Star related Pattern Programs

**StarPattern.java**
```java
package com.practice.pattern;

public class StarPattern {

	public static void main(String[] args) {

		System.out.println("First Star Pattern");
		firstStarPattern(4);

		System.out.println("Second Star Pattern");
		secondStarPattern(5);

		System.out.println("Third Star Pattern");
		thirdStarPattern(5);
	}

	static void firstStarPattern(int n) {
		// Outer for-loop
		for (int row = 1; row <= n; row++) {
			// Inner for-loop
			// for every row, run the col
			for (int col = 1; col <= row; col++) {
				System.out.print("* ");
			}
			// when one row is printed, we need to add a newline
			System.out.println();
		}
	}

	static void secondStarPattern(int n) {
		// Outer for-loop
		for (int row = 1; row <= n; row++) {
			// Inner for-loop
			for (int col = 1; col <= n; col++) {
				System.out.print("*");
			}
			// when one row is printed, we need to add a newline
			System.out.println();
		}
	}

	static void thirdStarPattern(int n) {

		for (int row = 1; row <= n; row++) {
			/*
			 * These two ways you can run this code for col = 1 and col 0
			 */
			// for(int col = 0; col < n-row; col++) {
			// System.out.print("*");
			// }
			for (int col = 1; col <= n - row + 1; col++) {
				System.out.print("*");
			}
			System.out.println("");
		}
	}
}
```

### Number related Pattern Program

**NumberPattern.java**

```java
package com.practice.pattern;

public class NumberPattern {
	
	public static void main(String[] args) {
		System.out.println("First Number Pattern");
		firstNumberPattern(5);
	}
	
	static void firstNumberPattern(int n) {
		for(int row = 1; row <= n; row++) {
			for(int col=1; col <= row; col++) {
				System.out.print(col + " ");
			}
			System.out.println();
		}
	}
}
```