#include<iostream>
using namespace std;

bool placeMark(char board[][3], int position, char mark){
    int raw = (position-1)/3;
    int col = (position-1)%3;

    if(board[raw][col] != 'X' && board[raw][col] != 'O'){
        board[raw][col] = mark;
        return true;
    }
    else{
        return false;
    }
}
bool checkWin(char board[][3]){

    for(int i=0; i<3; i++){
        // checking for raw
        if(board[i][0] == board[i][1] && board[i][1] == board[i][2]){
            return true;
        }
        // checking for col
        if(board[0][i] == board[1][i] && board[1][i] == board[2][i]){
            return true;
        }
    }
    // checking for diagonal
    if(board[0][0] == board[1][1] && board[1][1] == board[2][2]){
        return true;
    }
    if(board[0][2] == board[1][1] && board[1][1] == board[2][0]){
        return true;
    }

    return false;
}
bool checkDraw(char board[][3]){
    for(int i=0; i<3; i++){
        for(int j=0; j<3; j++){
            if(board[i][j] != 'X' && board[i][j] != 'O'){
                return false;
            }
        }
    }
    return true;
}

void resetBoard(char board[][3]){
    char val = '1';
    for(int i=0; i<3; i++){
        for(int j=0; j<3; j++){
            board[i][j] = val++;
        }
    }
}

void printboard(char board[][3]){
    for(int i=0; i<3; i++){
        for(int j=0; j<3; j++){
            if(j != 0){
                cout<<"|";
            }
            cout<<board[i][j];
        }
        cout<<endl;
    }
    cout<<endl;
}
int main(){
    char board[3][3] = {{'1','2','3'},{'4','5','6'},{'7','8','9'}};
    
    char player;
    int position;
    bool gameOver;

    char play;

    do{
        resetBoard(board);
        player = 'X';
        gameOver = false;

        printboard(board);

        while(!gameOver){

            cout<<"player "<<player<<" choose a move between (1-9) : ";
            cin>>position;

            // if position is ok then mark else show in valid input

            if(placeMark(board,position,player)){
                printboard(board);
                // checking for win
                if(checkWin(board)){
                    cout<<"player "<<player<<" wins !!"<<endl;
                    gameOver = true;

                }
                // checking for draw
                else if(checkDraw(board)){
                    cout<<"game draw !!"<<endl;
                    gameOver = true;
                }
                // switching turn
                else{
                    player = (player == 'X')? 'O':'X'; 
                }
            }

            else{
                cout<<"In valid move try again !!"<<endl;
            }
        }

        cout<<" Do want to play again (y/n) : ";
        cin>>play;

    }while(play == 'y' || play == 'Y');

}
