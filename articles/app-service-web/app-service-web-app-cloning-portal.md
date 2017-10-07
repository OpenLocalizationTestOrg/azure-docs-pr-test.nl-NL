---
title: aaaWeb klonen van de App met Azure Portal
description: Meer informatie over hoe tooclone uw Web-Apps toonew Web-Apps met Azure Portal.
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 20b0ae4e-67e8-4bae-9d74-8a24dc445cce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2016
ms.author: aelnably
ms.openlocfilehash: 605c4879f34d568e9981c34109f9496731c9ed18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Azure App Service-App met behulp van Azure-Portal klonen
Hallo-functie in voor het klonen [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) kunt u bestaande web-apps tooa nieuw gemaakt-app in een andere regio of in een eenvoudig kloon Hallo dezelfde regio. Hiermee schakelt u klanten toodeploy een aantal apps over verschillende regio's snel en eenvoudig.

Klonen van de App is momenteel alleen ondersteund voor premium-laag app service-abonnementen. gebruikt voor nieuwe functie Hallo Hallo dezelfde beperkingen als onderdeel van de back-up van Web Apps, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Klonen van een bestaande App
Hallo-web-app moet worden uitgevoerd in Hallo **Premium** modus zodat u een kloon voor web-app Hallo toocreate.

1. In Hallo [Azure Portal](https://portal.azure.com/), opent u de blade van uw web-app.
2. Klik op **extra**. Klik op Hallo **extra** blade klikt u op **kloon App**.
   
    ![][1]
   
   > [!NOTE]
   > Als de web-app Hallo nog niet Hallo **Premium** modus, ontvangt u een bericht weergegeven dat aangeeft Hallo ondersteund modi voor het klonen van de app. Op dit moment hebt u Hallo optie tooselect **Upgrade**.
   > 
   > 
3. In Hallo **kloon App** blade Geef een naam op van de nieuwe web-app hello, resourcegroep en App Service-Plan. Ook Hallo gebruiker worden kunnen toochoose of tooclone een aantal instellingen voor web-app bron of niet.
   
    ![][2]
4. Wanneer u op **maken** Hallo platform werkt over het maken van een kloon van Hallo bron web-app wordt gestart.

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Klonen van een bestaande App tooan App Service-omgeving
In Hallo **kloon App** blade Hallo klant hebt Hallo optie toochoose een groep van toepassingen in een bestaand App Service-omgeving.

## <a name="current-restrictions"></a>Huidige beperkingen
Deze functie is momenteel in preview, wij werken tooadd nieuwe mogelijkheden gedurende een bepaalde periode, Hallo volgende lijst worden Hallo bekende beperkingen op Hallo ondersteuning van het klonen van de app in Azure-Portal:

* Azure Traffic Manager-instellingen worden niet gekloond.
* Instellingen voor automatisch schalen worden niet gekloond.
* Back-upschema instellingen worden niet gekloond.
* VNET-instellingen worden niet gekloond.
* App Insights worden niet automatisch ingesteld op Hallo bestemming web-app
* Eenvoudige verificatie-instellingen worden niet gekloond.
* Kudu extensie worden niet gekloond.
* TiP regels worden niet gekloond.
* Database-inhoud worden niet gekloond.

### <a name="references"></a>Verwijzingen
* [Klonen van Web-App met behulp van PowerShell](app-service-web-app-cloning.md)
* [Back-up van een web-app in Azure App Service](web-sites-backup.md)
* [Hoe tooCreate een App-serviceomgeving](app-service-web-how-to-create-an-app-service-environment.md)
* [Een web-app maken in een App Service-omgeving](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Inleiding tooApp Service-omgeving](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
