#include <iostream>
#include <time.h>
using namespace std;

char board[3][3][3];
int choice;
char player = 'X', opponent = 'O'; 
int win;

struct Move 
{ 
	int row, col, bestVal; 
}; 

class Cube{
    public:
        char backBoard[3][3];
        char middleFacingBoard[3][3];
        char frontBoard[3][3];

        char leftBoard[3][3];
        char middleSideBoard[3][3];
        char rightBoard[3][3];

        char leftDiagBoard[3][3];
        char rightDiagBoard[3][3];

        void updateBoards(){
            char temp;
            //back
            for (int x = 0; x < 3; ++x) {
                temp = board[0][0][x];
                backBoard[x][0] = leftBoard[x][2] = leftDiagBoard[x][0] = temp;
                temp = board[0][1][x];
                backBoard[x][1] = middleSideBoard[x][2] = temp;
                temp = board[0][2][x];
                backBoard[x][2] = rightBoard[x][2] = rightDiagBoard[x][2] = temp;
            }

            //middle
            for (int x = 0; x < 3; ++x) {
                temp = board[1][0][x];
                middleFacingBoard[x][0] = leftBoard[x][1] = temp;
                temp = board[1][1][x];
                middleFacingBoard[x][1] = middleSideBoard[x][1] = leftDiagBoard[x][1] = rightDiagBoard[x][1] = temp;
                temp = board[1][2][x];
                middleFacingBoard[x][2] = rightBoard[x][1] = temp;
            }

            //front
            for (int x = 0; x < 3; ++x) {
                temp = board[2][0][x];
                frontBoard[x][0] = leftBoard[x][0] = rightDiagBoard[x][0] = temp;
                temp = board[2][1][x];
                frontBoard[x][1] = middleSideBoard[x][0] = temp;
                temp = board[2][2][x];
                frontBoard[x][2] = rightBoard[x][0] = leftDiagBoard[x][2] = temp;
            }
        }
}cube;

class AI{
    public:
    int evaluate(char b[3][3], char first, char second){
        // Checking for Rows for X or O victory. 
        for(int row = 0; row<3; row++){ 
            if(b[row][0] == b[row][1] && b[row][1] == b[row][2]){ 
                if(b[row][0] == first){
                    return 10; 
                }else{
                    if(b[row][0] == second){
                        return -10;
                    }
                }
            }
        }

        // Checking for Columns for X or O victory. 
        for(int col = 0; col<3; col++){ 
            if(b[0][col] == b[1][col] && b[1][col] == b[2][col]){ 
                if(b[0][col] == first){
                    return 10; 
                }else{
                    if(b[0][col] == second){
                        return -10;
                    }
                }
            }
        }

        // Checking for Diagonals for X or O victory. 
        if(b[0][0] == b[1][1] && b[1][1] == b[2][2]){
            if(b[0][0] == first){
                return 10; 
            }else{
                if(b[0][0] == second){
                    return -10;
                }
            }
        } 

        if(b[0][2] == b[1][1] && b[1][1] == b[2][0]){ 
            if(b[0][2] == first){
                return 10; 
            }else{
                if(b[0][2] == second){
                    return -10;
                }
            }
        } 

        // Else if none of them have won then return 0 
        return 0; 
    } 

    int minimax(char board[3][3], int depth, bool isMax, char first, char second){ 
        int score = evaluate(board, first, second); 

        // If Maximizer has won the game return his/her 
        // evaluated score 
        if(score == 10){ 
            return score;
        }

        // If Minimizer has won the game return his/her 
        // evaluated score 
        if(score == -10){ 
            return score; 
        }

        // If this maximizer's move 
        if(isMax){ 
            int best = -1000; 

            // Traverse all cells 
            for(int i = 0; i<3; i++){ 
                for(int j = 0; j<3; j++){ 
                    // Check if cell is empty 
                    if(board[i][j] != player && board[i][j] != opponent){   
                        char temp;
                        // Make the move
                        temp = board[i][j];
                        board[i][j] = first; 

                        // Call minimax recursively and choose 
                        // the maximum value 
                        best = max(best, minimax(board, depth+1, !isMax, first, second)); 

                        // Undo the move 
                        board[i][j] = temp; 
                    } 
                } 
            } 
            return best; 
        }else{// If this minimizer's move 
            int best = 1000; 

            // Traverse all cells 
            for(int i = 0; i<3; i++){ 
                for(int j = 0; j<3; j++){ 
                    // Check if cell is empty 
                    if(board[i][j] != player && board[i][j] != opponent){   
                        char temp;
                        // Make the move
                        temp = board[i][j];
                        board[i][j] = second; 

                        // Call minimax recursively and choose 
                        // the minimum value 
                        best = min(best, 
                            minimax(board, depth+1, !isMax, first, second)); 

                        // Undo the move 
                        board[i][j] = temp; 
                    } 
                } 
            } 
            return best; 
        } 
    } 

    // This will return the best possible move for the player 
    Move findBestMove(char board[3][3], char first, char second) 
    { 
        Move bestMove; 
        bestMove.row = -1; 
        bestMove.col = -1;
        bestMove.bestVal = -1; 

        // Traverse all cells, evaluate minimax function for 
        // all empty cells. And return the cell with optimal 
        // value. 
        for(int i = 0; i<3; i++){ 
            for(int j = 0; j<3; j++){ 
                // Check if cell is empty 
                if(board[i][j] != player && board[i][j] != opponent){ 
                    char temp;
                    // Make the move 
                    temp = board[i][j];
                    board[i][j] = first; 

                    // compute evaluation function for this 
                    // move. 
                    int moveVal = minimax(board, 0, false, first, second); 

                    // Undo the move 
                    board[i][j] = temp; 

                    // If the value of the current move is 
                    // more than the best value, then update 
                    // best/ 
                    if(moveVal > bestMove.bestVal){ 
                        bestMove.row = i; 
                        bestMove.col = j; 
                        bestMove.bestVal = moveVal; 
                    } 
                } 
            } 
        } 
        return bestMove; 
    }
    Move overallBestMove(char symbol, char first, char second){
        Move bestMove;
        bestMove = findBestMove(cube.backBoard, first, second);
        if(bestMove.bestVal == 10){
            board[0][bestMove.col][bestMove.row] = symbol;
            return bestMove;
        }
        bestMove = findBestMove(cube.middleFacingBoard, first, second);
        if(bestMove.bestVal == 10){
            board[1][bestMove.col][bestMove.row] = symbol;
            return bestMove;
        }
        bestMove = findBestMove(cube.frontBoard, first, second);
        if(bestMove.bestVal == 10){
            board[2][bestMove.col][bestMove.row] = symbol;
            return bestMove;
        }

        bestMove = findBestMove(cube.leftBoard, first, second);
        if(bestMove.bestVal == 10){
            board[2 - bestMove.col][0][bestMove.row] = symbol;
            return bestMove;
        }
        bestMove = findBestMove(cube.middleSideBoard, first, second);
        if(bestMove.bestVal == 10){
            board[2 - bestMove.col][1][bestMove.row] = symbol;
            return bestMove;
        }
        bestMove = findBestMove(cube.rightBoard, first, second);
        if(bestMove.bestVal == 10){
            board[2 - bestMove.col][2][bestMove.row] = symbol;
            return bestMove;
        }

        bestMove = findBestMove(cube.leftDiagBoard, first, second);
        if(bestMove.bestVal == 10){
            board[bestMove.col][bestMove.col][bestMove.row] = symbol;
            return bestMove;
        }
        bestMove = findBestMove(cube.rightDiagBoard, first, second);
        if(bestMove.bestVal == 10){
            board[bestMove.col][bestMove.col][bestMove.row] = symbol;
            return bestMove;
        }
        return bestMove;
    }
}ai;

class Player: public Cube{
    public:
        void getMove(char symbol){
            int row = 0;
            int collum = 0;
            int depth = 0;
            for(;;){
                cout << "\nWhich board would you like to go on (1-3): ";
                cin >> depth;

                while(depth != 1 && depth != 2 && depth != 3){
                    cout << "Invalid input. Please try again.";
                    cout << "\nWhich board would you like to go on (1-3): ";
                    cin >> depth;
                }

                depth -= 1;

                cout << "Where would you like to go (1-9): ";
                cin >> choice;
                
                while(choice != 1 && choice != 2 && choice != 3 && choice != 4 && choice != 5 && choice != 6 && choice != 7 && choice != 8 && choice != 9){
                    cout << "Invalid input. Please try again.";
                    cout << "\nWhere would you like to go: ";
                    cin >> choice;
                }

                switch(choice){
                    case 1: case 2: case 3:
                        row = 0;
                        break;
                    case 4: case 5: case 6:
                        row = 1;
                        break;
                    case 7: case 8: case 9:
                        row = 2;
                }

                switch(choice){
                    case 1: case 4: case 7:
                        collum = 0;
                        break;
                    case 2: case 5: case 8:
                        collum = 1;
                        break;
                    case 3: case 6: case 9:
                        collum = 2;
                }

                if(board[row][collum][depth] != 'X' && board[row][collum][depth] != 'O'){
                    board[row][collum][depth] = symbol;
                    break;
                }
                cout << "That space is taken! Please try again. ";
            }
        }
}human;

class Game: public Player{
    public:
    void checkWinMinor(char array[3][3], char symbol){
        if(array[0][0] == symbol && array[0][1] == symbol && array[0][2] == symbol){
            //XXX
            //
            //
            win = 1;
        }else{
            if(array[1][0] == symbol && array[1][1] == symbol && array[1][2] == symbol){
                //
                //XXX
                //
                win = 1;
            }else{
                if(array[2][0] == symbol && array[2][1] == symbol && array[2][2] == symbol){
                    //
                    //
                    //XXX
                    win = 1;
                }else{
                    if(array[0][0] == symbol && array[1][0] == symbol && array[2][0] == symbol){
                        //X
                        //X
                        //X
                        win = 1;
                    }else{
                        if(array[0][1] == symbol && array[1][1] == symbol && array[2][1] == symbol){
                            // X
                            // X
                            // X
                            win = 1;
                        }else{
                            if(array[0][2] == symbol && array[1][2] == symbol && array[2][2] == symbol){
                                //  X
                                //  X
                                //  X
                                win = 1;
                            }else{
                                if(array[0][0] == symbol && array[1][1] == symbol && array[2][2] == symbol){
                                    //X
                                    // X
                                    //  X
                                    win = 1;
                                }else{
                                    if(array[0][2] == symbol && array[1][1] == symbol && array[2][0] == symbol){
                                        //  X
                                        // X
                                        //X
                                        win = 1;
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }

    void checkWinMajor(char symbol){
        cube.updateBoards();

        checkWinMinor(cube.backBoard, symbol);
        checkWinMinor(cube.middleFacingBoard, symbol);
        checkWinMinor(cube.frontBoard, symbol);

        checkWinMinor(cube.leftBoard, symbol);
        checkWinMinor(cube.middleSideBoard, symbol);
        checkWinMinor(cube.rightBoard, symbol);

        checkWinMinor(cube.leftDiagBoard, symbol);
        checkWinMinor(cube.rightDiagBoard, symbol);
    }

    void printCube(){
        //top board
        cout << board[0][0][0] << "|" << board[0][1][0] << "|" << board[0][2][0];
        cout << "\n-----\n";
        cout << board[1][0][0] << "|" << board[1][1][0] << "|" << board[1][2][0];
        cout << "\n-----\n";
        cout << board[2][0][0] << "|" << board[2][1][0] << "|" << board[2][2][0];

        //middle board
        cout << "\n     " << board[0][0][1] << "|" << board[0][1][1] << "|" << board[0][2][1];
        cout << "\n     -----\n";
        cout << "     " << board[1][0][1] << "|" << board[1][1][1] << "|" << board[1][2][1];
        cout << "\n     -----\n";
        cout << "     " << board[2][0][1] << "|" << board[2][1][1] << "|" << board[2][2][1];

        //bottom board
        cout << "\n          " << board[0][0][2] << "|" << board[0][1][2] << "|" << board[0][2][2];
        cout << "\n          -----\n";
        cout << "          " << board[1][0][2] << "|" << board[1][1][2] << "|" << board[1][2][2];
        cout << "\n          -----\n";
        cout << "          " << board[2][0][2] << "|" << board[2][1][2] << "|" << board[2][2][2];
    }
}game;

void play(char symbol){
    game.printCube();
    human.getMove(symbol);
    game.checkWinMajor(symbol);
    if(win == 1){
        game.printCube();
        cout << "\nPlayer " << symbol << " wins!!!";
        return;
    }
}

int main(){
    char num;
    char answer;
    int numPlayers;
    int turn;
    int random;

    for(;;){
        win = 0;
        cout << "(1) Player vs Player\n"
                "(2) Player vs Computer\n"
                "What would you like to do: ";
        cin >> numPlayers;

        while(numPlayers != 1 && numPlayers != 2){
            cout << "Invalid input. Please try again.";
            cout << "(1) Player vs Player\n"
                    "(2) Player vs Computer\n"
                    "What would you like to do: ";
            cin >> numPlayers;
        }

        if(numPlayers == 2){
            cout << "(1) First\n"
                    "(2) Second\n"
                    "(3) Random\n"
                    "When would you like to go: ";
            cin >> turn;

            while(turn < 1 || turn > 3){
                cout << "Invalid input. Please try again";
                cout << "(1) First\n"
                        "(2) Second\n"
                        "(3) Random\n"
                        "When would you like to go: ";
                cin >> turn;
            }
        }  

        for (int z = 0; z < 3; ++z) {
            num = '1';
            for (int y = 0; y < 3; ++y) {
                for (int x = 0; x < 3; ++x) {
                    board[y][x][z] = num++;
                }
            }
        }

        if(numPlayers == 1){
            for(int i = 0; i < 13; ++i){
                play(player);
                if(win == 1){
                    break;
                }
                play(opponent);
                if(win == 1){
                    break;
                }
            }
        }else{
            if(turn == 1){
                for(int i = 0; i < 13; ++i){
                    game.printCube();
                    game.getMove(opponent);
                    game.checkWinMajor(opponent);
                    if(win == 1){
                        game.printCube();
                        cout << "\nYou won!!!";
                        break;
                    }
                    ai.overallBestMove(player, opponent, player);
                    game.checkWinMajor(player);
                    if(win == 1){
                        game.printCube();
                        cout << "\nThe computer has won!!!";
                        break;
                    }
                }
            }else{
                if(turn == 2){
                    for(int i = 0; i < 13; ++i){
                        ai.overallBestMove(player, player, opponent);
                        game.checkWinMajor(player);
                        game.printCube();
                        if(win == 1){
                            cout << "\nThe computer has won!!!";
                            break;
                        }
                        game.getMove(opponent);
                        game.checkWinMajor(opponent);
                        if(win == 1){
                            game.printCube();
                            cout << "\nYou won!!!";
                            break;
                        }
                    }
                }else{
                    srand(time(0));
                    random = rand() % 2;
                    if(random == 1){
                        cout << "You are going first\n";
                        for(int i = 0; i < 13; ++i){
                            game.printCube();
                            game.getMove(opponent);
                            game.checkWinMajor(opponent);
                            if(win == 1){
                                game.printCube();
                                cout << "\nYou won!!!";
                                break;
                            }
                            ai.overallBestMove(player, opponent, player);
                            game.checkWinMajor(player);
                            if(win == 1){
                                game.printCube();
                                cout << "\nThe computer has won!!!";
                                break;
                            }
                        }
                    }else{
                        cout << "You are going second\n";
                        for(int i = 0; i < 13; ++i){
                            ai.overallBestMove(player, player, opponent);
                            game.checkWinMajor(player);
                            game.printCube();
                            if(win == 1){
                                cout << "\nThe computer has won!!!";
                                break;
                            }
                            game.getMove(opponent);
                            game.checkWinMajor(opponent);
                            if(win == 1){
                                game.printCube();
                                cout << "\nYou won!!!";
                                break;
                            }
                        }
                    }
                }
            }
        }


        if(win == 0){
            cout << "\n";
            game.printCube();
            cout << "\nLooks like a draw!";
        }

        cout << "\nWould you like to play again (y/n): ";
        cin >> answer;

        while(answer != 'y' && answer != 'Y' && answer != 'n' && answer != 'N'){
            cout << "Invalid input. Please try again.";
            cin >> answer;
        }

        if(answer == 'n' || answer == 'N'){
            return 0;
        }
    }
}
