---
layout: post
title: Sieve of Eratosthenes
subtitle: Finding prime numbers made easy!
tags: [Algorithms, Competitive Programming, Java]
---

Prime numbers are numbers which have only two factors: 1 and the number itself. 2,3,5,7,11,... are examples of prime numbers.

If you were told to write a program to print first 'n' prime numbers, 
your first obvious approach would be to apply brute force i.e. you would take a number, c
heck whether it is divisible by any integer from 2 to (number-1), and on the basis of the results, 
decide whether the number is 
prime or not. This method would definitely generate the correct answer, 
but this algorithm is not quite efficient and considerable differences in time of 
execution can be observed when the number of prime numbers to be calculated is very large. 
Also, the brute force method would definitely lead to a **Time Limit Exceeded** error when 
used in a competitive programming contest.  
So, is there any other algorithm which can accomplish the same task in less time? 
(Ofcourse there is. What would be the point of writing this post if there wasn't one?) 
This algorithm is known as the [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes). 
So, how does this work? You take a boolean array indexed from 2 to 'n'.  
Initially, assign true value to all locations in the array. Let us assume 
that true indicates a prime number. Now, iterate from 2 to n. For each iteration, 
check if array has true value at that index. If yes, it's a prime number, print it. 
Additionally, we need to set the value false at indices which are multiples of the 
prime number since multiples of a prime number are composite numbers. There, 
you have your list of prime numbers. This method can still be made faster. 
Do you know how? We only need prime numbers less than square root of n. 
Why so? Because, by the time we find all the prime numbers upto square root of n, 
we would have marked all the composite numbers upto n with 'false' value in the array. 
Don't believe me? Go ahead, check for yourself!  

Now, what if you are asked to find all prime numbers between 
two user defined numbers? Here, the sieve of Eratosthenes cannot be used directly. 
In order to perform this task, we will modify our original algorithm a little. 
This modified algorithm is known as **Segmented Sieve of Eratosthenes**. 

Suppose you need to print all prime numbers from 
'n' to 'm'. First, we'll find all the prime numbers between 2 and square root of m 
(both inclusive). Then, we would eliminate all multiples of these prime numbers which 
exist between n and m. The remaining numbers would be prime and they would be printed. F
air enough? Easy, right!  

I feel comfortable coding in Java. 
A Java implementation of the Segmented Sieve of Eratosthenes is as follows:  

```java
import java.util.*;
import java.lang.*;

class PrimeNumber{
    public static void main(String[] args){
        //Creating Scanner instance
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter lower bound:");
        int n = sc.nextInt();  //Taking lower bound as input from user
        System.out.println("Enter upper bound:");
        int m = sc.nextInt();  //Taking upper bound as input from user
        
        int sq = (int)Math.sqrt(m);  //Finding square root of upper bound
        
        //Defining array of numbers among which all prime numbers to be checked exist.
        boolean[] primeArr = new boolean[sq+1];
        for (int i=0; i<=sq; i++){
            primeArr[i]=true;
        }
        
        //Defining array where all prime numbers found would be stored
        int[] prime = new int[sq+1];
        int j=0;
        
        //Checking whether prime or not
        for (int f=2; f<=sq; f++){
            if (primeArr[f]==true){
                prime[j]=f;
                j=j+1;
            }
            for (int s=f+f; s<=sq; s=s+f){
                primeArr[s]=false;
            }
        }
        
        int diff = m-n+1; //Total numbers existing from n to m
        primeArr = new boolean[diff];
        for (int i=0; i<diff; i++){
            primeArr[i]=true;
        }
        
        //Eliminating composite numbers between n and m
        for (int x=0; x<j; x++){
            //Pointing to greatest number less than n
            int lowkey = n/prime[x];
            lowkey = lowkey*prime[x];
            
            //Identifying composite numbers between n and m
            while (lowkey<=m){
                if (lowkey>=n && lowkey!=prime[x]){
                    primeArr[lowkey-n]=false;
                }
                lowkey = lowkey + prime[x];
            }
        }
        
        //Printing the prime numbers
        for (int i=0; i<diff; i++){
            if (primeArr[i]==true && (i+n)!=1){
                System.out.println(i+n);
            }
        }
    }
}
```
Default value at all indices of boolean array is false. So you can assume that false represents a
prime number and true represents a composite number. This will eliminate a `loop` in the code.  
Give this a try!
In case of queries, feel free to reach out :)
