int fsrPin = 0;     // the FSR and 10K pulldown are connected to a0
int fsrReading;     // the analog reading from the FSR resistor divider
  
void setup(void) {
  Serial.begin(9600);
  pinMode(7, OUTPUT);
}
 
void loop(void) {
  fsrReading = analogRead(fsrPin);  
 
  Serial.print("Analog reading = ");
  Serial.print(fsrReading);     // print the raw analog reading
 
  if (fsrReading > 800) {
    Serial.println(" - Overweight");
    digitalWrite(7,HIGH);
    delay(1000);
    digitalWrite(7,LOW);
    
  } 
  delay(1000);
}
