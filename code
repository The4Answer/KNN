	#include <iostream>
#include <fstream>
#include <vector>
#include <cmath>
#include <algorithm>
#include <string>
#include <deque>
#include <set>
#include <map>
#include <deque>
#include <queue>
#include <ctime>
#include <Windows.h>


using namespace std;

ifstream in("input.txt");
//ofstream cout("output.txt");

struct st {
	double hour, work, weight, height, time;
	double parents;
	char  yourself;
};

struct str {
	double dist;
	int ind;
};
vector <st> a;

bool cmp(str a, str b) {
	if (a.dist != b.dist)
		return a.dist < b.dist;
	else
		return a.ind < b.ind;
}

double changeP(string s) {					//change string to double	// ч+ч = 0; ч+к || к+ч = 0.5; к+к = 1
	if (s[0] == 'ч' && s[1] == 'ч')
		return 0;
	else if (s[0] == 'к' && s[1] == 'ч')
		return 0.5;
	else if (s[0] == 'ч' && s[1] == 'к')
		return 0.5;
	else if (s[0] == 'к' && s[1] == 'к')
		return 1;
	else {
		cout << "Program went wrong!";
		exit(0);
	}
}

void normalizing() {
	st Min = a[0], Max = a[0];
	for (int i = 1; i < a.size(); ++i) {
		//min
		Min.hour = min(Min.hour, a[i].hour);
		Min.work = min(Min.work, a[i].work);
		Min.weight = min(Min.weight, a[i].weight);
		Min.height = min(Min.height, a[i].height);
		Min.time = min(Min.time, a[i].time);
		Min.parents = min(Min.parents, a[i].parents);
		//max
		Max.hour = max(Max.hour, a[i].hour);
		Max.work = max(Max.work, a[i].work);
		Max.weight = max(Max.weight, a[i].weight);
		Max.height = max(Max.height, a[i].height);
		Max.time = max(Max.time, a[i].time);
		Max.parents = max(Max.parents, a[i].parents);
	}

	for (int i = 0; i < a.size(); ++i) {
		a[i].hour = (a[i].hour - Min.hour) / (Max.hour - Min.hour);
		a[i].work = (a[i].work - Min.work) / (Max.work - Min.work);
		a[i].weight = (a[i].weight - Min.weight) / (Max.weight - Min.weight);
		a[i].height = (a[i].height - Min.height) / (Max.height - Min.height);
		a[i].time = (a[i].time - Min.time) / (Max.time - Min.time);
		a[i].parents = (a[i].parents - Min.parents) / (Max.parents - Min.parents);
	}
}

int main() {
	SetConsoleCP(1251);
	SetConsoleOutputCP(1251);

															//Ввод данных//

	a.resize(19);
	for (int i = 0; i < a.size(); ++i)
	{
		string s;
		in >> a[i].hour >> a[i].work >> a[i].weight >> a[i].height >> a[i].time >> s >> a[i].yourself;
		a[i].parents = changeP(s);
	}
	st newS;
	string tmp;
	cout << "Write down information about new student:" << endl;
	cout << "Hours of sleep: ";
	cin >> newS.hour;
	cout << "Have a job? (1 = yes or 0 = no): ";
	cin >> newS.work;
	cout << "Weight: ";
	cin >> newS.weight;
	cout << "Height: ";
	cin >> newS.height;
	cout << "Time to MIREA in hours: ";
	cin >> newS.time;
	cout << "What does parents drink? (e.g. чк = tea + coffee): ";
	cin >> tmp;
	newS.parents = changeP(tmp);
	a.push_back(newS);
	
														// Нормализация //

	normalizing();

														//calc

	vector <str> distance;
	for (int i = 0; i < a.size() - 1; ++i) {
		str temp;
		temp.dist = sqrt((a[i].hour - a[19].hour)* (a[i].hour - a[19].hour) + 
			(a[i].work - a[19].work) * (a[i].work - a[19].work) + (a[i].weight - a[19].weight) * 
			(a[i].weight - a[19].weight) + (a[i].height - a[19].height) * 
			(a[i].height - a[19].height) + (a[i].time - a[19].time) * (a[i].time - a[19].time) + 
			(a[i].parents - a[19].parents) * (a[i].parents - a[19].parents));
		temp.ind = i;
		distance.push_back(temp);
	}
	sort(distance.begin(), distance.end(), cmp);

	cout << "Write down K:";
	int k = 4;
	cin >> k;
	int tea = 0, coffee = 0;
	double teaQ = 0, coffeeQ = 0;		//оценка близости
	for (int i = 0; i < k; ++i) {
		str temp = distance[i];
		if (a[temp.ind].yourself == 'ч') {
			tea++;
			teaQ += 1 / (temp.dist * temp.dist);
		}
		else if (a[temp.ind].yourself == 'к') {
			coffee++;
			coffeeQ += 1 / (temp.dist * temp.dist);
		}
	}

														//	results	//

	if (tea > coffee)
		cout << endl << "Student likes TEA" << endl;
	else if (coffee > tea)
		cout << endl << "Student likes COFFEE" << endl;
	else {
		if (teaQ > coffeeQ)
			cout << endl << "Student likes TEA" << endl;
		else if (teaQ < coffeeQ)
			cout << endl << "Student likes COFFEE" << endl;
		else
			cout << endl << "Program miscalculated =( " << endl;
	}

	system("pause");
	return 0;
}
