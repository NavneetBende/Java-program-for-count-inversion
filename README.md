Java program to count inversion
Here, in this page we will discuss the program to find the count inversion in Java .Inversion Count: For an array, inversion count indicates how far (or close) the array is from being sorted. If array is already sorted then the inversion count is 0. If an array is sorted in the reverse order then the inversion count is the maximum. 
Formally, two elements a[i] and a[j] form an inversion if a[i] > a[j] and i < j.
We are given with an array of integers and need to find the Inversion Count in the array.

Input: arr[] = {8, 4, 2, 1}
Output: 6
Explanation: Given array has six inversions: (8, 4), (4, 2), (8, 2), (8, 1), (4, 1), (2, 1).

Java program to count inversion
Algorithm :
Traverse the array from beginning to end
Using another loop, find the count of elements smaller
Than the current number up to that index for each element.
Add up the number of inversions for each index.
Count the number of inversions.
Java program to count inversion
Run
public
class Main {
    static int arr[] = new int[]{1, 6, 4, 5};
    static int getInvCount(int n) {
        int inv_count = 0;
        for (int i = 0; i < n - 1; i++)
            for (int j = i + 1; j < n; j++) if (arr[i] > arr[j]) inv_count++;
        return inv_count;
    }
    // Driver method to test the above function
    public
    static void main(String[] args) {
        System.out.println("Number of inversions are " + getInvCount(arr.length));
    }
}
Number of inversions are 2
Note
Time Complexity: O(n^2),Space Complexity:O(1)
Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Find the Union and Intersection of the two sorted arrays

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2 (Merge sort)
The concept is similar to merge sort in that each step divides the array into two equal or nearly equal halves until the base case is reached.
Create a function merge that counts the number of inversions that occur when two halves of an array are merged, and two indices I and j, where I is the index for the first half and j is an index for the second half. There are (mid – I inversions if a[i] is greater than a[j]. Because the left and right subarrays are sorted, all of the remaining elements in the left subarray (a[i+1], a[i+2],… a[mid]) are greater than a[j].
Make a recursive function that divides the array into halves and returns the answer by adding the number of inversions in the first half.
The number of inversion in the second half and the number of inversions by merging the two.
The base case of recursion is when there is only one element in the given half.
Print the answer
Run
import java.util.Arrays;
public class Main
{
 private static int mergeAndCount(int[] arr, int l, int m, int r)
    {
        // Left subarray
        int[] left = Arrays.copyOfRange(arr, l, m + 1);
        // Right subarray
        int[] right = Arrays.copyOfRange(arr, m + 1, r + 1);

        int i = 0, j = 0, k = l, swaps = 0;

        while (i < left.length && j < right.length) {
            if (left[i] <= right[j])
                arr[k++] = left[i++];
            else {
                arr[k++] = right[j++];
                swaps += (m + 1) - (l + i);
            }
        }
        while (i < left.length)
            arr[k++] = left[i++];
        while (j < right.length)
            arr[k++] = right[j++];
        return swaps;
    }

    // Merge sort function
    private static int mergeSortAndCount(int[] arr, int l, int r)
    {
        int count = 0;
        if (l < r) {
            int m = (l + r) / 2;

            // Total inversion count = left subarray count
            // + right subarray count + merge count

            // Left subarray count
            count += mergeSortAndCount(arr, l, m);
            // Right subarray count
            count += mergeSortAndCount(arr, m + 1, r);
            // Merge count
            count += mergeAndCount(arr, l, m, r);
        }

        return count;
    }


    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 1, 20, 6, 4, 5 };
        System.out.println(
            mergeSortAndCount(arr, 0, arr.length - 1));
    }
}
5
