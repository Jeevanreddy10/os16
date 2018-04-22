#include<stdio.h>
#include<pthread.h>
#include<semaphore.h>
pthread_t t1,t2,t3,t4,t5;
pthread_mutex_t l1,l2;
int a;
void *average();
void *maximum();
void *minimum();
void *login();
main()
{
	
	    int i;
        pthread_create(&t1,NULL,login,NULL);
		pthread_join(t1,NULL);
}
void *average()
{   
	pthread_mutex_lock(&l1);
	int kl[8],i,n,sum=0;
	float avg;
	printf("\nPlease enter the no .of intergers : ");
	scanf("%d",&n);
	printf("\nEnter the intergers : ");
	for(i=0;i<n;i++)
	scanf("%d",&kl[i]);
	for(i=0;i<n;i++)
	sum=sum+kl[i];
	avg=sum/n;
	printf("The average of given numbers is  %f",avg);
	pthread_mutex_unlock(&l1);
	pthread_exit(NULL);
}
void *maximum()
{
	pthread_mutex_lock(&l2);
	
	int kl[8],i,n,max,avg;
	printf("\nPlease enter the no .of intergers : ");
	scanf("%d",&n);
	printf("\nEnter the intergers : ");
	for(i=0;i<n;i++)
	scanf("%d",&kl[i]);i=0;
	max=kl[i];
	for(i=0;i<n;i++)
	{
		if(max<=kl[i])
		max=kl[i];
	}
	printf("The maximum of given numbers is  %d:",max);
	pthread_mutex_unlock(&l2);
		pthread_exit(NULL);
}
void *minimum()
{
	pthread_mutex_lock(&l1);
	
	int kl[8],i,n,min,avg;
	printf("\nPlease enter the no .of intergers : ");
	scanf("%d",&n);
	printf("\nEnter the intergers : ");
	for(i=0;i<n;i++)
	scanf("%d",&kl[i]);i=0;
	min=kl[i];
	for(i=0;i<n;i++)
	{
		if(min>=kl[i])
		min=kl[i];
	}
	printf("The maximum of given numbers is  %d:",min);
	pthread_mutex_unlock(&l1);
    	pthread_exit(NULL);
}
void *login()
{
	float t;
	sunny:
    printf("\n1. For Average\n2. For Maximum\n3. For Minimum\n4. For Exit\nEnter Your choice :: ");
    scanf("%d",&a);

	if(a==1)
	{ 
	   	printf("\nAverage\n");
		pthread_create(&t3,NULL,average,NULL);
		pthread_join(t3,NULL);
     }	
     
	 else if(a==2)
	{ 
	
	 	printf("\nMaximum\n");
		pthread_create(&t4,NULL,maximum,NULL);
		pthread_join(t4,NULL);
     }
	
	
	else if(a==3)
	{ 
	 	printf("\nMinimum \n");
		pthread_create(&t5,NULL,minimum,NULL);
		pthread_join(t5,NULL);
     }	
    
	else if(a==4)
	{
		pthread_exit(NULL);
		return 0;
	}
	pthread_exit(NULL);}
