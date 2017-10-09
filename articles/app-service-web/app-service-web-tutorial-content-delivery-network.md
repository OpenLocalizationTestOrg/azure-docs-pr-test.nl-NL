---
title: aaaAdd een CDN tooan Azure App Service | Microsoft Docs
description: Voeg een Content Delivery Network (CDN) tooan Azure App Service-toocache en leveren van de statische bestanden van servers sluiten tooyour klanten Hallo wereld.
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>Toevoegen van een Content Delivery Network (CDN) tooan Azure App Service

[Azure inhoud Delivery Network (CDN)](../cdn/cdn-overview.md) statische webinhoud op strategisch geplaatste locaties tooprovide maximale doorvoer voor het leveren van inhoud toousers plaatst. Hallo CDN verlaagt ook de belasting van de server op uw web-app. Deze zelfstudie laat zien hoe tooadd Azure CDN tooa [web-app in Azure App Service](app-service-web-overview.md). 

Hier volgt Hallo introductiepagina van Hallo voorbeeld statische HTML-site waarin u met werkt:

![Startpagina van voorbeeld-app](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

Wat u leert het volgende:

> [!div class="checklist"]
> * Een CDN-eindpunt maken.
> * Assets in cache vernieuwen.
> * Gebruik query tekenreeksen in de cache opgeslagen toocontrol versies.
> * Gebruik een aangepast domein voor Hallo CDN-eindpunt.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

- [Git installeren](https://git-scm.com/)
- [Installeer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Hallo-web-app maken

toocreate hello web-app die u met Volg Hallo werkt [statische HTML-Quick Start](app-service-web-get-started-html.md) via Hallo **bladeren toohello app** stap.

### <a name="have-a-custom-domain-ready"></a>Houd een aangepast domein bij de hand

toocomplete hello aangepast domein stap van deze zelfstudie, u moet een aangepast domein tooown en hebben toegang tot tooyour DNS-register voor uw domeinprovider (zoals GoDaddy). Bijvoorbeeld: tooadd DNS-vermeldingen voor `contoso.com` en `www.contoso.com`, hebt u toegang tooconfigure Hallo DNS-instellingen voor Hallo `contoso.com` hoofddomein.

Als u nog een domeinnaam hebt, kunt u na Hallo [App Service domein zelfstudie](custom-dns-web-site-buydomains-web-app.md) toopurchase een domein met hello Azure-portal. 

## <a name="log-in-toohello-azure-portal"></a>Meld u bij toohello Azure-portal

Open een browser en ga toohello [Azure-portal](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>Een CDN-profiel en -eindpunt maken

Selecteer in de Hallo linkernavigatiebalk, **App Services**, en selecteer vervolgens Hallo-app die u hebt gemaakt in Hallo [statische Quick Start voor HTML-](app-service-web-get-started-html.md).

![App Service-app in de Hallo portal selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

In Hallo **App Service** pagina in Hallo **instellingen** sectie **Networking > Azure CDN configureren voor uw app**.

![CDN in de Hallo portal selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

In Hallo **Azure Content Delivery Network** pagina, bieden Hallo **nieuw eindpunt** instellingen zoals opgegeven in de tabel Hallo.

![Profiel en -eindpunt maken in Hallo-portal](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Instelling | Voorgestelde waarde | Beschrijving |
| ------- | --------------- | ----------- |
| **CDN-profiel** | myCDNProfile | Selecteer **nieuw** toocreate een CDN-profiel. Een CDN-profiel is een verzameling van CDN-eindpunten met Hallo dezelfde prijscategorie. |
| **Prijscategorie** | Standard Akamai | Hallo [prijscategorie](../cdn/cdn-overview.md#azure-cdn-features) Hallo-provider en de beschikbare functies. In deze zelfstudie gebruiken we standaard Akamai. |
| **Naam van CDN-eindpunt** | De naam die uniek is in Hallo azureedge.net domein | U toegang tot uw resources in de cache op Hallo domein  *\<endpointname >. azureedge.net*.

Selecteer **Maken**.

Azure maakt Hallo-profiel en -eindpunt. Nieuw Hallo-eindpunt wordt weergegeven in Hallo **eindpunten** lijst op dezelfde pagina Hallo en wanneer deze ingericht Hallo status **met**.

![Nieuw eindpunt in lijst](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Test Hallo CDN-eindpunt

Als u de prijscategorie Verizon hebt geselecteerd, duurt het doorgaans ongeveer 90 minuten voor het eindpunt is ingericht. In Akamai duurt het inrichten enkele minuten

Hallo voorbeeld-app heeft een `index.html` bestand en *css*, *img*, en *js* mappen die andere statische elementen bevatten. Hallo inhoud paden voor al deze bestanden zijn Hallo dezelfde op Hallo CDN-eindpunt. Bijvoorbeeld, zowel van de volgende URL's Hallo Hallo toegang *bootstrap.css* bestand in Hallo *css* map:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Navigeer in een browser toohello volgende URL:

```
http://<endpointname>.azureedge.net/index.html
```

![Startpagina van voorbeeldapp waarvoor de gegevens vanuit CDN worden geleverd](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 U ziet Hallo dezelfde pagina dat u eerder in een Azure-web-app hebt uitgevoerd. Azure CDN activa Hallo oorsprong van web-app is opgehaald en wordt behoeve van Hallo CDN-eindpunt

tooensure dat deze pagina in het Hallo CDN, vernieuwen Hallo pagina is opgeslagen. Twee aanvragen voor hello dezelfde asset soms nodig zijn om hello CDN toocache Hallo aangevraagde inhoud.

Zie voor meer informatie over het maken van Azure CDN-profielen en -eindpunten [Aan de slag met Azure CDN](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Hallo CDN opschonen

Hallo CDN worden regelmatig vernieuwd daarbij behorende bronnen uit Hallo oorsprong web-app op basis van Hallo time to live (TTL)-configuratie. Hallo standaard TTL-waarde is zeven dagen.

Soms moet u mogelijk toorefresh Hallo CDN voordat Hallo verlopen van TTL--bijvoorbeeld, wanneer u de bijgewerkte inhoud toohello web-app implementeert. tootrigger vernieuwen, kunt u handmatig Hallo CDN resources opschonen. 

In deze sectie van de zelfstudie hello, een wijziging toohello web-app implementeren en opschonen Hallo CDN tootrigger Hallo CDN toorefresh de cache.

### <a name="deploy-a-change-toohello-web-app"></a>Een wijziging toohello web-app implementeren

Open Hallo `index.html` bestand en voeg toe '-V2 ' toohello H1-kop, zoals wordt weergegeven in Hallo voorbeeld te volgen: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Uw wijziging doorvoeren en het toohello web-app implementeren.

```bash
git commit -am "version 2"
git push azure master
```

Zodra de implementatie is voltooid, Zie bladeren toohello web-app-URL en u Hallo wijzigen.

```
http://<appname>.azurewebsites.net/index.html
```

![V2 in de titel van de web-app](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

Blader toohello CDN-eindpunt-URL voor het Hallo-startpagina en u niet ziet Hallo wijzigen, omdat in de cache opgeslagen versie van de Hallo in Hallo CDN nog niet is verlopen. 

```
http://<endpointname>.azureedge.net/index.html
```

![Geen V2 in de titel van het CDN](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Hallo CDN in de portal Hallo opschonen

tootrigger Hallo CDN tooupdate de versie van de cache, Hallo CDN opschonen.

Selecteer in de Hallo portal linkernavigatievenster, **resourcegroepen**, en selecteer vervolgens Hallo resourcegroep die u hebt gemaakt voor uw web-app (myResourceGroup).

![Resourcegroep selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

Selecteer in de lijst met resources Hallo uw CDN-eindpunt.

![Eindpunt selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

Hallo boven aan het Hallo **eindpunt** pagina, klikt u op **opschonen**.

![Leegmaken selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Voer Hallo paden naar inhoud gewenste toopurge. U kunt een volledig bestand pad toopurge geeft een afzonderlijk bestand of een segment pad toopurge en Vernieuw alle inhoud in een map. Omdat u gewijzigd `index.html`, zorg ervoor dat deze een van de paden Hallo.

Selecteer onderaan Hallo Hallo pagina, **opschonen**.

![Pagina leegmaken](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>Controleer of deze Hallo die CDN is bijgewerkt

Wacht totdat de Hallo opschonen aanvraag is verwerkt, doorgaans een paar minuten. toosee hello huidige status, selecteer Hallo belpictogram bovenaan Hallo Hallo pagina. 

![Melding voor leegmaken](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Blader toohello CDN-eindpunt-URL voor `index.html`, en u ziet nu Hallo V2 dat u op de startpagina Hallo toohello titel toegevoegd. Dit betekent dat Hallo CDN cache is vernieuwd.

```
http://<endpointname>.azureedge.net/index.html
```

![V2 in de titel van het CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Zie voor meer informatie [Een Azure CDN-eindpunt leegmaken](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Query tekenreeksen tooversion inhoud gebruiken

Hello Azure CDN biedt Hallo cacheopties gedrag te volgen:

* Queryreeksen negeren
* Queryreeksen in de cache opslaan overslaan
* Elke unieke URL in de cache opslaan 

Hallo eerst van deze is standaard hello, wat betekent dat er slechts één versie van een asset ongeacht Hallo queryreeks in Hallo URL-cache. 

In deze sectie van de zelfstudie Hallo wijzigen u opslaan in cache gedrag toocache voor elke unieke URL Hallo.

### <a name="change-hello-cache-behavior"></a>Hallo cache gedrag wijzigen

In de Azure-portal Hallo **CDN-eindpunt** pagina **Cache**.

Selecteer **elke unieke URL in de Cache** van Hallo **queryreeks cachegedrag** vervolgkeuzelijst.

Selecteer **Opslaan**.

![Selecteer cachegedrag van queryreeks](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Controleren of de unieke URL's afzonderlijk in de cache worden opgeslagen

In een browser navigeren toohello introductiepagina op Hallo CDN-eindpunt, maar u een querytekenreeks: 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

Hallo CDN retourneert Hallo huidige web app-inhoud, waaronder 'V2' hello post. 

tooensure dat deze pagina in het Hallo CDN, vernieuwen Hallo pagina is opgeslagen. 

Open `index.html` en wijzig 'V2' te 'V3', en implementeren van Hallo wijzigen. 

```bash
git commit -am "version 3"
git push azure master
```

Ga in een browser toohello CDN-eindpunt-URL met een nieuwe querytekenreeks, zoals `q=2`. Hallo CDN opgehaald Hallo huidige `index.html` bestands- en 'V3' wordt weergegeven.  Maar als u de navigatiefunctie toohello CDN-eindpunt met Hallo `q=1` queryreeks, ziet u 'V2'.

```
http://<endpointname>.azureedge.net/index.html?q=2
```

![V3 in de titel in het CDN, queryreeks 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

![V2 in de titel in het CDN, queryreeks 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

Deze uitvoer toont elke queryreeks anders wordt behandeld:

* q = 1 werd gebruikt voorafgaand aan, zodat inhoud in cache (V2) worden geretourneerd.
* q = 2 is nieuw, dus Hallo nieuwste web app inhoud worden opgehaald en (V3) geretourneerd.

Zie [Cachegedrag in Azure CDN bepalen met queryreeksen](../cdn/cdn-query-string.md) voor meer informatie.

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Toewijzen van een aangepast domein tooa CDN-eindpunt

U hebt uw aangepaste domein tooyour CDN-eindpunt toewijzen door een CNAME-record te maken. Een CNAME-record is een DNS-functie waarmee een brondomein domein tooa bestemming. U kunt bijvoorbeeld toewijzen `cdn.contoso.com` of `static.contoso.com` te`contoso.azureedge.net`.

Als u een aangepast domein niet hebt, kunt u na Hallo [App Service domein zelfstudie](custom-dns-web-site-buydomains-web-app.md) toopurchase een domein met hello Azure-portal. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Hallo hostnaam toouse Hello CNAME vinden

In Azure-portal Hallo **eindpunt** pagina, controleert u of **overzicht** is geselecteerd in de navigatie en selecteer vervolgens Hallo Hallo **+ aangepaste domeinen** knop bovenaan Hallo Hallo pagina.

![Aangepast domein toevoegen selecteren](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

In Hallo **toevoegen van een aangepast domein** pagina ziet u Hallo eindpunt host naam toouse bij het maken van een CNAME-record. Hallo-hostnaam is afgeleid van uw CDN-eindpunt-URL:  **&lt;EndpointName >. azureedge.net**. 

![Een domeinpagina toevoegen](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Hallo CNAME configureren bij uw domeinregistrar

Navigeer tooyour domeinregistrar website en Hallo sectie voor het maken van DNS-records gevonden. U vindt dit in een gedeelte zoals **Domeinnaam**, **DNS** of **Serverbeheernaam**.

Hallo sectie voor het beheren van CNAME-records vinden. U kunt toogo tooan geavanceerde instellingenpagina hebben en zoekt Hallo woorden CNAME-, Alias- of subdomeinen.

Een CNAME-record maken die uw gekozen subdomein toegewezen (bijvoorbeeld **statische** of **cdn**) toohello **eindpunt hostnaam** die eerder in Hallo portal weergegeven. 

### <a name="enter-hello-custom-domain-in-azure"></a>Hallo aangepast domein invoeren in Azure

Retourneren van toohello **toevoegen van een aangepast domein** pagina en voert u uw aangepaste domein, met inbegrip van subdomein hello, in het dialoogvenster Hallo. Geef bijvoorbeeld `cdn.contoso.com` op.   
   
Azure wordt gecontroleerd of Hallo CNAME-record bestaat voor Hallo-domeinnaam die u hebt ingevoerd. Als Hallo CNAME juist is, kan uw aangepaste domein wordt gevalideerd.

Voor Hallo CNAME-record toopropagate tooname servers op Hallo Internet kan tijd duren. Als uw domein is niet onmiddellijk gevalideerd, wacht een paar minuten en probeer het opnieuw.

### <a name="test-hello-custom-domain"></a>Test Hallo aangepast domein

Navigeer in een browser toohello `index.html` bestand met behulp van uw aangepaste domein (bijvoorbeeld `cdn.contoso.com/index.html`) tooverify die Hallo resultaat is hetzelfde als wanneer u gaat rechtstreeks te Hallo`<endpointname>azureedge.net/index.html`.

![Startpagina van voorbeeldapp met URL van aangepast domein](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Zie voor meer informatie [kaart Azure CDN inhoud tooa aangepast domein](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Volgende stappen

Wat u hebt geleerd:

> [!div class="checklist"]
> * Een CDN-eindpunt maken.
> * Assets in cache vernieuwen.
> * Gebruik query tekenreeksen in de cache opgeslagen toocontrol versies.
> * Gebruik een aangepast domein voor Hallo CDN-eindpunt.

Meer informatie over hoe toooptimize CDN prestaties in Hallo volgende artikelen:

> [!div class="nextstepaction"]
> [De prestaties verbeteren door bestanden in Azure CDN te comprimeren](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Vooraf assets op een Azure CDN-eindpunt laden](../cdn/cdn-preload-endpoint.md)
