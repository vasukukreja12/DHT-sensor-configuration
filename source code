#define BLYNK_PRINT Serial
#include <ESP8266WiFi.h>
#include <BlynkSimpleEsp8266.h>
#include <DHT.h>

char auth[] = "yPPHc5ilMQWJOs7t1nPxuaUwM1VwDR0G";

char ssid[] = "Redmi";
char pass[] = "qwerty01";

#define DHTPIN 2          // What digital pin we're connected to


#define DHTTYPE DHT11     // DHT 11

DHT dht(DHTPIN, DHTTYPE);
BlynkTimer timer;


void sendSensor()
{
  float h = dht.readHumidity();
  float t = dht.readTemperature(); 
  float t1 = dht.readTemperature(true);

  if (isnan(h) || isnan(t)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }
  Blynk.virtualWrite(V0, h);
  Blynk.virtualWrite(V1, t);
  Blynk.virtualWrite(V2 , t1);
}

void setup()
{
  // Debug console
  Serial.begin(9600);

  Blynk.begin(auth, ssid, pass);
  
  dht.begin();

  timer.setInterval(1000L, sendSensor);
}

void loop()
{
  Blynk.run();
  timer.run();
}
