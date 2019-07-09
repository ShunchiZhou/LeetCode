Input:
The size of a chess board. Generally, it is 8. as (8 x 8 is the size of a normal chess board.)

Output:
All the possible matrixes that represent in which row and column the N Queens can be placed.
If the solution does not exist, it will return false.

	1 0 0 0 0 0 0 0
	0 0 0 0 0 0 1 0
	0 0 0 0 1 0 0 0
	0 0 0 0 0 0 0 1
	0 1 0 0 0 0 0 0
	0 0 0 1 0 0 0 0
	0 0 0 0 0 1 0 0
	0 0 1 0 0 0 0 0

In this output, the value 1 indicates the correct place for the queens.
The 0 denotes the blank spaces on the chess board.

```JAVA
import java.util.Arrays;

class NQueen
{
	// N x N chessboard
	public static final int N = 8;

	// Function to check if two queens threaten each other or not
	static boolean isSafe(int board[][], int r, int c)
	{
		// return false if two queens share the same column
		for (int i = 0; i < r; i++)
			if (board[i][c] == 1)
				return false;

		// return false if two queens share the same \ diagonal
		for (int i = r, j = c; i >= 0 && j >= 0; i--, j--)
			if (board[i][j] == 1)
				return false;

		// return false if two queens share the same / diagonal
		for (int i = r, j = c; i >= 0 && j < N; i--, j++)
			if (board[i][j] == 1)
				return false;
				
		return true;
	}

	static void nQueen(int board[][], int r)
	{
		// if N queens are placed successfully, print the solution
		if (r == N)
		{
			for (int i = 0; i < N; i++)
			{
				for(int j = 0; j < N; j++)
					System.out.print(board[i][j] + " ");
				System.out.println();
			}
			System.out.println();
			return;
		}

		// place Queen at every square in current row r
		// and recur for each valid movement
		for (int i = 0; i < N; i++)
		{
			// if no two queens threaten each other
			if (isSafe(board, r, i))
			{
				// place queen on current square
				board[r][i] = 1;
				// recur for next row
				nQueen(board, r + 1);
				// backtrack and remove queen from current square
				board[r][i] = 0;
			}
		}
	}

	public static void main(String[] args)
	{
		// board[][] keeps track of position of Queens in
		// the current configuration
		int[][] board = new int[N][N];

		// initialize board[][] by 0
		for (int i = 0; i < N; i++)
		{
			for(int j = 0; j < N; j++)
				board[i][j]=0;
		}
		
		nQueen(board, 0);
	}
}
```