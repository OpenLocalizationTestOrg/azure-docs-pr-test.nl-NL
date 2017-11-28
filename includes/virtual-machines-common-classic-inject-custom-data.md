


<span data-ttu-id="77d19-101">Dit onderwerp wordt beschreven hoe:</span><span class="sxs-lookup"><span data-stu-id="77d19-101">This topic describes how to:</span></span>

* <span data-ttu-id="77d19-102">Gegevens invoeren in Azure een virtuele machine (VM), wanneer deze wordt ingericht.</span><span class="sxs-lookup"><span data-stu-id="77d19-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="77d19-103">Deze ophalen voor Windows- en Linux.</span><span class="sxs-lookup"><span data-stu-id="77d19-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="77d19-104">Speciale hulpprogramma's beschikbaar op sommige systemen gebruiken om te detecteren en aangepaste gegevens automatisch te verwerken.</span><span class="sxs-lookup"><span data-stu-id="77d19-104">Use special tools available on some systems to detect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="77d19-105">Dit artikel wordt beschreven hoe aangepaste gegevens met behulp van een virtuele machine gemaakt met de Azure Service Management API kan worden ingevoegd.</span><span class="sxs-lookup"><span data-stu-id="77d19-105">This article describes how custom data can be injected by using a VM created with the Azure Service Management API.</span></span> <span data-ttu-id="77d19-106">Zie voor het gebruik van de Azure Resource Management API [de voorbeeldsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="77d19-106">To see how to use the Azure Resource Management API, see [the example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="77d19-107">Injecteren van aangepaste gegevens in uw virtuele machine van Azure</span><span class="sxs-lookup"><span data-stu-id="77d19-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="77d19-108">Deze functie is momenteel alleen ondersteund in de [Azure-opdrachtregelinterface](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="77d19-108">This feature is currently supported only in the [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="77d19-109">Hier maken we een `custom-data.txt` -bestand met onze gegevens vervolgens invoeren die in naar de virtuele machine tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="77d19-109">Here we create a `custom-data.txt` file that contains our data, then inject that in to the VM during provisioning.</span></span> <span data-ttu-id="77d19-110">Hoewel u een van de opties voor de `azure vm create` opdracht, de volgende demonstreert een zeer eenvoudige benadering:</span><span class="sxs-lookup"><span data-stu-id="77d19-110">Although you may use any of the options for the `azure vm create` command, the following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-the-virtual-machine"></a><span data-ttu-id="77d19-111">Met behulp van aangepaste gegevens in de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="77d19-111">Using custom data in the virtual machine</span></span>
* <span data-ttu-id="77d19-112">Als uw Azure VM een VM op basis van Windows is, wordt het bestand voor aangepaste gegevens wordt opgeslagen in `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="77d19-112">If your Azure VM is a Windows-based VM, then the custom data file is saved to `%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="77d19-113">Hoewel het base64-gecodeerd overzetten van de lokale computer naar de nieuwe virtuele machine, kan deze worden automatisch gedecodeerd en worden geopend of direct gebruikt.</span><span class="sxs-lookup"><span data-stu-id="77d19-113">Although it was base64-encoded to transfer from the local computer to the new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="77d19-114">Als het bestand bestaat, wordt deze overschreven.</span><span class="sxs-lookup"><span data-stu-id="77d19-114">If the file exists, it is overwritten.</span></span> <span data-ttu-id="77d19-115">De beveiliging van de map is ingesteld op **System: volledig beheer** en **Administrators: volledig beheer**.</span><span class="sxs-lookup"><span data-stu-id="77d19-115">The security on the directory is set to **System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="77d19-116">Als uw Azure VM een VM op basis van Linux is, klikt u vervolgens het bestand voor aangepaste gegevens zich in een van de volgende locaties, afhankelijk van uw distro.</span><span class="sxs-lookup"><span data-stu-id="77d19-116">If your Azure VM is a Linux-based VM, then the custom data file will be located in one of the following places depending on your distro.</span></span> <span data-ttu-id="77d19-117">De gegevens zijn mogelijk base64-gecodeerd, dus misschien moet u eerst de gegevens decoderen:</span><span class="sxs-lookup"><span data-stu-id="77d19-117">The data may be base64-encoded, so you may need to decode the data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="77d19-118">Cloud-init op Azure</span><span class="sxs-lookup"><span data-stu-id="77d19-118">Cloud-init on Azure</span></span>
<span data-ttu-id="77d19-119">Als uw Azure VM van een installatiekopie van een Ubuntu of virtuele CoreOS is, kunt u CustomData gebruiken om te verzenden van een cloud-config naar cloud init.</span><span class="sxs-lookup"><span data-stu-id="77d19-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData to send a cloud-config to cloud-init.</span></span> <span data-ttu-id="77d19-120">Of als uw aangepaste gegevensbestand een script is, vervolgens cloud init kunt gewoon uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="77d19-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="77d19-121">Ubuntu Cloud installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="77d19-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="77d19-122">In de meeste Azure Linux-installatiekopieën, bewerkt u zou ' / etc/waagent.conf ' voor het configureren van de tijdelijke schijf en het wisselbestand.</span><span class="sxs-lookup"><span data-stu-id="77d19-122">In most Azure Linux images, you would edit "/etc/waagent.conf" to configure the temporary resource disk and swap file.</span></span> <span data-ttu-id="77d19-123">Zie [gebruikershandleiding voor Azure Linux Agent](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="77d19-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="77d19-124">Echter, op de Ubuntu Cloud-installatiekopieën, moet u cloud-init voor het configureren van de resource-schijf (dat wil zeggen, de 'kortstondige' schijf) en het wisselen van de partitie.</span><span class="sxs-lookup"><span data-stu-id="77d19-124">However, on the Ubuntu Cloud Images, you must use cloud-init to configure the resource disk (that is, the "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="77d19-125">Zie de volgende pagina op de wiki Ubuntu voor meer informatie: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="77d19-125">See the following page on the Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="77d19-126">Volgende stappen: met behulp van cloud-init</span><span class="sxs-lookup"><span data-stu-id="77d19-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="77d19-127">Zie voor meer informatie de [cloud init-documentatie voor Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="77d19-127">For further information, see the [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="77d19-128">Rol van Service Management REST API-verwijzing toevoegen</span><span class="sxs-lookup"><span data-stu-id="77d19-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="77d19-129">Azure-opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="77d19-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

