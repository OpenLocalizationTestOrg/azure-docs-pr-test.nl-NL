#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="6892d-101">openbare eindpunten op Hallo cloud toestel toocreate</span><span class="sxs-lookup"><span data-stu-id="6892d-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="6892d-102">Meld u aan toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="6892d-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="6892d-103">Ga te**virtuele Machines**, en selecteer en klik op Hallo virtuele machine die wordt gebruikt als uw toestel cloud.</span><span class="sxs-lookup"><span data-stu-id="6892d-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="6892d-104">Moet u een netwerk security group (NSG) regel toocontrol Hallo verkeersstroom toocreate in en uit de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="6892d-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="6892d-105">Volgende stappen toocreate een regel voor het NSG Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6892d-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="6892d-106">Selecteer **Netwerkbeveiligingsgroep**.</span><span class="sxs-lookup"><span data-stu-id="6892d-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="6892d-107">Klik op Hallo standaard netwerkbeveiligingsgroep toevoegen wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6892d-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="6892d-108">Selecteer **Inkomende beveiligingsregels**.</span><span class="sxs-lookup"><span data-stu-id="6892d-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="6892d-109">Klik op **+ toevoegen** toocreate een inkomende beveiligingsregel.</span><span class="sxs-lookup"><span data-stu-id="6892d-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="6892d-110">Binnenkomende beveiliging regel blade in Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="6892d-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="6892d-111">Voor Hallo **naam**, type Hallo volgende naam voor het Hallo-eindpunt: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="6892d-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="6892d-112">Voor Hallo **prioriteit**, selecteer een getal kleiner zijn dan 1000 (dit is de prioriteit voor de standaardregel Hallo Hallo).</span><span class="sxs-lookup"><span data-stu-id="6892d-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="6892d-113">Hogere Hallo waarde lagere Hallo prioriteit.</span><span class="sxs-lookup"><span data-stu-id="6892d-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="6892d-114">Set Hallo **bron** te**eventuele**.</span><span class="sxs-lookup"><span data-stu-id="6892d-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="6892d-115">Voor Hallo **Service**, selecteer **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="6892d-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="6892d-116">Hallo **Protocol** automatisch te ingesteld**TCP** en Hallo **poortbereik** te is ingesteld,**5986**.</span><span class="sxs-lookup"><span data-stu-id="6892d-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="6892d-117">Klik op **OK** toocreate Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="6892d-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="6892d-118">De laatste stap is tooassociate groepeert u de netwerkbeveiliging van uw met een subnet of een specifieke netwerkinterface.</span><span class="sxs-lookup"><span data-stu-id="6892d-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="6892d-119">Volgende stappen tooassociate Hallo uw netwerkbeveiligingsgroep aan een subnet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6892d-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="6892d-120">Ga te**subnetten**.</span><span class="sxs-lookup"><span data-stu-id="6892d-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="6892d-121">Klik op **Koppelen**.</span><span class="sxs-lookup"><span data-stu-id="6892d-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="6892d-122">Selecteer het virtuele netwerk en selecteer vervolgens de juiste subnet Hallo.</span><span class="sxs-lookup"><span data-stu-id="6892d-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="6892d-123">Klik op **OK** toocreate Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="6892d-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="6892d-124">Nadat het Hallo-regel is gemaakt, kunt u het adres details toodetermine Hallo openbare virtuele IP-adres (VIP) weergeven.</span><span class="sxs-lookup"><span data-stu-id="6892d-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="6892d-125">Noteer dit adres.</span><span class="sxs-lookup"><span data-stu-id="6892d-125">Record this address.</span></span>


