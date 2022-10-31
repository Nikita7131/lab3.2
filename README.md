# lab_3.2 Мартиненко Ре-22

![alt tag](https://github.com/Nikita7131/lab3.2/blob/main/%D0%B1%D0%BB%D0%BE%D0%BA%20%D1%81%D1%85%D0%B5%D0%BC%D0%B0.png?raw=true"Описание небудет)")​

```ruby
#include <Windows.h>
#include <stdio.h>
#include <stdlib.h>



//==================================================================================================================//
double func(double x) {
  return x * x * x - x * x + 2;
}
//==================================================================================================================//
double bisection(double a, double b, double EPSILON, unsigned int Debug_param, unsigned int Debug_values) {
  double c = a;
  unsigned int CntValuesPrined;
  while ((b - a) >= EPSILON) {
    c = (a + b) / 2;
    if (func(c) == 0.0) {
      break;
    }
    else if (func(c) * func(a) < 0) {
      b = c;
    }
    else {
      a = c;
    }
    switch (Debug_param) {
      case 1:
        printf("root  = %lf\n", c);
        break;
      case 2:
        printf("root  = %lf\n", c);
        CntValuesPrined ++;
        if (CntValuesPrined >= Debug_values) {
          CntValuesPrined = 0;
          switch (WhatTooDoo()) {
            case 1:
              Debug_param = 1;
              break;
            case 2:
              Debug_param = 0;
              break;
          }
        }
        break;
    }
  }
  return c;
}
//==================================================================================================================//
double method_chord(int x_prev, int x_curr, double e, unsigned int Debug_param, unsigned int Debug_values) {
  double x_next = 0;
  double tmp;
  unsigned int CntValuesPrined;
  do {
    tmp = x_next;
    x_next = x_curr - func(x_curr) * (x_prev - x_curr) / (func(x_prev) - func(x_curr));
    x_prev = x_curr;
    x_curr = tmp;
    switch (Debug_param) {
      case 1:
        printf("root  = %lf\n", abs(x_next - x_curr));
        break;
      case 2:
        printf("root  = %lf\n", abs(x_next - x_curr));
        CntValuesPrined ++;
        if (CntValuesPrined >= Debug_values) {
          CntValuesPrined = 0;
          switch (WhatTooDoo()) {
            case 1:
              Debug_param = 1;
              break;
            case 2:
              Debug_param = 0;
              break;
          }
        }
        break;
    }
  } while (abs(x_next - x_curr) > e);
  return x_next;
}
//==================================================================================================================//
int WhatTooDoo() {

  printf("\n первищено кількість ітерацій з видачею інформації для прийняття рішення, що робити далі :");
  printf("\n 0) продовжити з такою ж кількістю ітерацій;");
  printf("\n 1) виконати програма до кінця, поки не будуть знайдено корені рівняння; ");
  printf("\n 2) вийти із програми, перед виходом вивівши на екран отриманий проміжний результат підрахунку;");
  printf("\n ВАША ВІДПОВІДЬ: ");

  int WhatDo;

  scanf("\n %d", &WhatDo);

  printf("\n");

  return WhatDo;
}
//==================================================================================================================//
int main() {

  double StartTime;
  int Metod_Used;
  int a_input;
  int b_input;
  double eps_input;
  unsigned int Debug;
  unsigned int ValuesPrined;

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
  while (scanf("%d %d %fl", &a_input, &b_input, &eps_input) && func(a_input) * func(b_input) >= 0) {
    printf("Incorrect a and b, please try again:");
  }
  printf("\n");
  //==================================================================================================================//
  StartTime = clock();

  if (Metod_Used == 1) {
    printf("\n method_bisection = %lf\n", bisection(a_input, b_input, eps_input, Debug, ValuesPrined));
  } else {
    printf("\n method_chord = %f \n\n", method_chord(a_input, b_input, eps_input, Debug, ValuesPrined));
  }

  printf("\n Витрачений час на розрахунки = %f Sec\n\n", clock() - StartTime);
  //==================================================================================================================//
  return 0;
}


```



