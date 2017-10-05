---
title: Klonen van Web-App met Azure Portal
description: Informatie over het klonen van uw Web-Apps naar de nieuwe Web-Apps met Azure Portal.
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
ms.openlocfilehash: 9ebfa91c7972ab3c264032ead8376c23c1197a4b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-app-cloning-using-azure-portal"></a>Azure App Service-App met behulp van Azure-Portal klonen
De functie voor klonen in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) kunt u eenvoudig bestaande klonen web-apps naar een nieuwe app in een andere regio of in dezelfde regio. Hiermee schakelt u klanten een aantal apps implementeren in verschillende regio's snel en eenvoudig.

Klonen van de App is momenteel alleen ondersteund voor premium-laag app service-abonnementen. De nieuwe functie maakt gebruik van dezelfde beperkingen als de functie Web Apps back-up, Zie [Back-up van een web-app in Azure App Service](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="cloning-an-existing-app"></a>Klonen van een bestaande App
De web-app moet worden uitgevoerd in de **Premium** modus in als u een kloon voor de web-app maakt.

1. In de [Azure Portal](https://portal.azure.com/), opent u de blade van uw web-app.
2. Klik op **extra**. Klik op de **extra** blade, klikt u op **kloon App**.
   
    ![][1]
   
   > [!NOTE]
   > Als de web-app nog niet in de **Premium** modus, ontvangt u een bericht met de ondersteunde modi voor het klonen van de app. Op dit moment hebt u de optie te selecteren **Upgrade**.
   > 
   > 
3. In de **kloon App** blade een naam opgeven van de nieuwe web-app, resourcegroep en App Service-Plan. Ook de gebruiker kan kiezen of voor het klonen van een aantal instellingen voor web-app bron worden of niet.
   
    ![][2]
4. Wanneer u op **maken** het platform werkt over het maken van een kloon van de bron-web-app wordt gestart.

## <a name="cloning-an-existing-app-to-an-app-service-environment"></a>Klonen van een bestaande App aan een App-serviceomgeving
In de **kloon App** blade de klant heeft de optie voor het kiezen van een groep van toepassingen in een bestaand App Service-omgeving.

## <a name="current-restrictions"></a>Huidige beperkingen
Deze functie is momenteel in preview, wij werken als u wilt toevoegen van nieuwe mogelijkheden na verloop van tijd, in de volgende lijst worden de bekende beperkingen voor de huidige ondersteuning van het klonen van de app in Azure-Portal:

* Azure Traffic Manager-instellingen worden niet gekloond.
* Instellingen voor automatisch schalen worden niet gekloond.
* Back-upschema instellingen worden niet gekloond.
* VNET-instellingen worden niet gekloond.
* App Insights worden niet automatisch ingesteld op de doel-web-app
* Eenvoudige verificatie-instellingen worden niet gekloond.
* Kudu extensie worden niet gekloond.
* TiP regels worden niet gekloond.
* Database-inhoud worden niet gekloond.

### <a name="references"></a>Verwijzingen
* [Klonen van Web-App met behulp van PowerShell](app-service-web-app-cloning.md)
* [Back-up van een web-app in Azure App Service](web-sites-backup.md)
* [Een App Service-omgeving maken](app-service-web-how-to-create-an-app-service-environment.md)
* [Een web-app maken in een App Service-omgeving](app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Inleiding tot de App Service-omgeving](app-service-app-service-environment-intro.md)

<!--Image references-->
[1]: ./media/app-service-web-app-cloning-portal/CloningBlade.png
[2]: ./media/app-service-web-app-cloning-portal/CloneSettings.png
