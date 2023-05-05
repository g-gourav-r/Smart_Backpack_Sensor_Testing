char Incoming_value = 0;
/* Strap Sensors */
/*Strap Sensor 1*/
int fsrPin1 = 1;     
int fsrReading1;     
int fsrVoltage1;     
unsigned long fsrResistance1;  
unsigned long fsrConductance1; 
long fsrForce1;
/*Strap Sensor 2*/     
int fsrPin2 = 2;     
int fsrReading2;     
int fsrVoltage2;     
unsigned long fsrResistance2;  
unsigned long fsrConductance2; 
long fsrForce2;
long resultantForce;
/* Strap Sensors End*/
                
void setup() 
{
  Serial.begin(9600);               
}

/* Calibrate Start*/
void calibrate(){

    /*FSR1*/

    fsrReading1 = analogRead(fsrPin1);  
    //Serial.print("Analog reading = ");
    //Serial.println(fsrReading);
    // analog voltage reading ranges from about 0 to 1023 which maps to 0V to 5V (= 5000mV)
    fsrVoltage1 = map(fsrReading1, 0, 1023, 0, 5000);
    //Serial.print("Voltage reading in mV = ");
    //Serial.println(fsrVoltage);  
    if (fsrVoltage1 == 0) {
        Serial.println("No pressure");  
    } else {
        // The voltage = Vcc * R / (R + FSR) where R = 10K and Vcc = 5V
        // so FSR = ((Vcc - V) * R) / V        yay math!
        fsrResistance1 = 5000 - fsrVoltage1;     // fsrVoltage is in millivolts so 5V = 5000mV
        fsrResistance1 *= 10000;                // 10K resistor
        fsrResistance1 /= fsrVoltage1;
        //Serial.print("FSR resistance in ohms = ");
        //Serial.println(fsrResistance);
    
        fsrConductance1 = 1000000;           // we measure in micromhos so 
        fsrConductance1 /= fsrResistance1;
        //Serial.print("Conductance in microMhos: ");
        //Serial.println(fsrConductance);
    
        // Use the two FSR guide graphs to approximate the force
        if (fsrConductance1 <= 1000) {
        fsrForce1 = fsrConductance1 / 80;
        //Serial.print("Force in Newtons: ");
        //Serial.println(fsrForce);      
        } else {
        fsrForce1 = fsrConductance1 - 1000;
        fsrForce1 /= 30;
        //Serial.print("Force in Newtons: ");
        //Serial.println(fsrForce);            
        }
    }

    /*FSR 2*/

    fsrReading2 = analogRead(fsrPin2);  
    //Serial.print("Analog reading = ");
    //Serial.println(fsrReading);
    // analog voltage reading ranges from about 0 to 1023 which maps to 0V to 5V (= 5000mV)
    fsrVoltage2 = map(fsrReading2, 0, 1023, 0, 5000);
    //Serial.print("Voltage reading in mV = ");
    //Serial.println(fsrVoltage);  
    if (fsrVoltage2 == 0) {
        Serial.println("No pressure");  
    } else {
        // The voltage = Vcc * R / (R + FSR) where R = 10K and Vcc = 5V
        // so FSR = ((Vcc - V) * R) / V        yay math!
        fsrResistance2 = 5000 - fsrVoltage2;     // fsrVoltage is in millivolts so 5V = 5000mV
        fsrResistance2 *= 10000;                // 10K resistor
        fsrResistance2 /= fsrVoltage2;
        //Serial.print("FSR resistance in ohms = ");
        //Serial.println(fsrResistance);
    
        fsrConductance2 = 1000000;           // we measure in micromhos so 
        fsrConductance2 /= fsrResistance2;
        //Serial.print("Conductance in microMhos: ");
        //Serial.println(fsrConductance);
    
        // Use the two FSR guide graphs to approximate the force
        if (fsrConductance2 <= 1000) {
        fsrForce2 = fsrConductance2 / 80;
        //Serial.print("Force in Newtons: ");
        //Serial.println(fsrForce);      
        } else {
        fsrForce2 = fsrConductance2 - 1000;
        fsrForce2 /= 30;
        //Serial.print("Force in Newtons: ");
        //Serial.println(fsrForce);            
        }
    }

    resultantForce = fsrForce1-fsrForce2;
    Serial.println(resultantForce);
}
/* Calibrate End*/

void loop()
{
  if(Serial.available() > 0)  
  {        
    if(Incoming_value == '1')             
      calibrate();  
    else if(Incoming_value == '0')       
      digitalWrite(13, LOW);   
  }                            
} 
