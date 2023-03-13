#include <iostream>
#include <string>
#include <vector>
#include <Windows.h>
    
using namespace std;
    
int main()
{
    setlocale(LC_ALL, "rus");
    SetConsoleCP(1251);
    SetConsoleOutputCP(1251);
    int col, row;
    string txt, vektor;

    string alph = "абвгдеёжзийклмнопрстуфхцчшщъыьэюя";
    vector <int> num;
    cout << "Введите текст шифрования " << endl;
    cin >> txt;
    cout << "Введите количество колонок ключевой матрицы " << endl;
    cin >> col;
    cout << "Введите количество строк ключевой матрицы " << endl;
    cin >> row;
    cout << "Введите ключевую матрицу " << endl;
    int** keymatrix = new int* [row];
    for (int i = 0; i < row; i++)
    {
        keymatrix[i] = new int[col];
    }
    for (int i = 0; i < row; i++)
    {
        for (int j = 0; j < col; j++)
        {
            cin >> keymatrix[i][j];
        }
    }
    for (int i = 0; i < row; i++)
    {
        for (int j = 0; j < col; j++)
        {
            cout << keymatrix[i][j] << " ";
        }
        cout << endl;
    }
    while (txt.length() % row != 0)
    {
        txt.push_back('ъ');
    }
    for (int i = 0; i < txt.length(); i++)
    {
        for (int j = 0; j < alph.length(); j++)
        {
            if (txt[i] == alph[j])
            {
                num.push_back(j);
            }
        }
    }
    vector <int> ansnum;
    int c = 0;
    int k = 0;
    for (int n = 0; n < txt.length(); n += row)
    {
        for (int i = 0; i < row; i++)
        {
            c = 0;
            k = n;
            for (int j = 0; j < col; j++)
            {
                c += keymatrix[i][j] * num[k];
                k++;
            }
            ansnum.push_back(c);
        }
    }
    cout << endl;
    for (int i = 0; i < txt.length(); i++)
    {
        cout << ansnum[i] << endl;
    }
    return 0;
}
