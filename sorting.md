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

```
1. Bubble sort: compare adjacent element and bubble the larget element to end.
```

```
2. Selection sort:

3. mergesort

```
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
    ```
