---
title: streaming-eindpunten Hello Azure-portal aaaManage | Microsoft Docs
description: Dit onderwerp leest hoe toomanage streaming-eindpunten met hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Streaming-eindpunten Hello Azure-portal beheren

Dit onderwerp leest hoe toouse hello Azure portal toomanage streaming-eindpunten. 

>[!NOTE]
>Zorg ervoor dat tooreview hello [overzicht](media-services-streaming-endpoints-overview.md) onderwerp. 

Zie voor meer informatie over hoe tooscale streaming-eindpunt Hallo [dit](media-services-portal-scale-streaming-endpoints.md) onderwerp.

## <a name="start-managing-streaming-endpoints"></a>Beginnen met het streaming-eindpunten beheren 

streaming-eindpunten voor uw account beheren toostart Hallo te volgen.

1. In Hallo [Azure-portal](https://portal.azure.com/), selecteert u uw Azure Media Services-account.
2. In Hallo **instellingen** blade Selecteer **Streaming-eindpunten**.
   
    ![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> U wordt alleen gefactureerd als uw Streaming-eindpunt wordt uitgevoerd.

## <a name="adddelete-a-streaming-endpoint"></a>Een streaming-eindpunt toevoegen/verwijderen

>[!NOTE]
>Hallo standaardstreaming-eindpunt kan niet worden verwijderd.

streaming-eindpunt met behulp van tooadd/delete Hallo Azure-portal, Hallo te volgen:

1. tooadd een streaming-eindpunt, klikt u op Hallo **+ eindpunt** bovenaan Hallo Hallo pagina. 

    U kunt meerdere Streaming-eindpunten op als u van plan toohave bent verschillende CDN of een CDN en directe toegang.

2. een streaming-eindpunt toodelete druk op **verwijderen** knop.      
3. Klik op Hallo **Start** knop toostart Hallo streaming-eindpunt.
   
    ![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Hallo Streaming-eindpunt configureren
Streaming-eindpunt kunt u tooconfigure Hallo volgende eigenschappen:

* Toegangsbeheer
* Cache-control
* Cross-site-beleid

Zie voor gedetailleerde informatie over deze eigenschappen [StreamingEndpoint](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

U kunt de streaming-eindpunt configureren door Hallo volgende te doen:

1. Selecteer Hallo streaming-eindpunt dat u wilt dat tooconfigure.
2. Klik op **instellingen**.

Hier volgt een korte beschrijving van Hallo velden.

![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. Maximale cachegrootte beleid: de cachebewaartijd gebruikte tooconfigure voor activa geleverd door middel van deze streaming-eindpunt. Als geen waarde is ingesteld, wordt Hallo standaard gebruikt. Hallo standaardwaarden kunnen ook rechtstreeks in Azure-opslag worden gedefinieerd. Als Azure CDN voor Hallo streaming-eindpunt is ingeschakeld, moet u Hallo cache beleid waarde tooless dan 600 seconden niet instellen.  
2. Toegestane IP-adressen: toospecify IP-adressen die mogen tooconnect toohello gepubliceerd streaming-eindpunt wordt gebruikt. Als er geen IP-adressen is opgegeven, wordt elk IP-adres kunnen tooconnect. IP-adressen kunnen worden opgegeven als een enkel IP-adres (bijvoorbeeld: (10.0.0.1), een IP-adresbereik met een IP-adres en een CIDR-subnetmasker (bijvoorbeeld (10.0.0.1/22) of een IP-adresbereik IP-adres en een decimaal subnetmasker met punten (bijvoorbeeld: 10.0.0.1 ' () 255.255.255.0)').
3. Configuratie voor Akamai signature header-verificatie: gebruikt toospecify hoe handtekening header-verificatieaanvraag van Akamai servers is geconfigureerd. Verlooptijd is ingesteld op UTC.

## <a name="scale-your-premium-streaming-endpoint"></a>Schalen van uw Premium streaming-eindpunt

Raadpleeg [dit](media-services-portal-scale-streaming-endpoints.md) onderwerp voor meer informatie.

## <a id="enable_cdn"></a>Integratie van Azure CDN inschakelen

Wanneer u een nieuw account maakt, wordt standaard Streaming-eindpunt Azure CDN-integratie is standaard ingeschakeld.

Desgewenst kunt u later toodisable/enable Hallo CDN streaming-eindpunt moet Hallo **gestopt** status. Het kan too2 uur voor hello Azure CDN integratie tooget ingeschakeld en voor Hallo wijzigingen toobe active over alle Hallo CDN POP's duren. Echter, u kunt uw streaming-eindpunt en stream zonder onderbrekingen start vanaf Hallo streaming-eindpunt en zodra Hallo-integratie voltooid is, Hallo stroom van Hallo CDN worden geleverd. Streaming-eindpunt is niet tijdens Hallo inrichting periode **vanaf** status en u merkt wellicht degredad prestaties.

CDN-integratie is ingeschakeld in alle hello Azure datacenters execpt China en Federal Goverment regio's.

Zodra deze is ingeschakeld, Hallo **toegangsbeheer**, **aangepaste hostnaam** en **Akamai Signature-verificatie** configuratie opgehaald uitgeschakeld.
 
> [!IMPORTANT]
> Azure Media Services-integratie met Azure CDN is geïmplementeerd op **Azure CDN van Verizon** voor standaard streaming-eindpunten. Premium-streaming-eindpunten kan worden geconfigureerd met alle **Azure CDN prijzen lagen en providers**. Zie voor meer informatie over de functies van Azure CDN Hallo [overzicht van CDN](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Aanvullende overwegingen

* Wanneer CDN is ingeschakeld voor een streaming-eindpunt, kunnen geen clients inhoud rechtstreeks vanuit de oorsprong Hallo vragen. Als u uw inhoud met of zonder CDN Hallo mogelijkheid tootest moet, kunt u een ander streaming-eindpunt dat niet ingeschakeld CDN is kunt maken.
* Uw streaming endpoint hostnaam blijft Hallo dezelfde nadat de CDN is ingeschakeld. U hoeft niet toomake eventuele wijzigingen tooyour media services-werkstroom nadat CDN is ingeschakeld. Als uw streaming endpoint-hostnaam strasbourg.streaming.mediaservices.windows.net, nadat de CDN is ingeschakeld, wordt bijvoorbeeld Hallo exact dezelfde hostnaam gebruikt.
* Voor nieuwe streaming-eindpunten, kunt u CDN inschakelen door te maken van een nieuw eindpunt; voor bestaande streaming-eindpunten moet u toofirst stoppen Hallo eindpunt en klik vervolgens in-of uitschakelen Hallo CDN.
* Standaard streaming-eindpunt kan alleen worden geconfigureerd met behulp van **Verizon standaard CDN-provider** met behulp van Azure-beheerportal. U kunt echter andere Azure CDN-providers met REST API's inschakelen.

## <a name="configure-cdn-profile"></a>CDN-profiel configureren

U kunt Hallo CDN-profiel configureren met behulp van Hallo **beheren CDN** knop van Hallo boven.

![Streaming-eindpunt](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Volgende stappen
Media Services-leertrajecten bekijken.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

