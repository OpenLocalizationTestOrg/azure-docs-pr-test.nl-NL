---
title: aaaIntroduction tooAzure Advisor | Microsoft Docs
description: Gebruik Azure Advisor toooptimize uw Azure-implementaties.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 5d796fc06366221efdb6f1bda39ab3fb676abfd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-advisor"></a>Inleiding tooAzure Advisor

Meer informatie over Azure Advisor en de belangrijkste mogelijkheden en antwoorden toofrequently vragen ophalen.

## <a name="what-is-advisor"></a>Wat is Advisor?
Advisor is een persoonlijke cloud-consultant die u helpt volgen best practices toooptimize uw Azure-implementaties. Het analyseert uw resourceconfiguratie en de telemetrie van de informatie over het gebruik en vervolgens raadt oplossingen die u kunnen helpen verbeteren Hallo kosteneffectiviteit, prestaties, beschikbaarheid en beveiliging van uw Azure-resources.

Met Advisor, kunt u het volgende doen:
* Proactieve, bruikbare ophalen en gepersonaliseerde aanbevolen procedures. 
* Hallo prestaties, beveiliging en hoge beschikbaarheid van uw resources verbeteren bij het bepalen van verkoopkansen tooreduce uw algehele Azure hoeven te besteden aan.
* Aanbevelingen met voorgestelde acties inline worden opgehaald.

U kunt Advisor benaderen via Hallo [Azure-portal](https://aka.ms/azureadvisordashboard). Meld u aan toohello [portal](https://portal.azure.com), selecteer **Bladeren**, en schuif vervolgens te**Azure Advisor**. Hallo Advisor dashboard toont de persoonlijke aanbevelingen voor een geselecteerde abonnement. 

Hallo aanbevelingen worden onderverdeeld in vier categorieën: 

* **Hoge beschikbaarheid**: tooensure en Hallo continuïteit van uw bedrijfskritieke toepassingen te verbeteren. Zie voor meer informatie [aanbevelingen voor hoge beschikbaarheid van Advisor](advisor-high-availability-recommendations.md).

* **Beveiliging**: toodetect bedreigingen en zwakke plekken die toosecurity schendingen kunnen leiden. Zie voor meer informatie [Advisor beveiligingsaanbevelingen](advisor-security-recommendations.md).

* **Prestaties**: tooimprove Hallo snelheid van uw toepassingen. Zie voor meer informatie [Advisor prestaties aanbevelingen](advisor-performance-recommendations.md).

* **Kosten**: toooptimize en reduceren uw algehele Azure hoeven te besteden aan. Zie voor meer informatie [aanbevelingen van Advisor kosten](advisor-cost-recommendations.md).

  ![Advisor aanbeveling typen](./media/advisor-overview/advisor-all-tab-examples.png)

> [!NOTE]
> tooaccess aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor. Een abonnement is geregistreerd als een *abonnement eigenaar* gestart Hallo dashboard en klikt op Hallo van Advisor **aanbevelingen krijgen** knop. Dit is een *eenmalige bewerking*. Nadat het Hallo-abonnement is geregistreerd, kunt u Advisor aanbevelingen als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, een resourcegroep of een bepaalde resource.

U kunt klikken op een aanbeveling toolearn meer informatie. U kunt ook meer informatie over acties tootake profiteren van de gelegenheid uitvoeren of een probleem oplost. 

Advisor biedt aanbevelingen met inline acties of documentatie koppelingen. Te klikken op een inline-actie doorloopt u via een tooimplement 'begeleide gebruiker reis' deze. Te klikken op een koppeling documentatie verwijst toodocumentation waarin wordt beschreven hoe toomanually Hallo actie implementeren. 

Advisor updates aanbevelingen per uur. Als een aanbeveling tootake directe actie dat u niet wilt, kunt u deze uitstellen voor een opgegeven periode of genegeerd. 

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="how-do-i-access-advisor"></a>Hoe krijg ik toegang tot Advisor?
U kunt Advisor benaderen via Hallo [Azure-portal](https://aka.ms/azureadvisordashboard). Meld u aan toohello [portal](https://portal.azure.com), selecteer **Bladeren**, en schuif vervolgens te**Azure Advisor**. Hallo Advisor dashboard toont de persoonlijke aanbevelingen voor een geselecteerde abonnement. 

U kunt ook aanbevelingen van Advisor weergeven via de resourceblade van Hallo virtuele machine. Kies de virtuele machine en schuif vervolgens tooAdvisor aanbevelingen in Hallo-menu. 

### <a name="what-permissions-do-i-need-tooaccess-advisor"></a>Wat machtigingen doen ik tooaccess Advisor nodig?

tooaccess aanbevelingen Advisor te ontvangen, moet u eerst *registreren van uw abonnement* met Advisor. Een abonnement is geregistreerd als een *abonnement eigenaar* gestart Hallo dashboard en klikt op Hallo van Advisor **aanbevelingen krijgen** knop. Dit is een *eenmalige bewerking*. Nadat het Hallo-abonnement is geregistreerd, kunt u Advisor aanbevelingen als openen *eigenaar*, *Inzender*, of *lezer* voor een abonnement, een resourcegroep of een bepaalde resource.

### <a name="how-often-are-advisor-recommendations-updated"></a>Hoe vaak worden aanbevelingen van Advisor bijgewerkt?

Advisor aanbevelingen worden elk uur bijgewerkt.

### <a name="what-resources-does-advisor-provide-recommendations-for"></a>Welke bronnen biedt Advisor aanbevelingen voor?

Advisor bevat aanbevelingen voor virtuele machines, beschikbaarheidssets Toepassingsgateways, App-Services, SQL-servers, SQL-databases en Redis-Cache.

### <a name="can-i-snooze-or-dismiss-a-recommendation"></a>Kan ik uitstellen of een aanbeveling negeren?

toosnooze of een aanbeveling negeren, klikt u op Hallo **uitstellen** knop of koppeling. U kunt opgeven dat een tijd uitstellen periode of selecteer **nooit** toodismiss Hallo aanbeveling.

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over de aanbevelingen van Advisor, Zie:

* [Aan de slag met Advisor](advisor-get-started.md)
* [Hoge beschikbaarheid aanbevelingen Advisor te ontvangen](advisor-high-availability-recommendations.md)
* [Aanbevelingen voor beveiliging van Advisor](advisor-security-recommendations.md)
* [Aanbevelingen van Advisor-prestaties](advisor-performance-recommendations.md)
* [Advisor kosten aanbevelingen](advisor-cost-recommendations.md)
