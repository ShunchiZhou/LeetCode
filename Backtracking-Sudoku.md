
Sudoku is a 9x9 matrix filled with numbers 1 to 9 in such a way that every row, column and sub-matrix (3x3) has each of the digits from 1 to 9. We are provided with a partially filled 9x9 matrix and have to fill every remaining cell in it.

You can see that every row, column, and sub-matrix (3x3) contains each digit from 1 to 9. Thus, we can also conclude that a Sudoku is considered wrongly filled if it satisfies any of these criteria:

1. Any row contains the same number more than once.
2. Any column contains the same number more than once.
3. Any 3x3 sub-matrix has the same number more than once.

In backtracking, we first start with a sub-solution and if this sub-solution doesn't give us a correct final answer, then we just come back and change our sub-solution. We are going to solve our Sudoku in a similar way. The steps which we will follow are:

- If there are no unallocated cells, then the Sudoku is already solved. We will just return true.
- Or else, we will fill an unallocated cell with a digit between 1 to 9 so that there are no conflicts in any of the rows, columns, or the 3x3 sub-matrices.
- Now, we will try to fill the next unallocated cell and if this happens successfully, then we will return true.
- Else, we will come back and change the digit we used to fill the cell. If there is no digit which fulfills the need, then we will just return false as there is no solution of this Sudoku.

```JAVA
class Sudoku
{

	private static final int SIZE = 9;
	private static int[][] matrix = {
		{6,5,0,8,7,3,0,9,0},
		{0,0,3,2,5,0,0,0,8},
		{9,8,0,1,0,4,3,5,7},
		{1,0,5,0,0,0,0,0,0},
		{4,0,0,0,0,0,0,0,2},
		{0,0,0,0,0,0,5,0,3},
		{5,7,8,3,0,1,0,2,6},
		{2,0,0,0,4,8,9,0,0},
		{0,9,0,6,2,5,0,8,1}
	};

	private static void printSudoku()
	{
		for(int i=0;i<SIZE;i++)
		{
			for(int j=0;j<SIZE;j++)
			{
				System.out.print(matrix[i][j]+" ");
			}
			System.out.println("");
		}
	}


	//function to check if we can put a
	//value in a paticular cell or not
	private static boolean isSafe(int n, int r, int c)
	{
		//checking in row
		for(int i=0;i<SIZE;i++)
		{
			//there is a cell with same value
			if(matrix[r][i] == n)
				return false;
		}
		//checking column
		for(int i=0;i<SIZE;i++)
		{
			//there is a cell with the value equal to i
			if(matrix[i][c] == n)
				return false;
		}
		//checking sub matrix
		int row_start = (r/3)*3;
		int col_start = (c/3)*3;
		for(int i=row_start;i<row_start+3;i++)
		{
			for(int j=col_start;j<col_start+3;j++)
			{
				if(matrix[i][j]==n)
					return false;
			}
		}
		return true;
	}

	//function to solve sudoku
	//using backtracking
	public static boolean solveSudoku()
		{
			for(int row=0;row<9;row++)
			{
				for(int col=0;col<9;col++)
				{
					if(matrix[row][col]==0)
					{
						for(int i=1;i<=SIZE;i++)
						{
							if(isSafe(i, row, col))
							{
								matrix[row][col] = i;
								if(solveSudoku())
									return true;
								else
									matrix[row][col] = 0;
							}
						}
						return false;
					}
				}
			}
			return true;
		}

	public static void main(String[] args)
	{
		if (solveSudoku())
			printSudoku();
		else
			System.out.println("No solution");
	}
}
```
![](https://ws1.sinaimg.cn/large/006tNc79ly1g4u8qbr4xlj308u09ydft.jpg)