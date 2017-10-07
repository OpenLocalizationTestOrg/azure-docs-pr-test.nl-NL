---
title: een Azure Linux VM-ID aaaGet | Microsoft Docs
description: Hierin wordt beschreven hoe tooget en gebruik een unieke Azure Linux VM-id.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Toegang tot en met behulp van de unieke ID van Azure VM
De unieke ID van de Azure VM is een id 128 bits gecodeerd en opgeslagen in alle Azure IaaS VM's SMBIOS en kan op dit moment worden gelezen met platform BIOS-opdrachten.

De unieke ID van de Azure VM is een alleen-lezen eigenschap. Azure unieke ID van de VM niet veranderd bij opnieuw opstarten afsluiting van (hetzij geplande voor niet-geplande), starten/stoppen ongedaan toewijzen, service-herstel of terugzetten aanwezig. Nieuwe Azure VM-ID wordt is geconfigureerd als Hallo VM een momentopname en gekopieerde toocreate een nieuw exemplaar is.

> [!NOTE]
> Als u oudere VM's die zijn gemaakt en uitgevoerd sinds deze nieuwe functie (18 September 2014), hebt u uitgerold Start uw tooautomatically VM ophalen Azure unieke ID.
> 
> 

tooaccess Azure unieke ID van VM uit binnen Hallo VM:

## <a name="create-a-vm"></a>Een virtuele machine maken
Zie voor meer informatie [een virtuele Machine maken](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-toohello-vm"></a>Verbinding maken met toohello VM
Zie voor meer informatie [SSH in Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="query-vm-unique-id"></a>De unieke ID van de query VM
Opdracht (voorbeeld wordt **Ubuntu**):

```bash
sudo dmidecode | grep UUID
```

Voorbeeld van de verwachte resultaten:

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

Vervaldatum tooBig Endian bits ordening, zijn hello werkelijke unieke ID van de VM in dit geval:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

De unieke ID van de Azure VM kan worden gebruikt in verschillende scenario's of Hallo VM wordt uitgevoerd op Azure of on-premises en kan helpen uw licentiegegevens, rapportage of algemene bijhouden-vereisten die u van uw Azure IaaS-implementaties misschien. Veel onafhankelijke softwareleveranciers bouwen van toepassingen en gecertificeerd door ze in Azure moet mogelijk een Azure VM gedurende de levensduur en tootell tooidentify als Hallo VM wordt uitgevoerd op Azure, on-Premises of andere cloudproviders. Deze platform-id kunt bijvoorbeeld detecteren als Hallo-software correct is gelicentieerd of help toocorrelate elke VM tooits gegevensbron zoals tooassist over het instellen van de metrische gegevens voor Hallo rechts voor de juiste platform Hallo en tootrack en deze metrische gegevens voor de correleren andere toepassingen.

