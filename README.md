
![DALL·E 2024-12-08 18 47 36 - A minimalistic and modern logo for a project titled 'Turn-on-off-the-LED-using-STM32'  The logo should feature an LED icon, glowing with a light effec](https://github.com/user-attachments/assets/e4be3929-dc67-4be9-8fac-c2c971c23e18)


# Project Title

Turn-on-off-the-LED-using-STM32

  
This project demonstrates a simple example of controlling an LED using an STM32 microcontroller. The LED can be turned on and off based on predefined logic or external inputs, showcasing basic GPIO configuration and control. It serves as an introductory project to learn about STM32 programming and embedded systems.


# 🛠 Skills
C/C++, electronics circuit design, PCB



# API Reference
Command: Turn LED ON (0x01)
Command: Turn LED OFF (0x00)


# Appendix
Circuit diagrams for connecting the LED to the STM32.
Datasheets for the STM32 or LED.
Timing diagrams, if applicable.


# Author
Alpai GOLAN 
Role: Developer and tester.
GitHub: https://github.com/AlpaiGolan

# Roadmap
-Adding a button to toggle the LED state.
-Extending the project to control multiple LEDs.
-Implementing communication protocols (e.g., Bluetooth or UART) for remote control.

# Run Locally
-Wiring the hardware.
-Flashing the code.
-Monitoring the LED response to user inputs or predefined logic.

# Screenshots
-The hardware setup (STM32 connected to the LED).
-Code snippets or outputs in the development environment.
-LED lit up during operation.



# Wiring the hardware components
Notice that the LED has two pins: one of the pins is longer. The longer pin is the positive end of the led and is called the anode. The other pin is called the cathode.

Connect one side of the resistor with the anode pin of the LED, and the other side of the resistor with the GND pin of the STM32 Nucleo board.

Connect the cathode pin of the LED with the A1 pin of the STM32 Nucleo board.


# Code 
<details>
<summary>main.c</summary>

```
#include "main.h"
void SystemClock_Config(void);

static void MX_GPIO_Init(void);

int main(void) {
  HAL_Init();

  SystemClock_Config();

  MX_GPIO_Init();

  while (1) {
    HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_1);
    HAL_Delay(1000);
  }
}

void SystemClock_Config(void) {
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};

  __HAL_RCC_PWR_CLK_ENABLE();
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);

  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSI;
  RCC_OscInitStruct.HSIState = RCC_HSI_ON;
  RCC_OscInitStruct.HSICalibrationValue = RCC_HSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK) {
    Error_Handler();
  }

  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK | RCC_CLOCKTYPE_SYSCLK |
                                RCC_CLOCKTYPE_PCLK1 | RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_HSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK) {
    Error_Handler();
  }
}
static void MX_GPIO_Init(void) {
  GPIO_InitTypeDef GPIO_InitStruct = {0};

  __HAL_RCC_GPIOA_CLK_ENABLE();

  HAL_GPIO_WritePin(GPIOA, GPIO_PIN_1, GPIO_PIN_RESET);

  GPIO_InitStruct.Pin = GPIO_PIN_1;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_HIGH;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
}

void Error_Handler(void) {
  __disable_irq();
  while (1) {
  }
}
```



</details>


![Screenshot 2024-12-08 183811](https://github.com/user-attachments/assets/8303c932-14b3-4206-a4ca-b66a42b3b2c5)

![WhatsApp Image 2024-12-08 at 6 27 32 PM](https://github.com/user-attachments/assets/5b9a6998-3666-4c9a-9997-b6ef6b89ae84)







