# C/C++

## 指针、引用

```c++
#include <iostream>

int main(void) {
  int var, *pointer, &ref_var = var;

  pointer = &var;
  *pointer = 11;
  ref_var = 111;

  std::cout << "var value: " << var << std::endl;
  std::cout << "var address: " << &var << std::endl;

  std::cout << "pointer value: " << *pointer << std::endl;
  std::cout << "pointer address: " << pointer << std::endl;

  std::cout << "ref_var value: " << ref_var << std::endl;
  std::cout << "ref_var address: " << &ref_var << std::endl;

  return 0;
}
```

* [c++中，引用和指针的区别是什么？](https://www.zhihu.com/question/37608201/answer/72766337)