---
title: ASCIS 2020-Crypt
slug: ASCIS
date: 2021-08-05 00:00:00+0000
image: cover.jpg
categories:
    - CTF
tags:
    - CTF
---

## Phân tích

Đây là một chall thực hiện hiện encrypt file,file thưc hiên encrypt với 2 tham số  là “file key” và không phải key tùy chọn mà là key mặc định. 

![Pictur 1](1.png)
 
Load vào IDA ta có flow của chương trình.
 
![Pictur 2](2.png)

Mình tìm kiếm chuỗi “wrong key” sau đó trace ngược lên tại hàm sub_55D62DCA75AE() debug thì biết nó thực hiện so sánh 2 chuỗi số nếu đúng thì bắt đầu encrypt file còn không thì hiện lên màn hình “wrong key” như hình bên trên. 

Tiếp tục mình trace theo [rbp+var_240] thì biết input+1483973472739663,sau đó thì tại sub_55D62DCA75AE() so sánh với 4634706992063332.

He he vậy key=3150733519323669
 
![Pictur 3](3.png)

![Pictur 4](4.png)

![Pictur 5](5.png)

 
Bài này tên crypto nên mình thử dùng plugin fincrypto thì biết thực hiện mã hóa file bằng thuật toán mã hóa AES_ECB

![Pictur 6](6.png) 

Mình đặt bp tại 0x56438FFF5BBB debug thì được key là P4nd`p<c8gE;T$F8

![Pictur 7](7.png)

![Pictur 8](8.png)
 
Vậy bài này mình đã đủ thông tin,để thực giải mã mình sẽ dùng libary của pycryptodome.

![Pictur 9](9.png)

Mình load file decrypt vào CFF thì biết đó là 1 file ảnh .png

## FLAG 

```ASCIS{C4yp1o_1s_5impl3_b4t_C++_i5_cr4z9}```
 

