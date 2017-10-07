---
title: aaaEncrypt schijven op een Linux VM in Azure | Microsoft Docs
description: Hoe virtuele schijven op een Linux-VM voor het gebruik van de verbeterde beveiliging tooencrypt hello Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2a23b6fa-6941-4998-9804-8efe93b647b3
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: d6197742bc8562630e8395588c072093fc01d614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencrypt-virtual-disks-on-a-linux-vm"></a>Hoe tooencrypt virtuele schijven op een Linux-VM
Voor de uitgebreide virtuele machine (VM) beveiliging en naleving, kunnen virtuele schijven in Azure worden versleuteld. Schijven worden versleuteld met behulp van de cryptografische sleutels die worden beveiligd in een Azure Sleutelkluis. U kunt het gebruik ervan controleren en beheren van deze cryptografische sleutels. Dit artikel wordt beschreven hoe virtuele schijven op een Linux-VM met tooencrypt hello Azure CLI 2.0. U kunt ook uitvoeren met deze stappen Hello [Azure CLI 1.0](encrypt-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="quick-commands"></a>Snelle opdrachten
Als u moet tooquickly Hallo taak, na de sectie details Hallo base Hallo opdrachten tooencrypt virtuele schijven op de virtuele machine. Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#overview-of-disk-encryption).

Moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login). In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myKey*, en *myVM*.

Schakel eerst hello Azure Key Vault provider binnen uw Azure-abonnement met [az provider registreren](/cli/azure/provider#register) en maak een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld wordt een Resourcegroepnaam *myResourceGroup* in Hallo *eastus* locatie:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Maken van een Azure Key Vault met [az keyvault maken](/cli/azure/keyvault#create) en Hallo Sleutelkluis voor gebruik met schijfversleuteling inschakelen. Geef een unieke naam van de Sleutelkluis voor *keyvault_name* als volgt:

```azurecli
keyvault_name=mykeyvaultikf
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

Maken van een cryptografische sleutel in uw Sleutelkluis met [az keyvault-sleutel maken](/cli/azure/keyvault/key#create). Hallo volgende voorbeeld wordt een sleutel met de naam *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```

Maken van een service-principal met Azure Active Directory met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac). Hallo-service-principal ingangen Hallo verificatie en uitwisseling van de cryptografische sleutels uit Sleutelkluis. Hallo volgende voorbeeld wordt gelezen in Hallo waarden op voor de service-principal Hallo-Id en wachtwoord voor gebruik in latere opdrachten:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

Hallo wachtwoord wordt alleen uitgevoerd wanneer u Hallo-service-principal maken. Indien gewenst, weergeven en registreren Hallo wachtwoord (`echo $sp_password`). U kunt uw service-principals met lijst [az ad sp lijst](/cli/azure/ad/sp#list) en aanvullende informatie weergeven over een specifieke service-principal met [az ad sp weergeven](/cli/azure/ad/sp#show).

Machtigingen instellen voor uw Sleutelkluis met [az keyvault-beleid instellen](/cli/azure/keyvault#set-policy). Hallo in Hallo voorbeeld te volgen, service-principal-ID wordt geleverd door de voorgaande opdracht Hallo:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
    --key-permissions wrapKey \
    --secret-permissions set
```

Maak een VM met [az vm maken](/cli/azure/vm#create) en koppelt u een gegevensschijf 5 Gb. Alleen bepaalde marketplace-installatiekopieën ondersteuning bieden voor schijfversleuteling. Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM` met behulp van een **CentOS 7.2n** afbeelding:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour met behulp van VM Hallo `publicIpAddress` weergegeven in de uitvoer Hallo Hallo voorafgaand aan de opdracht. Maak een partitie en het bestandssysteem en Hallo gegevensschijf koppelen. Zie voor meer informatie [tooa Linux VM toomount Hallo nieuwe schijf verbinding](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Sluit uw SSH-sessie.

Versleutelen van uw virtuele machine met [az vm versleuteling inschakelen](/cli/azure/vm/encryption#enable). Hallo volgende voorbeeld wordt Hallo `$sp_id` en `$sp_password` variabelen in de voorgaande Hallo `ad sp create-for-rbac` opdracht:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Het duurt enige tijd Hallo schijf versleuteling proces toocomplete. Hallo-status van Hallo proces met bewaken [az vm versleuteling weergeven](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

status bevat Hallo **EncryptionInProgress**. Wacht totdat het Hallo-status voor Hallo OS schijf rapporten **VMRestartPending**, start u uw virtuele machine met [az vm opnieuw](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Hallo versleutelingsproces schijf voltooid tijdens het opstartproces hello, dus wacht een paar minuten voordat het controleren van de status van versleuteling opnieuw met Hallo **az vm versleuteling weergeven**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hallo moet nu statusrapport zowel Hallo OS en de gegevensschijf als **versleutelde**.

## <a name="overview-of-disk-encryption"></a>Overzicht van schijfversleuteling
Virtuele schijven op virtuele Linux-machines zijn versleuteld met behulp van rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Er zijn geen kosten voor het versleutelen van virtuele schijven in Azure. Cryptografische sleutels worden opgeslagen in Azure Key Vault met software-beveiliging, of u kunt importeren of genereren van uw tooFIPS gecertificeerde sleutels in Hardware Security Modules (HSM's) 140-2 level 2-standaarden. U beheer behouden over deze cryptografische sleutels en het gebruik ervan kunt controleren. Deze cryptografische sleutels zijn gebruikte tooencrypt en ontsleutelen van virtuele schijven gekoppelde tooyour VM. Een Azure Active Directory service-principal biedt een veilige mechanisme voor het uitgeven van deze cryptografische sleutels als virtuele machines van stroom in- of uitschakelen voorzien worden.

Hallo-proces voor het versleutelen van een virtuele machine is als volgt:

1. Maak een cryptografische sleutel in een Azure Sleutelkluis.
2. Configureer Hallo cryptografische sleutel toobe kan worden gebruikt voor het versleutelen van schijven.
3. tooread hello cryptografiesleutel van hello Azure Sleutelkluis, maak een Azure Active Directory-service principal met de juiste machtigingen Hallo.
4. Uitgeven Hallo opdracht tooencrypt uw virtuele schijven, opgeven hello Azure Active Directory-service-principal en de juiste cryptografische sleutel toobe gebruikt.
5. Hello Azure Active Directory-principal serviceaanvragen Hallo vereist cryptografiesleutel van Azure Sleutelkluis.
6. Hallo virtuele schijven worden versleuteld met behulp van de cryptografische sleutel Hallo opgegeven.

## <a name="encryption-process"></a>Versleutelingsproces
Schijfversleuteling is afhankelijk van Hallo extra onderdelen te volgen:

* **Azure Sleutelkluis** -toosafeguard cryptografische sleutels en geheimen die worden gebruikt voor Hallo schijf tokenversleuteling /-ontsleuteling proces gebruikt.
  * Als dit bestaat, kunt u een bestaande Azure Sleutelkluis. U hoeft geen toodedicate een Sleutelkluis tooencrypting schijven.
  * tooseparate administratieve grenzen en sleutel zichtbaarheid, kunt u een speciale Sleutelkluis.
* **Azure Active Directory** - ingangen Hallo veilig uitwisselen van vereiste cryptografische sleutels en verificatie voor acties aangevraagd.
  * Doorgaans kunt u een bestaand Azure Active Directory-exemplaar waarin de toepassing.
  * Hallo service-principal biedt een mechanisme voor beveiligde toorequest en de juiste cryptografische sleutels Hallo worden uitgegeven. U ontwikkelt een werkelijke toepassing die is geïntegreerd met Azure Active Directory niet.

## <a name="requirements-and-limitations"></a>Vereisten en beperkingen
Ondersteunde scenario's en vereisten voor de schijfversleuteling:

* Hallo Linux server SKU's - Ubuntu, CentOS, SUSE en SUSE Linux Enterprise Server (SLES) en Red Hat Enterprise Linux te volgen.
* Alle resources (zoals Sleutelkluis, een opslagaccount en een VM) moet in Hallo dezelfde Azure-regio en -abonnement.
* Standard A, D, DS, G en GS-serie biedt virtuele machines.

Schijfversleuteling is momenteel niet ondersteund in Hallo volgen scenario's:

* Basisstaffel virtuele machines.
* Virtuele machines gemaakt met behulp van Hallo klassieke implementatiemodel.
* OS-schijfversleuteling op Linux VM's uitschakelen.
* Hallo cryptografische sleutels op een al is versleuteld Linux-VM wordt bijgewerkt.

## <a name="create-azure-key-vault-and-keys"></a>Azure Sleutelkluis en de sleutels maken
Moet u Hallo nieuwste [Azure CLI 2.0](/cli/azure/install-az-cli2) geïnstalleerd en geregistreerd in Azure-account met behulp van tooan [az aanmelding](/cli/azure/#login). In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter *myResourceGroup*, *myKey*, en *myVM*.

de eerste stap Hallo toocreate een toostore Azure Sleutelkluis is de cryptografiesleutels. Azure Sleutelkluis sleutels en geheimen, kunnen opslaan of wachtwoorden die u toelaten om toosecurely ze implementeert in uw toepassingen en services. Voor versleuteling van de virtuele schijf, Sleutelkluis toostore een cryptografische sleutel die is gebruikt tooencrypt gebruiken of ontsleutelen van de virtuele schijven.

Hello Azure Key Vault provider binnen uw Azure-abonnement met ingeschakeld [az provider registreren](/cli/azure/provider#register) en maak een resourcegroep met [az groep maken](/cli/azure/group#create). Hallo volgende voorbeeld wordt een Resourcegroepnaam *myResourceGroup* in Hallo `eastus` locatie:

```azurecli
az provider register -n Microsoft.KeyVault
az group create --name myResourceGroup --location eastus
```

Hello Azure Key Vault met Hallo cryptografische sleutels en het bijbehorende compute resources, zoals opslag en virtuele machine zelf Hallo moeten zich bevinden in Hallo dezelfde regio. Maken van een Azure Key Vault met [az keyvault maken](/cli/azure/keyvault#create) en Hallo Sleutelkluis voor gebruik met schijfversleuteling inschakelen. Geef een unieke naam van de Sleutelkluis voor *keyvault_name* als volgt:

```azurecli
keyvault_name=myUniqueKeyVaultName
az keyvault create \
    --name $keyvault_name \
    --resource-group myResourceGroup \
    --location eastus \
    --enabled-for-disk-encryption True
```

U kunt met behulp van software of Hardware Security Model (HSM) protection cryptografiesleutels opslaan. Een HSM, moet een premium Sleutelkluis. Er is een extra kosten toocreating premium Sleutelkluis in plaats van standaard Sleutelkluis waarmee softwarematige beveiligde sleutels worden opgeslagen. toevoegen van een premium Sleutelkluis, in de voorgaande stap Hallo toocreate `--sku Premium` toohello opdracht. Hallo volgende voorbeeld wordt softwarematige beveiligde sleutels omdat er een standaard Sleutelkluis hebt gemaakt.

Voor beide beveiligingsmodellen moet hello Azure-platform toobe toorequest-Hallo cryptografiesleutels toegang verleend als Hallo VM wordt opgestart toodecrypt Hallo virtuele schijven. Maken van een cryptografische sleutel in uw Sleutelkluis met [az keyvault-sleutel maken](/cli/azure/keyvault/key#create). Hallo volgende voorbeeld wordt een sleutel met de naam *myKey*:

```azurecli
az keyvault key create --vault-name $keyvault_name --name myKey --protection software
```


## <a name="create-hello-azure-active-directory-service-principal"></a>Hello Azure Active Directory-service-principal maken
Wanneer virtuele schijven worden versleuteld en ontsleuteld, geeft u een account toohandle Hallo-authenticatie en uitwisselen van cryptografische sleutels uit Sleutelkluis. Dit account, een Azure Active Directory service-principal kunt hello Azure-platform toorequest Hallo juiste cryptografische sleutels namens Hallo VM. Een standaardexemplaar van de Azure Active Directory is beschikbaar in uw abonnement, hoewel veel organisaties hebben speciale mappen van Azure Active Directory.

Maken van een service-principal met Azure Active Directory met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac). Hallo volgende voorbeeld wordt gelezen in Hallo waarden op voor de service-principal Hallo-Id en wachtwoord voor gebruik in latere opdrachten:

```azurecli
read sp_id sp_password <<< $(az ad sp create-for-rbac --query [appId,password] -o tsv)
```

Hallo-wachtwoord wordt alleen weergegeven wanneer u Hallo service-principal maken. Indien gewenst, weergeven en registreren Hallo wachtwoord (`echo $sp_password`). U kunt uw service-principals met lijst [az ad sp lijst](/cli/azure/ad/sp#list) en aanvullende informatie weergeven over een specifieke service-principal met [az ad sp weergeven](/cli/azure/ad/sp#show).

toosuccessfully versleutelen of ontsleutelen van virtuele schijven, machtigingen op Hallo cryptografische sleutel die wordt opgeslagen in de Sleutelkluis moet set toopermit hello Azure Active Directory service principal tooread Hallo sleutels. Machtigingen instellen voor uw Sleutelkluis met [az keyvault-beleid instellen](/cli/azure/keyvault#set-policy). Hallo in Hallo voorbeeld te volgen, service-principal-ID wordt geleverd door de voorgaande opdracht Hallo:

```azurecli
az keyvault set-policy --name $keyvault_name --spn $sp_id \
  --key-permissions wrapKey \
  --secret-permissions set
```


## <a name="create-virtual-machine"></a>Virtuele machine maken
tooactually bepaalde virtuele schijven te versleutelen, kunt een virtuele machine maken en een gegevensschijf toevoegen. Maak een VM-tooencrypt met [az vm maken](/cli/azure/vm#create) en koppelt u een gegevensschijf 5 Gb. Alleen bepaalde marketplace-installatiekopieën ondersteuning bieden voor schijfversleuteling. Hallo volgende voorbeeld wordt een virtuele machine met de naam *myVM* met behulp van een **CentOS 7.2n** afbeelding:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image OpenLogic:CentOS:7.2n:7.2.20160629 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 5
```

SSH tooyour met behulp van VM Hallo `publicIpAddress` weergegeven in de uitvoer Hallo Hallo voorafgaand aan de opdracht. Maak een partitie en het bestandssysteem en Hallo gegevensschijf koppelen. Zie voor meer informatie [tooa Linux VM toomount Hallo nieuwe schijf verbinding](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#connect-to-the-linux-vm-to-mount-the-new-disk). Sluit uw SSH-sessie.


## <a name="encrypt-virtual-machine"></a>Virtuele machine versleutelen
tooencrypt hello virtuele schijven, u samenbrengen alle vorige Hallo-onderdelen:

1. Hello Azure Active Directory service-principal en wachtwoord opgeven.
2. Hallo Sleutelkluis toostore Hallo metagegevens voor uw versleutelde schijven opgeven.
3. Hallo cryptografische sleutels toouse voor Hallo daadwerkelijke versleuteling en ontsleuteling opgeven.
4. Geef op of u tooencrypt Hallo OS schijf, Hallo gegevensschijven of alle wilt.

Versleutelen van uw virtuele machine met [az vm versleuteling inschakelen](/cli/azure/vm/encryption#enable). Hallo volgende voorbeeld wordt Hallo `$sp_id` en `$sp_password` variabelen in de voorgaande Hallo `ad sp create-for-rbac` opdracht:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```

Het duurt enige tijd Hallo schijf versleuteling proces toocomplete. Hallo-status van Hallo proces met bewaken [az vm versleuteling weergeven](/cli/azure/vm/encryption#show):

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hallo uitvoer is vergelijkbaar toohello volgende ingekorte voorbeeld:

```json
[
  "dataDisk": "EncryptionInProgress",
  "osDisk": "EncryptionInProgress",
]
```

Wacht totdat het Hallo-status voor Hallo OS schijf rapporten **VMRestartPending**, start u uw virtuele machine met [az vm opnieuw](/cli/azure/vm#restart):

```azurecli
az vm restart --resource-group myResourceGroup --name myVM
```

Hallo versleutelingsproces schijf voltooid tijdens het opstartproces hello, dus wacht een paar minuten voordat het controleren van de status van versleuteling opnieuw met Hallo **az vm versleuteling weergeven**:

```azurecli
az vm encryption show --resource-group myResourceGroup --name myVM
```

Hallo moet nu statusrapport zowel Hallo OS en de gegevensschijf als **versleutelde**.


## <a name="add-additional-data-disks"></a>Toevoegen van extra gegevensschijven
Nadat u uw gegevensschijven hebt versleuteld, kunt u later toevoegen als u meer virtuele schijven tooyour VM en ook versleutelen. U kunt bijvoorbeeld een tweede virtuele schijf tooyour VM als volgt toevoegen:

```azurecli
az vm disk attach-new --resource-group myResourceGroup --vm-name myVM --size-in-gb 5
```

Voer Hallo opdracht tooencrypt Hallo virtuele schijven als volgt:

```azurecli
az vm encryption enable \
    --resource-group myResourceGroup \
    --name myVM \
    --aad-client-id $sp_id \
    --aad-client-secret $sp_password \
    --disk-encryption-keyvault $keyvault_name \
    --key-encryption-key myKey \
    --volume-type all
```


## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het beheren van Azure Sleutelkluis, met inbegrip van verwijderen van de cryptografische sleutels en kluizen, [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md).
* Zie voor meer informatie over schijfversleuteling, zoals het voorbereiden van een versleutelde aangepaste VM tooupload tooAzure, [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).
