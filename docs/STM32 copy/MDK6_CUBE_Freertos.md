# CubeMX使用Freertos初始化MDK6代码



![alt text](image-4.png)


打开以下目录
```
C:\Users\Admin\STM32Cube\Repository\STM32Cube_FW_F1_V1.8.6\Middlewares\Third_Party\FreeRTOS\Source\portable
```
![alt text](image-5.png)

将RVDS内所有文件复制，替换GCC所有文件。
等效命令
```
PS C:\Users\Admin\STM32Cube\Repository\STM32Cube_FW_F1_V1.8.6\Middlewares\Third_Party\FreeRTOS\Source\portable> rm -r .\GCC\
PS C:\Users\Admin\STM32Cube\Repository\STM32Cube_FW_F1_V1.8.6\Middlewares\Third_Party\FreeRTOS\Source\portable> cp -r .\RVDS\ .\GCC\
```

再次生成代码即可

参考链接：https://blog.csdn.net/tytyvyibijk/article/details/125589038