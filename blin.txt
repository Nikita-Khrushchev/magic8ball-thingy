#include <M5StickC.h>04
  float accX = 0;
  float accY = 0;
  float accZ = 0;
  const char* eightBall[] = { "As I see it, yes.", "Ask again later.", "Better not tell you now", "Cannot predict now.","Don’t count on it.","It is certain.","It is decidedly so.","Most likely.","My reply is no.","My sources say no.","Outlook not so good.","Outlook good.","Reply hazy, try again.","Signs point to yes.","Very doubtful.","Without a doubt.","Yes.","Yes – definitely","You may rely on it." };
  int eightBallRandomizer;
void setup(){
  // Initialize the M5StickC object
  M5.begin();
  M5.IMU.Init();
}
void loop() {
  M5.Lcd.fillScreen(BLUE);
  M5.Lcd.setTextColor(BLACK);
  M5.Lcd.setTextSize(2);
  M5.Lcd.setCursor(10,70);
  M5.Lcd.print("Magic");
  M5.Lcd.setCursor(5,90);
  M5.Lcd.print("8-Ball");
  eightBallRandomizer = random(0,19);
  while(1) {
    M5.IMU.getAccelData(&accX,&accY,&accZ);
    if(digitalRead(M5_BUTTON_HOME) == LOW || accX > 2 ||  accY > 2) {
      break;
    }
  }

  for(int i=0;i<1;i++) {
    M5.Lcd.setCursor(0,60);
    M5.Lcd.fillScreen(BLUE);
    eightBallRandomizer = random(0,19);
    M5.Lcd.println(eightBall[eightBallRandomizer]);
    delay(100);
  }
  delay(5000);
}
