# gameom
game
import random

def create_board(size=4):
    board = list(range(1, size*size)) + [0]
    random.shuffle(board)
    return [board[i*size:(i+1)*size] for i in range(size)]

def print_board(board):
    size = len(board)
    for row in board:
        print(' '.join(f"{n:2}" if n != 0 else '  ' for n in row))
    print()

def find_zero(board):
    for i, row in enumerate(board):
        for j, val in enumerate(row):
            if val == 0:
                return i, j

def move(board, direction):
    size = len(board)
    x, y = find_zero(board)
    dx, dy = {'w':(-1,0), 's':(1,0), 'a':(0,-1), 'd':(0,1)}.get(direction, (0,0))
    nx, ny = x + dx, y + dy
    if 0 <= nx < size and 0 <= ny < size:
        board[x][y], board[nx][ny] = board[nx][ny], board[x][y]
        return True
    return False

def is_solved(board):
    size = len(board)
    nums = [num for row in board for num in row]
    return nums == list(range(1, size*size)) + [0]

def main():
    print("Welcome to the Sliding Puzzle! Use w/a/s/d to move, q to quit.")
    board = create_board()
    while not is_solved(board):
        print_board(board)
        move_input = input("Move (w/a/s/d): ").lower()
        if move_input == 'q':
            print("Goodbye!")
            break
        if not move(board, move_input):
            print("Invalid move!")
    else:
        print_board(board)
        print("Congratulations! You solved the puzzle.")

if __name__ == "__main__":
    main()
    
