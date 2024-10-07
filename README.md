# line-following-robot
int IN1 = 2;  // Direction pin 1 for Motor 1, D4
int IN2 = 4;  // Direction pin 2 for Motor 1, D2

int IN3 = 13; // Direction pin 1 for Motor 2, D6
int IN4 = 12; // Direction pin 2 for Motor 2, D7

int L_S = 14; // Left IR sensor pin, D5
int R_S = 5;  // Right IR sensor pin, D1

void setup() {
    Serial.begin(9600);
    // Set all the motor control pins to outputs
    pinMode(IN1, OUTPUT);
    pinMode(IN2, OUTPUT);
    pinMode(IN3, OUTPUT);
    pinMode(IN4, OUTPUT);
    pinMode(L_S, INPUT);
    pinMode(R_S, INPUT);
}

void forward() {
    digitalWrite(IN1, HIGH);   // Motor 1 forward
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, HIGH);   // Motor 2 forward
    digitalWrite(IN4, LOW);
}

void left() {
    digitalWrite(IN1, LOW);   // Motor 1 backward
    digitalWrite(IN2, HIGH);
    digitalWrite(IN3, HIGH);   // Motor 2 forward
    digitalWrite(IN4, LOW);
}

void right() {
    digitalWrite(IN1, HIGH);   // Motor 1 forward
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);    // Motor 2 backward
    digitalWrite(IN4, HIGH);
}

void brake() {
    digitalWrite(IN1, LOW);
    digitalWrite(IN2, LOW);
    digitalWrite(IN3, LOW);
    digitalWrite(IN4, LOW);
}

void loop() {
    int leftSensor = digitalRead(L_S);
    int rightSensor = digitalRead(R_S);
    
    if (leftSensor == LOW && rightSensor == LOW) {
        // Both sensors see the line
        forward();  // Move forward
    } else if (leftSensor == LOW) {
        // Left sensor sees the line
        right();    // Turn right
    } else if (rightSensor == LOW) {
        // Right sensor sees the line
        left();     // Turn left
    } else {
        // No sensors see the line
        brake();    // Stop
    }
}
