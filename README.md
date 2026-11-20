(1)LED_BLINK_1_1对应必做作业1
  1.STM32CubeMX里面：
    像培训那样设置
    将PA5引脚设置成output
  2.Keil里面：
    while(1){}实现死循环
    然后用HAL_GPIO_TogglePin实现这个引脚电平的反转，让它在循环里面1和0不断互换，让LED闪烁
    HAL_Delay实现延时
(2)LED_BLINK_1_2对应必做作业2
  1.STM32CubeMX里面：
    同上
    将timer选TIM2,clock source选internal clock,这样计时器就选好了
    把prescaler改成7199,counter period改成2499
    把nvic setting 选上TIM2
  2.Keil里面：
    开启TIM2:HAL_TIM_BASE_Start_IT(&htim2)
    填上HAL_TIM-PeriodElapseCallBack,指定TIM2,然后用位反转函数将PA5的电平反转
(3)LED_EXTI_1_3对应必做作业3
  1.STM32CubeMX里面： 
    把PA0引脚设置成extio,high,pull-up
    把PA5引脚设置成output
  2.Keil里面：
    按下按钮，电平变化，触发中断，把PA0引脚编号传进去，用uint16_t类型
    用static保留上一次按下的时刻，用uint32_t类型，然后在用HAL_Gettick()返回这一次按下去的时刻
    判断相差有没有大于20ms，如果有，反转PA5的电平
    把这次的时刻记录成上一个时刻，用来和下一次对比
    
