#Counting in Binary
Binary representation may at first seem daunting, but it follows the familiar rules of counting presented in base-10. In order, then, to count in binary, first break down and analyze counting in base-10.
##Counting in Base-10
Counting in base-10, decimal, or normal counting is readily accessible to most people as it is the standard used around the world. When working with multiple bases use a subscript under each number to indicate its base. $10_{10}$ therefore means 10 in base 10.
 For clarity's sake all equations in this section will assume base-10 unless specified with a subscript.
###Definitions and Vocabulary
In order to analyze this counting system, a few terms have to be clearly defined: digit, place-value, order, and significance.

 A digit is the simplest numerical unit, consisting of unique symbols ranging from $0$ to $base-1$. In base-10 this would produce the 10 unique symbols for $0$ to $9$.

Place-value is the concept that the position of a digit within a number determines it's value. The formula for determining place-value is $d*10_b^p$ where $d$ is the digit, $b$ is the base, and $p$ is the place starting from 0. For instance $152_{10}$ breaks down by place-value into:
 $2*10^0 + 5*10^1 + 1*{10}^2 = 2 + 50+ 100 = 152$

Order is simply the order in which the numbers appear. In the regular representation of numbers the biggest number has the lowest order (or furthest to the left) and the smallest number has the highest order (or furthest to the right). In $152$, $1$ has the lowest order and $2$ has the highest order.

Significance is the size of each digit in place. The most significant digit is the digit in the highest place value. In the normal counting system this is also the lowest order digit. The least significant digit is the digit in the lowest place value. In the normal counting system this is also the highest order digit.

With these definition, an algorithm for counting can be described in base-10 and can be extended to all the other bases.
###Counting
Counting works by incrementing less significant digits until they can no longer increment (run out of unique digits) and only then incrementing the next least significant bit. In base-10, $0$ increments until $9$. Only then does the next least significant digit increment, giving us $10$. Starting again with the least significant digit, $10$ increments to $19$, before the next least significant digit changes, yielding $20$. This idea applies to base systems with more digits than decimal and those with less.
##Counting in Base-2
In this section all numbers are base-2 unless otherwise specified. Counting in base-2 uses the same algorithm described above for counting in base-10. Before jumping into that more vocabulary terms must be defined for talking about base-2.
###Definition and Vocabulary
Binary is the common name for base-2. Binary only has 2 unique digits $0$ and $1$ (the biggest digit is always 1 less than the base). Binary can be represented with the subscript 2 as in $0110_2$.
A bit is a single digit in binary. Bits also refer to the smallest unit of information. Information can be interpreted as anything, but binary refers specifically to the numerical interpretation.
###Counting
Applying the same algorithm used to count base-10, counting in binary is a very simple process. The least significant bit increments from $0$ to $1$ before the next least significant bit increments from $0$. For example to count from $0_{10}$ to $3_{10}$ first $0$ becomes $1$ before the next bit increments giving $10$. Then the least significant bit increments again from $10$ to $11$. Using the place-value formula convert the resulting binary to decimal to check the work. 
$1*10^0+1*10^1 = 1_{10} * 2_{10}^0 + 1_{10}*2_{10}^1=3_{10}$
