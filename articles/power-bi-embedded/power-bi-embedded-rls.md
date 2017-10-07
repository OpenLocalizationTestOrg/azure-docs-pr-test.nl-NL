---
title: aaaRow beveiligingsniveau met Power BI Embedded
description: Meer informatie over beveiliging met Power BI Embedded
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a>Beveiliging op rijniveau in Power BI Embedded

Beveiliging op rijniveau (RLS) kan worden gebruikt toorestrict gebruiker toegang tot tooparticular gegevens binnen een rapport of de gegevensset, zodat voor meerdere verschillende gebruikers toouse Hallo hetzelfde rapport tijdens alle zien van andere gegevens. Power BI Embedded biedt nu ondersteuning voor gegevenssets die zijn geconfigureerd voor beveiliging op Rijniveau.

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

Volgorde tootake profiteren van RLS is het belangrijk dat u begrijpt dat drie belangrijkste concepten; Gebruikers, rollen en -regels. Laten we dichter bij elke:

**Gebruikers** – deze bekijkt hello werkelijke eindgebruikers rapporten. Gebruikers worden geïdentificeerd in Power BI Embedded door Hallo gebruikersnaam eigenschap in een App-Token.

**Rollen** – gebruikers deel uitmaken van tooroles. Een rol is een container voor regels en kan de naam zoals 'Sales Manager' of 'Vertegenwoordiger'. In Power BI Embedded worden gebruikers geïdentificeerd door de eigenschap Hallo rollen in een App-Token.

**Regels** : rollen regels hebben en deze regels zijn Hallo werkelijke filters die toobe toegepast toohello gegevens gaat. Dit wordt mogelijk net zo eenvoudig als ' land Verenigde Staten = ' of iets meer dynamische.

### <a name="example"></a>Voorbeeld

Hallo rest van dit artikel bieden we een voorbeeld van RLS ontwerpen en verbruikt die in een ingesloten toepassing. Dit voorbeeld wordt Hallo [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX-bestand.

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

Onze Retail Analysis sample verkoopcijfers voor alle Hallo winkels in een bepaalde winkelketen. Zonder RLS, ongeacht welke regionale manager zich aanmeldt en weergaven hello rapport, ze ziet Hallo dezelfde gegevens. Senior management heeft bepaald dat elke regionale manager moet alleen zien Hallo sales voor Hallo winkels die ze beheren en toodo, kunnen we RLS gebruiken.

RLS is geschreven in Power BI Desktop. Hallo gegevensset en het rapport die worden geopend, kunnen we toodiagram weergave toosee Hallo schema switch:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

Hier volgen enkele dingen toonotice met dit schema:

* Alle maateenheden zoals **totale verkoop**, worden opgeslagen in Hallo **verkoop** feitentabel.
* Er zijn vier extra gerelateerde dimensietabellen: **Item**, **tijd**, **Store**, en **regionale**.
* Hallo pijlen op Hallo relatie regels aangeven hoe filters van één tabel tooanother stromen kunnen. Bijvoorbeeld, als een filter is geplaatst **tijd [datum]**, in het huidige schema Hallo deze alleen filtert u omlaag waarden in Hallo **verkoop** tabel. Er zijn geen andere tabellen wordt beïnvloed door dit filter sinds alle Hallo pijlen Hallo relatie punt toohello verkoop tabel en niet verwijderd.
* Hallo **regionale** tabel geeft aan wie Hallo manager is voor elk:
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

Op basis van dit schema als we een toohello filter toepassen **regionale Manager** kolom in tabel regionale Hallo en als Hallo gebruiker Hallo rapport weergeven met het filter overeenkomt met het filter ook omlaag hello wordt filteren **Store**en **verkoop** tabellen tooonly gegevens weergeven die voor die specifieke regionale manager.

Hier ziet u hoe:

1. Klik op Hallo modellering tabblad op **rollen beheren**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. Maak een nieuwe rol aangeroepen **Manager**.  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. In Hallo **regionale** tabel Voer Hallo DAX-expressie te volgen: **[regionale Manager] USERNAME() =**  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. toomake ervoor Hallo regels werken op Hallo **modelleren** tabblad **weergave als rollen**, en voer de volgende Hallo:  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   Hallo rapporten worden nu gegevens weergegeven als u zijn aangemeld als **Andrew Ma**.

Hallo-filter, Hallo manier werkwijze, toepassen worden gefilterd omlaag alle records in Hallo **regionale**, **Store**, en **verkoop** tabellen. Echter, vanwege de Filterrichting Hallo op Hallo relaties tussen **verkoop** en **tijd**, **verkoop** en **Item**, en **Item** en **tijd** tabellen worden niet gefilterd omlaag.

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

Die mogelijk ok voor deze vereiste, maar als we managers toosee items waarvoor ze niet beschikken over een verkoop niet wilt, we kan inschakelen bidirectionele cross filteren voor Hallo relatie en stroom Hallo beveiligingsfilter in beide richtingen. Dit kan worden gedaan door het Hallo-relatie tussen bewerken **verkoop** en **Item**, zoals deze:

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

Filters kunnen nu ook stromen van Hallo verkoop tabel toohello **Item** tabel:

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> Als u de modus DirectQuery voor uw gegevens, moet u tooenable bidirectionele-cross filteren op deze twee opties selecteren:

1. **Bestand** -> **opties en instellingen** -> **Voorbeeldfuncties** -> **inschakelen kruislings filteren in beide richtingen voor DirectQuery**.
2. **Bestand** -> **opties en instellingen** -> **DirectQuery** -> **onbeperkte meting in DirectQuery-modus toestaan**.

meer informatie over bidirectionele cross-filtering, download Hallo toolearn [bidirectionele cross-filteren in SQL Server Analysis Services 2016 en Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) technisch document.

Dit wordt afgerond alle Hallo-werk dat toobe in Power BI Desktop uitgevoerd moet, maar er is een meer stuk werk dat toobe gedaan toomake moet Hallo RLS regels hebben we werken in Power BI Embedded gedefinieerd. Gebruikers worden geverifieerd en geautoriseerd door uw toepassing en App-tokens zijn gebruikte toogrant die gebruiker toegang tooa specifieke Power BI Embedded rapporteren. Power BI Embedded geen specifieke gegevens die op die de gebruiker is. Voor RLS toowork moet u toopass enkele aanvullende context als onderdeel van uw app-token:

* **gebruikersnaam** (optioneel) – gebruikt voor beveiliging op Rijniveau dit is een tekenreeks die kan worden gebruikt toohelp identificatie Hallo gebruiker bij het toepassen van RLS regels. Zie rij beveiliging op rijniveau met Power BI Embedded
* **rollen** : een tekenreeks met Hallo rollen tooselect bij het toepassen van regels voor beveiliging op rijniveau. Als meer dan één rol wordt doorgegeven, moeten worden doorgegeven als een tekenreeksmatrix.

U Hallo-token maken met behulp van Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) methode. Als de eigenschap username Hallo aanwezig is, moet u ook ten minste één waarde doorgeven in rollen.

U kan bijvoorbeeld Hallo EmbedSample wijzigen. DashboardController regel 55 kan worden bijgewerkt vanuit

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

tot

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

Hallo volledige app-token wordt als volgt uitzien:

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

Nu met alle Hallo stukken samen zult wanneer iemand zich bij onze toepassing tooview dit rapport aanmeldt ze alleen kunnen toosee Hallo gegevens die ze toosee mogen, zoals gedefinieerd door onze beveiliging.

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a>Zie ook

[Beveiliging (RLS) met Power](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[Verifiëren en autoriseren in Power BI Embedded](power-bi-embedded-app-token-flow.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[Voorbeeld van ingesloten JavaScript](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Nog vragen? [Probeer Hallo Power BI-Community](http://community.powerbi.com/)

