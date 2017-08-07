# Azure-IoT-Hub-ESP8266-Easy-Connect
Send and receive IoT Hub messages from ESP8266 Arduino

This is an extraction of the [Get Started with Microsoft Azure IoT Starter Kit - Adafruit Feather Huzzah ESP8266 (Arduino-compatible)](https://github.com/Azure-Samples/iot-hub-c-huzzah-getstartedkit) sample. 
The difference is that this repo does not require a sensor or the simulation of one and also includes all configuration information in the code so you do not need to use the Serial Monitor to input credentials.

Download the three files in this repo:
1. Azure-IoT-Hub-ESP8266-Easy-Connect.ino
2. config.h
3. iothubClient.ino

Update the config.h file towards the bottom:
```
#define CONNECTION_STRING  "YOUR_DEVICE_CONNECTION_STRING_HERE"

#define WIFI_SSID     "YOUR_WIFI_SSID_HERE"
#define WIFI_PASS     "YOUR_WIFI_PASSWORD_HERE"
```

Install the [ESP8266 board](https://github.com/Azure-Samples/iot-hub-c-huzzah-getstartedkit#section1.5.1) and required libraries 
from the Arduino IDE. You can use Visual Studio Code with the Arduino extension to do this as well.
1. AzureIoTHub
2. AzureIoTUtility
3. AzureIoTProtocol_MQTT
4. ArduinoJSON

Upload to Arduino. Open serial monitor to see messages being sent to IoT Hub. 

Open the [Device Explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer#download) and send Messages to Device.

Board will use built-in LED and blink when sending and receiving messages.

The code in the `loop()` function is responsible for sending and receiving messages. Customize the message `YOUR_IOT_HUB_MESSAGE_HERE` with your desired message. 
```
void loop()
{
    if (!messagePending && messageSending)
    {
        char messagePayload[MESSAGE_MAX_LEN] = "YOUR_IOT_HUB_MESSAGE_HERE";
        sendMessage(iotHubClientHandle, messagePayload);
        messageCount++;
        delay(interval);
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    delay(10);
}
```
