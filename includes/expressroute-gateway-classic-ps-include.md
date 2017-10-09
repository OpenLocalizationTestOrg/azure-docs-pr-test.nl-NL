<span data-ttu-id="28862-101">U moet een VNet en een gatewaysubnet eerst maken voordat u gaat werken op Hallo taken te volgen.</span><span class="sxs-lookup"><span data-stu-id="28862-101">You must create a VNet and a gateway subnet first, before working on hello following tasks.</span></span> <span data-ttu-id="28862-102">Zie het artikel Hallo [configureren van een virtueel netwerk met de klassieke portal Hallo](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="28862-102">See hello article [Configure a Virtual Network using hello classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="28862-103">Een gateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="28862-103">Add a gateway</span></span>
<span data-ttu-id="28862-104">Gebruik de opdracht Hallo hieronder toocreate een gateway.</span><span class="sxs-lookup"><span data-stu-id="28862-104">Use hello command below toocreate a gateway.</span></span> <span data-ttu-id="28862-105">Niet zeker toosubstitute voor uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="28862-105">Be sure toosubstitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a><span data-ttu-id="28862-106">Controleer of het Hallo-gateway is gemaakt</span><span class="sxs-lookup"><span data-stu-id="28862-106">Verify hello gateway was created</span></span>
<span data-ttu-id="28862-107">Hallo-opdracht use hieronder tooverify die Hallo gateway is aangemaakt.</span><span class="sxs-lookup"><span data-stu-id="28862-107">Use hello command below tooverify that hello gateway has been created.</span></span> <span data-ttu-id="28862-108">Met deze opdracht haalt ook Hallo gateway-ID, die u nodig hebt voor andere bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="28862-108">This command also retrieves hello gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="28862-109">Een gateway vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="28862-109">Resize a gateway</span></span>
<span data-ttu-id="28862-110">Er zijn een aantal [Gateway-SKU's](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="28862-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="28862-111">U kunt Hallo opdracht toochange Hallo Gateway-SKU op elk gewenst moment volgen.</span><span class="sxs-lookup"><span data-stu-id="28862-111">You can use hello following command toochange hello Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28862-112">Met deze opdracht werkt niet voor UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="28862-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="28862-113">toochange uw gateway tooan UltraPerformance gateway, verwijdert u eerst de bestaande ExpressRoute-gateway Hallo, en maak vervolgens een nieuwe UltraPerformance-gateway.</span><span class="sxs-lookup"><span data-stu-id="28862-113">toochange your gateway tooan UltraPerformance gateway, first remove hello existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="28862-114">toodowngrade uw gateway uit een gateway UltraPerformance, verwijdert u eerst Hallo UltraPerformance gateway en maak vervolgens een nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="28862-114">toodowngrade your gateway from an UltraPerformance gateway, first remove hello UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="28862-115">Een gateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="28862-115">Remove a gateway</span></span>
<span data-ttu-id="28862-116">Gebruik de opdracht Hallo hieronder tooremove een gateway</span><span class="sxs-lookup"><span data-stu-id="28862-116">Use hello command below tooremove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>