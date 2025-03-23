You need to update the following line in your Python code to match the port where your Arduino is connected:
ser = serial.Serial('COM3', 9600)


Other than that, here is the Arduino code:
const int motorPin1 = 3;  // Motor 1 forward  
const int motorPin2 = 4;  // Motor 1 backward  
const int motorPin3 = 5;  // Motor 2 forward  
const int motorPin4 = 6;  // Motor 2 backward  
const int buttonPin = 7;  // Button pin  

bool auto_lock = false;  // Locking status  

void setup() {  
    pinMode(motorPin1, OUTPUT);  
    pinMode(motorPin2, OUTPUT);  
    pinMode(motorPin3, OUTPUT);  
    pinMode(motorPin4, OUTPUT);  
    pinMode(buttonPin, INPUT_PULLUP);  // Set button as input  
    Serial.begin(9600);  
}  

void loop() {  
    // Check button state  
    if (digitalRead(buttonPin) == LOW) {  // When the button is pressed (active low)  
        auto_lock = !auto_lock;  // Toggle lock status 
        Serial.println("BUTTON_PRESSED");
        delay(500);  // Short delay to prevent accidental multiple presses  
    }  

    if (Serial.available() > 0) {  
        char command = Serial.read();  // Read the incoming command  
        switch (command) {  
            case 'L':  // Move left  
                digitalWrite(motorPin1, HIGH);  
                digitalWrite(motorPin2, LOW);  
                digitalWrite(motorPin3, LOW);  
                digitalWrite(motorPin4, HIGH);  
                break;  
            case 'R':  // Move right  
                digitalWrite(motorPin1, LOW);  
                digitalWrite(motorPin2, HIGH);  
                digitalWrite(motorPin3, HIGH);  
                digitalWrite(motorPin4, LOW);  
                break;  
            case 'U':  // Move up  
                digitalWrite(motorPin1, HIGH);  
                digitalWrite(motorPin2, LOW);  
                digitalWrite(motorPin3, HIGH);  
                digitalWrite(motorPin4, LOW);  
                break;  
            case 'D':  // Move down  
                digitalWrite(motorPin1, LOW);  
                digitalWrite(motorPin2, HIGH);  
                digitalWrite(motorPin3, LOW);  
                digitalWrite(motorPin4, HIGH);  
                break;  
            case 'S':  // Stop  
                digitalWrite(motorPin1, LOW);  
                digitalWrite(motorPin2, LOW);  
                digitalWrite(motorPin3, LOW);  
                digitalWrite(motorPin4, LOW);  
                break;  
        }  
    }  
}  


After writing this code in the Arduino IDE, you should adjust the movement of motorPin values (LOW or HIGH) according to your machine's specific configuration.

In this code, the "auto lock" feature is triggered by a button that you connect to motorPin7 on the Arduino.

Lastly, the code currently detects red as an enemy and blue as a friend. If you want to change these colors, you can modify the contour color codes as you wish.
