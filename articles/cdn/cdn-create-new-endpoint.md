---
title: aaaGetting de slag met Azure CDN | Microsoft Docs
description: Dit onderwerp leest hoe tooenable hello Azure Content Delivery Network (CDN). Hallo-zelfstudie wordt begeleid Hallo maken van een nieuw CDN-profiel en -eindpunt.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Aan de slag met Azure CDN
In dit onderwerp wordt uitgelegd hoe u Azure CDN inschakelt door een nieuw CDN-profiel en -eindpunt te maken.

> [!IMPORTANT]
> Zie voor een inleiding toohow CDN werkt, evenals een lijst met functies, Hallo [overzicht van CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Nieuwe CDN-profielen maken
Een CDN-profiel is een verzameling van CDN-eindpunten.  Elk profiel bevat een of meer CDN-eindpunten.  U kunt desgewenst toouse meerdere profielen tooorganize uw CDN-eindpunten door internetdomein, webtoepassing of andere criteria.

> [!NOTE]
> Eén Azure-abonnement is standaard beperkt tooeight CDN-profielen. Elk CDN-profiel is beperkt tooten CDN-eindpunten.
> 
> Prijzen van CDN wordt toegepast op Hallo CDN-profiel niveau. Als u toouse een combinatie van Azure CDN Prijscategorieën wenst, moet u meerdere CDN-profielen.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Nieuwe CDN-eindpunten maken
**toocreate een nieuw CDN-eindpunt**

1. In Hallo [Azure Portal](https://portal.azure.com), navigeer tooyour CDN-profiel.  U kunt hebt vastgemaakt toohello dashboard in de vorige stap Hallo.  Als u niet, u kunt vinden door te klikken op **Bladeren**, klikt u vervolgens **CDN-profielen**, en te klikken op Hallo profiel u van plan bent tooadd het eindpunt.
   
    blade Hallo CDN-profiel wordt weergegeven.
   
    ![CDN-profiel][cdn-profile-settings]
2. Klik op Hallo **eindpunt toevoegen** knop.
   
    ![De knop Eindpunt toevoegen][cdn-new-endpoint-button]
   
    Hallo **een eindpunt toevoegen** blade wordt weergegeven.
   
    ![De blade Een eindpunt toevoegen][cdn-add-endpoint]
3. Voer een **naam** voor dit CDN-eindpunt.  Deze naam worden uw resources in de cache op Hallo domein gebruikte tooaccess `<endpointname>.azureedge.net`.
4. In Hallo **oorsprongtype** vervolgkeuzelijst selecteert u het oorsprongtype.  Selecteer **Storage** voor een Azure Storage-account, **Cloudservice** voor een Azure Cloud-service, **Web App** voor een Azure-webtoepassing of **Aangepaste oorsprong** voor een andere openbaar toegankelijke webserveroorsprong (gehost in Azure of ergens anders).
   
    ![Oorsprongtype CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. In Hallo **de hostnaam van oorsprong** vervolgkeuzelijst, selecteer of typ uw brondomein.  Hallo vervolgkeuzelijst bevat alle beschikbare oorsprongen van het Hallo-type die u hebt opgegeven in stap 4.  Als u hebt geselecteerd *aangepaste oorsprong* als uw **oorsprongtype**, voert u Hallo domein van uw aangepaste oorsprong.
6. In Hallo **oorsprongpad** tekst Voer Hallo pad toohello bronnen die u wilt toocache of laat de eigenschap leeg tooallow cache alle resource in Hallo domein dat u in stap 5 hebt opgegeven.
7. In Hallo **host-header van oorsprong**, Voer Hallo host-header gewenste Hallo CDN toosend bij elke aanvraag of laat de standaardwaarde Hallo.
   
   > [!WARNING]
   > Bepaalde oorsprongtypen, zoals Azure Storage en Web-Apps, vereisen Hallo host-header toomatch Hallo domein van de oorsprong Hallo. Tenzij u een bron die een host-header verschilt van het domein vereist hebt, laat u Hallo-standaardwaarde.
   > 
   > 
8. Voor **Protocol** en **poort van oorsprong**, geeft u Hallo-protocollen en poorten gebruikt tooaccess uw resources op Hallo oorsprong.  Er moet minimaal één protocol (HTTP of HTTPS) worden geselecteerd.
   
   > [!NOTE]
   > Hallo **poort van oorsprong** alleen van invloed op welke poort Hallo-eindpunt maakt gebruik van informatie van de oorsprong Hallo tooretrieve.  Hallo eindpunt zelf worden pas beschikbaar tooend clients op Hallo standaard HTTP en HTTPS-poorten (80 en 443), ongeacht Hallo **poort van oorsprong**.  
   > 
   > **Azure CDN van Akamai** eindpunten Hallo volledige TCP-poortbereik voor oorsprongen niet toestaan.  Zie [Azure CDN from Akamai Allowed Origin Ports](https://msdn.microsoft.com/library/mt757337.aspx) (Door Azure CDN van Akamai toegestane poorten van oorsprong) voor een lijst met poorten van oorsprong die niet zijn toegestaan.  
   > 
   > Toegang tot CDN-inhoud via HTTPS gelden Hallo volgende beperkingen:
   > 
   > * U moet Hallo opgegeven door Hallo CDN SSL-certificaat gebruiken. Certificaten van derden worden niet ondersteund.
   > * Moet u Hallo opgegeven CDN-domein (`<endpointname>.azureedge.net`) tooaccess HTTPS-inhoud. HTTPS-ondersteuning is niet beschikbaar voor aangepaste domeinnamen (CNAME's), aangezien Hallo CDN biedt geen ondersteuning voor aangepaste certificaten op dit moment.
   > 
   > 
9. Klik op Hallo **toevoegen** knop toocreate Hallo nieuw eindpunt.
10. Zodra het Hallo-eindpunt is gemaakt, wordt deze weergegeven in een lijst met eindpunten voor Hallo-profiel. Hallo lijstweergave kunt u zien Hallo URL toouse tooaccess in de cache opgeslagen inhoud, evenals Hallo brondomein.
    
    ![CDN-eindpunt][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > Hallo-eindpunt onmiddellijk worden niet beschikbaar voor gebruik, zoals het duurt voor Hallo registratie toopropagate via Hallo CDN.  Profielen van <b>Azure CDN van Akamai</b> worden doorgaans binnen één minuut doorgegeven.  Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.
    > 
    > Gebruikers die toouse Hallo CDN-domeinnaam proberen voordat Hallo-eindpuntconfiguratie is doorgegeven toohello POP's, ontvangen HTTP 404-responscodes.  Zie [Problemen oplossen met CDN-eindpunten die 404-statusberichten retourneren](cdn-troubleshoot-endpoint.md) als u een paar uur nadat u uw eindpunt hebt gemaakt, nog steeds 404-responsberichten ontvangt.
    > 
    > 

## <a name="see-also"></a>Zie ook
* [Het cachegedrag van aanvragen beheren met queryreeksen](cdn-query-string.md)
* [Hoe tooMap CDN inhoud tooa aangepaste domeinen](cdn-map-content-to-custom-domain.md)
* [Vooraf assets op een Azure CDN-eindpunt laden](cdn-preload-endpoint.md)
* [Een Azure CDN-eindpunt leegmaken](cdn-purge-endpoint.md)
* [Problemen oplossen voor CDN-eindpunten die 404-statusberichten retourneren](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
