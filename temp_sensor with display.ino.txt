#include <OneWire.h>                 //this library is used to covert temp sensor data in esp 32 understandable language
#include <DallasTemperature.h> //this library is used to covert that sensor data into human readable form
#include <Wire.h>        //to work with i2c
#include <Adafruit_GFX.h>    //to work with display
#include <Adafruit_SSD1306.h>

#define TEMP_SENSOR 5    
#define BUZZER_PIN  25     // defined the wire line that send sensor data to microcontroller
#define SCREEN_WIDTH 126
#define SCREEN_HEIGHT 64
#define OLED_RESET -1     //does not have any reset
#define OLED_ADDRESS 0x3C   //arduino send dato to specific adress of led


OneWire oneWire(TEMP_SENSOR);      // senoor is connected to pin 5 using one wire comm..
DallasTemperature sensor(&oneWire);        //converting that sensor data into human readble form using dallas library
Adafruit_SSD1306 display(SCREEN_WIDTH,SCREEN_HEIGHT,&Wire,OLED_RESET);
void setup() {
 Serial.begin(115200); //show temp on serial temp, with speed of 115200
 Wire.begin(21,22);    //pin 21 ,22 is used as I2C pins 
 sensor.begin() ;  //prepare sensor to read data]

 display.begin(SSD1306_SWITCHCAPVCC,OLED_ADDRESS);      // without this OLED will will not work
 display.clearDisplay();   //clear dislay
 display.setTextSize(2);    // doubles text size     // these are inbuilt fxns of adafruit library
 display.setTextColor(SSD1306_WHITE);        //set text color as white
 
}  // setup code runs only once

void loop() {
  sensor.requestTemperatures();      //request sensoor to sense data and provide the value
  float temperature = sensor.getTempCByIndex(0);    // 0-> one temp sensoor is being used  // covert data in esp understandable language
 // reads temp in celcius and store the value in temperature

  display.clearDisplay();
  display.setCursor(0,30);    //set cursor to intial location to display text
  display.print(temperature);
  display.print("deg C");

  display.display();    // to display the text finally
 
  Serial.print("temperature");
  Serial.print(temperature);
  Serial.println("degree C");    //ln-> prints data in new line
  
  if(temperature > 20){
    digitalWrite(BUZZER_PIN, HIGH);
    delay(50);
    digitalWrite(BUZZER_PIN, LOW);
    delay(50);
  }
}  //loop code runs again and again

