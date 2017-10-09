---
title: Opmerkingen bij de release aaaMedia Services | Microsoft Docs
description: Media Services-Release-opmerkingen
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ca2d7af-1cf0-45fa-9585-3b73f3ee057d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: media
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: c365b1133987267173ec858298c4c6de62744946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-release-notes"></a>Azure Media Services release-opmerkingen
Deze releaseopmerkingen geven een overzicht van wijzigingen van vorige versies en bekende problemen.

> [!NOTE]
> We willen toohear van onze klanten en zich richten op het oplossen van problemen die gevolgen hebben voor u. tooreport een probleem of vragen hebt, boek in Hallo [Azure Media Services MSDN-Forum].
> 
> 

## <a id="issues"></a>Bekende problemen
### <a id="general_issues"></a>Media Services-algemene problemen
| Probleem | Beschrijving |
| --- | --- |
| Enkele veelvoorkomende HTTP-headers zijn niet opgegeven in Hallo REST-API. |Als u Media Services toepassingen met Hallo REST-API ontwikkelen, vindt u dat een aantal veelvoorkomende HTTP-header-velden (met inbegrip van CLIENT-REQUEST-ID REQUEST-ID en RETURN-CLIENT-REQUEST-ID) worden niet ondersteund. Hallo-headers worden toegevoegd in een toekomstige update. |
| Percentage codering is niet toegestaan. |Media Services gebruikt Hallo-waarde van Hallo IAssetFile.Name eigenschap tijdens het bouwen van URL's voor Hallo streaming-inhoud (bijvoorbeeld http://{AMSAccount}.origin.mediaservices.windows.net/{GUID}/{IAssetFile.Name}/streamingParameters.) Om deze reden is procent codering niet toegestaan. waarde van Hallo Hallo **naam** eigenschap kan niet een van de volgende Hallo hebben [procent-encoding-gereserveerde tekens](http://en.wikipedia.org/wiki/Percent-encoding#Percent-encoding_reserved_characters):! *' ();: @& = + $, /? % # [] '. Bovendien kunnen alleen er een '.' Hallo bestandsnaamextensie. |
| Hallo ListBlobs-methode die deel uitmaakt van hello Azure-opslag-SDK versie 3.x is mislukt. |Media Services genereert een SAS-URL's op basis van Hallo [2012-02-12](https://docs.microsoft.com/rest/api/storageservices/Version-2012-02-12) versie. Als u toouse Azure-opslag-SDK toolist blobs in een blobcontainer wilt, gebruikt u Hallo [CloudBlobContainer.ListBlobs](http://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.listblobs.aspx) methode die deel uitmaakt van de versie van de Azure-opslag-SDK 2.x. Hallo ListBlobs-methode die deel uitmaakt van hello Azure-opslag-SDK versie 3.x zal mislukken. |
| Media Services mechanisme beperking beperkt Hallo Resourcegebruik voor toepassingen die overmatige aanvraag toohello service maken. Hallo-service mogelijk Hallo Service niet beschikbaar (503) HTTP-statuscode geretourneerd. |Zie voor meer informatie, Hallo beschrijving van het HTTP-statuscode Hallo 503 in Hallo [Azure Media Services-foutcodes](media-services-encoding-error-codes.md) onderwerp. |
| Tijdens het opvragen van entiteiten, moet u er een limiet van 1000 entiteiten in één keer wordt geretourneerd omdat openbare REST v2 queryresultaten resultaten too1000 beperkt is. |U moet toouse **overslaan** en **nemen** (.NET) / **boven** (REST) zoals beschreven in [in dit voorbeeld .NET](media-services-dotnet-manage-entities.md#enumerating-through-large-collections-of-entities) en [deze REST-API voorbeeld](media-services-rest-manage-entities.md#enumerating-through-large-collections-of-entities). |
| Sommige clients kunnen worden geleverd via een probleem herhaaldelijk tag in Hallo Smooth Streaming manifest. |Zie [deze](media-services-deliver-content-overview.md#known-issues) sectie voor meer informatie. |
| Azure Media Services .NET SDK objecten kunnen niet worden geserialiseerd en als gevolg hiervan niet werken met Azure cache. |Als u tooserialize Hallo SDK AssetCollection object tooadd probeert deze tooAzure opslaan in cache, een uitzondering gegenereerd. |
| Codering taken mislukken met een tekenreeks voor het bericht ' fase: DownloadFile. Code: System.NullReferenceException '. |Hallo typische codering werkstroom is tooupload invoer video bestand(en) tooan Asset invoeren, en het verzenden van een of meer codering taken voor die Asset, zonder verdere wijzigen die invoer Asset invoer. Echter, als u wijzigt Hallo invoer Asset (bijvoorbeeld door bestanden toevoegen/verwijderen/wijzigen binnen Hallo Asset) en klik vervolgens latere taken mislukken met een DownloadFile-fout. tijdelijke oplossing Hallo is toodelete Hallo invoer Asset en opnieuw uploaden bestand(en) tooa invoer nieuwe Asset. |

## <a id="rest_version_history"></a>Geschiedenis van de REST-API-versie
Zie voor meer informatie over Hallo versiegeschiedenis van REST-API voor Media Services [Azure Media Services REST API-verwijzing].

## <a name="june-2017-release"></a>Release van juni 2017

Ondersteunt nu het Media Services [Azure Active Directory (Azure AD)-gebaseerde verificatie](media-services-use-aad-auth-to-access-ams-api.md).

> [!IMPORTANT]
> Media Services ondersteunt momenteel hello Azure Access Control-servicemodel voor verificatie. Access Control-autorisatie wordt echter op 1 juni 2018 afgeschaft. U wordt aangeraden toohello Azure AD authentication model zo snel mogelijk te migreren.

## <a name="march-2017-release"></a>Maart 2017 Release

U kunt nu gebruiken Azure Media Standard te[automatisch genereren een ladder bitrate](media-services-autogen-bitrate-ladder-with-mes.md) door te geven 'Adaptief streamen' hello voorinstelling tekenreeks bij het maken van een taak die voor codering. 'Adaptieve Streaming' is Hallo aanbevolen voorinstelling als u wilt dat een video tooencode voor streaming met Media Services. Als u een codering voorinstelling toocustomize voor uw specifieke scenario nodig hebt, kunt u beginnen met [deze](media-services-mes-presets-overview.md) standaardinstellingen.

U kunt nu gebruiken Azure Media Standard of Media Encoder Premium werkstroom te[een codering taak maken die wordt gegenereerd fMP4 segmenten](media-services-generate-fmp4-chunks.md). 


## <a name="febuary-2017-release"></a>Februari 2017 Release

Vanaf 1 April 2017 worden elke record taak in uw account ouder is dan 90 dagen, automatisch verwijderd, samen met de bijbehorende records van de taak zelfs als Hallo kunt u het totale aantal records lager dan de maximumquotum Hallo is. Als u tooarchive Hallo projecttaak/informatie nodig hebt, kunt u Hallo code beschreven [hier](media-services-dotnet-manage-entities.md).

## <a name="january-2017-release"></a>Januari 2017 Release

In Microsoft Azure Media Services (AMS), een **Streaming-eindpunt** vertegenwoordigt een streaming-service die inhoud rechtstreeks tooa player clienttoepassing of tooa inhoud Delivery Network (CDN) voor verdere distributie kunt leveren. Media Services biedt ook naadloze integratie van Azure CDN. Hallo uitgaande stroom van een service StreamingEndpoint mag een live stream, video op aanvraag of progressief downloaden van de activa in uw Media Services-account. Elke Azure Media Services-account bevat standaard StreamingEndpoint. Aanvullende streaming-eindpunten kunnen worden gemaakt onder Hallo-account. Er zijn twee versies van streaming-eindpunten, 1.0 en 2.0. Vanaf januari 10 2017, bevatten nieuwe accounts AMS versie 2.0 **standaard** StreamingEndpoint. Aanvullende streaming-eindpunten dat u toothis account toevoegt, worden ook versie 2.0. Deze wijziging heeft geen invloed op bestaande accounts Hallo; bestaande streaming-eindpunten versie 1.0 zijn en mag de bijgewerkte tooversion 2.0. Met deze wijziging zal er wijzigingen in gedrag, facturering en functie (Zie voor meer informatie [dit](media-services-streaming-endpoints-overview.md) onderwerp).

Bovendien vanaf Hallo 2.15 versie bij Azure Media Services Hallo eigenschappen toohello Streaming-eindpunt entiteit volgende toegevoegd: **CdnProvider**, **CdnProfile**,  **FreeTrialEndTime**, **StreamingEndpointVersion**. Zie voor een gedetailleerd overzicht van deze eigenschappen [dit](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint). 

## <a name="december-2016-release"></a>2016 december Release

Azure Media Services kunt u nu tooaccess telemetrie/metrische gegevens voor de services. Hallo huidige versie van AMS kunt u het verzamelen van telemetriegegevens voor live kanaal StreamingEndpoint, en live archief entiteiten. Raadpleeg [dit](media-services-telemetry-overview.md) onderwerp voor meer informatie.

## <a id="july_changes16"></a>Release van juli 2016
### <a name="updates-toomanifest-file-ism-generated-by-encoding-tasks"></a>Updates toomanifest bestand (*. ISM) die worden gegenereerd door de codering van taken
Wanneer een taak die voor codering ingediende tooMedia Encoder Standard of Azure Media Encoder, Hallo codering taak genereert een [streaming manifestbestand](media-services-deliver-content-overview.md) (* ISM) bestand in Hallo uitvoer Asset. Met het meest recente servicerelease hello, is Hallo syntaxis van deze streaming manifestbestand bijgewerkt.

> [!NOTE]
> Hallo-syntaxis Hallo streaming-manifest (ISM)-bestand is gereserveerd voor intern gebruik en is onderwerp toochange in toekomstige releases. Neem geen wijzigen of Hallo inhoud van dit bestand bewerken.
> 
> 

### <a name="a-new-client-manifest-ismc-file-is-generated-in-hello-output-asset-when-an-encoding-task-outputs-one-or-more-mp4-files"></a>Een nieuwe client-manifest (*. ISMC)-bestand is gegenereerd in Hallo Asset uitgevoerd als er een taak die voor codering levert een of meer MP4-bestanden
Beginnen met het meest recente servicerelease hello, na voltooiing van een taak die voor codering die één meer MP4-bestanden, genereert Hallo uitvoer Hallo dat Asset bevat ook een streaming bestand van de client-manifest (*.ismc). Hallo .ismc bestand verbetert de prestaties van dynamische streaming Hallo. 

> [!NOTE]
> Hallo-syntaxis van Hallo client-manifest (.ismc)-bestand is gereserveerd voor intern gebruik, en is onderwerp toochange in toekomstige releases. Neem geen wijzigen of Hallo inhoud van dit bestand bewerken.
> 
> 

Zie voor meer informatie [dit](https://blogs.msdn.microsoft.com/randomnumber/2016/07/08/encoder-changes-within-azure-media-services-now-create-ismc-file/) blog.

### <a name="known-issues"></a>Bekende problemen
Sommige clients kunnen worden geleverd via een probleem herhaaldelijk tag in Hallo Smooth Streaming manifest. Zie [deze](media-services-deliver-content-overview.md#known-issues) sectie voor meer informatie.

## <a id="apr_changes16"></a>Release van april 2016
### <a name="azure-media-analytics"></a>Azure Media Analytics
Azure Media Analytics Azure Media Servces geïntroduceerd voor krachtige video intelligence. Zie voor gedetailleerde informatie [overzicht van Azure Media Services Analytics](media-services-analytics-overview.md).

### <a name="apple-fairplay-preview"></a>Apple FairPlay (Preview)
Azure Media Services nu kunt u toodynamically versleutelen van uw HTTP Live Streaming (HLS) met Apple FairPlay inhoud. U kunt ook AMS licentie delivery service toodeliver FairPlay-licenties tooclients gebruiken. Voor meer informatie gedetailleerde, Zie [gebruik Azure Media Services tooStream uw HLS inhoud beveiligd met Apple FairPlay ](media-services-protect-hls-with-fairplay.md).

## <a id="feb_changes16"></a>Februari 2016-Release
Hallo meest recente versie van Azure Media Services SDK voor .NET (3.5.3) bevat een Widevine gerelateerde fout-oplossing. Hallo-probleem is: AssetDeliveryPolicy kan niet opnieuw worden gebruikt voor meerdere activa versleuteld met Widevine. Als onderdeel van deze oplossingen fix Hallo eigenschap volgende is toegevoegd toohello SDK: **WidevineBaseLicenseAcquisitionUrl**.

    Dictionary<AssetDeliveryPolicyConfigurationKey, string> assetDeliveryPolicyConfiguration =
        new Dictionary<AssetDeliveryPolicyConfigurationKey, string>
    {
        {AssetDeliveryPolicyConfigurationKey.WidevineBaseLicenseAcquisitionUrl,"http://testurl"},

    };

## <a id="jan_changes_16"></a>Januari 2016-Release
De naam van de codering gereserveerde eenheden gewijzigd tooreduce verwarring met namen van de Encoder.

Hallo Basic, Standard en Premium codering gereserveerde eenheden zijn gewijzigd tooS1, S2 en S3 gereserveerde eenheden, respectievelijk.  Klanten die gebruikmaken van eenvoudige codering RUs vandaag S1 zien als Hallo label in Azure-Portal (en in Hallo factuur) tijdens het Standard en Premium Zie Hallo labels S2 en S3 respectievelijk. 

## <a id="dec_changes_15"></a>Release van december 2015

### <a name="azure-media-encoder-deprecation-announcement"></a>Azure Media Encoder afschaffing aankondiging

Azure Media Encoder afgeschaft vanaf ongeveer 12 maanden na de release Hallo van Media Encoder Standard.

### <a name="azure-sdk-for-php"></a>Azure SDK voor PHP
Hello Azure SDK team gepubliceerd een nieuwe versie van Hallo [Azure SDK voor PHP](http://github.com/Azure/azure-sdk-for-php) pakket met updates en nieuwe functies voor Microsoft Azure Media Services. In het bijzonder hello Azure Media Services SDK voor PHP nu ondersteunt het meest recente Hallo [content protection](media-services-content-protection-overview.md) functies: dynamische versleuteling met AES en DRM (PlayReady en Widevine) met en zonder beperking Token. Het ondersteunt ook schalen [Coderingseenheden](media-services-dotnet-encoding-units.md).

Zie voor meer informatie:

* Hallo [Microsoft Azure Media Services SDK voor PHP](http://southworks.com/blog/2015/12/09/new-microsoft-azure-media-services-sdk-for-php-release-available-with-new-features-and-samples/) blog.
* Hallo volgende [codevoorbeelden](http://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices) toohelp kunt u snel aan de slag:
  * **vodworkflow_aes.php**: dit is een PHP-bestand dat toont hoe toouse dynamische AES-128-versleuteling en de Service voor het leveren van sleutel. Deze is gebaseerd op Hallo .NET voorbeeld uitgelegd in [dit](media-services-protect-with-aes128.md) artikel.
  * **vodworkflow_aes.php**: dit is een PHP-bestand dat toont hoe toouse PlayReady dynamische versleuteling en de Service voor het leveren van licenties. Deze is gebaseerd op Hallo .NET voorbeeld uitgelegd in [dit](media-services-protect-with-drm.md) artikel.
  * **scale_encoding_units.php**: dit is een PHP-bestand dat toont hoe eenheid codering tooscale gereserveerd.

## <a id="nov_changes_15"></a>Release van november 2015
Azure Media Services biedt nu Google Widevine-licentieservice voor het leveren in Hallo cloud. Voor meer informatie raadpleegt u te[deze aankondiging blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/). Zie ook [in deze zelfstudie](media-services-protect-with-drm.md) en [GitHub-opslagplaats](http://github.com/Azure-Samples/media-services-dotnet-dynamic-encryption-with-drm). 

Houd er rekening mee dat Widevine-licentie levering van services geleverd door de Azure Media Services wordt uitgevoerd in preview. Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/announcing-google-widevine-license-delivery-services-public-preview-in-azure-media-services/).

## <a id="oct_changes_15"></a>Release van oktober 2015
Azure Media Services (AMS) is nu live in Hallo volgende datacenters: Brazilië-Zuid, India-West, Zuid-India en India, midden. U kunt nu hello Azure-portal te gebruiken[Media Service-accounts maken](media-services-portal-create-account.md) en uitvoeren van verschillende taken die worden beschreven [hier](https://azure.microsoft.com/documentation/services/media-services/). Live Encoding is echter niet ingeschakeld in deze datacenters. Bovendien zijn niet alle soorten gereserveerde coderingseenheden beschikbaar in deze datacenters.

* Brazilië - zuid: alleen standaard en eenvoudige gereserveerde coderingseenheden zijn beschikbaar
* India, westen; Zuid-India en India, midden: alleen eenvoudige gereserveerde coderingseenheden zijn beschikbaar

## <a id="september_changes_15"></a>Release van september 2015
* AMS nu aanbiedingen Hallo mogelijkheid tooprotect zowel Video-On-Demand (VOD) en Live gegevensstromen met Widevine modulaire DRM-technologie. Kunt u Hallo levering van services partners toohelp u leveren met Widevine-licenties te volgen: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/). Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/).
  
    U kunt [AMS .NET SDK](https://www.nuget.org/packages/windowsazure.mediaservices/) (te beginnen met Hallo versie 3.5.1) of REST-API tooconfigure uw AssetDeliveryConfiguration toouse Widevine.  
* AMS is ondersteuning toegevoegd voor Apple ProRes video's. U kunt nu uw QuickTime video's bronbestanden die gebruikmaken van Apple ProRes of andere codecs uploaden. Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/announcing-support-for-apple-prores-videos-in-azure-media-services/).
* U kunt nu Media Encoder Standard toodo subplan knipsel en live archief extractie gebruiken. Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/sub-clipping-and-live-archive-extraction-with-media-encoder-standard/).
* Hallo na filtering updates zijn aangebracht: 
  
  * Nu kunt u Apple HTTP Live Streaming (HLS)-indeling gebruiken met alleen audio-filter. Deze update kunt u tooremove alleen audio bijhouden door te geven (alleen audio = false) in Hallo-URL.
  * Wanneer u filters voor uw assets definieert, hebt u nu de mogelijkheid toocombine meerdere (up-to-date too3) in één URL filtert.
    
    Zie voor meer informatie [dit](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.
* AMS ondersteunt nu ik-Frames in HLS v4. Ik-Frame ondersteuning optimaliseert vooruit- of terugspoelen bewerkingen. Standaard zijn alle HLS v4 uitvoerwaarden I-Frame afspeellijst (EXT-X-I-FRAME-STREAM-INF).
  
    Zie voor meer informatie [dit](https://azure.microsoft.com/blog/azure-media-services-release-dynamic-manifest-composition-remove-hls-audio-only-track-and-hls-i-frame-track-support/) blog.

## <a id="august_changes_15"></a>Augustus 2015-Release
* Azure Media Services SDK voor Java V0.8.0 release en de nieuwe samples zijn nu beschikbaar. Zie voor meer informatie:
  
  * [Blogbericht](http://southworks.com/blog/2015/08/25/microsoft-azure-media-services-sdk-for-java-v0-8-0-released-and-new-samples-available/)
  * [Java-voorbeelden opslagplaats](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
* Azure Media Player-update met ondersteuning voor meerdere audiostroom. Zie voor meer informatie:
  * [Blogbericht](https://azure.microsoft.com/blog/2015/08/13/azure-media-player-update-with-multi-audio-stream-support/)

## <a id="july_changes_15"></a>Release van juli 2015
* Kondigt Hallo algemene beschikbaarheid van Media Encoder Standard. Zie voor meer informatie [dit blogbericht](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/).
  
    Media Encoder Standard maakt gebruik van standaardinstellingen die zijn beschreven in [dit](http://go.microsoft.com/fwlink/?LinkId=618336) sectie. Houd er rekening mee dat wanneer u een definitie voor 4k codeert, u Hallo krijgt **Premium** eenheidstype gereserveerd. Zie voor meer informatie [hoe tooScale codering](media-services-scale-media-processing-overview.md).
* Live realtime bijschriften met Azure Media Services en Player. Zie voor meer informatie [dit blogbericht](https://azure.microsoft.com/blog/2015/07/08/live-real-time-captions-with-azure-media-services-and-player/)

### <a name="media-services-net-sdk-updates"></a>Media Services .NET SDK-Updates
Azure Media Services .NET SDK is nu versie 3.4.0.0. Hallo volgende functionaliteit is in deze release toegevoegd:  

* Geïmplementeerde ondersteuning voor live archivering. Houd er rekening mee dat u een asset die een live-archief bevat niet downloaden.
* Geïmplementeerde ondersteuning voor dynamische filters.
* Geïmplementeerde functionaliteit waarmee gebruikers tookeep storage-container tijdens het verwijderen van de asset.
* Oplossingen voor problemen die betrekking tooretry beleidsregels in kanalen.
* Ingeschakeld **Media Encoder Premium werkstroom**.

## <a id="june_changes_15"></a>Release van juni 2015
### <a name="media-services-net-sdk-updates"></a>Media Services .NET SDK-Updates
Azure Media Services .NET SDK is nu versie 3.3.0.0. Hallo volgende functionaliteit is in deze release toegevoegd:  

* ondersteuning voor detectie van OpenId Connect-specificatie
* ondersteuning voor het verwerken van sleutels rollover identiteit provider zijde. 

Als u een id-provider waarmee OpenID Connect discovery-document (als Hallo volgende providers doen: Azure Active Directory, Google, Salesforce), kunt u opdracht geven Azure Media Services tooobtain ondertekeningssleutels voor de validatie van JWT-token van OpenID connect detectie-specificatie. 

Zie voor meer informatie [met behulp van Json Web sleutels van OpenID Connect detectie spec toowork met JWT-token verificatie in Azure Media Services](http://gtrifonov.com/2015/06/07/using-json-web-keys-from-openid-connect-discovery-spec-to-work-with-jwt-token-authentication-in-azure-media-services/).

## <a id="may_changes_15"></a>Release van mei 2015
Aankondiging Hallo volgende nieuwe functies:

* [Een voorbeeld van Live codering met Media Services](media-services-manage-live-encoder-enabled-channels.md)
* [Dynamische manifest](media-services-dynamic-manifest-overview.md)
* [Een voorbeeld van Azure Media Hyperlapse media-processor](https://azure.microsoft.com/blog/?p=286281&preview=1&_ppp=61e1a0b3db)

## <a id="april_changes_15"></a>Release van april 2015
### <a name="general-media-services-updates"></a>Algemene Media Services-Updates
* [Aankondiging van Azure MediaPlayer](https://azure.microsoft.com/blog/2015/04/15/announcing-azure-media-player/).
* Beginnen met Media Services REST 2.10, kanalen die geconfigureerd tooingest een RTMP-protocol zijn worden gemaakt met de primaire en secundaire URL's voor opnemen. Zie voor meer informatie [kanaal configuraties opnemen](media-services-live-streaming-with-onprem-encoders.md#channel_input)
* Azure Media Indexer-updates
* Ondersteuning voor Spaans
* Nieuwe configuratie-XML-indeling

Zie voor meer informatie [deze blog](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

### <a name="media-services-net-sdk-updates"></a>Media Services .NET SDK-Updates
Azure Media Services .NET SDK is nu versie 3.2.0.0.

Hallo Hieronder volgen enkele Hallo klantgerichte-updates:

* **Wijziging op te splitsen**: gewijzigd **TokenRestrictionTemplate.Issuer** en **TokenRestrictionTemplate.Audience** toobe van een type string.
* Updates gerelateerd toocreating aangepaste opnieuw beleidsregels.
* Oplossingen voor problemen gerelateerde toouploading/downloaden van bestanden.
* Hallo **MediaServicesCredentials** klasse accepteert nu de primaire en secundaire access control-eindpunt tooauthenticate tegen.

## <a id="march_changes_15"></a>Release van maart 2015
### <a name="general-media-services-updates"></a>Algemene Media Services-Updates
* Media Services biedt nu de integratie van Azure CDN. toosupport Hallo-integratie hello **CdnEnabled** eigenschap is toegevoegd, te**StreamingEndpoint**.  **CdnEnabled** kan worden gebruikt met de REST-API's vanaf versie 2.9 (Zie voor meer informatie [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint)).  **CdnEnabled** kan worden gebruikt met .NET SDK vanaf versie 3.1.0.2 (Zie voor meer informatie [StreamingEndpoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.istreamingendpoint\(v=azure.10\).aspx)).
* Aankondiging van **Media Encoder Premium werkstroom**. Zie voor meer informatie [Introducing Premium codering in Azure Media Services](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/).

## <a id="february_changes_15"></a>Februari 2015-Release
### <a name="general-media-services-updates"></a>Algemene Media Services-Updates
Media Services REST-API is nu versie 2.9. Vanaf deze versie, kunt u hello Azure CDN-integratie met streaming-eindpunten inschakelen. Zie voor meer informatie [StreamingEndpoint](https://msdn.microsoft.com/library/dn783468.aspx).

## <a id="january_changes_15"></a>Release van januari 2015
### <a name="general-media-services-updates"></a>Algemene Media Services-Updates
Aankondiging van algemene beschikbaarheid (GA) van de beveiliging van inhoud met dynamische versleuteling. Zie voor meer informatie [Azure Media Services verbetert de streaming-beveiliging met algemene beschikbaarheid van DRM technologie](https://azure.microsoft.com/blog/2015/01/29/azure-media-services-enhances-streaming-security-with-general-availability-of-drm-technology/).

### <a name="media-services-net-sdk-updates"></a>Media Services .NET SDK-Updates
Azure Media Services .NET SDK is nu versie 3.1.0.1.

Deze release Hallo standaardconstructor Microsoft.WindowsAzure.MediaServices.Client.ContentKeyAuthorization.TokenRestrictionTemplate als verouderd gemarkeerd. nieuwe constructor Hallo duurt TokenType als argument.

    TokenRestrictionTemplate template = new TokenRestrictionTemplate(TokenType.SWT);


## <a id="december_changes_14"></a>December 2014-Release
### <a name="general-media-services-updates"></a>Algemene Media Services-Updates
* Sommige updates en nieuwe functies zijn toohello Azure indexeerfunctie Mediaprocessor toegevoegd. Zie voor meer informatie [opmerkingen bij de Release van Azure Media Indexer versie 1.1.6.7](https://azure.microsoft.com/blog/2014/12/03/azure-media-indexer-version-1-1-6-7-release-notes/).
* Een nieuwe REST-API waarmee u tooupdate gereserveerde basiseenheden codering toegevoegd: [EncodingReservedUnitType met REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype).
* Toegevoegde CORS-ondersteuning voor de van sleutel-leveringsservice.
* Verbeterde prestaties van query's op autorisatie beleidsopties zijn uitgevoerd.
* Hallo in China datacentrum [levering van de URL van Key](https://docs.microsoft.com/rest/api/media/operations/contentkey#get_delivery_service_url) is nu per klant (net als in andere datacenters).
* Toegevoegde HLS automatisch doel duur. Bij het uitvoeren van live streamen, wordt dynamisch HLS altijd geleverd. Standaard berekend automatisch HLS segment verpakking verhouding (FragmentsPerSegment) op basis van Hallo keyframe interval (KeyFrameInterval), ook wel aangeduid tooas groep afbeeldingen – GOP die worden ontvangen van het Live coderingsprogramma Hallo Media Services. Zie voor meer informatie [werken met Azure Media Services Live Streaming].

### <a name="media-services-net-sdk-updates"></a>Media Services .NET SDK-Updates
* [Azure Media Services .NET SDK](http://www.nuget.org/packages/windowsazure.mediaservices/) is nu versie 3.1.0.0.
* Bijgewerkt Hallo .net SDK afhankelijkheid too.NET 4.5 Framework.
* Een nieuwe API waarmee u tooupdate gereserveerde basiseenheden codering toegevoegd. Zie voor meer informatie [gereserveerde eenheidstype bijwerken en codering RUs verhogen met .NET](media-services-dotnet-encoding-units.md).
* Toegevoegde JWT (JSON Web Token) ondersteuning voor token-authenticatie. Zie voor meer informatie [JWT-token verificatie in Azure Media Services en dynamische versleuteling](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).
* Toegevoegde relatieve verschuivingen voor BeginDate en ExpirationDate in Hallo PlayReady licentiesjabloon.

## <a id="november_changes_14"></a>Release van november 2014
* Media Services kunt u nu een live Smooth Streaming (FMP4) inhoud tooingest via een SSL-verbinding. tooingest via SSL, zorg ervoor dat tooupdate hello tooHTTPS URL voor opnemen.  Houd er rekening mee dat op dit moment AMS biedt geen ondersteuning voor SSL met aangepaste domeinen.  Zie voor meer informatie over live streamen [werken met Azure Media Services Live Streaming].
* U kan niet op dit moment een live stream RTMP opnemen via een SSL-verbinding.
* U kunt alleen streamen via SSL als Hallo streaming-eindpunt van waaruit u uw inhoud wilt leveren na 10 September 2014 werd gemaakt. Als uw streaming-URL's zijn gebaseerd op Hallo streaming-eindpunten die zijn gemaakt na 10 September, bevat Hallo-URL 'streaming.mediaservices.windows.net' (nieuwe Hallo-indeling). Streaming-URL's die 'origin.mediaservices.windows.net' (oude Hallo-indeling bevatten) bieden geen ondersteuning voor SSL. Als uw URL in de oude indeling Hallo is en toobe kunnen toostream via SSL gewenste, [maken van een nieuwe streaming-eindpunt](media-services-portal-manage-streaming-endpoints.md). URL's die zijn gemaakt op basis van nieuwe streaming-eindpunt toostream uw inhoud via SSL hello gebruiken.

## <a id="october_changes_14"></a>Release van oktober 2014
### <a id="new_encoder_release"></a>Media Services-codering Release
Kondigt Hallo nieuwe release van Media Services Azure Media Encoder. Hello meest recente Azure Media Encoder u alleen worden in rekening gebracht voor uitvoer in GB's, maar anders Hallo nieuwe encoder functie compatibel met eerdere encoder Hallo is. Voor meer informatie [Media Services Pricing Details]).

### <a id="oct_sdk"></a>Mediaservices .NET SDK
Media Services SDK voor .NET-extensies is nu versie 2.0.0.3.

Media Services SDK voor .NET is nu versie 3.0.0.8.

Hallo volgende wijzigingen zijn aangebracht:

* Refactoring in opnieuw beleid klassen.
* Headers voor aanvraag van gebruiker agent tekenreeks toohttp wordt toegevoegd.
* Nuget terugzetten build stap wordt toegevoegd.
* Scenario tests toouse x509 cert is hersteld uit de opslagplaats.
* Valideren van de instellingen bij het bijwerken van kanaal en streaming-end.

### <a name="new-github-repository-toohost-media-services-samples"></a>Nieuwe GitHub-opslagplaats toohost Media Services-voorbeelden
Voorbeelden bevinden zich in [Azure Media Services-voorbeelden GitHub-opslagplaats](https://github.com/Azure/Azure-Media-Services-Samples).

## <a id="september_changes_14"></a>Release van september 2014
Media Services REST metagegevens is nu versie 2.7. Zie voor meer informatie over de meest recente REST updates Hallo [Azure Media Services REST API-verwijzing].

Media Services SDK voor .NET is nu versie 3.0.0.7

### <a id="sept_14_breaking_changes"></a>Wijzigingen op te splitsen
* **Oorsprong** te gewijzigd[StreamingEndpoint].
* Een wijziging in Hallo standaardgedrag bij gebruik van Hallo **Azure-portal** tooencode en vervolgens publiceren MP4-bestanden.

Voorheen bij gebruik van Hallo klassieke Azure-Portal toopublish één bestand MP4 videoasset een SAS-URL moet worden gemaakt (SAS-URL's kunt u toodownload Hallo video van een blob-opslag). Wanneer u Hallo klassieke Azure-Portal tooencode en vervolgens één bestand MP4 videoasset publiceren gegenereerd Hallo momenteel URL punten tooan Azure Media Services streaming-eindpunt.  Deze wijziging heeft geen invloed op MP4-video's die rechtstreeks geüploade tooMedia Services en gepubliceerd zonder Azure Media Services wordt gecodeerd.

U hebt op dit moment Hallo na twee opties toosolve Hallo probleem.

* Streaming-eenheden inschakelen en gebruiken van dynamische pakketten toostream Hallo MP4 asset als smooth streaming-presentatie.
* Maken van een SAS-url toodownload Hallo MP4 (of progressief afspelen). Voor meer informatie over hoe u een SAS-locator toocreate Zie [leveren van inhoud].

### <a id="sept_14_GA_changes"></a>Nieuwe functies/scenario's die deel van de GA-release uitmaken
* **Indexeerfunctie Mediaprocessor**. Zie voor meer informatie [mediabestanden indexeren met Azure Media Indexer].
* Hallo [StreamingEndpoint] entiteit kunt u nu tooadd aangepaste (host) domeinnamen.
  
    Voor een aangepast domein naam toobe als streaming Eindpuntnaam van Hallo Media Services gebruikt, moet u tooadd aangepaste host namen tooyour streaming-eindpunt. Hallo REST API's van Media Services .NET SDK tooadd aangepaste hostnamen of gebruiken.
  
    Hallo overwegingen volgende van toepassing:
  
  * U moet eigenaar van de aangepaste domeinnaam Hallo Hallo hebben.
  * Hallo-eigendom van Hallo domeinnaam moet worden gevalideerd door Azure Media Services. toovalidate hello domein, maakt u een CName dat is toegewezen <MediaServicesAccountId>.<parent domain> tooverifydns. < mediaservices DNS-zone >. 
  * U moet een andere CName dat is toegewezen Hallo aangepaste host naam (bijvoorbeeld sports.contoso.com) tooyour Media Services StreamingEndpont van host-naam (bijvoorbeeld amstest.streaming.mediaservices.windows.net) maken.

    Zie voor meer informatie, Hallo **CustomHostNames** eigenschap in Hallo [StreamingEndpoint] onderwerp.

### <a id="sept_14_preview_changes"></a>Nieuwe functies/scenario's die deel van de openbare evaluatieversie Hallo uitmaken
* Live Streaming Preview. Zie voor meer informatie [werken met Azure Media Services Live Streaming].
* Sleutellevering-Service. Zie voor meer informatie [met behulp van dynamische AES-128-versleuteling en de Service voor het leveren van sleutel].
* Dynamische AES-versleuteling. Zie voor meer informatie [met behulp van dynamische AES-128-versleuteling en de Service voor het leveren van sleutel].
* Service voor het leveren van PlayReady-licenties. Zie voor meer informatie [met behulp van dynamische PlayReady-versleuteling en de Service voor het leveren van licenties].
* PlayReady-dynamische versleuteling. Zie voor meer informatie [met behulp van dynamische PlayReady-versleuteling en de Service voor het leveren van licenties].
* Media Services-sjabloon PlayReady-licenties. Zie voor meer informatie [Media Services PlayReady licentie sjabloon overzicht].
* Streaming opslag versleuteld activa. Zie voor meer informatie [Streaming opslag versleutelde inhoud].

## <a id="august_changes_14"></a>Augustus 2014-Release
Wanneer u een asset coderen, wordt na voltooiing van de coderingstaak Hallo een uitvoerasset geproduceerd. Tot deze release is Azure Media Services-Encoder metagegevens over activa uitvoer geproduceerd. Vanaf deze release Hallo encoder produceert ook metagegevens over invoer activa. Zie voor meer informatie, Hallo [invoer metagegevens] en [uitvoer metagegevens] onderwerpen.

## <a id="july_changes_14"></a>Release van juli 2014
Hallo volgende oplossingen voor problemen zijn aangebracht voor hello Azure Media Services Packager en Codeerder:

* Alleen audio speelt terug wanneer transmuxing een live archief asset tooHTTP Live streamen: dit probleem is opgelost en nu zowel audio en video worden afgespeeld.
* Wanneer een asset tooHTTP Live Streaming en AES-128-bits versleuteling van envelop verpakking, Hallo verpakt streams niet terug worden afgespeeld op Android-apparaten: deze fout is opgelost en verpakte stroom Hallo afspeelt op Android-apparaten die ondersteuning bieden voor HTTP Live Streaming.

## <a id="may_changes_14"></a>Mei 2014-Release
### <a id="may_14_changes"></a>Algemene Media Services-Updates
U kunt nu [dynamische pakketten] toostream HTTP Live Streaming (HLS) v3. toostream HLS v3, Hallo indeling toohello oorsprong locator pad toevoegen: * .ism/manifest(format=m3u8-aapl-v3). Zie voor meer informatie [Blog van Nick Drouin].

Dynamische pakketten nu ook ondersteunt het leveren van HLS (v3- en v4) versleuteld met PlayReady op basis van Smooth Streaming statisch is versleuteld met PlayReady. Voor meer informatie over tooencrypt Smooth Streaming met PlayReady Zie [Smooth Stream beveiligen met PlayReady].

### <a name="may_14_donnet_changes"></a>Media Services .NET SDK-Updates
Hallo na verbeteringen zijn opgenomen in Media Services .NET SDK 3.0.0.5 release Hallo:

* Betere snelheid en herstelmogelijkheden voor het uploaden/downloaden van media-elementen.
* Verbeteringen in opnieuw logica en tijdelijke uitzonderingsverwerking: 
  
  * De detectie en probeer het opnieuw logica tijdelijke fout zijn verbeterd voor uitzonderingen die worden veroorzaakt door het uitvoeren van query's, wanneer u wijzigingen opslaat, bestanden uploaden of downloaden. 
  * Bij het ophalen van Web-uitzonderingen (bijvoorbeeld tijdens een aanvraag van de ACS-token), ziet u dat fatale fouten sneller nu mislukken.

Zie voor meer informatie [probeer logica in Hallo Media Services SDK voor .NET].

## <a id="april_changes_14"></a>Release van april 2014-codering
### <a name="april_14_enocer_changes"></a>Media Services-codering Updates
* Toegevoegde ondersteuning voor het opnemen van AVI-bestanden geschreven met behulp van niet-lineaire editor Hallo gras Valley EDIUS, waarbij Hallo video licht is gecomprimeerd met gras Valley hoofdkantoor/HQX codec. Zie voor meer informatie [gras Valley kondigt EDIUS 7 Streaming via Hallo Cloud].
* Ondersteuning toegevoegd voor het opgeven van de naamconventie Hallo voor Hallo-bestanden die zijn geproduceerd door Hallo Media Encoder. Zie voor meer informatie [beheren Media Service Encoder uitvoer bestandsnamen].
* Ondersteuning toegevoegd voor overlays video en/of audio. Zie voor meer informatie [Overlays maken].
* Ondersteuning toegevoegd voor wilt samenvoegen meerdere video segmenten. Zie voor meer informatie [Video segmenten wilt].
* Een bug gerelateerde vaste tootranscoding van MP4s waar audio Hallo is gecodeerd met Audio MPEG-1 laag 3 (aka MP3).

## <a id="jan_feb_changes_14"></a>Releases van januari/februari 2014
### <a name="jan_fab_14_donnet_changes"></a>Azure Media Services .NET SDK 3.0.0.1, 3.0.0.2 en 3.0.0.3
Hallo-wijzigingen in 3.0.0.1 en 3.0.0.2 omvatten:

* Vaste problemen toousage van LINQ-query's met OrderBy-instructies.
* Testoplossingen in splitsen [GitHub] in op basis van een eenheid tests en Scenario's gebaseerde tests.

Zie voor meer informatie over wijzigingen Hallo: [releases van Azure Media Services .NET SDK 3.0.0.1 en 3.0.0.2].

Hallo volgende wijzigingen zijn aangebracht in 3.0.0.3:

* Azure storage-afhankelijkheden toouse versie 3.0.3.0 bijgewerkt. 
* Compatibiliteit met eerdere versies probleem voor 3.0 opgelost. *.* versies. 

## <a id="december_changes_13"></a>Versie van december 2013
### <a name="dec_13_donnet_changes"></a>Azure Media Services .NET SDK 3.0.0.0-prestatiemeters
> [!NOTE]
> 3.0.x.x versies zijn niet achterwaarts compatibel met 2.4.x.x releases.
> 
> 

meest recente versie van de Hallo Hallo Media Services SDK is nu 3.0.0.0-prestatiemeters. U kunt downloaden van de meest recente pakket Hallo van Nuget of ophalen Hallo bits van [GitHub].

Beginnen met Media Services SDK versie 3.0.0.0-prestatiemeters hello, kunt u Hallo hergebruiken [Azure Active Directory Access Control Service (ACS)] tokens. Zie voor meer informatie, Hallo 'hergebruiken besturingselement Service toegangstokens' sectie in Hallo [tooMedia Services verbinding met de Hallo Media Services SDK voor .NET] onderwerp.

### <a name="dec_13_donnet_ext_changes"></a>Azure Media Services .NET SDK Extensions 2.0.0.0
Hello Azure Media Services .NET SDK Extensions is een set uitbreidingsmethoden en Help-functies die uw code vereenvoudigen en maken het gemakkelijker toodevelop met Azure Media Services. U kunt de meest recente bits Hallo van krijgen [Azure Media Services .NET SDK Extensions].

## <a id="november_changes_13"></a>Release van november 2013
### <a name="nov_13_donnet_changes"></a>Azure Media Services .NET SDK wijzigingen
Vanaf deze versie kunt Hallo Media Services SDK voor .NET fouten worden verwerkt tijdelijke fout die zich voordoen kunnen bij het maken van aanroepen toohello REST API voor Media Services-laag.

## <a id="august_changes_13"></a>Versie augustus 2013
### <a name="aug_13_powershell_changes"></a>PowerShell-Cmdlets voor Media Services is opgenomen in de Azure Sdk-Tools
Hallo na Media Services PowerShell-cmdlets zijn nu opgenomen in [azure-sdk-tools].

* Get-AzureMediaServices 
  
    Bijvoorbeeld `Get-AzureMediaServicesAccount`.
* New-AzureMediaServicesAccount 
  
    Bijvoorbeeld `New-AzureMediaServicesAccount -Name “MediaAccountName” -Location “Region” -StorageAccountName “StorageAccountName”`.
* New-AzureMediaServicesKey 
  
    Bijvoorbeeld `New-AzureMediaServicesKey -Name “MediaAccountName” -KeyType Secondary -Force`.
* Remove-AzureMediaServicesAccount 
  
    Bijvoorbeeld `Remove-AzureMediaServicesAccount -Name “MediaAccountName” -Force`.

## <a id="june_changes_13"></a>Versie van juni 2013
### <a name="june_13_general_changes"></a>Wijzigingen van Azure Media Services
Hallo-wijzigingen die zijn vermeld in deze sectie zijn opgenomen in Hallo releases juni 2013 Media Services-updates.

* Mogelijkheid toolink meerdere opslagaccounts tooa Media Service-account. 
  
    StorageAccount
  
    Asset.StorageAccountName en Asset.StorageAccount
* Mogelijkheid tooupdate Job.Priority. 
* Melding Verwante entiteiten en eigenschappen: 
  
    JobNotificationSubscription
  
    NotificationEndPoint
  
    Job
* Asset.Uri 
* Locator.Name 

### <a name="june_13_dotnet_changes"></a>Wijzigingen van Azure Media Services .NET SDK
Hallo volgende wijzigingen zijn opgenomen in juni 2013 Media Services SDK worden vrijgegeven. Hallo is nieuwste Media Services SDK beschikbaar op GitHub.

* Vanaf versie Hallo 2.3.0.0, Hallo Media Services SDK biedt ondersteuning voor meerdere storage accounts tooa Media Services-account koppelen. Hallo ondersteunen volgende API's deze functie:
  
    Hello IStorageAccount type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.CloudMediaContext.StorageAccounts-eigenschap.
  
    Hello StorageAccount-eigenschap.
  
    Hello StorageAccountName-eigenschap.
  
    Zie voor meer informatie [Media Services-elementen beheren tussen meerdere Opslagaccounts].
* Kennisgeving met betrekking API's. Vanaf versie Hallo 2.2.0.0 er Hallo mogelijkheid toolisten tooAzure Queue storage meldingen. Zie voor meer informatie, [afhandeling van Media Services taak meldingen].
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.IJob.JobNotificationSubscriptions-eigenschap.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.INotificationEndPoint type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.IJobNotificationSubscription type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointCollection type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.NotificationEndPointType type.
  
    Hello Microsoft.WindowsAzure.MediaServices.Client.NotificationJobState type.
* Afhankelijkheid van hello Azure Storage Client SDK 2.0 (Microsoft.WindowsAzure.StorageClient.dll).
* Afhankelijkheid van OData 5.5 (Microsoft.Data.OData.dll).

## <a id="december_changes_12"></a>2012 december Release
### <a name="dec_12_dotnet_changes"></a>Wijzigingen van Azure Media Services .NET SDK
* IntelliSense: Ontbrekende Intellisense-documentatie voor veel typen toegevoegd.
* Microsoft.Practices.TransientFaultHandling.Core: Een probleem waarbij hello SDK nog steeds 'D een afhankelijkheid tooan oude versie van deze assembly opgelost. Hallo SDK nu verwijst naar versie 5.1.1209.1 van deze assembly.

Oplossingen voor problemen die zijn gevonden in Hallo November 2012 SDK:

* IAsset.Locators.Count: Dit aantal is nu juist gerapporteerd op nieuwe IAsset interfaces nadat alle locators zijn verwijderd.
* IAssetFile.ContentFileSize: Deze waarde wordt nu correct ingesteld na een upload door IAssetFile.Upload(filepath).
* IAssetFile.ContentFileSize: Deze eigenschap kan nu worden ingesteld bij het maken van een assetbestand. Was eerder alleen-lezen.
* IAssetFile.Upload(filepath): Een probleem waarbij deze Uploadmethode synchrone Hallo volgende fout wanneer u meerdere bestanden toohello asset uploadt is ArgumentOutOfRangeException opgelost. Hallo-fout is 'Server kan niet tooauthenticate Hallo-aanvraag. Zorg ervoor dat Hallo-waarde van de autorisatie-header wordt gevormd correct inclusief Hallo handtekening."
* IAssetFile.UploadAsync: Vaste een probleem waarbij niet meer dan 5 bestanden tegelijkertijd kunnen worden geüpload.
* IAssetFile.UploadProgressChanged: Deze gebeurtenis is nu beschikbaar via Hallo SDK.
* IAssetFile.DownloadAsync (string, BlobTransferClient, ILocator, CancellationToken): deze methode-overload is nu beschikbaar.
* IAssetFile.DownloadAsync: Vaste een probleem waarbij niet meer dan 5 bestanden tegelijkertijd kunnen worden gedownload.
* IAssetFile.Delete(): Een probleem waarbij aanroepen van delete kan een uitzondering genereren als er geen bestand is geüpload voor Hallo IAssetFile opgelost.
* Taken: Een probleem opgelost waarbij een 'MP4 tooSmooth Streams taak' met een 'PlayReady beveiliging taak' met behulp van een taaksjabloon chaining zou niet maken geen taken op alle.
* EncryptionUtils.GetCertificateFromStore(): Deze methode genereert niet langer een null-referentieuitzondering vanwege tooa fouten Hallo-certificaat op basis van certificaat configuratieproblemen te zoeken.

## <a id="november_changes_12"></a>November 2012 Release
Hallo wijzigingen beschreven in deze sectie zijn updates die zijn opgenomen in Hallo November 2012 (versie 2.0.0.0) SDK. Deze wijzigingen mogelijk code die zijn geschreven voor Hallo juni 2012 preview SDK release toobe gewijzigd of herschreven.

* Assets
  
    IAsset.Create(assetName) is Hallo alleen asset maken functie. IAsset.Create bestandsuploads bestanden niet meer als onderdeel van de methodeaanroep Hallo. IAssetFile gebruiken voor het uploaden.
  
    Hallo IAsset.Publish methode en Hallo AssetState.Publish opsommingswaarde zijn verwijderd uit Hallo Services SDK. Code die is gebaseerd op deze waarde moet opnieuw worden geschreven.
* FileInfo
  
    Deze klasse is verwijderd en vervangen door IAssetFile.
  
    IAssetFiles
  
    IAssetFile FileInfo vervangt en een ander gedrag. toouse, Hallo IAssetFiles object instantiëren, gevolgd door een bestand is geüpload behulp Hallo Media Services SDK of hello Azure-opslag-SDK. Hallo na IAssetFile.Upload overloads kan worden gebruikt:
  
  * IAssetFile.Upload(filePath): Een synchrone methode die Hallo thread geblokkeerd en wordt aanbevolen alleen tijdens het uploaden van één bestand.
  * IAssetFile.UploadAsync (filePath, blobTransferClient, locator, cancellationToken): een asynchrone bewerking. Dit is mechanisme voor het uploaden van Hallo voorkeur. 
    
    Bekende oplossingen: met behulp van Hallo cancellationToken annuleert inderdaad Hallo uploaden; Hallo annulering status van taken Hallo kan echter een aantal statussen zijn. U moet goed catch en verwerken van uitzonderingen.
* Locators
  
    Hallo oorsprong-specifieke versies zijn verwijderd. Hallo SAS-specifieke context. Locators.CreateSasLocator (asset, accessPolicy) worden gemarkeerd afgeschaft of verwijderd door de algemene beschikbaarheid. Hallo Locators Zie de sectie onder de nieuwe functionaliteit voor het gedrag van bijgewerkte.

## <a id="june_changes_12"></a>Preview-versie van juni 2012
Hallo volgende functionaliteit is nieuw in de release van November Hallo Hallo SDK.

* Entiteiten verwijderen
  
    IAsset, IAssetFile, ILocator, IAccessPolicy, IContentKey objecten zijn nu verwijderd op Hallo objectniveau, dat wil zeggen IObject.Delete(), in plaats van een verwijdering in Hallo verzameling, die cloudMediaContext.ObjCollection.Delete(objInstance) vereisen.
* Locators
  
    Locators moet nu worden gemaakt met de Hallo CreateLocator methode en Hallo LocatorType.SAS of LocatorType.OnDemandOrigin enum-waarden gebruiken als een argument voor specifiek type locator Hallo gewenste toocreate.
  
    Eigenschappen van nieuwe tooLocators toomake zijn toegevoegd deze eenvoudiger tooobtain bruikbare URI's voor uw inhoud. Dit nieuwe ontwerp Locators is bedoeld tooprovide meer flexibiliteit voor toekomstige van derden uitbreidbaarheid en eenvoudig te gebruiken voor media clienttoepassingen verhogen.
* Asynchrone methode-ondersteuning
  
    Ondersteuning voor asynchrone is methoden tooall toegevoegd.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

<!-- Anchors. -->

<!-- Images. -->

<!--- URLs. --->
[Azure Media Services MSDN-Forum]: http://social.msdn.microsoft.com/forums/azure/home?forum=MediaServices
[Azure Media Services REST API-verwijzing]: https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference
[Media Services Pricing Details]: http://azure.microsoft.com/pricing/details/media-services/
[invoer metagegevens]: http://msdn.microsoft.com/library/azure/dn783120.aspx
[uitvoer metagegevens]: http://msdn.microsoft.com/library/azure/dn783217.aspx
[leveren van inhoud]: http://msdn.microsoft.com/library/azure/hh973618.aspx
[mediabestanden indexeren met Azure Media Indexer]: http://msdn.microsoft.com/library/azure/dn783455.aspx
[StreamingEndpoint]: http://msdn.microsoft.com/library/azure/dn783468.aspx
[werken met Azure Media Services Live Streaming]: http://msdn.microsoft.com/library/azure/dn783466.aspx
[met behulp van dynamische AES-128-versleuteling en de Service voor het leveren van sleutel]: http://msdn.microsoft.com/library/azure/dn783457.aspx
[met behulp van dynamische PlayReady-versleuteling en de Service voor het leveren van licenties]: http://msdn.microsoft.com/library/azure/dn783467.aspx
[Preview features]: http://azure.microsoft.com/services/preview/
[Media Services PlayReady licentie sjabloon overzicht]: http://msdn.microsoft.com/library/azure/dn783459.aspx
[Streaming opslag versleutelde inhoud]: http://msdn.microsoft.com/library/azure/dn783451.aspx
[Azure portal]: https://manage.windowsazure.com
[dynamische pakketten]: http://msdn.microsoft.com/library/azure/jj889436.aspx
[Blog van Nick Drouin]: http://blog-ndrouin.azurewebsites.net/hls-v3-new-old-thing/
[Smooth Stream beveiligen met PlayReady]: http://msdn.microsoft.com/library/azure/dn189154.aspx
[probeer logica in Hallo Media Services SDK voor .NET]: http://msdn.microsoft.com/library/azure/dn745650.aspx
[gras Valley kondigt EDIUS 7 Streaming via Hallo Cloud]: http://www.streamingmedia.com/Producer/Articles/ReadArticle.aspx?ArticleID=96351&utm_source=dlvr.it&utm_medium=twitter
[beheren Media Service Encoder uitvoer bestandsnamen]: http://msdn.microsoft.com/library/azure/dn303341.aspx
[Overlays maken]: http://msdn.microsoft.com/library/azure/dn640496.aspx
[Video segmenten wilt]: http://msdn.microsoft.com/library/azure/dn640504.aspx
[releases van Azure Media Services .NET SDK 3.0.0.1 en 3.0.0.2]: http://www.gtrifonov.com/2014/02/07/windows-azure-media-services-.net-sdk-3.0.0.2-release/
[Azure Active Directory Access Control Service (ACS)]: http://msdn.microsoft.com/library/hh147631.aspx
[tooMedia Services verbinding met de Hallo Media Services SDK voor .NET]: http://msdn.microsoft.com/library/azure/jj129571.aspx
[Azure Media Services .NET SDK Extensions]: https://github.com/Azure/azure-sdk-for-media-services-extensions/tree/dev
[azure-sdk-tools]: https://github.com/Azure/azure-sdk-tools
[GitHub]: https://github.com/Azure/azure-sdk-for-media-services
[Media Services-elementen beheren tussen meerdere Opslagaccounts]: http://msdn.microsoft.com/library/azure/dn271889.aspx
[afhandeling van Media Services taak meldingen]: http://msdn.microsoft.com/library/azure/dn261241.aspx

