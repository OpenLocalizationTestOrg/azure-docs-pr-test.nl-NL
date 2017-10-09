---
title: aaaReset toegang tooan Azure Linux VM | Microsoft Docs
description: Hoe toomanage gebruikers en toegang opnieuw instellen voor het gebruik van virtuele Linux-machines Hallo VMAccess-extensie en hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="010d2-103">Beheren van gebruikers, SSH en controleer of herstel schijven over het gebruik van virtuele Linux-machines Hallo VMAccess-extensie Hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="010d2-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="010d2-104">Hallo-schijf op uw Linux-VM worden fouten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="010d2-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="010d2-105">U enigszins Hallo hoofdwachtwoord voor uw Linux-VM opnieuw instellen of uw persoonlijke SSH-sleutel per ongeluk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="010d2-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="010d2-106">Als dat is gebeurd terug in Hallo dagen van Hallo datacenter, zou u moet er toodrive en open vervolgens Hallo KVM tooget op Hallo server-console.</span><span class="sxs-lookup"><span data-stu-id="010d2-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="010d2-107">Hello Azure VMAccess-extensie beschouwen als die KVM-switch waarmee u tooaccess console tooreset toegang tooLinux Hallo of voer schijfonderhoud niveau.</span><span class="sxs-lookup"><span data-stu-id="010d2-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="010d2-108">Dit artikel ziet u hoe toouse hello Azure VMAccess-extensie toocheck of herstellen van een schijf, gebruikerstoegang opnieuw instellen, beheren van gebruikersaccounts of instellen Hallo SSH-configuratie op Linux.</span><span class="sxs-lookup"><span data-stu-id="010d2-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="010d2-109">U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="010d2-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="010d2-110">Manieren toouse hello VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="010d2-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="010d2-111">Er zijn twee manieren waarop u Hallo VMAccess-extensie op uw Linux VM's kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="010d2-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="010d2-112">Hello Azure CLI 2.0 en Hallo vereist parameters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="010d2-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="010d2-113">[Gebruik onbewerkte JSON-bestanden die Hallo VMAccess-extensie proces](#use-json-files-and-the-vmaccess-extension) en klik vervolgens op te volgen.</span><span class="sxs-lookup"><span data-stu-id="010d2-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="010d2-114">Hallo na gebruik van de voorbeelden [az vm gebruiker](/cli/azure/vm/user) opdrachten.</span><span class="sxs-lookup"><span data-stu-id="010d2-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="010d2-115">tooperform deze stappen, moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="010d2-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="010d2-116">SSH-sleutel opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="010d2-116">Reset SSH key</span></span>
<span data-ttu-id="010d2-117">Hallo volgende voorbeeld hersteld Hallo SSH-sleutel voor de gebruiker Hallo `azureuser` op Hallo VM met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="010d2-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="010d2-118">Wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="010d2-118">Reset password</span></span>
<span data-ttu-id="010d2-119">Hallo volgende voorbeeld wachtwoord opnieuw instellen Hallo voor Hallo gebruiker `azureuser` op Hallo VM met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="010d2-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="010d2-120">SSH opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="010d2-120">Restart SSH</span></span>
<span data-ttu-id="010d2-121">Hallo volgende voorbeeld wordt opnieuw opgestart Hallo SSH-daemon en opnieuw instellen van Hallo SSH configuratiewaarden toodefault die op een virtuele machine met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="010d2-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="010d2-122">Een gebruiker maken</span><span class="sxs-lookup"><span data-stu-id="010d2-122">Create a user</span></span>
<span data-ttu-id="010d2-123">Hallo volgende voorbeeld maakt u een gebruiker met de naam `myNewUser` met behulp van een SSH-sleutel voor verificatie op Hallo VM met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="010d2-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="010d2-124">Een gebruiker verwijderen</span><span class="sxs-lookup"><span data-stu-id="010d2-124">Delete a user</span></span>
<span data-ttu-id="010d2-125">Hallo volgende voorbeeld wordt verwijderd met de naam van een gebruiker `myNewUser` op Hallo VM met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="010d2-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="010d2-126">JSON-bestanden gebruiken en Hallo VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="010d2-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="010d2-127">Hallo volgen voorbeelden onbewerkte JSON-bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="010d2-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="010d2-128">Gebruik [az vm-extensie set](/cli/azure/vm/extension#set) toothen aanroepen uw JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="010d2-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="010d2-129">Deze JSON-bestanden kunnen ook worden aangeroepen vanuit de Azure-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="010d2-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="010d2-130">Toegang van gebruikers opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="010d2-130">Reset user access</span></span>
<span data-ttu-id="010d2-131">Als u toegang tooroot kwijt op uw Linux-VM bent hebt, kunt u een script VMAccess tooreset starten SSH-sleutel of het wachtwoord van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="010d2-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="010d2-132">tooreset hello openbare SSH-sleutel van een gebruiker, maak een bestand met de naam `reset_ssh_key.json` en -instellingen in de volgende indeling Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="010d2-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="010d2-133">Vervangt door uw eigen waarden Hallo `username` en `ssh_key` parameters:</span><span class="sxs-lookup"><span data-stu-id="010d2-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="010d2-134">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="010d2-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="010d2-135">tooreset het wachtwoord van een gebruiker, maak een bestand met de naam `reset_user_password.json` en -instellingen in de volgende indeling Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="010d2-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="010d2-136">Vervangt door uw eigen waarden Hallo `username` en `password` parameters:</span><span class="sxs-lookup"><span data-stu-id="010d2-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="010d2-137">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="010d2-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="010d2-138">SSH opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="010d2-138">Restart SSH</span></span>
<span data-ttu-id="010d2-139">toorestart Hallo SSH-daemon en Hallo SSH configuratiewaarden toodefault opnieuw instellen, maakt u een bestand met de naam `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="010d2-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="010d2-140">Hallo inhoud volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="010d2-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="010d2-141">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="010d2-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="010d2-142">Gebruikers beheren</span><span class="sxs-lookup"><span data-stu-id="010d2-142">Manage users</span></span>

<span data-ttu-id="010d2-143">toocreate een gebruiker die een SSH-sleutel voor verificatie gebruikt, maak een bestand met de naam `create_new_user.json` en -instellingen in de volgende indeling Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="010d2-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="010d2-144">Vervangt door uw eigen waarden Hallo `username` en `ssh_key` parameters:</span><span class="sxs-lookup"><span data-stu-id="010d2-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="010d2-145">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="010d2-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="010d2-146">toodelete een gebruiker, maak een bestand met de naam `delete_user.json` en Hallo volgende inhoud toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="010d2-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="010d2-147">Vervangen door uw eigen waarde voor Hallo `remove_user` parameter:</span><span class="sxs-lookup"><span data-stu-id="010d2-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="010d2-148">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="010d2-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="010d2-149">Controleren of herstellen Hallo-schijf</span><span class="sxs-lookup"><span data-stu-id="010d2-149">Check or repair hello disk</span></span>
<span data-ttu-id="010d2-150">U vmaccess gebruikt kunt u ook controleren en herstellen van een schijf die u toohello Linux VM toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="010d2-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="010d2-151">toocheck en vervolgens herstellen Hallo schijf, maakt u een bestand met de naam `disk_check_repair.json` en -instellingen in de volgende indeling Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="010d2-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="010d2-152">Vervangen door uw eigen waarde voor de naam Hallo van `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="010d2-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="010d2-153">Hallo VMAccess script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="010d2-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="010d2-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="010d2-154">Next steps</span></span>
<span data-ttu-id="010d2-155">Bijwerken van Linux, is het gebruik van hello Azure VMAccess-extensie is een methode toomake wijzigingen op een actieve Linux VM.</span><span class="sxs-lookup"><span data-stu-id="010d2-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="010d2-156">U kunt ook hulpprogramma's zoals cloud init en Azure Resource Manager-sjablonen toomodify uw Linux-VM gebruiken bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="010d2-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="010d2-157">Uitbreidingen van de virtuele machine en functies voor Linux</span><span class="sxs-lookup"><span data-stu-id="010d2-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="010d2-158">Azure Resource Manager-sjablonen met Linux VM-extensies</span><span class="sxs-lookup"><span data-stu-id="010d2-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="010d2-159">Met behulp van cloud-init toocustomize een Linux-VM tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="010d2-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

