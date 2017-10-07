---
title: aaaCreate gegevenspijplijnen met behulp van Azure .NET SDK | Microsoft Docs
description: Informatie over hoe tooprogrammatically maken, bewaken en beheren van Azure data factory's met behulp van de Data Factory-SDK.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="51392-103">Maken, bewaken en beheren van Azure data Factory met Azure Data Factory .NET SDK</span><span class="sxs-lookup"><span data-stu-id="51392-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="51392-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="51392-104">Overview</span></span>
<span data-ttu-id="51392-105">U kunt maken, bewaken en beheren van Azure data factory's programmatisch met behulp van Data Factory .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="51392-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="51392-106">Dit artikel bevat een overzicht die u kunt een voorbeeld .NET-consoletoepassing die wordt gemaakt en een gegevensfactory bewaakt toocreate volgen.</span><span class="sxs-lookup"><span data-stu-id="51392-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="51392-107">In dit artikel omvat niet alle Hallo .NET API van Data Factory.</span><span class="sxs-lookup"><span data-stu-id="51392-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="51392-108">Zie [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor uitgebreide documentatie over .NET API voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="51392-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="51392-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="51392-109">Prerequisites</span></span>
* <span data-ttu-id="51392-110">Visual Studio 2012 of 2013 of 2015</span><span class="sxs-lookup"><span data-stu-id="51392-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="51392-111">Download en installeer [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="51392-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="51392-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51392-112">Azure PowerShell.</span></span> <span data-ttu-id="51392-113">Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) artikel tooinstall Azure PowerShell op uw computer.</span><span class="sxs-lookup"><span data-stu-id="51392-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="51392-114">U Azure PowerShell toocreate een Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="51392-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="51392-115">Een toepassing maken in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51392-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="51392-116">Een Azure Active Directory-toepassing maken, een service-principal voor de toepassing hello maken en toewijzen toohello **Data Factory Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="51392-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="51392-117">Start **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="51392-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="51392-118">Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="51392-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="51392-119">Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="51392-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="51392-120">Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="51392-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="51392-121">Vervang  **&lt;NameOfAzureSubscription** &gt; met Hallo-naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="51392-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="51392-122">Noteer **SubscriptionId** en **TenantId** van Hallo-uitvoer van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="51392-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="51392-123">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht in PowerShell Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="51392-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="51392-124">Als de resourcegroep Hallo al bestaat, die u opgeeft of tooupdate deze (Y) of als (N).</span><span class="sxs-lookup"><span data-stu-id="51392-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="51392-125">Als u een andere resourcegroep gebruikt, moet u toouse Hallo-naam van de resourcegroep in plaats van ADFTutorialResourceGroup in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="51392-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="51392-126">Maak een Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="51392-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="51392-127">Als u krijgt de volgende fout hello, Geef een andere URL en voer de opdracht Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="51392-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="51392-128">Hallo AD-service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="51392-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="51392-129">Toevoegen van de service principal toohello **Data Factory Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="51392-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="51392-130">Ophalen van Hallo toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="51392-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="51392-131">Noteer Hallo toepassings-ID (applicationID) van Hallo-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="51392-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="51392-132">U moet na deze stappen beschikken over de volgende vier waarden:</span><span class="sxs-lookup"><span data-stu-id="51392-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="51392-133">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="51392-133">Tenant ID</span></span>
* <span data-ttu-id="51392-134">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="51392-134">Subscription ID</span></span>
* <span data-ttu-id="51392-135">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="51392-135">Application ID</span></span>
* <span data-ttu-id="51392-136">Wachtwoord (opgegeven in de eerste opdracht Hallo)</span><span class="sxs-lookup"><span data-stu-id="51392-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="51392-137">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="51392-137">Walkthrough</span></span>
<span data-ttu-id="51392-138">In Hallo scenario maakt u een gegevensfactory met een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="51392-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="51392-139">Hallo kopieeractiviteit gegevens worden gekopieerd vanuit een map in de map Azure blob storage tooanother van Hallo dezelfde blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="51392-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="51392-140">Hallo Kopieeractiviteit Hallo gegevensverplaatsing in Azure Data Factory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="51392-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="51392-141">Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="51392-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="51392-142">Zie [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over Hallo Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="51392-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="51392-143">Maak met behulp van Visual Studio 2012/2013/2015 een C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="51392-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="51392-144">Open **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="51392-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="51392-145">Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="51392-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="51392-146">Vouw **Templates** uit en selecteer **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="51392-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="51392-147">Tijdens deze walkthrough gebruikt u C#, maar u kunt een willekeurige .NET-taal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="51392-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="51392-148">Selecteer **consoletoepassing** uit de lijst Hallo van projecttypen op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="51392-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="51392-149">Voer **DataFactoryAPITestApp** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="51392-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="51392-150">Selecteer **C:\ADFGetStarted** voor Hallo locatie.</span><span class="sxs-lookup"><span data-stu-id="51392-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="51392-151">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="51392-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="51392-152">Klik op **extra**, wijst u te**NuGet Package Manager**, en klik op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="51392-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="51392-153">In Hallo **Package Manager Console**, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="51392-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="51392-154">Voer Hallo opdracht tooinstall Data Factory-pakket te volgen:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="51392-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="51392-155">Voer Hallo opdracht tooinstall Azure Active Directory-pakket (Active Directory-API in gebruikt Hallo code) te volgen:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="51392-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="51392-156">Vervang de inhoud Hallo van **App.config** bestand in Hallo-project met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="51392-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="51392-157">Waarden voor bijwerken in het bestand App.Config Hallo  **&lt;toepassings-ID&gt;**,  **&lt;wachtwoord&gt;**,  **&lt; Abonnements-ID&gt;**, en  **&lt;tenant-ID&gt;**  met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="51392-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="51392-158">Voeg de volgende Hallo **met** instructies toohello **Program.cs** bestand in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="51392-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="51392-159">Toevoegen na de code die u een exemplaar van maakt Hallo **DataPipelineManagementClient** klasse toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="51392-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="51392-160">U kunt dit object toocreate gebruiken een gegevensfactory, een gekoppelde service, invoer- en uitvoergegevenssets en een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="51392-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="51392-161">U kunt ook dit object toomonitor segmenten van een gegevensset gebruiken tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="51392-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="51392-162">Vervang de waarde Hallo van **resourceGroupName** met Hallo-naam van uw Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="51392-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="51392-163">Kunt u een resourcegroep met Hallo [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51392-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="51392-164">Naam van de data factory (dataFactoryName) toobe Hallo unieke bijwerken.</span><span class="sxs-lookup"><span data-stu-id="51392-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="51392-165">Naam van Hallo-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="51392-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="51392-166">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="51392-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="51392-167">Toevoegen Hallo code die wordt gemaakt na een **gegevensfactory** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="51392-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="51392-168">Toevoegen Hallo code die wordt gemaakt na een **gekoppelde Azure Storage-service** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="51392-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="51392-169">Vervang **storageaccountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="51392-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="51392-170">Hallo code die wordt gemaakt na toevoegen **invoer- en uitvoergegevenssets** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="51392-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="51392-171">Hallo **FolderPath** voor blob-invoerbron hello te is ingesteld**adftutorial /** waar **adftutorial** Hallo-naam van het Hallo-container in de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="51392-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="51392-172">Als deze container niet in de Azure blob-opslag bestaat, een container maken met deze naam: **adftutorial** en een container tekst bestand toohello te uploaden.</span><span class="sxs-lookup"><span data-stu-id="51392-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="51392-173">Hallo FolderPath voor Hallo uitvoer blob is ingesteld op: **adftutorial/apifactoryoutput / {segmenteren}** waar **segment** is dynamisch wordt berekend op basis van Hallo-waarde van **SliceStart**(en-tijd van elk segment starten).</span><span class="sxs-lookup"><span data-stu-id="51392-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="51392-174">Voeg Hallo volgende code die **wordt gemaakt en wordt geactiveerd op een pijplijn** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="51392-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="51392-175">Deze pijplijn heeft een **CopyActivity** die **BlobSource** als een bron neemt en **BlobSink** als een sink.</span><span class="sxs-lookup"><span data-stu-id="51392-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="51392-176">Hallo Kopieeractiviteit Hallo gegevensverplaatsing in Azure Data Factory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="51392-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="51392-177">Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="51392-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="51392-178">Zie [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over Hallo Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="51392-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="51392-179">Hallo na code toohello toevoegen **Main** methode tooget Hallo status van een gegevenssegment Hallo uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="51392-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="51392-180">Er is slechts één segment verwacht in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="51392-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="51392-181">**(optioneel)**  Toevoegen Hallo volgende code tooget Voer details voor een segment gegevens toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="51392-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="51392-182">Toevoegen van de volgende Help-methode die wordt gebruikt door Hallo Hallo **Main** methode toohello **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="51392-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="51392-183">Deze methode verschijnt een dialoogvenster waarmee u bieden **gebruikersnaam** en **wachtwoord** toolog in tooAzure portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="51392-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="51392-184">Vouw in Solution Explorer hello, Hallo project: **DataFactoryAPITestApp**, met de rechtermuisknop op **verwijzingen**, en klik op **verwijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="51392-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="51392-185">Schakel dit selectievakje in voor `System.Configuration` assembly en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="51392-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="51392-186">Hallo-consoletoepassing bouwen.</span><span class="sxs-lookup"><span data-stu-id="51392-186">Build hello console application.</span></span> <span data-ttu-id="51392-187">Klik op **bouwen** op en klik op Hallo **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="51392-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="51392-188">Controleer of er ten minste één bestand in Hallo adftutorial container in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="51392-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="51392-189">Als dat niet het geval is, maak Emp.txt-bestand in Kladblok met Hallo na inhoud en toohello adftutorial container te uploaden.</span><span class="sxs-lookup"><span data-stu-id="51392-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="51392-190">Hallo-voorbeeld uitvoeren door te klikken op **Debug** -> **foutopsporing starten** Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="51392-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="51392-191">Wanneer er Hallo **details van een gegevenssegment ophalen uitvoeren**, wacht een paar minuten en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="51392-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="51392-192">Gebruik hello Azure portal tooverify die gegevensfactory hello **APITutorialFactory** wordt gemaakt met de Hallo artefacten te volgen:</span><span class="sxs-lookup"><span data-stu-id="51392-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="51392-193">Gekoppelde service: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="51392-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="51392-194">Gegevensset: **DatasetBlobSource** en **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="51392-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="51392-195">Pijplijn: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="51392-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="51392-196">Controleren of een bestand voor uitvoer is gemaakt in Hallo **apifactoryoutput** map in Hallo **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="51392-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="51392-197">Een lijst met mislukte gegevenssegmenten ophalen</span><span class="sxs-lookup"><span data-stu-id="51392-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="51392-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51392-198">Next steps</span></span>
<span data-ttu-id="51392-199">Zie Hallo voorbeeld voor het maken van een pijplijn met .NET SDK waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database te volgen:</span><span class="sxs-lookup"><span data-stu-id="51392-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="51392-200">Een pijplijn toocopy gegevens uit Blob Storage tooSQL Database maken</span><span class="sxs-lookup"><span data-stu-id="51392-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
