#include <SoftwareSerial.h>
SoftwareSerial mySerial(2,3);
void setup() {
Serial.begin(9600);
mySerial.begin(9600);
pinMode(4,OUTPUT);
pinMode(5,OUTPUT);
pinMode(6,OUTPUT);
pinMode(7,OUTPUT);
}

void loop() {
  digitalWrite(4,LOW);
  digitalWrite(5,HIGH);
  digitalWrite(6,LOW);
  digitalWrite(7,HIGH);
  if(digitalRead(A0)==HIGH)
  {
    Serial.println("SENSE 1");
    digitalWrite(4,LOW);
    digitalWrite(5,LOW);
    digitalWrite(6,LOW);
    digitalWrite(7,LOW);
    SendMessage("CRACK IS DETECTED IN LEFT https://www.google.com/maps/search/?api=1&query=13.009571719760125,80.00502670603903");
    digitalWrite(4,LOW);
    digitalWrite(5,HIGH);
    digitalWrite(6,LOW);
    digitalWrite(7,HIGH);
    delay(1000);
  }
  if(digitalRead(A1)==HIGH)
  {
    digitalWrite(4,LOW);
    digitalWrite(5,LOW);
    digitalWrite(6,LOW);
    digitalWrite(7,LOW);
    Serial.println("SENSE 2");
    SendMessage("CRACK IS DETECTED IN RIGHT https://www.google.com/maps/search/?api=1&query=13.009571719760125,80.00502670603903");
    digitalWrite(4,LOW);
    digitalWrite(5,HIGH);
    digitalWrite(6,LOW);
    digitalWrite(7,HIGH);
    delay(1000);
  }
}

void SendMessage(String message)
{
  mySerial.println("AT+CMGF=1");
  delay(1000);
  mySerial.println("AT+CMGS=\"+918015992290\"\r");
  delay(1000);
  mySerial.println(message);
  delay(100);
  mySerial.println((char)26);
  delay(1000);
}
