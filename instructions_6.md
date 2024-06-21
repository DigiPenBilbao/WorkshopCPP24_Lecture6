# Final Project: Tic Tac Toe
The final project is to build a 2 people game: Tic Tac Toe ("3 en Raya" in spanish). This is going to be a turn based game, each turn a player will input the position where they want to put a token. After each turn, it is necessary to check if current player has won, if so the game must end, otherwise it should countinue.

First of all, it is necessary to choose the tokens for each player. Common tokens used in this game are: 'X' an 'O'. Thos values will be stored in variables of type char.
```c++
  char player_1 = 'X';
  char player_2 = 'O';
```
It is also needed to store the values for each cell. As there are 3 rows and 3 columns, it is necessary to make a choice, so what is going to be stored are the values for each row.
```c++
  char row_1[3];
  char row_2[3];
  char row_3[3];
```
Now it is time to initialize this rows with empty values ' '. Lets use a for loop to do that.
```c++
  for (int i = 0; i < 3; i++)
  {
    row_1[i] = ' ';    
    row_2[i] = ' ';    
    row_3[i] = ' ';    
  }
```

It is time to implement a display method that displays the state of the game and at the same time gives the players information of how to input their movement.
```c++
void display(char row_1[], char row_2[], char row_3[])
{
  std::cout << "\n TIC TAC TOE \n";
  std::cout << "1:" << row_1[0] << "   2:" << row_1[1] << "   3:" << row_1[2] << "\n";
  std::cout << "4:" << row_2[0] << "   5:" << row_2[1] << "   6:" << row_2[2] << "\n";
  std::cout << "7:" << row_3[0] << "   8:" << row_3[1] << "   9:" << row_3[2] << "\n";
}
```

It is time to develop a function that asks the player a movement and updates the arrays with the proper movement.
```c++
void input(char current_player, char row_1[], char row_2[], char row_3[])
{
  int position;
  std::cout << "Player " << current_player << " Introduce a position.\n";
  std::cin >> position;
  if (position == 1) row_1[0] = current_player;
  if (position == 2) row_1[1] = current_player;
  if (position == 3) row_1[2] = current_player;
  if (position == 4) row_2[0] = current_player;
  if (position == 5) row_2[1] = current_player;
  if (position == 6) row_2[2] = current_player;
  if (position == 7) row_3[0] = current_player;
  if (position == 8) row_3[1] = current_player;
  if (position == 9) row_3[2] = current_player;  
}
```

To finish with the functions, lets do a function that checks if a player has won. A basic way to do that is check all possibilites, it means each column, each row, and both diagonals. it is going to be a bit repeated code but it will work.
```c++
bool check_winner(char current_player, char row_1[], char row_2[], char row_3[])
{
  //Check rows
  if (row_1[0] == current_player && row_1[1] == current_player && row_1[2] == current_player) return true;
  if (row_2[0] == current_player && row_2[1] == current_player && row_2[2] == current_player) return true;
  if (row_3[0] == current_player && row_3[1] == current_player && row_3[2] == current_player) return true;
  // Check Columns
  if (row_1[0] == current_player && row_2[0] == current_player && row_3[0] == current_player) return true;
  if (row_1[1] == current_player && row_2[1] == current_player && row_3[1] == current_player) return true;
  if (row_1[2] == current_player && row_2[2] == current_player && row_3[2] == current_player) return true;
  // Check diagonals
  if (row_1[0] == current_player && row_2[1] == current_player && row_3[2] == current_player) return true;
  if (row_1[2] == current_player && row_2[1] == current_player && row_3[0] == current_player) return true;  
  return false;
}
```

Now it is time to put it together inside a while loop that will manage the turn of each player. This code must be inside the main function after the initializations already made.
```c++
  int movements = 0;
  while (movements < 9)
  {    
    display(row_1, row_2, row_3);
    input(current_player, row_1, row_2, row_3);
    if (check_winner(current_player, row_1, row_2, row_3))
    {
      std::cout << "\n CONGRATULATIONS PLAYER: " << current_player << " YOU WON!!";
      break;
    }
    else
    {
      if (current_player == player_1)  
      {
        current_player = player_2;
      }
      else
      {
        current_player = player_1;
      }
    }
    movements++;
  } 
  if (movements == 9)
  {
    std::cout << "\nTHERE IS A TIE!!!";
  }
  ```