# stm32_LED_counter
小程序；实现proteus中PA0-PA7引脚由PB0，PB1按钮控制二进制加减法
```C
#include "stm32f4xx.h"
void ChangeLED(unsigned counter);

int main()
{
	unsigned counter=0x0000;
	RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN | RCC_AHB1ENR_GPIOBEN;
	GPIOA->MODER |=0x00005555;
	while(1)
	{
		if (!(GPIOB->IDR & GPIO_IDR_ID0))
		{
			counter=counter+1;
			while((!(GPIOB->IDR & GPIO_IDR_ID0)));
			ChangeLED(counter);
		}
		else if (!(GPIOB->IDR & GPIO_IDR_ID1))
		{
			counter=counter-1;
			while((!(GPIOB->IDR & GPIO_IDR_ID1)));
			ChangeLED(counter);
		}		
	}
}

void ChangeLED(unsigned counter)
{
	GPIOA->ODR |= counter;
	GPIOA->ODR &= counter;
}

```

proteus:
---
![Uploading image.png…]()

