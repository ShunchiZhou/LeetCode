![](https://ws2.sinaimg.cn/large/006tNc79ly1g4u0imstg8j313w0pymy6.jpg)

# Approach 1: Backtracking

This is the inefficient solution where we try every single jump pattern that takes us from the first position to the last. We start from the first position and jump to every index that is reachable. We repeat the process until last index is reached. When stuck, backtrack.

``` java
class Solution {
	public boolean canJumpFromPosition(int position, int[] nums) {
		if (position == nums.length - 1) {
			return true;
		}

		int furthestJump = Math.min(position + nums[position], nums.length - 1);
		for (int nextPosition = position + 1; nextPosition <= furthestJump; nextPosition++) {
			if (canJumpFromPosition(nextPosition, nums)) {
				return true;
			}
		}

		return false;
	}

	public boolean canJump(int[] nums) {
		return canJumpFromPosition(0, nums);
	}
	public static void main(String[] args) {
		int[] nums={3,2,1,0,4};
		System.out.println(new Solution().canJump(nums));
	}
}
```

Time complexity: O(2<sup>n</sup>). There are 2<sup>n</sup>(upper bound) ways of jumping from the first position to the last, where n is the length of array nums. For a complete proof, please refer to Appendix A.

Space complexity: O(n). Recursion requires additional memory for the stack frames. 

# Approach 2: Dynamic Programming Top-down
```java
import java.util.*;

enum Index {
	GOOD, BAD, UNKNOWN
}

class Solution {
	static Index[] memo;

	public boolean canJumpFromPosition(int position, int[] nums) {
		
		if (memo[position] != Index.UNKNOWN) {
			return memo[position] == Index.GOOD ? true : false;
		}

		int furthestJump = Math.min(position + nums[position], nums.length - 1);
		for (int nextPosition = position + 1; nextPosition <= furthestJump; nextPosition++) {
			if (canJumpFromPosition(nextPosition, nums)) {
				memo[position] = Index.GOOD;
				return true;
			}
			
		}
		memo[position] = Index.BAD;
		return false;
	}

	public boolean canJump(int[] nums) {
		memo = new Index[nums.length];
		for (int i = 0; i < memo.length; i++) {
			memo[i] = Index.UNKNOWN;
		}
		memo[memo.length - 1] = Index.GOOD;
		return canJumpFromPosition(0, nums);
	}
	
	public static void main(String[] args) {
			int[] nums={2, 4, 2, 1, 0, 2, 0};
			new Solution().canJump(nums);			
		}
}
```
# Approach 3: Dynamic Programming Bottom-up
```java
import java.util.*;

enum Index {
	GOOD, BAD, UNKNOWN
}

class Solution {
	public boolean canJump(int[] nums) {
		Index[] memo = new Index[nums.length];
		for (int i = 0; i < memo.length; i++) {
			memo[i] = Index.UNKNOWN;
		}
		memo[memo.length - 1] = Index.GOOD;

		for (int i = nums.length - 2; i >= 0; i--) {
			int furthestJump = Math.min(i + nums[i], nums.length - 1);
			for (int j = i + 1; j <= furthestJump; j++) {
				if (memo[j] == Index.GOOD) {
					memo[i] = Index.GOOD;
					break;
				}
			}
		}
		return memo[0] == Index.GOOD;
	}
	
	public static void main(String[] args) {
			int[] nums={2, 4, 2, 1, 0, 2, 0};
			System.out.println(new Solution().canJump(nums));
		}
}
```
# Approach 4: Greedy
```java
class Solution {
	public boolean canJump(int[] nums) {
		int lastPos = nums.length - 1;
		for (int i = nums.length - 1; i >= 0; i--) {
			if (i + nums[i] >= lastPos) {
				lastPos = i;
			}
		}
		return lastPos == 0;
	}
	
	public static void main(String[] args) {
				int[] nums={2, 4, 2, 1, 0, 2, 0};
				System.out.println(new Solution().canJump(nums));
			}
}
```
# Conclusion
The question left unanswered is how should one approach such a question in an interview scenario. I would say "it depends". The perfect solution is cleaner and shorter than all the other versions, but it might not be so straightforward to figure out.

The (recursive) backtracking is the easiest to figure out, so it is worth mentioning it verbally while warming up for the tougher challenge. It might be that your interviewer actually wants to see that solution, but if not, mention that there might be a dynamic programming solution and try to think how could you use a memoization table. If you figure it out and the interviewer wants you to go for the top-down approach, it will not generally be time to think of the bottom-up version, but I would always mention the advantages of this technique as a final thought in the interview.

Most people are stuck when converting from top-down Dynamic Programming (expressed naturally in recursion) to bottom-up. Practicing similar problems will help bridge this gap.



