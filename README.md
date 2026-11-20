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
    把prescaler改成7199,counter period改成2499，因为数从0开始数
    把nvic setting 选上TIM2
  2.Keil里面：
    开启TIM2:HAL_TIM_BASE_Start_IT(&htim2)
    填上HAL_TIM-PeriodElapseCallBack,指定TIM2,然后用位反转函数将PA5的电平反转
    
    
