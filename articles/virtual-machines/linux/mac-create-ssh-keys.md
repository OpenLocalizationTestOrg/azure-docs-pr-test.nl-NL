---
title: aaaCreate en gebruikt een SSH sleutelpaar voor virtuele Linux-machines in Azure | Microsoft Docs
description: Hoe toocreate en gebruik een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines in Azure tooimprove beveiliging van het verificatieproces Hallo Hallo.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a>Hoe toocreate en gebruikt een SSH-sleutel voor openbare en persoonlijke voor virtuele Linux-machines in Azure koppelen
Met de combinatie van een secure shell (SSH), kunt u virtuele machines (VM's) maken in Azure die SSH-sleutels gebruiken voor verificatie, hoeft u Hallo wachtwoorden toolog in. Dit artikel ziet u hoe tooquickly genereren en het gebruik van een SSH-protocol versie 2 RSA openbare en persoonlijke sleutelbestand paar voor virtuele Linux-machines. Zie voor meer stappen en aanvullende voorbeelden gegeven gedetailleerde, [gedetailleerde stappen toocreate SSH-sleutelparen en certificaten](create-ssh-keys-detailed.md).

## <a name="create-an-ssh-key-pair"></a>Een SSH-sleutelpaar maken
Gebruik Hallo `ssh-keygen` toocreate SSH openbare en persoonlijke sleutelbestanden die gemaakt in Hallo standaard zijn opdracht `~/.ssh` directory, maar u kunt aanvullende wachtwoordzin (een wachtwoord tooaccess Hallo persoonlijke sleutelbestand) en een andere locatie opgeven wanneer u wordt gevraagd. Hallo volgende opdracht uit een Bash-shell, het beantwoorden van Hallo prompts met uw eigen gegevens worden uitgevoerd.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a>Hallo SSH-sleutelpaar gebruiken
Hallo openbare sleutel die u op uw Linux-VM in Azure plaatst, wordt standaard opgeslagen in `~/.ssh/id_rsa.pub`, tenzij u Hallo locatie gewijzigd wanneer u ze hebt gemaakt. Als u Hallo [Azure CLI 2.0](/cli/azure) toocreate uw VM Hallo-locatie van deze openbare sleutel opgeven wanneer u Hallo [az vm maken](/cli/azure/vm#create) Hello `--ssh-key-path` optie. Als u inhoud kopiëren en Hallo van Hallo openbaar-sleutelbestand toouse in hello Azure-portal of een Resource Manager-sjabloon plakken, zorg er dan voor dat u alle aanvullende witruimte niet kopiëren. Als u OS X gebruikt, kunt u bijvoorbeeld Hallo openbaar-sleutelbestand doorsluizen (standaard **~/.ssh/id_rsa.pub**) te**pbcopy** toocopy Hallo inhoud (Er zijn andere Linux-programma's die hetzelfde is, zoals Hallo`xclip`).

Als u niet vertrouwd bent met openbare SSH-sleutels, kunt u de openbare sleutel bekijken door `cat` als volgt uit te voeren. Vervang `~/.ssh/id_rsa.pub` door de locatie van uw eigen openbare-sleutelbestand:

```bash
cat ~/.ssh/id_rsa.pub
```

Met de openbare sleutel Hallo op uw virtuele machine in Azure, IP-adres of de DNS-naam van uw virtuele machine gebruik van SSH tooyour VM Hallo (onthouden tooreplace `azureuser` en `myvm.westus.cloudapp.azure.com` hieronder met Hallo beheerdersgebruikersnaam en het volledig gekwalificeerde domeinnaam Hallo-- of het IP-adres):

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

Als u een wachtwoordzin opgegeven tijdens het maken van uw sleutelpaar, Voer Hallo wachtwoordzin wanneer u wordt gevraagd tijdens het Hallo-aanmelding. (Hallo-server toegevoegd tooyour `~/.ssh/known_hosts` map en u won't gevraagd tooconnect pas weer Hallo openbare sleutel van uw Azure VM-wijzigingen of Hallo-servernaam is verwijderd van `~/.ssh/known_hosts`.)

## <a name="next-steps"></a>Volgende stappen

Virtuele machines die zijn gemaakt met behulp van SSH-sleutels zijn standaard geconfigureerd met wachtwoorden die zijn uitgeschakeld, toomake brute-geforceerde raden probeert aanzienlijk duurder en daarom moeilijk. Dit onderwerp beschrijft het maken van een eenvoudig SSH-sleutelpaar voor snel gebruik. Als u meer hulp bij het maken van uw SSH-sleutelpaar nodig of extra certificaten nodig, Zie [gedetailleerde stappen toocreate SSH-sleutelparen en certificaten](create-ssh-keys-detailed.md).

U kunt virtuele machines die gebruikmaken van uw SSH-sleutelpaar met hello Azure-portal, CLI en sjablonen maken:

* [Maak een beveiligde Linux-VM met hello Azure-portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Maak een beveiligde Linux-VM met hello Azure CLI 2.0)](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
