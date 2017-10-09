### <a name="noconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - er is geen gatewayverbinding

tooadd aanvullende adresvoorvoegsels:

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
```

tooremove adresvoorvoegsels:<br>
Hallo-voorvoegsels die u niet langer weglaten. In dit voorbeeld wordt niet langer nodig voorvoegsel 20.0.0.0/24 (van Hallo vorige voorbeeld), zodat we de lokale netwerkgateway Hallo bijwerken, met uitzondering van voorvoegsel.

```powershell
$local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
-AddressPrefix @('10.0.0.0/24','30.0.0.0/24')
```

### <a name="withconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - gatewayverbinding bestaande

Als u een gatewayverbinding hebt en tooadd wilt of Hallo IP-adresvoorvoegsels is opgenomen in uw lokale netwerkgateway verwijdert, moet u toodo Hallo stappen hebt uitgevoerd, in volgorde. Dit veroorzaakt enige downtime in uw VPN-verbinding. Als u IP-adresvoorvoegsels wijzigt, hoeft u geen toodelete Hallo VPN-gateway. U hoeft alleen tooremove Hallo verbinding.


1. Hallo-verbinding verwijderen.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName
  ```
2. Hallo-adresvoorvoegsels wijzigen voor uw lokale netwerkgateway.
   
  Hallo-variabele voor Hallo LocalNetworkGateway instellen.

  ```powershell
  $local = Get-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName
  ```
   
  Hallo-adresvoorvoegsels wijzigen.
   
  ```powershell
  Set-AzureRmLocalNetworkGateway -LocalNetworkGateway $local `
  -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24')
  ```
3. Hallo verbinding maken. In dit voorbeeld configureren we een IPsec-verbindingstype. Wanneer u opnieuw de verbinding maakt, gebruikt u Hallo verbindingstype dat is opgegeven voor uw configuratie. Zie voor aanvullende verbindingstypen Hallo [PowerShell-cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) pagina.
   
  Hallo-variabele voor Hallo VirtualNetworkGateway instellen.

  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name RMGateway  -ResourceGroupName MyRGName
  ```
   
  Hallo verbinding maken. In dit voorbeeld wordt de variabele Hallo $local die u in stap 2 hebt ingesteld.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName -Location 'West US' `
  -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec `
  -RoutingWeight 10 -SharedKey 'abc123'
  ```