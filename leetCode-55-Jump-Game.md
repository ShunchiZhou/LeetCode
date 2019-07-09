![](https://ws2.sinaimg.cn/large/006tNc79ly1g4u0imstg8j313w0pymy6.jpg)

# Approach 1: Backtracking

This is the inefficient solution where we try every single jump pattern that takes us from the first position to the last. We start from the first position and jump to every index that is reachable. We repeat the process until last index is reached. When stuck, backtrack.

``` JAVA
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


# Conclusion


