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