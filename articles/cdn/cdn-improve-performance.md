---
title: aaaImprove prestaties door het comprimeren van bestanden in Azure CDN | Microsoft Docs
description: Meer informatie over hoe tooimprove bestandsoverdracht snelheid en toeneemt laadprestaties van de pagina door de bestanden in Azure CDN te comprimeren.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: af1cddff-78d8-476b-a9d0-8c2164e4de5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9a1698b6c29233c2e2e6fb17cdd8e919ae8bfa1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="improve-performance-by-compressing-files-in-azure-cdn"></a>De prestaties verbeteren door het comprimeren van bestanden in Azure CDN
Compressie is een eenvoudige en effectieve methode tooimprove bestand overdrachtssnelheid en de pagina load prestaties door het bestand voordat het verkleinen van Hallo-server wordt verzonden. Het verlaagt de bandbreedtekosten en biedt een responsievere ervaring voor uw gebruikers.

Er zijn twee manieren tooenable compressie:

* U kunt compressie inschakelen op uw server oorsprong in dat geval hello CDN passeren Hallo gecomprimeerde bestanden uit en levert tooclients gecomprimeerde bestanden die ze aanvragen.
* U kunt compressie rechtstreeks op CDN randservers, waarin case Hallo CDN comprimeert Hallo van bestanden en dienen ze tooend gebruikers, zelfs als ze niet zijn gecomprimeerd door de bronserver Hallo inschakelen.

> [!IMPORTANT]
> CDN-configuratiewijzigingen sommige toopropagate tijd via Hallo-netwerk.  Voor <b>Azure CDN van Akamai</b> profielen, doorgeven voltooid gewoonlijk in onder één minuut.  Voor <b>Azure CDN van Verizon</b> profielen, meestal ziet u uw wijzigingen toepassen binnen 90 minuten.  Als dit Hallo eerst die u compressie voor uw CDN-eindpunt hebt ingesteld, moet u wachten op van 1 tot 2 uur toobe ervoor Hallo compressie-instellingen zijn doorgegeven toohello POP's voor het oplossen van problemen
> 
> 

## <a name="enabling-compression"></a>Compressie inschakelen
> [!NOTE]
> Hallo categorieën Standard en Premium-CDN bieden dezelfde functionaliteit voor compressie hello, maar hello gebruikersinterface verschilt.  Zie voor meer informatie over de verschillen tussen de lagen Standard en Premium-CDN Hallo [overzicht van Azure CDN](cdn-overview.md).
> 
> 

### <a name="standard-tier"></a>Standaardlaag
> [!NOTE]
> Deze sectie geldt te**Azure CDN Standard van Verizon** en **Azure CDN Standard van Akamai** profielen.
> 
> 

1. Klik op Hallo CDN-eindpunt gewenst toomanage Hallo CDN-profielpagina.
   
    ![CDN-profiel pagina eindpunten](./media/cdn-file-compression/cdn-endpoints.png)
   
    Hallo CDN-eindpunt pagina wordt geopend.
2. Klik op Hallo **configureren** knop.
   
    ![Knop pagina CDN-profiel beheren](./media/cdn-file-compression/cdn-config-btn.png)
   
    Hallo CDN configuratiepagina wordt geopend.
3. Schakel **compressie**.
   
    ![CDN-opties voor compressie](./media/cdn-file-compression/cdn-compress-standard.png)
4. Gebruik de standaardtypen hello, of wijzig Hallo lijst door te verwijderen of toevoegen, bestandstypen.
   
   > [!TIP]
   > Tijdens mogelijk is, wordt het wordt niet aangeraden tooapply compressie toocompressed indelingen, zoals ZIP, MP3, MP4, JPG, enzovoort.
   > 
   > 
5. Wanneer u klaar bent, klikt u op Hallo **opslaan** knop.

### <a name="premium-tier"></a>Premiumlaag
> [!NOTE]
> Deze sectie geldt te**Azure CDN Premium van Verizon** profielen.
> 
> 

1. Klik op Hallo Hallo CDN-profielpagina **beheren** knop.
   
    ![Knop pagina CDN-profiel beheren](./media/cdn-file-compression/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
2. Houd de muis boven Hallo **HTTP grote** tabblad en houd de muis boven Hallo **Cache-instellingen** doel.  Klik op **compressie**.

    ![Compressie bestandsselectie](./media/cdn-file-compression/cdn-compress-select.png)
   
    Opties voor compressie worden weergegeven.
   
    ![Bestandscompressie](./media/cdn-file-compression/cdn-compress-files.png)
3. Compressie inschakelen door te klikken op Hallo **compressie ingeschakeld** keuzerondje.  Voer Hallo MIME-typen gewenste toocompress als een door komma's gescheiden lijst met (zonder spaties) in Hallo **bestandstypen** textbox.
   
   > [!TIP]
   > Tijdens mogelijk is, wordt het wordt niet aangeraden tooapply compressie toocompressed indelingen, zoals ZIP, MP3, MP4, JPG, enzovoort. 
   > 
   > 
4. Wanneer u klaar bent, klikt u op Hallo **Update** knop.

## <a name="compression-rules"></a>Regels voor compressie
Deze tabellen beschrijven Azure CDN compressie gedrag voor elk scenario.

> [!IMPORTANT]
> Voor **Azure CDN van Verizon** (standaard en Premium), alleen in aanmerking komende bestanden zijn gecomprimeerd.  toobe in aanmerking komen voor compressie, een bestand moet:
> 
> * Groter zijn dan 128 bytes.
> * Kleiner dan 1 MB zijn.
> 
> Voor **Azure CDN van Akamai**, alle bestanden in aanmerking komen voor compressie.
> 
> Een bestand moet voor alle Azure CDN-producten, een MIME-type dat is [geconfigureerd voor compressie](#enabling-compression).
> 
> **Azure CDN van Verizon** profielen (standaard en Premium) ondersteuning **gzip** (GNU zip), **deflate**, **bzip2**, of **br** codering (Brotli). Hallo compressie wordt voor het coderen van Brotli alleen aan de rand van het Hallo gedaan. Hallo clientbrowser moet verzenden Hallo-aanvraag voor het coderen van Brotli en Hallo gecomprimeerde asset moet zijn gecomprimeerd Hallo oorsprong zijde eerst. 
>
>**Azure CDN van Akamai** profielen ondersteunen alleen **gzip** codering.
> 
> **Azure CDN van Akamai** eindpunten altijd aanvragen **gzip** gecodeerde bestanden vanuit de oorsprong hello, ongeacht het Hallo-clientaanvraag. 

### <a name="compression-disabled-or-file-is-ineligible-for-compression"></a>Compressie uitgeschakeld of het bestand is niet in aanmerking voor compressie
| Aangevraagde indeling van de client (via de header Accept-Encoding) | In de cache-bestandsindeling | CDN-antwoord toohello client | Opmerkingen |
| --- | --- | --- | --- |
| Gecomprimeerd |Gecomprimeerd |Gecomprimeerd | |
| Gecomprimeerd |Niet-gecomprimeerde |Niet-gecomprimeerde | |
| Gecomprimeerd |Niet in cache |Wel of niet gecomprimeerd |Is afhankelijk van het antwoord van de oorsprong |
| Niet-gecomprimeerde |Gecomprimeerd |Niet-gecomprimeerde | |
| Niet-gecomprimeerde |Niet-gecomprimeerde |Niet-gecomprimeerde | |
| Niet-gecomprimeerde |Niet in cache |Niet-gecomprimeerde | |

### <a name="compression-enabled-and-file-is-eligible-for-compression"></a>Compressie is ingeschakeld en de bestandsnaam komt in aanmerking voor compressie
| Aangevraagde indeling van de client (via de header Accept-Encoding) | In de cache-bestandsindeling | CDN-antwoord toohello client | Opmerkingen |
| --- | --- | --- | --- |
| Gecomprimeerd |Gecomprimeerd |Gecomprimeerd |CDN-transcodes tussen ondersteunde indelingen |
| Gecomprimeerd |Niet-gecomprimeerde |Gecomprimeerd |CDN voert compressie |
| Gecomprimeerd |Niet in cache |Gecomprimeerd |CDN uitvoert compressie als oorsprong niet-gecomprimeerde retourneert.  **Azure CDN van Verizon** geeft niet-gecomprimeerde bestand op de eerste aanvraag Hallo en vervolgens comprimeert Hallo en caches Hallo-bestand voor volgende aanvragen.  Bestanden met `Cache-Control: no-cache` header nooit worden gecomprimeerd. |
| Niet-gecomprimeerde |Gecomprimeerd |Niet-gecomprimeerde |CDN voert decompressie |
| Niet-gecomprimeerde |Niet-gecomprimeerde |Niet-gecomprimeerde | |
| Niet-gecomprimeerde |Niet in cache |Niet-gecomprimeerde | |

## <a name="media-services-cdn-compression"></a>Media Services-CDN-compressie
Voor Media Services CDN ingeschakeld streaming-eindpunten, compressie is standaard ingeschakeld voor Hallo typen inhoud te volgen: vnd.ms-toepassing-sstr + xml, application/dash+xml,application/vnd.apple.mpegurl, toepassing/f4m + xml. U kunt geen in-of uitschakelen compressie voor Hallo typen met behulp van hello Azure-portal vermeld.  

## <a name="see-also"></a>Zie ook
* [Problemen met CDN-bestandscompressie oplossen](cdn-troubleshoot-compression.md)    

