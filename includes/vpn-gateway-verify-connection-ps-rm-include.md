<span data-ttu-id="1b749-101">U kunt met de cmdlet 'Get-AzureRmVirtualNetworkGatewayConnection', met of zonder -Debug, verifiëren of de verbinding is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="1b749-101">You can verify that your connection succeeded by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="1b749-102">Gebruik het volgende cmdlet-voorbeeld om de waarden aan te passen aan uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="1b749-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="1b749-103">Selecteer A als dit wordt gevraagd om alles uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1b749-103">If prompted, select 'A' in order to run 'All'.</span></span> <span data-ttu-id="1b749-104">In het voorbeeld verwijst "-Name" naar de naam van de verbinding die u wilt testen.</span><span class="sxs-lookup"><span data-stu-id="1b749-104">In the example, '-Name' refers to the name of the connection that you want to test.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="1b749-105">Bekijk de waarden nadat de cmdlet is voltooid.</span><span class="sxs-lookup"><span data-stu-id="1b749-105">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="1b749-106">In het onderstaande voorbeeld wordt de verbindingsstatus weergegeven als Verbonden en ziet u inkomende en uitgaande bytes.</span><span class="sxs-lookup"><span data-stu-id="1b749-106">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```