---
layout: post
title: How to Discover Prime Numbers with Python
image: "/posts/primes_image.jpeg"
tags: [Python, Primes]
---

In this article, we'll explore a Python function designed to identify all prime numbers less than a specified integer. For instance, inputting 100 would return all prime numbers under that threshold.

Firstly, what exactly is a Prime number? It's a number divisible only by 1 and itself. So, 7 qualifies because only 1 and 7 divide it without leaving a remainder. On the other hand, 8 doesn’t qualify because it is divisible by 1, 2, 4, and 8.

Let’s delve into the specifics!

---

We begin by defining the upper boundary for our prime search, starting with the number 20, meaning we seek primes less than or equal to 20.

```ruby
n = 20
```

The smallest prime is 2. We'll first generate a set of numbers from 2 up to our upper limit, n. We choose a set because it offers specific functions that help in efficiently eliminating non-prime numbers.

```ruby
number_range = set(range(2, n+1))
```

Next, we need somewhere to store the primes we find—a list is perfectly suited for this.

```ruby
primes_list = []
```

Before using a loop to automate the process, it’s helpful to manually step through the logic to ensure it functions correctly. Let's manually check and move the first prime from our set to our list.

When a number is determined to be a prime, we'll add it to primes_list.

```ruby
print(number_range)
>>> {2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
prime = number_range.pop()
print(prime)
>>> 2
print(number_range)
>>> {3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
```

With the first number confirmed as a prime, we add it to our list.

```ruby
primes_list.append(prime)
print(primes_list)
>>> [2]
```

To streamline the process, we generate multiples of the prime up to 20 and use a set function called difference_update to remove these multiples from number_range, since any multiple of a number other than itself or 1 isn’t a prime.

```ruby
multiples = set(range(prime*2, n+1, prime))
number_range.difference_update(multiples)
print(number_range)
>>> {3, 5, 7, 9, 11, 13, 15, 17, 19}
```

For larger sets of numbers, this procedure can be efficiently repeated using a while loop, which we'll demonstrate for primes under 1000.

```ruby
n = 1000
number_range = set(range(2, n+1))
primes_list = []

while number_range:
    prime = number_range.pop()
    primes_list.append(prime)
    multiples = set(range(prime*2, n+1, prime))
    number_range.difference_update(multiples)
```

Finally, we display the results:

```ruby
print(primes_list)
>>> [2, 3, 5, 7, 11, 13, 17, 19, 23, ...]
```

To summarize our discovery:

```ruby
prime_count = len(primes_list)
largest_prime = max(primes_list)
print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
>>> There are 168 prime numbers between 1 and 1000, the largest of which is 997
```

WWe can encapsulate this logic into a function for easy use:

```ruby
def primes_finder(n):
    number_range = set(range(2, n+1))
    primes_list = []
    while number_range:
        prime = number_range.pop()
        primes_list.append(prime)
        multiples = set(range(prime*2, n+1, prime))
        number_range.difference_update(multiples)
    print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
```

Let's test it with a higher value, such as one million:
```ruby
primes_finder(1000000)
>>> There are 78498 prime numbers between 1 and 1000000, the largest of which is 999983
```

Important Note: Pop() Method in Sets
Using pop() on a set in Python is generally reliable for retrieving the lowest element, but because sets are unordered, this is not guaranteed. For more accuracy, particularly in formal applications, you might replace the pop() method with explicit sorting to guarantee the lowest element is selected each time, though this method is somewhat slower. Here’s how you can modify the code:

```ruby
prime = min(sorted(number_range))
number_range.remove(prime)
```

