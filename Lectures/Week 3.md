# 1. Sorting Algorithms

## 1.1. Bubble Sort

Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order. This algorithm is not suitable for large data sets as its average and worst-case time complexity is quite high.

```java
// Java program for implementation of Bubble Sort
class BubbleSort {

	void bubbleSort(int arr[]) {
		int n = arr.length;

		for (int i = 0; i < n - 1; i++)
			for (int j = 0; j < n - i - 1; j++)
				if (arr[j] > arr[j + 1]) {
					// swap arr[j+1] and arr[j]
					int temp = arr[j];
					arr[j] = arr[j + 1];
					arr[j + 1] = temp;
				}
	}

	// Prints the array
	void printArray(int arr[]) {
		int n = arr.length;

		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");

		System.out.println();
	}

	// Driver method to test above
	public static void main(String args[]) {
		BubbleSort ob = new BubbleSort();
		int arr[] = { 64, 34, 25, 12, 22, 11, 90 };

		ob.bubbleSort(arr);

		System.out.println("Sorted array");

		ob.printArray(arr);
	}
}
```

## 1.2. Insertion Sort

Insertion sort is a simple sorting algorithm that works similar to the way you sort playing cards in your hands. The array is virtually split into a sorted and an unsorted part. Values from the unsorted part are picked and placed at the correct position in the sorted part.

### 1.2.1. Characteristics of Insertion Sort

This algorithm is one of the simplest algorithm with simple implementation
Basically, Insertion sort is efficient for small data values
Insertion sort is adaptive in nature, i.e. it is appropriate for data sets which are already partially sorted.

```java
// Java program for implementation of Insertion Sort
class InsertionSort {
	// Function to sort array using insertion sort
	void sort(int arr[]) {
		int n = arr.length;

		for (int i = 1; i < n; ++i) {
			int key = arr[i];
			int j = i - 1;

			/*
			 * Move elements of arr[0..i-1], that are greater than key, to one position
			 * ahead of their current position
			 */
			while (j >= 0 && arr[j] > key) {
				arr[j + 1] = arr[j];
				j = j - 1;
			}

			arr[j + 1] = key;
		}
	}

	// A utility function to print array of size n
	static void printArray(int arr[]) {
		int n = arr.length;

		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");

		System.out.println();
	}

	// Driver method
	public static void main(String args[]) {
		int arr[] = { 12, 11, 13, 5, 6 };

		InsertionSort ob = new InsertionSort();
		ob.sort(arr);

		printArray(arr);
	}
}
```

## 1.3. Merge Sort

The Merge Sort algorithm is a sorting algorithm that is based on the Divide and Conquer paradigm. In this algorithm, the array is initially divided into two equal halves and then they are combined in a sorted manner.

### 1.3.1. Merge Sort Working Process

Think of it as a recursive algorithm continuously splits the array in half until it cannot be further divided. This means that if the array becomes empty or has only one element left, the dividing will stop, i.e. it is the base case to stop the recursion. If the array has multiple elements, split the array into halves and recursively invoke the merge sort on each of the halves. Finally, when both halves are sorted, the merge operation is applied. Merge operation is the process of taking two smaller sorted arrays and combining them to eventually make a larger one.

```java
// Java program for Merge Sort
class MergeSort {
	// Merges two subarrays of arr[].
	// First subarray is arr[l..m]
	// Second subarray is arr[m+1..r]
	void merge(int arr[], int l, int m, int r) {
		// Find sizes of two subarrays to be merged
		int n1 = m - l + 1;
		int n2 = r - m;

		// Create temp arrays
		int L[] = new int[n1];
		int R[] = new int[n2];

		// Copy data to temp arrays
		for (int i = 0; i < n1; ++i)
			L[i] = arr[l + i];
		for (int j = 0; j < n2; ++j)
			R[j] = arr[m + 1 + j];

		// Merge the temp arrays

		// Initial indexes of first and second subarrays
		int i = 0, j = 0;

		// Initial index of merged subarray array
		int k = l;
		while (i < n1 && j < n2) {
			if (L[i] <= R[j]) {
				arr[k] = L[i];
				i++;
			} else {
				arr[k] = R[j];
				j++;
			}
			k++;
		}

		// Copy remaining elements of L[] if any
		while (i < n1) {
			arr[k] = L[i];
			i++;
			k++;
		}

		// Copy remaining elements of R[] if any
		while (j < n2) {
			arr[k] = R[j];
			j++;
			k++;
		}
	}

	// Main function that sorts arr[l..r] using
	// merge()
	void sort(int arr[], int l, int r) {
		if (l < r) {
			// Find the middle point
			int m = l + (r - l) / 2;

			// Sort first and second halves
			sort(arr, l, m);
			sort(arr, m + 1, r);

			// Merge the sorted halves
			merge(arr, l, m, r);
		}
	}

	// A utility function to print array of size n
	static void printArray(int arr[]) {
		int n = arr.length;
		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");
		System.out.println();
	}

	// Driver code
	public static void main(String args[]) {
		int arr[] = { 12, 11, 13, 5, 6, 7 };

		System.out.println("Given Array");
		printArray(arr);

		MergeSort ob = new MergeSort();
		ob.sort(arr, 0, arr.length - 1);

		System.out.println("\nSorted array");
		printArray(arr);
	}
}
```

## 1.4. Selection Sort

The selection sort algorithm sorts an array by repeatedly finding the minimum element (considering ascending order) from the unsorted part and putting it at the beginning.

The algorithm maintains two subarrays in a given array.

```java
// Java program for implementation of Selection Sort
class SelectionSort {
	void sort(int arr[]) {
		int n = arr.length;

		// One by one move boundary of unsorted subarray
		for (int i = 0; i < n - 1; i++) {
			// Find the minimum element in unsorted array
			int min_idx = i;

			for (int j = i + 1; j < n; j++)
				if (arr[j] < arr[min_idx])
					min_idx = j;

			// Swap the found minimum element with the first
			// element
			int temp = arr[min_idx];
			arr[min_idx] = arr[i];
			arr[i] = temp;
		}
	}

	// Prints the array
	void printArray(int arr[]) {
		int n = arr.length;

		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");

		System.out.println();
	}

	// Driver code to test above
	public static void main(String args[]) {
		SelectionSort ob = new SelectionSort();
		int arr[] = { 64, 25, 12, 22, 11 };

		ob.sort(arr);

		System.out.println("Sorted array");

		ob.printArray(arr);
	}
}
```
