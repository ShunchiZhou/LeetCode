![](https://ws3.sinaimg.cn/large/006tNc79ly1g4vfarryqlj31900pidgs.jpg)

# Approach 1
```java
class Solution {
    public int[] plusOne(int[] digits) {
        int n=digits.length;
        int carry=(digits[n-1]+1)/10;
        digits[n-1]=(digits[n-1]+1)%10;
        
        for(int i=n-2;i>=0;i--){    
            int tmp=digits[i];
            digits[i]=(tmp+carry)%10;
            carry=(tmp+carry)/10;
        }
        if(carry!=0){
            int[] res=new int[n+1];
            res[0]=1;
            return res;
        }
        return digits;
    }
}
```



