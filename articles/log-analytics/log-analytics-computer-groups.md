---
title: aaaComputer groepen in logboekanalyse Meld zoekopdrachten | Microsoft Docs
description: Computergroepen in Log Analytics kunnen u tooscope logboek zoekopdrachten tooa bepaalde set van computers.  Dit artikel wordt beschreven Hallo verschillende methoden kunt u toocreate computergroepen en hoe toouse die ze in een logboek zoeken.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Meld u zoekopdrachten computergroepen in Log Analytics

>[!NOTE]
> Dit artikel wordt beschreven Hallo gebruik van computergroepen Hallo huidige logboek Anayltics query language gebruiken.    Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), dan anders werkt de computergroepen.  Opmerkingen zijn opgenomen in dit artikel met andere Hallo-syntaxis en het gedrag voor nieuwe querytaal Hallo.  


Computergroepen in Log Analytics kunnen u tooscope [Meld zoekopdrachten](log-analytics-log-searches.md) tooa bepaalde set computers.  Elke groep wordt gevuld met computers met behulp van een query die u definieert of groepen importeren uit verschillende bronnen.  Als u Hallo is opgenomen in een logboek zoekopdracht, zijn Hallo resultaten beperkt toorecords die overeenkomen met de computers in de groep Hallo Hallo.

## <a name="creating-a-computer-group"></a>Een computergroep maken
U kunt een computergroep maken in met behulp van een Hallo methoden in de volgende tabel Hallo logboekanalyse.  Meer informatie over elke methode vindt u in de volgende secties voor Hallo. 

| Methode | Beschrijving |
|:--- |:--- |
| Zoekopdrachten in logboeken |Maak een logboek zoekquery waarmee een lijst met computers en Hallo resultaten opslaan als een computergroep. |
| API voor zoeken in logboeken |Gebruik Hallo Log-API van zoekservice tooprogrammatically Maak een computergroep op basis van resultaten van een zoekopdracht logboek Hallo. |
| Active Directory |Automatisch scannen Hallo-groepslidmaatschap van de agentcomputers die lid zijn van een Active Directory-domein en een groep maken in Log Analytics voor elke beveiligingsgroep. |
| WSUS |Automatisch scannen van WSUS-servers of clients gebruiken om groepen en maakt u een groep in Log Analytics voor elk. |

### <a name="log-search"></a>Zoekopdrachten in logboeken
Computergroepen gemaakt op basis van een zoekopdracht logboek bevat alle Hallo-computers die zijn geretourneerd door een zoekopdracht die u definieert.  Deze query wordt uitgevoerd telkens wanneer de computergroep hello wordt gebruikt zodat alle wijzigingen die sinds Hallo-groep is gemaakt wordt weergegeven.

Hallo te volgen procedure toocreate een computergroep van een zoekopdracht logboek gebruiken.

1. [Maken van een zoekopdracht logboek](log-analytics-log-searches.md) die resulteert in een lijst van computers.  Hallo zoeken moet retourneren een unieke set van computers met behulp van ongeveer **Distinct Computer** of **count() door Computer te meten** in Hallo-query.  
2. Klik op Hallo **opslaan** knop Hallo boven aan het welkomstscherm.
3. Selecteer **Ja** te**deze query opslaan als een computergroep**.
4. Typ in een **naam** en een **categorie** voor Hallo-groep.  Als er een zoekopdracht met dezelfde naam en categorie al Hallo bestaat, moet u zijn na vragen aan gebruiker toooverwrite deze.  U kunt meerdere zoekopdrachten met dezelfde naam in verschillende categorieën Hallo hebben. 

Hieronder vindt u voorbeelden van zoekopdrachten die u kunt opslaan als een computergroep.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md) vervolgens hello volgende wijzigingen aangebracht toohello procedure toocreate een nieuwe computergroep worden.
>  
> - Hallo query toocreate vergezeld gaan van een computergroep `distinct Computer`.  Hier volgt een voorbeeld van een query toocreate een computergroep.<br>`Heartbeat | where Computer contains "srv" `
> - Wanneer u een nieuwe computergroep maakt, moet u een alias in toevoeging toohello naam opgeven.  U Hallo alias gebruiken wanneer u de computergroep Hallo in een query zoals hieronder wordt beschreven.  

### <a name="log-search-api"></a>Meld u API van zoekservice
Computergroepen die zijn gemaakt met de Hallo Log-API van zoekservice zijn Hallo dezelfde als de zoekopdrachten die zijn gemaakt met een zoekopdracht logboek.

Zie voor meer informatie over het maken van een computergroep Hallo Log zoeken-API met [computergroepen in logboek logboekanalyse zoeken REST-API](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Wanneer u Log Analytics tooimport Active Directory-groepslidmaatschappen configureert, wordt geanalyseerd Hallo-groepslidmaatschap van computers met Hallo OMS-agent verbonden met het domein.  Een computergroep in logboekanalyse gemaakt voor elke beveiligingsgroep in Active Directory en elke computer toegevoegd toohello computergroepen toohello beveiligingsgroepen waarvan die ze lid van zijn overeenkomt.  Dit lidmaatschap wordt voortdurend bijgewerkt voor elke 4 uur.  

Configureren van logboekanalyse tooimport Active Directory-beveiligingsgroepen van Hallo **computergroepen** menu van logboekanalyse **instellingen**.  Selecteer **Automation** en vervolgens **importeren Active Directory-groepslidmaatschappen van computers**.  Er is geen verdere configuratie nodig.

![Computergroepen uit Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Wanneer groepen ingevoerd zijn, hello menu lijsten Hallo aantal computers met groepslidmaatschappen gedetecteerd en Hallo aantal groepen geïmporteerd.  U kunt klikken op een van deze koppelingen tooreturn hello **ComputerGroup** records met deze informatie.

### <a name="windows-server-update-service"></a>Windows Server updateservice
Bij het configureren van logboekanalyse tooimport WSUS-groepslidmaatschappen, Hallo die gericht is op het lidmaatschap van alle computers met Hallo OMS-agent wordt geanalyseerd.  Als u aan de clientzijde is ontwikkelt, elke computer die is verbonden tooOMS en maakt deel uit van een WSUS targeting van groepen het groepslidmaatschap geïmporteerd tooLog Analytics. Als u van server side gebruikmaakt ontwikkelt, Hallo OMS-agent moet worden geïnstalleerd op Hallo WSUS-server in de volgorde voor Hallo groepslidmaatschap informatie toobe geïmporteerd tooOMS.  Dit lidmaatschap wordt voortdurend bijgewerkt voor elke 4 uur. 

Configureren van logboekanalyse tooimport Active Directory-beveiligingsgroepen van Hallo **computergroepen** menu van logboekanalyse **instellingen**.  Selecteer **Active Directory** en vervolgens **importeren Active Directory-groepslidmaatschappen van computers**.  Er is geen verdere configuratie nodig.

![Computergroepen uit Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Wanneer groepen ingevoerd zijn, hello menu lijsten Hallo aantal computers met groepslidmaatschappen gedetecteerd en Hallo aantal groepen geïmporteerd.  U kunt klikken op een van deze koppelingen tooreturn hello **ComputerGroup** records met deze informatie.

## <a name="managing-computer-groups"></a>Computergroepen beheren
U kunt bekijken van computergroepen die zijn gemaakt met een zoekopdracht logboek of Log zoeken-API van Hallo Hallo **computergroepen** menu van logboekanalyse **instellingen**.  Klik op Hallo **x** in Hallo **verwijderen** kolom toodelete Hallo-computergroep.  Klik op Hallo **leden weergeven** pictogram voor een groep toorun Hallo groep logboek zoekquery waarmee de leden ervan. 

![Opgeslagen computergroepen](media/log-analytics-computer-groups/configure-saved.png)

Hallo toomodify groep, maakt u een nieuwe groep Hello dezelfde **categorie** en **naam** toooverwrite Hallo oorspronkelijke groep.

## <a name="using-a-computer-group-in-a-log-search"></a>Met behulp van de groep van een computer in een logboek zoekopdracht
U Hallo syntaxis toorefer tooa computergroep in een logboek zoekopdracht te volgen.  Geven Hallo **categorie** is optioneel en is alleen vereist als u computergroepen met dezelfde naam in verschillende categorieën Hallo hebt. 

    $ComputerGroups[Category: Name]

Wanneer u een zoekopdracht uitvoert, worden leden van alle computergroepen opgenomen in de zoekopdracht Hallo Hallo eerst opgelost.  Als de groep Hallo is gebaseerd op een zoekopdracht logboek, wordt die zoekopdracht uitgevoerd tooreturn Hallo leden van Hallo groep voordat u Hallo op het hoogste niveau logboek zoekopdracht uitvoert.

Computergroepen worden meestal gebruikt met Hallo **IN** -component in Hallo logboek zoeken zoals Hallo volgt in:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Als uw werkruimte bijgewerkte toohello is [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), u een computergroep in een query door de alias behandelen als een functie, zoals in het volgende voorbeeld Hallo gebruiken:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Groeperen van computerrecords
Een record gemaakt in Hallo OMS-opslagplaats voor elke computer groepslidmaatschap gemaakt op basis van Active Directory of WSUS.  Deze records zijn een type **ComputerGroup** en Hallo eigenschappen in de volgende tabel Hallo hebben.  Records worden niet gemaakt voor computergroepen op basis van het logboek zoekopdrachten.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Computer |Naam van de computer die lid is Hallo. |
| Groep |Naam van groep Hallo. |
| GroupFullName |Volledig pad toohello groep inclusief Hallo bron- en naam van de gegevensbron. |
| GroupSource |Bron van die groep die is verzameld van is. <br><br>Active Directory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |Naam van Hallo-bron die groep Hallo is verzameld.  Voor Active Directory is dit Hallo domeinnaam. |
| ManagementGroupName |De naam van de beheergroep Hallo voor SCOM-agents.  Dit is voor andere agents AOI -\<werkruimte-ID\> |
| TimeGenerated |Datum en tijd Hallo computergroep is gemaakt of bijgewerkt. |

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) tooanalyze Hallo gegevens verzameld van gegevensbronnen en oplossingen.  

