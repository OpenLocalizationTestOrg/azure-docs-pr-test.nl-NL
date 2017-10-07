---
title: aaaEncrypt schijven op een Linux-VM met hello Azure CLI 1.0 | Microsoft Docs
description: Hoe tooencrypt schijven op een Linux-VM met hello Azure CLI 1.0 en Hallo Resource Manager-implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a>Versleutelen van schijven op een Linux-VM met hello Azure CLI 1.0
Voor de uitgebreide virtuele machine (VM) beveiliging en naleving, kunnen virtuele schijven in Azure worden versleuteld in rust. Schijven worden versleuteld met behulp van de cryptografische sleutels die worden beveiligd in een Azure Sleutelkluis. U kunt het gebruik ervan controleren en beheren van deze cryptografische sleutels. Dit artikel wordt beschreven hoe virtuele schijven op een Linux-VM met tooencrypt hello Azure CLI 1.0 en Hallo Resource Manager-implementatiemodel.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI-versies toocomplete Hallo taak
U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:

- [Azure CLI 1.0](#quick-commands) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)
- [Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel

## <a name="quick-commands"></a>Snelle opdrachten
Als u moet tooquickly Hallo taak, na de sectie details Hallo base Hallo opdrachten tooencrypt virtuele schijven op de virtuele machine. Meer gedetailleerde informatie en context voor elke stap u rest Hallo van Hallo document vindt [vanaf hier](#overview-of-disk-encryption).

U moet Hallo [nieuwste Azure CLI 1.0](../../xplat-cli-install.md) geïnstalleerd en geregistreerd in het Hallo-Resource Manager-modus als volgt gebruiken:

```azurecli
azure config mode arm
```

In Hallo vervangen volgende voorbeelden parameternamen voorbeeld door uw eigen waarden. De namen van de voorbeeld-parameter `myResourceGroup`, `myKeyVault`, en `myVM`.

Eerst hello Azure Key Vault provider binnen uw Azure-abonnement ingeschakeld en een resourcegroep maken. Hallo volgende voorbeeld wordt een Resourcegroepnaam `myResourceGroup` in Hallo `WestUS` locatie:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Maak een Azure Sleutelkluis. Hallo volgende voorbeeld wordt een Sleutelkluis met de naam `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

Een cryptografische sleutel in uw Sleutelkluis maken en inschakelen voor schijfversleuteling. Hallo volgende voorbeeld wordt een sleutel met de naam `myKey`:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

Maak een eindpunt met Azure Active Directory voor het verwerken van Hallo verificatie en uitwisselen van cryptografische sleutels uit Sleutelkluis. Hallo `--home-page` en `--identifier-uris` hoeft geen toobe Werkelijke routeerbare adresruimte. Voor Hallo hoogste niveau van beveiliging, worden clientgeheimen gebruikt in plaats van wachtwoorden. Hello Azure CLI kan momenteel niet clientgeheimen genereren. Clientgeheimen kunnen alleen worden gegenereerd in hello Azure-portal. Hallo volgende voorbeeld wordt een Azure Active Directory-eindpunt met de naam `myAADApp` en maakt gebruik van een wachtwoord van `myPassword`. Geef uw eigen wachtwoord als volgt:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Opmerking Hallo `applicationId` in Hallo-uitvoer van de voorgaande opdracht hello wordt weergegeven. Deze toepassing-ID wordt gebruikt in Hallo stappen te volgen:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

Een data schijf tooan bestaande virtuele machine toevoegen. Hallo volgende voorbeeld wordt een schijf tooa van gegevens met de naam VM `myVM`:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Controleer de details Hallo voor uw Sleutelkluis en Hallo sleutel die u hebt gemaakt. U moet de kluis-ID sleutel, URI en sleutel Hallo URL in de laatste stap Hallo. Hallo volgende voorbeeld bekijkt hello details voor een Sleutelkluis met de naam `myKeyVault` en de sleutel met de naam `myKey`:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Versleutelen van uw schijven als volgt invoeren van uw eigen namen van parameters in:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Hello Azure CLI biedt geen uitgebreide fouten tijdens het versleutelingsproces Hallo. Raadpleeg voor aanvullende informatie voor probleemoplossing `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`. Als Hallo veel variabelen voorafgaand aan de opdracht heeft en u krijgt niet veel opgave toowhy Hallo mislukt, een voorbeeld van de volledige opdracht is als volgt:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Controleer ten slotte coderingsstatus Hallo opnieuw tooconfirm dat uw virtuele schijven nu zijn gecodeerd. Hallo volgende voorbeeld controleert Hallo status van een virtuele machine met de naam `myVM` in Hallo `myResourceGroup` resourcegroep:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a>Overzicht van schijfversleuteling
Virtuele schijven op virtuele Linux-machines zijn versleuteld met behulp van rest [dm-crypt](https://wikipedia.org/wiki/Dm-crypt). Er zijn geen kosten voor het versleutelen van virtuele schijven in Azure. Cryptografische sleutels worden opgeslagen in Azure Key Vault met software-beveiliging, of u kunt importeren of genereren van uw tooFIPS gecertificeerde sleutels in Hardware Security Modules (HSM's) 140-2 level 2-standaarden. U beheer behouden over deze cryptografische sleutels en het gebruik ervan kunt controleren. Deze cryptografische sleutels zijn gebruikte tooencrypt en ontsleutelen van virtuele schijven gekoppelde tooyour VM. Een Azure Active Directory-eindpunt biedt een veilige mechanisme voor het uitgeven van deze cryptografische sleutels als virtuele machines van stroom in- of uitschakelen voorzien worden.

Hallo-proces voor het versleutelen van een virtuele machine is als volgt:

1. Maak een cryptografische sleutel in een Azure Sleutelkluis.
2. Configureer Hallo cryptografische sleutel toobe kan worden gebruikt voor het versleutelen van schijven.
3. een eindpunt met Azure Active Directory met de juiste machtigingen Hallo tooread Hallo cryptografiesleutel van hello Azure Key Vault maken
4. Uitgeven Hallo opdracht tooencrypt uw virtuele schijven, geven hello Azure Active Directory-eindpunt en de juiste cryptografische sleutel toobe gebruikt.
5. Hello Azure Active Directory-eindpunt vereist cryptografische sleutel Hallo-aanvragen van Azure Sleutelkluis.
6. Hallo virtuele schijven worden versleuteld met behulp van de cryptografische sleutel Hallo opgegeven.

## <a name="supporting-services-and-encryption-process"></a>Ondersteuning van services en versleuteling
Schijfversleuteling is afhankelijk van Hallo extra onderdelen te volgen:

* **Azure Sleutelkluis** -toosafeguard cryptografische sleutels en geheimen die worden gebruikt voor Hallo schijf tokenversleuteling /-ontsleuteling proces gebruikt.
  * Als dit bestaat, kunt u een bestaande Azure Sleutelkluis. U hoeft geen toodedicate een Sleutelkluis tooencrypting schijven.
  * tooseparate administratieve grenzen en sleutel zichtbaarheid, kunt u een speciale Sleutelkluis.
* **Azure Active Directory** - ingangen Hallo veilig uitwisselen van vereiste cryptografische sleutels en verificatie voor acties aangevraagd.
  * Doorgaans kunt u een bestaand Azure Active Directory-exemplaar waarin de toepassing.
  * Hallo toepassing is van een eindpunt voor Hallo Sleutelkluis en de virtuele Machine services toorequest en ophalen van de juiste cryptografische sleutels Hallo uitgegeven. U ontwikkelt een werkelijke toepassing die is geïntegreerd met Azure Active Directory niet.

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

## <a name="create-hello-azure-key-vault-and-keys"></a>Maak hello Azure Sleutelkluis en de sleutels
toocomplete hello rest van deze handleiding, moet u Hallo [nieuwste Azure CLI 1.0](../../xplat-cli-install.md) geïnstalleerd en geregistreerd in het Hallo-Resource Manager-modus als volgt gebruiken:

```azurecli
azure config mode arm
```

In de gehele opdrachtvoorbeelden hello, vervangen door alle voorbeeldparameters uw eigen namen, locatie en sleutelwaarden. Hallo volgende voorbeelden wordt gebruikt een conventie `myResourceGroup`, `myKeyVault`, `myAADApp`, enzovoort.

de eerste stap Hallo toocreate een toostore Azure Sleutelkluis is de cryptografiesleutels. Azure Sleutelkluis sleutels en geheimen, kunnen opslaan of wachtwoorden die u toelaten om toosecurely ze implementeert in uw toepassingen en services. Voor versleuteling van de virtuele schijf, Sleutelkluis toostore een cryptografische sleutel die is gebruikt tooencrypt gebruiken of ontsleutelen van de virtuele schijven.

Hello Azure Sleutelkluis-provider in uw Azure-abonnement inschakelen en vervolgens een resourcegroep maken. Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `WestUS` locatie:

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

Hello Azure Key Vault met Hallo cryptografische sleutels en het bijbehorende compute resources, zoals opslag en virtuele machine zelf Hallo moeten zich bevinden in Hallo dezelfde regio. Hallo volgende voorbeeld wordt een Azure Sleutelkluis met de naam `myKeyVault`:

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

U kunt met behulp van software of Hardware Security Model (HSM) protection cryptografiesleutels opslaan. Een HSM, moet een premium Sleutelkluis. Er is een extra kosten toocreating premium Sleutelkluis in plaats van standaard Sleutelkluis waarmee softwarematige beveiligde sleutels worden opgeslagen. toevoegen van een premium Sleutelkluis, in de voorgaande stap Hallo toocreate `--sku Premium` toohello opdracht. Hallo volgende voorbeeld wordt softwarematige beveiligde sleutels omdat er een standaard Sleutelkluis hebt gemaakt.

Voor beide beveiligingsmodellen moet hello Azure-platform toobe toorequest-Hallo cryptografiesleutels toegang verleend als Hallo VM wordt opgestart toodecrypt Hallo virtuele schijven. Een coderingssleutel binnen uw Sleutelkluis maken en inschakelen voor gebruik met versleuteling van de virtuele schijf. Hallo volgende voorbeeld wordt een sleutel met de naam `myKey` en schakelt u deze voor de schijfversleuteling:

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a>Hello Azure Active Directory-toepassing maken
Wanneer virtuele schijven worden versleuteld en ontsleuteld, gebruikt u een eindpunt toohandle Hallo-authenticatie en uitwisselen van cryptografische sleutels uit Sleutelkluis. Dit eindpunt, een Azure Active Directory-toepassing kunt hello Azure-platform toorequest Hallo juiste cryptografische sleutels namens Hallo VM. Een standaardexemplaar van de Azure Active Directory is beschikbaar in uw abonnement, hoewel veel organisaties hebben speciale mappen van Azure Active Directory.

Als u niet een volledige Azure Active Directory-toepassing maakt, Hallo `--home-page` en `--identifier-uris` parameters in het volgende voorbeeld Hallo hoeft geen toobe Werkelijke routeerbare adresruimte. Hallo bepaalt volgende voorbeeld ook een geheim op basis van wachtwoorden in plaats van genereren van sleutels van binnen hello Azure-portal. Als deze tijd kan niet genereren van sleutels worden uitgevoerd vanuit hello Azure CLI.

Uw Azure Active Directory-toepassing maken. Hallo volgende voorbeeld maakt u een toepassing met de naam `myAADApp` en maakt gebruik van een wachtwoord van `myPassword`. Geef uw eigen wachtwoord als volgt:

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

Maak een notitie van Hallo `applicationId` die wordt geretourneerd als Hallo uitvoer van de voorgaande opdracht Hallo. Deze toepassing-ID wordt gebruikt in een aantal Hallo resterende stappen. Maak vervolgens een service principal name (SPN) zodat de toepassing hello toegankelijk binnen uw omgeving. toosuccessfully versleutelen of ontsleutelen van virtuele schijven, machtigingen op Hallo cryptografische sleutel die wordt opgeslagen in de Sleutelkluis moet set toopermit hello tooread Hallo-sleutels Azure Active Directory-toepassingen.

Hallo SPN maken en de juiste machtigingen Hallo als volgt instellen:

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a>Toevoegen van een virtuele schijf en versleutelingsstatus controleren
tooactually bepaalde virtuele schijven te versleutelen, kunt een schijf tooan bestaande virtuele machine toevoegen. Voeg een 5Gb gegevens schijf tooan bestaande VM als volgt:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Hallo virtuele schijven zijn momenteel niet versleuteld. Hallo huidige coderingsstatus van uw virtuele machine als volgt bekijken:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a>Versleutelen van virtuele schijven
toonow versleutelen Hallo virtuele schijven, samenbrengen van alle vorige Hallo-onderdelen:

1. Hello Azure Active Directory-toepassing en het wachtwoord opgeven.
2. Hallo Sleutelkluis toostore Hallo metagegevens voor uw versleutelde schijven opgeven.
3. Hallo cryptografische sleutels toouse voor Hallo daadwerkelijke versleuteling en ontsleuteling opgeven.
4. Geef op of u tooencrypt Hallo OS schijf, Hallo gegevensschijven of alle wilt.

U kunt Hallo gedetailleerde gegevens voor uw Azure Sleutelkluis en Hallo sleutel die u hebt gemaakt, als u nodig hebt Hallo Sleutelkluis-ID, URI, en vervolgens sleutel URL in de laatste stap Hallo bekijken:

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

Versleutelen van uw virtuele schijven met Hallo-uitvoer van Hallo `azure keyvault show` en `azure keyvault key show` opdrachten als volgt:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

Aangezien hello voorgaande opdracht veel variabelen heeft, hello volgende voorbeeld is de volledige opdracht Hallo ter referentie:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

Hello Azure CLI biedt geen uitgebreide fouten tijdens het versleutelingsproces Hallo. Raadpleeg voor aanvullende informatie voor probleemoplossing `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` op Hallo VM u versleutelt.

Ten slotte kunt Hallo versleutelingsstatus controleren opnieuw tooconfirm dat uw virtuele schijven nu zijn gecodeerd:

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a>Toevoegen van extra gegevensschijven
Nadat u uw gegevensschijven hebt versleuteld, kunt u later toevoegen als u meer virtuele schijven tooyour VM en ook versleutelen. Bij het uitvoeren van Hallo `azure vm enable-disk-encryption` opdracht, verhoging Hallo sequence versie met behulp van Hallo `--sequence-version` parameter. Deze reeks versie-parameter kunt u tooperform herhaalde bewerkingen op Hallo dezelfde virtuele machine.

U kunt bijvoorbeeld een tweede virtuele schijf tooyour VM als volgt toevoegen:

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

Deze keer Hallo toe te voegen als Hallo opdracht tooencrypt Hallo virtuele schijven, opnieuw `--sequence-version` parameter en stijgende Hallo waarde van de eerste als volgt uitvoeren:

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het beheren van Azure Sleutelkluis, met inbegrip van verwijderen van de cryptografische sleutels en kluizen, [Key Vault beheren met CLI](../../key-vault/key-vault-manage-with-cli2.md).
* Zie voor meer informatie over schijfversleuteling, zoals het voorbereiden van een versleutelde aangepaste VM tooupload tooAzure, [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).
