# eigen

> [Eigen](http://eigen.tuxfamily.org) is a C++ template library for linear algebra: matrices, vectors, numerical solvers, and related algorithms.

## startup

```bash
# Ubuntu
sudo apt install libeigen3-dev
g++ -I /usr/include/eigen3 demo.cpp -o demo
```

```c++
// demo.cpp
#include <Eigen/Core>
#include <iostream>
using namespace std;
using namespace Eigen;

void printEigenVersion();
void printMatrix();

int main()
{
  cout << "Print Eigen Version:" << endl;
  printEigenVersion();

  cout << endl;

  cout << "Print Matrix:" << endl;
  printMatrix();
  return 0;
}

void printEigenVersion()
{
  cout << "Eigen version: " << EIGEN_MAJOR_VERSION << "." << EIGEN_MINOR_VERSION << endl;
}

void printMatrix()
{
  Matrix3f A = Matrix3f::Identity();
  cout << A << endl;
}
```

## Install

```bash
# ubuntu install
sudo apt install libeigen3-dev

# linux
git clone git@github.com:eigenteam/eigen-git-mirror.git
mv eigen-git-mirror /usr/include/eigen3
```

## 资源

1. [Eigen Tutorial](https://dritchie.github.io/csci2240/assignments/eigen_tutorial.pdf)