---
title: een Java-toepassing tooAzure App Service Web Apps aaaAdd
description: Deze zelfstudie leert u hoe tooadd een page of application tooyour exemplaar van Azure App Service Web Apps die al is geconfigureerd voor toouse Java.
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
ms.openlocfilehash: 2feb464b2933921ad2887779a6b7589634e2e2f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a>Een Java-toepassing tooAzure App Service Web Apps toevoegen
Zodra u hebt uw Java-web-app in geïnitialiseerd [Azure App Service] [ Azure App Service] zoals beschreven op [een Java-web-app maken in Azure App Service](web-sites-java-get-started.md), kunt u uw toepassing door het plaatsen van uploaden uw WAR in Hallo **webapps** map.

Hallo navigatie pad toohello **webapps** map verschilt op basis van hoe u uw exemplaar van de Web-Apps hebt ingesteld.

* Als u uw web-app instelt met behulp van hello Azure Marketplace, Hallo pad toohello **webapps** map bevindt zich in de vorm van Hallo **d:\home\site\wwwroot\bin\application\_server\webapps**, waarbij **toepassing\_server** Hallo naam is van de toepassingsserver Hallo van toepassing zijn op uw Web-Apps-exemplaar. 
* Als u uw web-app instelt met behulp van Azure configuratiegebruikersinterface hello, Hallo pad toohello **webapps** map bevindt zich in de vorm van Hallo **d:\home\site\wwwroot\webapps**. 

U kunt bron besturingselement tooupload gebruikmaken uw toepassing of webpagina's, inclusief [continue integratiescenario's](app-service-continuous-deployment.md). FTP is ook een optie voor het uploaden van uw toepassing of webpagina's. Zie voor meer informatie over het implementeren van uw toepassingen via FTP [implementeren van uw app tooAzure App Service].

Opmerking voor Tomcat web-apps: nadat u uw toohello WAR-bestand hebt geüpload **webapps** map Hallo Tomcat-toepassingsserver detecteert dat u deze hebt toegevoegd en wordt automatisch geladen. Houd er rekening mee dat als u bestanden (met uitzondering van WAR-bestanden) toohello hoofdmap kopieert, Hallo-toepassingsserver toobe opnieuw wordt gestart moet voordat deze bestanden kunnen worden gebruikt. Hallo autoload functionaliteit voor Hallo Tomcat Java web-apps uitgevoerd op Azure is gebaseerd op een nieuwe WAR-bestand wordt toegevoegd, of nieuwe bestanden of mappen toegevoegd toohello **webapps** map. 

<a name="see-also"></a>

## <a name="see-also"></a>Zie ook
Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].

[Application-Insights-App-Insights-Java-Get-Started](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[implementeren van uw app tooAzure App Service]: ./web-sites-deploy.md
