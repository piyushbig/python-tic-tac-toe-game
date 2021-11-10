# python-tic-tac-toe-game
It consist the all python code of a game called tic tac toe
#HERE WE IMPORT CLEAR_OUTPUT() WHICH WILL CLEAR OUT THE BAORD WHEN FUNCTION CALLED AGAIN AND AGAIN


from IPython.display import clear_output
#FIRST WE CREATE A BOARD TO PLAY

def display_board(board):
    clear_output()  # Remember, this only works in jupyter!
    
    print('   |   |')
    print(' ' + board[7] + ' | ' + board[8] + ' | ' + board[9])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[4] + ' | ' + board[5] + ' | ' + board[6])
    print('   |   |')
    print('-----------')
    print('   |   |')
    print(' ' + board[1] + ' | ' + board[2] + ' | ' + board[3])
    print('   |   |')


#Here we can check our output
board=['#','X','O','X','O','X','O','X','O','X']
display_board(board)


"""NEXT we will define a function who take input from the plyer and assign their markers to 'x' or 'o'"""


def player_input():

    marker = ''
    
    while marker !='x' and marker !='o':
        marker = input("pick up any x or y: ")
        
    player1 = marker
        
    if player1 =='x':
        player2 ='o'
    else:
        player2 ='x'
            
    return (player1,player2)
    
    player_input()
    
    
 """NEXT we will write a function that takes in the board list object, a marker ('X' or 'O'), 
and a desired position (number 1-9) and assigns it to the board."""


def place_marker(board, marker, position):
    
    board[position]=marker
    
    
 
 """NEXT We will write Write a function that takes in a board and checks to see if someone has won."""
 
 
def win_check(board,mark):
    
    return ((board[7] == mark and board[8] == mark and board[9] == mark) or # across the top
    (board[4] == mark and board[5] == mark and board[6] == mark) or # across the middle
    (board[1] == mark and board[2] == mark and board[3] == mark) or # across the bottom
    (board[7] == mark and board[4] == mark and board[1] == mark) or # down the middle
    (board[8] == mark and board[5] == mark and board[2] == mark) or # down the middle
    (board[9] == mark and board[6] == mark and board[3] == mark) or # down the right side
    (board[7] == mark and board[5] == mark and board[3] == mark) or # diagonal
    (board[9] == mark and board[5] == mark and board[1] == mark)) # diagonal
    
win_check(board,'X')


"""NEXT we will write a function that uses the random module to randomly decide which player goes first. You may want to lookup random.randint() 
Return a string of which player went first."""

import random

def choose_first():
    if random.randint(0, 1) == 0:
        return 'Player 2'
    else:
        return 'Player 1'
        
 """NEXT we will Write a function that returns a boolean indicating whether a space on the board is freely available."""

def space_check(board,position):
    return board[position]==' '
    
    
"""NEXT we will Write a function that checks if the board is full and returns a boolean value. True if full, False otherwise."""
def full_board_check(board):
    for i in range(1,10):
        if space_check(board, i):
            return False
    return True
    
    
"""NEXT we will Write a function that asks for a player's next position (as a number 1-9) and then uses the function from step 6 to check if its a free position. 
If it is, then return the position for later use."""

def player_choice(board):
    position = 0
    
    while position not in [1,2,3,4,5,6,7,8,9] or not space_check(board, position):
        position = int(input('Choose your next position (1-9): '))
        
    return position
    
    
    
"""NEXT we will Write a function that asks the player if they want to play again and returns a boolean True if they do want to play again."""

def replay():
    
    return input('Do you want to play again? Enter Yes or No: ').lower().startswith('y')
    
    
"""the final touch code algorithm to implement all functions"""   
    
print("welcome to the game tic tac toe")

while True:
    # Reset the board
    theBoard = [' '] * 10
    player1_marker, player2_marker = player_input()
    turn = choose_first()
    print(turn + ' will go first.')
    
    play_game = input('Are you ready to play? Enter Yes or No.')
    
    if play_game.lower()[0] == 'y':
        game_on = True
    else:
        game_on = False

    while game_on:
        if turn == 'Player 1':
            # Player1's turn.
            
            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player1_marker, position)

            if win_check(theBoard, player1_marker):
                display_board(theBoard)
                print('Congratulations! You have won the game!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a draw!')
         else:
            turn = 'Player 2'
        
            display_board(theBoard)
            position = player_choice(theBoard)
            place_marker(theBoard, player2_marker, position)

            if win_check(theBoard, player2_marker):
                display_board(theBoard)
                print('Player 2 has won!')
                game_on = False
            else:
                if full_board_check(theBoard):
                    display_board(theBoard)
                    print('The game is a draw!')
                    break
                else:
                   turn = 'Player 1'

    if not replay():
        break           
