---
title: aaaSolution doelen instellen in OMS | Microsoft Docs
description: Doelitems oplossing is een functie in Operations Management Suite (OMS) waarmee u toolimit management oplossingen tooa specifieke set van agents.  Dit artikel wordt beschreven hoe een scopeconfiguratie toocreate en tooa oplossing toepassen.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: bwren
ms.openlocfilehash: 6f8c8109e0d9e282e18724bf8b673b10de8e498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-solution-targeting-in-operations-management-suite-oms-tooscope-management-solutions-toospecific-agents-preview"></a>Oplossing die gericht is in de Operations Management Suite (OMS) tooscope oplossingen toospecific beheeragents (Preview) gebruiken
Wanneer u een oplossing tooOMS toevoegt, wordt deze automatisch geïmplementeerd door standaard tooall Windows en Linux-agents verbonden tooyour werkruimte voor logboekanalyse.  U kunt voor een oplossing toomanage uw kosten- en limit Hallo hoeveelheid gegevens die worden verzameld door het beperken van tooa bepaalde set van agents.  Dit artikel wordt beschreven hoe toouse **oplossing Targeting** dit is een OMS-functie waarmee u een scope tooapply tooyour oplossingen.

## <a name="how-tootarget-a-solution"></a>Hoe tootarget een oplossing
Er zijn drie stappen tootargeting een oplossing zoals beschreven in Hallo uit te voeren.  Houd er rekening mee dat u zowel Hallo OMS-portal en hello Azure-portal voor de verschillende stappen moet.


### <a name="1-create-a-computer-group"></a>1. Maak een computergroep
U Hallo-computers die u wilt de tooinclude in een bereik door het maken van een [computergroep](../log-analytics/log-analytics-computer-groups.md) in logboekanalyse.  Hallo-computergroep worden op basis van een zoekopdracht logboek of geïmporteerd uit andere bronnen zoals Active Directory of WSUS-groepen. Als [hieronder beschreven](#solutions-and-agents-that-cant-be-targeted)alleen voor computers die rechtstreeks zijn verbonden tooLog Analytics worden opgenomen in het Hallo-bereik.

Zodra u gemaakt in de werkruimte Hallo-computergroep hebt, je Klik opneemt in de configuratie van een scope die toegepast tooone of meer oplossingen worden kan.
 
 
 ### <a name="2-create-a-scope-configuration"></a>2. De configuratie van een scope maken
 Een **scopeconfiguratie** bevat een of meer computergroepen en kan toegepaste tooone of meer oplossingen. 
 
 Een scopeconfiguratie maken met Hallo proces te volgen.  

 1. In Azure-portal Hallo, te navigeren**logboekanalyse** en selecteer uw werkruimte.
 2. In de eigenschappen voor Hallo werkruimte onder Hallo **werkruimte gegevensbronnen** Selecteer **bereik configuraties**.
 3. Klik op **toevoegen** toocreate een nieuwe scopeconfiguratie.
 4. Typ een **naam** voor Hallo scopeconfiguratie.
 5. Klik op **Selecteer computergroepen**.
 6. Selecteer Hallo computergroep die u hebt gemaakt en desgewenst een andere groepen tooadd toohello configuratie.  Klik op **Selecteren**.  
 6. Klik op **OK** toocreate Hallo scopeconfiguratie. 


 ### <a name="3-apply-hello-scope-configuration-tooa-solution"></a>3. Hallo bereik configuratie tooa oplossing toepassen.
Zodra u de configuratie van een scope hebt, kunt klikt u vervolgens u deze toepassen tooone of meer oplossingen.  Houd er rekening mee dat tijdens een configuratie met één scope kan worden gebruikt met meerdere oplossingen, elke oplossing alleen één scopeconfiguratie gebruiken kan.

De configuratie van een bereik met Hallo na toepassen.  

 1. In Azure-portal Hallo, te navigeren**logboekanalyse** en selecteer uw werkruimte.
 2. Selecteer in de eigenschappen voor werkruimte Hallo Hallo **oplossingen**.
 3. Klik op Hallo oplossing gewenste tooscope.
 4. In de eigenschappen voor Hallo oplossing onder Hallo **werkruimte gegevensbronnen** Selecteer **oplossing als doel**.  Als het Hallo-optie is niet beschikbaar vervolgens [deze oplossing kan niet worden gericht](#solutions-and-agents-that-cant-be-targeted).
 5. Klik op **toevoegen scopeconfiguratie**.  Als u al een oplossing voor configuratie toegepast toothis vervolgens deze optie niet beschikbaar.  Hallo bestaande configuratie voordat u een andere toevoegt, moet u verwijderen.
 6. Klik op Hallo scopeconfiguratie die u hebt gemaakt.
 7. Bekijk Hallo **Status** van Hallo configuratie tooensure waarin het **geslaagd**.  Als het Hallo-status is een fout aangeeft, klikt u op Hallo ellips toohello rechts van Hallo-configuratie en selecteer **bewerken scopeconfiguratie** toomake wijzigingen.

## <a name="solutions-and-agents-that-cant-be-targeted"></a>Oplossingen en agents die niet worden gericht
Hieronder vindt u Hallo criteria voor agents en oplossingen die met het doel van de oplossing kunnen niet worden gebruikt.

- Oplossing die gericht is alleen van toepassing op toosolutions die tooagents implementeert.
- Oplossing targeting toosolutions geleverd door Microsoft alleen van toepassing.  Dit geldt niet toosolutions [gemaakt door uzelf of partners](operations-management-suite-solutions-creating.md).
- U kunt alleen agents die rechtstreeks verbinding tooLog Analytics gemaakt filter.  Oplossingen implementeren automatisch tooany agents die deel uitmaken van een verbonden Operations Manager-beheergroep of ze zijn opgenomen in de configuratie van een bereik.

### <a name="exceptions"></a>Uitzonderingen
Oplossing als doel kan niet worden gebruikt met Hallo criteria oplossingen te volgen, ondanks dat ze Hallo passen vermeld.

- Evaluatie van agent-status

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over oplossingen inclusief Hallo-oplossingen die beschikbaar tooinstall in uw omgeving op [toevoegen Azure Log Analytics management oplossingen tooyour werkruimte](../log-analytics/log-analytics-add-solutions.md).
- Meer informatie over het maken van computergroepen op [computergroepen in logboekanalyse Meld zoekopdrachten](../log-analytics/log-analytics-computer-groups.md).