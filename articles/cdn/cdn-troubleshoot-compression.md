---
title: aaaTroubleshooting bestandscompressie in Azure CDN | Microsoft Docs
description: Problemen oplossen met Azure CDN bestandscompressie.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Problemen met CDN-bestandscompressie oplossen
Dit artikel helpt u problemen oplossen met [CDN bestandscompressie](cdn-improve-performance.md).

Als u meer hulp op elk gewenst moment in dit artikel nodig hebt, kunt u raadplegen hello Azure deskundigen op [hello Azure MSDN en forums Stack Overflow Hallo](https://azure.microsoft.com/support/forums/). U kunt ook kunt u ook een incident voor ondersteuning van Azure bestand. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en klik op **Get Support**.

## <a name="symptom"></a>Symptoom
Compressie voor uw eindpunt is ingeschakeld, maar de bestanden niet-gecomprimeerde worden geretourneerd.

> [!TIP]
> toocheck of de bestanden zijn gecomprimeerd wordt geretourneerd, moet u een hulpprogramma zoals toouse [Fiddler](http://www.telerik.com/fiddler) of uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Selectievakje Hallo HTTP-antwoordheaders geretourneerd met de CDN in de cache opgeslagen inhoud.  Als er een header met de naam is `Content-Encoding` met een waarde van **gzip**, **bzip2**, of **deflate**, uw inhoud wordt gecomprimeerd.
> 
> ![Inhoud-Encoding-header](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Oorzaak
Er zijn verschillende mogelijke oorzaken, inclusief:

* Hallo aangevraagde inhoud is niet in aanmerking komen voor compressie.
* Compressie is niet ingeschakeld voor Hallo bestandstype aangevraagd.
* Hallo HTTP-aanvraag bevat geen aanvragen van een geldige compressietype header.

## <a name="troubleshooting-steps"></a>Stappen voor probleemoplossing
> [!TIP]
> Net als bij het implementeren van nieuwe eindpunten configuratiewijzigingen CDN sommige toopropagate tijd via Hallo-netwerk.  Normaal gesproken worden wijzigingen toegepast binnen 90 minuten.  Als dit Hallo eerst die u compressie voor uw CDN-eindpunt hebt ingesteld, moet u wachten op van 1 tot 2 uur toobe ervoor Hallo compressie-instellingen toohello POP's zijn doorgegeven. 
> 
> 

### <a name="verify-hello-request"></a>Hallo aanvraag controleren
Eerst moet er een snelle controle op Hallo aanvraag doen.  U kunt uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview Hallo-aanvragen worden gedaan.

* Controleer of het Hallo-aanvraag wordt verzonden tooyour eindpunt-URL, `<endpointname>.azureedge.net`, en niet uw oorsprong.
* Controleer of het Hallo-aanvraag bevat een **Accept-Encoding** header en het Hallo-waarde voor deze koptekst bevat **gzip**, **deflate**, of **bzip2** .

> [!NOTE]
> **Azure CDN van Akamai** profielen alleen ondersteuning voor **gzip** codering.
> 
> 

![CDN-aanvraagheaders](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Controleer of de compressie-instellingen (standaard CDN-profiel)
> [!NOTE]
> Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN Standard van Verizon** of **Azure CDN Standard van Akamai** profiel. 
> 
> 

Navigeer tooyour eindpunt in Hallo [Azure-portal](https://portal.azure.com) en klik op Hallo **configureren** knop.

* Controleer of compressie is ingeschakeld.
* Controleer of Hallo MIME-type voor Hallo inhoud toobe gecomprimeerd is opgenomen in de lijst Hallo van gecomprimeerde indelingen.

![CDN compressie-instellingen](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Controleer of de compressie-instellingen (Premium-CDN-profiel)
> [!NOTE]
> Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN Premium van Verizon** profiel.
> 
> 

Navigeer tooyour eindpunt in Hallo [Azure-portal](https://portal.azure.com) en klik op Hallo **beheren** knop.  de aanvullende portal Hello wordt geopend.  Houd de muis boven Hallo **HTTP grote** tabblad en houd de muis boven Hallo **Cache-instellingen** doel.  Klik op **compressie**. 

* Controleer of compressie is ingeschakeld.
* Controleer of Hallo **bestandstypen** lijst bevat een lijst door komma's gescheiden (zonder spaties) met MIME-typen.
* Controleer of Hallo MIME-type voor Hallo inhoud toobe gecomprimeerd is opgenomen in de lijst Hallo van gecomprimeerde indelingen.

![CDN premium compressie-instellingen](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Controleer of het Hallo-inhoud in cache wordt opgeslagen
> [!NOTE]
> Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN van Verizon** profiel (Standard of Premium).
> 
> 

Controleer met ontwikkelhulpprogramma's van uw browser Hallo headers tooensure Hallo responsbestand opgeslagen in de cache in Hallo regio waar deze wordt aangevraagd.

* Controleer de Hallo **Server** antwoordheader.  Hallo-header moet Hallo-indeling hebben **Platform (ID POP-Server)**, zoals in het volgende voorbeeld Hallo.
* Controleer de Hallo **X-Cache** antwoordheader.  Hallo-header moet worden gelezen **bereikt**.  

![CDN-antwoordheaders](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Controleer of het Hallo-bestand voldoet aan de vereiste grootte Hallo
> [!NOTE]
> Deze stap is alleen van toepassing als uw CDN-profiel is een **Azure CDN van Verizon** profiel (Standard of Premium).
> 
> 

toobe in aanmerking komen voor compressie, een bestand moet voldoen aan Hallo volgens de vereisten van de grootte:

* Groter zijn dan 128 bytes.
* Kleiner dan 1 MB.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Controleer Hallo van de aanvraag op de bronserver Hallo voor een **Via** koptekst
Hallo **Via** HTTP-header aangeeft toohello-webserver die Hallo aanvraag wordt doorgegeven via een proxyserver.  Microsoft IIS-webservers standaard antwoorden niet comprimeren wanneer Hallo-aanvraag bevat een **Via** header.  toooverride dit gedrag Hallo volgende uitvoeren:

* **IIS 6**: [ingesteld HcNoCompressionForProxies = 'FALSE' in de eigenschappen van de IIS-Metabase Hallo](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 en hoger**: [zowel **noCompressionForHttp10** en **noCompressionForProxies** tooFalse in de serverconfiguratie Hallo](http://www.iis.net/configreference/system.webserver/httpcompression)

