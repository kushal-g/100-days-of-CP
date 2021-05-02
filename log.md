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
<br><br>

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
<br><br><br>
### Day 2: April 30, 2021 
<br>

**Today's Progress**: Completed the following 3 Questions:
<ol>
    <li>Sort Array by Increasing Frequency: Given an array of integers nums, sort the array in increasing order based on the frequency of the values. If multiple values have the same frequency, sort them in decreasing order. Return the sorted array.</li>
    <br>
    <li>Goat Latin: 

A sentence S is given, composed of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.)

The rules of Goat Latin are as follows:

If a word begins with a vowel (a, e, i, o, or u), append "ma" to the end of the word.
For example, the word 'apple' becomes 'applema'.
 
If a word begins with a consonant (i.e. not a vowel), remove the first letter and append it to the end, then add "ma".
For example, the word "goat" becomes "oatgma".
 
Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
For example, the first word gets "a" added to the end, the second word gets "aa" added to the end and so on.
Return the final sentence representing the conversion from S to Goat Latin. </li>
    <br>
    <li>Island Perimeter: 
    
You are given row x col grid representing a map where grid[i][j] = 1 represents land and grid[i][j] = 0 represents water.

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes", meaning the water inside isn't connected to the water around the island. One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.</li>
</ol>
<br><br>

**Thoughts:**

<ol>
    <li>Sort Array by Increasing Frequency: Had a straightforward approach of using a sort function and calling the sort method. I also found an interesting second approach where we formed buckets according to frequency and then added elements to a new array according to that.</li>
    <br>
    <li>Goat Latin: Pretty straightforward. Had to do exactly what it said.</li>
    <br>
    <li>Island Perimeter: Used DFS to find all elements of the island and checked the number of sides which faced sea for every block of island and summed them to get the perimeter. Saw an approach which didn't use DFS and just iterated over entire matrix to find the same sum which was surprisingly faster. Weird.</li>
</ol>
<br><br>

**Link(s) to work:** 
<ol>
    <li>Sort Array by Increasing Frequency: 
        <ul>
            <li><a href="https://leetcode.com/submissions/detail/487140869/" target="_blank"> Approach 1</a></li>
            <li><a href="https://leetcode.com/submissions/detail/487145550/" target="_blank">Approach 2</a></li>
        </ul>
    </li>
    <br>
    <li><a href="https://leetcode.com/submissions/detail/487152843/" target="_blank">Goat Latin</a></li>
    <br>
    <li><a href="https://leetcode.com/submissions/detail/487165537/" target="_blank">Island Perimeter</a></li>
</ol>
<br><br><br>

### Day 3: May 1, 2021 
<br>

**Today's Progress**: Completed the following 3 Questions:
<ol>
    <li>Prefix and Suffix Search:

Design a special dictionary which has some words and allows you to search the words in it by a prefix and a suffix.

Implement the WordFilter class:

WordFilter(string[] words) Initializes the object with the words in the dictionary.
f(string prefix, string suffix) Returns the index of the word in the dictionary which has the prefix prefix and the suffix suffix. If there is more than one valid index, return the largest of them. If there is no such word in the dictionary, return -1.</li>
    <br>
    <li>Find the Distance Value Between Two Arrays: 
    
Given two integer arrays arr1 and arr2, and the integer d, return the distance value between the two arrays.

The distance value is defined as the number of elements arr1[i] such that there is not any element arr2[j] where |arr1[i]-arr2[j]| <= d.</li>
    <br>
    <li>Divisor Game: 
    
Alice and Bob take turns playing a game, with Alice starting first.

Initially, there is a number n on the chalkboard. On each player's turn, that player makes a move consisting of:

Choosing any x with 0 < x < n and n % x == 0.
Replacing the number n on the chalkboard with n - x.
Also, if a player cannot make a move, they lose the game.

Return true if and only if Alice wins the game, assuming both players play optimally.</li>
</ol>
<br><br>

**Thoughts:**

<ol>
    <li>Prefix and Suffix Search: Surprisingly, this is a hard question on leetcode! I could think of the dictionary solution easily once my brute force solution gave me TLE. However, I missed one tiny thing where I needed an extra character to add between suffix and prefix to differentiate between similar strings generated from different prefixes and suffixes. All in all, a good brain workout.</li>
    <br>
    <li>Find the Distance Value Between Two Arrays: Pretty straightforward. Had to do exactly what it said.</li>
    <br>
    <li>Divisor Game: Kinda happy I could think in terms of DP and solve this question. However should have noticed a much more obvious pattern where it's true for even numbers and false for odd numbers. I thought about it for a sec but then for some reason didn't pursue it.</li>
</ol>
<br><br>

**Link(s) to work:** 
<ol>
    <li>
        <a href="https://leetcode.com/submissions/detail/487566058/" target="_blank">Prefix and Suffix Search</a>
    </li>
    <br>
    <li><a href="https://leetcode.com/submissions/detail/487567624/" target="_blank">Find the Distance Value Between Two Arrays</a></li>
    <br>
    <li>Divisor Game:
        <ul>
        <li><a href="https://leetcode.com/submissions/detail/487572529/">DP Approach</a></li>
        <li><a href="https://leetcode.com/submissions/detail/487573023/">O(1) Approach</a></li>
        </ul>
    </li>
</ol>