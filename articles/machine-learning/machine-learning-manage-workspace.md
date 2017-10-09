---
title: een Machine Learning-werkruimte aaaManage | Microsoft Docs
description: Toegang tooAzure Machine Learning werkruimten, beheren en implementeren en beheren van ML API-webservices
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="39d73-103">Een Azure Machine Learning-werkruimte beheren</span><span class="sxs-lookup"><span data-stu-id="39d73-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="39d73-104">Zie voor meer informatie over het beheren van Web-services Hallo Machine Learning-webservices portal [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="39d73-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="39d73-105">U kunt de werkruimten Machine Learning in beide hello Azure-portal beheren of Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="39d73-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="39d73-106">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="39d73-106">Use hello Azure portal</span></span>

<span data-ttu-id="39d73-107">toomanage een werkruimte in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="39d73-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="39d73-108">Meld u aan toohello [Azure-portal](https://portal.azure.com/) met een administrator-account Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="39d73-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="39d73-109">Voer 'machine learning werkruimten' in het zoekvak Hallo bovenaan Hallo Hallo pagina, en selecteer vervolgens **Machine Learning-werkruimten**.</span><span class="sxs-lookup"><span data-stu-id="39d73-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="39d73-110">Klik op de gewenste toomanage Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="39d73-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="39d73-111">Bovendien toohello standaard resource management informatie en opties die beschikbaar zijn, kunt u:</span><span class="sxs-lookup"><span data-stu-id="39d73-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="39d73-112">Weergave **eigenschappen** : deze pagina Hallo werkruimte en resource-informatie wordt weergegeven en kunt u Hallo-abonnement en resourcegroep die deze werkruimte is verbonden met.</span><span class="sxs-lookup"><span data-stu-id="39d73-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="39d73-113">**Opslagsleutels Resync** -Hallo werkruimte onderhoudt sleutels toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="39d73-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="39d73-114">Als sleutels Hallo storage-account wordt gewijzigd, wordt u kunt klikken op **sleutels synchroniseren** toosynchronize Hallo sleutels met Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="39d73-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="39d73-115">toomanage Hallo-webservices die zijn gekoppeld aan deze werkruimte Hallo Machine Learning-webservices portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39d73-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="39d73-116">Zie [hello Azure Machine Learning-webservices portal met een webservice beheren](machine-learning-manage-new-webservice.md) voor volledige informatie.</span><span class="sxs-lookup"><span data-stu-id="39d73-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="39d73-117">toodeploy of beheren van nieuwe webservices, moet u zijn toegewezen medewerker of beheerdersrol op Hallo abonnement toowhich Hallo-webservice wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="39d73-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="39d73-118">Als u een andere gebruiker tooa machine learning-werkruimte uitnodigen, moet u ze toewijzen als tooa Inzender of administrator-rol op Hallo abonnement voordat ze kunnen implementeren of beheren van webservices.</span><span class="sxs-lookup"><span data-stu-id="39d73-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="39d73-119">Zie voor meer informatie over toegangsmachtigingen instellen [toegangstoewijzingen weergeven voor gebruikers en groepen in Azure portal - openbare preview Hallo](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="39d73-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="39d73-120">Hallo klassieke Azure-portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="39d73-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="39d73-121">Hallo klassieke Azure-portal kunt u uw werkruimten Machine Learning om te beheren:</span><span class="sxs-lookup"><span data-stu-id="39d73-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="39d73-122">Controleren hoe Hallo werkruimte wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="39d73-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="39d73-123">Hallo werkruimte tooallow configureren of weigeren van toegang</span><span class="sxs-lookup"><span data-stu-id="39d73-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="39d73-124">Webservices die zijn gemaakt in de werkruimte Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="39d73-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="39d73-125">Hallo werkruimte verwijderen</span><span class="sxs-lookup"><span data-stu-id="39d73-125">Delete hello workspace</span></span>

<span data-ttu-id="39d73-126">Hallo-dashboardtabblad biedt bovendien een overzicht van het gebruik van uw werkruimte en een snelle weergave van uw werkruimtegegevens.</span><span class="sxs-lookup"><span data-stu-id="39d73-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="39d73-127">In Azure Machine Learning Studio, op Hallo **WEBSERVICES** tabblad, u kunt toevoegen, bijwerken of verwijderen van een Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="39d73-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="39d73-128">een werkruimte in de klassieke Azure-portal Hallo toomanage:</span><span class="sxs-lookup"><span data-stu-id="39d73-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="39d73-129">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) met uw Microsoft Azure-account - Hallo account gebruiken dat is gekoppeld aan hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="39d73-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="39d73-130">In het Configuratiescherm Hallo Microsoft Azure-services, klikt u op **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="39d73-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="39d73-131">Klik op de gewenste toomanage Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="39d73-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="39d73-132">Hallo-pagina voor werkruimte heeft drie tabbladen:</span><span class="sxs-lookup"><span data-stu-id="39d73-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="39d73-133">**DASHBOARD** -kunt u tooview werkruimte gebruiks- en informatie</span><span class="sxs-lookup"><span data-stu-id="39d73-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="39d73-134">**CONFIGUREER** -kunt u toomanage access toohello-werkruimte</span><span class="sxs-lookup"><span data-stu-id="39d73-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="39d73-135">**WEBSERVICES** -kunt u toomanage webservices die zijn gepubliceerd vanuit deze werkruimte</span><span class="sxs-lookup"><span data-stu-id="39d73-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="39d73-136">toomonitor hoe Hallo werkruimte wordt gebruikt</span><span class="sxs-lookup"><span data-stu-id="39d73-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="39d73-137">Klik op Hallo **DASHBOARD** tabblad.</span><span class="sxs-lookup"><span data-stu-id="39d73-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="39d73-138">U kunt vanuit Hallo-dashboard algemene informatie over het gebruik van uw werkruimte weergeven en ophalen van een snelle weergave van informatie van de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="39d73-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="39d73-139">Hallo **COMPUTE** diagram toont de rekenresources hello wordt gebruikt door het Hallo-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="39d73-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="39d73-140">U kunt Hallo weergave toodisplay relatieve of absolute waarden wijzigen en u Hallo tijdsbestek weergegeven in de grafiek Hallo kan wijzigen.</span><span class="sxs-lookup"><span data-stu-id="39d73-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="39d73-141">**Overzicht gebruik** Azure-opslag wordt gebruikt door Hallo werkruimte wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="39d73-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="39d73-142">**Snelle weergave** bevat een samenvatting van de werkruimte informatie en nuttige koppelingen.</span><span class="sxs-lookup"><span data-stu-id="39d73-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="39d73-143">Hallo **aanmelden tooML Studio** koppeling Hallo u momenteel bent aangemeld bij Microsoft-Account met behulp van Machine Learning Studio wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="39d73-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="39d73-144">Hallo u toosign in toohello Azure classic portal toocreate een werkruimte gebruikt Microsoft-Account heeft automatisch geen machtiging tooopen die werkruimte.</span><span class="sxs-lookup"><span data-stu-id="39d73-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="39d73-145">tooopen een werkruimte, moet u zijn aangemeld toohello Microsoft-Account dat is gedefinieerd als eigenaar van de werkruimte Hallo Hallo of moet u een uitnodiging uit Hallo eigenaar toojoin Hallo werkruimte tooreceive.</span><span class="sxs-lookup"><span data-stu-id="39d73-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="39d73-146">toogrant of onderbreken van toegang voor gebruikers</span><span class="sxs-lookup"><span data-stu-id="39d73-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="39d73-147">Klik op Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="39d73-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="39d73-148">U kunt van tabblad Hallo-configuratie:</span><span class="sxs-lookup"><span data-stu-id="39d73-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="39d73-149">Toegang toohello Machine Learning-werkruimte onderbreken door te klikken op weigeren.</span><span class="sxs-lookup"><span data-stu-id="39d73-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="39d73-150">Gebruikers kunnen niet meer kunnen tooopen Hallo werkruimte in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="39d73-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="39d73-151">toorestore openen, klikt u op toestaan.</span><span class="sxs-lookup"><span data-stu-id="39d73-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="39d73-152">toomanage extra accounts die hebben toegang tot toohello werkruimte in Machine Learning Studio, klikt u op **aanmelden tooML Studio** in Hallo **DASHBOARD** tabblad (Zie Hallo voorgaande opmerking met betrekking tot  **Sign-in tooML Studio**).</span><span class="sxs-lookup"><span data-stu-id="39d73-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="39d73-153">Hiermee opent u de werkruimte Hallo in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="39d73-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="39d73-154">Klik op Hallo van hieruit **instellingen** tabblad en vervolgens **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="39d73-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="39d73-155">U kunt klikken op **meer gebruikers UITNODIGEN** toogive gebruikers toegang tot toohello werkruimte, of Selecteer een gebruiker en klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="39d73-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="39d73-156">webservices toomanage in deze werkruimte</span><span class="sxs-lookup"><span data-stu-id="39d73-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="39d73-157">Klik op Hallo **WEBSERVICES** tabblad.</span><span class="sxs-lookup"><span data-stu-id="39d73-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="39d73-158">Dit geeft een lijst van webservices die worden gepubliceerd vanuit deze werkruimte.</span><span class="sxs-lookup"><span data-stu-id="39d73-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="39d73-159">toomanage een webservice, klikt u op Hallo-naam in Hallo lijst tooopen Hallo pagina van de webservice.</span><span class="sxs-lookup"><span data-stu-id="39d73-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="39d73-160">Een webservice heeft misschien een of meer eindpunten zijn gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="39d73-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="39d73-161">U kunt meer eindpunten in toevoeging toohello 'Default' eindpunt definiëren.</span><span class="sxs-lookup"><span data-stu-id="39d73-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="39d73-162">tooadd Hallo eindpunt, klikt u op **eindpunten beheren** onderaan Hallo Hallo dashboard tooopen hello Azure Machine Learning-webservices-portal.</span><span class="sxs-lookup"><span data-stu-id="39d73-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="39d73-163">toodelete eindpunt (u kunt Hallo 'Default' eindpunt niet verwijderen), klik op het selectievakje Hallo aan Hallo begin van Hallo eindpunt rij en klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="39d73-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="39d73-164">Hiermee verwijdert u Hallo endpoint van Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="39d73-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="39d73-165">Als een toepassing hello webservice-eindpunt wanneer Hallo-eindpunt wordt verwijderd, ontvangt de toepassing hello een Hallo fout volgende keer dat deze tooaccess Hallo-service probeert.</span><span class="sxs-lookup"><span data-stu-id="39d73-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="39d73-166">Klik op de naam van een Web service-eindpunt tooopen Hallo deze.</span><span class="sxs-lookup"><span data-stu-id="39d73-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="39d73-167">U kunt algemene informatie over het gebruik van uw Web-service gedurende een periode weergeven vanuit Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="39d73-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="39d73-168">U kunt Hallo periode tooview selecteren in Hallo periode vervolgkeuzemenu in de rechterbovenhoek Hallo Hallo gebruik grafieken.</span><span class="sxs-lookup"><span data-stu-id="39d73-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="39d73-169">Hallo-dashboard ziet Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="39d73-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="39d73-170">**Aanvragen gedurende een periode** bevat een stap grafiek van Hallo aantal aanvragen gedurende Hallo geselecteerde periode.</span><span class="sxs-lookup"><span data-stu-id="39d73-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="39d73-171">Kunt u identificeren als er pieken in gebruik.</span><span class="sxs-lookup"><span data-stu-id="39d73-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="39d73-172">**Reactie op aanvragen aanvragen** Hallo kunt u het totale aantal aanvragen en antwoorden aanroepen Hallo-service heeft ontvangen via Hallo geselecteerde tijdsperiode en het aantal kunnen niet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="39d73-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="39d73-173">**Gemiddelde tijd voor aanvragen en antwoorden Compute** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="39d73-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="39d73-174">**Batch-aanvragen** Hallo totaal aantal weergeven batchaanvragen Hallo service via Hallo geselecteerde periode heeft ontvangen en hoeveel is mislukt.</span><span class="sxs-lookup"><span data-stu-id="39d73-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="39d73-175">**Gemiddelde latentie van de taak** wordt een gemiddelde van tijd Hallo nodig tooexecute Hallo ontvangen aanvragen.</span><span class="sxs-lookup"><span data-stu-id="39d73-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="39d73-176">**Fouten** wordt Hallo cumulatieve aantal fouten die zijn opgetreden in aanroepen toohello-webservice.</span><span class="sxs-lookup"><span data-stu-id="39d73-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="39d73-177">**Services-kosten** Hallo kosten voor Hallo-abonnement is gekoppeld aan het Hallo-service wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="39d73-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="39d73-178">Vanaf de configuratiepagina hello, kunt u de volgende eigenschappen Hallo bijwerken:</span><span class="sxs-lookup"><span data-stu-id="39d73-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="39d73-179">**Beschrijving** kunt u een beschrijving op voor Hallo webservice tooenter.</span><span class="sxs-lookup"><span data-stu-id="39d73-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="39d73-180">De beschrijving is een verplicht veld.</span><span class="sxs-lookup"><span data-stu-id="39d73-180">Description is a required field.</span></span>
* <span data-ttu-id="39d73-181">**Logboekregistratie** kunt u tooenable of schakelt u fout bij het aanmelden Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="39d73-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="39d73-182">Zie voor meer informatie over logboekregistratie inschakelen [logboekregistratie voor Machine Learning-webservices](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="39d73-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="39d73-183">**Inschakelen van voorbeeldgegevens** kunt u voorbeeldgegevens tooprovide waarmee u tootest Hallo aanvraag en antwoord-service kunt.</span><span class="sxs-lookup"><span data-stu-id="39d73-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="39d73-184">Als u de webservice Hallo in Machine Learning Studio gemaakt, Hallo voorbeeldgegevens is genomen van Hallo gegevens uw gebruikte tootrain uw model.</span><span class="sxs-lookup"><span data-stu-id="39d73-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="39d73-185">Als u Hallo-service via een programma hebt gemaakt, worden Hallo gegevens worden opgehaald van Hallo bijvoorbeeld gegevens die u hebt opgegeven als onderdeel van Hallo JSON-pakket.</span><span class="sxs-lookup"><span data-stu-id="39d73-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

