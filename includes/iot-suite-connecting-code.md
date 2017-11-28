## <a name="specify-the-behavior-of-the-iot-device"></a><span data-ttu-id="0c063-101">Het gedrag van het IoT-apparaat opgeven</span><span class="sxs-lookup"><span data-stu-id="0c063-101">Specify the behavior of the IoT device</span></span>

<span data-ttu-id="0c063-102">De clientbibliotheek van de IoT Hub-serialisatiefunctie maakt gebruik van een model om de opmaak op te geven van de berichten die het apparaat uitwisselt met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="0c063-102">The IoT Hub serializer client library uses a model to specify the format of the messages the device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="0c063-103">Voeg de volgende variabelendeclaraties achter de `#include`-instructies toe.</span><span class="sxs-lookup"><span data-stu-id="0c063-103">Add the following variable declarations after the `#include` statements.</span></span> <span data-ttu-id="0c063-104">Vervang de waarden van de tijdelijke aanduidingen [apparaat-id] en [apparaatsleutel] door de waarden die u voor het apparaat hebt genoteerd in het dashboard van de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="0c063-104">Replace the placeholder values [Device Id] and [Device Key] with values you noted for your device in the remote monitoring solution dashboard.</span></span> <span data-ttu-id="0c063-105">Gebruik de hostnaam van de IoT Hub uit het oplossingsdashboard om [IoTHub-naam] te vervangen.</span><span class="sxs-lookup"><span data-stu-id="0c063-105">Use the IoT Hub Hostname from the solution dashboard to replace [IoTHub Name].</span></span> <span data-ttu-id="0c063-106">Als uw IoT Hub-hostnaam bijvoorbeeld **contoso.azure devices.net** is, vervangt u [IoTHub-naam] door **contoso**:</span><span class="sxs-lookup"><span data-stu-id="0c063-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="0c063-107">Voeg de volgende code toe om het model te definiëren dat het apparaat in staat stelt om met IoT Hub te communiceren.</span><span class="sxs-lookup"><span data-stu-id="0c063-107">Add the following code to define the model that enables the device to communicate with IoT Hub.</span></span> <span data-ttu-id="0c063-108">Dit model bepaalt dat het apparaat:</span><span class="sxs-lookup"><span data-stu-id="0c063-108">This model specifies that the device:</span></span>

   - <span data-ttu-id="0c063-109">Temperatuur, externe temperatuur, vochtigheid en een apparaat-id als telemetrie kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="0c063-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="0c063-110">Metagegevens over het apparaat naar IoT Hub kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="0c063-110">Can send metadata about the device to IoT Hub.</span></span> <span data-ttu-id="0c063-111">Het apparaat verzendt bij het opstarten basismetagegevens in een **DeviceInfo**-object.</span><span class="sxs-lookup"><span data-stu-id="0c063-111">The device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="0c063-112">Gerapporteerde eigenschappen naar de apparaatdubbel in IoT Hub kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="0c063-112">Can send reported properties, to the device twin in IoT Hub.</span></span> <span data-ttu-id="0c063-113">Deze gerapporteerde eigenschappen zijn gegroepeerd in configuratie-, apparaat- en systeemeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0c063-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="0c063-114">Gewenste eigenschappen die in de apparaatdubbel in IoT Hub zijn ingesteld, kan ontvangen en hierop kan reageren.</span><span class="sxs-lookup"><span data-stu-id="0c063-114">Can receive and act on desired properties set in the device twin in IoT Hub.</span></span>
   - <span data-ttu-id="0c063-115">Kan reageren op de directe methoden **Reboot** en **InitiateFirmwareUpdate** die via de oplossingsportal worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0c063-115">Can respond to the **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through the solution portal.</span></span> <span data-ttu-id="0c063-116">Met behulp van gerapporteerde eigenschappen stuurt het apparaat informatie over de ondersteunde directe methoden.</span><span class="sxs-lookup"><span data-stu-id="0c063-116">The device sends information about the direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define the Model
    BEGIN_NAMESPACE(Contoso);

    /* Reported properties */
    DECLARE_STRUCT(SystemProperties,
      ascii_char_ptr, Manufacturer,
      ascii_char_ptr, FirmwareVersion,
      ascii_char_ptr, InstalledRAM,
      ascii_char_ptr, ModelNumber,
      ascii_char_ptr, Platform,
      ascii_char_ptr, Processor,
      ascii_char_ptr, SerialNumber
    );

    DECLARE_STRUCT(LocationProperties,
      double, Latitude,
      double, Longitude
    );

    DECLARE_STRUCT(ReportedDeviceProperties,
      ascii_char_ptr, DeviceState,
      LocationProperties, Location
    );

    DECLARE_MODEL(ConfigProperties,
      WITH_REPORTED_PROPERTY(double, TemperatureMeanValue),
      WITH_REPORTED_PROPERTY(uint8_t, TelemetryInterval)
    );

    /* Part of DeviceInfo */
    DECLARE_STRUCT(DeviceProperties,
      ascii_char_ptr, DeviceID,
      _Bool, HubEnabledState
    );

    DECLARE_DEVICETWIN_MODEL(Thermostat,
      /* Telemetry (temperature, external temperature and humidity) */
      WITH_DATA(double, Temperature),
      WITH_DATA(double, ExternalTemperature),
      WITH_DATA(double, Humidity),
      WITH_DATA(ascii_char_ptr, DeviceId),

      /* DeviceInfo */
      WITH_DATA(ascii_char_ptr, ObjectType),
      WITH_DATA(_Bool, IsSimulatedDevice),
      WITH_DATA(ascii_char_ptr, Version),
      WITH_DATA(DeviceProperties, DeviceProperties),

      /* Device twin properties */
      WITH_REPORTED_PROPERTY(ReportedDeviceProperties, Device),
      WITH_REPORTED_PROPERTY(ConfigProperties, Config),
      WITH_REPORTED_PROPERTY(SystemProperties, System),

      WITH_DESIRED_PROPERTY(double, TemperatureMeanValue, onDesiredTemperatureMeanValue),
      WITH_DESIRED_PROPERTY(uint8_t, TelemetryInterval, onDesiredTelemetryInterval),

      /* Direct methods implemented by the device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-the-behavior-of-the-device"></a><span data-ttu-id="0c063-117">Het gedrag van het apparaat implementeren</span><span class="sxs-lookup"><span data-stu-id="0c063-117">Implement the behavior of the device</span></span>
<span data-ttu-id="0c063-118">Voeg nu code toe om het gedrag te implementeren dat in het model is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0c063-118">Now add code that implements the behavior defined in the model.</span></span>

1. <span data-ttu-id="0c063-119">Voeg de volgende functies toe die de gewenste eigenschappen verwerken die in het oplossingsdashboard zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0c063-119">Add the following functions that handle the desired properties set in the solution dashboard.</span></span> <span data-ttu-id="0c063-120">De volgende gewenste eigenschappen zijn in het model gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="0c063-120">These desired properties are defined in the model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of the type of the MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of the type of the MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="0c063-121">Voeg de volgende functies toe die de directe methoden verwerken die via de IoT Hub worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="0c063-121">Add the following functions that handle the direct methods invoked through the IoT hub.</span></span> <span data-ttu-id="0c063-122">De volgende directe methoden zijn in het model gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="0c063-122">These direct methods are defined in the model:</span></span>

    ```c
    /* Handlers for direct methods */
    METHODRETURN_HANDLE Reboot(Thermostat* thermostat)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Rebooting\"");
      printf("Received reboot request\r\n");
      return result;
    }

    METHODRETURN_HANDLE InitiateFirmwareUpdate(Thermostat* thermostat, ascii_char_ptr FwPackageURI)
    {
      (void)(thermostat);

      METHODRETURN_HANDLE result = MethodReturn_Create(201, "\"Initiating Firmware Update\"");
      printf("Recieved firmware update request. Use package at: %s\r\n", FwPackageURI);
      return result;
    }
    ```

1. <span data-ttu-id="0c063-123">Voeg de volgende functie toe die een bericht naar de vooraf geconfigureerde oplossing verzendt:</span><span class="sxs-lookup"><span data-stu-id="0c063-123">Add the following function that sends a message to the preconfigured solution:</span></span>
   
    ```c
    /* Send data to IoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable to create a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted the message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="0c063-124">Voeg de volgende callbackhandler toe die wordt uitgevoerd wanneer het apparaat nieuwe gerapporteerde eigenschapswaarden naar de vooraf geconfigureerde oplossing heeft verzonden:</span><span class="sxs-lookup"><span data-stu-id="0c063-124">Add the following callback handler that runs when the device has sent new reported property values to the preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="0c063-125">Voeg de volgende functie toe om het apparaat te verbinden met de vooraf geconfigureerde oplossing in de cloud, en gegevens uit te wisselen.</span><span class="sxs-lookup"><span data-stu-id="0c063-125">Add the following function to connect your device to the preconfigured solution in the cloud, and exchange data.</span></span> <span data-ttu-id="0c063-126">Deze functie voert de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="0c063-126">This function performs the following steps:</span></span>

    - <span data-ttu-id="0c063-127">Initialiseert het platform.</span><span class="sxs-lookup"><span data-stu-id="0c063-127">Initializes the platform.</span></span>
    - <span data-ttu-id="0c063-128">Registreert de Contoso-naamruimte bij de serialisatiebibliotheek.</span><span class="sxs-lookup"><span data-stu-id="0c063-128">Registers the Contoso namespace with the serialization library.</span></span>
    - <span data-ttu-id="0c063-129">Initialiseert de client met de verbindingsreeks van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="0c063-129">Initializes the client with the device connection string.</span></span>
    - <span data-ttu-id="0c063-130">Maakt een exemplaar van het **thermostaat**model.</span><span class="sxs-lookup"><span data-stu-id="0c063-130">Create an instance of the **Thermostat** model.</span></span>
    - <span data-ttu-id="0c063-131">Maakt en verzendt gerapporteerde eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="0c063-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="0c063-132">Verzendt een **DeviceInfo**-object.</span><span class="sxs-lookup"><span data-stu-id="0c063-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="0c063-133">Maakt een lus om elke seconde telemetrie te verzenden.</span><span class="sxs-lookup"><span data-stu-id="0c063-133">Creates a loop to send telemetry every second.</span></span>
    - <span data-ttu-id="0c063-134">Deïnitialiseert alle resources.</span><span class="sxs-lookup"><span data-stu-id="0c063-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed to initialize the platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable to SERIALIZER_REGISTER_NAMESPACE\n");
          }
          else
          {
            IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, MQTT_Protocol);
            if (iotHubClientHandle == NULL)
            {
              printf("Failure in IoTHubClient_CreateFromConnectionString\n");
            }
            else
            {
      #ifdef MBED_BUILD_TIMESTAMP
              // For mbed add the certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed to set option \"TrustedCerts\"\n");
              }
      #endif // MBED_BUILD_TIMESTAMP
              Thermostat* thermostat = IoTHubDeviceTwin_CreateThermostat(iotHubClientHandle);
              if (thermostat == NULL)
              {
                printf("Failure in IoTHubDeviceTwin_CreateThermostat\n");
              }
              else
              {
                /* Set values for reported properties */
                thermostat->Config.TemperatureMeanValue = 55.5;
                thermostat->Config.TelemetryInterval = 3;
                thermostat->Device.DeviceState = "normal";
                thermostat->Device.Location.Latitude = 47.642877;
                thermostat->Device.Location.Longitude = -122.125497;
                thermostat->System.Manufacturer = "Contoso Inc.";
                thermostat->System.FirmwareVersion = "2.22";
                thermostat->System.InstalledRAM = "8 MB";
                thermostat->System.ModelNumber = "DB-14";
                thermostat->System.Platform = "Plat 9.75";
                thermostat->System.Processor = "i3-7";
                thermostat->System.SerialNumber = "SER21";
                /* Specify the signatures of the supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot the device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI to specifiy the URI of the firmware file\"}";

                /* Send reported properties to IoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object to IoT Hub at startup\n");
      
                  thermostat->ObjectType = "DeviceInfo";
                  thermostat->IsSimulatedDevice = 0;
                  thermostat->Version = "1.0";
                  thermostat->DeviceProperties.HubEnabledState = 1;
                  thermostat->DeviceProperties.DeviceID = (char*)deviceId;

                  unsigned char* buffer;
                  size_t bufferSize;

                  if (SERIALIZE(&buffer, &bufferSize, thermostat->ObjectType, thermostat->Version, thermostat->IsSimulatedDevice, thermostat->DeviceProperties) != CODEFIRST_OK)
                  {
                    (void)printf("Failed serializing DeviceInfo\n");
                  }
                  else
                  {
                    sendMessage(iotHubClientHandle, buffer, bufferSize);
                  }

                  /* Send telemetry */
                  thermostat->Temperature = 50;
                  thermostat->ExternalTemperature = 55;
                  thermostat->Humidity = 50;
                  thermostat->DeviceId = (char*)deviceId;

                  while (1)
                  {
                    unsigned char*buffer;
                    size_t bufferSize;

                    (void)printf("Sending sensor value Temperature = %f, Humidity = %f\n", thermostat->Temperature, thermostat->Humidity);

                    if (SERIALIZE(&buffer, &bufferSize, thermostat->DeviceId, thermostat->Temperature, thermostat->Humidity, thermostat->ExternalTemperature) != CODEFIRST_OK)
                    {
                      (void)printf("Failed sending sensor value\r\n");
                    }
                    else
                    {
                      sendMessage(iotHubClientHandle, buffer, bufferSize);
                    }

                    ThreadAPI_Sleep(1000);
                  }

                  IoTHubDeviceTwin_DestroyThermostat(thermostat);
                }
              }
              IoTHubClient_Destroy(iotHubClientHandle);
            }
            serializer_deinit();
          }
        }
        platform_deinit();
      }
    ```
   
    <span data-ttu-id="0c063-135">Ter referentie volgt hier een voorbeeld van een **telemetrie**bericht dat naar de vooraf geconfigureerde oplossing is verzonden:</span><span class="sxs-lookup"><span data-stu-id="0c063-135">For reference, here is a sample **Telemetry** message sent to the preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```