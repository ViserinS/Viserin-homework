##  贪吃蛇

#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#include <time.h>
#include <windows.h>

void init(char map[30][60], int snake[400][3]);  //初始化游戏 
void makeMap(char map[30][60],int snake[400][3],int food[]);  //绘制地图 
void move(int snake[400][3],int direct);  //移动 
void makeFood(int food[]);   //食物生成 
void showView(char map[30][60]);   //绘制视图 
int ifEat(int head, int food[2]);  //判断食物是否被吃掉 
int ifReprat(int snake[400][3], int x, int y); //判断生成的食物是否在蛇身上 
int ifBump(int head);  //判断是否相撞 
void getKey();

const int W = 60;  //以下 全局变量 
const int H  = 30;
char map[30][60];
char key;
int direct = 4;
int food[2] = {8,10};
int head;
int snake[400][3];


int main() {                    //主函数

	init(map, snake);
	while (1) {
		getKey();
		system("cls");
		Sleep(30);
		move(snake, direct);
		if (!food[0]&&!food[1]) {
			makeFood(food);
		}
		makeMap(map, snake, food);
		showView(map);
		if (ifBump(head)) {
			printf("GAME OVER,YOUR SCORE：%d", head);
			break;
		}
		getKey();
	}
	getchar();
	return 0;
}

void init(char map[30][60], int snake[400][3]) { //初始化地图 
​	snake[0][0] = 0, snake[0][1] = 9, snake[0][2] = 7;
​	snake[1][0] = 0, snake[1][1] = 9, snake[1][2] = 8;
​	snake[2][0] = 1, snake[2][1] = 9, snake[2][2] = 9;
​	for (int i = 0;i<H;i++) {
​		for (int j = 0;j<W;j++) {
​			if (i == 0 || j == 0 || i == H - 1 || j == W - 1) {
​				map[i][j] = '*';
​			}
​			else {
​				map[i][j] = ' ';
​			}
​		}
​	}
}

void showView(char map[30][60]) {  
​	for (int i = 0;i<H;i++) {
​		for (int j = 0;j<W;j++) {
​				printf("%c", map[i][j]);
​		}
​		printf("\n");
​	}
}

void move(int snake[400][3],int direct) {//让蛇的坐标开始移动
​	int x, y;
​	for (int i = 0;i < 400;i++) {
​		if (snake[i][0] == 1) {
​			head = i;
​			break;
​		}
​	}
​	//找到头并将头的坐标保留用于下一个补上来
​	x = snake[head][1];
​	y = snake[head][2];
​	switch (direct){
​		case 1://向上
​			snake[head][1]--;
​			break;
​		case 2://向下
​			snake[head][1]++;
​			break;
​		case 3://向左
​			snake[head][2]--;
​			break;
​		case 4://向右
​			snake[head][2]++;
​			break;
​	}
​	if (ifEat(head, food)) { //判断是否会吃掉食物，并将之前身体放到前一个的位置上
​		snake[head + 1][0] = 1, snake[head + 1][1] = food[0], snake[head + 1][2] = food[1];
​		snake[head][0] = 0;
​		food[0] = 0, food[1] = 0;
​	}
​		for (int j = head - 1;j >= 0;j--) {
​			int temp;
​			temp = x, x = snake[j][1], snake[j][1] = temp;
​			temp = y, y = snake[j][2], snake[j][2] = temp;
​		}
}

void makeFood(int food[]) {//生成食物的坐标
​	srand(time(0));
​	int x = rand() % 55 + 2, y = rand() % 25 + 2;
​	while (ifReprat(snake,x,y)) {
​		x = rand() % 55 + 2, y = rand() % 25 + 2;
​	}
​	food[0] = y;
​	food[1] = x;
}

void makeMap(char map[30][60], int snake[400][3], int food[]) {
​	int i;
​	//重新初始化地图
​	for (int i = 0;i<H;i++) {
​		for (int j = 0;j<W;j++) {
​			if (i == 0 || j == 0 || i == H - 1 || j == W - 1) {
​				map[i][j] = '*';
​			}
​			else {
​				map[i][j] = ' ';
​			}
​		}
​	}
​	//重新绘制蛇
​	for (i = 0;i < 400;i++) {
​		if (snake[i][0] == 1) break;
​		map[snake[i][1]][snake[i][2]] = 'T';
​	}
​	//绘制头和食物
​	map[snake[i][1]][snake[i][2]] = 'H';
​	map[food[0]][food[1]] = '$';
}


int ifEat(int head,int food[2]) {  //判断是否吃到食物 
​	if (snake[head][1] == food[0] && snake[head][2] == food[1])
​		return 1;
​	else
​		return 0;
}

int ifReprat(int snake[400][3],int x,int y) {//判断生成的食物是否与蛇有重复
​	for (int i = 0;i < 400;i++) {
​		if (snake[i][0] == 1) break;
​		if ((snake[i][1] == x&&snake[i][2] == y)) {
​			return 1;
​		}
​	}
​	return 0;
}

int ifBump(int head) {   //判断是否相撞 
​		if ((snake[head][2]==0|| snake[head][2] == 59)  ||  (snake[head][1] == 0|| snake[head][1] == 29))//撞墙
​			return 1;
​		for (int i = 0;i < head-1;i++) {
​			if ((snake[i][1] == snake[head][1]&&snake[i][2] == snake[head][2])) {//幢自己
​				return 1;
​			}
​		}
​		return 0;
}
void getKey() {
​	if (_kbhit()) {
​		key = _getch();
​	}
​	switch (key) {
​	case 'H': //按 上 键 
​		if (direct != 2)
​			direct = 1;
​		break;
​	case 'P': // 按 下 键 
​		if (direct != 1)
​			direct = 2;
​		break;
​	case 'K': //按 左 键 
​		if (direct != 4)
​			direct = 3;
​		break;
​	case 'M': //按 右 键 
​		if (direct != 3)
​			direct = 4;
​		break;
​	}
}