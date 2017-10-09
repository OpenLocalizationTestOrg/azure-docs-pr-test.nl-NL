
1. <span data-ttu-id="41f25-101">Meld u aan tooyour Azure-abonnement met Hallo stappen in [tooAzure verbinding van hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="41f25-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="41f25-102">Zorg ervoor dat u in Hallo klassieke implementatiemodus zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="41f25-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="41f25-103">Hallo Linux installatiekopie weten dat u wilt dat tooload uit de beschikbare installatiekopieën Hallo als volgt:</span><span class="sxs-lookup"><span data-stu-id="41f25-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="41f25-104">Gebruik in een opdrachtpromptvenster van Windows **find** in plaats van grep.</span><span class="sxs-lookup"><span data-stu-id="41f25-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="41f25-105">Gebruik `azure vm create` toocreate een virtuele machine met Linux-installatiekopie Hallo van Hallo vorige lijst.</span><span class="sxs-lookup"><span data-stu-id="41f25-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="41f25-106">In deze stap maakt u een cloudservice en een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="41f25-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="41f25-107">U kunt ook verbinding maken met deze VM tooan bestaande cloudservice met een `-c` optie.</span><span class="sxs-lookup"><span data-stu-id="41f25-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="41f25-108">Maken van een SSH-eindpunt toolog in toohello virtuele Linux-machine Hello `-e` optie.</span><span class="sxs-lookup"><span data-stu-id="41f25-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="41f25-109">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met Hallo `Ubuntu-14_04_4-LTS` installatiekopie in Hallo `West US` locatie, en voegt u een gebruikersnaam `ops`:</span><span class="sxs-lookup"><span data-stu-id="41f25-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="41f25-110">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="41f25-110">hello output is similar toohello following example:</span></span>

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
   > <span data-ttu-id="41f25-111">Voor een virtuele Linux-machine, moet u opgeven Hallo `-e` optie in `vm create`.</span><span class="sxs-lookup"><span data-stu-id="41f25-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="41f25-112">Het is niet mogelijk tooenable SSH nadat Hallo virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="41f25-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="41f25-113">Lees voor meer informatie over SSH [hoe tooUse SSH met Linux op Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="41f25-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="41f25-114">U kunt Hallo kenmerken van Hallo VM controleren via Hallo `azure vm show` opdracht.</span><span class="sxs-lookup"><span data-stu-id="41f25-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="41f25-115">Hallo volgende voorbeeld vindt u gegevens voor de virtuele machine met de naam Hallo `myVM`:</span><span class="sxs-lookup"><span data-stu-id="41f25-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="41f25-116">Start uw virtuele machine met Hallo `azure vm start` opdracht als volgt:</span><span class="sxs-lookup"><span data-stu-id="41f25-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="41f25-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="41f25-117">Next steps</span></span>
<span data-ttu-id="41f25-118">Lees voor meer informatie over deze opdrachten voor de virtuele machine Azure CLI 1.0 Hallo [Using hello Azure CLI 1.0 met Hallo klassieke implementatie API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="41f25-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

