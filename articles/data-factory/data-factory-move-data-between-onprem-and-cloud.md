---
title: Verplaatsen van gegevens - Data Management Gateway | Microsoft Docs
description: Stel een gegevensgateway in om gegevens te verplaatsen tussen on-premises en de cloud. Gebruik Data Management Gateway in Azure Data Factory om uw gegevens te verplaatsen.
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
ms.openlocfilehash: 565091e24a8c0009793e2e2365fb95013cad5028
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-between-on-premises-sources-and-the-cloud-with-data-management-gateway"></a><span data-ttu-id="f25f1-105">Gegevens verplaatsen tussen lokale bronnen en de cloud met Data Management Gateway</span><span class="sxs-lookup"><span data-stu-id="f25f1-105">Move data between on-premises sources and the cloud with Data Management Gateway</span></span>
<span data-ttu-id="f25f1-106">Dit artikel bevat een overzicht van de gegevensintegratie tussen on-premises gegevensopslagexemplaren en cloud gegevensarchieven gebruik Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f25f1-106">This article provides an overview of data integration between on-premises data stores and cloud data stores using Data Factory.</span></span> <span data-ttu-id="f25f1-107">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel en andere data factory core concepten artikelen: [gegevenssets](data-factory-create-datasets.md) en [pijplijnen](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f25f1-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article and other data factory core concepts articles: [datasets](data-factory-create-datasets.md) and [pipelines](data-factory-create-pipelines.md).</span></span>

## <a name="data-management-gateway"></a><span data-ttu-id="f25f1-108">Gegevensbeheergateway</span><span class="sxs-lookup"><span data-stu-id="f25f1-108">Data Management Gateway</span></span>
<span data-ttu-id="f25f1-109">U moet de Data Management Gateway installeren op uw on-premises machine zwevend gegevens uit een on-premises gegevensopslag inschakelen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-109">You must install Data Management Gateway on your on-premises machine to enable moving data to/from an on-premises data store.</span></span> <span data-ttu-id="f25f1-110">De gateway kan worden geïnstalleerd op dezelfde computer als het gegevensarchief of op een andere computer, zolang de gateway verbinding met de gegevensopslag maken kan.</span><span class="sxs-lookup"><span data-stu-id="f25f1-110">The gateway can be installed on the same machine as the data store or on a different machine as long as the gateway can connect to the data store.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f25f1-111">Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> 

<span data-ttu-id="f25f1-112">De volgende procedure laat zien hoe een gegevensfactory maken met een pijplijn die de gegevens vanuit een on-premises verplaatst u **SQL Server** database naar een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="f25f1-112">The following walkthrough shows you how to create a data factory with a pipeline that moves data from an on-premises **SQL Server** database to an Azure blob storage.</span></span> <span data-ttu-id="f25f1-113">Als onderdeel van de procedure installeert en configureert u de gegevensbeheergateway op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f25f1-113">As part of the walkthrough, you install and configure the Data Management Gateway on your machine.</span></span>

## <a name="walkthrough-copy-on-premises-data-to-cloud"></a><span data-ttu-id="f25f1-114">Overzicht: kopieer on-premises gegevens in de cloud</span><span class="sxs-lookup"><span data-stu-id="f25f1-114">Walkthrough: copy on-premises data to cloud</span></span>
<span data-ttu-id="f25f1-115">In dit scenario moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f25f1-115">In this walkthrough you do the following steps:</span></span> 

1. <span data-ttu-id="f25f1-116">Maak een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f25f1-116">Create a data factory.</span></span>
2. <span data-ttu-id="f25f1-117">Maak een data management gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-117">Create a data management gateway.</span></span> 
3. <span data-ttu-id="f25f1-118">Gekoppelde services voor de bron- en sink gegevensarchieven maken.</span><span class="sxs-lookup"><span data-stu-id="f25f1-118">Create linked services for source and sink data stores.</span></span>
4. <span data-ttu-id="f25f1-119">Maak gegevenssets vertegenwoordigen de invoer-en uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="f25f1-119">Create datasets to represent input and output data.</span></span>
5. <span data-ttu-id="f25f1-120">Een pijplijn maken met een kopieeractiviteit om de gegevens te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-120">Create a pipeline with a copy activity to move the data.</span></span>

## <a name="prerequisites-for-the-tutorial"></a><span data-ttu-id="f25f1-121">Vereisten voor de zelfstudie</span><span class="sxs-lookup"><span data-stu-id="f25f1-121">Prerequisites for the tutorial</span></span>
<span data-ttu-id="f25f1-122">Voordat u deze procedure begint, hebt u de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="f25f1-122">Before you begin this walkthrough, you must have the following prerequisites:</span></span>

* <span data-ttu-id="f25f1-123">**Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-123">**Azure subscription**.</span></span>  <span data-ttu-id="f25f1-124">Als u geen abonnement hebt, kunt u binnen een paar minuten een gratis proefaccount maken.</span><span class="sxs-lookup"><span data-stu-id="f25f1-124">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f25f1-125">Zie de [gratis proefversie](http://azure.microsoft.com/pricing/free-trial/) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f25f1-125">See the [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="f25f1-126">**Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-126">**Azure Storage Account**.</span></span> <span data-ttu-id="f25f1-127">Gebruik van de blob storage als een **bestemming/sink** gegevens opslaan in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f25f1-127">You use the blob storage as a **destination/sink** data store in this tutorial.</span></span> <span data-ttu-id="f25f1-128">Als u geen Azure storage-account hebt, raadpleegt u de [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor stappen voor het maken van een artikel.</span><span class="sxs-lookup"><span data-stu-id="f25f1-128">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
* <span data-ttu-id="f25f1-129">**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-129">**SQL Server**.</span></span> <span data-ttu-id="f25f1-130">U gebruikt een lokale SQL Server-database als een **bron** gegevens opslaan in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f25f1-130">You use an on-premises SQL Server database as a **source** data store in this tutorial.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="f25f1-131">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="f25f1-131">Create data factory</span></span>
<span data-ttu-id="f25f1-132">In deze stap maakt u de Azure portal gebruiken voor het maken van een Azure Data Factory-exemplaar met de naam **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-132">In this step, you use the Azure portal to create an Azure Data Factory instance named **ADFTutorialOnPremDF**.</span></span>

1. <span data-ttu-id="f25f1-133">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f25f1-133">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f25f1-134">Klik op **+ nieuw**, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-134">Click **+ NEW**, click **Intelligence + analytics**, and click **Data Factory**.</span></span>

   ![Nieuw -> DataFactory](./media/data-factory-move-data-between-onprem-and-cloud/NewDataFactoryMenu.png)  
3. <span data-ttu-id="f25f1-136">In de **nieuwe gegevensfactory** pagina **ADFTutorialOnPremDF** voor de naam.</span><span class="sxs-lookup"><span data-stu-id="f25f1-136">In the **New data factory** page, enter **ADFTutorialOnPremDF** for the Name.</span></span>

    ![Toevoegen aan Startboard](./media/data-factory-move-data-between-onprem-and-cloud/OnPremNewDataFactoryAddToStartboard.png)

   > [!IMPORTANT]
   > <span data-ttu-id="f25f1-138">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="f25f1-138">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="f25f1-139">Als u de foutmelding: **Data factory-naam 'ADFTutorialOnPremDF' is niet beschikbaar**, wijzig de naam van de gegevensfactory (bijvoorbeeld yournameADFTutorialOnPremDF) en probeert u het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f25f1-139">If you receive the error: **Data factory name “ADFTutorialOnPremDF” is not available**, change the name of the data factory (for example, yournameADFTutorialOnPremDF) and try creating again.</span></span> <span data-ttu-id="f25f1-140">Gebruik deze naam in plaats van ADFTutorialOnPremDF tijdens het uitvoeren van de resterende stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f25f1-140">Use this name in place of ADFTutorialOnPremDF while performing remaining steps in this tutorial.</span></span>
   >
   > <span data-ttu-id="f25f1-141">De naam van de gegevensfactory wordt in de toekomst mogelijk geregistreerd als **DNS**-naam en wordt daarmee ook voor iedereen zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="f25f1-141">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="f25f1-142">Selecteer het **Azure-abonnement** waarvoor u de gegevensfactory wilt maken.</span><span class="sxs-lookup"><span data-stu-id="f25f1-142">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="f25f1-143">Selecteer een bestaande **resourcegroep** of maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f25f1-143">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="f25f1-144">Voor de zelfstudie maakt u een resourcegroep met de naam: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-144">For the tutorial, create a resource group named: **ADFTutorialResourceGroup**.</span></span>
6. <span data-ttu-id="f25f1-145">Klik op **maken** op de **nieuwe gegevensfactory** pagina.</span><span class="sxs-lookup"><span data-stu-id="f25f1-145">Click **Create** on the **New data factory** page.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f25f1-146">Als u Data Factory-exemplaren wilt maken, moet u lid zijn van de rol [Inzender Data Factory](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) op abonnements-/resourcegroepsniveau.</span><span class="sxs-lookup"><span data-stu-id="f25f1-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="f25f1-147">Nadat het maken voltooid is, ziet u de **Data Factory** pagina zoals in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f25f1-147">After creation is complete, you see the **Data Factory** page as shown in the following image:</span></span>

   ![Data Factory-startpagina](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDataFactoryHomePage.png)

## <a name="create-gateway"></a><span data-ttu-id="f25f1-149">Gateway maken</span><span class="sxs-lookup"><span data-stu-id="f25f1-149">Create gateway</span></span>
1. <span data-ttu-id="f25f1-150">In de **Data Factory** pagina, klikt u op **auteur en implementeren van** tegel starten de **Editor** voor de data factory.</span><span class="sxs-lookup"><span data-stu-id="f25f1-150">In the **Data Factory** page, click **Author and deploy** tile to launch the **Editor** for the data factory.</span></span>

    ![Tegel Ontwerpen en implementeren](./media/data-factory-move-data-between-onprem-and-cloud/author-deploy-tile.png)
2. <span data-ttu-id="f25f1-152">In de Data Factory-Editor, klikt u op **... Meer** op de werkbalk en klikt u vervolgens op **nieuwe gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-152">In the Data Factory Editor, click **... More** on the toolbar and then click **New data gateway**.</span></span> <span data-ttu-id="f25f1-153">U kunt ook u kunt met de rechtermuisknop op **gegevensgateways** in de structuurweergave en klik op **nieuwe gegevensgateway**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-153">Alternatively, you can right-click **Data Gateways** in the tree view, and click **New data gateway**.</span></span>

   ![Nieuwe gegevensgateway op werkbalk](./media/data-factory-move-data-between-onprem-and-cloud/NewDataGateway.png)
3. <span data-ttu-id="f25f1-155">In de **maken** pagina **adftutorialgateway** voor de **naam**, en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-155">In the **Create** page, enter **adftutorialgateway** for the **name**, and click **OK**.</span></span>     

    ![Pagina Gateway maken](./media/data-factory-move-data-between-onprem-and-cloud/OnPremCreateGatewayBlade.png)

    > [!NOTE]
    > <span data-ttu-id="f25f1-157">In dit scenario maakt u de logische gateway met slechts één knooppunt (lokale Windows-machine).</span><span class="sxs-lookup"><span data-stu-id="f25f1-157">In this walkthrough, you create the logical gateway with only one node (on-premises Windows machine).</span></span> <span data-ttu-id="f25f1-158">U kunt een data management gateway uitbreiden door meerdere lokale computers koppelen aan de gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-158">You can scale out a data management gateway by associating multiple on-premises machines with the gateway.</span></span> <span data-ttu-id="f25f1-159">U kunt schalen omhoog door het aantal data movement taken die kunnen tegelijkertijd worden uitgevoerd op een knooppunt te verhogen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-159">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="f25f1-160">Deze functie is ook beschikbaar voor een logische gateway met één knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f25f1-160">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="f25f1-161">Zie [schaal data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f25f1-161">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>  
4. <span data-ttu-id="f25f1-162">In de **configureren** pagina, klikt u op **rechtstreeks op deze computer installeren**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-162">In the **Configure** page, click **Install directly on this computer**.</span></span> <span data-ttu-id="f25f1-163">Deze actie downloadt van het installatiepakket voor de gateway, wordt geïnstalleerd, configureert en registreert de gateway op de computer.</span><span class="sxs-lookup"><span data-stu-id="f25f1-163">This action downloads the installation package for the gateway, installs, configures, and registers the gateway on the computer.</span></span>  

   > [!NOTE]
   > <span data-ttu-id="f25f1-164">Internet Explorer of een webbrowser die Microsoft ClickOnce compatibel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f25f1-164">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>
   >
   > <span data-ttu-id="f25f1-165">Als u met Chrome werkt, gaat u naar de [Chrome Web Store](https://chrome.google.com/webstore/), zoekt u op het trefwoord 'ClickOnce', en kiest en installeert u een van de ClickOnce-extensies.</span><span class="sxs-lookup"><span data-stu-id="f25f1-165">If you are using Chrome, go to the [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>
   >
   > <span data-ttu-id="f25f1-166">Doe hetzelfde voor Firefox (install-invoegtoepassing).</span><span class="sxs-lookup"><span data-stu-id="f25f1-166">Do the same for Firefox (install add-in).</span></span> <span data-ttu-id="f25f1-167">Klik op **Menu openen** op de werkbalk (**drie horizontale lijnen** in de rechterbovenhoek), klikt u op **invoegtoepassingen**, zoeken met het sleutelwoord 'ClickOnce', kies een van de ClickOnce-extensies en te installeren.</span><span class="sxs-lookup"><span data-stu-id="f25f1-167">Click **Open Menu** button on the toolbar (**three horizontal lines** in the top-right corner), click **Add-ons**, search with "ClickOnce" keyword, choose one of the ClickOnce extensions, and install it.</span></span>    
   >
   >

    ![Gateway - pagina configureren](./media/data-factory-move-data-between-onprem-and-cloud/OnPremGatewayConfigureBlade.png)

    <span data-ttu-id="f25f1-169">Op deze manier is de eenvoudigste manier (met één muisklik) te downloaden, installeren, configureren en registreren van de gateway in één enkele stap.</span><span class="sxs-lookup"><span data-stu-id="f25f1-169">This way is the easiest way (one-click) to download, install, configure, and register the gateway in one single step.</span></span> <span data-ttu-id="f25f1-170">U ziet de **Microsoft Data Management Gateway Configuration Manager** toepassing op uw computer is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f25f1-170">You can see the **Microsoft Data Management Gateway Configuration Manager** application is installed on your computer.</span></span> <span data-ttu-id="f25f1-171">U kunt ook het uitvoerbare bestand vinden **ConfigManager.exe** in de map: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-171">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**.</span></span>

    <span data-ttu-id="f25f1-172">U kunt ook downloaden en gateway handmatig installeren met behulp van de koppelingen op deze pagina en registreren met behulp van de sleutel die wordt weergegeven in de **nieuwe sleutel** in het tekstvak.</span><span class="sxs-lookup"><span data-stu-id="f25f1-172">You can also download and install gateway manually by using the links in this page and register it using the key shown in the **NEW KEY** text box.</span></span>

    <span data-ttu-id="f25f1-173">Zie [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor de details over de gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-173">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the gateway.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f25f1-174">U moet een beheerder op de lokale computer installeren en configureren van de Data Management Gateway is.</span><span class="sxs-lookup"><span data-stu-id="f25f1-174">You must be an administrator on the local computer to install and configure the Data Management Gateway successfully.</span></span> <span data-ttu-id="f25f1-175">U kunt extra gebruikers toevoegen aan de **Data Management Gateway-gebruikers** lokale Windows-groep.</span><span class="sxs-lookup"><span data-stu-id="f25f1-175">You can add additional users to the **Data Management Gateway Users** local Windows group.</span></span> <span data-ttu-id="f25f1-176">De leden van deze groep kunnen het Data Management Gateway Configuration Manager-hulpprogramma gebruiken om de gateway te configureren.</span><span class="sxs-lookup"><span data-stu-id="f25f1-176">The members of this group can use the Data Management Gateway Configuration Manager tool to configure the gateway.</span></span>
   >
   >
5. <span data-ttu-id="f25f1-177">Wacht een paar minuten of wacht tot u de volgende melding:</span><span class="sxs-lookup"><span data-stu-id="f25f1-177">Wait for a couple of minutes or wait until you see the following notification message:</span></span>

    ![Gateway-installatie is geslaagd](./media/data-factory-move-data-between-onprem-and-cloud/gateway-install-success.png)
6. <span data-ttu-id="f25f1-179">Start **Data Management Gateway Configuration Manager** toepassing op uw computer.</span><span class="sxs-lookup"><span data-stu-id="f25f1-179">Launch **Data Management Gateway Configuration Manager** application on your computer.</span></span> <span data-ttu-id="f25f1-180">In de **Search** venster, type **Data Management Gateway** voor toegang tot dit hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="f25f1-180">In the **Search** window, type **Data Management Gateway** to access this utility.</span></span> <span data-ttu-id="f25f1-181">U kunt ook het uitvoerbare bestand vinden **ConfigManager.exe** in de map: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span><span class="sxs-lookup"><span data-stu-id="f25f1-181">You can also find the executable **ConfigManager.exe** in the folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**</span></span>

    ![Gateway-Configuratiebeheer](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDMGConfigurationManager.png)
7. <span data-ttu-id="f25f1-183">Controleer of u `adftutorialgateway is connected to the cloud service` bericht.</span><span class="sxs-lookup"><span data-stu-id="f25f1-183">Confirm that you see `adftutorialgateway is connected to the cloud service` message.</span></span> <span data-ttu-id="f25f1-184">De statusbalk in het onderste worden **verbonden met de cloudservice** samen met een **groen vinkje**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-184">The status bar the bottom displays **Connected to the cloud service** along with a **green check mark**.</span></span>

    <span data-ttu-id="f25f1-185">Op de **Start** tabblad kunt u ook de volgende bewerkingen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f25f1-185">On the **Home** tab, you can also do the following operations:</span></span>

   * <span data-ttu-id="f25f1-186">**Registreren** een gateway met een sleutel van de Azure-portal met behulp van de knop registreren.</span><span class="sxs-lookup"><span data-stu-id="f25f1-186">**Register** a gateway with a key from the Azure portal by using the Register button.</span></span>
   * <span data-ttu-id="f25f1-187">**Stop** de Data Management Gateway Host Service uitgevoerd op uw computer met de gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-187">**Stop** the Data Management Gateway Host Service running on your gateway machine.</span></span>
   * <span data-ttu-id="f25f1-188">**Updates plannen** moet worden geïnstalleerd op een bepaald tijdstip van de dag.</span><span class="sxs-lookup"><span data-stu-id="f25f1-188">**Schedule updates** to be installed at a specific time of the day.</span></span>
   * <span data-ttu-id="f25f1-189">Wanneer de gateway is **laatst bijgewerkt**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-189">View when the gateway was **last updated**.</span></span>
   * <span data-ttu-id="f25f1-190">Geef de tijd waarop een update voor de gateway kan worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f25f1-190">Specify time at which an update to the gateway can be installed.</span></span>
8. <span data-ttu-id="f25f1-191">Overschakelen naar de **instellingen** tabblad. Het certificaat dat is opgegeven in de **certificaat** worden gebruikt om de referenties voor het lokale gegevensarchief die u in de portal opgeeft versleutelen/ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-191">Switch to the **Settings** tab. The certificate specified in the **Certificate** section is used to encrypt/decrypt credentials for the on-premises data store that you specify on the portal.</span></span> <span data-ttu-id="f25f1-192">(optioneel) Klik op **wijziging** voor gebruik in plaats hiervan uw eigen certificaat.</span><span class="sxs-lookup"><span data-stu-id="f25f1-192">(optional) Click **Change** to use your own certificate instead.</span></span> <span data-ttu-id="f25f1-193">De gateway maakt standaard gebruik van het certificaat dat automatisch wordt gegenereerd door de Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="f25f1-193">By default, the gateway uses the certificate that is auto-generated by the Data Factory service.</span></span>

    ![De configuratie van de gateway-certificaat](./media/data-factory-move-data-between-onprem-and-cloud/gateway-certificate.png)

    <span data-ttu-id="f25f1-195">U kunt ook de volgende acties uitvoeren op de **instellingen** tabblad:</span><span class="sxs-lookup"><span data-stu-id="f25f1-195">You can also do the following actions on the **Settings** tab:</span></span>

   * <span data-ttu-id="f25f1-196">Weergeven of Exporteer het certificaat wordt gebruikt door de gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-196">View or export the certificate being used by the gateway.</span></span>
   * <span data-ttu-id="f25f1-197">Wijzig de HTTPS-eindpunt dat is gebruikt door de gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-197">Change the HTTPS endpoint used by the gateway.</span></span>    
   * <span data-ttu-id="f25f1-198">Stel een HTTP-proxy moet worden gebruikt door de gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-198">Set an HTTP proxy to be used by the gateway.</span></span>     
9. <span data-ttu-id="f25f1-199">(optioneel) Overschakelen naar de **Diagnostics** tabblad, Controleer de **uitgebreide logboekregistratie inschakelen** optie als u uitgebreide logboekregistratie die u gebruiken kunt voor het oplossen van problemen met de gateway in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-199">(optional) Switch to the **Diagnostics** tab, check the **Enable verbose logging** option if you want to enable verbose logging that you can use to troubleshoot any issues with the gateway.</span></span> <span data-ttu-id="f25f1-200">Gegevens in het logboek vindt u in **logboeken** onder **logboeken toepassingen en Services** -> **Data Management Gateway** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f25f1-200">The logging information can be found in **Event Viewer** under **Applications and Services Logs** -> **Data Management Gateway** node.</span></span>

    ![Tabblad Diagnostische gegevens](./media/data-factory-move-data-between-onprem-and-cloud/diagnostics-tab.png)

    <span data-ttu-id="f25f1-202">U kunt ook uitvoeren met de volgende acties in de **Diagnostics** tabblad:</span><span class="sxs-lookup"><span data-stu-id="f25f1-202">You can also perform the following actions in the **Diagnostics** tab:</span></span>

   * <span data-ttu-id="f25f1-203">Gebruik **testverbinding** sectie met een lokale gegevensbron met behulp van de gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-203">Use **Test Connection** section to an on-premises data source using the gateway.</span></span>
   * <span data-ttu-id="f25f1-204">Klik op **logboeken bekijken** om te zien van het logboek Data Management Gateway in een venster Logboeken.</span><span class="sxs-lookup"><span data-stu-id="f25f1-204">Click **View Logs** to see the Data Management Gateway log in an Event Viewer window.</span></span>
   * <span data-ttu-id="f25f1-205">Klik op **logboeken verzenden** met Logboeken van de afgelopen zeven dagen een zip-bestand uploaden naar Microsoft te vergemakkelijken oplossen van problemen met uw.</span><span class="sxs-lookup"><span data-stu-id="f25f1-205">Click **Send Logs** to upload a zip file with logs of last seven days to Microsoft to facilitate troubleshooting of your issues.</span></span>
10. <span data-ttu-id="f25f1-206">Op de **Diagnostics** tabblad, in de **testverbinding** sectie **SqlServer** voor het type van het gegevensarchief, voer de naam van de databaseserver, de naam van de database verificatietype opgeven, gebruikersnaam en wachtwoord invoeren en op **testen** om te controleren of de gateway verbinding met de database maken kan.</span><span class="sxs-lookup"><span data-stu-id="f25f1-206">On the **Diagnostics** tab, in the **Test Connection** section, select **SqlServer** for the type of the data store, enter the name of the database server, name of the database, specify authentication type, enter user name, and password, and click **Test** to test whether the gateway can connect to the database.</span></span>
11. <span data-ttu-id="f25f1-207">Ga naar de webbrowser en in de **Azure-portal**, klikt u op **OK** op de **configureren** pagina en klik vervolgens op de **nieuwe gegevensgateway** pagina.</span><span class="sxs-lookup"><span data-stu-id="f25f1-207">Switch to the web browser, and in the **Azure portal**, click **OK** on the **Configure** page and then on the **New data gateway** page.</span></span>
12. <span data-ttu-id="f25f1-208">U ziet **adftutorialgateway** onder **gegevensgateways** in de structuurweergave links.</span><span class="sxs-lookup"><span data-stu-id="f25f1-208">You should see **adftutorialgateway** under **Data Gateways** in the tree view on the left.</span></span>  <span data-ttu-id="f25f1-209">Als u erop klikt, ziet u de bijbehorende JSON.</span><span class="sxs-lookup"><span data-stu-id="f25f1-209">If you click it, you should see the associated JSON.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="f25f1-210">Gekoppelde services maken</span><span class="sxs-lookup"><span data-stu-id="f25f1-210">Create linked services</span></span>
<span data-ttu-id="f25f1-211">In deze stap maakt u twee gekoppelde services: **AzureStorageLinkedService** en **SqlServerLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-211">In this step, you create two linked services: **AzureStorageLinkedService** and **SqlServerLinkedService**.</span></span> <span data-ttu-id="f25f1-212">De **SqlServerLinkedService** koppelingen van een lokale SQL Server-database en de **AzureStorageLinkedService** gekoppelde service een Azure blob-archief is gekoppeld aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f25f1-212">The **SqlServerLinkedService** links an on-premises SQL Server database and the **AzureStorageLinkedService** linked service links an Azure blob store to the data factory.</span></span> <span data-ttu-id="f25f1-213">U maakt een pijplijn verderop in dit scenario waarmee gegevens worden gekopieerd van de lokale SQL Server-database naar de Azure blob-store.</span><span class="sxs-lookup"><span data-stu-id="f25f1-213">You create a pipeline later in this walkthrough that copies data from the on-premises SQL Server database to the Azure blob store.</span></span>

#### <a name="add-a-linked-service-to-an-on-premises-sql-server-database"></a><span data-ttu-id="f25f1-214">Een gekoppelde service toevoegen aan een lokale SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="f25f1-214">Add a linked service to an on-premises SQL Server database</span></span>
1. <span data-ttu-id="f25f1-215">In de **Data Factory-Editor**, klikt u op **nieuwe gegevensopslag** op de werkbalk en selecteer **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-215">In the **Data Factory Editor**, click **New data store** on the toolbar and select **SQL Server**.</span></span>

   ![Nieuwe SQL-Server gekoppeld-service](./media/data-factory-move-data-between-onprem-and-cloud/NewSQLServer.png)
2. <span data-ttu-id="f25f1-217">In de **JSON-editor** aan de rechterkant, komen de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f25f1-217">In the **JSON editor** on the right, do the following steps:</span></span>

   1. <span data-ttu-id="f25f1-218">Voor de **gatewayName**, geef **adftutorialgateway**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-218">For the **gatewayName**, specify **adftutorialgateway**.</span></span>    
   2. <span data-ttu-id="f25f1-219">In de **connectionString**, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f25f1-219">In the **connectionString**, do the following steps:</span></span>    

      1. <span data-ttu-id="f25f1-220">Voor **servername**, voer de naam van de server die als host fungeert voor de SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="f25f1-220">For **servername**, enter the name of the server that hosts the SQL Server database.</span></span>
      2. <span data-ttu-id="f25f1-221">Voor **databasename**, voer de naam van de database.</span><span class="sxs-lookup"><span data-stu-id="f25f1-221">For **databasename**, enter the name of the database.</span></span>
      3. <span data-ttu-id="f25f1-222">Klik op **versleutelen** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="f25f1-222">Click **Encrypt** button on the toolbar.</span></span> <span data-ttu-id="f25f1-223">Ziet u de toepassing Referentiebeheer.</span><span class="sxs-lookup"><span data-stu-id="f25f1-223">You see the Credentials Manager application.</span></span>

         ![Referenties Manager-toepassing](./media/data-factory-move-data-between-onprem-and-cloud/credentials-manager-application.png)
      4. <span data-ttu-id="f25f1-225">In de **instelling referenties** in het dialoogvenster verificatietype, gebruikersnaam en wachtwoord opgeven en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-225">In the **Setting Credentials** dialog box, specify authentication type, user name, and password, and click **OK**.</span></span> <span data-ttu-id="f25f1-226">Als de verbinding geslaagd is, de versleutelde referenties worden opgeslagen in de JSON en het dialoogvenster wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="f25f1-226">If the connection is successful, the encrypted credentials are stored in the JSON and the dialog box closes.</span></span>
      5. <span data-ttu-id="f25f1-227">Het tabblad leeg browser dat in het dialoogvenster gestart als deze optie wordt niet automatisch gesloten sluiten en terug te gaan naar het tabblad met de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f25f1-227">Close the empty browser tab that launched the dialog box if it is not automatically closed and get back to the tab with the Azure portal.</span></span>

         <span data-ttu-id="f25f1-228">Op de gatewaycomputer deze referenties zijn **versleutelde** met behulp van een Data Factory-service-certificaat.</span><span class="sxs-lookup"><span data-stu-id="f25f1-228">On the gateway machine, these credentials are **encrypted** by using a certificate that the Data Factory service owns.</span></span> <span data-ttu-id="f25f1-229">Als u wilt het certificaat dat is gekoppeld aan de Data Management Gateway in plaats daarvan gebruiken, raadpleegt u [referenties veilig instellen](#set-credentials-and-security).</span><span class="sxs-lookup"><span data-stu-id="f25f1-229">If you want to use the certificate that is associated with the Data Management Gateway instead, see [Set credentials securely](#set-credentials-and-security).</span></span>    
   3. <span data-ttu-id="f25f1-230">Klik op **implementeren** gekoppelde service op de opdrachtbalk voor het implementeren van de SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="f25f1-230">Click **Deploy** on the command bar to deploy the SQL Server linked service.</span></span> <span data-ttu-id="f25f1-231">Hier ziet u de gekoppelde service in de structuurweergave.</span><span class="sxs-lookup"><span data-stu-id="f25f1-231">You should see the linked service in the tree view.</span></span>

      ![De service SQL Server is gekoppeld in de structuurweergave](./media/data-factory-move-data-between-onprem-and-cloud/sql-linked-service-in-tree-view.png)    

#### <a name="add-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="f25f1-233">Een gekoppelde service voor een Azure storage-account toevoegen</span><span class="sxs-lookup"><span data-stu-id="f25f1-233">Add a linked service for an Azure storage account</span></span>
1. <span data-ttu-id="f25f1-234">In de **Data Factory-Editor**, klikt u op **nieuwe gegevensopslag** op de opdrachtbalk klikken en op **Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-234">In the **Data Factory Editor**, click **New data store** on the command bar and click **Azure storage**.</span></span>
2. <span data-ttu-id="f25f1-235">Voer de naam van uw Azure storage-account voor de **accountnaam**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-235">Enter the name of your Azure storage account for the **Account name**.</span></span>
3. <span data-ttu-id="f25f1-236">Voer de sleutel voor uw Azure storage-account voor de **accountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-236">Enter the key for your Azure storage account for the **Account key**.</span></span>
4. <span data-ttu-id="f25f1-237">Klik op **implementeren** voor het implementeren van de **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-237">Click **Deploy** to deploy the **AzureStorageLinkedService**.</span></span>

## <a name="create-datasets"></a><span data-ttu-id="f25f1-238">Gegevenssets maken</span><span class="sxs-lookup"><span data-stu-id="f25f1-238">Create datasets</span></span>
<span data-ttu-id="f25f1-239">In deze stap maakt u invoer en uitvoergegevenssets maken die invoer- en gegevens voor de kopieerbewerking vertegenwoordigen (On-premises SQL Server-database = > Azure-blobopslag).</span><span class="sxs-lookup"><span data-stu-id="f25f1-239">In this step, you create input and output datasets that represent input and output data for the copy operation (On-premises SQL Server database => Azure blob storage).</span></span> <span data-ttu-id="f25f1-240">Voordat u de gegevenssets, voer de volgende stappen uit (gedetailleerde stappen volgt de lijst):</span><span class="sxs-lookup"><span data-stu-id="f25f1-240">Before creating datasets, do the following steps (detailed steps follows the list):</span></span>

* <span data-ttu-id="f25f1-241">Maak een tabel met de naam **emp** in de SQL Server-Database u als een gekoppelde service toegevoegd aan de gegevensfactory en enkele voorbeelden van vermeldingen in de tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-241">Create a table named **emp** in the SQL Server Database you added as a linked service to the data factory and insert a couple of sample entries into the table.</span></span>
* <span data-ttu-id="f25f1-242">Maak een blobcontainer met de naam **adftutorial** in de Azure blob storage-account die u als een gekoppelde service toegevoegd aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f25f1-242">Create a blob container named **adftutorial** in the Azure blob storage account you added as a linked service to the data factory.</span></span>

### <a name="prepare-on-premises-sql-server-for-the-tutorial"></a><span data-ttu-id="f25f1-243">On-premises SQL Server voorbereiden voor de zelfstudie</span><span class="sxs-lookup"><span data-stu-id="f25f1-243">Prepare On-premises SQL Server for the tutorial</span></span>
1. <span data-ttu-id="f25f1-244">In de database die u hebt opgegeven voor de on-premises gekoppelde SQL Server service (**SqlServerLinkedService**), de volgende SQL-script gebruiken om te maken de **emp** tabel in de database.</span><span class="sxs-lookup"><span data-stu-id="f25f1-244">In the database you specified for the on-premises SQL Server linked service (**SqlServerLinkedService**), use the following SQL script to create the **emp** table in the database.</span></span>

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
2. <span data-ttu-id="f25f1-245">Aantal voorbeelden in de tabel invoegen:</span><span class="sxs-lookup"><span data-stu-id="f25f1-245">Insert some sample into the table:</span></span>

    ```SQL
    INSERT INTO emp VALUES ('John', 'Doe')
    INSERT INTO emp VALUES ('Jane', 'Doe')
    ```

### <a name="create-input-dataset"></a><span data-ttu-id="f25f1-246">Invoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="f25f1-246">Create input dataset</span></span>

1. <span data-ttu-id="f25f1-247">Klik in de **Data Factory-editor** op **... Meer**, klikt u op **nieuwe gegevensset** op de opdrachtbalk klikken en op **SQL Server-tabel**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-247">In the **Data Factory Editor**, click **... More**, click **New dataset** on the command bar, and click **SQL Server table**.</span></span>
2. <span data-ttu-id="f25f1-248">Vervang de JSON in het rechterdeelvenster met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f25f1-248">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="f25f1-249">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="f25f1-249">Note the following points:</span></span>

   * <span data-ttu-id="f25f1-250">**type** is ingesteld op **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-250">**type** is set to **SqlServerTable**.</span></span>
   * <span data-ttu-id="f25f1-251">**tableName** is ingesteld op **emp**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-251">**tableName** is set to **emp**.</span></span>
   * <span data-ttu-id="f25f1-252">**linkedServiceName** is ingesteld op **SqlServerLinkedService** (u hebt deze gekoppelde service gemaakt eerder in dit scenario.).</span><span class="sxs-lookup"><span data-stu-id="f25f1-252">**linkedServiceName** is set to **SqlServerLinkedService** (you had created this linked service earlier in this walkthrough.).</span></span>
   * <span data-ttu-id="f25f1-253">Voor een invoergegevensset die niet worden gegenereerd door een andere pijplijn in Azure Data Factory, moet u instellen **externe** naar **true**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-253">For an input dataset that is not generated by another pipeline in Azure Data Factory, you must set **external** to **true**.</span></span> <span data-ttu-id="f25f1-254">Hiermee wordt aangegeven dat de invoergegevens buiten de Azure Data Factory-service wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="f25f1-254">It denotes the input data is produced external to the Azure Data Factory service.</span></span> <span data-ttu-id="f25f1-255">U kunt optioneel opgeven de beleidsregels van elke externe gegevens met behulp van de **externalData** -element in de **beleid** sectie.</span><span class="sxs-lookup"><span data-stu-id="f25f1-255">You can optionally specify any external data policies using the **externalData** element in the **Policy** section.</span></span>    

   <span data-ttu-id="f25f1-256">Zie [gegevens verplaatsen naar/van de SQL Server](data-factory-sqlserver-connector.md) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-256">See [Move data to/from SQL Server](data-factory-sqlserver-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="f25f1-257">Klik op **implementeren** op de opdrachtbalk om de gegevensset te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f25f1-257">Click **Deploy** on the command bar to deploy the dataset.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="f25f1-258">Uitvoergegevensset maken</span><span class="sxs-lookup"><span data-stu-id="f25f1-258">Create output dataset</span></span>

1. <span data-ttu-id="f25f1-259">In de **Data Factory-Editor**, klikt u op **nieuwe gegevensset** op de opdrachtbalk klikken en op **Azure Blob storage**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-259">In the **Data Factory Editor**, click **New dataset** on the command bar, and click **Azure Blob storage**.</span></span>
2. <span data-ttu-id="f25f1-260">Vervang de JSON in het rechterdeelvenster met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f25f1-260">Replace the JSON in the right pane with the following text:</span></span>

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
   <span data-ttu-id="f25f1-261">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="f25f1-261">Note the following points:</span></span>

   * <span data-ttu-id="f25f1-262">**type** is ingesteld op **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-262">**type** is set to **AzureBlob**.</span></span>
   * <span data-ttu-id="f25f1-263">**linkedServiceName** is ingesteld op **AzureStorageLinkedService** (u hebt deze gekoppelde service gemaakt in stap 2).</span><span class="sxs-lookup"><span data-stu-id="f25f1-263">**linkedServiceName** is set to **AzureStorageLinkedService** (you had created this linked service in Step 2).</span></span>
   * <span data-ttu-id="f25f1-264">**folderPath** is ingesteld op **adftutorial/outfromonpremdf** waar outfromonpremdf is de map in de container adftutorial.</span><span class="sxs-lookup"><span data-stu-id="f25f1-264">**folderPath** is set to **adftutorial/outfromonpremdf** where outfromonpremdf is the folder in the adftutorial container.</span></span> <span data-ttu-id="f25f1-265">Maak de **adftutorial** container als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="f25f1-265">Create the **adftutorial** container if it does not already exist.</span></span>
   * <span data-ttu-id="f25f1-266">De **beschikbaarheid** wordt ingesteld op **elk uur** (de **frequentie** wordt ingesteld op **elk uur** en het **interval** wordt ingesteld op **1**).</span><span class="sxs-lookup"><span data-stu-id="f25f1-266">The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).</span></span>  <span data-ttu-id="f25f1-267">De Data Factory-service een gegevenssegment uitvoer genereert elk uur in de **emp** tabel in de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f25f1-267">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL Database.</span></span>

   <span data-ttu-id="f25f1-268">Als u geen opgeeft een **fileName** voor een **uitvoertabel**, de bestanden in die worden gegenereerd de **folderPath** zijn met de naam in de volgende indeling: Data.<Guid>. txt (bijvoorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="f25f1-268">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

   <span data-ttu-id="f25f1-269">Om in te stellen **folderPath** en **fileName** dynamisch op basis van de **SliceStart** tijd, gebruikt u de eigenschap partitionedBy.</span><span class="sxs-lookup"><span data-stu-id="f25f1-269">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the partitionedBy property.</span></span> <span data-ttu-id="f25f1-270">In het volgende voorbeeld worden voor folderPath Year, Month en Day gebruikt van de SliceStart-waarde (tijd waarop is begonnen met het verwerken van het segment). Voor fileName wordt gebruikgemaakt van Hour van de SliceStart-waarde.</span><span class="sxs-lookup"><span data-stu-id="f25f1-270">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="f25f1-271">Als er bijvoorbeeld een segment wordt geproduceerd voor 2014-10-20T08:00:00, wordt folderName ingesteld op wikidatagateway/wikisampledataout/2014/10/20 en wordt fileName ingesteld op 08.csv.</span><span class="sxs-lookup"><span data-stu-id="f25f1-271">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span>

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

    <span data-ttu-id="f25f1-272">Zie [gegevens verplaatsen naar/van Azure Blob Storage](data-factory-azure-blob-connector.md) voor meer informatie over de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f25f1-272">See [Move data to/from Azure Blob Storage](data-factory-azure-blob-connector.md) for details about JSON properties.</span></span>
3. <span data-ttu-id="f25f1-273">Klik op **implementeren** op de opdrachtbalk om de gegevensset te implementeren.</span><span class="sxs-lookup"><span data-stu-id="f25f1-273">Click **Deploy** on the command bar to deploy the dataset.</span></span> <span data-ttu-id="f25f1-274">Controleer of u zowel de gegevenssets in de structuurweergave.</span><span class="sxs-lookup"><span data-stu-id="f25f1-274">Confirm that you see both the datasets in the tree view.</span></span>  

## <a name="create-pipeline"></a><span data-ttu-id="f25f1-275">Pijplijn maken</span><span class="sxs-lookup"><span data-stu-id="f25f1-275">Create pipeline</span></span>
<span data-ttu-id="f25f1-276">In deze stap maakt u een **pijplijn** met een **Kopieeractiviteit** die gebruikmaakt van **EmpOnPremSQLTable** als invoer en **OutputBlobTable** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f25f1-276">In this step, you create a **pipeline** with one **Copy Activity** that uses **EmpOnPremSQLTable** as input and **OutputBlobTable** as output.</span></span>

1. <span data-ttu-id="f25f1-277">Klik in Data Factory-Editor **... Meer** en vervolgens op **Nieuwe pijplijn**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-277">In Data Factory Editor, click **... More**, and click **New pipeline**.</span></span>
2. <span data-ttu-id="f25f1-278">Vervang de JSON in het rechterdeelvenster met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f25f1-278">Replace the JSON in the right pane with the following text:</span></span>    

    ```JSON   
     {
         "name": "ADFTutorialPipelineOnPrem",
         "properties": {
         "description": "This pipeline has one Copy activity that copies data from an on-prem SQL to Azure blob",
         "activities": [
           {
             "name": "CopyFromSQLtoBlob",
             "description": "Copy data from on-prem SQL server to blob",
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
   > <span data-ttu-id="f25f1-279">Vervang de waarde van de eigenschap **start** door de huidige dag en de waarde **end** door de volgende dag.</span><span class="sxs-lookup"><span data-stu-id="f25f1-279">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span>
   >
   >

   <span data-ttu-id="f25f1-280">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="f25f1-280">Note the following points:</span></span>

   * <span data-ttu-id="f25f1-281">In het gedeelte activiteiten is alleen activiteit waarvan **type** is ingesteld op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-281">In the activities section, there is only activity whose **type** is set to **Copy**.</span></span>
   * <span data-ttu-id="f25f1-282">**Invoer** voor de activiteit is ingesteld op **EmpOnPremSQLTable** en **uitvoer** voor de activiteit is ingesteld op **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-282">**Input** for the activity is set to **EmpOnPremSQLTable** and **output** for the activity is set to **OutputBlobTable**.</span></span>
   * <span data-ttu-id="f25f1-283">In de **typeProperties** sectie **SqlSource** is opgegeven als de **gegevensbrontype** en ** BlobSink ** is opgegeven als de **sink-type**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-283">In the **typeProperties** section, **SqlSource** is specified as the **source type** and **BlobSink **is specified as the **sink type**.</span></span>
   * <span data-ttu-id="f25f1-284">SQL-query `select * from emp` is opgegeven voor de **sqlReaderQuery** eigenschap van **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-284">SQL query `select * from emp` is specified for the **sqlReaderQuery** property of **SqlSource**.</span></span>

   <span data-ttu-id="f25f1-285">Zowel de begin- als einddatum en -tijd moeten de [ISO-indeling](http://en.wikipedia.org/wiki/ISO_8601) hebben.</span><span class="sxs-lookup"><span data-stu-id="f25f1-285">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="f25f1-286">Bijvoorbeeld: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="f25f1-286">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="f25f1-287">De **eindtijd** is optioneel, maar we gebruiken hem in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="f25f1-287">The **end** time is optional, but we use it in this tutorial.</span></span>

   <span data-ttu-id="f25f1-288">Als u geen waarde opgeeft voor de eigenschap **end**, wordt automatisch **start + 48 uur** gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f25f1-288">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="f25f1-289">Als u de pijplijn voor onbepaalde tijd wilt uitvoeren, geeft u **9/9/9999** op als waarde voor de eigenschap **end**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-289">To run the pipeline indefinitely, specify **9/9/9999** as the value for the **end** property.</span></span>

   <span data-ttu-id="f25f1-290">U definieert de tijdsduur waarin de gegevenssegmenten worden verwerkt op basis van de **beschikbaarheid** eigenschappen die zijn gedefinieerd voor elke Azure Data Factory-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="f25f1-290">You are defining the time duration in which the data slices are processed based on the **Availability** properties that were defined for each Azure Data Factory dataset.</span></span>

   <span data-ttu-id="f25f1-291">In het bovenstaande voorbeeld zijn er 24 gegevenssegmenten omdat er elk uur één gegevenssegment wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f25f1-291">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>        
3. <span data-ttu-id="f25f1-292">Klik op **implementeren** op de opdrachtbalk om de gegevensset te implementeren (tabel is een rechthoekige gegevensset).</span><span class="sxs-lookup"><span data-stu-id="f25f1-292">Click **Deploy** on the command bar to deploy the dataset (table is a rectangular dataset).</span></span> <span data-ttu-id="f25f1-293">Bevestig dat de pijplijn wordt weergegeven in de structuurweergave onder **pijplijnen** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f25f1-293">Confirm that the pipeline shows up in the tree view under **Pipelines** node.</span></span>  
4. <span data-ttu-id="f25f1-294">Klik nu op **X** twee keer te sluiten van de pagina terugkeren naar de **Data Factory** pagina voor de **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-294">Now, click **X** twice to close the page to get back to the **Data Factory** page for the **ADFTutorialOnPremDF**.</span></span>

<span data-ttu-id="f25f1-295">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="f25f1-295">**Congratulations!**</span></span> <span data-ttu-id="f25f1-296">U hebt een Azure-gegevensfactory, gekoppelde services, gegevenssets en een pijplijn gemaakt en u hebt ingesteld voor de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="f25f1-296">You have successfully created an Azure data factory, linked services, datasets, and a pipeline and scheduled the pipeline.</span></span>

#### <a name="view-the-data-factory-in-a-diagram-view"></a><span data-ttu-id="f25f1-297">De gegevensfactory weergeven in een diagramweergave</span><span class="sxs-lookup"><span data-stu-id="f25f1-297">View the data factory in a Diagram View</span></span>
1. <span data-ttu-id="f25f1-298">In de **Azure-portal**, klikt u op **Diagram** tegel op de startpagina van de **ADFTutorialOnPremDF** gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="f25f1-298">In the **Azure portal**, click **Diagram** tile on the home page for the **ADFTutorialOnPremDF** data factory.</span></span> <span data-ttu-id="f25f1-299">:</span><span class="sxs-lookup"><span data-stu-id="f25f1-299">:</span></span>

    ![Diagram koppeling](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramLink.png)
2. <span data-ttu-id="f25f1-301">U ziet een diagram dat lijkt op de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="f25f1-301">You should see the diagram similar to the following image:</span></span>

    ![Diagramweergave](./media/data-factory-move-data-between-onprem-and-cloud/OnPremDiagramView.png)

    <span data-ttu-id="f25f1-303">U kunt inzoomen, uitzoomen, zoomen naar 100%, zoomen past, automatisch plaats pijplijnen en gegevenssets en afkomst weergeven (upstream- en downstreamitems van items worden gemarkeerd geselecteerde).</span><span class="sxs-lookup"><span data-stu-id="f25f1-303">You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and datasets, and show lineage information (highlights upstream and downstream items of selected items).</span></span>  <span data-ttu-id="f25f1-304">U kunt dubbelklikken op een object (invoer/uitvoer gegevensset of pijplijn) Controleer de eigenschappen voor.</span><span class="sxs-lookup"><span data-stu-id="f25f1-304">You can double-click an object (input/output dataset or pipeline) to see properties for it.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="f25f1-305">De pijplijn bewaken</span><span class="sxs-lookup"><span data-stu-id="f25f1-305">Monitor pipeline</span></span>
<span data-ttu-id="f25f1-306">In deze stap gebruikt u Azure Portal om te controleren wat er gebeurt in een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="f25f1-306">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span> <span data-ttu-id="f25f1-307">U kunt ook PowerShell-cmdlets gebruiken om gegevenssets en pijplijnen te bewaken.</span><span class="sxs-lookup"><span data-stu-id="f25f1-307">You can also use PowerShell cmdlets to monitor datasets and pipelines.</span></span> <span data-ttu-id="f25f1-308">Zie voor meer informatie over het bewaken van [pijplijnen bewaken en beheren](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="f25f1-308">For details about monitoring, see [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md).</span></span>

1. <span data-ttu-id="f25f1-309">Dubbelklik in het diagram op **EmpOnPremSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-309">In the diagram, double-click **EmpOnPremSQLTable**.</span></span>  

    ![EmpOnPremSQLTable segmenten](./media/data-factory-move-data-between-onprem-and-cloud/OnPremSQLTableSlicesBlade.png)
2. <span data-ttu-id="f25f1-311">U ziet dat de gegevenssegmenten up allemaal **gereed** status omdat de pipeline-duur (tijd met de eindtijd) in het verleden.</span><span class="sxs-lookup"><span data-stu-id="f25f1-311">Notice that all the data slices up are in **Ready** state because the pipeline duration (start time to end time) is in the past.</span></span> <span data-ttu-id="f25f1-312">Het is ook omdat u de gegevens in de SQL Server-database hebt geplaatst en er voortdurend.</span><span class="sxs-lookup"><span data-stu-id="f25f1-312">It is also because you have inserted the data in the SQL Server database and it is there all the time.</span></span> <span data-ttu-id="f25f1-313">Bevestig dat er geen segmenten weergegeven in de **probleemsegmenten** sectie onderaan.</span><span class="sxs-lookup"><span data-stu-id="f25f1-313">Confirm that no slices show up in the **Problem slices** section at the bottom.</span></span> <span data-ttu-id="f25f1-314">Als u wilt weergeven van alle segmenten **meer** onder aan de lijst met segmenten.</span><span class="sxs-lookup"><span data-stu-id="f25f1-314">To view all the slices, click **See More** at the bottom of the list of slices.</span></span>
3. <span data-ttu-id="f25f1-315">Nu In de **gegevenssets** pagina, klikt u op **OutputBlobTable**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-315">Now, In the **Datasets** page, click **OutputBlobTable**.</span></span>

    ![OputputBlobTable segmenten](./media/data-factory-move-data-between-onprem-and-cloud/OutputBlobTableSlicesBlade.png)
4. <span data-ttu-id="f25f1-317">Klik op een gegevenssegment uit de lijst en u ziet de **gegevenssegment** pagina.</span><span class="sxs-lookup"><span data-stu-id="f25f1-317">Click any data slice from the list and you should see the **Data Slice** page.</span></span> <span data-ttu-id="f25f1-318">U ziet dat de activiteit voor het segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f25f1-318">You see activity runs for the slice.</span></span> <span data-ttu-id="f25f1-319">Er is slechts één activiteit die meestal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f25f1-319">You see only one activity run usually.</span></span>  

    ![Blade gegevenssegment](./media/data-factory-move-data-between-onprem-and-cloud/DataSlice.png)

    <span data-ttu-id="f25f1-321">Als het segment niet de status **Gereed** heeft, kunt u de upstreamsegmenten bekijken die niet de status Gereed hebben en die voorkomen dat de huidige status wordt uitgevoerd. U ziet deze segmenten in de lijst **Upstreamsegmenten die niet gereed zijn**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-321">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
5. <span data-ttu-id="f25f1-322">Klik op de **activiteit die wordt uitgevoerd** uit de lijst onderaan om te zien **details uitvoering van activiteit**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-322">Click the **activity run** from the list at the bottom to see **activity run details**.</span></span>

   ![De pagina Details uitvoering van activiteit](./media/data-factory-move-data-between-onprem-and-cloud/ActivityRunDetailsBlade.png)

   <span data-ttu-id="f25f1-324">Hier ziet u informatie zoals de doorvoer, de duur en de gateway die wordt gebruikt voor de gegevensoverdracht.</span><span class="sxs-lookup"><span data-stu-id="f25f1-324">You would see information such as throughput, duration, and the gateway used to transfer the data.</span></span>
6. <span data-ttu-id="f25f1-325">Klik op **X** alle pagina's totdat u sluiten</span><span class="sxs-lookup"><span data-stu-id="f25f1-325">Click **X** to close all the pages until you</span></span>
7. <span data-ttu-id="f25f1-326">teruggaan naar de startpagina van de **ADFTutorialOnPremDF**.</span><span class="sxs-lookup"><span data-stu-id="f25f1-326">get back to the home page for the **ADFTutorialOnPremDF**.</span></span>
8. <span data-ttu-id="f25f1-327">(optioneel) Klik op **pijplijnen**, klikt u op **ADFTutorialOnPremDF**, en detailanalyse van invoertabellen (**verbruikt**) of uitvoergegevenssets (**geproduceerde**).</span><span class="sxs-lookup"><span data-stu-id="f25f1-327">(optional) Click **Pipelines**, click **ADFTutorialOnPremDF**, and drill through input tables (**Consumed**) or output datasets (**Produced**).</span></span>
9. <span data-ttu-id="f25f1-328">Gebruik hulpprogramma's zoals [Microsoft Opslagverkenner](http://storageexplorer.com/) om te controleren of een blob of het bestand is gemaakt voor elk uur.</span><span class="sxs-lookup"><span data-stu-id="f25f1-328">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to verify that a blob/file is created for each hour.</span></span>

   ![Azure Opslagverkenner](./media/data-factory-move-data-between-onprem-and-cloud/OnPremAzureStorageExplorer.png)

## <a name="next-steps"></a><span data-ttu-id="f25f1-330">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f25f1-330">Next steps</span></span>
* <span data-ttu-id="f25f1-331">Zie [Data Management Gateway](data-factory-data-management-gateway.md) artikel voor de details over de Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="f25f1-331">See [Data Management Gateway](data-factory-data-management-gateway.md) article for all the details about the Data Management Gateway.</span></span>
* <span data-ttu-id="f25f1-332">Zie [gegevens kopiëren van Azure-Blob naar Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor meer informatie over het gebruik van de Kopieeractiviteit om gegevens te verplaatsen van een brongegevensarchief naar een gegevensopslag sink.</span><span class="sxs-lookup"><span data-stu-id="f25f1-332">See [Copy data from Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to learn about how to use Copy Activity to move data from a source data store to a sink data store.</span></span>
