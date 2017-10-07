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
# <a name="add-a-java-application-tooazure-app-service-web-apps"></a><span data-ttu-id="6f81d-103">Een Java-toepassing tooAzure App Service Web Apps toevoegen</span><span class="sxs-lookup"><span data-stu-id="6f81d-103">Add a Java application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="6f81d-104">Zodra u hebt uw Java-web-app in geïnitialiseerd [Azure App Service] [ Azure App Service] zoals beschreven op [een Java-web-app maken in Azure App Service](web-sites-java-get-started.md), kunt u uw toepassing door het plaatsen van uploaden uw WAR in Hallo **webapps** map.</span><span class="sxs-lookup"><span data-stu-id="6f81d-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in hello **webapps** folder.</span></span>

<span data-ttu-id="6f81d-105">Hallo navigatie pad toohello **webapps** map verschilt op basis van hoe u uw exemplaar van de Web-Apps hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6f81d-105">hello navigation path toohello **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="6f81d-106">Als u uw web-app instelt met behulp van hello Azure Marketplace, Hallo pad toohello **webapps** map bevindt zich in de vorm van Hallo **d:\home\site\wwwroot\bin\application\_server\webapps**, waarbij **toepassing\_server** Hallo naam is van de toepassingsserver Hallo van toepassing zijn op uw Web-Apps-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="6f81d-106">If you set up your web app by using hello Azure Marketplace, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is hello name of hello application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="6f81d-107">Als u uw web-app instelt met behulp van Azure configuratiegebruikersinterface hello, Hallo pad toohello **webapps** map bevindt zich in de vorm van Hallo **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="6f81d-107">If you set up your web app by using hello Azure configuration UI, hello path toohello **webapps** folder is in hello form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="6f81d-108">U kunt bron besturingselement tooupload gebruikmaken uw toepassing of webpagina's, inclusief [continue integratiescenario's](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="6f81d-108">Note that you can use source control tooupload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="6f81d-109">FTP is ook een optie voor het uploaden van uw toepassing of webpagina's. Zie voor meer informatie over het implementeren van uw toepassingen via FTP [implementeren van uw app tooAzure App Service].</span><span class="sxs-lookup"><span data-stu-id="6f81d-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app tooAzure App Service].</span></span>

<span data-ttu-id="6f81d-110">Opmerking voor Tomcat web-apps: nadat u uw toohello WAR-bestand hebt geüpload **webapps** map Hallo Tomcat-toepassingsserver detecteert dat u deze hebt toegevoegd en wordt automatisch geladen.</span><span class="sxs-lookup"><span data-stu-id="6f81d-110">Note for Tomcat web apps: Once you've uploaded your WAR file toohello **webapps** folder, hello Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="6f81d-111">Houd er rekening mee dat als u bestanden (met uitzondering van WAR-bestanden) toohello hoofdmap kopieert, Hallo-toepassingsserver toobe opnieuw wordt gestart moet voordat deze bestanden kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6f81d-111">Note that if you copy files (other than WAR files) toohello ROOT directory, hello application server will need toobe restarted before those files are used.</span></span> <span data-ttu-id="6f81d-112">Hallo autoload functionaliteit voor Hallo Tomcat Java web-apps uitgevoerd op Azure is gebaseerd op een nieuwe WAR-bestand wordt toegevoegd, of nieuwe bestanden of mappen toegevoegd toohello **webapps** map.</span><span class="sxs-lookup"><span data-stu-id="6f81d-112">hello autoload functionality for hello Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added toohello **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="6f81d-113">Zie ook</span><span class="sxs-lookup"><span data-stu-id="6f81d-113">See Also</span></span>
<span data-ttu-id="6f81d-114">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="6f81d-114">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

[<span data-ttu-id="6f81d-115">Application-Insights-App-Insights-Java-Get-Started</span><span class="sxs-lookup"><span data-stu-id="6f81d-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[implementeren van uw app tooAzure App Service]: ./web-sites-deploy.md
