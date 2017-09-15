<!--author=alkohli last changed: 06/22/17-->

#### <a name="to-create-a-volume-container"></a><span data-ttu-id="96b8e-101">Een volumecontainer maken</span><span class="sxs-lookup"><span data-stu-id="96b8e-101">To create a volume container</span></span>
1. <span data-ttu-id="96b8e-102">Ga naar de StorSimple-apparaatbeheerservice en klik op **Apparaten**.</span><span class="sxs-lookup"><span data-stu-id="96b8e-102">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="96b8e-103">Selecteer en klik op een apparaat in de lijst in tabelvorm met apparaten.</span><span class="sxs-lookup"><span data-stu-id="96b8e-103">From the tabular listing of the devices, select and click a device.</span></span> 

    ![De blade Volumecontainer](./media/storsimple-8000-create-volume-container/createvolumecontainer1.png)

2. <span data-ttu-id="96b8e-105">Klik op het apparaatdashboard op **Volumecontainer toevoegen**</span><span class="sxs-lookup"><span data-stu-id="96b8e-105">In the device dashboard, click **+ Add volume container**</span></span>

    ![De blade Volumecontainer](./media/storsimple-8000-create-volume-container/createvolumecontainer2.png)

3. <span data-ttu-id="96b8e-107">Doe het volgende op de blade **Volumecontainer toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="96b8e-107">In the **Add volume container** blade:</span></span>
   
   1. <span data-ttu-id="96b8e-108">Het apparaat wordt automatisch geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="96b8e-108">The device is automatically selected.</span></span>
   2. <span data-ttu-id="96b8e-109">Geef een **naam** op voor uw volumecontainer.</span><span class="sxs-lookup"><span data-stu-id="96b8e-109">Supply a **Name** for your volume container.</span></span> <span data-ttu-id="96b8e-110">De naam moet 3 tot 32 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="96b8e-110">The name must be 3 to 32 characters long.</span></span> <span data-ttu-id="96b8e-111">U kunt de naam van een volumecontainer niet wijzigen zodra deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96b8e-111">You cannot rename a volume container once it is created.</span></span>
   3. <span data-ttu-id="96b8e-112">Schakel **Versleuteling van cloudopslag inschakelen** in om versleuteling in te schakelen van de gegevens die van het apparaat naar de cloud worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="96b8e-112">Select **Enable Cloud Storage Encryption** to enable encryption of the data sent from the device to the cloud.</span></span>
   4. <span data-ttu-id="96b8e-113">Geef een **versleutelingssleutel voor cloudopslag** van 8 tot 32 tekens op en bevestig deze.</span><span class="sxs-lookup"><span data-stu-id="96b8e-113">Provide and confirm a **Cloud Storage Encryption Key** that is 8 to 32 characters long.</span></span> <span data-ttu-id="96b8e-114">De sleutel wordt door het apparaat gebruikt voor toegang tot versleutelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="96b8e-114">This key is used by the device to access encrypted data.</span></span>
   5. <span data-ttu-id="96b8e-115">Selecteer een **opslagaccount** om aan deze volumecontainer te koppelen.</span><span class="sxs-lookup"><span data-stu-id="96b8e-115">Select a **Storage Account** to associate with this volume container.</span></span> <span data-ttu-id="96b8e-116">U kunt een bestaand opslagaccount kiezen of het standaardaccount dat is gegenereerd toen de service werd gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96b8e-116">You can choose an existing storage account or the default account that is generated at the time of service creation.</span></span> <span data-ttu-id="96b8e-117">U kunt ook de optie **Nieuwe toevoegen** gebruiken om een opslagaccount op te geven dat niet is gekoppeld aan dit serviceabonnement.</span><span class="sxs-lookup"><span data-stu-id="96b8e-117">You can also use the **Add new** option to specify a storage account that is not linked to this service subscription.</span></span>
   6. <span data-ttu-id="96b8e-118">Selecteer **Onbeperkt** in de vervolgkeuzelijst **Bandbreedte opgeven** als u alle beschikbare bandbreedte wilt verbruiken.</span><span class="sxs-lookup"><span data-stu-id="96b8e-118">Select **Unlimited** in the **Specify bandwidth** drop-down list if you wish to consume all the available bandwidth.</span></span> <span data-ttu-id="96b8e-119">U kunt deze optie ook instellen op **Aangepast** om bandbreedtebesturingselementen te implementeren en een waarde tussen 1 Mbps en 1000 Mbps op te geven.</span><span class="sxs-lookup"><span data-stu-id="96b8e-119">You can also set this option to **Custom** to employ bandwidth controls, and specify a value between 1 Mbps and 1,000 Mbps.</span></span>
      <span data-ttu-id="96b8e-120">Als u beschikt over informatie over uw bandbreedtegebruik, kunt u de bandbreedte mogelijk toewijzen op basis van een planning door een **bandbreedtesjabloon te selecteren**.</span><span class="sxs-lookup"><span data-stu-id="96b8e-120">If you have your bandwidth usage information available, you may be able to allocate bandwidth based on a schedule by specifying **Select a bandwidth template**.</span></span> <span data-ttu-id="96b8e-121">Voor een stapsgewijze procedure gaat u naar [Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template) (Een bandbreedtesjabloon toevoegen).</span><span class="sxs-lookup"><span data-stu-id="96b8e-121">For a step-by-step procedure, go to [Add a bandwidth template](../articles/storsimple/storsimple-8000-manage-bandwidth-templates.md#add-a-bandwidth-template).</span></span>

      ![De blade Volumecontainer](./media/storsimple-8000-create-volume-container/createvolumecontainer6b.png)
   7. <span data-ttu-id="96b8e-123">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="96b8e-123">Click **Create**.</span></span>

        ![De blade Volumecontainer](./media/storsimple-8000-create-volume-container/createvolumecontainer6.png)
   
       <span data-ttu-id="96b8e-125">U krijgt een melding wanneer de volumecontainer is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96b8e-125">You are notified when the volume container is successfully created.</span></span>

       ![Melding over volumecontainer](./media/storsimple-8000-create-volume-container/createvolumecontainer8.png)

   <span data-ttu-id="96b8e-127">De nieuwe volumecontainer wordt vermeld in de lijst met volumecontainers voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="96b8e-127">The newly created volume container is listed in the list of volume containers for your device.</span></span>

   ![De blade Volumecontainer toevoegen](./media/storsimple-8000-create-volume-container/createvolumecontainer9.png)


