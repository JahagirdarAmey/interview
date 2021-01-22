### Numbers

1. Reverse a number 

```
public static int reverseNumber(int number){
   int reverse=0;
   int remainder;
           
   while(number>0){
       remainder=number%10;
       number=number/10;
       reverse=reverse*10+remainder;
   }          
   return reverse;
}
```

2. Fibonacci series

```
public static void generateFibonacciSeries(int n){
   int first=0;  //first number of series
   int second=1; //second number of series
   int temp;
           
   System.out.print("FibonacciSeries: "+ first+" "+second+" ");
      for(int i=0;i<n;i++){
                  temp=first+second;
                  first=second;
                  second=temp;            
                  System.out.print(temp+" ");
      }
}
```

3. Prime number

```
public static boolean isPrimeNumber(int n){
                  
   for(int i=2;i<=Math.sqrt(n);i++){
        if(n%i==0){
           return false;
             }
        }
    return true;  //means number wasn't divisible by any of the number, it's a prime number.
}
```


4. sum of digits

```
public static int sumOfDigits(int number){
           int sum=0;
           int remainder;
           
           while(number>0){
                  remainder=number%10;
                  number=number/10;
                  sum+=remainder;
           }          
           return sum;
    }
```


5. Binary number 

```
 public static boolean isBinaryNumber(int n){      
        while(n != 0){
         if(n%10 > 1){
             return false;  //number containing any digit greater than 1 means its not binary.
         }
         n = n/10;    
        }
        return true;
    }
```

7. Factorial

```
 public static int findFactorial(int num){
           int factorial=1;
           while(num>0){
                  factorial=factorial*num;
                  num--;
           }
           return factorial;
    }

 /*OUTPUT
 
Factorial of 4 is: 24
 
*/

```
