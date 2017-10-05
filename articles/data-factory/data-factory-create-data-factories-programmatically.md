---
title: Gegevenspijplijnen maken met behulp van Azure .NET SDK | Microsoft Docs
description: Informatie over het programmatisch maken, bewaken en beheren van Azure data factory's met behulp van de Data Factory-SDK.
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
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="99acc-103">Maken, bewaken en beheren van Azure data Factory met Azure Data Factory .NET SDK</span><span class="sxs-lookup"><span data-stu-id="99acc-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="99acc-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="99acc-104">Overview</span></span>
<span data-ttu-id="99acc-105">U kunt maken, bewaken en beheren van Azure data factory's programmatisch met behulp van Data Factory .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="99acc-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="99acc-106">Dit artikel bevat een overzicht die u volgen kunt om een .NET-console voorbeeldtoepassing die u maakt en bewaakt een gegevensfactory maken.</span><span class="sxs-lookup"><span data-stu-id="99acc-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="99acc-107">Dit artikel behandelt niet de volledige Data Factory .NET API.</span><span class="sxs-lookup"><span data-stu-id="99acc-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="99acc-108">Zie [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor uitgebreide documentatie over .NET API voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="99acc-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="99acc-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="99acc-109">Prerequisites</span></span>
* <span data-ttu-id="99acc-110">Visual Studio 2012 of 2013 of 2015</span><span class="sxs-lookup"><span data-stu-id="99acc-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="99acc-111">Download en installeer [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="99acc-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="99acc-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99acc-112">Azure PowerShell.</span></span> <span data-ttu-id="99acc-113">Volg de instructies in [Azure PowerShell installeren en configureren](/powershell/azure/overview) om Azure PowerShell te installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="99acc-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="99acc-114">Azure PowerShell wordt gebruikt om een Azure Active Directory-toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="99acc-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="99acc-115">Een toepassing maken in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99acc-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="99acc-116">Maak een Azure Active Directory-toepassing, maak een service-principal voor de toepassing en wijs deze toe aan de rol **Inzender Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="99acc-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="99acc-117">Start **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="99acc-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="99acc-118">Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="99acc-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="99acc-119">Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="99acc-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="99acc-120">Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="99acc-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="99acc-121">Vervang **&lt;NameOfAzureSubscription**&gt; door de naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="99acc-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="99acc-122">Noteer de **SubscriptionId** en de **TenantId** uit de uitvoer van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="99acc-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="99acc-123">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door de volgende opdracht uit te voeren in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="99acc-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="99acc-124">Als de resourcegroep al bestaat, geeft u aan of u deze wilt bijwerken (Y) of ongewijzigd wilt laten (N).</span><span class="sxs-lookup"><span data-stu-id="99acc-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="99acc-125">Als u een andere resourcegroep gebruikt, moet u voor deze zelfstudie de naam van uw resourcegroep gebruiken in plaats van ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="99acc-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="99acc-126">Maak een Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="99acc-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="99acc-127">Als u de volgende fout ziet, geeft u een andere URL op en voert u de opdracht opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="99acc-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="99acc-128">Maak de AD-service-principal.</span><span class="sxs-lookup"><span data-stu-id="99acc-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="99acc-129">Voeg de service-principal toe aan de rol **Inzender Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="99acc-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="99acc-130">Haal de toepassings-id op.</span><span class="sxs-lookup"><span data-stu-id="99acc-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="99acc-131">Noteer de toepassings-id (applicationID in de uitvoer).</span><span class="sxs-lookup"><span data-stu-id="99acc-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="99acc-132">U moet na deze stappen beschikken over de volgende vier waarden:</span><span class="sxs-lookup"><span data-stu-id="99acc-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="99acc-133">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="99acc-133">Tenant ID</span></span>
* <span data-ttu-id="99acc-134">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="99acc-134">Subscription ID</span></span>
* <span data-ttu-id="99acc-135">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="99acc-135">Application ID</span></span>
* <span data-ttu-id="99acc-136">Wachtwoord (opgegeven in de eerste opdracht)</span><span class="sxs-lookup"><span data-stu-id="99acc-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="99acc-137">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="99acc-137">Walkthrough</span></span>
<span data-ttu-id="99acc-138">In dit overzicht kunt u een gegevensfactory maken met een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="99acc-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="99acc-139">De kopieeractiviteit kopieert gegevens van een map in de Azure blob-opslag naar een andere map in dezelfde blob storage.</span><span class="sxs-lookup"><span data-stu-id="99acc-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="99acc-140">Met de kopieeractiviteit wordt de gegevensverplaatsing in Azure Data Factory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99acc-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="99acc-141">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="99acc-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="99acc-142">Zie [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="99acc-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="99acc-143">Maak met behulp van Visual Studio 2012/2013/2015 een C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="99acc-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="99acc-144">Open **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="99acc-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="99acc-145">Klik op **File**, houd de muisaanwijzer op **New** en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="99acc-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="99acc-146">Vouw **Templates** uit en selecteer **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="99acc-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="99acc-147">Tijdens deze walkthrough gebruikt u C#, maar u kunt een willekeurige .NET-taal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="99acc-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="99acc-148">Selecteer **Console Application** uit de lijst met projecttypen aan de rechterkant.</span><span class="sxs-lookup"><span data-stu-id="99acc-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="99acc-149">Voer **DataFactoryAPITestApp** in als de naam.</span><span class="sxs-lookup"><span data-stu-id="99acc-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="99acc-150">Selecteer **C:\ADFGetStarted** als de locatie.</span><span class="sxs-lookup"><span data-stu-id="99acc-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="99acc-151">Klik op **OK** om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="99acc-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="99acc-152">Klik op **Tools**, wijs **NuGet Package Manager** aan en klik op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="99acc-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="99acc-153">Voer de volgende stappen uit in de **Package Manager Console**:</span><span class="sxs-lookup"><span data-stu-id="99acc-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="99acc-154">Voer de volgende opdracht uit om het Data Factory-pakket te installeren: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="99acc-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="99acc-155">Voer de volgende opdracht uit om het Azure Active Directory-pakket te installeren (u gebruikt de Active Directory API in de code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="99acc-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="99acc-156">Vervang de inhoud van **App.config** bestand in het project met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="99acc-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="99acc-157">Waarden voor bijwerken in het bestand App.Config  **&lt;toepassings-ID&gt;**,  **&lt;wachtwoord&gt;**,  **&lt;abonnement ID&gt;**, en  **&lt;tenant-ID&gt;**  met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="99acc-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="99acc-158">Voeg de volgende **met** instructies voor het **Program.cs** bestand in het project.</span><span class="sxs-lookup"><span data-stu-id="99acc-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

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
6. <span data-ttu-id="99acc-159">Voeg de volgende code toe aan de methode **Main** om een instantie van de klasse **DataPipelineManagementClient** te maken.
</span><span class="sxs-lookup"><span data-stu-id="99acc-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="99acc-160">U gebruikt dit object om een gegevensfactory, een gekoppelde service, gegevenssets voor invoer en uitvoer, en een pijplijn te maken.</span><span class="sxs-lookup"><span data-stu-id="99acc-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="99acc-161">U gebruikt dit object ook om segmenten van een gegevensset te bewaken tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="99acc-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="99acc-162">Vervang de waarde van **resourceGroupName** door de naam van uw Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="99acc-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="99acc-163">U kunt maken met een resource-groep met de [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="99acc-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="99acc-164">Werk de naam van de data factory (dataFactoryName) zodanig bij dat deze uniek is.</span><span class="sxs-lookup"><span data-stu-id="99acc-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="99acc-165">De naam van de gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="99acc-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="99acc-166">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="99acc-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="99acc-167">Voeg de volgende code die een **gegevensfactory** maakt toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="99acc-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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
8. <span data-ttu-id="99acc-168">Voeg de volgende code die een **gekoppelde Azure Storage-service** maakt toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="99acc-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="99acc-169">Vervang **storageaccountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="99acc-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="99acc-170">Voeg de volgende code die **gegevenssets voor invoer en uitvoer** maakt toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="99acc-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="99acc-171">De **FolderPath** voor de blob-invoerbron is ingesteld op **adftutorial /** waar **adftutorial** is de naam van de container in de blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="99acc-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="99acc-172">Als deze container niet in de Azure blob-opslag bestaat, een container maken met deze naam: **adftutorial** en een tekstbestand te uploaden naar de container.</span><span class="sxs-lookup"><span data-stu-id="99acc-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="99acc-173">Het mappad voor de uitvoer-blob is ingesteld op: **adftutorial/apifactoryoutput / {segmenteren}** waar **segment** dynamisch wordt berekend op basis van de waarde van **SliceStart** () datum / tijd van elk segment starten).</span><span class="sxs-lookup"><span data-stu-id="99acc-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="99acc-174">Voeg de volgende code die **een pijplijn maakt en activeert** toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="99acc-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="99acc-175">Deze pijplijn heeft een **CopyActivity** die **BlobSource** als een bron neemt en **BlobSink** als een sink.</span><span class="sxs-lookup"><span data-stu-id="99acc-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="99acc-176">Met de kopieeractiviteit wordt de gegevensverplaatsing in Azure Data Factory uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99acc-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="99acc-177">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="99acc-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="99acc-178">Zie [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="99acc-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

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
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
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
12. <span data-ttu-id="99acc-179">Voeg de volgende code toe aan de methode **Main** om de status van een gegevenssegment van de uitvoergegevensset te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="99acc-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="99acc-180">Er is slechts één segment verwacht in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="99acc-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
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
13. <span data-ttu-id="99acc-181">**(optioneel)**  Voeg de volgende code als u wilt ophalen uitvoeren details voor een gegevenssegment naar de **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="99acc-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
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
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="99acc-182">Voeg de volgende Help-methode toe die door de methode **Main** wordt gebruikt voor de klasse **Program**.</span><span class="sxs-lookup"><span data-stu-id="99acc-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="99acc-183">Deze methode verschijnt een dialoogvenster waarmee u bieden **gebruikersnaam** en **wachtwoord** die u gebruikt voor aanmelding bij Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="99acc-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

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

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="99acc-184">Vouw het project in Solution Explorer: **DataFactoryAPITestApp**, met de rechtermuisknop op **verwijzingen**, en klik op **verwijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="99acc-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="99acc-185">Schakel dit selectievakje in voor `System.Configuration` assembly en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="99acc-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="99acc-186">Bouw de consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="99acc-186">Build the console application.</span></span> <span data-ttu-id="99acc-187">Klik op **Build** in het menu en klik op **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="99acc-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="99acc-188">Controleer of er ten minste één bestand in de container adftutorial in uw Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="99acc-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="99acc-189">Als dit niet het geval is, Emp.txt-bestand in Kladblok met de volgende inhoud maken en uploaden naar de container adftutorial.</span><span class="sxs-lookup"><span data-stu-id="99acc-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="99acc-190">Voer het voorbeeld uit door op **Debug** -> **Start Debugging** te klikken in het menu.</span><span class="sxs-lookup"><span data-stu-id="99acc-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="99acc-191">Als u **Getting run details of a data slice** ziet, wacht u een paar minuten en drukt u op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="99acc-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="99acc-192">Gebruik Azure Portal om te controleren of de gegevensfactory **APITutorialFactory** wordt gemaakt met de volgende artefacten:</span><span class="sxs-lookup"><span data-stu-id="99acc-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="99acc-193">Gekoppelde service: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="99acc-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="99acc-194">Gegevensset: **DatasetBlobSource** en **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="99acc-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="99acc-195">Pijplijn: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="99acc-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="99acc-196">Controleren of een bestand voor uitvoer is gemaakt de **apifactoryoutput** map in de **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="99acc-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="99acc-197">Een lijst met mislukte gegevenssegmenten ophalen</span><span class="sxs-lookup"><span data-stu-id="99acc-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
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

## <a name="next-steps"></a><span data-ttu-id="99acc-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99acc-198">Next steps</span></span>
<span data-ttu-id="99acc-199">Zie het volgende voorbeeld voor het maken van een pijplijn met .NET SDK waarmee gegevens worden gekopieerd van een Azure blob-opslag met een Azure SQL database:</span><span class="sxs-lookup"><span data-stu-id="99acc-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="99acc-200">Een pijplijn om gegevens te kopiëren van Blob-opslag met SQL-Database maken</span><span class="sxs-lookup"><span data-stu-id="99acc-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
