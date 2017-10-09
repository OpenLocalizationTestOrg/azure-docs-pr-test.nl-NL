U kunt controleren of de verbinding is voltooid met behulp van de cmdlet Hallo 'Get-AzureVNetConnection'.

1. Gebruik Hallo cmdlet-voorbeeld te volgen, Hallo waarden toomatch configureren zelf. Hallo-naam van het virtuele netwerk Hallo moet tussen aanhalingstekens als deze spaties bevat.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Nadat het Hallo-cmdlet is voltooid, kunt u Hallo waarden weergeven. Status van de connectiviteit hello wordt weergegeven als 'Verbonden' in hello onderstaand voorbeeld en ziet u inkomende en uitgaande bytes.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal