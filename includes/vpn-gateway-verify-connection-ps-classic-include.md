<span data-ttu-id="962df-101">U kunt controleren of de verbinding is voltooid met behulp van de cmdlet Hallo 'Get-AzureVNetConnection'.</span><span class="sxs-lookup"><span data-stu-id="962df-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="962df-102">Gebruik Hallo cmdlet-voorbeeld te volgen, Hallo waarden toomatch configureren zelf.</span><span class="sxs-lookup"><span data-stu-id="962df-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="962df-103">Hallo-naam van het virtuele netwerk Hallo moet tussen aanhalingstekens als deze spaties bevat.</span><span class="sxs-lookup"><span data-stu-id="962df-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="962df-104">Nadat het Hallo-cmdlet is voltooid, kunt u Hallo waarden weergeven.</span><span class="sxs-lookup"><span data-stu-id="962df-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="962df-105">Status van de connectiviteit hello wordt weergegeven als 'Verbonden' in hello onderstaand voorbeeld en ziet u inkomende en uitgaande bytes.</span><span class="sxs-lookup"><span data-stu-id="962df-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal