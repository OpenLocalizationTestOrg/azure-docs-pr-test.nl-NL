### <span data-ttu-id="cb930-101"><a name="noconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - er is geen gatewayverbinding</span><span class="sxs-lookup"><span data-stu-id="cb930-101"><a name="noconnection"></a>toomodify local network gateway IP address prefixes - no gateway connection</span></span>

<span data-ttu-id="cb930-102">tooadd aanvullende adresvoorvoegsels:</span><span class="sxs-lookup"><span data-stu-id="cb930-102">tooadd additional address prefixes:</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

<span data-ttu-id="cb930-103">tooremove adresvoorvoegsels:</span><span class="sxs-lookup"><span data-stu-id="cb930-103">tooremove address prefixes:</span></span><br>
<span data-ttu-id="cb930-104">Hallo-voorvoegsels die u niet langer weglaten.</span><span class="sxs-lookup"><span data-stu-id="cb930-104">Leave out hello prefixes that you no longer need.</span></span> <span data-ttu-id="cb930-105">In dit voorbeeld wordt niet langer nodig voorvoegsel 20.0.0.0/24 (van Hallo vorige voorbeeld), zodat we de lokale netwerkgateway Hallo bijwerken, met uitzondering van voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="cb930-105">In this example, we no longer need prefix 20.0.0.0/24 (from hello previous example), so we update hello local network gateway, excluding that prefix.</span></span>

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <span data-ttu-id="cb930-106"><a name="withconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - gatewayverbinding bestaande</span><span class="sxs-lookup"><span data-stu-id="cb930-106"><a name="withconnection"></a>toomodify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="cb930-107">Als u een gatewayverbinding hebt en tooadd wilt of Hallo IP-adresvoorvoegsels is opgenomen in uw lokale netwerkgateway verwijdert, moet u toodo Hallo stappen hebt uitgevoerd, in volgorde.</span><span class="sxs-lookup"><span data-stu-id="cb930-107">If you have a gateway connection and want tooadd or remove hello IP address prefixes contained in your local network gateway, you need toodo hello following steps, in order.</span></span> <span data-ttu-id="cb930-108">Dit veroorzaakt enige downtime in uw VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="cb930-108">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="cb930-109">Als u IP-adresvoorvoegsels wijzigt, hoeft u geen toodelete Hallo VPN-gateway.</span><span class="sxs-lookup"><span data-stu-id="cb930-109">When modifying IP address prefixes, you don't need toodelete hello VPN gateway.</span></span> <span data-ttu-id="cb930-110">U hoeft alleen tooremove Hallo verbinding.</span><span class="sxs-lookup"><span data-stu-id="cb930-110">You only need tooremove hello connection.</span></span>


1. <span data-ttu-id="cb930-111">Hallo-verbinding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cb930-111">Remove hello connection.</span></span>

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. <span data-ttu-id="cb930-112">Hallo-adresvoorvoegsels wijzigen voor uw lokale netwerkgateway.</span><span class="sxs-lookup"><span data-stu-id="cb930-112">Modify hello address prefixes for your local network gateway.</span></span>
   
  <span data-ttu-id="cb930-113">Hallo-variabele voor Hallo LocalNetworkGateway instellen.</span><span class="sxs-lookup"><span data-stu-id="cb930-113">Set hello variable for hello LocalNetworkGateway.</span></span>

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="cb930-114">Hallo-adresvoorvoegsels wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cb930-114">Modify hello prefixes.</span></span>
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. <span data-ttu-id="cb930-115">Hallo verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="cb930-115">Create hello connection.</span></span> <span data-ttu-id="cb930-116">In dit voorbeeld configureren we een IPsec-verbindingstype.</span><span class="sxs-lookup"><span data-stu-id="cb930-116">In this example, we configure an IPsec connection type.</span></span> <span data-ttu-id="cb930-117">Wanneer u opnieuw de verbinding maakt, gebruikt u Hallo verbindingstype dat is opgegeven voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="cb930-117">When you recreate your connection, use hello connection type that is specified for your configuration.</span></span> <span data-ttu-id="cb930-118">Zie voor aanvullende verbindingstypen Hallo [PowerShell-cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="cb930-118">For additional connection types, see hello [PowerShell cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) page.</span></span>
   
  <span data-ttu-id="cb930-119">Hallo-variabele voor Hallo VirtualNetworkGateway instellen.</span><span class="sxs-lookup"><span data-stu-id="cb930-119">Set hello variable for hello VirtualNetworkGateway.</span></span>

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  <span data-ttu-id="cb930-120">Hallo verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="cb930-120">Create hello connection.</span></span> <span data-ttu-id="cb930-121">In dit voorbeeld wordt de variabele Hallo $local die u in stap 2 hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cb930-121">This example uses hello variable $local that you set in step 2.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```