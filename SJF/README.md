# SJF (Shortest Job First)

# Aim: Write a C program to implement the various process scheduling mechanisms such as SJF
Scheduling.
# Algorithm:
1: Start the process
2: Accept the number of processes in the ready Queue
3: For each process in the ready Q, assign the process id and accept the CPU burst time
4: Start the Ready Q according the shortest Burst time by sorting according to lowest to highest
       bursttime.
5: Set the waiting time of the first process as ‘0’ and its turnaround time as its burst time.
6: For each process in the ready queue, calculate
         (a) Waiting time for process(n)= waiting time of process (n-1) + Burst time of process(n-1)
         (b) Turn around time for Process(n)= waiting time of Process(n)+ Burst time for process(n)
7: Calculate
        (c) Average waiting time = Total waiting Time / Number of process
            • Average Turnaround time = Total Turnaround Time / Number of process
 8: Stop the process


# Program:

#include<stdio.h>
int main()
{
 int bt[20],p[20],wt[20],tat[20],i,j,n,total=0,pos,temp;
 float avg_wt,avg_tat;
 printf("Enter number of process:");
 scanf("%d",&n);
 printf("\nEnter Burst Time:\n");
 for(i=0;i<n;i++)
 {
 printf("p%d:",i+1);
 scanf("%d",&bt[i]);
 p[i]=i+1; //contains process number
 }
//sorting burst time in ascending order using selection sort
 for(i=0;i<n;i++)
 {
 pos=i;
 for(j=i+1;j<n;j++)
 {
 if(bt[j]<bt[pos])
 pos=j;
 }
 temp=bt[i];
 bt[i]=bt[pos];
 bt[pos]=temp;
 temp=p[i];
 p[i]=p[pos];
 p[pos]=temp;
 }
wt[0]=0; //waiting time for first process will be zero
 //calculate waiting time
 for(i=1;i<n;i++)
 {
 wt[i]=0;

 for(j=0;j<i;j++)
 wt[i]+=bt[j];
 total+=wt[i];
 }
 avg_wt=(float)total/n; //average waiting time
 total=0;
 printf("\nProcess\t Burst Time \tWaiting Time\tTurnaround Time");
for(i=0;i<n;i++)
 {
 tat[i]=bt[i]+wt[i]; //calculate turnaround time
 total+=tat[i];
 printf("\np%d\t\t %d\t\t %d\t\t\t%d",p[i],bt[i],wt[i],tat[i]);
 }
 avg_tat=(float)total/n; //average turnaround time
 printf("\n\nAverage Waiting Time=%f",avg_wt);
 printf("\nAverage Turnaround Time=%f\n",avg_tat);
}
