---
title: aaaMicrosoft Power BI Embedded - verbindende tooa-gegevensbron
description: Power BI Embedded, toodata bronnen verbinding maken
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Verbinding maken met gegevensbron tooa
Met **Power BI Embedded**, kunt u rapporten insluiten in uw eigen app. Wanneer u een Power BI-rapport in uw app insluiten, Hallo rapport toohello gegevens door de onderliggende verbinding **importeren** een kopie van Hallo gegevens of door **rechtstreeks verbinding maken** toohello gegevensbron via  **DirectQuery**.

Hier volgen Hallo verschillen tussen het gebruik van **importeren** en **DirectQuery**.

| Importeren | DirectQuery |
| --- | --- |
| Tabellen, kolommen *en gegevens* zijn geïmporteerd of gekopieerd naar de gegevensset Hallo van het rapport. toosee die opgetreden toohello onderliggende gegevens wordt gewijzigd, moet u vernieuwen of importeren, een volledige, actuele gegevensset opnieuw. |Alleen *tabellen en kolommen* zijn geïmporteerd of gekopieerd naar de gegevensset Hallo van het rapport. U weergeven altijd de meest recente gegevens Hallo. |

Met Power BI Embedded u DirectQuery kunt gebruiken met gegevensbronnen van de cloud, maar niet on-premises gegevensbronnen op dit moment.

> [!NOTE]
> Hallo wordt On-Premises Data Gateway niet ondersteund met Power BI Embedded op dit moment. Dit betekent dat u DirectQuery niet gebruiken met on-premises gegevensbronnen.

## <a name="supported-data-sources"></a>Ondersteunde gegevensbronnen

**DirectQuery**
* Azure SQL-database
* Azure SQL Data Warehouse

**Importeren**

U kunt importeren met alle beschikbare gegevensbronnen Hallo in Power BI Desktop. U gaat **niet** kunnen toorefresh worden gegevens in Power BI Embedded. U hebt wijzigingen tooupload tooyour PBIX-bestand tooPower BI Embedded. Dit is vanwege toono beschikbare gateway. 

## <a name="benefits-of-using-directquery"></a>Voordelen van het gebruik van DirectQuery
Er zijn twee belangrijke voordelen bij gebruik van **DirectQuery**:

* **DirectQuery** kunt u visualisaties op zeer grote gegevenssets bouwt, waar deze anders unfeasible toofirst importeren zijn zou alle Hallo gegevens.
* Onderliggende gegevenswijzigingen kunt vereisen een vernieuwing van gegevens, en voor sommige rapporten hello moet toodisplay actuele gegevens kunt vereisen grote hoeveelheden gegevens veroorzaken, waardoor opnieuw importeren gegevens unfeasible. Daarentegen **DirectQuery** rapporten altijd actuele gegevens gebruiken.

## <a name="limitations-of-directquery"></a>Beperkingen van DirectQuery
   Er zijn enkele beperkingen toousing **DirectQuery**:

* Alle tabellen moeten afkomstig zijn van een individuele database.
* Als Hallo-query te complex is, treedt er een fout op. tooremedy hello fout moet u de Hallo query opsplitsen zodat deze minder complex is. Als het Hallo-query moet complex zijn, moet u tooimport Hallo gegevens in plaats van **DirectQuery**.
* Relatie voor het filteren is beperkt tooa één richting, in plaats van beide richtingen.
* U kunt Hallo-gegevenstype van een kolom niet wijzigen.
* Standaard worden de beperkingen op DAX-expressies toegestaan in metingen geplaatst. Zie [DirectQuery en metingen](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery en metingen
tooensure query's verzonden van de onderliggende gegevensbron toohello hebben aanvaardbare prestaties, beperkingen worden opgelegd voor metingen. Wanneer u **Power BI Desktop**, geavanceerde gebruikers kunnen kiezen toobypass deze beperking door te kiezen **bestand > Opties en instellingen > opties**. In Hallo **opties** dialoogvenster kiezen **DirectQuery**, en selecteer de optie Hallo **onbeperkte metingen in DirectQuery-modus toestaan**. Wanneer deze optie is geselecteerd, kan een DAX-expressie die is geldig voor een meting kan worden gebruikt. Gebruikers moeten zich op de hoogte; dat sommige expressies die uitstekend presteren wanneer Hallo gegevens worden geïmporteerd kunnen echter resulteren in zeer traag query's toohello back-end bron wanneer in **DirectQuery** modus. 

## <a name="see-also"></a>Zie ook
* [Aan de slag met Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)

