---
title: Computergroepen in logboekanalyse Meld zoekopdrachten | Microsoft Docs
description: Computergroepen in Log Analytics kunnen u bereik logboek zoekopdrachten aan een bepaalde set van computers.  In dit artikel beschrijft de verschillende methoden die u gebruiken kunt om computergroepen en hoe ze te gebruiken in een zoekopdracht logboek te maken.
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
ms.openlocfilehash: a2ddc932343d54963a378ee27dc962a790326b2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Meld u zoekopdrachten computergroepen in Log Analytics

>[!NOTE]
> Dit artikel wordt het gebruik van computergroepen met behulp van de huidige logboek Anayltics querytaal beschreven.    Als uw werkruimte is bijgewerkt naar de [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), dan anders werkt de computergroepen.  Opmerkingen zijn opgenomen in dit artikel met de syntaxis van de andere en het gedrag voor de nieuwe query language.  


Computergroepen in Log Analytics kunnen u bereik [Meld zoekopdrachten](log-analytics-log-searches.md) aan een bepaalde set van computers.  Elke groep wordt gevuld met computers met behulp van een query die u definieert of groepen importeren uit verschillende bronnen.  Wanneer de groep is opgenomen in een zoekopdracht in de logboekbestanden, zijn de resultaten beperkt tot records die overeenkomen met de computers in de groep.

## <a name="creating-a-computer-group"></a>Een computergroep maken
U kunt een computergroep maken in een van de methoden in de volgende tabel met logboekanalyse.  In de onderstaande secties vindt u meer informatie over elke methode. 

| Methode | Beschrijving |
|:--- |:--- |
| Zoekopdrachten in logboeken |Maak een logboek zoekquery waarmee een lijst met computers en de resultaten opslaan als een computergroep. |
| API voor zoeken in logboeken |Het logboek zoeken-API maken op een computergroep op basis van de resultaten van een zoekopdracht logboek gebruiken. |
| Active Directory |Automatisch scannen van het groepslidmaatschap van de agentcomputers die lid zijn van een Active Directory-domein en een groep maken in Log Analytics voor elke beveiligingsgroep. |
| WSUS |Automatisch scannen van WSUS-servers of clients gebruiken om groepen en maakt u een groep in Log Analytics voor elk. |

### <a name="log-search"></a>Zoekopdrachten in logboeken
Gemaakt op basis van een zoekopdracht logboek computergroepen bevatten alle computers geretourneerd door een zoekopdracht die u definieert.  Deze query wordt uitgevoerd telkens wanneer de computergroep wordt gebruikt zodat alle wijzigingen die sinds de groep is gemaakt wordt weergegeven.

Gebruik de volgende procedure een computergroep maken van een zoekopdracht logboek.

1. [Maken van een zoekopdracht logboek](log-analytics-log-searches.md) die resulteert in een lijst van computers.  De zoekopdracht moet een unieke set computers retourneren met behulp van ongeveer **Distinct Computer** of **count() door Computer te meten** in de query.  
2. Klik op de **opslaan** knop aan de bovenkant van het scherm.
3. Selecteer **Ja** naar **deze query opslaan als een computergroep**.
4. Typ in een **naam** en een **categorie** voor de groep.  Als een zoekopdracht met dezelfde naam en categorie al bestaat, worden wordt u gevraagd om te overschrijven.  U kunt meerdere zoekopdrachten met dezelfde naam hebben in verschillende categorieën. 

Hieronder vindt u voorbeelden van zoekopdrachten die u kunt opslaan als een computergroep.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Als uw werkruimte is bijgewerkt naar de [querytaal van nieuwe logboekanalyse](log-analytics-log-search-upgrade.md) en vervolgens de volgende wijzigingen zijn aangebracht aan de procedure voor het maken van een nieuwe computergroep.
>  
> - De query voor het maken van een computergroep moet bevatten `distinct Computer`.  Hieronder volgt een voorbeeld van een query naar een computergroep maken.<br>`Heartbeat | where Computer contains "srv" `
> - Wanneer u een nieuwe computergroep maakt, moet u een alias naast de naam opgeven.  U kunt de alias gebruiken bij gebruik van de computergroep in een query zoals hieronder wordt beschreven.  

### <a name="log-search-api"></a>Meld u API van zoekservice
Computergroepen die zijn gemaakt met de Search-API van het logboek zijn hetzelfde als de zoekopdrachten die zijn gemaakt met een zoekopdracht logboek.

Zie voor meer informatie over het maken van de groep van een computer met de Search-API van het logboek [computergroepen in logboek logboekanalyse zoeken REST-API](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Wanneer u Log Analytics Active Directory-groepslidmaatschappen importeren configureert, wordt het groepslidmaatschap van computers met de OMS-agent lid van domein geanalyseerd.  Een computergroep in logboekanalyse gemaakt voor elke beveiligingsgroep in Active Directory en elke computer is toegevoegd aan de overeenkomt met de beveiligingsgroepen waarvan die ze lid van zijn computergroepen.  Dit lidmaatschap wordt voortdurend bijgewerkt voor elke 4 uur.  

Configureren van logboekanalyse voor het importeren van Active Directory-beveiligingsgroepen van de **computergroepen** menu van logboekanalyse **instellingen**.  Selecteer **Automation** en vervolgens **importeren Active Directory-groepslidmaatschappen van computers**.  Er is geen verdere configuratie nodig.

![Computergroepen uit Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Wanneer u groepen zijn geïmporteerd, worden in het menu het aantal computers met groepslidmaatschappen gedetecteerd en het aantal groepen geïmporteerd worden.  U kunt klikken op een van deze koppelingen om terug te keren de **ComputerGroup** records met deze informatie.

### <a name="windows-server-update-service"></a>Windows Server updateservice
Wanneer u Log Analytics WSUS-groepslidmaatschappen importeren configureert, wordt het lidmaatschap van de toewijzing van alle computers met de OMS-agent geanalyseerd.  Als u aan de clientzijde heeft ontwikkelt, elke computer die is verbonden met OMS en maakt deel uit van een WSUS het groepslidmaatschap geïmporteerd met logboekanalyse groepen als doel. Als u van server side gebruikmaakt moet ontwikkelt, de OMS agent worden geïnstalleerd op de WSUS-server om de gegevens worden geïmporteerd op OMS.  Dit lidmaatschap wordt voortdurend bijgewerkt voor elke 4 uur. 

Configureren van logboekanalyse voor het importeren van Active Directory-beveiligingsgroepen van de **computergroepen** menu van logboekanalyse **instellingen**.  Selecteer **Active Directory** en vervolgens **importeren Active Directory-groepslidmaatschappen van computers**.  Er is geen verdere configuratie nodig.

![Computergroepen uit Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Wanneer u groepen zijn geïmporteerd, worden in het menu het aantal computers met groepslidmaatschappen gedetecteerd en het aantal groepen geïmporteerd worden.  U kunt klikken op een van deze koppelingen om terug te keren de **ComputerGroup** records met deze informatie.

## <a name="managing-computer-groups"></a>Computergroepen beheren
U kunt weergeven computergroepen die zijn gemaakt op basis van een zoekopdracht logboek of de Search-API van het logboek van de **computergroepen** menu van logboekanalyse **instellingen**.  Klik op de **x** in de **verwijderen** kolom te verwijderen van de computergroep.  Klik op de **leden weergeven** pictogram voor een groep voor het uitvoeren van de groep logboek zoekquery waarmee de leden ervan. 

![Opgeslagen computergroepen](media/log-analytics-computer-groups/configure-saved.png)

Voor het wijzigen van de groep, kunt u een nieuwe groep maken met dezelfde **categorie** en **naam** naar de oorspronkelijke groep overschrijven.

## <a name="using-a-computer-group-in-a-log-search"></a>Met behulp van de groep van een computer in een logboek zoekopdracht
U de volgende syntaxis gebruiken om te verwijzen naar een computergroep in een logboek zoekopdracht.  Geven de **categorie** is optioneel en is alleen vereist als er computergroepen met dezelfde naam in verschillende categorieën. 

    $ComputerGroups[Category: Name]

Wanneer u een zoekopdracht uitvoert, worden de leden van alle computergroepen die is opgenomen in de zoekopdracht eerst opgelost.  Als de groep is gebaseerd op een zoekopdracht logboek, wordt die zoekopdracht uitgevoerd om te retourneren van de leden van de groep voordat u de zoekopdracht op het hoogste niveau logboek uitvoert.

Computergroepen worden doorgaans gebruikt voor de **IN** -component in de zoekopdracht logboek zoals in het volgende voorbeeld:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Als uw werkruimte is bijgewerkt naar de [nieuwe logboekanalyse querytaal](log-analytics-log-search-upgrade.md), u een computergroep gebruiken in een query door de alias behandelen als een functie, zoals in het volgende voorbeeld:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Groeperen van computerrecords
Een record gemaakt in de OMS-opslagplaats voor elke computer groepslidmaatschap gemaakt op basis van Active Directory of WSUS.  Deze records zijn een type **ComputerGroup** en de eigenschappen in de volgende tabel hebben.  Records worden niet gemaakt voor computergroepen op basis van het logboek zoekopdrachten.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Type |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Computer |Naam van de computer die lid is. |
| Groep |De naam van de groep. |
| GroupFullName |Volledig pad naar de groep met inbegrip van de bron en de naam van de gegevensbron. |
| GroupSource |Bron van die groep die is verzameld van is. <br><br>Active Directory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |De naam van de bron waarvan de groep is verzameld.  Dit is de domeinnaam voor Active Directory. |
| ManagementGroupName |Naam van de beheergroep voor SCOM-agents.  Dit is voor andere agents AOI -\<werkruimte-ID\> |
| TimeGenerated |Datum en tijd van de computergroep is gemaakt of bijgewerkt. |

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over [Meld zoekopdrachten](log-analytics-log-searches.md) om de gegevens verzameld van gegevensbronnen en oplossingen te analyseren.  

