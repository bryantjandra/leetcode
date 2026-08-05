```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        
        for i in range(0, 9):
            mySet = set()
            for j in range(0, 9):
                if board[i][j] in mySet:
                    return False
                elif board[i][j] == '.':
                    continue
                else:
                    mySet.add(board[i][j])
                    continue
        

        for i in range(0, 9):
            mySet = set()
            for j in range(0, 9):
                if board[j][i] in mySet:
                    return False
                elif board[j][i] == '.':
                    continue
                else:
                    mySet.add(board[j][i])
                    continue
        
        for boxRow in range(0,9,3):
            for boxCol in range(0,9,3): # boxRow + boxCol indicate the starting position for each box.
                mySet = set()
                for i in range(boxRow, boxRow + 3):
                    for j in range(boxCol, boxCol + 3):
                        if board[i][j] in mySet:
                            return False
                        elif board[i][j] == '.':
                            continue
                        else:
                            mySet.add(board[i][j])
                            continue

        return True

# 0,0 --> 0,1 --> 0,2 --> 1,0 --> 1,1 --> 1,2 --> 2,0 --> 2,1 --> 2,2
# 0,3 --> 0,4 --> 0,5 --> 1,3 --> 1,4 --> 1,5 --> 2,3 --> 2,4 --> 2,5
# 0,6 --> 0,7 --> 0,8 --> 1,6 --> 1,7 --> 1,8 --> 2,6 --> 2,7 --> 2,8



# 3,0 --> 3,1 --> 3,2 --> 4,0 --> 4,1 --> 4,2 --> 5,0 --> 5,1 --> 5,2
# 3,3 --> 3,4 --> 3,5 --> 4,3 --> 4,4 --> 4,5 --> 5,3 --> 5,4 --> 5,5
# 3,6 --> 3,7 --> 3,8 --> 4,6 --> 4,7 --> 4,8 --> 5,6 --> 5,7 --> 5,8   

```