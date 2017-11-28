<span data-ttu-id="66c0d-101">U kunt controleren of de verbinding met de cmdlet 'Get-AzureVNetConnection' is voltooid.</span><span class="sxs-lookup"><span data-stu-id="66c0d-101">You can verify that your connection succeeded by using the 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="66c0d-102">Gebruik het volgende cmdlet-voorbeeld om de waarden aan te passen aan uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="66c0d-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="66c0d-103">De naam van het virtuele netwerk moet tussen aanhalingstekens als deze spaties bevat.</span><span class="sxs-lookup"><span data-stu-id="66c0d-103">The name of the virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="66c0d-104">Bekijk de waarden nadat de cmdlet is voltooid.</span><span class="sxs-lookup"><span data-stu-id="66c0d-104">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="66c0d-105">In het volgende voorbeeld wordt de status van de connectiviteit wordt weergegeven als 'Verbonden' en ziet u inkomende en uitgaande bytes.</span><span class="sxs-lookup"><span data-stu-id="66c0d-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : The connectivity state for the local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal