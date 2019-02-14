# unorandomrelay

 
/*
 * Arduino code to control 16 channel relay with Arduino UNO
 * 
 * Written by Ahmad Shamshiri for Robojax.com on Sunday Oct 08, 2018 
 * at 10:35 in Ajax, Ontario, Canada
 * Watch video instruction for this code: https://youtu.be/Q9aBI4ELKC4
 * Modified by REA Electric 14 Feb 2019 NSW, AUstralia
 * Simple Random Relay selection
 * See Example https://youtu.be/P9LIQ3Znmek
 * 
 * This code is "AS IS" without warranty or liability. Free to be used as long as you keep this note intact.* 
 * This code has been download from Robojax.com
    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <https://www.gnu.org/licenses/>.
 */


const int controlPin[16] = {2,3,4,5,6,7,8,9,10,11,12,A0,A1,A2,A3,A4}; // define pins

const int triggerType = LOW;// your relay type
int loopDelay = 1000;// delay in loop
int tmpStat =1;
long randLEDNo;


void setup() {

  // randomSeed() will then shuffle the random function.
  randomSeed(analogRead(0));

  for(int i=0; i<16; i++)
  {
    pinMode(controlPin[i], OUTPUT);// set pin as output
    if(triggerType ==LOW){
      digitalWrite(controlPin[i], HIGH); // set initial state OFF for low trigger relay
    }else{
       digitalWrite(controlPin[i], LOW); // set initial state OFF for high trigger relay     
    }
  }
  
  Serial.begin(9600);// initialize serial monitor with 9600 baud
}

void loop() {


  randLEDNo =random(0,3);
  
azchannelControl(randLEDNo,1, random(100,200)); // turn relay ON 

// channelControl(randLEDNo,1, 100); // turn relay ON 
 //  delay(5000);// wait for loopDelay ms
  channelControl(randLEDNo,0, 0); // turn relay OFF           
  
}

/*
 * funciton: channelControl
 * turns ON or OFF specific relay channel
 * @param relayChannel is integer value channel from 0 to 15
 * @param action is 1 for ON or 0 for OFF
 * @param t is time in melisecond
 */
void channelControl(int relayChannel, int action, int t)
{
  int state =LOW;
  String statTXT =" ON";
  if(triggerType == LOW)
  {    
    if (action ==0)// if OFF requested
    {
      state = HIGH;
      statTXT = " OFF";
    }
    digitalWrite(controlPin[relayChannel], state);
    if(t >0 )
    {
      delay(t);
    }
       Serial.print ("Channel: ");
       Serial.print(relayChannel); 
       Serial.print(statTXT);
       Serial.print(" - "); 
       Serial.println(t);        
  }else{
    if (action ==1)// if ON requested
    {
      state = HIGH;     
    }else{
      statTXT = " OFF";    
    }
    digitalWrite(controlPin[relayChannel], state);
    if(t >0 )
    {
      delay(t);
    }
       Serial.print ("Channel: ");
       Serial.print(relayChannel); 
       Serial.print(statTXT);
       Serial.print(" - "); 
       Serial.println(t);    
  }

}

 
