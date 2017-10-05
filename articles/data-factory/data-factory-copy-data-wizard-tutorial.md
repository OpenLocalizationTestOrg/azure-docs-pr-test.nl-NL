---
title: "Zelfstudie: een pijplijn maken met de wizard Kopiëren | Microsoft Docs"
description: "In deze zelfstudie maakt u een Azure Data Factory-pijplijn met een kopieeractiviteit. Hiervoor gebruikt u de wizard Kopiëren die wordt ondersteund door Data Factory."
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
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="9be1b-103">Zelfstudie: een pijplijn maken met de kopieeractiviteit middels de Data Factory-wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="9be1b-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9be1b-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="9be1b-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="9be1b-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="9be1b-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="9be1b-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9be1b-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="9be1b-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9be1b-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="9be1b-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9be1b-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="9be1b-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="9be1b-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="9be1b-110">REST API</span><span class="sxs-lookup"><span data-stu-id="9be1b-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="9be1b-111">.NET-API</span><span class="sxs-lookup"><span data-stu-id="9be1b-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="9be1b-112">Deze zelfstudie laat zien hoe u de **Wizard Kopiëren** kunt gebruiken om gegevens uit een Azure Blob-opslag te kopiëren naar een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="9be1b-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="9be1b-113">Met de **Wizard Kopiëren** van Azure Data Factory maakt u snel een gegevenspijplijn waarmee u gegevens uit een ondersteund brongegevensarchief kunt kopiëren naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="9be1b-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="9be1b-114">Daarom wordt u aangeraden de wizard te gebruiken als eerste stap bij het maken van een voorbeeldpijplijn voor uw gegevensverplaatsingsscenario.</span><span class="sxs-lookup"><span data-stu-id="9be1b-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="9be1b-115">Zie [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als doel.</span><span class="sxs-lookup"><span data-stu-id="9be1b-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="9be1b-116">Deze zelfstudie laat zien hoe u een Azure-gegevensfactory kunt maken, de wizard Kopiëren kunt starten en een reeks stappen kunt uitvoeren om informatie over uw scenario voor gegevensopname/-verplaatsing op te geven.</span><span class="sxs-lookup"><span data-stu-id="9be1b-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="9be1b-117">Nadat u de stappen in de wizard hebt voltooid, maakt de wizard automatisch een pijplijn met een kopieeractiviteit om gegevens te kopiëren uit een Azure Blob-opslag naar Azure SQL-databases.</span><span class="sxs-lookup"><span data-stu-id="9be1b-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="9be1b-118">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="9be1b-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9be1b-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9be1b-119">Prerequisites</span></span>
<span data-ttu-id="9be1b-120">U dient eerst te voldoen aan de vereisten in het artikel [Overzicht van de zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voordat u deze zelfstudie volgt.</span><span class="sxs-lookup"><span data-stu-id="9be1b-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="9be1b-121">Een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="9be1b-121">Create data factory</span></span>
<span data-ttu-id="9be1b-122">In deze stap gebruikt u Azure Portal om een Azure Data Factory met de naam **ADFTutorialDataFactory** te maken.</span><span class="sxs-lookup"><span data-stu-id="9be1b-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="9be1b-123">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9be1b-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9be1b-124">Klik in het linkermenu op **+ NIEUW**, klik op **Gegevens + analyse** en **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Nieuw -> DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="9be1b-126">In de blade **Nieuwe gegevensfactory**:</span><span class="sxs-lookup"><span data-stu-id="9be1b-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="9be1b-127">Voer **ADFTutorialDataFactory** in als **naam**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="9be1b-128">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="9be1b-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="9be1b-129">Als dit foutbericht wordt geretourneerd: `Data factory name “ADFTutorialDataFactory” is not available`, wijzigt u de naam van de gegevensfactory (bijvoorbeeld uwnaamADFTutorialDataFactoryDDMMJJJJ) en maakt een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="9be1b-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="9be1b-130">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="9be1b-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Naam van gegevensfactory niet beschikbaar](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="9be1b-132">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="9be1b-133">Voer een van de volgende stappen uit voor de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="9be1b-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="9be1b-134">Selecteer **Bestaande gebruiken** om een bestaande resourcegroep te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9be1b-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="9be1b-135">Selecteer **Nieuwe maken** als u een naam voor een resourcegroep wilt typen.</span><span class="sxs-lookup"><span data-stu-id="9be1b-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="9be1b-136">Voor sommige van de stappen in deze zelfstudie wordt ervan uitgegaan dat u voor de resourcegroep de naam **ADFTutorialResourceGroup** gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9be1b-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="9be1b-137">Zie [Resourcegroepen gebruiken om Azure-resources te beheren](../azure-resource-manager/resource-group-overview.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9be1b-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="9be1b-138">Selecteer een **locatie** voor de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="9be1b-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="9be1b-139">Selecteer het selectievakje **Vastmaken aan dashboard** onderaan de blade.</span><span class="sxs-lookup"><span data-stu-id="9be1b-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="9be1b-140">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-140">Click **Create**.</span></span>
      
       ![Blade voor een nieuwe gegevensfactory](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="9be1b-142">Wanneer het aanmaken is voltooid, ziet u de blade **Gegevensfactory** zoals op de volgende afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9be1b-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Startpagina van de gegevensfactory](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="9be1b-144">De wizard Kopiëren starten</span><span class="sxs-lookup"><span data-stu-id="9be1b-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="9be1b-145">Klik op de blade Gegevensfactory op **Gegevens kopiëren [PREVIEW]** om de **wizard Kopiëren** te starten.</span><span class="sxs-lookup"><span data-stu-id="9be1b-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="9be1b-146">Als u ziet dat de webbrowser is vastgelopen bij Autoriseren..., schakelt u **Cookies van derden en sitegegevens blokkeren** in de browserinstellingen uit. U kunt deze instelling ook ingeschakeld laten en een uitzondering maken voor **login.microsoftonline.com**. Open de wizard vervolgens opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9be1b-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="9be1b-147">Op de pagina **Eigenschappen**:</span><span class="sxs-lookup"><span data-stu-id="9be1b-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="9be1b-148">Voer **CopyFromBlobToAzureSql** in als **taaknaam**</span><span class="sxs-lookup"><span data-stu-id="9be1b-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="9be1b-149">Voer de **beschrijving** in (optioneel).</span><span class="sxs-lookup"><span data-stu-id="9be1b-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="9be1b-150">Wijzig de **Startdatum en -tijd** en de **Einddatum en -tijd** zodat de einddatum is ingesteld op vandaag en de startdatum op vijf dagen eerder.</span><span class="sxs-lookup"><span data-stu-id="9be1b-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="9be1b-151">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-151">Click **Next**.</span></span>  
      
      ![Hulpprogramma voor kopiëren - pagina Eigenschappen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="9be1b-153">Op de pagina **Brongegevensarchief** klikt u op de tegel **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="9be1b-154">U gebruikt deze pagina om het brongegevensarchief op te geven voor de kopieertaak.</span><span class="sxs-lookup"><span data-stu-id="9be1b-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![Hulpprogramma voor kopiëren - pagina van brongegevensarchief](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="9be1b-156">Op de pagina **Het Azure Blob Storage-account opgeven**:</span><span class="sxs-lookup"><span data-stu-id="9be1b-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="9be1b-157">Voer **AzureStorageLinkedService** in als **naam van de gekoppelde service**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="9be1b-158">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="9be1b-159">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="9be1b-160">Selecteer een **Azure-opslagaccount** uit de lijst met Azure-opslagaccounts die beschikbaar is voor het abonnement dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9be1b-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="9be1b-161">U kunt er ook voor kiezen om de opslagaccountinstellingen handmatig op te geven. Selecteer daarvoor de optie **Handmatig invoeren** als **accountselectiemethode** en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Hulpprogramma voor kopiëren - Het Azure Blob Storage-account opgeven](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="9be1b-163">Op de pagina **Het invoerbestand of de invoermap kiezen**:</span><span class="sxs-lookup"><span data-stu-id="9be1b-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="9be1b-164">Dubbelklik op **adftutorial** (map).</span><span class="sxs-lookup"><span data-stu-id="9be1b-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="9be1b-165">Selecteer **emp.txt** en klik op **Kiezen**</span><span class="sxs-lookup"><span data-stu-id="9be1b-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Hulpprogramma voor kopiëren - Het invoerbestand of de invoermap kiezen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="9be1b-167">Klik op de pagina **Het invoerbestand of de invoermap kiezen** op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="9be1b-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="9be1b-168">Selecteer niet **Binaire kopie**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-168">Do not select **Binary copy**.</span></span> 
   
    ![Hulpprogramma voor kopiëren - Het invoerbestand of de invoermap kiezen](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="9be1b-170">Op de pagina **Bestandsinstellingen** ziet u de scheidingstekens en het schema dat automatisch is gedetecteerd door de wizard tijdens het parseren van het bestand.</span><span class="sxs-lookup"><span data-stu-id="9be1b-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="9be1b-171">U kunt de scheidingstekens ook handmatig invoeren zodat de wizard Kopiëren stopt met automatisch detecteren, of als u wilt dat gegevens worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="9be1b-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="9be1b-172">Klik op **Volgende** nadat u de scheidingstekens hebt gecontroleerd en een voorbeeld van de gegevens hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="9be1b-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Hulpprogramma voor kopiëren - Bestandsindelingsinstellingen](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="9be1b-174">Op de pagina Doelgegevensarchief selecteert u **Azure SQL Database** en klikt u op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Hulpprogramma voor kopiëren - Doelarchief kiezen](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="9be1b-176">Op de pagina **De Azure SQL Database opgeven**:</span><span class="sxs-lookup"><span data-stu-id="9be1b-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="9be1b-177">Typ **AzureSqlLinkedService** in het veld **Verbindingsnaam**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="9be1b-178">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **Server-/databaseselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="9be1b-179">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="9be1b-180">Selecteer de **servernaam** en **database**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="9be1b-181">Voer de **gebruikersnaam** en het **wachtwoord** in.</span><span class="sxs-lookup"><span data-stu-id="9be1b-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="9be1b-182">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-182">Click **Next**.</span></span>  
      
      ![Hulpprogramma voor kopiëren - Azure SQL-database opgeven](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="9be1b-184">Op de pagina **Tabeltoewijzing** selecteert u uit de vervolgkeuzelijst **emp** in het veld **Bestemming** en klikt u op de **pijl naar beneden** (optioneel) om het schema en een voorbeeld van de gegevens te bekijken.</span><span class="sxs-lookup"><span data-stu-id="9be1b-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Hulpprogramma voor kopiëren - Tabeltoewijzing](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="9be1b-186">Op de pagina **Schematoewijzing** klikt u op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Hulpprogramma voor kopiëren - Schematoewijzing](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="9be1b-188">Op de pagina **Prestatie-instellingen** klikt u op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Hulpprogramma voor kopiëren - Prestatie-instellingen](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="9be1b-190">Lees de informatie op de pagina **Samenvatting** en klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="9be1b-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="9be1b-191">De wizard maakt twee gekoppelde services, twee gegevenssets (invoer en uitvoer) en één pijplijn in de gegevensfactory (van waaruit u de wizard Kopiëren hebt gestart).</span><span class="sxs-lookup"><span data-stu-id="9be1b-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Hulpprogramma voor kopiëren - Prestatie-instellingen](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="9be1b-193">Monitor starten en toepassing beheren</span><span class="sxs-lookup"><span data-stu-id="9be1b-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="9be1b-194">Klik op de pagina **Implementatie** op de koppeling: `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="9be1b-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Hulpprogramma voor kopiëren - Implementeren voltooid](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="9be1b-196">De bewakingstoepassing wordt gestart op een afzonderlijk tabblad in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="9be1b-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![App voor bewaking](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="9be1b-198">Klik op de knop **Vernieuwen** in de lijst **ACTIVITEITSVENSTERS** onderaan om de meest recente status van uursegmenten te zien.</span><span class="sxs-lookup"><span data-stu-id="9be1b-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="9be1b-199">U ziet vijf activiteitsvensters voor vijf dagen tussen de start- en eindtijd voor de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="9be1b-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="9be1b-200">De lijst wordt niet automatisch vernieuwd. Het kan dus zijn dat u een paar keer op Vernieuwen moet klikken om alle activiteitsvensters weer te geven met de status Gereed.</span><span class="sxs-lookup"><span data-stu-id="9be1b-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="9be1b-201">Selecteer een activiteitsvenster in de lijst.</span><span class="sxs-lookup"><span data-stu-id="9be1b-201">Select an activity window in the list.</span></span> <span data-ttu-id="9be1b-202">Bekijk de details hierover deze in de **Activiteitsvensterverkenner** aan de rechterkant.</span><span class="sxs-lookup"><span data-stu-id="9be1b-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![Details van activiteitsvenster](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="9be1b-204">Let op: de datums 11, 12, 13, 14 en 15 hebben een groene kleur. Dit betekent dat de dagelijkse uitvoersegmenten voor deze datums al zijn geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="9be1b-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="9be1b-205">U ziet deze kleurcodering ook bij de pijplijn en de uitvoergegevensset in de diagramweergave.</span><span class="sxs-lookup"><span data-stu-id="9be1b-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="9be1b-206">U ziet (op basis van de kleurcodering) dat in de vorige stap al twee segmenten zijn gemaakt, dat één segment momenteel wordt verwerkt en dat de andere twee segmenten wachten op verwerking.</span><span class="sxs-lookup"><span data-stu-id="9be1b-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="9be1b-207">Zie het artikel [Pijplijnen bewaken en beheren met behulp van de app voor bewaking](data-factory-monitor-manage-app.md) voor meer informatie over het gebruik van deze toepassing.</span><span class="sxs-lookup"><span data-stu-id="9be1b-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9be1b-208">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9be1b-208">Next steps</span></span>
<span data-ttu-id="9be1b-209">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="9be1b-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="9be1b-210">De volgende tabel bevat een lijst met gegevensarchieven die worden ondersteund als bron en doel voor de kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="9be1b-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="9be1b-211">Klik voor details over velden/eigenschappen die u ziet in de wizard Kopiëren voor een gegevensarchief, in de tabel op de koppeling voor dit gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="9be1b-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 