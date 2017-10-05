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
# <a name="add-a-java-application-to-azure-app-service-web-apps"></a><span data-ttu-id="88802-103">Een Java-toepassing aan Azure App Service Web Apps toevoegen</span><span class="sxs-lookup"><span data-stu-id="88802-103">Add a Java application to Azure App Service Web Apps</span></span>
<span data-ttu-id="88802-104">Zodra u hebt uw Java-web-app in geïnitialiseerd [Azure App Service] [ Azure App Service] zoals beschreven op [een Java-web-app maken in Azure App Service](web-sites-java-get-started.md), voor het uploaden van de toepassing door het plaatsen van uw WAR in de **webapps** map.</span><span class="sxs-lookup"><span data-stu-id="88802-104">Once you have initialized your Java web app in [Azure App Service][Azure App Service] as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md), you can upload your application by placing your WAR in the **webapps** folder.</span></span>

<span data-ttu-id="88802-105">De navigatie-pad naar de **webapps** map verschilt op basis van hoe u uw exemplaar van de Web-Apps hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="88802-105">The navigation path to the **webapps** folder differs based on how you set up your Web Apps instance.</span></span>

* <span data-ttu-id="88802-106">Als u uw web-app instelt met behulp van Azure Marketplace, het pad naar de **webapps** map bevindt zich in het formulier **d:\home\site\wwwroot\bin\application\_server\webapps**, waarbij **toepassing\_server** is de naam van de toepassingsserver actief voor uw Web-Apps-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="88802-106">If you set up your web app by using the Azure Marketplace, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\bin\application\_server\webapps**, where **application\_server** is the name of the application server in effect for your Web Apps instance.</span></span> 
* <span data-ttu-id="88802-107">Als u uw web-app instelt met behulp van de configuratie van de Azure-gebruikersinterface het pad naar de **webapps** map bevindt zich in het formulier **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="88802-107">If you set up your web app by using the Azure configuration UI, the path to the **webapps** folder is in the form **d:\home\site\wwwroot\webapps**.</span></span> 

<span data-ttu-id="88802-108">Opmerking u bronbeheer kunt gebruiken voor het uploaden van uw toepassing of webpagina's, inclusief [continue integratiescenario's](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="88802-108">Note that you can use source control to upload your application or web pages, including [continuous integration scenarios](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="88802-109">FTP is ook een optie voor het uploaden van uw toepassing of webpagina's. Zie voor meer informatie over het implementeren van uw toepassingen via FTP [uw app implementeren in Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="88802-109">FTP is also an option for uploading your application or web pages; for more information about deploying your applications over FTP, see [Deploy your app to Azure App Service].</span></span>

<span data-ttu-id="88802-110">Opmerking voor Tomcat web-apps: nadat u het WAR-bestand hebt geüpload de **webapps** map, de Tomcat-toepassingsserver detecteert dat u deze hebt toegevoegd en wordt automatisch geladen.</span><span class="sxs-lookup"><span data-stu-id="88802-110">Note for Tomcat web apps: Once you've uploaded your WAR file to the **webapps** folder, the Tomcat application server will detect that you've added it and will automatically load it.</span></span> <span data-ttu-id="88802-111">Houd er rekening mee dat als u bestanden (met uitzondering van WAR-bestanden) naar de hoofdmap kopiëren, de toepassingsserver moet opnieuw worden opgestart voordat u deze bestanden worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="88802-111">Note that if you copy files (other than WAR files) to the ROOT directory, the application server will need to be restarted before those files are used.</span></span> <span data-ttu-id="88802-112">De functionaliteit autoload voor de Tomcat-Java-web-apps uitgevoerd op Azure is gebaseerd op een nieuwe WAR-bestand wordt toegevoegd of nieuwe bestanden of mappen die zijn toegevoegd aan de **webapps** map.</span><span class="sxs-lookup"><span data-stu-id="88802-112">The autoload functionality for the Tomcat Java web apps running on Azure is based on a new WAR file being added, or new files or directories added to the **webapps** folder.</span></span> 

<a name="see-also"></a>

## <a name="see-also"></a><span data-ttu-id="88802-113">Zie ook</span><span class="sxs-lookup"><span data-stu-id="88802-113">See Also</span></span>
<span data-ttu-id="88802-114">In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.</span><span class="sxs-lookup"><span data-stu-id="88802-114">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

[<span data-ttu-id="88802-115">Application-Insights-App-Insights-Java-Get-Started</span><span class="sxs-lookup"><span data-stu-id="88802-115">application-insights-app-insights-java-get-started</span></span>](../application-insights/app-insights-java-get-started.md)

<!-- URL List -->

<span data-ttu-id="88802-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="88802-116">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
<span data-ttu-id="88802-117">[uw app implementeren in Azure App Service]: ./web-sites-deploy.md</span><span class="sxs-lookup"><span data-stu-id="88802-117">[Deploy your app to Azure App Service]: ./web-sites-deploy.md</span></span>
