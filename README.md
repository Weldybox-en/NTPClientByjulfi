# NTPClient by julfi

## Installing

The installation is slightly different from the original. This one had to be installed manually!

- First, download the archive librairy
- Copy and past the directory in your IDE librairy managment directory. (Ardiuno IDE or Platformio)
- I personnaly use platformio and the correct directory is located here by default: *C:\Users\#username\.platformio\lib*

It look like this:

<p align="left">

  <img src="https://imgur.com/KVYgPec.png">
</p>

## Typical use

Connect to a NTP server, here is how:

```cpp
#include <NTPClientByjulfi.h>
// change next line to use with another board/shield
#include <ESP8266WiFi.h>
//#include <WiFi.h> // for WiFi shield
//#include <WiFi101.h> // for WiFi 101 shield or MKR1000
#include <WiFiUdp.h>

const char *ssid     = "<SSID>";
const char *password = "<PASSWORD>";

WiFiUDP ntpUDP;

// By default 'time.nist.gov' is used with 60 seconds update interval and
// no offset
NTPClient timeClient(ntpUDP);

// You can specify the time server pool and the offset, (in seconds)
// additionaly you can specify the update interval (in milliseconds).
// NTPClient timeClient(ntpUDP, "europe.pool.ntp.org", 3600, 60000);

void setup(){
  Serial.begin(115200);
  WiFi.begin(ssid, password);

  while ( WiFi.status() != WL_CONNECTED ) {
    delay ( 500 );
    Serial.print ( "." );
  }

  timeClient.begin();
}

void loop() {
  timeClient.update();

  Serial.print("Formatted time : ");Serial.println(timeClient.getFormattedTime());

  /* Newly added methods */
  Serial.print("The month's number: ");Serial.println(timeClient.getMonth());
  Serial.print("The year: ");Serial.println(timeClient.getYear());
  Serial.print("The actual day's number: ");Serial.println(timeClient.getRealDay());

  delay(1000);
}
```

 ## Support me
 
I've decide to share for free my work because i've learn tanks to that! For me, sharing project like this for free accelerate the knowledge corculation and that very cool.

But i'm student and like every student i'm broken :(
So, if you can, feel free to buy me a coffe :D

[![paypal](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/jvZuQ8SYo)
