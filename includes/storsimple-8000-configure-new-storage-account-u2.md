<!--author=alkohli last changed: 01/20/17-->


#### <a name="to-add-a-storage-account-credential-in-the-same-azure-subscription-as-the-storsimple-device-manager-service"></a><span data-ttu-id="1e5ed-101">Een opslagaccountreferentie toevoegen aan hetzelfde Azure-abonnement als de StorSimple-apparaatbeheerfunctie</span><span class="sxs-lookup"><span data-stu-id="1e5ed-101">To add a storage account credential in the same Azure subscription as the StorSimple Device Manager service</span></span>

1. <span data-ttu-id="1e5ed-102">Ga naar uw StorSimple-apparaatbeheerservice.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-102">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="1e5ed-103">Klik in de sectie **Configuratie** op **Opslagaccountreferenties**.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-103">In the **Configuration** section, click **Storage account credentials**.</span></span>

    ![Opslagaccountreferenties](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct1.png)

2. <span data-ttu-id="1e5ed-105">Klik op de blade **Opslagaccountreferenties** op **+ Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-105">On the **Storage account credentials** blade, click **+ Add**.</span></span>

    ![Een opslagaccountreferentie toevoegen](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct2.png)

3. <span data-ttu-id="1e5ed-107">Voer de volgende stappen uit op de blade **Een opslagaccountreferentie toevoegen**:</span><span class="sxs-lookup"><span data-stu-id="1e5ed-107">In the **Add a storage account credential** blade, do the following steps:</span></span>

    1. <span data-ttu-id="1e5ed-108">Als u een opslagaccountreferentie aan hetzelfde Azure-abonnement als uw service toevoegt, zorg ervoor dat **Huidig** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-108">As you are adding a storage account credential in the same Azure subscription as your service, ensure that **Current** is selected.</span></span>

    2. <span data-ttu-id="1e5ed-109">Selecteer een bestaand opslagaccount in de vervolgkeuzelijst **opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-109">From the **storage account** dropdown list, select an existing storage account.</span></span>

    3. <span data-ttu-id="1e5ed-110">Op basis van het opslagaccount dat is geselecteerd, wordt de **locatie** weergegeven (grijs weergeven en kan hier niet worden gewijzigd).</span><span class="sxs-lookup"><span data-stu-id="1e5ed-110">Based on the storage account selected, the **location** will be displayed (grayed out and cannot be changed here).</span></span>

    4. <span data-ttu-id="1e5ed-111">Schakel **SSL-modus inschakelen** in om een beveiligd kanaal te maken voor de netwerkcommunicatie tussen uw apparaat en de cloud.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-111">Select **Enable SSL Mode** to create a secure channel for network communication between your device and the cloud.</span></span> <span data-ttu-id="1e5ed-112">Schakel het selectievakje **SSL inschakelen** alleen uit als u binnen een privécloud werkt.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-112">Disable **Enable SSL** only if you are operating within a private cloud.</span></span>

        ![De blade Opslagaccountreferenties toevoegen](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct3.png)

    5. <span data-ttu-id="1e5ed-114">Klik op **Toevoegen** om het maken van de taak voor de opslagaccountreferentie te starten.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-114">Click **Add** to start the job creation for the storage account credential.</span></span> <span data-ttu-id="1e5ed-115">U ontvangt een melding nadat de opslagaccountreferentie is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-115">You will be notified after the storage account credential is successfully created.</span></span>

        ![Melding dat het maken van de opslagaccountreferenties is geslaagd](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct5.png)

<span data-ttu-id="1e5ed-117">De nieuwe opslagaccountreferenties worden weergegeven onder de lijst met **Opslagaccountreferenties**.</span><span class="sxs-lookup"><span data-stu-id="1e5ed-117">The newly created storage account credential will be displayed under the list of **Storage account credentials**.</span></span>

![Lijst met opslagaccountreferenties](./media/storsimple-8000-configure-new-storage-account-u2/createnewstorageacct6.png)

