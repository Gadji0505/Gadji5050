//Найтисколярное произведение двух векторов(массивов), заданными воодимим n
#include <iostream>
#include <thread>
#include <mutex>
std::mutex mtx;
using namespace std;
void print_block(int* a,int* b ,int n, int* summ, int start)
{
    mtx.lock();
    for (int i = 0; i < n; i+=2)
        *(summ) += a[i] * b[i] ;
    mtx.unlock();
}
int main()
{
    setlocale(LC_ALL,"RU");
    int  n, x , l = 0;
    int summ = 0;
    cout << "Введите количество элементов векторов" << endl;
    cin >> n;
    int* a = new int[n];
    int* b = new int[n];
    cout << "Введите элементы первого вектора";
    for (int i = 0; i < n; i++)
    {
        cin >> a[i];
    }
    cout << "Введите элементы второго вектора";
    for (int i = 0; i < n; i++)
    {
        cin >> b[i];
    }
    thread th1(print_block, a, b, n, &summ, 0);
    thread th2(print_block, a, b, n, &summ, 1);
    th1.join();
    th2.join();
    cout << summ << endl;
}
