import random
from os import system, name
dx = [-1,-1,-1,0,0,1,1,1]
dy = [-1,0,1,-1,1,-1,0,1]

#Clearing the console
def clear(): 
    if name == 'nt': 
        _ = system('cls') 
    else: 
        _ = system('clear') 

n = int(input("Board size:"))
k = int(input("Number of bombs:"))

Board = [[0 for i in range(n+2)] for i in range(n+2)]
VisibleBoard = [['X' for i in range(n+2)] for i in range(n+2)]
VisitedBoard = [[0 for i in range(n+2)] for i in range(n+2)]

#Initialazing the board
#With random bombs places
#And calculating after placing bombs each value in the matrix
def init():
	global n
	global k
	for q in range(1,k+1):
		while True:
			i = random.randint(1,n)
			j = random.randint(1,n)
			if Board[i][j] == 0:
				Board[i][j] = -1
				break
	for i in range(1,n+1):
		for j in range(1,n+1):
			if Board[i][j] != -1:
				sum = 0
				for q in range(0,8):
					if Board[i+dx[q]][j+dy[q]] == -1:
						sum += 1
				Board[i][j] = sum

#Function to print the board
def print_Board(to_print_Board):
	global n
	for i in range(1,n+1):
		for j in range(1,n+1):
			print(to_print_Board[i][j], end=" ")
		print('\n', end="")

#Winning condition
def Won():
	sum = 0
	for i in range(1,n+1):
		for j in range(1,n+1):
			sum += VisitedBoard[i][j]
	if sum == n*n:
		return 1
	else:
		return 0

#To see if i went out if the matrix
def inMatrix(x):
	if x<1 or x>n:
		return 0
	return 1

#The function that discovers all the blocks with 0 in them
def Discover(x,y):
	VisitedBoard[x][y] = 1
	VisibleBoard[x][y] = 0
	for q in range(0,8):
		if VisitedBoard[x+dx[q]][y+dy[q]] == 0 and inMatrix(x+dx[q]) and inMatrix(y+dy[q]):
			VisitedBoard[x+dx[q]][y+dy[q]] = 1
			if Board[x+dx[q]][y+dy[q]] == 0:
				Discover(x+dx[q],y+dy[q])
			else:
				VisibleBoard[x+dx[q]][y+dy[q]] = Board[x+dx[q]][y+dy[q]]

#The actual game
def Game():
	global k
	while True:
		clear()
		print_Board(VisibleBoard)
		print("Choose an action:")
		print("1 for setting a flag")
		print("2 for choosing a tile")
		action = int(input())
		x = int(input("Line tile:"))
		y = int(input("Column tile:"))
		if action == 1:
			VisitedBoard[x][y] = 1
			VisibleBoard[x][y] = 'F'
			k -= 1
			if k == 0 and Won() == 1:
				print("Game is won!")
				break
		elif Board[x][y] == -1:
			print("Game Over!")
			print_Board(Board)				
			break
		elif Board[x][y] == 0:
			Discover(x,y)
		else:
			VisitedBoard[x][y] = 1
			VisibleBoard[x][y] = Board[x][y]

init()
Game()
