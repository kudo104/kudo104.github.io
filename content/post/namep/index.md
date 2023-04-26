---
title: Namep
slug: CTF
date: 2021-08-10 00:00:00+0000
image: cover.jpg
categories:
    - CTF
tags:
    - CTF
---

## Phân tích
Chạy file Namep.exe 

![Picture 1](1.png)

Load file  vào CFF explorer để biết được file có resource,mình thấy không có định đạng nên chắc đã bị encode.
 
![Picture 2](2.png)

Load file vào IDA.

Sau một lúc phân tích thì biết file này load resource sau đó decode resource và thực thi cái resource.

Việc decode thực hiện phép xor mặc định với 0x33 
 
 ![Picture 3](3.png)

 ![Picture 4](4.png)

 ![Picture 5](5.png)
 

Sau khi mình decode resource thì vẫn không biết đây là gì xin hint từ ông anh mới biết đây là một shellcode.
 
![Picture 6](6.png)

Mình run shellcode thì biết nó load 1 file gì đó dump ra và load vào IDA,thì tìm được block này hehe file cần tìm đây rồi.

![Picture 7](7.png)

![Picture 8](8.png)

![Picture 9](9.png)

Mình trace ngược lên trên thì biết flag có chuỗi con ASCI nếu không có thì in ra thông báo “Noob~” và ngược lại.

Tiếp tục trace lên trên thì flag được decode bằng mã hóa rc4,mình biết được chuỗi đầu ra nhưng không biết key bao nhiêu byte tiếp tục trace thì key được trả về tại hàm sub_100017A0().Sau một lúc phân tích thì key chỉ có 4 byte,vậy bài này mình đã đủ thông tin để brute.

 
![Picture 10](10.png)

 

Đây là code của mình.
 
![Picture 11](11.png) 

## FLAG 

```ASCIS{a_s1mpl3_pr0toco1}```



