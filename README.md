# AUTOMATIC-LED-CONTROL-USING-IR-SENSOR
##  AIM
To design and implement a system using the *STM32 microcontroller* where an LED automatically turns ON or OFF based on the input from an *IR sensor*.

---

##  Components Required
- STM32 Nucleo or Discovery Board (e.g., *Nucleo-G071RB*)
- IR Sensor Module
- LED (5mm Green or any color)
- Jumper wires
- Breadboard

---

##  Theory
An *IR sensor* detects the presence of an object by emitting and receiving infrared light.

### IR Sensor Behavior
- When an *object is detected, the IR sensor output goes **LOW (0V)*.
- When *no object is detected, the output stays **HIGH (3.3V)*.

### Microcontroller Response
- If *IR output = LOW* → *LED ON*
- If *IR output = HIGH* → *LED OFF*
### *Procedure*

1. Open *STM32CubeIDE*.
  <img width="1920" height="1149" alt="Screenshot 2025-11-06 131201" src="https://github.com/user-attachments/assets/05248ca6-9b1a-4728-93f5-4c2b603eb4b4" />

2. Click *File → New STM32 Project*.
   <img width="940" height="555" alt="image" src="https://github.com/user-attachments/assets/de7a7760-2692-4cac-a780-1087e5d6df2d" />

3. Select the *target microcontroller* or board and click *Next*.
  <img width="940" height="558" alt="image" src="https://github.com/user-attachments/assets/6e1731c2-18ab-4de7-8688-5ca8406f7d2a" />


4. Name the project.
  <img width="940" height="915" alt="image" src="https://github.com/user-attachments/assets/4f8e94a0-6705-4d0d-81dc-1fbf5423e924" />

5. The corresponding .ioc file will be generated automatically.
  <img width="940" height="553" alt="image" src="https://github.com/user-attachments/assets/7b998bd6-b6ba-4319-92a6-d03bb01f1eaf" />

6. Configure the pins as *GPIO (Input/Output), **USART*, etc. as needed.
   <img width="940" height="553" alt="image" src="https://github.com/user-attachments/assets/44dfe329-4d47-4f4c-8531-996cddff9baa" />


7. Save the configuration (Ctrl + S) – the base C program will be generated automatically.
  <img width="940" height="558" alt="image" src="https://github.com/user-attachments/assets/8cb090e8-fe2b-4515-8ebf-a3463a9e5e73" />

 
8. Edit the generated main program as required.
   <img width="940" height="556" alt="image" src="https://github.com/user-attachments/assets/f347bb52-f64e-4a99-8f7d-9ca0b0b4cfd7" />

9. Click *Project → Build All*.
   <img width="940" height="555" alt="image" src="https://github.com/user-attachments/assets/e5290cfd-6e43-4146-8275-c484745383b9" />

10. Link the *HEX file* using the post-build process.
    <img width="940" height="426" alt="image" src="https://github.com/user-attachments/assets/56bab4ed-0b81-4b4b-a64c-57067baf3d28" />

11. Click *Debug* and connect the *STM Nucleo Board*.
   <img width="940" height="557" alt="image" src="https://github.com/user-attachments/assets/90e9d738-e338-430d-8dbf-f6983f6a5036" />

13. Click *Run* to execute the program.
    
---

### 💻 *Program*


c
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
    HAL_Init();
    SystemClock_Config();
    MX_GPIO_Init();

    while (1)
    {
        GPIO_PinState ir = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_10); // IR OUT at PA10 (D2)

	      if (ir == GPIO_PIN_RESET)  // IR sensor HIGH = object detected
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_SET); // Turn ON LED
	      }
	      else
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_RESET); // Turn OFF LED
	      }

	      HAL_Delay(100);
    }
}

---
### OUTPUT
CASE 1: LED ON 
	![WhatsApp Image 2025-11-05 at 19 24 37_8bf0d766](https://github.com/user-attachments/assets/3c686f91-6327-42a2-9a66-7d355078d963)
CASE 2: LED OFF
	![WhatsApp Image 2025-11-05 at 19 24 50_b76f736e](https://github.com/user-attachments/assets/19de543b-4d9e-43f0-80bd-da715bb5c4a3)
---
### RESULT

The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.
