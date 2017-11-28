
1. <span data-ttu-id="4cd98-101">Meld u aan bij uw Azure-abonnement met behulp van de stappen in [Connect to Azure from the Azure CLI 1.0](../articles/xplat-cli-connect.md) (Verbinding maken met Azure via de Azure CLI 1.0).</span><span class="sxs-lookup"><span data-stu-id="4cd98-101">Sign in to your Azure subscription using the steps listed in [Connect to Azure from the Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="4cd98-102">Zorg er als volgt voor dat u zich in de klassieke implementatiemodus bevindt:</span><span class="sxs-lookup"><span data-stu-id="4cd98-102">Make sure you are in the Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="4cd98-103">Doe het volgende om de Linux-installatiekopie te zoeken die u wilt laden:</span><span class="sxs-lookup"><span data-stu-id="4cd98-103">Find out the Linux image that you want to load from the available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="4cd98-104">Gebruik in een opdrachtpromptvenster van Windows **find** in plaats van grep.</span><span class="sxs-lookup"><span data-stu-id="4cd98-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="4cd98-105">Gebruik `azure vm create` om een virtuele machine te maken met de Linux-installatiekopie uit de vorige lijst.</span><span class="sxs-lookup"><span data-stu-id="4cd98-105">Use `azure vm create` to create a VM with the Linux image from the previous list.</span></span> <span data-ttu-id="4cd98-106">In deze stap maakt u een cloudservice en een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4cd98-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="4cd98-107">U kunt deze virtuele machine ook verbinden met een bestaande cloudservice met de optie `-c`.</span><span class="sxs-lookup"><span data-stu-id="4cd98-107">You could also connect this VM to an existing cloud service with a `-c` option.</span></span> <span data-ttu-id="4cd98-108">Maak een SSH-eindpunt voor aanmelding bij de virtuele Linux-machine met de optie `-e`.</span><span class="sxs-lookup"><span data-stu-id="4cd98-108">Create an SSH endpoint to log in to the Linux virtual machine with the `-e` option.</span></span> <span data-ttu-id="4cd98-109">In het volgende voorbeeld wordt een virtuele machine met de naam `myVM` gemaakt met behulp van de installatiekopie `Ubuntu-14_04_4-LTS` op de locatie `West US`, en voegt u de gebruikersnaam `ops` toe:</span><span class="sxs-lookup"><span data-stu-id="4cd98-109">The following example creates a VM named `myVM` using the `Ubuntu-14_04_4-LTS` image in the `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="4cd98-110">De uitvoer lijkt op die in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4cd98-110">The output is similar to the following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4cd98-111">Voor een virtuele Linux-machine moet u de optie `-e` opgeven in `vm create`.</span><span class="sxs-lookup"><span data-stu-id="4cd98-111">For a Linux virtual machine, you must provide the `-e` option in `vm create`.</span></span> <span data-ttu-id="4cd98-112">Het is niet mogelijk om SSH in te schakelen nadat de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4cd98-112">It is not possible to enable SSH after the virtual machine has been created.</span></span> <span data-ttu-id="4cd98-113">Zie voor meer informatie over SSH [SSH gebruiken met Linux op Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cd98-113">For more details on SSH, read [How to Use SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="4cd98-114">U kunt de kenmerken van de virtuele machine controleren via de opdracht `azure vm show`.</span><span class="sxs-lookup"><span data-stu-id="4cd98-114">You can verify the attributes of the VM by using the `azure vm show` command.</span></span> <span data-ttu-id="4cd98-115">In het volgende voorbeeld worden gegevens weergegeven voor de virtuele machine met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4cd98-115">The following example lists information for the VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="4cd98-116">Start de virtuele machine als volgt met de opdracht `azure vm start`:</span><span class="sxs-lookup"><span data-stu-id="4cd98-116">Start your VM with the `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="4cd98-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4cd98-117">Next steps</span></span>
<span data-ttu-id="4cd98-118">Lees voor meer informatie over deze Azure CLI 1.0-opdrachten voor virtuele machines [Using the Azure CLI 1.0 with the Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) (De Azure CLI 1.0 gebruiken met de API voor klassieke implementatie).</span><span class="sxs-lookup"><span data-stu-id="4cd98-118">For details on all these Azure CLI 1.0 virtual machine commands, read the [Using the Azure CLI 1.0 with the Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

