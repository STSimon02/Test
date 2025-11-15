#include <Adafruit_NeoPixel.h>
#define button_Pin 33
#define led_Data 13
#define led_Anzahl 63

bool lastButtonState = LOW;
bool buttonState = LOW;    
bool ledState = LOW;  

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(led_Anzahl, led_Data, NEO_GRB + NEO_KHZ800);

void setup() {
  pixels.begin();
  Serial.begin(115200);
  pinMode(button_Pin, INPUT);
  pinMode(led_Data, OUTPUT);
}


void loop() {
  buttonState = digitalRead(button_Pin);
  if(buttonState == HIGH && lastButtonState == LOW){
    ledState = !ledState;
     delay(500);
}
  if(ledState == HIGH){
        for(int i=0; i < led_Anzahl; i++){
          pixels.setPixelColor(i, pixels.Color(255,255,255)); //  White color.
          }
        pixels.show(); // This sends the updated pixel color to the hardware.
        delay(10);
        Serial.println("LED an");
  
      }
  else if (ledState == LOW){
    for (int i=0; i < led_Anzahl; i++){
          pixels.setPixelColor(i, pixels.Color(0,0,0));
          }
        pixels.show();
        delay(10);
        Serial.println("LED aus");
          
 }
 delay(100);
}
