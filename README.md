# wannianli
万年历
#include <stdio.h>
/*
题目报告：输入年月日后能打印出当月日历
未能重复查询；
未能给予星号； 
*/
int year,month,week,date;
int run_months[12]={31,29,31,30,31,30,31,31,30,31,30,31};
int ping_months[12]={31,28,31,30,31,30,31,31,30,31,30,31};	//全局变量 

int leap(int year){
//判断闰平年 
	if(year % 400 ==0||year%4==0&&year%4!=0){
		return 1;
	}else{
		return 0;
	}
}
int week_of(int year){//返回xx年1月1日是星期几 

	if(year==1){//公元1年1月1日是星期一
		return 1;
	}
	
	int sum=0;
	for(int i=1;i<year;i++){
		if(leap(i)==1){
			sum=sum+366;
		} else{
			sum=sum+365;
		}
	}
	return (sum+1)%7;
}
int judge_month(int month){
	if(leap(year)==1){
		switch(month){
		case 1:return 31;
		case 2:return 29;
		case 3:return 31;
		case 4:return 30;
		case 5:return 31;
		case 6:return 30;
		case 7:return 31;
		case 8:return 31;
		case 9:return 30;
		case 10:return 31;
		case 11:return 30;
		case 12:return 31;
		}
	}else{
		switch(month){
		case 1:return 31;
		case 2:return 28;
		case 3:return 31;
		case 4:return 30;
		case 5:return 31;
		case 6:return 30;
		case 7:return 31;
		case 8:return 31;
		case 9:return 30;
		case 10:return 31;
		case 11:return 30;
		case 12:return 31;
		}
	}
}
int date_of_month(int date){
	int i,j;
	date = week_of(year);//对星期几做初始化：把当年第一天的值赋给它； 
	int run_months[12]={31,29,31,30,31,30,31,31,30,31,30,31};
	int ping_months[12]={31,28,31,30,31,30,31,31,30,31,30,31};
	
	if(leap(year)==1){
	//得出所求月份第一天是星期几 
		for(i = 0;i<month;i++){
		j += run_months[i];
		date = week_of(year)+j;
		}
	}else{
		for(i = 0;i<month;i++){
		date = week_of(year)+j;
	}
 	return date%7;
 }
}
	 


int main(){

	
	int year,month,day;
	int i,j,table,month_days;
	printf("请输入年月日，每个数字间隔一个空格；");
	scanf("%d %d %d",&year,&month,&day);
	printf("\t\t\t%d年\t\t\t\n\t\t\t%d月\t\t\t\n",year,month); 
	printf("日	一	二	三	四	五	六\n");
	
	date = date_of_month(date);//月一星期几 
	for(i=0;i<date;i++){
		printf("\t");
		table++;//根据每月第一天星期几来对齐 
	}
	if(leap(year)==1){
		month_days = run_months[month];
		for(j = 1;j<=month_days;j++){
			printf("%d\t",j);
			table++;
			if(table%7==0){
				printf("\n");//满足七天换行 
			}
		}
	}else{
		month_days = ping_months[month];
		for(j = 1;j<=month_days;j++){
			printf("%d\t",j);
			table++;
			if(table%7==0){
				printf("\n");
			}
		}
	}
	
	
	return 0;
}
