# Problem 115 - 古明地恋的指针

**ACMOJ Problem ID**: 2095

## Table of Contents

- [Problem 115 - 古明地恋的指针](#problem-115-古明地恋的指针)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
    - [Background](#background)
  - [Assignment Description](#assignment-description)
    - [Grade Composition](#grade-composition)
  - [Assignment Requirements](#assignment-requirements)
    - [Input Format](#input-format)
    - [Output Format](#output-format)
    - [Samples](#samples)
    - [Data Constraints](#data-constraints)
  - [Per-Testcase Resource Limits](#per-testcase-resource-limits)
  - [Test Data](#test-data)
  - [Submission Requirements](#submission-requirements)
    - [Submission Format](#submission-format)
    - [Submission Guidelines](#submission-guidelines)
    - [Evaluation Notes](#evaluation-notes)
    - [Academic Integrity](#academic-integrity)

## Introduction

### Background

This problem tests algorithmic problem-solving skills.

## Assignment Description

### Grade Composition

| Grading Component | Percentage |
| :--: | :--: |
| Pass **2095. 古明地恋的指针** | 80% |
| Code Review | 20% |

Here are several points that need clarification:

- In the Code Review, we will **strictly examine your code style and repository organization structure, etc.**

- This assignment provides some sample data for testing, stored in the `/workspace/data/115/data_test/` directory. Note that these are not the test cases on the Online Judge. Passing all local test cases does not guarantee that you will pass the OJ tests.

- Besides the provided sample data, we also encourage you to design your own test data based on your program logic to assist debugging.

## Assignment Requirements

### Problem Description

> 古明地恋一直处于无意识的状态，以至于她本人也不知道接下来她自己会做什么。

古明地恋具有操纵无意识的程度的能力，能够在无意识的情况下行动。然而，这也给她带来了不少的麻烦。

现在，她正在学习程序设计课程。然而，她总是会无意识地忘记归还申请的内存。为了防止她再次在机考的时候出现 memory leak，她决定实现一个智能的指针，其可以在析构的时候自动释放内存，这样她就再也不用担心内存泄漏了。同时，为了防止 double free，她要求一个指针只能被一个智能指针所占有。当然，智能指针的行为也应该与普通的指针几乎一致。

由于她一直处于无意识状态，现在又不知道跑到哪里去了。你能帮恋恋实现这个智能指针吗？模板如下:

```C++
#pragma once
#include <new>
#include <utility>
// 你不可以使用其他任何头文件

namespace sjtu {

/**
 * @brief 一个可以在离开作用域之后自动归还内存的指针。
 * unique_ptr <_Tp> 行为应该和普通指针 _Tp * 几乎一致。
 * @tparam _Tp 模板参数，指针指向的类型。
 */
template <typename _Tp>
class unique_ptr {
  private:
    // 你可以自由地增加成员变量和成员函数

  public:
    // 构造一个空的指针 (nullptr)
    unique_ptr();

    // 同一个指针不能被多个 unique_ptr 指向
    unique_ptr(const unique_ptr &) = delete;

    // 移动构造函数。移交所有权。
    // 注意移交后要把 other 置空。
    unique_ptr(unique_ptr &&other);

    // 析构函数。释放指针指向的内存。
    // 需要注意，delete nullptr 是安全的。
    ~unique_ptr();

    // 同一个指针不能被多个 unique_ptr 指向
    unique_ptr &operator=(const unique_ptr &) = delete;

    // 移动赋值运算符。移交所有权。
    // 注意移交后要把 other 置空。
    unique_ptr &operator=(unique_ptr &&other);

    // 接管一个普通 _Tp 类型的指针的所有权
    explicit unique_ptr(_Tp *);

    // 重置为空指针。同时释放指针指向的内存。
    void reset();

    // 转移所有权，返回指针指向的对象的地址
    // 同时，自己要置空。
    _Tp *release();

    // 返回指针指向的对象的地址
    // 所有权不转移。
    _Tp *get() const;

    // 重载 * 运算符(解引用)，返回指针指向的对象的引用
    _Tp &operator*();

    // 重载 -> 运算符(成员访问)，返回指针指向的对象的地址
    _Tp *operator->();
};

// 对于一个 unique_ptr，你最多只能存一个指针
static_assert(sizeof(unique_ptr<int>) <= sizeof(void *)) ;

// 创建一个 unique_ptr，指向一个用 new 分配的 _Tp 对象
template <typename _Tp>
unique_ptr <_Tp> make_unique(const _Tp &);

// Bonus: (不作为考察内容)
// (如果写了,请删除上面的这个 make_unique)
// (否则,请删除下面的这个 make_unique)
// 可变长参数列表 + 万能引用
// 创建一个 unique_ptr，指向一个用 new 分配的 _Tp 对象
// 参数列表长度可变，且有左值引用和右值引用两种版本
// 当传入左值 T &， Args 类型被推导为 T &
// 当传入右值 T &&，Args 类型被推导为 T
// 你需要了解如何用 std::forward 实现完美转发
template <typename _Tp, typename... Args>
unique_ptr <_Tp> make_unique(Args &&... args);

} // namespace sjtu

```

### Input Format



### Output Format



### Samples

No sample data provided for this problem.

### Data Constraints

## Resource Limits

- **Time Limit**: 2000 ms
- **Memory Limit**: 256 MiB

## Per-Testcase Resource Limits

- **Time Limit (per test case)**: 2000 ms
- **Memory Limit (per test case)**: 256 MiB
- **Disk Usage**: No disk usage is permitted.

## Test Data

The test data for this problem is located at `/workspace/data/115/data_test/`.

## Submission Requirements

### Submission Format

Submit a single C++ source file to the Online Judge. The OJ provides its own `main.cpp` which `#include "src.hpp"`. Your submission will be written to `src.hpp` and compiled together with the OJ's driver code.

### Submission Guidelines

- The submitted code must be able to compile successfully through the above compilation process
- The program needs to be able to read data from standard input and write results to standard output
- Please ensure the code runs correctly within the given time and space limits
- **You must use C++ or C language** to implement this assignment

### Evaluation Notes

- The evaluation system will test your program using the provided test data
- The program output must exactly match the expected output (including format)
- Exceeding time or memory limits will be judged as the corresponding error type
- Please pay attention to the overall time performance of your code and the time complexity of each part of your algorithm.

### Academic Integrity

If any violations are found during evaluation or code review (including but not limited to using unconventional methods to pass test cases), your final score may be significantly reduced or become **0 points**.
