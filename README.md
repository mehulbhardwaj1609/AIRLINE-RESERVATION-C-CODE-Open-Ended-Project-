# AIRLINE-RESERVATION
CODE


#include <iostream>
#include <cstdio>
#include <cstring>
#include<iomanip>
#include <ctype.h>
using namespace std;

struct customer{
char name[20];
int age;
long date;
char source[30];
char dest[30];
char fname[20];
int ftime;
int fcost;
char route[10][30];
int s;
}c;

const int MAXNODES = 10,INF = 99999;
char sour[20],des[20],a[10][30],b[10][30];
char cities[10][30]={"Mumbai","Kolkata","Banglore","Delhi","Lucknow","Chennai","Pune","Ahemdabad","Hyderabad","Chandigarh"};
 char flightc[MAXNODES][20]={"GVR101","MKN102","LDB103","GYU104","UWB105","EAQ106","KJD107","CRN108","ASV109","KED110",};
 char flightt[MAXNODES][20]={"WEG101","KRC102","KRV103","WDB104","GTC105","IBR106","AMY107","LYV108","HRE109","PLO110",};
void fnDijkstra(int [][MAXNODES], int [], int [], int[], int, int, int);

void display_cities(char cities[MAXNODES][30],char flightc[MAXNODES][20],char flightt[MAXNODES][20])
{
     cout<<"\nName of City\t"<<setw(20)<<"Cost Efficient Flight\t"<<setw(15)<<"Time Efficient Flight \n";
    for(int i=0;i<MAXNODES;i++)
    {

        cout<<setw(12)<<cities[i]<<"\t"<<setw(15)<<flightc[i]<<"\t"<<setw(20)<<flightt[i]<<endl;
    }
}

void print_ticket()
{

    cout<<"\n\n\n*******************************************************************************************************************************************************************************************************************";
    cout<<"\n\n";
    //cout<<"---------------------------------------------------------------------------------------------------------\n";
    cout<<"Flight : "<<c.fname;
    cout<<"\nDeparture City : "<<c.source;
    cout<<"\nArrival City : "<<c.dest;
    cout<<"\nPath of Flight : ";
    for(int i=0;i<c.s-1;i++)
        cout<<c.route[i]<<" <-- ";
     cout<<c.source;
    cout<<"\nPNR : TR"<<(rand()%(9999 - 1001 + 1)) + 1001;
    cout<<"\nDate : "<<c.date;
   // cout<<"\nPassenger Details : ";
    cout<<"\nPassenger Name : "<<c.name;
    cout<<"\nAge : "<<c.age;
    cout<<"\nSeat No. : "<<(rand()%(76 -1 + 1)) + 1;
    cout<<"\nDuration of Flight : "<<c.ftime<<" hr";
    cout<<"\nPrice : INR "<<c.fcost;
    cout<<"\n\n\n*******************************************************************************************************************************************************************************************************************";


}


void book_ticket(char cities[MAXNODES][30],char flightc[MAXNODES][20],char flightt[MAXNODES][20])
{

int choice,ch,dist1[MAXNODES],dist2[MAXNODES],visited1[MAXNODES],path1[MAXNODES],visited2[MAXNODES],path2[MAXNODES],i,k,source,dest,flag=0,flag2=0;
char sour[20],des[20];
int price=0,t=0,x=0,y=0;
int cost[MAXNODES][MAXNODES]={0,99999,3000,99999,7000,5000,2200,99999,99999,99999,
                             99999,0,99999,99999,3000,10000,99999,8600,5000,99999,
                             3000,99999,0,99999,99999,1000,99999,99999,2000,99999,
                             99999,99999,99999,0,3500,99999,99999,99999,2500,3500,
                             7000,3000,99999,3500,0,99999,99999,5000,99999,99999,
                             5000,10000,1000,99999,99999,0,99999,11000,99999,99999,
                             2200,99999,99999,99999,99999,99999,0,2000,99999,5700,
                             99999,8600,99999,99999,5000,11000,2000,0,4500,2400,
                             99999,5000,2000,2500,99999,99999,99999,4500,0,99999,
                             99999,99999,99999,3500,99999,99999,5700,2400,99999,0};
 int time[MAXNODES][MAXNODES]={0,99999,2,99999,3,2,1,99999,99999,99999,
                               99999,0,99999,99999,3,4,99999,5,3,99999,
                               2,99999,0,99999,99999,1,99999,99999,2,99999,
                               99999,99999,99999,0,2,99999,99999,99999,3,1,
                               3,3,99999,2,0,99999,99999,3,99999,99999,
                               2,4,1,99999,99999,0,99999,5,99999,99999,
                               1,99999,99999,99999,99999,99999,0,3,99999,3,
                               99999,5,99999,99999,3,5,3,0,2,3,
                               99999,3,2,3,99999,99999,99999,2,0,99999,
                               99999,99999,99999,1,99999,99999,3,3,99999,0};

start:
 cout << "\nEnter the Source City" << endl;
 cin >> sour;
 strcpy(c.source,sour);
 for(int i=0;i<MAXNODES;i++)
 {   // transform(sour.begin(), sour.end(), sour.begin(), ::tolower);
     // transform(cities[i].begin(), s2.end(), s2.begin(), ::tolower);
     if(strcmp(sour,cities[i])==0)
        {source=i;
        flag=1;
        }

 }
 if(flag==0)
 {
     cout<<"We do not travel from this source city"<<endl<<"Please Enter again : ";
     goto start;
 }
 cout << "Enter the Destination City" << endl;
 cin >> des;
 strcpy(c.dest,des);
 for(int i=0;i<MAXNODES;i++)
 {
     if(strcmp(des,cities[i])==0)
 {dest=i;
  flag2=1;
 }
 }
 if(flag2==0)
 {
     cout<<"We do not travel to this destination city"<<endl<<"Please Enter again : ";
     goto start;
 }

 while(1)
{

    cout<<"\n\n1.Cost Efficient Flight\n2.Time Efficient Flight\n3.Book your Flight\n4.Change source and destination:\n5.Back to Main Menu:";
    cout<<"\nEnter your choice:";
    cin>>choice;
    switch(choice)
    {
    case 1:

    cout<<"\n\nCost Efficient Flight Details : ";
    fnDijkstra(cost,dist1,path1,visited1,source,dest,MAXNODES);
    cout<<"\nRoute for the travel : ";
    if (dist1[dest] == INF)
    cout << dest << " not reachable" << endl;
    else
    {

    i = dest;
    k=dest;
    strcpy(a[x++],cities[dest]);
    do
    {
    cout << cities[i] << " <-- ";

    i = path1[i];
    t+=time[k][i];
    k=i;
    strcpy(a[x++],cities[i]);
    }while (i!= source);
    cout << cities[i];
    //a[x]="\0";
    cout<< "\nCost of Flight = INR " << dist1[dest] << endl;
    cout<<"Duration of Flight = "<<t<<" hr";
    }
    cout<<endl<<"Flight Name:"<<flightc[source];
        break;

    case 2:
        cout<<"\n\nTime Efficient Flight Details : ";
        fnDijkstra(time,dist2,path2,visited2,source,dest,MAXNODES);
        cout<<"\nRoute for the travel : ";
    if (dist2[dest] == INF)
    cout << dest << " not reachable" << endl;
    else
    {
    i = dest;
    k=dest;
    strcpy(b[y++],cities[dest]);
    do
    {
  cout << cities[i] << "<--";
    i = path2[i];

    price+=cost[k][i];
    k=i;
    strcpy(b[y++],cities[i]);
    }while (i!= source);
    cout << cities[i]<<endl;
   // b[y]="\0";
    cout<<"Cost of Flight = INR "<<price;
    cout<< "\nDuration of Flight = " << dist2[dest]<<" hr";

    }
    cout<<endl<<"Flight Name:"<<flightt[source];
        break;


    case 3:
       cout<<"\nSelect option 1 or 2 : ";
       cin>>ch;
       if(ch==1)
       {cout<<endl<<flightc[source];
       strcpy(c.fname,flightc[source]);
       c.ftime=dist2[dest];
       c.fcost=price;
       c.fcost=dist1[dest];
       memcpy(c.route,a,sizeof(a));
       c.s=x;
       }
       else
        {cout<<endl<<flightt[dest];
        strcpy(c.fname,flightt[source]);
       c.ftime=dist2[dest];
       c.fcost=price;
       c.s=y;
       memcpy(c.route,b,sizeof(b));
        };
       cout<<" is held for booking"<<endl;
       cout<<"Enter the Booking Details"<<endl;
       cout<<"Name : ";
       cin>>c.name;
       cout<<"Age : ";
       cin>>c.age;
       cout<<"Date of travel(ddmmyyyy) : ";
       cin>>c.date;

       cout<<"Booking Finalised for travelling from "<<sour<<" to "<<des;
       cout<<"\n Your Ticket:\n";
       print_ticket();
       return;

    case 4:
        goto start;
    case 5:
        return;
    default:
        cout<<"Invalid Choice";


    }

}

}

int main(void)
{
//cost[MAXNODES][MAXNODES],time[MAXNODE][MAXNODE],dist[MAXNODES],visited[MAXNODES],path[MAXNODES],i,j,source,dest;
 int choice;
cout << "\n\n\n\n\n\n\t\t\t\t\t\t\t@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\n";
	cout << "\t\t\t\t\t\t\t@@ _______________________________________________________________________________________ @@\n";
	cout << "\t\t\t\t\t\t\t@@|                                           		                                  |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                           		                                  |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                           		                                  |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                           		                                  |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                           		                                  |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                           		                                  |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                        WELCOME TO                                     |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                                                                       |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                 AIRLINE RESERVATION SYSTEM                            |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                                                                       |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                                                                       |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                                                                       |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                                                                       |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                                                                       |@@\n";
	cout << "\t\t\t\t\t\t\t@@|                                                                                       |@@\n";
	cout << "\t\t\t\t\t\t\t@@|_______________________________________________________________________________________|@@\n";
	cout << "\t\t\t\t\t\t\t@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\n\n\n\n\t\t\t\t\t";
//cout<<"****************************************************************************************WELCOME********************************************************************************************************************"<<endl;
//cout<<"******************************************************************************************TO***********************************************************************************************************************"<<endl;
//cout<<"*************************************************************************************INDIGO*AIRLINES***************************************************************************************************************";
while(1)
{
    cout<<"\n\n\n1.Cities we travel\n2.Book your Flight\n3.Print your ticket\n4.Exit";
    cout<<"\nEnter your choice:";
    cin>>choice;
    switch(choice)
    {
    case 1:
        display_cities(cities,flightc,flightt);
        break;

    case 2:
        book_ticket(cities,flightc,flightt);
        break;
    case 3:
        print_ticket();
        break;
    case 4:
       exit(0);
    default:
        cout<<"Invalid Choice";

    }

}
return 0;
}

void fnDijkstra(int c[MAXNODES][MAXNODES], int d[MAXNODES], int p[MAXNODES],int s[MAXNODES], int so, int de, int n)
{
 int i,j,a,b,min;
 for (i=0;i<n;i++)
 {
 s[i] = 0;
 d[i] = c[so][i];
 p[i] = so;
 }
 s[so] = 1;
 for (i=1;i<n;i++)
 {
 min = INF;
 a = -1;
 for (j=0;j<n;j++)
 {
 if (s[j] == 0)
 {
 if (d[j] < min)
 {
 min = d[j];
 a = j;
 }
 }
 }
 if (a == -1) return;
 s[a] = 1;
 if (a == de) return;

 for (b=0;b<n;b++)
 {
 if (s[b] == 0)
 {
 if (d[a] + c[a][b] < d[b])
 {
 d[b] = d[a] + c[a][b];
 p[b] = a;
 }
 }
 }
 }
}
