<span data-ttu-id="66903-101">U moet een VNet en een gatewaysubnet eerst maken voordat u gaat werken op de volgende taken.</span><span class="sxs-lookup"><span data-stu-id="66903-101">You must create a VNet and a gateway subnet first, before working on the following tasks.</span></span> <span data-ttu-id="66903-102">Zie het artikel [configureren van een virtueel netwerk met de klassieke portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="66903-102">See the article [Configure a Virtual Network using the classic portal](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) for more information.</span></span>   

## <a name="add-a-gateway"></a><span data-ttu-id="66903-103">Een gateway toevoegen</span><span class="sxs-lookup"><span data-stu-id="66903-103">Add a gateway</span></span>
<span data-ttu-id="66903-104">Gebruik de onderstaande opdracht voor het maken van een gateway.</span><span class="sxs-lookup"><span data-stu-id="66903-104">Use the command below to create a gateway.</span></span> <span data-ttu-id="66903-105">Zorg ervoor dat vervangen door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="66903-105">Be sure to substitute any values for your own.</span></span>

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-the-gateway-was-created"></a><span data-ttu-id="66903-106">Controleer of dat de gateway is gemaakt</span><span class="sxs-lookup"><span data-stu-id="66903-106">Verify the gateway was created</span></span>
<span data-ttu-id="66903-107">Gebruik de onderstaande opdracht om te controleren of de gateway is aangemaakt.</span><span class="sxs-lookup"><span data-stu-id="66903-107">Use the command below to verify that the gateway has been created.</span></span> <span data-ttu-id="66903-108">Met deze opdracht haalt ook de gateway-ID die u nodig hebt voor andere bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="66903-108">This command also retrieves the gateway ID, which you need for other operations.</span></span>

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a><span data-ttu-id="66903-109">Een gateway vergroten of verkleinen</span><span class="sxs-lookup"><span data-stu-id="66903-109">Resize a gateway</span></span>
<span data-ttu-id="66903-110">Er zijn een aantal [Gateway-SKU's](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span><span class="sxs-lookup"><span data-stu-id="66903-110">There are a number of [Gateway SKUs](../articles/expressroute/expressroute-about-virtual-network-gateways.md).</span></span> <span data-ttu-id="66903-111">De volgende opdracht kunt u de Gateway-SKU op elk moment wijzigen.</span><span class="sxs-lookup"><span data-stu-id="66903-111">You can use the following command to change the Gateway SKU at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66903-112">Met deze opdracht werkt niet voor UltraPerformance gateway.</span><span class="sxs-lookup"><span data-stu-id="66903-112">This command doesn't work for UltraPerformance gateway.</span></span> <span data-ttu-id="66903-113">Als u wilt uw gateway uit naar een gateway UltraPerformance wijzigen, verwijdert u eerst de bestaande ExpressRoute-gateway en maak vervolgens een nieuwe UltraPerformance-gateway.</span><span class="sxs-lookup"><span data-stu-id="66903-113">To change your gateway to an UltraPerformance gateway, first remove the existing ExpressRoute gateway, and then create a new UltraPerformance gateway.</span></span> <span data-ttu-id="66903-114">Als u wilt uw gateway van een gateway UltraPerformance downgraden, verwijdert u eerst de gateway UltraPerformance en maak vervolgens een nieuwe gateway.</span><span class="sxs-lookup"><span data-stu-id="66903-114">To downgrade your gateway from an UltraPerformance gateway, first remove the UltraPerformance gateway, and then create a new gateway.</span></span> 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a><span data-ttu-id="66903-115">Een gateway verwijderen</span><span class="sxs-lookup"><span data-stu-id="66903-115">Remove a gateway</span></span>
<span data-ttu-id="66903-116">Gebruik de onderstaande opdracht om een gateway te verwijderen</span><span class="sxs-lookup"><span data-stu-id="66903-116">Use the command below to remove a gateway</span></span>

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>