---
title: aaaLogging voor Machine Learning-webservices | Microsoft Docs
description: Meer informatie over hoe logboekregistratie tooenable voor Machine Learning-webservices. Logboekregistratie biedt aanvullende informatie toohelp oplossen Hallo API's.
services: machine-learning
documentationcenter: 
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c54d41e1-0300-46ef-bbfc-d6f7dca85086
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: raymondl;garye
ms.openlocfilehash: ed23933d52d2151af658af2307d7df8743071f65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="58917-104">Logboekregistratie inschakelen voor Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="58917-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="58917-105">Dit document bevat informatie over de mogelijkheden van Machine Learning-webservices logboekregistratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="58917-105">This document provides information on hello logging capability of Machine Learning web services.</span></span> <span data-ttu-id="58917-106">Logboekregistratie biedt aanvullende informatie, dan slechts een foutnummer en een bericht die kan helpen bij het oplossen van uw aanroepen toohello Machine Learning API's.</span><span class="sxs-lookup"><span data-stu-id="58917-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls toohello Machine Learning APIs.</span></span>  

## <a name="how-tooenable-logging-for-a-web-service"></a><span data-ttu-id="58917-107">Hoe tooenable logboekregistratie voor een webservice</span><span class="sxs-lookup"><span data-stu-id="58917-107">How tooenable logging for a Web service</span></span>

<span data-ttu-id="58917-108">Inschakelen van logboekregistratie van Hallo [Azure Machine Learning-webservices](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="58917-108">You enable logging from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="58917-109">Meld u aan toohello Azure Machine Learning-webservices-portal op [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="58917-109">Sign in toohello Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="58917-110">Voor een webservice klassiek kunt u ook toohello portal opvragen door te klikken op **nieuwe Services webervaring** op Hallo Machine Learning-webservices pagina in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="58917-110">For a Classic web service, you can also get toohello portal by clicking **New Web Services Experience** on hello Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Nieuwe koppeling van de ervaring van de Web-Services](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="58917-112">Klik op de bovenste menubalk Hallo **Web Services** voor een nieuwe webservice of klik op **klassieke webservices** voor een klassiek webservice.</span><span class="sxs-lookup"><span data-stu-id="58917-112">On hello top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selecteer Nieuw of klassiek webservices](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="58917-114">Een nieuwe webservice, klikt u op Hallo naam van de webservice.</span><span class="sxs-lookup"><span data-stu-id="58917-114">For a New web service, click hello web service name.</span></span> <span data-ttu-id="58917-115">Voor een webservice klassieke op Hallo naam van de webservice en klik op de volgende pagina Hallo op Hallo juiste eindpunt.</span><span class="sxs-lookup"><span data-stu-id="58917-115">For a Classic web service, click hello web service name and then on hello next page click hello appropriate endpoint.</span></span>

4. <span data-ttu-id="58917-116">Klik op de bovenste menubalk Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="58917-116">On hello top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="58917-117">Set Hallo **logboekregistratie inschakelen** te optie*fout* (toolog alleen fouten) of *alle* (voor volledige logboekregistratie).</span><span class="sxs-lookup"><span data-stu-id="58917-117">Set hello **Enable Logging** option too*Error* (toolog only errors) or *All* (for full logging).</span></span>

   ![Niveau van logboekregistratie selecteren](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="58917-119">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="58917-119">Click **Save**.</span></span>

7. <span data-ttu-id="58917-120">Voor klassieke webservices maken Hallo **ml diagnostics** container.</span><span class="sxs-lookup"><span data-stu-id="58917-120">For Classic web services, create hello **ml-diagnostics** container.</span></span>

   <span data-ttu-id="58917-121">Alle web service-logboeken worden opgeslagen in een blob-container met de naam **ml diagnostics** in Hallo storage-account is gekoppeld aan het Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="58917-121">All web service logs are kept in a blob container named **ml-diagnostics** in hello storage account associated with hello web service.</span></span> <span data-ttu-id="58917-122">Voor nieuwe web-services, wordt deze container gemaakt Hallo eerste keer dat u toegang Hallo-webservice tot.</span><span class="sxs-lookup"><span data-stu-id="58917-122">For New web services, this container is created hello first time you access hello web service.</span></span> <span data-ttu-id="58917-123">Voor klassieke webservices moet u toocreate Hallo container als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="58917-123">For Classic web services, you need toocreate hello container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="58917-124">In Hallo [Azure-portal](https://portal.azure.com), gaat u toohello storage-account is gekoppeld aan het Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="58917-124">In hello [Azure portal](https://portal.azure.com), go toohello storage account associated with hello web service.</span></span>

   2. <span data-ttu-id="58917-125">Onder **Blob-Service**, klikt u op **Containers**.</span><span class="sxs-lookup"><span data-stu-id="58917-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="58917-126">Als Hallo container **ml diagnostics** niet bestaat, klikt u op **+ Container**, geven Hallo container Hallo naam 'ml-diagnostics' en selecteer Hallo **toegangstype** als 'Blob'.</span><span class="sxs-lookup"><span data-stu-id="58917-126">If hello container **ml-diagnostics** doesn't exist, click **+Container**, give hello container hello name "ml-diagnostics", and select hello **Access type** as "Blob".</span></span> <span data-ttu-id="58917-127">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="58917-127">Click **OK**.</span></span>

      ![Niveau van logboekregistratie selecteren](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="58917-129">Hallo Web Services-Dashboard in Machine Learning Studio heeft ook een switch tooenable logboekregistratie voor een webservice klassiek.</span><span class="sxs-lookup"><span data-stu-id="58917-129">For a Classic web service, hello Web Services Dashboard in Machine Learning Studio also has a switch tooenable logging.</span></span> <span data-ttu-id="58917-130">Aangezien logboekregistratie wordt nu beheerd via Hallo Web Services-portal, moet u echter tooenable logboekregistratie via Hallo-portal, zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="58917-130">However, because logging is now managed through hello Web Services portal, you need tooenable logging through hello portal as described in this article.</span></span> <span data-ttu-id="58917-131">Als u al ingeschakeld logboekregistratie in Studio, in Hallo Web Services-Portal, logboekregistratie uitschakelen en opnieuw inschakelen.</span><span class="sxs-lookup"><span data-stu-id="58917-131">If you already enabled logging in Studio, then in hello Web Services Portal, disable logging and enable it again.</span></span>


## <a name="hello-effects-of-enabling-logging"></a><span data-ttu-id="58917-132">Hallo gevolgen van het inschakelen van logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="58917-132">hello effects of enabling logging</span></span>
<span data-ttu-id="58917-133">Als logboekregistratie is ingeschakeld, Hallo diagnostische gegevens en fouten van webservice-eindpunt Hallo worden vastgelegd in Hallo **ml diagnostics** blob-container in hello Azure Storage-Account gekoppeld aan van de gebruiker van het Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="58917-133">When logging is enabled, hello diagnostics and errors from hello web service endpoint are logged in hello **ml-diagnostics** blob container in hello Azure Storage Account linked with hello user’s workspace.</span></span> <span data-ttu-id="58917-134">Deze container bevat alle Hallo diagnostische gegevens voor alle Hallo webservice-eindpunten voor alle Hallo werkruimten die zijn gekoppeld aan dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="58917-134">This container holds all hello diagnostics information for all hello web service endpoints for all hello workspaces associated with this storage account.</span></span>

<span data-ttu-id="58917-135">Hallo logboeken kunnen worden weergegeven met behulp van een Hallo beschikbaar tooexplore van verschillende hulpprogramma's voor een Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="58917-135">hello logs can be viewed using any of hello several tools available tooexplore an Azure Storage Account.</span></span> <span data-ttu-id="58917-136">Hallo eenvoudigste kan worden toonavigate toohello storage-account in hello Azure-portal, klikt u op **Containers**, en klik vervolgens op Hallo container **ml diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="58917-136">hello easiest may be toonavigate toohello storage account in hello Azure portal, click **Containers**, and then click hello container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="58917-137">Blob-logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="58917-137">Log blob detail information</span></span>
<span data-ttu-id="58917-138">Elke blob in de container Hallo bevat Hallo diagnostische gegevens voor exact één van de volgende activiteiten Hallo:</span><span class="sxs-lookup"><span data-stu-id="58917-138">Each blob in hello container holds hello diagnostics information for exactly one of hello following actions:</span></span>

* <span data-ttu-id="58917-139">De uitvoering van Hallo Batchuitvoering methode</span><span class="sxs-lookup"><span data-stu-id="58917-139">An execution of hello Batch-Execution method</span></span>  
* <span data-ttu-id="58917-140">Uitvoering van een van de methode Hallo aanvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="58917-140">An execution of hello Request-Response method</span></span>  
* <span data-ttu-id="58917-141">Initialisatie van een container van aanvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="58917-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="58917-142">Hallo-naam van elke blob heeft een voorvoegsel Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="58917-142">hello name of each blob has a prefix of hello following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="58917-143">Waar _type logboek registreren_ is een van de volgende waarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="58917-143">Where _Log type_ is one of hello following values:</span></span>  

* <span data-ttu-id="58917-144">Batch</span><span class="sxs-lookup"><span data-stu-id="58917-144">batch</span></span>  
* <span data-ttu-id="58917-145">score/aanvragen</span><span class="sxs-lookup"><span data-stu-id="58917-145">score/requests</span></span>  
* <span data-ttu-id="58917-146">score/init</span><span class="sxs-lookup"><span data-stu-id="58917-146">score/init</span></span>  

