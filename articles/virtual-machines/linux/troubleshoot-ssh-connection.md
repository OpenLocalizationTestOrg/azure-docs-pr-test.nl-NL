---
title: Problemen met SSH-verbinding naar een Azure-virtuele machine | Microsoft Docs
description: Klik hier voor meer informatie over het oplossen van problemen zoals 'SSH-verbinding is mislukt' of 'SSH-verbinding geweigerd' voor een virtuele machine van Azure waarop Linux wordt uitgevoerd.
keywords: SSH verbinding geweigerd, ssh fout, azure ssh, SSH-verbinding is mislukt
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: top-support-issue,azure-service-management,azure-resource-manager
ms.assetid: dcb82e19-29b2-47bb-99f2-900d4cfb5bbb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: iainfou
ms.openlocfilehash: 3a282c8b2c2ba2749de6a2d3688bd57d75703b22
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-ssh-connections-to-an-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="3f21c-104">Problemen met SSH-verbindingen met een Azure Linux VM die is mislukt, fouten, of wordt geweigerd</span><span class="sxs-lookup"><span data-stu-id="3f21c-104">Troubleshoot SSH connections to an Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="3f21c-105">Er zijn diverse redenen dat u op problemen Secure Shell (SSH), SSH verbindingsfouten stuit, of SSH wordt geweigerd wanneer u probeert verbinding maken met virtuele Linux-machine (VM).</span><span class="sxs-lookup"><span data-stu-id="3f21c-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try to connect to a Linux virtual machine (VM).</span></span> <span data-ttu-id="3f21c-106">Dit artikel helpt u bij het vinden en los de problemen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-106">This article helps you find and correct the problems.</span></span> <span data-ttu-id="3f21c-107">U kunt de Azure-portal, Azure CLI of uitbreiding van de VM-toegang voor Linux kunt oplossen van problemen met de verbinding.</span><span class="sxs-lookup"><span data-stu-id="3f21c-107">You can use the Azure portal, Azure CLI, or VM Access Extension for Linux to troubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3f21c-108">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u de Azure-experts raadplegen op [MSDN Azure en Stack Overflow-forums](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="3f21c-108">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="3f21c-109">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="3f21c-110">Ga naar de [ondersteuning van Azure site](http://azure.microsoft.com/support/options/) en selecteer **ondersteuning krijgen**.</span><span class="sxs-lookup"><span data-stu-id="3f21c-110">Go to the [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="3f21c-111">Voor meer informatie over het gebruik van Azure ondersteuning voor de [ondersteuning van Microsoft Azure Veelgestelde vragen over](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="3f21c-111">For information about using Azure Support, read the [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="3f21c-112">Snelle stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="3f21c-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="3f21c-113">Probeer opnieuw verbinding te maken met de virtuele machine na elke stap.</span><span class="sxs-lookup"><span data-stu-id="3f21c-113">After each troubleshooting step, try reconnecting to the VM.</span></span>

1. <span data-ttu-id="3f21c-114">De SSH-configuratie opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-114">Reset the SSH configuration.</span></span>
2. <span data-ttu-id="3f21c-115">Stel de referenties voor de gebruiker opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="3f21c-115">Reset the credentials for the user.</span></span>
3. <span data-ttu-id="3f21c-116">Controleer of de [Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) regels SSH-verkeer toestaan.</span><span class="sxs-lookup"><span data-stu-id="3f21c-116">Verify the [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="3f21c-117">Zorg ervoor dat een Netwerkbeveiligingsgroep-regel bestaat voor de SSH-verkeer toestaan (standaard TCP-poort 22).</span><span class="sxs-lookup"><span data-stu-id="3f21c-117">Ensure that a Network Security Group rule exists to permit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="3f21c-118">U kunt geen poortomleiding gebruiken / toewijzen zonder gebruik van een Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f21c-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="3f21c-119">Controleer de [VM resourcestatus](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f21c-119">Check the [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="3f21c-120">Zorg ervoor dat de virtuele machine als goed rapporteert.</span><span class="sxs-lookup"><span data-stu-id="3f21c-120">Ensure that the VM reports as being healthy.</span></span>
   * <span data-ttu-id="3f21c-121">Als er diagnostische gegevens over opstarten is ingeschakeld, controleert u of dat de virtuele machine is niet rapportage van fouten in de logboeken.</span><span class="sxs-lookup"><span data-stu-id="3f21c-121">If you have boot diagnostics enabled, verify the VM is not reporting boot errors in the logs.</span></span>
5. <span data-ttu-id="3f21c-122">Start opnieuw op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3f21c-122">Restart the VM.</span></span>
6. <span data-ttu-id="3f21c-123">Implementeer de virtuele machine opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3f21c-123">Redeploy the VM.</span></span>

<span data-ttu-id="3f21c-124">Blijven lezen voor meer gedetailleerde stappen voor probleemoplossing en uitleg.</span><span class="sxs-lookup"><span data-stu-id="3f21c-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-to-troubleshoot-ssh-connection-issues"></a><span data-ttu-id="3f21c-125">Beschikbare methoden voor het oplossen van problemen met SSH-verbinding</span><span class="sxs-lookup"><span data-stu-id="3f21c-125">Available methods to troubleshoot SSH connection issues</span></span>
<span data-ttu-id="3f21c-126">U kunt opnieuw instellen van referenties of SSH-configuratie met een van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="3f21c-126">You can reset credentials or SSH configuration using one of the following methods:</span></span>

* <span data-ttu-id="3f21c-127">[Azure-portal](#use-the-azure-portal) - handig als u opnieuw wilt instellen snel de SSH-configuratie of de SSH-sleutel en u de Azure-hulpprogramma's geïnstalleerd hoeft.</span><span class="sxs-lookup"><span data-stu-id="3f21c-127">[Azure portal](#use-the-azure-portal) - great if you need to quickly reset the SSH configuration or SSH key and you don't have the Azure tools installed.</span></span>
* <span data-ttu-id="3f21c-128">[Azure CLI 2.0](#use-the-azure-cli-20) : als u zich al op de opdrachtregel snel opnieuw instellen van de SSH-configuratie of de referenties.</span><span class="sxs-lookup"><span data-stu-id="3f21c-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on the command line, quickly reset the SSH configuration or credentials.</span></span> <span data-ttu-id="3f21c-129">U kunt ook de [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="3f21c-129">You can also use the [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="3f21c-130">[Azure VMAccessForLinux-extensie](#use-the-vmaccess-extension) - maken en gebruiken als json-definitiebestanden om in te stellen van de SSH-configuratie of gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="3f21c-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files to reset the SSH configuration or user credentials.</span></span>

<span data-ttu-id="3f21c-131">Probeer opnieuw verbinding te maken met uw virtuele machine na elke stap voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="3f21c-131">After each troubleshooting step, try connecting to your VM again.</span></span> <span data-ttu-id="3f21c-132">Als u nog steeds geen verbinding maken, probeert u de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="3f21c-132">If you still cannot connect, try the next step.</span></span>

## <a name="use-the-azure-portal"></a><span data-ttu-id="3f21c-133">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="3f21c-133">Use the Azure portal</span></span>
<span data-ttu-id="3f21c-134">De Azure portal biedt een snelle manier om in te stellen van de SSH-configuratie of de gebruiker referenties zonder alle hulpprogramma's te installeren op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="3f21c-134">The Azure portal provides a quick way to reset the SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="3f21c-135">Selecteer uw virtuele machine in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3f21c-135">Select your VM in the Azure portal.</span></span> <span data-ttu-id="3f21c-136">Schuif omlaag naar de **ondersteuning + probleemoplossing** sectie en selecteer **wachtwoord opnieuw instellen** zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3f21c-136">Scroll down to the **Support + Troubleshooting** section and select **Reset password** as in the following example:</span></span>

![SSH-configuratie of de referenties in de Azure-portal opnieuw instellen](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-the-ssh-configuration"></a><span data-ttu-id="3f21c-138">De SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-138">Reset the SSH configuration</span></span>
<span data-ttu-id="3f21c-139">Selecteer als eerste stap `Reset configuration only` van de **modus** Vervolgkeuzelijst als in de vorige schermafbeelding klik vervolgens op de **opnieuw instellen** knop.</span><span class="sxs-lookup"><span data-stu-id="3f21c-139">As a first step, select `Reset configuration only` from the **Mode** drop-down menu as in the preceding screenshot, then click the **Reset** button.</span></span> <span data-ttu-id="3f21c-140">Zodra deze actie is voltooid, probeert u opnieuw toegang krijgen tot uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3f21c-140">Once this action has completed, try to access your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="3f21c-141">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="3f21c-142">Als u de referenties van een bestaande gebruiker herstellen, selecteert u `Reset SSH public key` of `Reset password` van de **modus** vervolgkeuzelijst zoals in de vorige schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="3f21c-142">To reset the credentials of an existing user, select either `Reset SSH public key` or `Reset password` from the **Mode** drop-down menu as in the preceding screenshot.</span></span> <span data-ttu-id="3f21c-143">Geef de gebruikersnaam en een SSH-sleutel of het nieuwe wachtwoord en klik op de **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="3f21c-143">Specify the username and an SSH key or new password, then click the **Reset** button.</span></span>

<span data-ttu-id="3f21c-144">U kunt ook een gebruiker met sudo-machtigingen op de virtuele machine vanaf dit menu maken.</span><span class="sxs-lookup"><span data-stu-id="3f21c-144">You can also create a user with sudo privileges on the VM from this menu.</span></span> <span data-ttu-id="3f21c-145">Voer een nieuwe gebruikersnaam en het bijbehorende wachtwoord of de SSH-sleutel en klik vervolgens op de **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="3f21c-145">Enter a new username and associated password or SSH key, and then click the **Reset** button.</span></span>

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="3f21c-146">De Azure CLI 2.0 gebruiken</span><span class="sxs-lookup"><span data-stu-id="3f21c-146">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="3f21c-147">Als u nog niet gedaan hebt, installeert u de nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u aan op een Azure-account met [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="3f21c-147">If you haven't already, install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="3f21c-148">Als u hebt gemaakt en de installatiekopie van een aangepaste Linux-schijf geüpload, controleert u of de [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versie 2.0.5 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3f21c-148">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="3f21c-149">VM's zijn gemaakt met behulp van afbeeldingen, is deze uitbreiding voor toegang tot al geïnstalleerd en geconfigureerd voor u.</span><span class="sxs-lookup"><span data-stu-id="3f21c-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="3f21c-150">SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-150">Reset SSH configuration</span></span>
<span data-ttu-id="3f21c-151">U kunt in eerste instantie voor het instellen van de SSH-configuratie op de standaardwaarden en de SSH-server op de virtuele machine opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="3f21c-151">You can initially try resetting the SSH configuration to default values and rebooting the SSH server on the VM.</span></span> <span data-ttu-id="3f21c-152">Houd er rekening mee dat dit niet de gebruikersnaam, wachtwoord of SSH-sleutels wijzigt.</span><span class="sxs-lookup"><span data-stu-id="3f21c-152">Note that this does not change the user account name, password, or SSH keys.</span></span>
<span data-ttu-id="3f21c-153">Het volgende voorbeeld wordt [az vm gebruiker opnieuw instellen-ssh](/cli/azure/vm/user#reset-ssh) opnieuw instellen van de SSH-configuratie op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-153">The following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) to reset the SSH configuration on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-154">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="3f21c-155">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="3f21c-156">Het volgende voorbeeld wordt [az vm gebruikersupdate](/cli/azure/vm/user#update) opnieuw instellen van de referenties voor `myUsername` op de waarde die is opgegeven in `myPassword`, op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-156">The following example uses [az vm user update](/cli/azure/vm/user#update) to reset the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-157">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="3f21c-158">Als u verificatie van SSH-sleutel gebruikt, kunt u de SSH-sleutel voor een bepaalde gebruiker herstellen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-158">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="3f21c-159">Het volgende voorbeeld wordt **az vm set-linux-gebruikers toegang tot** bijwerken van de SSH-sleutel die is opgeslagen in `~/.ssh/id_rsa.pub` voor de gebruiker met de naam `myUsername`, op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-159">The following example uses **az vm access set-linux-user** to update the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-160">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-the-vmaccess-extension"></a><span data-ttu-id="3f21c-161">Gebruik de VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="3f21c-161">Use the VMAccess extension</span></span>
<span data-ttu-id="3f21c-162">De VM-extensie voor toegang voor Linux wordt gelezen in een json-bestand dat acties definieert uit te voeren. Deze acties omvatten opnieuw instellen van SSHD, opnieuw instellen van een SSH-sleutel of een gebruiker toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-162">The VM Access Extension for Linux reads in a json file that defines actions to carry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="3f21c-163">U nog steeds de Azure CLI gebruiken om aan te roepen de VMAccess-extensie, maar u kunt de json-bestanden hergebruiken over meerdere VM's, indien gewenst.</span><span class="sxs-lookup"><span data-stu-id="3f21c-163">You still use the Azure CLI to call the VMAccess extension, but you can reuse the json files across multiple VMs if desired.</span></span> <span data-ttu-id="3f21c-164">Deze aanpak kunt u een opslagplaats voor json-bestanden die vervolgens kan worden aangeroepen voor bepaalde scenario's maken.</span><span class="sxs-lookup"><span data-stu-id="3f21c-164">This approach allows you to create a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="3f21c-165">SSHD opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-165">Reset SSHD</span></span>
<span data-ttu-id="3f21c-166">Maak een bestand met de naam `settings.json` met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="3f21c-166">Create a file named `settings.json` with the following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="3f21c-167">De Azure CLI, u vervolgens aanroepen de `VMAccessForLinux` uitbreiding opnieuw instellen van uw SSHD-verbinding door te geven van uw json-bestand.</span><span class="sxs-lookup"><span data-stu-id="3f21c-167">Using the Azure CLI, you then call the `VMAccessForLinux` extension to reset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="3f21c-168">Het volgende voorbeeld wordt [az vm-extensie set](/cli/azure/vm/extension#set) opnieuw in te stellen SSHD op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-168">The following example uses [az vm extension set](/cli/azure/vm/extension#set) to reset SSHD on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-169">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="3f21c-170">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="3f21c-171">Als SSHD lijkt te laten functioneren, kunt u de referenties voor een afzender gebruiker opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-171">If SSHD appears to function correctly, you can reset the credentials for a giver user.</span></span> <span data-ttu-id="3f21c-172">Als u het wachtwoord voor een gebruiker herstellen, maakt u een bestand met de naam `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-172">To reset the password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="3f21c-173">Het volgende voorbeeld worden de referenties voor `myUsername` op de waarde die is opgegeven in `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-173">The following example resets the credentials for `myUsername` to the value specified in `myPassword`.</span></span> <span data-ttu-id="3f21c-174">Voer de volgende regels in uw `settings.json` -bestand, met behulp van uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="3f21c-174">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="3f21c-175">Of als u de SSH-sleutel voor een gebruiker herstellen, moet u eerst een bestand met de naam maken `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-175">Or to reset the SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="3f21c-176">Het volgende voorbeeld worden de referenties voor `myUsername` op de waarde die is opgegeven in `myPassword`, op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-176">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-177">Voer de volgende regels in uw `settings.json` -bestand, met behulp van uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="3f21c-177">Enter the following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="3f21c-178">Nadat uw json-bestand is gemaakt, kunt u de Azure CLI gebruiken om aan te roepen de `VMAccessForLinux` uitbreiding opnieuw instellen van uw SSH-gebruikersreferenties door te geven van uw json-bestand.</span><span class="sxs-lookup"><span data-stu-id="3f21c-178">After creating your json file, use the Azure CLI to call the `VMAccessForLinux` extension to reset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="3f21c-179">Het volgende voorbeeld worden de referenties op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-179">The following example resets credentials on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-180">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="3f21c-181">Gebruik de Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3f21c-181">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="3f21c-182">Als u dat nog niet gedaan hebt, [installeren van de Azure CLI 1.0 en maak verbinding met uw Azure-abonnement](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3f21c-182">If you haven't already, [install the Azure CLI 1.0 and connect to your Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="3f21c-183">Zorg ervoor dat u van Resource Manager-modus als volgt gebruikmaakt:</span><span class="sxs-lookup"><span data-stu-id="3f21c-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="3f21c-184">Als u hebt gemaakt en de installatiekopie van een aangepaste Linux-schijf geüpload, controleert u of de [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versie 2.0.5 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3f21c-184">If you created and uploaded a custom Linux disk image, make sure the [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="3f21c-185">VM's zijn gemaakt met behulp van afbeeldingen, is deze uitbreiding voor toegang tot al geïnstalleerd en geconfigureerd voor u.</span><span class="sxs-lookup"><span data-stu-id="3f21c-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="3f21c-186">SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-186">Reset SSH configuration</span></span>
<span data-ttu-id="3f21c-187">De configuratie van de SSHD is mogelijk onjuist geconfigureerd of de service is een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="3f21c-187">The SSHD configuration itself may be misconfigured or the service encountered an error.</span></span> <span data-ttu-id="3f21c-188">U kunt herstellen SSHD om ervoor te zorgen dat de SSH-configuratie zelf is geldig.</span><span class="sxs-lookup"><span data-stu-id="3f21c-188">You can reset SSHD to make sure the SSH configuration itself is valid.</span></span> <span data-ttu-id="3f21c-189">Opnieuw instellen van SSHD, moet de eerste probleemoplossing die u rekening houden.</span><span class="sxs-lookup"><span data-stu-id="3f21c-189">Resetting SSHD should be the first troubleshooting step you take.</span></span>

<span data-ttu-id="3f21c-190">Het volgende voorbeeld wordt SSHD op een virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-190">The following example resets SSHD on a VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-191">Uw eigen namen voor virtuele machine en de resource als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="3f21c-192">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="3f21c-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="3f21c-193">Als SSHD lijkt te laten functioneren, kunt u het wachtwoord voor een afzender gebruiker opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-193">If SSHD appears to function correctly, you can reset the password for a giver user.</span></span> <span data-ttu-id="3f21c-194">Het volgende voorbeeld worden de referenties voor `myUsername` op de waarde die is opgegeven in `myPassword`, op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-194">The following example resets the credentials for `myUsername` to the value specified in `myPassword`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-195">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="3f21c-196">Als u verificatie van SSH-sleutel gebruikt, kunt u de SSH-sleutel voor een bepaalde gebruiker herstellen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-196">If using SSH key authentication, you can reset the SSH key for a given user.</span></span> <span data-ttu-id="3f21c-197">De SSH-sleutel die is opgeslagen in het volgende voorbeeld-updates `~/.ssh/id_rsa.pub` voor de gebruiker met de naam `myUsername`, op de virtuele machine met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-197">The following example updates the SSH key stored in `~/.ssh/id_rsa.pub` for the user named `myUsername`, on the VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-198">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="3f21c-199">Een VM opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="3f21c-199">Restart a VM</span></span>
<span data-ttu-id="3f21c-200">Als u opnieuw instellen van de SSH-configuratie en de gebruikersreferenties, of is een fout opgetreden in dat geval, kunt u proberen opnieuw starten van de virtuele machine naar adres onderliggende compute-problemen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-200">If you have reset the SSH configuration and user credentials, or encountered an error in doing so, you can try restarting the VM to address underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="3f21c-201">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3f21c-201">Azure portal</span></span>
<span data-ttu-id="3f21c-202">Als u wilt starten op een virtuele machine met de Azure portal, selecteer uw virtuele machine en klik op de **opnieuw** knop zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3f21c-202">To restart a VM using the Azure portal, select your VM and click the **Restart** button as in the following example:</span></span>

![Opnieuw opstarten van een virtuele machine in de Azure-portal](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="3f21c-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3f21c-204">Azure CLI 1.0</span></span>
<span data-ttu-id="3f21c-205">Het volgende voorbeeld start de virtuele machine met de naam opnieuw `myVM` in de resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-205">The following example restarts the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-206">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="3f21c-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3f21c-207">Azure CLI 2.0</span></span>
<span data-ttu-id="3f21c-208">Het volgende voorbeeld wordt [az vm opnieuw](/cli/azure/vm#restart) opnieuw opstarten van de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-208">The following example uses [az vm restart](/cli/azure/vm#restart) to restart the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-209">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="3f21c-210">Een virtuele machine opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="3f21c-210">Redeploy a VM</span></span>
<span data-ttu-id="3f21c-211">U kunt een virtuele machine naar een ander knooppunt in Azure, die mogelijk onderliggende netwerkproblemen opgelost opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="3f21c-211">You can redeploy a VM to another node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="3f21c-212">Zie voor meer informatie over het opnieuw distribueren van een virtuele machine [opnieuw implementeren van virtuele machine naar een nieuw Azure knooppunt](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f21c-212">For information about redeploying a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="3f21c-213">Nadat deze is voltooid, kortstondige schijfgegevens niet verloren en dynamische IP-adressen die gekoppeld aan de virtuele machine zijn wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="3f21c-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="3f21c-214">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3f21c-214">Azure portal</span></span>
<span data-ttu-id="3f21c-215">Als u wilt implementeren op een virtuele machine met de Azure portal, selecteert u de virtuele machine en schuif omlaag naar de **ondersteuning + probleemoplossing** sectie.</span><span class="sxs-lookup"><span data-stu-id="3f21c-215">To redeploy a VM using the Azure portal, select your VM and scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="3f21c-216">Klik op de **implementeren** knop zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3f21c-216">Click the **Redeploy** button as in the following example:</span></span>

![Implementeren van een virtuele machine in de Azure portal](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="3f21c-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="3f21c-218">Azure CLI 1.0</span></span>
<span data-ttu-id="3f21c-219">Het volgende voorbeeld de virtuele machine met de naam redeploys `myVM` in de resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-219">The following example redeploys the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-220">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="3f21c-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3f21c-221">Azure CLI 2.0</span></span>
<span data-ttu-id="3f21c-222">Het volgende Voorbeeldgebruik [az vm opnieuw distribueren](/cli/azure/vm#redeploy) te implementeren van de virtuele machine met de naam `myVM` in de resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="3f21c-222">The following example use [az vm redeploy](/cli/azure/vm#redeploy) to redeploy the VM named `myVM` in the resource group named `myResourceGroup`.</span></span> <span data-ttu-id="3f21c-223">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f21c-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-the-classic-deployment-model"></a><span data-ttu-id="3f21c-224">Virtuele machines die zijn gemaakt met behulp van het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="3f21c-224">VMs created by using the Classic deployment model</span></span>
<span data-ttu-id="3f21c-225">Probeer deze stappen voor het oplossen van de meest voorkomende fouten van de SSH-verbinding voor VM's die zijn gemaakt met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3f21c-225">Try these steps to resolve the most common SSH connection failures for VMs that were created by using the classic deployment model.</span></span> <span data-ttu-id="3f21c-226">Probeer opnieuw verbinding te maken met de virtuele machine na elke stap.</span><span class="sxs-lookup"><span data-stu-id="3f21c-226">After each step, try reconnecting to the VM.</span></span>

* <span data-ttu-id="3f21c-227">Opnieuw instellen van externe toegang van de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f21c-227">Reset remote access from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="3f21c-228">De Azure-portal, selecteer uw virtuele machine en klik op de **extern opnieuw instellen...**  knop.</span><span class="sxs-lookup"><span data-stu-id="3f21c-228">On the Azure portal, select your VM and click the **Reset Remote...** button.</span></span>
* <span data-ttu-id="3f21c-229">Start opnieuw op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3f21c-229">Restart the VM.</span></span> <span data-ttu-id="3f21c-230">Op de [Azure-portal](https://portal.azure.com), selecteert u de virtuele machine en klik op de **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="3f21c-230">On the [Azure portal](https://portal.azure.com), select your VM and click the **Restart** button.</span></span>
    
* <span data-ttu-id="3f21c-231">Implementeer de virtuele machine naar een nieuw Azure knooppunt opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3f21c-231">Redeploy the VM to a new Azure node.</span></span> <span data-ttu-id="3f21c-232">Zie voor meer informatie over het implementeren van een virtuele machine [opnieuw implementeren van virtuele machine naar een nieuw Azure knooppunt](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f21c-232">For information about how to redeploy a VM, see [Redeploy virtual machine to new Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="3f21c-233">Nadat deze is voltooid, kortstondige schijfgegevens niet verloren en dynamische IP-adressen die gekoppeld aan de virtuele machine zijn wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="3f21c-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with the virtual machine will be updated.</span></span>
* <span data-ttu-id="3f21c-234">Volg de instructies in [opnieuw instellen van een wachtwoord of SSH voor virtuele machines op basis van Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) naar:</span><span class="sxs-lookup"><span data-stu-id="3f21c-234">Follow the instructions in [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="3f21c-235">Het wachtwoord of SSH-sleutel opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-235">Reset the password or SSH key.</span></span>
  * <span data-ttu-id="3f21c-236">Maak een *sudo* gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="3f21c-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="3f21c-237">De SSH-configuratie opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-237">Reset the SSH configuration.</span></span>
* <span data-ttu-id="3f21c-238">Controleer de status van de VM-resource voor problemen met het platform.</span><span class="sxs-lookup"><span data-stu-id="3f21c-238">Check the VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="3f21c-239">Selecteer uw virtuele machine en schuif naar beneden **instellingen** > **Controleer Health**.</span><span class="sxs-lookup"><span data-stu-id="3f21c-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3f21c-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3f21c-240">Additional resources</span></span>
* <span data-ttu-id="3f21c-241">Als u nog steeds niet SSH met uw virtuele machine na de na stappen te volgen, Zie [meer gedetailleerde stappen voor probleemoplossing](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) om te controleren van extra stappen uitvoeren om het probleem kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="3f21c-241">If you are still unable to SSH to your VM after following the after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to review additional steps to resolve your issue.</span></span>
* <span data-ttu-id="3f21c-242">Zie voor meer informatie over het oplossen van toegang tot toepassingen [toegang tot een toepassing die wordt uitgevoerd op een virtuele machine van Azure oplossen](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="3f21c-242">For more information about troubleshooting application access, see [Troubleshoot access to an application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="3f21c-243">Zie voor meer informatie over het oplossen van virtuele machines die zijn gemaakt met behulp van het klassieke implementatiemodel [opnieuw instellen van een wachtwoord of SSH voor virtuele machines op basis van Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3f21c-243">For more information about troubleshooting virtual machines that were created by using the classic deployment model, see [How to reset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

