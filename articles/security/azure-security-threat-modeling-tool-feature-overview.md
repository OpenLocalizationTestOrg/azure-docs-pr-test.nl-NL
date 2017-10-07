---
title: aaaMicrosoft Threat Modeling hulpprogramma - Azure | Microsoft Docs
description: Meer informatie over alle Hallo functies die beschikbaar zijn in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>Overzicht van Threat Modeling hulpprogramma-functies

We zijn blij dat u hebt gekozen toouse Hallo Threat Modeling hulpprogramma voor uw threat modeling behoeften! Als u dit nog niet hebt gedaan, gaat u naar  **[aan de slag met Hallo Threat Modeling hulpprogramma](./azure-security-threat-modeling-tool-getting-started.md)**  toolearn Hallo basisbeginselen.

> Onze hulpprogramma vaak wordt bijgewerkt, dus controleer dit vaak toosee helpen onze nieuwste functies en verbeteringen.

Te klikken op de knop 'Een nieuwe Model maken' hello wordt geopend, een lege startpagina, vergelijkbare toohello afbeelding hieronder:

![Lege startpagina](./media/azure-security-threat-modeling-tool/tmtstart.png)

Met behulp risicomodel Hallo gemaakt door ons team in Hallo  **[aan de slag](./azure-security-threat-modeling-tool-getting-started.md)**  voorbeeld gaan we Bekijk alle Hallo functies die beschikbaar zijn in Hallo hulpprogramma vandaag.

![Basic risicomodel](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>Navigatie

Vooraleer Hallo ingebouwde functies, gaan we via Hallo hoofdonderdelen gevonden in het Hallo-hulpprogramma

### <a name="menu-items"></a>Menu-items

Hallo-ervaring moet soortgelijke tooother Microsoft-producten. Laten we beginnen door te gaan via Hallo op het hoogste niveau menu-items:

![Menu-Items](./media/azure-security-threat-modeling-tool/menuitems.png)

| Label                               | Details      |
| --------------------------------------- | ------------ |
| **File** | <ul><li>Open, opslaan en sluiten van bestanden</li><li>Meld u in/out van OneDrive-accounts</li><li>Koppelingen (weergave + bewerken) te delen</li><li>Bestandsgegevens weergeven</li><li>Toepassen van nieuwe sjabloon tooExisting modellen</li></ul> |
| **Bewerken** | Ongedaan maken/opnieuw acties, als ook een kopie plakken en verwijderen |
| **Weergave** | <ul><li>Schakelen tussen **Analysis** en **ontwerp** weergaven</li><li>Open gesloten windows (e.g.stencils, eigenschappen van het element en berichten)</li><li>Lay-out toodefault instellingen opnieuw instellen</li></ul> |
| **Diagram** | Diagrammen toevoegen, verwijderen en door 'tabbladen' diagrammen navigeren |
| **Rapporten** | HTML-rapporten tooshare maken met anderen |
| **Help** | Handleidingen toohelp u Hallo-hulpprogramma gebruiken |

Hallo pictogrammen zijn snelkoppelingen voor Hallo op het hoogste niveau menu's:

| Pictogram                               | Details      |
| --------------------------------------- | ------------ |
| **Open** | Hiermee opent u een nieuw bestand |
| **Opslaan** | Huidige bestand wordt opgeslagen |
| **Ontwerp** | In de ontwerpweergave gaat hier kunt u modellen maken |
| **Analyseren** | Toont gegenereerd bedreigingen en hun eigenschappen |
| **Diagram toevoegen** | Nieuw diagram (vergelijkbaar toonew tabs in Excel) wordt toegevoegd |
| **Diagram verwijderen** | Hiermee verwijdert u Huidig diagram |
| **Knippen/kopiëren/plakken** | Elementen delen-kopieën/geplakt |
| **Ongedaan maken/opnieuw uitvoeren** | Hiermee wordt ongedaan gemaakt/voert acties |
| **Inzoomen- / uitzoomen** | Zoomt in en uit Hallo diagram voor een beter beeld |
| **Feedback** | Hiermee opent u Hallo MSDN-Forum |

### <a name="canvas"></a>Canvas

Hallo ruimte waar u slepen en neerzetten van elementen in. Slepen en neerzetten is Hallo snelste en meest efficiënte manier toobuild modellen. U kunt ook met de rechtermuisknop op en selecteer in de Hallo menu, dat wordt toegevoegd algemene versies van het Hallo-elementen die u gebruikt, zoals hieronder wordt weergegeven.

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Hallo stencil neer te zetten op Hallo canvas

![Canvas neerzetten](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>Te klikken op Hallo stencil

![Eigenschappen van het element](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>Stencils

Wanneer u vindt stencils alle beschikbare toouse op basis van geselecteerde Hallo-sjabloon. Als u de juiste elementen Hallo vinden kunt, probeer het opnieuw met een andere sjabloon of wijzigen van één toofit uw behoeften. In het algemeen moet u kunnen toofind een combinatie van categorieën zoals Hallo die hieronder:

| Stencilnaam                               | Details      |
| --------------------------------------- | ------------ |
| **Proces** | Toepassingen, Browser invoegtoepassingen, Threads, virtuele Machines |
| **Externe interactie** | Verificatieproviders, Browsers, gebruikers, webtoepassingen |
| **Gegevensopslag** | Cache, opslag, configuratie-bestanden, Databases, register |
| **Gegevensstroom** | Binaire ALPC, HTTP, HTTPS/TLS/SSL, IOCTL, IPSec, benoemde Pipe, RPC/DCOM, SMB, UDP |
| **Lijn grens vertrouwen** | Bedrijfsnetwerken, Internet, Machine, Sandbox, gebruiker/kernelmodus |

### <a name="notesmessages"></a>Opmerkingen bij de/Messages

| Onderdeel                               | Details      |
| --------------------------------------- | ------------ |
| **Berichten** | Interne hulpprogramma logica die gebruikers waarschuwt wanneer er een fout optreedt, zoals geen gegevensoverdrachten tussen elementen |
| **Opmerkingen bij de** | Opmerkingen bij de handmatige toegevoegde toohello bestands door engineering-teams in de rest Hallo ontwerp- en evaluatieproces |

### <a name="element-properties"></a>Eigenschappen van het element

Deze verschillen per Hallo-elementen die zijn geselecteerd. Alle andere elementen bevatten naast vertrouwen grenzen 3 algemene selecties:

| Eigenschap element                               | Details      |
| --------------------------------------- | ------------ |
| **Naam** | Handig is voor de naamgeving van uw processen, archieven, interacties en stromen toobe gemakkelijk kunt herkennen |
| **Buiten het bereik** | Indien geselecteerd, wordt Hallo-element genomen buiten Hallo threat generatie matrix (niet aanbevolen) |
| **Reden voor buiten het bereik** | Reden veld toolet gebruikers weten waarom buiten het bereik is geselecteerd |

Eigenschappen worden onder elke categorie element gewijzigd. Klik op elk element tooinspect Hallo beschikbare opties of Hallo sjabloon toolearn meer openen. Hiermee kunt krijgen tot Hallo-functies.

## <a name="welcome-screen"></a>Welkomstscherm

Hallo-welkomstscherm is Hallo eerste wat die u ziet wanneer u Hallo app opent.

### <a name="open-a-model"></a>Een model openen

Muiswijzer op de knop 'Open een Model' ziet u 2 verborgen opties: 'Openen vanaf deze Computer' en "Openen vanuit OneDrive." Hallo eerst bestand openen welkomstscherm wordt geopend terwijl Hallo tweede u Hallo aanmelden proces voor OneDrive doorloopt, zodat u bestanden en mappen toopick na een geslaagde verificatie.

![Model openen](./media/azure-security-threat-modeling-tool/openmodel.png)

![Openen van de Computer of OneDrive](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>Feedback, suggesties en problemen

Als u deze optie selecteert, gaat u toohello MSDN-Forums voor SDL-hulpprogramma's. Het is een uitstekende manier toocheck uit wat anderen hierover Hallo hulpprogramma, met inbegrip van tijdelijke oplossingen en nieuwe ideeën.

![Feedback](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>Ontwerpweergave

Wanneer u opent of een nieuw model maakt, wordt u geleid toohello ontwerpweergave.

### <a name="adding-elements"></a>Het toevoegen van elementen

Er zijn 2 manieren tooadd elementen op Hallo raster:

- **Slepen en neerzetten** : Sleep Hallo gewenste element toohello raster en gebruikt u Hallo element eigenschappen tooprovide aanvullende informatie.
- **Klik met de rechtermuisknop** : klik met de rechtermuisknop ergens op Hallo raster en selecteer in het vervolgkeuzemenu Hallo. Een algemene weergave van dat element worden weergegeven op het welkomstscherm.

### <a name="connecting-elements"></a>Verbinding maken met elementen

Er zijn 2 manieren elementen tooconnect in hulpprogramma Hallo:

- **Slepen en neerzetten** : Sleep Hallo gewenste gegevensstroom toohello raster en verbinding maken met beide uiteinden toohello geschikte elementen.
- **Klik op + Shift** : klik op de eerste Hallo-element (het versturen van gegevens) en houdt u Shift-toets ingedrukt Hallo en vervolgens selecteert Hallo tweede element (ontvangen van gegevens). Klik met de rechtermuisknop en selecteer "Verbinding maken." Als u een bidirectionele-gegevensstroom, is Hallo volgorde niet als belangrijk.

### <a name="properties"></a>Eigenschappen

Bevat alle Hallo-eigenschappen die kunnen worden gewijzigd op Hallo stencils in Hallo diagram geplaatst. toosee hello eigenschappen, klikt u op Hallo stencil en Hallo informatie dienovereenkomstig worden ingevuld. Hallo in het volgende voorbeeld ziet u voor en na een 'Database' stencil wordt gesleept Hallo diagram:

#### <a name="before"></a>Voordat u

![Voordat u](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>Na

![Na](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>Berichten

Als u een risicomodel maakt en gegevens tooconnect loopt tooelements vergeet, bericht berichtvenster Hallo tooact. U kunt tooignore deze of Voer Hallo instructies toofix Hallo probleem. 

![Berichten](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>Opmerkingen

U tooadd notities tooyour diagram toocapture kunt alle uw ideeën schakelen tussen tabbladen van berichten tooNotes

## <a name="analysis-view"></a>Analyse weergeven

Als u klaar bent voor het bouwen van uw diagram overschakelen via tooanalysis weergeven door te gaan toohello bovenste menuselecties en Hallo Vergrootglas volgende toohello paint palet kiezen.

![Analyse weergeven](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>Gegenereerde threat selectie

Wanneer u op een bedreiging klikt, kunt u gebruikmaken van drie unieke functies:

| Functie                               | Info      |
| --------------------------------------- | ------------ |
| **Lees Indicator** | <p>Bedreiging is nu gemarkeerd als gelezen die eenvoudig kunt u bijhouden van Hallo artikelen die u al hebben doorlopen</p><p>![Lezen/ongelezen Indicator](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **Interactie Focus** | <p>Interactie in Hallo diagram die behoren toothat threat is gemarkeerd</p><p>![Interactie Focus](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **Eigenschappen van de Threat** | <p>Als u meer informatie over Hallo dreiging wordt ingevuld in Hallo threat eigenschappenvenster</p><p>![Eigenschappen van de Threat](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>Prioriteit wijzigen

Hallo prioriteitsniveau van elke gegenereerde bedreiging ook wijzigt, worden hun toomake kleuren het eenvoudig tooidentify hoog, gemiddeld en laag prioriteit bedreigingen.

![Prioriteit wijzigen](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>Threat eigenschappen bewerkbare velden

Zoals u in Hallo afbeelding hierboven, kunnen gebruikers wijzigen Hallo informatie die wordt gegenereerd door Hallo hulpprogramma een ook informatie toocertain velden, zoals rechtvaardiging toevoegen. Deze velden worden gegenereerd door de sjabloon hello, dus als u meer informatie nodig voor elke bedreiging, u ten zeerste toomake wijzigingen bent.

![Eigenschappen van de Threat](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>Rapporten

Als u veranderende prioriteiten bent klaar en bijwerken Hallo-status van elke bedreiging gegenereerd, u kunt Hallo bestand opslaan en/of afdrukken door te gaan te 'rapporteren' en klik vervolgens 'volledige rapport maken." U wordt gevraagd tooname Hallo rapport en zodra u dit doet, ziet u iets dergelijks toohello afbeelding hieronder:

![Rapport](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>Volgende stappen

een sjabloon voor het Hallo-community toocontribute Ga tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)**  pagina. **[Download](https://aka.ms/tmtpreview)**  Hallo hulpprogramma tooget Vandaag gestart.
