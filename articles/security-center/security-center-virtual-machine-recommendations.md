---
title: aaaProtecting uw virtuele machines in Azure Security Center | Microsoft Docs
description: Dit document gaat in Azure Security Center aanbevelingen die u helpen beveiligen van uw virtuele machines en blijven in overeenstemming met het beveiligingsbeleid.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 926c04974f61215b4a3e02646f23dafb87c793e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a>Beveiligen van uw virtuele machines in Azure Security Center
Azure Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources. Wanneer het Beveiligingscentrum identificeert mogelijke beveiligingsproblemen, maakt deze aanbevelingen die u helpt bij Hallo Hallo nodig-besturingselementen configureren.  Aanbevelingen tooAzure brontypen die van toepassing: virtuele machines (VM's), netwerken, SQL en toepassingen.

In dit artikel biedt de aanbevelingen die van toepassing zijn tooVMs.  VM aanbevelingen center rond gegevensverzameling, systeemupdates, inrichting van antimalware, toepassen versleutelen van uw VM-schijven en meer.  Gebruik Hallo onderstaande tabel als een verwijzing toohelp erkent u Hallo beschikbaar VM aanbevelingen en elk criterium doen als u deze toe te passen.

## <a name="available-vm-recommendations"></a>Beschikbare VM aanbevelingen
| Aanbeveling | Beschrijving |
| --- | --- |
| [Gegevensverzameling voor abonnementen inschakelen](security-center-enable-data-collection.md) |Raadt aan om te schakelen op het verzamelen van gegevens in het Hallo-beveiligingsbeleid voor elk van uw abonnementen en alle virtuele machines (VM's) in uw abonnementen. |
| [Schakel versleuteling voor Azure Storage-Account](security-center-enable-encryption-for-storage-account.md) | Raadt aan dat u Azure Storage-Service: versleuteling voor gegevens in rust inschakelen. Versleuteling voor opslag-Service (SSE) werkt Hallo door gegevens te coderen wanneer deze wordt geschreven tooAzure opslag en voordat ophalen ontsleutelt. SSE is momenteel alleen beschikbaar voor hello Azure Blob-service en kan worden gebruikt voor blok-blobs, pagina-blobs en toevoeg-blobs. toolearn meer, Zie [Service versleuteling van opslag voor gegevens in rust](../storage/common/storage-service-encryption.md).</br>SSE wordt alleen ondersteund op Resource Manager storage-accounts. Klassieke opslagaccounts worden momenteel niet ondersteund. Zie toounderstand Hallo klassieke en het Resource Manager-implementatiemodel, [Azure-implementatiemodellen](../azure-classic-rm.md). |
| [Beveiligingsproblemen met het besturingssysteem herstellen](security-center-remediate-os-vulnerabilities.md) |Dat u uw besturingssysteemconfiguraties zijn uitgelijnd met de Hallo aanbevolen configuratieregels, raadt bijvoorbeeld staan geen wachtwoorden toobe opgeslagen. |
| [Systeemupdates toepassen](security-center-apply-system-updates.md) |Raadt aan dat u ontbrekende systeembeveiliging en essentiële updates tooVMs implementeert. |
| [Toepassen van een Just-In-Time netwerk toegangsbeheer](security-center-just-in-time.md) | Adviseert toe te passen alleen bij het VM-time-toegang. Hallo alleen in de functie is in preview en beschikbaar is op Hallo standaardcategorie van Security Center. Zie [prijzen](security-center-pricing.md) toolearn meer informatie over Security Center de prijscategorie. |
| [Opnieuw opstarten na systeemupdates](security-center-apply-system-updates.md#reboot-after-system-updates) |Raadt aan dat u een VM toocomplete Hallo proces van het toepassen van systeemupdates opnieuw opgestart. |
| [Eindpuntbeveiliging installeren](security-center-install-endpoint-protection.md) |Raadt het inrichten van antimalware-programma's tooVMs (alleen Windows-VM's). |
| [Endpoint Protection-statusmeldingen oplossen](security-center-resolve-endpoint-protection-health-alerts.md) |Hiermee wordt aanbevolen om Endpoint Protection-fouten op te lossen. |
| [VM-agent inschakelen](security-center-enable-vm-agent.md) |Hiermee schakelt u toosee waarvoor VMs Hallo VM-Agent. Hallo VM-Agent moet worden geïnstalleerd op virtuele machines in de volgorde tooprovision patch scannen basislijn scannen en antimalwareprogramma's. Hallo VM-Agent wordt standaard geïnstalleerd voor virtuele machines die vanuit Azure Marketplace Hallo worden geïmplementeerd. Hallo artikel [VM-Agent en -extensies – deel 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) bevat informatie over hoe tooinstall Hallo VM-Agent. |
| [Schijfversleuteling toepassen](security-center-apply-disk-encryption.md) |Hiermee wordt aanbevolen om de VM-schijven te versleutelen met behulp van Azure Disk Encryption. (Voor VM's van Windows en Linux.) Versleuteling wordt aanbevolen voor zowel hello OS- en gegevensvolumes op de virtuele machine. |
| [Besturingssysteemversie bijwerken](security-center-update-os-version.md) |Raadt aan dat u voor uw Cloudservice toohello meest recente versie beschikbaar voor OS-familie Hallo besturingssysteem (OS) versie bijwerken.  toolearn meer informatie over Cloudservices, Zie Hallo [Cloud Services-overzicht](../cloud-services/cloud-services-choose-me.md). |
| [Beoordeling van beveiligingslekken is niet geïnstalleerd](security-center-vulnerability-assessment-recommendations.md) |Hiermee wordt aanbevolen om een oplossing voor de beoordeling van beveiligingslekken te installeren op de VM. |
| [Beveiligingsproblemen herstellen](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Hiermee kunt u toosee systeem- en beveiligingsproblemen die worden gedetecteerd door Hallo vulnerability assessment oplossing is geïnstalleerd op de virtuele machine. |

## <a name="see-also"></a>Zie ook
toolearn meer informatie over de aanbevelingen die van toepassing zijn tooother Azure brontypen, Zie de volgende Hallo:

* [Beveiligen van uw toepassingen in Azure Security Center](security-center-application-recommendations.md)
* [Beveiligen van uw netwerk in Azure Security Center](security-center-network-recommendations.md)
* [Beveiligen van uw Azure SQL-service in Azure Security Center](security-center-sql-service-recommendations.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
