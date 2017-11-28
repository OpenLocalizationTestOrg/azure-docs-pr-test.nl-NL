---
title: Informatie over het beheren van AzureML-webservices met behulp van API Management | Microsoft Docs
description: Een handleiding met het beheren van AzureML-webservices met behulp van API Management.
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
ms.openlocfilehash: 65eff3f4971f79886a840bb19bf76aaab48878de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="learn-how-to-manage-azureml-web-services-using-api-management"></a><span data-ttu-id="36e26-104">Informatie over het beheren van AzureML-webservices met API Management</span><span class="sxs-lookup"><span data-stu-id="36e26-104">Learn how to manage AzureML web services using API Management</span></span>
## <a name="overview"></a><span data-ttu-id="36e26-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="36e26-105">Overview</span></span>
<span data-ttu-id="36e26-106">Deze handleiding wordt beschreven hoe u snel aan de slag met API Management voor het beheren van de AzureML-webservices.</span><span class="sxs-lookup"><span data-stu-id="36e26-106">This guide shows you how to quickly get started using API Management to manage your AzureML web services.</span></span>

## <a name="what-is-azure-api-management"></a><span data-ttu-id="36e26-107">Wat is Azure API Management?</span><span class="sxs-lookup"><span data-stu-id="36e26-107">What is Azure API Management?</span></span>
<span data-ttu-id="36e26-108">Azure API Management is een Azure-service waarmee u uw REST-API-eindpunten beheren door gebruikerstoegang, beperking en bewaking van het dashboard te definiëren.</span><span class="sxs-lookup"><span data-stu-id="36e26-108">Azure API Management is an Azure service that lets you manage your REST API endpoints by defining user access, usage throttling, and dashboard monitoring.</span></span> <span data-ttu-id="36e26-109">Klik op [hier](https://azure.microsoft.com/services/api-management/) voor meer informatie over Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="36e26-109">Click [here](https://azure.microsoft.com/services/api-management/) for details on Azure API Management.</span></span> <span data-ttu-id="36e26-110">Klik op [hier](../api-management/api-management-get-started.md) voor richtlijnen voor het aan de slag met Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="36e26-110">Click [here](../api-management/api-management-get-started.md) for a guide on how to get started with Azure API Management.</span></span> <span data-ttu-id="36e26-111">Deze andere gids, die in deze handleiding is gebaseerd op, vindt meer onderwerpen, waaronder melding configuraties, laag prijzen, antwoord verwerking, gebruikersverificatie, producten, developer-abonnementen en gebruik dashboarding maken.</span><span class="sxs-lookup"><span data-stu-id="36e26-111">This other guide, which this guide is based on, covers more topics, including notification configurations, tier pricing, response handling, user authentication, creating products, developer subscriptions, and usage dashboarding.</span></span>

## <a name="what-is-azureml"></a><span data-ttu-id="36e26-112">Wat is AzureML?</span><span class="sxs-lookup"><span data-stu-id="36e26-112">What is AzureML?</span></span>
<span data-ttu-id="36e26-113">AzureML is een Azure-service voor machine learning-waarmee u eenvoudig ontwikkelen, implementeren en geavanceerde analyseoplossingen delen.</span><span class="sxs-lookup"><span data-stu-id="36e26-113">AzureML is an Azure service for machine learning that enables you to easily build, deploy, and share advanced analytics solutions.</span></span> <span data-ttu-id="36e26-114">Klik op [hier](https://azure.microsoft.com/services/machine-learning/) voor meer informatie over AzureML.</span><span class="sxs-lookup"><span data-stu-id="36e26-114">Click [here](https://azure.microsoft.com/services/machine-learning/) for details on AzureML.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36e26-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="36e26-115">Prerequisites</span></span>
<span data-ttu-id="36e26-116">Voor het voltooien van deze handleiding hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="36e26-116">To complete this guide, you need:</span></span>

* <span data-ttu-id="36e26-117">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="36e26-117">An Azure account.</span></span> <span data-ttu-id="36e26-118">Als u geen Azure-account hebt, klikt u op [hier](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie over het maken van een gratis proefaccount.</span><span class="sxs-lookup"><span data-stu-id="36e26-118">If you don’t have an Azure account, click [here](https://azure.microsoft.com/pricing/free-trial/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="36e26-119">Een AzureML-account.</span><span class="sxs-lookup"><span data-stu-id="36e26-119">An AzureML account.</span></span> <span data-ttu-id="36e26-120">Als u geen account voor met AzureML hebt, klikt u op [hier](https://studio.azureml.net/) voor meer informatie over het maken van een gratis proefaccount.</span><span class="sxs-lookup"><span data-stu-id="36e26-120">If you don’t have an AzureML account, click [here](https://studio.azureml.net/) for details on how to create a free trial account.</span></span>
* <span data-ttu-id="36e26-121">De werkruimte, service en api_key voor een AzureML-experiment geïmplementeerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="36e26-121">The workspace, service, and api_key for an AzureML experiment deployed as a web service.</span></span> <span data-ttu-id="36e26-122">Klik op [hier](machine-learning-create-experiment.md) voor meer informatie over het maken van een experiment AzureML.</span><span class="sxs-lookup"><span data-stu-id="36e26-122">Click [here](machine-learning-create-experiment.md) for details on how to create an AzureML experiment.</span></span> <span data-ttu-id="36e26-123">Klik op [hier](machine-learning-publish-a-machine-learning-web-service.md) voor meer informatie over het implementeren van een AzureML als een webservice experimenteren.</span><span class="sxs-lookup"><span data-stu-id="36e26-123">Click [here](machine-learning-publish-a-machine-learning-web-service.md) for details on how to deploy an AzureML experiment as a web service.</span></span> <span data-ttu-id="36e26-124">Bijlage A bevat ook instructies voor het maken en testen van een eenvoudig experiment van AzureML en als een webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="36e26-124">Alternately, Appendix A has instructions for how to create and test a simple AzureML experiment and deploy it as a web service.</span></span>

## <a name="create-an-api-management-instance"></a><span data-ttu-id="36e26-125">Een API Management-exemplaar maken</span><span class="sxs-lookup"><span data-stu-id="36e26-125">Create an API Management instance</span></span>
<span data-ttu-id="36e26-126">Hieronder vindt u de stappen voor het beheren van de AzureML-webservice met behulp van API Management.</span><span class="sxs-lookup"><span data-stu-id="36e26-126">Below are the steps for using API Management to manage your AzureML web service.</span></span> <span data-ttu-id="36e26-127">Maak eerst een service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="36e26-127">First create a service instance.</span></span> <span data-ttu-id="36e26-128">Meld u aan bij de [klassieke Portal](https://manage.windowsazure.com/) en klik op **nieuw** > **App Services** > **API Management**  >  **Maken**.</span><span class="sxs-lookup"><span data-stu-id="36e26-128">Log in to the [Classic Portal](https://manage.windowsazure.com/) and click **New** > **App Services** > **API Management** > **Create**.</span></span>

![instantie maken](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-instance.png)

<span data-ttu-id="36e26-130">Geef een unieke **URL**.</span><span class="sxs-lookup"><span data-stu-id="36e26-130">Specify a unique **URL**.</span></span> <span data-ttu-id="36e26-131">Maakt gebruik van deze handleiding **demoazureml** – moet u ervoor kiezen een iets andere betekenis.</span><span class="sxs-lookup"><span data-stu-id="36e26-131">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="36e26-132">Kies het gewenste **Abonnement** en de gewenste **Regio** voor uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="36e26-132">Choose the desired **Subscription** and **Region** for your service instance.</span></span> <span data-ttu-id="36e26-133">Klik na het maken van uw selecties op de knop Volgende.</span><span class="sxs-lookup"><span data-stu-id="36e26-133">After making your selections, click the next button.</span></span>

![maken van service 1](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-1.png)

<span data-ttu-id="36e26-135">Geef een waarde op voor de **organisatienaam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-135">Specify a value for the **Organization Name**.</span></span> <span data-ttu-id="36e26-136">Maakt gebruik van deze handleiding **demoazureml** – moet u ervoor kiezen een iets andere betekenis.</span><span class="sxs-lookup"><span data-stu-id="36e26-136">This guide uses **demoazureml** – you will need to choose something different.</span></span> <span data-ttu-id="36e26-137">Voer uw e-mailadres in de **e-mail beheerder** veld.</span><span class="sxs-lookup"><span data-stu-id="36e26-137">Enter your email address in the **administrator e-mail** field.</span></span> <span data-ttu-id="36e26-138">Dit e-mailadres wordt gebruikt voor meldingen van het API Management-systeem.</span><span class="sxs-lookup"><span data-stu-id="36e26-138">This email address is used for notifications from the API Management system.</span></span>

![maken van service 2](./media/machine-learning-manage-web-service-endpoints-using-api-management/create-service-2.png)

<span data-ttu-id="36e26-140">Schakel het selectievakje in om uw service-exemplaar te maken.</span><span class="sxs-lookup"><span data-stu-id="36e26-140">Click the check box to create your service instance.</span></span> <span data-ttu-id="36e26-141">*Het duurt dertig minuten duren voordat een nieuwe service moet worden gemaakt*.</span><span class="sxs-lookup"><span data-stu-id="36e26-141">*It takes up to thirty minutes for a new service to be created*.</span></span>

## <a name="create-the-api"></a><span data-ttu-id="36e26-142">De API maken</span><span class="sxs-lookup"><span data-stu-id="36e26-142">Create the API</span></span>
<span data-ttu-id="36e26-143">Zodra het service-exemplaar is gemaakt, wordt de volgende stap is het maken van de API.</span><span class="sxs-lookup"><span data-stu-id="36e26-143">Once the service instance is created, the next step is to create the API.</span></span> <span data-ttu-id="36e26-144">Een API bestaat uit een reeks bewerkingen die vanuit een clienttoepassing kunnen worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="36e26-144">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="36e26-145">API-bewerkingen worden geproxied naar bestaande webservices.</span><span class="sxs-lookup"><span data-stu-id="36e26-145">API operations are proxied to existing web services.</span></span> <span data-ttu-id="36e26-146">Deze handleiding maakt API's aan de bestaande webservices AzureML RRS en BES proxyinstellingen.</span><span class="sxs-lookup"><span data-stu-id="36e26-146">This guide creates APIs that proxy to the existing AzureML RRS and BES web services.</span></span>

<span data-ttu-id="36e26-147">API's worden gemaakt en geconfigureerd via de API-publicatieportal, die wordt geopend via de klassieke Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="36e26-147">APIs are created and configured from the API publisher portal, which is accessed through the Azure Classic Portal.</span></span> <span data-ttu-id="36e26-148">De als publicatieportal wilt openen, selecteer uw service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="36e26-148">To reach the publisher portal, select your service instance.</span></span>

![Selecteer-service-exemplaar](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-service-instance.png)

<span data-ttu-id="36e26-150">Klik op **beheren** in de klassieke Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="36e26-150">Click **Manage** in the Azure Classic Portal for your API Management service.</span></span>

![beheren-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/manage-service.png)

<span data-ttu-id="36e26-152">Klik op **API's** van de **API Management** menu aan de linkerkant en klik vervolgens op **API toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="36e26-152">Click **APIs** from the **API Management** menu on the left, and then click **Add API**.</span></span>

![menu-beheer-API](./media/machine-learning-manage-web-service-endpoints-using-api-management/api-management-menu.png)

<span data-ttu-id="36e26-154">Type **AzureML Demo API** als de **Web API-naam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-154">Type **AzureML Demo API** as the **Web API name**.</span></span> <span data-ttu-id="36e26-155">Type **https://ussouthcentral.services.azureml.net** als de **webservice-URL**.</span><span class="sxs-lookup"><span data-stu-id="36e26-155">Type **https://ussouthcentral.services.azureml.net** as the **Web service URL**.</span></span> <span data-ttu-id="36e26-156">Type **azureml-demo** als de **achtervoegsel URL Web-API**.</span><span class="sxs-lookup"><span data-stu-id="36e26-156">Type **azureml-demo** as the **Web API URL suffix**.</span></span> <span data-ttu-id="36e26-157">Controleer **HTTPS** als de **URL Web-API** schema.</span><span class="sxs-lookup"><span data-stu-id="36e26-157">Check **HTTPS** as the **Web API URL** scheme.</span></span> <span data-ttu-id="36e26-158">Selecteer **Starter** als **producten**.</span><span class="sxs-lookup"><span data-stu-id="36e26-158">Select **Starter** as **Products**.</span></span> <span data-ttu-id="36e26-159">Wanneer u klaar bent, klikt u op **opslaan** voor het maken van de API.</span><span class="sxs-lookup"><span data-stu-id="36e26-159">When finished, click **Save** to create the API.</span></span>

![nieuwe-api toevoegen](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-new-api.png)

## <a name="add-the-operations"></a><span data-ttu-id="36e26-161">De bewerkingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="36e26-161">Add the operations</span></span>
<span data-ttu-id="36e26-162">Klik op **toevoegbewerking** bewerkingen toevoegen aan deze API.</span><span class="sxs-lookup"><span data-stu-id="36e26-162">Click **Add operation** to add operations to this API.</span></span>

![toevoegen-bewerking](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-operation.png)

<span data-ttu-id="36e26-164">De **nieuwe bewerking** venster wordt weergegeven en de **handtekening** tabblad wordt standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="36e26-164">The **New operation** window will be displayed and the **Signature** tab will be selected by default.</span></span>

## <a name="add-rrs-operation"></a><span data-ttu-id="36e26-165">RRS bewerking toevoegen</span><span class="sxs-lookup"><span data-stu-id="36e26-165">Add RRS Operation</span></span>
<span data-ttu-id="36e26-166">Maak eerst een bewerking voor de AzureML RRS-service.</span><span class="sxs-lookup"><span data-stu-id="36e26-166">First create an operation for the AzureML RRS service.</span></span> <span data-ttu-id="36e26-167">Selecteer **POST** als de **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="36e26-167">Select **POST** as the **HTTP verb**.</span></span> <span data-ttu-id="36e26-168">Type **/workspaces/ {werkruimte} /services/ {service} / execute? api-version = {apiversion} & details = {details}** als de **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="36e26-168">Type **/workspaces/{workspace}/services/{service}/execute?api-version={apiversion}&details={details}** as the **URL template**.</span></span> <span data-ttu-id="36e26-169">Type **RRS uitvoeren** als de **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-169">Type **RRS Execute** as the **Display name**.</span></span>

![rrs-bewerking-handtekening toevoegen](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-signature.png)

<span data-ttu-id="36e26-171">Klik op **antwoorden** > **toevoegen** op de linkerkant en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="36e26-171">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="36e26-172">Klik op **opslaan** opslaan van deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="36e26-172">Click **Save** to save this operation.</span></span>

![toevoegen-rrs--bewerkingsantwoord](./media/machine-learning-manage-web-service-endpoints-using-api-management/add-rrs-operation-response.png)

## <a name="add-bes-operations"></a><span data-ttu-id="36e26-174">BES bewerkingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="36e26-174">Add BES Operations</span></span>
<span data-ttu-id="36e26-175">Schermopnamen worden niet vermeld voor de BES bewerkingen zoals ze vergelijkbaar met die zijn voor de bewerking Bronrecords toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="36e26-175">Screenshots are not included for the BES operations as they are very similar to those for adding the RRS operation.</span></span>

### <a name="submit-but-not-start-a-batch-execution-job"></a><span data-ttu-id="36e26-176">Een taak Batchuitvoering verzenden (maar niet worden gestart)</span><span class="sxs-lookup"><span data-stu-id="36e26-176">Submit (but not start) a Batch Execution job</span></span>
<span data-ttu-id="36e26-177">Klik op **toevoegbewerking** de bewerking voor met AzureML BES toevoegen aan de API.</span><span class="sxs-lookup"><span data-stu-id="36e26-177">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="36e26-178">Selecteer **POST** voor de **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="36e26-178">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="36e26-179">Type **/workspaces/ {werkruimte} /services/ {service} / taken? api-version = {apiversion}** voor de **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="36e26-179">Type **/workspaces/{workspace}/services/{service}/jobs?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="36e26-180">Type **BES indienen** voor de **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-180">Type **BES Submit** for the **Display name**.</span></span> <span data-ttu-id="36e26-181">Klik op **antwoorden** > **toevoegen** op de linkerkant en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="36e26-181">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="36e26-182">Klik op **opslaan** opslaan van deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="36e26-182">Click **Save** to save this operation.</span></span>

### <a name="start-a-batch-execution-job"></a><span data-ttu-id="36e26-183">Een taak Batchuitvoering starten</span><span class="sxs-lookup"><span data-stu-id="36e26-183">Start a Batch Execution job</span></span>
<span data-ttu-id="36e26-184">Klik op **toevoegbewerking** de bewerking voor met AzureML BES toevoegen aan de API.</span><span class="sxs-lookup"><span data-stu-id="36e26-184">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="36e26-185">Selecteer **POST** voor de **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="36e26-185">Select **POST** for the **HTTP verb**.</span></span> <span data-ttu-id="36e26-186">Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid} / starten? api-version = {apiversion}** voor de **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="36e26-186">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}/start?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="36e26-187">Type **BES Start** voor de **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-187">Type **BES Start** for the **Display name**.</span></span> <span data-ttu-id="36e26-188">Klik op **antwoorden** > **toevoegen** op de linkerkant en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="36e26-188">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="36e26-189">Klik op **opslaan** opslaan van deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="36e26-189">Click **Save** to save this operation.</span></span>

### <a name="get-the-status-or-result-of-a-batch-execution-job"></a><span data-ttu-id="36e26-190">De status of het resultaat van een taak Batchuitvoering ophalen</span><span class="sxs-lookup"><span data-stu-id="36e26-190">Get the status or result of a Batch Execution job</span></span>
<span data-ttu-id="36e26-191">Klik op **toevoegbewerking** de bewerking voor met AzureML BES toevoegen aan de API.</span><span class="sxs-lookup"><span data-stu-id="36e26-191">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="36e26-192">Selecteer **ophalen** voor de **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="36e26-192">Select **GET** for the **HTTP verb**.</span></span> <span data-ttu-id="36e26-193">Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid}? api-version = {apiversion}** voor de **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="36e26-193">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="36e26-194">Type **BES Status** voor de **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-194">Type **BES Status** for the **Display name**.</span></span> <span data-ttu-id="36e26-195">Klik op **antwoorden** > **toevoegen** op de linkerkant en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="36e26-195">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="36e26-196">Klik op **opslaan** opslaan van deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="36e26-196">Click **Save** to save this operation.</span></span>

### <a name="delete-a-batch-execution-job"></a><span data-ttu-id="36e26-197">Een taak Batchuitvoering verwijderen</span><span class="sxs-lookup"><span data-stu-id="36e26-197">Delete a Batch Execution job</span></span>
<span data-ttu-id="36e26-198">Klik op **toevoegbewerking** de bewerking voor met AzureML BES toevoegen aan de API.</span><span class="sxs-lookup"><span data-stu-id="36e26-198">Click **add operation** to add the AzureML BES operation to the API.</span></span> <span data-ttu-id="36e26-199">Selecteer **verwijderen** voor de **HTTP-term**.</span><span class="sxs-lookup"><span data-stu-id="36e26-199">Select **DELETE** for the **HTTP verb**.</span></span> <span data-ttu-id="36e26-200">Type **/workspaces/ {werkruimte} /services/ {service} /jobs/ {jobid}? api-version = {apiversion}** voor de **URL sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="36e26-200">Type **/workspaces/{workspace}/services/{service}/jobs/{jobid}?api-version={apiversion}** for the **URL template**.</span></span> <span data-ttu-id="36e26-201">Type **BES verwijderen** voor de **weergavenaam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-201">Type **BES Delete** for the **Display name**.</span></span> <span data-ttu-id="36e26-202">Klik op **antwoorden** > **toevoegen** op de linkerkant en selecteer **200 OK**.</span><span class="sxs-lookup"><span data-stu-id="36e26-202">Click **Responses** > **ADD** on the left and select **200 OK**.</span></span> <span data-ttu-id="36e26-203">Klik op **opslaan** opslaan van deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="36e26-203">Click **Save** to save this operation.</span></span>

## <a name="call-an-operation-from-the-developer-portal"></a><span data-ttu-id="36e26-204">Een bewerking aanroepen vanuit de ontwikkelaarsportal</span><span class="sxs-lookup"><span data-stu-id="36e26-204">Call an operation from the Developer Portal</span></span>
<span data-ttu-id="36e26-205">Bewerkingen kunnen rechtstreeks vanuit de portal voor ontwikkelaars die biedt een handige manier om te bekijken en testen van de bewerkingen van een API worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="36e26-205">Operations can be called directly from the Developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="36e26-206">In deze handleiding stap roept u de **RRS uitvoeren** methode die is toegevoegd aan de **AzureML Demo API**.</span><span class="sxs-lookup"><span data-stu-id="36e26-206">In this guide step you will call the **RRS Execute** method that was added to the **AzureML Demo API**.</span></span> <span data-ttu-id="36e26-207">Klik op **ontwikkelaarsportal** in het menu aan de bovenkant rechtsboven in de klassieke Portal.</span><span class="sxs-lookup"><span data-stu-id="36e26-207">Click **Developer portal** from the menu at the top right of the Classic Portal.</span></span>

![portal voor ontwikkelaars](./media/machine-learning-manage-web-service-endpoints-using-api-management/developer-portal.png)

<span data-ttu-id="36e26-209">Klik op **API's** van het bovenste menu en klik op **AzureML Demo API** om de beschikbare bewerkingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="36e26-209">Click **APIs** from the top menu, and then click **AzureML Demo API** to see the operations available.</span></span>

![demoazureml-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/demoazureml-api.png)

<span data-ttu-id="36e26-211">Selecteer **RRS uitvoeren** voor de bewerking.</span><span class="sxs-lookup"><span data-stu-id="36e26-211">Select **RRS Execute** for the operation.</span></span> <span data-ttu-id="36e26-212">Klik op **Try It**.</span><span class="sxs-lookup"><span data-stu-id="36e26-212">Click **Try It**.</span></span>

![Try it](./media/machine-learning-manage-web-service-endpoints-using-api-management/try-it.png)

<span data-ttu-id="36e26-214">Aanvraagparameters, typt u uw **werkruimte**, **service**, **2.0** voor de **apiversion**, en **waar**voor de **details**.</span><span class="sxs-lookup"><span data-stu-id="36e26-214">For Request parameters, type your **workspace**,  **service**, **2.0** for the **apiversion**, and  **true** for the **details**.</span></span> <span data-ttu-id="36e26-215">U vindt uw **werkruimte** en **service** in het dashboard voor met AzureML web service (Zie **testen van de webservice** in bijlage A).</span><span class="sxs-lookup"><span data-stu-id="36e26-215">You can find your **workspace** and **service** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="36e26-216">Aanvraagheaders, klikt u op **header toevoegen** en het type **Content-Type** en **application/json**, klikt u vervolgens op **header toevoegen** en het type  **Autorisatie** en **Bearer <YOUR AZUREML SERVICE API-KEY>** .</span><span class="sxs-lookup"><span data-stu-id="36e26-216">For Request headers, click **Add header** and type **Content-Type** and **application/json**, then click **Add header** and type **Authorization** and **Bearer <YOUR AZUREML SERVICE API-KEY>**.</span></span> <span data-ttu-id="36e26-217">U vindt uw **api-sleutel** in het dashboard voor met AzureML web service (Zie **testen van de webservice** in bijlage A).</span><span class="sxs-lookup"><span data-stu-id="36e26-217">You can find your **api key** in the AzureML web service dashboard (see **Test the web service** in Appendix A).</span></span>

<span data-ttu-id="36e26-218">Type **{'Invoer': {"input1": {'ColumnNames': ["Col2"] "waarden": [[' Dit is een goede dag']]}}, "GlobalParameters": {}}** voor de aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="36e26-218">Type **{"Inputs": {"input1": {"ColumnNames": ["Col2"], "Values": [["This is a good day"]]}}, "GlobalParameters": {}}** for the request body.</span></span>

![azureml-demo-api](./media/machine-learning-manage-web-service-endpoints-using-api-management/azureml-demo-api.png)

<span data-ttu-id="36e26-220">Klik op **verzenden**.</span><span class="sxs-lookup"><span data-stu-id="36e26-220">Click **Send**.</span></span>

![Verzenden](./media/machine-learning-manage-web-service-endpoints-using-api-management/send.png)

<span data-ttu-id="36e26-222">Nadat een bewerking is aangeroepen, de ontwikkelaarsportal de **aangevraagde URL** van de back-end-service de **antwoordstatus**, wordt de **antwoordheaders**, en eventuele  **Antwoordinhoud**.</span><span class="sxs-lookup"><span data-stu-id="36e26-222">After an operation is invoked, the developer portal displays the **Requested URL** from the back-end service, the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![status van het antwoord](./media/machine-learning-manage-web-service-endpoints-using-api-management/response-status.png)

## <a name="appendix-a---creating-and-testing-a-simple-azureml-web-service"></a><span data-ttu-id="36e26-224">Bijlage A - maken en testen van een eenvoudige AzureML-webservice</span><span class="sxs-lookup"><span data-stu-id="36e26-224">Appendix A - Creating and testing a simple AzureML web service</span></span>
### <a name="creating-the-experiment"></a><span data-ttu-id="36e26-225">Het experiment maken</span><span class="sxs-lookup"><span data-stu-id="36e26-225">Creating the experiment</span></span>
<span data-ttu-id="36e26-226">Hieronder volgen de stappen voor het maken van een eenvoudig experiment van AzureML en deze is geïmplementeerd als een webservice.</span><span class="sxs-lookup"><span data-stu-id="36e26-226">Below are the steps for creating a simple AzureML experiment and deploying it as a web service.</span></span> <span data-ttu-id="36e26-227">De service wordt als een kolom van willekeurige tekst invoeren en retourneert een reeks functies die worden weergegeven als gehele getallen zijn.</span><span class="sxs-lookup"><span data-stu-id="36e26-227">The web service takes as input a column of arbitrary text and returns a set of features represented as integers.</span></span> <span data-ttu-id="36e26-228">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="36e26-228">For example:</span></span>

| <span data-ttu-id="36e26-229">Tekst</span><span class="sxs-lookup"><span data-stu-id="36e26-229">Text</span></span> | <span data-ttu-id="36e26-230">Gecodeerde tekst</span><span class="sxs-lookup"><span data-stu-id="36e26-230">Hashed Text</span></span> |
| --- | --- |
| <span data-ttu-id="36e26-231">Dit is een goede dag</span><span class="sxs-lookup"><span data-stu-id="36e26-231">This is a good day</span></span> |<span data-ttu-id="36e26-232">1 1 2 2 0 2 0 1</span><span class="sxs-lookup"><span data-stu-id="36e26-232">1 1 2 2 0 2 0 1</span></span> |

<span data-ttu-id="36e26-233">Eerst met een browser naar keuze, gaat u naar: [https://studio.azureml.net/](https://studio.azureml.net/) en voer uw referenties aan te melden.</span><span class="sxs-lookup"><span data-stu-id="36e26-233">First, using a browser of your choice, navigate to: [https://studio.azureml.net/](https://studio.azureml.net/) and enter your credentials to log in.</span></span> <span data-ttu-id="36e26-234">Maak vervolgens een nieuw, leeg experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-234">Next, create a new blank experiment.</span></span>

![experiment-sjablonen voor het zoeken](./media/machine-learning-manage-web-service-endpoints-using-api-management/search-experiment-templates.png)

<span data-ttu-id="36e26-236">De naam in **SimpleFeatureHashingExperiment**.</span><span class="sxs-lookup"><span data-stu-id="36e26-236">Rename it to **SimpleFeatureHashingExperiment**.</span></span> <span data-ttu-id="36e26-237">Vouw **gegevenssets opgeslagen** en sleep **adresboek beoordelingen van Amazon** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-237">Expand **Saved Datasets** and drag **Book Reviews from Amazon** onto your experiment.</span></span>

![eenvoudige-functie-hashing-experiment](./media/machine-learning-manage-web-service-endpoints-using-api-management/simple-feature-hashing-experiment.png)

<span data-ttu-id="36e26-239">Vouw **Data Transformation** en **manipulatie** en sleep **Select Columns in Dataset** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-239">Expand **Data Transformation** and **Manipulation** and drag **Select Columns in Dataset** onto your experiment.</span></span> <span data-ttu-id="36e26-240">Verbinding maken met **boek beoordelingen van Amazon** naar **kolommen in gegevensset selecteren**.</span><span class="sxs-lookup"><span data-stu-id="36e26-240">Connect **Book Reviews from Amazon** to **Select Columns in Dataset**.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/project-columns.png)

<span data-ttu-id="36e26-242">Klik op **Select Columns in Dataset** en klik vervolgens op **Launch column selector** en selecteer **Col2**.</span><span class="sxs-lookup"><span data-stu-id="36e26-242">Click **Select Columns in Dataset** and then click **Launch column selector** and select **Col2**.</span></span> <span data-ttu-id="36e26-243">Klik op het vinkje om deze wijzigingen van kracht.</span><span class="sxs-lookup"><span data-stu-id="36e26-243">Click the checkmark to apply these changes.</span></span>

![select-columns](./media/machine-learning-manage-web-service-endpoints-using-api-management/select-columns.png)

<span data-ttu-id="36e26-245">Vouw **Tekstanalyse** en sleep **hash-functie** naar het experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-245">Expand **Text Analytics** and drag **Feature Hashing** onto the experiment.</span></span> <span data-ttu-id="36e26-246">Verbinding maken met **kolommen in gegevensset selecteren** naar **hash-functie**.</span><span class="sxs-lookup"><span data-stu-id="36e26-246">Connect **Select Columns in Dataset** to **Feature Hashing**.</span></span>

![verbinding maken met project kolommen](./media/machine-learning-manage-web-service-endpoints-using-api-management/connect-project-columns.png)

<span data-ttu-id="36e26-248">Type **3** voor de **bitsize Hashing**.</span><span class="sxs-lookup"><span data-stu-id="36e26-248">Type **3** for the **Hashing bitsize**.</span></span> <span data-ttu-id="36e26-249">Hiermee maakt u 8 (23) kolommen.</span><span class="sxs-lookup"><span data-stu-id="36e26-249">This will create 8 (23) columns.</span></span>

![hashing bitsize](./media/machine-learning-manage-web-service-endpoints-using-api-management/hashing-bitsize.png)

<span data-ttu-id="36e26-251">U wilt op dit moment klikken **uitvoeren** voor het testen van het experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-251">At this point, you may want to click **Run** to test the experiment.</span></span>

![uitvoeren](./media/machine-learning-manage-web-service-endpoints-using-api-management/run.png)

### <a name="create-a-web-service"></a><span data-ttu-id="36e26-253">Een webservice maken</span><span class="sxs-lookup"><span data-stu-id="36e26-253">Create a web service</span></span>
<span data-ttu-id="36e26-254">Maak nu een webservice.</span><span class="sxs-lookup"><span data-stu-id="36e26-254">Now create a web service.</span></span> <span data-ttu-id="36e26-255">Vouw **webservice** en sleep **invoer** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-255">Expand **Web Service** and drag **Input** onto your experiment.</span></span> <span data-ttu-id="36e26-256">Verbinding maken met **invoer** naar **hash-functie**.</span><span class="sxs-lookup"><span data-stu-id="36e26-256">Connect **Input** to **Feature Hashing**.</span></span> <span data-ttu-id="36e26-257">Ook slepen **uitvoer** naar uw experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-257">Also drag **output** onto your experiment.</span></span> <span data-ttu-id="36e26-258">Verbinding maken met **uitvoer** naar **hash-functie**.</span><span class="sxs-lookup"><span data-stu-id="36e26-258">Connect **Output** to **Feature Hashing**.</span></span>

![output-naar--hash-functies](./media/machine-learning-manage-web-service-endpoints-using-api-management/output-to-feature-hashing.png)

<span data-ttu-id="36e26-260">Klik op **publiceren webservice**.</span><span class="sxs-lookup"><span data-stu-id="36e26-260">Click **Publish web service**.</span></span>

![publiceren-web-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/publish-web-service.png)

<span data-ttu-id="36e26-262">Klik op **Ja** voor het publiceren van het experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-262">Click **Yes** to publish the experiment.</span></span>

![Ja om te publiceren](./media/machine-learning-manage-web-service-endpoints-using-api-management/yes-to-publish.png)

### <a name="test-the-web-service"></a><span data-ttu-id="36e26-264">De webservice testen</span><span class="sxs-lookup"><span data-stu-id="36e26-264">Test the web service</span></span>
<span data-ttu-id="36e26-265">Een webservice AzureML bestaat uit RSS (aanvraag/antwoord-service) en eindpunten van BES (batch uitvoering service).</span><span class="sxs-lookup"><span data-stu-id="36e26-265">An AzureML web service consists of RSS (request/response service) and BES (batch execution service) endpoints.</span></span> <span data-ttu-id="36e26-266">RSS is voor synchrone uitvoering.</span><span class="sxs-lookup"><span data-stu-id="36e26-266">RSS is for synchronous execution.</span></span> <span data-ttu-id="36e26-267">BES is voor het uitvoeren van asynchrone taak.</span><span class="sxs-lookup"><span data-stu-id="36e26-267">BES is for asynchronous job execution.</span></span> <span data-ttu-id="36e26-268">Als u wilt testen van uw web-service met het onderstaande voorbeeld Python bron, wellicht moet u download en installeer de Azure SDK voor Python (Zie: [het installeren van Python](../python-how-to-install.md)).</span><span class="sxs-lookup"><span data-stu-id="36e26-268">To test your web service with the sample Python source below, you may need to download and install the Azure SDK for Python (see: [How to install Python](../python-how-to-install.md)).</span></span>

<span data-ttu-id="36e26-269">U moet ook de **werkruimte**, **service**, en **api_key** van uw experiment voor het onderstaande voorbeeld de gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="36e26-269">You will also need the **workspace**, **service**, and **api_key** of your experiment for the sample source below.</span></span> <span data-ttu-id="36e26-270">U kunt de werkruimte en de service vinden door te klikken op **aanvragen/reacties** of **Batchuitvoering** voor uw experiment in het dashboard van web service.</span><span class="sxs-lookup"><span data-stu-id="36e26-270">You can find the workspace and service by clicking either **Request/Response** or **Batch Execution** for your experiment in the web service dashboard.</span></span>

![Zoek-werkruimte-en-service](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-workspace-and-service.png)

<span data-ttu-id="36e26-272">U vindt de **api_key** door te klikken op uw experiment in het dashboard van web service.</span><span class="sxs-lookup"><span data-stu-id="36e26-272">You can find the **api_key** by clicking your experiment in the web service dashboard.</span></span>

![zoeken-api-sleutel](./media/machine-learning-manage-web-service-endpoints-using-api-management/find-api-key.png)

#### <a name="test-rrs-endpoint"></a><span data-ttu-id="36e26-274">Test RRS-eindpunt</span><span class="sxs-lookup"><span data-stu-id="36e26-274">Test RRS endpoint</span></span>
##### <a name="test-button"></a><span data-ttu-id="36e26-275">Knop Testen</span><span class="sxs-lookup"><span data-stu-id="36e26-275">Test button</span></span>
<span data-ttu-id="36e26-276">Een eenvoudige manier voor het testen van het eindpunt RRS is te klikken op **testen** op het web service-dashboard.</span><span class="sxs-lookup"><span data-stu-id="36e26-276">An easy way to test the RRS endpoint is to click **Test** on the web service dashboard.</span></span>

![Test](./media/machine-learning-manage-web-service-endpoints-using-api-management/test.png)

<span data-ttu-id="36e26-278">Type **dit is een goede dag** voor **col2**.</span><span class="sxs-lookup"><span data-stu-id="36e26-278">Type **This is a good day** for **col2**.</span></span> <span data-ttu-id="36e26-279">Klik op het vinkje.</span><span class="sxs-lookup"><span data-stu-id="36e26-279">Click the checkmark.</span></span>

![Geef gegevens](./media/machine-learning-manage-web-service-endpoints-using-api-management/enter-data.png)

<span data-ttu-id="36e26-281">U ziet ongeveer</span><span class="sxs-lookup"><span data-stu-id="36e26-281">You will see something like</span></span>

![Voorbeeld van uitvoer](./media/machine-learning-manage-web-service-endpoints-using-api-management/sample-output.png)

##### <a name="sample-code"></a><span data-ttu-id="36e26-283">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="36e26-283">Sample Code</span></span>
<span data-ttu-id="36e26-284">Een andere manier voor het testen van uw RRS is vanuit uw clientcode.</span><span class="sxs-lookup"><span data-stu-id="36e26-284">Another way to test your RRS is from your client code.</span></span> <span data-ttu-id="36e26-285">Als u op **aanvragen/reacties** op het dashboard en Ga naar de onderkant verschijnt voorbeeldcode voor C#, Python en R. U ziet ook de syntaxis van de aanvraag RRS, met inbegrip van de aanvraag-URI, kopteksten en hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="36e26-285">If you click **Request/response** on the dashboard and scroll to the bottom, you will see sample code for C#, Python, and R. You will also see the syntax of the RRS request, including the request URI, headers, and body.</span></span>

<span data-ttu-id="36e26-286">Deze handleiding ziet u een werkende Python-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="36e26-286">This guide shows a working Python example.</span></span> <span data-ttu-id="36e26-287">U moet aanpassen zodat deze met de **werkruimte**, **service**, en **api_key** van uw experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-287">You will need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span>

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
        print("The request failed with status code: " + str(error.code))
        print(error.info())
        print(json.loads(error.read()))

#### <a name="test-bes-endpoint"></a><span data-ttu-id="36e26-288">Test BES eindpunt</span><span class="sxs-lookup"><span data-stu-id="36e26-288">Test BES endpoint</span></span>
<span data-ttu-id="36e26-289">Klik op **Batchuitvoering** op het dashboard en Ga naar de onderkant.</span><span class="sxs-lookup"><span data-stu-id="36e26-289">Click **Batch execution** on the dashboard and scroll to the bottom.</span></span> <span data-ttu-id="36e26-290">Ziet u voorbeelden van code voor C#, Python en R. Ook ziet u de syntaxis van de BES aanvragen voor het verzenden van een taak, een taak starten, de status of de resultaten van een taak ophalen en verwijderen van een taak.</span><span class="sxs-lookup"><span data-stu-id="36e26-290">You will see sample code for C#, Python, and R. You will also see the syntax of the BES requests to submit a job, start a job, get the status or results of a job, and delete a job.</span></span>

<span data-ttu-id="36e26-291">Deze handleiding ziet u een werkende Python-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="36e26-291">This guide shows a working Python example.</span></span> <span data-ttu-id="36e26-292">U wilt wijzigen met de **werkruimte**, **service**, en **api_key** van uw experiment.</span><span class="sxs-lookup"><span data-stu-id="36e26-292">You need to modify it with the **workspace**, **service**, and **api_key** of your experiment.</span></span> <span data-ttu-id="36e26-293">Bovendien moet u wijzigen de **opslagaccountnaam**, **opslagaccountsleutel**, en **opslag containernaam**.</span><span class="sxs-lookup"><span data-stu-id="36e26-293">Additionally, you need to modify the **storage account name**, **storage account key**, and **storage container name**.</span></span> <span data-ttu-id="36e26-294">Tot slot moet u wijzigen van de locatie van de **invoerbestand** en de locatie van de **uitvoerbestand**.</span><span class="sxs-lookup"><span data-stu-id="36e26-294">Lastly, you will need to modify the location of the **input file** and the location of the **output file**.</span></span>

    import urllib2
    import json
    import time
    from azure.storage import *
    workspace = "<REPLACE WITH YOUR WORKSPACE ID>"
    service = "<REPLACE WITH YOUR SERVICE ID>"
    api_key = "<REPLACE WITH THE API KEY FOR YOUR WEB SERVICE>"
    storage_account_name = "<REPLACE WITH YOUR AZURE STORAGE ACCOUNT NAME>"
    storage_account_key = "<REPLACE WITH YOUR AZURE STORAGE KEY>"
    storage_container_name = "<REPLACE WITH YOUR AZURE STORAGE CONTAINER NAME>"
    input_file = "<REPLACE WITH THE LOCATION OF YOUR INPUT FILE>" # Example: C:\\mydata.csv
    output_file = "<REPLACE WITH THE LOCATION OF YOUR OUTPUT FILE>" # Example: C:\\myresults.csv
    input_blob_name = "mydatablob.csv"
    output_blob_name = "myresultsblob.csv"
    def printHttpError(httpError):
    print("The request failed with status code: " + str(httpError.code))
    print(httpError.info())
    print(json.loads(httpError.read()))
    return
    def saveBlobToFile(blobUrl, resultsLabel):
    print("Reading the result from " + blobUrl)
    try:
        response = urllib2.urlopen(blobUrl)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    with open(output_file, "w+") as f:
        f.write(response.read())
    print(resultsLabel + " have been written to the file " + output_file)
    return
    def processResults(result):
    first = True
    results = result["Results"]
    for outputName in results:
        result_blob_location = results[outputName]
        sas_token = result_blob_location["SasBlobToken"]
        base_url = result_blob_location["BaseLocation"]
        relative_url = result_blob_location["RelativeLocation"]
        print("The results for " + outputName + " are available at the following Azure Storage location:")
        print("BaseLocation: " + base_url)
        print("RelativeLocation: " + relative_url)
        print("SasBlobToken: " + sas_token)
        if (first):
            first = False
            url3 = base_url + relative_url + sas_token
            saveBlobToFile(url3, "The results for " + outputName)
    return

    def invokeBatchExecutionService():
    url = "https://ussouthcentral.services.azureml.net/workspaces/" + workspace +"/services/" + service +"/jobs"
    blob_service = BlobService(account_name=storage_account_name, account_key=storage_account_key)
    print("Uploading the input to blob storage...")
    data_to_upload = open(input_file, "r").read()
    blob_service.put_blob(storage_container_name, input_blob_name, data_to_upload, x_ms_blob_type="BlockBlob")
    print "Uploaded the input to blob storage"
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
    print("Submitting the job...")
    # submit the job
    req = urllib2.Request(url + "?api-version=2.0", body, headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    result = response.read()
    job_id = result[1:-1] # remove the enclosing double-quotes
    print("Job ID: " + job_id)
    # start the job
    print("Starting the job...")
    req = urllib2.Request(url + "/" + job_id + "/start?api-version=2.0", "", headers)
    try:
        response = urllib2.urlopen(req)
    except urllib2.HTTPError, error:
        printHttpError(error)
        return
    url2 = url + "/" + job_id + "?api-version=2.0"

    while True:
        print("Checking the job status...")
        # If you are using Python 3+, replace urllib2 with urllib.request in the follwing code
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
