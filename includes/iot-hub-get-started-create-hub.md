## <a name="create-an-iot-hub"></a>Een IoT Hub maken
Een iothub voor uw gesimuleerde apparaat app tooconnect te maken. Hallo volgende stappen ziet u hoe toocomplete dit taak door met behulp van hello Azure-portal.

1. Meld u aan toohello [Azure-portal][lnk-portal].
1. Klik in de Snelbalk hello, **nieuw** > **Internet der dingen** > **IoT Hub**.
   
    ![Snelbalk Azure Portal][1]
1. In Hallo **IoT-hub** blade kiest Hallo-configuratie voor uw IoT-hub.
   
    ![Blade IoT Hub][2]
   
   1. In Hallo **naam** Voer een naam voor uw IoT-hub. Als hello **naam** is geldig en beschikbaar is, een groen vinkje weergegeven in Hallo **naam** vak.
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. Selecteer een [prijs- en schaalcategorie][lnk-pricing]. Voor deze zelfstudie is geen bepaalde laag vereist. Gebruik voor deze zelfstudie Hallo gratis F1-laag.
   1. Maak in **Resourcegroep** een nieuwe resourcegroep of selecteer een bestaande. Zie voor meer informatie [toomanage uw Azure-resources met behulp van de resource groepen][lnk-resource-groups].
   1. In **locatie**, selecteer Hallo locatie toohost uw IoT-hub. Voor deze zelfstudie kiest uw dichtstbijzijnde locatie.
1. Wanneer u de configuratieopties voor uw IoT Hub hebt gekozen, klikt u op **Maken**.  Het kan enkele minuten duren voordat Azure toocreate uw IoT-hub. toocheck hello status, kunt u voortgang Hallo op Hallo Startboard of in het meldingenvenster Hallo.
   
    ![Status Nieuwe IoT Hub][3]
1. Wanneer Hallo IoT-hub is gemaakt, klikt u op Hallo nieuwe tegel voor uw IoT-hub in hello Azure portal tooopen Hallo blade voor Hallo nieuwe iothub. Maak een notitie van Hallo **hostnaam**, en klik vervolgens op **gedeeld toegangsbeleid**.
   
    ![Blade Nieuwe IoT Hub][4]
1. In Hallo **gedeeld toegangsbeleid** blade, klikt u op Hallo **iothubowner** beleid, en kopieert en noteer Hallo verbindingsreeks IoT-Hub in Hallo **iothubowner** blade. Zie voor meer informatie [toegangsbeheer] [ lnk-access-control] in Hallo 'IoT Hub developer guide'.
   
    ![Blade Gedeeld toegangsbeleid][5]

<!-- Images. -->
[1]: ./media/iot-hub-get-started-create-hub/create-iot-hub1.png
[2]: ./media/iot-hub-get-started-create-hub/create-iot-hub2.png
[3]: ./media/iot-hub-get-started-create-hub/create-iot-hub3.png
[4]: ./media/iot-hub-get-started-create-hub/create-iot-hub4.png
[5]: ./media/iot-hub-get-started-create-hub/create-iot-hub5.png

<!-- Links -->
[lnk-resource-groups]: ../articles/azure-resource-manager/resource-group-portal.md
[lnk-portal]: https://portal.azure.com/
[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-access-control]: ../articles/iot-hub/iot-hub-devguide-security.md
