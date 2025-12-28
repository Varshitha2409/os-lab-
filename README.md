OS 

Prg 3: Producer and Consumer

#include<stdio.h> 
void main() 
{
 int buffer[10], bufsize, in, out, produce, consume, choice=0; 
in = 0; 
out = 0; 
bufsize = 10; 
while(choice !=3) 
    { 
      printf("\n 1. Produce \t 2. Consume \t3. Exit ");
      printf("\n Enter your choice: "); 
      scanf("%d", &choice); 
      switch(choice) 
            { 
            case 1: 
                  if((in+1)%bufsize==out) 
                       printf("\n Buffer is Full");
                  else
                        { 
                         printf("\n Enter the value: "); 
                         scanf("%d", &produce); 
                         buffer[in] = produce;
                         in = (in+1)%bufsize; 
                        }
                    break; 
           case 2: 
                if(in == out)
                     printf("\n Buffer is Empty");
                else
                    { 
                    consume = buffer[out]; 
                    printf("\n The consumed value is %d", consume); 
                    out = (out+1)%bufsize;
                    } 
                     break; 
                    }
              }
  }
o/p:
 1.producer 2. consumer 3.exit
enter your choice :1
enter the value :10
1.producer 2. consumer 3.exit
enter your choice :1
enter the value :20
1.producer 2. consumer 3.exit
enter your choice :2
The consumed value is 10
1.producer 2. consumer 3.exit
enter your choice :2
The consumed value is 20
1.producer 2. consumer 3.exit
enter your choice :2
buffer is empty .

Prg 5: CPU (FCFS(Without arrival time)):

#include<stdio.h> 
#include<conio.h> 
int main() 
{
 int bt[20], wt[20], tat[20], i, n;
 float wtavg, tatavg; 
printf("\nEnter the number of processes -- ");
 scanf("%d", &n); 
for(i=0;i<n;i++) 
{ 
printf("\nEnter Burst Time for Process %d -- ", i); 
scanf("%d", &bt[i]); 
} 
wt[0] = wtavg = 0; 
tat[0] = tatavg = bt[0];
 for(i=1;i<n;i++)
 {
 wt[i] = wt[i-1] +bt[i-1];
 tat[i] = tat[i-1] +bt[i]; 
wtavg = wtavg + wt[i]; 
tatavg = tatavg + tat[i]; 
} 
printf("\t PROCESS \tBURST TIME \t WAITING TIME\t TURNAROUND TIME\n"); 
for(i=0;i<n;i++)
 printf("\n\t P%d \t\t %d \t\t %d \t\t %d", i, bt[i], wt[i], tat[i]); 
printf("\nAverage Waiting Time -- %f", wtavg/n);
 printf("\nAverage Turnaround Time -- %f", tatavg/n); 

}
o/p:
Enter the number of processes:5
enter the burst time for process 0 : 2
enter the burst time for process 0 : 6
enter the burst time for process 0 : 4
enter the burst time for process 0 : 7
enter the burst time for process 0 : 4
Process           BT       WT       TAT
P0                    2          0          2
P1                    6          2          8
P2                    4          8         12
P3                    7         12        19 
P4                    4         19        23
Average WT =8.200
Average TAT = 12.800

ii. with arrival time 

#include <stdio.h>

int main() {
    int n, bt[20], at[20], wt[20], tat[20], ct[20];
    int i, j, temp;
    float wtavg = 0, tatavg = 0;
    int p[20];
    printf("Enter the number of processes: ");
    scanf("%d", &n);
    for (i = 0; i < n; i++) {
        p[i] = i + 1;
        printf("\nEnter Arrival Time for Process %d: ", i + 1);
        scanf("%d", &at[i]);
        printf("Enter Burst Time for Process %d: ", i + 1);
        scanf("%d", &bt[i]);
    }
    for (i = 0; i < n - 1; i++) {
        for (j = i + 1; j < n; j++) {
            if (at[i] > at[j]) {
                temp = at[i]; at[i] = at[j]; at[j] = temp;
                temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = p[i];  p[i] = p[j];  p[j] = temp;
            }
        }
    }
    ct[0] = at[0] + bt[0];
    tat[0] = ct[0] - at[0];
    wt[0] = tat[0] - bt[0];
    for (i = 1; i < n; i++) {
        if (at[i] > ct[i - 1])
            ct[i] = at[i] + bt[i];  
        else
            ct[i] = ct[i - 1] + bt[i];
        tat[i] = ct[i] - at[i];
        wt[i] = tat[i] - bt[i];
    }
    for (i = 0; i < n; i++) {
        wtavg += wt[i];
        tatavg += tat[i];
    }
    printf("\n------------------------------------------------------------");
    printf("\nProcess\tAT\tBT\tCT\tTAT\tWT");
    printf("\n------------------------------------------------------------");
    for (i = 0; i < n; i++) {
        printf("\nP%d\t%d\t%d\t%d\t%d\t%d", p[i], at[i], bt[i], ct[i], tat[i], wt[i]);
    }
    printf("\n------------------------------------------------------------");
    printf("\nAverage Turnaround Time = %.2f", tatavg / n);
    printf("\nAverage Waiting Time = %.2f\n", wtavg / n);
    return 0;
}
Prg 4: Dining philosopher

#include<stdio.h>
#include<stdlib.h>
int one();
int two() ;

int tph, philname[20], status[20], howhung, hu[20], cho; 
int main() 
{ 
    int i; 
    printf("\n\nDINING PHILOSOPHER PROBLEM"); 
    printf("\nEnter the total no. of philosophers: "); 
    scanf("%d",&tph); 
    for(i=0;i<tph;i++)
    { 
        philname[i] = (i); status[i]=1; 
    } 
    printf("How many are hungry : "); 
    scanf("%d", &howhung);
    if(howhung==tph)
    { 
        printf("\nAll are hungry..\nDead lock stage will occur"); 
        printf("\nExiting..");
        } 
        else
        { 
            for(i=0;i<howhung;i++)
            {
                printf("Enter philosopher %d position: ",(i+1)); 
                scanf("%d", &hu[i]); status[hu[i]]=2;   
            } 
            do 
            { 
                printf("1.One can eat at a time\t2.Two can eat at a time\t3.Exit\nEnter your choice:"); 
                scanf("%d", &cho);
                switch(cho) 
                { 
                    case 1:
                            one(); 
                            break; 
                    case 2: 
                             two(); 
                             break; 
                    case 3:
                        exit(0); 
                    default: 
                        printf("\nInvalid option.."); 
                }
            }
            while(1);
            } 
    
} 

int one()
{
    int pos=0, x, i; 
    printf("\nAllow one philosopher to eat at any time\n"); 
    for(i=0;i<howhung; i++, pos++) 
    { printf("\nP %d is granted to eat", philname[hu[pos]]); 
    for(x=pos+1;x<howhung;x++)
    printf("\nP %d is waiting", philname[hu[x]]);
    } 
} 


int two() 
{ 
int i, j, s=0, t, r, x; 
printf("\n Allow two philosophers to eat at same time\n");
for(i=0;i<howhung;i++) 
{ 
    for(j=i+1;j<howhung;j++)
    {
        if(abs(hu[i]-hu[j])!=1&& abs(hu[i]-hu[j])!=(tph-1))
        { 
            printf("\n\ncombination %d \n", (s+1)); 
            t=hu[i];
            r=hu[j];
            s++; 
            printf("\nP %d and P %d are granted to eat", philname[hu[i]], philname[hu[j]]);
            for(x=0;x<howhung;x++)
            { 
                if((hu[x]!=t)&&(hu[x]!=r))
                printf("\nP %d is waiting", philname[hu[x]]);
                } 
     } 
    }
    }
    }
o/p:
1.
DINING PHILOSOPHER PROBLEM
Enter the total number of  philosophers:3
how mny are hungry :3
All are hungry..
Dead lock stage will occur
Exiting..
2.
Enter the total no. of philosophers: 3
How many are hungry : 1
Enter philosopher 1 position: 2
1. 1 can eat at a time 2. 2 can eat at a time 3.exit
Enter your choice: 1
Allow one philosopher to eat at any time
P 2 is granted to eat
3.
Enter the total no. of philosophers: 3
How many are hungry : 2
Enter philosopher 1 position: 2
Enter philosopher 2 position: 4
1. 1 can eat at a time 2. 2 can eat at a time 3.exit
Enter your choice: 1
Allow one philosopher to eat at any time
P 2 is granted to eat
P 4 is waiting
P 4 is granted to eat
1. 1 can eat at a time 2. 2 can eat at a time 3.exit
Enter your choice: 2
Allow 2 philosopher to eat at the same time
combination 1
p2 and p4 are granted to eat
prg 7: bankers algorithm

#include <stdio.h>

int max[100][100], alloc[100][100], need[100][100], avail[100];
int n, r;

void input() {
    int i, j;
    printf("Enter number of processes: ");
    scanf("%d", &
    printf("Enter number of resources: ");
    scanf("%d", &r);
    printf("Enter Max matrix:\n");
    for(i=0;i<n;i++)
        for(j=0;j<r;j++)
            scanf("%d", &max[i][j]);
    printf("Enter Allocation matrix:\n");
    for(i=0;i<n;i++)
        for(j=0;j<r;j++)
            scanf("%d", &alloc[i][j]);
    printf("Enter Available resources:\n");
    for(j=0;j<r;j++)
        scanf("%d", &avail[j]);
}

void display() {
    int i,j;
    printf("\nProcess\tAlloc\tMax\tAvail\n");
    for(i=0;i<n;i++) {
        printf("P%d\t", i+1);
        for(j=0;j<r;j++) printf("%d ", alloc[i][j]);
        printf("\t");
        for(j=0;j<r;j++) printf("%d ", max[i][j]);
        printf("\t");
        if(i==0)
            for(j=0;j<r;j++) printf("%d ", avail[j]);
        printf("\n");
    }
}

void calculate() {
    int finish[100]={0}, safeSeq[100];
    int i,j,k, count=0, found;
    // Need matrix
    printf("\nNeed Matrix:\n");
    for(i=0;i<n;i++){
        for(j=0;j<r;j++){
            need[i][j] = max[i][j] - alloc[i][j];
            printf("%d ", need[i][j]);
        }
        printf("\n");
    }
    while(count < n) {
        found = 0;

        for(i=0;i<n;i++) {
            if(finish[i] == 0) {

                for(j=0;j<r;j++)
                    if(need[i][j] > avail[j])
                        break;

                if(j == r) {  
                    for(k=0;k<r;k++)
                        avail[k] += alloc[i][k];   

                    safeSeq[count++] = i;
                    finish[i] = 1;
                    found = 1;
                }
            }
        }

        if(!found) break;
    }

    if(count == n) {
        printf("\nSystem is in SAFE state.\nSafe Sequence: ");
        for(i=0;i<n;i++) printf("P%d ", safeSeq[i]);
    } else {
        printf("\nSystem is in UNSAFE state (Deadlock Detected).\n");
    }
}

int main() {
    printf("***** Banker's Algorithm *****\n");
    input();
    display();
    calculate();
    return 0;
}
************ Banker's Algorithm ************

Enter the no of Processes          5
Enter the no of resources instances  3

Enter the Max Matrix
7 5 3
3 2 2
9 0 2
2 2 2
4 3 3

Enter the Allocation Matrix
0 1 0
2 0 0
3 0 2
2 1 1
0 0 2

Enter the available Resources
3 3 2

Process    Allocation    Max        Available
P1             0 1 0         7 5 3            3 3 2
P2             2 0 0         3 2 2
P3             3 0 2         9 0 2
P4             2 1 1         2 2 2
P5             0 0 2         4 3 3

----------- Need Matrix -----------
7 4 3
1 2 2
6 0 0
0 1 1
4 3 1

Safe Sequence:
P2 -> P4 -> P5 -> P1 -> P3 ->

The system is in safe state

Program 8:
A. First Fit

#include<stdio.h> 
#include<conio.h>
#define max 25
void main() 
{ 
int frag[max],b[max],f[max],i,j,nb,nf,temp; 
static int bf[max],ff[max];
printf("\n\tMemory Management Scheme - First Fit"); 
printf("\nEnter the number of blocks:"); 
scanf("%d",&nb); 
printf("Enter the number of files:"); 
scanf("%d",&nf); 
printf("\nEnter the size of the blocks:-\n"); 
for(i=1;i<=nb;i++)
{
printf("Block %d:",i); scanf("%d",&b[i]);}
printf("Enter the size of the files :-\n");
for(i=1;i<=nf;i++) 
{ 
printf("File %d:",i);
scanf("%d",&f[i]); 
}
for(i=1;i<=nf;i++)
{ 
for(j=1;j<=nb;j++)
{
if(bf[j]!=1)
{
temp=b[j]-f[i];if(temp>=0) 
{ 
ff[i]=j;
break;
}
}
} 
frag[i]=temp;
bf[ff[i]]=1;
}
printf("\nFile_no:\tFile_size :\tBlock_no:\tBlock_size:\tFragement"); for(i=1;i<=nf;i++)
printf("\n%d\t\t%d\t\t%d\t\t%d\t\t%d",i,f[i],ff[i],b[ff[i]],frag[i]); 
getch();
}
o/p:
INPUT:
Enter the number of blocks: 3
Enter the number of files: 2
Enter the size of the blocks:
Block 1: 5
Block 2: 2
Block 3: 7
Enter the size of the files:
File 1: 1
File 2: 4
OUTPUT
File No	File Size	Block No	Block Size	Fragment
1	          1	           1	          5	                  4
2             	  4	           3             7	                  3

B. worst Fit

#include<stdio.h> 
#include<conio.h> 
#define max 25 
void main() 
{ 
int frag[max],b[max],f[max],i,j,nb,nf,temp,highest=0; 
static int bf[max],ff[max]; 
printf("\n\tMemory Management Scheme - Worst Fit");
 printf("\nEnter the number of blocks:");
scanf("%d",&nb); 
printf("Enter the number of files:"); 
scanf("%d",&nf); 
printf("\nEnter the size of the blocks:-\n"); 
for(i=1;i<=nb;i++) 
{
printf("Block %d:",i);
scanf("%d",&b[i]); 
}
printf("Enter the size of the files :-\n"); for(i=1;i<=nf;i++) 
{ 
printf("File %d:",i);
scanf("%d",&f[i]);} 
for(i=1;i<=nf;i++) 
{ 
for(j=1;j<=nb;j++) 
{ 
if(bf[j]!=1) //if bf[j] is not allocated 
{ 
temp=b[j]-f[i]; 
if(temp>=0)
if(highest<temp) 
{
ff[i]=j; 
highest=temp;} 
}
} 
frag[i]=highest;bf[ff[i]]=1; 
highest=0; 
} 
printf("\nFile_no:\tFile_size :\tBlock_no:\tBlock_size:\tFragement");
for(i=1;i<=nf;i++) 
printf("\n%d\t\t%d\t\t%d\t\t%d\t\t%d",i,f[i],ff[i],b[ff[i]],frag[i]); getch();
}
o/p:
INPUT:
Enter the number of blocks: 3
Enter the number of files: 2
Enter the size of the blocks:
Block 1: 5
Block 2: 2
Block 3: 7
Enter the size of the files:
File 1: 1
File 2: 4
OUTPUT
File No	File Size	Block No	Block Size	Fragment
1	          1	           3	          7	                  6
2             	  4	           1             5	                  1
Program 1:
a.read (),write().

#include<unistd.h>
int main()
{
int nread;
char buff[20];
nread=read(0,buff,10);
write (1,buff,nread);
return 0;
}
o/p
babbyamma
babbyamma

b. 10 characters

#include<unistd.h>
#include<fcntl.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<stdio.h>
int main()
{
int n,f,f1;
char buff[10];
f=open("seeking",O_RDWR);
f1=lseek(f,10,SEEK_SET);
printf("Pointer is at %d position\n",f1);
read(f,buff,10);
write(1,buff,10);
}
o/p
cc filename.c
echo "1234567890abcdefghijxxxxxxxx" > seeking 
./a.out
Pointer is at 10 Position 
abcdefghij

Program 9
A.FIFO 

#include<stdio.h>
 void main() 
{
int i, j, k, f, pf=0, count=0, rs[25], m[10], n; 
printf("\n Enter the length of reference string -- "); 
scanf("%d",&n); printf("\n Enter the reference string -- "); 
for(i=0;i<n;i++) 
scanf("%d",&rs[i]); 
printf("\n Enter no. of frames -- "); 
scanf("%d",&f);
for(i=0;i<f;i++) 
m[i]=-1; 
printf("\n The Page Replacement Process is -- \n"); 
for(i=0;i<n;i++) 
{ 
for(k=0;k<f;k++) 
{
if(m[k]==rs[i]) break;
}
if(k==f) 
{ 
m[count++]=rs[i];
pf++; 
}
for(j=0;j<f;j++)
printf("\t%d",m[j]);
if(k==f) 
printf("\tPF No. %d",pf); printf("\n");
if(count==f) 
count=0; 
} 
printf("\n The number of Page Faults using FIFO are %d",pf);
}
I/P
Enter the length of reference string -- 20
Enter the reference string --
7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1 7 0 1
Enter no. of frames -- 3


O/P:
7   -1  -1        PF No. 1
7    0  -1        PF No. 2
7    0   1        PF No. 3
2    0   1        PF No. 4
2    0   1       
2    3   1        PF No. 5
2    3   0        PF No. 6
4    3   0        PF No. 7
4    2   0        PF No. 8
4    2   3        PF No. 9
0    2   3        PF No. 10
0    2   3
0    2   3      
0    1   3        PF No. 11
0    1   2        PF No. 12
0    1   2
7    1   2        PF No. 13
7    0   2        PF No. 14
7    0   1        PF No. 15

The number of Page Fault using FIFO are 15

B. LRU 
 
#include<stdio.h> 
 void main() 
{ 
int i, j , k, min, rs[25], m[10], count[10], flag[25], n, f, pf=0, next=1; 
printf("Enter the length of reference string -- "); 
scanf("%d",&n); printf("Enter the reference string -- ");
for(i=0;i<n;i++)
{ 
scanf("%d",&rs[i]); 
flag[i]=0;
}
printf("Enter the number of frames -- "); 
scanf("%d",&f); 
for(i=0;i<f;i++) 
{ 
count[i]=0; 
m[i]=-1; 
}
printf("\nThe Page Replacement process is -- \n");
for(i=0;i<n;i++) 
{ 
for(j=0;j<f;j++)
{
if(m[j]==rs[i]) 
{
flag[i]=1; 
count[j]=next; next++; 
} 
}
if(flag[i]==0) 
{ 
if(i<f)
{
m[i]=rs[i];
count[i]=next; 
next++; 
} 
else
{ 
min=0; 
for(j=1;j<f;j++)
if(count[min] > count[j])
min=j; 
m[min]=rs[i]; 
count[min]=next;
next++;
} 
pf++; 
} 
for(j=0;j<f;j++) 
printf("%d\t", m[j]);
if(flag[i]==0)
printf("PF No. -- %d" , pf); 
printf("\n"); 
} 
printf("\nThe number of page faults using LRU are %d",pf); 

}
i/p:
Enter the length of reference string -- 20
Enter the reference string --
7 0 1 2 0 3 2 4 0 3 0 3 2 1 3 0 1 0 7 0
Enter the number of frames -- 3


O/P:
7   -1  -1        PF No. 1
7    0  -1        PF No. 2
7    0   1        PF No. 3
2    0   1        PF No. 4
2    0   1        
2    0   3        PF No. 5
2    0   3       
4    0   3        PF No. 6
4    0   2        PF No. 7
4    3   2        PF No. 8
0    3   2        PF No. 9
0    3   2
0    3   2      
1    3   2       PF No. 10
1    3   2     
1    0   2        PF No. 11
1    0   2
1    0   7        PF No. 12
1    0   7
1    0   7
The number of Page Fault using LRU are 12

Program 10

A. SSTF Scheduling 
#include<stdio.h>
#include<math.h>
int main()
{
int queue[100],t[100],head,seek=0,n,i,j,temp;
float avg;
printf("*** SSTF Disk Scheduling Algorithm ***\n");
printf("Enter the size of Queue\t");
scanf("%d",&n);
printf("Enter the Queue\t");
for(i=0;i<n;i++)
{
scanf("%d",&queue[i]);
}
printf("Enter the initial head position\t");
scanf("%d",&head);
for(i=1;i<n;i++)
t[i]=abs(head-queue[i]);
for(i=0;i<n;i++)
{
for(j=i+1;j<n;j++)
{
if(t[i]>t[j])
{
temp=t[i];
t[i]=t[j];
t[j]=temp;
temp=queue[i];
queue[i]=queue[j];
queue[j]=temp;
}
}
}
for(i=1;i<n-1;i++)
{
seek=seek+abs(head-queue[i]);
head=queue[i];
}
printf("\nTotal Seek Time is%d\t",seek);
avg=seek/(float)n;
printf("\nAverage Seek Time is %f\t",avg);
return 0;
}

OUTPUT: 
*** SSTF Disk Scheduling Algorithm *** 
Enter the size of Queue 5 
Enter the Queue 10 17 2 15 4 
Enter the initial head position 3 
Total Seek Time is14 
Average Seek Time is 2.800000 
RESULT: 
Thus the program was executed and verified successfully.

B. SCAN Scheduling 
SCAN DISK SCHEDULING ALGORITHM 
#include<stdio.h>
void main()
{
    int t[20], d[20], h, i, j, n, temp, k, atr[20], p = 0, sum = 0;
    printf("enter the no of tracks to be traveresed ");
    scanf("%d", &n);
    printf("enter the position of head ");
    scanf("%d", &h);
    t[0] = h;
    printf("enter the tracks ");
    for (i = 1; i <= n; i++)
        scanf("%d", &t[i]);
    for (i = 0; i <= n; i++)
    {
        for (j = 0; j < n - i; j++)
        {
            if (t[j] > t[j + 1])
            {
                temp = t[j];
                t[j] = t[j + 1];
                t[j + 1] = temp;
            }
        }
    }
    for (i = 0; i <= n; i++)
        if (t[i] == h)
            k = i;
    for (i = k + 1; i <= n; i++)
        atr[p++] = t[i];
    for (i = k - 1; i >= 0; i--)
        atr[p++] = t[i];
    for (i = 0; i < p; i++)
    {
        if (i == 0)
            d[i] = atr[i] - h;
        else
            d[i] = atr[i] - atr[i - 1];
        if (d[i] < 0) d[i] = -d[i];
        sum += d[i];
    }
    printf("\n\nTracks Traversed\tDifference Between tracks\n");
    for (i = 0; i < p; i++)
        printf("%d\t\t\t%d\n", atr[i], d[i]);
    printf("\nAverage header movements: %.2f", (float)sum / n);
}


INPUT 
Enter no.of tracks to be traveresed:9  
enter the position of head :100
Enter tracks:55 58 60 70 18 90 150 160 184  
OUTPUT: 
Tracks Traversed  
150               
160        
184    
90    
70    
60    
58    
55    
18    
Difference Between tracks 
50 
10 
24 
94 
20 
10 
2 
3 
37 
Average head movement is 27.78

Program 11:
A. SEQUENTIAL FILE ALLOCATION
#include<stdio.h>
#include <string.h>

struct fileTable
{ 
char name[20]; 
int sb, nob;
}ft[30]; 
void main() 
{ 
int i, j, n; 
char s[20]; 
printf("Enter no of files :"); 
scanf("%d",&n); 
for(i=0;i<n;i++)
{ 
printf("\nEnter file name %d :",i+1); 
scanf("%s",ft[i].name); 
printf("Enter starting block of file %d :",i+1); 
scanf("%d",&ft[i].sb); 
printf("Enter no of blocks in file %d :",i+1); 
scanf("%d",&ft[i].nob); 
} 
printf("\nEnter the file name to be searched -- "); 
scanf("%s",s); 
for(i=0;i<n;i++) 
if(strcmp(s, ft[i].name)==0)
break; 
if(i==n) 
printf("\nFile Not Found"); 
else 
{ 
printf("\nFILE NAME START BLOCK NO OF BLOCKS BLOCKS OCCUPIED\n"); 
printf("\n%s\t\t%d\t\t%d\t",ft[i].name,ft[i].sb,ft[i].nob); 
for(j=0;j<ft[i].nob;j++)
printf("%d, ",ft[i].sb+j);
} 
}

INPUT: Enter no of files :3 
Enter file name 1 :A  
Enter starting block of file 1 :85  
Enter no of blocks in file 1 :6  
Enter file name 2 :B  
Enter starting block of file 2 :102 
Enter no of blocks in file 2 :4  
Enter file name 3 :C  
Enter starting block of file 3 :60  
Enter no of blocks in file 3 :4  
Enter the file name to be searched -- B  
OUTPUT:  
FILE NAME     START BLOCK    NO OF BLOCKS        BLOCKS OCCUPIED 
B                          102                         4                            102,103,104,105      

B. INDEXED FILE ALLOCATION
#include<stdio.h> 
#include <string.h>

struct fileTable 
{ 
char name[20];
int nob, blocks[30];
}ft[30]; 
void main() 
{ 
int i, j, n; 
char s[20]; 
printf("Enter no of files :");
scanf("%d",&n);
for(i=0;i<n;i++)
{ 
printf("\nEnter file name %d :",i+1); 
scanf("%s",ft[i].name);
printf("Enter no of blocks in file %d :",i+1); 
scanf("%d",&ft[i].nob); 
printf("Enter the blocks of the file :"); 
for(j=0;j<ft[i].nob;j++) 
scanf("%d",&ft[i].blocks[j]);
} 
printf("\nEnter the file name to be searched -- "); 
scanf("%s",s); 
for(i=0;i<n;i++) 
if(strcmp(s, ft[i].name)==0) 
break; 
if(i==n) 
printf("\nFile Not Found"); 
else 
{ 
printf("\nFILE NAME NO OF BLOCKS BLOCKS OCCUPIED"); 
printf("\n %s\t\t%d\t",ft[i].name,ft[i].nob); 
for(j=0;j<ft[i].nob;j++)
printf("%d, ",ft[i].blocks[j]); 
} 
}

INPUT:  
Enter no of files : 2  
Enter file 1 : A  
Enter no of blocks in file 1 : 4  
Enter the blocks of the file 1 : 12 23 9 4  

Enter file 2 : G  
Enter no of blocks in file 2: 5  
Enter the blocks of the file 2: 88 77 66 55 44 
Enter the file to be searched: G  
OUTPUT:  
FILE NAME       NO OF BLOCKS               BLOCKS OCCUPIED    
G                            5                                     88, 77, 66, 55, 44 13
   
Prg 2: IPC

a.Shared Memory for Writer Process 
#include<stdio.h> 
#include<stdlib.h> 
#include<unistd.h> 
#include<sys/shm.h> 
#include<string.h> 
 
int main() 
{ 
int i; 
void *shared_memory; 
char buff[100]; 
int shmid; 
shmid=shmget((key_t)2345, 1024, 0666|IPC_CREAT);  
printf("Key of shared memory is %d\n",shmid); 
shared_memory=shmat(shmid,NULL,0);  
printf("Process attached at %p\n",shared_memory);  
printf("Enter some data to write to shared memory\n"); 
read(0,buff,100);
strcpy(shared_memory,buff);
printf("You wrote : %s\n",(char *)shared_memory); 
} 
Output: 
Key of shared memory is 0 
Process attached at x7ffe04fb000 
Enter some data to write to shared memory 
Hello World 
You wrote: Hello World 

b.Shared Memory for Reader Process 
#include<stdio.h> 
#include<stdlib.h> 
#include<unistd.h> 
#include<sys/shm.h> 
#include<string.h> 
int main() 
{ 
int i; 
void *shared_memory; 
char buff[100]; 
int shmid; 
shmid=shmget((key_t)2345, 1024, 0666); 
printf("Key of shared memory is %d\n",shmid); 
shared_memory=shmat(shmid,NULL,0);
printf("Process attached at %p\n",shared_memory); 
printf("Data read from shared memory is : %s\n",(char *)shared_memory); 
}
o/p:
Key of Shared memory is 0 
Process attached at 0x7f76b4292999 
Data read from shared memory is: Hello World

commands:                                            
172.31.31.20    
UN:user24
PW:csuser24
vi filename.c  (create file)
Press Insert and Type the code 
esc:w(to save)
esc:wq(to save and exit)
cc filename.c(compile)
./a.out (run)
