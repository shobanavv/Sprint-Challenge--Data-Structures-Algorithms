Add your answers to the Algorithms exercises here.
Analysis of Algorithms
Exercise I. Give an analysis of the running time with respect to the input size n of each of the following program fragments below:

a) a = 0;
while (a < n * n * n)
a = a + n * n;

#Answers:

## Part a)
O(n) / linear - the bound is cubic, but the rate of growth is quadratic.


b) // input array is of length n i = array.length - 1;
while (array[i] > x && i >= 0)
i = i/2;

## Part b)
O(log(n)) / logarithmic (assuming integers not floats) - `i` is cut in half each
iteration, and the comparison to `x` is irrelevant.

c) sum = 0;
for (i = 0; i < Math.sqrt(n) / 2; i++)
       for ( j = i; j < 8 + i; j++)
         for (k = j; k < 8 + j; k++)
sum++;

## Part c)
O(sqrt(n)) - a somewhat unusual but still distinct complexity, determined fully
by the outer loop. The two inner loops are both always length 8 so are dropped.


d) sum = 0;
for (i = 1; i < n; i *= 2)
        for (j = 0; j < n; j++)
           sum++;

## Part d)
O(n*log(n)) / log-linear (or "linearithmic") - the outer loop is logarithmic,
the inner is linear, and the total complexity is just their product.


e) sum = 0;
for (i = 0; i < n; i++)
       for (j = i + 1; j < n; j++)
         for (k = j + 1; k < n; k++)
           for (l = k + 1; l < 10 + k; l++)
             sum++;

## Part e)
O(n^3) / cubic - the outer loop is linear, the next two nested loops are both
linear (in the worst/general case), and the innermost is just constant (9).


f) bunnyEars = function (bunnies) { // here bunnies === n if (bunnies === 0) return 0;
return 2 + bunnyEars(bunnies-1);
}

## Part f)
O(n) / linear - essentially equivalent to a simple for loop but recursive.

g) search = function (array, arraySize, target) { // here arraySize === n if (arraySize > 0) {
         if (array[arraySize-1] === target) return true;
         else return search(array, arraySize-1, target);
       }
      return false;
     }

## Part g)
O(n) / linear - it can return early, but worst/general case is linear.


#Exercise II. Questions. Answers below.
a) Given an array a of n numbers, design a linear running time algorithm to find the maximum value of a[j] - a[i], where j ≥ i.

b) Suppose that you have an n-story building and plenty of eggs. Suppose also that an egg is broken if it is thrown off floor f or higher, and unbroken otherwise. Devise a strategy to determine the value of f such that the number of dropped eggs is minimized.
1

Exercise III. Below is the the pseudo-code for the Quicksort algorithm:
function quicksort(array)
   if length(array) <= 1
       return array
   select and remove a pivot element pivot from array
   create empty lists less and greater
   for each x in array
       if x <= pivot then append x to less
       else append x to greater
   return concatenate(quicksort(less), list(pivot), quicksort(greater))
a) Suppose we implement quicksort so that the pivot is always chosen to be the first element of the array. What is the running time of this algorithm on an input array that is already sorted? Why?
b) Suppose we implement quicksort so that the pivot is always magically chosen to be the median element of the array. What is the running time of this algorithm? Why?

# Exercise II

## Part a)
The naive (quadratic) approach would be a nested for loop, over `i` and `j`, that compares all possible combinations and remembers the one with the biggest difference.

The correct/efficient (linear) approach is to loop over the array once tracking the minimum value and maximum difference in the same pass.

Pseudocode:
```
minVal = a[0]
maxDiff = 0
for i in 1...n:
    minVal = min(minVal, a[i])
    maxDiff = max(maxDiff, a[i] - minVal)
return maxDiff
```

## Part b)
This is a conceptual question, and can be answered in a number of ways - the key
insight is that you should essentially implement a binary search. Start by
dropping an egg from the middle floor - if it breaks, go to the midway point
between where you are and the bottom. If it doesn't, go to the midway point
between where you are and the top. Either way, continue until you've narrowed
on the specific lowest floor that causes it to break, and that is `f`.


# Exercise III

## Part a)
The runtime will be O(n^2) / quadratic - there will be a linear number of passes
on possible pivots, and each pivot will be compared with (on average) a linear