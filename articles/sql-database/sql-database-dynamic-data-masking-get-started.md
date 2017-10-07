---
title: aaaAzure SQL-Database dynamische-gegevensmaskering | Microsoft docs
description: SQL-Database dynamische-gegevensmaskering blootstelling van gevoelige gegevens beperkt door het toonon beheerdersmogelijkheden maskeren
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: 4b36d78e-7749-4f26-9774-eed1120a9182
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/09/2017
ms.author: ronitr; ronmat
ms.openlocfilehash: 68b55128dc096f7e3dd0e5ed1427b39da5d64736
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-dynamic-data-masking"></a>De dynamische gegevensmaskering SQL-Database

Gevoelige gegevens blootstelling SQL-Database dynamische-gegevensmaskering beperkt door het toonon beheerdersmogelijkheden maskeren. 

Dynamische gegevensmaskering helpt voorkomen dat onbevoegde toegang toosensitive gegevens doordat klanten toodesignate hoeveel Hallo gevoelige gegevens tooreveal met minimale gevolgen voor de toepassingslaag Hallo. Het is een beveiligingsfunctie op basis van beleid dat gevoelige gegevens in de resultatenset Hallo van een query Hallo via aangewezen databasevelden, verbergt tijdens het Hallo-gegevens in Hallo-database wordt niet gewijzigd.

Bijvoorbeeld, een medewerker van de in het midden van een aanroep van aanroepfuncties door verschillende cijfers van het nummer van hun creditcard kan worden geïdentificeerd, maar die gegevens items mag niet volledig zijn blootgesteld toohello van de klantenservice. Een maskeringsregel kan worden gedefinieerd dat alle maskers maar Hallo vier cijfers van een willekeurig aantal creditcard in de resultatenset Hallo van een query laatste. Als een ander voorbeeld mag een masker relevante gegevens gedefinieerde tooprotect persoonsgegevens (PII) gegevens, zodat een ontwikkelaar productieomgevingen opvragen kan voor het oplossen van problemen regelgeving overtreden.

## <a name="sql-database-dynamic-data-masking-basics"></a>SQL-Database dynamische-gegevensmaskering basisbeginselen
U Stel een beleid in Hallo voor dynamische gegevensmaskering Azure-portal door te selecteren Hallo dynamische-gegevensmaskering bewerking in de blade SQL Database-configuratie of de instellingenblade.

### <a name="dynamic-data-masking-permissions"></a>Machtigingen voor maskering van dynamische gegevens
Dynamische-gegevensmaskering kan worden geconfigureerd door Hallo Azure Database beheerder, serverbeheerder of officer beveiligingsrollen.

### <a name="dynamic-data-masking-policy"></a>Beleid voor maskering van dynamische gegevens
* **SQL-gebruikers uitgesloten van maskering** : een set van SQL-gebruikers of AAD-identiteiten die toegankelijk gegevens in Hallo SQL ophalen-queryresultaten. Gebruikers met administrator-bevoegdheden zijn altijd uitgesloten van maskering en Zie Hallo oorspronkelijke gegevens zonder eventuele masker.
* **Regels maskeren** -een reeks regels die definiëren Hallo aangewezen velden toobe gemaskeerd en Hallo gegevensmaskeringsfunctie die wordt gebruikt. Hallo aangewezen velden kan worden gedefinieerd met een schema databasenaam, de tabelnaam en de kolomnaam.
* **Functies maskeren** -een aantal methoden waarmee Hallo blootstelling van gegevens voor verschillende scenario's.

| Maskeringsfunctie | Logica maskeren |
| --- | --- |
| **Standaard** |**Volledige maskeren volgens toohello gegevens typen Hallo aangewezen velden**<br/><br/>• Gebruik XXXX of minder Xs als Hallo Hallo veld minder dan 4 tekens voor de gegevenstypen string (nchar, ntext, nvarchar is).<br/>• Gebruik een nulwaarde voor numerieke gegevenstypen (bigint, bits, decimal, int, money, numerieke, smallint, smallmoney, tinyint, float, real).<br/>• Gebruik 01-01-1900 voor datum/tijd-gegevenstypen (datum, datetime2, datetime, datetimeoffset, smalldatetime, tijd).<br/>• Voor SQL-variant Hallo standaardwaarde van het huidige type hello wordt gebruikt.<br/>• Voor het Hallo-XML-document <masked/> wordt gebruikt.<br/>• Gebruik een lege waarde voor speciale gegevenstypen (tijdstempel tabel, hierarchyid, GUID, binary, image, varbinary ruimtelijke typen). |
| **Creditcard** |**Methode, die Hallo beschrijft maskeren laatste vier cijfers van Hallo aangewezen velden** en voegt u een constante tekenreeks als voorvoegsel in Hallo vorm van een creditcard toe.<br/><br/>XXXX-XXXX-XXXX-1234 |
| **E-mail** |**Methode, die beschrijft de eerste letter Hallo en Hallo domein vervangt door XXX.com maskeren** met behulp van een constante tekenreeks voorvoegsel in Hallo vorm van een e-mailadres.<br/><br/>aXX@XXXX.com |
| **Willekeurig getal** |**Methode, waarmee een willekeurig getal genereert maskeren** volgens toohello geselecteerd grenzen en werkelijke gegevenstypen. Als grenzen aangewezen Hallo gelijk zijn, is Hallo gegevensmaskeringsfunctie een constante waarde.<br/><br/>![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/1_DDM_Random_number.png) |
| **Aangepaste tekst** |**Methode, welke gegarandeerd Hallo eerste en laatste tekens maskeren** en wordt een aangepaste opvulling tekenreeks in het midden Hallo toegevoegd. Als de oorspronkelijke reeks Hallo korter dan Hallo beschikbaar gesteld voor- en achtervoegsel en is wordt alleen Hallo opvulling van de tekenreeks gebruikt. <br/>voorvoegsel [opvulling] achtervoegsel<br/><br/>![Navigatiedeelvenster](./media/sql-database-dynamic-data-masking-get-started/2_DDM_Custom_text.png) |

<a name="Anchor1"></a>

### <a name="recommended-fields-toomask"></a>Aanbevolen velden toomask
Hallo vlaggen-engine aanbevelingen DDM bepaalde velden uit de database als potentieel gevoelige velden, die mogelijk geschikt voor maskering. Hallo blade dynamische-Gegevensmaskering in Hallo-portal ziet u Hallo aanbevolen kolommen voor uw database. U hoeft alleen toodo is, klikt u op **masker toevoegen** voor een of meer kolommen en vervolgens **opslaan** tooapply een masker voor deze velden.

## <a name="set-up-dynamic-data-masking-for-your-database-using-powershell-cmdlets"></a>Instellen van de dynamische-gegevensmaskering voor de database met de Powershell-cmdlets
Zie [Cmdlets van Azure SQL Database](https://msdn.microsoft.com/library/azure/mt574084.aspx).

## <a name="set-up-dynamic-data-masking-for-your-database-using-rest-api"></a>Instellen van dynamische gegevens maskeren voor de database met de REST-API
Zie [bewerkingen voor Azure SQL-Databases](https://msdn.microsoft.com/library/dn505719.aspx).

