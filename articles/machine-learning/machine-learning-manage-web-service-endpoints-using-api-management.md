---
title: aaaLearn hoe toomanage AzureML web services met behulp van API Management | Microsoft Docs
description: Een handleiding die laat zien hoe toomanage AzureML web services met behulp van API Management.
keywords: machine learning api management
services: machine-learning
documentationcenter: 
author: roalexan
manager: jhubbard
editor: 
ms.assetid: 05150ae1-5b6a-4d25-ac67-fb2f24a68e8d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: roalexan
ms.openlocfilehash: 6e764fbfd71be6cc908a1c8d3d8889969fc651a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-how-toomanage-azureml-web-services-using-api-management"></a><span data-ttu-id="f3c01-104">Meer informatie over hoe toomanage AzureML web services met behulp van API Management</span><span class="sxs-lookup"><span data-stu-id="f3c01-104">Learn how toomanage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="f3c01-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f3c01-105">Overview</span></span>
<span data-ttu-id="f3c01-106">Deze handleiding ontdekt u hoe tooquickly aan de slag met API Management toomanage AzureML-webservices.</span><span class="sxs-lookup"><span data-stu-id="f3c01-106">This guide shows you how tooquickly get started using API Management toomanage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="f3c01-107">Wat is Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="f3c01-107">What is Azure API Management?</span></span>
<span data-ttu-id="f3c01-108">Azure API Management is een Azure-service waarmee u uw REST-API-eindpunten beheren door gebruikerstoegang, beperking en bewaking van het dashboard te definiëren.</span><span class="sxs-lookup"><span data-stu-id="f3c01-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="f3c01-109">Klik op [hier](https://azure.microsoft.com/services/api-management/) voor meer informatie over Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="f3c01-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="f3c01-110">Klik op [hier](../api-management/api-management-get-started.md) handleiding over hoe tooget aan de slag met Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="f3c01-110">Click [here](../api-management/api-management-get-started.md) for a guide on how tooget started with Azure API Management.</span></span> <span data-ttu-id="f3c01-111">Deze andere gids, die in deze handleiding is gebaseerd op, vindt meer onderwerpen, waaronder melding configuraties, laag prijzen, antwoord verwerking, gebruikersverificatie, producten, developer-abonnementen en gebruik dashboarding maken.</span><span class="sxs-lookup"><span data-stu-id="f3c01-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="f3c01-112">Wat is AzureML?</span><span class="sxs-lookup"><span data-stu-id="f3c01-112">What is AzureML?</span></span>
<span data-ttu-id="f3c01-113">AzureML is een Azure-service voor machine learning waarmee u tooeasily build, implementeren en geavanceerde analyseoplossingen delen.</span><span class="sxs-lookup"><span data-stu-id="f3c01-113">AzureML is an Azure service for machine learning that enables you tooeasily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="f3c01-114">Klik op [hier](https://azure.microsoft.com/services/machine-learning/) voor meer informatie over AzureML.</span><span class="sxs-lookup"><span data-stu-id="f3c01-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3c01-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f3c01-115">Prerequisites</span></span>
<span data-ttu-id="f3c01-116">toocomplete deze handleiding, moet u:</span><span class="sxs-lookup"><span data-stu-id="f3c01-116">toocomplete this guide, you need:</span></span>

* <span data-ttu-id="f3c01-117">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="f3c01-117">An Azure account.</span></span> <span data-ttu-id="f3c01-118">Als u geen Azure-account hebt, klikt u op [hier](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie over hoe u een gratis proefaccount toocreate.</span><span class="sxs-lookup"><span data-stu-id="f3c01-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="f3c01-119">Een AzureML-account.</span><span class="sxs-lookup"><span data-stu-id="f3c01-119">An AzureML account.</span></span> <span data-ttu-id="f3c01-120">Als u geen account voor met AzureML hebt, klikt u op [hier](https://studio.azureml.net/) voor meer informatie over hoe u een gratis proefaccount toocreate.</span><span class="sxs-lookup"><span data-stu-id="f3c01-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how toocreate a free trial account.</span></span>
* <span data-ttu-id="f3c01-121">Hallo-werkruimte, service en api_key voor een AzureML-experiment geïmplementeerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="f3c01-121">hello workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="f3c01-122">Klik op [hier](machine-learning-create-experiment.md) voor meer informatie over hoe een AzureML toocreate experimenteren.</span><span class="sxs-lookup"><span data-stu-id="f3c01-122">Click [here](machine-learning-create-experiment.md) for details on how toocreate an AzureML experiment.</span></span> <span data-ttu-id="f3c01-123">Klik op [hier](machine-learning-publish-a-machine-learning-web-service.md) voor meer informatie over hoe een AzureML toodeploy experimenteren als een webservice.</span><span class="sxs-lookup"><span data-stu-id="f3c01-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how toodeploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="f3c01-124">Bijlage A bevat ook instructies voor hoe toocreate en test een eenvoudige AzureML experimenteren en als een webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="f3c01-124">Alternately, Appendix A has instructions for how toocreate and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="f3c01-125">Een API Management-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="f3c01-125">Create an API Management instance</span></span>
<span data-ttu-id="f3c01-126">Hieronder vindt Hallo stappen voor het gebruik van API Management toomanage uw AzureML-webservice.</span><span class="sxs-lookup"><span data-stu-id="f3c01-126">Below are hello steps for using API Management toomanage your AzureML web service.</span></span> <span data-ttu-id="f3c01-127">Maak eerst een service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f3c01-127">First create a service instance.</span></span> <span data-ttu-id="f3c01-128">Meld u bij toohello [klassieke Portal](https://manage.windowsazure.com/) en klik op **nieuw** > **App Services** > **API Management**  >  **Maken**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-128">Log in toohello [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![instantie maken](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="f3c01-130">Geef een unieke **URL**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-130">Specify a unique **URL**.</span></span> <span data-ttu-id="f3c01-131">Maakt gebruik van deze handleiding **demoazureml** – u moet toochoose een ander.</span><span class="sxs-lookup"><span data-stu-id="f3c01-131">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="f3c01-132">Kies Hallo gewenst **abonnement** en **regio** voor uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f3c01-132">Choose hello desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="f3c01-133">Nadat u uw selecties, klik op de knop voor volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3c01-133">After making your selections, click hello next button.</span></span>

![maken van service 1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="f3c01-135">Geef een waarde op voor Hallo **organisatienaam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-135">Specify a value for hello **Organization Name**.</span></span> <span data-ttu-id="f3c01-136">Maakt gebruik van deze handleiding **demoazureml** – u moet toochoose een ander.</span><span class="sxs-lookup"><span data-stu-id="f3c01-136">This guide uses **demoazureml** – you will need toochoose something different.</span></span> <span data-ttu-id="f3c01-137">Voer uw e-mailadres in Hallo **e-mail beheerder** veld.</span><span class="sxs-lookup"><span data-stu-id="f3c01-137">Enter your email address in hello **administrator e-mail** field.</span></span> <span data-ttu-id="f3c01-138">Dit e-mailadres wordt gebruikt voor meldingen van Hallo API Management-systeem.</span><span class="sxs-lookup"><span data-stu-id="f3c01-138">This email address is used for notifications from hello API Management system.</span></span>

![maken van service 2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="f3c01-140">Klik op Hallo selectievakje toocreate uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f3c01-140">Click hello check box toocreate your service instance.</span></span> <span data-ttu-id="f3c01-141">*Het duurt om toothirty minuten voor een nieuwe service toobe gemaakt*.</span><span class="sxs-lookup"><span data-stu-id="f3c01-141">*It takes up toothirty minutes for a new service toobe created*.</span></span>

## <a name="create-hello-api"></a><span data-ttu-id="f3c01-142">Hallo-API maken</span><span class="sxs-lookup"><span data-stu-id="f3c01-142">Create hello API</span></span>
<span data-ttu-id="f3c01-143">Zodra Hallo service-exemplaar is gemaakt, is de volgende stap Hallo toocreate Hallo API.</span><span class="sxs-lookup"><span data-stu-id="f3c01-143">Once hello service instance is created, hello next step is toocreate hello API.</span></span> <span data-ttu-id="f3c01-144">Een API bestaat uit een reeks bewerkingen die vanuit een clienttoepassing kunnen worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f3c01-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="f3c01-145">API-bewerkingen worden via proxy tooexisting webservices.</span><span class="sxs-lookup"><span data-stu-id="f3c01-145">API operations are proxied tooexisting web services.</span></span> <span data-ttu-id="f3c01-146">Deze handleiding maakt API's die proxy toohello bestaande AzureML RRS en BES webservices.</span><span class="sxs-lookup"><span data-stu-id="f3c01-146">This guide creates APIs that proxy toohello existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="f3c01-147">API's worden gemaakt en geconfigureerd van Hallo API-publicatieportal, die wordt geopend via Hallo klassieke Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="f3c01-147">APIs are created and configured from hello API publisher portal, which is accessed through hello Azure Classic Portal.</span></span> <span data-ttu-id="f3c01-148">tooreach Hallo publisher portal, selecteer uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f3c01-148">tooreach hello publisher portal, select your service instance.</span></span>

![Selecteer-service-exemplaar](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="f3c01-150">Klik op **beheren** in Hallo klassieke Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="f3c01-150">Click **Manage** in hello Azure Classic Portal for your API Management service.</span></span>

![beheren-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="f3c01-152">Klik op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **API toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-152">Click **APIs** from hello **API Management** menu on hello left, and then click **Add API**.</span></span>

![menu-beheer-API](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="f3c01-154">Type **AzureML Demo API** als Hallo **Web API-naam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-154">Type **AzureML Demo API** as hello **Web API name**.</span></span> <span data-ttu-id="f3c01-155">Type **https://ussouthcentral.services.azureml.net** als Hallo **webservice-URL**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-155">Type **https://ussouthcentral.services.azureml.net** as hello **Web service URL**.</span></span> <span data-ttu-id="f3c01-156">Type **azureml-demo** als Hallo **achtervoegsel URL Web-API**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-156">Type **azureml-demo** as hello **Web API URL suffix**.</span></span> <span data-ttu-id="f3c01-157">Controleer **HTTPS** als Hallo **URL Web-API** schema.</span><span class="sxs-lookup"><span data-stu-id="f3c01-157">Check **HTTPS** as hello **Web API URL** scheme.</span></span> <span data-ttu-id="f3c01-158">Selecteer **Starter** als **producten**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="f3c01-159">Wanneer u klaar bent, klikt u op **opslaan** toocreate Hallo API.</span><span class="sxs-lookup"><span data-stu-id="f3c01-159">When finished, click **Save** toocreate hello API.</span></span>

![nieuwe-api toevoegen](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-hello-operations"></a><span data-ttu-id="f3c01-161">Hallo bewerkingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3c01-161">Add hello operations</span></span>
<span data-ttu-id="f3c01-162">Klik op **toevoegbewerking** tooadd operations toothis API.</span><span class="sxs-lookup"><span data-stu-id="f3c01-162">Click **Add operation** tooadd operations toothis API.</span></span>

![toevoegen-bewerking](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="f3c01-164">Hallo **nieuwe bewerking** venster wordt weergegeven en Hallo **handtekening** tabblad wordt standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f3c01-164">hello **New operation** window will be displayed and hello **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="f3c01-165">RRS bewerking toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3c01-165">Add RRS Operation</span></span>
<span data-ttu-id="f3c01-166">Maak eerst een bewerking voor Hallo AzureML RRS-service.</span><span class="sxs-lookup"><span data-stu-id="f3c01-166">First create an operation for hello AzureML RRS service.</span></span> <span data-ttu-id="f3c01-167">Selecteer **POST** als Hallo **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-167">Select **POST** as hello **HTTP verb**.</span></span> <span data-ttu-id="f3c01-168">Type **/workspaces/ {werkruimte} /services/ {service} / execute? api-version = {apiversion} & details = {details}** als Hallo **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as hello **URL template**.</span></span> <span data-ttu-id="f3c01-169">Type **RRS uitvoeren** als Hallo **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-169">Type **RRS Execute** as hello **Display name**.</span></span>

![rrs-bewerking-handtekening toevoegen](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="f3c01-171">Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-171">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f3c01-172">Klik op **opslaan** toosave deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="f3c01-172">Click **Save** toosave this operation.</span></span>

![toevoegen-rrs--bewerkingsantwoord](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="f3c01-174">BES bewerkingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="f3c01-174">Add BES Operations</span></span>
<span data-ttu-id="f3c01-175">Schermopnamen worden niet vermeld voor BES operations Hallo zoals ze vergelijkbaar toothose zijn voor het toevoegen van Hallo RRS-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f3c01-175">Screenshots are not included for hello BES operations as they are very similar toothose for adding hello RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="f3c01-176">Een taak Batchuitvoering verzenden (maar niet worden gestart)</span><span class="sxs-lookup"><span data-stu-id="f3c01-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="f3c01-177">Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API.</span><span class="sxs-lookup"><span data-stu-id="f3c01-177">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f3c01-178">Selecteer **POST** voor Hallo **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-178">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="f3c01-179">Type **/workspaces/ {werkruimte} /services/ {service} / taken? api-version = {apiversion}** voor Hallo **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f3c01-180">Type **BES indienen** voor Hallo **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-180">Type **BES Submit** for hello **Display name**.</span></span> <span data-ttu-id="f3c01-181">Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-181">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f3c01-182">Klik op **opslaan** toosave deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="f3c01-182">Click **Save** toosave this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="f3c01-183">Een taak Batchuitvoering starten</span><span class="sxs-lookup"><span data-stu-id="f3c01-183">Start a Batch Execution job</span></span>
<span data-ttu-id="f3c01-184">Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API.</span><span class="sxs-lookup"><span data-stu-id="f3c01-184">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f3c01-185">Selecteer **POST** voor Hallo **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-185">Select **POST** for hello **HTTP verb**.</span></span> <span data-ttu-id="f3c01-186">Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid} / starten? api-version = {apiversion}** voor Hallo **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f3c01-187">Type **BES Start** voor Hallo **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-187">Type **BES Start** for hello **Display name**.</span></span> <span data-ttu-id="f3c01-188">Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-188">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f3c01-189">Klik op **opslaan** toosave deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="f3c01-189">Click **Save** toosave this operation.</span></span>

### <a name="get-hello-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="f3c01-190">Hallo status of het resultaat van een taak Batchuitvoering ophalen</span><span class="sxs-lookup"><span data-stu-id="f3c01-190">Get hello status or result of a Batch Execution job</span></span>
<span data-ttu-id="f3c01-191">Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API.</span><span class="sxs-lookup"><span data-stu-id="f3c01-191">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f3c01-192">Selecteer **ophalen** voor Hallo **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-192">Select **GET** for hello **HTTP verb**.</span></span> <span data-ttu-id="f3c01-193">Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid}? api-version = {apiversion}** voor Hallo **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f3c01-194">Type **BES Status** voor Hallo **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-194">Type **BES Status** for hello **Display name**.</span></span> <span data-ttu-id="f3c01-195">Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-195">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f3c01-196">Klik op **opslaan** toosave deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="f3c01-196">Click **Save** toosave this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="f3c01-197">Een taak Batchuitvoering verwijderen</span><span class="sxs-lookup"><span data-stu-id="f3c01-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="f3c01-198">Klik op **toevoegbewerking** tooadd hello AzureML BES bewerking toohello API.</span><span class="sxs-lookup"><span data-stu-id="f3c01-198">Click **add operation** tooadd hello AzureML BES operation toohello API.</span></span> <span data-ttu-id="f3c01-199">Selecteer **verwijderen** voor Hallo **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-199">Select **DELETE** for hello **HTTP verb**.</span></span> <span data-ttu-id="f3c01-200">Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid}? api-version = {apiversion}** voor Hallo **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for hello **URL template**.</span></span> <span data-ttu-id="f3c01-201">Type **BES verwijderen** voor Hallo **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-201">Type **BES Delete** for hello **Display name**.</span></span> <span data-ttu-id="f3c01-202">Klik op **antwoorden** > **toevoegen** op Hallo linker- en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-202">Click **Responses** > **ADD** on hello left and select **200 OK**.</span></span> <span data-ttu-id="f3c01-203">Klik op **opslaan** toosave deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="f3c01-203">Click **Save** toosave this operation.</span></span>

## <a name="call-an-operation-from-hello-developer-portal"></a><span data-ttu-id="f3c01-204">Een bewerking aanroepen vanuit Hallo-Portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="f3c01-204">Call an operation from hello Developer Portal</span></span>
<span data-ttu-id="f3c01-205">Bewerkingen rechtstreeks vanuit de ontwikkelaarsportal hello, waardoor een handige manier tooview kunnen worden aangeroepen en Hallo bewerkingen van een API testen.</span><span class="sxs-lookup"><span data-stu-id="f3c01-205">Operations can be called directly from hello Developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="f3c01-206">In deze handleiding stap u roept Hallo **RRS uitvoeren** methode die is toegevoegd toohello **AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-206">In this guide step you will call hello **RRS Execute** method that was added toohello **AzureML Demo API**.</span></span> <span data-ttu-id="f3c01-207">Klik op **-portal voor ontwikkelaars** in Hallo Hallo menu rechts van de klassieke Portal Hallo top.</span><span class="sxs-lookup"><span data-stu-id="f3c01-207">Click **Developer portal** from hello menu at hello top right of hello Classic Portal.</span></span>

![portal voor ontwikkelaars](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="f3c01-209">Klik op **API's** van Hallo bovenste menu en klik vervolgens op **AzureML Demo API** toosee Hallo bewerkingen die beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="f3c01-209">Click **APIs** from hello top menu, and then click **AzureML Demo API** toosee hello operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="f3c01-211">Selecteer **RRS uitvoeren** voor Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="f3c01-211">Select **RRS Execute** for hello operation.</span></span> <span data-ttu-id="f3c01-212">Klik op **Try It**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-212">Click **Try It**.</span></span>

![Try it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="f3c01-214">Aanvraagparameters, typt u uw **werkruimte**, **service**, **2.0** voor Hallo **apiversion**, en **waar**voor Hallo **details**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-214">For Request parameters, type your **workspace**,  **service**, **2.0** for hello **apiversion**, and  **true** for hello **details**.</span></span> <span data-ttu-id="f3c01-215">U vindt uw **werkruimte** en **service** in Hallo AzureML web servicedashboard (Zie **Hallo webservice testen** in bijlage A).</span><span class="sxs-lookup"><span data-stu-id="f3c01-215">You can find your **workspace** and **service** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="f3c01-216">Aanvraagheaders, klikt u op **header toevoegen** en het type **Content-Type** en **application/json**, klikt u vervolgens op **header toevoegen** en het type  **Autorisatie** en **Bearer <YOUR AZUREML SERVICE API-KEY>** .</span><span class="sxs-lookup"><span data-stu-id="f3c01-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="f3c01-217">U vindt uw **api-sleutel** in Hallo AzureML web servicedashboard (Zie **Hallo webservice testen** in bijlage A).</span><span class="sxs-lookup"><span data-stu-id="f3c01-217">You can find your **api key** in hello AzureML web service dashboard (see **Test hello web service** in Appendix A).</span></span>

<span data-ttu-id="f3c01-218">Type **{'Invoer': {"input1": {'ColumnNames': ["Col2"] "waarden": [[' Dit is een goede dag']]}}, "GlobalParameters": {}}** voor Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="f3c01-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for hello request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="f3c01-220">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-220">Click **Send**.</span></span>

![Verzenden](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="f3c01-222">Nadat een bewerking is aangeroepen, Hallo ontwikkelaarsportal hello **aangevraagde URL** van Hallo back-endservice, Hallo **antwoordstatus**, Hallo **antwoordheaders**, en er is een **antwoordinhoud**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-222">After an operation is invoked, hello developer portal displays hello **Requested URL** from hello back-end service, hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![status van het antwoord](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="f3c01-224">Bijlage A - maken en testen van een eenvoudige AzureML-webservice</span><span class="sxs-lookup"><span data-stu-id="f3c01-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-hello-experiment"></a><span data-ttu-id="f3c01-225">Hallo-experiment maken</span><span class="sxs-lookup"><span data-stu-id="f3c01-225">Creating hello experiment</span></span>
<span data-ttu-id="f3c01-226">Hieronder vindt u Hallo stappen voor het maken van een eenvoudig experiment van AzureML en deze is geïmplementeerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="f3c01-226">Below are hello steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="f3c01-227">web-service wordt als invoer een kolom van willekeurige tekst Hello en retourneert een reeks functies die worden weergegeven als gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="f3c01-227">hello web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="f3c01-228">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f3c01-228">For example:</span></span>

| <span data-ttu-id="f3c01-229">Tekst</span><span class="sxs-lookup"><span data-stu-id="f3c01-229">Text</span></span> | <span data-ttu-id="f3c01-230">Gecodeerde tekst</span><span class="sxs-lookup"><span data-stu-id="f3c01-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="f3c01-231">Dit is een goede dag</span><span class="sxs-lookup"><span data-stu-id="f3c01-231">This is a good day</span></span> |<span data-ttu-id="f3c01-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="f3c01-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="f3c01-233">Eerst met een browser naar keuze, gaat u naar: [https://studio.azureml.net/](https://studio.azureml.net/) en voer uw referenties toolog in.</span><span class="sxs-lookup"><span data-stu-id="f3c01-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials toolog in.</span></span> <span data-ttu-id="f3c01-234">Maak vervolgens een nieuw, leeg experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-234">Next, create a new blank experiment.</span></span>

![experiment-sjablonen voor het zoeken](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="f3c01-236">Wijzig de naam ervan te**SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-236">Rename it too**SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="f3c01-237">Vouw **gegevenssets opgeslagen** en sleep **adresboek beoordelingen van Amazon** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![eenvoudige-functie-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="f3c01-239">Vouw **Data Transformation** en **manipulatie** en sleep **Select Columns in Dataset** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="f3c01-240">Verbinding maken met **adresboek beoordelingen van Amazon** te**Select Columns in Dataset**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-240">Connect **Book Reviews from Amazon** too**Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="f3c01-242">Klik op **Select Columns in Dataset** en klik vervolgens op **Launch column selector** en selecteer **Col2**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="f3c01-243">Klik op Hallo vinkje tooapply deze wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="f3c01-243">Click hello checkmark tooapply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="f3c01-245">Vouw **Tekstanalyse** en sleep **hash-functie** op Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-245">Expand **Text Analytics** and drag **Feature Hashing** onto hello experiment.</span></span> <span data-ttu-id="f3c01-246">Verbinding maken met **Select Columns in Dataset** te**hash-functie**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-246">Connect **Select Columns in Dataset** too**Feature Hashing**.</span></span>

![verbinding maken met project kolommen](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="f3c01-248">Type **3** voor Hallo **bitsize Hashing**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-248">Type **3** for hello **Hashing bitsize**.</span></span> <span data-ttu-id="f3c01-249">Hiermee maakt u 8 (23) kolommen.</span><span class="sxs-lookup"><span data-stu-id="f3c01-249">This will create 8 (23) columns.</span></span>

![hashing bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="f3c01-251">Op dit moment kunt u tooclick **uitvoeren** tootest Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-251">At this point, you may want tooclick **Run** tootest hello experiment.</span></span>

![uitvoeren](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="f3c01-253">Een webservice maken</span><span class="sxs-lookup"><span data-stu-id="f3c01-253">Create a web service</span></span>
<span data-ttu-id="f3c01-254">Maak nu een webservice.</span><span class="sxs-lookup"><span data-stu-id="f3c01-254">Now create a web service.</span></span> <span data-ttu-id="f3c01-255">Vouw **webservice** en sleep **invoer** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="f3c01-256">Verbinding maken met **invoer** te**hash-functie**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-256">Connect **Input** too**Feature Hashing**.</span></span> <span data-ttu-id="f3c01-257">Ook slepen **uitvoer** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="f3c01-258">Verbinding maken met **uitvoer** te**hash-functie**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-258">Connect **Output** too**Feature Hashing**.</span></span>

![output-naar--hash-functies](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="f3c01-260">Klik op **publiceren webservice**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-260">Click **Publish web service**.</span></span>

![publiceren-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="f3c01-262">Klik op **Ja** toopublish Hallo experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-262">Click **Yes** toopublish hello experiment.</span></span>

![Ja om te publiceren](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-hello-web-service"></a><span data-ttu-id="f3c01-264">Hallo webservice testen</span><span class="sxs-lookup"><span data-stu-id="f3c01-264">Test hello web service</span></span>
<span data-ttu-id="f3c01-265">Een webservice AzureML bestaat uit RSS (aanvraag/antwoord-service) en eindpunten van BES (batch uitvoering service).</span><span class="sxs-lookup"><span data-stu-id="f3c01-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="f3c01-266">RSS is voor synchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="f3c01-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="f3c01-267">BES is voor het uitvoeren van asynchrone taak.</span><span class="sxs-lookup"><span data-stu-id="f3c01-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="f3c01-268">tootest uw web-service met de onderstaande Hallo voorbeeld Python-bron, moet u mogelijk toodownload en installatie hello Azure SDK voor Python (Zie: [hoe tooinstall Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="f3c01-268">tootest your web service with hello sample Python source below, you may need toodownload and install hello Azure SDK for Python (see: [How tooinstall Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="f3c01-269">U moet ook Hallo **werkruimte**, **service**, en **api_key** van uw experiment voor Hallo voorbeeld bron hieronder.</span><span class="sxs-lookup"><span data-stu-id="f3c01-269">You will also need hello **workspace**, **service**, and **api_key** of your experiment for hello sample source below.</span></span> <span data-ttu-id="f3c01-270">U kunt Hallo werkruimte en service vinden door te klikken op **aanvragen/reacties** of **Batchuitvoering** voor uw experiment in Hallo web service-dashboard.</span><span class="sxs-lookup"><span data-stu-id="f3c01-270">You can find hello workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in hello web service dashboard.</span></span>

![Zoek-werkruimte-en-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="f3c01-272">U vindt Hallo **api_key** door te klikken op uw experiment in Hallo web service-dashboard.</span><span class="sxs-lookup"><span data-stu-id="f3c01-272">You can find hello **api_key** by clicking your experiment in hello web service dashboard.</span></span>

![zoeken-api-sleutel](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="f3c01-274">Test RRS-eindpunt</span><span class="sxs-lookup"><span data-stu-id="f3c01-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="f3c01-275">Knop Testen</span><span class="sxs-lookup"><span data-stu-id="f3c01-275">Test button</span></span>
<span data-ttu-id="f3c01-276">Een eenvoudige manier tootest Hallo RRS-eindpunt is tooclick **Test** op Hallo web service-dashboard.</span><span class="sxs-lookup"><span data-stu-id="f3c01-276">An easy way tootest hello RRS endpoint is tooclick **Test** on hello web service dashboard.</span></span>

![Test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="f3c01-278">Type **dit is een goede dag** voor **col2**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="f3c01-279">Klik op Hallo vinkje.</span><span class="sxs-lookup"><span data-stu-id="f3c01-279">Click hello checkmark.</span></span>

![Geef gegevens](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="f3c01-281">U ziet ongeveer</span><span class="sxs-lookup"><span data-stu-id="f3c01-281">You will see something like</span></span>

![Voorbeeld van uitvoer](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="f3c01-283">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="f3c01-283">Sample Code</span></span>
<span data-ttu-id="f3c01-284">Een andere manier tootest uw RRS is vanuit uw clientcode.</span><span class="sxs-lookup"><span data-stu-id="f3c01-284">Another way tootest your RRS is from your client code.</span></span> <span data-ttu-id="f3c01-285">Als u op **aanvragen/reacties** onder Hallo dashboard en blader toohello, ziet u de voorbeeldcode van C#, Python en R. U ziet ook Hallo syntaxis van Hallo RRS-aanvraag, waaronder Hallo aanvraag-URI, kopteksten en hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="f3c01-285">If you click **Request/response** on hello dashboard and scroll toohello bottom, you will see sample code for C#, Python, and R. You will also see hello syntax of hello RRS request, including hello request URI, headers, and body.</span></span>

<span data-ttu-id="f3c01-286">Deze handleiding ziet u een werkende Python-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f3c01-286">This guide shows a working Python example.</span></span> <span data-ttu-id="f3c01-287">U moet toomodify met Hallo **werkruimte**, **service**, en **api_key** van uw experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-287">You will need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span>

    import urllib2
    import json
    workspace = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE WORKSPACE ID>"
    service = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE SERVICE ID>"
    api_key = "<REPLACE WITH YOUR EXPERIMENT’S WEB SERVICE API KEY>"
    data = {
    "Inputs": {
        "input1": {
            "ColumnNames": ["Col2"],
            "Values": [ [ "This is a good day" ] ]
        },
    },
    "GlobalParameters": { }
    }
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace + "/services/" + service + "/execute?api-version=2.0&details=true"
    headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}
    body = str.encode(json.dumps(data))
    try:
        req = urllib2.Request(url, body, headers)
        response = urllib2.urlopen(req)
        result = response.read()
        print "result:" + result
            except urllib2.HTTPError, error:
        print("hello request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="f3c01-288">Test BES eindpunt</span><span class="sxs-lookup"><span data-stu-id="f3c01-288">Test BES endpoint</span></span>
<span data-ttu-id="f3c01-289">Klik op **Batchuitvoering** Hallo dashboard en blader toohello onderaan.</span><span class="sxs-lookup"><span data-stu-id="f3c01-289">Click **Batch execution** on hello dashboard and scroll toohello bottom.</span></span> <span data-ttu-id="f3c01-290">Ziet u voorbeelden van code voor C#, Python en R. U ziet ook de syntaxis van de Hallo van Hallo BES aanvragen toosubmit een taak, een taak starten Hallo status of de resultaten van een taak ophalen en verwijderen van een taak.</span><span class="sxs-lookup"><span data-stu-id="f3c01-290">You will see sample code for C#, Python, and R. You will also see hello syntax of hello BES requests toosubmit a job, start a job, get hello status or results of a job, and delete a job.</span></span>

<span data-ttu-id="f3c01-291">Deze handleiding ziet u een werkende Python-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f3c01-291">This guide shows a working Python example.</span></span> <span data-ttu-id="f3c01-292">U moet toomodify met Hallo **werkruimte**, **service**, en **api_key** van uw experiment.</span><span class="sxs-lookup"><span data-stu-id="f3c01-292">You need toomodify it with hello **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="f3c01-293">Daarnaast moet u toomodify hello **opslagaccountnaam**, **opslagaccountsleutel**, en **opslag containernaam**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-293">Additionally, you need toomodify hello **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="f3c01-294">Tot slot moet u toomodify Hallo locatie Hallo **invoerbestand** en de locatie van Hallo Hallo **uitvoerbestand**.</span><span class="sxs-lookup"><span data-stu-id="f3c01-294">Lastly, you will need toomodify hello location of hello **input file** and hello location of hello **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH hello API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH hello LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH hello LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("hello request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading hello result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written toohello file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("hello results for " + outputName + " are available at hello following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "hello results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading hello input tooblob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded hello input tooblob storage"
    input_blob_path = "/" + storage_container_name + "/" + input_blob_name
    connection_string = "DefaultEndpointsProtocol=https;AccountName=" + storage_account_name + ";AccountKey=" + storage_account_key
    payload =  {
        "Input": {
            "ConnectionString": connection_string,
            "RelativeLocation": input_blob_path
        },
        "Outputs": {
            "output1": { "ConnectionString": connection_string, "RelativeLocation": "/" + storage_container_name + "/" + output_blob_name },
        },
        "GlobalParameters": {
        }
    }
        body = str.encode(json.dumps(payload))
    headers = { "Content-Type":"application/json", "Authorization":("Bearer " + api_key)}
    print("Submitting hello job...")
    # submit hello job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove hello enclosing double-quotes
    print("Job ID: " + job_id)
    # start hello job
    print("Starting hello job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking hello job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in hello follwing code
        req = urllib2.Request(url2, headers = { "Authorization":("Bearer " + api_key) })
        try:
            response = urllib2.urlopen(req)
        except urllib2.HTTPError, error:
            printHttpError(error)
            return
        result = json.loads(response.read())
        status = result["StatusCode"]
        print "status:" + status
        if (status == 0 or status == "NotStarted"):
            print("Job " + job_id + " not yet started...")
        elif (status == 1 or status == "Running"):
            print("Job " + job_id + " running...")
        elif (status == 2 or status == "Failed"):
            print("Job " + job_id + " failed!")
            print("Error details: " + result["Details"])
            break
        elif (status == 3 or status == "Cancelled"):
            print("Job " + job_id + " cancelled!")
            break
        elif (status == 4 or status == "Finished"):
            print("Job " + job_id + " finished!")
            processResults(result)
            break
        time.sleep(1) # wait one second
    return
    invokeBatchExecutionService()
