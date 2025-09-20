# array

'''

#include<stdio.h>
#include<stdlib.h>

// Function declarations
void generateRandomNumbers(int*, int);
void printArray(int*,int);
void mergeSort(int*, int, int);
void merge(int*, int, int, int);

int main(void)
{
    //varaible declarations
    int* arr = NULL;
    int size;

    //code
    printf("Enter the size of an Array : ");
    scanf("%d", &size);

    //allocate dynamic memeory
    arr = (int*)malloc(sizeof(int) * size);

    //check for memory error
    if (arr == NULL)
    {
        printf("memory allcoation failed. \n");
        <img width="1920" height="1080" alt="Screenshot (61)" src="https://github.com/user-attachments/assets/9faf5751-c032-4b67-8f1a-8a41aba34844" />

        exit(-1);
    }

    //fill the array with random numbers
    generateRandomNumbers(arr, size);

    //print the original array
    printf("The original Array: \n");
    printArray(arr, size);

    mergeSort(arr, 0, size - 1);

    //print the Sorted array
    printf("The Sorted Array: \n");
    printArray(arr, size);

    //free the memory
    free(arr);
    arr = NULL;

    return(0);
}

void generateRandomNumbers(int* arr, int size)
{
    //varaible declarations
    int i;

    //code
    for (i = 0; i < size; i++)
        arr[i] = rand() % 100;
}

void printArray(int* arr, int size)
{
    //varaible declarations
    int i;

    //code
    for (i = 0; i < size; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

void mergeSort(int* arr, int first, int last)
{
    //varaible declarations
    int mid;
    //code
    if (first < last)
    {
        mid = (first + last) / 2;
        mergeSort(arr, first, mid);
        mergeSort(arr, mid + 1, last);
        merge(arr, first, mid, last);
    }
}

void merge(int* arr, int first, int mid, int last)
{
    //varaible declarations
    int* L = NULL; //for left array
    int* R = NULL; // for right array

    int len1 = mid - first + 1; //length of array 1
    int len2 = last - mid;  // length array 2

    int i;
    int j;
    int k;

    //Code
    //Create two new arrays
    L = (int*)malloc(sizeof(int) * len1);
    R = (int*)malloc(sizeof(int) * len2);

    if (L == NULL || R == NULL)
    {
        printf("Memory allocation faild to L and R arrays.\n");
        exit(-2);
    }

    // Copy the elements in Left array and Right Array
    k = first;
    for (i = 0; i < len1; i++)
    {
        L[i] = arr[k];
        k++;
    }
    k = mid + 1;
    for (i = 0; i < len2; i++)
    {
        R[i] = arr[k];
        k++;
    }

    //merge the Left and Right array in sorting manner in arr 
    i = 0;
    j = 0;
    k = first;

    while (i < len1 && j < len2)
    {
        if (L[i] < R[j])
        {
            arr[k] = L[i];
            k++;
            i++;
        }
        else
        {
            arr[k] = R[j];
            k++;
            j++;
        }
    }
    //Copy the remaining elements from L arry if any
    while (i < len1)
    {
        arr[k] = L[i];
        k++;
        i++;
    }
    //Copy the remaining elements from R arry if any
    while (j < len2)
    {
        arr[k] = R[j];
        k++;
        j++;
    }

    //Free the memory of L and R arrays
    free(L);
    L = NULL;
    free(R);
    R = NULL;
}

'''
