#define _CRT_SECURE_NO_WARNINGS
#include<time.h>
#include<iostream>
#include<string>
#include<vector>
#include<stdlib.h>
#include<windows.h>
using namespace std;
void Time_Show();
const int P_Num = 2;
struct P_Node
{
	string ID;
	int Time = 0;
	int In_h, In_m, In_s;
	P_Node* next;
};
class P_Stack//停车场 栈
{
public:
	P_Stack() { top = NULL; }
	~P_Stack() {};
	int In_P(string);
	void Out_P(string);//指定元素出栈
	int Empty() { if (top == NULL)return 1; else return 0; }
	int Find(string);
	int surplus() { return P_surplus; }
private:
	P_Node P_Car[P_Num];
	P_Node *top;
	int P_surplus = P_Num;
};

int P_Stack::In_P(string ID)
{
	if (P_surplus == 0)
		return 1;
	else
	{

		P_Node *s = new P_Node;
		s->ID = ID;
		time_t now;
		time_t seconds;
		seconds = time(NULL);
		struct tm* tm_now;
		time(&now);
		tm_now = localtime(&now);
		s->In_h = tm_now->tm_hour;
		s->In_m = tm_now->tm_min;
		s->In_s = tm_now->tm_sec;
		s->next = top;
		top = s;
		s->Time = int(seconds);
		P_surplus--;
		cout << "车辆 " << ID << " 停在停车场" << P_Num - P_surplus << "号";
		Sleep(3000);
		return 0;
	}
}

void P_Stack::Out_P(string x)
{
	if (P_surplus == P_Num)
		cout << "停车场为空" << endl;
	else
	{
		time_t seconds;
		seconds = time(NULL);
		int n = int(seconds);
		P_Node* s = top;
		while (s->ID == x)
		{
			s = s->next;
		}
		cout << "车辆 " << x << " 的车主您好！以下是您的停车费详情:" << endl;
		printf("车辆进入停车场时间:%02d:%02d:%02d\n", s->In_h, s->In_m, s->In_s);
		Time_Show();
		printf("停留时长:%.2f分钟\n", double((n - s->Time) / 60));
		printf("应缴费用:%.2fm元\n", double((n - s->Time) / 60));
		P_surplus++;
		Sleep(6000);
	}
}
int P_Stack::Find(string x)
{
	P_Node *s = top;
	while (s != NULL)
	{
		if (s->ID == x)
			return 1;
		else
			s = s->next;
	}
}
const int Maxnum = 2 ;
struct Road_Node
{
	string ID;
	Road_Node* next;
};
class Road_Queue//便道 队列
{
public:
	Road_Queue();
	~Road_Queue() {};
	void In_Road(string,int);
	string Out();
	int Find(string);
	int Empty() { if (front == rear)return 1; else return 0; }
	int surplus() { return R_surplus; }
private:
	 Road_Node Road_Car[Maxnum];
  	 Road_Node *front, *rear;
	 int R_surplus = Maxnum;
};
Road_Queue::Road_Queue()
{
	Road_Node* s = new Road_Node;
	s->next = NULL;
	front = rear = s;
}

void Road_Queue::In_Road(string x,int a)
{
	if (R_surplus == 0)
	{
		cout << "停车场与便道全满";
		Sleep(3000);
	}
	else
	{
		Road_Node* s = new Road_Node;
		s->ID = x;
		s->next = NULL;
		R_surplus--;
		if (a == 0) //0为第一次
		{
			cout << "车辆 " << x << " 停在便道" << Maxnum - R_surplus << "号";
			Sleep(3000);
		}
		rear->next = s;
		rear = s;
	}
}
int Road_Queue::Find(string x)
{
	Road_Node* p = new Road_Node;
	if (front != NULL&&front->next!= NULL)
	{
		p = front->next;
		while (p != NULL)
		{
			if (p->ID == x)
				return 1;
			else
				p = p->next;
		}
	}
}
string Road_Queue::Out()
{
	Road_Node* p = new Road_Node;
	string x;
	p = front->next;
	x = p->ID;
	front->next = p->next;
	if (p->next == NULL)
	{
		rear = front;
	}
	delete p;
	R_surplus++;
	return x;
}
void UI()
{
	system("cls");
	cout << "输入数字进行操作:" << endl;
	cout << "1.有车驶入" << endl;
	cout << "2.有车离开" << endl;
}

void Time_Show()
{
	time_t now;
	struct tm* tm_now;
	time(&now);
	tm_now = localtime(&now);
	printf("当前系统时间:%02d:%02d:%02d\n", tm_now->tm_hour, tm_now->tm_min, tm_now->tm_sec);
}
int main()
{
	P_Stack P;
	Road_Queue Road;
	Time_Show();
	cout << "系统初始化" << endl << "停车场容纳数量为" << P_Num << endl;
	cout << "便道的容纳数量为" << Maxnum;
	Sleep(3000);
	while (1)
	{
		UI();
		string temp;
		cin >> temp;
		if (temp == "1")//1.判断停车场内是否满 2.停车场满的话看便道 3.都满   （如果可停输出位置）
		{
			One:cout << "输入车牌:";
			string id; cin >> id;
			if (id.length() != 8)
			{
				cout << "非法车牌，请核对后重新输入" << endl;
				Sleep(3000);
				goto One;
			}
			int x = P.In_P(id);//1
			if (x)
			{
				Road.In_Road(id,0);//2,3
			}
		}
		if (temp == "2")//1.停车场出来输出时间与收费 2.便道出来输出时间
		{
			Two:cout<< "输入车牌:";
			string id; cin >> id;
			if (id.length() != 8)
			{
				cout << "非法车牌，请核对后重新输入" << endl;
				Sleep(3000);
				goto Two;
			}
			int in_p = P.Find(id);
			int in_road = Road.Find(id);
			if (in_p != 1 && in_road != 1)
			{
				cout << "停车场与便道中无此车，请核对后重新输入" << endl;
				Sleep(3000);
				goto Two;
			}
			if (in_p == 1)//出车在停车场
			{
				P.Out_P(id);
				if(P.surplus() == P_Num - 1)
				{
					cout << "因停车场空余一车位，便道1号车进入停车场" << endl;
					P.In_P(Road.Out());
					Sleep(3000);
				}
			}
			if (in_road == 1)//如果在便道
			{
				int count = 0;
				string Temp_Queue[Maxnum];
				for (int i = 0; i < Maxnum - Road.surplus(); i++)
				{
					if (Road.Out() == id)
					{
						cout << "车辆 " << id << " 从便道离开" << endl;
						Sleep(3000);
					}
					else
					{
						Temp_Queue[i] = Road.Out();
						count++;
					}
				}
				for (int i = 0; i < count; i++)
				{
					Road.In_Road(Temp_Queue[i],0);
				}

				
			}
		}
	}
}
