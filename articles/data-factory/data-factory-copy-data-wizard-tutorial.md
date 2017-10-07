---
title: "Zelfstudie: een pijplijn maken met de wizard Kopiëren | Microsoft Docs"
description: "In deze zelfstudie maakt maakt u een Azure Data Factory-pijplijn met een Kopieeractiviteit via Hallo Wizard kopiëren die door Data Factory worden ondersteund"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="0c76d-103">Zelfstudie: een pijplijn maken met de kopieeractiviteit middels de Data Factory-wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="0c76d-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0c76d-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="0c76d-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="0c76d-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="0c76d-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="0c76d-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0c76d-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="0c76d-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0c76d-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="0c76d-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c76d-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="0c76d-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="0c76d-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="0c76d-110">REST API</span><span class="sxs-lookup"><span data-stu-id="0c76d-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="0c76d-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="0c76d-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="0c76d-112">Deze zelfstudie leert u hoe toouse hello **Wizard kopiëren** toocopy gegevens uit een Azure blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0c76d-112">This tutorial shows you how toouse hello **Copy Wizard** toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

<span data-ttu-id="0c76d-113">Hello Azure Data Factory **Wizard kopiëren** kunt u tooquickly een gegevens-pijplijn waarmee gegevens worden gekopieerd van een ondersteunde gegevensbron data store tooa ondersteund doelgegevensopslagplaats maken.</span><span class="sxs-lookup"><span data-stu-id="0c76d-113">hello Azure Data Factory **Copy Wizard** allows you tooquickly create a data pipeline that copies data from a supported source data store tooa supported destination data store.</span></span> <span data-ttu-id="0c76d-114">Daarom raden we aan Hallo wizard te gebruiken als een eerste stap toocreate een voorbeeldpijplijn voor uw scenario van de verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="0c76d-114">Therefore, we recommend that you use hello wizard as a first step toocreate a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="0c76d-115">Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als doel.</span><span class="sxs-lookup"><span data-stu-id="0c76d-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="0c76d-116">Deze zelfstudie leert u hoe toocreate een Azure data factory, Hallo Start de Wizard kopiëren, gaat u door een reeks stappen tooprovide details over uw gegevens opname/gegevensverplaatsing scenario.</span><span class="sxs-lookup"><span data-stu-id="0c76d-116">This tutorial shows you how toocreate an Azure data factory, launch hello Copy Wizard, go through a series of steps tooprovide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="0c76d-117">Wanneer u klaar bent met stappen in de wizard Hallo Hallo wizard maakt automatisch een pijplijn met een Kopieeractiviteit toocopy-gegevens van een Azure blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0c76d-117">When you finish steps in hello wizard, hello wizard automatically creates a pipeline with a Copy Activity toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="0c76d-118">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="0c76d-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c76d-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0c76d-119">Prerequisites</span></span>
<span data-ttu-id="0c76d-120">Voldoen aan vereisten die worden vermeld in Hallo [overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) artikel voordat u deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="0c76d-120">Complete prerequisites listed in hello [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="0c76d-121">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="0c76d-121">Create data factory</span></span>
<span data-ttu-id="0c76d-122">In deze stap gebruikt u Hallo toocreate met Azure portal een Azure-gegevensfactory met de naam **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-122">In this step, you use hello Azure portal toocreate an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="0c76d-123">Meld u bij te[Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c76d-123">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c76d-124">Klik op **+ nieuw** van de linkerbovenhoek hello, klikt u op **gegevens en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-124">Click **+ NEW** from hello top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Nieuw -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="0c76d-126">In Hallo **nieuwe gegevensfactory** blade:</span><span class="sxs-lookup"><span data-stu-id="0c76d-126">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="0c76d-127">Voer **ADFTutorialDataFactory** voor Hallo **naam**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-127">Enter **ADFTutorialDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="0c76d-128">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="0c76d-128">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="0c76d-129">Als u de foutmelding Hallo: `Data factory name “ADFTutorialDataFactory” is not available`, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameADFTutorialDataFactoryYYYYMMDD) en probeert u het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="0c76d-129">If you receive hello error: `Data factory name “ADFTutorialDataFactory” is not available`, change hello name of hello data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="0c76d-130">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="0c76d-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Naam van gegevensfactory niet beschikbaar](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="0c76d-132">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="0c76d-133">Voor de resourcegroep Doe Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0c76d-133">For Resource Group, do one of hello following steps:</span></span> 
      
      - <span data-ttu-id="0c76d-134">Selecteer **gebruik bestaande** tooselect een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0c76d-134">Select **Use existing** tooselect an existing resource group.</span></span>
      - <span data-ttu-id="0c76d-135">Selecteer **nieuw** tooenter een naam voor een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0c76d-135">Select **Create new** tooenter a name for a resource group.</span></span>
          
        <span data-ttu-id="0c76d-136">Sommige van Hallo stappen in deze zelfstudie wordt ervan uitgegaan dat u de naam van de Hallo: **ADFTutorialResourceGroup** voor Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="0c76d-136">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="0c76d-137">toolearn over resourcegroepen, Zie [toomanage uw Azure-resources met behulp van de resource groepen](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0c76d-137">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="0c76d-138">Selecteer een **locatie** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="0c76d-138">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="0c76d-139">Selecteer **pincode toodashboard** selectievakje onderaan Hallo Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="0c76d-139">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="0c76d-140">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-140">Click **Create**.</span></span>
      
       ![Blade voor een nieuwe gegevensfactory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="0c76d-142">Nadat het maken van Hallo voltooid is, ziet u Hallo **Data Factory** blade zoals weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="0c76d-142">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>
   
   ![Startpagina van de gegevensfactory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="0c76d-144">De wizard Kopiëren starten</span><span class="sxs-lookup"><span data-stu-id="0c76d-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="0c76d-145">Klik op de Data Factory-blade hello, **kopiëren van gegevens [PREVIEW]** toolaunch hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-145">On hello Data Factory blade, click **Copy data [PREVIEW]** toolaunch hello **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="0c76d-146">Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt **blokkeren van cookies van derden en sitegegevens** instelling in de browserinstellingen hello (of) Houd deze ingeschakeld en maakt een uitzondering voor  **Login.microsoftonline.com** en probeer het opnieuw starten van Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="0c76d-146">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in hello browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="0c76d-147">In Hallo **eigenschappen** pagina:</span><span class="sxs-lookup"><span data-stu-id="0c76d-147">In hello **Properties** page:</span></span>
   
   1. <span data-ttu-id="0c76d-148">Voer **CopyFromBlobToAzureSql** in als **taaknaam**</span><span class="sxs-lookup"><span data-stu-id="0c76d-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="0c76d-149">Voer de **beschrijving** in (optioneel).</span><span class="sxs-lookup"><span data-stu-id="0c76d-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="0c76d-150">Wijziging Hallo **begindatum tijd** en Hallo **einddatum en-tijd** zodat Hallo-einddatum is ingesteld tootoday en datum toofive dagen eerder worden gestart.</span><span class="sxs-lookup"><span data-stu-id="0c76d-150">Change hello **Start date time** and hello **End date time** so that hello end date is set tootoday and start date toofive days earlier.</span></span>  
   4. <span data-ttu-id="0c76d-151">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-151">Click **Next**.</span></span>  
      
      ![Hulpprogramma voor kopiëren - pagina Eigenschappen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="0c76d-153">Op Hallo **brongegevensarchief** pagina, klikt u op **Azure Blob Storage** tegel.</span><span class="sxs-lookup"><span data-stu-id="0c76d-153">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="0c76d-154">U gebruikt deze pagina toospecify Hallo-brongegevensarchief voor Hallo kopieertaak.</span><span class="sxs-lookup"><span data-stu-id="0c76d-154">You use this page toospecify hello source data store for hello copy task.</span></span> 
   
    ![Hulpprogramma voor kopiëren - pagina van brongegevensarchief](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="0c76d-156">Op Hallo **hello Azure Blob storage-account opgeven** pagina:</span><span class="sxs-lookup"><span data-stu-id="0c76d-156">On hello **Specify hello Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="0c76d-157">Voer **AzureStorageLinkedService** in als **naam van de gekoppelde service**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="0c76d-158">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="0c76d-159">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="0c76d-160">Selecteer een **Azure storage-account** van Hallo lijst met Azure storage accounts beschikbaar in het abonnement Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="0c76d-160">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="0c76d-161">U kunt ook tooenter Opslaginstellingen account handmatig door het selecteren van **handmatig invoeren** optie voor Hallo **Accountselectiemethode**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-161">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**, and then click **Next**.</span></span> 
      
      ![Hulpprogramma voor kopiëren - hello Azure Blob storage-account opgeven](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="0c76d-163">Op **Kies Hallo invoerbestand of de map** pagina:</span><span class="sxs-lookup"><span data-stu-id="0c76d-163">On **Choose hello input file or folder** page:</span></span>
   
   1. <span data-ttu-id="0c76d-164">Dubbelklik op **adftutorial** (map).</span><span class="sxs-lookup"><span data-stu-id="0c76d-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="0c76d-165">Selecteer **emp.txt** en klik op **Kiezen**</span><span class="sxs-lookup"><span data-stu-id="0c76d-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="0c76d-167">Op Hallo **Kies Hallo invoerbestand of de map** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-167">On hello **Choose hello input file or folder** page, click **Next**.</span></span> <span data-ttu-id="0c76d-168">Selecteer niet **Binaire kopie**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-168">Do not select **Binary copy**.</span></span> 
   
    ![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="0c76d-170">Op Hallo **bestandsindelingsinstellingen** pagina ziet u Hallo scheidingstekens en het Hallo-schema die automatisch worden gedetecteerd door de wizard Hallo door parseren Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="0c76d-170">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> <span data-ttu-id="0c76d-171">U kunt ook Hallo scheidingstekens handmatig invoeren voor Hallo kopie wizard toostop auto-detecteren of toooverride.</span><span class="sxs-lookup"><span data-stu-id="0c76d-171">You can also enter hello delimiters manually for hello copy wizard toostop auto-detecting or toooverride.</span></span> <span data-ttu-id="0c76d-172">Klik op **volgende** nadat u hello scheidingstekens bekijkt en een voorbeeld van gegevens.</span><span class="sxs-lookup"><span data-stu-id="0c76d-172">Click **Next** after you review hello delimiters and preview data.</span></span> 
   
    ![Hulpprogramma voor kopiëren - Bestandsindelingsinstellingen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="0c76d-174">Pagina op Hallo bestemming gegevens opslaan, selecteert u **Azure SQL Database**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-174">On hello Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Hulpprogramma voor kopiëren - Doelarchief kiezen](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="0c76d-176">Op **Geef hello Azure SQL database** pagina:</span><span class="sxs-lookup"><span data-stu-id="0c76d-176">On **Specify hello Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="0c76d-177">Voer **AzureSqlLinkedService** voor Hallo **verbindingsnaam** veld.</span><span class="sxs-lookup"><span data-stu-id="0c76d-177">Enter **AzureSqlLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="0c76d-178">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **Server-/databaseselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="0c76d-179">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="0c76d-180">Selecteer de **servernaam** en **database**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="0c76d-181">Voer de **gebruikersnaam** en het **wachtwoord** in.</span><span class="sxs-lookup"><span data-stu-id="0c76d-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="0c76d-182">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-182">Click **Next**.</span></span>  
      
      ![Hulpprogramma voor kopiëren - Azure SQL-database opgeven](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="0c76d-184">Op Hallo **tabeltoewijzing** pagina **emp** voor Hallo **bestemming** veld uit de vervolgkeuzelijst hello, klikt u op **pijl-omlaag** (optioneel) toosee hello schema en toopreview Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="0c76d-184">On hello **Table mapping** page, select **emp** for hello **Destination** field from hello drop-down list, click **down arrow** (optional) toosee hello schema and toopreview hello data.</span></span>
    
     ![Hulpprogramma voor kopiëren - Tabeltoewijzing](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="0c76d-186">Op Hallo **schematoewijzing** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-186">On hello **Schema mapping** page, click **Next**.</span></span>
    
    ![Hulpprogramma voor kopiëren - Schematoewijzing](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="0c76d-188">Op Hallo **prestatie-instellingen** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-188">On hello **Performance settings** page, click **Next**.</span></span> 
    
    ![Hulpprogramma voor kopiëren - Prestatie-instellingen](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="0c76d-190">Bekijk de informatie in Hallo **samenvatting** pagina en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="0c76d-190">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="0c76d-191">Hallo-wizard maakt twee gekoppelde services, twee gegevenssets (invoer en uitvoer) en één pijplijn in de gegevensfactory hello (van waaruit u Hallo Wizard kopiëren hebt gestart).</span><span class="sxs-lookup"><span data-stu-id="0c76d-191">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span> 
    
    ![Hulpprogramma voor kopiëren - Prestatie-instellingen](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="0c76d-193">Monitor starten en toepassing beheren</span><span class="sxs-lookup"><span data-stu-id="0c76d-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="0c76d-194">Op Hallo **implementatie** pagina, klikt u op de koppeling Hallo: `Click here toomonitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="0c76d-194">On hello **Deployment** page, click hello link: `Click here toomonitor copy pipeline`.</span></span>
   
   ![Hulpprogramma voor kopiëren - Implementeren voltooid](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="0c76d-196">Hallo monitoring-toepassing wordt gestart op een afzonderlijke tabblad in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="0c76d-196">hello monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![App voor bewaking](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="0c76d-198">toosee hello laatste status van elk uur segmenten, klikt u op **vernieuwen** knop in Hallo **ACTIVITEITSVENSTERS** lijst Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="0c76d-198">toosee hello latest status of hourly slices, click **Refresh** button in hello **ACTIVITY WINDOWS** list at hello bottom.</span></span> <span data-ttu-id="0c76d-199">Ziet u vijf activiteitsvensters gedurende vijf dagen tussen de begin- en eindtijden voor Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="0c76d-199">You see five activity windows for five days between start and end times for hello pipeline.</span></span> <span data-ttu-id="0c76d-200">Hallo-lijst niet automatisch wordt vernieuwd, zodat u mogelijk de moet tooclick, een paar keer voordat u alle Hallo activiteit windows hello status Ready heeft vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="0c76d-200">hello list is not automatically refreshed, so you may need tooclick Refresh a couple of times before you see all hello activity windows in hello Ready state.</span></span> 
4. <span data-ttu-id="0c76d-201">Selecteer een venster van de activiteit in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="0c76d-201">Select an activity window in hello list.</span></span> <span data-ttu-id="0c76d-202">Zie Hallo voor meer informatie over het Hallo **activiteit venster Explorer** op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="0c76d-202">See hello details about it in hello **Activity Window Explorer** on hello right.</span></span>

    ![Details van activiteitsvenster](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="0c76d-204">Merk op dat Hallo datums 11, 12, 13, 14 en 15 in groen, wat betekent dat Hallo dagelijkse uitvoer segmenten voor deze datums zijn al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c76d-204">Notice that hello dates 11, 12, 13, 14, and 15 are in green color, which means that hello daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="0c76d-205">U ook zien kleurcodering op Hallo pijplijn en uitvoergegevensset in de diagramweergave Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0c76d-205">You also see this color coding on hello pipeline and hello output dataset in hello diagram view.</span></span> <span data-ttu-id="0c76d-206">In de vorige stap Hallo, zoals u ziet dat twee segmenten zijn al gemaakt, een segment wordt verwerkt en hello twee andere toobe verwerkt wachten (gebaseerd op Hallo van kleurcodering).</span><span class="sxs-lookup"><span data-stu-id="0c76d-206">In hello previous step, notice that two slices have already been produced, one slice is currently being processed, and hello other two are waiting toobe processed (based on hello color coding).</span></span> 

    <span data-ttu-id="0c76d-207">Zie het artikel [Pijplijnen bewaken en beheren met behulp van de app voor bewaking](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="0c76d-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c76d-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c76d-208">Next steps</span></span>
<span data-ttu-id="0c76d-209">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="0c76d-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="0c76d-210">Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="0c76d-210">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="0c76d-211">Klik op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel voor meer informatie over de velden/eigenschappen die u in de wizard voor het kopiëren van een gegevensarchief Hallo ziet.</span><span class="sxs-lookup"><span data-stu-id="0c76d-211">For details about fields/properties that you see in hello copy wizard for a data store, click hello link for hello data store in hello table.</span></span> 
