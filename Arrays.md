# Arrays Example Programs

## 1. Linear Search (Find Index of Element)
```java
class LinearSearch {
    public static int search(int[] arr, int x) {
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == x) {
                return i;
            }
        }
        return -1;  // not found
    }
}
```

## 2. Largest Element in Array
```java
class LargestElement {
    public static int largest(int[] arr) {
        int max = arr[0];
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        return max;
    }
}
```

## 3. Reverse an Array (Two-pointer method)
```java
class ReverseArray {
    public static void reverse(int[] arr) {
        for (int i = 0; i < arr.length / 2; i++) {
            int temp = arr[i];
            arr[i] = arr[arr.length - 1 - i];
            arr[arr.length - 1 - i] = temp;
        }
    }
}
```

## 4. Check If Array Is Sorted (Ascending)
```java
class CheckSorted {
    public static boolean isSorted(int[] arr) {
        for (int i = 0; i < arr.length - 1; i++) {
            if (arr[i] > arr[i + 1]) {
                return false;
            }
        }
        return true;
    }
}
```

## 5. Reverse Array — Using While Loop (Alternative Logic)
```java
class ReverseArray2 {
    public static void reverse(int[] arr) {
        int start = 0;
        int end = arr.length - 1;

        while (start < end) {
            int temp = arr[start];
            arr[start] = arr[end];
            arr[end] = temp;
            start++;
            end--;
        }
    }
}
```
# Java Array Programs – Collection

This repository contains various basic Java programs related to arrays, including:
- Print array
- Sum, average
- Positive / Negative / Zero count
- Even / Odd count
- Max / Min value and index
- Print all numbers greater than k

---

# <span style="color:#00bfff;">Java Array Programs – Full Collection</span>

This repository contains various useful Java programs related to arrays.

---

## <span style="color:#ff6600;">1. Print Array + Count Positive/Negative/Zero + Even/Odd</span>

```java
import java.util.Scanner;

public class ara1 {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        int size = sc.nextInt();
        int[] arr = new int[size];

        for(int i = 0; i < size; i++){
            arr[i] = sc.nextInt();
        }

        for(int i = 0; i < size; i++){
            System.out.print(arr[i] + " ");
        }
        System.out.println();

        int pos = 0, neg = 0, zero = 0;
        for(int i = 0; i < size; i++){
            if(arr[i] > 0) pos++;
            else if(arr[i] < 0) neg++;
            else zero++;
        }

        System.out.println("Positive: " + pos);
        System.out.println("Negative: " + neg);
        System.out.println("Zero: " + zero);

        int even = 0, odd = 0;
        for(int i = 0; i < size; i++){
            if(arr[i] % 2 == 0) even++;
            else odd++;
        }

        System.out.println("Even: " + even);
        System.out.println("Odd: " + odd);
    }
}
```
## <span style="color:#ff3399;">2. Count Positive, Negative, Zero</span>
```java
import java.util.Scanner;

public class CountNumbers {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        int size = sc.nextInt();
        int[] arr = new int[size];

        for(int i = 0; i < size; i++){
            arr[i] = sc.nextInt();
        }

        int pos = 0, neg = 0, zero = 0;

        for(int i = 0; i < size; i++){
            if(arr[i] > 0) pos++;
            else if(arr[i] < 0) neg++;
            else zero++;
        }

        System.out.println("Positive count: " + pos);
        System.out.println("Negative count: " + neg);
        System.out.println("Zero count: " + zero);
    }
}
```
## <span style="color:#33cc33;">3. Minimum Value in Array</span>
```java
import java.util.Scanner;

public class MinValue {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        int size = sc.nextInt();
        int[] arr = new int[size];

        for(int i = 0; i < size; i++){
            arr[i] = sc.nextInt();
        }

        int min = arr[0];

        for(int i = 0; i < size; i++){
            if(arr[i] < min){
                min = arr[i];
            }
        }

        System.out.println("Minimum: " + min);
    }
}
```
## <span style="color:#cc00ff;">4. Average of Array</span>
```java
import java.util.Scanner;

public class Average {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        int size = sc.nextInt();
        int[] arr = new int[size];
        double sum = 0;

        for(int i = 0; i < size; i++){
            arr[i] = sc.nextInt();
        }

        for(int i = 0; i < size; i++){
            sum += arr[i];
        }

        double avg = sum / size;
        System.out.println("Average: " + avg);
    }
}
```
## <span style="color:#ff0000;">5. Print Array + Sum</span>
```java
import java.util.Scanner;

public class PrintAndSum {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        int size = sc.nextInt();
        int[] arr = new int[size];
        int sum = 0;

        for(int i = 0; i < size; i++){
            arr[i] = sc.nextInt();
        }

        for(int i = 0; i < size; i++){
            System.out.print(arr[i] + " ");
        }

        for(int i = 0; i < size; i++){
            sum += arr[i];
        }

        System.out.println("\nSum: " + sum);
    }
}
```
## <span style="color:#0099ff;">6. Index of Max & Min Element</span>
```java
import java.util.Scanner;

public class IndexOfMinMax {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        int size = sc.nextInt();
        int[] arr = new int[size];

        for(int i = 0; i < size; i++){
            arr[i] = sc.nextInt();
        }

        int min = arr[0], max = arr[0];
        int minIndex = 0, maxIndex = 0;

        for(int i = 0; i < size; i++){
            if(arr[i] > max){
                max = arr[i];
                maxIndex = i;
            }
            if(arr[i] < min){
                min = arr[i];
                minIndex = i;
            }
        }

        System.out.println("Max: " + max + " Index: " + maxIndex);
        System.out.println("Min: " + min + " Index: " + minIndex);
    }
}
```
## <span style="color:#ffaa00;">7. Print All Numbers Greater Than K</span>
```java
import java.util.Scanner;

public class GreaterThanK {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        int size = sc.nextInt();
        int[] arr = new int[size];

        for(int i = 0; i < size; i++){
            arr[i] = sc.nextInt();
        }

        int k = sc.nextInt();
        System.out.print("Greater Than K value : ");

        for(int i = 0; i < size; i++){
            if(arr[i] > k){
                System.out.print(arr[i] + " ");
            }
        }
    }
}


```
