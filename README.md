#include <iostream>
#include <fstream>
#include <utility>
#include <string.h>
using namespace std;

int main(int argc, char *argv[])
{
    int m, n;
    int (*matr)[1000] = new int [1000][1000];
    int (*peak)[2] = new int [1000000][2];
    //pair <int , int > peak[100000];
    int count = 0;
    int check = 0;
    ifstream infile;
    ofstream outfile;
    *strrchr(argv[0], '\\') = '\0';
    string path;
    string pathin, pathout;

    //path = string(argv[0]) + "\\"  + argv[1] + "\\";

   /* if(argc != 2){
        cout << "Input error." << endl;
        return 1;
    }
    else if(!infile){
        cout << "Can not open the file." << endl;
        return 1;
    }
    else{*/
        //pathin = path + "matrix.data";
        infile.open("TA_matrix_1.data");
        //pathout = path + "final.peak";
        outfile.open("TA_final_1.peak");
    
        infile>>m>>n;
        for( int i = 1; i <= m; i++)
            for( int j = 1 ; j <= n; j++)
                infile>>matr[i][j];

        for( int i = 1; i <= m; i++){
            for( int j = 1; j <= n; j++){
                //cout<<"i = "<<i<<"   j = "<<j<<endl;
                if( i > 1){
                    if(matr[i][j]>=matr[i-1][j]) check = 1;
                    else continue;
                }
                if( i < m){
                    if(matr[i][j]>=matr[i+1][j]) check = 1;
                    else continue;
                }
                if( j > 1){
                    if(matr[i][j]>=matr[i][j-1]) check = 1;
                    else continue;
                }
                if( j < n){
                    if(matr[i][j]>=matr[i][j+1]) check = 1;
                    else continue;
                }
     
                if( check == 1 ){
                    //peak[count].first = i;
                    //peak[count].second = j;
                    peak[count][0] = i;
                    peak[count][1] = j;
                    count++;
                }      
            }
        }

        outfile<<count<<endl;
        for( int i = 0; i < count; i++)
           // outfile<<peak[i].first<<" "<<peak[i].second<<endl;
            outfile<<peak[i][0]<<" "<<peak[i][1]<<endl;
        infile.close();
        outfile.close();
        return 0;
    //}
}
