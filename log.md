# 100 Days Of Code - Log

### Day 1: April 29, 2021 
<br>

**Today's Progress**: Completed the following 3 Questions:
<ol>
    <li>Pair Sums: Given an integer array arr of size N and an integer S. Return the list of all pairs of elements such that for each sum of elements of each pair equals to S.</li>
    <br>
    <li>Overlapping Intervals: You have been given the start and end times of 'N' intervals. Write a function to check if any two intervals overlap with each other.</li>
    <br>
    <li>Minimum Absolute Difference: Given an array of distinct integers arr, find all pairs of elements with the minimum absolute difference of any two elements. Return a list of pairs in ascending order(with respect to pairs), each pair [a, b]</li>
</ol>
<br><br>

**Thoughts:** I tried out the Guided Paths feaure of Coding Ninjas today for a systematic approach to this 100 days of Code. Going to shift back to LeetCode now.

<ol>
    <li>Pair Sums: There were a lot of cases that I didn't take into account and even misinterpreted the question on the first time. But in the end, I was able to think of a solution on my own and complete it. I still need to practice thinking about these cases before writing the code to get better at whiteboard interviews.</li>
    <br>
    <li>Overlapping Intervals: Very easy question once you know how to merge intervals. Took the same approach to do it.</li>
    <br>
    <li>Minimum Absolute Difference: A nice question where you had to notice a tiny thing to form all the pairs quickly. Enjoyed doing this one!</li>
</ol>

**Link(s) to work:** 
1. [Pair Sum](https://www.codingninjas.com/codestudio/guided-paths/interview-guide-for-product-based-companies/content/110297/offering/1280152)

```c++
#include <unordered_map>
#include <algorithm>

bool sorter(vector<int> a, vector<int> b){
    if(a[0]!=b[0])
        return a[0] < b[0];
    return a[1] < b[1];
}

vector<vector<int>> pairSum(int arr[], int n, int S)
{
    //cout<<n<<S<<endl;
   unordered_map<int,int> freq;
   vector<vector<int>>res;
   for(int i=0;i<n;i++){
       freq[arr[i]]++;
   }
   
    for(auto e: freq){
        int num = e.first;
        int count = e.second;
        if(count && freq[S-num]){
            int turns = 0;
            if(num!=S-num){
                turns = count * freq[S-num];
            }else{
                turns = ((count) * (count - 1)) / 2;
            }
            while(turns){
                    vector<int> soln;
                    soln.push_back(min(num,S-num));
                    soln.push_back(max(num,S-num));
                    res.push_back(soln);
                    turns--;
            }
            freq[num] = 0;
            freq[S-num] = 0;
        } 
    }
    sort(res.begin(),res.end(),sorter);
    return res;
}
```

2. [Overlapping Intervals](https://www.codingninjas.com/codestudio/guided-paths/interview-guide-for-product-based-companies/content/110297/offering/1280151)

```c++
#include <vector>
#include <algorithm>

bool sorter(vector<int> a, vector<int>b){
	if(a[0]!=b[0])
        return a[0] < b[0];
    return a[1] < b[1];
}

bool checkOverlappingIntervals(long* start, long* end, int n)
{
	vector<vector<int>> intervals;
    for(int i=0;i<n;i++){
        vector<int> interval = {start[i], end[i]};
        intervals.push_back(interval);
    }
    sort(intervals.begin(),intervals.end(),sorter);
    
    for(int i=0;i<n-1;i++){
        if(intervals[i][0]==intervals[i+1][0]){
            return true;
        }
        else if(intervals[i+1][0]<intervals[i][1]){
            return true;
        }
    }
    return false;
}


```

3. [Minimum Absolute Difference](https://leetcode.com/submissions/detail/486800252/)

```c++
class Solution {
public:
    vector<vector<int>> minimumAbsDifference(vector<int>& arr) {
        int n = arr.size();
        sort(arr.begin(),arr.end());
        int min = INT_MAX;
        for(int i=0;i<n-1;i++){
            if(min>abs(arr[i]-arr[i+1])){
                min = abs(arr[i]-arr[i+1]);
            }
        }
        
        vector<vector<int>> soln;
        for(int i=0;i<n-1;i++){
            if(min==abs(arr[i]-arr[i+1])){
                vector<int> a;
                a.push_back(arr[i]);
                a.push_back(arr[i+1]);
                soln.push_back(a);
            }
        }
        
        return soln;
        
    }
};
```
