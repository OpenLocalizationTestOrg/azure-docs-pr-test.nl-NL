## <a name="create-a-resource-group"></a><span data-ttu-id="c2277-101">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="c2277-101">Create a resource group</span></span>

<span data-ttu-id="c2277-102">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c2277-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="c2277-103">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="c2277-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="c2277-104">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="c2277-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="c2277-105">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="c2277-105">Create a virtual machine</span></span>

<span data-ttu-id="c2277-106">Een virtuele machine maken met de Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c2277-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="c2277-107">Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* en SSH-sleutels gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="c2277-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="c2277-108">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="c2277-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="c2277-109">Wanneer Hallo VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="c2277-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="c2277-110">Let op Hallo `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="c2277-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="c2277-111">Dit adres is gebruikte tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="c2277-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="c2277-112">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="c2277-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="c2277-113">Standaard worden alleen SSH-verbindingen zijn toegestaan in Linux VM's geïmplementeerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2277-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="c2277-114">Omdat deze virtuele machine toobe een webserver gaat, moet u tooopen poort 80 van Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="c2277-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="c2277-115">Gebruik Hallo [az vm open poort](/cli/azure/vm#open-port) opdracht tooopen Hallo gewenst poort.</span><span class="sxs-lookup"><span data-stu-id="c2277-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="c2277-116">SSH in uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="c2277-116">SSH into your VM</span></span>


<span data-ttu-id="c2277-117">Als u niet al weet Hallo openbare IP-adres van uw virtuele machine, Voer Hallo [az netwerk openbare ip-lijst](/cli/azure/network/public-ip#list) opdracht:</span><span class="sxs-lookup"><span data-stu-id="c2277-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="c2277-118">Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c2277-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="c2277-119">Vervang Hallo juiste openbare IP-adres van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="c2277-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="c2277-120">In dit voorbeeld Hallo IP-adres is *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="c2277-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

