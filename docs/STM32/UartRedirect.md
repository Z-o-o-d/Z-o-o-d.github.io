 #不使能微库microlib重定义打印
 
头文件添加
```
  #include "stdio.h"
```

```
  typedef struct __FILE FILE;
  struct __FILE 
  { 
    int handle; 
  }; 
  FILE __stdout;           

  int fputc(int ch, FILE *f)
  {      
    while((USART1->SR&0X40)==0);          //这里使用的是串口1，如用其他串口请自行修改
      USART1->DR = (uint8_t) ch;      
      return ch;
  }
```