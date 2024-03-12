#include <stdio.h> 
#include <stdlib.h> 
#include <time.h> 
#include <conio.h> 
#include <windows.h>

#define SIZE 10

int main() {

	int field[SIZE + 2][SIZE + 2];
	int show_field[SIZE + 2][SIZE + 2];
	int mine = 10;

	srand(time(NULL));

	for (int i = 0; i < SIZE + 2; i++)
	{
		for (int j = 0; j < SIZE + 2; j++)
			field[i][j] = 0;
	}

	int i = 0;
	while (i < mine)
	{
		int x = rand() % 10 + 1;
		int y = rand() % 10 + 1;

		if (field[x][y] == -1)
			continue;
		field[x][y] = -1;
		i++;
	}


	for (int i = 1; i <= SIZE; i++)
	{
		for (int j = 1; j <= SIZE; j++)
		{
			int check;

			if (field[i][j] == -1)
			{
				show_field[i][j] = -1;
				continue;
			}

			check = field[i + 1][j - 1] + field[i + 1][j] + field[i + 1][j + 1] +
				field[i][j - 1] + field[i][j + 1] +
				field[i - 1][j - 1] + field[i - 1][j] + field[i - 1][j + 1];


			show_field[i][j] = -1 * check;
		}
	}



	//===================================== 실행 부분 

	int end = 1;
	int nkey;
	int cur_x = 1, cur_y = 1;

	int show[SIZE + 2][SIZE + 2];

	for (int i = 0; i < SIZE + 2; i++)
	{
		for (int j = 0; j < SIZE + 2; j++)
		{
			show[i][j] = 10;
		}
	}

	printf("10: 빈칸, w,a,s,d: 이동, f: 상호작용\n");
	printf("지뢰 개수: %d", mine);

	printf("%4d", 0);
	for (int i = 1; i <= SIZE; i++)
		printf("%4d", i);
	printf("\n");
	printf("============================================");
	printf("\n");
	for (int i = 1; i <= SIZE; i++)
	{
		printf("%3d |", i);
		for (int j = 1; j <= SIZE; j++)
		{
			printf("%3d ", show[i][j]);
		}

		printf("\n");
	}
	printf("(세로, 가로): (%d, %d)", cur_x, cur_y);


	while (end)
	{
		if (_kbhit())
		{
			nkey = _getch();
			if (nkey == 'w')
			{
				if (cur_x == 1)
					continue;
				else
					cur_x -= 1;
			}
			else if (nkey == 's')
			{
				if (cur_x == (SIZE))
					continue;
				else
					cur_x += 1;
			}
			else if (nkey == 'a')
			{
				if (cur_y == 1)
					continue;
				else
					cur_y -= 1;
			}
			else if (nkey == 'd')
			{
				if (cur_y == (SIZE))
					continue;
				else
					cur_y += 1;
			}
			else if (nkey == 'f')
			{
				if (field[cur_x][cur_y] == -1)
				{
					system("cls");
					end = 0;
				}
				else
				{
					show[cur_x][cur_y] = show_field[cur_x][cur_y];
				}
			}


			system("cls");

			printf("%4d", 0);
			for (int i = 1; i <= SIZE; i++)
				printf("%4d", i);
			printf("\n");
			printf("============================================");
			printf("\n");
			for (int i = 1; i <= SIZE; i++)
			{
				printf("%3d |", i);
				for (int j = 1; j <= SIZE; j++)
				{
					printf("%3d ", show[i][j]);
				}

				printf("\n");
			}
			printf("(세로, 가로): (%d, %d)", cur_x, cur_y);

		}

	}
	system("cls");


	for (int i = 1; i <= SIZE; i++)
	{
		for (int j = 1; j <= SIZE; j++)
			printf("%2d ", show_field[i][j]);
		printf("\n");
	}
	
	printf("지뢰: -1\n");

	printf("종료");
}
