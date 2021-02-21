* [宏的使用](#宏的使用)
* [static的使用](#static的使用)



## 宏的使用
### 一、利用宏写单元测试
1、do{} while(0) 的使用

2、宏展开时，如果有打印log，可以通过__FILE__和__LINE__定位到具体位置

3、format的使用，%.17g

* %f：十进制浮点数（单、双精度
* %e：科学记数法（尾数/指数）。保留小数点后六位。
* %g：至多6位有效数字，去除多余的0

```c++
#define EXPECT_EQ_BASE(equality, expect, actual, format) \
    do {\
        test_count++;\
        if (equality)\
            test_pass++;\
        else {\
            fprintf(stderr, "%s:%d: expect: " format " actual: " format "\n", __FILE__, __LINE__, expect, actual);\
            main_ret = 1;\
        }\
    } while(0)
 
#define EXPECT_EQ_INT(expect, actual) EXPECT_EQ_BASE((expect) == (actual), expect, actual, "%d")
#define EXPECT_EQ_DOUBLE(expect, actual) EXPECT_EQ_BASE((expect) == (actual), expect, actual, "%.17g")
```
