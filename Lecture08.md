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



