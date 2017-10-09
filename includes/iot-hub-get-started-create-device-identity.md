## <a name="create-a-device-identity"></a><span data-ttu-id="b01b9-101">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="b01b9-101">Create a device identity</span></span>

<span data-ttu-id="b01b9-102">In deze sectie gebruikt u een Node.js-hulpprogramma aangeroepen [iothub explorer] [ iot-hub-explorer] toocreate een apparaat-id voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b01b9-102">In this section, you use a Node.js tool called [iothub-explorer][iot-hub-explorer] toocreate a device identity for this tutorial.</span></span> <span data-ttu-id="b01b9-103">Apparaat-id's zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="b01b9-103">Device IDs are case sensitive.</span></span>

1. <span data-ttu-id="b01b9-104">Voer Hallo volgende in uw omgeving opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="b01b9-104">Run hello following in your command-line environment:</span></span>

    `npm install -g iothub-explorer@latest`

1. <span data-ttu-id="b01b9-105">Voer vervolgens de volgende opdracht toologin tooyour hub Hallo.</span><span class="sxs-lookup"><span data-stu-id="b01b9-105">Then, run hello following command toologin tooyour hub.</span></span> <span data-ttu-id="b01b9-106">Vervang `{iot hub connection string}` Hello IoT Hub-verbindingsreeks die u eerder hebt gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="b01b9-106">Substitute `{iot hub connection string}` with hello IoT Hub connection string you previously copied:</span></span>

    `iothub-explorer login "{iot hub connection string}"`

1. <span data-ttu-id="b01b9-107">Maak ten slotte een nieuw apparaat-id genoemd `myDeviceId` met Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="b01b9-107">Finally, create a new device identity called `myDeviceId` with hello command:</span></span>

    `iothub-explorer create myDeviceId --connection-string`

   [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

<span data-ttu-id="b01b9-108">Noteer Hallo apparaat verbindingsreeks uit het Hallo-resultaat.</span><span class="sxs-lookup"><span data-stu-id="b01b9-108">Make a note of hello device connection string from hello result.</span></span> <span data-ttu-id="b01b9-109">Deze verbindingsreeks van het apparaat wordt gebruikt door Hallo apparaat app tooconnect tooyour IoT-Hub als een apparaat.</span><span class="sxs-lookup"><span data-stu-id="b01b9-109">This device connection string is used by hello device app tooconnect tooyour IoT Hub as a device.</span></span>

![][img-identity]

<span data-ttu-id="b01b9-110">Raadpleeg te[aan de slag met IoT Hub] [ lnk-getstarted] tooprogrammatically apparaat-id's maken.</span><span class="sxs-lookup"><span data-stu-id="b01b9-110">Refer too[Getting started with IoT Hub][lnk-getstarted] tooprogrammatically create device identities.</span></span>

<!-- images and links -->
[img-identity]: media/iot-hub-get-started-create-device-identity/devidentity.png

[iot-hub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md

[lnk-getstarted]: ../articles/iot-hub/iot-hub-csharp-csharp-getstarted.md
