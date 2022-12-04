# 指针类型变量的定义与基本操作
## 指针的定义
```cpp
#include <iostream>
using namespace std;
int main() {
    int *p;
    int x = 10;
    p = &x;
    
    cout << x << endl;
    cout << p << endl;
    cout << &p << endl;
}
```

## 指针赋值操作
```cpp
#include <iostream>
using namespace std;
int main() {
    int x, *p, *p1;
    double y, *q;
    p = &x;
    q = &y; 
    // p = &y;  // 逐行去掉注释，看看会有什么错误
    // q = &x; 
    p1 = p;
    // p1 = q;
}
```

```cpp
#include <iostream>
using namespace std;
int main() {
    int x, *p, *p1;
    double y, *q;
    p = 0;
    // p = 120; // 去掉注释，看看会有什么错误
    p = (int *)120;

    void *any_pointer;
    any_pointer = &x;
    any_pointer = &y;
}
```

## 间接访问操作
```cpp
#include <iostream>
using namespace std;
int main() {
    int x;
    int *p;
    p = &x;
    x = 1;
    *p = 2;
}
```

# 动态变量
## 创建动态变量
```cpp
#include <iostream>
using namespace std;
int main() {
    int *p1, *p2;
    p1 = new int; 
    p2 = (int *) malloc(sizeof(int)); 
}
```

## 创建动态数组
```cpp
#include <iostream>
using namespace std;
int main() {
    int *p3, *p4;
    p3 = new int[n]; 
    p4 = (int *) malloc(sizeof(int)*n);
}
```

## 创建二维动态数组


# 指针作为函数形参
## 例: 交换两个指针变量值的函数
```cpp
void swap(int **x, int **y) { 
    int *t;
    t = *x;
    *x = *y;
    *y = t;
}

int main() {    
    int a = 0, b = 1;
    int *p = &a, *q = &b;
    cout << *p << ',' << *q << endl;  //p指向a，q指向b。输出：0,1
    swap(&p, &q);
    cout << *p << ',' << *q << endl;  //p指向b，q指向a。输出：1,0
    return 0;
}
```

# 通用指针 void *
```cpp
int main() {
    int a = 10;
    void *ptr = &a;
    cout << *ptr << endl;
    return 0;
}

```cpp
int main() {
    int a = 10;
    void *ptr = &a;
    cout << *(int *) ptr << endl;
    return 0;
}
```

# 函数指针
## 例: 编写一个程序，根据输入的要求执行在一个函数表中定义的某个函数
```cpp
#include<iostream>
#include<cmath>
using namespace std;
const int MAX_LEN = 3;
double (*func_list[MAX_LEN])(double) = {sin, cos, tan};
int main() {
    int index; double x;
    do {
        cout << "Which function? (0:sin 1:cos 2:tan):";
        cin >> index;
    } while (index < 0 || index > 2);
    cout << "x = ";
    cin >> x;
    cout << "y = " << (*func_list[index])(x) << endl;
    return 0;
}
```

# 程序的内存布局
尝试下面的代码，观察不同类型变量的区别
```cpp
int a = 1; // global (inited) 
int b;     // global (uninited) 
int f(void) { 
    int c = 0;        // automatic (local) 
    static int d = 0; // static (inited) 
    d++; 
    int *p = new int; // dynamic 
    delete p; 
} 
```
