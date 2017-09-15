## <a name="how-to-create-a-virtual-network-using-a-network-config-file-from-powershell"></a><span data-ttu-id="3e060-101">Het maken van een virtueel netwerk met een configuratiebestand netwerk vanuit PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e060-101">How to create a virtual network using a network config file from PowerShell</span></span>
<span data-ttu-id="3e060-102">Azure maakt gebruik van een xml-bestand voor het definiëren van alle virtuele netwerken die beschikbaar zijn in een abonnement.</span><span class="sxs-lookup"><span data-stu-id="3e060-102">Azure uses an xml file to define all virtual networks available to a subscription.</span></span> <span data-ttu-id="3e060-103">U kunt dit bestand downloaden, bewerkt om te wijzigen of verwijderen van de bestaande virtuele netwerken en nieuwe virtuele netwerken maken.</span><span class="sxs-lookup"><span data-stu-id="3e060-103">You can download this file, edit it to modify or delete existing virtual networks, and create new virtual networks.</span></span> <span data-ttu-id="3e060-104">In deze zelfstudie u meer informatie over het downloaden van dit bestand, netwerk-configuratie (of netcfg) bestand genoemd en bewerken om te maken van een nieuw virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="3e060-104">In this tutorial, you learn how to download this file, referred to as network configuration (or netcfg) file, and edit it to create a new virtual network.</span></span> <span data-ttu-id="3e060-105">Zie voor meer informatie over het configuratiebestand van het netwerk, de [Azure virtual network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="3e060-105">To learn more about the network configuration file, see the [Azure virtual network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

<span data-ttu-id="3e060-106">Als een virtueel netwerk maken met een netcfg-bestand met behulp van PowerShell, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3e060-106">To create a virtual network with a netcfg file using PowerShell, complete the following steps:</span></span>

1. <span data-ttu-id="3e060-107">Als u Azure PowerShell nog nooit hebt gebruikt, voer de stappen in de [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) artikel, vervolgens aanmelden bij Azure en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="3e060-107">If you have never used Azure PowerShell, complete the steps in the [How to Install and Configure Azure PowerShell](/powershell/azureps-cmdlets-docs) article, then sign in to Azure and select your subscription.</span></span>
2. <span data-ttu-id="3e060-108">Via de Azure PowerShell-console, gebruiken de **Get-AzureVnetConfig** cmdlet voor het downloaden van het configuratiebestand van het netwerk naar een map op uw computer met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3e060-108">From the Azure PowerShell console, use the **Get-AzureVnetConfig** cmdlet to download the network configuration file to a directory on your computer by running the following command:</span></span> 
   
   ```powershell
   Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="3e060-109">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3e060-109">Expected output:</span></span>
  
      ```
      XMLConfiguration                                                                                                     
      ----------------                                                                                                     
      <?xml version="1.0" encoding="utf-8"?>...
      ```

3. <span data-ttu-id="3e060-110">Open het bestand dat u in stap 2, gebruikmakend van een XML- of -editor toepassing opgeslagen en zoekt u de  **<VirtualNetworkSites>**  element.</span><span class="sxs-lookup"><span data-stu-id="3e060-110">Open the file you saved in step 2 using any XML or text editor application, and look for the **<VirtualNetworkSites>** element.</span></span> <span data-ttu-id="3e060-111">Als er geen netwerken hebt gemaakt, elk netwerk wordt weergegeven als een eigen  **<VirtualNetworkSite>**  element.</span><span class="sxs-lookup"><span data-stu-id="3e060-111">If you have any networks already created, each network is displayed as its own **<VirtualNetworkSite>** element.</span></span>
4. <span data-ttu-id="3e060-112">Toevoegen voor het maken van het virtuele netwerk in dit scenario wordt de volgende XML net onder de  **<VirtualNetworkSites>**  element:</span><span class="sxs-lookup"><span data-stu-id="3e060-112">To create the virtual network described in this scenario, add the following XML just under the **<VirtualNetworkSites>** element:</span></span>

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
   
5. <span data-ttu-id="3e060-113">Sla het configuratiebestand van het netwerk.</span><span class="sxs-lookup"><span data-stu-id="3e060-113">Save the network configuration file.</span></span>
6. <span data-ttu-id="3e060-114">Via de Azure PowerShell-console, gebruiken de **Set AzureVnetConfig** cmdlet voor het uploaden van het configuratiebestand van het netwerk met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3e060-114">From the Azure PowerShell console, use the **Set-AzureVnetConfig** cmdlet to upload the network configuration file by running the following command:</span></span> 
   
   ```powershell
   Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
   ```
   
   <span data-ttu-id="3e060-115">Geretourneerd uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3e060-115">Returned output:</span></span>
   
      ```
      OperationDescription OperationId                          OperationStatus
      -------------------- -----------                          ---------------
      Set-AzureVNetConfig  <Id>                                 Succeeded 
      ```
   
   <span data-ttu-id="3e060-116">Als **OperationStatus** is niet *geslaagd* in de uitvoer van de geretourneerde controleren op fouten en volledige stap 6 van het xml-bestand opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3e060-116">If **OperationStatus** is not *Succeeded* in the returned output, check the xml file for errors and complete step 6 again.</span></span>

7. <span data-ttu-id="3e060-117">Via de Azure PowerShell-console, gebruiken de **Get-AzureVnetSite** cmdlet om te controleren of het nieuwe netwerk is toegevoegd met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3e060-117">From the Azure PowerShell console, use the **Get-AzureVnetSite** cmdlet to verify that the new network was added by running the following command:</span></span> 

   ```powershell
   Get-AzureVNetSite -VNetName TestVNet
   ```
   
   <span data-ttu-id="3e060-118">De uitvoer van de geretourneerde (afgekort) omvat de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="3e060-118">The returned (abbreviated) output includes the following text:</span></span>
  
      ```
      AddressSpacePrefixes : {192.168.0.0/16}
      Location             : Central US
      Name                 : TestVNet
      State                : Created
      Subnets              : {FrontEnd, BackEnd}
      OperationDescription : Get-AzureVNetSite
      OperationStatus      : Succeeded
      ```
