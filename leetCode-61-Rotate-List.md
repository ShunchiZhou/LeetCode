![](https://ws2.sinaimg.cn/large/006tNc79ly1g4v8vb5didj30zo0r6ab1.jpg)

# Approach 1
``` java

 // Definition for singly-linked list.
class ListNode {
	int val;
	ListNode next;
	ListNode(int x) { val = x; }
	}

class Solution {
	public ListNode rotateRight(ListNode head, int k) {
        //base cases
        if (head==null) return null;
        
        // close the linked list into the ring
		int count=1;
		ListNode p1=head;
		while (p1.next!=null) {
            count++;
			p1=p1.next;			
		}
        p1.next=head;
        p1=p1.next;
               
		int pos=count-k%count;
		if (pos==count) {
			return head;
		}
		while (pos>1) {			
			pos--;
			p1=p1.next;
		}
		ListNode newHead=p1.next;
		p1.next=null;		
		return newHead;
	}
}
class slList{
	public static void main(String[] args) {
		ListNode head=new ListNode(3);
		ListNode dummyHead=head;
		head.next=new ListNode(2);
		head=head.next;
		head.next=new ListNode(1);
		head=head.next;
		head.next=new ListNode(0);
		head=head.next;
		head.next=null;
		ListNode newHead=new Solution().rotateRight(dummyHead, 1);
		while (newHead!=null) {
			System.out.println(newHead.val);
			newHead=newHead.next;
		}
	}
}
```


