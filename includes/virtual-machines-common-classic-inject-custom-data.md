


<span data-ttu-id="b3c4c-101">Dit onderwerp wordt beschreven hoe:</span><span class="sxs-lookup"><span data-stu-id="b3c4c-101">This topic describes how to:</span></span>

* <span data-ttu-id="b3c4c-102">Gegevens invoeren in Azure een virtuele machine (VM), wanneer deze wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="b3c4c-103">Deze ophalen voor Windows- en Linux.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="b3c4c-104">Gebruik van speciale hulpprogramma's beschikbaar op sommige systemen toodetect en aangepaste gegevens automatisch afhandelen.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="b3c4c-105">Dit artikel wordt beschreven hoe aangepaste gegevens met behulp van een virtuele machine gemaakt met hello Azure Service Management API kan worden ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="b3c4c-106">hoe toouse hello Azure Resource Management-API, Zie toosee [Hallo voorbeeldsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="b3c4c-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="b3c4c-107">Injecteren van aangepaste gegevens in uw virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="b3c4c-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="b3c4c-108">Deze functie is momenteel alleen ondersteund in Hallo [Azure-opdrachtregelinterface](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="b3c4c-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="b3c4c-109">Hier maken we een `custom-data.txt` -bestand met onze gegevens vervolgens invoeren die in toohello VM tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="b3c4c-110">Hoewel u mogelijk Hallo opties voor Hallo `azure vm create` opdracht Hallo volgende demonstreert een zeer eenvoudige benadering:</span><span class="sxs-lookup"><span data-stu-id="b3c4c-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="b3c4c-111">Met behulp van aangepaste gegevens in de Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="b3c4c-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="b3c4c-112">Als uw Azure VM een VM op basis van Windows is, wordt de Hallo aangepaste gegevens te opgeslagen`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="b3c4c-113">Hoewel het base64-gecodeerd tootransfer van Hallo lokale computer toohello nieuwe VM is automatisch gedecodeerd en kan worden geopend of direct gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="b3c4c-114">Als het Hallo-bestand aanwezig is, wordt deze overschreven.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="b3c4c-115">Hallo-beveiliging op Hallo directory te is ingesteld**System: volledig beheer** en **Administrators: volledig beheer**.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="b3c4c-116">Als uw Azure VM een VM op basis van Linux is en vervolgens de aangepaste gegevensbestand Hallo bevindt zich een van de volgende hello wordt geplaatst, afhankelijk van uw distro.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="b3c4c-117">Hallo-gegevens mogelijk base64-gecodeerd, dus u toodecode Hallo gegevens eerst moet misschien:</span><span class="sxs-lookup"><span data-stu-id="b3c4c-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="b3c4c-118">Cloud-init op Azure</span><span class="sxs-lookup"><span data-stu-id="b3c4c-118">Cloud-init on Azure</span></span>
<span data-ttu-id="b3c4c-119">Als uw Azure VM van een installatiekopie van een Ubuntu of virtuele CoreOS is, kunt u CustomData toosend toocloud initialisatie in een cloud-configuratie kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="b3c4c-120">Of als uw aangepaste gegevensbestand een script is, vervolgens cloud init kunt gewoon uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="b3c4c-121">Ubuntu Cloud installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="b3c4c-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="b3c4c-122">In de meeste Azure Linux-installatiekopieën, bewerkt u zou ' / etc/waagent.conf ' tooconfigure Hallo tijdelijke schijf en de wisselruimte bronbestand.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="b3c4c-123">Zie [gebruikershandleiding voor Azure Linux Agent](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="b3c4c-124">Echter op Hallo Ubuntu Cloud installatiekopieën, moet u cloud-init tooconfigure Hallo resource schijf (dat wil zeggen, Hallo 'kortstondige' schijf) en de wisselruimte partitie.</span><span class="sxs-lookup"><span data-stu-id="b3c4c-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="b3c4c-125">Hallo na pagina op Hallo Ubuntu wiki voor meer informatie Zie: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="b3c4c-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="b3c4c-126">Volgende stappen: met behulp van cloud-init</span><span class="sxs-lookup"><span data-stu-id="b3c4c-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="b3c4c-127">Zie voor meer informatie, Hallo [cloud init-documentatie voor Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="b3c4c-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="b3c4c-128">Rol van Service Management REST API-verwijzing toevoegen</span><span class="sxs-lookup"><span data-stu-id="b3c4c-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="b3c4c-129">Azure-opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="b3c4c-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

