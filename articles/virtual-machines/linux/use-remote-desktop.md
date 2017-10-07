---
title: aaaUse extern bureaublad tooa Linux VM in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall en configureren van extern bureaublad (xrdp) tooconnect tooa Linux VM in Azure met grafische hulpprogramma's
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: iainfou
ms.openlocfilehash: 64d30be101ceeb49fc05bb10293ad63db358efe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-remote-desktop-tooconnect-tooa-linux-vm-in-azure"></a><span data-ttu-id="b702f-103">Installeren en configureren van extern bureaublad tooconnect tooa Linux VM in Azure</span><span class="sxs-lookup"><span data-stu-id="b702f-103">Install and configure Remote Desktop tooconnect tooa Linux VM in Azure</span></span>
<span data-ttu-id="b702f-104">Linux virtuele machines (VM's) in Azure worden meestal beheerd vanuit de opdrachtregel Hallo via een secure shell (SSH)-verbinding.</span><span class="sxs-lookup"><span data-stu-id="b702f-104">Linux virtual machines (VMs) in Azure are usually managed from hello command line using a secure shell (SSH) connection.</span></span> <span data-ttu-id="b702f-105">Wanneer nieuwe tooLinux of voor snelle scenario's voor probleemoplossing Hallo van extern bureaublad kan bijvoorbeeld worden gebruikt eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="b702f-105">When new tooLinux, or for quick troubleshooting scenarios, hello use of remote desktop may be easier.</span></span> <span data-ttu-id="b702f-106">Dit artikel details hoe tooinstall en configureren van een bureaublad-omgeving ([xfce](https://www.xfce.org)) en extern bureaublad ([xrdp](http://www.xrdp.org)) voor uw Linux-VM met Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="b702f-106">This article details how tooinstall and configure a desktop environment ([xfce](https://www.xfce.org)) and remote desktop ([xrdp](http://www.xrdp.org)) for your Linux VM using hello Resource Manager deployment model.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b702f-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b702f-107">Prerequisites</span></span>
<span data-ttu-id="b702f-108">In dit artikel is vereist voor een bestaande Linux VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="b702f-108">This article requires an existing Linux VM in Azure.</span></span> <span data-ttu-id="b702f-109">Als u toocreate een virtuele machine moet, een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b702f-109">If you need toocreate a VM, use one of hello following methods:</span></span>

- <span data-ttu-id="b702f-110">Hallo [Azure CLI 2.0](quick-create-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b702f-110">hello [Azure CLI 2.0](quick-create-cli.md)</span></span>
- <span data-ttu-id="b702f-111">Hallo [Azure-portal](quick-create-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b702f-111">hello [Azure portal](quick-create-portal.md)</span></span>


## <a name="install-a-desktop-environment-on-your-linux-vm"></a><span data-ttu-id="b702f-112">Een bureaubladomgeving installeren op uw Linux-VM</span><span class="sxs-lookup"><span data-stu-id="b702f-112">Install a desktop environment on your Linux VM</span></span>
<span data-ttu-id="b702f-113">De meeste Linux virtuele machines in Azure beschikt niet over een bureaubladomgeving standaard geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b702f-113">Most Linux VMs in Azure do not have a desktop environment installed by default.</span></span> <span data-ttu-id="b702f-114">Linux VM's worden meestal beheerd met behulp van SSH-verbindingen in plaats van een bureaublad-omgeving.</span><span class="sxs-lookup"><span data-stu-id="b702f-114">Linux VMs are commonly managed using SSH connections rather than a desktop environment.</span></span> <span data-ttu-id="b702f-115">Er zijn verschillende bureaubladomgevingen in Linux die u kunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="b702f-115">There are various desktop environments in Linux that you can choose.</span></span> <span data-ttu-id="b702f-116">Afhankelijk van uw keuze van bureaubladomgeving van mogelijk één too2 GB aan schijfruimte, gebruiken en 5 too10 minuten tooinstall nemen en alle vereist hello-pakketten te configureren.</span><span class="sxs-lookup"><span data-stu-id="b702f-116">Depending on your choice of desktop environment, it may consume one too2 GB of disk space, and take 5 too10 minutes tooinstall and configure all hello required packages.</span></span>

<span data-ttu-id="b702f-117">Hallo volgende voorbeeld wordt geïnstalleerd Hallo lightweight [xfce4](https://www.xfce.org/) bureaubladomgeving op een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="b702f-117">hello following example installs hello lightweight [xfce4](https://www.xfce.org/) desktop environment on an Ubuntu VM.</span></span> <span data-ttu-id="b702f-118">Opdrachten voor andere distributies enigszins verschillen (Gebruik `yum` tooinstall op Red Hat Enterprise Linux en configureer de juiste `selinux` regels of gebruik `zypper` tooinstall op SUSE, bijvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="b702f-118">Commands for other distributions vary slightly (use `yum` tooinstall on Red Hat Enterprise Linux and configure appropriate `selinux` rules, or use `zypper` tooinstall on SUSE, for example).</span></span>

<span data-ttu-id="b702f-119">Eerst SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="b702f-119">First, SSH tooyour VM.</span></span> <span data-ttu-id="b702f-120">Hallo volgende voorbeeld maakt verbinding met de naam VM toohello *myvm.westus.cloudapp.azure.com* Hallo gebruikersnaam van *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="b702f-120">hello following example connects toohello VM named *myvm.westus.cloudapp.azure.com* with hello username of *azureuser*:</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="b702f-121">Als u van Windows gebruikmaakt en meer informatie over het gebruik van SSH nodig hebt, raadpleegt u [hoe toouse SSH-sleutels met Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b702f-121">If you are using Windows and need more information on using SSH, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

<span data-ttu-id="b702f-122">Vervolgens installeert met behulp van xfce `apt` als volgt:</span><span class="sxs-lookup"><span data-stu-id="b702f-122">Next, install xfce using `apt` as follows:</span></span>

```bash
sudo apt-get update
sudo apt-get install xfce4
```

## <a name="install-and-configure-a-remote-desktop-server"></a><span data-ttu-id="b702f-123">Installeren en configureren van een extern bureaublad-server</span><span class="sxs-lookup"><span data-stu-id="b702f-123">Install and configure a remote desktop server</span></span>
<span data-ttu-id="b702f-124">Nu dat u een bureaubladomgeving geïnstalleerd hebt, configureert u een extern bureaublad-services toolisten voor binnenkomende verbindingen.</span><span class="sxs-lookup"><span data-stu-id="b702f-124">Now that you have a desktop environment installed, configure a remote desktop service toolisten for incoming connections.</span></span> <span data-ttu-id="b702f-125">[xrdp](http://xrdp.org) is een open-source Remote Desktop Protocol (RDP)-server die beschikbaar is op de meeste Linux-distributies en werkt goed samen met xfce.</span><span class="sxs-lookup"><span data-stu-id="b702f-125">[xrdp](http://xrdp.org) is an open source Remote Desktop Protocol (RDP) server that is available on most Linux distributions, and works well with xfce.</span></span> <span data-ttu-id="b702f-126">Installeer xrdp op uw Ubuntu VM als volgt:</span><span class="sxs-lookup"><span data-stu-id="b702f-126">Install xrdp on your Ubuntu VM as follows:</span></span>

```bash
sudo apt-get install xrdp
```

<span data-ttu-id="b702f-127">Vertel xrdp welke toouse bureaubladomgeving bij het starten van uw sessie.</span><span class="sxs-lookup"><span data-stu-id="b702f-127">Tell xrdp what desktop environment toouse when you start your session.</span></span> <span data-ttu-id="b702f-128">Xrdp toouse xfce als de bureaubladomgeving als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="b702f-128">Configure xrdp toouse xfce as your desktop environment as follows:</span></span>

```bash
echo xfce4-session >~/.xsession
```

<span data-ttu-id="b702f-129">Hallo xrdp service voor Hallo wijzigingen tootake effect als volgt opnieuw starten:</span><span class="sxs-lookup"><span data-stu-id="b702f-129">Restart hello xrdp service for hello changes tootake effect as follows:</span></span>

```bash
sudo service xrdp restart
```


## <a name="set-a-local-user-account-password"></a><span data-ttu-id="b702f-130">Wachtwoord voor een lokale gebruikersaccount instellen</span><span class="sxs-lookup"><span data-stu-id="b702f-130">Set a local user account password</span></span>
<span data-ttu-id="b702f-131">Als u een wachtwoord voor uw gebruikersaccount gemaakt toen u uw virtuele machine hebt gemaakt, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="b702f-131">If you created a password for your user account when you created your VM, skip this step.</span></span> <span data-ttu-id="b702f-132">Als u alleen verificatie van SSH-sleutel en niet het wachtwoord van een lokale account instellen hoeft, een wachtwoord opgeven voordat u xrdp toolog in tooyour VM gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b702f-132">If you only use SSH key authentication and do not have a local account password set, specify a password before you use xrdp toolog in tooyour VM.</span></span> <span data-ttu-id="b702f-133">xrdp accepteren niet SSH-sleutels voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="b702f-133">xrdp cannot accept SSH keys for authentication.</span></span> <span data-ttu-id="b702f-134">Hallo volgende voorbeeld wordt een wachtwoord voor gebruikersaccount Hallo *azureuser*:</span><span class="sxs-lookup"><span data-stu-id="b702f-134">hello following example specifies a password for hello user account *azureuser*:</span></span>

```bash
sudo passwd azureuser
```

> [!NOTE]
> <span data-ttu-id="b702f-135">Opgeven van een wachtwoord wordt uw SSHD configuratie toopermit wachtwoord aanmeldingen niet bijgewerkt als die op dit moment niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="b702f-135">Specifying a password does not update your SSHD configuration toopermit password logins if it currently does not.</span></span> <span data-ttu-id="b702f-136">U kunt vanuit het beveiligingsoogpunt van tooconnect tooyour VM desgewenst met een SSH-tunnel met verificatie op basis van sleutels en sluit tooxrdp.</span><span class="sxs-lookup"><span data-stu-id="b702f-136">From a security perspective, you may wish tooconnect tooyour VM with an SSH tunnel using key-based authentication and then connect tooxrdp.</span></span> <span data-ttu-id="b702f-137">Zo ja, overslaan Hallo volgende stap over het maken van een security group regel tooallow extern bureaublad netwerkverkeer.</span><span class="sxs-lookup"><span data-stu-id="b702f-137">If so, skip hello following step on creating a network security group rule tooallow remote desktop traffic.</span></span>


## <a name="create-a-network-security-group-rule-for-remote-desktop-traffic"></a><span data-ttu-id="b702f-138">Een Netwerkbeveiligingsgroep regel maken voor extern bureaublad-verkeer</span><span class="sxs-lookup"><span data-stu-id="b702f-138">Create a Network Security Group rule for Remote Desktop traffic</span></span>
<span data-ttu-id="b702f-139">tooallow extern bureaublad-verkeer tooreach uw Linux VM, een groep voor de netwerkbeveiligingsregel moet toobe gemaakt waarmee TCP op poort 3389 tooreach uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b702f-139">tooallow Remote Desktop traffic tooreach your Linux VM, a network security group rule needs toobe created that allows TCP on port 3389 tooreach your VM.</span></span> <span data-ttu-id="b702f-140">Zie voor meer informatie over netwerkbeveiligingsgroepen [wat is er een Netwerkbeveiligingsgroep?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b702f-140">For more information about network security group rules, see [What is a Network Security Group?](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span> <span data-ttu-id="b702f-141">U kunt ook [gebruik hello Azure portal toocreate een groep voor de netwerkbeveiligingsregel](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b702f-141">You can also [use hello Azure portal toocreate a network security group rule](../windows/nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b702f-142">Hallo volgende voorbeelden maakt een groep van de netwerkbeveiligingsregel met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) met de naam *myNetworkSecurityGroupRule* te*toestaan* verkeer op *tcp* poort *3389*.</span><span class="sxs-lookup"><span data-stu-id="b702f-142">hello following examples create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) named *myNetworkSecurityGroupRule* too*allow* traffic on *tcp* port *3389*.</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1010 \
    --destination-port-range 3389
```


## <a name="connect-your-linux-vm-with-a-remote-desktop-client"></a><span data-ttu-id="b702f-143">Verbinding maken met uw Linux-VM met een extern bureaublad-client</span><span class="sxs-lookup"><span data-stu-id="b702f-143">Connect your Linux VM with a Remote Desktop client</span></span>
<span data-ttu-id="b702f-144">Open uw lokale extern-bureaubladclient en verbinding maken met toohello IP-adres of de DNS-naam van uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="b702f-144">Open your local remote desktop client and connect toohello IP address or DNS name of your Linux VM.</span></span> <span data-ttu-id="b702f-145">Hallo gebruikersnaam en wachtwoord invoeren voor Hallo-gebruikersaccount op de virtuele machine als volgt:</span><span class="sxs-lookup"><span data-stu-id="b702f-145">Enter hello username and password for hello user account on your VM as follows:</span></span>

![Verbinding maken met behulp van extern bureaublad-client tooxrdp](./media/use-remote-desktop/remote-desktop-client.png)

<span data-ttu-id="b702f-147">Als de verificatie is gelukt, Hallo xfce bureaubladomgeving laadt en Zoek vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="b702f-147">After authenticating, hello xfce desktop environment will load and look similar toohello following example:</span></span>

![xfce bureaubladomgeving via xrdp](./media/use-remote-desktop/xfce-desktop-environment.png)


## <a name="troubleshoot"></a><span data-ttu-id="b702f-149">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="b702f-149">Troubleshoot</span></span>
<span data-ttu-id="b702f-150">Als u verbinding maken met behulp van een extern bureaublad-client voor Linux-VM tooyour, `netstat` op uw Linux-VM tooverify die uw virtuele machine naar RDP-verbindingen als volgt luistert:</span><span class="sxs-lookup"><span data-stu-id="b702f-150">If you cannot connect tooyour Linux VM using a Remote Desktop client, use `netstat` on your Linux VM tooverify that your VM is listening for RDP connections  as follows:</span></span>

```bash
sudo netstat -plnt | grep rdp
```

<span data-ttu-id="b702f-151">Hallo volgende voorbeeld ziet u Hallo VM luisteren op TCP-poort 3389 zoals verwacht:</span><span class="sxs-lookup"><span data-stu-id="b702f-151">hello following example shows hello VM listening on TCP port 3389 as expected:</span></span>

```bash
tcp     0     0      127.0.0.1:3350     0.0.0.0:*     LISTEN     53192/xrdp-sesman
tcp     0     0      0.0.0.0:3389       0.0.0.0:*     LISTEN     53188/xrdp
```

<span data-ttu-id="b702f-152">Hallo xrdp service niet wordt geluisterd, op een VM Ubuntu start Hallo-service als als volgt:</span><span class="sxs-lookup"><span data-stu-id="b702f-152">If hello xrdp service is not listening, on an Ubuntu VM restart hello service as follows:</span></span>

```bash
sudo service xrdp restart
```

<span data-ttu-id="b702f-153">Bekijk wordt geregistreerd in */var/log*Thug op uw VM Ubuntu nakijken op aanwijzingen als toowhy Hallo-service reageert niet.</span><span class="sxs-lookup"><span data-stu-id="b702f-153">Review logs in */var/log*Thug  on your Ubuntu VM for indications as toowhy hello service may not be responding.</span></span> <span data-ttu-id="b702f-154">U kunt ook bewaken Hallo syslog tijdens een poging verbinding met extern bureaublad tooview fouten:</span><span class="sxs-lookup"><span data-stu-id="b702f-154">You can also monitor hello syslog during a remote desktop connection attempt tooview any errors:</span></span>

```bash
tail -f /var/log/syslog
```

<span data-ttu-id="b702f-155">Andere zoals Red Hat Enterprise Linux en SUSE Linux-distributies mogelijk op verschillende manieren toorestart services en alternatieve log-bestand locaties tooreview.</span><span class="sxs-lookup"><span data-stu-id="b702f-155">Other Linux distributions such as Red Hat Enterprise Linux and SUSE may have different ways toorestart services and alternate log file locations tooreview.</span></span>

<span data-ttu-id="b702f-156">Als u geen antwoord niet in uw extern-bureaubladclient krijgt en alle gebeurtenissen in het systeemlogboek Hallo niet ziet, wordt de reden hiervoor is dat het externe bureaublad verkeer Hallo VM kan niet bereiken.</span><span class="sxs-lookup"><span data-stu-id="b702f-156">If you do not receive any response in your remote desktop client and do not see any events in hello system log, this behavior indicates that remote desktop traffic cannot reach hello VM.</span></span> <span data-ttu-id="b702f-157">Bekijk uw netwerk beveiliging groep regels tooensure dat u een regel toopermit TCP op poort 3389 hebt.</span><span class="sxs-lookup"><span data-stu-id="b702f-157">Review your network security group rules tooensure that you have a rule toopermit TCP on port 3389.</span></span> <span data-ttu-id="b702f-158">Zie voor meer informatie [problemen met toepassing](../windows/troubleshoot-app-connection.md).</span><span class="sxs-lookup"><span data-stu-id="b702f-158">For more information, see [Troubleshoot application connectivity issues](../windows/troubleshoot-app-connection.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b702f-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b702f-159">Next steps</span></span>
<span data-ttu-id="b702f-160">Zie voor meer informatie over het maken en gebruiken van SSH-sleutels met Linux VM's [maken SSH-sleutels voor virtuele Linux-machines in Azure](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="b702f-160">For more information about creating and using SSH keys with Linux VMs, see [Create SSH keys for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

<span data-ttu-id="b702f-161">Zie voor meer informatie over het gebruik van SSH op Windows [hoe toouse SSH-sleutels met Windows](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="b702f-161">For information on using SSH from Windows, see [How toouse SSH keys with Windows](ssh-from-windows.md).</span></span>

