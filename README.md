# ESP-32
ESP32 is a series of low-cost, low-power system on a chip microcontrollers with integrated Wi-Fi and dual-mode Bluetooth.
![esp1](https://github.com/shaikhahObaid/ESP-32/assets/111530370/f82736ef-f766-4dec-a43a-c71709a6a418)

## Circle explanation
The function of the circuit lies in showing how the ESP-32 works, as it will initially connect to the Internet, after that it will read the http link, and if the word is forward, then the red LED will light, and if the word is backward, the yellow LED will light, and so on...
## Circuit view and simulation
![00](https://github.com/shaikhahObaid/ESP-32/assets/111530370/e69c8c0b-b5b7-43da-8a74-d0d6ed83e67c)

https://wokwi.com/projects/373017941843953665 
## The code 
#include <WiFi.h>

#include <HTTPClient.h>

const char* ssid = "Wokwi-GUEST";

const char* password = "";

const String url = "https://s-m.com.sa/f.html"; 
//file:///C:/Users/%D8%B4%D9%8A%D8%AE%D9%87%20%D8%B9%D8%A8%D9%8A%D8%AF%20%D8%A8%D8%A7%D9%84%D8%AD%D9%85%D8%B1/Documents/Screen%20Robot/%D8%A3%D8%AC%D8%B2%D8%A7%D8%A1%20%D8%B1%D9%88%D8%A8%D9%88%D8%AA%20%D8%A7%D9%84%D8%B4%D8%A7%D8%B4%D8%A9/2.html
String payload = "";

void setup() {

  Serial.begin(115200);
  
  WiFi.begin(ssid, password);
  
  pinMode(34, OUTPUT);//F
  
  pinMode(25, OUTPUT);//B
  
  pinMode(12, OUTPUT);//L
  
  pinMode(13, OUTPUT);//R
  
  Serial.print("Hello World ");
  
  while (WiFi.status() != WL_CONNECTED) {
  
    delay(500);
    
    Serial.print("Connecting to WiFi");
    
    Serial.println( );
    
  }

  Serial.print("OK! IP=");
  
  Serial.println(WiFi.localIP());

  Serial.print("Fetching " + url + "... ");

  


}

void loop() {

  HTTPClient http;
  
  http.begin(url);
  
  int httpResponseCode = http.GET();
  
  if (httpResponseCode > 0) {
  
    Serial.print("HTTP ");
    
    Serial.println(httpResponseCode);
    
    payload = http.getString();
    
    Serial.println();
    
    Serial.println(payload);
    
    if( payload == "forward" )
    
      digitalWrite(34, HIGH);
      
    else if (payload == "backward") 
    
      digitalWrite(25, HIGH);
      
    else if (payload == "left") 
    
      digitalWrite(12, HIGH); 
      
    else if (payload == "right") 
    
      digitalWrite(13, HIGH);
    
  }
  
  else {
  
    Serial.print("Error code: ");
    
    Serial.println(httpResponseCode);
    
    Serial.println(":-(");
    
  }
  
}
