---
title: Toegang instellen voor een Azure Linux VM | Microsoft Docs
description: Het beheren van gebruikers en -toegang op de virtuele Linux-machines met behulp van de VMAccess-extensie en de Azure CLI 2.0 opnieuw instellen
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
ms.openlocfilehash: 587c73278a9a92776276a811c5c4c8d3db773de3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-20"></a><span data-ttu-id="32e94-103">Beheren van gebruikers, SSH en controleer of het herstellen van schijven op virtuele Linux-machines met behulp van de VMAccess-extensie met de Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="32e94-103">Manage users, SSH, and check or repair disks on Linux VMs using the VMAccess Extension with the Azure CLI 2.0</span></span>
<span data-ttu-id="32e94-104">De schijf op uw Linux-VM worden fouten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="32e94-104">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="32e94-105">U enigszins het root-wachtwoord opnieuw instellen voor uw Linux-VM of uw persoonlijke SSH-sleutel per ongeluk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="32e94-105">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="32e94-106">Als dat is gebeurd terug in de dagen van het datacenter, zou u moet er station en open vervolgens de KVM ophalen via de serverconsole.</span><span class="sxs-lookup"><span data-stu-id="32e94-106">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="32e94-107">De Azure-VMAccess-extensie beschouwen als die KVM-switch waarmee u toegang tot de console opnieuw instellen naar Linux of voer schijfonderhoud niveau.</span><span class="sxs-lookup"><span data-stu-id="32e94-107">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="32e94-108">In dit artikel laat zien hoe de VMAccess-extensie van Azure gebruiken om te controleren of herstellen van een schijf, gebruikerstoegang opnieuw instellen, beheren van gebruikersaccounts of opnieuw instellen van de SSH-configuratie op Linux.</span><span class="sxs-lookup"><span data-stu-id="32e94-108">This article shows you how to use the Azure VMAccess Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSH configuration on Linux.</span></span> <span data-ttu-id="32e94-109">U kunt deze stappen ook uitvoeren met de [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="32e94-109">You can also perform these steps with the [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-to-use-the-vmaccess-extension"></a><span data-ttu-id="32e94-110">Manieren om te gebruiken de VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="32e94-110">Ways to use the VMAccess Extension</span></span>
<span data-ttu-id="32e94-111">Er zijn twee manieren waarop u de VMAccess-extensie op uw virtuele Linux-machines kan gebruiken:</span><span class="sxs-lookup"><span data-stu-id="32e94-111">There are two ways that you can use the VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="32e94-112">Gebruik de Azure CLI 2.0 en de vereiste parameters.</span><span class="sxs-lookup"><span data-stu-id="32e94-112">Use the Azure CLI 2.0 and the required parameters.</span></span>
* <span data-ttu-id="32e94-113">[Gebruik onbewerkte JSON-bestanden die de VMAccess-extensie verwerken](#use-json-files-and-the-vmaccess-extension) en klik vervolgens op te volgen.</span><span class="sxs-lookup"><span data-stu-id="32e94-113">[Use raw JSON files that the VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="32e94-114">Gebruik de volgende voorbeelden [az vm gebruiker](/cli/azure/vm/user) opdrachten.</span><span class="sxs-lookup"><span data-stu-id="32e94-114">The following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="32e94-115">Als u wilt deze stappen uitvoert, moet u de meest recente [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in het gebruik van een Azure-account [az aanmelding](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="32e94-115">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="32e94-116">SSH-sleutel opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="32e94-116">Reset SSH key</span></span>
<span data-ttu-id="32e94-117">Het volgende voorbeeld wordt de SSH-sleutel voor de gebruiker `azureuser` op de virtuele machine met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="32e94-117">The following example resets the SSH key for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="32e94-118">Wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="32e94-118">Reset password</span></span>
<span data-ttu-id="32e94-119">Het wachtwoord voor de gebruiker opnieuw instellen van het volgende voorbeeld `azureuser` op de virtuele machine met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="32e94-119">The following example resets the password for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="32e94-120">SSH opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="32e94-120">Restart SSH</span></span>
<span data-ttu-id="32e94-121">Het volgende voorbeeld de SSH-daemon opnieuw is opgestart en de SSH-configuratie opnieuw instellen naar standaardwaarden op een virtuele machine met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="32e94-121">The following example restarts the SSH daemon and resets the SSH configuration to default values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="32e94-122">Een gebruiker maken</span><span class="sxs-lookup"><span data-stu-id="32e94-122">Create a user</span></span>
<span data-ttu-id="32e94-123">Het volgende voorbeeld wordt een gebruiker met de naam `myNewUser` met behulp van een SSH-sleutel voor verificatie op de virtuele machine met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="32e94-123">The following example creates a user named `myNewUser` using an SSH key for authentication on the VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="32e94-124">Een gebruiker verwijderen</span><span class="sxs-lookup"><span data-stu-id="32e94-124">Delete a user</span></span>
<span data-ttu-id="32e94-125">Het volgende voorbeeld wordt een gebruiker met de naam `myNewUser` op de virtuele machine met de naam `myVM`:</span><span class="sxs-lookup"><span data-stu-id="32e94-125">The following example deletes a user named `myNewUser` on the VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-the-vmaccess-extension"></a><span data-ttu-id="32e94-126">Gebruik JSON-bestanden en de VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="32e94-126">Use JSON files and the VMAccess Extension</span></span>
<span data-ttu-id="32e94-127">De volgende voorbeelden onbewerkte JSON-bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="32e94-127">The following examples use raw JSON files.</span></span> <span data-ttu-id="32e94-128">Gebruik [az vm-extensie set](/cli/azure/vm/extension#set) aan te roepen vervolgens uw JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="32e94-128">Use [az vm extension set](/cli/azure/vm/extension#set) to then call your JSON files.</span></span> <span data-ttu-id="32e94-129">Deze JSON-bestanden kunnen ook worden aangeroepen vanuit de Azure-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="32e94-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="32e94-130">Toegang van gebruikers opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="32e94-130">Reset user access</span></span>
<span data-ttu-id="32e94-131">Als u hebt geen toegang meer tot hoofdmap op uw Linux-VM, kunt u een script vmaccess gebruikt als de SSH-sleutel van een gebruiker of het wachtwoord opnieuw wilt starten.</span><span class="sxs-lookup"><span data-stu-id="32e94-131">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset a user's SSH key or password.</span></span>

<span data-ttu-id="32e94-132">Als u wilt de openbare SSH-sleutel van een gebruiker instellen, maakt u een bestand met de naam `reset_ssh_key.json` en -instellingen toevoegen in de volgende indeling.</span><span class="sxs-lookup"><span data-stu-id="32e94-132">To reset the SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in the following format.</span></span> <span data-ttu-id="32e94-133">Vervang uw eigen waarden voor de `username` en `ssh_key` parameters:</span><span class="sxs-lookup"><span data-stu-id="32e94-133">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="32e94-134">Voer het script VMAccess met:</span><span class="sxs-lookup"><span data-stu-id="32e94-134">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="32e94-135">Als u wilt een gebruikerswachtwoord opnieuw instelt, maakt u een bestand met de naam `reset_user_password.json` en -instellingen toevoegen in de volgende indeling.</span><span class="sxs-lookup"><span data-stu-id="32e94-135">To reset a user password, create a file named `reset_user_password.json` and add settings in the following format.</span></span> <span data-ttu-id="32e94-136">Vervang uw eigen waarden voor de `username` en `password` parameters:</span><span class="sxs-lookup"><span data-stu-id="32e94-136">Substitute your own values for the `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="32e94-137">Voer het script VMAccess met:</span><span class="sxs-lookup"><span data-stu-id="32e94-137">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="32e94-138">SSH opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="32e94-138">Restart SSH</span></span>
<span data-ttu-id="32e94-139">Als u wilt de SSH-daemon starten en de SSH-configuratie opnieuw instellen naar standaardwaarden, maakt u een bestand met de naam `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="32e94-139">To restart the SSH daemon and reset the SSH configuration to default values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="32e94-140">Voeg de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="32e94-140">Add the following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="32e94-141">Voer het script VMAccess met:</span><span class="sxs-lookup"><span data-stu-id="32e94-141">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="32e94-142">Gebruikers beheren</span><span class="sxs-lookup"><span data-stu-id="32e94-142">Manage users</span></span>

<span data-ttu-id="32e94-143">Maak een bestand met de naam voor het maken van een gebruiker die een SSH-sleutel voor verificatie gebruikt, `create_new_user.json` en -instellingen toevoegen in de volgende indeling.</span><span class="sxs-lookup"><span data-stu-id="32e94-143">To create a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in the following format.</span></span> <span data-ttu-id="32e94-144">Vervang uw eigen waarden voor de `username` en `ssh_key` parameters:</span><span class="sxs-lookup"><span data-stu-id="32e94-144">Substitute your own values for the `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="32e94-145">Voer het script VMAccess met:</span><span class="sxs-lookup"><span data-stu-id="32e94-145">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="32e94-146">Als u wilt een gebruiker verwijdert, maakt u een bestand met de naam `delete_user.json` en voegt u de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="32e94-146">To delete a user, create a file named `delete_user.json` and add the following content.</span></span> <span data-ttu-id="32e94-147">Vervangen door uw eigen waarde voor de `remove_user` parameter:</span><span class="sxs-lookup"><span data-stu-id="32e94-147">Substitute your own value for the `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="32e94-148">Voer het script VMAccess met:</span><span class="sxs-lookup"><span data-stu-id="32e94-148">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-the-disk"></a><span data-ttu-id="32e94-149">Controleer of het herstellen van de schijf</span><span class="sxs-lookup"><span data-stu-id="32e94-149">Check or repair the disk</span></span>
<span data-ttu-id="32e94-150">U vmaccess gebruikt kunt u ook controleren en herstellen van een schijf die u hebt toegevoegd aan de Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="32e94-150">Using VMAccess you can also check and repair a disk that you added to the Linux VM.</span></span>

<span data-ttu-id="32e94-151">Om te controleren en herstel daarna de schijf, maakt u een bestand met de naam `disk_check_repair.json` en -instellingen toevoegen in de volgende indeling.</span><span class="sxs-lookup"><span data-stu-id="32e94-151">To check and then repair the disk, create a file named `disk_check_repair.json` and add settings in the following format.</span></span> <span data-ttu-id="32e94-152">Vervangen door uw eigen waarde voor de naam van `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="32e94-152">Substitute your own value for the name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="32e94-153">Voer het script VMAccess met:</span><span class="sxs-lookup"><span data-stu-id="32e94-153">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="32e94-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="32e94-154">Next steps</span></span>
<span data-ttu-id="32e94-155">Bijwerken van Linux via de Azure-VMAccess-extensie is een methode wijzigingen aanbrengen in een actieve Linux VM.</span><span class="sxs-lookup"><span data-stu-id="32e94-155">Updating Linux using the Azure VMAccess Extension is one method to make changes on a running Linux VM.</span></span> <span data-ttu-id="32e94-156">U kunt ook hulpprogramma's zoals cloud init en Azure Resource Manager-sjablonen gebruiken om te wijzigen van uw Linux VM op opstarten.</span><span class="sxs-lookup"><span data-stu-id="32e94-156">You can also use tools like cloud-init and Azure Resource Manager templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="32e94-157">Uitbreidingen van de virtuele machine en functies voor Linux</span><span class="sxs-lookup"><span data-stu-id="32e94-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="32e94-158">Azure Resource Manager-sjablonen met Linux VM-extensies</span><span class="sxs-lookup"><span data-stu-id="32e94-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="32e94-159">Gebruik van cloud-init voor het aanpassen van een Linux-VM tijdens het maken van</span><span class="sxs-lookup"><span data-stu-id="32e94-159">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md)

