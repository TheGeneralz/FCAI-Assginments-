# File:Connect four

# purpose:Play connect four with your friends and have fun

# Author:Mohamed Rashed

# Id:20230335

# you will have to download pygame and numpy to play the game
import sys
import numpy as np
import pygame
import math

# The colores that are being used
BLUE = (0, 0, 200)
BLACK = (0, 0, 0)
RED = (200, 0, 0)
YELLOW = (200, 200, 0)

# The row and column count
row_count = 6
col_count = 7


# This function just creates the board
def create_board():
    board = np.zeros((row_count, col_count))
    return board


# This function draws the board
def draw_board(board):
    # This draws the board
    for c in range(col_count):
        for r in range(row_count):
            # Drawing a blue colour for the board itself and black colour for the background
            pygame.draw.rect(screen, BLUE, (c * SQUARESIZE, r * SQUARESIZE + SQUARESIZE, SQUARESIZE, SQUARESIZE))
            pygame.draw.circle(screen, BLACK, (
                int(c * SQUARESIZE + SQUARESIZE / 2), int(r * SQUARESIZE + SQUARESIZE + SQUARESIZE / 2)), RADIUS)

    for c in range(col_count):
        for r in range(row_count):

            # This draws a red circle for the first player
            if board[r][c] == 1:
                pygame.draw.circle(screen, RED,
                                   (int(c * SQUARESIZE + SQUARESIZE / 2), hight - int(r * SQUARESIZE + SQUARESIZE / 2)),
                                   RADIUS)

            # This draws a Yellow circle for the 2nd player
            elif board[r][c] == 2:
                pygame.draw.circle(screen, YELLOW,
                                   (int(c * SQUARESIZE + SQUARESIZE / 2), hight - int(r * SQUARESIZE + SQUARESIZE / 2)),
                                   RADIUS)
    pygame.display.update()


# This function is used for
def drop_piece(board, row, move, piece):
    board[row][move] = piece


# This function is used to check if the place we put the circus at is valid
def valid_location(board, move):
    return board[row_count - 1][move] == 0


# This function checks for open rows
def get_open_row(board, move):
    for r in range(row_count):
        if board[r][move] == 0:
            return r


# This function checks for the winning move
def Winning(board, piece):
    # Horizontal winning
    for c in range(col_count - 3):
        for r in range(row_count):

            # The row stays the same and the column inc. by one
            if board[r][c] == piece and board[r][c + 1] == piece and board[r][c + 2] == piece and board[r][c + 3] == piece:
                return True

    # Vertical winning
    for c in range(col_count):
        for r in range(row_count - 3):

            # The column stays the same and the row inc. by one
            if board[r][c] == piece and board[r + 1][c] == piece and board[r + 2][c] == piece and board[r + 3][c] == piece:
                return True

    # Diagonal +ve winning
    for c in range(col_count - 3):
        for r in range(row_count - 3):

            # The column and the row inc. by one
            if board[r][c] == piece and board[r + 1][c + 1] == piece and board[r + 2][c + 2] == piece and board[r + 3][
                c + 3] == piece:
                return True

    # Diagonal -ve winning
    for c in range(col_count - 3):
        for r in range(3, row_count):

            # The column inc. by one and the row dec. by one
            if board[r][c] == piece and board[r - 1][c + 1] == piece and board[r - 2][c + 2] == piece and board[r - 3][
                c + 3] == piece:
                return True


# This function is needed for the matrix
def print_board(board):
    print(np.flip(board, 0))


# I'm pretty sure you can figure everything by its name but just for good measure
# create the board and print ps:you have to create the board then draw it then display it
board = create_board()
print(board)

game_over = False
turn = 0

pygame.init()

# Needing equations for the board and circles
SQUARESIZE = 100
width = col_count * SQUARESIZE
hight = (row_count + 1) * SQUARESIZE
size = (width, hight)

# To display the screen
screen = pygame.display.set_mode(size)
RADIUS = int(SQUARESIZE / 2 - 5)

# Drawing the board and displaying it
draw_board(board)
pygame.display.update()

myfont = pygame.font.SysFont('monospace', 75)

# The main part of the code
while not game_over:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            sys.exit()

        # This if statement is where I make the circles follow the mouse pointer
        if event.type == pygame.MOUSEMOTION:
            pygame.draw.rect(screen, BLACK, (0, 0, width, SQUARESIZE))
            posx = event.pos[0]

            # If player 1
            if turn == 0:
                pygame.draw.circle(screen, RED, (posx, int(SQUARESIZE / 2)), RADIUS)
            # If player 2
            else:
                pygame.draw.circle(screen, YELLOW, (posx, int(SQUARESIZE / 2)), RADIUS)
        pygame.display.update()

        # if the user press the left mouse button
        if event.type == pygame.MOUSEBUTTONDOWN:

            # Here we use all the previous functions to check every thing we do this for both players

            # If player 1
            if turn == 0:
                posx = event.pos[0]
                move = int(math.floor(posx / SQUARESIZE))

                if valid_location(board, move):
                    row = get_open_row(board, move)
                    drop_piece(board, row, move, 1)

                    if Winning(board, 1):
                        Label = myfont.render('Player 1 wins!!', 1, RED)
                        screen.blit(Label, (40, 10))
                        game_over = True

            # If player 2
            else:
                posx = event.pos[0]
                move = int(math.floor(posx / SQUARESIZE))

                if valid_location(board, move):
                    row = get_open_row(board, move)
                    drop_piece(board, row, move, 2)
                    if Winning(board, 2):
                        Label = myfont.render('Player 2 wins!!', 1, YELLOW)
                        screen.blit(Label, (40, 10))
                        game_over = True

            print_board(board)
            draw_board(board)
            turn += 1
            turn = turn % 2

            if game_over:
                pygame.time.wait(3000)
