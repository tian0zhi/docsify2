# **STM 32入门**

## **1.&nbsp;&nbsp;点亮一颗LED灯**

基本步骤

- 使能所需外设
- 配置外设的工作模式
- 使用外设

<p align="center">
        <img src="../Embedded/pic_stm32/pic5.png" width="60%"/>
        <br>
       LED 链接端口
</p>

<p align="center">
        <img src="../Embedded/pic_stm32/pic6.png" width="60%"/>
        <br>
       LED 链接GPIO——PF9,GPIOF的第九位
</p>


```clike
#define RCC_AHB1ENR (*(volatile unsigned int *)(0x40023800 + 0x30))
#define GPIOF_MODER (*(volatile unsigned int *)(0x40021400 + 0x00))
#define GPIOF_ODR   (*(volatile unsigned int *)(0x40021400 + 0x14))

int main()
{
    //使能PF模块的时钟，这里的RCC是指复位、时钟、控制
    RCC_AHB1ENR |= 1<<5;//使能GPIO_F端口，如下图所示它在寄存器第5位。
    // 设置PF9的功能为输出，工作模式配置
    GPIOF_MODER &= ~(3<<(2*9));//3为11，左移18位并取反‘与’，对相应位置置零。
    GPIOF_MODER |= 1<<(2*9);//1为01，左移18位并 ‘或’，对相应位置置1，工作模式设为输出。
    //设置PF9输出低电平，点亮LED灯
    GPIOF_ODR &= ~(1<<9);

    while(1);
    return 0;
}
```
<p align="center">
        <img src="../Embedded/pic_stm32/pic2.png" width="60%"/>
        <br>
        在GPIO_F所在总线寄存器上使能GPIO_F
</p>

<p align="center">
        <img src="../Embedded/pic_stm32/pic3.png" width="60%"/>
        <br>
       配置GPIO_F工作模式
</p>

<p align="center">
        <img src="../Embedded/pic_stm32/pic1.png" width="60%"/>
        <br>
       配置GPIO_F输出
</p>

<p align="center">
        <img src="../Embedded/pic_stm32/pic4.png" width="60%"/>
        <br>
       寄存器起始位置映射
</p>


## **2.寄存器配置中的位运算**