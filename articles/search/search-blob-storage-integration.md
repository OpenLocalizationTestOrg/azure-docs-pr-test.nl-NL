---
title: aaaAdding Azure Search tooBlob Storage | Microsoft Docs
description: Een index in code met hello Azure Search HTTP REST-API maken.
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Blob-opslag doorzoeken met Azure Search

Zoeken op Hallo verschillende typen inhoud opgeslagen in Azure Blob storage kan een toosolve moeilijk probleem zijn. U kunt echter index en zoeken Hallo inhoud van uw Blobs in een paar muisklikken met behulp van Azure Search. Zoeken in de Blob-opslag is vereist voor het inrichten van een Azure Search-service. Hallo verschillende Servicelimieten en Prijscategorieën van Azure Search kunt u vinden op Hallo [pagina met prijzen](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>Wat is Azure Search?
[Azure Search](https://aka.ms/whatisazsearch) is een search-oplossing waarmee u gemakkelijk voor ontwikkelaars tooadd robuuste zoekopdracht in volledige tekst tooweb en mobiele toepassingen ondervindt. -Service en Azure Search verwijdert Hallo nodig toomanage elke infrastructuur zoeken bij aanbieding een [uptime van 99,9% SLA](https://aka.ms/azuresearchsla).

Met geavanceerde ondersteuning voor talen 56 Azure Search uw inhoud analyseren en taalspecifieke constructies op intelligente wijze verwerkt. Azure Search biedt ook Hallo extra toobuild een uitgebreide zoekervaring voor de gebruiker. Eenvoudige tooadd functies zoals meervoudige navigatie en typeahead zoeksuggesties treffers markeren toouser interfaces met behulp van Azure Search is. toolearn over de functies van Azure Search kunt u lezen Hallo-service [documentatie](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Kraken openen en zoeken door Hallo inhoud van de opmaak van de enterprise-documenten
Met ondersteuning voor [extractie document](https://aka.ms/azsblobindexer) in Azure Blob storage, Azure Search Hallo inhoud van de verschillende bestandstypen die zijn opgeslagen in blobs kunt indexeren:
- PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT bericht (Outlook e-mailberichten)
- HTML
- Bestanden met tekst zonder opmaak

Tekst en metagegevens van deze bestandstypen uitpakken, is het eenvoudig toosearch over meerdere indelingen met een enkele query toofind Hallo meest relevante documenten ongeacht type. Door het Hallo-inhoud en Hallo metagegevens van Microsoft Office-documenten, PDF-bestanden, en e-mailberichten, de mogelijke toobuild een robuuste enterprise inhoudsbeheer-oplossing met behulp van Blob storage en Azure Search indexeren.

## <a name="search-through-your-blob-metadata"></a>Het doorzoeken van de blobmetagegevens
Een veelvoorkomend scenario waarmee u eenvoudig toosort via blobs van elk type inhoud kunt is tooindex Hallo blob aangepaste, door de gebruiker gedefinieerde metagegevens zoals Hallo Systeemeigenschappen voor elk van uw blobs. Op deze manier wordt informatie voor elke blob ongeacht Hallo type document in Hallo blob zodat u eenvoudig kunt sorteren en facet geïndexeerd voor alle inhoud van de Blob-opslag.

[Meer dat informatie over het indexeren van blob-metagegevens.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Zoeken naar afbeelding
Azure Search zoeken in volledige tekst, meervoudige navigatie en sorteren mogelijkheden kunnen worden toegepast toohello metagegevens van de installatiekopieën die zijn opgeslagen in blobs.

Als deze installatiekopieën worden vooraf verwerkt met behulp van Hallo [Computer Vision-API](https://www.microsoft.com/cognitive-services/computer-vision-api) van cognitieve Services van Microsoft, is het mogelijk tooindex Hallo visuele inhoud gevonden in elke installatiekopie inclusief OCR en handschriftherkenning. We werken over het toevoegen van OCR en andere installatiekopie verwerkingscapaciteit direct tooAzure zoeken, als u geïnteresseerd bent in deze mogelijkheden Neem een aanvraag indienen op onze [UserVoice](https://aka.ms/azsuv) of [Stuur ons een e-mail](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Index en zoek via JSON-blobs
Azure Search mag geconfigureerde tooextract gestructureerd inhoud gevonden in de blobs die JSON bevatten. Azure Search kunt lezen JSON-blobs en parseren Hallo gestructureerd inhoud in de juiste velden Hallo van een Azure Search-document. Azure Search kunt ook rekening houden met blobs die een matrix van JSON-objecten bevatten en toewijzen van elk element tooa afzonderlijk Azure Search-document.

Houd er rekening mee dat bij het parseren van JSON kan niet op dit moment worden geconfigureerd via Hallo-portal. [Meer informatie over de JSON parseren in Azure Search.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Snel starten
Azure Search kunt tooblobs rechtstreeks vanuit de Blob-opslag portalblade Hallo worden toegevoegd.

![](./media/search-blob-storage-integration/blob-blade.png)

Een stroom kunt u een bestaande Azure Search-service selecteren of een nieuwe service maken te klikken op de optie 'Azure Search toevoegen' Hallo worden gestart. Als u een nieuwe service maakt, wordt u gaat buiten de portal ervaring uw Storage-account. U moet toore-toohello opslag portalblade navigeren en opnieuw optie Hallo "Azure Search toevoegen", waarin u de bestaande service Hallo kunt selecteren.

### <a name="next-steps"></a>Volgende stappen
Meer informatie over hello Azure Blob Zoekindexeerfunctie in Hallo volledige [documentatie](https://aka.ms/azsblobindexer).
