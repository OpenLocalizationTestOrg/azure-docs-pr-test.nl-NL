## <a name="specify-hello-behavior-of-hello-iot-device"></a>Geef gedrag op Hallo van Hallo IoT-apparaat

Hallo clientbibliotheek van IoT Hub serialisatiefunctie gebruikt een model toospecify Hallo Hallo berichten Hallo apparaat uitwisselingen met IoT Hub.

1. Hallo variabelendeclaraties volgen na Hallo toevoegen `#include` instructies. Vervang de waarden van de tijdelijke aanduiding Hallo [apparaat-Id] en [apparaatsleutel] met waarden die u voor uw apparaat in Hallo dashboard externe controle oplossing hebt genoteerd. Hallo IoT Hub-hostnaam van Hallo oplossing dashboard tooreplace [IoTHub Name] gebruiken. Als uw IoT Hub-hostnaam bijvoorbeeld **contoso.azure devices.net** is, vervangt u [IoTHub-naam] door **contoso**:
   
    ```c
    static const char* deviceId = "[Device Id]";
    static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
    ```

1. Voeg Hallo code toodefine Hallo model waarmee Hallo apparaat toocommunicate met IoT Hub te volgen. Dit model geeft aan dat het Hallo-apparaat:

   - Temperatuur, externe temperatuur, vochtigheid en een apparaat-id als telemetrie kan verzenden.
   - Kan metagegevens over Hallo apparaat tooIoT Hub verzenden. Hallo apparaat verzendt basismetagegevens een **DeviceInfo** object tijdens het opstarten.
   - Kan verzenden gemelde eigenschappen toohello apparaat twin in IoT-Hub. Deze gerapporteerde eigenschappen zijn gegroepeerd in configuratie-, apparaat- en systeemeigenschappen.
   - Kan ontvangen van en reageren op de gewenste eigenschappen instellen in Hallo apparaat twin in IoT-Hub.
   - Kan reageren toohello **opnieuw opstarten** en **InitiateFirmwareUpdate** methoden aangeroepen via de portal van de oplossing Hallo direct. Hallo apparaat verzendt informatie over Hallo rechtstreekse methoden ondersteunt met behulp van gerapporteerde eigenschappen.
   
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

## <a name="implement-hello-behavior-of-hello-device"></a>Hallo-gedrag van Hallo-apparaat implementeren
Voeg nu code Hallo gedrag in Hallo model gedefinieerd implementeert.

1. Hallo functies dat gewenst Hallo-eigenschappen instellen in het dashboard van de oplossing Hallo verwerken na toevoegen. Deze gewenste eigenschappen zijn gedefinieerd in Hallo model:

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

1. Hallo functies waarmee Hallo rechtstreekse methoden aangeroepen via Hallo iothub worden verwerkt na toevoegen. Deze rechtstreekse methoden zijn gedefinieerd in Hallo model:

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

1. Hallo volgen functie die u een bericht toohello vooraf geconfigureerde oplossing verzendt toevoegen:
   
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

1. Voeg Hallo retouraanroep-handler die wordt uitgevoerd wanneer het Hallo-apparaat heeft verzonden nieuwe gemelde eigenschapswaarden toohello vooraf geconfigureerde oplossing te volgen:

    ```c
    /* Callback after sending reported properties */
    void deviceTwinCallback(int status_code, void* userContextCallback)
    {
      (void)(userContextCallback);
      printf("IoTHub: reported properties delivered with status_code = %u\n", status_code);
    }
    ```

1. Hallo volgende tooconnect werken uw apparaat toohello vooraf geconfigureerde oplossing in de cloud Hallo en uitwisselen van gegevens toevoegen. Deze functie voert Hallo stappen te volgen:

    - Initialiseert Hallo-platform.
    - Registreert Hallo Contoso naamruimte met Hallo serialisatie-bibliotheek.
    - Initialiseert Hallo-client met verbindingsreeks Hallo-apparaat.
    - Maak een instantie van Hallo **thermostaat** model.
    - Maakt en verzendt gerapporteerde eigenschapswaarden.
    - Verzendt een **DeviceInfo**-object.
    - Maakt een lus toosend telemetrie per seconde.
    - Deïnitialiseert alle resources.

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
   
    Ter referentie: Hier volgt een voorbeeld **telemetrie** verzonden bericht toohello vooraf geconfigureerde oplossing:
   
    ```
    {"DeviceId":"mydevice01", "Temperature":50, "Humidity":50, "ExternalTemperature":55}
    ```