# Project Name/Title Goes Here
This will serve as a brief description of your project. Limit this to three sentences because it can become overly long at that point. This copy should draw the user in and make she/him want to read more.









<video src="2020-12-07 05-39-57.mov" controls="controls">
</video>




















  
# Bill Of Materials

| Item | Qty | Price | Where to Buy |
| ------------- | ------------- | ------------- | ------------- |
| Adeept Robotic Arm Kit  | 1  | $64.99  | https://www.amazon.com/dp/B087R8DLG6 |
| Breadboard  | 1 |  $6.75  | https://www.amazon.com/BB400-Solderless-Plug-BreadBoard-tie-points/dp/B0040Z1ERO |
| Potentiometer  | 1 | $1.85  |  https://www.tubesandmore.com/products/potentiometer-alpha-linear-38-bushing  |
| Micro Servo | 1 | $5.95 | https://www.adafruit.com/product/169  |
| Jumper Wires  | 6 | 10¢/wire  |  https://www.amazon.com/Breadboard-Jumper-Wire-75pcs-pack/dp/B0040DEI9M |
| Arduino Uno Board  | 1  | $27.60  | https://store-usa.arduino.cc/products/arduino-uno-rev3?selectedStore=us  |
| Arduino IDE  | 1  | $0  | https://www.arduino.cc/en/software/ |


/*************************************************************************************
*  Robot Control with Android App and NodeMCU
*
*  Differential Robot using H-Bridget L293D
*   
*  Voice activation and response
*
*  Developed by Marcelo Rovai on 31March17
*  Visit my blog: https://MJRoBot.org 
*   
************************************************************************************/
#include <WiFi.h>
WiFiClient client;
WiFiServer server(80);
const char* ssid = "FBI Prius";
const char* password = "G4ffyF00d789!";
String  command =""; // Command received from Android device

// Set Motor Control Pins
int eneLeftMotor = 12;  // D6 - enable Mortor Left
int leftMotor1 = 14;    // D4 - left Motor +
int leftMotor2 = 27;    // D3 - left Motor - 
int rightMotor1 = 26;    // D8 - right Motor +
int rightMotor2 = 25;    // D7 - right Motor -
int eneRightMotor = 33; // D5 - enable Mortor Right

void setup()
{
Serial.begin(115200);

pinMode(eneLeftMotor, OUTPUT); 
pinMode(eneRightMotor, OUTPUT); 
pinMode(leftMotor1, OUTPUT); 
pinMode(leftMotor2, OUTPUT);  
pinMode(rightMotor1, OUTPUT);  
pinMode(rightMotor2, OUTPUT);  

digitalWrite(eneLeftMotor,LOW);
digitalWrite(eneRightMotor,LOW);
digitalWrite(leftMotor1,LOW);
digitalWrite(leftMotor2,LOW);
digitalWrite(rightMotor1,LOW);
digitalWrite(rightMotor2,LOW);

connectWiFi();
server.begin();
}

void loop()
{
  client = server.available();
  if (!client) return; 
  command = checkClient ();

  if (command == "forward" || command == "frente" || command == "a frente")  forwardMotor();
  else if (command == "reverse" || command == "reverso"|| command == "voltar") reverseMotor();
  else if (command == "left"    || command == "esquerda") leftMotor();    
  else if (command == "right"   || command == "direita") rightMotor();     
  else if (command == "stop"    || command == "pare" || command == "parar" || command == "parando")     stopMotor();     

  sendBackEcho(command); // send command echo back to android device
  command = "";   
} 

/* command motor forward */
void forwardMotor(void)   
{
Serial.println("FORWARD");
digitalWrite(eneLeftMotor,HIGH);
digitalWrite(eneRightMotor,HIGH);

digitalWrite(leftMotor1,HIGH);
digitalWrite(leftMotor2,LOW);
digitalWrite(rightMotor1,HIGH);
digitalWrite(rightMotor2,LOW);
}

/* command motor backward */
void reverseMotor(void)   
{
Serial.println("REVERSE");
digitalWrite(eneLeftMotor,HIGH);
digitalWrite(eneRightMotor,HIGH);

digitalWrite(leftMotor1,LOW);
digitalWrite(leftMotor2,HIGH);
digitalWrite(rightMotor1,LOW);
digitalWrite(rightMotor2,HIGH);
}

/* command motor turn left */
void leftMotor(void)   
{
Serial.println("LEFT");
digitalWrite(eneLeftMotor,HIGH);
digitalWrite(eneRightMotor,HIGH); 

digitalWrite(leftMotor1,LOW);
digitalWrite(leftMotor2,HIGH);
digitalWrite(rightMotor1,HIGH);
digitalWrite(rightMotor2,LOW);
}

/* command motor turn right */
void rightMotor(void)   
{
Serial.println("RIGHT");
digitalWrite(eneLeftMotor,HIGH);
digitalWrite(eneRightMotor,HIGH);

digitalWrite(leftMotor1,HIGH);
digitalWrite(leftMotor2,LOW);
digitalWrite(rightMotor1,LOW);
digitalWrite(rightMotor2,HIGH);
}

/* command motor stop */
void stopMotor(void)   
{
digitalWrite(eneLeftMotor,LOW);
digitalWrite(eneRightMotor,LOW);

digitalWrite(leftMotor1,LOW);
digitalWrite(leftMotor2,LOW);
digitalWrite(rightMotor1,LOW);
digitalWrite(rightMotor2,LOW);
}

/* connecting WiFi */
void connectWiFi()
{
Serial.println("Connecting to WIFI");
WiFi.begin(ssid, password);
while ((!(WiFi.status() == WL_CONNECTED)))
{
  delay(300);
  Serial.print("..");
}
Serial.println("");
Serial.println("WiFi connected");
Serial.println("NodeMCU Local IP is : ");
Serial.print((WiFi.localIP()));
}

/* check command received from Android Device */
String checkClient (void)
{
while(!client.available()) delay(1); 
String request = client.readStringUntil('\r');
request.remove(0, 5);
request.remove(request.length()-9,9);
return request;
}

/* send command echo back to android device */
void sendBackEcho(String echo)
{
client.println("HTTP/1.1 200 OK");
client.println("Content-Type: text/html");
client.println("");
client.println("<!DOCTYPE HTML>");
client.println("<html>");
client.println(echo);
client.println("</html>");
client.stop();
delay(1);
}
'''
  
# Final Milestone
My final milestone is the increased reliability and accuracy of my robot. I ameliorated the sagging and fixed the reliability of the finger. As discussed in my second milestone, the arm sags because of weight. I put in a block of wood at the base to hold up the upper arm; this has reverberating positive effects throughout the arm. I also realized that the forearm was getting disconnected from the elbow servo’s horn because of the weight stress on the joint. Now, I make sure to constantly tighten the screws at that joint. 

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612573869/video_to_markdown/images/youtube--F7M7imOVGug-c05b58ac6eb4c4700831b2b3070cd403.jpg )](https://www.youtube.com/watch?v=F7M7imOVGug&feature=emb_logo "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
My final milestone is the increased reliability and accuracy of my robot. I ameliorated the sagging and fixed the reliability of the finger. As discussed in my second milestone, the arm sags because of weight. I put in a block of wood at the base to hold up the upper arm; this has reverberating positive effects throughout the arm. I also realized that the forearm was getting disconnected from the elbow servo’s horn because of the weight stress on the joint. Now, I make sure to constantly tighten the screws at that joint.

[![Third Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612574014/video_to_markdown/images/youtube--y3VAmNlER5Y-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=y3VAmNlER5Y&feature=emb_logo "Second Milestone"){:target="_blank" rel="noopener"}
# First Milestone
  

My first milestone was setting up and hooking up the Raspberry Pi and all the necessary components onto my tv. The heatsinks, the sd card, and the controller were all added to ensure that the Raspberry Pi was working. Instead of the Raspberry Pi Os software, I had to first download a different software called Retro Pie. With Retro Pie, I needed to download an Imager for Raspberry Pi. Raspberry Pi Imager automatically downloads a list of the latest versions of Raspbian supported by the Raspberry Pi. Raspbian is the typical Raspberry Pi Os software, the one I needed on the Raspberry Pi was Retro Pi. With the included SD card, I plugged in the SD into my computer and launched the Imager. The imager allowed me to set the Operating System to Retro Pi instead of Raspbian onto the SD card. With the OS imaged onto the SD, I plugged the SD card back into the Raspberry Pi and rebooted the system and Retro Bi booted up.

[![First Milestone]
[![Milestone 1](https://res.cloudinary.com/marcomontalbano/image/upload/v1655494836/video_to_markdown/images/youtube--eeJcswv33rA-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=eeJcswv33rA&feature=youtu.be&ab_channel=BlueStampEng "Milestone 1")
