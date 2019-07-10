![](https://ws2.sinaimg.cn/large/006tNc79ly1g4vh5fwf7cj30tq0kgaah.jpg)

# Approach 1
```java
class Solution {
    public String addBinary(String a, String b) {
        int n=a.length()-1;
        int m=b.length()-1;
        int carry=0;
        String res="";
        while(n>=0||m>=0||carry==1){
            int tmp=(n>=0?a.charAt(n)-'0':0)+(m>=0?b.charAt(m)-'0':0)+carry;
            carry=tmp/2;
            res=(char)tmp%2+res;
            n--;m--;
        }
        return res;
    }
}
```



