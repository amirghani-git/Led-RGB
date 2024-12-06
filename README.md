# led RGB
// تعریف پایه‌ها
const int redPin = 9;
const int greenPin = 6;
const int bluePin = 11;
const int potPin = A0;

void setup() {
  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);
}

void loop() {
  // خواندن مقدار پتانسیومتر
  int potValue = analogRead(potPin);
  
  // تبدیل مقدار به دامنه ۰ تا ۷۶۵ (جمع سه رنگ RGB)
  int colorValue = map(potValue, 0, 1023, 0, 765);
  
  int redValue, greenValue, blueValue;

  // تغییر مقدار رنگ‌ها بر اساس مقدار پتانسیومتر
  if (colorValue <= 255) {
    redValue = 255 - colorValue;
    greenValue = colorValue;
    blueValue = 0;
  } else if (colorValue <= 510) {
    redValue = 0;
    greenValue = 510 - colorValue;
    blueValue = colorValue - 255;
  } else {
    redValue = colorValue - 510;
    greenValue = 0;
    blueValue = 765 - colorValue;
  }

  // تنظیم شدت نور LED RGB
  analogWrite(redPin, redValue);
  analogWrite(greenPin, greenValue);
  analogWrite(bluePin, blueValue);

  delay(100); // تاخیر برای پایداری بیشتر
}
