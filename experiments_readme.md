# Analysis of Algorithms (AOA) Experiments

This repository contains C programs for various algorithm experiments.

## 1. Selection Sort
```c
#include<stdio.h>
#include<conio.h>

void main()
{
    int a[10], i, j, n, k;
    int temp, min;
    clrscr();
    printf("Enter the no. of elements:-->");
    scanf("%d", &n);
    
    for(i=0; i<n; i++)
    {
        printf("\nEnter a[%d]:->", i+1);
        scanf("%d", &a[i]);
    }
    
    for(i=0; i<n-1; i++)
    {
        min = i;
        for(j=i+1; j<n; j++)
        {
            if(a[j] < a[min])
            {
                min = j;
            }
        }
        if(min != i)
        {
            temp = a[i];
            a[i] = a[min];
            a[min] = temp;
        }
        printf("\nOutput after pass %d -->", i+1);
        for(k=0; k<n; k++)
        {
            printf("\t%d", a[k]);
        }
    }
    getch();
}
```

## 2. Merge Sort
```c
#include<stdio.h>
#include<conio.h>

void merge_sort(int low, int high, int a[], int b[]) {
    int mid, i, j, k;
    if (high <= low) {
        return;
    }
    
    mid = (low + high) / 2;
    i = low;
    j = mid + 1;
    
    merge_sort(low, mid, a, b);
    merge_sort(mid + 1, high, a, b);
    
    for (k = low; k <= high; k++) {
        if (i == mid + 1) {
            b[k] = a[j];
            j++;
        } else if (j == high + 1) {
            b[k] = a[i];
            i++;
        } else if (a[i] < a[j]) {
            b[k] = a[i];
            i++;
        } else {
            b[k] = a[j];
            j++;
        }
    }
    
    for (k = low; k <= high; k++) {
        a[k] = b[k];
    }
}

void main() {
    int a[100], b[100], n, i;
    clrscr();
    printf("Enter number of elements in the array \n");
    scanf("%d", &n);
    printf("Enter %d integers \n", n);
    for (i = 0; i < n; i++)
        scanf("%d", &a[i]);
        
    merge_sort(0, n - 1, a, b);
    
    printf("Printing the sorted array:\n");
    for (i = 0; i < n; i++)
        printf("\t%d", a[i]);
        
    getch();
}
```

## 3. All Pairs Shortest Path (Dynamic Programming)
```c
#include<stdio.h>
#include<conio.h>

int min(int, int);

void floyds(int p[10][10], int n) {
    int i, j, k;
    for(k=1; k<=n; k++)
        for(i=1; i<=n; i++)
            for(j=1; j<=n; j++)
                if(i==j)
                    p[i][j] = 0;
                else
                    p[i][j] = min(p[i][j], p[i][k] + p[k][j]);
}

int min(int a, int b) {
    if(a < b)
        return(a);
    else
        return(b);
}

void main() {
    int p[10][10], w, n, e, u, v, i, j;
    clrscr();
    printf("\n Enter the number of vertices:");
    scanf("%d", &n);
    printf("\n Enter the number of edges:");
    scanf("%d", &e);
    
    for(i=1; i<=n; i++) {
        for(j=1; j<=n; j++)
            p[i][j] = 999;
    }
    
    for(i=1; i<=e; i++) {
        printf("\n Enter the end vertices of edges %d with its weight:\n", i);
        scanf("%d%d%d", &u, &v, &w);
        p[u][v] = w;
    }
    
    printf("\n Matrix of input data:\n");
    for(i=1; i<=n; i++) {
        for(j=1; j<=n; j++)
            printf("%d \t", p[i][j]);
        printf("\n");
    }
    
    floyds(p, n);
    
    printf("\n transitive closure:\n");
    for(i=1; i<=n; i++) {
        for(j=1; j<=n; j++)
            printf("%d \t", p[i][j]);
        printf("\n");
    }
    
    printf("\n The shortest paths are:\n");
    for(i=1; i<=n; i++)
        for(j=1; j<=n; j++) {
            if(i != j)
                printf("\n <%d,%d>=%d", i, j, p[i][j]);
        }
    getch();
}
```

## 4. Naive String Matching
```c
#include<stdio.h>
#include<conio.h>
#include<string.h>

int naivestringmatch(char text[100], char pattern[100]);

void main()
{
    char text[100], pattern[100];
    int status;
    clrscr();
    printf("\n enter the text :-->");
    gets(text);
    printf("\n enter the pattern :-->");
    gets(pattern);
    status = naivestringmatch(text, pattern);
    
    if(status == -1)
    {
        printf("\n match not found!");
    }
    else
    {
        printf("\n match found on %d position !", status);
    }
    getch();
}

int naivestringmatch(char text[100], char pattern[100])
{
    int n, m, i, j, count = 0, temp = 0;
    n = strlen(text);
    m = strlen(pattern);
    
    for(i=0; i<=n-m; i++)
    {
        temp++;
        for(j=0; j<m; j++)
        {
            if(text[i+j] == pattern[j])
                count++;
        }
        if(count == m)
            return temp;
        count = 0;
    }
    return -1;
}
```

## 5. Minimum and Maximum Value in Array (Divide and Conquer)
```c
#include<stdio.h>
#include<conio.h>

int max, min;
int a[100];

void maxmin(int i, int j)
{
    int max1, min1, mid;
    if(i == j)
    {
        max = min = a[i];
    }
    else if (i == j - 1)
    {
        if(a[i] < a[j])
        {
            max = a[j];
            min = a[i];
        }
        else
        {
            max = a[i];
            min = a[j];
        }
    }
    else
    {
        mid = (i + j) / 2;
        maxmin(i, mid);
        max1 = max; 
        min1 = min;
        
        maxmin(mid + 1, j);
        
        if (max < max1)
            max = max1;
        if (min > min1)
            min = min1;
    }
}

void main()
{
    int i, num;
    clrscr();
    printf("\nEnter the total number of numbers: ");
    scanf("%d", &num);
    printf("Enter the numbers: \n");
    for(i=1; i<=num; i++)
        scanf("%d", &a[i]);
        
    max = a[1];
    min = a[1];
    
    maxmin(1, num);
    
    printf("Minimum element in an array:%d\n", min);
    printf("Maximum element in an array:%d\n", max);
    getch();
}
```