## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie doet u het volgende:

* U maakt een Node.js-console-app die reageert op een directe methode die door de cloud wordt aangeroepen.
* U activeert een gesimuleerde firmware-update.
* U gebruikt de gerapporteerde eigenschappen om apparaatdubbelquery's in te schakelen die de apparaten identificeren en vaststellen wanneer er voor het laatst een firmware-update op deze apparaten is uitgevoerd.

Stap 1: Maak een lege map genaamd **manageddevice**.  Maak in de map **simulateddevice** een bestand met de naam package.json door achter de opdrachtprompt de volgende opdracht op te geven. Accepteer alle standaardwaarden:
   
    ```
    npm init
    ```

Stap 2: bij de opdrachtprompt in de **manageddevice** map, voer de volgende opdracht voor het installeren van de **azure-iot-device** en **azure-iot-device-mqtt** apparaat-SDK pakketten:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Stap 3: Gebruik een teksteditor, maak een **dmpatterns_fwupdate_device.js** bestand de **manageddevice** map.

Stap 4: Voeg de volgende 'vereist' instructies aan het begin van de **dmpatterns_fwupdate_device.js** bestand:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Stap 5: Voeg een **connectionString** variabele en deze gebruiken voor het maken een **Client** exemplaar. Vervang de tijdelijke aanduiding `{yourdeviceconnectionstring}` door de verbindingsreeks die u eerder hebt genoteerd in de sectie Een apparaat-id maken:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Stap 6: Voeg de volgende functie die wordt gebruikt voor het bijwerken van de gerapporteerde eigenschappen toe:
   
    ```
    var reportFWUpdateThroughTwin = function(twin, firmwareUpdateValue) {
      var patch = {
          iothubDM : {
            firmwareUpdate : firmwareUpdateValue
          }
      };
   
      twin.properties.reported.update(patch, function(err) {
        if (err) throw err;
        console.log('twin state reported: ' + firmwareUpdateValue.status);
      });
    };
    ```

Stap 7: Voeg de volgende functies die simuleren downloaden en de firmware-installatiekopie toe te passen:
   
    ```
    var simulateDownloadImage = function(imageUrl, callback) {
      var error = null;
      var image = "[fake image data]";
   
      console.log("Downloading image from " + imageUrl);
   
      callback(error, image);
    }
   
    var simulateApplyImage = function(imageData, callback) {
      var error = null;
   
      if (!imageData) {
        error = {message: 'Apply image failed because of missing image data.'};
      }
   
      callback(error);
    }
    ```

Stap 8: Voeg de volgende functie die de status van de firmware bijwerken via de gerapporteerde eigenschappen naar wordt **wachten**. Normaal gesproken worden apparaten op de hoogte gesteld van een beschikbare update, waarna een door de beheerder gedefinieerd beleid ervoor zorgt dat het apparaat de update downloadt en toepast. In deze functie moet de logica voor het inschakelen van dat beleid worden uitgevoerd. Voor het gemak wacht de steekproef vier seconden voordat u de firmware-installatiekopie te downloaden:
   
    ```
    var waitToDownload = function(twin, fwPackageUriVal, callback) {
      var now = new Date();
   
      reportFWUpdateThroughTwin(twin, {
        fwPackageUri: fwPackageUriVal,
        status: 'waiting',
        error : null,
        startedWaitingTime : now.toISOString()
      });
      setTimeout(callback, 4000);
    };
    ```

Stap 9: Voeg de volgende functie die de status van de firmware bijwerken via de gerapporteerde eigenschappen naar wordt **downloaden**. De functie simuleert vervolgens het downloaden van de firmware, waarna de updatestatus van de firmware wordt gewijzigd in **downloadFailed** of **downloadComplete**:
   
    ```
    var downloadImage = function(twin, fwPackageUriVal, callback) {
      var now = new Date();   
   
      reportFWUpdateThroughTwin(twin, {
        status: 'downloading',
      });
   
      setTimeout(function() {
        // Simulate download
        simulateDownloadImage(fwPackageUriVal, function(err, image) {
   
          if (err)
          {
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadfailed',
              error: {
                code: error_code,
                message: error_message,
              }
            });
          }
          else {        
            reportFWUpdateThroughTwin(twin, {
              status: 'downloadComplete',
              downloadCompleteTime: now.toISOString(),
            });
   
            setTimeout(function() { callback(image); }, 4000);   
          }
        });
   
      }, 4000);
    }
    ```

Stap 10: Voeg de volgende functie die de status van de firmware bijwerken via de gerapporteerde eigenschappen naar wordt **toepassen**. De functie simuleert vervolgens het toepassen van de firmware, waarna de updatestatus van de firmware wordt gewijzigd in **applyFailed** of **applyComplete**:
    
    ```
    var applyImage = function(twin, imageData, callback) {
      var now = new Date();   
    
      reportFWUpdateThroughTwin(twin, {
        status: 'applying',
        startedApplyingImage : now.toISOString()
      });
    
      setTimeout(function() {
    
        // Simulate apply firmware image
        simulateApplyImage(imageData, function(err) {
          if (err) {
            reportFWUpdateThroughTwin(twin, {
              status: 'applyFailed',
              error: {
                code: err.error_code,
                message: err.error_message,
              }
            });
          } else { 
            reportFWUpdateThroughTwin(twin, {
              status: 'applyComplete',
              lastFirmwareUpdate: now.toISOString()
            });    
    
          }
        });
    
        setTimeout(callback, 4000);
    
      }, 4000);
    }
    ```

Stap 11: Voeg de volgende functie die verantwoordelijk is voor de **firmwareUpdate** directe methode en initieert de fasen firmware-update-proces:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond the cloud app for the direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response to method \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get the parameter from the body of the method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain the device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start the multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

Stap 12: Voeg de volgende code die is verbonden met uw IoT-hub:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect to IotHub client');
      }  else {
        console.log('Client connected to IoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 