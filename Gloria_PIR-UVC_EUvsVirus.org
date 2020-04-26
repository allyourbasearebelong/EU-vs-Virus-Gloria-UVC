// EUvsVirus.org
// #team-c08-Gloria  
// Prototype by Kenneth O'Regan
// PIR triggering UVC LED for Public Transport Sterilization
// There must be no human movement within the rear seats of the taxi to trigger the UVC ensuring no human exposure

int ledPin = 13;                // Pin for the UVC LED
int PIR_Pin = 2;                // PIR sensor digital input
int pirState = LOW;             // Start the PIR in low state
int val = 0;                    // Variable for reading the pin status
 
void setup() {
  pinMode(ledPin, OUTPUT);      // Setup LED as output
  pinMode(PIR_Pin, INPUT);      // Setup sensor as input
  
  Serial.begin(9600);
}
 
void loop(){
  val = digitalRead(PIR_Pin);   // Continously read input value
  if (val == LOW) {             // Check if the input is HIGH
    delay(2000);
    digitalWrite(ledPin, HIGH); // Turn UVC LED ON
    if (pirState == LOW) {
      
      Serial.println("No passenger detected, it's safe to start UVC");
      
      pirState = HIGH;
    }
    
  } else {
    digitalWrite(PIR_Pin, HIGH); // turn LED OFF
    if (pirState == LOW){
      
      Serial.println("Passenger detected, it's not safe to to start UVC!");
      
      pirState = LOW;
    }
  }
}
