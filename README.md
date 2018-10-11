# peakfind

#include<fstream>
#include<iostream>
#include<stdlib.h>
#include<time.h>
#include<queue>
using namespace std;
int main(){
	int m,n;
	int ans=0;
	ifstream inFile("matrixsmall.data",ios::in);
	ofstream outFile("final.peak",ios::out);
	inFile >> m >> n;
	cout << m <<" " << n << endl;
	queue <int*> B;
	int A[m][n];
	queue <int> Ax,Ay;
	for(int i =0;i<m;i++){
		for(int j =0;j<n;j++){
			inFile >> A[i][j];
		}
	}
	for(int i=0;i<m;i++){
		for(int j=0;j<n;j++){
			if(i==0){
				if(j==0){
					if(A[i][j]>=A[i][j+1]&&A[i][j]>=A[i+1][j]){
						Ax.push(i+1);
						Ay.push(j+1);
						ans++;
					}
				}
				else if (j == n-1){
					if(A[i][j]>=A[i][j-1]&&A[i][j]>=A[i+1][j]){
						Ax.push(i+1);
						Ay.push(j+1);
						ans++;
					}
				}
				else{
					if(A[i][j]>=A[i+1][j]&&A[i][j]>=A[i][j-1]&&A[i][j]>=A[i][j+1]){
						Ax.push(i+1);
						Ay.push(j+1);
						ans++;
					}
				}
			}
			else if(i==m-1){
				if(j==0){
					if(A[i][j]>=A[i][j+1]&&A[i][j]>=A[i-1][j]){
						Ax.push(i+1);
						Ay.push(j+1);
						ans++;
					}
				}
				else if (j == n-1){
					if(A[i][j]>=A[i][j-1]&&A[i][j]>=A[i-1][j]){
						Ax.push(i+1);
						Ay.push(j+1);
						ans++;
					}
				}
				else{
					if(A[i][j]>=A[i-1][j]&&A[i][j]>=A[i][j-1]&&A[i][j]>=A[i][j+1]){
						Ax.push(i+1);
						Ay.push(j+1);
						ans++;
					}
				}
			}
			else {
				if(A[i][j]>=A[i-1][j]&&A[i][j]>=A[i+1][j]&&A[i][j]>=A[i][j-1]&&A[i][j]>=A[i][j+1]){
					Ax.push(i+1);
					Ay.push(j+1);
					ans++;
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
	}
	return 0;
}
