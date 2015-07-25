# EllipticalController
Arduino micro pseudo code to convert Elliptical walker for PC play.

int laser1; 
int laser2;
int sensor1;
int sensor2;
 
void setup() {
    pinMode(laser1, OUTPUT);
    pinMode(laser2, OUTPUT);
    pinMode(sensor1, INPUT);
    pinMode(sensor2, INPUT);
    digitalWrite(laser1, HIGH); //Activate laser
    digitalWrite(laser2, HIGH); //Activate laser
    Keyboard.begin(); 
}
 
 
void loop() {
    getDirection();
    if (dt == 0)
	dt = millis();
    tachometer();
    if (millis() - dt > 100) {
	movePlayer();
	toStop();
	dt = 0;
    }
}
 
//Calculate speed of main wheel. Bad way to do it.....but it works.
count = 0;
int intensity = 0;
int intensityLast = 0;
void tachometer() {
    intensity = analogRead(photoDiode);
	if (intensityLast < 100)
	     if (intensity < 100);
	     else {
	        count++;
	     }
	else 
        if (intensityLast > 100)
	    if (intensity > 100);
	    else {
		count++;	
	    }
    intensityLast = intensity;
}
 
//Releases all keys when wheel stops.
void toStop() {
    if (count < minSpeed)
	Keyboard.releaseAll();
}
 
void movePlayer() {
    if (crawling) {
	Keyboard.press(crawl keys);
    } 
    else if (running) {
	Keyboard.press(run keys);
    }
    else if (walking){	
	Keyboard.press(walk keys);
    }
}
 
int readValue = 0;
int step = 0;
void getDirection() {
 
  sensor_01 = digitalRead(sensor2);
  sensor_00 = digitalRead(sensor1);
 
  if(sensor_00 == 0 && sensor_01 == 0){
    if(step == 1){
      readValue--;
      dir = 'backward';
    }
    if(step == 3){
      readValue++;
      dir = 'forward';
    }
    step = 0;
  }
 
  if(sensor_00 == 0 && sensor_01 == 1){
    if(step == 2){
      readValue--;
      dir = 'backward';
    }
    if(step == 0){
      readValue++;
      dir = 'forward';
    }
    step = 1;
  }
 
  if(sensor_00 == 1 && sensor_01 == 1){
    if(step == 3){
      readValue--;
      dir = 'backward';
    }
    if(step == 1){
      readValue++;
      dir = 'forward';
    }
    step = 2;
  }
 
  if(sensor_00 == 1 && sensor_01 == 0){
    if(step == 0){
      readValue--;
      dir = 'backward';
    }
    if(step == 2){
      readValue++;
      dir = 'forward';
    }
    step = 3;
  }
}
