---
title: Azure Disk Encryption Veelgestelde vragen | Microsoft Docs
description: In dit artikel vindt u antwoorden op veelgestelde vragen voor Microsoft Azure Disk Encryption for Windows en Linux IaaS VM's.
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: 7188da52-5540-421d-bf45-d124dee74979
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: devtiw
ms.openlocfilehash: 0d15bf42c156ea7a72c54d690f4016877913efe4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-disk-encryption-frequently-asked-questions-faq"></a>Azure Disk Encryption Frequently Asked Questions (FAQ)

Deze Veelgestelde vragen over de antwoorden op vragen over Azure disk encryption voor Windows en Linux IaaS VM's, voor meer informatie over deze service, lezen [Azure Disk Encryption for Windows en Linux IaaS VM's](https://docs.microsoft.com/azure/security/azure-security-disk-encryption).

## <a name="general-questions"></a>Algemene vragen
**V:** Welke regio is de schijf van Azure-versleuteling in GA?

**A:** Azure disk encryption voor Windows en Linux IaaS VM's is beschikbaar in GA in alle openbare Azure-regio.

**V:** welke gebruiker merkt dat zijn beschikbaar bij Azure Disk Encryption?

**A:** Azure schijf versleuteling GA ondersteunt Azure Resource Manager-sjablonen, Azure PowerShell, Azure CLI. Hierdoor kunt u veel flexibiliteit in die u drie verschillende opties hebt voor schijf-codering inschakelen voor uw IaaS VM's. Meer informatie over de gebruikerservaring en stapsgewijze instructies vindt u in de implementatiescenario's voor Azure Disk Encryption en ervaringen.

**V:** hoeveel kost Azure Disk Encryption?

**A:** er zijn geen kosten voor het versleutelen van VM-schijven met Azure Disk Encryption.

**V:** welke lagen van de virtuele machine kan ik gebruiken Azure Disk Encryption met?

**A:** Azure Disk Encryption is alleen beschikbaar in Standard-laag VMs inclusief [A, D, DS, G, GS, F](https://azure.microsoft.com/pricing/details/virtual-machines/) enzovoort reeks IaaS VM's met inbegrip van virtuele machines met premium-opslag. Het is niet beschikbaar op virtuele machines van Basic laag.

**V:** wat Linux-distributies worden ondersteund door Azure Disk Encryption?

**A:** Azure Disk Encryption wordt ondersteund op de volgende server Linux-distributies en versies:

| Linux-distributie | Versie | Type van het volume voor de versleuteling wordt ondersteund|
| --- | --- |--- |
| Ubuntu | 16.04-DAGELIJKS-TNS | Besturingssysteem en schijf |
| Ubuntu | 14.04.5-DAILY-LTS | Besturingssysteem en schijf |
| RHEL | 7.3 | Besturingssysteem en schijf |
| RHEL | 7.2 | Besturingssysteem en schijf |
| RHEL | 6.8 | Besturingssysteem en schijf |
| RHEL | 6.7 | Gegevensschijf |
| CentOS | 7.3 | Besturingssysteem en schijf |
| CentOS | 7.2n | Besturingssysteem en schijf |
| CentOS | 6.8 | Besturingssysteem en schijf |
| CentOS | 7.1 | Gegevensschijf |
| CentOS | 7.0 | Gegevensschijf |
| CentOS | 6.7 | Gegevensschijf |
| CentOS | 6.6 | Gegevensschijf |
| CentOS | 6.5 | Gegevensschijf |
| openSUSE | 13.2 | Gegevensschijf |
| SLES | 12 SP1 | Gegevensschijf |
| SLES | Prioriteit: 12-SP1 | Gegevensschijf |
| SLES | HPC 12 | Gegevensschijf |
| SLES | Prioriteit: 11-SP4 | Gegevensschijf |
| SLES | 11 SP4 | Gegevensschijf |

**V:** hoe kan ik aan de slag met Azure Disk Encryption?

**A:** klanten kunnen lezen hoe aan de slag door te lezen van de whitepaper Azure Disk Encryption is zich [hier](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)

**V:** kan ik de opstart- en gegevens volumes met Azure Disk Encryption coderen?

**A:** Ja, u opstart- en gegevensvolumes voor Windows en Linux IaaS VM's kunt versleutelen. Voor Windows-VM's kunt u de gegevens zonder eerste encrpting volume met het besturingssysteem niet coderen. U kunt het gegevensvolume zonder het besturingssysteem encryptinng volume eerst versleutelen voor Linux VM's. Zodra u hebt het besturingssysteemvolume versleuteld voor Liux, wordt uitschakelen van IaaS VM's van Linux-versleuteling op een volume met het besturingssysteem niet ondersteund

**V:** biedt Azure Disk Encryption inschakelen met een 'bring your own key' (BYOK) mogelijkheid?

**A:** Ja, kunt u uw eigen sleutel versleutelingssleutels opgeven. Deze sleutels behoud in Azure Sleutelkluis, die de sleutelarchief voor Azure Disk Encryption is. Zie voor meer informatie over de sleutelcodering belangrijke scenario's, de implementatiescenario's voor Azure Disk Encryption en ervaringen

**V:** kan ik een Azure gemaakt sleutelcodering sleutel gebruiken?

**A:** Ja, u kunt Azure sleutelkluis sleutels coderingssleutel voor Azure disk encryption gebruik genereren. Deze sleutels behoud in Azure Sleutelkluis, die de sleutelarchief voor Azure Disk Encryption is. Zie voor meer informatie over de sleutelcodering belangrijke scenario's, de implementatiescenario's voor Azure Disk Encryption en ervaringen

**V:** kan ik lokale key management service/HSM ter bescherming van de versleutelingssleutels gebruiken?

**A:** u lokale key management service/HSM ter bescherming van de versleutelingssleutels met Azure disk encryption niet gebruiken. U kunt alleen de Azure sleutelkluis-service gebruiken ter bescherming van de versleutelingssleutels. Zie voor meer informatie over de sleutelcodering belangrijke scenario's, de implementatiescenario's voor Azure Disk Encryption en ervaringen

**V:** schijfversleuteling wat zijn de vereisten voor Azure configureren?

**A:** de Azure schijf versleuteling vereiste PowerShell-script voor het maken van AAD-toepassing maken van nieuwe sleutelkluis of setup bestaande sleutelkluis voor toegang tot de schijf versleuteling inschakelen van versleuteling en beveiliging geheimen en de sleutel.  Zie voor meer informatie over de sleutelcodering belangrijke scenario's, de vereisten voor Azure Disk Encryption en implementatiescenario's en oplossingen

**V:** waar vind ik meer informatie over het gebruik van PowerShell voor Azure Disk Encryption configureren?

**A:** hebben We sommige geweldige artikelen over hoe u Azure Disk Encryption basistaken, evenals meer geavanceerde scenario's kunt uitvoeren. Bekijk voor de basistaken verkennen [Azure Disk Encryption met Azure PowerShell - Part 1](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/16/explore-azure-disk-encryption-with-azure-powershell/). Zie voor meer geavanceerde scenario's, verkennen [Azure Disk Encryption met Azure PowerShell – deel 2](https://blogs.msdn.microsoft.com/azuresecurity/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2/)

**V:** welke versie van Azure PowerShell wordt ondersteund door Azure Disk Encryption?

**A:** gebruik van de nieuwste versie van Azure PowerShell SDK-versie van Azure Disk Encryption te configureren. Download de nieuwste versie van [Azure PowerShell](https://github.com/Azure/azure-powershell/releases). Azure Disk Encryption wordt niet ondersteund door Azure SDK-versie 1.1.0.

> [!NOTE]
> De extensie Linux Azure schijf versleuteling preview is afgeschaft. Raadpleeg de documentatie voor meer informatie, [hier](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/12/deprecating-azure-disk-encryption-preview-extension-for-linux-iaas-vms/)

**V:** kan ik Azure disk encryption toepassen op mijn aangepaste Linux-installatiekopie?

**A:** u Azure disk encryption kan toepassen op uw aangepaste Linux-installatiekopie. Wij ondersteunen alleen de Linux-afbeeldingen voor de ondersteunde distributies die hierboven worden genoemd. We bieden geen ondersteuning voor aangepaste Linux-installatiekopieën momenteel

**V:** kunt ik updates toepassen op een Linux Red Hat VM die gebruikmaakt van Yum update?

**A:** Ja, u kunt werken en of een Red Hat Linnux VM aanwijzingen te volgen patch [hier](https://blogs.msdn.microsoft.com/azuresecurity/2017/07/13/applying-updates-to-a-encrypted-azure-iaas-red-hat-vm-using-yum-update/)

**V:** waar kan ik ga naar de vraag of geef feedback

**A:** kunt u vragen of feedback op het forum van Azure disk encryption vraagt bieden [hier](https://social.msdn.microsoft.com/Forums/home?forum=AzureDiskEncryption)

## <a name="see-also"></a>Zie ook
In dit document hebt u geleerd meer informatie over de meest voorkomende vragen met betrekking tot Azure disk encryption toe voor meer informatie over deze service en de mogelijkheid lezen:

- [Schijfversleuteling in Azure Security Center toepassen](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Een virtuele Machine van Azure versleutelen](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Azure Data Encryption in rust](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
