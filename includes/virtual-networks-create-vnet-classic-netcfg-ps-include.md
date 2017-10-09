## <a name="how-toocreate-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="c82d7-101">Hoe toocreate een virtueel netwerk met een netwerk-config bestand van PowerShell</span><span class="sxs-lookup"><span data-stu-id="c82d7-101">How toocreate a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="c82d7-102">Azure gebruikt een XML-bestand toodefine alle virtuele netwerken beschikbaar tooa abonnement.</span><span class="sxs-lookup"><span data-stu-id="c82d7-102">Azure uses an xml file toodefine all virtual networks available tooa subscription.</span></span> <span data-ttu-id="c82d7-103">U kunt dit bestand downloaden, toomodify te bewerken of verwijderen van de bestaande virtuele netwerken en nieuwe virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="c82d7-103">You can download this file, edit it toomodify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="c82d7-104">In deze zelfstudie leert u hoe toodownload dit bestand waarnaar wordt verwezen tooas network configuration (of netcfg) en toocreate een nieuw virtueel netwerk te bewerken.</span><span class="sxs-lookup"><span data-stu-id="c82d7-104">In this tutorial, you learn how toodownload this file, referred tooas network configuration (or netcfg) file, and edit it toocreate a new virtual network.</span></span> <span data-ttu-id="c82d7-105">toolearn meer informatie over het netwerkconfiguratiebestand Hallo Hallo Zie [Azure virtual network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="c82d7-105">toolearn more about hello network configuration file, see hello [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="c82d7-106">toocreate een virtueel netwerk met een netcfg-bestand met behulp van PowerShell, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c82d7-106">toocreate a virtual network with a netcfg file using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="c82d7-107">Als u Azure PowerShell nog nooit hebt gebruikt, volledige Hallo stappen voor het Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azureps-cmdlets-docs) artikel, vervolgens tooAzure aanmelden en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="c82d7-107">If you have never used Azure PowerShell, complete hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in tooAzure and select your subscription.</span></span>
2. <span data-ttu-id="c82d7-108">Vanuit hello Azure PowerShell-console, gebruiken Hallo **Get-AzureVnetConfig** cmdlet toodownload Hallo netwerk bestand tooa configuratiemap op uw computer door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="c82d7-108">From hello Azure PowerShell console, use hello **Get-AzureVnetConfig** cmdlet toodownload hello network configuration file tooa directory on your computer by running hello following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="c82d7-109">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c82d7-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="c82d7-110">Open Hallo bestand dat u in stap 2, gebruikmakend van elke toepassing van de editor voor XML- of opgeslagen en zoekt u naar Hallo  **<VirtualNetworkSites>**  element.</span><span class="sxs-lookup"><span data-stu-id="c82d7-110">Open hello file you saved in step 2 using any XML or text editor application, and look for hello **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="c82d7-111">Als er geen netwerken hebt gemaakt, elk netwerk wordt weergegeven als een eigen  **<VirtualNetworkSite>**  element.</span><span class="sxs-lookup"><span data-stu-id="c82d7-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="c82d7-112">toocreate hello virtueel netwerk dat wordt beschreven in dit scenario toevoegen na XML onder Hallo Hallo  **<VirtualNetworkSites>**  element:</span><span class="sxs-lookup"><span data-stu-id="c82d7-112">toocreate hello virtual network described in this scenario, add hello following XML just under hello **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="c82d7-113">Hallo netwerk-configuratiebestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="c82d7-113">Save hello network configuration file.</span></span>
6. <span data-ttu-id="c82d7-114">Vanuit hello Azure PowerShell-console, gebruiken Hallo **Set AzureVnetConfig** cmdlet tooupload Hallo netwerk configuratiebestand door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="c82d7-114">From hello Azure PowerShell console, use hello **Set-AzureVnetConfig** cmdlet tooupload hello network configuration file by running hello following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="c82d7-115">Geretourneerd uitvoer:</span><span class="sxs-lookup"><span data-stu-id="c82d7-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="c82d7-116">Als **OperationStatus** is niet *geslaagd* in Hallo uitvoer geretourneerd, controle op Hallo XML-bestand voor de fouten en volledige stap 6 opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c82d7-116">If **OperationStatus** is not *Succeeded* in hello returned output, check hello xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="c82d7-117">Vanuit hello Azure PowerShell-console, gebruiken Hallo **Get-AzureVnetSite** cmdlet tooverify die nieuwe netwerk Hallo is toegevoegd door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="c82d7-117">From hello Azure PowerShell console, use hello **Get-AzureVnetSite** cmdlet tooverify that hello new network was added by running hello following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="c82d7-118">Hallo geretourneerd (afgekort) uitvoer bevat de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="c82d7-118">hello returned (abbreviated) output includes hello following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
