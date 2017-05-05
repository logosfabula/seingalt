# seingalt
Arduino photogrammetry box

[potentiometer_steady.ino]

int potPin = 5;    // select the input pin for the potentiometer
//int ledPin = 13;   // select the pin for the LED
int potentiometer_read = 0;       // variable to store the value coming from the sensor
int wait = 100;
int potentiometer_value = 0;
int last_potentiometer_value = 0;
int potentiometer_min_value = 0;
int potentiometer_max_value = 180;

void setup() 
{
  //pinMode(ledPin, OUTPUT);  // declare the ledPin as an OUTPUT
  Serial.begin(9600);
}

void loop() 
{
  potentiometer_read = analogRead(potPin);    // read the value from the sensor
  potentiometer_value = read_potentiometer(potentiometer_read, potentiometer_min_value, potentiometer_max_value);
  potentiometer_value = map(pow(potentiometer_read,2)/256,0,4088,potentiometer_min_value,potentiometer_max_value);
  potentiometer_value = stabilise(potentiometer_value, last_potentiometer_value);
  last_potentiometer_value = potentiometer_value;
  
  Serial.println(potentiometer_value);
  delay(wait);
}

void p_read()
{
  int potentiometer_read = 0;       // variable to store the value coming from the sensor
  int wait = 100;
  int potentiometer_value = 0;
  int last_potentiometer_value = 0;
  int potentiometer_min_value = 0;
  int potentiometer_max_value = 180;
  
}

int stabilise(int current_value, int last_value)
{
  return (abs(current_value - last_value) == 1) ? max(current_value, last_value) : current_value;
}

int read_potentiometer(int potentiometer_read, int potentiometer_min_value, int potentiometer_max_value)
{
  return map(pow(potentiometer_read,2)/256,0,4088,potentiometer_min_value,potentiometer_max_value);
}

