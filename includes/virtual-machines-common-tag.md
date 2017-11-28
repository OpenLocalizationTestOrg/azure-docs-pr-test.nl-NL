


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="e1479-101">Labels van een virtuele Machine via sjablonen</span><span class="sxs-lookup"><span data-stu-id="e1479-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="e1479-102">Eerst gaan we kijken tagging via sjablonen.</span><span class="sxs-lookup"><span data-stu-id="e1479-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="e1479-103">[Deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) plaatst labels op de volgende bronnen: Compute (virtuele Machine) en opslag (Storage-Account) netwerk (openbare IP-adres, virtuele netwerk en Network Interface).</span><span class="sxs-lookup"><span data-stu-id="e1479-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on the following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="e1479-104">Deze sjabloon is voor een virtuele machine van Windows, maar kan worden aangepast voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="e1479-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="e1479-105">Klik op de **implementeren in Azure** knop van de [sjabloonkoppeling](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="e1479-105">Click the **Deploy to Azure** button from the [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="e1479-106">Dit, gaat u naar de [Azure-portal](https://portal.azure.com/) waarin u deze sjabloon kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="e1479-106">This will navigate to the [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Eenvoudige implementatie met labels](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="e1479-108">Deze sjabloon bevat de volgende codes: *afdeling*, *toepassing*, en *gemaakt door*.</span><span class="sxs-lookup"><span data-stu-id="e1479-108">This template includes the following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="e1479-109">U kunt toevoegen/bewerken deze tags rechtstreeks in de sjabloon indien andere tagnaam gewenst.</span><span class="sxs-lookup"><span data-stu-id="e1479-109">You can add/edit these tags directly in the template if you would like different tag names.</span></span>

![Azure labels in een sjabloon](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="e1479-111">Zoals u ziet, worden de labels worden gedefinieerd als sleutel-waardeparen, gescheiden door een dubbele punt (:).</span><span class="sxs-lookup"><span data-stu-id="e1479-111">As you can see, the tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="e1479-112">De labels moeten worden gedefinieerd in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="e1479-112">The tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="e1479-113">Sla het sjabloonbestand nadat u deze bewerken met de labels van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="e1479-113">Save the template file after you finish editing it with the tags of your choice.</span></span>

<span data-ttu-id="e1479-114">Vervolgens gaat u naar de **Parameters bewerken** sectie, kunt u de waarden invullen voor de labels.</span><span class="sxs-lookup"><span data-stu-id="e1479-114">Next, in the **Edit Parameters** section, you can fill out the values for your tags.</span></span>

![Labels bewerken in Azure-portal](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="e1479-116">Klik op **maken** om deze sjabloon met de waarden van uw code te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e1479-116">Click **Create** to deploy this template with your tag values.</span></span>

## <a name="tagging-through-the-portal"></a><span data-ttu-id="e1479-117">Via de Portal-tagging</span><span class="sxs-lookup"><span data-stu-id="e1479-117">Tagging through the Portal</span></span>
<span data-ttu-id="e1479-118">Na het maken van uw resources met labels, kunt u weergeven, toevoegen en verwijderen van de labels in de portal.</span><span class="sxs-lookup"><span data-stu-id="e1479-118">After creating your resources with tags, you can view, add, and delete tags in the portal.</span></span>

<span data-ttu-id="e1479-119">Selecteer het pictogram labels de labels weergeven:</span><span class="sxs-lookup"><span data-stu-id="e1479-119">Select the tags icon to view your tags:</span></span>

![Pictogram van de labels in Azure-portal](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="e1479-121">Een nieuwe code via de portal door te definiëren van uw eigen sleutel-waardepaar toevoegt en sla het.</span><span class="sxs-lookup"><span data-stu-id="e1479-121">Add a new tag through the portal by defining your own Key/Value pair, and save it.</span></span>

![Nieuw label toevoegen in Azure-portal](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="e1479-123">Uw nieuwe code wordt nu weergegeven in de lijst met labels voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="e1479-123">Your new tag should now appear in the list of tags for your resource.</span></span>

![Nieuwe code opgeslagen in Azure-portal](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

