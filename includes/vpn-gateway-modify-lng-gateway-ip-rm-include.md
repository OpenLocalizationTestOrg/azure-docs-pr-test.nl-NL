### <a name="gwipnoconnection"></a>toomodify hello lokale netwerkgateway GatewayIpAddress - er is geen gatewayverbinding

Als Hallo VPN-apparaat dat u wilt dat tooconnect toohas het openbare IP-adres is gewijzigd, moet u toomodify Hallo lokale netwerk gateway tooreflect die wijzigen. Hallo voorbeeld toomodify een lokale netwerkgateway die geen een gatewayverbinding gebruiken.

Als u deze waarde wijzigt, kunt u ook Hallo adresvoorvoegsels op Hallo wijzigen hetzelfde moment. Ervoor toouse Hallo bestaande naam van uw lokale netwerkgateway worden in volgorde toooverwrite Hallo huidige instellingen. Als u een andere naam gebruikt, kunt u een nieuwe lokale netwerkgateway maken, in plaats van het overschrijven van Hallo bestaande.

```powershell
New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
-Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
-GatewayIpAddress "5.4.3.2" -ResourceGroupName MyRGName
```

### <a name="gwipwithconnection"></a>toomodify hello lokale netwerkgateway GatewayIpAddress - bestaande gatewayverbinding

Als Hallo VPN-apparaat dat u wilt dat tooconnect toohas het openbare IP-adres is gewijzigd, moet u toomodify Hallo lokale netwerk gateway tooreflect die wijzigen. Als er al een gatewayverbinding bestaat, moet u eerst tooremove Hallo verbinding. Nadat Hallo verbinding is verwijderd, kunt u Hallo gateway IP-adres wijzigen en maak een nieuwe verbinding. U kunt ook de adresvoorvoegsels Hallo op Hallo wijzigen hetzelfde moment. Dit veroorzaakt enige downtime in uw VPN-verbinding. Als u IP-adres van Hallo gateway wijzigt, hoeft u geen toodelete Hallo VPN-gateway. U hoeft alleen tooremove Hallo verbinding.
 

1. Hallo-verbinding verwijderen. U vindt Hallo-naam van de verbinding met de cmdlet Hallo 'Get-AzureRmVirtualNetworkGatewayConnection'.

  ```powershell
  Remove-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName `
  -ResourceGroupName MyRGName
  ```
2. De waarde van de 'GatewayIpAddress' hello wijzigen. U kunt ook de adresvoorvoegsels Hallo op Hallo wijzigen hetzelfde moment. Deze ervoor toouse Hallo bestaande naam van uw lokale netwerk toooverwrite Hallo huidige instellingen van de gateway. Als u dit niet doet, kunt u een nieuwe lokale netwerkgateway maken, Hallo bestaande in plaats van wordt overschreven.

  ```powershell
  New-AzureRmLocalNetworkGateway -Name MyLocalNetworkGWName `
  -Location "West US" -AddressPrefix @('10.0.0.0/24','20.0.0.0/24','30.0.0.0/24') `
  -GatewayIpAddress "104.40.81.124" -ResourceGroupName MyRGName
  ```
3. Hallo verbinding maken. In dit voorbeeld configureren we een IPsec-verbindingstype. Wanneer u opnieuw de verbinding maakt, gebruikt u Hallo verbindingstype dat is opgegeven voor uw configuratie. Zie voor aanvullende verbindingstypen Hallo [PowerShell-cmdlet](https://msdn.microsoft.com/library/mt603611.aspx) pagina.  de naam van tooobtain hello VirtualNetworkGateway, kunt u Hallo 'Get-AzureRmVirtualNetworkGateway' cmdlet uitvoeren.
   
    Hallo-variabelen worden ingesteld.

  ```powershell
  $local = Get-AzureRMLocalNetworkGateway -Name MyLocalNetworkGWName -ResourceGroupName MyRGName `
  $vnetgw = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName MyRGName
  ```
   
    Hallo verbinding maken.

  ```powershell 
  New-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnectionName -ResourceGroupName MyRGName `
  -Location "West US" `
  -VirtualNetworkGateway1 $vnetgw `
  -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```