## <a name="create-an-iot-hub"></a><span data-ttu-id="b4804-101">Een IoT Hub maken</span><span class="sxs-lookup"><span data-stu-id="b4804-101">Create an IoT hub</span></span>
<span data-ttu-id="b4804-102">Een iothub voor uw gesimuleerde apparaat app tooconnect te maken.</span><span class="sxs-lookup"><span data-stu-id="b4804-102">Create an IoT hub for your simulated device app tooconnect to.</span></span> <span data-ttu-id="b4804-103">Hallo volgende stappen ziet u hoe toocomplete dit taak door met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="b4804-103">hello following steps show you how toocomplete this task by using hello Azure portal.</span></span>

1. <span data-ttu-id="b4804-104">Meld u aan toohello [Azure-portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="b4804-104">Sign in toohello [Azure portal][lnk-portal].</span></span>
1. <span data-ttu-id="b4804-105">Klik in de Snelbalk hello, **nieuw** > **Internet der dingen** > **IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b4804-105">In hello Jumpbar, click **New** > **Internet of Things** > **IoT Hub**.</span></span>
   
    ![Snelbalk Azure Portal][1]
1. <span data-ttu-id="b4804-107">In Hallo **IoT-hub** blade kiest Hallo-configuratie voor uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b4804-107">In hello **IoT hub** blade, choose hello configuration for your IoT hub.</span></span>
   
    ![Blade IoT Hub][2]
   
   1. <span data-ttu-id="b4804-109">In Hallo **naam** Voer een naam voor uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b4804-109">In hello **Name** box, enter a name for your IoT hub.</span></span> <span data-ttu-id="b4804-110">Als hello **naam** is geldig en beschikbaar is, een groen vinkje weergegeven in Hallo **naam** vak.</span><span class="sxs-lookup"><span data-stu-id="b4804-110">If hello **Name** is valid and available, a green check mark appears in hello **Name** box.</span></span>
    [!INCLUDE [iot-hub-pii-note-naming-hub](iot-hub-pii-note-naming-hub.md)]
   
   1. <span data-ttu-id="b4804-111">Selecteer een [prijs- en schaalcategorie][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="b4804-111">Select a [pricing and scale tier][lnk-pricing].</span></span> <span data-ttu-id="b4804-112">Voor deze zelfstudie is geen bepaalde laag vereist.</span><span class="sxs-lookup"><span data-stu-id="b4804-112">This tutorial does not require a specific tier.</span></span> <span data-ttu-id="b4804-113">Gebruik voor deze zelfstudie Hallo gratis F1-laag.</span><span class="sxs-lookup"><span data-stu-id="b4804-113">For this tutorial, use hello free F1 tier.</span></span>
   1. <span data-ttu-id="b4804-114">Maak in **Resourcegroep** een nieuwe resourcegroep of selecteer een bestaande.</span><span class="sxs-lookup"><span data-stu-id="b4804-114">In **Resource group**, either create a resource group, or select an existing one.</span></span> <span data-ttu-id="b4804-115">Zie voor meer informatie [toomanage uw Azure-resources met behulp van de resource groepen][lnk-resource-groups].</span><span class="sxs-lookup"><span data-stu-id="b4804-115">For more information, see [Using resource groups toomanage your Azure resources][lnk-resource-groups].</span></span>
   1. <span data-ttu-id="b4804-116">In **locatie**, selecteer Hallo locatie toohost uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b4804-116">In **Location**, select hello location toohost your IoT hub.</span></span> <span data-ttu-id="b4804-117">Voor deze zelfstudie kiest uw dichtstbijzijnde locatie.</span><span class="sxs-lookup"><span data-stu-id="b4804-117">For this tutorial, choose your nearest location.</span></span>
1. <span data-ttu-id="b4804-118">Wanneer u de configuratieopties voor uw IoT Hub hebt gekozen, klikt u op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="b4804-118">When you have chosen your IoT hub configuration options, click **Create**.</span></span>  <span data-ttu-id="b4804-119">Het kan enkele minuten duren voordat Azure toocreate uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b4804-119">It can take a few minutes for Azure toocreate your IoT hub.</span></span> <span data-ttu-id="b4804-120">toocheck hello status, kunt u voortgang Hallo op Hallo Startboard of in het meldingenvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="b4804-120">toocheck hello status, you can monitor hello progress on hello Startboard or in hello Notifications panel.</span></span>
   
    ![Status Nieuwe IoT Hub][3]
1. <span data-ttu-id="b4804-122">Wanneer Hallo IoT-hub is gemaakt, klikt u op Hallo nieuwe tegel voor uw IoT-hub in hello Azure portal tooopen Hallo blade voor Hallo nieuwe iothub.</span><span class="sxs-lookup"><span data-stu-id="b4804-122">When hello IoT hub has been created successfully, click hello new tile for your IoT hub in hello Azure portal tooopen hello blade for hello new IoT hub.</span></span> <span data-ttu-id="b4804-123">Maak een notitie van Hallo **hostnaam**, en klik vervolgens op **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="b4804-123">Make a note of hello **Hostname**, and then click **Shared access policies**.</span></span>
   
    ![Blade Nieuwe IoT Hub][4]
1. <span data-ttu-id="b4804-125">In Hallo **gedeeld toegangsbeleid** blade, klikt u op Hallo **iothubowner** beleid, en kopieert en noteer Hallo verbindingsreeks IoT-Hub in Hallo **iothubowner** blade.</span><span class="sxs-lookup"><span data-stu-id="b4804-125">In hello **Shared access policies** blade, click hello **iothubowner** policy, and then copy and make note of hello IoT Hub connection string in hello **iothubowner** blade.</span></span> <span data-ttu-id="b4804-126">Zie voor meer informatie [toegangsbeheer] [ lnk-access-control] in Hallo 'IoT Hub developer guide'.</span><span class="sxs-lookup"><span data-stu-id="b4804-126">For more information, see [Access control][lnk-access-control] in hello "IoT Hub developer guide."</span></span>
   
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
