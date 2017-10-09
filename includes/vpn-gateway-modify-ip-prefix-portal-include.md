### <span data-ttu-id="c5aeb-101"><a name="noconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - er is geen gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="c5aeb-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="tooadd-additional-address-prefixes"></a><span data-ttu-id="c5aeb-102">tooadd aanvullende adresvoorvoegsels:</span><span class="sxs-lookup"><span data-stu-id="c5aeb-102">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="c5aeb-103">Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-103">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="c5aeb-104">Hallo IP-adresruimte toevoegen in Hallo *aanvullend adresbereik toevoegen* vak.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-104">Add hello IP address space in hello *Add additional address range* box.</span></span>
3. <span data-ttu-id="c5aeb-105">Klik op **opslaan** toosave uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-105">Click **Save** toosave your settings.</span></span>

#### <a name="tooremove-address-prefixes"></a><span data-ttu-id="c5aeb-106">tooremove adresvoorvoegsels:</span><span class="sxs-lookup"><span data-stu-id="c5aeb-106">tooremove address prefixes:</span></span>

1. <span data-ttu-id="c5aeb-107">Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-107">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="c5aeb-108">Klik op Hallo **'...'** op Hallo regel Hallo voorvoegsel met de gewenste tooremove.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-108">Click hello **'...'** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="c5aeb-109">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-109">Click **Remove**.</span></span>
4. <span data-ttu-id="c5aeb-110">Klik op **opslaan** toosave uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-110">Click **Save** toosave your settings.</span></span>

### <span data-ttu-id="c5aeb-111"><a name="withconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - gatewayverbinding bestaande</span><span class="sxs-lookup"><span data-stu-id="c5aeb-111"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="c5aeb-112">Als u een gatewayverbinding hebt en tooadd wilt of Hallo IP-adresvoorvoegsels is opgenomen in uw lokale netwerkgateway verwijdert, moet u toodo Hallo stappen hebt uitgevoerd, in volgorde.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-112">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="c5aeb-113">Dit veroorzaakt enige downtime in uw VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="c5aeb-114">Als u IP-adresvoorvoegsels wijzigt, hoeft u geen toodelete Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-114">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="c5aeb-115">U hoeft alleen tooremove Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-115">You only need tooremove hello connection.</span></span>

#### <a name="1-remove-hello-connection"></a><span data-ttu-id="c5aeb-116">1. Hallo-verbinding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-116">1. Remove hello connection.</span></span>

1. <span data-ttu-id="c5aeb-117">Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-117">On hello Local Network Gateway resource, in hello **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="c5aeb-118">Klik op Hallo **...**  op Hallo-regel voor elke verbinding en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-118">Click hello **...** on hello line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="c5aeb-119">Klik op **opslaan** toosave uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-119">Click **Save** toosave your settings.</span></span>

#### <a name="2-modify-hello-address-prefixes"></a><span data-ttu-id="c5aeb-120">2. Hallo-adresvoorvoegsels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-120">2. Modify hello address prefixes.</span></span>

<span data-ttu-id="c5aeb-121">tooadd aanvullende adresvoorvoegsels:</span><span class="sxs-lookup"><span data-stu-id="c5aeb-121">tooadd additional address prefixes:</span></span>

1. <span data-ttu-id="c5aeb-122">Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-122">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="c5aeb-123">Hallo IP-adresruimte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-123">Add hello IP address space.</span></span>
3. <span data-ttu-id="c5aeb-124">Klik op **opslaan** toosave uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-124">Click **Save** toosave your settings.</span></span>

<span data-ttu-id="c5aeb-125">tooremove adresvoorvoegsels:</span><span class="sxs-lookup"><span data-stu-id="c5aeb-125">tooremove address prefixes:</span></span>

1. <span data-ttu-id="c5aeb-126">Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-126">On hello Local Network Gateway resource, in hello **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="c5aeb-127">Klik op Hallo **...**  op Hallo regel Hallo voorvoegsel met de gewenste tooremove.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-127">Click hello **...** on hello line containing hello prefix you want tooremove.</span></span>
3. <span data-ttu-id="c5aeb-128">Klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-128">Click **Remove**.</span></span>
4. <span data-ttu-id="c5aeb-129">Klik op **opslaan** toosave uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-129">Click **Save** toosave your settings.</span></span>

#### <a name="3-recreate-hello-connection"></a><span data-ttu-id="c5aeb-130">3. Maak opnieuw verbinding Hallo.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-130">3. Recreate hello connection.</span></span>

1. <span data-ttu-id="c5aeb-131">Navigeer toohello virtuele netwerkgateway voor uw VNet.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-131">Navigate toohello Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="c5aeb-132">(Geen hello lokale netwerkgateway.)</span><span class="sxs-lookup"><span data-stu-id="c5aeb-132">(Not hello Local Network Gateway.)</span></span>
2. <span data-ttu-id="c5aeb-133">Op de virtuele-netwerkgateway Hallo in Hallo **instellingen** sectie, klikt u op **verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-133">On hello Virtual Network Gateway, in hello **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="c5aeb-134">Klik op Hallo **+ toevoegen** tooopen hello **verbinding toevoegen** blade.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-134">Click hello **+ Add** tooopen hello **Add connection** blade.</span></span>
4. <span data-ttu-id="c5aeb-135">Maak opnieuw een verbinding.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-135">Recreate your connection.</span></span>
5. <span data-ttu-id="c5aeb-136">Klik op **OK** toocreate Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="c5aeb-136">Click **OK** toocreate hello connection.</span></span>
