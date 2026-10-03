---
title: Decide Whether a Number is a Palindrome
description: LeetCode No.9
pubDate: 2026-10-03
draft: false
tags:
  - leetcode
  - algorithm
---

We are given an integer `x`, and wish to check whether is is a palindrome. For example, `x = 121` is a palindrome, because flipping it gives `121`. The number `123` is not a palindrome, because `321` is its inverse.

We consider some simple cases where we may have an instant judgement. Any negative number is not a palindrome, because `-a` writes `reverse(a)-`. It is different from `-a` by the location of `-` sign. Any single digit number is a palindrome. Any number divisible by 10 is not a palindrome number. For example, `x = 120` is not a palindrome. Its reverse is `021`, and no proper integer input `x` may start with `0`.

How do we tell a palindrome in general cases? The simple solution is to turn `x` into a string, and then judge whether the string is a palindrome. This can easily be done with a 2-pointer technique in C++. 

We are interested in a solution not requiring type casting. If we can find `y = reverse(x)`, and then compare `y` with `x`, we are done. We consider given `x`, how to find `y`. Take $x = 313$ as an example. 

```
STEP 1:
x = 3 1 3
		^ 
		3 
y = 3 0 0 = 3 * 10^2
STEP 2:
x = 3 1 3 
	  ^
	  1
y = 3 1 0 = 3 * 10^2 + 1 * 10^1
STEP 3:
x = 3 1 3 
	^
	3
y = 3 1 3 = 3 * 10^2 + 1 * 10^1 + 3 * 10^0
```
The diagram shows how to do it. We have `x` is between `100-1000`, so the power corresponding to first digit should be `10^2`. We move digit in `x` to the left, we find the number there, and then multiply by a power of `10` with exponent decreased by 1, and so on. 

The method works well for a human mind, but not for a computer. We can identify where the largest power in `y` should start from by inspecting `x`. But for a computer, it doesn't automatically know this. Of course we can do so with a while loop, but this would be more troublesome.

```
# include <cmath>
int power = 0;

while (x > pow(10, power + 1)){
	power ++;
}

for (int i = power; i >=0; i++){
	y += [digit of x, counting backwards] * 10 ^ i;
}
```

Notice building `y` can be recursive. We don't need `y` to start with `3xx` immediately. We can let `y` be 3 to begin with. When we add the next digit, we multiply `y` by 10 and then add the needed digit. So, in practice, `y` should be built up as `3 -> 3 * 10 + 1 = 31 -> 31 * 10 + 3 = 313`. 

The next difficulty is: how to make a computer know what the second digit of `x` is. For human, we can inspect with eyes. A computer can't do it. But this is pretty easy. We know the first digit is `3`. This can simply be found as `x % 10`. After this being added to `y`, we don't need it anymore. So, just remove this digit from `x`. This is saying:
```
First digit:
x = 3 1 3 
		^
		3 = x % 10
		
Second digit:
	This is first digit
		   |
x = (313 - 3) / 10
  = 3 1 
	  ^
	  1 = x % 10
Third digit:
This is second digit
		  |
x = (31 - 1) / 10
  = 3 
    ^ 
    3 = 3 % 10

```

So we can present the solution: 
```
bool isPalindrome(int x){
	// judge simple answers first. 
	
	if (x < 0){
		return false;
	}
	
	if (x < 10){// x >= 0 guaranteed because previous condition won't hold.
		return true;
	}
	
	if (x % 10 == 0){
		return false;
	}
	
	// general situations
	int xBackUp = x; // we need to modify x, so remember orginal value.
	int remainder = x % 10;
	long y = remainder; // the first digit can be intialised direcly.
						// need to let y be large. say x = 123456789,
						// reversing it leads to y = 987654321. 
						// y can be quite large, so we need long or long long.
						
	while (x > 10){ // when x = 3, we can stop. when x = 31, still need to do.
		x = (x - remainder) / 10;
		remainder = x % 10;
		y = (y * 10) + remainder;
	}
	
	return y == xBackUp;
	
}



```
