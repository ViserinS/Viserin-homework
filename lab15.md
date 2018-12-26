### 一、实验目的

1. 了解 算法 与 “智能” 的关系
2. 通过算法赋予蛇智能
3. 了解 Linux IO 设计的控制

### 二、实验环境

1. Linux Only. 你可以选择 Unbutu、Centos 等发行版。

2. 建议编辑环境 Vim 或 Vscode, 编译 gcc.

3. 第一次使用 Linux，建议使用虚拟机。可以使用其他同学准备好的 Vbox 镜像![微信图片_20181226223416.png](https://github.com/ViserinS/Viserin-homework/blob/gh-pages/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20181226223416.png?raw=true)


**决定蛇行走的方向函数的伪代码**

```
    // Hx,Hy: 头的位置
    // Fx,Fy：食物的位置
	function whereGoNext(Hx,Hy,Fx,Fy) {
	// 用数组movable[3]={“a”,”d”,”w”,”s”} 记录可走的方向
	// 用数组distance[3]={0,0,0,0} 记录离食物的距离
	// 分别计算蛇头周边四个位置到食物的距离。H头的位置，F食物位置
	//     例如：假设输入”a” 则distance[0] = |Fx – (Hx-1)| + |Fy – Hy|
	//           如果 Hx-1，Hy 位置不是Blank，则 distance[0] = 9999
	// 选择distance中存最小距离的下标p，注意最小距离不能是9999
	// 返回 movable[p]
	}
```

**2、智能蛇的程序框架**

```
	输出字符矩阵
	WHILE not 游戏结束 DO
        wait(time)
		ch＝whereGoNext(Hx,Hy,Fx,Fy)
		CASE ch DO
		‘A’:左前进一步，break 
		‘D’:右前进一步，break    
		‘W’:上前进一步，break    
		‘S’:下前进一步，break    
		END CASE
		输出字符矩阵
	END WHILE
	输出 Game Over!!!
```

C语言实现



![微信图片_20181226223408.png](https://github.com/ViserinS/Viserin-homework/blob/gh-pages/images/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20181226223408.png?raw=true)



```
char move(int hx,int hy,int fx,int fy) {
	char move[4]={'a','s','d','w'};
	int distance[4]={0,0,0,0};
	int index=0;
	
	if(zone[hy][hx-1]==SNAKE_AREA) {
		distance[0]=abs((fx-(hx-1)))+abs((fy-hy));
	}
	else {
		distance[0]=999;
	}
	
	if(zone[hy+1][hx]==SNAKE_AREA) {
		distance[1]=abs(fx-hx)+abs(fy-(hy+1));
	} 
	else {
		distance[1]=999;
	}
	if(zone[hy][hx+1]==SNAKE_AREA) {
		distance[2]=abs(fx-(hx+1))+abs(fy-hy);
	}
	else {
		distance[2]=999;
	}
	if(zone[hy-1][hx]==SNAKE_AREA) {
		distance[3]=abs(fx-hx)+abs(fy-(hy-1));
	}
	else {
		distance[3]=999;
	}

	
	index=min(distance);
	
	return move[index];
}

int min(const int*distance) {
	int i=0;
	int min=distance[0];
	int index=0;
	
	for(i=1;i<4;i++) {
		if(min>distance[i]&&distance[i]!=999) {
			min=distance[i];
			index=i;
		}
	}
	
	return index;
}
```