 Round Robin

Aim: Write a C program to implement the various process scheduling mechanisms such as Round
Robin Scheduling.
 
Algorithm
1: Start the process
2: Accept the number of processes in the ready Queue and time quantum (or) time slice
3: For each process in the ready Q, assign the process id and accept the CPU burst time
4: Calculate the no. of time slices for each process where
     No. of time slice for process(n) = burst time process(n)/time slice
5: If the burst time is less than the time slice then the no. of time slices =1.
6: Consider the ready queue is a circular Q, calculate
        (a) Waiting time for process(n) = waiting time of process(n-1)+ burst time of process(n-1 ) +
              the time difference in getting the CPU from process(n-1)
        (b) Turn around time for process(n) = waiting time of process(n) + burst time of process(n)+ the
               time difference in getting CPU from process(n).
7: Calculate
       (a) Average waiting time = Total waiting Time / Number of process
    (b) Average Turnaround time = Total Turnaround Time / Number of process Step 
8: Stop the proces.

program:
 
#include<stdio.h>
 int main()
{
 
  int count,j,n,time,remain,flag=0,time_quantum;
  int wait_time=0,turnaround_time=0,at[10],bt[10],rt[10];
  printf("Enter Total Process:\t ");
  scanf("%d",&n);
  remain=n;
  for(count=0;count<n;count++)
  {
    printf("Enter Arrival Time and Burst Time for Process Process Number %d :",count+1);
    scanf("%d",&at[count]);
    scanf("%d",&bt[count]);
    rt[count]=bt[count];
  }
  printf("Enter Time Quantum:\t");
  scanf("%d",&time_quantum);
  printf("\n\nProcess\t|Turnaround Time|Waiting Time\n\n");
  for(time=0,count=0;remain!=0;)
  {
    if(rt[count]<=time_quantum && rt[count]>0)
    {
      time+=rt[count];
      rt[count]=0;
      flag=1;
    }
    else if(rt[count]>0)
    {
      rt[count]-=time_quantum;
      time+=time_quantum;
    }
    if(rt[count]==0 && flag==1)
    {
      remain--;
      printf("P[%d]\t|\t%d\t|\t%d\n",count+1,time-at[count],time-at[count]-bt[count]);
      wait_time+=time-at[count]-bt[count];
      turnaround_time+=time-at[count];
      flag=0;
    }
    if(count==n-1)
      count=0;
    else if(at[count+1]<=time)
      count++;
    else
      count=0;
  }
  printf("\nAverage Waiting Time= %f\n",wait_time*1.0/n);
  printf("Avg Turnaround Time = %f",turnaround_time*1.0/n);
  
  return 0;
}
