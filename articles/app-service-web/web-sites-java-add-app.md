---
title: Een Java-toepassing aan Azure App Service Web Apps toevoegen
description: Deze zelfstudie laat zien hoe u een pagina of uw exemplaar van Azure App Service Web Apps die al is geconfigureerd voor het gebruik van Java-toepassing toevoegen.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9b46528b-e2d0-4f26-b8d7-af94bd8c31ef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: c28e7c499ed02b759df580f4b14a971b6aec5b67
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a>Een Java-toepassing aan Azure App Service Web Apps toevoegen
Zodra u hebt uw Java-web-app in geïnitialiseerd [Azure App Service] [ Azure App Service] zoals beschreven op [een Java-web-app maken in Azure App Service](web-sites-java-get-started.md), voor het uploaden van de toepassing door het plaatsen van uw WAR in de **webapps** map.

De navigatie-pad naar de **webapps** map verschilt op basis van hoe u uw exemplaar van de Web-Apps hebt ingesteld.

* Als u uw web-app instelt met behulp van Azure Marketplace, het pad naar de **webapps** map bevindt zich in het formulier **d:\home\site\wwwroot\bin\application\_server\webapps**, waarbij **toepassing\_server** is de naam van de toepassingsserver actief voor uw Web-Apps-exemplaar. 
* Als u uw web-app instelt met behulp van de configuratie van de Azure-gebruikersinterface het pad naar de **webapps** map bevindt zich in het formulier **d:\home\site\wwwroot\webapps**. 

Opmerking u bronbeheer kunt gebruiken voor het uploaden van uw toepassing of webpagina's, inclusief [continue integratiescenario's](app-service-continuous-deployment.md). FTP is ook een optie voor het uploaden van uw toepassing of webpagina's. Zie voor meer informatie over het implementeren van uw toepassingen via FTP [uw app implementeren in Azure App Service].

Opmerking voor Tomcat web-apps: nadat u het WAR-bestand hebt geüpload de **webapps** map, de Tomcat-toepassingsserver detecteert dat u deze hebt toegevoegd en wordt automatisch geladen. Houd er rekening mee dat als u bestanden (met uitzondering van WAR-bestanden) naar de hoofdmap kopiëren, de toepassingsserver moet opnieuw worden opgestart voordat u deze bestanden worden gebruikt. De functionaliteit autoload voor de Tomcat-Java-web-apps uitgevoerd op Azure is gebaseerd op een nieuwe WAR-bestand wordt toegevoegd of nieuwe bestanden of mappen die zijn toegevoegd aan de **webapps** map. 

<a name="see-also"></a>

## <a name="see-also"></a>Zie ook
In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.

[Application-Insights-App-Insights-Java-Get-Started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[uw app implementeren in Azure App Service]: ./web-sites-deploy.md
