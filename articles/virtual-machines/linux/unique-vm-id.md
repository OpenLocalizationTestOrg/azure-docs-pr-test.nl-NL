---
title: Een Azure Linux VM-ID ophalen | Microsoft Docs
description: Hierin wordt beschreven hoe halen en gebruik van een Azure Linux VM unieke ID.
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
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a>Toegang tot en met behulp van de unieke ID van Azure VM
De unieke ID van de Azure VM is een id 128 bits gecodeerd en opgeslagen in alle Azure IaaS VM's SMBIOS en kan op dit moment worden gelezen met platform BIOS-opdrachten.

De unieke ID van de Azure VM is een alleen-lezen eigenschap. Azure unieke ID van de VM niet veranderd bij opnieuw opstarten afsluiting van (hetzij geplande voor niet-geplande), starten/stoppen ongedaan toewijzen, service-herstel of terugzetten aanwezig. Als de virtuele machine een momentopname is en voor het maken van een nieuw exemplaar gekopieerd, wordt echter nieuwe Azure VM-ID geconfigureerd.

> [!NOTE]
> Als u oudere VMs gemaakt en uw virtuele machine automatisch ophalen van een Azure unieke id uitgevoerd sinds deze nieuwe functie kreeg uitgerold (18 September 2014), neem opnieuw opstarten
> 
> 

Toegang krijgen tot Azure unieke ID van VM uit vanuit de virtuele machine:

## <a name="create-a-vm"></a>Een virtuele machine maken
Zie voor meer informatie [een virtuele Machine maken](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="connect-to-the-vm"></a>Verbinding maken met de virtuele machine
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

Als gevolg van Big Endian bit ordening, zijn werkelijke unieke ID van de VM in dit geval:

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

De unieke ID van de Azure VM kan worden gebruikt in verschillende scenario's of de virtuele machine wordt uitgevoerd op Azure of on-premises en kan helpen uw licentiegegevens, rapportage of algemene bijhouden-vereisten die u van uw Azure IaaS-implementaties misschien. Kunnen het veel onafhankelijke softwareleveranciers bouwen van toepassingen en gecertificeerd door ze in Azure nodig te identificeren van een Azure VM gedurende de levenscyclus en zien of als de virtuele machine wordt uitgevoerd op Azure, on-Premises of op andere cloudproviders. Deze platform-id kan bijvoorbeeld helpen detecteren als de software correct is gelicentieerd of kunnen geen VM-gegevens naar de bron, zoals correleren om u te helpen bij het instellen van de juiste metrische gegevens voor de juiste platform en voor het bijhouden en deze metrische gegevens voor ander gebruik correleren.

