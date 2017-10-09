### <span data-ttu-id="57c8d-101"><a name="gwipnoconnection"></a>toomodify hello lokale netwerkgateway GatewayIpAddress - er is geen gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="57c8d-101"><a name="gwipnoconnection"></a> toomodify hello local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="57c8d-102">Als Hallo VPN-apparaat dat u wilt dat tooconnect toohas het openbare IP-adres is gewijzigd, moet u toomodify Hallo lokale netwerk gateway tooreflect die wijzigen.</span><span class="sxs-lookup"><span data-stu-id="57c8d-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="57c8d-103">Hallo voorbeeld toomodify een lokale netwerkgateway die geen een gatewayverbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="57c8d-103">Use hello example toomodify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="57c8d-104">Als u deze waarde wijzigt, kunt u ook Hallo adresvoorvoegsels op Hallo wijzigen hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="57c8d-104">When modifying this value, you can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="57c8d-105">Ervoor toouse Hallo bestaande naam van uw lokale netwerkgateway worden in volgorde toooverwrite Hallo huidige instellingen.</span><span class="sxs-lookup"><span data-stu-id="57c8d-105">Be sure toouse hello existing name of your local network gateway in order toooverwrite hello current settings.</span></span> <span data-ttu-id="57c8d-106">Als u een andere naam gebruikt, kunt u een nieuwe lokale netwerkgateway maken, in plaats van het overschrijven van Hallo bestaande.</span><span class="sxs-lookup"><span data-stu-id="57c8d-106">If you use a different name, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="57c8d-107"><a name="gwipwithconnection"></a>toomodify hello lokale netwerkgateway GatewayIpAddress - bestaande gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="57c8d-107"><a name="gwipwithconnection"></a>toomodify hello local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="57c8d-108">Als Hallo VPN-apparaat dat u wilt dat tooconnect toohas het openbare IP-adres is gewijzigd, moet u toomodify Hallo lokale netwerk gateway tooreflect die wijzigen.</span><span class="sxs-lookup"><span data-stu-id="57c8d-108">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="57c8d-109">Als er al een gatewayverbinding bestaat, moet u eerst tooremove Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="57c8d-109">If a gateway connection already exists, you first need tooremove hello connection.</span></span> <span data-ttu-id="57c8d-110">Nadat Hallo verbinding is verwijderd, kunt u Hallo gateway IP-adres wijzigen en maak een nieuwe verbinding.</span><span class="sxs-lookup"><span data-stu-id="57c8d-110">After hello connection is removed, you can modify hello gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="57c8d-111">U kunt ook de adresvoorvoegsels Hallo op Hallo wijzigen hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="57c8d-111">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="57c8d-112">Dit veroorzaakt enige downtime in uw VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="57c8d-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="57c8d-113">Als u IP-adres van Hallo gateway wijzigt, hoeft u geen toodelete Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="57c8d-113">When modifying hello gateway IP address, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="57c8d-114">U hoeft alleen tooremove Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="57c8d-114">You only need tooremove hello connection.</span></span>
 

1. <span data-ttu-id="57c8d-115">Hallo-verbinding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="57c8d-115">Remove hello connection.</span></span> <span data-ttu-id="57c8d-116">U vindt Hallo-naam van de verbinding met de cmdlet Hallo 'Get-AzureRmVirtualNetworkGatewayConnection'.</span><span class="sxs-lookup"><span data-stu-id="57c8d-116">You can find hello name of your connection by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="57c8d-117">De waarde van de 'GatewayIpAddress' hello wijzigen.</span><span class="sxs-lookup"><span data-stu-id="57c8d-117">Modify hello 'GatewayIpAddress' value.</span></span> <span data-ttu-id="57c8d-118">U kunt ook de adresvoorvoegsels Hallo op Hallo wijzigen hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="57c8d-118">You can also modify hello address prefixes at hello same time.</span></span> <span data-ttu-id="57c8d-119">Deze ervoor toouse Hallo bestaande naam van uw lokale netwerk toooverwrite Hallo huidige instellingen van de gateway.</span><span class="sxs-lookup"><span data-stu-id="57c8d-119">Be sure toouse hello existing name of your local network gateway toooverwrite hello current settings.</span></span> <span data-ttu-id="57c8d-120">Als u dit niet doet, kunt u een nieuwe lokale netwerkgateway maken, Hallo bestaande in plaats van wordt overschreven.</span><span class="sxs-lookup"><span data-stu-id="57c8d-120">If you don't, you create a new local network gateway, instead of overwriting hello existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="57c8d-121">Hallo verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="57c8d-121">Create hello connection.</span></span> <span data-ttu-id="57c8d-122">In dit voorbeeld configureren we een IPsec-verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="57c8d-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="57c8d-123">Wanneer u opnieuw de verbinding maakt, gebruikt u Hallo verbindingstype dat is opgegeven voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="57c8d-123">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="57c8d-124">Zie voor aanvullende verbindingstypen Hallo [PowerShell-cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="57c8d-124">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="57c8d-125">de naam van tooobtain hello VirtualNetworkGateway, kunt u Hallo 'Get-AzureRmVirtualNetworkGateway' cmdlet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="57c8d-125">tooobtain hello VirtualNetworkGateway name, you can run hello 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="57c8d-126">Hallo-variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="57c8d-126">Set hello variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="57c8d-127">Hallo verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="57c8d-127">Create hello connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```