//peakfind

#include<fstream>
#include<iostream>
#include<stdlib.h>
#include<time.h>
#include<queue>
#include<string.h>
using namespace std;

char ifileDir[50];
char ofileDir[50];

ifstream inFile;
ofstream outFile;
	
int main(int argc,char *argv[]){
	int m,n;
	int ans=0;
	if(argc <=1) {
		cout << "參數為空" <<endl;
		return 1;
	}
	strcat(ifileDir,argv[1]);
	strcat(ifileDir,"/matrix.data");
	strcat(ofileDir,argv[1]);
	strcat(ofileDir,"/final.peak");
	inFile.open(ifileDir,ios::in);
	outFile.open(ofileDir,ios::out);
	inFile >> m >> n;
//	cout << m <<" " << n << endl;
	int A[3][n];
	queue <int> Ax,Ay;
	if(m != 1){
	for(int i =0;i<m;i++){
		for(int j =0;j<n;j++){
			inFile >> A[i%3][j];
			if(i>=1){
				if(j>=1){
				int comrow = (i-1)%3;
				int comcol = j-1;
				if(i == 1){
					if(comcol == 0){
						if(A[comrow][comcol]>=A[comrow][comcol+1]&&A[comrow][comcol]>=A[(comrow+1)%3][comcol]){
							Ax.push(i);
							Ay.push(j);
							ans++;
//							cout << "i = " <<i<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][comcol] <<endl << "right = " << A[comrow][comcol+1] <<endl <<"down = " << A[(comrow+1)%3][comcol] <<endl;
						}
					}
					else{
						if(A[comrow][comcol]>=A[(comrow+1)%3][comcol]&&A[comrow][comcol]>=A[comrow][comcol-1]&&A[comrow][comcol]>=A[comrow][comcol+1]){
							Ax.push(i);
							Ay.push(j);
							ans++;
//							cout << "i = " <<i<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][comcol] <<endl <<"left = " << A[comrow][comcol-1] <<endl << "right = " << A[comrow][comcol+1] <<endl <<"down = " << A[(comrow+1)%3][comcol] <<endl;
						}
					}
					if(j == n-1&&A[comrow][j]>=A[comrow][j-1]&&A[comrow][j]>=A[(comrow+1)%3][j]){
						Ax.push(i);
						Ay.push(j+1);
						ans++;
//						cout << "i = " <<i<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][j] <<endl <<"left = " << A[comrow][j-1] <<endl <<"down = " << A[(comrow+1)%3][j] <<endl;
					}
				}
				else{
					if(comcol == 0){
						if(A[comrow][comcol]>=A[comrow][comcol+1]&&A[comrow][comcol]>=A[(comrow+1)%3][comcol]&&A[comrow][comcol]>=A[(comrow+2)%3][comcol]){
							Ax.push(i);
							Ay.push(j);
							ans++;
//							cout << "i = " <<i<<" , j = " << j <<endl << "A[i][j] = " << A[i-1][j-1] <<endl << "right = " << A[comrow][comcol+1] <<endl <<"up = " << A[(comrow+1)%3][comcol] <<endl <<"down = " << A[comrow+1][comcol] <<endl;
						}
					}
					else{
						if(A[comrow][comcol]>=A[(comrow+1)%3][comcol]&&A[comrow][comcol]>=A[(comrow+2)%3][comcol]&&A[comrow][comcol]>=A[comrow][comcol-1]&&A[comrow][comcol]>=A[comrow][comcol+1]){
							Ax.push(i);
							Ay.push(j);
							ans++;
//							cout << "i = " <<i<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][comcol] <<endl <<"left = " << A[comrow][comcol-1] <<endl << "right = " << A[comrow][comcol+1] <<endl <<"up = " << A[(comrow+2)%3][comcol] <<endl <<"down = " << A[(comrow+1)%3][comcol] <<endl;
						}
					}
					if(j == n-1&&A[comrow][j]>=A[comrow][j-1]&&A[comrow][j]>=A[(comrow+1)%3][j]&&A[comrow][j]>=A[(comrow+2)%3][j]){
						Ax.push(i);
						Ay.push(j+1);
						ans++;
//						cout << "i = " <<i<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][comcol] <<endl <<"left = " << A[comrow][comcol-1] <<endl  <<"up = " << A[(comrow+2)%3][comcol] <<endl <<"down = " << A[(comrow+1)%3][comcol] <<endl;
					}	
				}
				}
			}
		}
	}
	for(int j =1;j<n;j++){
		int comrow = (m-1)%3;
		int comcol = j-1;
		if(comcol == 0){
			if(A[comrow][comcol]>=A[(comrow+2)%3][comcol]&&A[comrow][comcol]>=A[comrow][comcol+1]){
				Ax.push(m);
				Ay.push(j);
				ans++;
	//			cout << "i = " <<m<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][comcol] <<endl <<"left = " << A[comrow][comcol-1] <<endl  <<"up = " << A[(comrow+2)%3][comcol] <<endl ;
				}
			}
			else{
				if(A[comrow][comcol]>=A[(comrow+2)%3][comcol]&&A[comrow][comcol]>=A[comrow][comcol+1]&&A[comrow][comcol]>=A[comrow][comcol-1]){
					Ax.push(m);
					Ay.push(j);
					ans++;
		//			cout << "i = " <<m<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][comcol] <<endl <<"left = " << A[comrow][comcol-1] <<endl <<"right = " << A[comrow][comcol+1] << endl <<"up = " << A[(comrow+2)%3][comcol] <<endl ;
				}
			}
			if(j == n-1&&A[comrow][j]>=A[(comrow+2)%3][j]&&A[comrow][j]>=A[comrow][j-1]){
				Ax.push(m);
				Ay.push(j+1);
				ans++;
	//			cout << "i = " <<m<<" , j = " << j <<endl << "A[i][j] = " << A[comrow][comcol] <<endl <<"left = " << A[comrow][comcol-1] <<endl  <<"up = " << A[(comrow+2)%3][comcol] <<endl;
			}
	}
	}
	else if(m == 1){
		for(int j=0;j<n;j++){
			inFile >> A[0][j];
			if(j>=1){
				int comcol = j-1;
				if(comcol == 0){
					if(A[0][comcol]>=A[0][comcol+1]){
						ans++;
						Ax.push(1);
						Ay.push(comcol+1);
					}
				}
				else{
					if(A[0][comcol]>=A[0][comcol-1]&&A[0][comcol]>=A[0][comcol+1]){
						ans++;
						Ax.push(1);
						Ay.push(comcol+1);
					}
				}
				if(j == n-1){
					if(A[0][j]>=A[0][j-1]){
						ans++;
						Ax.push(1);
						Ay.push(j+1);
					}
					}
			}
		}
	}
	cout << ans <<endl;
	outFile << ans <<endl;
	for(int i=0;i<ans;i++){
//		cout << Ax.front() << " " << Ay.front() << endl;
		outFile << Ax.front() << " " << Ay.front() << endl;
		Ax.pop();
		Ay.pop();
//	}
	}
	return 0;
}
