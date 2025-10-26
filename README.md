# CS-350
Emerging Systems Architectures &amp; Technologies

Summarize the project and what problem it was solving.

1. This project utilizes a raspberry Pi 4 and peripherals for a temperature/humidity sensor, LCD display, LEDs, input buttons and a serial input to construct a thermostat.

Using python’s gpiozero library, a state machine application was designed to meet the following requirements:

*	The default set point should be 72 degrees Fahrenheit.
*	Use the AHT20 temperature sensor to read the room temperature (via I2C).
•	Use the two LEDs (red and blue) to indicate whether the system is heating or cooling.
*	If the system is heating and the current temperature is below the set point, the red LED should fade in and out.
*	If the system is cooling and the current temperature is above the set point, the blue LED	should fade in and out.
* If the system is heating and the current temperature is at or above the set point, the red LED should be on and solid.
* If the system is cooling and the current temperature is at or below the set point, the blue LED should be on and solid.
* The three buttons in the circuit will be used to change the behavior of the overall system.
* The first button is used to toggle the state machine between off, heating, and cooling.
* The second button is used to raise the system's set point by one degree.
* The third button is used to lower the system's set point by one degree.
* The LCD in the circuit will be used to display the state of the thermostat to the user.
* The first line of the LCD should always be the date and current time of the system.
* The second line of the LCD should alternate between the current temperature and a line indicating which state the system is currently in and the temperature set point.
* The UART must be configured to output the state of the thermostat over the serial port.
* The output should be a single string that is updated every 30 seconds.
* The output string should be comma delimited.
* The fields of the output string should be the following:
  * State of the thermostat (off, heat, cool)
  * The current temperature
  * The temperature set point

2. What did you do particularly well?

Testing of this application was done using physical hardware connected to a headless raspberry Pi. To optimize development and testing, I configured Visual Studio Code to connect directly to the raspberry Pi, allowing for remote development and debugging of the application.

3. Where could you improve?

One improvement I wanted to make to the application was how a temperature change is displayed on the LCD screen. In the current state, the application switches between different views based on timing. An improvement would be to process the change and display it immediately upon change. Immediate feedback to the user would eliminate the chance of them continuing to press the temperature change button because they believed the button press didn’t register. I wasn’t sure if I could just call the screen.updateScreen method directly from a button press. 

4. What tools and/or resources are you adding to your support network?

I have a much better understanding of State Machines and how the cycle/ticks of a SM can impact the inputs and actions taken also the unnecessary compute power it can require.

5. What skills from this project will be particularly transferable to other projects and/or course work?

Having a better knowledge of state machines and the benefits it provides has already been helpful for some from-end applications I’ve recently designed for work. The specific application I designed was for collecting images from a remote server that drives a gige camera. The user captures and image and assigns a class, which will be used for machine learning purposes. By designing specific states of the application and associated code, it can be reused. In my example, I would have likely duplicated code to the set the screen to a wait state several times. Now it’s contained in a single method, making it much easier to maintain.

6. How did you make this project maintainable, readable, and adaptable?

For the management of the LEDs, I included logic for when the system is actively heating. If the system was actively cooling, the system would not attempt to turn the LED to pulse again. The was done to maintain repeatable behavior from the LED. The achieve this, a global variable was created to track the status of equip_state; which be either heating, cooling or off. For future development of this application, this variable state could be used to drive relays related to these functions.
