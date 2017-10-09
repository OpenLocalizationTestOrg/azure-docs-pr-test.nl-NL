stappen voor deze taak gebruik een VNet Hallo gebaseerd op Hallo waarden in Hallo configuratielijst verwijzing te volgen. Extra instellingen en namen worden ook beschreven in deze lijst. We gebruik niet deze lijst in een van de stappen hello, hoewel we variabelen op basis van waarden in deze lijst hello toevoegen. U kunt Hallo lijst toouse kopiëren als een verwijzing, waarbij Hallo waarden vervangt door uw eigen.

**Lijst van configuratie-verwijzing**

* Virtuele-netwerknaam = "TestVNet"
* Virtuele adresruimte van het netwerk 192.168.0.0/16 =
* Resourcegroep = "TestRG"
* Subnet1 Name = 'FrontEnd' 
* Adresruimte Subnet1 = '192.168.1.0/24'
* De naam van de gateway-Subnet: 'GatewaySubnet' u moet altijd een gatewaysubnet de naam *GatewaySubnet*.
* Gateway-Subnet-adresruimte = "192.168.200.0/26"
* Regio = 'VS-Oost'
* Gatewaynaam = 'GW'
* De naam van de IP-gateway = "GWIP"
* IP-gatewayconfiguratie Name = "gwipconf"
* Type = "ExpressRoute" dit type is vereist voor een ExpressRoute-configuratie.
* Gateway openbare IP-naam = 'gwpip'

## <a name="add-a-gateway"></a>Een gateway toevoegen
1. Verbinding maken met tooyour Azure-abonnement.

  ```powershell 
  Login-AzureRmAccount
  Get-AzureRmSubscription 
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. De variabelen voor deze oefening declareren. Niet zeker tooedit Hallo voorbeeld tooreflect Hallo instellingen die u toouse wilt.

  ```powershell 
  $RG = "TestRG"
  $Location = "East US"
  $GWName = "GW"
  $GWIPName = "GWIP"
  $GWIPconfName = "gwipconf"
  $VNetName = "TestVNet"
  ```
3. Het virtuele netwerkobject Hallo opslaan als een variabele.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  ```
4. Voeg een gateway subnet tooyour virtueel netwerk. Hallo gatewaysubnet moet de naam 'GatewaySubnet'. U moet een gatewaysubnet toe van/27 of groter (/ 26/25 enz.).

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet -AddressPrefix 192.168.200.0/26
  ```
5. Hallo configuratie instellen.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Hallo gatewaysubnet opslaan als een variabele.

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
  ```
7. Vraag een openbaar IP-adres aan. Hallo IP-adres is aangevraagd voordat het Hallo-gateway te kunnen maken. U kunt Hallo IP-adres dat u wilt dat toouse; niet opgeven het wordt dynamisch toegewezen. U gebruikt dit IP-adres in de volgende configuratiesectie Hallo. Hallo AllocationMethod moet dynamisch zijn.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName  -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  ```
8. Hallo-configuratie voor uw gateway maken. Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse. In deze stap maakt opgeeft u Hallo-configuratie die wordt gebruikt bij het maken van de gateway Hallo. Deze stap maakt geen daadwerkelijk Hallo gateway-object. Hallo-voorbeeld hieronder toocreate uw gatewayconfiguratie gebruiken.

  ```powershell
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```
9. Hallo-gateway maken. In deze stap Hallo **- GatewayType** is vooral van belang. Hallo-waarde moet u **ExpressRoute**. Na het uitvoeren van deze cmdlets kunt Hallo gateway 45 minuten of meer toocreate duren.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG -Location $Location -IpConfigurations $ipconf -GatewayType Expressroute -GatewaySku Standard
  ```

## <a name="verify-hello-gateway-was-created"></a>Controleer of het Hallo-gateway is gemaakt
Gebruik Hallo na opdrachten tooverify die Hallo gateway is gemaakt:

```powershell
Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG
```

## <a name="resize-a-gateway"></a>Een gateway vergroten of verkleinen
Er zijn een aantal [Gateway-SKU's](../articles/expressroute/expressroute-about-virtual-network-gateways.md). U kunt Hallo opdracht toochange Hallo Gateway-SKU op elk gewenst moment volgen.

> [!IMPORTANT]
> Met deze opdracht werkt niet voor UltraPerformance gateway. toochange uw gateway tooan UltraPerformance gateway, verwijdert u eerst de bestaande ExpressRoute-gateway Hallo, en maak vervolgens een nieuwe UltraPerformance-gateway. toodowngrade uw gateway uit een gateway UltraPerformance, verwijdert u eerst Hallo UltraPerformance gateway en maak vervolgens een nieuwe gateway.
> 
> 

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="remove-a-gateway"></a>Een gateway verwijderen
Gebruik Hallo opdracht tooremove een gateway te volgen:

```powershell
Remove-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
```