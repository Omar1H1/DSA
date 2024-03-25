
Def of an Algorithm : 

a step by step process to solve a computation problem 

Def of a program : 

a step by step process to solve a computation problem 

#### then what is the difference between them ? 

Programs needs to be designed first before been written, we don't do try and error when creating a good program, so we first make an algorithm and then write some sudo code, not really in any coding language .

##### Algorithm : 

- Design 
- Domain knowledge "can be written by the client it's just step by step process"
- Any language "even just pure English as long as it's understandable"
-  Doesn't depend on hardware or software
- Analyze 
##### Program : 
- implementation
- programmer 
- programming language 
- Depends  on Hardware and OS
- Testing

## 1.1 Priory Analysis and Posteriori Testing : 


#### Prior Analysis :
- Algorithm 
- independent of programming language
- Hardware independent
- Time and space function

#### Posteriori Testing : 
- Program
- language dependent
- Hardware dependent
- watch time and bytes 


## 1.2 Characteristics of Algorithm:

- **Input**: An algorithm can take zero or more inputs.
- **Output**: It must generate one or more outputs.
- **Definiteness**: Every statement of an algorithm must be understood and solvable.
- **Finiteness**: An algorithm must have an end or be defined to run forever.
- **Effectiveness**: Every statement must serve a purpose.

## 1.3 How to write and Analyze Algorithm :

#### What are we looking for when we analyze an algorithm ?
- **Time** : time it takes from the output to the input
- **Space** : how much of space, memory this algorithm will take to do the task
- **Data transfer** : for cloud base ... etc
- **Power consummation**
- **Cpu Registers** 

```c
Algorithm Swap(a, b) {
     temp = a;
     a = b;
     b = temp;
}
```

To analyze the time that this algorithm takes, let's suppose that each statement takes a one unit of time, then
`temp = a;` ----- 1
`a = b;` ----- 1
`b = temp;` ---- 1

Then f(n) = 3
O(n) = 1 constant

To analyze space we count the variables 

`a` --- 1
`b` --- 1
`temp` --- 1

s(n) = 3 words

O(n) = 1 constant 


#### 1.4 Frequency Count Method : 

```c
Algorithm Sum (a,n) {
    s = 0;  
    for(i = 0; i < n, i++) {
     s = s + a[i]
    }
    return s;
}
```

A is a one dimension Array, and N is the length of said Array.

as we saw in the previous example time can be measured by assigning one unit of time for each statement, and in this case we will take in consideration the frequency of set statements also as we do a loop . 

`s = 0` ---- 1
`i = 0` --- 1
`i < n` ---- n + 1 "we check for the false case too"
`i++` --- n
`s = s + A[i°` --- n
`return s` --- 1

f(n) = 3n + 4
we look for the polynomial degree with is 1 or just n  
O(n)


Space Complexity  :
`a` --- n
`n` --- 1
`i` --- 1
`s` ---- 1
s(n) = n + 3
which is O(n)


Now let's find the sum of 2D Array :

```c
Algorithm Add(A, B, n) {
    let C be a new 2D array of size n x n
    for i from 0 to n-1 {
        for j from 0 to n-1 {
            C[i][j] = A[i][j] + B[i][j]
        }
    }
    return C
}
```

time Complexity :

Initialization of array C: O(1)
Outer loop: n iterations => O(n)
Inner loop: n iterations * n iterations => O(n^2)
Addition operation inside inner loop: n^2 operations => O(n^2)
Return statement: O(1)

Total time complexity = O(1) + O(n) + O(n^2) + O(1) = O(n^2)

space complexity
Array C: O(n^2)
Loop variables and temporary variables: O(1)
Return value: O(n^2)


```c
Algorithm Multiply(A, B, n) {
    let C be a new 3D array of size n x n x n
    for i from 0 to n-1 {
        for j from 0 to n-1 {
            for k from 0 to n-1 {
                C[i][j][k] = 0
                for l from 0 to n-1 {
                    C[i][j][k] = C[i][j][k] + A[i][l][k] * B[l][j][k]
                }
            }
        }
    }
    return C
}

```




#### 1.5.1 Time complexity #1 : 

``` c
   for (i = 0; i < n; i++) {
      stmt;
   }
```

 `for (i = 0; i < n; i++)` :  n + 1, +1 because we gonna check for the false condition
 `stmt` : inside the loop will execute n times

  the time complexity will be O(n), thus we can ignore the loop initialization and go directly to how many times the statement inside the loop has been executed .

if the loop init was `for (i = n; i > 0, i--)` so the loops is starting from n going down till 0 (discriminating) the time complexity will still be n.

if the loop init was `for(i = 1; i < n; i+2)` so the loop will be running half of n times $n/2$, it's only the degree of polynomial that counts . 


```c
   for (i = 0; i < n; i++) {
	   for  (j = 0; j < i; j++) {
		   stmt;
	   }
   }
```

let's trace this function :

- When `i = 0`, since `0 < n` (condition true), we enter the inner loop. However, `j < i` is false (`0 < 0`), so the inner loop doesn't execute.
- When `i = 1`, since `1 < n` (condition true), we enter the inner loop. Now, `j < i` is true (`0 < 1`), so the inner loop executes once. Then `j` becomes 1, and `j < i` becomes false (`1 < 1`), so we exit the inner loop.
- When `i = 2`, since `2 < n` (condition true), we enter the inner loop. Now, `j < i` is true (`0 < 2`), so the inner loop executes once. Then `j` becomes 1, and `j < i` remains true (`1 < 2`), so the inner loop executes again. Then `j` becomes 2, and `j < i` becomes false (`2 < 2`), so we exit the inner loop.
- When `i = 3`, since `3 < n` (condition true), we enter the inner loop. Now, `j < i` is true (`0 < 3`), so the inner loop executes once. Then `j` becomes 1, and `j < i` remains true (`1 < 3`), so the inner loop executes again. Then `j` becomes 2, and `j < i` remains true (`2 < 3`), so the inner loop executes once more. Then `j` becomes 3, and `j < i` becomes false (`3 < 3`), so we exit the inner loop.
- When `i = 4`, since `4 < n` (condition true), we enter the inner loop. Now, `j < i` is true (`0 < 4`), so the inner loop executes once. Then `j` becomes 1, and `j < i` remains true (`1 < 4`), so the inner loop executes again. Then `j` becomes 2, and `j < i` remains true (`2 < 4`), so the inner loop executes once more. Then `j` becomes 3, and `j < i` remains true (`3 < 4`), so the inner loop executes once more. Then `j` becomes 4, and `j < i` becomes false (`4 < 4`), so we exit the inner loop.
- When `i = 5`, since `5 < n` (condition true), we enter the inner loop. Now, `j < i` is true (`0 < 5`), so the inner loop executes once. Then `j` becomes 1, and `j < i` remains true (`1 < 5`), so the inner loop executes again. Then `j` becomes 2, and `j < i` remains true (`2 < 5`), so the inner loop executes once more. Then `j` becomes 3, and `j < i` remains true (`3 < 5`), so the inner loop executes once more. Then `j` becomes 4, and `j < i` remains true (`4 < 5`), so the inner loop executes once more. Then `j` becomes 5, and `j < i` becomes false (`5 < 5`), so we exit the inner loop.
-  After running this enough times we can see a pattern, the statement inside the inner loop will run exactly n times, the formula to find the [sum of natural numbers](https://omerseyfeddinkoc.medium.com/the-proof-behind-the-sum-of-the-first-n-natural-numbers-8559ebfb8346) is $n(n+1) \div 2$ which can be written as $(n^2 + 1) \div 2$, and the degree of the polynomial here is $n^2$

So O ($n^2$)

let's take a look at this function :

```c
   p = 0;
   for(i = 1; p <= i; i++){
	   p = p + i;
   }
```

let's trace this algorithm : 


| i   | p                           |
| --- | --------------------------- |
| 1   | 0 + 1                       |
| 2   | 1 + 2                       |
| 3   | 1 + 2 + 3                   |
| 4   | 1 + 2 + 3 + 4               |
| 5   | 1 + 2 + 3 + 4 + 5           |
| k   | 1 + 2 + 3 + 4 + 5 + ... + k |

the loop will stop if we assume that  `k > n`, since $p = (k(k+1)) \div 2$ , $(k(k+1)) \div 2 > n$
$k^2 > n$
$k > \sqrt {n}$

so O($\sqrt {n}$)

#### Time Complexity Example #2 :

let's say we have this function: 

```c
  for(i = 1; i < n; i = i * 2) {
	  stmt;
  }
```

let's trace it :

| i               |
| --------------- |
| 1               |
| $1 * 2 = 2$     |
| $2 * 2 = 2^2$   |
| $2^2 * 2 = 2^3$ |
| $2^3 * 2 = 2^4$ |
| \|              |
| \|              |
| \|              |
| $2^k$           |

Assume $i >= n$

$\because i = 2^k$
$\therefore 2^k >= n$
    $2^k = n$
     $k = log_{2} n$

$O(log_{2} n)$

let's take look at this example :

```c
  for (i = 1; i <= n; i ++) {
	  stmt;
  }
```

$i = 1 + 1 + 1 + .... + 1 = n$
$k = n$
```c
  for (i = 1; i < n; i ++) {
	  stmt;
  }
```

$i = 1 * 2 * 2 * 2 * .... = n$
$2^k = n$
$k = log_{2} n$

so we can say for every loop where the value of i is getting multiplied we can say the time is $log_{x}n$ where x is equal to the value of what i is multiplied  with.

we should always ceil the value of $logn$ !!


```c
   for (i = n; i >= 1; i = i / 2) {
	   stmt;
   }
```

same thing as we saw with i ++ and i --

time complexity is the same $O(log_{2}n)$

```c
  for(i = 0; i * i < n; i++) {
      stmt;
  }
```

$i * i < n$
the loop will stop when :

$i * i >= n$
$i^2 = n$
$i = \sqrt {n}$

$O(\sqrt {n})$

```c
   p = 0
   for (i = 1; i < n; i * 2) {
        stmt;
   }
   for (j = 1; j < p; j * 2) {
        stmt;
   }
```

for the first loop :

$O(log {n})$

and the second :

$O(log {p})$

$\because p = log {n}$
$\therefore O(log log {n})$



let's  look at what we have seen so far :

`for (i = 0; i < n; i++)` ---- $O(n)$
`for (i = n; i > 1; i--)` ---- $O(n)$
`for (i = 0; i < n; i + 2)` ---- $\frac {n}{2}$  $O(n)$
`for (i = 1; i < n; i = i * 2)` ---- $O(log_{2} n)$
`for (i = 1; i < n; i = i * 3)` ---- $O(log_{3} n)$
`for (i = 1; i < n; i = i / 2)` ---- $O(log_{2} n)$


#### 1.5.3 Time Complexity of While and if #3 :

```c
i = 0;
while(i < n) {
   stmt
   i++
}
```

$f(n) = 3n + 2$
$O(n)$


```c
a = 1;
while( a < b) {
   stmt
   a = a * 2
}
```

let's trace it :

| a               |
| --------------- |
| 1               |
| $1 * 2 = 2$     |
| $2 * 2 = 2^2$   |
| $2^2 * 2 = 2^3$ |
| $2^3 * 2 = 2^4$ |
| \|              |
| \|              |
| \|              |
| $2^k$           |
this loop will terminate when:
$a >= b$
$\because a = 2^k$
$\therefore 2^k >= b$
    $2^k = b$
    $k = log_{2}b$
$O(logn)$


#### 1.6 Classes of functions : 

Types of time functions we have seen :
- $O(1)$ ----> constant 
- $O(logn)$ -----> logarithmic
- $O(n)$ -----> linear
- $O(n^2)$ -----> Quadratic
- $O(n^3)$ ------> cubic
- $O(2^n)$ Exponential

#### 1.7 Compare Class of Functions : 

$1 < logn < n < \sqrt {n} < nlogn < n^2 < n^3 < ... < 2^n < 3^n ... < n^n$

| $log n$ | $n$ | $n^2$ | $2^n$ |
| ------- | --- | ----- | ----- |
| 0       | 1   | 1     | 2     |
| 1       | 2   | 4     | 4     |
| 2       | 4   | 16    | 16    |
| 3       | 8   | 64    | 256   |
|         |     |       |       |
|         |     |       |       |
|         |     |       |       |

![](https://miro.medium.com/v2/resize:fit:750/format:webp/0*sHLx8GgoVye4Ku2c.png)


#### 1.8.1 Asymptotic Notations Big O - Omega $\Omega$ - Theta $\theta$  #1 :

- O big-oh upper bound.
- $\Omega$ big-omega lower bound.
- $\theta$ Theta Average bound.

##### Def of Big-oh :
The function $f(n) = O(g(n)) \iff \exists$ + constants such that $f(n) \leq c * g(n)   \forall n \geq n_{0}$

Example :

$f(n) = 2n + 3$
$2n + 3 \geq 10n$   $\forall n \geq 1$

`f(n) = 2n + 3`
`c = 10`
`g(n) = n`

$\therefore f(n) = O(n)$
