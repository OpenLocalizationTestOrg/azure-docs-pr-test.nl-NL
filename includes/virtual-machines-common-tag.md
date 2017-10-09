


## <a name="tagging-a-virtual-machine-through-templates"></a><span data-ttu-id="bb97a-101">Labels van een virtuele Machine via sjablonen</span><span class="sxs-lookup"><span data-stu-id="bb97a-101">Tagging a Virtual Machine through Templates</span></span>
<span data-ttu-id="bb97a-102">Eerst gaan we kijken tagging via sjablonen.</span><span class="sxs-lookup"><span data-stu-id="bb97a-102">First, let’s look at tagging through templates.</span></span> <span data-ttu-id="bb97a-103">[Deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) plaatst labels op Hallo volgende resources: Compute (virtuele Machine) en opslag (Storage-Account) netwerk (openbare IP-adres, virtuele netwerk en Network Interface).</span><span class="sxs-lookup"><span data-stu-id="bb97a-103">[This template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) places tags on hello following resources: Compute (Virtual Machine), Storage (Storage Account), and Network (Public IP Address, Virtual Network, and Network Interface).</span></span> <span data-ttu-id="bb97a-104">Deze sjabloon is voor een virtuele machine van Windows, maar kan worden aangepast voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="bb97a-104">This template is for a Windows VM but can be adapted for Linux VMs.</span></span>

<span data-ttu-id="bb97a-105">Klik op Hallo **implementeren tooAzure** knop van Hallo [sjabloonkoppeling](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span><span class="sxs-lookup"><span data-stu-id="bb97a-105">Click hello **Deploy tooAzure** button from hello [template link](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags).</span></span> <span data-ttu-id="bb97a-106">Dit, gaat u toohello [Azure-portal](https://portal.azure.com/) waarin u deze sjabloon kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="bb97a-106">This will navigate toohello [Azure portal](https://portal.azure.com/) where you can deploy this template.</span></span>

![Eenvoudige implementatie met labels](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

<span data-ttu-id="bb97a-108">Deze sjabloon bevat Hallo tags te volgen: *afdeling*, *toepassing*, en *gemaakt door*.</span><span class="sxs-lookup"><span data-stu-id="bb97a-108">This template includes hello following tags: *Department*, *Application*, and *Created By*.</span></span> <span data-ttu-id="bb97a-109">U kunt toevoegen/bewerken deze tags rechtstreeks in de sjabloon Hallo indien andere tagnaam gewenst.</span><span class="sxs-lookup"><span data-stu-id="bb97a-109">You can add/edit these tags directly in hello template if you would like different tag names.</span></span>

![Azure labels in een sjabloon](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

<span data-ttu-id="bb97a-111">Zoals u ziet, worden Hallo labels worden gedefinieerd als sleutel-waardeparen, gescheiden door een dubbele punt (:).</span><span class="sxs-lookup"><span data-stu-id="bb97a-111">As you can see, hello tags are defined as key/value pairs, separated by a colon (:).</span></span> <span data-ttu-id="bb97a-112">Hallo-labels moeten worden gedefinieerd in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="bb97a-112">hello tags must be defined in this format:</span></span>

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

<span data-ttu-id="bb97a-113">Hallo-sjabloonbestand opslaan als u klaar bent met het bewerken met labels Hallo van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="bb97a-113">Save hello template file after you finish editing it with hello tags of your choice.</span></span>

<span data-ttu-id="bb97a-114">Vervolgens gaat u naar Hallo **Parameters bewerken** sectie u vult Hallo waarden voor de labels.</span><span class="sxs-lookup"><span data-stu-id="bb97a-114">Next, in hello **Edit Parameters** section, you can fill out hello values for your tags.</span></span>

![Labels bewerken in Azure-portal](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

<span data-ttu-id="bb97a-116">Klik op **maken** toodeploy deze sjabloon met de waarden van uw code.</span><span class="sxs-lookup"><span data-stu-id="bb97a-116">Click **Create** toodeploy this template with your tag values.</span></span>

## <a name="tagging-through-hello-portal"></a><span data-ttu-id="bb97a-117">Via de Portal Hallo-tagging</span><span class="sxs-lookup"><span data-stu-id="bb97a-117">Tagging through hello Portal</span></span>
<span data-ttu-id="bb97a-118">Na het maken van uw resources met labels, kunt u weergeven, toevoegen en verwijderen van labels in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="bb97a-118">After creating your resources with tags, you can view, add, and delete tags in hello portal.</span></span>

<span data-ttu-id="bb97a-119">Selecteer Hallo labels pictogram tooview de labels:</span><span class="sxs-lookup"><span data-stu-id="bb97a-119">Select hello tags icon tooview your tags:</span></span>

![Pictogram van de labels in Azure-portal](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

<span data-ttu-id="bb97a-121">Een nieuwe code via Hallo portal door te definiëren van uw eigen sleutel-waardepaar toevoegt en sla het.</span><span class="sxs-lookup"><span data-stu-id="bb97a-121">Add a new tag through hello portal by defining your own Key/Value pair, and save it.</span></span>

![Nieuw label toevoegen in Azure-portal](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

<span data-ttu-id="bb97a-123">Uw nieuwe code wordt nu weergegeven in de lijst Hallo van codes voor uw resource.</span><span class="sxs-lookup"><span data-stu-id="bb97a-123">Your new tag should now appear in hello list of tags for your resource.</span></span>

![Nieuwe code opgeslagen in Azure-portal](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

