---
title: Security Center Troubleshooting Guide aaaAzure | Microsoft Docs
description: Dit document helpt tootroubleshoot problemen in Azure Security Center.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Handleiding voor het oplossen van problemen met Azure Security Center
Deze gids is bedoeld voor IT-professionals (IT), gegevensbeveiligingsanalisten en cloudbeheerders die willen Azure Security Center gebruikt en moeten dat problemen met betrekking tot tootroubleshoot Security Center.

>[!NOTE] 
>Begin juni 2017 vanaf kan Security Center toocollect en store-gegevens van Microsoft Monitoring Agent Hallo gebruikt. Zie [Azure Security Center-Platform migratie](security-center-platform-migration.md) toolearn meer. Hallo-informatie in dit artikel beschrijft Security Center functionaliteit na de overgang toohello Microsoft Monitoring Agent.
>

## <a name="troubleshooting-guide"></a>Handleiding voor het oplossen van problemen
Deze handleiding wordt uitgelegd hoe tootroubleshoot Security Center gerelateerde problemen. Hallo probleemoplossing in Security Center uitgevoerd en de meeste vindt plaats door eerst te zoeken naar Hallo [controlelogboek](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) records voor Hallo onderdeel is mislukt. Met controlelogboeken kunt u het volgende bepalen:

* Welke bewerkingen er hebben plaatsgevonden
* Wie Hallo-bewerking gestart
* Wanneer Hallo-bewerking heeft plaatsgevonden
* Hallo-status van Hallo-bewerking
* Hallo-waarden van andere eigenschappen die u kunnen helpen onderzoek Hallo-bewerking

Hallo-controlelogboek bevat alle schrijfbewerkingen (PUT, POST, verwijderen) uitgevoerd op uw resources, maar geen leesbewerkingen (GET bevat).

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
Security Center gebruikt Hallo Microsoft Monitoring Agent – dit Hallo dezelfde agent die wordt gebruikt door Hallo Operations Management Suite en Log Analytics-service – toocollect beveiligingsgegevens van uw virtuele machines in Azure is. Nadat gegevensverzameling is ingeschakeld en Hallo agent correct is geïnstalleerd in de doelmachine hello, moet Hallo procedure hieronder worden uitgevoerd:

* HealthService.exe

Als u Hallo services management console (services.msc) opent, ziet u ook Hallo Microsoft Monitoring Agent-service wordt uitgevoerd zoals hieronder wordt weergegeven:

![Services](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

welke versie van het Hallo-agent die u hebt, toosee openen **Taakbeheer**, in Hallo **processen** tabblad vinden Hallo **Microsoft Monitoring Agent-Service**, met de rechtermuisknop op het en Klik op **eigenschappen**. In Hallo **Details** tabblad, kijkt u Hallo bestandsversie zoals hieronder wordt weergegeven:

![File](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Installatiescenario's voor Microsoft Monitoring Agent
Er zijn twee installatiescenario's die verschillende resultaten opleveren kunnen bij het Hallo Microsoft Monitoring Agent installeren op uw computer. Hallo ondersteund scenario's:

* **Agent die automatisch wordt geïnstalleerd door Security Center**: in dit scenario kunt u zich kunt tooview Hallo waarschuwingen in de locaties, Security Center en logboek zoeken. U ontvangt e-mailmeldingen toohello e-mailadres dat is geconfigureerd in het Hallo-beveiligingsbeleid voor Hallo abonnement Hallo resource bij hoort.
.
* **De agent handmatig is geïnstalleerd op een virtuele machine zich in Azure**: in dit scenario, als u agents hebt gedownload en geïnstalleerd handmatig voorafgaande tooFebruary 2017, kunt u waarschuwingen van de kunnen tooview Hallo in Hallo Security Center portal alleen als u filteren op Hallo Hallo-werkruimte abonnement behoort. In geval filter op Hallo abonnement Hallo resource van jou is, niet kunnen toosee waarschuwingen. U ontvangt e-mailmeldingen toohello e-mailadres dat is geconfigureerd in het Hallo-beveiligingsbeleid voor Hallo abonnement Hallo werkruimte tot behoort.

>[!NOTE]
> tooavoid hello gedrag uitgelegd in Hallo tweede, zorg ervoor dat u de nieuwste versie Hallo van Hallo agent downloaden.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>Problemen oplossen met de netwerkvereisten voor de Monitoring Agent
Voor agents tooconnect tooand registreren met Security Center, moeten ze toegang toonetwork bronnen, met inbegrip van poortnummers Hallo en domein-URL's hebben.

- Proxy-servers moet u tooensure die Hallo juiste proxyserver resources zijn geconfigureerd in instellingen voor de agent. Lees dit artikel voor meer informatie over [hoe toochange proxy-instellingen Hallo](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).
- Voor firewalls die toegang toohello Internet beperken, moet u tooconfigure uw firewall toopermit toegang tooOMS. De agent-instellingen hoeven niet te worden aangepast.

Hallo volgende tabel ziet u bronnen die nodig zijn voor communicatie.

| Agentresource | Poorten | HTTPS-controle overslaan |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Ja |
| *.oms.opinsights.azure.com | 443 | Ja |
| *.blob.core.windows.net | 443 | Ja |
| *.azure-automation.net | 443 | Ja |

Als u voorbereiden op problemen met Hallo-agent ondervindt, moet u ervoor dat tooread Hallo artikel [hoe tootroubleshoot Operations Management Suite voorbereiden problemen](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>Oplossen van problemen met niet goed werkende eindpuntbeveiliging

Hallo guest-agent is Hallo bovenliggende proces van alles Hallo [Microsoft Antimalware](../security/azure-security-antimalware.md) extensie heeft. Wanneer Hallo guest agent mislukt mislukt Hallo Microsoft Antimalware die wordt uitgevoerd als een onderliggend proces van Hallo guest-agent ook.  In scenario's zoals die wordt aanbevolen tooverify Hallo de volgende opties:

- Als Hallo doel VM een aangepaste installatiekopie is en Hallo maker van Hallo VM nooit guest-agent geïnstalleerd.
- Als Hallo doel een Linux-VM in plaats van een virtuele machine van Windows hello Windows-versie van Hallo antimalware extensie vervolgens te installeren op een Linux-VM is mislukt. Hallo Linux Gast-agent heeft bepaalde vereisten in termen van de versie van het besturingssysteem en de vereiste pakketten en niet aan deze vereisten wordt voldaan Hallo VM-agent werkt niet als er een. 
- Als Hallo VM is gemaakt met een oude versie van de gastagent. Als emulator was, moet u zich bewust zijn dat een aantal oude agents kunnen niet automatisch bijwerken zelf toohello nieuwere versie en kan dit probleem toothis leiden. Gebruik altijd Hallo meest recente versie van de gastagent als het maken van uw eigen installatiekopieën.
- Sommige beheersoftware van derden mogelijk uitschakelen Hallo guest-agent of locaties voor toegang tot toocertain bestand blokkeren. Als u van derden geïnstalleerd op de virtuele machine hebt, zorg er dan voor dat die Hallo-agent op de uitsluitingslijst Hallo is.
- Bepaalde firewall-instellingen of een Netwerkbeveiligingsgroep (NSG) blokkeren netwerkverkeer tooand van gastagent.
- Een toegangsbeheerlijst (ACL) blokkeert mogelijk de toegang tot de schijf.
- Onvoldoende schijfruimte blokkeren Hallo guest-agent niet goed werken. 

Standaard Hallo Microsoft Antimalware-gebruikersinterface is uitgeschakeld, het lezen van [inschakelen van Microsoft Antimalware-gebruikersinterface op VM's na implementatie van Azure Resource Manager](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) voor meer informatie over het tooenable deze als u nodig hebt.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Het oplossen van problemen bij het laden van Hallo-dashboard

Als u bij het laden van Hallo Security Center-dashboard problemen, zorg ervoor dat de gebruiker Hallo registreert Hallo abonnement tooSecurity Center (dat wil zeggen Hallo eerste gebruiker die Security Center geopend met Hallo abonnement) en Hallo-gebruiker die u wilt tooturn op verzamelen van gegevens moet *eigenaar* of *Inzender* op Hallo-abonnement. Vanaf dat moment op ook gebruikers met *lezer* op Hallo abonnement Hallo dashboard/waarschuwingen/aanbeveling, beleid kunt bekijken.

## <a name="contacting-microsoft-support"></a>Contact opnemen met Microsoft-ondersteuning
Sommige problemen kunnen worden geïdentificeerd met Hallo richtlijnen in dit artikel, anderen u ook vindt beschreven op Hallo Security Center openbare [Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter). Als u aanvullende hulp nodig hebt om bepaalde problemen op te lossen, kunt u via **Azure Portal** een nieuwe ondersteuningsaanvraag openen. Dit doet u als volgt: 

![Microsoft-ondersteuning](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>Zie ook
In dit document, u leert hoe tooconfigure beveiligingsbeleid in Azure Security Center. toolearn meer informatie over Azure Security Center Hallo ziet:

* [Azure Security Center Planning- en Bedieningsgids](security-center-planning-and-operations-guide.md) : meer informatie hoe tooplan en Hallo ontwerpoverwegingen tooadopt Azure Security Center begrijpen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) : meer informatie over hoe toomonitor Hallo status van uw Azure-resources
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen
* [Partneroplossingen bewaken met Azure Security Center](security-center-partner-solutions.md) : meer informatie over hoe toomonitor gezondheidsstatus van uw partneroplossingen Hallo.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service
* [Azure-beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/): lees blogberichten over de beveiliging en naleving van Azure

