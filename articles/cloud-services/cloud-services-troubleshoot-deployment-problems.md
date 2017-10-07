---
title: problemen met cloud service-implementatie aaaTroubleshoot | Microsoft Docs
description: Er zijn enkele veelvoorkomende problemen die u ondervindt mogelijk bij het implementeren van een cloud service tooAzure. Dit artikel bevat toosome van deze oplossingen.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Problemen met cloud service-implementatie oplossen
Wanneer u een tooAzure cloud service application-pakket implementeert, kunt u informatie over de implementatie van Hallo van Hallo **eigenschappen** deelvenster in hello Azure-portal. Hallo details kunt u in dit deelvenster toohelp u problemen met de cloudservice hello en u kunt deze informatie tooAzure ondersteuning bieden bij het openen van een nieuwe ondersteuningsaanvraag.

U vindt Hallo **eigenschappen** deelvenster als volgt:

* In Azure-portal hello, klik op Hallo-implementatie van de cloudservice, **alle instellingen**, en klik vervolgens op **eigenschappen**.
* In klassieke Azure-portal hello, klik op Hallo-implementatie van de cloudservice, **DASHBOARD**, dat zich bevindt op Hallo rechterbenedenhoek van de pagina hello (onder **snelle weergave**). Let erop dat er geen label 'Eigenschappen' aanwezig op dit deelvenster is.

> [!NOTE]
> U kunt inhoud Hallo Hallo kopiëren **eigenschappen** deelvenster toohello Klembord door te klikken op Hallo-pictogram in Hallo rechterbovenhoek Hallo deelvenster.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Probleem: ik geen toegang tot mijn website, maar mijn implementatie is gestart en alle rolinstanties zijn gereed
Hallo-website-URL koppeling wordt weergegeven in de portal Hallo omvat geen Hallo-poort. Hallo-standaardpoort voor websites is 80. Als uw toepassing geconfigureerde toorun in een andere poort, moet u Hallo juiste poort nummer toohello URL toevoegen bij het openen van Hallo-website.

1. Klik in hello Azure-portal, op Hallo-implementatie van de cloudservice.
2. In Hallo **eigenschappen** deelvenster van de Azure-portal Hallo Hallo poorten voor rolinstanties Hallo controleren (onder **invoer eindpunten**).
3. Als het niet is Hallo poort 80, Hallo juiste poort waarde toohello URL toevoegen wanneer u toegang Hallo-toepassing tot. toospecify een niet-standaardpoort Typ Hallo-URL, gevolgd door een dubbele punt (:), gevolgd door Hallo poortnummer, zonder spaties.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Probleem: Mijn rolinstanties gerecycled zonder mij doen
Service herstel gebeurt automatisch wanneer Azure knooppunten probleem wordt gedetecteerd en wordt daarom rol exemplaren toonew knooppunten verplaatst. Wanneer dit gebeurt, ziet u mogelijk uw rolinstanties automatisch worden gerecycled. toofind als service herstel opgetreden:

1. Klik in hello Azure-portal, op Hallo-implementatie van de cloudservice.
2. In Hallo **eigenschappen** deelvenster Hallo Azure-portal Hallo informatie controleren en bepalen of herstel van de service opgetreden tijdens het Hallo-tijd die u Hallo rollen recyclen waargenomen.

Functies wordt ook ongeveer recycle één keer per maand tijdens host-OS en guest-OS-updates.  
Zie voor meer informatie Hallo blogbericht [rol exemplaar opnieuw wordt opgestart vanwege tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Probleem: die ik kan geen VIP's wisselen doen en een foutbericht ontvangt
Geen VIP's wisselen is niet toegestaan als een implementatie-update uitgevoerd wordt. Implementatie-updates automatisch kunnen worden uitgevoerd wanneer:

* Een nieuwe gastbesturingssysteem beschikbaar is en u zijn geconfigureerd voor automatische updates.
* Service herstel optreedt.

toofind uit verhindert als een automatische update dat u geen VIP's wisselen doen:

1. Klik in hello Azure-portal, op Hallo-implementatie van de cloudservice.
2. In Hallo **eigenschappen** deelvenster Hallo Azure-portal bekijkt hello waarde van **Status**. Als het **gereed**, controleert u **laatste bewerking** toosee als een onlangs heeft plaatsgevonden waardoor mogelijk Hallo VIP wisselen.
3. Herhaal stap 1 en 2 voor Hallo productie-implementatie.
4. Als u een automatische update wordt uitgevoerd, wacht u totdat het toofinish voordat de poging toodo Hallo VIP wisselen.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Probleem: Er is een rolinstantie lussen tussen gestart, initialiseert, bezet en gestopt
Dit probleem kan duiden op een probleem met uw programmacode, pakket of configuratiebestand. In dat geval moet u kunnen toosee Hallo status wijzigen om de paar minuten en hello Azure-portal staat mogelijk ongeveer **Recycling**, **bezet**, of **Bezig met initialiseren**. Dit geeft aan dat er iets mis met de toepassing hello waardoor Hallo rolinstantie wordt uitgevoerd.

Voor meer informatie over het tootroubleshoot voor dit probleem, Zie Hallo blogbericht [Azure PaaS Compute Diagnostics-gegevens](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) en [algemene problemen die functies oorzaak toorecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Probleem: Mijn toepassing werkt niet
1. Klik op Hallo rolinstantie in hello Azure-portal.
2. In Hallo **eigenschappen** deelvenster Hallo Azure-portal, overweeg Hallo voorwaarden tooresolve na uw probleem:
   * Als rolinstantie Hallo onlangs is gestopt (u kunt controleren Hallo-waarde van **afbreken aantal**), Hallo-implementatie kan worden bijgewerkt. Wacht toosee als rolinstantie Hallo hervat werkt op een eigen.
   * Als de rolinstantie Hallo **bezet**, Controleer uw toepassing code toosee hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) gebeurtenis wordt verwerkt. Of u kunt mogelijk tooadd los van de code die verantwoordelijk is voor deze gebeurtenis.
   * Diagnostische gegevens Hallo doorlopen en probleemoplossing in Hallo blogbericht [Azure PaaS Compute Diagnostics-gegevens](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Als u uw cloudservice recyclen, u opnieuw instellen Hallo-eigenschappen voor implementatie van Hallo Hallo-informatie voor het oorspronkelijke probleem Hallo effectief te wissen.
>
>

## <a name="next-steps"></a>Volgende stappen
Meer [probleemoplossing artikelen](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) voor cloudservices.

Zie hoe tootroubleshoot cloud service rol problemen met behulp van Azure PaaS computer diagnostische gegevens toolearn [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
