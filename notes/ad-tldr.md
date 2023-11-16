# Algorithm Design 22/23

# Mathematical Background
## Counting
### Permutations
A **permutation** of a finite set $S$ s a **ordered** sequence of all the elements in $S$, with each element appearing exactly once. 
For example, with $S = \{a, b, c\}$ we have $6$ permutations: $abc, acb, bac, bca, cab, cba$. 

For a set $S$ of $n$ elements we have $n!$ permutations, since there are $n$ ways to choose the first element of the sequence, $n-1$ ways of choosing the second element and so on. 

A **k-permutation** of $S$ is an **ordered** sequence of $k$ elements of $S$, with no element appearing more than once, and with $k < |S| = n$. 
We can say that a classic permutation is a $n$-permutation of the set $S$. 

The number of $k$-permutations of a $n$-set is: 
$$n(n-1)(n-2)\dots(n-k+1)= \frac{n!}{(n-k)!}$$
### Combinations
A **k-combination** of an $n$-set $S$ is simply a $k$-**subset** of $S$. 
For example, the $4$-set $\{a,b,c,d\}$ has $6$ $2$-combinations: $ab, ac, ad, bc, bd, cd$.
It is then clear that with combinations **the order do not matters**.

We can express the number of $k$-combinations of an $n$-set in terms of the number of $k$-permutations of an $n$-set.
Every $k$-combination has exactly $k!$ permutations of its elements, each of which is a distinct $k$-permutation of the $n$-set itself. 
Thus the number of $k$-combinations of a $n$-set is the number of $k$-permutations divided by $k!$

From the formula seen above about $k$-permutations we have that: $$k\text{-combinations} = \frac{n!}{k!(n-k)!}$$
### Binomial Coefficient
The notation $\binom{n}{k}$ denotes the number of $k$-combinations of an $n$-set. 
So we know that: $$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$
The binomial coefficient is symmetric in $k$ and $n-k$: 
$$\binom{n}{k} = \binom{n}{n-k}$$
## Probability
We define the **probability** in terms of a **sample space** $S$, which is a set whose elements are called **outcomes** or **elementary events**. 
An **event** is a subset of the sample space $S$. 

The event $S$ is called **certain event**, and the event $\emptyset$ is called the **null event**. 
We say that two events $A, B$ are **mutually exclusive** if $A \cap B = \emptyset$. 

An outcome $s \in S$ also define an event $\{s\}$, which we sometimes write as just $s$. 
By definition **all outcomes are mutually exclusive.**
### Axioms of Probability
A **probability distribution** $P$ on a sample space $S$ is a mapping from events of $S$ to real numbers satisfying the following axioms: 
1) $P(A) \geq 0$ for any event $A$
2) $P(S) = 1$
3) $P(A \cup B) = P(A) + P(B)$ for any two mutual exclusive events $A$ and $B$

We call $P(A)$ the **probability** of the event $A$. 

From the above axioms we derive several results: 
1) $P(\emptyset) = 0$
2) $A \subseteq B \implies P(A) \leq P(B)$ 
3) $P(\bar{A}) = 1 - P(A)$ 
4) $P(A\cup B) = P(A) + P(B) - P(A\cap B) \leq P(A) + P(B)$, for any two events $A, B$
### Discrete Probability Distribution
A **probability distribution** is **discrete** if it is defined over a finite (or countably infinite) sample space. 
Let $S$ be a finite sample space, then for any event $A \subseteq S$ we have 
$$P(A) = \Sigma_{s\in A}\ P(s)$$
since outcomes, specifically those in$A$, are mutually exclusive. 

If $S$ is finite and every outcome $s \in S$ has $P(s) = \frac{1}{|S|}$ we say that we have a **uniform probability distribution** on $S$. 
### Conditional Probability and Independence
Conditional probability formalizes the notion of having prior partial knowledge of the outcome of an experiment. 
The **conditional probability** of an event $A$ given that another event $B$ occurs is defined as 
$$P(A|B)= \frac{P(A\cap B)}{P(B)}$$
whenever $P(B) \neq 0$. 

Two events are said **independent** if $P(A\cap B) = P(A)P(B)$. 
Given two independent events $A$ and $B$ with $P(B) \neq 0$, then we have that $P(A|B) = P(A)$. 
### Bayes's Theorem
From the conditional probability and the commutative law $A\cap B = B \cap A$ it follows that for two events $A$ and $B$, each with non-zero probability, we have:
$$P(A\cap B) = P(B)P(A|B) = P(A)P(B|A)$$
And solving the conditional probability we obtain that: 
$$P(A|B) = \frac{P(A)P(B|A)}{P(B)}$$
which is known as the **Bayes's Theorem**. 
### (Discrete) Random Variables
A **(discrete) random variable** $X$ is a function from a finite (or countably infinite) sample space $S$ to the real numbers. 
It associates a real number with each possible outcome of an experiment, which allows us to work with the probability distribution induced on the resulting set of numbers. 

For a random variable $X$ and a real number $x$ we define the event $X = x$ to be the event $\{s \in S : X(s) = x\}$, and thus 
$$P(X = x) = \Sigma_{s \in S:X(s) = x}\ P(s)$$
**Example:**
Say we roll a pair of $6$-sided dice. There are $36$ outcomes in the sample space $S$. 
The dices are fair, so the probability distribution is uniform: each outcome $s\in S$ is equally likely with probability $\frac{1}{36}$.

Let's define the random variable $X$ to be the maximum of the two values showing on the dice. 
Now we can use $X$ to compute the probability of events such as "the max value between the two dices is $3$", by just computing $P(X=3)$, which is $\frac{5}{36}$ as there are $5$ outcomes where $3$ is the maximum number. 
#### Expected Value
The most useful summary of the distribution of a random variable is the "average" of the values it takes on. 
The **expected value** of a discrete random variable $X$ is: 
$$E[X] = \Sigma_x\ x\cdot P(X = x)$$
**Example:**
Consider a game in which you flip two fairs coins. 
You earn $3$$ for each head but lose $2$$ for each tail. 
The expected value for a random variable $X$ representing your earning is: 
$$
\begin{align}
E[X] = 6\cdot P(HH) + 1 \cdot P(HT) - 4\cdot P(TT) = 6\cdot \frac{1}{4} + 1\cdot \frac{1}{2} - 4\cdot \frac{1}{4} = 1
\end{align}
$$

The expected value has the following properties: 
1) **linearity:** $E[X + Y] = E[X] + E[Y]$ 
2) $E[\alpha X] = \alpha E[X]$
3) if two variables $X, Y$ are independent and each has a defined expectations then $E[XY]=E[X]E[Y]$ 

When a random variable $X$ takes on values from $\mathbb{N}$ we have a formula for its expectations: 
$$E[X] = \Sigma_{i=1}^\infty \ P(X \geq 1)$$
##### Variance and Standard Deviation 
**The expected value of a random variable does not express how "spread out" the variable values are.**
The notion of **variance** mathematically express how far from the mean a random variable's values are likely to be. 
The variance of a random variable $X$ with mean $E[X]$ is defined as: $$Var[X] = E[X^2] - E^2[X]$$We can also show that $E[X^2] = Var[X] + E^2[X]$. 

The variance of a random variable $X$ and the variance of $\alpha X$ are related: 
$$Var[\alpha X] = \alpha^2 Var[X]$$
When $X$ and $Y$ are independent random variables we have: 
$$Var[X +Y] = Var[X] + Var[Y]$$
The **standard deviation** of a random variable $X$, denoted by $\sigma$, is the nonnegative square root of the variance of $X$. 
### Indicator Random Variables
In order to analyze many algorithms we use **indicator random variables**. 
Indicator random variables provide a convenient method for converting between probabilities and expectations. 
Given a sample space $S$ and an event $A$, the **indicator random variable** $I(A)$ associated with the event $A$ is defined as: 
$$
I(A) = 
\begin{cases}
1\ \ \ \text{if $A$ occurs} \\
0\ \ \ \text{if $A$ do not occurs}
\end{cases}
$$
Another notation is the following:
$$
X_i = 
\begin{cases}
1\ \ \ \text{event $i$ occur with probability $p$} \\
0\ \ \ \text{event $i$ don't occur, with probability $1-p$}
\end{cases}
$$
We can compute the expected value of indicator variables: $E[X_i] = 1\cdot p + 0\cdot (1-p)$
If we define a random variable $X = \Sigma_{i=1}^t X_i$ we obtain that 
$$
E[X] = \Sigma_{i=1}^t E[X_i] = \Sigma_{i=1}^tP(X_i = 1) = t\cdot p
$$
Said easy: **the expected value of an indicator random variable associated with an event is equal to the probability that event occurs.**
# Las Vegas vs Monte Carlo
In the context of **probabilistic algorithms** we have two categories: 
- **Las Vegas Algorithms:**
	- no errors, but the running time is probabilistic, very good w.h.p (with high probability)
	- e.g.: QuickSort
- **Monte Carlo Algorithms:**
	- $1$-sided / $2$-sided errors (false positive/negatives or both), running time is worst-case
	- e.g.: Karp-Rabin Fingerprint
# Random Permutation
Let's see how we can randomly permute an array of $n$ elements. 
The goal is to produce a **uniform random permutation**, that is,, a permutation that is as likely as any other permutation. 
To do so we need a function `rand(a,b)` that returns at random an integer in the interval $[a,b]$, where each element $i$ has probability of being picked equal to $\frac{1}{b-a+1}$. 
Mind that in practice we obtain a **pseudo-random** choice, as truly random is undecidable. 

To obtain a random permutation we then use the following function: 
```java
void randomPermutation(int[] array){
	int n = array.length(); 
	for(int i = 1; i < n; i++)
		swap(array[i], array[rand(i,n)]);
}
```
It can be proved, using indicator variables, that each permutation is generated with a probability very close to $\frac{1}{n!}$

**A randomized algorithm is often the simplest and most efficient way to solve a problem.**
Being able to produce random permutations in a very efficient way is then crucial.
# The Hiring/Headphones Problem
You need to hire a new assistant. The employment agency send you a list of candidates, and you interview them starting from the first of the list.
You must pay the employment agency a small fee to interview an applicant. 
To actually hire an assistant is more costly, however, since you must first fire your current assistant and pay a substantial hiring fee to the agency. 
Nonetheless you are committed to having, at all times, the best possible person for the job. 
Therefore you decide that after interviewing each applicant, if that applicant is better than the current assistant, you will fire the current assistant and hire the new applicant. 

**This is a first example where the randomization is a way to improve the complexity, in the average case.**
If we use the order given by the list the cost is predetermined and it's easy to compute, but it turns out that, in the average case, we can improve the complexity by creating a random permutation of the assistants, using the function seen before.

Let $X$ be the random variable whose value equals the number of times you hire a new assistant. 
We could then apply the definition of expected value $E[X] = \Sigma_{x=1}^n x\cdot P(X = x)$ but this calculation is quite difficult to compute. 
We instead exploit the random indicator variables. 

Let $X_i$ be the indicator random variable associated with the event in which the $i$-th candidate is hired: 
$$
X_i = 
\begin{cases}
1\ \ \ \text{candidate $i$ is hired with probability $p_i$} \\
0\ \ \ \text{candidate $i$ is not hired, with probability $1-p_i$}
\end{cases}
$$
We then see that $X = X_1 + X_2 + \dots + X_N$

We notice that $p_i$ is the probability that the $i-th$ candidate is better than all the previous $i-1$ candidates (and therefore he gets hired) 
We can then compute $p_i$
$$p_i= \frac{\text{all candidates so far but the last is the best seen}}{\text{all candidates so far}} = \frac{(i-1)!}{i!} = \frac{1}{i}$$

We can then use $X = \Sigma_{i=1}^n X_i$ and compute its expected value:
$$E[X] = \Sigma_{i=1}^n E[X_i] = \Sigma_{i=1}^n \frac{1}{i} \sim \ \text{harmonic series:} \log(n) $$
# The Birthday Paradox
The probability problem asks for the probability that, in a set of $m$ randomly chosen people, at least two will share a birthday.
The **birthday paradox** refers to the counterintuitive fact that only $23$ people are needed for that probability to exceed $50\%$. 

We have $n = 365$ days. 
Given a person $i$ and a person $j$, with $i \neq j$,  let's define indicator variables
$$
X_{ij} = 
\begin{cases}
1\ \ \ \text{$i$ and $j$ have the same birthday, with probability $p$ } \\
0\ \ \ \text{otherwise, with probability $1-p$}
\end{cases}
$$
Every person has probability of being born in a day $k$ equal to $1/n$. 
Then $P(i\ \text{born on day k}\ \  \cap \ j\ \text{born on day k}) = \frac{1}{n}\cdot \frac{1}{n}$ as the two events are independent.
Thus we have: 
$$E[X_{ij}] = p = \Sigma_{k=1}^n \frac{1}{n}\frac{1}{n} = \Sigma_{k=1}^n \frac{1}{n^2} = \frac{1}{n}$$
Let's now consider $m$ as the number of people we choose. 
We define $X = \Sigma_{i=1}^m\Sigma_{j = i+1}^m X_{ij}$ as the number of pairs of people among $m$ that have the same birthday. 
Therefore we have: 
$$
E[X] = \Sigma_{i =1}^m\Sigma_{j=i+1}^m E[X_{ij}] = \binom{m}{2}\frac{1}{n} = \frac{m(m-1)}{2}\frac{1}{n}
$$
And $E[X] \geq 1$ holds when $m(m-1) \geq 2n \implies m \sim \sqrt{2n}$. 
Since $n = 365$ we have $m \sim 27$. 
# Randomized QuickSort
To show how randomization can improve drastically the performance on the average case (and the **expected case**) we show quick sort and its randomized version.
## QuickSort
QuickSort applies the divide-and-conquer method for sorting a subarray $A[p:r]$
- **Divide** by partitioning (rearranging) the array $A[p:r]$ into two, possibly empty, subarrays $A[p:q-1]$ (aka the **low side**) and $A[q+1:r]$ (aka the **high side**) such that each element in the low side of the partition is less than or equal to the **pivot** $A[q]$, which is in turn less than or equal to each element in the high side. Compute the index $q$ of the pivot as part of this partitioning procedure. 
- **Conquer** by calling quicksort recursively to sort each of the subarrays $A[p:q-1]$ and $A[q+1:r]$ 
- **Combine** by doing nothing

We can then write in pseudocode the procedure that implement quicksort. 
To sort an entire $n$-element array $A[1:n]$ the initial call is `quicksort(A, 1, n)`
```java
void quicksort(int A[], p, r){
	if(p < r){
		// partition around the pivot, wich ends up in A[q]
		q = partition(A, p, r);
		quicksort(A, p, q-1); // recursively sort the low side
		quicksort(A, q+1, r); // recursively sort the high side
	}
}
```

The key of the algorithm is the **partitioning step**, which rearranges the subarray $A[p:r]$ in place, returning the index of the dividing point between the two sides of the partition. 
```java
int partition(int A[], p, r){
	// the pivot: the last element of the current subarray
	int x = A[r]; 
	// highest index into the low side
	int i = p-1; 
	// process each element other than the pivot
	for(int j = p; j < r; j++) 
		// does this element belong to the low side?
		if(A[j] <= x){ 
			 // index of a new slot on the low side
			i = i+1;
			// put this element there
			swap(A[i], A[j]) 
		}
	// the pivot just go the right of the low side
	swap(A[i+1], A[r]) 
	// new index of the pivot
	return i+1 
}
```
Mind that `i` is the index where we put the "current" element smaller than the pivot. 
### Performance of QuickSort
The running time of QuickSort depends on how balanced each partitioning is, which in turn depends on which elements are used as pivots. 
If the two sides of a partition are about the same size (aka the partitioning is balanced) then the algorithm runs asymptotically as fast as MergeSort. 
On the other hand, if the partitioning is unbalanced the performance are asymptotically similar to InsertionSort. 
#### Worst-Case Partitioning 
The worst-case behavior for QuickSort occurs when the partitioning produces one subproblem with $n-1$ elements and one with $0$ elements. 
Let us assume that this unbalanced partitioning arises in each recursive call. 
The partitioning costs $\Theta(n)$ time. 
Since the recursive call on an array of size $0$ returns without doing anything, $T(0) = \Theta(1)$, and the recurrence for the running time is: 
$$
T(n) = T(n-1)+ T(0) + \Theta(n) = T(n-1) +\Theta(n)
$$
but we know, thanks to our assumptions, that $T(n-1) = T(n-2) + \Theta(n-1)$, and so on until we reach $T(n-n) = T(0)$. 

Summing all the costs incurred at each level of the recursion we obtain an arithmetic series which evaluates to $\Theta(n^2)$. 
Thus, if the partitioning is maximally unbalanced at every recursive level of the algorithm, the running time is $\Theta(n^2)\ \ \square$
## Randomized QuickSort 
Instead of always using $A[r]$ as the pivot, the randomized QuickSort randomly chooses the pivot from the subarray $A[p:r]$, where each element has an equal probability of being choses. 
It then exchanges that element with $A[r]$ before partitioning. 
Because the pivot is chosen randomly we expect the split of the input array to be reasonably balanced on average.

```
randomized-partition(A, p, r)
	i = rand(p, r)
	swap(A[r], A[i])
	return partition(A, p, r)

randomized-quicksort(A, p, r)
	if p < r
		q = randomized-partition(A, p, r)
		randomized-quicksort(A, p, q-1)
		randomized-quicksort(A, q+1, r)
```
### Analysis of RQS
We compute the cost of the RQS counting the number of comparison between the elements of the array: a comparison costs $\Theta(1)$, hence the number of comparisons gives the time complexity of the whole algorithm. 

1) For the purpose of this analysis the output of `randomized-quicksort(A, p, r)` is $z_1 < \dots < z_n$, we index the elements in $A$ by their position in the sorted output, rather than the position in the input. We denote the set $\{z_i, \dots, z_j\}$ with $Z_{ij}$
2) When two keys $z_i$ and $z_j$ are compared? When one of them is chosen as pivot
3) How many times $z_i$ and $z_j$ are compared? At most once, since the pivot are removed from future comparisons (at the end of the partition the pivot is in its rightful place)
4) $z_i$ and $z_j$ are compared: $|A[p:q]| \geq j-i+1$ since at least all of $z_i, \dots, z_j$ are in $A[p:q]$

We can now define:
$$
X_{ij\ |\ i < j} = 
\begin{cases}
1\ \ \ \text{$z_i$ and $z_j$ are compared at any time} \\
0\ \ \ \text{otherwise}
\end{cases}
$$
So that we can define $$X = \Sigma_{i=1}^n\Sigma_{j=i+1}^n\ X_{ij}$$as the number of comparisons in the execution of `randomized-quicksort(A, 1, n)`
This is thanks to the fact that $z_i$ and $z_j$ are compared at most once. 

We now want to compute $E[X]$. 
We know that $X_{ij}$ are indicator variables: 
$$
\begin{align}
E[X_{ij}] &= \\
& = P(X_{ij} = 1) \\
& = P((z_i, z_j \in Z_{ij}) \cap  (z_i\ \text{or}\ z_j\ \text{is the pivot for}\ A[p:q])) \text{, and since}\ P(A \cap B) \leq P(B) \\
& \leq P(z_i\ \text{or}\ z_j\ \text{is the pivot for}\ A[p:q]) \\
& = \frac{2}{|A[p:q]|} \\
& \leq \frac{2}{j-i+1}
\end{align}
$$
Now we can compute the expected value of $X$: 
$$
\begin{align}
E[X] &= \\
& =\Sigma_{i=1}^{n-1}\Sigma_{j=i+1}^n E[X_{ij}], \text{and since}\ E[X_{ij}] \leq \frac{2}{j-i+1} \\ 
& = \Sigma_{i=1}^{n-1}\Sigma_{k=1}^{n-i}\ \frac{2}{k+1}, \text{change of variable}  \\
& \leq \Sigma_{i=1}^{n-1}\Sigma_{k=1}^n \frac{2}{k} \\
& = \Sigma_{i=1}^{n-1}O(\log(n)) \\
& = O(n\log(n))\
\end{align}
$$
$\square$
# Karp-Rabin Fingerprint
**How to check equality of files?**
It can be done deterministically, but it is very slow for large files. 

We can se a file as a binary string $s = 01\dots1\dots0$, with $w = |s|$, 
$s$ can also be seen as a huge number $\in [0, 2^n -1]$. 

Given another file/sequence $s'$, can we check $s = s'$?
Yes, it can be done in $O(n)$ time, using the Karp-Rabin Fingerprint.

We define a fingerprint function $F$ that produces a number for a given sequence/number $s$ $$F(s) = s\ \text{mod}\ p$$for a randomly chosen prime $p$. 

There is the issue of the **collision**, given two sequences/files $k_1, k_2 \in [0\dots 2^n -1]$ we have this two cases: 
$$
\begin{align}
& F(k_1) \neq F(k_2) \implies k_1 \neq k_2 \\
& F(k_1) = F(k_2) \implies \begin{cases}k_1 = k_2 \\ k_1 \neq k_2\ \text{1-sided error with a given probability}\end{cases}
\end{align}
$$
$1$-sided **error**: $k_1 \neq k_2 \land F(k_1) = F(k_2)$. 

**Idea:** before starting a computation we
- choose a parameter $\tau$ *sufficiently large* (see later)
- choose uniformly and randomly a prime number in $[2\dots \tau]$
so that the probability of error is very low.

Let's consider the case $F(k_1) = F(k_2) \implies k_1\ \text{mod}\ p = k_2\ \text{mod}\ p$. 
We call such a prime $p$ a **bad prime**. 
$$
\begin{align}
P(\text{error}) & \\  
& = P_{p\leq \tau}(k_1 \neq k_2 \land F(k_1) = F(k_2))\\ 
& = \frac{\text{number of bad primes}\leq \tau}{\text{primes p}\leq \tau}  \\
& = \frac{?}{\tau/\log(\tau)}
\end{align}
$$
To complete the computation of $P(\text{error})$ we considering the following results: 
- **Observation:** both $k_1$ and $k_2$ require $n$ bits for being represented. 
- **Theorem:** the number of distinct prime divisors on any number less than $2^n$ is at most $n$. 
	- **Proof:** each prime number is greater than $1$. If a number $n$ has more than $t$ distinct prime divisors, then $n \geq 2^t$. If $n$ has more than $t$ prime divisors then $n = d_1 \cdot \dots d_{t+1}$, where each $d_i \geq 2$, hence $n \geq 2^t$

By the previous theorem we get that for any integer $k$ of $n$ bits there are at most $n$ primes in its prime factorization. 
Thus: there are at most $n$ bad primes (in common for two of the files/numbers $k_1, k_2$ of same length)

Therefore:
$$
\begin{align}
P(\text{error}) &= \\  
& = P_{p\leq \tau}(k_1 \neq k_2 \land F(k_1) = F(k_2)) \\ 
& = \frac{\text{number of bad primes}\leq \tau}{\text{primes p}\leq \tau} \\
& = \frac{?}{\tau/\log(\tau)} \\
& \leq \frac{n}{\tau/\log(\tau)} \\
& \triangleright \ \text{since}\ \frac{\tau}{\log(\tau)} = n^{c+1},\ \text{we choose}\ \tau \sim (n^{c+1}\log(n))\ \text{and we get} \\
& = \frac{1}{n^c}
\end{align}
$$
Where $c$ is an arbitrary constant. 
We can choose a $\tau$ *sufficiently large* so that $c$ is big enough to guarantee a very low error probability $\square$
# Pattern Matching
Let's consider the problem of pattern matching in strings. A **text** is a string $X = x_1x_2\dots x_n$ and a **pattern** is a string $Y = y_1y_2\dots y_m$, both over a fixed finite alphabet, such that $m \le n$.
We restrict, without losing generality, the alphabet $\Sigma$ to $\{0,1\}$. 
The pattern occurs in the text if there is a $j \in \{1,2,\dots,\ n-m+1\}$ such that for $i \in [1, m]$ we have $x_{j+i-1} = y_i$. 

**The pattern matching problem is that of finding an occurrence (if any) of a given pattern in the text.**
The problem can be trivially solved in $O(nm)$ time trying for a match at all locations i. 
We describe a Monte Carlo algorithm that achieves a running time of $O(n+m)$, and later we will present the same algorithm in a Las Vegas fashion. 

**Monte Carlo:**
Let's define the string $X(j) = x_jx_{j+1}\dots x_{x+m-1}$ as the substring of length $m$ in $X$ that starts at position $j$. 
A match occurs if there is a choice of $j$, for $j \in [1, n-m+1]$, for which $Y = X(j)$. 
We make the solution unique by requiring that the algorithm find the smallest value of $j$ such that $X(j) = Y$. 

We choose a fingerprint function $F$ seen before and compare $F(Y)$ with each of the fingerprints $F(X(j))$. 
An error occurs if $F(Y) = F(X(j)) \land Y \neq X(j)$, which is a one-sided error, a **false positive.**

We interpret the strings $Y$ and $X(j)$ as $m$-bit integers, and compare their fingerprints $F_p(Y)$ and $F_p(X(j))$ instead of trying to match each symbol in the two string.

The only possible error is that we get the same fingerprint when $Y \neq X(j)$, and as before
$$
\begin{align}
P(\text{error}) &= \\
& = \text{probability of collision}\ \cdot \ \text{number of patterns} \\
& \le \frac{m}{\tau\log(\tau)} \cdot (n-m+1) \\ 
& \le \frac{nm}{\tau\log(\tau)} \\ 
& \le \frac{n^2}{\tau\log(\tau)} \\
& \le \frac{1}{n^c},\ \text{with}\ \tau \sim n^{c+2}\log(m)
\end{align}
$$
**Las Vegas:**
To build the Las Vegas we simply do some modifications to the previous algorithm. 
Whenever a match occurs between $F(Y)$ and some $F(X(j))$, we compare the strings $Y$ and $X(j)$ in $O(m)$ time. 

If this is a false match, we detect it and abandon the whole process in favor of using the brute-force $O(nm)$ time algorithm. 
This means that when the fingerprints are equals but $Y \neq X(j)$ we switch to the trivial algorithm. 
As usual, the expected cost is the same of the Monte Carlo version, but the worst case is given by the brute-force cost. 
# Union Bound
The union bound, says that for any finite or countable set of events, **the probability that at least one of the events happens is no greater than the sum of the probabilities of the individual events.** 
**This inequality provides an upper bound on the probability of occurrence of at least one of a countable number of events in terms of the individual probabilities of the events.**
$$P(A\cup B) \leq P(A) + P(B)$$
