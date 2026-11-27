（2）Homwwork_2_1对应必做作业1
  1.Cube MX里面：
    PA0选EXTI0，双边沿触发，pull-up
    PA5选output
    选TIM2，PSC写7199，Counter Period写9，在NVIC开启TIM2中断
  2.Keil里面：
    全局变量：
      light是灯的模式，0是常灭，1是常亮，2是闪烁
      press是按下按钮的时间
      count是记录闪烁
    开启TIM2定时器
    用EXTI回调函数判断长按还是短按：
      先判断按的时间是否是20ms以上，消抖
      记录按下和松开的时间差
      如果时间差小于1000ms，是短按，light如果是1就变成0，如果是0就变成1，如果是2就变成0
      如果时间差大于1000ms，light如果是2就变成1，如果是0或者1就变成2
      最后将上次的时刻记作现在的时刻
    TIM2回调处理闪烁：
      light如果是0就写引脚RESET，count变0，如果是1就写引脚是SET，count变0
      light如果是2就count++,count到100就翻转PA5的电平，然后count变0
      
(1)Homework_2_2对应必做作业2
  我用一个按钮控制呼吸灯和舵机的转换
  1.CubeMX里面：
    PA0选EXTI0，下降沿，pull-up，NVIC Setting选EXTIline0 interrupt
    Timer选TIM3
    Clock Source选Internal Clock
    channel 1和channel 2分别选上PWM Generation CH1和CH2
    PSC写71
    ARR写19999
  2.Keil里面：
    全局变量：
      button，0是呼吸灯，1是舵机
    用HAL_TIM_PWM_START()分别开启两个PWM，channel 1对应PA6，Channel 2对应PA7
    按下PA0中断回调：
      消抖20ms
      button如果是1就变0，如果是0就变1
    button如果是0
      计数器先判断有没有按下按钮改变button的值，如果没有，i从0到19999,再从19999到0
      用__HAL_TIM_SET_COMPARE函数设置的值随i变化，让占空比从0%变到100%
      延时5ms,让呼吸周期变成2s
    button如果是1
      计数器先判断有没有按下按钮改变button的值，如果没有，spin从0到180.再从180到0
      CCR = 500 + (spin * 2000/180)，spin就是角度
      用__HAL_TIM_SET_COMPARE函数设置的值随CCR变化
      延时10ms

(3)Homework_2_3对应必做作业3
  其实培训PPT里面包含几乎全部步骤了
  1.Cube MX里面：
    PA0选ADC1_IN0，变成模拟输入，然后把Sampling Time写成55.5 Cycles
  2.KEIL:
    HAL_ADC_Start(),启动ADC转换
    HAL_ADC_PollForConversion(),轮询每次等待10ms
    ADC = HAL_ADC_GetValue()，读取转换结果给ADC
    HAL_ADC_Stop(),停下ADC
    把数字换算成电压Dian_ya
    延时100ms
    
    
    
  
    
      
      
      
    
    
    
    
