#include <Servo.h>

Servo Servo1;
Servo Mac;

Servo finalDoor;

int rgb1 = 11;
int rgb2 = 9;


const int copperSwitch1 = 4;


const int copperSwitch2 = 5;

const int copperSwitch3 =  13;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
const int copperSwitch4 = 10;
const int copperSwitch5 = 8;


int copperSwitchVal;
int copperSwitchVal2;
int copperSwitchVal3;
int copperSwitchVal4;
int copperSwitchVal5;                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       ;

bool part1Complete;
bool part2Complete;
bool part3Complete;
bool part4Complete;
bool part5Complete;

void setup() {

// Set up the interactions 

  Servo1.attach(3);
  Mac.attach(12);
  finalDoor.attach(7);
  pinMode(copperSwitch1, INPUT);
  pinMode(copperSwitch2, INPUT);
  pinMode(copperSwitch3, INPUT);
  pinMode(copperSwitch4, INPUT);
  pinMode(copperSwitch5, INPUT);                                                                                                                                                                                                                                                                                                                                                        

 
 
  pinMode(rgb1,  OUTPUT);              
  pinMode(rgb2, OUTPUT);


// Don't run other interactions until previous interactions before that are complete


  part1Complete = false;
  part2Complete = false;
  part3Complete = false;
  part4Complete = false;
  part5Complete = false;
 Serial.begin(9600);
  // put your setup code here, to run once:
}

void loop(){




  // put your main code here, to run repeatedly:
  copperSwitchVal = digitalRead(copperSwitch1);
  copperSwitchVal2 = digitalRead(copperSwitch2);
  copperSwitchVal3 = digitalRead(copperSwitch3);
  copperSwitchVal4 = digitalRead(copperSwitch4);
  copperSwitchVal5 = digitalRead(copperSwitch5);

// Spin the pit crew around quickly

 
  if (copperSwitchVal == HIGH){
    Servo1.write(180);
     Serial.println(copperSwitchVal);
     
      if(part1Complete == false){
        part1Complete = true;
      }
  }
  else{
    Servo1.write(90);

  }

// Turn on the finish line light
  
  if (part1Complete == true && copperSwitchVal2){
 
    setColor1(255, 255, 255);
 
    if (part2Complete == false){
      part2Complete = true;
    }
  }
  else{
    setColor1(0, 0, 0);
  }

// Turn Mack by 90 degrees counterclockwise. 


  if (part2Complete = true && copperSwitchVal3 == HIGH){
    Mac.write(180);
    if(part3Complete == false){
      part3Complete = true;
    }
  }
  else if(part3Complete == true){
    Mac.write(180);
  }
  else{
    Mac.write(90);
  }

// Turn on the light inside the building in Radiator Springs. 

  if(part3Complete == true && copperSwitchVal4 == HIGH){
    setColor2(255, 255, 255);
    Serial.println("Light working");

    if(part4Complete == false){
      part4Complete = true;
  }
  }
  else{
    setColor2(0, 0, 0);
  }
 

// Move around the door with the arrows pointing towards the King. 

  if(part4Complete == true && copperSwitchVal5 == HIGH){
    finalDoor.write(180);
    Serial.println("door open");
    if(part5Complete == false){
      part5Complete = true;
    }
  }

  //else if(part5Complete == true){
    //finalDoor.write(180);
  //}
  else{
    finalDoor.write(0);
  }
}





void setColor1(int redValue, int greenValue,  int blueValue) {
  analogWrite(rgb1, redValue);

}

void setColor2(int redValue, int greenValue, int blueValue){
  analogWrite(rgb2, greenValue);

}
