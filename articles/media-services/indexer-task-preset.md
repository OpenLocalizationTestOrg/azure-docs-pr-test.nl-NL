---
title: aaaTask vooraf voor Azure Media Indexer
description: In dit onderwerp geeft een overzicht van taak vooraf voor Azure Media Indexer.
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Taak vooraf voor Azure Media Indexer

Azure Media Indexer is een Mediaprocessor dat u tooperform Hallo taken te volgen: doorzoekbaar maken van media-bestanden en inhoud, gesloten closed captioning houdt en trefwoorden genereren, index assetbestanden die deel van uw asset uitmaken.

Dit onderwerp wordt beschreven Hallo taak vooraf ingesteld dat u nodig hebt toopass tooyour taak te indexeren. Zie voor een compleet voorbeeld [mediabestanden met Azure Media Indexer indexeren](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>Azure Media Indexer-configuratie-XML

Hallo volgende tabel bevat uitleg over elementen en kenmerken van Hallo configuratie-XML.

|Naam|Require|Beschrijving|
|---|---|---|
|Invoer|De waarde True|Asset-bestanden die u tooindex wilt.<br/>Azure Media Indexer ondersteunt Hallo media-bestandsindelingen te volgen: MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV. <br/><br/>U kunt Hallo bestandsnaam (s) opgeven in Hallo **naam** of **lijst** kenmerk Hallo **invoer** element (zoals hieronder wordt weergegeven). Als u niet welke tooindex asset-bestand opgeeft, wordt het primaire bestand Hallo opgenomen. Als geen assetbestand primaire is ingesteld, wordt de eerste bestand Hallo Hallo invoer actief in geïndexeerd.<br/><br/>tooexplicitly hello asset-bestandsnaam opgeven, doen:<br/>```<input name="TestFile.wmv" />```<br/><br/>U kunt ook meerdere assetbestanden (omhoog too10-bestanden) in één keer index. toodo dit:<br/>-Maak een tekstbestand (manifestbestand) en geef deze extensie .lst.<br/>-Een lijst met alle Hallo asset bestandsnamen toevoegen in het manifestbestand van uw invoer asset toothis.<br/>-Toevoegen (uploaden) thanifest bestand toohello asset.<br/>-Hallo naam opgeven van het manifestbestand Hallo in kenmerk Hallo-invoer.<br/>```<input list="input.lst">```<br/><br/>**Opmerking:** als u meer dan 10 bestanden toohello manifestbestand toevoegt, Hallo indexering taak mislukt met foutcode Hallo 2006.|
|Metagegevens|ONWAAR|Metagegevens voor Hallo opgegeven asset-bestanden.<br/>```<metadata key="..." value="..." />```<br/><br/>U kunt waarden voor vooraf gedefinieerde sleutels opgeven. <br/><br/>Op dit moment worden Hallo na sleutels ondersteund:<br/><br/>**titel** en **beschrijving** -tooupdate Hallo taal model tooimprove spraakherkenning gebruikt.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**gebruikersnaam** en **wachtwoord** : wordt gebruikt voor verificatie bij het downloaden van internet-bestanden via http of https.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Hallo gebruikersnaam en wachtwoord waarden toe te passen tooall media URL's in Hallo invoer manifest.|
|database<br/><br/>Toegevoegd in versie 1.2. Alleen ondersteund Hallo-functie is momenteel spraakherkenning ('ASR').|ONWAAR|Hallo spraakherkenning functie heeft Hallo instellingen sleutels te volgen:<br/><br/>Taal:<br/>-Hallo van natuurlijke taal toobe herkend in multimedia Hallo-bestand.<br/>-Engels en Spaans<br/><br/>CaptionFormats:<br/>-een door puntkomma's gescheiden lijst met Hallo gewenst bijschrift uitvoerindelingen (indien aanwezig)<br/>-ttml; sami; webvtt<br/><br/><br/>GenerateAIB:<br/>-Een Booleaanse vlag die aangeeft of een AIB-bestand (voor gebruik met SQL Server en Hallo klant indexeerfunctie IFilter) vereist is. Zie voor meer informatie, met behulp van AIB bestanden met Azure Media Indexer en SQL Server.<br/>-Waar is; De waarde False<br/><br/>GenerateKeywords:<br/>-Een Booleaanse vlag die aangeeft of een sleutelwoord XML-bestand vereist is.<br/>-Waar is; De waarde False.|

## <a name="azure-media-indexer-configuration-xml-example"></a>Azure Media Indexer configuration XML-voorbeeld

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Volgende stappen

Zie [mediabestanden met Azure Media Indexer indexeren](media-services-index-content.md).

