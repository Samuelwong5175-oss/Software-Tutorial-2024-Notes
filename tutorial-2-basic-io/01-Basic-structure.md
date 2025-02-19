# Tutorial 2: IOs on Embedded Systems

[Back to Main](README.md)

<details>
<summary>Authors</summary>

Ivan Lok(yfilok@connect.ust.hk)
Modified from:
Dicaprio Cheung, Joseph Lam, Binay Gurung, Anshuman Medhi

</details>

> A important reminder for you guys before we begin:
> Please **DO NOT** put the mainboard on your computer or any metal surface.
> It can burn both your computer and also the pcb.

## Basic Structure in the `main.c`

After we have discussed some basic C programming, let us move forward to programming with STM32.

The `main.c` file for STM32 projects typically follows a structured format designed to facilitate embedded system programming. This structure is generated by STM32CubeMX and includes several key sections:

```c
int main(void) {

    /* USER CODE BEGIN 1 */
    /* USER CODE END 1 */

    /* MCU Configuration--------------------------------------------------------*/
    /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
    HAL_Init();
    /* USER CODE BEGIN Init */

    /* USER CODE END Init */

    /* Configure the system clock */
    SystemClock_Config();

    /* USER CODE BEGIN SysInit */

    /* USER CODE END SysInit */

    /* Initialize all configured peripherals */
    MX_GPIO_Init();

    //The System will call the _Init Function of all peripherals here

    /* USER CODE BEGIN 2 */
    /* USER CODE END 2 */

    /* Infinite loop */
    /* USER CODE BEGIN WHILE */
    while (1) {
        /* USER CODE END WHILE */
        /* USER CODE BEGIN 3 */
    }
    /* USER CODE END 3 */
}
```

- The most notable difference is that CubeMX has provided a `while` loop for you by default. This is because we want our code to be running continuously on the robot and wait for control signals (e.g. from a remote control) instead of just turning off after doing one action. (Imagine if your phone turned off immediately after calling someone)

  - An important thing to keep in mind is that a lot of your code should be continuously looping within the `while` loop. Even when the robot is doing nothing, it should be still looping and checking for new control commands repeatedly. (e.g. has a button been pressed?) Below is a simplified example for your reference:
      <details><summary>Modified Real Code</summary>

    ```c
    while (1)
    {
        CurrentTime = HAL_GetTick();
        SW1State = !gpio_read(SW1);
        SW2State = !gpio_read(SW2);
        ADC_Reading() //Function to read IR Sensor Value via ADC
        encoder_operation();
        if (!startstate && SW1State)
            startstate = 1;
        callibrationLoop(&lf);
        controlLoop(&lf);
        if (startstate){
                Speed_Control(lf.left_speed, lf.right_speed);
        }
    }
    ```

      </details>

  - But since the code is looping repeatedly, be aware of variables being overwritten or functions being called multiple times.

  > If you have played with Arduino before, the `while` loop acts like the `loop()`

- Another key difference is the placeholder for user code. To make sure our code works properly with the hardware, STM32CubeIDE helps generate a lot of code for us. The problem with this is that your own code can be unintentionally modified during the generation process.\
  To make sure your code won't be changed in any way, make sure to place your code between the specified areas:

        ```c
            /* USER CODE BEGIN Init */
            // place your code here
            /* USER CODE END Init */
            // code here may be changed by the IDE!
        ```

[Continue to The Next Page](./02-GPIO.md)
