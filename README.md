# 42_cpp09

So this is the final module of our introduction to cpp. We have three exercises and we are allowed to use the STL and containers but the container we choose to solve one exercise must be different from the other two. Therefore it is recommended to read through all the exercises before starting to solve them. 

## Exercise 00: Bitcoin Exchange

> You have to create a program which outputs the value of a certain amount of bitcoin on a certain date.  
This program must use a database in csv format which will represent bitcoin price
over time. This database is provided with this subject.  
The program will take as input a second database, storing the different prices/dates
to evaluate.  
The csv contains pairs of date/price like `2011-08-27,10.01`.

## Exercise 01: Reverse Polish Notation
> Your program must take an inverted Polish mathematical expression as an argu-
ment.
• The numbers used in this operation and passed as arguments will always be less
than 10. The calculation itself but also the result do not take into account this rule.  
• Your program must process this expression and output the correct result on the
standard output.  
• If an error occurs during the execution of the program an error message should be
displayed on the standard output.  
• Your program must be able to handle operations with these tokens: "+ - / *".

## Exercise 02: PmergeMe
> Your program must be able to use a positive integer sequence as argument.
• you need to use the Ford-Johnson algorithm.
• Your program must use the merge-insert sort algorithm to sort the positive integer
sequence
• You must use at least two different containers in your code to validate this exercise. Your program must be able to handle at
least 3000 different integers.

### Ford-Johnson algorithm
> In computer science, merge-insertion sort or the Ford–Johnson algorithm is a comparison sorting algorithm published in 1959 by L. R. Ford Jr. and Selmer M. Johnson. It uses fewer comparisons in the worst case than the best previously known algorithms, binary insertion sort and merge sort, and for 20 years it was the sorting algorithm with the fewest known comparisons. Although not of practical significance, it remains of theoretical interest in connection with the problem of sorting with a minimum number of comparisons. - wiki

Ok just to make sure you are following me, they are not the same :)
The Ford-Johnson algorithm is a variant of merge sort, it's a specific optimization that aims to reduce the number of comparisons needed in the worst case scenario. So the wiki page is misleading. The Ford-Johnson algorithm employs a strategy to reduce the number of comparisons needed in the merging step, making it more efficient in terms of comparisons. While the Ford-Johnson algorithm is theoretically interesting for its comparison efficiency, it's not widely used in practice due to its potential overhead and complexity compared to standard merge sort implementations

An example implementation of the ford johnson algorithm given to me by google gemini is as follows:
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

// Function to calculate the distance between two elements in an array
int distance(const vector<int>& arr, int i, int j) {
    return abs(arr[i] - arr[j]);
}

// Function to sort an array using the Ford-Johnson algorithm
void fordJohnsonSort(vector<int>& arr) {
    int n = arr.size();

    // Base case: If there are only two elements, sort them
    if (n <= 2) {
        sort(arr.begin(), arr.end());
        return;
    }

    // Divide the array into two halves
    int mid = n / 2;
    vector<int> left(arr.begin(), arr.begin() + mid);
    vector<int> right(arr.begin() + mid, arr.end());

    // Recursively sort  
 the left and right halves
    fordJohnsonSort(left);
    fordJohnsonSort(right);

    // Merge the sorted halves using Ford-Johnson's optimization
    int i = 0, j = 0, k = 0;
    while (i < left.size() && j < right.size()) {
        if (left[i] <= right[j]) {
            arr[k++] = left[i++];
        } else {
            arr[k++] = right[j++];
            // Ford-Johnson optimization: If the difference between the current element in the right half and the last element in the left half is less than the difference between the current element in the left half and the last element in the right half,
            // then swap the current elements in the left and right halves
            if (i > 0 && distance(arr, k - 1, j) < distance(arr, i - 1, j)) {
                swap(arr[k - 1], arr[k - 2]);
            }
        }
    }

    // Copy the remaining elements from the left or right half
    while (i < left.size()) {
        arr[k++] = left[i++];
    }
    while (j < right.size()) {
        arr[k++] = right[j++];
    }
}
```
In the above code there is just one point where the algo differs from the standard merge sort.

## Links
https://en.wikipedia.org/wiki/Merge-insertion_sort


