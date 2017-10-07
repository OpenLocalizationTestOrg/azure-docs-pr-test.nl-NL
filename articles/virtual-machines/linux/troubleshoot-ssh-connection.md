---
title: de SSH-verbinding aaaTroubleshoot problemen tooan Azure VM | Microsoft Docs
description: Hoe tootroubleshoot problemen zoals 'SSH-verbinding is mislukt' of 'SSH-verbinding geweigerd' voor een Azure VM waarop Linux wordt uitgevoerd.
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
ms.openlocfilehash: dfb4e75e571c8306edf5f300c4e0f07a5fe7750a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-ssh-connections-tooan-azure-linux-vm-that-fails-errors-out-or-is-refused"></a><span data-ttu-id="e7755-104">Problemen met SSH-verbindingen tooan Azure Linux VM die is mislukt, fouten, of wordt geweigerd</span><span class="sxs-lookup"><span data-stu-id="e7755-104">Troubleshoot SSH connections tooan Azure Linux VM that fails, errors out, or is refused</span></span>
<span data-ttu-id="e7755-105">Er zijn diverse redenen dat u op problemen Secure Shell (SSH), SSH verbindingsfouten stuit, of SSH wordt geweigerd wanneer u tooconnect tooa virtuele Linux-machine (VM probeert).</span><span class="sxs-lookup"><span data-stu-id="e7755-105">There are various reasons that you encounter Secure Shell (SSH) errors, SSH connection failures, or SSH is refused when you try tooconnect tooa Linux virtual machine (VM).</span></span> <span data-ttu-id="e7755-106">In dit artikel helpt u bij het zoeken en de juiste Hallo problemen.</span><span class="sxs-lookup"><span data-stu-id="e7755-106">This article helps you find and correct hello problems.</span></span> <span data-ttu-id="e7755-107">U kunt het gebruiken van hello Azure-portal, Azure CLI of VM-extensie voor toegang voor Linux tootroubleshoot en oplossen van problemen met de verbinding.</span><span class="sxs-lookup"><span data-stu-id="e7755-107">You can use hello Azure portal, Azure CLI, or VM Access Extension for Linux tootroubleshoot and resolve connection problems.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e7755-108">Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](http://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="e7755-108">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](http://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="e7755-109">U kunt ook een incident voor ondersteuning van Azure indienen.</span><span class="sxs-lookup"><span data-stu-id="e7755-109">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="e7755-110">Ga toohello [ondersteuning van Azure site](http://azure.microsoft.com/support/options/) en selecteer **ondersteuning krijgen**.</span><span class="sxs-lookup"><span data-stu-id="e7755-110">Go toohello [Azure support site](http://azure.microsoft.com/support/options/) and select **Get support**.</span></span> <span data-ttu-id="e7755-111">Lees voor informatie over het gebruik van de ondersteuning van Azure Hallo [ondersteuning van Microsoft Azure Veelgestelde vragen over](http://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="e7755-111">For information about using Azure Support, read hello [Microsoft Azure support FAQ](http://azure.microsoft.com/support/faq/).</span></span>

## <a name="quick-troubleshooting-steps"></a><span data-ttu-id="e7755-112">Snelle stappen voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="e7755-112">Quick troubleshooting steps</span></span>
<span data-ttu-id="e7755-113">Probeer opnieuw verbinding te maken toohello VM na elke stap voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="e7755-113">After each troubleshooting step, try reconnecting toohello VM.</span></span>

1. <span data-ttu-id="e7755-114">Hallo SSH-configuratie opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="e7755-114">Reset hello SSH configuration.</span></span>
2. <span data-ttu-id="e7755-115">Hallo-referenties voor Hallo gebruiker instellen.</span><span class="sxs-lookup"><span data-stu-id="e7755-115">Reset hello credentials for hello user.</span></span>
3. <span data-ttu-id="e7755-116">Controleer of Hallo [Netwerkbeveiligingsgroep](../../virtual-network/virtual-networks-nsg.md) regels SSH-verkeer toestaan.</span><span class="sxs-lookup"><span data-stu-id="e7755-116">Verify hello [Network Security Group](../../virtual-network/virtual-networks-nsg.md) rules permit SSH traffic.</span></span>
   * <span data-ttu-id="e7755-117">Zorg ervoor dat een regel Netwerkbeveiligingsgroep toopermit SSH verkeer (standaard TCP-poort 22 bestaat).</span><span class="sxs-lookup"><span data-stu-id="e7755-117">Ensure that a Network Security Group rule exists toopermit SSH traffic (by default, TCP port 22).</span></span>
   * <span data-ttu-id="e7755-118">U kunt geen poortomleiding gebruiken / toewijzen zonder gebruik van een Azure load balancer.</span><span class="sxs-lookup"><span data-stu-id="e7755-118">You cannot use port redirection / mapping without using an Azure load balancer.</span></span>
4. <span data-ttu-id="e7755-119">Controleer de Hallo [VM resourcestatus](../../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7755-119">Check hello [VM resource health](../../resource-health/resource-health-overview.md).</span></span> 
   * <span data-ttu-id="e7755-120">Zorg ervoor dat Hallo VM rapporten als in orde.</span><span class="sxs-lookup"><span data-stu-id="e7755-120">Ensure that hello VM reports as being healthy.</span></span>
   * <span data-ttu-id="e7755-121">Als er diagnostische gegevens over opstarten is ingeschakeld, controleert u of Hallo VM is niet opstartfouten rapporteert in Hallo Logboeken.</span><span class="sxs-lookup"><span data-stu-id="e7755-121">If you have boot diagnostics enabled, verify hello VM is not reporting boot errors in hello logs.</span></span>
5. <span data-ttu-id="e7755-122">Opnieuw opstarten Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e7755-122">Restart hello VM.</span></span>
6. <span data-ttu-id="e7755-123">Hallo VM implementeren.</span><span class="sxs-lookup"><span data-stu-id="e7755-123">Redeploy hello VM.</span></span>

<span data-ttu-id="e7755-124">Blijven lezen voor meer gedetailleerde stappen voor probleemoplossing en uitleg.</span><span class="sxs-lookup"><span data-stu-id="e7755-124">Continue reading for more detailed troubleshooting steps and explanations.</span></span>

## <a name="available-methods-tootroubleshoot-ssh-connection-issues"></a><span data-ttu-id="e7755-125">Beschikbare methoden tootroubleshoot SSH-verbindingsproblemen</span><span class="sxs-lookup"><span data-stu-id="e7755-125">Available methods tootroubleshoot SSH connection issues</span></span>
<span data-ttu-id="e7755-126">U kunt opnieuw instellen van referenties of met een van de volgende methoden Hallo SSH-configuratie:</span><span class="sxs-lookup"><span data-stu-id="e7755-126">You can reset credentials or SSH configuration using one of hello following methods:</span></span>

* <span data-ttu-id="e7755-127">[Azure-portal](#use-the-azure-portal) - handig als u tooquickly moet Hallo SSH-configuratie of SSH-sleutel opnieuw instellen en u geen Hallo van Azure-hulpprogramma's geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e7755-127">[Azure portal](#use-the-azure-portal) - great if you need tooquickly reset hello SSH configuration or SSH key and you don't have hello Azure tools installed.</span></span>
* <span data-ttu-id="e7755-128">[Azure CLI 2.0](#use-the-azure-cli-20) : als u al op de opdrachtregel Hallo snel Hallo SSH-configuratie opnieuw instellen of referenties bent.</span><span class="sxs-lookup"><span data-stu-id="e7755-128">[Azure CLI 2.0](#use-the-azure-cli-20) - if you are already on hello command line, quickly reset hello SSH configuration or credentials.</span></span> <span data-ttu-id="e7755-129">U kunt ook Hallo [Azure CLI 1.0](#use-the-azure-cli-10)</span><span class="sxs-lookup"><span data-stu-id="e7755-129">You can also use hello [Azure CLI 1.0](#use-the-azure-cli-10)</span></span>
* <span data-ttu-id="e7755-130">[Azure VMAccessForLinux-extensie](#use-the-vmaccess-extension) - maken en gebruiken van json-definitie bestanden tooreset Hallo SSH-configuratie of gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="e7755-130">[Azure VMAccessForLinux extension](#use-the-vmaccess-extension) - create and reuse json definition files tooreset hello SSH configuration or user credentials.</span></span>

<span data-ttu-id="e7755-131">Probeer na elke stap tooyour VM opnieuw verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="e7755-131">After each troubleshooting step, try connecting tooyour VM again.</span></span> <span data-ttu-id="e7755-132">Als u nog steeds geen verbinding maken, probeert u de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="e7755-132">If you still cannot connect, try hello next step.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="e7755-133">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e7755-133">Use hello Azure portal</span></span>
<span data-ttu-id="e7755-134">Hello Azure-portal biedt een snelle manier tooreset Hallo SSH-configuratie of gebruikersreferenties zonder alle hulpprogramma's installeert op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="e7755-134">hello Azure portal provides a quick way tooreset hello SSH configuration or user credentials without installing any tools on your local computer.</span></span>

<span data-ttu-id="e7755-135">Selecteer uw virtuele machine in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e7755-135">Select your VM in hello Azure portal.</span></span> <span data-ttu-id="e7755-136">Schuif omlaag toohello **ondersteuning + probleemoplossing** sectie en selecteer **wachtwoord opnieuw instellen** zoals Hallo volgt in:</span><span class="sxs-lookup"><span data-stu-id="e7755-136">Scroll down toohello **Support + Troubleshooting** section and select **Reset password** as in hello following example:</span></span>

![SSH-configuratie of de referenties in hello Azure-portal opnieuw instellen](./media/troubleshoot-ssh-connection/reset-credentials-using-portal.png)

### <a name="reset-hello-ssh-configuration"></a><span data-ttu-id="e7755-138">Hallo SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-138">Reset hello SSH configuration</span></span>
<span data-ttu-id="e7755-139">Selecteer als eerste stap `Reset configuration only` van Hallo **modus** Vervolgkeuzelijst als in Hallo voorgaande schermafbeelding, klik vervolgens op Hallo **opnieuw instellen** knop.</span><span class="sxs-lookup"><span data-stu-id="e7755-139">As a first step, select `Reset configuration only` from hello **Mode** drop-down menu as in hello preceding screenshot, then click hello **Reset** button.</span></span> <span data-ttu-id="e7755-140">Zodra deze actie is voltooid, probeer het tooaccess uw virtuele machine opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e7755-140">Once this action has completed, try tooaccess your VM again.</span></span>

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e7755-141">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-141">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e7755-142">tooreset hello referenties van een bestaande gebruiker selecteren `Reset SSH public key` of `Reset password` van Hallo **modus** vervolgkeuzelijst zoals in Hallo voorgaande schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="e7755-142">tooreset hello credentials of an existing user, select either `Reset SSH public key` or `Reset password` from hello **Mode** drop-down menu as in hello preceding screenshot.</span></span> <span data-ttu-id="e7755-143">Geef Hallo gebruikersnaam en een SSH-sleutel of het nieuwe wachtwoord en klik op Hallo **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="e7755-143">Specify hello username and an SSH key or new password, then click hello **Reset** button.</span></span>

<span data-ttu-id="e7755-144">U kunt ook een gebruiker met sudo-bevoegdheden op Hallo VM in dit menu maken.</span><span class="sxs-lookup"><span data-stu-id="e7755-144">You can also create a user with sudo privileges on hello VM from this menu.</span></span> <span data-ttu-id="e7755-145">Voer een nieuwe gebruikersnaam en het bijbehorende wachtwoord of de SSH-sleutel en klik vervolgens op Hallo **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="e7755-145">Enter a new username and associated password or SSH key, and then click hello **Reset** button.</span></span>

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="e7755-146">Hello Azure CLI 2.0 gebruiken</span><span class="sxs-lookup"><span data-stu-id="e7755-146">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="e7755-147">Als u nog niet gedaan hebt, installeert u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) en meld u bij het gebruik van de Azure-account tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e7755-147">If you haven't already, install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="e7755-148">Als u hebt gemaakt en de installatiekopie van een aangepaste Linux-schijf geüpload, zorg ervoor dat Hallo [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versie 2.0.5 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e7755-148">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="e7755-149">VM's zijn gemaakt met behulp van afbeeldingen, is deze uitbreiding voor toegang tot al geïnstalleerd en geconfigureerd voor u.</span><span class="sxs-lookup"><span data-stu-id="e7755-149">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="e7755-150">SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-150">Reset SSH configuration</span></span>
<span data-ttu-id="e7755-151">U kunt in eerste instantie probeer het opnieuw instellen Hallo SSH toodefault configuratiewaarden en Hallo SSH-server opnieuw op te starten op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e7755-151">You can initially try resetting hello SSH configuration toodefault values and rebooting hello SSH server on hello VM.</span></span> <span data-ttu-id="e7755-152">Houd er rekening mee dat dit niet Hallo gebruikersnaam, wachtwoord of SSH-sleutels wijzigt.</span><span class="sxs-lookup"><span data-stu-id="e7755-152">Note that this does not change hello user account name, password, or SSH keys.</span></span>
<span data-ttu-id="e7755-153">Hallo volgende voorbeeld wordt [az vm gebruiker opnieuw instellen-ssh](/cli/azure/vm/user#reset-ssh) tooreset Hallo SSH-configuratie op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-153">hello following example uses [az vm user reset-ssh](/cli/azure/vm/user#reset-ssh) tooreset hello SSH configuration on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-154">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-154">Use your own values as follows:</span></span>

```azurecli
az vm user reset-ssh --resource-group myResourceGroup --name myVM
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e7755-155">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-155">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e7755-156">Hallo volgende voorbeeld wordt [az vm gebruikersupdate](/cli/azure/vm/user#update) tooreset Hallo-referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`, op Hallo VM met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-156">hello following example uses [az vm user update](/cli/azure/vm/user#update) tooreset hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-157">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-157">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
     --username myUsername --password myPassword
```

<span data-ttu-id="e7755-158">Als u verificatie van SSH-sleutel gebruikt, kunt u Hallo SSH-sleutel voor een bepaalde gebruiker herstellen.</span><span class="sxs-lookup"><span data-stu-id="e7755-158">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="e7755-159">Hallo volgende voorbeeld wordt **az vm set-linux-gebruikers toegang tot** tooupdate Hallo SSH-sleutel wordt opgeslagen in `~/.ssh/id_rsa.pub` voor Hallo-gebruiker met de naam `myUsername`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-159">hello following example uses **az vm access set-linux-user** tooupdate hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-160">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-160">Use your own values as follows:</span></span>

```azurecli
az vm user update --resource-group myResourceGroup --name myVM \
    --username myUsername --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="use-hello-vmaccess-extension"></a><span data-ttu-id="e7755-161">Hallo VMAccess-extensie gebruiken</span><span class="sxs-lookup"><span data-stu-id="e7755-161">Use hello VMAccess extension</span></span>
<span data-ttu-id="e7755-162">Hallo VM-extensie voor toegang voor Linux wordt gelezen in een json-bestand dat wordt gedefinieerd toocarry acties uit. Deze acties omvatten opnieuw instellen van SSHD, opnieuw instellen van een SSH-sleutel of een gebruiker toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="e7755-162">hello VM Access Extension for Linux reads in a json file that defines actions toocarry out. These actions include resetting SSHD, resetting an SSH key, or adding a user.</span></span> <span data-ttu-id="e7755-163">U hello Azure CLI toocall hello VMAccess-extensie, maar hergebruik Hallo json-bestanden over meerdere VM's desgewenst.</span><span class="sxs-lookup"><span data-stu-id="e7755-163">You still use hello Azure CLI toocall hello VMAccess extension, but you can reuse hello json files across multiple VMs if desired.</span></span> <span data-ttu-id="e7755-164">Deze aanpak kunt u toocreate een opslagplaats voor json-bestanden die vervolgens kan worden aangeroepen voor bepaalde scenario's.</span><span class="sxs-lookup"><span data-stu-id="e7755-164">This approach allows you toocreate a repository of json files that can then be called for given scenarios.</span></span>

### <a name="reset-sshd"></a><span data-ttu-id="e7755-165">SSHD opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-165">Reset SSHD</span></span>
<span data-ttu-id="e7755-166">Maak een bestand met de naam `settings.json` Hello volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="e7755-166">Create a file named `settings.json` with hello following content:</span></span>

```json
{  
    "reset_ssh":"True"
}
```

<span data-ttu-id="e7755-167">Hello Azure CLI, u vervolgens aanroepen Hallo `VMAccessForLinux` extensie tooreset uw SSHD verbinding door te geven van uw json-bestand.</span><span class="sxs-lookup"><span data-stu-id="e7755-167">Using hello Azure CLI, you then call hello `VMAccessForLinux` extension tooreset your SSHD connection by specifying your json file.</span></span> <span data-ttu-id="e7755-168">Hallo volgende voorbeeld wordt [az vm-extensie set](/cli/azure/vm/extension#set) tooreset SSHD op Hallo VM met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-168">hello following example uses [az vm extension set](/cli/azure/vm/extension#set) tooreset SSHD on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-169">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-169">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e7755-170">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-170">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e7755-171">Als SSHD correct wordt weergegeven toofunction, kunt u Hallo-referenties voor een afzender gebruiker herstellen.</span><span class="sxs-lookup"><span data-stu-id="e7755-171">If SSHD appears toofunction correctly, you can reset hello credentials for a giver user.</span></span> <span data-ttu-id="e7755-172">tooreset hello wachtwoord voor een gebruiker, maak een bestand met de naam `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="e7755-172">tooreset hello password for a user, create a file named `settings.json`.</span></span> <span data-ttu-id="e7755-173">Hallo volgende voorbeeld hersteld Hallo referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="e7755-173">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`.</span></span> <span data-ttu-id="e7755-174">Voer de volgende regels in Hallo uw `settings.json` -bestand, met behulp van uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="e7755-174">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "password":"myPassword"
}
```

<span data-ttu-id="e7755-175">Of tooreset Hallo SSH-sleutel voor een gebruiker, maakt u eerst een bestand met de naam `settings.json`.</span><span class="sxs-lookup"><span data-stu-id="e7755-175">Or tooreset hello SSH key for a user, first create a file named `settings.json`.</span></span> <span data-ttu-id="e7755-176">Hallo volgende voorbeeld hersteld Hallo referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-176">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-177">Voer de volgende regels in Hallo uw `settings.json` -bestand, met behulp van uw eigen waarden:</span><span class="sxs-lookup"><span data-stu-id="e7755-177">Enter hello following lines into your `settings.json` file, using your own values:</span></span>

```json
{
    "username":"myUsername", "ssh_key":"mySSHKey"
}
```

<span data-ttu-id="e7755-178">Nadat uw json-bestand is gemaakt, gebruikt u hello Azure CLI toocall hello `VMAccessForLinux` extensie tooreset uw SSH-gebruikersreferenties door te geven van uw json-bestand.</span><span class="sxs-lookup"><span data-stu-id="e7755-178">After creating your json file, use hello Azure CLI toocall hello `VMAccessForLinux` extension tooreset your SSH user credentials by specifying your json file.</span></span> <span data-ttu-id="e7755-179">Hallo volgende voorbeeld worden de referenties op Hallo VM met de naam `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-179">hello following example resets credentials on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-180">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-180">Use your own values as follows:</span></span>

```azurecli
az vm extension set --resource-group philmea --vm-name Ubuntu \
    --name VMAccessForLinux --publisher Microsoft.OSTCExtensions --version 1.2 --settings settings.json
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="e7755-181">Gebruik hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e7755-181">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="e7755-182">Als u dat nog niet gedaan hebt, [hello Azure CLI 1.0 installeren en verbinding maken met Azure-abonnement tooyour](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e7755-182">If you haven't already, [install hello Azure CLI 1.0 and connect tooyour Azure subscription](../../cli-install-nodejs.md).</span></span> <span data-ttu-id="e7755-183">Zorg ervoor dat u van Resource Manager-modus als volgt gebruikmaakt:</span><span class="sxs-lookup"><span data-stu-id="e7755-183">Make sure that you are using Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="e7755-184">Als u hebt gemaakt en de installatiekopie van een aangepaste Linux-schijf geüpload, zorg ervoor dat Hallo [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) versie 2.0.5 of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e7755-184">If you created and uploaded a custom Linux disk image, make sure hello [Microsoft Azure Linux Agent](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) version 2.0.5 or later is installed.</span></span> <span data-ttu-id="e7755-185">VM's zijn gemaakt met behulp van afbeeldingen, is deze uitbreiding voor toegang tot al geïnstalleerd en geconfigureerd voor u.</span><span class="sxs-lookup"><span data-stu-id="e7755-185">For VMs created using Gallery images, this access extension is already installed and configured for you.</span></span>

### <a name="reset-ssh-configuration"></a><span data-ttu-id="e7755-186">SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-186">Reset SSH configuration</span></span>
<span data-ttu-id="e7755-187">Hallo SSHD configuratie zelf is mogelijk onjuist geconfigureerd of Hallo-service is een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="e7755-187">hello SSHD configuration itself may be misconfigured or hello service encountered an error.</span></span> <span data-ttu-id="e7755-188">U kunt herstellen SSHD toomake of SSH-configuratie voor Hallo zelf geldig is.</span><span class="sxs-lookup"><span data-stu-id="e7755-188">You can reset SSHD toomake sure hello SSH configuration itself is valid.</span></span> <span data-ttu-id="e7755-189">Opnieuw instellen van SSHD moet Hallo eerste probleemoplossing die u rekening houden.</span><span class="sxs-lookup"><span data-stu-id="e7755-189">Resetting SSHD should be hello first troubleshooting step you take.</span></span>

<span data-ttu-id="e7755-190">Hallo volgende voorbeeld wordt SSHD op een virtuele machine met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-190">hello following example resets SSHD on a VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e7755-191">Uw eigen namen voor virtuele machine en de resource als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-191">Use your own VM and resource group names as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --reset-ssh
```

### <a name="reset-ssh-credentials-for-a-user"></a><span data-ttu-id="e7755-192">SSH-referenties voor een gebruiker opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="e7755-192">Reset SSH credentials for a user</span></span>
<span data-ttu-id="e7755-193">Als SSHD correct wordt weergegeven toofunction, kunt u Hallo wachtwoord voor een afzender gebruiker herstellen.</span><span class="sxs-lookup"><span data-stu-id="e7755-193">If SSHD appears toofunction correctly, you can reset hello password for a giver user.</span></span> <span data-ttu-id="e7755-194">Hallo volgende voorbeeld hersteld Hallo referenties voor `myUsername` toohello waarde die is opgegeven `myPassword`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-194">hello following example resets hello credentials for `myUsername` toohello value specified in `myPassword`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-195">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-195">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
     --user-name myUsername --password myPassword
```

<span data-ttu-id="e7755-196">Als u verificatie van SSH-sleutel gebruikt, kunt u Hallo SSH-sleutel voor een bepaalde gebruiker herstellen.</span><span class="sxs-lookup"><span data-stu-id="e7755-196">If using SSH key authentication, you can reset hello SSH key for a given user.</span></span> <span data-ttu-id="e7755-197">Voorbeeld van updates na Hallo Hallo SSH-sleutel die zijn opgeslagen in `~/.ssh/id_rsa.pub` voor Hallo-gebruiker met de naam `myUsername`, op de virtuele machine met de naam Hallo `myVM` in `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-197">hello following example updates hello SSH key stored in `~/.ssh/id_rsa.pub` for hello user named `myUsername`, on hello VM named `myVM` in `myResourceGroup`.</span></span> <span data-ttu-id="e7755-198">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-198">Use your own values as follows:</span></span>

```azurecli
azure vm reset-access --resource-group myResourceGroup --name myVM \
    --user-name myUsername --ssh-key-file ~/.ssh/id_rsa.pub
```


## <a name="restart-a-vm"></a><span data-ttu-id="e7755-199">Een VM opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="e7755-199">Restart a VM</span></span>
<span data-ttu-id="e7755-200">Als u opnieuw instellen van de SSH-configuratie en gebruikersreferenties hello, of is een fout opgetreden in dat geval, kunt u proberen opnieuw te starten Hallo VM tooaddress onderliggende compute-problemen.</span><span class="sxs-lookup"><span data-stu-id="e7755-200">If you have reset hello SSH configuration and user credentials, or encountered an error in doing so, you can try restarting hello VM tooaddress underlying compute issues.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="e7755-201">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e7755-201">Azure portal</span></span>
<span data-ttu-id="e7755-202">een virtuele machine met toorestart Hallo Azure portal, selecteer uw virtuele machine en klik op Hallo **opnieuw** knop zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="e7755-202">toorestart a VM using hello Azure portal, select your VM and click hello **Restart** button as in hello following example:</span></span>

![Opnieuw opstarten van een virtuele machine in hello Azure-portal](./media/troubleshoot-ssh-connection/restart-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="e7755-204">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e7755-204">Azure CLI 1.0</span></span>
<span data-ttu-id="e7755-205">Hallo voorbeeld opnieuw wordt opgestart na Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-205">hello following example restarts hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e7755-206">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-206">Use your own values as follows:</span></span>

```azurecli
azure vm restart --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="e7755-207">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e7755-207">Azure CLI 2.0</span></span>
<span data-ttu-id="e7755-208">Hallo volgende voorbeeld wordt [az vm opnieuw](/cli/azure/vm#restart) toorestart Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-208">hello following example uses [az vm restart](/cli/azure/vm#restart) toorestart hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e7755-209">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-209">Use your own values as follows:</span></span>

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```


## <a name="redeploy-a-vm"></a><span data-ttu-id="e7755-210">Een virtuele machine opnieuw implementeren</span><span class="sxs-lookup"><span data-stu-id="e7755-210">Redeploy a VM</span></span>
<span data-ttu-id="e7755-211">U kunt een virtuele machine tooanother-knooppunt in Azure, die mogelijk onderliggende netwerkproblemen opgelost opnieuw implementeren.</span><span class="sxs-lookup"><span data-stu-id="e7755-211">You can redeploy a VM tooanother node within Azure, which may correct any underlying networking issues.</span></span> <span data-ttu-id="e7755-212">Zie voor meer informatie over het opnieuw distribueren van een virtuele machine [opnieuw implementeren van virtuele machine toonew Azure knooppunt](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7755-212">For information about redeploying a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="e7755-213">Nadat deze is voltooid, kortstondige schijfgegevens niet verloren en dynamische IP-adressen die gekoppeld aan Hallo virtuele machine zijn wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e7755-213">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
> 
> 

### <a name="azure-portal"></a><span data-ttu-id="e7755-214">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e7755-214">Azure portal</span></span>
<span data-ttu-id="e7755-215">een virtuele machine met tooredeploy Hallo Azure portal, selecteer uw virtuele machine en schuif omlaag toohello **ondersteuning + probleemoplossing** sectie.</span><span class="sxs-lookup"><span data-stu-id="e7755-215">tooredeploy a VM using hello Azure portal, select your VM and scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="e7755-216">Klik op Hallo **implementeren** knop zoals Hallo volgt in:</span><span class="sxs-lookup"><span data-stu-id="e7755-216">Click hello **Redeploy** button as in hello following example:</span></span>

![Implementeren van een virtuele machine in hello Azure-portal](./media/troubleshoot-ssh-connection/redeploy-vm-using-portal.png)

### <a name="azure-cli-10"></a><span data-ttu-id="e7755-218">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e7755-218">Azure CLI 1.0</span></span>
<span data-ttu-id="e7755-219">voorbeeld redeploys na Hallo Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-219">hello following example redeploys hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e7755-220">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-220">Use your own values as follows:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --name myVM
```

### <a name="azure-cli-20"></a><span data-ttu-id="e7755-221">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e7755-221">Azure CLI 2.0</span></span>
<span data-ttu-id="e7755-222">Hallo na gebruik bijvoorbeeld [az vm opnieuw distribueren](/cli/azure/vm#redeploy) tooredeploy Hallo VM met de naam `myVM` in Hallo resourcegroep met de naam `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="e7755-222">hello following example use [az vm redeploy](/cli/azure/vm#redeploy) tooredeploy hello VM named `myVM` in hello resource group named `myResourceGroup`.</span></span> <span data-ttu-id="e7755-223">Uw eigen waarden als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e7755-223">Use your own values as follows:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM
```

## <a name="vms-created-by-using-hello-classic-deployment-model"></a><span data-ttu-id="e7755-224">Virtuele machines die zijn gemaakt met behulp van Hallo klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="e7755-224">VMs created by using hello Classic deployment model</span></span>
<span data-ttu-id="e7755-225">Probeer deze stappen tooresolve Hallo meest voorkomende SSH verbindingsfouten voor virtuele machines die zijn gemaakt met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="e7755-225">Try these steps tooresolve hello most common SSH connection failures for VMs that were created by using hello classic deployment model.</span></span> <span data-ttu-id="e7755-226">Probeer opnieuw verbinding te maken toohello VM na elke stap.</span><span class="sxs-lookup"><span data-stu-id="e7755-226">After each step, try reconnecting toohello VM.</span></span>

* <span data-ttu-id="e7755-227">Opnieuw instellen van externe toegang van Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e7755-227">Reset remote access from hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e7755-228">Op Hallo van Azure-portal, selecteer uw virtuele machine en klikt u op Hallo **extern opnieuw instellen...**  knop.</span><span class="sxs-lookup"><span data-stu-id="e7755-228">On hello Azure portal, select your VM and click hello **Reset Remote...** button.</span></span>
* <span data-ttu-id="e7755-229">Opnieuw opstarten Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="e7755-229">Restart hello VM.</span></span> <span data-ttu-id="e7755-230">Op Hallo [Azure-portal](https://portal.azure.com), selecteert u de virtuele machine en klik op Hallo **opnieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="e7755-230">On hello [Azure portal](https://portal.azure.com), select your VM and click hello **Restart** button.</span></span>
    
* <span data-ttu-id="e7755-231">Implementeer Hallo VM tooa nieuwe Azure knooppunt opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e7755-231">Redeploy hello VM tooa new Azure node.</span></span> <span data-ttu-id="e7755-232">Voor informatie over het tooredeploy een VM, Zie [opnieuw implementeren van virtuele machine toonew Azure knooppunt](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7755-232">For information about how tooredeploy a VM, see [Redeploy virtual machine toonew Azure node](../windows/redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  
    <span data-ttu-id="e7755-233">Nadat deze is voltooid, kortstondige schijfgegevens niet verloren en dynamische IP-adressen die gekoppeld aan Hallo virtuele machine zijn wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e7755-233">After this operation finishes, ephemeral disk data will be lost and dynamic IP addresses that are associated with hello virtual machine will be updated.</span></span>
* <span data-ttu-id="e7755-234">Volg de instructies in Hallo [hoe tooreset een wachtwoord of SSH voor virtuele machines op basis van Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) naar:</span><span class="sxs-lookup"><span data-stu-id="e7755-234">Follow hello instructions in [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) to:</span></span>
  
  * <span data-ttu-id="e7755-235">Hallo-wachtwoord opnieuw instellen of SSH-sleutel.</span><span class="sxs-lookup"><span data-stu-id="e7755-235">Reset hello password or SSH key.</span></span>
  * <span data-ttu-id="e7755-236">Maak een *sudo* gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="e7755-236">Create a *sudo* user account.</span></span>
  * <span data-ttu-id="e7755-237">Hallo SSH-configuratie opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="e7755-237">Reset hello SSH configuration.</span></span>
* <span data-ttu-id="e7755-238">Controleer de resourcestatus Hallo van de virtuele machine voor problemen met het platform.</span><span class="sxs-lookup"><span data-stu-id="e7755-238">Check hello VM's resource health for any platform issues.</span></span><br>
     <span data-ttu-id="e7755-239">Selecteer uw virtuele machine en schuif naar beneden **instellingen** > **Controleer Health**.</span><span class="sxs-lookup"><span data-stu-id="e7755-239">Select your VM and scroll down **Settings** > **Check Health**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7755-240">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e7755-240">Additional resources</span></span>
* <span data-ttu-id="e7755-241">Als u nog steeds niet tooSSH tooyour VM nadat de volgende stappen hello, Zie [meer gedetailleerde stappen voor probleemoplossing](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview extra stappen tooresolve uw probleem.</span><span class="sxs-lookup"><span data-stu-id="e7755-241">If you are still unable tooSSH tooyour VM after following hello after steps, see [more detailed troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tooreview additional steps tooresolve your issue.</span></span>
* <span data-ttu-id="e7755-242">Zie voor meer informatie over het oplossen van toegang tot toepassingen [problemen met toegang tooan toepassing die wordt uitgevoerd op een virtuele machine van Azure](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e7755-242">For more information about troubleshooting application access, see [Troubleshoot access tooan application running on an Azure virtual machine](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="e7755-243">Zie voor meer informatie over het oplossen van virtuele machines die zijn gemaakt met het klassieke implementatiemodel Hallo [hoe tooreset een wachtwoord of SSH voor virtuele machines op basis van Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7755-243">For more information about troubleshooting virtual machines that were created by using hello classic deployment model, see [How tooreset a password or SSH for Linux-based virtual machines](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

