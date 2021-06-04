# Mobile-Controlled-RC-Car


![Aruino car](https://i.ytimg.com/vi/BbASlFelJSQ/maxresdefault.jpg)
  
### `Connections`

Motor Shield | Motors
------------ | -------------
 Motor Shield Pin 1 | Rightside Front Motor
 Motor Shield Pin 2 | Leftside Front Motor
 Motor Shield Pin 3 | Rightside Back Motor
 Motor Shield Pin 4 | Leftside Back Motor
 
 ### `Connecting Bluetooth module to Arduino Shield`
 
![Bluetooth](http://forbiddenbit.com/wp-content/uploads/2020/01/schema-1024x877-1.jpg)
 
 
 ### `Suggestion`
 
 * Change the `motor.setSpeed(255)` number to (Range : 0~255),for limit the speed of the car.
 * Switch on the bluetooth while connecting through app.

```C++

#include <AFMotor.h>


AF_DCMotor motor1(1, MOTOR12_1KHZ);    // Rightside Front Motor
AF_DCMotor motor2(2, MOTOR12_1KHZ);    // Leftside Front Motor
AF_DCMotor motor3(3, MOTOR34_1KHZ);    // Rightside Back Motor
AF_DCMotor motor4(4, MOTOR34_1KHZ);    // Leftside Back Motor

char command; 

void setup() 
{       
  Serial.begin(9600);  
}

void loop(){
  if(Serial.available() > 0){ 
    command = Serial.read(); 
    Stop(); 
    switch(command){
    case 'F':  
      forward();
      break;
    case 'B':  
       back();
      break;
    case 'L':  
      left();
      break;
    case 'R':
      right();
      break;
    }
  } 
}

void forward()
{
  motor1.setSpeed(255);
  motor1.run(FORWARD); 
  motor2.setSpeed(255); 
  motor2.run(FORWARD); 
  motor3.setSpeed(255);
  motor3.run(FORWARD); 
  motor4.setSpeed(255);
  motor4.run(FORWARD); 
}

void back()
{
  motor1.setSpeed(255); 
  motor1.run(BACKWARD); 
  motor2.setSpeed(255); 
  motor2.run(BACKWARD); 
  motor3.setSpeed(255); 
  motor3.run(BACKWARD); 
  motor4.setSpeed(255); 
  motor4.run(BACKWARD); 
}

void left()
{
  motor1.setSpeed(255); 
  motor1.run(BACKWARD); 
  motor2.setSpeed(255); 
  motor2.run(BACKWARD); 
  motor3.setSpeed(255); 
  motor3.run(FORWARD);  
  motor4.setSpeed(255); 
  motor4.run(FORWARD);  
}

void right()
{
  motor1.setSpeed(255); 
  motor1.run(FORWARD); 
  motor2.setSpeed(255); 
  motor2.run(FORWARD);
  motor3.setSpeed(255); 
  motor3.run(BACKWARD); 
  motor4.setSpeed(255);
  motor4.run(BACKWARD); 
} 

void Stop()
{
  motor1.setSpeed(0); 
  motor1.run(RELEASE);
  motor2.setSpeed(0);
  motor2.run(RELEASE); 
  motor3.setSpeed(0); 
  motor3.run(RELEASE); 
  motor4.setSpeed(0);
  motor4.run(RELEASE); 
}

```
