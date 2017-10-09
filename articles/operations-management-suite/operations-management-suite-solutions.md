---
title: aaaSolutions in Operations Management Suite (OMS) | Microsoft Docs
description: Oplossingen Hallo functionaliteit van Operations Management Suite (OMS) uitbreiden door te geven verpakte beheerscenario dat klanten tootheir OMS-werkruimte kunnen toevoegen.  Dit artikel bevat informatie over hoe aangepaste oplossingen die zijn gemaakt door klanten en partners.
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 1f054a4e-6243-4a66-a62a-0031adb750d8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/01/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5b5a538f1bc4b5577bec94db08bd43668bc6584a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-management-solutions-in-operations-management-suite-oms-preview"></a>Werken met oplossingen voor beheer in Operations Management Suite (OMS) (Preview)
> [!NOTE]
> Dit is voorlopige documentatie voor de beheeroplossingen in OMS die zich momenteel in preview.    
> 
> 

Beheeroplossingen Hallo functionaliteit van Operations Management Suite (OMS) uitbreiden door verpakte beheerscenario dat klanten tootheir omgeving kunnen toevoegen.  Bovendien te[oplossingen die worden geleverd door Microsoft](../log-analytics/log-analytics-add-solutions.md), partners en klanten management oplossingen toobe in hun eigen omgeving gebruikt of gemaakt beschikbaar toocustomers via Hallo community kunnen maken.

## <a name="finding-and-installing-management-solutions"></a>Zoeken en installeren van oplossingen voor het beheer
Er zijn meerdere methoden voor het vinden en te installeren van oplossingen voor het beheer, zoals beschreven in Hallo uit te voeren.

### <a name="azure-marketplace"></a>Azure Marketplace
Oplossingen voor het beheer door Microsoft geleverd en vertrouwde partners kunnen worden geïnstalleerd vanaf hello Azure Marketplace in hello Azure-portal.

1. Toohello aanmelden met Azure-portal.
2. Selecteer in het linkerdeelvenster Hallo **meer services**.
3. Een Schuif naar beneden te**oplossingen** of type *oplossingen* in Hallo **Filter** dialoogvenster.
4. Klik op Hallo **+ toevoegen** knop.
5. Zoeken naar oplossingen die u geïnteresseerd in een bent door te bladeren, te klikken op Hallo **Filter** uit-knop of typen in Hallo **Search Everthing** vak.
6. Klik op een marketplace-item tooview gedetailleerde informatie.
7. Klik op **maken** tooopen hello **oplossing toevoegen** deelvenster.
8. U zult de vraag toorequired informatie zoals Hallo [OMS werkruimte en de Automation-account](#oms-workspace-and-automation-account) bovendien toovalues voor parameters die in de oplossing Hallo.
9. Klik op **maken** tooinstall Hallo oplossing.

### <a name="oms-portal"></a>OMS-Portal
Beheeroplossingen geleverd door Microsoft kunnen worden geïnstalleerd vanaf Hallo galerie met oplossingen in Hallo OMS-portal.

1. Meld u bij toohello OMS-portal.
2. Klik op Hallo **galerie met oplossingen** tegel.
3. Meer informatie over de verschillende beschikbare oplossingen op Hallo galerie met OMS oplossingen pagina. Klik op Hallo-naam van dat u wilt dat tooadd tooOMS Hallo-oplossing.
4. Op de pagina Hallo voor Hallo-oplossing die u hebt geselecteerd, wordt gedetailleerde informatie over Hallo oplossing weergegeven. Klik op **Add**.
5. Een nieuwe tegel voor Hallo-oplossing die u hebt toegevoegd wordt weergegeven op Hallo van overzichtspagina in OMS en u kunt deze gaan gebruiken nadat uw gegevens Hallo OMS-service verwerkt.

### <a name="azure-quickstart-templates"></a>Azure-snelstartsjablonen
Leden van de community Hallo kunnen indienen management oplossingen tooAzure Quick Start-sjablonen.  U kunt deze sjablonen voor de installatie later downloaden of controleren ze toolearn hoe te[maken van uw eigen oplossingen](#creating-a-solution).

1. Hallo Doe als bij [OMS werkruimte en de Automation-account](#oms-workspace-and-automation-account) toolink een werkruimte en -account.
2. Ga te[Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).  
3. Zoeken naar een oplossing waarmee u geïnteresseerd bent in.
4. Selecteer Hallo-oplossing van Hallo resultaten tooview de details ervan.
5. Klik op Hallo **tooAzure implementeren** knop.
6. U zult na vragen aan gebruiker tooprovide informatie zoals Hallo resourcegroep en locatie in toevoeging toovalues voor parameters die in Hallo-oplossing.
7. Klik op **aankoop** tooinstall Hallo oplossing.

### <a name="deploy-azure-resource-manager-template"></a>Azure Resource Manager-sjabloon implementeren
Oplossingen die u via het Hallo-community of die u hebt [zelf maken](#creating-a-solution) worden geïmplementeerd als een Resource Manager-sjabloon en u kunt een van de Hallo standaardmethoden voor [implementeren van een sjabloon](../azure-resource-manager/resource-group-template-deploy-portal.md).  Opmerking voordat u de oplossing Hallo installeert, moet u maken en koppelen van Hallo [OMS werkruimte en de Automation-account](#oms-workspace-and-automation-account).

## <a name="oms-workspace-and-automation-account"></a>OMS-werkruimte en de Automation-account
De meeste oplossingen vereisen een [OMS-werkruimte](../log-analytics/log-analytics-manage-access.md) toocontain weergaven en een [Automation-account](../automation/automation-security-overview.md#automation-account-overview) toocontain runbooks en verwante resources. Hallo werkruimte en de account moet voldoen aan Hallo volgens de vereisten.

* Een oplossing kan alleen een OMS-werkruimte en een Automation-account gebruiken.  
* Hallo OMS-werkruimte en de Automation-account gebruikt door een oplossing moet gekoppelde tooone een andere. Een OMS-werkruimte kan alleen worden gekoppelde tooone Automation-account kan, en een Automation-account alleen gekoppelde tooone OMS-werkruimte.
* toobe gekoppeld, Hallo OMS-werkruimte en de Automation-account moet zich in dezelfde resourcegroep en regio Hallo.  Hallo-uitzondering is een OMS-werkruimte in de regio VS-Oost en en de Automation-account in VS-Oost 2.

### <a name="creating-a-link-between-an-oms-workspace-and-automation-account"></a>Maken van een koppeling tussen een OMS-werkruimte en de Automation-account
Hoe u Hallo OMS-werkruimte opgeven en Automation-account is afhankelijk van de installatiemethode Hallo voor uw oplossing.

* Wanneer u een oplossing van Microsoft via Hallo OMS-portal installeert, wordt deze in de huidige OMS-werkruimte Hallo is geïnstalleerd en geen Automation-account is vereist.
* U wordt gevraagd om een OMS-werkruimte en de Automation-account en Hallo koppeling tussen deze voor u is gemaakt tijdens de installatie van een oplossing via hello Azure Marketplace.  
* Voor oplossingen buiten hello Azure Marketplace, moet u Hallo OMS-werkruimte en de Automation-account koppelen voordat u de oplossing Hallo installeert.  U kunt dit doen door keuze Hallo OMS-werkruimte en de Automation-account te selecteren van een oplossing in hello Azure Marketplace.  U hebt geen tooactually Hallo oplossing niet installeren omdat het Hallo-koppeling wordt gemaakt als Hallo OMS-werkruimte en de Automation-account zijn geselecteerd.  Zodra het Hallo-koppeling is gemaakt, kunt klikt u vervolgens u die OMS-werkruimte en de Automation-account voor een oplossing. 

### <a name="verifying-hello-link-between-an-oms-workspace-and-automation-account"></a>Hallo-koppeling tussen een OMS-werkruimte en de Automation-account controleren
U kunt controleren of Hallo koppeling tussen een OMS-werkruimte en een Automation-account met behulp van Hallo procedure te volgen.

1. Selecteer Hallo Automation-account in hello Azure-portal.
2. Scroll toohello onderaan Hallo **instellingen** deelvenster.
3. Als er een sectie met de naam is **OMS-bronnen** in Hallo **instellingen** deelvenster en vervolgens dit account is aangesloten tooan OMS-werkruimte.
4. Selecteer **werkruimte** tooview Hallo details van Hallo OMS-werkruimte toothis Automation-account gekoppeld.

## <a name="listing-management-solutions"></a>Oplossingen voor het beheer van aanbieding
Hallo te volgen procedure tootooview Hallo beheeroplossingen in Hallo werkruimten gekoppelde tooyour Azure-abonnement gebruiken.

1. Toohello aanmelden met Azure-portal.
2. Selecteer in het linkerdeelvenster Hallo **meer services**.
3. Een Schuif naar beneden te**oplossingen** of type *oplossingen* in Hallo **Filter** dialoogvenster.
4. Oplossingen die zijn geïnstalleerd in al uw werkruimten wordt weergegeven.

Houd er rekening mee dat u alleen Hallo Microsoft solutions geïnstalleerd in de huidige werkruimte Hallo met Hallo OMS-portal kunt weergeven.

## <a name="removing-a-management-solution"></a>Een oplossing voor het beheer verwijderen
Wanneer een oplossing voor het beheer wordt verwijderd, worden ook alle resources in het Hallo-oplossing verwijderd.  

1. Hallo-oplossing niet vinden in hello Azure-portal met Hallo-procedure in [aanbieding oplossingen](#listing-solutions).
2. Selecteer de gewenste tooremove Hallo-oplossing.
3. Klik op Hallo **verwijderen** knop.

## <a name="creating-a-management-solution"></a>Maken van een beheeroplossing
Volledige informatie over het maken van oplossingen zijn beschikbaar op [om oplossingen te maken in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md). 

## <a name="next-steps"></a>Volgende stappen
* Search [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates) voor voorbeelden van andere Resource Manager-sjablonen.
* Maak uw eigen [beheeroplossingen](operations-management-suite-solutions-creating.md).

