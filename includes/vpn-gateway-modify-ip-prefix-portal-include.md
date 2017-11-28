### <span data-ttu-id="9bb0a-101"><a name="noconnection"></a>IP-adresvoorvoegsels wijzigen voor de gateway van een lokaal netwerk - geen gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="9bb0a-101"><a name="noconnection"></a>To modify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="to-add-additional-address-prefixes"></a><span data-ttu-id="9bb0a-102">Ga als volgt te werk om aanvullende voorvoegsels toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="9bb0a-102">To add additional address prefixes:</span></span>

1. <span data-ttu-id="9bb0a-103">Op de lokale netwerkgateway-bron in de **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-103">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="9bb0a-104">Voeg de IP-adresruimte in de *aanvullend adresbereik toevoegen* vak.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-104">Add the IP address space in the *Add additional address range* box.</span></span>
3. <span data-ttu-id="9bb0a-105">Klik op **opslaan** uw instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-105">Click **Save** to save your settings.</span></span>

#### <a name="to-remove-address-prefixes"></a><span data-ttu-id="9bb0a-106">Ga als volgt te werk om adresvoorvoegsels te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="9bb0a-106">To remove address prefixes:</span></span>

1. <span data-ttu-id="9bb0a-107">Op de lokale netwerkgateway-bron in de **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-107">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="9bb0a-108">Klik op de **'...'**</span><span class="sxs-lookup"><span data-stu-id="9bb0a-108">Click the **'...'**</span></span> <span data-ttu-id="9bb0a-109">op de regel met het voorvoegsel dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-109">on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="9bb0a-110">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-110">Click **Remove**.</span></span>
4. <span data-ttu-id="9bb0a-111">Klik op **opslaan** uw instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-111">Click **Save** to save your settings.</span></span>

### <span data-ttu-id="9bb0a-112"><a name="withconnection"></a>IP-adresvoorvoegsels wijzigen voor de gateway van een lokaal netwerk - bestaande gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="9bb0a-112"><a name="withconnection"></a>To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="9bb0a-113">Als u een gatewayverbinding hebt en u IP-adresvoorvoegsels wilt toevoegen aan of verwijderen uit uw lokale netwerkgateway, moet u de volgende stappen uitvoeren in de volgorde waarin ze staan vermeld.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-113">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="9bb0a-114">Dit veroorzaakt enige downtime in uw VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-114">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="9bb0a-115">Als u IP-adresvoorvoegsels wijzigt, hoeft u de VPN-gateway niet te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-115">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="9bb0a-116">U hoeft alleen de verbinding te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-116">You only need to remove the connection.</span></span>

#### <a name="1-remove-the-connection"></a><span data-ttu-id="9bb0a-117">1. Verwijder de verbinding.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-117">1. Remove the connection.</span></span>

1. <span data-ttu-id="9bb0a-118">Op de lokale netwerkgateway-bron in de **instellingen** sectie, klikt u op **verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-118">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="9bb0a-119">Klik op de **...**  op de regel voor elke verbinding en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-119">Click the **...** on the line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="9bb0a-120">Klik op **opslaan** uw instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-120">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-address-prefixes"></a><span data-ttu-id="9bb0a-121">2. De adresvoorvoegsels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-121">2. Modify the address prefixes.</span></span>

<span data-ttu-id="9bb0a-122">Ga als volgt te werk om aanvullende voorvoegsels toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="9bb0a-122">To add additional address prefixes:</span></span>

1. <span data-ttu-id="9bb0a-123">Op de lokale netwerkgateway-bron in de **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-123">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="9bb0a-124">De IP-adresruimte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-124">Add the IP address space.</span></span>
3. <span data-ttu-id="9bb0a-125">Klik op **opslaan** uw instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-125">Click **Save** to save your settings.</span></span>

<span data-ttu-id="9bb0a-126">Ga als volgt te werk om adresvoorvoegsels te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="9bb0a-126">To remove address prefixes:</span></span>

1. <span data-ttu-id="9bb0a-127">Op de lokale netwerkgateway-bron in de **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-127">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="9bb0a-128">Klik op de **...**  op de regel met het voorvoegsel op dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-128">Click the **...** on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="9bb0a-129">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-129">Click **Remove**.</span></span>
4. <span data-ttu-id="9bb0a-130">Klik op **opslaan** uw instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-130">Click **Save** to save your settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="9bb0a-131">3. Maak de verbinding opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-131">3. Recreate the connection.</span></span>

1. <span data-ttu-id="9bb0a-132">Navigeer naar de virtuele netwerkgateway voor uw VNet.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-132">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="9bb0a-133">(Niet de lokale netwerkgateway.)</span><span class="sxs-lookup"><span data-stu-id="9bb0a-133">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="9bb0a-134">Op de virtuele netwerkgateway in de **instellingen** sectie, klikt u op **verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-134">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="9bb0a-135">Klik op de **+ toevoegen** openen de **verbinding toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-135">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="9bb0a-136">Maak opnieuw een verbinding.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-136">Recreate your connection.</span></span>
5. <span data-ttu-id="9bb0a-137">Klik op **OK** om de verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="9bb0a-137">Click **OK** to create the connection.</span></span>