# Algorithm Design 22/23

## Mathematical Background
### Counting
#### Permutations
A **permutation** of a finite set $S$ s a **ordered** sequence of all the elements in $S$, with each element appearing exactly once. 
For example, with $S = \{a, b, c\}$ we have $6$ permutations: $abc, acb, bac, bca, cab, cba$. 

For a set $S$ of $n$ elements we have $n!$ permutations, since there are $n$ ways to choose the first element of the sequence, $n-1$ ways of choosing the second element and so on. 

A **k-permutation** of $S$ is an **ordered** sequence of $k$ elements of $S$, with no element appearing more than once, and with $k < |S| = n$. 
We can say that a classic permutation is a $n$-permutation of the set $S$. 

The number of $k$-permutations of a $n$-set is: 
$$n(n-1)(n-2)\dots(n-k+1)= \frac{n!}{(n-k)!}$$
#### Combinations
A **k-combination** of an $n$-set $S$ is simply a $k$-**subset** of $S$. 
For example, the $4$-set $\{a,b,c,d\}$ has $6$ $2$-combinations: $ab, ac, ad, bc, bd, cd$.
It is then clear that with combinations **the order do not matters**.

We can express the number of $k$-combinations of an $n$-set in terms of the number of $k$-permutations of an $n$-set.
Every $k$-combination has exactly $k!$ permutations of its elements, each of which is a distinct $k$-permutation of the $n$-set itself. 
Thus the number of $k$-combinations of a $n$-set is the number of $k$-permutations divided by $k!$

From the formula seen above about $k$-permutations we have that: $$k\text{-combinations} = \frac{n!}{k!(n-k)!}$$
#### Binomial Coefficient
The notation $\binom{n}{k}$ denotes the number of $k$-combinations of an $n$-set. 
So we know that: $$\binom{n}{k} = \frac{n!}{k!(n-k)!}$$
The binomial coefficient is symmetric in $k$ and $n-k$: 
$$\binom{n}{k} = \binom{n}{n-k}$$
### Probability
We define the **probability** in terms of a **sample space** $S$, which is a set whose elements are called **outcomes** or **elementary events**. 
An **event** is a subset of the sample space $S$. 

The event $S$ is called **certain event**, and the event $\emptyset$ is called the **null event**. 
We say that two events $A, B$ are **mutually exclusive** if $A \cap B = \emptyset$. 

An outcome $s \in S$ also define an event $\{s\}$, which we sometimes write as just $s$. 
By definition **all outcomes are mutually exclusive.**
#### Axioms of Probability
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
#### Discrete Probability Distribution
A **probability distribution** is **discrete** if it is defined over a finite (or countably infinite) sample space. 
Let $S$ be a finite sample space, then for any event $A \subseteq S$ we have 
$$P(A) = \Sigma_{s\in A}\ P(s)$$
since outcomes, specifically those in$A$, are mutually exclusive. 

If $S$ is finite and every outcome $s \in S$ has $P(s) = \frac{1}{|S|}$ we say that we have a **uniform probability distribution** on $S$. 
#### Conditional Probability and Independence
Conditional probability formalizes the notion of having prior partial knowledge of the outcome of an experiment. 
The **conditional probability** of an event $A$ given that another event $B$ occurs is defined as 
$$P(A|B)= \frac{P(A\cap B)}{P(B)}$$
whenever $P(B) \neq 0$. 

Two events are said **independent** if $P(A\cap B) = P(A)P(B)$. 
Given two independent events $A$ and $B$ with $P(B) \neq 0$, then we have that $P(A|B) = P(A)$. 
#### Bayes's Theorem
From the conditional probability and the commutative law $A\cap B = B \cap A$ it follows that for two events $A$ and $B$, each with non-zero probability, we have:
$$P(A\cap B) = P(B)P(A|B) = P(A)P(B|A)$$
And solving the conditional probability we obtain that: 
$$P(A|B) = \frac{P(A)P(B|A)}{P(B)}$$
which is known as the **Bayes's Theorem**. 
#### (Discrete) Random Variables
A **(discrete) random variable** $X$ is a function from a finite (or countably infinite) sample space $S$ to the real numbers. 
It associates a real number with each possible outcome of an experiment, which allows us to work with the probability distribution induced on the resulting set of numbers. 

For a random variable $X$ and a real number $x$ we define the event $X = x$ to be the event $\{s \in S : X(s) = x\}$, and thus 
$$P(X = x) = \Sigma_{s \in S:X(s) = x}\ P(s)$$
**Example:**
Say we roll a pair of $6$-sided dice. There are $36$ outcomes in the sample space $S$. 
The dices are fair, so the probability distribution is uniform: each outcome $s\in S$ is equally likely with probability $\frac{1}{36}$.

Let's define the random variable $X$ to be the maximum of the two values showing on the dice. 
Now we can use $X$ to compute the probability of events such as "the max value between the two dices is $3$", by just computing $P(X=3)$, which is $\frac{5}{36}$ as there are $5$ outcomes where $3$ is the maximum number. 
##### Expected Value
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
###### Variance and Standard Deviation 
**The expected value of a random variable does not express how "spread out" the variable values are.**
The notion of **variance** mathematically express how far from the mean a random variable's values are likely to be. 
The variance of a random variable $X$ with mean $E[X]$ is defined as: $$Var[X] = E[X^2] - E^2[X]$$We can also show that $E[X^2] = Var[X] + E^2[X]$. 

The variance of a random variable $X$ and the variance of $\alpha X$ are related: 
$$Var[\alpha X] = \alpha^2 Var[X]$$
When $X$ and $Y$ are independent random variables we have: 
$$Var[X +Y] = Var[X] + Var[Y]$$
The **standard deviation** of a random variable $X$, denoted by $\sigma$, is the nonnegative square root of the variance of $X$. 
#### Indicator Random Variables
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
$$P(A\cup B) \leq P(A) + P(B)$$We will often refer to the union bound with UB.
# Universal Hash Family
There are data structures (e.g., hash tables) and algorithms (e.g. bloom filters, see later on) that uses hash functions as key ingredient. 
In those situation we need a *good* hash function.
Along with being efficiently computable, what properties a good hash function have?
How you design good hash functions? 

We first define that an hash function $h$ maps the universe $U$ of keys to a smaller set $$h: U \rightarrow \{0, 1,\ \dots\ m-1\}$$We will often use the notation $[m]$ to represent $\{0,\ \dots,\ m-1\}$. 

An "ideal" hash function $h$ would have, for each possible input $k$, an output $h(k)$ that is an element randomly and independently chosen uniformly in the range $[0, m-1]$. 
Once a value $h(k)$ is randomly chosen, each subsequent call to $h$ with the same $k$ yields the same output $h(k)$. 
We call such an ideal hash function an **independent uniform hash function**. 
Such hash function do not exists but we will analyze the hashing under the assumption of independent uniform hash functions, and then present ways of achieving useful practical approximations. 

Given $\mathcal{H}$ a family of hash functions, each of the form $h: U \rightarrow [m]$, we say that
- $\mathcal{H}$ is **uniform** if for any key $k \in U$ and for any slot $q \in [m]$, the probability that $h(k) = q$ is $\frac{1}{m}$
- $\mathcal{H}$ is **universal** if for any distinct keys $k_1$ and $k_2$ in $U$, the probability that $h(k_1) = h(k_2)$, that is the probability of having a collision, is at most $\frac{1}{m}$

More specifically, the number of $h$ such that there is a collision for two distinct keys $k_1, k_2$ is $\frac{|\mathcal{H}|}{m}$.
Then: 
$$
P(\text{collision}) = \frac{\text{number of bad choices of $h$ in $\mathcal{H}$}}{\text{number of $h$ in $\mathcal{H}$}} \le \frac{|\mathcal{H}|/m}{|\mathcal{H}|} = \frac{1}{m}
$$

Let's now consider the family $\mathcal{H}$ of hash functions, where each $h \in \mathcal{H}$ is defined as
$$h_{a,b}(x) = ((ax+b)\ \text{mod}\ p)\ \text{mod}\ m$$
where: 
- $a, b$ are chosen at random, with: 
	- $a \in \mathbb{Z}_p^+ = \{1,2,\ \dots, p-1\}$
	- $b \in \mathbb{Z}_p = {\{0,1,\ \dots, p-1\}}$
- $m$ is provided by the user
- $p$ is a prime number in $[m+1,\ \dots,\ 2m]$

The family of all such hash functions is $$\mathcal{H}_{pm} = \{h_{ab}: a \in \mathbb{Z}_p^+\ \text{and}\ b\in \mathbb{Z}_p\}$$where each hash function $h_{ab}$ maps $\mathbb{Z}_p$ to $\mathbb{Z}_m$. 

Since we have $p-1$ choices for $a$ and $p$ choices for $b$, the collection $\mathcal{H}_{pm}$ contains $p(p-1)$ hash functions. 
We can draw, uniformly at random, a choice of $h_{a,b}\in \mathcal{H}$ with a probability $\frac{1}{|\mathcal{H}|} = \frac{1}{p(p-1)}$

**Theorem:** the class $\mathcal{H}_{pm}$ is universal. 
**Proof:** Consider two distinct keys $k, l$ from $\mathbb{Z}_p$. For a given hash function $h_{ab}$ we let 
$$
\begin{align}
&r = (ak + b)\ \text{mod}\ p \\
&s = (al + b)\ \text{mod}\ p 
\end{align}
$$
From a known theorem, since $p$ is the same, we can subtract the congruences: 
$$
\begin{align}
r-s &\equiv ak+b-al-b\ \text{mod}\ p \rightarrow \\  
\rightarrow r -s &\equiv ak-al\ \text{mod}\ p \rightarrow \\
\rightarrow r -s &\equiv a(k-l)\ \text{mod}\ p
\end{align}
$$
Now, by hypothesis we have: 
$\bullet \ \ a \ne 0$ as $a\in\mathbb{Z}_p^+$ 
$\bullet \ \ k \ne l$
$\bullet \ \ k, l \in [0, p-1] \implies$ $k$ and $l$ can not be divided by $p$, therefore $(k-l)\ \text{mod}\ p \ne 0$

Since we know that $a \ne 0$ and $(k-l) \ne 0$ modulo $p$ we derive that $a(k-l)\ \text{mod}\ p \ne 0$, hence $(r-s)\ \text{mod}\ p \ne 0$. 
We can then conclude that $r \ne s$. 

Therefore, when computing any $h_{ab}\in\mathcal{H}_{pm}$, distinct inputs $k$ and $l$ map to distinct values $r$ and $s$ modulo $p$; there are no collisions yet at the "mod $p$ level". 
Moreover, each of the possible $p(p-1)$ choices of the pair $(a,b)$ with $a\ne0$ yields a different resulting pair $(r,s)$ with $r\ne s$, since we can solve for $a$ and $b$, given $r$ and $s$: 
$$
\begin{align}
a &= ((r -s)((k-l)^{-1}\ \text{mod}\ p))\ \text{mod}\ p \\
b &= (r - ak)\ \text{mod}\ p
\end{align}
$$
where $((k-l)^{-1}\ \text{mod}\ p)$ denotes the unique multiplicative inverse, modulo $p$, of $k-l$. 

Since there are only $p(p-1)$ possible pairs $(r,s)$ with $r\ne s$, there is a one-to-one correspondence between pairs $(a,b)$ with $a\ne0$ and pairs $(r,s)$ with $r\ne s$. 
Thus, for any given pair of inputs $k$ and $l$, if we pick $(a,b)$ uniformly at random from $\mathbb{Z}_p^+ \times \mathbb{Z}_p$, the resulting pair $(r,s)$ is equally likely to be any pair of distinct values modulo $p$. 

Therefore, the probability that distinct keys $k$ and $l$ collide is equal to the probability that $r\equiv s\ (\text{mod}\ m)$ when $r$ and $s$ are randomly chosen as distinct values modulo $p$. 

For a given value of $r$, of the $p-1$ possible remaining values for $s$, the number of values $s$ such that $s \ne r$ and $r\equiv s\ (\text{mod}\ p)$ is at most
$$
\begin{align}
\lceil p/m \rceil -1 &\leq ((p+m-1)/m)-1\ \star \\
&=(p-1)/m
\end{align}
$$
Where $\star$ is given by the known inequality
$$
\lceil a/b \rceil \leq \lceil (a+(b-1))/b \rceil
$$
The probability that $s$ collides with $r$ when reduced modulo $m$ is at most $\frac{1}{m}$.

Therefore, for any pair of distinct values $k,l \in \mathbb{Z}_p$, we have $$P(h_{ab}(k) = h_{ab}(l)) \le \frac{1}{m}$$so that $\mathcal{H}_{pm}$ is indeed universal $\square$
# Markov's Inequality
**Markov's Inequality gives an upper bound for the probability that a non-negative function of a random variable is greater or equal to some positive constant.**
Markov's inequality (and other similar inequalities) relate probabilities to expectations, and provide (frequently loose but still useful) bounds for the cumulative distribution function of a random variable.

If $X$ is a non-negative random variable and $a >0$, then the probability that $X$ is at least $a$ is at most the expectation of $X$ divided by $a$.
In symbols: 
$$P(X\geq a) \leq \frac{E[X]}{a}$$
# Cuckoo Hashing
A **dictionary** is a data structure for storing a set of items, that support three basic operations: 
- $lookup(x)$, which returns $true$ if $x$ is in the current set, $false$ otherwise
- $insert(x)$, which adds the item $x$ to the current set if not already present
- $delete(x)$, which removes the item $x$ from the current set if present

A simple but not efficient way of implementing a dictionary is a linked list, where: 
- $lookup(x)$ cost $O(n)$
- $insert(x)$ cost $O(n)$ as first we have to check that $x$ is not already in the list
- $delete(x)$ cost $O(n)$

We now present the **cuckoo hashing**, **a way of implementing a dictionary where the three operations are constant** **worst-case.**
As always, the problem with hashing are collisions. 
In cuckoo hashing they are handled by using **two different hash functions** $h_1, h_2$ picked at random from an universal hash family $\mathcal{H}$. 
Instead of requiring that $x$ is stored at a position $h(x)$, for any key $x$ we have two alternatives: we insert $x$ in $h_1(x)$ or in $h_2(x)$. 

What happens when the positions $h_1(x)$ and $h_2(x)$ are already occupied? 
We **throw out** the current value $y$ at $h_1(x)$ and we store there $x$.
At this point we use $h_2(y)$ to find if there is a suitable alternative for $y$. If the alternative position for $y$ is vacant then we are good. 
Otherwise we do for $y$ what we just did for $x$: throw out the current occupant $z$ of $h_2(y)$ and try to find a place for $z$. 
This is continued until the procedure finds a vacant position or has taken too long. 
In the latter, new hash functions are chosen in $\mathcal{H}$ and the whole data structure is rebuilt, or **rehashed**. 

The operations $lookup(x)$ and $delete(x)$ are clearly $O(1)$ worst-time. 
$insert(x)$ creates a path from the first node $h_1(x)$ to some node $j$ where we insert $x$. 
The cost is then the length of the path, but insertion can also cause the rehashing of the whole table.
## Insertion Cost
We choose $h_1, h_2$ independently and uniformly at random from the universal hash family $$\mathcal{H} = \{((ax+b)\ \text{mod}\ p)\ \text{mod}\ m\ : p > m, a \in \mathbb{Z}_p^+, b\in \mathbb{Z}_p\}$$In particular, given the key $x\in U$ and $i, j \in [m]$ we have that $$P(h_1(x) = i \land h_2(x) = j)\leq \frac{\lceil p/m\rceil^2}{(p-1)p} \sim \frac{1}{m^2}\ \ \ \star$$$\star:$ Take it as a known theorem. 
To remember that $P(h_1(x) = i \land h_2(x)) \le \frac{1}{m^2}$ you can think that 
- $P(h_1(x) = i) \le 1/m$
- $P(h_2(x) = j) \le 1/m$  
- for two are independent events $A, B$ we have that $P(A \land B) = P(A)P(B)$

Now, consider the set $S$ of keys and the hash functions $h_1, h_2$. 
Conceptually we build an undirected graph $G=(V,E)$ where $|V|=m$ and $|E|=n$, and:
- the **vertices** are in $V = \{0,1,\dots,m-1\}$ and represent the table positions
- the **edges** are random: $E = \{(h_1(x), h_2(x)) : x \in S\}$ 
	- $G$ is actually a multigraph: two vertices can be connected by multiple edges. 

**Consider the insertion** of a new key $x$, which corresponds to a new edge $e = (h_1(x), h_2(x))$ in $G$. 
At this point one of three situations may happen: 
1) one of the table positions in $h_1(x)$ or $h_2(x)$ is free, and $x$ is placed there: $O(1)$
2) the positions are taken, so the insertion follows a path in $G$ throwing out keys till a free position is found
3) as in the previous case, but here we traverse a cycle, which means that we have to rehash the whole table. 

We need to analyze **2)** and **3)**: the goal is $O(1)$ expected time. 
We assume that $m$ (number of buckets, the table's size) is $>$ than $2cn$ ($|S|=n$) for a constant $c > 2$.
### Case 2: A Free Position is Eventually Found
Let $i$ be the starting position (the position where $x$ "should have been placed"), and $j$ the ending position (the position where $x$ is actually placed) in the path. 
We say that $k$ is the length of the path $i \rightarrow j$ in $G$. 

**Lemma:**
For any position $i, j$, the probability that exists a path $i\rightarrow j$ of length $\geq 1$ (which is also the shortest path from $i$ to $j$) is at most $\frac{1}{c^km}$. 
Alternatively said: $$P(\exists\ \text{the path}\ i\rightarrow j\in G\ \text{of length}\ k) \le\frac{1}{c^km}$$**Proof:**
We prove it by induction on $k$.
**base case:** $k =1$, $i\rightarrow j$ is just an edge. 
$$
\begin{align}
P(\exists\ \text{edge}\ i\rightarrow j \in G) &= \\
&=\Sigma_{x\in S}\ P[(h_1(x)= i \land h_2(x) = x) \lor (h_1(x) = j \land h_2(x) = i)]\\
&\le n\cdot 2\cdot \frac{1}{m^2},\ \text{thanks to}\ \star \\
&\le \frac{1}{cm} \spadesuit
\end{align}
$$
where $\spadesuit$ is obtained thanks to the assumption we made: 
$$
\begin{align}
m > 2cn &\rightarrow \frac{m}{c}> 2n \\ 
&\implies \\
\frac{2n}{m^2} &< \frac{m}{cm^2} = \frac{1}{cm}
\end{align}
$$
**inductive case:** $k > 1$
Here we have a path that goes through a vertex $r$ with $r \neq i,j$ such that the successor of $r$ is $j$
Alternatively said: abusing notation, consider the vertex $r = j-1$ in the path $i\rightarrow j$
$$i \longrightarrow r \rightarrow j$$
The length of the sub-path $i \rightarrow r$ is $k-1$: here we will apply the inductive hypothesis. 
$$
\begin{align}
P(\exists\ \text{path}\ i\rightarrow j\ \text{of length}\ k)&\le \\
&\le \Sigma_{k \in (V-\{i,j\})}\ P(\exists\ \text{path}\ i\rightarrow r\ \text{of length}\ k-1 \land\exists\ \text{edge}\ r\rightarrow j)  \\
&= P(\exists\ \text{path}\ i\rightarrow r\ \text{of length}\ k-1)\cdot P(\exists\ \text{edge}\ r\rightarrow j\ |\ \exists\ i\rightarrow k)\ \circledast 
\end{align}
$$
where $\circledast$ is obtained by the rule $P(A\land B) = P(A|B)P(B)$. 

At this point we have that 
- $P(\exists\ \text{path}\ i\rightarrow r\ \text{of length}\ k-1) \le \frac{1}{c^km}$ by inductive hypothesis
- $P(\exists\ \text{edge}\ r\rightarrow j\ |\ \exists\ i\rightarrow k\ \text{of length}\ k -1) \le \frac{1}{cm}$, as this is the base case  

And we conclude that 
$$
\circledast \le \frac{1}{c^km}\cdot \frac{1}{cm} = \frac{1}{c^km^2} <\frac{1}{c^km}\ \square
$$

Now, we know that the insertion time in this case is $O(1 + k)$ as 
- $1$ to compute the first position $i$
- $k$ to follow the path from $i$ to $j$

At this point we can compute the average cost for **2)** by computing the expected length of the path $i\rightarrow j$
$$
\begin{align}
O(1 + E[k]) &= \\ 
&= O(1+\Sigma_{k=1}^n\ k\cdot \frac{1}{c^km}) \\
& = O(1+ \frac{1}{m})\ \bigstar \\
&= O(1)
\end{align}
$$
$\bigstar$ is given by the fact that $\Sigma_{k=1}^n\ k\cdot \frac{1}{c^km} = \frac{1}{m}$ is a known summatory. 
### Case 3: No Free Position, Rehashing
In this case a cycle appears and thus a rehashing is performed in $O(n)$ time. 
We choose two new hash functions $h_1', h_2' \in \mathcal{H}$ and we reinsert all the keys from scratch. 
$$
\begin{align}
P(\exists\ \text{cycle in}\ G) &=_{\text{UB}} \Sigma_{i=0}^{m-1}\ P(\exists\ \text{a path from $i$ to $j=i$}) \\
&= \Sigma_{i=0}^{m-1}\Sigma_{k\ge1}\ P(\exists\ \text{path $i\rightarrow j=i$ of length $k$})  \\
&\le \Sigma_{i=0}^{m-1}\Sigma_{k\ge1}\ \frac{1}{c^km}\ ,\ \text{as in case 2)} \\
&= \frac{1}{m}\Sigma_{i=0}^{m-1}\Sigma_{k\ge1}\ \frac{1}{c^k} \\ 
&< \frac{1}{m}\Sigma_{i=0}^{m-1}\frac{1}{c-1},\ \text{as $\Sigma_{k\ge1}\ \frac{1}{c^k} < \frac{1}{c-1}$} \\
& = \frac{1}{c-1} \diamondsuit
\end{align}
$$
$\diamondsuit$ is obtained since $\frac{1}{c-1}$ is independent in the $\Sigma$, hence we take it out. 
The summatory becomes then $\frac{1}{c-1}\frac{1}{m}\Sigma_{i=0}^{m-1}\ 1 = \frac{1}{c-1}\frac{1}{m} m = \frac{1}{c-1}$
Since we assumed that $c > 2$ we have that $\frac{1}{c-1}$, which is the probability $p$ of rehashing, is $< 1$. 

So we now we know that: 
- rehashing occurs with probability nearly $p = \frac{1}{c-1} < 1$
- rehashing takes $O(n)$ if it succeeds 

The point is now: **how many rehashing?**
- $1$ rehash with probability $p$
- $2$ rehash with probability $p^2$
- ... 
- $t$ rehash with probability $p^t$

The expected number of rehashing is $\Sigma_{t>=1}tp^t = O(1)$ as $p<1$.

So, about the insertion: if there is a cycle starting at position $i$ we have $O(1)$ rehash on average, then: 
$$
\begin{align} 
P(\exists\ \text{cycle starting from $i$}) &\leq \\ 
&\leq P(\exists\ \text{path $i\rightarrow j = i$}) \\
&= \Sigma_{k=1}^n \frac{1}{c^km} \\
&= \frac{1}{m}\Sigma_{k=1}^n \frac{1}{c^k} \\ 
&< \frac{1}{m}\frac{1}{c-1}, \ \text{as $\Sigma_{k=1}^n \frac{1}{c^k} < \frac{1}{c-1}$}\\
&= \frac{1}{m}\cdot p,\ \text{as $\frac{1}{c-1} = p$}\\
&= \frac{p}{m} 
\end{align}
$$
Thus we pay $O(n)$, the cost of rehashing, with probability $\frac{p}{m}$, giving $O(\frac{np}{m}) = O(1)$ expected cost $\square$
# Bloom Filter
**A bloom filter is a simple space-efficient randomized data structure for representing a set in order to support membership queries.** 
Bloom filters allow false positives but the space saving often outweigh this drawback when the probability of an error is controlled. 

A **bloom filter does not store the keys!**
We have a set $S \subseteq U$ of keys, but we do not want to store them in the BF, as they are too many. The goal is to check if $x \in S$, without storing the keys in $S$.

Let's take a universal hash family $\mathcal{H}$, we choose at random $k$ hash functions $h_1,\dots, h_k \in \mathcal{H}$ where $h_i:U\rightarrow [m]$. 
We then take a bit vector $B$, a compact array of $m$ bits initialized to $0$s, and we do $$x\in S \rightarrow_{BF} \forall\ B[h_i(x)]=1$$To check whether $x$ is in $S$ we simply return $B[h_1(x)] \land \dots \land B[h_k(x)]$ $\diamondsuit$
It is clear that: 
- $lookup(x)$: check the membership of a key cost $O(k)$ time
- $insert(x)$: insert an key cost $O(k)$ time
- $delete(x)$: deleting an element is not supported in this version

As before, there is the possibility of having a 1-sided error, a **false positive**: $$x \notin S \land (B[h_1(x)] \land \dots B[h_k(x)] = 1)$$Let's now say that $f$ is the probability of error: $$f = P(\text{error}) = P(x\notin S\ \text{but $\diamondsuit$ is true})$$We have now two points to solve: 
1) what is the error probability $f$
2) what are the best parameters to minimize $f$?
## Error Probability
Suppose that the bloom filter has been built, we have $B$, and we take a generic position $q$. 

**step 1)**
$P(B[q] = 1) = 1 - P(B[q] = 0)$

**step 2)**
Let's fix a function $h_i$, we know that $P(h_i(x) = q) = 1/m$ by definition of $h_i \in \mathcal{H}$
We know that $B[q] = 0$ when $h_i(x) = 0$
So we have $P(h_i(x) \ne q) = 1 - P(h_i(x) = q) = 1 - \frac{1}{m}$
Alternatively said: $P(B[q] = 0\ |\ h_i\ \text{is chosen}) = 1 - \frac{1}{m}$ 

**step 3)**
Let's relax the previous step by removing the fixated $i$-th hash function: $$
\begin{align}
P(B[q]=0) &= \\
&= P(\text{all the $k$ hash functions do not give q}) \\
&= (1-\frac{1}{m})^k
\end{align}
$$**step 4)**
We relax the previous step: we apply the same reasoning for all the keys in $S$$$P(B[q] = 0) = [(1-\frac{1}{m})^k]^n$$**step 5)** 
We can apply the result of **step 4)** in the equation of **step 1)**
$$
\begin{align}
P(B[q] = 1) &=\\ 
&= 1 - P(B[q] = 0) \\ 
&= 1 - (1-\frac{1}{m})^{nk} \\
& = 1 - p',\ \text{as we define $p'=(1-\frac{1}{m})^{nk}$ }
\end{align}
$$
**We have then computed the probability of failure:**
$$f = P(\text{error}) = P(x\notin S\ \text{but $\diamondsuit$ is true}) = (1 - p')^k$$
## Choosing the Best Parameters
We want to **minimize** the failure probability $f = (1-p')^k$, where $p' = (1-\frac{1}{m})^{nk}$
Remember the Taylor expansion: $(1+y)\sim e^y$ for small $y$. 
Then we can write$$p' = (1-\frac{1}{m})^{nk} \sim_{y =\frac{1}{m}} (e^{-\frac{1}{m}})^{nk} = e^{-\frac{nk}{m}} = p$$So we now try to minimize $(1-p)^k$, using the logarithm to both sides of the equation:
$$
\begin{align}
&1) \log(1-p)^k = k\log(1-p) \\
&2) \log(p)= -\frac{nk}{m}\log(e) \rightarrow \log(p) = -\frac{nk}{m} \rightarrow k = -\frac{m}{n}\log(p)
\end{align}
$$
We can then put $1)$ in $2)$ and we obtain 
$$-\frac{m}{n}\log(p)\log(1-p)$$
We minimize over $p$, it's the best choice for $p$ is $\frac{1}{2}$
$$
\begin{align}
&f\sim(1-p)^k = \frac{1}{2^k} = \frac{1}{2^{-\frac{m}{n}\log(2)}} = \frac{1}{2^{\frac{m}{n}\log(2)}} = (2^{-\log(2)})^\frac{m}{n} < 0.618^{\frac{m}{n}} \\
&k = \frac{m}{n}\log(p) = \frac{m}{n}\log(2)
\end{align}
$$
**observations:** 
- $2^{-log(2)} = 0.618$
- you have to choose $m$ accordingly
$\square$ 
## Space Complexity
We have seen how Bloom Filter is a solution for a membership problem that actually do not store the keys. 
The **space complexity** is: $m$ bits plus $O(k)$ words:
- $m$ bits to store the bitmap $B$
- $O(k)$ words to store $k$ hash functions: storing the pairs $(a,b)$ of each $h_i$ takes $k$ words

Let's be more careful about the space. 
Consider $f$ and do the logarithm: 
$$
\begin{align}
&\log(f)\sim\frac{m}{n}\log(2)\log(\frac{1}{2}) =_{(\log(1/2)=-1)} -\frac{m}{n}\log(2) \\ 
&\implies m\sim\frac{n\log(f)}{\log(\frac{1}{2})\log(2)}=\frac{n\log(\frac{1}{f})}{\log(2)}\sim 1.44\cdot n\log(\frac{1}{f})\ \text{bits}
\end{align}
$$
**We have computed both the time and space complexity of BF.** 
# Approximate Dictionary: Succinct Rank DS
Consider a set $S$ of $n$ keys chosen from a universe $U$. 
For a given ($1$-side) error probability $0 < f < 1$, we learned that Bloom Filters achieve probability $f$ using $k \sim \frac{m}{n}\log(2)$ hash functions that map $U \rightarrow [m]$. 
They take $O(k)$ time and use nearly $1.44\cdot n\log(1/f)$ bits of space
**Is it possible to do better?**

**Information Theory Lower Bound (IT)**
Take a set $S \subseteq U$ and let $|U| = m$ and  $|S| = n$. 
How many sets $S\subseteq U$ of size $n$ we can have? $\binom{m}{n}$ 
The information theory lower bound states that using less than $\log\binom{m}{n} \sim n\log(\frac{m}{n})$ bits cannot give a correct algorithm: indeed using less bits forces two sets $S'$ and $S''$ to get the same binary representation, so the *exact* membership is impossible. 

Here are the **lower bounds for the membership problem:**
- time: **trivial**, $\Theta(1)$ for both query and insertion
- space: $\geq n\log(\frac{1}{f})$, **to prove**
And here the **upper bounds** for the membership problem: 
- time: $O(1)$ with $1$ hash function, **to prove**
- space: $\sim n\log(\frac{1}{f})$ bits $+$ lower order terms, **to prove**
## Lower Bound
Let's call $D'$ the approximate dictionary for a set $S$ with an error probability $1/f$. 
Then let's call $D$ the exact dictionary for some $S\subseteq S'$, and we say that $$\frac{|S'/ S|}{U} = f$$We have that $$
\begin{align}
S'&= \{x \in U:\ \text{approximate dictionary says yes}\} \\
&= \{x \in U: D'(x)=true\}
\end{align}$$$S$ are the actual elements, $S'$ are the elements that $D'$ recognize as part of $S$.
$D'$ can be wrong. 
We can have a $1$-side error for $S$: $S\subseteq S'$ as all keys in $S$ are accepted, plus the extra (*wrong*) keys in $S/ S'$.

Consider this problem:
- let $D'$ be the exact dictionary for $S'$
	- notice that $D'$ is also an approximate dictionary for $S$
- let $D$ be the approximate dictionary for $S$

**Question:** given $D'$, can we get $D$?
Let's say that $b'$ is the number of bits required by $D'$.
Then we have that $D = D' +\ \text{extra bits to mark correct answers from}\ D'$
So we get an exact dictionary $D$, and then it must require at least $\log\binom{m}{n}$ by IT. 

So we have: $$
\begin{align}
&|D| \geq \log\binom{m}{n},\ \text{by IT}\\
&|D' +\text{extra bits}| \geq \log\binom{m}{n},\ \text{as $D'$+\ extra bits is a dictionary for $S$}
\end{align}
$$If we look closely we see that 
$$|D' +\text{extra bits}| = |D'|+ \clubsuit \log\binom{|S'|}{|S|}\ \bigstar$$$\clubsuit:$ number of bits we need to mark $D'(x)$ to make it an exact dictionary

We then remember the initial assumptions: $$\begin{align}
|S'| &= \\
&=|S| + |S\backslash S'| \\
&= |S| + |U|\cdot f\  \star\\
&= n+fm
\\ 
\\
&\star: \frac{|S/S|}{|U|} = f \iff |S'/S|=fm
\end{align}$$So we can resume $\bigstar$: 
$$
\begin{align}
|D' +\text{extra bits}| &= \\
&=|D'|+ \log\binom{|S'|}{|S|}\\
&= b'+\log\binom{n+fm}{n}
\end{align}
$$
**Putting things together:** $$
\begin{align}
b'+ \log\binom{n+fm}{n} \ge \log\binom{m}{n} &= \\
&= b' \ge \log\binom{m}{n} - \log\binom{n+fm}{n} \\
&\sim  b'\ge n\log(\frac{m}{n}) -n\log(\frac{n+fm}{n})\ \nabla \\
&\sim b' \ge n\log(\frac{m}{n}) -n\log(\frac{fm}{n})\ \star \\
&= b' \ge n(\log(\frac{m}{n})-\log(\frac{fm}{n})) \\
&=b' \ge n(\log(\frac{m}{n})+\log(\frac{n}{fm}))\\ 
&= b' \ge n(\log(\frac{m}{n}\cdot\frac{n}{fm})) \\
&= b' \ge n\log(\frac{1}{f})\ \square
\end{align}
$$Where: 
- $\nabla:$ $\log\binom{m}{n} \sim n\log(\frac{m}{n})$
- $\star:$ $\log(\frac{n+fm}{n}) \sim \log(\frac{fm}{n})$ as $\frac{n+fm}{n} = 1 + \frac{fm}{n}$

**We proved the lower bound.**
## Upper Bound
(Succinct Rand DS)
*I skip this part, too hard and boring.* 
# Load Balancing