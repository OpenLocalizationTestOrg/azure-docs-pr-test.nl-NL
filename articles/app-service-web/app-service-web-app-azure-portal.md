---
title: aaaReference voor navigeren hello Azure-portal
description: Hallo andere gebruikerservaringen meer voor Web-App Service tussen Hallo-beheerportal en hello Azure Portal
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Naslaginformatie voor navigeren hello Azure-portal
Azure Websites heten voortaan [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). We bijwerkt op alle onze documentatie tooreflect deze naam wijzigings- en tooprovide instructies voor hello Azure-Portal. Totdat dit proces is voltooid, kunt u dit document als richtlijn voor het werken met Web-Apps in hello Azure-portal.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>Hallo toekomstige Hallo klassieke Azure-Portal
Terwijl u Hallo huisstijl wijzigingen in de klassieke Azure-Portal hello zult, wordt deze portal Hallo proces wordt vervangen door hello Azure-Portal. Als de klassieke portal Hallo geleidelijk, is Hallo focus voor de ontwikkeling van nieuwe verschuiving van toohello Azure-Portal. Alle toekomstige nieuwe functies voor Web-Apps wordt geleverd in hello Azure-Portal. Beginnen met hello Azure Portal tootake profiteren van Hallo nieuwste en beste dat de Web-Apps toooffer hebben.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Lay-out verschillen tussen Hallo klassieke Azure-Portal en Azure-Portal
In de klassieke portal Hallo Hallo alle Azure services aan de linkerzijde Hallo worden weergegeven. Navigatie in de klassieke portal Hallo volgt waar te starten vanaf het Hallo-service en gaat u naar elk element in een boomstructuur. Deze structuur is geschikt als onafhankelijke onderdelen beheren. Toepassingen die zijn gebouwd op Azure zijn echter een verzameling met elkaar verbonden services, en deze structuur is niet ideaal voor het werken met verzamelingen van services. 

Hello Azure-portal maakt het eenvoudig toobuild toepassingen end-to-end van onderdelen uit meerdere services. Hallo-portal is ingedeeld als *trajecten*. Een *reis* is een reeks *blades*, die zijn containers voor Hallo verschillende onderdelen. Bijvoorbeeld, instellen van het automatisch schalen voor een web-app is een *reis* die u gaat verschillende blades zoals weergegeven in het volgende voorbeeld Hallo: Hallo **website** blade (dat blade titel nog niet bijgewerkt toouse is nieuwe terminologie Hello), Hallo **instellingen** blade en Hallo **uitschalen** blade. In voorbeeld Hallo automatische schaling wordt ingesteld toodepend op CPU-gebruik, dus er ook is een **CPU-Percentage** blade. Hallo componenten binnen Hallo *blades* heten *delen*, die eruit tegels. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Navigatie-voorbeeld: een web-app maken
Maken van nieuwe WebApps is nog steeds zo soepel 1-2-3. Hallo volgende afbeelding toont Hallo klassieke portal en Hallo portal side-by-side toodemonstrate die weinig is gewijzigd in Hallo minder stappen nodig tooget een web-app van en die wordt uitgevoerd. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

In Hallo-portal kunt u kiezen uit de meest voorkomende typen Hallo van web-apps, met inbegrip van toepassingen zoals WordPress populaire galerie. Voor een volledige lijst met beschikbare toepassingen, gaat u naar Hallo [Azure Marketplace].

Wanneer u een web-app maakt, u de URL opgeven App Service-abonnement en de locatie in net als in de klassieke portal Hallo Hallo-portal. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Bovendien kunt Hallo portal u andere algemene instellingen definiëren. Bijvoorbeeld: [resourcegroepen](../azure-resource-manager/resource-group-overview.md) eenvoudige toosee maken en beheren van Azure gerelateerde resources. 

## <a name="navigation-example-settings-and-features"></a>Navigatie-voorbeeld: instellingen en functies
Alle Hallo instellingen en functies nu logisch zijn gegroepeerd in een enkel blade, van waaruit u kunt navigeren.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

U kunt bijvoorbeeld aangepaste domeinen maken door te klikken op **aangepaste domeinen en SSL** in Hallo **instellingen** blade.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset van een waarschuwing voor bewaking, klik op **aanvragen en fouten** en vervolgens **waarschuwing toevoegen**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

tooenable diagnostics, klikt u op **diagnostische logboeken** in Hallo **instellingen** blade.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

tooconfigure toepassingsinstellingen, klikt u op **toepassingsinstellingen** in Hallo **instellingen** blade. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Dan Hallo merknaam, enkele dingen in Hallo-portal zijn verwijderd of hernoemd gegroepeerd anders toomake deze eenvoudiger toofind ze. Bijvoorbeeld: hieronder staat een screenshot van de bijbehorende pagina Hallo app-instellingen (**configureren**) in de klassieke portal Hallo.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Meer bronnen
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

