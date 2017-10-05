---
title: Logboekregistratie voor Machine Learning-webservices | Microsoft Docs
description: Informatie over het inschakelen van logboekregistratie voor Machine Learning-webservices. Logboekregistratie biedt aanvullende informatie voor het oplossen van de API's.
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
ms.openlocfilehash: 7d0b2db01427430d6b0a317cdfefc265dd4b06e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-logging-for-machine-learning-web-services"></a><span data-ttu-id="fe378-104">Logboekregistratie inschakelen voor Machine Learning-webservices</span><span class="sxs-lookup"><span data-stu-id="fe378-104">Enable logging for Machine Learning web services</span></span>
<span data-ttu-id="fe378-105">Dit document bevat informatie over de mogelijkheid tot het vastleggen van Machine Learning-webservices.</span><span class="sxs-lookup"><span data-stu-id="fe378-105">This document provides information on the logging capability of Machine Learning web services.</span></span> <span data-ttu-id="fe378-106">Logboekregistratie biedt aanvullende informatie, dan slechts een foutnummer en een bericht die kan helpen bij het oplossen van de aanroepen van de Machine Learning API's.</span><span class="sxs-lookup"><span data-stu-id="fe378-106">Logging provides additional information, beyond just an error number and a message, that can help you troubleshoot your calls to the Machine Learning APIs.</span></span>  

## <a name="how-to-enable-logging-for-a-web-service"></a><span data-ttu-id="fe378-107">Het inschakelen van logboekregistratie voor een webservice</span><span class="sxs-lookup"><span data-stu-id="fe378-107">How to enable logging for a Web service</span></span>

<span data-ttu-id="fe378-108">Inschakelen van logboekregistratie van het [Azure Machine Learning-webservices](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="fe378-108">You enable logging from the [Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span> 

1. <span data-ttu-id="fe378-109">Aanmelden bij de portal voor Azure Machine Learning-webservices op [https://services.azureml.net](https://services.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="fe378-109">Sign in to the Azure Machine Learning Web Services portal at [https://services.azureml.net](https://services.azureml.net).</span></span> <span data-ttu-id="fe378-110">Voor een webservice klassiek, u kunt ook opvragen bij de portal door te klikken op **nieuwe Services webervaring** op de pagina Machine Learning-webservices in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="fe378-110">For a Classic web service, you can also get to the portal by clicking **New Web Services Experience** on the Machine Learning Web Services page in Machine Learning Studio.</span></span>

   ![Nieuwe koppeling van de ervaring van de Web-Services](media/machine-learning-web-services-logging/new-web-services-experience-link.png)

2. <span data-ttu-id="fe378-112">In het bovenste menu, klikt u op **webservices** voor een nieuwe webservice of klik op **klassieke webservices** voor een klassiek webservice.</span><span class="sxs-lookup"><span data-stu-id="fe378-112">On the top menu bar, click **Web Services** for a New web service, or click **Classic Web Services** for a Classic web service.</span></span>

   ![Selecteer Nieuw of klassiek webservices](media/machine-learning-web-services-logging/select-web-service.png)

3. <span data-ttu-id="fe378-114">Een nieuwe webservice, klikt u op de naam van de webservice.</span><span class="sxs-lookup"><span data-stu-id="fe378-114">For a New web service, click the web service name.</span></span> <span data-ttu-id="fe378-115">Voor een klassieke-webservice, klikt u op de naam van de webservice en klik vervolgens op de volgende pagina op het juiste eindpunt.</span><span class="sxs-lookup"><span data-stu-id="fe378-115">For a Classic web service, click the web service name and then on the next page click the appropriate endpoint.</span></span>

4. <span data-ttu-id="fe378-116">In het bovenste menu, klikt u op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="fe378-116">On the top menu bar, click **Configure**.</span></span>

5. <span data-ttu-id="fe378-117">Stel de **logboekregistratie inschakelen** optie naar *fout* (alleen om fouten te registreren) of *alle* (voor volledige logboekregistratie).</span><span class="sxs-lookup"><span data-stu-id="fe378-117">Set the **Enable Logging** option to *Error* (to log only errors) or *All* (for full logging).</span></span>

   ![Niveau van logboekregistratie selecteren](media/machine-learning-web-services-logging/enable-logging.png)

6. <span data-ttu-id="fe378-119">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="fe378-119">Click **Save**.</span></span>

7. <span data-ttu-id="fe378-120">Voor klassieke webservices, maken de **ml diagnostics** container.</span><span class="sxs-lookup"><span data-stu-id="fe378-120">For Classic web services, create the **ml-diagnostics** container.</span></span>

   <span data-ttu-id="fe378-121">Alle web service-logboeken worden opgeslagen in een blob-container met de naam **ml diagnostics** in het opslagaccount dat is gekoppeld met de webservice.</span><span class="sxs-lookup"><span data-stu-id="fe378-121">All web service logs are kept in a blob container named **ml-diagnostics** in the storage account associated with the web service.</span></span> <span data-ttu-id="fe378-122">Deze container gemaakt voor nieuwe web-services de eerste keer dat u toegang de webservice tot.</span><span class="sxs-lookup"><span data-stu-id="fe378-122">For New web services, this container is created the first time you access the web service.</span></span> <span data-ttu-id="fe378-123">Voor klassieke webservices moet u de container maken als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="fe378-123">For Classic web services, you need to create the container if it doesn't already exist.</span></span> 

   1. <span data-ttu-id="fe378-124">In de [Azure-portal](https://portal.azure.com), gaat u naar het opslagaccount dat is gekoppeld met de webservice.</span><span class="sxs-lookup"><span data-stu-id="fe378-124">In the [Azure portal](https://portal.azure.com), go to the storage account associated with the web service.</span></span>

   2. <span data-ttu-id="fe378-125">Onder **Blob-Service**, klikt u op **Containers**.</span><span class="sxs-lookup"><span data-stu-id="fe378-125">Under **Blob Service**, click **Containers**.</span></span>

   3. <span data-ttu-id="fe378-126">Als de container **ml diagnostics** niet bestaat, klikt u op **+ Container**, geven de container de naam 'ml-diagnostische gegevens' en selecteer de **toegangstype** als 'Blob'.</span><span class="sxs-lookup"><span data-stu-id="fe378-126">If the container **ml-diagnostics** doesn't exist, click **+Container**, give the container the name "ml-diagnostics", and select the **Access type** as "Blob".</span></span> <span data-ttu-id="fe378-127">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="fe378-127">Click **OK**.</span></span>

      ![Niveau van logboekregistratie selecteren](media/machine-learning-web-services-logging/create-ml-diagnostics-container.png)

> [!TIP]
>
> <span data-ttu-id="fe378-129">Voor een webservice klassieke heeft het Dashboard van de Web-Services in Machine Learning Studio ook een switch logboekregistratie in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="fe378-129">For a Classic web service, the Web Services Dashboard in Machine Learning Studio also has a switch to enable logging.</span></span> <span data-ttu-id="fe378-130">Omdat logboekregistratie wordt nu beheerd via het Web Services-portal, moet u echter inschakelen van logboekregistratie in via de portal, zoals beschreven in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="fe378-130">However, because logging is now managed through the Web Services portal, you need to enable logging through the portal as described in this article.</span></span> <span data-ttu-id="fe378-131">Als u al ingeschakeld logboekregistratie in Studio, in de Web Services-Portal-logboekregistratie uitschakelen en opnieuw inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fe378-131">If you already enabled logging in Studio, then in the Web Services Portal, disable logging and enable it again.</span></span>


## <a name="the-effects-of-enabling-logging"></a><span data-ttu-id="fe378-132">De gevolgen van het inschakelen van logboekregistratie</span><span class="sxs-lookup"><span data-stu-id="fe378-132">The effects of enabling logging</span></span>
<span data-ttu-id="fe378-133">Als logboekregistratie is ingeschakeld, de diagnostische gegevens en fouten van de webservice-eindpunt worden vastgelegd in de **ml diagnostics** blob-container in Azure Storage-Account gekoppeld aan de gebruiker werkruimte.</span><span class="sxs-lookup"><span data-stu-id="fe378-133">When logging is enabled, the diagnostics and errors from the web service endpoint are logged in the **ml-diagnostics** blob container in the Azure Storage Account linked with the user’s workspace.</span></span> <span data-ttu-id="fe378-134">Deze container bevat de diagnostische gegevens voor alle de webservice-eindpunten voor de werkruimten die zijn gekoppeld aan dit opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="fe378-134">This container holds all the diagnostics information for all the web service endpoints for all the workspaces associated with this storage account.</span></span>

<span data-ttu-id="fe378-135">De logboeken kunnen worden weergegeven met een van de verschillende beschikbare hulpprogramma's om te verkennen van een Azure Storage-Account.</span><span class="sxs-lookup"><span data-stu-id="fe378-135">The logs can be viewed using any of the several tools available to explore an Azure Storage Account.</span></span> <span data-ttu-id="fe378-136">De eenvoudigste manier is mogelijk gaat u naar het opslagaccount in de Azure portal, klikt u op **Containers**, en klik vervolgens op de container **ml diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="fe378-136">The easiest may be to navigate to the storage account in the Azure portal, click **Containers**, and then click the container **ml-diagnostics**.</span></span>  

## <a name="log-blob-detail-information"></a><span data-ttu-id="fe378-137">Blob-logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="fe378-137">Log blob detail information</span></span>
<span data-ttu-id="fe378-138">Elke blob in de container bevat de diagnostische gegevens voor exact één van de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="fe378-138">Each blob in the container holds the diagnostics information for exactly one of the following actions:</span></span>

* <span data-ttu-id="fe378-139">Uitvoering van een van de Batch-Execution-methode</span><span class="sxs-lookup"><span data-stu-id="fe378-139">An execution of the Batch-Execution method</span></span>  
* <span data-ttu-id="fe378-140">Uitvoering van een van de methode aanvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="fe378-140">An execution of the Request-Response method</span></span>  
* <span data-ttu-id="fe378-141">Initialisatie van een container van aanvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="fe378-141">Initialization of a Request-Response container</span></span>

<span data-ttu-id="fe378-142">De naam van elke blob heeft een voorvoegsel van de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="fe378-142">The name of each blob has a prefix of the following form:</span></span> 


`{Workspace Id}-{Web service Id}-{Endpoint Id}/{Log type}`


<span data-ttu-id="fe378-143">Waar _type logboek registreren_ is een van de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="fe378-143">Where _Log type_ is one of the following values:</span></span>  

* <span data-ttu-id="fe378-144">Batch</span><span class="sxs-lookup"><span data-stu-id="fe378-144">batch</span></span>  
* <span data-ttu-id="fe378-145">score/aanvragen</span><span class="sxs-lookup"><span data-stu-id="fe378-145">score/requests</span></span>  
* <span data-ttu-id="fe378-146">score/init</span><span class="sxs-lookup"><span data-stu-id="fe378-146">score/init</span></span>  

