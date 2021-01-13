This project interfaces HC-SR04 ultrasonic sensor along with the stm32f407 discovery board. 
User can either paste the code attached in the word document in any desired IDE and after giving connections (Vcc,GND, echo pin to PD9 and trigger pin to PD10) can download the code to board and can monitor the distance variable which would contain the distance obtained from the sensor. The following part is for users who want to know the configurations in STM32CubeMx.
The ultrasonic sensor  has to be connected with a 5v supply from the board and has to be grounded with the GND pin from the board too. It has 2 pins, echo and trigger. These pins has to be controlled in order to get the distance. According to the code, echo pin is connected to PD9 and trigger pin has been connected to PD10. 
Softwares used:
STM32CubeMx was used to configure the discovery board.
CubeMx configurations:
The clock speed of the microcontroller has been set to 84MHz, but it can be changed as per user requirement. 
Pin configurations in CubeMx:
PD9 (connected to echo pin) has to be configured as GPIO input and PD10 (connected to trigger pin) has to be configured as GPIO output.
PD12-PD15 are internally connected to LEDs. So, if the user wants to change the color of LED corresponding to change in distance, these 4 pins can be set as GPIO output.
Configuring Timer:
First, set the clock source to internal clock in CubeMX. Pre scale the timer clock to 1MHz (1MHz corresponds to 1 microsecond, so we can generate the required delay in microseconds). In the program, define a function to manage the timer. Configure the Auto reload value and monitor the SR bit to monitor the timer overflow.
Getting distance from the sensor:
According to the data sheet of the HC-SR04 sensor, the trigger pin has to be set high for 10 microseconds. To obtain delay in microseconds, timer has to be configured. After 10 microseconds, reset the trigger pin. Next, poll till the echo pin sets high, and read the pulse width of the echo pulse, as long as the echo pin is high. The distance can be calculated by distance=(echo width).(speed of sound)/2
