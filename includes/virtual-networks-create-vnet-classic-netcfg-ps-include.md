## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a>Hoe toocreate een virtueel netwerk met een netwerk-config bestand van PowerShell
Azure gebruikt een XML-bestand toodefine alle virtuele netwerken beschikbaar tooa abonnement. U kunt dit bestand downloaden, toomodify te bewerken of verwijderen van de bestaande virtuele netwerken en nieuwe virtuele netwerken maken. In deze zelfstudie leert u hoe toodownload dit bestand waarnaar wordt verwezen tooas network configuration (of netcfg) en toocreate een nieuw virtueel netwerk te bewerken. toolearn meer informatie over het netwerkconfiguratiebestand Hallo Hallo Zie [Azure virtual network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).

toocreate een virtueel netwerk met een netcfg-bestand met behulp van PowerShell, volledige Hallo stappen te volgen:

1. Als u Azure PowerShell nog nooit hebt gebruikt, volledige Hallo stappen voor het Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azureps-cmdlets-docs) artikel, vervolgens tooAzure aanmelden en uw abonnement te selecteren.
2. Vanuit hello Azure PowerShell-console, gebruiken Hallo **Get-AzureVnetConfig** cmdlet toodownload Hallo netwerk bestand tooa configuratiemap op uw computer door het uitvoeren van de volgende opdracht Hallo: 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   Verwachte uitvoer:
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. Open Hallo bestand dat u in stap 2, gebruikmakend van elke toepassing van de editor voor XML- of opgeslagen en zoekt u naar Hallo  **<VirtualNetworkSites>**  element. Als er geen netwerken hebt gemaakt, elk netwerk wordt weergegeven als een eigen  **<VirtualNetworkSite>**  element.
4. toocreate hello virtueel netwerk dat wordt beschreven in dit scenario toevoegen na XML onder Hallo Hallo  **<VirtualNetworkSites>**  element:

   ```xml
        <VirtualNetworkSite name="TestVNet" Location="East US">
          <AddressSpace>
            <AddressPrefix>192.168.0.0/16</AddressPrefix>
          </AddressSpace>
          <Subnets>
            <Subnet name="FrontEnd">
              <AddressPrefix>192.168.1.0/24</AddressPrefix>
            </Subnet>
            <Subnet name="BackEnd">
              <AddressPrefix>192.168.2.0/24</AddressPrefix>
            </Subnet>
          </Subnets>
        </VirtualNetworkSite>
   ```
   
5. Hallo netwerk-configuratiebestand opslaan.
6. Vanuit hello Azure PowerShell-console, gebruiken Hallo **Set AzureVnetConfig** cmdlet tooupload Hallo netwerk configuratiebestand door het uitvoeren van de volgende opdracht Hallo: 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   Geretourneerd uitvoer:
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   Als **OperationStatus** is niet *geslaagd* in Hallo uitvoer geretourneerd, controle op Hallo XML-bestand voor de fouten en volledige stap 6 opnieuw.

7. Vanuit hello Azure PowerShell-console, gebruiken Hallo **Get-AzureVnetSite** cmdlet tooverify die nieuwe netwerk Hallo is toegevoegd door het uitvoeren van de volgende opdracht Hallo: 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   Hallo geretourneerd (afgekort) uitvoer bevat de volgende tekst hello:
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
