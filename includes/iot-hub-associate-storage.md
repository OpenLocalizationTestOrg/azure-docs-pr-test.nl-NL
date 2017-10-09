## <a name="associate-an-azure-storage-account-tooiot-hub"></a>Een Azure Storage-account tooIoT Hub koppelen

Omdat de gesimuleerde apparaattoepassing Hallo een bestand tooa blob uploadt, hebt u een [Azure Storage](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account) account gekoppeld tooIoT Hub. Wanneer u een Azure Storage-account aan een IoT-hub koppelen, genereert Hallo iothub een SAS-URI. Een apparaat kan gebruiken deze SAS-URI toosecurely upload een bestand tooa blob-container. Hallo service IoT Hub en Hallo coördineren apparaat-SDK's Hallo-proces dat wordt gegenereerd Hallo SAS-URI en maakt het beschikbaar tooa apparaat toouse tooupload een bestand.

Volg de instructies in Hallo [configureren bestand geüpload met behulp van Azure-portal Hallo](../articles/iot-hub/iot-hub-configure-file-upload.md) tooassociate een Azure Storage-account tooyour IoT-hub. Zorg ervoor dat een blob-container gekoppeld aan uw IoT-hub is en dat bestandsmeldingen zijn ingeschakeld.

![Schakel meldingen in bestand in de portal](media/iot-hub-associate-storage/enable-file-notifications.png)