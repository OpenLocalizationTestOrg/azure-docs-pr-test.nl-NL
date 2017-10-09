## <a name="specify-hello-behavior-of-hello-iot-device"></a><span data-ttu-id="fbede-101">Geef gedrag op Hallo van Hallo IoT-apparaat</span><span class="sxs-lookup"><span data-stu-id="fbede-101">Specify hello behavior of hello IoT device</span></span>

<span data-ttu-id="fbede-102">Hallo clientbibliotheek van IoT Hub serialisatiefunctie gebruikt een model toospecify Hallo Hallo berichten Hallo apparaat uitwisselingen met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="fbede-102">hello IoT Hub serializer client library uses a model toospecify hello format of hello messages hello device exchanges with IoT Hub.</span></span>

1. <span data-ttu-id="fbede-103">Hallo variabelendeclaraties volgen na Hallo toevoegen `#include` instructies.</span><span class="sxs-lookup"><span data-stu-id="fbede-103">Add hello following variable declarations after hello `#include` statements.</span></span> <span data-ttu-id="fbede-104">Vervang de waarden van de tijdelijke aanduiding Hallo [apparaat-Id] en [apparaatsleutel] met waarden die u voor uw apparaat in Hallo dashboard externe controle oplossing hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="fbede-104">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="fbede-105">Hallo IoT Hub-hostnaam van Hallo oplossing dashboard tooreplace [IoTHub Name] gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fbede-105">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="fbede-106">Als uw IoT Hub-hostnaam bijvoorbeeld **contoso.azure devices.net** is, vervangt u [IoTHub-naam] door **contoso**:</span><span class="sxs-lookup"><span data-stu-id="fbede-106">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. <span data-ttu-id="fbede-107">Voeg Hallo code toodefine Hallo model waarmee Hallo apparaat toocommunicate met IoT Hub te volgen.</span><span class="sxs-lookup"><span data-stu-id="fbede-107">Add hello following code toodefine hello model that enables hello device toocommunicate with IoT Hub.</span></span> <span data-ttu-id="fbede-108">Dit model geeft aan dat het Hallo-apparaat:</span><span class="sxs-lookup"><span data-stu-id="fbede-108">This model specifies that hello device:</span></span>

   - <span data-ttu-id="fbede-109">Temperatuur, externe temperatuur, vochtigheid en een apparaat-id als telemetrie kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="fbede-109">Can send temperature, external temperature, humidity, and a device id as telemetry.</span></span>
   - <span data-ttu-id="fbede-110">Kan metagegevens over Hallo apparaat tooIoT Hub verzenden.</span><span class="sxs-lookup"><span data-stu-id="fbede-110">Can send metadata about hello device tooIoT Hub.</span></span> <span data-ttu-id="fbede-111">Hallo apparaat verzendt basismetagegevens een **DeviceInfo** object tijdens het opstarten.</span><span class="sxs-lookup"><span data-stu-id="fbede-111">hello device sends basic metadata in a **DeviceInfo** object at startup.</span></span>
   - <span data-ttu-id="fbede-112">Kan verzenden gemelde eigenschappen toohello apparaat twin in IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="fbede-112">Can send reported properties, toohello device twin in IoT Hub.</span></span> <span data-ttu-id="fbede-113">Deze gerapporteerde eigenschappen zijn gegroepeerd in configuratie-, apparaat- en systeemeigenschappen.</span><span class="sxs-lookup"><span data-stu-id="fbede-113">These reported properties are grouped into configuration, device, and system properties.</span></span>
   - <span data-ttu-id="fbede-114">Kan ontvangen van en reageren op de gewenste eigenschappen instellen in Hallo apparaat twin in IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="fbede-114">Can receive and act on desired properties set in hello device twin in IoT Hub.</span></span>
   - <span data-ttu-id="fbede-115">Kan reageren toohello **opnieuw opstarten** en **InitiateFirmwareUpdate** methoden aangeroepen via de portal van de oplossing Hallo direct.</span><span class="sxs-lookup"><span data-stu-id="fbede-115">Can respond toohello **Reboot** and **InitiateFirmwareUpdate** direct methods invoked through hello solution portal.</span></span> <span data-ttu-id="fbede-116">Hallo apparaat verzendt informatie over Hallo rechtstreekse methoden ondersteunt met behulp van gerapporteerde eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="fbede-116">hello device sends information about hello direct methods it supports using reported properties.</span></span>
   
    ```c
    // Define hello Model
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

      /* Direct methods implemented by hello device */
      WITH_METHOD(Reboot),
      WITH_METHOD(InitiateFirmwareUpdate, ascii_char_ptr, FwPackageURI),

      /* Register direct methods with solution portal */
      WITH_REPORTED_PROPERTY(ascii_char_ptr_no_quotes, SupportedMethods)
    );

    END_NAMESPACE(Contoso);
    ```

## <a name="implement-hello-behavior-of-hello-device"></a><span data-ttu-id="fbede-117">Hallo-gedrag van Hallo-apparaat implementeren</span><span class="sxs-lookup"><span data-stu-id="fbede-117">Implement hello behavior of hello device</span></span>
<span data-ttu-id="fbede-118">Voeg nu code Hallo gedrag in Hallo model gedefinieerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="fbede-118">Now add code that implements hello behavior defined in hello model.</span></span>

1. <span data-ttu-id="fbede-119">Hallo functies dat gewenst Hallo-eigenschappen instellen in het dashboard van de oplossing Hallo verwerken na toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fbede-119">Add hello following functions that handle hello desired properties set in hello solution dashboard.</span></span> <span data-ttu-id="fbede-120">Deze gewenste eigenschappen zijn gedefinieerd in Hallo model:</span><span class="sxs-lookup"><span data-stu-id="fbede-120">These desired properties are defined in hello model:</span></span>

    ```c
    void onDesiredTemperatureMeanValue(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TemperatureMeanValue = %f\r\n", thermostat->TemperatureMeanValue);

    }

    void onDesiredTelemetryInterval(void* argument)
    {
      /* By convention 'argument' is of hello type of hello MODEL */
      Thermostat* thermostat = argument;
      printf("Received a new desired_TelemetryInterval = %d\r\n", thermostat->TelemetryInterval);
    }
    ```

1. <span data-ttu-id="fbede-121">Hallo functies waarmee Hallo rechtstreekse methoden aangeroepen via Hallo iothub worden verwerkt na toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fbede-121">Add hello following functions that handle hello direct methods invoked through hello IoT hub.</span></span> <span data-ttu-id="fbede-122">Deze rechtstreekse methoden zijn gedefinieerd in Hallo model:</span><span class="sxs-lookup"><span data-stu-id="fbede-122">These direct methods are defined in hello model:</span></span>

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

1. <span data-ttu-id="fbede-123">Hallo volgen functie die u een bericht toohello vooraf geconfigureerde oplossing verzendt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="fbede-123">Add hello following function that sends a message toohello preconfigured solution:</span></span>
   
    ```c
    /* Send data tooIoT Hub */
    static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
    {
      IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
      if (messageHandle == NULL)
      {
        printf("unable toocreate a new IoTHubMessage\r\n");
      }
      else
      {
        if (IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, NULL, NULL) != IOTHUB_CLIENT_OK)
        {
          printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
          printf("IoTHubClient accepted hello message for delivery\r\n");
        }

        IoTHubMessage_Destroy(messageHandle);
      }
      free((void*)buffer);
    }
    ```

1. <span data-ttu-id="fbede-124">Voeg Hallo retouraanroep-handler die wordt uitgevoerd wanneer het Hallo-apparaat heeft verzonden nieuwe gemelde eigenschapswaarden toohello vooraf geconfigureerde oplossing te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbede-124">Add hello following callback handler that runs when hello device has sent new reported property values toohello preconfigured solution:</span></span>

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. <span data-ttu-id="fbede-125">Hallo volgende tooconnect werken uw apparaat toohello vooraf geconfigureerde oplossing in de cloud Hallo en uitwisselen van gegevens toevoegen.</span><span class="sxs-lookup"><span data-stu-id="fbede-125">Add hello following function tooconnect your device toohello preconfigured solution in hello cloud, and exchange data.</span></span> <span data-ttu-id="fbede-126">Deze functie voert Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="fbede-126">This function performs hello following steps:</span></span>

    - <span data-ttu-id="fbede-127">Initialiseert Hallo-platform.</span><span class="sxs-lookup"><span data-stu-id="fbede-127">Initializes hello platform.</span></span>
    - <span data-ttu-id="fbede-128">Registreert Hallo Contoso naamruimte met Hallo serialisatie-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="fbede-128">Registers hello Contoso namespace with hello serialization library.</span></span>
    - <span data-ttu-id="fbede-129">Initialiseert Hallo-client met verbindingsreeks Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="fbede-129">Initializes hello client with hello device connection string.</span></span>
    - <span data-ttu-id="fbede-130">Maak een instantie van Hallo **thermostaat** model.</span><span class="sxs-lookup"><span data-stu-id="fbede-130">Create an instance of hello **Thermostat** model.</span></span>
    - <span data-ttu-id="fbede-131">Maakt en verzendt gerapporteerde eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="fbede-131">Creates and sends reported property values.</span></span>
    - <span data-ttu-id="fbede-132">Verzendt een **DeviceInfo**-object.</span><span class="sxs-lookup"><span data-stu-id="fbede-132">Sends a **DeviceInfo** object.</span></span>
    - <span data-ttu-id="fbede-133">Maakt een lus toosend telemetrie per seconde.</span><span class="sxs-lookup"><span data-stu-id="fbede-133">Creates a loop toosend telemetry every second.</span></span>
    - <span data-ttu-id="fbede-134">Deïnitialiseert alle resources.</span><span class="sxs-lookup"><span data-stu-id="fbede-134">Deinitializes all resources.</span></span>

      ```c
      void remote_monitoring_run(void)
      {
        if (platform_init() != 0)
        {
          printf("Failed tooinitialize hello platform.\n");
        }
        else
        {
          if (SERIALIZER_REGISTER_NAMESPACE(Contoso) == NULL)
          {
            printf("Unable tooSERIALIZER_REGISTER_NAMESPACE\n");
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
              // For mbed add hello certificate information
              if (IoTHubClient_SetOption(iotHubClientHandle, "TrustedCerts", certificates) != IOTHUB_CLIENT_OK)
              {
                  printf("Failed tooset option \"TrustedCerts\"\n");
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
                /* Specify hello signatures of hello supported direct methods */
                thermostat->SupportedMethods = "{\"Reboot\": \"Reboot hello device\", \"InitiateFirmwareUpdate--FwPackageURI-string\": \"Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file\"}";

                /* Send reported properties tooIoT Hub */
                if (IoTHubDeviceTwin_SendReportedStateThermostat(thermostat, deviceTwinCallback, NULL) != IOTHUB_CLIENT_OK)
                {
                  printf("Failed sending serialized reported state\n");
                }
                else
                {
                  printf("Send DeviceInfo object tooIoT Hub at startup\n");
      
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
   
    <span data-ttu-id="fbede-135">Ter referentie: Hier volgt een voorbeeld **telemetrie** verzonden bericht toohello vooraf geconfigureerde oplossing:</span><span class="sxs-lookup"><span data-stu-id="fbede-135">For reference, here is a sample **Telemetry** message sent toohello preconfigured solution:</span></span>
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```