---
title: aaaAzure Media Services-concepten | Microsoft Docs
description: In dit onderwerp overzicht een van Azure Media Services-concepten
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Azure Media Services-concepten
In dit onderwerp biedt een overzicht van de belangrijkste Media Services-concepten Hallo.

## <a id="assets"></a>Activa en opslag
### <a name="assets"></a>Assets
Een [Asset](https://docs.microsoft.com/rest/api/media/operations/asset) bevat digitale bestanden (inclusief video, audio, afbeeldingen, verzamelingen miniaturen, tekst tekstsporen en ondertitelingsbestanden bestanden) en Hallo metagegevens over deze bestanden. Nadat Hallo digitale bestanden zijn geüpload naar een asset, kunnen deze worden gebruikt in Hallo Media Services-codering en werkstromen streaming.

Een asset is toegewezen tooa blob-container in Azure Storage-account Hallo en Hallo-bestanden in Hallo asset worden opgeslagen als blok-blobs in de container. Pagina-blobs worden niet ondersteund door Azure Media Services.

Wanneer u beslist welke media-inhoud tooupload en opslaan in een asset Hallo overwegingen volgende van toepassing:

* Een asset mag slechts één, unieke exemplaar van media-inhoud bevatten. Bijvoorbeeld, een enkel bewerken van een aflevering TV, film of aankondiging.
* Een asset mag niet meerdere vertoningen of bewerkingen van een bestand met audiovisuele bevatten. Een voorbeeld van een onjuist gebruik van een Asset zou toostore geprobeerd meer dan één TV aflevering, aankondiging of meerdere camerahoeken van een enkele productie binnen een asset. Meerdere vertoningen of wijzigingen van een audiovisuele bestand opslaan in een asset kan leiden tot problemen bij het verzenden van codering taken, streaming en Hallo levering van asset hello later in de werkstroom Hallo beveiligen.  

### <a name="asset-file"></a>Assetbestand
Een [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) vertegenwoordigt een werkelijke video of audio-bestand dat is opgeslagen in een blob-container. Een assetbestand is altijd gekoppeld aan een asset en een asset kan een of veel bestanden bevatten. Hallo Media Services-Encoder taak mislukt als een object van het bestand asset niet gekoppeld aan een digitaal bestand in een blob-container is.

Hallo **AssetFile** exemplaar en de werkelijke mediabestand Hallo zijn twee verschillende objecten. Hallo AssetFile exemplaar bevat metagegevens over mediabestand hello, terwijl het mediabestand Hallo Hallo echte media-inhoud bevat.

U moet niet proberen toochange Hallo inhoud van de blob-containers die zijn gegenereerd door Media Services zonder gebruik van Media Service-API's.

### <a name="asset-encryption-options"></a>Opties voor versleuteling van Assets
Afhankelijk van Hallo type inhoud dat u wilt dat tooupload, opslaan en leveren, Media Services biedt verschillende opties voor codering die u kunt kiezen uit.

>[!NOTE]
>Er wordt geen versleuteling wordt gebruikt. Dit is de standaardwaarde Hallo. Wanneer u deze optie wordt de inhoud is niet beveiligd de overdracht of in rust in de opslag.

Als u van plan toodeliver een MP4 via progressief downloaden bent, gebruikt u deze optie tooupload uw inhoud.

**StorageEncrypted** : Gebruik deze optie tooencrypt uw versleutelde inhoud lokaal met AES 256-bitsversleuteling en upload het tooAzure opslag wordt bewaard in rust versleuteld. Automatisch worden beveiligd met storage encryption activa niet-versleuteld en geplaatst in een versleuteld bestand system eerdere tooencoding en eventueel opnieuw versleutelde voorafgaande toouploading weer als een nieuwe uitvoerasset. Hallo primaire gebruiksvoorbeeld voor versleuteling van opslag is dat u wilt toosecure uw invoer mediabestanden van hoge kwaliteit met sterke versleuteling-op schijf rest. 

In de volgorde toodeliver een gecodeerde asset opslag, moet u beleid voor de levering van Hallo actief configureren zodat Media Services weet hoe u toodeliver uw inhoud wilt. Voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid (bijvoorbeeld, AES, PlayReady of er wordt geen versleuteling). 

**CommonEncryptionProtected** -Gebruik deze optie als u wilt dat tooencrypt (of uploaden die al is versleuteld) inhoud met Common Encryption of PlayReady DRM (bijvoorbeeld Smooth Streaming beveiligd met PlayReady DRM).

**EnvelopeEncryptionProtected** – Gebruik deze optie als u wilt dat tooprotect (of uploaden al beveiligd) HTTP Live Streaming (HLS) versleuteld met Advanced Encryption Standard (AES). Als u al is versleuteld met AES HLS uploadt, moet deze zijn gecodeerd door Transform Manager.

### <a name="access-policy"></a>Beleid voor toegang
Een [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) machtigingen (zoals lezen, schrijven en lijst) en de duur van toegang tooan asset definieert. Normaal zou u een AccessPolicy object tooa locator dan gebruikt tooaccess Hallo bestanden in een asset worden doorgeven.

>[!NOTE]
>Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen, bijvoorbeeld een beleid voor locators die beoogde tooremain aanwezig gedurende een lange periode (niet-upload policies zijn). Raadpleeg [dit](media-services-dotnet-manage-entities.md#limit-access-policies) onderwerp voor meer informatie.

### <a name="blob-container"></a>BLOB-container
Een blob-container is een groepering van een reeks blobs. BLOB-containers worden gebruikt in een Media Services als grens punt voor toegangsbeheer en Shared Access Signature (SAS)-locators op activa. Een Azure Storage-account kan een onbeperkt aantal blob-containers bevatten. Een container kan een onbeperkt aantal blobs bevatten.

>[!NOTE]
> U moet niet proberen toochange Hallo inhoud van de blob-containers die zijn gegenereerd door Media Services zonder gebruik van Media Service-API's.
> 
> 

### <a id="locators"></a>Locators
[Locator](https://docs.microsoft.com/rest/api/media/operations/locator)s bieden een vermelding punt tooaccess Hallo bestanden in een asset. Een toegangsbeleid is gebruikte toodefine Hallo machtigingen en duur dat een client toegang tooa asset gegeven heeft. Locators kunnen een groot aantal tooone relatie hebben met een toegangsbeleid, zoals dat verschillende locators bieden verschillende begintijden en verbinding typen toodifferent clients tijdens het gebruik van alle Hallo dezelfde machtigingen en duur van de instellingen. echter, vanwege een beleid voor gedeelde toegangsbeperking ingesteld met Azure storage-services, er geen meer dan vijf unieke locators die tegelijk zijn gekoppeld aan een bepaalde asset. 

Media Services ondersteunt twee typen locators: OnDemandOrigin-locators, toostream media (bijvoorbeeld MPEG DASH, HLS of Smooth Streaming) gebruikt of progressief downloaden van media en SAS-URL-locators, gebruikte tooupload of downloaden van media-bestanden to\from Azure-opslag. 

>[!NOTE]
>Hallo lijst machtiging (AccessPermissions.List) mag niet worden gebruikt bij het maken van een OnDemandOrigin-locator. 

### <a name="storage-account"></a>Storage-account
Alle toegang tooAzure opslag wordt gedaan via een opslagaccount. Een Media Service-account kunt koppelen aan een of meer opslagaccounts. Een account kan een onbeperkt aantal containers bevatten, zolang de totale grootte onder 500TB per storage-account is.  Media Services SDK niveau tooling tooallow biedt u toomanage meerdere opslagaccounts en de belasting in evenwicht Hallo distributie van uw assets tijdens het uploaden van toothese accounts op basis van metrische gegevens of willekeurige distributie. Voor meer informatie raadpleegt u Working with [Azure Storage](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>Jobs en taken
Een [taak](https://https://docs.microsoft.com/rest/api/media/operations/job) is gewoonlijk gebruikte tooprocess (bijvoorbeeld index of coderen) een audio/video-presentatie. Als u meerdere video's verwerkt, een taak maken voor elke video toobe gecodeerd.

Een taak bevat metagegevens over Hallo verwerking toobe uitgevoerd. Elke taak bevat een of meer [taak](https://docs.microsoft.com/rest/api/media/operations/task)s die een atomic verwerkingstaak in de invoer activa, geef uitvoer activa, een Mediaprocessor en de bijbehorende instellingen. Taken in een job kunnen keten worden samengesteld, waarbij de uitvoerasset Hallo van een taak wordt gegeven als Hallo invoercode asset toohello volgende taak. Op deze manier kan één taak bevatten alle Hallo verwerking nodig is voor een presentatie media.

## <a id="encoding"></a>Codering
Azure Media Services biedt meerdere opties voor het Hallo-codering van media in Hallo cloud.

Wanneer u begint met Media Services, is het belangrijk toounderstand Hallo verschil tussen codecs en bestandsindelingen.
Codecs zijn Hallo-software die Hallo compressie/decompressie algoritmen implementeert dat bestandsindelingen zijn containers waarin Hallo gecomprimeerd video.

Media Services biedt dynamische pakketten zodat u uw adaptive bitrate MP4- of Smooth Streaming inhoud gecodeerde in de streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) toodeliver zonder dat u hoeft toore-pakket in een van deze streaming-indelingen.

tootake profiteren van [dynamische pakketten](media-services-dynamic-packaging-overview.md), u moet tooencode uw tussentijds (bron) bestand in een set adaptive bitrate MP4-bestanden of adaptive bitrate Smooth Streaming-bestanden en hebt u ten minste één standard of premium streaming-eindpunt in de status is gestart.

Media Services ondersteunt Hallo op aanvraag coderingsprogramma's die worden beschreven in dit artikel te volgen:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium Workflow](media-services-encode-asset.md#media-encoder-premium-workflow)

Zie voor meer informatie over ondersteunde coderingsprogramma's [coderingsprogramma's](media-services-encode-asset.md).

## <a name="live-streaming"></a>Live Streaming
In Azure Media Services vertegenwoordigt een kanaal een pijplijn voor het verwerken van live streaming inhoud. Een kanaal ontvangt live invoer gegevensstromen in twee manieren:

* Een on-premises live codering verzendt multi-bitrate RTMP of Smooth Streaming (gefragmenteerde MP4) toohello Channel. U kunt Hallo volgende live coderingsprogramma's die multi-bitrate Smooth Streaming uitvoeren: MediaExcel, Ateme, stel communicatie, Envivio, Cisco en Elemental. Hallo volgende live coderingsprogramma's voeren RTMP: Adobe Flash Live coderingsprogramma, Telestream Wirecast, Teradek, Haivision en Tricaster coderingsprogramma's. Hallo opgenomen streams doorgeven kanalen zonder verdere transcodering en codering. Desgevraagd levert Media Services Hallo stroom toocustomers.
* Een single-bitrate stream (in een Hallo volgende indelingen: RTP (MPEG-TS)), RTMP of Smooth Streaming (gefragmenteerde MP4)) toohello-kanaal dat is ingeschakeld tooperform live codering met Media Services wordt verzonden. Hallo kanaal voert live codering Hallo binnenkomende single-bitrate stream tooa multi-bitrate (adaptieve) videostream. Desgevraagd levert Media Services Hallo stroom toocustomers.

### <a name="channel"></a>Kanaal
In Media Services [kanaal](https://docs.microsoft.com/rest/api/media/operations/channel)s zijn verantwoordelijk voor het verwerken van live streaming inhoud. Een kanaal biedt een invoereindpunt (de URL voor opnemen) vervolgens live transcoder tooa te bieden. Hallo kanaal live invoer gegevensstromen van live transcoder Hallo ontvangt en wordt het beschikbaar gemaakt voor streaming via een of meer streaming-eindpunten. Kanalen bieden ook een preview-eindpunt (preview URL) toopreview te gebruiken en uw stream te valideren voordat verdere verwerking en levering.

U krijgt Hallo URL's en Hallo preview opnemen wanneer u Hallo kanaal hebt gemaakt. tooget deze URL's, Hallo kanaal heeft geen toobe status Hallo gestart. Wanneer u klaar toostart gegevens van een live transcoder in Hallo kanaal worden gepusht bent, moet Hallo kanaal worden gestart. Zodra de live transcoder Hallo ophalen van gegevens start, kunt u uw stream te bekijken.

Elke Media Services-account kan meerdere kanalen, meerdere programma's en meerdere streaming-eindpunten bevatten. Afhankelijk van Hallo bandbreedte en beveiliging behoeften zijn StreamingEndpoint services speciale tooone of meer kanalen. Alle StreamingEndpoint kunt halen uit een kanaal.

### <a name="program-event"></a>Programma (gebeurtenis)
Een [programma (gebeurtenis)](https://docs.microsoft.com/rest/api/media/operations/program) kunt u toocontrol Hallo publiceren en opslaan van segmenten in een live stream. Kanalen beheren programma's (gebeurtenissen). Hallo is kanaal- en programma-relatie vergelijkbaar tootraditional media waarbij een kanaal een constante stream met inhoud heeft en een programma bereik toosome getimede gebeurtenis op dat kanaal.
Kunt u het aantal uren waarop u tooretain Hallo opgenomen inhoud voor Hallo programma door de instelling Hallo Hallo **ArchiveWindowLength** eigenschap. Deze waarde kan worden ingesteld van minimaal 5 minuten tooa maximaal 25 uur.

ArchiveWindowLength bepaalt ook de maximale hoeveelheid tijd die clients terug in tijd vanaf de huidige live positie Hallo zoeken kunnen Hallo. Programma's kunnen uitvoeren in de opgegeven tijdsduur hello, maar de inhoud die achter de lengte van Hallo venster valt, wordt altijd verwijderd. De waarde van deze eigenschap bepaalt ook hoe lang Hallo client manifesten kunnen groeien.

Elk programma (gebeurtenis) is gekoppeld aan een Asset. toopublish hello programma moet u een locator voor Hallo gekoppelde asset. Met deze locator kunt u een streaming-URL die u kunt tooyour clients leveren toobuild.

Een kanaal biedt ondersteuning voor maximaal toothree gelijktijdig actieve programma's, zodat u kunt meerdere archieven van Hallo maken dezelfde binnenkomende stream. Hiermee kunt u toopublish en te archiveren verschillende onderdelen van een gebeurtenis naar behoefte. De vereiste van uw bedrijf is bijvoorbeeld tooarchive zes uur van een programma, maar toobroadcast alleen de laatste tien minuten. tooaccomplish, moet u twee gelijktijdig actieve programma's toocreate. Een programma wordt ingesteld tooarchive zes uur van de gebeurtenis Hallo maar Hallo programma wordt niet gepubliceerd. Hallo andere programma is set tooarchive voor 10 minuten en dit programma is gepubliceerd.

Zie voor meer informatie:

* [Werken met kanalen die zijn ingeschakeld tooPerform Live codering met Azure Media Services](media-services-manage-live-encoder-enabled-channels.md)
* [Werken met kanalen die een multi-bitrate livestream van on-premises encoders ontvangen](media-services-live-streaming-with-onprem-encoders.md)
* [Quota's en beperkingen](media-services-quotas-and-limitations.md).

## <a name="protecting-content"></a>Beschermen van inhoud
### <a name="dynamic-encryption"></a>Dynamische versleuteling
Azure Media Services kunt u toosecure uw media Hallo tijd vanaf uw computer via de opslag, verwerking en levering. Media Services kunt u uw inhoud dynamisch worden versleuteld met Advanced Encryption Standard (AES) (met behulp van 128-bits coderingssleutels) en algemene codering (CENC) met PlayReady en/of Widevine DRM toodeliver. Media Services biedt ook een service voor het leveren van AES-sleutels en PlayReady-licenties tooauthorized clients.

Op dit moment kunt u Hallo volgende streaming-indelingen kunt versleutelen: HLS, MPEG DASH en Smooth Streaming. U kunt progressief downloaden niet coderen.

Als u voor Media Services tooencrypt een asset wilt, kunt u tooassociate een versleutelingssleutel (CommonEncryption of EnvelopeEncryption) moet aan uw asset en autorisatiebeleid voor Hallo sleutel ook configureren.

Als u toostream een gecodeerde asset opslag wilt, moet u beleid voor de levering van Hallo actief in volgorde toospecify configureren hoe u wilt dat toodeliver uw asset.

Wanneer een stream is aangevraagd door een speler, Media Services gebruikt Hallo opgegeven sleutel toodynamically versleutelen van uw inhoud met behulp van een envelop codering (met AES) of de algemene codering (met PlayReady of Widevine). toodecrypt hello stream, Hallo player vraagt de Hallo sleutel van Hallo sleutellevering-service. toodecide of Hallo gebruiker is gemachtigd tooget Hallo sleutel, Hallo service beoordeelt Hallo autorisatiebeleid die u hebt opgegeven voor Hallo-sleutel.

### <a name="token-restriction"></a>Tokenbeperking
Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: open, token beperking of IP-beperking. Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS). Media Services ondersteunt tokens in Hallo Simple Web Tokens (SWT) en JSON Web Token (JWT)-indeling. Media Services biedt geen Token Services beveiligen. U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS tooissue tokens. Hallo STS moet geconfigureerde toocreate token van een ondertekend met Hallo opgegeven sleutel- en claims die u hebt opgegeven in de configuratie van Hallo tokenbeperking. Hallo Media Services sleutellevering service Hallo aangevraagd toohello (of licentiegegevens)-client retourneert als Hallo token geldig is en Hallo claims in Hallo token overeenkomen met die zijn geconfigureerd voor hello (of licentiegegevens).

Wanneer u Hallo token beperkte beleid configureert, kunt u Hallo verificatie van de primaire sleutel, uitgever en doelgroep parameters moet opgeven. Hallo verificatie van de primaire sleutel bevat Hallo key of Hallo-token is ondertekend met, de uitgever Hallo secure token-service die het Hallo-token uitgeeft. Hallo doelgroep (ook wel bereik genoemd) wordt beschreven Hallo bedoeling van Hallo token of Hallo resource Hallo token gemachtigd voor toegang tot. Hallo Media Services-service voor sleutellevering valideert dat deze waarden in Hallo token Hallo-waarden in de sjabloon Hallo overeenkomen.

Zie voor meer informatie Hallo artikelen te volgen:

[Overzicht van de inhoud beveiligen](media-services-content-protection-overview.md)
[beveiligen met AES-128](media-services-protect-with-aes128.md)
[beveiligen met DRM](media-services-protect-with-drm.md)

## <a name="delivering"></a>Leveren
### <a id="dynamic_packaging"></a>Dynamische pakketten
Als u werkt met Media Services, wordt aangeraden tooencode uw tussentijds een adaptive bitrate MP4-bestanden instellen en deze vervolgens converteren Hallo stellen toohello gewenste indeling met behulp van Hallo [dynamische pakketten](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>Streaming-eindpunt
Een StreamingEndpoint vertegenwoordigt een streaming-service die inhoud rechtstreeks tooa player clienttoepassing of tooa inhoud Delivery Network (CDN) voor verdere distributie (Azure Media Services biedt nu hello Azure CDN-integratie.) kunt leveren Hallo uitgaande stroom van een streaming-eindpunt-service kan niet een live stream of een video op aanvraag actief in uw Media Services-account. Media Services-klanten, kiest u een **standaard** streaming-eindpunt of één of meer **Premium** streaming-eindpunten, op basis van tootheir behoeften. Standaard streaming-eindpunt is geschikt voor de meeste streaming belastingen. 

Standard-streaming-eindpunten zijn geschikt voor de meeste streaming-workloads. Standaard Streaming-eindpunten bieden Hallo flexibiliteit toodeliver uw inhoud toovirtually elk apparaat via dynamische pakketten in HLS, MPEG-DASH en Smooth Streaming, evenals een dynamische versleuteling voor Microsoft PlayReady, Google Widevine, Apple Fairplay , en AES128.  Ze ook schalen van zeer kleine toovery grote doelgroepen met duizenden gelijktijdige gebruikers via de integratie van Azure CDN. Als u een geavanceerde werkbelasting of uw streaming capaciteitsvereisten niet passen toostandard streaming-eindpunt doorvoer doelen of gewenste toocontrol Hallo capaciteit van Hallo StreamingEndpoint service toohandle groeiende bandbreedte nodig heeft, wordt het aanbevolen tooallocate-schaaleenheden (ook wel bekend als premium streamingeenheden).

Het is raadzaam toouse dynamische pakketten en/of dynamische versleuteling.

>[!NOTE]
>Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 

Raadpleeg [dit](media-services-portal-manage-streaming-endpoints.md) onderwerp voor meer informatie.

U kunt hebben standaard too2 streaming-eindpunten in uw Media Services-account. Zie voor een hogere limiet toorequest [quota's en beperkingen](media-services-quotas-and-limitations.md).

U wordt alleen gefactureerd als uw StreamingEndpoint wordt uitgevoerd.

### <a name="asset-delivery-policy"></a>Leveringsbeleid voor Assets
Een Hallo stappen in Hallo Media Services van de werkstroom voor contentlevering configureren [leveringsbeleid voor assets ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)dat u wilt dat toobe gestreamd. Hallo-leveringsbeleid voor Assets wordt Media Services uitgelegd hoe u wilt voor uw asset toobe geleverd: in welke streaming protocol moet uw asset worden dynamisch verpakt (voor bijvoorbeeld MPEG DASH, HLS, Smooth Streaming of alle), al dan niet de gewenste toodynamically uw asset coderen en hoe (envelop of common encryption).

Als er een gecodeerde asset opslag voordat uw asset kan worden gestreamd, opgegeven Hallo streaming server verwijdert Hallo-versleuteling voor opslag en stromen inhoud met Hallo leveringsbeleid voor. Bijvoorbeeld: toodeliver uw asset versleuteld met Advanced Encryption Standard (AES) versleutelingssleutel, set Hallo beleid type tooDynamicEnvelopeEncryption. opslagversleuteling tooremove en stroom Hallo asset in Hallo wissen, stel Hallo beleid type tooNoDynamicEncryption.

### <a name="progressive-download"></a>Progressief downloaden
Progressieve download kunt u toostart media afspelen voordat het hele bestand Hallo is gedownload. U kunt een MP4-bestand alleen progressief downloaden.

>[!NOTE]
>U moet versleutelde activa ontsleutelen als u wilt dat ze toobe progressief downloaden.

tooprovide gebruikers met progressieve download-URL's, moet u eerst een OnDemandOrigin-locator maken. Hallo locator, geeft u Hallo base pad toohello asset maken. Vervolgens moet u de naam van de tooappend Hallo van MP4-bestand. Bijvoorbeeld:

http://amstest1.streaming.mediaservices.Windows.NET/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>Streaming-URL 's
Uw inhoud tooclients streaming. tooprovide gebruikers met streaming-URL's, moet u eerst maken een OnDemandOrigin-locator. Maken van Hallo locator, geeft u Hallo base pad toohello asset die u wilt dat toostream Hallo-inhoud bevat. Echter, toobe kunnen toostream deze inhoud hoeft toomodify verder in dit pad. een volledige URL toohello manifestbestand streamen, moet u Hallo-locator pad samenvoegen tooconstruct (filename.ism) naam van waarde en Hallo manifestbestand. Vervolgens append /Manifest en een geschikte indeling (indien nodig) toohello locator-pad.

U kunt ook de inhoud streamen via een SSL-verbinding. toodo, zorg ervoor dat uw streaming URL's starten met HTTPS. Op dit moment ondersteuning AMS geen voor SSL met aangepaste domeinen.  

>[!NOTE]
>U kunt alleen streamen via SSL als Hallo streaming-eindpunt van waaruit u uw inhoud wilt leveren na 10 September 2014 werd gemaakt. Als uw streaming-URL's zijn gebaseerd op Hallo streaming-eindpunten die zijn gemaakt na 10 September, bevat Hallo-URL 'streaming.mediaservices.windows.net' (nieuwe Hallo-indeling). Streaming-URL's die 'origin.mediaservices.windows.net' (oude Hallo-indeling bevatten) bieden geen ondersteuning voor SSL. Als de URL de oude indeling Hallo heeft en toobe kunnen toostream via SSL gewenste, maakt u een nieuwe streaming-eindpunt. URL's die zijn gemaakt op basis van nieuwe streaming-eindpunt toostream uw inhoud via SSL hello gebruiken.

Hallo volgende lijst beschrijft de verschillende streaming-indelingen en worden voorbeelden gegeven:

* Smooth Streaming

{streaming-eindpuntnaam-media services-accountnaam}.streaming.mediaservices.windows.net/{locator-id}/{bestandsnaam}.ism/Manifest

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest

* MPEG DASH

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(Format=MPD-time-csf)

* Apple HTTP Live Streaming (HLS) V4

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(Format=m3u8-aapl)

* Apple HTTP Live Streaming (HLS) V3

{streaming-eindpunt naam media services-account name}.streaming.mediaservices.windows.net/{locator ID}/{filename}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.Windows.NET/fecebb23-46F6-490d-8b70-203e86b0df58/BigBuckBunny.ISM/manifest(Format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

