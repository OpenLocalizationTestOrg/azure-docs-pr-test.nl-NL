---
title: aaaAzure Security Center en Azure Virtual Machines | Microsoft Docs
description: Dit document helpt u toounderstand hoe Azure Security Center u virtuele Machines van Azure kunt beschermen.
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/24/2017
ms.author: yurid
ms.openlocfilehash: d5e80e9341263a57f3100cb032a066f037e913a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines"></a>Azure Security Center en Azure Virtual Machines
[Azure Security Center](https://azure.microsoft.com/services/security-center/) helpt u bij het detecteren, voorkomen van en reageren toothreats. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

In dit artikel wordt gedemonstreerd hoe Security Center u kan helpen uw VM (virtuele machine) van Azure te beveiligen.

## <a name="why-use-security-center"></a>Waarom Security Center gebruiken?
Met Security Center kunt u gegevens van virtuele machines in Azure beveiligen door inzicht te bieden in de beveiligingsinstellingen van de virtuele machine. Wanneer Security Center uw virtuele machines beveiligt, wordt Hallo na mogelijkheden beschikbaar zijn:

* Besturingssysteem (OS) beveiligingsinstellingen Hello aanbevolen configuratieregels
* Updates voor systeembeveiliging en essentiële updates die ontbreken
* Aanbevelingen voor eindpuntbeveiliging
* Validatie voor schijfversleuteling
* Beoordeling en herstel van beveiligingslekken
* Detectie van bedreigingen

Bovendien toohelping uw Azure VM's beveiligen, Security Center biedt ook beveiligingsbewaking en beheer voor Cloud Services, App-Services en virtuele netwerken. 

> [!NOTE]
> Zie [inleiding tooAzure Security Center](security-center-intro.md) toolearn meer informatie over Azure Security Center.
> 
> 

## <a name="prerequisites"></a>Vereisten
de slag met Azure Security Center tooget u moet tooknow en houd rekening met de volgende Hallo:

* U moet een abonnement tooMicrosoft Azure hebben. Zie [Prijzen van Beveiligingscentrum](https://azure.microsoft.com/pricing/details/security-center/) voor meer informatie over de gratis laag en standaardlaag in Security Center.
* Plan uw acceptatie Security Center, Zie [Azure Security Center plannen en de operations guide](security-center-planning-and-operations-guide.md) toolearn meer informatie over overwegingen voor planning en bewerkingen.
* Zie [Azure Security Center frequently asked questions (FAQ)](security-center-faq.md) (Veelgestelde vragen over Azure Security Center) voor informatie over de ondersteuning van besturingssystemen. 

## <a name="set-security-policy"></a>Beveiligingsbeleid instellen
Gegevens verzamelen behoeften toobe ingeschakeld zodat die Azure Security Center kunt verzamelen Hallo informatie die nodig is tooprovide aanbevelingen en waarschuwingen die worden gegenereerd, gebaseerd op Hallo beveiligingsbeleid voor die u configureren. In onderstaande Hallo afbeelding, kunt u zien dat **gegevensverzameling** is ingeschakeld **op**.

Een beveiligingsbeleid bepaalt Hallo set besturingselementen wordt aanbevolen voor resources binnen de opgegeven abonnement of resourcegroep groep Hallo. Voordat u beveiligingsbeleid inschakelt, moet u gegevensverzameling is ingeschakeld, Security Center verzamelt gegevens uit uw virtuele machines in volgorde van tooassess hun beveiligingsstatus aanbevelingen voor beveiliging bieden, en wordt u geïnformeerd toothreats. In Security Center definieert u beleid voor uw Azure-abonnementen of de resourcegroepen op basis van tooyour en van het bedrijf beveiligingsbehoeften Hallo type toepassingen of de vertrouwelijkheid van gegevens in elk abonnement Hallo. 

![Beveiligingsbeleid](./media/security-center-virtual-machine/security-center-virtual-machine-fig1.png)

> [!NOTE]
> meer informatie over elk toolearn **preventiebeleid** beschikbaar, Zie [instellen van beveiligingsbeleid](security-center-policies.md) artikel.
> 
> 

## <a name="manage-security-recommendations"></a>Aanbevelingen voor beveiliging beheren
Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources. Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan. Hallo aanbevelingen helpt u bij Hallo Hallo nodig-besturingselementen configureren.

Na het instellen van een beveiligingsbeleid, analyseert Security Center Hallo beveiligingsstatus van uw resources tooidentify potentiële beveiligingslekken naar voren. Hallo aanbevelingen worden weergegeven in een tabel waarin elke regel staat voor een bepaalde aanbeveling. Hallo in de volgende tabel bevat enkele voorbeelden van aanbevelingen voor virtuele Azure-machines en elk criterium doen als u deze toe te passen. Wanneer u een aanbeveling selecteert, krijgt u informatie die laat zien u hoe tooimplement Hallo aanbeveling in Security Center.

| Aanbeveling | Beschrijving |
| --- | --- |
| [Gegevensverzameling voor abonnementen inschakelen](security-center-enable-data-collection.md) |Raadt aan om te schakelen op het verzamelen van gegevens in het Hallo-beveiligingsbeleid voor elk van uw abonnementen en alle virtuele machines (VM's) in uw abonnementen. |
| [Beveiligingsproblemen met het besturingssysteem herstellen](security-center-remediate-os-vulnerabilities.md) |Dat u uw besturingssysteemconfiguraties zijn uitgelijnd met de Hallo aanbevolen configuratieregels, raadt bijvoorbeeld staan geen wachtwoorden toobe opgeslagen. |
| [Systeemupdates toepassen](security-center-apply-system-updates.md) |Raadt aan dat u ontbrekende systeembeveiliging en essentiële updates tooVMs implementeert. |
| [Opnieuw opstarten na systeemupdates](security-center-apply-system-updates.md#reboot-after-system-updates) |Raadt aan dat u een VM toocomplete Hallo proces van het toepassen van systeemupdates opnieuw opgestart. |
| [Eindpuntbeveiliging installeren](security-center-install-endpoint-protection.md) |Raadt het inrichten van antimalware-programma's tooVMs (alleen Windows-VM's). |
| [Endpoint Protection-statusmeldingen oplossen](security-center-resolve-endpoint-protection-health-alerts.md) |Hiermee wordt aanbevolen om Endpoint Protection-fouten op te lossen. |
| [VM-agent inschakelen](security-center-enable-vm-agent.md) |Hiermee schakelt u toosee waarvoor VMs Hallo VM-Agent. Hallo VM-Agent moet worden geïnstalleerd op virtuele machines in de volgorde tooprovision patch scannen basislijn scannen en antimalwareprogramma's. Hallo VM-Agent wordt standaard geïnstalleerd voor virtuele machines die vanuit Azure Marketplace Hallo worden geïmplementeerd. Hallo artikel [VM-Agent en -extensies – deel 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) bevat informatie over hoe tooinstall Hallo VM-Agent. |
| [Schijfversleuteling toepassen](security-center-apply-disk-encryption.md) |Hiermee wordt aanbevolen om de VM-schijven te versleutelen met behulp van Azure Disk Encryption. (Voor VM's van Windows en Linux.) Versleuteling wordt aanbevolen voor zowel hello OS- en gegevensvolumes op de virtuele machine. |
| [Beoordeling van beveiligingslekken is niet geïnstalleerd](security-center-vulnerability-assessment-recommendations.md) |Hiermee wordt aanbevolen om een oplossing voor de beoordeling van beveiligingslekken te installeren op de VM. |
| [Beveiligingsproblemen herstellen](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Hiermee kunt u toosee systeem- en beveiligingsproblemen die worden gedetecteerd door Hallo vulnerability assessment oplossing is geïnstalleerd op de virtuele machine. |

> [!NOTE]
> toolearn meer informatie over aanbevelingen, Zie [aanbevelingen voor beveiliging beheren](security-center-recommendations.md) artikel.
> 
> 

## <a name="monitor-security-health"></a>Beveiligingsstatus controleren
Nadat u hebt ingeschakeld [beveiligingsbeleid](security-center-policies.md) voor resources van een abonnement, analyseert Security Center Hallo beveiliging van uw resources tooidentify potentiële beveiligingslekken naar voren.  U kunt bekijken Hallo beveiligingsstatus van uw resources samen met eventuele problemen op Hallo **resourcebeveiligingsstatus** blade. Wanneer u klikt op **virtuele machines** in Hallo **beveiliging** tegel status, Hallo **virtuele machines** blade geopend met aanbevelingen voor uw virtuele machines. 

![Beveiligingsstatus](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Beheren en hierop reageren toosecurity waarschuwingen
Security Center automatisch verzamelt, analyseert en integreert logboekgegevens van uw Azure-resources, het Hallo-netwerk en de verbonden partneroplossingen (zoals een firewall en endpoint protection-oplossingen), toodetect Werkelijke dreigingen en fout-positieven te verminderen. Dankzij het gebruik van een diverse aggregatie van [detectiemogelijkheden](security-center-detection-capabilities.md), Security Center is kunnen toogenerate prioriteit beveiligingswaarschuwingen toohelp u snel Hallo probleem onderzoeken en aanbevelingen voor hoe tooremediate mogelijke aanvallen.

![Beveiligingswaarschuwingen](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Selecteer een waarschuwing toolearn beveiliging meer informatie over Hallo gebeurtenis(sen) waarmee geactiveerd Hallo waarschuwing en wat, indien aanwezig, stappen u moet tootake tooremediate een aanval. Beveiligingswaarschuwingen zijn gegroepeerd op [type](security-center-alerts-type.md) en datum.

## <a name="see-also"></a>Zie ook
toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.

