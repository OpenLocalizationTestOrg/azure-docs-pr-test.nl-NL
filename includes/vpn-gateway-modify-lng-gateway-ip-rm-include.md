### <span data-ttu-id="2fb5d-101"><a name="gwipnoconnection"></a> Het 'gatewayIpAddress' van de lokale netwerkgateway wijzigen - geen gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="2fb5d-101"><a name="gwipnoconnection"></a> To modify the local network gateway 'GatewayIpAddress' - no gateway connection</span></span>

<span data-ttu-id="2fb5d-102">Als van het VPN-apparaat waarmee u verbinding wilt maken het openbare IP-adres is gewijzigd, moet u de gateway van het lokale netwerk aanpassen met deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="2fb5d-103">Gebruik het voorbeeld om een lokale netwerkgateway die geen gatewayverbinding heeft te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-103">Use the example to modify a local network gateway that does not have a gateway connection.</span></span>

<span data-ttu-id="2fb5d-104">Wanneer u deze waarde wijzigt, kunt u tegelijkertijd ook de adresvoorvoegsels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-104">When modifying this value, you can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="2fb5d-105">Zorg ervoor dat u de bestaande naam van de gateway van uw lokale netwerk gebruikt om de huidige instellingen te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-105">Be sure to use the existing name of your local network gateway in order to overwrite the current settings.</span></span> <span data-ttu-id="2fb5d-106">Als u een andere naam gebruikt, maakt u een nieuwe lokale netwerkgateway in plaats van de bestaande gateway te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-106">If you use a different name, you create a new local network gateway, instead of overwriting the existing one.</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <span data-ttu-id="2fb5d-107"><a name="gwipwithconnection"></a>Het 'gatewayIpAddress' van de lokale netwerkgateway wijzigen - bestaande gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="2fb5d-107"><a name="gwipwithconnection"></a>To modify the local network gateway 'GatewayIpAddress' - existing gateway connection</span></span>

<span data-ttu-id="2fb5d-108">Als van het VPN-apparaat waarmee u verbinding wilt maken het openbare IP-adres is gewijzigd, moet u de gateway van het lokale netwerk aanpassen met deze wijziging.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-108">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="2fb5d-109">Als er al een gatewayverbinding bestaat, moet u die verbinding eerst verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-109">If a gateway connection already exists, you first need to remove the connection.</span></span> <span data-ttu-id="2fb5d-110">Nadat de verbinding is verwijderd, kunt u het IP-adres van de gateway wijzigen en een nieuwe verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-110">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="2fb5d-111">U kunt tegelijkertijd ook de adresvoorvoegsels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-111">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="2fb5d-112">Dit veroorzaakt enige downtime in uw VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-112">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="2fb5d-113">Als u het IP-adres van de gateway wijzigt, hoeft u de VPN-gateway niet te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-113">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="2fb5d-114">U hoeft alleen de verbinding te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-114">You only need to remove the connection.</span></span>
 

1. <span data-ttu-id="2fb5d-115">Verwijder de verbinding.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-115">Remove the connection.</span></span> <span data-ttu-id="2fb5d-116">U kunt de naam van uw verbinding vinden met behulp van de cmdlet 'Get-AzureRmVirtualNetworkGatewayConnection'.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-116">You can find the name of your connection by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="2fb5d-117">Wijzig de waarde 'GatewayIpAddress'.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-117">Modify the 'GatewayIpAddress' value.</span></span> <span data-ttu-id="2fb5d-118">U kunt tegelijkertijd ook de adresvoorvoegsels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-118">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="2fb5d-119">Zorg ervoor dat u de bestaande naam van de gateway van uw lokale netwerk gebruikt om de huidige instellingen te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-119">Be sure to use the existing name of your local network gateway to overwrite the current settings.</span></span> <span data-ttu-id="2fb5d-120">Als u dit niet doet, maakt u een nieuwe lokale netwerkgateway in plaats van de bestaande gateway te overschrijven.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-120">If you don't, you create a new local network gateway, instead of overwriting the existing one.</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. <span data-ttu-id="2fb5d-121">Maak de verbinding.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-121">Create the connection.</span></span> <span data-ttu-id="2fb5d-122">In dit voorbeeld configureren we een IPsec-verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-122">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="2fb5d-123">Wanneer u uw verbinding opnieuw maakt, gebruikt u het verbindingstype dat is opgegeven voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-123">When you recreate your connection, use the connection type that is specified for your configuration.</span></span> <span data-ttu-id="2fb5d-124">Zie de pagina [PowerShell-cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) voor aanvullende verbindingstypen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-124">For additional connection types, see the [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>  <span data-ttu-id="2fb5d-125">U kunt de cmdlet 'Get-AzureRmVirtualNetworkGateway' uitvoeren om de VirtualNetworkGateway-naam te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-125">To obtain the VirtualNetworkGateway name, you can run the 'Get-AzureRmVirtualNetworkGateway' cmdlet.</span></span>
   
    <span data-ttu-id="2fb5d-126">Stel de variabelen in.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-126">Set the variables.</span></span>

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    <span data-ttu-id="2fb5d-127">Maak de verbinding.</span><span class="sxs-lookup"><span data-stu-id="2fb5d-127">Create the connection.</span></span>

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```