---
title: aaaReset Linux VM wachtwoord en SSH-sleutel uit Hallo CLI | Microsoft Docs
description: Hoe toouse hello VMAccess-extensie van hello Azure-opdrachtregelinterface (CLI) tooreset een Linux-VM-wachtwoord of SSH-sleutel, herstel Hallo SSH-configuratie en consistentie van de schijf controleren
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="6ae9f-103">Hoe tooreset een Linux-VM-wachtwoord of SSH-sleutel, los Hallo SSH-configuratie en consistentie van de schijf met behulp van Hallo VMAccess-extensie controleren</span><span class="sxs-lookup"><span data-stu-id="6ae9f-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="6ae9f-104">Als u geen tooa virtuele Linux-machine in Azure verbinding maken vanwege een vergeten wachtwoord, een onjuiste sleutel voor Secure Shell (SSH) of een probleem met de Hallo SSH-configuratie, Hallo VMAccessForLinux-extensie met hello Azure CLI tooreset Hallo wachtwoord of SSH-sleutel, oplossen Hallo SSH-configuratie en controleren van de consistentie van de schijf.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="6ae9f-105">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6ae9f-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="6ae9f-106">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="6ae9f-107">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="6ae9f-108">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="6ae9f-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="6ae9f-109">Met hello Azure CLI, gebruikt u Hallo **azure vm-extensie set** via de opdrachtregelinterface (Bash, Terminal-opdrachtprompt) tooaccess-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="6ae9f-110">Voer **help azure vm-extensie set** voor het gebruik van gedetailleerde extensie.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="6ae9f-111">U kunt doen met Azure CLI hello, Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="6ae9f-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="6ae9f-112">Hallo-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="6ae9f-113">Hallo SSH-sleutel opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="6ae9f-114">Hallo wachtwoord en Hallo SSH-sleutel opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="6ae9f-115">Een nieuw sudo-gebruikersaccount maken</span><span class="sxs-lookup"><span data-stu-id="6ae9f-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="6ae9f-116">Hallo SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="6ae9f-117">Een gebruiker verwijderen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="6ae9f-118">Hallo-status van Hallo VMAccess-extensie weergeven</span><span class="sxs-lookup"><span data-stu-id="6ae9f-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="6ae9f-119">Controleer de consistentie van toegevoegde schijven</span><span class="sxs-lookup"><span data-stu-id="6ae9f-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="6ae9f-120">Herstellen van toegevoegde schijven op uw Linux-VM</span><span class="sxs-lookup"><span data-stu-id="6ae9f-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="6ae9f-121">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6ae9f-121">Prerequisites</span></span>
<span data-ttu-id="6ae9f-122">Hiervoor hebt u toodo Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6ae9f-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="6ae9f-123">U moet te[hello Azure CLI installeren](../../../cli-install-nodejs.md) en [tooyour abonnement verbinding](../../../xplat-cli-connect.md) toouse Azure resources zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="6ae9f-124">Juiste modus voor het klassieke implementatiemodel Hallo HALLO hallo door volgende te typen bij de opdrachtprompt Hallo instellen:</span><span class="sxs-lookup"><span data-stu-id="6ae9f-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="6ae9f-125">Een nieuw wachtwoord of SSH-sleutels hebben als u wilt dat tooreset een.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="6ae9f-126">U kunt deze niet nodig als u wilt dat tooreset Hallo SSH-configuratie.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="6ae9f-127"><a name="pwresetcli"></a>Hallo-wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="6ae9f-128">Maak een bestand op uw lokale computer met de naam PrivateConf.json met deze regels.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="6ae9f-129">Vervang **gebruik met Windows** en  **myP@ssW0rd**  met uw eigen gebruikersnaam en wachtwoord en stel uw eigen datum voor verlopen.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="6ae9f-130">Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6ae9f-131"><a name="sshkeyresetcli"></a>Hallo SSH-sleutel opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="6ae9f-132">Maak een bestand met de naam PrivateConf.json met deze inhoud.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="6ae9f-133">Vervang Hallo **gebruik met Windows** en **mySSHKey** waarden door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="6ae9f-134">Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="6ae9f-135"><a name="resetbothcli"></a>Zowel Hallo wachtwoord en Hallo SSH-sleutel opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="6ae9f-136">Maak een bestand met de naam PrivateConf.json met deze inhoud.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="6ae9f-137">Vervang Hallo **gebruik met Windows**, **mySSHKey** en  **myP@ssW0rd**  waarden door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="6ae9f-138">Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6ae9f-139"><a name="createnewsudocli"></a>Een nieuw sudo-gebruikersaccount maken</span><span class="sxs-lookup"><span data-stu-id="6ae9f-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="6ae9f-140">Als u uw gebruikersnaam vergeet, kunt u VMAccess toocreate een nieuw bestand met de Hallo sudo-instantie.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="6ae9f-141">In dit geval Hallo bestaande gebruikersnaam en wachtwoord worden niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="6ae9f-142">een nieuwe sudo-gebruiker met wachtwoord toegang, gebruik Hallo script in toocreate [Hallo-wachtwoord opnieuw instellen](#pwresetcli) en Hallo nieuwe gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="6ae9f-143">een nieuwe gebruiker met sudo met SSH toegang tot de sleutel, gebruik Hallo script in toocreate [Hallo SSH-sleutel opnieuw instellen](#sshkeyresetcli) en geeft u de nieuwe gebruikersnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="6ae9f-144">U kunt ook [Hallo wachtwoord en het Hallo SSH-sleutel opnieuw ingesteld](#resetbothcli) toocreate een nieuwe gebruiker met wachtwoord en toegang tot de sleutel van SSH.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="6ae9f-145"><a name="sshconfigresetcli"></a>Hallo SSH-configuratie opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="6ae9f-146">Als SSH-configuratie Hallo zich in een ongewenste status, kunt u ook toegang toohello VM verliezen.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="6ae9f-147">U kunt Hallo VMAccess-extensie tooreset hello tooits standaard configuratiestatus gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="6ae9f-148">toodo dus u hoeft alleen maar tooset Hallo 'reset_ssh' sleutel te 'True'.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="6ae9f-149">Hallo-extensie wordt Hallo SSH-server opnieuw opstarten en opent u Hallo SSH-poort op de virtuele machine Hallo SSH configuratiewaarden toodefault opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="6ae9f-150">Hallo gebruikersaccount (naam, wachtwoord of SSH-sleutels) worden niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="6ae9f-151">/etc/ssh/sshd_config bevindt Hallo SSH-configuratiebestand die opnieuw wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="6ae9f-152">Maak een bestand met de naam PrivateConf.json met deze inhoud.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="6ae9f-153">Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6ae9f-154"><a name="deletecli"></a>Een gebruiker verwijderen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="6ae9f-155">Als u een gebruikersaccount zonder aan te melden bij toohello VM rechtstreeks toodelete wilt, kunt u dit script gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="6ae9f-156">Maak een bestand met de naam PrivateConf.json met deze inhoud, vervangen door Hallo gebruiker naam tooremove voor **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="6ae9f-157">Voer deze opdracht, waarbij u de naam van uw virtuele machine voor Hallo vervangt **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="6ae9f-158"><a name="statuscli"></a>Hallo-status van Hallo VMAccess-extensie weergeven</span><span class="sxs-lookup"><span data-stu-id="6ae9f-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="6ae9f-159">status van de toodisplay Hallo Hallo VMAccess-extensie, wordt deze opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="6ae9f-160"><a name='checkdisk'></a>Controleer de consistentie van toegevoegde schijven</span><span class="sxs-lookup"><span data-stu-id="6ae9f-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="6ae9f-161">toorun fsck op alle schijven in uw virtuele Linux-machine, moet u toodo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="6ae9f-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="6ae9f-162">Maak een bestand met de naam PublicConf.json met deze inhoud.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="6ae9f-163">Controleer de dat schijf duurt voordat een Booleaanse waarde of toocheck schijven tooyour virtuele machine gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="6ae9f-164">Voer deze opdracht tooexecute, vervangen door de naam van uw virtuele machine voor Hallo **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="6ae9f-165"><a name='repairdisk'></a>Herstellen van schijven</span><span class="sxs-lookup"><span data-stu-id="6ae9f-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="6ae9f-166">toorepair-schijven die u niet wilt koppelen of koppelpunt configuratiefouten hebt, gebruikt u Hallo VMAccess-extensie tooreset Hallo koppelpunt configuratie op uw virtuele Linux-machine.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="6ae9f-167">Hallo-naam van de schijf vervangen door **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="6ae9f-168">Maak een bestand met de naam PublicConf.json met deze inhoud.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="6ae9f-169">Voer deze opdracht tooexecute, vervangen door de naam van uw virtuele machine voor Hallo **myVM**.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="6ae9f-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6ae9f-170">Next steps</span></span>
* <span data-ttu-id="6ae9f-171">Als u toouse Azure PowerShell-cmdlets of Azure Resource Manager sjablonen tooreset Hallo wachtwoord of SSH-sleutel wilt, los Hallo SSH-configuratie, en controleren van de consistentie van de schijf, Zie Hallo [VMAccess-extensie-documentatie op GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="6ae9f-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="6ae9f-172">U kunt ook Hallo [Azure-portal](https://portal.azure.com) tooreset Hallo wachtwoord of SSH-sleutel van een Linux-VM in het klassieke implementatiemodel Hallo geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="6ae9f-173">U kunt momenteel Hallo portal wilt toothis gebruiken voor een Linux-VM is geïmplementeerd in Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="6ae9f-174">Zie [over functies en uitbreidingen van de virtuele machine](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over het gebruik van VM-extensies voor Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="6ae9f-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

