#include <stdio.h>
struct process{
    int burst, wait, comp, f;
}
p[20]={0,0};

int main()
{
    int n, i, j, totalwait=0, totalturn=0, quantum, flag=1,time=0;
    printf("\n Enter The No Of Process :");
    scanf ("%d", &n);
    printf("\n Enter The quantum time(in ms):");
    scanf("%d",&quantum);
    for(i=0;i<n;i++){
        printf("Enter The Burst Time (in ms): For Process #%2d:", i+1);
        scanf("%d",&p[i].burst);
        p[i].f=1;
    }
    printf("\n Order of Execution \n");
    printf("\n Process Starting Ending Remaining ");
    printf("\n Time Time Time");
    while(flag==1){
    flag=0;
    for(i=0;i<n;i++){
    if(p[i].f==1){
    flag=1;
    j=quantum;
    if((p[i].burst-p[i].comp)>quantum){
    p[i].comp+=quantum;
    }
    if((p[i].burst-p[i].comp)>quantum){
    p[i].comp+=quantum;
    }
    else{
    p[i].wait=time-p[i].comp;
    j=p[i].burst-p[i].comp;
    p[i].comp=p[i].burst;
    p[i].f=0;
    }
    printf("\nprocess # %-3d %-10d %-10d%-10d", i+1,time,time+j,p[i].burst-p[i].comp);
    time+=j; 
    }
    }
    }
    printf("\n\n------------------");
    printf("\nProcess \t Waiting Time TurnAround Time ");
    for(i=0;i<n;i++){
    printf("\nProcess # %-12d%-15d%-15d",i+1,p[i].wait,p[i].wait+p[i].burst);
    totalwait=totalwait+p[i].wait;
    totalturn=totalturn+p[i].wait+p[i].burst;
    }
    printf("\n\nAverage\n------------------");
    printf("\nWaiting Time : %fms",totalwait/(float)n);
    printf("\nTurnAround Time : %fms\n\n",totalturn/(float)n);
return 0;
}
