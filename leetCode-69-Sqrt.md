![](https://ws3.sinaimg.cn/large/006tNc79ly1g4vm1woglyj317o0osdgl.jpg)

# Approach 1
```java
class Solution {
    public static int mySqrt(int x) {
        int i=0;
        while(i*i<x&&i*i>=0){
            i++;        
        }
        if(i*i==x) return i;
        return i-1;
    }
}
```

# Approach 2
```java
class Solution {
    public static int mySqrt(int x) {
        if(x==0) return 0;
        int left=1,right=x/2;
        if(left>=right) return left;
        while(true){
            int i=left+(right-left)/2;
            if(i<x/i) left=i+1;
            else{
                if(i == x/i) return i;
                if(i-1 < x/(i-1)) return i-1;
                right=i-1;
            }
        }
    }
}
```

```cpp
	// This is a hello world program for C.
	#include <stdio.h>
	
	int main(){
	  printf("Hello World!");
	  return 1;
	}

```