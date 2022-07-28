# Thinking-about-optimization
My thoughts while improving myself at optimization

A lot of people (like me) like problem solving, but a lot of times we get stuck. There are times when we are unable to get the right answers and there are times when our solutions don't perform well with a few test cases, take a long time, eventually exceed the time limit, or result in bad performance :(. Sometimes it's hard to dump the current solution and start again from scratch with the same problem. 

Below, I am trying to document my learning while trying to become good with optimizations while problem solving.

## Why do we need to consider optimization?
- Take the simple example of writing a programme to get the number of factors of a given number.
- Suppose we are doing it as below 

    ```java
    	int countFactors(int n){
		int count = 0;
		for(int i=1;i<n;i++){
			if(n%i == 0)
				count++;
		}
		return count;
	}
    ``` 
- Now, assume we require 1 second for 10^8 iterations. For 10^9 iterations, it will need 10 seconds (i.e : 10^8 * 10)  
- Suppose we have given a number which is bigger than 10000000000000 (ten trillion ;p just for the sake of example, assume that our int can store 10 trillion), which will need 10^8 * 10^10 iterations.
- Which means 10^10 seconds = (10^10/(60*60*24)) ~ 115741 days ~ 316 years :(


## How to find ways to optimise your code?
- For any problem like the above, start figuring out the patterns. 
- For example, factors of 10 are : 1,2,5,10(observed something?) => (1 * 10)=>10  (2 * 5)=>10
- Same way, Factors of 100 are 
	(1 * 100) , (2 * 50) , (4 * 25) , (5 * 20), (10 * 10) lets consider all these pairs as (a*b) where N=a*b where all a<=b and b = N/a
- Now as a <=b	-> a <= N/a -> a^2 <= N i.e a<= sqrt(N), max value of a will be sqrt(N).
- For every a there are equal number of b's, also consider a corner case where : a==b (in above case 10*10)
- With the help of above observations, our code will be
  ```java
    	int countFactors(int n){
		int count = 0;
		for(int a=1; a <= sqrt(n) ;i++){ 
			// above condition(a<=sqrt(n)) can also be written as == a*a <= n  
			if(a*a == n){
				//case where a == b
				count ++;	
			} 
			else if(n%2 == 0){
				count += 2 ;
			} 
		}
		return count;
	} 
    ```  
		
       

## Things to keep your eye on to avoid delayed response 


## Mathematical tips and tricks for common problems.
- Sum of 1st n numbers.
- Use the correct formula with the help of this mind-blowing observation : https://nrich.maths.org/2478#:~:text=Gauss%20added%20the%20rows%20pairwise,quantity%20in%20a%20clever%20way. 
- Suppose you are finding square root of a perfect square,
	```java
  	//brute force approach 
	for(int i=1; i < n ;i++){ 
		if(i*i==n){
			return i;
		}
	}	
    ```  
- Let's observe one example to find out the sqrt of 64 (64 is a perfect square). Let's apply divide and conquer, 
	1. 64/2 -> 32 & 32*32= 1024 > 64 , so discard all possibilities which are greater than 32, now max is 32, 
	2. 32/2 = 16 & 16*16 = 256 >64 , now discard all valued greater than 16,
	3. 16/2 = 8 & 8*8 == 64. so return 8, and we reached to the correct answer in just 3 steps.
 
- Arithmatic Progressions : a, a+d , a+2d , a+3d , ... , a+(n-1)d
	Sum of 1st n terms in AP :  S = n/2(2a+(n-1)d) , refer above link if want to know how this formula is derived.

- Geometric Progressions : a , a*r , a*r2 , ... , a* (r^n-1)
	Sum of 1st n terms in GP : S=a(r^(n-1))/(r-1)

## Calculating the number of iterations

-lets take one tricky example 

   	```java
  	//brute force approach 
	for(int i=0; i < n ;i++){ 
		for(int j=1; j <= n ; j = j*2){
			print(i & j)
		}
	}
	/*
		Note : we are multiplying j by 2 till j < n  , the number of iterations will also be similar in case of j=n ; j>1 ; j=j/2
		//i.e. we are dividing the number till it bocomes 1 (i.e. logN)

	   	|	iteration of i	|	total iterations of j	|
	   	| 	 1		| 	[1 1] 			|	
		|	 2		|       [1 2]  log2		|
		|	 3		|  	[1 2]  log3()		|
		|	 .		|		.		|
		|	 .		|		.		|
		|	 .		|		.		|
		| 	 N		| 	[1 LogN] 		|
		| Total iterations 	| 	N * log(N)		|
		*/	
    	```  

## Time complexity 
	 logN < sqrt(n) < N < Nlog(N) < N^2 < 2^n < N!				 
Even worst case complexities are esier because we need to think in perspective of N.i.e. input we are receiving. I know so selfish right?😂
But that's important, never miss the input constraints to avoid TLE. 

