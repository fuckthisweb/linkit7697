#include <LWiFi.h>
#include "MCS.h"

char _lwifi_ssid[] = "basstomouth";
char _lwifi_pass[] = "peter1224";

MCSDevice mcs("DeKxX1KO", "9RO0PaUX0npSfzl8");
MCSControllerOnOff MySwitch("MySwitch");

void setup()
{
  Serial.begin(9600);

  mcs.addChannel(MySwitch);
  Serial.println("Wi-Fi connecting");
  while (WiFi.begin(_lwifi_ssid, _lwifi_pass) != WL_CONNECTED) { delay(1000); }
  Serial.println("Wi-Fiok");
  while(!mcs.connected()) { mcs.connect(); }
  Serial.println("MCS ok");
  Serial.begin(9600);
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop()
{
  while (!mcs.connected()) {
    mcs.connect();
    if (mcs.connected()) { Serial.println("MCS reconnect"); }
  }
  mcs.process(100);

  if (MySwitch.updated()) {
    Serial.print("renew :");
    Serial.println(MySwitch.value());

    if (MySwitch.value()) {
      digitalWrite(LED_BUILTIN, HIGH);

    } else {
      digitalWrite(LED_BUILTIN, LOW);
    }
  }
  delay(1000);
}
