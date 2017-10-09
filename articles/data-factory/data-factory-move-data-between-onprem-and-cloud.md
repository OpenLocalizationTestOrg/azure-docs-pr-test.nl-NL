---
title: gegevens aaaMove - Data Management Gateway | Microsoft Docs
description: Instellen van een data gateway toomove gegevens tussen on-premises en Hallo cloud. Gebruik van Data Management Gateway in Azure Data Factory toomove uw gegevens.
keywords: gegevensgateway, gegevensintegratie, gegevens, gatewayreferenties verplaatsen
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 7bf6d8fd-04b5-499d-bd19-eff217aa4a9c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 314341c142d5260c785b7e82081774f044450e81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-between-on-premises-sources-and-hello-cloud-with-data-management-gateway"></a><span data-ttu-id="675a6-105">Gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="675a6-105">Move data between on-premises sources and hello cloud with Data Management Gateway</span></span>
<span data-ttu-id="675a6-106">Dit artikel bevat een overzicht van de gegevensintegratie tussen on-premises gegevensopslagexemplaren en cloud gegevensarchieven gebruik Data Factory.</span><span class="sxs-lookup"><span data-stu-id="675a6-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="675a6-107">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel en andere data factory core concepten artikelen: [gegevenssets](data-factory-create-datasets.md) en [pijplijnen](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="675a6-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="675a6-108">Gegevensbeheergateway</span><span class="sxs-lookup"><span data-stu-id="675a6-108">Data Management Gateway</span></span>
<span data-ttu-id="675a6-109">U moet de Data Management Gateway installeren op uw lokale machine tooenable verplaatsen van gegevens vanuit een on-premises gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="675a6-109">You must install Data Management Gateway on your on-premises machine tooenable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="675a6-110">Hallo-gateway kan worden geïnstalleerd op dezelfde computer als gegevensarchief Hallo of op een andere computer, zolang het Hallo-gateway verbinding kan maken van gegevensarchief toohello Hallo.</span><span class="sxs-lookup"><span data-stu-id="675a6-110">hello gateway can be installed on hello same machine as hello data store or on a different machine as long as hello gateway can connect toohello data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="675a6-111">Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="675a6-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="675a6-112">Hallo volgende overzicht toont u hoe een gegevensfactory met een pipeline die de gegevens vanuit een on-premises verplaatst toocreate **SQL Server** tooan Azure blob-opslag van de database.</span><span class="sxs-lookup"><span data-stu-id="675a6-112">hello following walkthrough shows you how toocreate a data factory with a pipeline that moves data from an on-premises **SQL Server** database tooan Azure blob storage.</span></span> <span data-ttu-id="675a6-113">Als onderdeel van het Hallo-scenario, installeren en configureren Hallo Data Management Gateway op uw computer.</span><span class="sxs-lookup"><span data-stu-id="675a6-113">As part of hello walkthrough, you install and configure hello Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-toocloud"></a><span data-ttu-id="675a6-114">Overzicht: lokale gegevens toocloud kopiëren</span><span class="sxs-lookup"><span data-stu-id="675a6-114">Walkthrough: copy on-premises data toocloud</span></span>
<span data-ttu-id="675a6-115">In dit scenario u Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="675a6-115">In this walkthrough you do hello following steps:</span></span> 

1. <span data-ttu-id="675a6-116">Een gegevensfactory maakt.</span><span class="sxs-lookup"><span data-stu-id="675a6-116">Create a data factory.</span></span>
2. <span data-ttu-id="675a6-117">Maak een data management gateway.</span><span class="sxs-lookup"><span data-stu-id="675a6-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="675a6-118">Gekoppelde services voor de bron- en sink gegevensarchieven maken.</span><span class="sxs-lookup"><span data-stu-id="675a6-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="675a6-119">Maken van gegevenssets toorepresent invoer- en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="675a6-119">Create datasets toorepresent input and output data.</span></span>
5. <span data-ttu-id="675a6-120">Een pijplijn maken met een kopie toomove Hallo activiteitsgegevens.</span><span class="sxs-lookup"><span data-stu-id="675a6-120">Create a pipeline with a copy activity toomove hello data.</span></span>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="675a6-121">Vereisten voor het Hallo-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="675a6-121">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="675a6-122">Voordat u deze procedure begint, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="675a6-122">Before you begin this walkthrough, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="675a6-123">**Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="675a6-123">**Azure subscription**.</span></span>  <span data-ttu-id="675a6-124">Als u geen abonnement hebt, kunt u binnen een paar minuten een gratis proefaccount maken.</span><span class="sxs-lookup"><span data-stu-id="675a6-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="675a6-125">Zie Hallo [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="675a6-125">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="675a6-126">**Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="675a6-126">**Azure Storage Account**.</span></span> <span data-ttu-id="675a6-127">Gebruik van Hallo blob storage als een **bestemming/sink** gegevens opslaan in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="675a6-127">You use hello blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="675a6-128">Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel voor stappen toocreate een.</span><span class="sxs-lookup"><span data-stu-id="675a6-128">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="675a6-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="675a6-129">**SQL Server**.</span></span> <span data-ttu-id="675a6-130">In deze zelfstudie gebruikt u een on-premises SQL Server-database als een **brongegevensopslag**.</span><span class="sxs-lookup"><span data-stu-id="675a6-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="675a6-131">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="675a6-131">Create data factory</span></span>
<span data-ttu-id="675a6-132">In deze stap gebruikt u hello Azure portal toocreate een Azure Data Factory-exemplaar met de naam **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="675a6-132">In this step, you use hello Azure portal toocreate an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="675a6-133">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="675a6-133">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="675a6-134">Klik op **+ nieuw**, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="675a6-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nieuw -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="675a6-136">In Hallo **nieuwe gegevensfactory** pagina **ADFTutorialOnPremDF** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="675a6-136">In hello **New data factory** page, enter **ADFTutorialOnPremDF** for hello Name.</span></span>

    ![TooStartboard toevoegen](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="675a6-138">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="675a6-138">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="675a6-139">Als u de foutmelding Hallo: **Data factory-naam 'ADFTutorialOnPremDF' is niet beschikbaar**, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameADFTutorialOnPremDF) en probeert u het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="675a6-139">If you receive hello error: **Data factory name “ADFTutorialOnPremDF” is not available**, change hello name of hello data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="675a6-140">Gebruik deze naam in plaats van ADFTutorialOnPremDF tijdens het uitvoeren van de resterende stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="675a6-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="675a6-141">Hallo-naam van de gegevensfactory Hallo mogelijk geregistreerd als een **DNS** naam in de toekomst Hallo en daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="675a6-141">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="675a6-142">Selecteer Hallo **Azure-abonnement** waar u Hallo data factory toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="675a6-142">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="675a6-143">Selecteer een bestaande **resourcegroep** of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="675a6-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="675a6-144">Maak een resourcegroep met de naam voor Hallo-zelfstudie: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="675a6-144">For hello tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="675a6-145">Klik op **maken** op Hallo **nieuwe gegevensfactory** pagina.</span><span class="sxs-lookup"><span data-stu-id="675a6-145">Click **Create** on hello **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="675a6-146">toocreate Data Factory-exemplaren, moet u lid zijn van Hallo [Data Factory Inzender](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rol op het niveau van de Hallo abonnement/resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="675a6-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="675a6-147">Nadat het maken voltooid is, ziet u Hallo **Data Factory** pagina zoals in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="675a6-147">After creation is complete, you see hello **Data Factory** page as shown in hello following image:</span></span>

   ![Data Factory-startpagina](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="675a6-149">Gateway maken</span><span class="sxs-lookup"><span data-stu-id="675a6-149">Create gateway</span></span>
1. <span data-ttu-id="675a6-150">In Hallo **Data Factory** pagina, klikt u op **auteur en implementeren van** tegel toolaunch hello **Editor** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="675a6-150">In hello **Data Factory** page, click **Author and deploy** tile toolaunch hello **Editor** for hello data factory.</span></span>

    ![Tegel Ontwerpen en implementeren](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="675a6-152">In Hallo Data Factory-Editor, klikt u op **... Meer** op Hallo van de werkbalk en klik vervolgens op **nieuwe gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="675a6-152">In hello Data Factory Editor, click **... More** on hello toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="675a6-153">U kunt ook u kunt met de rechtermuisknop op **gegevensgateways** in Hallo structuurweergave en klik op **nieuwe gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="675a6-153">Alternatively, you can right-click **Data Gateways** in hello tree view, and click **New data gateway**.</span></span>

   ![Nieuwe gegevensgateway op werkbalk](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="675a6-155">In Hallo **maken** pagina **adftutorialgateway** voor Hallo **naam**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="675a6-155">In hello **Create** page, enter **adftutorialgateway** for hello **name**, and click **OK**.</span></span>     

    ![Pagina Gateway maken](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="675a6-157">In dit scenario maakt u Hallo logische gateway met slechts één knooppunt (lokale Windows-machine).</span><span class="sxs-lookup"><span data-stu-id="675a6-157">In this walkthrough, you create hello logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="675a6-158">U kunt een data management gateway uitbreiden door meerdere lokale computers koppelen aan Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="675a6-158">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="675a6-159">U kunt schalen omhoog door het aantal data movement taken die kunnen tegelijkertijd worden uitgevoerd op een knooppunt te verhogen.</span><span class="sxs-lookup"><span data-stu-id="675a6-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="675a6-160">Deze functie is ook beschikbaar voor een logische gateway met één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="675a6-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="675a6-161">Zie [schaal data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="675a6-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="675a6-162">In Hallo **configureren** pagina, klikt u op **rechtstreeks op deze computer installeren**.</span><span class="sxs-lookup"><span data-stu-id="675a6-162">In hello **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="675a6-163">Deze actie Hallo-installatiepakket voor de gateway Hallo downloadt, installeert, configureert en registreert Hallo-gateway op Hallo-computer.</span><span class="sxs-lookup"><span data-stu-id="675a6-163">This action downloads hello installation package for hello gateway, installs, configures, and registers hello gateway on hello computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="675a6-164">Internet Explorer of een webbrowser die Microsoft ClickOnce compatibel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="675a6-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="675a6-165">Als u Chrome gebruikt, gaat u toohello [Chrome web store](https://chrome.google.com/webstore/), zoeken met het sleutelwoord 'ClickOnce', kies een van de ClickOnce-extensies Hallo en deze installeren.</span><span class="sxs-lookup"><span data-stu-id="675a6-165">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="675a6-166">Hallo dezelfde voor Firefox (install-invoegtoepassing).</span><span class="sxs-lookup"><span data-stu-id="675a6-166">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="675a6-167">Klik op **Menu openen** op de werkbalk hello (**drie horizontale lijnen** in de rechterbovenhoek Hallo), klikt u op **invoegtoepassingen**, zoeken met het sleutelwoord 'ClickOnce', kies een van de Hallo ClickOnce-extensies en te installeren.</span><span class="sxs-lookup"><span data-stu-id="675a6-167">Click **Open Menu** button on hello toolbar (**three horizontal lines** in hello top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Gateway - pagina configureren](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="675a6-169">Op deze manier is de eenvoudigste manier (met één muisklik) toodownload hello, installeren, configureren en Hallo gateway registreren in één enkele stap.</span><span class="sxs-lookup"><span data-stu-id="675a6-169">This way is hello easiest way (one-click) toodownload, install, configure, and register hello gateway in one single step.</span></span> <span data-ttu-id="675a6-170">U kunt zien Hallo **Microsoft Data Management Gateway Configuration Manager** toepassing op uw computer is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="675a6-170">You can see hello **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="675a6-171">U kunt ook vinden Hallo uitvoerbare **ConfigManager.exe** in de map Hallo: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="675a6-171">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="675a6-172">U kunt ook downloaden en gateway handmatig installeren met behulp van Hallo koppelingen op deze pagina en registreren met behulp van Hallo-sleutel die wordt weergegeven in Hallo **nieuwe sleutel** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="675a6-172">You can also download and install gateway manually by using hello links in this page and register it using hello key shown in hello **NEW KEY** text box.</span></span>

    <span data-ttu-id="675a6-173">Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor alle informatie over gateway-Hallo Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="675a6-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="675a6-174">U moet een beheerder op Hallo lokale computer tooinstall en Hallo Data Management Gateway is configureren.</span><span class="sxs-lookup"><span data-stu-id="675a6-174">You must be an administrator on hello local computer tooinstall and configure hello Data Management Gateway successfully.</span></span> <span data-ttu-id="675a6-175">U kunt extra gebruikers toohello toevoegen **Data Management Gateway-gebruikers** lokale Windows-groep.</span><span class="sxs-lookup"><span data-stu-id="675a6-175">You can add additional users toohello **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="675a6-176">Hallo-leden van deze groep kunnen Hallo Data Management Gateway Configuration Manager hulpprogramma tooconfigure Hallo gateway gebruiken.</span><span class="sxs-lookup"><span data-stu-id="675a6-176">hello members of this group can use hello Data Management Gateway Configuration Manager tool tooconfigure hello gateway.</span></span>
   >
   >
5. <span data-ttu-id="675a6-177">Wacht een paar minuten of wacht tot u Hallo Meldingsbericht te volgen:</span><span class="sxs-lookup"><span data-stu-id="675a6-177">Wait for a couple of minutes or wait until you see hello following notification message:</span></span>

    ![Gateway-installatie is geslaagd](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="675a6-179">Start **Data Management Gateway Configuration Manager** toepassing op uw computer.</span><span class="sxs-lookup"><span data-stu-id="675a6-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="675a6-180">In Hallo **Search** venster, type **Data Management Gateway** tooaccess dit hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="675a6-180">In hello **Search** window, type **Data Management Gateway** tooaccess this utility.</span></span> <span data-ttu-id="675a6-181">U kunt ook vinden Hallo uitvoerbare **ConfigManager.exe** in de map Hallo: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="675a6-181">You can also find hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gateway-Configuratiebeheer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="675a6-183">Controleer of u `adftutorialgateway is connected toohello cloud service` bericht.</span><span class="sxs-lookup"><span data-stu-id="675a6-183">Confirm that you see `adftutorialgateway is connected toohello cloud service` message.</span></span> <span data-ttu-id="675a6-184">Hallo statusbalk Hallo onder geeft **verbonden toohello cloudservice** samen met een **groen vinkje**.</span><span class="sxs-lookup"><span data-stu-id="675a6-184">hello status bar hello bottom displays **Connected toohello cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="675a6-185">Op Hallo **Start** tabblad kunt u ook doen Hallo volgende bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="675a6-185">On hello **Home** tab, you can also do hello following operations:</span></span>

   * <span data-ttu-id="675a6-186">**Registreren** een gateway met een sleutel van hello Azure-portal met behulp van Hallo registreren knop.</span><span class="sxs-lookup"><span data-stu-id="675a6-186">**Register** a gateway with a key from hello Azure portal by using hello Register button.</span></span>
   * <span data-ttu-id="675a6-187">**Stop** Hallo Data Management Gateway Host Service uitgevoerd op uw computer met de gateway.</span><span class="sxs-lookup"><span data-stu-id="675a6-187">**Stop** hello Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="675a6-188">**Updates plannen** toobe geïnstalleerd op een bepaald tijdstip van Hallo dag.</span><span class="sxs-lookup"><span data-stu-id="675a6-188">**Schedule updates** toobe installed at a specific time of hello day.</span></span>
   * <span data-ttu-id="675a6-189">Weergeven wanneer Hallo gateway **laatst bijgewerkt**.</span><span class="sxs-lookup"><span data-stu-id="675a6-189">View when hello gateway was **last updated**.</span></span>
   * <span data-ttu-id="675a6-190">Geef de tijd waarop de gateway van een update toohello kan worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="675a6-190">Specify time at which an update toohello gateway can be installed.</span></span>
8. <span data-ttu-id="675a6-191">Overschakelen toohello **instellingen** tabblad Hallo certificaat is opgegeven in Hallo **certificaat** sectie is gebruikte tooencrypt/ontsleutelen referenties voor Hallo on-premises gegevensopslag die u op Hallo-portal opgeeft.</span><span class="sxs-lookup"><span data-stu-id="675a6-191">Switch toohello **Settings** tab. hello certificate specified in hello **Certificate** section is used tooencrypt/decrypt credentials for hello on-premises data store that you specify on hello portal.</span></span> <span data-ttu-id="675a6-192">(optioneel) Klik op **wijziging** toouse uw eigen certificaat in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="675a6-192">(optional) Click **Change** toouse your own certificate instead.</span></span> <span data-ttu-id="675a6-193">Hallo-gateway gebruikt standaard Hallo-certificaat dat automatisch wordt gegenereerd door Hallo Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="675a6-193">By default, hello gateway uses hello certificate that is auto-generated by hello Data Factory service.</span></span>

    ![De configuratie van de gateway-certificaat](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="675a6-195">U kunt ook doen Hallo volgende acties op Hallo **instellingen** tabblad:</span><span class="sxs-lookup"><span data-stu-id="675a6-195">You can also do hello following actions on hello **Settings** tab:</span></span>

   * <span data-ttu-id="675a6-196">Weergeven of Hallo certificaat dat wordt gebruikt door de gateway Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="675a6-196">View or export hello certificate being used by hello gateway.</span></span>
   * <span data-ttu-id="675a6-197">Hallo HTTPS-eindpunt is gebruikt door de gateway Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="675a6-197">Change hello HTTPS endpoint used by hello gateway.</span></span>    
   * <span data-ttu-id="675a6-198">Stel een HTTP-proxy toobe gebruikt door Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="675a6-198">Set an HTTP proxy toobe used by hello gateway.</span></span>     
9. <span data-ttu-id="675a6-199">(optioneel) Overschakelen toohello **Diagnostics** tabblad, controleert u Hallo **uitgebreide logboekregistratie inschakelen** optie als u tooenable uitgebreide logboekregistratie die u tootroubleshoot eventuele problemen met Hallo-gateway gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="675a6-199">(optional) Switch toohello **Diagnostics** tab, check hello **Enable verbose logging** option if you want tooenable verbose logging that you can use tootroubleshoot any issues with hello gateway.</span></span> <span data-ttu-id="675a6-200">Hallo logboekinformatie vindt u in **logboeken** onder **logboeken toepassingen en Services** -> **Data Management Gateway** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="675a6-200">hello logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Tabblad Diagnostische gegevens](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="675a6-202">U kunt ook uitvoeren met de volgende activiteiten in Hallo Hallo **Diagnostics** tabblad:</span><span class="sxs-lookup"><span data-stu-id="675a6-202">You can also perform hello following actions in hello **Diagnostics** tab:</span></span>

   * <span data-ttu-id="675a6-203">Gebruik **testverbinding** sectie tooan lokale gegevensbron met behulp van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="675a6-203">Use **Test Connection** section tooan on-premises data source using hello gateway.</span></span>
   * <span data-ttu-id="675a6-204">Klik op **logboeken bekijken** toosee Hallo Data Management Gateway zich in een Event Viewer-venster.</span><span class="sxs-lookup"><span data-stu-id="675a6-204">Click **View Logs** toosee hello Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="675a6-205">Klik op **logboeken verzenden** tooupload een zip-bestand met de logboeken van de afgelopen zeven dagen tooMicrosoft toofacilitate oplossen van problemen met uw.</span><span class="sxs-lookup"><span data-stu-id="675a6-205">Click **Send Logs** tooupload a zip file with logs of last seven days tooMicrosoft toofacilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="675a6-206">Op Hallo **Diagnostics** tabblad in Hallo **testverbinding** sectie **SqlServer** voor Hallo Hallo gegevenstype opslaan, voer de naam Hallo van Hallo-databaseserver, de naam van Hallo-database, verificatietype opgeven, gebruikersnaam en wachtwoord invoeren en klikt u op **Test** tootest of Hallo gateway verbinding toohello database kunt maken.</span><span class="sxs-lookup"><span data-stu-id="675a6-206">On hello **Diagnostics** tab, in hello **Test Connection** section, select **SqlServer** for hello type of hello data store, enter hello name of hello database server, name of hello database, specify authentication type, enter user name, and password, and click **Test** tootest whether hello gateway can connect toohello database.</span></span>
11. <span data-ttu-id="675a6-207">Switch toohello webbrowser, en in Hallo **Azure-portal**, klikt u op **OK** op Hallo **configureren** pagina en klik vervolgens op Hallo **nieuwe gegevensgateway** pagina.</span><span class="sxs-lookup"><span data-stu-id="675a6-207">Switch toohello web browser, and in hello **Azure portal**, click **OK** on hello **Configure** page and then on hello **New data gateway** page.</span></span>
12. <span data-ttu-id="675a6-208">U ziet **adftutorialgateway** onder **gegevensgateways** in Hallo structuurweergave Hallo links.</span><span class="sxs-lookup"><span data-stu-id="675a6-208">You should see **adftutorialgateway** under **Data Gateways** in hello tree view on hello left.</span></span>  <span data-ttu-id="675a6-209">Als u erop klikt, ziet u Hallo JSON die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="675a6-209">If you click it, you should see hello associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="675a6-210">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="675a6-210">Create linked services</span></span>
<span data-ttu-id="675a6-211">In deze stap maakt u twee gekoppelde services: **AzureStorageLinkedService** en **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="675a6-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="675a6-212">Hallo **SqlServerLinkedService** koppelt u een lokale SQL Server-database en het Hallo **AzureStorageLinkedService** een Azure blob-archief toohello data factory gekoppelde service is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="675a6-212">hello **SqlServerLinkedService** links an on-premises SQL Server database and hello **AzureStorageLinkedService** linked service links an Azure blob store toohello data factory.</span></span> <span data-ttu-id="675a6-213">U maakt een pijplijn verderop in dit scenario waarmee gegevens worden gekopieerd van Hallo lokale SQL Server-database toohello Azure blob-archief.</span><span class="sxs-lookup"><span data-stu-id="675a6-213">You create a pipeline later in this walkthrough that copies data from hello on-premises SQL Server database toohello Azure blob store.</span></span>

#### <a name="add-a-linked-service-tooan-on-premises-sql-server-database"></a><span data-ttu-id="675a6-214">Toevoegen van een gekoppelde service tooan lokale SQL Server-database</span><span class="sxs-lookup"><span data-stu-id="675a6-214">Add a linked service tooan on-premises SQL Server database</span></span>
1. <span data-ttu-id="675a6-215">In Hallo **Data Factory-Editor**, klikt u op **nieuwe gegevensopslag** op Hallo werkbalk en selecteer **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="675a6-215">In hello **Data Factory Editor**, click **New data store** on hello toolbar and select **SQL Server**.</span></span>

   ![Nieuwe SQL-Server gekoppeld-service](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="675a6-217">In Hallo **JSON-editor** op Hallo rechts, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="675a6-217">In hello **JSON editor** on hello right, do hello following steps:</span></span>

   1. <span data-ttu-id="675a6-218">Voor Hallo **gatewayName**, geef **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="675a6-218">For hello **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="675a6-219">In Hallo **connectionString**, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="675a6-219">In hello **connectionString**, do hello following steps:</span></span>    

      1. <span data-ttu-id="675a6-220">Voor **servername**, voer de naam Hallo van Hallo-server die als host fungeert voor de SQL Server-database Hallo.</span><span class="sxs-lookup"><span data-stu-id="675a6-220">For **servername**, enter hello name of hello server that hosts hello SQL Server database.</span></span>
      2. <span data-ttu-id="675a6-221">Voor **databasename**, typ Hallo van Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="675a6-221">For **databasename**, enter hello name of hello database.</span></span>
      3. <span data-ttu-id="675a6-222">Klik op **versleutelen** op de werkbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="675a6-222">Click **Encrypt** button on hello toolbar.</span></span> <span data-ttu-id="675a6-223">U ziet Hallo Referentiebeheer toepassing.</span><span class="sxs-lookup"><span data-stu-id="675a6-223">You see hello Credentials Manager application.</span></span>

         ![Referenties Manager-toepassing](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="675a6-225">In Hallo **instelling referenties** in het dialoogvenster verificatietype, gebruikersnaam en wachtwoord opgeven en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="675a6-225">In hello **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="675a6-226">Hallo verbinding geslaagd is, Hallo versleutelde referenties zijn opgeslagen in Hallo JSON als Hallo dialoogvenster wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="675a6-226">If hello connection is successful, hello encrypted credentials are stored in hello JSON and hello dialog box closes.</span></span>
      5. <span data-ttu-id="675a6-227">Sluit Hallo leeg browsertabblad die in het dialoogvenster voor Hallo gestart als deze niet automatisch wordt gesloten en terughalen toohello tabblad Hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="675a6-227">Close hello empty browser tab that launched hello dialog box if it is not automatically closed and get back toohello tab with hello Azure portal.</span></span>

         <span data-ttu-id="675a6-228">Op de gatewaycomputer hello, deze referenties zijn **versleutelde** met behulp van een certificaat dat de Data Factory Hallo service bezit.</span><span class="sxs-lookup"><span data-stu-id="675a6-228">On hello gateway machine, these credentials are **encrypted** by using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="675a6-229">Als u toouse Hallo certificaat dat is gekoppeld aan Hallo Data Management Gateway in plaats daarvan wilt, Zie [referenties veilig instellen](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="675a6-229">If you want toouse hello certificate that is associated with hello Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="675a6-230">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gekoppelde SQL-Server-service.</span><span class="sxs-lookup"><span data-stu-id="675a6-230">Click **Deploy** on hello command bar toodeploy hello SQL Server linked service.</span></span> <span data-ttu-id="675a6-231">U ziet de service in de structuurweergave Hallo Hallo gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="675a6-231">You should see hello linked service in hello tree view.</span></span>

      ![SQL Server gekoppeld-service in de structuurweergave Hallo](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="675a6-233">Een gekoppelde service voor een Azure storage-account toevoegen</span><span class="sxs-lookup"><span data-stu-id="675a6-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="675a6-234">In Hallo **Data Factory-Editor**, klikt u op **nieuwe gegevensopslag** op Hallo opdrachtbalk en klik op **Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="675a6-234">In hello **Data Factory Editor**, click **New data store** on hello command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="675a6-235">Hallo-naam van uw Azure storage-account voor Hallo **accountnaam**.</span><span class="sxs-lookup"><span data-stu-id="675a6-235">Enter hello name of your Azure storage account for hello **Account name**.</span></span>
3. <span data-ttu-id="675a6-236">Voer Hallo-sleutel voor uw Azure storage-account voor Hallo **accountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="675a6-236">Enter hello key for your Azure storage account for hello **Account key**.</span></span>
4. <span data-ttu-id="675a6-237">Klik op **implementeren** toodeploy hello **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="675a6-237">Click **Deploy** toodeploy hello **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="675a6-238">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="675a6-238">Create datasets</span></span>
<span data-ttu-id="675a6-239">In deze stap maakt u invoer en uitvoergegevenssets maken die invoer- en gegevens voor de kopieerbewerking Hallo vertegenwoordigen (On-premises SQL Server-database = > Azure-blobopslag).</span><span class="sxs-lookup"><span data-stu-id="675a6-239">In this step, you create input and output datasets that represent input and output data for hello copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="675a6-240">Voordat u de gegevenssets, Hallo volgende stappen uit (gedetailleerde stappen volgt Hallo lijst):</span><span class="sxs-lookup"><span data-stu-id="675a6-240">Before creating datasets, do hello following steps (detailed steps follows hello list):</span></span>

* <span data-ttu-id="675a6-241">Maak een tabel met de naam **emp** in SQL Server-Database u toegevoegd als een gekoppelde service toohello data factory Hallo en enkele voorbeelden van vermeldingen in Hallo tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="675a6-241">Create a table named **emp** in hello SQL Server Database you added as a linked service toohello data factory and insert a couple of sample entries into hello table.</span></span>
* <span data-ttu-id="675a6-242">Maak een blobcontainer met de naam **adftutorial** in hello Azure blob storage-account die u hebt toegevoegd als een gekoppelde service toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="675a6-242">Create a blob container named **adftutorial** in hello Azure blob storage account you added as a linked service toohello data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-hello-tutorial"></a><span data-ttu-id="675a6-243">On-premises SQL Server voorbereiden voor Hallo-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="675a6-243">Prepare On-premises SQL Server for hello tutorial</span></span>
1. <span data-ttu-id="675a6-244">Gekoppelde service in Hallo-database die u hebt opgegeven voor Hallo on-premises SQL Server (**SqlServerLinkedService**), gebruiken de volgende SQL-script toocreate Hallo Hallo **emp** tabel in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="675a6-244">In hello database you specified for hello on-premises SQL Server linked service (**SqlServerLinkedService**), use hello following SQL script toocreate hello **emp** table in hello database.</span></span>

    ```SQL   
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
        CONSTRAINT PK_emp PRIMARY KEY (ID)
    )
    GO
    ```
2. <span data-ttu-id="675a6-245">Aantal voorbeelden in Hallo tabel invoegen:</span><span class="sxs-lookup"><span data-stu-id="675a6-245">Insert some sample into hello table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="675a6-246">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="675a6-246">Create input dataset</span></span>

1. <span data-ttu-id="675a6-247">In Hallo **Data Factory-Editor**, klikt u op **... Meer**, klikt u op **nieuwe gegevensset** op Hallo opdrachtbalk en klik op **SQL Server-tabel**.</span><span class="sxs-lookup"><span data-stu-id="675a6-247">In hello **Data Factory Editor**, click **... More**, click **New dataset** on hello command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="675a6-248">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="675a6-248">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {        
        "name": "EmpOnPremSQLTable",
        "properties": {
            "type": "SqlServerTable",
            "linkedServiceName": "SqlServerLinkedService",
            "typeProperties": {
                "tableName": "emp"
            },
            "external": true,
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "externalData": {
                    "retryInterval": "00:01:00",
                    "retryTimeout": "00:10:00",
                    "maximumRetry": 3
                }
            }
        }
    }     
    ```     
   <span data-ttu-id="675a6-249">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="675a6-249">Note hello following points:</span></span>

   * <span data-ttu-id="675a6-250">**type** te is ingesteld,**SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="675a6-250">**type** is set too**SqlServerTable**.</span></span>
   * <span data-ttu-id="675a6-251">**tableName** te is ingesteld,**emp**.</span><span class="sxs-lookup"><span data-stu-id="675a6-251">**tableName** is set too**emp**.</span></span>
   * <span data-ttu-id="675a6-252">**linkedServiceName** te is ingesteld,**SqlServerLinkedService** (u hebt deze gekoppelde service gemaakt eerder in dit scenario.).</span><span class="sxs-lookup"><span data-stu-id="675a6-252">**linkedServiceName** is set too**SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="675a6-253">Voor een invoergegevensset die niet worden gegenereerd door een andere pijplijn in Azure Data Factory, moet u instellen **externe** te**true**.</span><span class="sxs-lookup"><span data-stu-id="675a6-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** too**true**.</span></span> <span data-ttu-id="675a6-254">Hiermee wordt aangegeven Hallo invoergegevens geproduceerde externe toohello Azure Data Factory-service is.</span><span class="sxs-lookup"><span data-stu-id="675a6-254">It denotes hello input data is produced external toohello Azure Data Factory service.</span></span> <span data-ttu-id="675a6-255">U kunt optioneel beleid externe gegevens met behulp van Hallo opgeven **externalData** -element in Hallo **beleid** sectie.</span><span class="sxs-lookup"><span data-stu-id="675a6-255">You can optionally specify any external data policies using hello **externalData** element in hello **Policy** section.</span></span>    

   <span data-ttu-id="675a6-256">Zie [gegevens verplaatsen naar/van de SQL Server](data-factory-sqlserver-connector.md) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="675a6-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="675a6-257">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="675a6-257">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="675a6-258">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="675a6-258">Create output dataset</span></span>

1. <span data-ttu-id="675a6-259">In Hallo **Data Factory-Editor**, klikt u op **nieuwe gegevensset** op Hallo opdrachtbalk en klik op **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="675a6-259">In hello **Data Factory Editor**, click **New dataset** on hello command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="675a6-260">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="675a6-260">Replace hello JSON in hello right pane with hello following text:</span></span>

    ```JSON   
    {
        "name": "OutputBlobTable",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "adftutorial/outfromonpremdf",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
     }
    ```   
   <span data-ttu-id="675a6-261">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="675a6-261">Note hello following points:</span></span>

   * <span data-ttu-id="675a6-262">**type** te is ingesteld,**AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="675a6-262">**type** is set too**AzureBlob**.</span></span>
   * <span data-ttu-id="675a6-263">**linkedServiceName** te is ingesteld,**AzureStorageLinkedService** (u hebt deze gekoppelde service gemaakt in stap 2).</span><span class="sxs-lookup"><span data-stu-id="675a6-263">**linkedServiceName** is set too**AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="675a6-264">**folderPath** te is ingesteld,**adftutorial/outfromonpremdf** waarbij outfromonpremdf Hallo-map in Hallo adftutorial container is.</span><span class="sxs-lookup"><span data-stu-id="675a6-264">**folderPath** is set too**adftutorial/outfromonpremdf** where outfromonpremdf is hello folder in hello adftutorial container.</span></span> <span data-ttu-id="675a6-265">Hallo maken **adftutorial** container als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="675a6-265">Create hello **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="675a6-266">Hallo **beschikbaarheid** te is ingesteld,**per uur** (**frequentie** instellen te**uur** en **interval** te instellen **1**).</span><span class="sxs-lookup"><span data-stu-id="675a6-266">hello **availability** is set too**hourly** (**frequency** set too**hour** and **interval** set too**1**).</span></span>  <span data-ttu-id="675a6-267">Hallo Data Factory-service genereert een gegevenssegment uitvoer elk uur in Hallo **emp** tabel in hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="675a6-267">hello Data Factory service generates an output data slice every hour in hello **emp** table in hello Azure SQL Database.</span></span>

   <span data-ttu-id="675a6-268">Als u geen opgeeft een **fileName** voor een **uitvoertabel**, Hallo gegenereerd bestanden in Hallo **folderPath** naam op basis van indeling na Hallo: Data.<Guid>. txt (bijvoorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="675a6-268">If you do not specify a **fileName** for an **output table**, hello generated files in hello **folderPath** are named in hello following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="675a6-269">tooset **folderPath** en **fileName** dynamisch op basis van Hallo **SliceStart** tijd, gebruikt u de eigenschap partitionedBy Hallo.</span><span class="sxs-lookup"><span data-stu-id="675a6-269">tooset **folderPath** and **fileName** dynamically based on hello **SliceStart** time, use hello partitionedBy property.</span></span> <span data-ttu-id="675a6-270">In Hallo voorbeeld te volgen, folderPath gebruikt jaar, maand en dag van Hallo SliceStart (starttijd van Hallo-segment wordt verwerkt) en fileName wordt gebruikgemaakt van Hour van Hallo SliceStart.</span><span class="sxs-lookup"><span data-stu-id="675a6-270">In hello following example, folderPath uses Year, Month, and Day from hello SliceStart (start time of hello slice being processed) and fileName uses Hour from hello SliceStart.</span></span> <span data-ttu-id="675a6-271">Bijvoorbeeld, als een segment wordt geproduceerd voor 2014-10-20T08:00:00, Hallo folderName ingesteld toowikidatagateway/wikisampledataout/2014/10/20 en Hallo fileName too08.csv is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="675a6-271">For example, if a slice is being produced for 2014-10-20T08:00:00, hello folderName is set toowikidatagateway/wikisampledataout/2014/10/20 and hello fileName is set too08.csv.</span></span>

    ```JSON
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy":
    [

        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
    ],
    ```

    <span data-ttu-id="675a6-272">Zie [gegevens verplaatsen naar/van Azure Blob Storage](data-factory-azure-blob-connector.md) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="675a6-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="675a6-273">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="675a6-273">Click **Deploy** on hello command bar toodeploy hello dataset.</span></span> <span data-ttu-id="675a6-274">Controleer of u beide Hallo gegevenssets in de structuurweergave Hallo.</span><span class="sxs-lookup"><span data-stu-id="675a6-274">Confirm that you see both hello datasets in hello tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="675a6-275">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="675a6-275">Create pipeline</span></span>
<span data-ttu-id="675a6-276">In deze stap maakt u een **pijplijn** met een **Kopieeractiviteit** die gebruikmaakt van **EmpOnPremSQLTable** als invoer en **OutputBlobTable** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="675a6-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="675a6-277">Klik in Data Factory-Editor **... Meer** en vervolgens op **Nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="675a6-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="675a6-278">Hallo JSON in het rechterdeelvenster Hallo vervangen door Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="675a6-278">Replace hello JSON in hello right pane with hello following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL tooAzure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server tooblob",
             "type": "Copy",
             "inputs": [
               {
                 "name": "EmpOnPremSQLTable"
               }
             ],
             "outputs": [
               {
                 "name": "OutputBlobTable"
               }
             ],
             "typeProperties": {
               "source": {
                 "type": "SqlSource",
                 "sqlReaderQuery": "select * from emp"
               },
               "sink": {
                 "type": "BlobSink"
               }
             },
             "Policy": {
               "concurrency": 1,
               "executionPriorityOrder": "NewestFirst",
               "style": "StartOfInterval",
               "retry": 0,
               "timeout": "01:00:00"
             }
           }
         ],
         "start": "2016-07-05T00:00:00Z",
         "end": "2016-07-06T00:00:00Z",
         "isPaused": false
       }
     }
    ```   
   > [!IMPORTANT]
   > <span data-ttu-id="675a6-279">Vervang de waarde Hallo Hallo **start** eigenschap met de huidige dag Hallo en **end** waarde met de volgende dag Hallo.</span><span class="sxs-lookup"><span data-stu-id="675a6-279">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span>
   >
   >

   <span data-ttu-id="675a6-280">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="675a6-280">Note hello following points:</span></span>

   * <span data-ttu-id="675a6-281">In het gedeelte activiteiten Hallo is alleen activiteit waarvan **type** te is ingesteld,**kopie**.</span><span class="sxs-lookup"><span data-stu-id="675a6-281">In hello activities section, there is only activity whose **type** is set too**Copy**.</span></span>
   * <span data-ttu-id="675a6-282">**Invoer** voor Hallo activiteit te is ingesteld**EmpOnPremSQLTable** en **uitvoer** voor Hallo activiteit te is ingesteld**OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="675a6-282">**Input** for hello activity is set too**EmpOnPremSQLTable** and **output** for hello activity is set too**OutputBlobTable**.</span></span>
   * <span data-ttu-id="675a6-283">In Hallo **typeProperties** sectie **SqlSource** is opgegeven als Hallo **gegevensbrontype** en ** BlobSink ** is opgegeven als Hallo **sink-type**.</span><span class="sxs-lookup"><span data-stu-id="675a6-283">In hello **typeProperties** section, **SqlSource** is specified as hello **source type** and **BlobSink **is specified as hello **sink type**.</span></span>
   * <span data-ttu-id="675a6-284">SQL-query `select * from emp` is opgegeven voor Hallo **sqlReaderQuery** eigenschap van **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="675a6-284">SQL query `select * from emp` is specified for hello **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="675a6-285">Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben.</span><span class="sxs-lookup"><span data-stu-id="675a6-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="675a6-286">Bijvoorbeeld: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="675a6-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="675a6-287">Hallo **end** tijd is optioneel, maar er worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="675a6-287">hello **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="675a6-288">Als u geen waarde voor Hallo opgeeft **end** eigenschap, wordt berekend als '**start + 48 uur**'.</span><span class="sxs-lookup"><span data-stu-id="675a6-288">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="675a6-289">toorun hello pijplijn voor onbepaalde tijd, geef **9/9/9999** als waarde voor Hallo Hallo **end** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="675a6-289">toorun hello pipeline indefinitely, specify **9/9/9999** as hello value for hello **end** property.</span></span>

   <span data-ttu-id="675a6-290">U Hallo definieert tijdsduur aangeeft in welke Hallo gegevenssegmenten worden verwerkt op basis van Hallo **beschikbaarheid** eigenschappen die zijn gedefinieerd voor elke Azure Data Factory-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="675a6-290">You are defining hello time duration in which hello data slices are processed based on hello **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="675a6-291">In voorbeeld hello zijn er 24 gegevenssegmenten omdat elke gegevenssegment per uur is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="675a6-291">In hello example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="675a6-292">Klik op **implementeren** op Hallo opdrachtbalk toodeploy Hallo gegevensset (tabel is een rechthoekige gegevensset).</span><span class="sxs-lookup"><span data-stu-id="675a6-292">Click **Deploy** on hello command bar toodeploy hello dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="675a6-293">Bevestig dat Hallo-pijplijn wordt weergegeven in de structuurweergave Hallo onder **pijplijnen** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="675a6-293">Confirm that hello pipeline shows up in hello tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="675a6-294">Klik nu op **X** tweemaal tooclose Hallo pagina tooget back toohello **Data Factory** pagina voor Hallo **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="675a6-294">Now, click **X** twice tooclose hello page tooget back toohello **Data Factory** page for hello **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="675a6-295">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="675a6-295">**Congratulations!**</span></span> <span data-ttu-id="675a6-296">U hebt een Azure-gegevensfactory, gekoppelde services, gegevenssets en een pijplijn en geplande Hallo pijplijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="675a6-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled hello pipeline.</span></span>

#### <a name="view-hello-data-factory-in-a-diagram-view"></a><span data-ttu-id="675a6-297">Het Hallo-gegevensfactory weergeven in een diagramweergave</span><span class="sxs-lookup"><span data-stu-id="675a6-297">View hello data factory in a Diagram View</span></span>
1. <span data-ttu-id="675a6-298">In Hallo **Azure-portal**, klikt u op **Diagram** tegel op de startpagina Hallo van Hallo **ADFTutorialOnPremDF** gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="675a6-298">In hello **Azure portal**, click **Diagram** tile on hello home page for hello **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="675a6-299">:</span><span class="sxs-lookup"><span data-stu-id="675a6-299">:</span></span>

    ![Diagram koppeling](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="675a6-301">U ziet Hallo diagram vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="675a6-301">You should see hello diagram similar toohello following image:</span></span>

    ![Diagramweergave](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="675a6-303">U kunt inzoomen, uitzoomen, zoomen too100%, zoomen toofit, automatisch positie pijplijnen en gegevenssets en afkomst weergeven (upstream- en downstreamitems van items worden gemarkeerd geselecteerde).</span><span class="sxs-lookup"><span data-stu-id="675a6-303">You can zoom in, zoom out, zoom too100%, zoom toofit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="675a6-304">U kunt dubbelklikken op de eigenschappen van een object (invoer/uitvoer gegevensset of pijplijn) toosee voor.</span><span class="sxs-lookup"><span data-stu-id="675a6-304">You can double-click an object (input/output dataset or pipeline) toosee properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="675a6-305">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="675a6-305">Monitor pipeline</span></span>
<span data-ttu-id="675a6-306">In deze stap gebruikt u hello Azure portal toomonitor wat in een Azure data factory gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="675a6-306">In this step, you use hello Azure portal toomonitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="675a6-307">U kunt ook PowerShell-cmdlets toomonitor gegevenssets en pijplijnen.</span><span class="sxs-lookup"><span data-stu-id="675a6-307">You can also use PowerShell cmdlets toomonitor datasets and pipelines.</span></span> <span data-ttu-id="675a6-308">Zie voor meer informatie over het bewaken van [pijplijnen bewaken en beheren](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="675a6-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="675a6-309">Dubbelklik in het Hallo-diagram op **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="675a6-309">In hello diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable segmenten](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="675a6-311">Merk op dat alle Hallo gegevenssegmenten up zijn in **gereed** omdat Hallo pijplijn duur (tijd tooend begintijd) in de afgelopen Hallo status.</span><span class="sxs-lookup"><span data-stu-id="675a6-311">Notice that all hello data slices up are in **Ready** state because hello pipeline duration (start time tooend time) is in hello past.</span></span> <span data-ttu-id="675a6-312">Het is ook omdat u Hallo gegevens in SQL Server-database Hallo hebt geplaatst en er alle Hallo tijd is.</span><span class="sxs-lookup"><span data-stu-id="675a6-312">It is also because you have inserted hello data in hello SQL Server database and it is there all hello time.</span></span> <span data-ttu-id="675a6-313">Bevestig dat er geen segmenten in Hallo weergegeven **probleemsegmenten** sectie Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="675a6-313">Confirm that no slices show up in hello **Problem slices** section at hello bottom.</span></span> <span data-ttu-id="675a6-314">Klik op tooview alle Hallo segmenten **meer** Hallo Hallo lijst segmenten onderaan in.</span><span class="sxs-lookup"><span data-stu-id="675a6-314">tooview all hello slices, click **See More** at hello bottom of hello list of slices.</span></span>
3. <span data-ttu-id="675a6-315">Nu In Hallo **gegevenssets** pagina, klikt u op **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="675a6-315">Now, In hello **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable segmenten](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="675a6-317">Klik op een gegevenssegment uit de lijst Hallo en ziet u Hallo **gegevenssegment** pagina.</span><span class="sxs-lookup"><span data-stu-id="675a6-317">Click any data slice from hello list and you should see hello **Data Slice** page.</span></span> <span data-ttu-id="675a6-318">U ziet de activiteit wordt uitgevoerd voor Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="675a6-318">You see activity runs for hello slice.</span></span> <span data-ttu-id="675a6-319">Er is slechts één activiteit die meestal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="675a6-319">You see only one activity run usually.</span></span>  

    ![Blade gegevenssegment](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="675a6-321">Als Hallo segment zich niet in Hallo **gereed** staat, kunt u zien Hallo upstreamsegmenten die niet gereed zijn en blokkeren het huidige segment uitgevoerd Hallo Hallo **upstreamsegmenten die niet gereed** lijst.</span><span class="sxs-lookup"><span data-stu-id="675a6-321">If hello slice is not in hello **Ready** state, you can see hello upstream slices that are not Ready and are blocking hello current slice from executing in hello **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="675a6-322">Klik op Hallo **activiteit die wordt uitgevoerd** uit de lijst Hallo op Hallo onder toosee **details uitvoering van activiteit**.</span><span class="sxs-lookup"><span data-stu-id="675a6-322">Click hello **activity run** from hello list at hello bottom toosee **activity run details**.</span></span>

   ![De pagina Details uitvoering van activiteit](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="675a6-324">Ziet u informatie zoals doorvoer, de duur en Hallo gateway tootransfer Hallo gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="675a6-324">You would see information such as throughput, duration, and hello gateway used tootransfer hello data.</span></span>
6. <span data-ttu-id="675a6-325">Klik op **X** tooclose alle pagina's totdat u Hallo</span><span class="sxs-lookup"><span data-stu-id="675a6-325">Click **X** tooclose all hello pages until you</span></span>
7. <span data-ttu-id="675a6-326">startpagina toohello terughalen voor Hallo **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="675a6-326">get back toohello home page for hello **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="675a6-327">(optioneel) Klik op **pijplijnen**, klikt u op **ADFTutorialOnPremDF**, en detailanalyse van invoertabellen (**verbruikt**) of uitvoergegevenssets (**geproduceerde**).</span><span class="sxs-lookup"><span data-stu-id="675a6-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="675a6-328">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) tooverify dat een blob of het bestand is gemaakt voor elk uur.</span><span class="sxs-lookup"><span data-stu-id="675a6-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) tooverify that a blob/file is created for each hour.</span></span>

   ![Azure Opslagverkenner](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="675a6-330">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="675a6-330">Next steps</span></span>
* <span data-ttu-id="675a6-331">Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor alle informatie over Data Management Gateway Hallo Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="675a6-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all hello details about hello Data Management Gateway.</span></span>
* <span data-ttu-id="675a6-332">Zie [gegevens kopiëren van Azure Blob-tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn over hoe toouse Kopieeractiviteit toomove gegevens uit een brongegevens tooa sink gegevensopslag opslaan.</span><span class="sxs-lookup"><span data-stu-id="675a6-332">See [Copy data from Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) toolearn about how toouse Copy Activity toomove data from a source data store tooa sink data store.</span></span>
