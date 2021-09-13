---
layout:     post
title:      "C++ string split - C++"
subtitle:   " \"Format\""
date:       2021-09-13 17:47:00
author:     "Yongmin"
header-img: "img/gyul.jpg"
catalog: true
tags:
    - Format
    - C++
  
---

# 용도
입력이 예를 들어 “hello world”라고 주어졌을 때, hello와 wolrd를 따로 입력을 받고 싶을 때 사용하는 코드이다.

# 소스 코드

```c++
#include<iostream>
#include<string>
#include<vector>
#include<sstream>

using namespace std;

int main()
{
    string str="hello world";
    istringstream ss(str);
    string stringBuffer;
    vector<string> v;

    while (getline(ss, stringBuffer, ' ')){
        v.push_back(stringBuffer);
        cout<<stringBuffer<<" ";
    }
    
    return 0;
}
```
