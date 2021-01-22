### String Programs 

1. Reverse a string 

```
  public static String reverseString(String originalString){
           char ar[]=originalString.toCharArray();
           char temp;
           for(int i=0,j=ar.length-1; i<(ar.length/2); i++,j--){
                  temp=ar[i];
                  ar[i]=ar[j];
                  ar[j]=temp;
           }
           return new String(ar);
  }


Using StringBuffer 

String originalString="abcde"; //String to be reversed
StringBuffer sb=new StringBuffer(originalString);
           
System.out.println("Original String: "+originalString);
System.out.println("Reversed String: "+sb.reverse());    

```

