# Collections Related Java Programs
	
* [List Related Programs](#list-related-programs)
    * [Write a Java Program to iterate ArrayList using for-loop, while-loop, and advance for-loop](#1-write-a-java-program-to-iterate-arraylist-using-for-loop-while-loop-and-advance-for-loop)
* [Map Related Programs](#map-related-programs)
    * [Write a Java Program to count the number of words in a string using HashMap](#1-write-a-java-program-to-count-the-number-of-words-in-a-string-using-hashmap)
    * [Write a Java Program to iterate HashMap using While and advance for loop](#2-write-a-java-program-to-iterate-hashmap-using-while-and-advance-for-loop)


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