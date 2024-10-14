# Sorting

## Sorting: 
time complexity: Ω, θ, O
space complexity: O
Online: If an algo is online we can add more inputs consecutively. adding more input wont affect the result
stable: order of input is maintained
inplace: Aux space: O(1)

> **Selection Sort:** Unstable \(Can be turned stable\), Ω\(N²\) - θ\(N²\) - O\(N²\) : O\(1\)
> **Bubble Sort:** Stable**,** Ω\(N\) - θ\(N²\) - O\(N²\) : O\(1\)
> **Insertion Sort:** Stable, Ω\(N\) - θ\(N²\) - O\(N²\) : O\(1\)
> **Merge Sort:** Stable, Ω\(NlogN\) - θ\(NlogN\) - O\(NlogN\) : O\(N\)
> **Quick Sort:** Unstable \(Can be turned stable\), Ω\(NlogN\) - θ\(NlogN\) - O\(N²\) : O\(1\)

```cpp
1. Bubble sort: compare adjacent element and bubble the larget element to end.

2. Selection sort:


1. mergesort
private static void merge(int[] arr, int l, int m, int r){
        int n1 = m-l+1;
        int n2 = r-m;
        int[] L= new int[n1+1];
        int[] R= new int[n2+1];
        
        for(int i=0;i<n1;i++){
            L[i] = arr[l+i];
        }
        for(int j=0;j<n2;j++){
            R[j] = arr[m+j+1];
        }
        
        L[n1] = Integer.MAX_VALUE;
        R[n2] = Integer.MAX_VALUE;
        
        int i=0,j=0;
        for(int k=l;k<=r;k++){
            if(L[i]<=R[j]){
                arr[k] = L[i];
                i++;
            }else{
                arr[k] = R[j];
                j++;
            }
        }
    }
    public static void mergeSort(int[] arr, int l, int r){
        if(l<r){
            int m = l+ (r-l)/2;
            mergeSort(arr,l,m);
            mergeSort(arr,m+1,r);
            merge(arr,l,m,r);
        }
        
    }

2. Quick sort: /* Randomized quick sort (picking random pivot index instead of r) gives
NlogN in worst aswell */
// Quick sort is worst when - already sorted (asc or desc) or all elems are same

import java.lang.Math;
class Solution {

    private int random(int l,int r){
        return l + (int) (Math.random() * (r - l));
    }



    private int partition(int A[],int l,int r){
        int i = l-1;
        for(int j=l;j<r;j++){
            if(A[j]<A[r]){
                i++;
                //exchange A[i] with A[j]
                int k = A[i];
                A[i] = A[j];
                A[j] = k;
            }
        }
        //exchange A[i+1] with A[r]
        int temp = A[r];
        A[r] = A[i+1];
        A[i+1] = temp;
        return i+1;
    }

    private int randomPartition(int[] A,int l, int r){
        int pivot = random(l,r);
        // Swap A[pivot] with A[r] to move pivot element to the end
        int temp = A[pivot];
        A[pivot] = A[r];
        A[r] = temp;
        return partition(A,l,r);

    }

    private int[] quickSort(int[] nums,int l,int r){
        if(l<r){
        int m = randomPartition(nums,l,r);
        quickSort(nums,l,m-1);
        quickSort(nums,m+1,r);
        }
        return nums;   
    }

    public int[] sortArray(int[] nums) {
        int[] arr = quickSort(nums,0,nums.length-1);
        return arr;
    }
}

3. class Solution {

    // Corrected swap method to swap elements in the array
    public void swap(int[] nums, int a, int b) {
        int temp = nums[a];
        nums[a] = nums[b];
        nums[b] = temp;
    }

    // Heapify method to maintain max-heap property
    private void heapify(int[] nums, int n, int i) {
        int largest = i;  // Initialize largest as root
        int l = 2 * i + 1;  // Left child
        int r = 2 * i + 2;  // Right child

        // If left child is larger than root
        if (l < n && nums[l] > nums[largest]) {
            largest = l;
        }

        // If right child is larger than largest so far
        if (r < n && nums[r] > nums[largest]) {
            largest = r;
        }

        // If largest is not root, swap and continue heapifying
        if (largest != i) {
            swap(nums, i, largest);  // Swap root with largest
            heapify(nums, n, largest);  // Heapify the affected subtree
        }
    }

    // Build the heap (rearrange the array)
    private void buildHeap(int[] nums, int n) {
        for (int i = (n / 2) - 1; i >= 0; i--) {
            heapify(nums, n, i);
        }
    }

    // Heap sort method
    private void heapsort(int[] nums, int n) {
        // Build a max heap
        buildHeap(nums, n);

        // Extract elements from the heap one by one
        for (int i = n - 1; i > 0; i--) {
            // Move current root (largest) to the end
            swap(nums, 0, i);

            // Call heapify on the reduced heap
            heapify(nums, i, 0);
        }
    }

    // Main method to sort the array
    public int[] sortArray(int[] nums) {
        heapsort(nums, nums.length);
        return nums;
    }

    // Testing the solution
    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] nums = {12, 11, 13, 5, 6, 7};
        int[] sortedArray = solution.sortArray(nums);

        System.out.println("Sorted Array: ");
        for (int num : sortedArray) {
            System.out.print(num + " ");
        }
    }
}

```
