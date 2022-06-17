# Alarm-vehicle
This project is used for the protection of vehicle in which it is designed against thieves
## The first time we need the components of the circuit done this project,these components are as follows
-Arduino uno ![image](https://user-images.githubusercontent.com/105424030/174350010-5d2ea934-e236-4961-98d7-d8bec1cf19a3.png)
-BC547 ![image](https://user-images.githubusercontent.com/105424030/174350672-71726d88-0a64-4ec8-b146-7492c5aba117.png)
-Button active ![image](https://user-images.githubusercontent.com/105424030/174352106-ddb51272-b7a5-45b9-9319-97c0afaee4e2.png)
-Diode 1N4148 ![image](https://user-images.githubusercontent.com/105424030/174352550-9d1e053d-c465-42cc-afd2-d8bbfde65c9d.png)
-Capacitor 100nF ![image](https://user-images.githubusercontent.com/105424030/174353506-d5993710-b6ed-4ebf-8aaa-56fd11371488.png)
-LED_GREEN ![image](https://user-images.githubusercontent.com/105424030/174353835-b621339d-a25f-4ba8-9f16-16c438dee6bf.png)
-LM016L ![image](https://user-images.githubusercontent.com/105424030/174354187-94fa56e7-a04a-4dce-a131-287dd4a421ec.png)
-POT ![image](https://user-images.githubusercontent.com/105424030/174355868-372b672a-2d0f-41f7-8fdb-eb1e6d564307.png)
-RELAY ![image](https://user-images.githubusercontent.com/105424030/174356573-c3dfc98b-6731-43ee-aa88-d8c53f4ca740.png)
- 2* Resistor 10k ![image](https://user-images.githubusercontent.com/105424030/174356938-c29d4f8f-8606-4e5c-a2ca-35cca64c6abd.png)
-SIM900D ![image](https://user-images.githubusercontent.com/105424030/174357171-ff79bda4-faab-45f4-9064-77f91b71a6d8.png)
- TBLOCK-13 ![image](https://user-images.githubusercontent.com/105424030/174357760-383cebb1-93aa-47f2-8456-10e87cb611de.png)
- VIBRATION SW-420 ![image](https://user-images.githubusercontent.com/105424030/174358113-2cafa765-a8c7-488b-818a-5543493489c4.png)
## Circuit with proteus is ![image](https://user-images.githubusercontent.com/105424030/174375637-626f9d8f-f193-4019-bca7-1b30081a70e1.png)
## For the code that will be introduced in Arduino is the following:
#include<LiquidCrystal.h>

#include<SoftwareSerial.h>

LiquidCrystal lcd(7,6,5,4,3,2);

SoftwareSerial GSM(0,1);

const int Switch=8;

const int Sensor=9;

int Buzzer=13;

void stepup(){

  pinMode(Sensor,INPUT);
  
  pinMode(Buzzer,OUTPUT);
  
  Serial.begin(9600);
  
  lcd.begin(16, 2);
  
}

void loop()
{

  if(digitalRead(Switch)==HIGH)
  
  {
  
    lcd.setCursor(0,0);
    lcd.print("Security System");
    lcd.setCursor(0,1);
    lcd.print(" on  ");

      if(digitalRead(Sensor)==HIGH)
      
  {
  
    lcd.setCursor(0, 0);
    lcd.print("Theft Detected");
    lcd.setCursor(0, 1);
    lcd.print("Sending SMS....  ");
    
    digitalWrite(13,HIGH);

 sendSMS();
 
    delay(500);
    
  }
  
  else
  
{

  digitalWrite(13,LOW);
  
}

  }

  
  
    lcd.setCursor(0,0);
    lcd.print("Security System");
    lcd.setCursor(0,1);
    lcd.print("Desactivated  ");
    lcd.print("Security System");
    lcd.setCursor(0,1);
    lcd.print("Desactivated  ");
    
    }

   void sendSMS()
   
   {
   
    Serial.println("AT+CMGD=1");
    
    delay(100);

    Serial.println("AT+CMGD=1");
    
    delay(100);

    Serial.print("AT+CMGW=");
    Serial.write(34);
    Serial.print("+237********24");
    Serial.write(34);
    Serial.println();
    delay(400);

    Serial.println("Alert: Theft Detected");
    
    delay(100);

    Serial.write(26);
    delay(100);
    delay(100);

    Serial.println("AT+CMSS=1");
    
    delay(100);
    
   }
