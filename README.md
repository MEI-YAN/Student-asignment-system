# Student-asignment-system
only another repository
//Student management system
#include<iostream>
#include<fstream>
#include<string>
#include<iomanip>
#include<conio.h>
using namespace std;
const int MAX = 100;

class Student
{
public:
	Student() {};
	~Student() {};
	void add();
	void search();
	void show();
	void alter();
	void del();
	void stat();
	void save();
	void read();
	void input();
	void output();
	double average();
	void rank();
	void ustudent();
	void bstudent();
	void dstudent();
protected:
	string name;
	int    num;
	string sex;
	int    math;
	int    Englich;
	int    Chinese;
	int    physical;
	int    Cyuyan;
	double Ascore;
private:
	double avmath;
	double avEnglich;
	double avChinese;
	double avphycial;
	double avCyuyan;
};
Student M[MAX];
int static top = 0;
void Student::input()
{
	cout << "输入学号：" << endl;
	cin >> num;
	cout << "输入姓名：" << endl;
	cin >> name;
	cout << "输入性别：" << endl;
	cin >> sex;
	cout << "输入数学成绩：" << endl;
	cin >> math;
	cout << "输入英语成绩：" << endl;
	cin >> Englich;
	cout << "输入语文成绩：" << endl;
	cin >> Chinese;
	cout << "输入物理成绩：" << endl;
	cin >> physical;
	cout << "输入C语言成绩：" << endl;
	cin >> Cyuyan;
}
void Student::output()
{
	/*cout << "学号：" << setw(9) << "姓名:" << setw(9) << "性别：" << setw(9) << "数学成绩："
		<< setw(9) << "英语成绩：" << setw(9) << "语文成绩：" << setw(9) << "物理成绩："
		<< setw(9) << "C语言成绩：" << endl;*/
	cout << num << setw(9) << name << setw(8) << sex << setw(8) << math << setw(9)
		<< Englich << setw(10) << Chinese << setw(10) << physical << setw(9)
		<< Cyuyan << endl;
}

void Student::read()
{
	top = 0;
	system("cls");
	ifstream infile("学生.txt", ios::in);
	if (!infile)
	{
		cout << "打开失败！" << endl;
		return;
	}
	int i = 0;
	while (infile >> M[i].num >> M[i].name >> M[i].sex >> M[i].math
		>> M[i].Englich >> M[i].Chinese >> M[i].physical >> M[i].Cyuyan)
	{
		i++;
		top = i;
	}
	infile.close();
}

void Student::save()
{
	ofstream outfile("学生.txt", ios::out);
	if (!outfile)
	{
		cout << "打开失败！" << endl;
		return;
	}
	int i;
	for (i = 0; i < top; i++)
	{
		outfile << M[i].num << setw(9) << M[i].name << setw(8) << M[i].sex << setw(8) << M[i].math
			<< setw(9) << M[i].Englich << setw(10) << M[i].Chinese << setw(9) << M[i].physical << setw(9) << M[i].Cyuyan << endl;
	}
	cout << "保存成功！" << endl;
	outfile.close();
}

void Student::add()
{
	system("cls");
	read();
	if (top >= MAX)
	{
		cout << "人员已满" << endl;
		return;
	}
	cout << "输入要添加的学号：" << endl;
	int n;
	cin >> n;
	for (int i = 0; i < top; i++)
	{
		if (n == M[i].num)
		{
			cout << "该学号的学生已存在" << endl;
			return;
		}
	}
	Student s;
	cout << "请再次输入新添加人员的信息" << endl;
	s.input();
	cout << "是否确认添加？ 1、是 2、否" << endl;
	int a;
	cin >> a;
	if (a == 1)
	{
		M[top] = s;
		top = top + 1;
		save();
	}
	else
	{
		cout << "放弃添加" << endl;
		return;
	}
}

void Student::search()
{
	system("cls");
	read();
	if (top == 0)
	{
		cout << "当前系统没有存储记录！" << endl;
		return;
	}
	cout << "请输入选项 1、按学号查找 2、按姓名查找 0、退出查找:";
	int choice;
	cin >> choice;
	switch (choice)
	{
	case 1: {
		cout << "请输入要查找的学号：" << endl;
		int number;
		cin >> number;
		for (int i = 0; i < top; i++)
		{
			if (M[i].num = number)
			{

				cout << "学号：" << setw(9) << "姓名:" << setw(9) << "性别：" << setw(9) << "数学成绩："
					<< setw(9) << "英语成绩：" << setw(9) << "语文成绩：" << setw(9) << "物理成绩："
					<< setw(9) << "C语言成绩：" << endl;
				M[i].output();
				return;
			}
		}
		cout << "查无此人！" << endl;
	}; break;
	case 2:
	{
		cout << "请输入要查找的姓名：" << endl;
		string name1;
		cin >> name1;
		for (int i = 0; i < top; i++)
		{
			if (M[i].name == name1)
			{
				cout << "学号：" << setw(9) << "姓名:" << setw(9) << "性别：" << setw(9) << "数学成绩："
					<< setw(9) << "英语成绩：" << setw(9) << "语文成绩：" << setw(9) << "物理成绩："
					<< setw(9) << "C语言成绩：" << endl;
				M[i].output();
			}
		}
		cout << "查无此人！" << endl;
	}; break;
	case 0:break;
	default:cout << "输入错误！请输入0~3的数字" << endl; system("pause"); search(); 
		break;
	}
}

void Student::show()
{
	system("cls");
	read();
	if (top == 0)
	{
		cout << "无数据！" << endl;
		return;
	}
	cout << "学号：" << setw(9) << "姓名:" << setw(9) << "性别：" << setw(9) << "数学成绩："
		<< setw(9) << "英语成绩：" << setw(9) << "语文成绩：" << setw(9) << "物理成绩："
		<< setw(9) << "C语言成绩：" << endl;
	for (int i = 0; i < top; i++)
		M[i].output();
}

void Student::alter()
{
	system("cls");
	read();
	if (top == 0)
	{
		cout << "当前系统没有储存记录！" << endl;
		return;
	}
	int number;
	cout << "请输入要修改的学生学号：" << endl;
	cin >> number;
	for (int i = 0; i < top; i++)
	{
		if (M[i].num == number)
		{
			cout << "学号：" << setw(9) << "姓名:" << setw(9) << "性别：" << setw(9) << "数学成绩："
				<< setw(9) << "英语成绩：" << setw(9) << "语文成绩：" << setw(9) << "物理成绩："
				<< setw(9) << "C语言成绩：" << endl;
			M[i].output();
			cout << "1、选择修改" << endl;
			/*cout << "请选择修改范围：1、全部修改 2、修改编号 3、修改姓名 4、修改性别" << endl;*/
			/*cout << "5、修改数学成绩 6、修改英语成绩 7、修改语文成绩 8、修改物理成绩、9、修改C语言成绩" << endl;*/
			cout << "0、退出修改系统" << endl;
			int choice;
			cin >> choice;
			switch (choice)
			{
			case 1:
			{
				cout << "输入修改后的学号：" << endl;
				int n;
				cin >> n;
				for (int j = 0; j < top; j++)
				{
					if (n == M[j].num)
					{
						cout << "该学号的人员已经存在" << endl;
						return;
				    }
				}
				cout << "输入修改后的姓名：" << endl;
				cin >> name;
				cout << "输入修改后的性别：" << endl;
				cin >> sex;
				cout << "输入修改后的数学成绩：" << endl;
				cin >> math;
				cout << "输入修改后的英语成绩：" << endl;
				cin >> Englich;
				cout << "输入修改后的语文成绩：" << endl;
				cin >> Chinese;
				cout << "输入修改后的物理成绩：" << endl;
				cin >> physical;
				cout << "输入修改后的C语言成绩：" << endl;
				cin >> Cyuyan;
				cout<< "是否确认修改？1、是 2、否" << endl;
				int a;
				cin >> a;
				if (a == 1)
				{
					M[i].num = n;
					M[i].name = name;
					M[i].sex = sex;
					M[i].math = math;
					M[i].Englich = Englich;
					M[i].Chinese = Chinese;
					M[i].physical = physical;
					M[i].Cyuyan = Cyuyan;
				}
				else
				{
					cout << "放弃修改" << endl;
					return;
				}
				save();

			}; break;
			case 0:cout << "退出修改系统" << endl; return; break;
			default:cout << "无此选项！请输入0或1！" << endl; system("pause"); break;
			}
			cout << "修改完成" << endl;
			return;
		}
	}
	cout << "查无此人" << endl;
}

void Student::del()
{
	system("cls");
	read();
	if (top == 0)
	{
		cout << "当前系统没有存储记录" << endl;
		return;
	}
	int choice;
	cout << "请选择删除方式：1、按学号删除 2、按姓名删除 0、退出删除:";
	cin >> choice;
	switch (choice)
	{
	case 1:
	{
		cout << "请输入所要删除学生的学号：" << endl;
		int number;
		cin >> number;
		for (int i = 0; i < top; i++)
		{
			if (M[i].num == number)
			{
				cout << "学号：" << setw(9) << "姓名:" << setw(9) << "性别：" << setw(9) << "数学成绩："
					<< setw(9) << "英语成绩：" << setw(9) << "语文成绩：" << setw(9) << "物理成绩："
					<< setw(9) << "C语言成绩：" << endl;
				M[i].output();
				cout << "是否确认删除？ 1、是 2、否" << endl;
				int choice;
				cin >> choice;
				switch (choice)
				{
				case 1:
				{
					for (int j = i; j < top; j++)
						M[j] = M[j + 1];
					cout << "删除成功！" << endl;
					top = top - 1;
				}; save(); break;
				case 2:return;
				default:cout << "没有此选项！" << endl;
				}return;//.......//
			}
		}
		cout << "无此人！" << endl;
	}; system("pause"); del(); break;
	case 2:
	{
		cout << "请输入所要删除学生的姓名：" << endl;
		string  name1;
		cin >> name1;
		for (int i = 0; i < top; i++)
		{
			if (M[i].name == name1)
			{
				cout << "学号：" << setw(9) << "姓名:" << setw(9) << "性别：" << setw(9) << "数学成绩："
					<< setw(9) << "英语成绩：" << setw(9) << "语文成绩：" << setw(9) << "物理成绩："
					<< setw(9) << "C语言成绩：" << endl;
				M[i].output();
				cout << "是否确认删除？ 1、是 2、否" << endl;
				int choice;
				cin >> choice;
				switch (choice)
				{
				case 1:
				{
					for (int j = i; j < top; j++)
						M[j] = M[j + 1];
					cout << "删除成功！" << endl;
					top = top - 1;
				}; save(); break;
				case 2:return;
				default:cout << "没有此选项！" << endl;
				}return;//.......//
			}
		}
		cout << "无此人！" << endl;
	}; system("pause"); del(); break;
  case 0:break; 
	default:cout << "输入错误！请输入0~3的数字" << endl;
		system("pause"); del(); break;
	}
	save();
}
double Student::average()
{
	system("cls");
	read();
	cout << "各科均分成绩如下：" << endl;
	double avmath = 0;
	double avEnglich = 0;
	double avChinese = 0;
	double avphycial = 0;
	double avCyuyan = 0;
	for (int i = 0; i < top; i++)
	{
		avmath = M[i].math + avmath;
		avEnglich = M[i].Englich + avEnglich;
		avChinese = M[i].Chinese + avChinese;
		avphycial = M[i].physical + avphycial;
		avCyuyan = M[i].Cyuyan + avCyuyan;
	}
	avmath = avmath / top;
	avEnglich = avEnglich / top;
	avChinese = avChinese / top;
	avphycial = avphycial / top;
	avCyuyan = avCyuyan / top;
	cout << "数学平均分为：" << avmath << endl;
	cout << "英语平均分为：" << avEnglich << endl;
	cout << "语文平均分为：" << avChinese << endl;
	cout << "物理平均分为：" << avphycial << endl;
	cout << "C语言平均分为：" << avCyuyan << endl;
	save();
	Student::avmath = avmath;
	Student::avEnglich = avEnglich;
	Student::avChinese = avChinese;
	Student::avphycial = avphycial;
	Student::avCyuyan = avCyuyan;
	return avmath;
	return avEnglich;
	return avChinese;
	return avphycial;
	return avCyuyan;
}


void Student::rank()
{
	system("cls");
	read();
	cout << "总分排名如下：" << endl;
	for (int i = 0; i < top; i++)
	{
		M[i].Ascore = M[i].math + M[i].Englich + M[i].Chinese + M[i].physical + M[i].Cyuyan;
	}
	int i, j;
	double temp;
	for(i=0;i<top-1;i++)
		for(j=i+1;j<top;j++)
		{
			if (M[i].Ascore <= M[j].Ascore)
			{
				temp = M[j].Ascore;
				M[j].Ascore = M[i].Ascore;
				M[i].Ascore = temp;
			}
		
		}
	for (i = 0; i < top; i++)
	{
		cout << "名次" << i+1<<"  ";
		cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "总分：" << M[i].Ascore << endl;
	}
	save();
}

void Student::ustudent()
{
	system("cls");
	read();
	cout << "优秀学生为:" << endl;
	for (int i=0; i < top; i++)
	{
		if (M[i].math >90)
		{
			cout << "数学成绩中高于90分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "数学成绩：" << M[i].math << endl;
			cout << endl;
		}
		if (M[i].Englich >90)
		{
			cout << "英语成绩中高于90分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "英语成绩：" << M[i].Englich << endl;
			cout << endl;
		}
		if (M[i].Chinese >90)
		{
			cout << "语文成绩中高于90分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "语文成绩：" << M[i].Chinese << endl;
			cout << endl;
		}
		if (M[i].physical >90)
		{
			cout << "物理成绩中高于90分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "物理成绩：" << M[i].physical << endl;
			cout << endl;
		}
		if (M[i].Cyuyan >90)
		{
			cout << "C语言成绩中高于90分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "数学成绩：" << M[i].Cyuyan << endl;
			cout << endl;
		}
	}
	save();
}

void Student::bstudent()
{
	system("cls");
	read();
	cout << "不及格学生为：" << endl;
	for (int i = 0; i < top; i++)
	{
		if (M[i].math < 60)
		{
			cout << "数学成绩中低于60分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "数学成绩：" << M[i].math << endl;
			cout << endl;
		}
		if (M[i].Englich < 60)
		{
			cout << "英语成绩中低于60分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "英语成绩：" << M[i].Englich << endl;
			cout << endl;
		}
		if (M[i].Chinese < 60)
		{
			cout << "语文成绩中低于60分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "语文成绩：" << M[i].Chinese << endl;
			cout << endl;
		}
		if (M[i].physical < 60)
		{
			cout << "物理成绩中低于60分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "物理成绩：" << M[i].physical << endl;
			cout << endl;
		}
		if (M[i].Cyuyan < 60)
		{
			cout << "C语言成绩中低于60分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "数学成绩：" << M[i].Cyuyan << endl;
			cout << endl;
		}
	}
	save();
}

void Student::dstudent()
{
	system("cls");
	read();
	cout << "低于平均分成绩：" << endl;
	average();
	for (int i = 0; i < top; i++)
	{
		if (M[i].math < avmath)
		{
			cout << "数学成绩中低于平均分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "数学成绩：" << M[i].math << endl;
			cout << endl;
		}
		if (M[i].Englich < avEnglich)
		{
			cout << "英语成绩中低于平均分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "英语成绩：" << M[i].Englich << endl;
			cout << endl;
		}
		if (M[i].Chinese < avChinese)
		{
			cout << "语文成绩中低于平均分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "语文成绩：" << M[i].Chinese << endl;
			cout << endl;
		}
		if (M[i].physical < avphycial)
		{
			cout << "物理成绩中低于平均分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "物理成绩：" << M[i].physical << endl;
			cout << endl;
		}
		if (M[i].Cyuyan < avCyuyan)
		{
			cout << "C语言成绩中低于平均分的学生：";
			cout << "学号：" << M[i].num << "\t" << "姓名：" << M[i].name << "\t" << "性别：" << M[i].sex << "\t" << "数学成绩：" << M[i].Cyuyan << endl;
			cout << endl;
		}
	}
	save();
}

void Student::stat()
{
	system("cls");
	read();
	int choice;
	do {
		system("cls");
		cout << ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>" << endl;
		cout << "||                     成绩管理系统                              ||" << endl;
		cout << "||   1、添加  2、查询 3、删除 4、总览 5、修改  6、不及格学生     ||" << endl;
		cout << "||   7、均分  8、总分排名  9、优秀学生  10、低于均分  0、退出    ||" << endl;
		cout << "<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<" << endl;
		cout << "请输入所要操作的编号：" << endl;
		cin >> choice;
		switch (choice)
		{
		case 1:add(); _getch(); system("cls"); break;
		case 2:search(); _getch(); system("cls"); break;
		case 3:del(); _getch(); system("cls"); break;
		case 4:show(); _getch(); system("cls"); break;
		case 5:alter(); _getch(); system("cls"); break;
		case 6:bstudent(); _getch(); system("cls"); break;
		case 7:average(); _getch(); system("cls"); break;
		case 8:rank(); _getch(); system("cls"); break;
		case 9:ustudent(); _getch(); system("cls"); break;
		case 10:dstudent(); _getch(); system("clc"); break;
		case 0:cout << "谢谢您的使用!" << endl; break;
		default:cout << "无此选项！ 请输入0~8的数字" << endl; system("pause"); stat();
			break;
		}
	} while (choice != 0);
}

int main()
{
	system("cls");
	Student s;
	s.stat();
	system("pause");
	return 0;
}
  
