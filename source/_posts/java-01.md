---
title: java编程中使用二进制进行权限或状态控制
date: 2018-01-04 22:49:50
tags: java
categories: java 
---

## 编程中使用二进制进行权限或状态控制

## 与或非运算符

- &是按位与(双目运算符,需要2个操作数) 
- |是按位或(双目运算符) 
- ～是按位非(单目运算符) 

### 例子

* 1&0=0, 0&1=0, 0&0=0, 1&1=1 
* 1|0=1, 0|1=1, 0|0=0, 1|1=1 
* ~1=0,~0=1 
* a|=b等价于a=a|b; 同理a&=b等价于a=a&b 

<!--more-->

### java例子 

```
package test;  
public class Rights {  
  
    public static void main(String[] args) {  
        int a=1; // 001 状态a  
        int b=2; // 010 状态b  
        int c=4; // 100 状态c  
          
        int ab = a | b; // 001 | 010 = 011 初始状态  
          
        System.out.println(ab | c); // 011 | 100 = 111 添加c的状态  
        System.out.println(ab & (~b)); // 011 & (~010) = 011 & 101 = 001 去除b的状态  
          
        System.out.println((ab & b) == b); // 011 & 010 = 010 判断是否有b的权限：(ab & b)==b  
        System.out.println((ab & c) == c); // 011 & 100 = 000   
    }  
}  

```

## 使用二进制进行权限或状态控制

```
package test;  
  
public class Test {  
public static void main(String[] args) {  
  
        /** 
         * 四种权限 ，当前定义为int，以下二进制表示只取后四位作说明 
         */  
  
        // 添加  
        int c = 1;// ...0001=2^0  
        // 查询  
        int r = 2;// ...0010=2^1  
        // 修改  
        int u = 4;// ...0100=2^3  
        // 删除  
        int d = 8;// ...1000=2^4  
  
        /** 
         *  
         * 大家可以观察四种权限的二进制表示的规律 ，都是2的N次方， 
         * 就表示本身，添加权限有最后一位为其它为0,查询倒数第二位为1其它都为0，修改倒数第三个为1其它都为0，删除倒数第四个为1其它都为0 
         *  
         */  
  
        /** 
         * 这样表示有哪种权限时可以用 |(按位或) 操作 
         *  
         */  
  
        // 用户A有添加和修改权限  
        int usera = c | r | u;  
  
        // 用户B有添加和删除权限  
        int userb = c | d;  
  
        /** 
         * 判断用户是否有某种权限用用户权限和要判断的权限进行 &(按位与) 操作，结果为要判断的权限值时表示用户有此权限，否则没有此权限 
         */  
        System.out.println();  
        if ((usera & u) == u) {  
            System.out.println("用户a有更新权限");  
        } else {  
            System.out.println("用户a没有有更新权限");  
        }  
  
        /** 
         * 给用户添加权限用用户权限和要添加的权限|(按位或) 操作再覆盖之前权限值 
         */  
        System.out.println();  
        if ((userb & u) == u) {  
            System.out.println("用户b有更新权限");  
        } else {  
            System.out.println("用户b没有更新权限");  
        }  
  
        System.out.println("==>给用户b添加更新权限");  
        userb = userb | u;  
  
        if ((userb & u) == u) {  
            System.out.println("用户b有更新权限");  
        } else {  
            System.out.println("用户b没有更新权限");  
        }  
  
        /** 
         * 取消用户某种权限,用用户权限和要取消的权限按位取反后进行按位 操作，再覆盖之前权限值 
         */  
        System.out.println();  
        if ((usera & r) == r) {  
            System.out.println("用户a有查询权限");  
        } else {  
            System.out.println("用户a没有查询权限");  
        }  
  
        System.out.println("==>取消用户a的查询权限");  
        usera = usera & (~r);  
  
        if ((usera & r) == r) {  
            System.out.println("用户a有查询权限");  
        } else {  
            System.out.println("用户a没有查询权限");  
        }  
    }  
  
}  
```

## 二进制和十进制之间的转换

```
package test;  
  
public class Trans {  
  
    public static void main(String[] args) {  
        int bit = 7;  
        System.out.println(Integer.toBinaryString(bit)); // 十进制转二进制  
  
        Integer it = Integer.valueOf("111", 2);  
        System.out.println(it);// 转换为10进制结果  
    }  
}  
```

