# lab_3.2 Мартиненко Ре-22

![alt tag](https://github.com/Nikita7131/lab3.2/blob/main/main.png "Описание небудет)")​

```ruby

#include <Windows.h>
#include <stdio.h>
#include <math.h>
#include <conio.h>

int a,b;
double e = 0.01;
double c;

double result;
int Metod_Used;
unsigned int Debug;

int ValuesPrined;
int CntValuesPrined = 0;

//==============================================================================================================//
double func(double x) {
  return pow(x, 3) - 18 * x - 83;
  // return 2*pow((x-1000),3)-3*pow((x+500),2)+(4*x)-5; // завдання 15 варіанту, але воно інколи ламає весь код
}
//==============================================================================================================//
double method_chord(int x_prev, int x_curr, double e) {
  double x_next = 0;
  double tmp;
  do {
    tmp = x_next;
    x_next = x_curr - func(x_curr) * (x_prev - x_curr) / (func(x_prev) - func(x_curr));
    x_prev = x_curr;
    x_curr = tmp;
    switch (Debug) {
      case 1:
        printf("Root = %lf\n", x_next);
        break;
      case 2:
        printf("Root = %lf\n", x_next);
        CntValuesPrined ++;
        if (CntValuesPrined >= ValuesPrined) {
          WhatTooDoo();
        }
        break;
    }
    printf("abs = %lf\n", abs(x_next - x_curr));

  } while (abs(x_next - x_curr) > e);
  return x_next;
}
//==============================================================================================================//
void bisection(double a, double b) {
  c = a;
  while ((b - a) >= e) {
    c = (a + b) / 2;
    if (func(c) == 0.0) {
      switch (Debug) {
        case 1:
          printf("Root = %lf\n", c);
          break;
        case 2:
          printf("Root = %lf\n", c);
          CntValuesPrined ++;
          if (CntValuesPrined >= ValuesPrined) {
            WhatTooDoo();
          }
          break;
      }
      break;
    }
    else if (func(c)*func(a) < 0) {
      b = c;
      switch (Debug) {
        case 1:
          printf("Root = %lf\n", c);
          break;
        case 2:
          printf("Root = %lf\n", c);
          CntValuesPrined ++;
          if (CntValuesPrined >= ValuesPrined) {
            WhatTooDoo();
          }
          break;
      }
    }
    else {
      a = c;
      switch (Debug) {
        case 1:
          printf("Root = %lf\n", c);
          break;
        case 2:
          printf("Root = %lf\n", c);
          CntValuesPrined ++;
          if (CntValuesPrined >= ValuesPrined) {
            WhatTooDoo();
          }
          break;
      }
    }
  }
}
//==============================================================================================================//
void WhatTooDoo() {

  printf("\n первищено кількість ітерацій з видачею інформації для прийняття рішення, що робити далі :");
  printf("\n 0) продовжити з такою ж кількістю ітерацій;");
  printf("\n 1) виконати програма до кінця, поки не будуть знайдено корені рівняння; ");
  printf("\n 2) вийти із програми, перед виходом вивівши на екран отриманий проміжний результат підрахунку;");
  printf("\n ВАША ВІДПОВІДЬ: ");

  int WhatDo;

  scanf("\n %d", &WhatDo);

  CntValuesPrined = 0;
  switch (WhatDo) {
    case 1:
      Debug = 1;
      break;
    case 2:
      Debug = 0;
      break;
  }

  printf("\n");
}
//==============================================================================================================//
int main() {
  double StartTime;
  //==============================================================================================================//
  SetConsoleOutputCP(1251); // вмикаєм кирилицю
  SetConsoleCP(1251);

  printf(" Created by Nikita Martynenko, Re-22\n");
  printf("\n Виберіть метод обчислення рівняння:\n");
  //==============================================================================================================//
  printf("\n   1 - методом половинного ділення");
  printf("\n   2 - методом хорд");

  printf("\n ВАША ВІДПОВІДЬ: ");
  while (scanf("%d", &Metod_Used) && Metod_Used - 1u > 1) {
    printf("\n Error, please try again:\n ");
  };
  //==============================================================================================================//
  printf("\n enter: 0-NoDebug  1-Debug  2-Debug with parametrs: ");
  while (scanf("%d", &Debug) && Debug > 2) {
    printf("\n Error, please try again:\n ");
  };
  if (Debug == 2) {
    printf("\n кількість ітерацій з видачею інформації для прийняття рішення, що робити далі :");
    scanf("%d", &ValuesPrined);
  }
  //==============================================================================================================//
  printf("\n Введіть a, b, eps:");
  while (scanf("%d %d %fl", &a, &b, &e) && func(a) * func(b) >= 0) {
    printf("Incorrect a and b, please try again:");
  }
  printf("\n");
  //==============================================================================================================//
  StartTime = clock();
  if (Metod_Used == 1) {
    bisection(a, b);
    result = c;
    printf("\n method_bisection = %lf\n", result);
  }
  if (Metod_Used == 2) {
    result = method_chord(a, b, e);
    printf("\n method_chord = %f \n\n", result);
  }
  printf("\n Витрачений час на розрахунки = %f Sec\n\n", clock() - StartTime);
  //==============================================================================================================//
  return 0;
}

```



