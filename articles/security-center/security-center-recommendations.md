---
title: beveiligingsaanbevelingen voor de aaaManaging in Azure Security Center | Microsoft Docs
description: Dit document begeleidt u bij hoe aanbevelingen in Azure Security Center helpen u bij het beveiligen van uw Azure-resources en blijven in overeenstemming met het beveiligingsbeleid.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Aanbevelingen voor beveiliging in Azure Security Center beheren
Dit document leert u hoe u toouse aanbevelingen in Azure Security Center toohelp beschermt uw Azure-resources.

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit document is niet een stapsgewijze handleiding.
>
>

## <a name="what-are-security-recommendations"></a>Wat zijn aanbevelingen voor beveiliging?
Security Center analyseert periodiek Hallo beveiligingsstatus van uw Azure-resources. Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan. Hallo aanbevelingen helpt u bij Hallo Hallo nodig-besturingselementen configureren.

## <a name="implementing-security-recommendations"></a>Implementatie van aanbevelingen voor beveiliging
### <a name="set-recommendations"></a>Set-aanbevelingen
In [beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md), u informatie over het:

* Beveiligingsbeleid configureren.
* Schakel gegevensverzameling.
* Kies welke toosee aanbevelingen als onderdeel van uw beveiligingsbeleid.

Huidige beleid aanbevelingen center rond systeemupdates, basislijnregels, antimalwareprogramma's [netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md) op subnetten en netwerkinterfaces, SQL database auditing transparent data encryption voor SQL-database en web application firewalls.  [Beveiligingsbeleid instellen](security-center-policies.md) bevat een beschrijving van elke optie aanbeveling.

### <a name="monitor-recommendations"></a>Monitor aanbevelingen
Na het instellen van een beveiligingsbeleid, analyseert Security Center Hallo beveiligingsstatus van uw resources tooidentify potentiële beveiligingslekken naar voren. Hallo **aanbevelingen** tegel op Hallo **Security Center** blade laat u weten Hallo kunt u het totale aantal geïdentificeerd door Security Center aanbevelingen.

![Aanbevelingen tegel][1]

toosee hello details van elke aanbeveling:

Selecteer Hallo **aanbevelingen tegel** op Hallo **Security Center** blade. Hallo **aanbevelingen** blade wordt geopend.

Hallo aanbevelingen worden weergegeven in een tabel waarin elke regel staat voor een bepaalde aanbeveling. Hallo-kolommen van deze tabel zijn:

* **BESCHRIJVING**: uitgelegd Hallo aanbeveling en wat er gedaan tooaddress toobe moet het.
* **RESOURCE**: geeft een lijst van Hallo resources toowhich deze aanbeveling is van toepassing.
* **STATUS**: Beschrijving van de huidige status Hallo Hallo aanbeveling:
  * **Open**: Hallo aanbeveling nog niet is opgelost.
  * **Bezig**: Hallo aanbeveling wordt momenteel toegepast toohello resources en de door u is geen actie vereist.
  * **Opgelost**: Hallo aanbeveling is al voltooid (in dit geval Hallo-regel is lichter gekleurd weergegeven).
* **ERNST**: wordt Hallo ernst van deze bepaalde aanbeveling beschreven:
  * **Hoge**: een beveiligingsprobleem bestaat voor een belangrijke resource (zoals een toepassing, een virtuele machine of een netwerkbeveiligingsgroep) en aandacht vereist.
  * **Gemiddeld**: een beveiligingsprobleem bestaat en niet-kritieke of extra stappen zijn vereist tooeliminate of toocomplete een proces.
  * **Lage**: een beveiligingslek dat moet worden opgelost, maar geen onmiddellijke aandacht vereist. (Standaard lage aanbevelingen worden niet weergegeven, maar u kunt filteren op aanbevelingen als u wilt dat toosee ze.)

Gebruik Hallo onderstaande tabel als een verwijzing toohelp erkent u Hallo beschikbaar aanbevelingen en elke eigenschap als u deze toe te passen.

> [!NOTE]
> Gewenste toounderstand hello [klassieke en Resource Manager-implementatiemodel](../azure-classic-rm.md) voor Azure-resources.
>
>

| Aanbeveling | Beschrijving |
| --- | --- |
| [Gegevensverzameling voor abonnementen inschakelen](security-center-enable-data-collection.md) |Raadt aan om te schakelen op het verzamelen van gegevens in het Hallo-beveiligingsbeleid voor elk van uw abonnementen en alle virtuele machines (VM's) in uw abonnementen. |
| [Beveiligingsproblemen met het besturingssysteem herstellen](security-center-remediate-os-vulnerabilities.md) |Raadt aan dat u uw besturingssysteemconfiguraties zijn afgestemd op Hallo aanbevolen configuratieregels, bijvoorbeeld, niet toestaan dat wachtwoorden toobe opgeslagen. |
| [Systeemupdates toepassen](security-center-apply-system-updates.md) |Raadt aan dat u ontbrekende systeembeveiliging en essentiële updates tooVMs implementeert. |
| [Toepassen van een Just-In-Time netwerk toegangsbeheer](security-center-just-in-time.md) | Adviseert toe te passen alleen bij het VM-time-toegang. Hallo alleen in de functie is in preview en beschikbaar is op Hallo standaardcategorie van Security Center. Zie [prijzen](security-center-pricing.md) toolearn meer informatie over Security Center de prijscategorie. |
| [Opnieuw opstarten na systeemupdates](security-center-apply-system-updates.md#reboot-after-system-updates) |Raadt aan dat u een VM toocomplete Hallo proces van het toepassen van systeemupdates opnieuw opgestart. |
| [Een firewall voor webtoepassingen toevoegen](security-center-add-web-application-firewall.md) |Raadt aan dat u een web application firewall (WAF) voor web-eindpunten implementeert. Een WAF aanbeveling wordt voor een openbare internetgerichte IP (exemplaar niveau IP- of Load Balanced IP) met een gekoppelde netwerkbeveiligingsgroep met poorten voor inkomend web openen (80,443) weergegeven. </br>Security Center raadt aan dat u een WAF toohelp inrichten bescherming tegen aanvallen die gericht is op uw webtoepassingen op virtuele machines en op App Service-omgeving. Een as-omgeving (App Service omgeving) is een [Premium](https://azure.microsoft.com/pricing/details/app-service/) service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het veilig uitvoeren van Azure App Service-apps. toolearn meer informatie over het as-omgeving, Zie Hallo [documentatie van App Service-omgeving](../app-service/app-service-app-service-environments-readme.md).</br>U kunt meerdere webtoepassingen in Security Center beveiligen door deze toepassingen tooyour bestaande WAF implementaties toe te voegen. |
| [Toepassingsbeveiliging voltooien](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello configuratie van een WAF, verkeer moet omgeleide toohello WAF toestel. Na deze aanbeveling is Hallo benodigde installatiebestanden wijzigingen voltooid. |
| [Een firewall van de volgende generatie toevoegen](security-center-add-next-generation-firewall.md) |Raadt aan dat u, een volgende generatie Firewall (NGFW) van een Microsoft-partner tooincrease uw beveiligingsinstellingen toevoegt. |
| [Verkeer alleen via NGFW sturen](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Raadt aan dat u configureert (NSG) netwerkbeveiligingsgroepen die binnenkomend verkeer tooyour VM via uw NGFW afdwingen. |
| [Eindpuntbeveiliging installeren](security-center-install-endpoint-protection.md) |Raadt het inrichten van antimalware-programma's tooVMs (alleen Windows-VM's). |
| [Endpoint Protection-statusmeldingen oplossen](security-center-resolve-endpoint-protection-health-alerts.md) |Hiermee wordt aanbevolen om Endpoint Protection-fouten op te lossen. |
| [Netwerkbeveiligingsgroepen op subnetten of virtuele machines inschakelen](security-center-enable-network-security-groups.md) |Raadt het nsg's op subnetten of VM's in te schakelen. |
| [Toegang tot en met een Internetgericht eindpunt beperken](security-center-restrict-access-through-internet-facing-endpoints.md) |Raadt aan dat u regels voor binnenkomend verkeer voor het nsg's configureren. |
| [Controle en detectie van bedreigingen op SQL-servers inschakelen](security-center-enable-auditing-on-sql-servers.md) |Raadt aan dat u de controle en detectie van bedreigingen voor Azure SQL-servers inschakelen. (Alleen voor azure SQL-service. Bevat geen SQL uitgevoerd op uw virtuele machines.) |
| [Controle en detectie van bedreigingen op SQL-databases inschakelen](security-center-enable-auditing-on-sql-databases.md) |Raadt aan dat u de controle en detectie van bedreigingen voor Azure SQL-databases inschakelen. (Alleen voor azure SQL-service. Bevat geen SQL uitgevoerd op uw virtuele machines.) |
| [Transparante gegevensversleuteling inschakelt op de SQL-databases](security-center-enable-transparent-data-encryption.md) |Raadt aan om versleuteling voor SQL-databases in te schakelen. (Alleen azure SQL-service). |
| [VM-agent inschakelen](security-center-enable-vm-agent.md) |Hiermee schakelt u toosee waarvoor VMs Hallo VM-Agent. Hallo VM-Agent moet worden geïnstalleerd op virtuele machines tooprovision patch scannen basislijn scannen en antimalwareprogramma's. Hallo VM-Agent wordt standaard geïnstalleerd voor virtuele machines die vanuit Azure Marketplace Hallo worden geïmplementeerd. Hallo artikel [VM-Agent en -extensies – deel 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) bevat informatie over hoe tooinstall Hallo VM-Agent. |
| [Schijfversleuteling toepassen](security-center-apply-disk-encryption.md) |Hiermee wordt aanbevolen om de VM-schijven te versleutelen met behulp van Azure Disk Encryption. (Voor VM's van Windows en Linux.) Versleuteling wordt aanbevolen voor zowel hello OS- en gegevensvolumes op de virtuele machine. |
| [Contactgegevens voor beveiliging verstrekken](security-center-provide-security-contact-details.md) |Raadt u beveiliging bieden de contactgegevens voor elk van uw abonnementen. Contactgegevens is een e-mailadres en telefoonnummer getal. Hallo informatie is gebruikte toocontact u als onze beveiligingsteam vindt dat uw resources worden getroffen. |
| [Besturingssysteemversie bijwerken](security-center-update-os-version.md) |Raadt aan dat u voor uw Cloudservice toohello meest recente versie beschikbaar voor OS-familie Hallo besturingssysteem (OS) versie bijwerken.  toolearn meer informatie over Cloudservices, Zie Hallo [Cloud Services-overzicht](../cloud-services/cloud-services-choose-me.md). |
| [Beoordeling van beveiligingslekken is niet geïnstalleerd](security-center-vulnerability-assessment-recommendations.md) |Hiermee wordt aanbevolen om een oplossing voor de beoordeling van beveiligingslekken te installeren op de VM. |
| [Beveiligingsproblemen herstellen](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Hiermee kunt u toosee systeem- en beveiligingsproblemen die worden gedetecteerd door Hallo vulnerability assessment oplossing is geïnstalleerd op de virtuele machine. |
| [Schakel versleuteling voor Azure Storage-Account](security-center-enable-encryption-for-storage-account.md) | Raadt aan dat u Azure Storage-Service: versleuteling voor gegevens in rust inschakelen. Versleuteling voor opslag-Service (SSE) werkt Hallo door gegevens te coderen wanneer deze wordt geschreven tooAzure opslag en voordat ophalen ontsleutelt. SSE is momenteel alleen beschikbaar voor hello Azure Blob-service en kan worden gebruikt voor blok-blobs, pagina-blobs en toevoeg-blobs. toolearn meer, Zie [Service versleuteling van opslag voor gegevens in rust](../storage/common/storage-service-encryption.md).</br>SSE wordt alleen ondersteund op Resource Manager storage-accounts. |

U kunt filteren en aanbevelingen negeren.

1. Selecteer **Filter** op Hallo **aanbevelingen** blade. Hallo **Filter** blade wordt geopend en u Hallo ernst en status waarden voor toosee selecteren.

    ![Filter aanbevelingen][2]
2. Als u vaststelt dat een aanbeveling is niet van toepassing, kunt u Hallo aanbeveling negeren en deze vervolgens uit uw weergave filteren. Er zijn twee manieren toodismiss een aanbeveling. Een manier is tooright klikt u op een item en selecteer vervolgens **sluiten**. Hallo andere toohover boven een item, klikt u op Hallo drie punten die worden weergegeven toohello rechts en selecteer vervolgens **sluiten**. U kunt ontslagen aanbevelingen weergeven door te klikken op **Filter**, en vervolgens te selecteren **genegeerd**.

    ![Aanbeveling negeren][3]

### <a name="apply-recommendations"></a>Toepassen van aanbevelingen
Bekijk bepalen alle aanbevelingen welke u moet eerst toepassen. U wordt aangeraden prioriteitsniveau hello te gebruiken, zoals Hallo belangrijkste parameter tooevaluate welke aanbevelingen eerst moeten worden toegepast.

Selecteer een aanbeveling in Hallo tabel van de bovenstaande aanbevelingen en doorlopen als een voorbeeld van hoe tooapply een aanbeveling.

## <a name="next-steps"></a>Volgende stappen
In dit document, kunt u aanbevelingen in Security Center geïntroduceerd toosecurity was. toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) : meer informatie hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
