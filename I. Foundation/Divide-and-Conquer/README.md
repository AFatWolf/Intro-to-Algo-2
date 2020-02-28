# 4.Divide and Conquer.  
## 4.1. The maximun-subarray problem.  
Given a array of n elements, find the maximun-subarray.  
**A brute force solution:**  
We can easily devise a brute-force solution by trying every possible subarray. This approach would take O(n^2) time.  
**A solution using divide-and-conquer.**  
Suppose we want to find a maximum subarray of the subarray A[low..high]. Divide-and-conquer suggests that we divide the subarraya into two subarrays of as equal size as possible.  
Therefore, we divide the subarray A[low..high] into 2 subarrays: A[low..mid], A[mid+1..high]. Let call the subarray with maximum sum is A[i..j].  
There are 3 options for the subarray belong to:  
+ Entirely in the subarray A[low...mid]. low <= i <= j <= mid.    
+ Entirely in the subarray A[mid+1..high]. mid+1<=i<=j<=high.    
+ Crossing the mid point. i <=mid < j.  

As we can see, the first two case, we can recall the result of A[low..mid] and A[mid+1..high].    
To solve the final case, we could devise 2 other maximum value of a subarray:  
+ maxL[i..j]: the maximum subarray of array A[i..j] that start from i-th position.  // save the position.
+ maxR[i..j]: the maximum subarray of array A[i..j] that end at j-th position.  // save the position.  
**Psuedocode:**
```
FindMaximum-Subarray(A,low,high):  
if low == high:  
	if a[low] < 0: maxL[low..high] = maxR[low..high] = max[low..high] = -1. (empty string will be a better choise).  
	maxL[low...high] = low.  
	maxR[low...high] = low.  
	max[low..high] = low.  
else:  
	(left_low,left_high,leftsum) = findMaximum-Subarray(A,low,mid)  
	(right_low,right_high,rightsum) = findMaximum-Subarray(A,mid+1,r)  
	(mid_low,mid_high,rightsum) = findMaximum-Subarray(A, maxR[low..mid],maxL[mid+1..r])  
	//
	maxL[low..high] = (max[mid+1..high] == -1 ? maxL[low..high] : max[mid+1..high]).  
	// same idea for maxR.  
	// compare three sum and return the opitmizing solution.  
```
**Note:** We also have a interesting method to solve this problem using binary-search... You can see the solution below for greedy approach:  
```
int maxSubArraySum(int a[], int size)   
{  
    int max_so_far = INT_MIN, max_ending_here = 0;  
    for (int i = 0; i < size; i++)  
    {  
        max_ending_here = max_ending_here + a[i];  
        if (max_so_far < max_ending_here)  
            max_so_far = max_ending_here;  
        if (max_ending_here < 0)  
            max_ending_here = 0;  
    }  
    return max_so_far;   
```  

## 4.2. Strassen algorithm for matrix multiplication.  
