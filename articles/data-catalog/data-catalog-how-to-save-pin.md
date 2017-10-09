---
title: aaaSave zoekopdrachten en pincode gegevensassets in Azure Data Catalog | Microsoft Docs
description: Hoe tooarticle markeren mogelijkheden in Azure Data Catalog voor het opslaan van gegevensbronnen en gegevensassets voor later gebruik.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Zoekopdrachten en pincode gegevensassets opslaan in Azure Data Catalog
## <a name="introduction"></a>Inleiding
Azure Data Catalog bevat mogelijkheden voor detectie van gegevensbronnen. U kunt snel zoeken en filteren Hallo catalogus toolocate gegevensbronnen en begrijpen van het beoogde gebruik, waardoor het gemakkelijker toofind Hallo juiste gegevens voor Hallo taak op dat moment.

Maar wat gebeurt er als u tooregularly moet werken met Hallo dezelfde gegevens? En wat gebeurt er als u en andere gebruikers regelmatig bij te uw kennis toohello dragen dezelfde gegevensbronnen in de catalogus Hallo? In deze situaties met toorepeatedly probleem Hallo dezelfde zoekacties inefficiënt zijn. Dit is waar opgeslagen zoekopdracht en vastgemaakt gegevensassets kunnen helpen.

## <a name="saved-searches"></a>Opgeslagen zoekopdrachten
Een opgeslagen zoekopdracht in Data Catalog is een definitie van een herbruikbare, per gebruiker zoeken. U kunt een zoekopdracht, zoals zoektermen, labels en andere filters definiëren en vervolgens opslaan. U kunt opnieuw uitvoeren Hallo opgeslagen zoekopdracht definitie hoger tooreturn eventuele gegevensassets die overeenkomen met de zoekcriteria.

### <a name="create-a-saved-search"></a>Maken van een opgeslagen zoekopdracht
een opgeslagen zoekopdracht toocreate Hallo te volgen:
1. Hello Azure Data Catalog, in portal Hallo **huidige zoekopdracht** venster, klikt u op **opslaan**. 

    ![Koppeling van huidige zoekopdracht instellingen opslaan](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Voer de zoekcriteria Hallo tooreuse wilt en klik vervolgens op **opslaan**.

    ![Huidige zoekinstellingen opgeslagen zoeknaam](./media/data-catalog-how-to-save-pin/02-name.png)

3. Wanneer u wordt gevraagd, typt u een naam voor de opgeslagen zoekopdracht Hallo. Kies een naam die zinnig is en die beschrijft Hallo gegevensassets die worden geretourneerd door Hallo zoeken.

### <a name="manage-saved-searches"></a>Opgeslagen zoekopdrachten beheren
Nadat u hebt opgeslagen zoekopdrachten voor een of meer, een **opgeslagen zoekacties** optie wordt weergegeven onder Hallo **huidige zoekopdracht** vak. Wanneer het Hallo-lijst is uitgevouwen, worden alle opgeslagen zoekopdrachten worden weergegeven.

 ![Lijst met opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/03-list.png)

Hallo volgende doen:

* tooexecute een zoekopdracht, selecteert u een opgeslagen zoekopdracht in Hallo-lijst.

* tooview een lijst met opties voor een opgeslagen zoekopdracht, klikt u op Hallo omlaag Pijl volgende toohello zoeknaam.

    ![Opties voor het beheer opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/04-managing.png)

* Selecteer een nieuwe naam voor de zoekopdracht op Hallo opgeslagen tooenter **naam**. Hallo zoeken definitie is niet gewijzigd.

* tooremove hello opgeslagen zoekopdracht uit de lijst, selecteert **verwijderen**, en bevestig vervolgens Hallo verwijdering.

* uw zoekopdracht standaard selecteert toomark Hallo opgeslagen zoekactie **opslaan als standaard**. Als u een 'empty' zoeken op de introductiepagina van hello Azure Data Catalog uitvoert, wordt uw standaard-zoekopdracht wordt uitgevoerd. Bovendien Hallo zoeken die gemarkeerd als Hallo standaardzoekopdracht wordt weergegeven boven Hallo Hallo **opgeslagen zoekacties** lijst.

### <a name="organizational-saved-searches"></a>Organisatie opgeslagen zoekopdrachten
Alle gebruikers in uw organisatie kunt zoekopdrachten voor eigen gebruik opslaan. Data Catalog beheerders kunnen ook gezocht naar alle gebruikers binnen de organisatie Hallo opslaan. Wanneer beheerders een zoekopdracht opslaat, ze worden weergegeven met een **Share binnen Hallo bedrijf** optie. Deze optie shares Hallo opgeslagen zoekactie voor alle gebruikers in de organisatie Hallo selecteren.

 ![Organisatie opgeslagen zoekopdrachten](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Vastgemaakte gegevensassets
U kunt met opgeslagen zoekopdrachten opslaan en opnieuw zoeken definities gebruiken. Hallo-gegevensassets die worden geretourneerd door Hallo zoekopdrachten kunnen worden gewijzigd na verloop van tijd als de inhoud Hallo van Hallo catalogus wijzigen. Wanneer u gegevensassets vastmaken, kunt u expliciet specifieke gegevens activa toomake identificeren ze gemakkelijker tooaccess zonder toouse een zoekopdracht.

Een gegevensasset vastmaken is eenvoudig. tooadd hello gegevens asset tooyour vastgemaakt lijst, klikt u op Hallo **pincode** pictogram. Hallo-pictogram wordt weergegeven in de hoek Hallo van Hallo asset tegel in de weergave tile hello en in de linkerkolom Hallo in de lijstweergave Hallo in hello Azure Data Catalog-portal.

![Hallo-gegevensasset Punaisepictogram](./media/data-catalog-how-to-save-pin/05-pinning.png)

Een gegevensasset losmaken is even eenvoudig. Klik op Hallo **losmaken** pictogram tootoggle Hallo-instelling voor de geselecteerde asset Hallo.

![Hallo-gegevensasset losmaken pictogram](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>Hallo Mijn activa-sectie
Hallo Data Catalog portal introductiepagina bevat een **Mijn activa** sectie waarin de activa van belang toohello huidige gebruiker. Deze sectie bevat zowel vastgemaakt activa en opgeslagen zoekopdrachten.

![Hallo Mijn activa-sectie op Hallo-startpagina](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Samenvatting
Azure Data Catalog bevat mogelijkheden waarmee u gemakkelijker toodiscover Hallo gegevensbronnen die u nodig, zodat u en andere leden van de organisatie kunnen minder tijd nodig voor zoekt gegevens en meer tijd ermee te werken. Opgeslagen zoekopdrachten en vastgemaakt gegevens activa op deze belangrijkste mogelijkheden, bouwen zodat gebruikers de gegevensbronnen die ze met herhaaldelijk werken gemakkelijk kunnen herkennen.
