#include <iostream>
#include<cstdlib>
#include <chrono>
#include <fstream>

using namespace std;
using namespace std::chrono;

int v1[1000], v2[10000], v3[100000];

void getNumbers(int n, int *v)
{
    srand((unsigned) time(NULL));
    for(int i=1; i<=n; i++) {
        v[i] = 10000 + (rand() % 1000000);
    }
}

void insertionSort(int v[], int n)
{
    int i, key, j;
    for (i = 1; i < n; i++)
    {
        key = v[i];
        for(j = i - 1; j >= 0 && v[j] > key; j--) {
            v[j + 1] = v[j];
        }
        v[j + 1] = key;
    }
}

void bubbleSort(int arr[], int n)
{
    int i, j;
    for (i = 0; i < n - 1; i++)
        for (j = 0; j < n - i - 1; j++)
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
}

void swap(int *a, int *b) {
    int t = *a;
    *a = *b;
    *b = t;
}




int partition(int array[], int smaller, int bigger) {
    int pivot = array[bigger];
    int i = (smaller - 1);
    for (int j = smaller; j < bigger; j++) {
        if (array[j] <= pivot) {
            i++;
            swap(&array[i], &array[j]);
        }
    }
    swap(&array[i + 1], &array[bigger]);
    return (i + 1);
}

void quickSort(int array[], int low, int high) {
    if (low < high) {

        int piv = partition(array, low, high);
        quickSort(array, low, piv - 1);
        quickSort(array, piv + 1, high);
    }
}



void merge(int array[], int const left, int const mid,int const right)
{
    auto const subArrayOne = mid - left + 1;
    auto const subArrayTwo = right - mid;

    auto *leftArray = new int[subArrayOne],
            *rightArray = new int[subArrayTwo];

    for (auto i = 0; i < subArrayOne; i++)
        leftArray[i] = array[left + i];
    for (auto j = 0; j < subArrayTwo; j++)
        rightArray[j] = array[mid + 1 + j];

    auto indexOfSubArrayOne = 0,
            indexOfSubArrayTwo = 0;
    int indexOfMergedArray= left;
    while (indexOfSubArrayOne < subArrayOne && indexOfSubArrayTwo < subArrayTwo) {
        if (leftArray[indexOfSubArrayOne] <= rightArray[indexOfSubArrayTwo]) {
            array[indexOfMergedArray] = leftArray[indexOfSubArrayOne];
            indexOfSubArrayOne++;
        }
        else {
            array[indexOfMergedArray] = rightArray[indexOfSubArrayTwo];
            indexOfSubArrayTwo++;
        }
        indexOfMergedArray++;
    }
    while (indexOfSubArrayOne < subArrayOne) {
        array[indexOfMergedArray] = leftArray[indexOfSubArrayOne];
        indexOfSubArrayOne++;
        indexOfMergedArray++;
    }
    while (indexOfSubArrayTwo < subArrayTwo) {
        array[indexOfMergedArray] = rightArray[indexOfSubArrayTwo];
        indexOfSubArrayTwo++;
        indexOfMergedArray++;
    }
    delete[] leftArray;
    delete[] rightArray;
}

void mergeSort(int array[], int const begin, int const end)
{
    if (begin >= end)
        return;

    auto mid = begin + (end - begin) / 2;
    mergeSort(array, begin, mid);
    mergeSort(array, mid + 1, end);
    merge(array, begin, mid, end);
}

int getMax(int arr[], int n)
{
    int mx = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > mx)
            mx = arr[i];
    return mx;
}


void countSort(int arr[], int n, int exp)
{
    int out[n];
    int i, count[10] = { 0 };
    for (i = 0; i < n; i++)
        count[(arr[i] / exp) % 10]++;

    for (i = 1; i < 10; i++)
        count[i] += count[i - 1];

    for (i = n - 1; i >= 0; i--) {
        out[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    for (i = 0; i < n; i++)
        arr[i] = out[i];
}

void radixsort(int arr[], int n)
{
    int m = getMax(arr, n);
    for (int exp = 1; m / exp > 0; exp *= 10)
        countSort(arr, n, exp);
}

int findMax(int arr[], int n)
{
    int i,max=arr[0],cnt=0;
    for(i=1;i<n;i++)
    {
        if(arr[i]>max)
            max=arr[i];
    }
    while(max>0)
    {
        cnt++;
        max=max/10;
    }
    return cnt;
}

void bucketSort(int arr[],int *bucket[],int n)
{
    static int i,j[10],k,l,s=1;
    int c;
    c=findMax(arr,n);

    for(int m=0;m<c;m++)
    {
        for(i=0;i<10;i++)
            j[i]=0;
        for(i=0;i<n;i++)
        {
            k=(arr[i]/s)%10;
            bucket[k][j[k]]=arr[i];
            j[k]++;
        }

        l=0;
        for(i=0;i<10;i++)
        {
            for(k=0;k<j[i];k++)
            {
                arr[l]=bucket[i][k];
                l++;
            }
        }
        s*=10;
    }
}

void heapify(int arr[], int N, int i)
{
    int largest = i;

    int l = 2 * i + 1;

    int r = 2 * i + 2;

    if (l < N && arr[l] > arr[largest])
        largest = l;

    if (r < N && arr[r] > arr[largest])
        largest = r;

    if (largest != i) {
        swap(arr[i], arr[largest]);

        heapify(arr, N, largest);
    }
}


void heapSort(int arr[], int N)
{
    for (int i = N / 2 - 1; i >= 0; i--)
        heapify(arr, N, i);

    for (int i = N - 1; i > 0; i--) {
        swap(arr[0], arr[i]);
        heapify(arr, i, 0);
    }
}
void timeInsertionSort()
{
    cout << "--------------Insertion sort:--------------\n\n";
    auto start = high_resolution_clock::now();
    insertionSort(v1,1000);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    cout << "1000 numbers: "<< duration.count() << " ms\n";

    start = high_resolution_clock::now();
    insertionSort(v2,10000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "10000 numbers: " << duration.count() << " ms\n";

    start = high_resolution_clock::now();
    insertionSort(v3,100000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "100000 numbers: " << duration.count() << " ms\n\n";
}


void timeBubbleSort()
{
    cout << "\n\n--------------Bubble sort:--------------\n";
    auto start = high_resolution_clock::now();
    bubbleSort(v1,1000);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    cout << "1000 numbers: "<< duration.count() << " ms\n";

    start = high_resolution_clock::now();
    bubbleSort(v2,10000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "10000 numbers: " << duration.count() << " ms\n";

    start = high_resolution_clock::now();
    bubbleSort(v3,100000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "100000 numbers: " << duration.count() << " ms\n\n";
}



void timeQuickSort()
{
    cout << "\n\n--------------Quick Sort:--------------\n";
    auto start = high_resolution_clock::now();
    quickSort(v1,0,999);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    cout << "1000 numbers: "<< duration.count() << " ms\n";

    start = high_resolution_clock::now();
    quickSort(v2,0,9999);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "10000 numbers: " << duration.count() << " ms\n";

    start = high_resolution_clock::now();
    quickSort(v3,0,30000); // It cannot sort to 100000 as it just ends
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "100000 numbers: " << duration.count() << " ms\n\n";
}

void timeMergeSort()
{
    cout << "\n\n--------------Merge Sort:--------------\n";
    auto start = high_resolution_clock::now();
    mergeSort(v1,0,999);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    cout << "1000 numbers: "<< duration.count() << " ms\n";

    start = high_resolution_clock::now();
    mergeSort(v2,0,9999);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "10000 numbers: " << duration.count() << " ms\n";

    start = high_resolution_clock::now();
    mergeSort(v3,0,99999);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "100000 numbers: " << duration.count() << " ms\n\n";
}

void timeRadixSort()
{

    cout << "--------------Radix sort:--------------\n\n";
    auto start = high_resolution_clock::now();
    radixsort(v1,1000);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    cout << "1000 numbers: "<< duration.count() << " ms\n";

    start = high_resolution_clock::now();
    radixsort(v2,10000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "10000 numbers: " << duration.count() << " ms\n";

    start = high_resolution_clock::now();
    radixsort(v3,100000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "100000 numbers: " << duration.count() << " ms\n\n";
}

void timeBucketSort()
{
    int i;
    int *bucket[10];
    for(i=0;i<10;i++)
        bucket[i]=new int[1000];
    cout << "--------------Bucket sort:--------------\n\n";
    auto start = high_resolution_clock::now();
    bucketSort(v1,bucket,1000);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    cout << "1000 numbers: "<< duration.count() << " ms\n";

    for(i=0;i<10;i++)
        bucket[i]=new int[10000];
    start = high_resolution_clock::now();
    bucketSort(v2,bucket,10000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "10000 numbers: " << duration.count() << " ms\n";

    for(i=0;i<10;i++)
        bucket[i]=new int[100000];
    start = high_resolution_clock::now();
    bucketSort(v3,bucket,100000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "100000 numbers: " << duration.count() << " ms\n\n";
}


void timeHeapSort()
{
    cout << "\n\n--------------Heap sort:--------------\n";
    auto start = high_resolution_clock::now();
    heapSort(v1,1000);
    auto stop = high_resolution_clock::now();
    auto duration = duration_cast<microseconds>(stop - start);
    cout << "1000 numbers: "<< duration.count() << " ms\n";

    start = high_resolution_clock::now();
    heapSort(v2,10000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "10000 numbers: " << duration.count() << " ms\n";

    start = high_resolution_clock::now();
    heapSort(v3,100000);
    stop = high_resolution_clock::now();
    duration = duration_cast<microseconds>(stop - start);
    cout << "100000 numbers: " << duration.count() << " ms\n\n";
}


void read()
{
    ifstream fout("1000.txt");
    for(int i = 0; i < 1000; i++)
        fout >> v1[i];
    ifstream fout2("10000.txt");
    for(int i = 0; i < 10000; i++)
        fout2 >> v2[i];
    ifstream fout3("100000.txt");
    for(int i = 0; i < 100000; i++)
        fout3 >> v3[i];
    fout.close();
    fout2.close();
    fout3.close();
}
void writeNumbers()
{
    getNumbers(1000,v1);
    getNumbers(10000,v2);
    getNumbers(100000,v3);
    ofstream fout("1000.txt");
    for(int i = 0; i < 1000; i++)
        fout << v1[i] << " ";
    ofstream fout2("10000.txt");
    for(int i = 0; i < 10000; i++)
        fout2 << v2[i] << " ";
    ofstream fout3("100000.txt");
    for(int i = 0; i < 100000; i++)
        fout3 << v3[i] << " ";
    fout.close();
    fout2.close();
    fout3.close();
}
int main()
{

    read();
    timeInsertionSort();
    read();

    timeBubbleSort();
    read();

    timeRadixSort();
    read();

    timeBucketSort();
    read();

    timeHeapSort();
    read();

    timeMergeSort();
    read();

    timeQuickSort();




    return 0;
}
