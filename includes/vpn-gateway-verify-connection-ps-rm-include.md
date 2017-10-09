<span data-ttu-id="29c09-101">U kunt controleren of de verbinding is voltooid met behulp van 'Get-AzureRmVirtualNetworkGatewayConnection' hello cmdlet met of zonder '-Debug'.</span><span class="sxs-lookup"><span data-stu-id="29c09-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="29c09-102">Gebruik Hallo cmdlet-voorbeeld te volgen, Hallo waarden toomatch configureren zelf.</span><span class="sxs-lookup"><span data-stu-id="29c09-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="29c09-103">Als u wordt gevraagd, selecteert u "A" in de volgorde toorun 'All'.</span><span class="sxs-lookup"><span data-stu-id="29c09-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="29c09-104">In voorbeeld Hallo '-naam ' toohello-naam van Hallo-verbinding die u wilt dat tootest verwijst.</span><span class="sxs-lookup"><span data-stu-id="29c09-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="29c09-105">Nadat het Hallo-cmdlet is voltooid, kunt u Hallo waarden weergeven.</span><span class="sxs-lookup"><span data-stu-id="29c09-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="29c09-106">In Hallo voorbeeld hieronder toont verbindingsstatus Hallo zoals 'Verbonden' en u inkomende en uitgaande bytes zien kunt.</span><span class="sxs-lookup"><span data-stu-id="29c09-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```