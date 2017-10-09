<span data-ttu-id="415bd-101">stappen voor deze taak gebruik een VNet Hallo gebaseerd op Hallo waarden in Hallo configuratielijst verwijzing te volgen.</span><span class="sxs-lookup"><span data-stu-id="415bd-101">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="415bd-102">Extra instellingen en namen worden ook beschreven in deze lijst.</span><span class="sxs-lookup"><span data-stu-id="415bd-102">Additional settings and names are also outlined in this list.</span></span> <span data-ttu-id="415bd-103">We gebruik niet deze lijst in een van de stappen hello, hoewel we variabelen op basis van waarden in deze lijst hello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="415bd-103">We don't use this list directly in any of hello steps, although we do add variables based on hello values in this list.</span></span> <span data-ttu-id="415bd-104">U kunt Hallo lijst toouse kopiëren als een verwijzing, waarbij Hallo waarden vervangt door uw eigen.</span><span class="sxs-lookup"><span data-stu-id="415bd-104">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="415bd-105">**Lijst van configuratie-verwijzing**</span><span class="sxs-lookup"><span data-stu-id="415bd-105">**Configuration reference list**</span></span>

* <span data-ttu-id="415bd-106">Virtuele-netwerknaam = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="415bd-106">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="415bd-107">Virtuele adresruimte van het netwerk 192.168.0.0/16 =</span><span class="sxs-lookup"><span data-stu-id="415bd-107">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="415bd-108">Resourcegroep = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="415bd-108">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="415bd-109">Subnet1 Name = 'FrontEnd'</span><span class="sxs-lookup"><span data-stu-id="415bd-109">Subnet1 Name = "FrontEnd"</span></span> 
* <span data-ttu-id="415bd-110">Adresruimte Subnet1 = '192.168.1.0/24'</span><span class="sxs-lookup"><span data-stu-id="415bd-110">Subnet1 address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="415bd-111">De naam van de gateway-Subnet: 'GatewaySubnet' u moet altijd een gatewaysubnet de naam *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="415bd-111">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
* <span data-ttu-id="415bd-112">Gateway-Subnet-adresruimte = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="415bd-112">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="415bd-113">Regio = 'VS-Oost'</span><span class="sxs-lookup"><span data-stu-id="415bd-113">Region = "East US"</span></span>
* <span data-ttu-id="415bd-114">Gatewaynaam = 'GW'</span><span class="sxs-lookup"><span data-stu-id="415bd-114">Gateway Name = "GW"</span></span>
* <span data-ttu-id="415bd-115">De naam van de IP-gateway = "GWIP"</span><span class="sxs-lookup"><span data-stu-id="415bd-115">Gateway IP Name = "GWIP"</span></span>
* <span data-ttu-id="415bd-116">IP-gatewayconfiguratie Name = "gwipconf"</span><span class="sxs-lookup"><span data-stu-id="415bd-116">Gateway IP configuration Name = "gwipconf"</span></span>
* <span data-ttu-id="415bd-117">Type = "ExpressRoute" dit type is vereist voor een ExpressRoute-configuratie.</span><span class="sxs-lookup"><span data-stu-id="415bd-117">Type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="415bd-118">Gateway openbare IP-naam = 'gwpip'</span><span class="sxs-lookup"><span data-stu-id="415bd-118">Gateway Public IP Name = "gwpip"</span></span>

## <a name="add-a-gateway"></a><span data-ttu-id="415bd-119">Een gateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="415bd-119">Add a gateway</span></span>
1. <span data-ttu-id="415bd-120">Verbinding maken met tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="415bd-120">Connect tooyour Azure Subscription.</span></span>

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="415bd-121">De variabelen voor deze oefening declareren.</span><span class="sxs-lookup"><span data-stu-id="415bd-121">Declare your variables for this exercise.</span></span> <span data-ttu-id="415bd-122">Niet zeker tooedit Hallo voorbeeld tooreflect Hallo instellingen die u toouse wilt.</span><span class="sxs-lookup"><span data-stu-id="415bd-122">Be sure tooedit hello sample tooreflect hello settings that you want toouse.</span></span>

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. <span data-ttu-id="415bd-123">Het virtuele netwerkobject Hallo opslaan als een variabele.</span><span class="sxs-lookup"><span data-stu-id="415bd-123">Store hello virtual network object as a variable.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. <span data-ttu-id="415bd-124">Voeg een gateway subnet tooyour virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="415bd-124">Add a gateway subnet tooyour Virtual Network.</span></span> <span data-ttu-id="415bd-125">Hallo gatewaysubnet moet de naam 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="415bd-125">hello gateway subnet must be named "GatewaySubnet".</span></span> <span data-ttu-id="415bd-126">U moet een gatewaysubnet toe van/27 of groter (/ 26/25 enz.).</span><span class="sxs-lookup"><span data-stu-id="415bd-126">You should create a gateway subnet that is /27 or larger (/26, /25, etc.).</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. <span data-ttu-id="415bd-127">Hallo configuratie instellen.</span><span class="sxs-lookup"><span data-stu-id="415bd-127">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. <span data-ttu-id="415bd-128">Hallo gatewaysubnet opslaan als een variabele.</span><span class="sxs-lookup"><span data-stu-id="415bd-128">Store hello gateway subnet as a variable.</span></span>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. <span data-ttu-id="415bd-129">Vraag een openbaar IP-adres aan.</span><span class="sxs-lookup"><span data-stu-id="415bd-129">Request a public IP address.</span></span> <span data-ttu-id="415bd-130">Hallo IP-adres is aangevraagd voordat het Hallo-gateway te kunnen maken.</span><span class="sxs-lookup"><span data-stu-id="415bd-130">hello IP address is requested before creating hello gateway.</span></span> <span data-ttu-id="415bd-131">U kunt Hallo IP-adres dat u wilt dat toouse; niet opgeven het wordt dynamisch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="415bd-131">You cannot specify hello IP address that you want toouse; it’s dynamically allocated.</span></span> <span data-ttu-id="415bd-132">U gebruikt dit IP-adres in de volgende configuratiesectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="415bd-132">You'll use this IP address in hello next configuration section.</span></span> <span data-ttu-id="415bd-133">Hallo AllocationMethod moet dynamisch zijn.</span><span class="sxs-lookup"><span data-stu-id="415bd-133">hello AllocationMethod must be Dynamic.</span></span>

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. <span data-ttu-id="415bd-134">Hallo-configuratie voor uw gateway maken.</span><span class="sxs-lookup"><span data-stu-id="415bd-134">Create hello configuration for your gateway.</span></span> <span data-ttu-id="415bd-135">Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse.</span><span class="sxs-lookup"><span data-stu-id="415bd-135">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="415bd-136">In deze stap maakt opgeeft u Hallo-configuratie die wordt gebruikt bij het maken van de gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="415bd-136">In this step, you are specifying hello configuration that will be used when you create hello gateway.</span></span> <span data-ttu-id="415bd-137">Deze stap maakt geen daadwerkelijk Hallo gateway-object.</span><span class="sxs-lookup"><span data-stu-id="415bd-137">This step does not actually create hello gateway object.</span></span> <span data-ttu-id="415bd-138">Hallo-voorbeeld hieronder toocreate uw gatewayconfiguratie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="415bd-138">Use hello sample below toocreate your gateway configuration.</span></span>

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. <span data-ttu-id="415bd-139">Hallo-gateway maken.</span><span class="sxs-lookup"><span data-stu-id="415bd-139">Create hello gateway.</span></span> <span data-ttu-id="415bd-140">In deze stap Hallo **- GatewayType** is vooral van belang.</span><span class="sxs-lookup"><span data-stu-id="415bd-140">In this step, hello **-GatewayType** is especially important.</span></span> <span data-ttu-id="415bd-141">Hallo-waarde moet u **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="415bd-141">You must use hello value **ExpressRoute**.</span></span> <span data-ttu-id="415bd-142">Na het uitvoeren van deze cmdlets kunt Hallo gateway 45 minuten of meer toocreate duren.</span><span class="sxs-lookup"><span data-stu-id="415bd-142">After running these cmdlets, hello gateway can take 45 minutes or more toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="415bd-143">Controleer of het Hallo-gateway is gemaakt</span><span class="sxs-lookup"><span data-stu-id="415bd-143">Verify hello gateway was created</span></span>
<span data-ttu-id="415bd-144">Gebruik Hallo na opdrachten tooverify die Hallo gateway is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="415bd-144">Use hello following commands tooverify that hello gateway has been created:</span></span>

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a><span data-ttu-id="415bd-145">Een gateway vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="415bd-145">Resize a gateway</span></span>
<span data-ttu-id="415bd-146">Er zijn een aantal [Gateway-SKU's](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="415bd-146">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="415bd-147">U kunt Hallo opdracht toochange Hallo Gateway-SKU op elk gewenst moment volgen.</span><span class="sxs-lookup"><span data-stu-id="415bd-147">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="415bd-148">Met deze opdracht werkt niet voor UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="415bd-148">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="415bd-149">toochange uw gateway tooan UltraPerformance gateway, verwijdert u eerst de bestaande ExpressRoute-gateway Hallo, en maak vervolgens een nieuwe UltraPerformance-gateway.</span><span class="sxs-lookup"><span data-stu-id="415bd-149">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="415bd-150">toodowngrade uw gateway uit een gateway UltraPerformance, verwijdert u eerst Hallo UltraPerformance gateway en maak vervolgens een nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="415bd-150">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span>
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a><span data-ttu-id="415bd-151">Een gateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="415bd-151">Remove a gateway</span></span>
<span data-ttu-id="415bd-152">Gebruik Hallo opdracht tooremove een gateway te volgen:</span><span class="sxs-lookup"><span data-stu-id="415bd-152">Use hello following command tooremove a gateway:</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```