U kunt controleren of de verbinding is voltooid met behulp van 'Get-AzureRmVirtualNetworkGatewayConnection' hello cmdlet met of zonder '-Debug'. 

1. Gebruik Hallo cmdlet-voorbeeld te volgen, Hallo waarden toomatch configureren zelf. Als u wordt gevraagd, selecteert u "A" in de volgorde toorun 'All'. In voorbeeld Hallo '-naam ' toohello-naam van Hallo-verbinding die u wilt dat tootest verwijst.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Nadat het Hallo-cmdlet is voltooid, kunt u Hallo waarden weergeven. In Hallo voorbeeld hieronder toont verbindingsstatus Hallo zoals 'Verbonden' en u inkomende en uitgaande bytes zien kunt.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```