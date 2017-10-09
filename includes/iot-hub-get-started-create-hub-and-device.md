## <a name="create-an-iot-hub"></a>Een IoT Hub maken

1. In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Internet der dingen** > **IoT Hub**.

   ![Maken van een IoT-hub in hello Azure-portal](../articles/iot-hub/media/iot-hub-create-hub-and-device/1_create-azure-iot-hub-portal.png)
2. In Hallo **IoT-hub** deelvenster Voer Hallo-informatie voor uw IoT-hub te volgen:

     **Naam**: Hallo-naam van uw IoT-hub invoeren. Als Hallo-naam die u invoert geldig is, wordt er een groen vinkje weergegeven.

     **Prijs-en schaal**: Selecteer Hallo **F1 - vrije** laag. Deze optie is voldoende voor deze demo. Zie voor meer informatie, Hallo [prijs-en schaalniveau](https://azure.microsoft.com/pricing/details/iot-hub/).

     **Resourcegroep**: een resource groep toohost Hallo iothub maken of een bestaande gebruiken. Zie voor meer informatie [gebruik resourcegroepen toomanage uw Azure-resources](../articles/azure-resource-manager/resource-group-portal.md).

     **Locatie**: Selecteer Hallo dichtstbijzijnde locatie tooyou waar Hallo IoT-hub is gemaakt.

     **Pincode toodashboard**: Selecteer deze optie voor eenvoudige toegang tooyour iothub uit Hallo-dashboard.

   ![Voer informatie toocreate uw IoT-hub](../articles/iot-hub/media/iot-hub-create-hub-and-device/2_fill-in-fields-for-azure-iot-hub-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]

3. Klik op **Create**. Uw IoT-hub kan toocreate van enkele minuten duren. U kunt de voortgang in Hallo bekijken **meldingen** deelvenster.

   ![Meldingen over de voortgang van uw IoT-hub bekijken](../articles/iot-hub/media/iot-hub-create-hub-and-device/3_notification-azure-iot-hub-creation-progress-portal.png)

4. Nadat uw IoT-hub is gemaakt, klikt u erop op Hallo-dashboard. Maak een notitie van Hallo **hostnaam**, en klik vervolgens op **gedeeld toegangsbeleid**.

   ![Hallo-hostnaam van uw IoT-hub ophalen](../articles/iot-hub/media/iot-hub-create-hub-and-device/4_get-azure-iot-hub-hostname-portal.png)

5. In Hallo **gedeeld toegangsbeleid** deelvenster, klikt u op Hallo **iothubowner** beleid, en vervolgens kopiëren en maak een notitie van Hallo **verbindingsreeks** van uw iothub. Zie voor meer informatie [besturingselement toegang tooIoT Hub](../articles/iot-hub/iot-hub-devguide-security.md).

> [!NOTE] 
U hoeft deze iothubowner-verbindingsreeks niet te installeren voor deze zelfstudie. Echter, moet u mogelijk het voor een aantal Hallo-zelfstudies voor verschillende IoT-scenario's na het voltooien van deze configuratie.

   ![Uw IoT-hub-verbindingsreeks ophalen](../articles/iot-hub/media/iot-hub-create-hub-and-device/5_get-azure-iot-hub-connection-string-portal.png)

## <a name="register-a-device-in-hello-iot-hub-for-your-device"></a>Een apparaat in Hallo IoT-hub voor uw apparaat registreren

1. In Hallo [Azure-portal](https://portal.azure.com/), opent u uw IoT-hub.

2. Klik op **Apparatenverkenner**.
3. Klik in deelvenster apparaat Explorer Hallo op **toevoegen** tooadd een apparaat tooyour IoT-hub. Vervolgens Hallo na:

   **Apparaat-ID**: Hallo-ID van het nieuwe apparaat Hallo invoeren. Apparaat-id's zijn hoofdlettergevoelig.

   **Verificatietype**: selecteer **Symmetrische sleutel**.

   **Automatisch sleutels genereren**: schakel dit selectievakje in.

   **Verbinding maken met apparaat tooIoT Hub**: klik op **inschakelen**.

   ![Een apparaat in Hallo Explorer van uw iothub apparaat toevoegen](../articles/iot-hub/media/iot-hub-create-hub-and-device/6_add-device-in-azure-iot-hub-device-explorer-portal.png)

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

4. Klik op **Opslaan**.
5. Nadat het Hallo-apparaat is gemaakt, opent u Hallo-apparaat in Hallo **apparaat Explorer** deelvenster.
6. Noteer de primaire sleutel Hallo van Hallo-verbindingsreeks.

   ![Hallo apparaat verbindingsreeks ophalen](../articles/iot-hub/media/iot-hub-create-hub-and-device/7_get-device-connection-string-in-device-explorer-portal.png)
