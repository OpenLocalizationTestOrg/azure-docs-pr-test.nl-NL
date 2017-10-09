U moet een VNet en een gatewaysubnet eerst maken voordat u gaat werken op Hallo taken te volgen. Zie het artikel Hallo [configureren van een virtueel netwerk met de klassieke portal Hallo](../articles/expressroute/expressroute-howto-vnet-portal-classic.md) voor meer informatie.   

## <a name="add-a-gateway"></a>Een gateway toevoegen
Gebruik de opdracht Hallo hieronder toocreate een gateway. Niet zeker toosubstitute voor uw eigen waarden.

    New-AzureVirtualNetworkGateway -VNetName "MyAzureVNET" -GatewayName "ERGateway" -GatewayType Dedicated -GatewaySKU  Standard

## <a name="verify-hello-gateway-was-created"></a>Controleer of het Hallo-gateway is gemaakt
Hallo-opdracht use hieronder tooverify die Hallo gateway is aangemaakt. Met deze opdracht haalt ook Hallo gateway-ID, die u nodig hebt voor andere bewerkingen.

    Get-AzureVirtualNetworkGateway

## <a name="resize-a-gateway"></a>Een gateway vergroten of verkleinen
Er zijn een aantal [Gateway-SKU's](../articles/expressroute/expressroute-about-virtual-network-gateways.md). U kunt Hallo opdracht toochange Hallo Gateway-SKU op elk gewenst moment volgen.

> [!IMPORTANT]
> Met deze opdracht werkt niet voor UltraPerformance gateway. toochange uw gateway tooan UltraPerformance gateway, verwijdert u eerst de bestaande ExpressRoute-gateway Hallo, en maak vervolgens een nieuwe UltraPerformance-gateway. toodowngrade uw gateway uit een gateway UltraPerformance, verwijdert u eerst Hallo UltraPerformance gateway en maak vervolgens een nieuwe gateway. 
> 
> 

    Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance

## <a name="remove-a-gateway"></a>Een gateway verwijderen
Gebruik de opdracht Hallo hieronder tooremove een gateway

    Remove-AzureVirtualNetworkGateway -GatewayId <Gateway ID>