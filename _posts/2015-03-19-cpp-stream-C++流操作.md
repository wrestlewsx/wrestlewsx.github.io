---
layout: post
title: C++流操作
category: 技术
tags: C++
description: 详细记录C++中难以理解的流操作以及错误解决
---
#  C++流的使用
## 每次使用完流,记得要关闭,虽然有时候并不是必须的.
`streamname.close();`
## 重定向
   在Linux终端或者Windows命令提示符模式下,使用重定向可以改变输入源和输出源 </br>
   <pre><code> 
   ~$ program '<'input.filetype >output.filetype #去掉多余的'' 
   </code></pre>
   <br> 在Linux和Unix下,'>' '<'默认是标准输出和标准输入,'2>'则是标准错误(即std::cerr)
## 输出流
   <br>1. ostream类提供了 put() 和 write() 方法用来输出 </br>

      cout.put('W'); //输出字符Ｗ,可以拼接使用就像重载之后的 '<<'
      cout.write("Candy Bob",5); //输出第一个参数的第二个参数个长度
   <br>2. 刷新输出缓冲区可以有两种方法,原理都是重载 '<<' </br>
   <br>   前者与后者的差别就在与后者刷新缓冲区后多了一个换行操作 </br>

      cout << "Show Now!" << flush; //相当于flush(cout);
      cout << "Show Now!" << endl;  
   <br>3. 可以通过流操作修改现实的进制, 默认十进制,十六进制,八进制 </br>

      int n = 100;
      cout << n << endl;
      //八进制
      cout << oct << n << endl;
      //十六进制
      cout << hex << n << endl;
      //这种作用是持久的,在不用的时候记得转换回来
      dec(cout); //代表转换为十进制 cout << dec;同样适用  

   <br>4. 我们可以调整字段宽度来达到美观,但Ｃ++有一种数据完整大于美观的理念,所以即使你设置了字段宽度,一旦超过还是会
        打乱阵型,以保证数据的完整性.
   </br>

      cout.fill('*');//使用'*'填充空白,注意此为持久的.
      for(int i = 0;i < 100;i*=10)
      {
        cout.width(5);
        cout << i << ":";
        cout.width(8);
        cout << i * i << endl;
      }//注意，width()方法并不是持久的,也就是说每次排版都需要使用一次该方法.
   <br>5. 浮点数的使用 </br>

      cout.precision(2);//设置浮点数的精度为2,Ｃ++默认六位精度,但不显示末尾的0.
      cout.setf(ios_base::showpoint);//显示末尾的零
## 输入流
   <br> cin检查输入: 当读取到的流和指定的类型不符合的时候,不符合的流中的数据被保留,留待下一次读取.并返回flase
       可以使用while语句进行判断 </br>

      int input, sum;
      while(cin >> input)
      sum += input;
   <br> 当流由于输入不匹配失败时,发生的问题十分复杂,简述为位设置问题,使用下列代码恢复 </br>

      while(cin >> input)
         sum += input;
      if(cin.fail() && !cin.eof())
      {
         cin.clear();              //重置流状态,但此时还是有残余留在流中
         while(!isspace(cin.get()))//丢弃那些残留在流中妨碍下一次输入的不符合的输入
               continue;           //头文件 cctype
      }
      cin >> input; //现在可以继续输入了
   <br> 字符串的输入:`get(char*, int)` 和 `getline(char*, int)` </br>
   <br> get读取少于第二个参数减1个或遇见换行符,并将换行符留在流中,getline则将换行符抽取并丢弃</br>
   <br> `get(char*, int, char)` 和 `getline(char*, int, char)` </br>
   <br> 第三个参数则是分界符,读取到分界符号时停止读取. </br>
