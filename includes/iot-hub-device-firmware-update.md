## <a name="create-a-simulated-device-app"></a><span data-ttu-id="083ef-101">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="083ef-101">Create a simulated device app</span></span>
<span data-ttu-id="083ef-102">In deze sectie doet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="083ef-102">In this section, you:</span></span>

* <span data-ttu-id="083ef-103">Een Node.js-consoletoepassing die tooa directe methode aangeroepen door Hallo cloud reageert maken</span><span class="sxs-lookup"><span data-stu-id="083ef-103">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="083ef-104">U activeert een gesimuleerde firmware-update.</span><span class="sxs-lookup"><span data-stu-id="083ef-104">Trigger a simulated firmware update</span></span>
* <span data-ttu-id="083ef-105">Gebruik Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze een firmware-update voor het laatst hebt voltooid</span><span class="sxs-lookup"><span data-stu-id="083ef-105">Use hello reported properties tooenable device twin queries tooidentify devices and when they last completed a firmware update</span></span>

<span data-ttu-id="083ef-106">Stap 1: Maak een lege map genaamd **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="083ef-106">Step 1: Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="083ef-107">In Hallo **manageddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="083ef-107">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="083ef-108">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="083ef-108">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```

<span data-ttu-id="083ef-109">Stap 2: bij de opdrachtprompt in Hallo **manageddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt** apparaat SDK-pakketten:</span><span class="sxs-lookup"><span data-stu-id="083ef-109">Step 2: At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

<span data-ttu-id="083ef-110">Stap 3: Gebruik een teksteditor, maak een **dmpatterns_fwupdate_device.js** bestand in Hallo **manageddevice** map.</span><span class="sxs-lookup"><span data-stu-id="083ef-110">Step 3: Using a text editor, create a **dmpatterns_fwupdate_device.js** file in hello **manageddevice** folder.</span></span>

<span data-ttu-id="083ef-111">Stap 4: Toevoegen Hallo volgende 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_fwupdate_device.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="083ef-111">Step 4: Add hello following 'require' statements at hello start of hello **dmpatterns_fwupdate_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
<span data-ttu-id="083ef-112">Stap 5: Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="083ef-112">Step 5: Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="083ef-113">Vervang Hallo `{yourdeviceconnectionstring}` tijdelijke aanduiding met Hallo-verbindingsreeks die u eerder hebt genoteerd in het gedeelte voor Hallo 'Een apparaat-id maken' eerder:</span><span class="sxs-lookup"><span data-stu-id="083ef-113">Replace hello `{yourdeviceconnectionstring}` placeholder with hello connection string you previously made a note of in hello "Create a device identity" section previously:</span></span>
   
    ```
    var connectionString = '{yourdeviceconnectionstring}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

<span data-ttu-id="083ef-114">Stap 6: Voeg Hallo volgende functie die is gebruikt tooupdate gerapporteerd eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="083ef-114">Step 6: Add hello following function that is used tooupdate reported properties:</span></span>
   
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

<span data-ttu-id="083ef-115">Stap 7: Toevoegen Hallo na functies die simuleren downloaden en Hallo firmware-installatiekopie toe te passen:</span><span class="sxs-lookup"><span data-stu-id="083ef-115">Step 7: Add hello following functions that simulate downloading and applying hello firmware image:</span></span>
   
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

<span data-ttu-id="083ef-116">Stap 8: Hallo volgen dat updates Hallo firmware-updatestatus via Hallo eigenschappen te gerapporteerd functie toevoegen**wachten**.</span><span class="sxs-lookup"><span data-stu-id="083ef-116">Step 8: Add hello following function that updates hello firmware update status through hello reported properties too**waiting**.</span></span> <span data-ttu-id="083ef-117">Normaal gesproken apparaten op de hoogte zijn van een update beschikbaar en een beheerder gedefinieerd beleid zorgt ervoor dat Hallo apparaat toostart downloaden en toepassen van de Hallo-update.</span><span class="sxs-lookup"><span data-stu-id="083ef-117">Typically, devices are informed of an available update and an administrator defined policy causes hello device toostart downloading and applying hello update.</span></span> <span data-ttu-id="083ef-118">Deze functie is waar Hallo logica tooenable die beleid moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="083ef-118">This function is where hello logic tooenable that policy should run.</span></span> <span data-ttu-id="083ef-119">Voor het gemak wacht Hallo voorbeeld tot vier seconden voordat u doorgaat toodownload Hallo firmware-image:</span><span class="sxs-lookup"><span data-stu-id="083ef-119">For simplicity, hello sample waits for four seconds before proceeding toodownload hello firmware image:</span></span>
   
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

<span data-ttu-id="083ef-120">Stap 9: Toevoegen Hallo volgen functie dat updates Hallo firmware-updatestatus via Hallo eigenschappen te gerapporteerd**downloaden**.</span><span class="sxs-lookup"><span data-stu-id="083ef-120">Step 9: Add hello following function that updates hello firmware update status through hello reported properties too**downloading**.</span></span> <span data-ttu-id="083ef-121">Hallo functie vervolgens simuleert een download van de firmware en ten slotte updates firmware-update status tooeither Hallo **downloadFailed** of **downloadComplete**:</span><span class="sxs-lookup"><span data-stu-id="083ef-121">hello function then simulates a firmware download and finally updates hello firmware update status tooeither **downloadFailed** or **downloadComplete**:</span></span>
   
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

<span data-ttu-id="083ef-122">Stap 10: Hallo volgen dat updates Hallo firmware-updatestatus via Hallo eigenschappen te gerapporteerd functie toevoegen**toepassen**.</span><span class="sxs-lookup"><span data-stu-id="083ef-122">Step 10: Add hello following function that updates hello firmware update status through hello reported properties too**applying**.</span></span> <span data-ttu-id="083ef-123">Hallo functie vervolgens simuleert toepassen Hallo firmware-image en ten slotte updates firmware-update status tooeither Hallo **applyFailed** of **applyComplete**:</span><span class="sxs-lookup"><span data-stu-id="083ef-123">hello function then simulates applying hello firmware image and finally updates hello firmware update status tooeither **applyFailed** or **applyComplete**:</span></span>
    
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

<span data-ttu-id="083ef-124">Stap 11: Toevoegen Hallo volgende werken dat Hallo ingangen **firmwareUpdate** directe methode en initieert Hallo fasen firmware proces niet bijwerken:</span><span class="sxs-lookup"><span data-stu-id="083ef-124">Step 11: Add hello following function that handles hello **firmwareUpdate** direct method and initiates hello multi-stage firmware update process:</span></span>
    
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

<span data-ttu-id="083ef-125">Stap 12: Voeg Hallo code die verbinding tooyour IoT-hub maakt te volgen:</span><span class="sxs-lookup"><span data-stu-id="083ef-125">Step 12: Finally, add hello following code that connects tooyour IoT hub:</span></span>
    
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
> <span data-ttu-id="083ef-126">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="083ef-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="083ef-127">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout](https://msdn.microsoft.com/library/hh675232.aspx).</span><span class="sxs-lookup"><span data-stu-id="083ef-127">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling](https://msdn.microsoft.com/library/hh675232.aspx).</span></span>
> 
> 