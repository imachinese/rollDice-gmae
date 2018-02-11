# rollDice-gmae
c++
#include<iostream>
#include<cstdlib>
#include<ctime>
using namespace std;
int rollDice();
enum position{CONTINUE,WIN,LOSE};
void main()
{
	srand((unsigned)time(NULL));
	const int N = 1000000;
	int sum, mypoint;
	double roll_times=0.0;
	int win_num=0, lose_num=0;
	position gameState;
	for (int i = 0; i < N; i++)
	{
		sum = rollDice();
		roll_times++;
		switch (sum)
		{
		case 7:
		case 11:
			gameState = WIN;
			break;
		case 2:
		case 3:
		case 12:
			gameState = LOSE;
			break;
		default:
			gameState = CONTINUE;
			mypoint = sum;
			break;

		}
		while (gameState == CONTINUE)
		{
			sum = rollDice();
			roll_times++;
			if (sum == mypoint)
				gameState = WIN;
			else if (sum == 7)
				gameState = LOSE;
			
		}
		if (gameState == WIN)
			win_num++;
		else
			lose_num++;
		if (i < 12)
		{
			if (gameState == WIN)
				cout << "NO." << i + 1 << " player win" << endl;
			else
				cout << "NO." << i + 1 << " player lose" << endl;
		}
	}
	double revarge;
	revarge =roll_times / N;
	cout << "N=" << N << endl;
	cout << "win:" << win_num << " lose:" << lose_num << endl;
	cout << "posibility:" << (float)win_num / N << endl;
	cout << "revarge roltimes:" << revarge << endl;
	
}
int rollDice()
{
	int dice1, dice2, worksum;
	dice1 = rand() % 6 + 1;
	dice2 = rand() % 6 + 1;
	worksum = dice1 + dice2;
	return worksum;

}
