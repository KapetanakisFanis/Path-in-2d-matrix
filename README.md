# Path-in-2d-matrix 

#include<stdio.h>
#include<stdlib.h>
#include <time.h>
/*author Kapetanakis Fanis*/

int** create(int,int);
void display(int **, int,int);
void process(int**,int,int,int,int*,int*,int*,int,int,int);
void results(int*,int,int,int*);

int main()
{
	int m,n,sum=0,ak=0,l=0,i;
	int **table;
	int *max,*pin,*pin1;
	max=&ak;
	pin=(int*)malloc(2*(m+n-1)*sizeof(int));
	pin1=(int*)malloc(2*(m+n-1)*sizeof(int));
	
    printf("give rows and columns to create an array!\n");
	scanf("%d%d",&m,&n);
		
    table = create(m,n);	
    display(table,m,n);	
    process(table,0,0,sum,pin,pin1,max,l,m,n);
    
	results(pin1,m,n,max);
	
     for(i=0;i<1;i++){printf("\nBYE!\n"); }
    
	return 0;
}

int** create(int m, int n){
	int** table;
	int i,j,r1,r2,r3;
	table = (int**)malloc(m*sizeof(int*));
	for(i=0;i<m;i++)
	{
		table[i]=(int*)malloc(n*sizeof(int));
	} 
	
	srand(time (NULL));
   r1=rand()%(m*n+1);
   
   for(i=0;i<r1;i++)
   {  
      r2=rand()%m;
      r3=rand()%n;
      table[r2][r3]=1;
   }
   for(i=0;i<m;i++)
	{
		for(j=0;j<n;j++)
		{
			if(table[i][j]!=1)
			   table[i][j]=0;
		}
	}
		
    return table;
	
}

void display(int ** table,int m, int n){
	int i,j;
    for(i=0;i<m;i++)
	 {
	 	for(j=0;j<n;j++)
	 	{
	 		printf("%d--",table[i][j]);
	 		
		 }
		 printf("\n");
		 }	
	 
}

void process(int** table, int x, int y,int sum,int* pin,int* pin1,int* max,int l,int m,int n)
{   
    int i,j,a;

    if(x==(m-1) || y==(n-1)){
    if(x==(m-1)){
        for(j=y;j<n;j++) {
            pin[l]=x;
            pin[l+1]=j;
            l=l+2;
             if(table[x][j]==1){ sum=sum+1;}
        }
    }
    
    if(y==(n-1)){
        for(i=x;i<m;i++){
            pin[l]=i;
            pin[l+1]=y;
            l=l+2;
            if(table[i][y]==1){sum=sum+1;}
        }
       
    }
    if(sum>*max){
        *max=sum;
       for(a=0;a<(2*(m+n-1));a++) {pin1[a]=pin[a];}
        }
       l=0;

       return;
        
  }    
    
   if(table[x][y]==1){sum=sum+1;}
    pin[l]=x;
    pin[l+1]=y;
    l=l+2;
    
				
    process(table,x+1,y,sum,pin,pin1,max,l,m,n);
    
    process(table,x,y+1,sum,pin,pin1,max,l,m,n);
       
}
void results(int* pin1, int m, int n,int* max){
	int k;
	for(k=0;k<(2*(m+n-1));k++)
	{
	 if(k%2==0)	
	   printf("(%d,",pin1[k]+1);
	 else
	   printf("%d)-",pin1[k]+1);
  	}
  	
    printf("\nThe maximum number of coins is: %d",*max);
}

