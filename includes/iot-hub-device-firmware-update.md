## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b575d-101">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="b575d-101">Create a simulated device app</span></span>
<span data-ttu-id="b575d-102">In deze sectie doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="b575d-102">In this section, you:</span></span>

* <span data-ttu-id="b575d-103">U maakt een Node.js-console-app die reageert op een directe methode die door de cloud wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b575d-103">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="b575d-104">U activeert een gesimuleerde firmware-update.</span><span class="sxs-lookup"><span data-stu-id="b575d-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="b575d-105">U gebruikt de gerapporteerde eigenschappen om apparaatdubbelquery's in te schakelen die de apparaten identificeren en vaststellen wanneer er voor het laatst een firmware-update op deze apparaten is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b575d-105">Use the reported properties to enable device twin queries to identify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="b575d-106">Stap 1: Maak een lege map genaamd **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="b575d-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="b575d-107">Maak in de map **simulateddevice** een bestand met de naam package.json door achter de opdrachtprompt de volgende opdracht op te geven.</span><span class="sxs-lookup"><span data-stu-id="b575d-107">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="b575d-108">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="b575d-108">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="b575d-109">Stap 2: bij de opdrachtprompt in de **manageddevice** map, voer de volgende opdracht voor het installeren van de **azure-iot-device** en **azure-iot-device-mqtt** apparaat-SDK pakketten:</span><span class="sxs-lookup"><span data-stu-id="b575d-109">Step 2: At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="b575d-110">Stap 3: Gebruik een teksteditor, maak een **dmpatterns_fwupdate_device.js** bestand de **manageddevice** map.</span><span class="sxs-lookup"><span data-stu-id="b575d-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in the **manageddevice** folder.</span></span>

<span data-ttu-id="b575d-111">Stap 4: Voeg de volgende 'vereist' instructies aan het begin van de **dmpatterns_fwupdate_device.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="b575d-111">Step 4: Add the following 'require' statements at the start of the **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="b575d-112">Stap 5: Voeg een **connectionString** variabele en deze gebruiken voor het maken een **Client** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b575d-112">Step 5: Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="b575d-113">Vervang de tijdelijke aanduiding `{yourdeviceconnectionstring}` door de verbindingsreeks die u eerder hebt genoteerd in de sectie Een apparaat-id maken:</span><span class="sxs-lookup"><span data-stu-id="b575d-113">Replace the `{yourdeviceconnectionstring}` placeholder with the connection string you previously made a note of in the "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="b575d-114">Stap 6: Voeg de volgende functie die wordt gebruikt voor het bijwerken van de gerapporteerde eigenschappen toe:</span><span class="sxs-lookup"><span data-stu-id="b575d-114">Step 6: Add the following function that is used to update reported properties:</span></span>
   
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

<span data-ttu-id="b575d-115">Stap 7: Voeg de volgende functies die simuleren downloaden en de firmware-installatiekopie toe te passen:</span><span class="sxs-lookup"><span data-stu-id="b575d-115">Step 7: Add the following functions that simulate downloading and applying the firmware image:</span></span>
   
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

<span data-ttu-id="b575d-116">Stap 8: Voeg de volgende functie die de status van de firmware bijwerken via de gerapporteerde eigenschappen naar wordt **wachten**.</span><span class="sxs-lookup"><span data-stu-id="b575d-116">Step 8: Add the following function that updates the firmware update status through the reported properties to **waiting**.</span></span> <span data-ttu-id="b575d-117">Normaal gesproken worden apparaten op de hoogte gesteld van een beschikbare update, waarna een door de beheerder gedefinieerd beleid ervoor zorgt dat het apparaat de update downloadt en toepast.</span><span class="sxs-lookup"><span data-stu-id="b575d-117">Typically, devices are informed of an available update and an administrator defined policy causes the device to start downloading and applying the update.</span></span> <span data-ttu-id="b575d-118">In deze functie moet de logica voor het inschakelen van dat beleid worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b575d-118">This function is where the logic to enable that policy should run.</span></span> <span data-ttu-id="b575d-119">Voor het gemak wacht de steekproef vier seconden voordat u de firmware-installatiekopie te downloaden:</span><span class="sxs-lookup"><span data-stu-id="b575d-119">For simplicity, the sample waits for four seconds before proceeding to download the firmware image:</span></span>
   
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

<span data-ttu-id="b575d-120">Stap 9: Voeg de volgende functie die de status van de firmware bijwerken via de gerapporteerde eigenschappen naar wordt **downloaden**.</span><span class="sxs-lookup"><span data-stu-id="b575d-120">Step 9: Add the following function that updates the firmware update status through the reported properties to **downloading**.</span></span> <span data-ttu-id="b575d-121">De functie simuleert vervolgens het downloaden van de firmware, waarna de updatestatus van de firmware wordt gewijzigd in **downloadFailed** of **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="b575d-121">The function then simulates a firmware download and finally updates the firmware update status to either **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="b575d-122">Stap 10: Voeg de volgende functie die de status van de firmware bijwerken via de gerapporteerde eigenschappen naar wordt **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="b575d-122">Step 10: Add the following function that updates the firmware update status through the reported properties to **applying**.</span></span> <span data-ttu-id="b575d-123">De functie simuleert vervolgens het toepassen van de firmware, waarna de updatestatus van de firmware wordt gewijzigd in **applyFailed** of **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="b575d-123">The function then simulates applying the firmware image and finally updates the firmware update status to either **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="b575d-124">Stap 11: Voeg de volgende functie die verantwoordelijk is voor de **firmwareUpdate** directe methode en initieert de fasen firmware-update-proces:</span><span class="sxs-lookup"><span data-stu-id="b575d-124">Step 11: Add the following function that handles the **firmwareUpdate** direct method and initiates the multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="b575d-125">Stap 12: Voeg de volgende code die is verbonden met uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="b575d-125">Step 12: Finally, add the following code that connects to your IoT hub:</span></span>
    
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
> <span data-ttu-id="b575d-126">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b575d-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b575d-127">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="b575d-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 