```cpp
1. Maximum Subarray: maximum subarray in range A[low...high] -> Any contiguous max subarray, A[i...j] must lie at one of these places:
a. entirely in left subarray A[low...mid]
b. entirely in right subarray A[mid+1...high]
c. crossing the midpoint, low<=i<=mid<j<=high, i.e. between low and high.

finally max of all three subarrays is ans
T(n) = 2T(n/2) + O(n) = nlogn


  class Solution {
    private int findMaxCrossSubArray(int[] nums, int l, int m, int h){
        int leftSum = Integer.MIN_VALUE;
        int sum = 0;
        for(int i =m;i>=l;i--){
            sum = sum+nums[i];
            if(sum>leftSum){
                leftSum = sum;
            }
        }

        int rightSum = Integer.MIN_VALUE;
        sum = 0;
        for(int i=m+1;i<=h;i++){
            sum=sum+nums[i];
            if(sum>rightSum){
                rightSum = sum;
            }
        }
        return rightSum+leftSum;
    }

    private int findMaxSubArray(int[] nums, int l, int h){
        if(h==l){
            return nums[l];
        }else{
            int m = l+ (h-l)/2;
            int leftSum = findMaxSubArray(nums,l,m);
            int rightSum = findMaxSubArray(nums,m+1,h);
            int crossSum = findMaxCrossSubArray(nums,l,m,h);
            if(leftSum>=rightSum && leftSum>=crossSum){
                return leftSum;
            }else if(rightSum >= leftSum && rightSum>=crossSum){
                return rightSum;
            }else{
                return crossSum;
            }
        }
    }

    public int maxSubArray(int[] nums) {
        int sum = findMaxSubArray(nums, 0, nums.length-1);
        return sum;
        
    }
}
```
