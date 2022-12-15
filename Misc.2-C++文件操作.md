# 1. 概述
* 文件是数据的集合，通常存储在磁盘上，便于以后使用；
* 几乎所有的程序都用文件存储信息，如：数据库管理系统、操作系统、编译器等；
* 所有文件都有名字。
* 使用文件的过程
  - 必须打开文件 
  - 对文件进行读或者写操作
  - 文件操作结束时关闭文件

## 1.1 文件流类型
在对文件进行读写之前，必须正确设置。
```cpp
#include <fstream>
// std::ofstream  输出文件流
// std::ifstream  输入文件流
// std::fstream   文件流
```

# 2. 打开文件
在对文件进行读或写操作之前必须先打开文件 
```cpp
#include <fstream>
using namespace std;
int main() {
    ifstream input_file;
    input_file.open("d:\\test.csv");
    return 0;
}
```

```cpp
#include <fstream>
using namespace std;
int main() {
    ifstream input_file;
    char filename[20];
    
    cin >>  filename;
    input_file.open(filename);
    return 0;
}
```

需要注意的是，```ifstream```只能用于从文件中读取数据；```ofstream```只能用于向文件写数据。

## 2.1 打开文件的方式
使用```fstream```类型的对象时，第二个参数用于表明文件的打开方式。可选的方式有
|参数|含义|数值|
|:----:|:----:|:----:|
|```ios::app```|追加模式|1|
|```ios::ate```|如果已存在，直接转到文件尾部|2|
|```ios::binary```|二进制方式|4|
|```ios::in```|从文件中读数据|8|
|```ios::out```|向文件中写数据|16|
|```ios::trunc```|若文件存在，删除其内容|32|

```cpp
#include <fstream>
using namespace std;
int main() {
    fstream input_file;
    input_file.open("d:\\test.csv", ios::out);
    return 0;
}
```

## 2.2 测试文件是否打开成功
```cpp
#include <fstream>
using namespace std;
int main() {
    ifstream data_file;
    data_file.open("cust.dat", ios::in);
    if (!data_file) {  
        cout << "Fail to open the file." << endl;
        exit(0);
    }
    return 0;
}
```

## 2.3 关闭文件
当程序不再使用文件时，应关闭文件：
* 文件缓冲区是一块小的内存空间
* 操作系统限制同时打开的文件数量 

利用`close()`方法来关闭文件。

```cpp
#include <fstream>
using namespace std;
int main() {
    ifstream data_file;
    data_file.open("cust.dat", ios::in);
    if (!data_file) {  
        cout << "Fail to open the file." << endl;
        exit(0);
    }
    data_file.close(); 
    return 0;
}
```

# 3. 文件操作
## 3.1 写文件
使用 `<<` 操作向一个文件写入信息

```cpp
int main() {
    fstream data_file  ;
    data_file.open("bands.txt", ios::out);
    if (!data_file) {    
        cout << "Error opening file.\n";
        exit(0);
    }

    data_file << "Linkin Park\n";
    data_file.close( );                  
    
    data_file.open("bands.txt", ios::out|ios::app);    
    data_file << "Coldplay\n";
    data_file.close();              
    
    return 0;
}
```

### 格式化输出到文件
```cpp
int main() {  
    fstream out_file("numbers.txt", ios::out);
    int nums[3][3] = {1234, 3, 567, 34, 8, 6789, 124, 2345, 89};
    
    for( int  row = 0 ; row < 3 ; row++ ) {       
        for( int  col = 0 ; col < 3 ; col++ ) {
            out_file << setw(10) << nums[row][col] <<"  " ;
        }
        out_file << endl ;
    }
    
    out_file.close( );
    return 0;
}
```

## 3.2 读文件
使用 `>>` 从文件读数据

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>
using namespace std;

int main() {
    fstream data_file;
    char band_name[81];
    data_file.open("bands.txt", ios::in);
    if (!data_file) {
        cout << "File open error!" << endl;
        exit(0);
    }
    
    for(int count = 0; count < 2; count++) {
        data_file >> band_name;
        cout << band_name << endl;
    }
    data_file.close( );            
    return 0;
}
```

### 检测文件结束
`eof()` （end of file）函数报告文件结尾，意味着文件指针已经超出了最后一个数据的范围，无数据可读。


# 文件流做参数
**文件流对象可以传递给函数, 但是必须通过引用的方式传递**
```cpp
bool openFileIn(fstream &, char[]);
void showContents(fstream &);
void main() {   
    fstream data_file;
    if (!openFileIn(data_file, "bands.txt")) {
        cout << "File open error!" << endl;
        exit(0);
    }
    showContents(data_file);
    data_file.close( );
}

bool openFileIn(fstream &file, char name[]){
    file.open(name, ios::in);
    return file.fail() ? false : true;
}

void showContents(fstream &file) {
    char name [81];
    while(!file.eof()) {
        file >> name;
        if(file.fail()) break;
        cout << name << " " ;
    } 
}


```
