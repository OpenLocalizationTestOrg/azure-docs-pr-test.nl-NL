---
title: Verwijzing voor het navigeren door de Azure-portal
description: Meer informatie over de verschillende gebruikerservaringen voor Web-App Service tussen de beheerportal en de Azure Portal
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
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a>Verwijzing voor het navigeren door de Azure-portal
Azure Websites heten voortaan [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714). We bijwerkt onze documentatie in overeenstemming met deze naamswijziging en met instructies voor de Azure-Portal alle. Totdat dit proces is voltooid, kunt u dit document als richtlijn voor het werken met Web-Apps in Azure portal.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a>De toekomst van de klassieke Azure Portal
Terwijl u de huisstijl wijzigingen in de klassieke Azure-Portal zult, wordt deze portal is bezig te vervangen door de Azure-Portal. Als u de klassieke portal is geleidelijk stopgezet, wordt de focus voor het ontwikkelen van nieuwe verschuiving naar de Azure Portal. Alle toekomstige nieuwe functies voor Web-Apps wordt geleverd in de Azure-Portal. Starten met Azure Portal om te profiteren van de nieuwste en beste dat Web-Apps te bieden hebben.

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a>Lay-out verschillen tussen de klassieke Azure-Portal en de Azure Portal
Alle Azure-services worden in de klassieke portal weergegeven aan de linkerzijde. Navigatie in de klassieke portal volgt boomstructuur, waarbij het starten van de service en gaat u naar elk element. Deze structuur is geschikt als onafhankelijke onderdelen beheren. Toepassingen die zijn gebouwd op Azure zijn echter een verzameling met elkaar verbonden services, en deze structuur is niet ideaal voor het werken met verzamelingen van services. 

De Azure-portal kunt eenvoudig toepassingen end-to-end van onderdelen uit meerdere services bouwen. De portal is ingedeeld als *trajecten*. Een *reis* is een reeks *blades*, dat zijn containers voor de verschillende onderdelen. Bijvoorbeeld, instellen van het automatisch schalen voor een web-app is een *reis* die u gaat verschillende blades zoals weergegeven in het volgende voorbeeld: de **website** blade (dat blade titel nog niet zijn bijgewerkt voor het gebruik van de nieuwe terminologie), de **instellingen** blade en de **uitschalen** blade. In het voorbeeld automatische schaling wordt ingesteld afhankelijk is van de CPU-gebruik, dus er ook is een **CPU-Percentage** blade. De onderdelen binnen de *blades* heten *delen*, die eruit tegels. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Navigatie-voorbeeld: een web-app maken
Maken van nieuwe WebApps is nog steeds zo soepel 1-2-3. De volgende afbeelding toont de klassieke portal en de portal side-by-side ter illustratie van weinig is gewijzigd in het aantal stappen die nodig zijn voor een web-app laten en wordt uitgevoerd. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

In de portal kunt u kiezen uit de meest voorkomende typen van web-apps, met inbegrip van toepassingen zoals WordPress populaire galerie. Voor een volledige lijst met beschikbare toepassingen, gaat u naar de [Azure Marketplace].

Wanneer u een web-app maakt, u de URL opgeven App Service-abonnement en de locatie in de portal, net zoals u in de klassieke portal doen. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Bovendien kunt de portal u andere algemene instellingen definiëren. Bijvoorbeeld: [resourcegroepen](../azure-resource-manager/resource-group-overview.md) kunt u eenvoudig aan bekijken en gerelateerde Azure-resources te beheren. 

## <a name="navigation-example-settings-and-features"></a>Navigatie-voorbeeld: instellingen en functies
Alle instellingen en functies worden nu logisch gegroepeerd in een enkel blade, van waaruit u kunt navigeren.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

U kunt bijvoorbeeld aangepaste domeinen maken door te klikken op **aangepaste domeinen en SSL** in de **instellingen** blade.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

Als u een waarschuwing voor bewaking instelt, klikt u op **aanvragen en fouten** en vervolgens **waarschuwing toevoegen**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

Om diagnostische gegevens inschakelen, klikt u op **diagnostische logboeken** in de **instellingen** blade.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Om toepassingsinstellingen te configureren, klikt u op **toepassingsinstellingen** in de **instellingen** blade. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Anders dan de naam van het merk, zijn een aantal items in de portal verwijderd of hernoemd gegroepeerd anders makkelijker te vinden. Bijvoorbeeld: hieronder staat een screenshot van de bijbehorende pagina app-instellingen (**configureren**) in de klassieke portal.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Meer bronnen
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)

