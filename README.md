# Codeshows Contest 3 Editorial

## Coding Problems
### Paparazzi
#### Approach
We need to notice that we decide to stay on the day `D`, all the people whose range includes this point will be happy on this day.
Consider a single range `[L, R]`, any `X` days from `L` to `R` if included will increase the total happiness by `X`. 
So we can take an `M` sized array and for each range, add 1 to all positions in the range `[L, R]` signifying that if some day `D` is included, the total happiness will increase by the number of people that will be happy if this day is included.

To understand this visually, take the sample
```
3 7 3
1 2
6 7
4 5
```

Take 7 days, initially have all 0  
Then for each range add 1 in the range `[L, R]`
```
1 2 3 4 5 6 7
0 0 0 0 0 0 0 - Initially
1 1 0 0 0 0 0 - [1, 2]
1 1 0 0 0 1 1 - [6, 7]
1 1 0 1 1 1 1 - [4, 5]
```

If we pick the days [2, 4], we can get a happiness of 2, we recieve 1 happiness from person 1, and 1 from person 3.
If we pick the days [4, 6], we can get a happiness of 3, we recieve 2 happiness from person 2, and 1 from person 3.

Then we can try to pick all `K` consecutive days and pick the one with maximum total happiness.
What is the happiness in a range? The sum of the happiness on all the individiual days in that range.

#### Implementation
How to build the required array?  

Trivially this can be done by simple looping but that will time out.  
We can use the concept of a difference array which will help us update a range in constant time.  
For each range, we can `increment A[L]` and `decrement A[R + 1]`.  
Then build a prefix sum of this array to build the required array.

How to find the total happiness of a selected range?

We need to know what is the happiness in range `[i, i + K - 1]`.  
We know it is equal to the total sum of the numbers in that range.  
So once again we can build a prefix sum of this array.  
Then, `sum[L, R] = sum[1, R] - sum[1, L-1]`

Overall the problem can thus be solved in `O(M)` time.

### Chef Troubles 
#### Approach
Try to solve this problem for a single ingredient first.  
Suppose we want to make a dish with quality `at least X`, this means the ingredient must have a quality `at least X`. And out of all the shops that sell the ingredient with quality `at least X` we must pick the shop that sells it at the `least price P`. 

Let us see what happens if we try to make a dish with quality at least,

- `X' such that X' > X`  
The new price of the dish will be, `P'>= P`
- `X' such that X' < X`  
The new price of the dish will be, `P'<= P`

This means we can apply `Binary Search` to find the `largest X`, such that `P <= Budget`

If `P > Budget`, we need to find a `smaller X`  
If `P <= Budget`, we need to find a `larger X`

We can apply this same idea for multiple ingredients.  
We pick a quality `X`, for each ingredient we buy from the shop, that sells the ingredient at `quality at least X` and has the `least price`.

The running time of this approach is `O(N * M * log(maxQ))`, where maxQ is the maximum quality present.

## MCQs

![Q1](/mcq/1.jpg)

Since sum of digits is 3 the number is divisible by 3 so there exists no number other than 3 which is prime.