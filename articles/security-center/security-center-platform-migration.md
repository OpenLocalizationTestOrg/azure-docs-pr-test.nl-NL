---
title: Security Center-Platform migratie aaaAzure | Microsoft Docs
description: Dit document wordt uitgelegd op een bepaalde wijzigingen toohello manier Azure Security Center-gegevens worden verzameld.
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 80246b00-bdb8-4bbc-af54-06b7d12acf58
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: yurid
ms.openlocfilehash: 28cb8d85912a3f62941cf113da51070081b5eda2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-platform-migration"></a>Migratie van Azure Security Center-platform

Begin juni 2017 vanaf kan implementeert Azure Security Center belangrijke wijzigingen toohello manier waarop beveiligingsgegevens worden verzameld en opgeslagen.  Deze wijzigingen ontgrendelen nieuwe mogelijkheden, zoals Hallo mogelijkheid tooeasily zoekgegevens voor beveiliging en betere wordt uitgelijnd met andere Azure-beheer en controle van services.

> [!NOTE]
> Hallo platform migratie moet geen invloed op uw productieresources en is geen actie nodig van uw kant.


## <a name="whats-happening-during-this-platform-migration"></a>Wat gebeurt er tijdens deze platformmigratie?

Security Center gebruikt voorheen hello Azure Monitoring Agent toocollect beveiligingsgegevens van uw virtuele machines. Dit omvat informatie over beveiligingsconfiguraties die gebruikte tooidentify beveiligingsproblemen, en beveiligingsgebeurtenissen, de gebruikte toodetect bedreigingen. Deze gegevens werden opgeslagen in uw opslagaccounts in Azure.

Voortaan, dat Security Center gebruikt Hallo Microsoft Monitoring Agent – is dit Hallo dezelfde agent die wordt gebruikt door Hallo Operations Management Suite en Log Analytics-service. Gegevens die worden verzameld van deze agent wordt opgeslagen in een bestaand *logboekanalyse* [werkruimte](../log-analytics/log-analytics-manage-access.md) die zijn gekoppeld aan uw Azure-abonnement of een nieuwe workspace(s), waarbij rekening wordt gehouden account Hallo geolocatie Hallo VM .

## <a name="agent"></a>Agent

Als onderdeel van de overgang Hallo Hallo Microsoft Monitoring Agent (voor [Windows](../log-analytics/log-analytics-windows-agents.md) of [Linux](../log-analytics/log-analytics-linux-agents.md)) is geïnstalleerd op alle Azure Virtual machines uit die momenteel worden gegevens verzameld.  Als de virtuele machine al Hallo Microsoft Monitoring Agent is geïnstalleerd heeft, Hallo Security Center maakt gebruik van de huidige Hallo agent geïnstalleerd.

Voor een bepaalde tijd (doorgaans een paar dagen), wordt beide agents uitgevoerd naast elkaar tooensure een soepele migratie zonder verlies van gegevens. Hiermee schakelt u Microsoft toovalidate die nieuwe gegevens pijplijn Hallo voordat het gebruik van de huidige pipeline Hallo beëindigde operationeel is. Eenmaal geverifieerde hello Azure Monitoring Agent wordt verwijderd uit uw virtuele machines. U hoeft hier niets voor te doen. U ontvangt een e-mailbericht wanneer alle klanten die zijn gemigreerd.
 
Het is niet raadzaam dat u handmatig hello Azure Monitoring Agent tijdens de migratie Hallo verwijderen zoals hiaten in de beveiligingsgegevens kunnen leiden. Neem contact op met [Microsoft Customer Service and Support](https://support.microsoft.com/contactus/) als u meer hulp nodig hebt. 

Microsoft Monitoring Agent voor Windows Hello gebruiken TCP-poort 443, lezen vereist [Azure Security Center Troubleshooting Guide](security-center-troubleshooting-guide.md) voor meer informatie.


> [!NOTE] 
> Omdat Hallo Microsoft Monitoring Agent kan worden gebruikt door andere beheertaken voor Azure en bewaking van services Hallo-agent niet automatisch verwijderd wanneer u gegevens verzamelen uitschakelen in Security Center. U kunt echter handmatig Hallo-agent verwijderen indien nodig.

## <a name="workspace"></a>Werkruimte

Zoals eerder aangegeven, gegevens verzamelen van Microsoft Monitoring Agent (namens Security Center) worden opgeslagen in een bestaande logboekanalyse Hallo workspace(s) die is gekoppeld aan uw Azure-abonnement of een nieuwe workspace(s), waarbij rekening wordt gehouden account Hallo geolocatie Hallo VM.

In hello Azure-portal, kunt u een lijst met uw Log Analytics-werkruimten, inclusief alle gemaakt door Security Center toosee bladeren. Een gerelateerde resourcegroep wordt gemaakt voor nieuwe werkruimten. Werkruimten en resourcegroepen volgen beide deze naamconventie:

- Werkruimte: *Standaardwerkruimte-[abonnement-ID]-[geo]*
- Resourcegroep: *Standaardresoucegroep-[geo]* 
 
Voor werkruimten die zijn gemaakt door Security Center worden gegevens 30 dagen bewaard. Voor bestaande werkruimten is bewaarperiode gebaseerd op Hallo werkruimte prijscategorie.

> [!NOTE]
> Gegevens die eerder door Security Center werden verzameld, blijven aanwezig in uw opslagaccounts. Nadat het Hallo-migratie is voltooid, kunt u deze accounts voor opslag verwijderen.

### <a name="oms-security-solution"></a>OMS-beveiligingsoplossing 

Voor bestaande klanten die geen OMS-beveiligingsoplossing hebben geïnstalleerd, installeert Microsoft deze in hun werkruimte. De oplossing is echter alleen gericht op virtuele machines van Azure. U moet deze oplossing niet verwijderen, omdat er geen automatisch herstel is als dit wordt gedaan via de OMS-beheerconsole.


## <a name="other-updates"></a>Andere Updates

We zijn een aantal extra nauwelijks zijn bijgewerkt rolt in combinatie met Hallo platform migratie:

- Aanvullende versies van het besturingssysteem worden ondersteund. Overzicht van Hallo [hier](security-center-faq.md#virtual-machines).
- Hallo-lijst van OS beveiligingsproblemen zal worden uitgebreid. Overzicht van Hallo [hier](https://gallery.technet.microsoft.com/Azure-Security-Center-a789e335).
- [Prijzen](https://azure.microsoft.com/pricing/details/security-center/) zijn pro rato per uur (voorheen was dit per dag). Voor sommige klanten zal dit leiden tot kostenbesparingen.
- Verzamelen van gegevens wordt vereist en wordt automatisch ingeschakeld voor klanten op Hallo standaardcategorie prijzen.
- Azure Security Center start met het detecteren van antimalware-oplossingen die niet zijn geïmplementeerd via Azure-extensies. Detectie van Symantec Endpoint Protection en Defender voor Windows 2016 zal als eerste beschikbaar zijn.
- Beleid ter preventie en meldingen worden alleen geconfigureerd op Hallo *abonnement* niveau, maar de prijzen kan nog steeds worden ingesteld op Hallo *resourcegroep* niveau

