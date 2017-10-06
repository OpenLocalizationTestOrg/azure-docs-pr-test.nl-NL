---
title: een Azure CDN-eindpunt aaaPurge | Microsoft Docs
description: Meer informatie over hoe alle toopurge in de cache opgeslagen inhoud van een Azure CDN-eindpunt.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 0b50230b-fe82-4740-90aa-95d4dde8bd4f
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a09f4a49aa1e2d7655ecae44b5126c11c28fd599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="purge-an-azure-cdn-endpoint"></a>Een Azure CDN-eindpunt leegmaken
## <a name="overview"></a>Overzicht
Azure CDN edge-knooppunten cache activa totdat van Hallo actief time to live (TTL) is verlopen.  Nadat van Hallo actief TTL verloopt, wanneer een client Hallo asset bij Hallo edge-knooppunt aanvraagt, wordt de Hallo edge-knooppunt een nieuwe, bijgewerkte kopie van Hallo asset tooserve Hallo-clientaanvraag ophalen en de vernieuwen Hallo cache opslaan.

Hallo best practice toomake ervoor dat uw gebruikers altijd de meest recente versie Hallo van uw assets ophalen is tooversion uw assets voor elke update en deze publiceren als nieuwe URL's.  CDN wordt onmiddellijk Hallo nieuwe activa voor de volgende clientaanvragen Hallo ophalen.  U kunt soms desgewenst toopurge in de cache opgeslagen inhoud van alle knooppunten van de rand en zorgen dat ze alle tooretrieve nieuwe bijgewerkte activa.  Dit kan zijn vanwege tooupdates tooyour-webtoepassing of tooquickly update assets die onjuiste gegevens bevatten.

> [!TIP]
> Opmerking dat alleen Hallo opschonen wist in cache opgeslagen inhoud op Hallo CDN edge-servers.  Eventuele downstream caches, zoals proxyservers en caches van lokale, kunnen nog steeds een cachekopie van Hallo-bestand worden gehouden.  Het is belangrijk tooremember dit tijdens het instellen van een bestand time to live.  U kunt een downstream toorequest Hallo meest recente clientversie van uw bestand afdwingen door een unieke naam geven telkens wanneer u deze bijwerken of door gebruik te maken van [query opslaan in cache](cdn-query-string.md).  
> 
> 

Deze zelfstudie leert u het opschonen van de activa van alle knooppunten van de rand van een eindpunt.

## <a name="walkthrough"></a>Walkthrough
1. In Hallo [Azure Portal](https://portal.azure.com), bladeren toohello CDN-profiel met de gewenste toopurge Hallo-eindpunt.
2. Klik op Hallo opschonen knop Hallo CDN-profiel blade.
   
    ![Blade CDN-profiel](./media/cdn-purge-endpoint/cdn-profile-blade.png)
   
    Hallo opschonen blade wordt geopend.
   
    ![Blade CDN-opschonen](./media/cdn-purge-endpoint/cdn-purge-blade.png)
3. Op Hallo opschonen blade, Hallo serviceadres toopurge uit Hallo URL vervolgkeuzelijst wilt selecteren.
   
    ![Formulier opschonen](./media/cdn-purge-endpoint/cdn-purge-form.png)
   
   > [!NOTE]
   > U kunt ook toohello opschonen blade opvragen door te klikken op Hallo **opschonen** knop op de blade Hallo CDN-eindpunt.  In dat geval Hallo **URL** veld worden vooraf ingevuld met het adres van Hallo van dat specifieke eindpunt.
   > 
   > 
4. Selecteer welke activa u wenst toopurge van Hallo edge-knooppunten.  Als u wenst dat tooclear alle activa, klikt u op Hallo **Alles opschonen** selectievakje.  Anders tekst hello pad van elk actief gewenste toopurge in Hallo **pad** textbox. Hieronder indelingen worden ondersteund in Hallo-pad.
    1. **Opschonen van één URL**: individuele asset opschonen door te geven van de volledige URL hello, met of zonder Hallo bestandsextensie, bijvoorbeeld`/pictures/strasbourg.png`;`/pictures/strasbourg`
    2. **Jokertekens opschonen**: sterretje (\*) kan worden gebruikt als een jokerteken. Opschonen van mappen, submappen en bestanden onder een eindpunt met `/*` in pad Hallo of opschonen van alle submappen en bestanden in een specifieke map die door te geven Hallo map gevolgd door `/*`, bijvoorbeeld`/pictures/*`.  Houd er rekening mee dat leegmaken met jokertekens wordt momenteel niet ondersteund door Azure CDN van Akamai. 
    3. **Opschonen van domein hoofdmap**: opschonen Hallo hoofdmap van het Hallo-eindpunt met '/' Hallo-pad.
   
   > [!TIP]
   > Paden moeten worden opgegeven voor opschonen en moet een relatieve URL die voldoen aan de volgende Hallo [reguliere expressie](https://msdn.microsoft.com/library/az24scfc.aspx). **Alles opschonen** en **jokertekens opschonen** niet wordt ondersteund door **Azure CDN van Akamai** momenteel.
   > > Opschonen van één URL`@"^\/(?>(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/?)*)$";`  
   > > Queryreeks`@"^(?:\?[-\@_a-zA-Z0-9\/%:;=!,.\+'&\(\)\u0020]*)?$";`  
   > > Jokertekens opschonen `@"^\/(?:[a-zA-Z0-9-_.%=\(\)\u0020]+\/)*\*$";`. 
   > 
   > Meer **pad** tekstvakken wordt weergegeven nadat u hebt ingevoerd tekst tooallow toobuild een lijst met meerdere elementen.  U kunt activa verwijderen uit de lijst Hallo door te klikken op de knop met het weglatingsteken (...) Hallo.
   > 
5. Klik op Hallo **opschonen** knop.
   
    ![Knop verwijderen](./media/cdn-purge-endpoint/cdn-purge-button.png)

> [!IMPORTANT]
> Opschonen aanvragen nemen ongeveer 2-3 minuten tooprocess met **Azure CDN van Verizon** (standaard en Premium), en ongeveer 7 minuten met **Azure CDN van Akamai**.  Azure CDN heeft een limiet van 50 gelijktijdige aanvragen op elk moment verwijderen. 
> 
> 

## <a name="see-also"></a>Zie ook
* [Vooraf assets op een Azure CDN-eindpunt laden](cdn-preload-endpoint.md)
* [Naslaginformatie over Azure CDN REST-API - opschonen of een eindpunt vooraf laden](https://msdn.microsoft.com/library/mt634451.aspx)

