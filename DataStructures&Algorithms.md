#### Will it scale?
- For algorithms, scalability refers to how the algorithm performs in terms of execution time and memory usage as the input size increases.
- When you’re working with a small amount of data, an expensive algorithm may still feel fast. However, as the amount of data increases, an expensive algorithm becomes crippling. 


#### Big O(Omicron) notation 
- Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity.
- Big O is the language used to compare performance of algorithms (time and space).
- Most common characteristics are:
  -  Constant O(1)
  -  Linear O(n)
  -  Quadratic O(n^2)
  -  Logarithmic O(logn)
- When we talk about Big O, we talk about the worst case. And we can trade-off time for space. 
- 大O符號（英語：Big O notation），又稱為漸進符號，是用於描述函式漸近行為的數學符號。更確切地說，它是用另一個（通常更簡單的）函式來描述一個函式數量級的漸近上界。
- 大O符號是由德國數論學家保羅·巴赫曼在其1892年的著作《解析數論》（Analytische Zahlentheorie）首先引入的。而這個記號則是在另一位德國數論學家艾德蒙·朗道的著作中才推廣的，因此它有時又稱為朗道符號（Landau symbols）。代表「order of ...」（……階）的大O，最初是一個大寫希臘字母「Ο」（omicron），現今用的是大寫拉丁字母「O」。
- Big Omega : Big Omega notation is used to measure the best-case runtime for an algorithm. This isn’t as useful as Big O because getting the best case is often untenable.
- Big Theta : Big Theta notation is used to measure the runtime for an algorithm that has the same best and worse case.
- Big O Notation: 1. time(how fast), 2. space(how much memory).
- [Cheat Sheet](https://www.bigocheatsheet.com)


#### Time complexity
- Time complexity is a measure of the time required to run an algorithm as the input size increases.
- Constant time: A constant time algorithm is one that has the same running time regardless of the size of the input. The Big O notation for constant time is O(1).
- Linear time: As the amount of data increases, the running time increases by the same amount. That’s why you have the straight linear graph illustrated above. The Big O notation for linear time is O(n).
- Quadratic time: As the size of the input data increases, the amount of time it takes for the algorithm to run increases drastically. Thus, n squared algorithms don’t perform well at scale. The Big O notation for quadratic time is O(n²).
- Logarithmic time: As input data increases, the time it takes to execute the algorithm increases at a slow rate. Algorithms in this category are few but extremely powerful in situations that allow for it. The Big O notation for logarithmic time complexity is O(log n).
- Quasilinear time: Quasilinear time algorithms perform worse than linear time but dramatically better than quadratic time. The Big-O notation for quasilinear time complexity is O(n log n) which is a multiplication of linear and logarithmic time. So quasilinear fits between logarithmic and linear time; it is worse than linear time but still better than many of the other complexities.
- Other time complexities: These time complexities include polynomial time, exponential time, factorial time and more.
- It is important to note that time complexity is a high-level overview of performance, and it doesn’t judge the speed of the algorithm beyond the general ranking scheme. This means that two algorithms can have the same time complexity, but one may still be much faster than the other. For small data sets, time complexity may not be an accurate measure of actual speed.

#### Notes: 
- Time complexity is a measure on the time required to run an algorithm as the input size increases.
- You should know about constant time, logarithmic time, linear time, quasilinear time and quadratic time and be able to order them by cost.
- Space complexity is a measure of the resources required for the algorithm to run.
- Big O notation is used to represent the general form of time and space complexity.
- Time and space complexity are high-level measures of scalability; they do not measure the actual speed of the algorithm itself.
- For small data sets, time complexity is usually irrelevant. For example, a quasilinear algorithm can be slower than a quadratic algorithm when n is small.

#### Tips
- Hash Maps / Dictionaries are your freind.

#### Array
- Arrays can contain anything
- Arrays are of a fixed size
- Arrays support random access
- Get/Set methods for array
