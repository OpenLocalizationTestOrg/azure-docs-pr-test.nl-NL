---
title: aaaConfiguring inhoudsbeveiliging beleidsregels met behulp van Azure-portal Hallo | Microsoft Docs
description: In dit artikel laat zien hoe toouse hello Azure portal tooconfigure content protection-beleid. Hallo artikel wordt ook toont hoe tooenable dynamische versleuteling voor de activa.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Beleidsregels voor beveiliging van inhoud met behulp van hello Azure-portal configureren
> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
> 
> 

## <a name="overview"></a>Overzicht
Microsoft Azure Media Services (AMS) kunt u toosecure uw media Hallo tijd vanaf uw computer via de opslag, verwerking en levering. Media Services kunt u toodeliver uw inhoud versleuteld dynamisch met Advanced Encryption Standard (AES) (met behulp van coderingssleutels 128-bits), common encryption (CENC) met PlayReady en/of Widevine DRM en Apple FairPlay. 

AMS voorziet in een service voor het leveren van DRM-licenties en AES wissen sleutels tooauthorized clients. Hello Azure-portal kunt u toocreate een **sleutel/licentie autorisatiebeleid** voor alle typen versleutelingen.

In dit artikel laat zien hoe tooconfigure inhoud beveiligingsbeleid Hello Azure-portal. Hallo artikel wordt ook toont hoe tooapply dynamische versleuteling tooyour activa.


> [!NOTE]
> Als u hello Azure classic portal toocreate protection-beleid gebruikt, Hallo beleid mogelijk niet in Hallo [Azure-portal](https://portal.azure.com/). Alle Hallo oude beleidsregels echter nog steeds aanwezig zijn. U kunt ze controleren met behulp van Azure Media Services .NET SDK of Hallo Hallo [Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) hulpprogramma (toosee Hallo beleidsregels, klik met de rechtermuisknop op Hallo asset -> weergave informatie (F4) -> Klik op inhoud sleutels tabblad -> Klik op het Hallo-sleutel). 
> 
> Als u uw asset werken met beleid voor nieuwe tooencrypt wilt, configureert u deze met hello Azure-portal, klik op Opslaan en dynamische versleuteling toepassen. 
> 
> 

## <a name="start-configuring-content-protection"></a>Beginnen met de configuratie van de beveiliging van inhoud
toouse hello portal toostart content protection globale tooyour AMS-account configureren Hallo te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. Selecteer **instellingen** > **Content protection**.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>Autorisatiebeleid voor de sleutel/licentie
AMS ondersteunt meerdere manieren van gebruikers die sleutel of licentie-aanvragen te verifiëren. Hallo autorisatiebeleid voor inhoudssleutels moet worden geconfigureerd door u en voldaan door de client om Hallo sleutel/licentie toobe delived toohello client. Hallo autorisatiebeleid voor inhoudssleutels kan een of meer autorisatiebeperkingen hebben: **openen** of **token** beperking.

Hello Azure-portal kunt u toocreate een **sleutel/licentie autorisatiebeleid** voor alle typen versleutelingen.

### <a name="open"></a>Open
Open beperking houdt in dat systeem Hallo Hallo sleutel tooanyone die sleutels aanvragen levert. Deze beperking kan handig zijn voor testdoeleinden. 

### <a name="token"></a>Token
Hallo token beleid voor de beperkte vergezeld van een token dat is uitgegeven door een Secure Token Service (STS). Media Services ondersteunt tokens in Hallo Simple Web Tokens (SWT) en JSON Web Token (JWT)-indeling. Media Services biedt geen Token Services beveiligen. U kunt een aangepaste STS maken of gebruikmaken van Microsoft Azure ACS tooissue tokens. Hallo STS moet geconfigureerde toocreate token van een ondertekend met Hallo opgegeven sleutel- en claims die u hebt opgegeven in de configuratie van Hallo tokenbeperking. Hallo Media Services sleutellevering service Hallo aangevraagd toohello (of licentiegegevens)-client retourneert als Hallo token geldig is en Hallo claims in Hallo token overeenkomen met die zijn geconfigureerd voor hello (of licentiegegevens).

U moet bij het configureren van token beperkte beleid Hallo Hallo verificatie van de primaire sleutel, uitgever en doelgroep parameters opgeven. Hallo verificatie van de primaire sleutel bevat Hallo key of Hallo-token is ondertekend met, de uitgever Hallo secure token-service die het Hallo-token uitgeeft. Hallo doelgroep (ook wel bereik genoemd) wordt beschreven Hallo bedoeling van Hallo token of Hallo resource Hallo token gemachtigd voor toegang tot. Hallo Media Services-service voor sleutellevering valideert dat deze waarden in Hallo token Hallo-waarden in de sjabloon Hallo overeenkomen.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>PlayReady-rechtensjabloon
Zie voor gedetailleerde informatie over Hallo PlayReady rechtensjabloon [Media Services PlayReady licentie sjabloon overzicht](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>Niet-permanente
Als u de licentie als niet-permanente configureert, wordt deze alleen bewaard in het geheugen tijdens het Hallo-speler Hallo-licentie gebruikt.  

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Permanente
Als u Hallo licentie als permanente configureert, wordt deze opgeslagen in de permanente opslag op Hallo-client.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Widevine-rechtensjabloon
Zie voor gedetailleerde informatie over Hallo Widevine rechtensjabloon [Widevine-licentie sjabloon overzicht](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>Basic
Wanneer u selecteert **Basic**, Hallo sjabloon wordt gemaakt met alle standaardwaarden waarden.

### <a name="advanced"></a>Geavanceerd
Zie voor gedetailleerde uitleg over geavanceerde optie Widevine configuraties [dit](media-services-widevine-license-template-overview.md) onderwerp.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>FairPlay-configuratie
tooenable FairPlay versleuteling, moet u tooprovide Hallo certificaat-App en toepassing geheime sleutel (vraag) via Hallo FairPlay configuratieoptie. Zie voor gedetailleerde informatie over de vereisten en FairPlay configuratie [dit](media-services-protect-hls-with-fairplay.md) artikel.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Dynamische versleuteling tooyour asset toepassen
tootake profiteren van dynamische versleuteling hoeft u tooencode uw bronbestand in een set adaptive bitrate MP4-bestanden.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Selecteer een asset die u tooencrypt wilt
uw assets selecteert u toosee **instellingen** > **activa**.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>Versleutelen met AES of DRM
Indrukken **versleutelen** op een actief, krijgt u twee opties: **AES** of **DRM**. 

#### <a name="aes"></a>AES
AES wissen sleutelcodering wordt ingeschakeld voor alle protocollen voor streaming: Smooth Streaming, HLS en MPEG-DASH.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Wanneer u Hallo DRM tabblad selecteert, krijgt u verschillende mogelijkheden van het beleid van de beveiliging van inhoud (die u moet nu hebt geconfigureerd) + een reeks protocollen voor streaming.

* **PlayReady en Widevine met MPEG-DASH** -wordt uw MPEG-DASH-stream met PlayReady en Widevine DRM's dynamisch versleutelen.
* **PlayReady en Widevine met MPEG-DASH + FairPlay met HLS** -wordt dynamisch versleutelen u MPEG-DASH-stroom met PlayReady en Widevine DRM's. Uw HLS-streams met FairPlay zal ook worden versleuteld.
* **PlayReady alleen met Smooth Streaming, HLS en MPEG-DASH** -wordt dynamisch versleutelen Smooth Streaming, HLS, MPEG-DASH-streams met PlayReady DRM.
* **Widevine alleen met MPEG-DASH** -wordt dynamisch versleutelen u MPEG-DASH met Widevine DRM.
* **FairPlay alleen met HLS** -wordt uw HLS-stream met FairPlay dynamisch versleutelen.

tooenable FairPlay versleuteling, moet u tooprovide Hallo certificaat-App en toepassing geheime sleutel (vraag) via Hallo FairPlay configuratieoptie van blade Hallo Content Protection-instellingen.

![Inhoud beschermen](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Wanneer u Hallo versleutelingsselectie hebt gemaakt, drukt u op **toepassen**.

>[!NOTE] 
>Als u van plan bent tooplay een AES HLS in Safari versleuteld, Zie [deze blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Volgende stappen
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

