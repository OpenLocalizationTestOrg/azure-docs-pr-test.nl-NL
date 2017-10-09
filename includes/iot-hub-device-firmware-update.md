## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie doet u het volgende:

* Een Node.js-consoletoepassing die tooa directe methode aangeroepen door Hallo cloud reageert maken
* U activeert een gesimuleerde firmware-update.
* Gebruik Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze een firmware-update voor het laatst hebt voltooid

Stap 1: Maak een lege map genaamd **manageddevice**.  In Hallo **manageddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```

Stap 2: bij de opdrachtprompt in Hallo **manageddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt** apparaat SDK-pakketten:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

Stap 3: Gebruik een teksteditor, maak een **dmpatterns_fwupdate_device.js** bestand in Hallo **manageddevice** map.

Stap 4: Toevoegen Hallo volgende 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_fwupdate_device.js** bestand:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
Stap 5: Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar. Vervang Hallo `{yourdeviceconnectionstring}` tijdelijke aanduiding met Hallo-verbindingsreeks die u eerder hebt genoteerd in het gedeelte voor Hallo 'Een apparaat-id maken' eerder:
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

Stap 6: Voeg Hallo volgende functie die is gebruikt tooupdate gerapporteerd eigenschappen:
   
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

Stap 7: Toevoegen Hallo na functies die simuleren downloaden en Hallo firmware-installatiekopie toe te passen:
   
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

Stap 8: Hallo volgen dat updates Hallo firmware-updatestatus via Hallo eigenschappen te gerapporteerd functie toevoegen**wachten**. Normaal gesproken apparaten op de hoogte zijn van een update beschikbaar en een beheerder gedefinieerd beleid zorgt ervoor dat Hallo apparaat toostart downloaden en toepassen van de Hallo-update. Deze functie is waar Hallo logica tooenable die beleid moet worden uitgevoerd. Voor het gemak wacht Hallo voorbeeld tot vier seconden voordat u doorgaat toodownload Hallo firmware-image:
   
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

Stap 9: Toevoegen Hallo volgen functie dat updates Hallo firmware-updatestatus via Hallo eigenschappen te gerapporteerd**downloaden**. Hallo functie vervolgens simuleert een download van de firmware en ten slotte updates firmware-update status tooeither Hallo **downloadFailed** of **downloadComplete**:
   
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

Stap 10: Hallo volgen dat updates Hallo firmware-updatestatus via Hallo eigenschappen te gerapporteerd functie toevoegen**toepassen**. Hallo functie vervolgens simuleert toepassen Hallo firmware-image en ten slotte updates firmware-update status tooeither Hallo **applyFailed** of **applyComplete**:
    
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

Stap 11: Toevoegen Hallo volgende werken dat Hallo ingangen **firmwareUpdate** directe methode en initieert Hallo fasen firmware proces niet bijwerken:
    
    ```
    var onFirmwareUpdate = function(request, response) {
    
      // Respond hello cloud app for hello direct method
      response.send(200, 'FirmwareUpdate started', function(err) {
        if (!err) {
          console.error('An error occured when sending a method response:\n' + err.toString());
        } else {
          console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
        }
      });
    
      // Get hello parameter from hello body of hello method request
      var fwPackageUri = request.payload.fwPackageUri;
    
      // Obtain hello device twin
      client.getTwin(function(err, twin) {
        if (err) {
          console.error('Could not get device twin.');
        } else {
          console.log('Device twin acquired.');
    
          // Start hello multi-stage firmware update
          waitToDownload(twin, fwPackageUri, function() {
            downloadImage(twin, fwPackageUri, function(imageData) {
              applyImage(twin, imageData, function() {});    
            });  
          });
    
        }
      });
    }
    ```

Stap 12: Voeg Hallo code die verbinding tooyour IoT-hub maakt te volgen:
    
    ```
    client.open(function(err) {
      if (err) {
        console.error('Could not connect tooIotHub client');
      }  else {
        console.log('Client connected tooIoT Hub.  Waiting for firmwareUpdate direct method.');
      }
    
      client.onDeviceMethod('firmwareUpdate', onFirmwareUpdate);
    });
    ```

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout](https://msdn.microsoft.com/library/hh675232.aspx).
> 
> 