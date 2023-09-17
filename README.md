#include <iostream>
using namespace std;

// Function to initialize the game board
void initializeBoard(char board[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            board[i][j] = ' ';
        }
    }
}

// Function to display the game board
void displayBoard(char board[3][3]) {
    cout << "  1 2 3" << endl;
    for (int i = 0; i < 3; i++) {
        cout << i + 1 << " ";
        for (int j = 0; j < 3; j++) {
            cout << board[i][j];
            if (j < 2) cout << "|";
        }
        cout << endl;
        if (i < 2) cout << "  -+-+-" << endl;
    }
}

// Function to check if a player has won
bool checkWin(char board[3][3], char player) {
    // Check rows, columns, and diagonals
    for (int i = 0; i < 3; i++) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
            return true;
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player)
            return true;
    }
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player)
        return true;
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player)
        return true;
    return false;
}

// Function to check if the game is a draw
bool checkDraw(char board[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (board[i][j] == ' ')
                return false;
        }
    }
    return true;
}

int main() {
    char board[3][3];
    char currentPlayer = 'X';
    bool gameWon = false;
    bool gameDraw = false;

    initializeBoard(board);

    while (!gameWon && !gameDraw) {
        displayBoard(board);
        cout << "Player " << currentPlayer << ", enter your move (row and column): ";
        int row, col;
        cin >> row >> col;

        // Check if the input is valid
        if (row < 1 || row > 3 || col < 1 || col > 3 || board[row - 1][col - 1] != ' ') {
            cout << "Invalid move! Try again." << endl;
            continue;
        }

        // Update the board with the player's move
        board[row - 1][col - 1] = currentPlayer;

        // Check for a win or draw
        gameWon = checkWin(board, currentPlayer);
        gameDraw = checkDraw(board);

        // Switch players
        currentPlayer = (currentPlayer == 'X') ? 'O' : 'X';
    }

    displayBoard(board);

    if (gameWon) {
        cout << "Player " << currentPlayer << " wins!" << endl;
    } else {
        cout << "It's a draw!" << endl;
    }

    cout << "Do you want to play again? (Y/N): ";
    char playAgain;
    cin >> playAgain;

    if (playAgain == 'Y' || playAgain == 'y') {
        main(); // Restart the game
    }

    return 0;
}

