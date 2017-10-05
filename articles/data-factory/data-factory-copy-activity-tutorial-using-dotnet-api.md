---
title: 'Zelfstudie: een pijplijn maken met Copy Activity in .NET API | Microsoft Docs'
description: In deze zelfstudie maakt u een Azure Data Factory-pijplijn met Copy Activity. Hiervoor gebruikt u .NET API.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 30c7cd1ba455d7b1bc93d76e7ee79455bb52aae9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="a1658-103">Zelfstudie: een pijplijn maken met de kopieeractiviteit in .NET API</span><span class="sxs-lookup"><span data-stu-id="a1658-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a1658-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="a1658-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="a1658-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="a1658-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="a1658-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a1658-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="a1658-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1658-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="a1658-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1658-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="a1658-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="a1658-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="a1658-110">REST API</span><span class="sxs-lookup"><span data-stu-id="a1658-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="a1658-111">.NET-API</span><span class="sxs-lookup"><span data-stu-id="a1658-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="a1658-112">In dit artikel leert u hoe u [.NET API](https://portal.azure.com) kunt gebruiken om een gegevensfactory te maken met een pijplijn waarmee gegevens worden gekopieerd van een Azure blobopslag naar een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="a1658-112">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="a1658-113">Als u niet bekend bent met Azure Data Factory, lees dan het artikel [Inleiding tot Azure Data Factory](data-factory-introduction.md) voordat u deze zelfstudie volgt.</span><span class="sxs-lookup"><span data-stu-id="a1658-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="a1658-114">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="a1658-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="a1658-115">De kopieeractiviteit in Data Factory kopieert gegevens uit een ondersteund gegevensarchief naar een ondersteund sinkgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a1658-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="a1658-116">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="a1658-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="a1658-117">De activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens veilig, betrouwbaar en schaalbaar kunnen worden gekopieerd tussen verschillende gegevensarchieven.</span><span class="sxs-lookup"><span data-stu-id="a1658-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="a1658-118">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="a1658-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="a1658-119">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="a1658-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="a1658-120">Ook kunt u twee activiteiten koppelen (de ene activiteit na de andere laten uitvoeren) door de uitvoergegevensset van één activiteit in te stellen als invoergegevensset voor een andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="a1658-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="a1658-121">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a1658-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="a1658-122">Zie [Naslaginformatie over de .NET API voor Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor volledige documentatie over .NET API voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a1658-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="a1658-123">In de gegevenspijplijn in deze zelfstudie worden gegevens van een brongegevensarchief gekopieerd naar een doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a1658-123">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="a1658-124">Zie [Zelfstudie: een pijplijn maken om gegevens te transformeren met een Hadoop-cluster](data-factory-build-your-first-pipeline.md) voor meer informatie over het transformeren van gegevens met Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a1658-124">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1658-125">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a1658-125">Prerequisites</span></span>
* <span data-ttu-id="a1658-126">Neem [Overzicht van de zelfstudie en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) door voor een overzicht van de zelfstudie en voer de **vereiste** stappen uit.</span><span class="sxs-lookup"><span data-stu-id="a1658-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="a1658-127">Visual Studio 2012 of 2013 of 2015</span><span class="sxs-lookup"><span data-stu-id="a1658-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="a1658-128">Download en installeer [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="a1658-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="a1658-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1658-129">Azure PowerShell.</span></span> <span data-ttu-id="a1658-130">Volg de instructies in [Azure PowerShell installeren en configureren](../powershell-install-configure.md) om Azure PowerShell te installeren op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a1658-130">Follow instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="a1658-131">Azure PowerShell wordt gebruikt om een Azure Active Directory-toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="a1658-131">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="a1658-132">Een toepassing maken in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a1658-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="a1658-133">Maak een Azure Active Directory-toepassing, maak een service-principal voor de toepassing en wijs deze toe aan de rol **Inzender Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="a1658-133">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="a1658-134">Start **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="a1658-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="a1658-135">Voer de volgende opdracht uit en geef de gebruikersnaam en het wachtwoord op waarmee u zich aanmeldt bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1658-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="a1658-136">Voer de volgende opdracht uit om alle abonnementen voor dit account weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a1658-136">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="a1658-137">Voer de volgende opdracht uit om het abonnement te selecteren waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="a1658-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="a1658-138">Vervang **&lt;NameOfAzureSubscription**&gt; door de naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a1658-138">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a1658-139">Noteer de **SubscriptionId** en de **TenantId** uit de uitvoer van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="a1658-139">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="a1658-140">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door de volgende opdracht uit te voeren in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1658-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="a1658-141">Als de resourcegroep al bestaat, geeft u aan of u deze wilt bijwerken (Y) of ongewijzigd wilt laten (N).</span><span class="sxs-lookup"><span data-stu-id="a1658-141">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="a1658-142">Als u een andere resourcegroep gebruikt, moet u voor deze zelfstudie de naam van uw resourcegroep gebruiken in plaats van ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="a1658-142">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="a1658-143">Maak een Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a1658-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="a1658-144">Als u de volgende fout ziet, geeft u een andere URL op en voert u de opdracht opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="a1658-144">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="a1658-145">Maak de AD-service-principal.</span><span class="sxs-lookup"><span data-stu-id="a1658-145">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="a1658-146">Voeg de service-principal toe aan de rol **Inzender Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="a1658-146">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="a1658-147">Haal de toepassings-id op.</span><span class="sxs-lookup"><span data-stu-id="a1658-147">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="a1658-148">Noteer de toepassings-id (applicationID in de uitvoer).</span><span class="sxs-lookup"><span data-stu-id="a1658-148">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="a1658-149">U moet na deze stappen beschikken over de volgende vier waarden:</span><span class="sxs-lookup"><span data-stu-id="a1658-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="a1658-150">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="a1658-150">Tenant ID</span></span>
* <span data-ttu-id="a1658-151">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="a1658-151">Subscription ID</span></span>
* <span data-ttu-id="a1658-152">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="a1658-152">Application ID</span></span>
* <span data-ttu-id="a1658-153">Wachtwoord (opgegeven in de eerste opdracht)</span><span class="sxs-lookup"><span data-stu-id="a1658-153">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="a1658-154">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="a1658-154">Walkthrough</span></span>
1. <span data-ttu-id="a1658-155">Maak met behulp van Visual Studio 2012/2013/2015 een C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="a1658-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="a1658-156">Open **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="a1658-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="a1658-157">Klik op **File**, houd de muisaanwijzer op **New** en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="a1658-157">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="a1658-158">Vouw **Templates** uit en selecteer **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="a1658-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="a1658-159">Tijdens deze walkthrough gebruikt u C#, maar u kunt een willekeurige .NET-taal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1658-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="a1658-160">Selecteer **Console Application** uit de lijst met projecttypen aan de rechterkant.</span><span class="sxs-lookup"><span data-stu-id="a1658-160">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="a1658-161">Voer **DataFactoryAPITestApp** in als de naam.</span><span class="sxs-lookup"><span data-stu-id="a1658-161">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="a1658-162">Selecteer **C:\ADFGetStarted** als de locatie.</span><span class="sxs-lookup"><span data-stu-id="a1658-162">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="a1658-163">Klik op **OK** om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="a1658-163">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="a1658-164">Klik op **Tools**, wijs **NuGet Package Manager** aan en klik op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="a1658-164">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="a1658-165">Voer de volgende stappen uit in de **Package Manager Console**:</span><span class="sxs-lookup"><span data-stu-id="a1658-165">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="a1658-166">Voer de volgende opdracht uit om het Data Factory-pakket te installeren: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="a1658-166">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="a1658-167">Voer de volgende opdracht uit om het Azure Active Directory-pakket te installeren (u gebruikt de Active Directory API in de code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="a1658-167">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="a1658-168">Voeg de volgende sectie **appSetttings** toe aan het bestand **App.config**.</span><span class="sxs-lookup"><span data-stu-id="a1658-168">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="a1658-169">Deze instellingen worden gebruikt door de Help-methode: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="a1658-169">These settings are used by the helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="a1658-170">Vervang de waarden voor **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** en **&lt;Tenant ID&gt;** door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="a1658-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="a1658-171">Voeg de volgende **using**-instructies toe aan het bronbestand (Program.cs) in het project.</span><span class="sxs-lookup"><span data-stu-id="a1658-171">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

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

6. <span data-ttu-id="a1658-172">Voeg de volgende code toe aan de methode **Main** om een instantie van de klasse **DataPipelineManagementClient** te maken.
</span><span class="sxs-lookup"><span data-stu-id="a1658-172">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="a1658-173">U gebruikt dit object om een gegevensfactory, een gekoppelde service, gegevenssets voor invoer en uitvoer, en een pijplijn te maken.</span><span class="sxs-lookup"><span data-stu-id="a1658-173">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="a1658-174">U gebruikt dit object ook om segmenten van een gegevensset te bewaken tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="a1658-174">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="a1658-175">Vervang de waarde van **resourceGroupName** door de naam van uw Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a1658-175">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="a1658-176">Werk de naam van de data factory (dataFactoryName) zodanig bij dat deze uniek is.</span><span class="sxs-lookup"><span data-stu-id="a1658-176">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="a1658-177">De naam van de gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="a1658-177">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="a1658-178">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="a1658-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="a1658-179">Voeg de volgende code die een **gegevensfactory** maakt toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="a1658-179">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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

    <span data-ttu-id="a1658-180">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="a1658-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="a1658-181">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="a1658-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="a1658-182">Bijvoorbeeld een kopieeractiviteit om gegevens van een bron- naar een doelgegevensopslagplaats te kopiëren en een HDInsight Hive-activiteit om een Hive-script uit te voeren voor het transformeren van invoergegevens naar productuitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="a1658-182">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="a1658-183">U begint in deze stap met het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a1658-183">Let's start with creating the data factory in this step.</span></span>
8. <span data-ttu-id="a1658-184">Voeg de volgende code die een **gekoppelde Azure Storage-service** maakt toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="a1658-184">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a1658-185">Vervang **storageaccountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="a1658-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="a1658-186">U maakt gekoppelde services in een gegevensfactory om uw gegevensarchieven en compute-services aan de gegevensfactory te koppelen.</span><span class="sxs-lookup"><span data-stu-id="a1658-186">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="a1658-187">In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="a1658-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="a1658-188">U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel).</span><span class="sxs-lookup"><span data-stu-id="a1658-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="a1658-189">Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="a1658-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="a1658-190">De AzureStorageLinkedService koppelt uw Azure-opslagaccount aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a1658-190">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="a1658-191">Dit opslagaccount is het account waarin u een container hebt gemaakt en gegevens hebt geüpload als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a1658-191">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="a1658-192">Voeg de volgende code die een **gekoppelde Azure SLQ-service** maakt toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="a1658-192">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a1658-193">Vervang **servername**, **databasename**, **username** en **password** door de namen van uw Azure SQL-server, database, gebruiker en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a1658-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="a1658-194">De AzureSqlLinkedService koppelt uw Azure SQL-database aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a1658-194">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="a1658-195">De gegevens die worden gekopieerd uit de blobopslag worden opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="a1658-195">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="a1658-196">Als onderdeel van de [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) hebt u de emp-tabel in deze database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a1658-196">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="a1658-197">Voeg de volgende code die **gegevenssets voor invoer en uitvoer** maakt toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="a1658-197">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="a1658-198">In de vorige stap hebt u gekoppelde services gemaakt om uw Azure-opslagaccount en Azure SQL-database aan de gegevensfactory te koppelen.</span><span class="sxs-lookup"><span data-stu-id="a1658-198">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="a1658-199">In deze stap definieert u twee gegevenssets, InputDataset en OutputDataset genaamd, die staan voor de invoer- en uitvoergegevens die zijn opgeslagen in de gegevensarchieven waarnaar wordt verwezen door respectievelijk de AzureStorageLinkedService en de AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="a1658-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="a1658-200">De gekoppelde Azure Storage-service geeft de verbindingsreeks op die de Data Factory-service tijdens runtime gebruikt om verbinding te maken met uw Azure-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a1658-200">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="a1658-201">En de blobgegevensset voor invoer (InputDataset) geeft de container en de map met de invoergegevens op.</span><span class="sxs-lookup"><span data-stu-id="a1658-201">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="a1658-202">Op dezelfde manier geeft de gekoppelde Azure SQL Database-service de verbindingsreeks op die de Data Factory-service in runtime gebruikt om verbinding te maken met uw Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="a1658-202">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="a1658-203">En de uitvoergegevensset van de SQL-tabel (OututDataset) geeft de tabel in de database op waarnaar de gegevens uit de blobopslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="a1658-203">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span>

    <span data-ttu-id="a1658-204">In deze stap maakt u een gegevensset met de naam InputDataset die verwijst naar een blobbestand (emp.txt) in de hoofdmap van een blobcontainer (adftutorial) in Azure Storage. Deze container wordt vertegenwoordigd door de gekoppelde AzureStorageLinkedService-service.</span><span class="sxs-lookup"><span data-stu-id="a1658-204">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="a1658-205">Als u geen waarde voor de fileName hebt opgeven (of hebt overgeslagen), worden gegevens uit alle blobs in de invoermap naar het doel gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="a1658-205">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="a1658-206">In deze zelfstudie geeft u een waarde op voor de fileName.</span><span class="sxs-lookup"><span data-stu-id="a1658-206">In this tutorial, you specify a value for the fileName.</span></span>    

    <span data-ttu-id="a1658-207">In deze stap maakt u een uitvoergegevensset met de naam **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="a1658-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="a1658-208">Deze gegevensset wijst naar een SQL-tabel in de Azure SQL-database die wordt vertegenwoordigd door **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="a1658-208">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="a1658-209">Voeg de volgende code die **een pijplijn maakt en activeert** toe aan de methode **Main**.</span><span class="sxs-lookup"><span data-stu-id="a1658-209">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="a1658-210">In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a1658-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="a1658-211">Houd rekening met de volgende punten:</span><span class="sxs-lookup"><span data-stu-id="a1658-211">Note the following points:</span></span>
   
    - <span data-ttu-id="a1658-212">In het gedeelte Activiteiten is er slechts één activiteit waarvan **type** is ingesteld op **Copy**.</span><span class="sxs-lookup"><span data-stu-id="a1658-212">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="a1658-213">Zie het artikel [Activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) voor meer informatie over kopieeractiviteiten.</span><span class="sxs-lookup"><span data-stu-id="a1658-213">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="a1658-214">In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a1658-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="a1658-215">De invoer voor de activiteit is ingesteld op **InputDataset** en de uitvoer voor de activiteit is ingesteld op **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="a1658-215">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="a1658-216">In het gedeelte **typeProperties** is **BlobSource** opgegeven als het brontype en **SqlSink** als het sink-type.</span><span class="sxs-lookup"><span data-stu-id="a1658-216">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="a1658-217">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een volledige lijst van gegevensarchieven die worden ondersteund door kopieeractiviteiten als bronnen en sinks.</span><span class="sxs-lookup"><span data-stu-id="a1658-217">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="a1658-218">Klik op de koppeling in de tabel voor informatie over het gebruik van een specifiek ondersteund gegevensarchief als een bron/sink.</span><span class="sxs-lookup"><span data-stu-id="a1658-218">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
   
    <span data-ttu-id="a1658-219">Momenteel is de uitvoergegevensset dat wat de planning aanstuurt.</span><span class="sxs-lookup"><span data-stu-id="a1658-219">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="a1658-220">In deze zelfstudie is de uitvoergegevensset geconfigureerd voor het produceren van een segment eenmaal per uur.</span><span class="sxs-lookup"><span data-stu-id="a1658-220">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="a1658-221">De pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, ofwel 24 uur.</span><span class="sxs-lookup"><span data-stu-id="a1658-221">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="a1658-222">Daarom worden 24 segmenten van de uitvoergegevensset door de pijplijn geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a1658-222">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span>
12. <span data-ttu-id="a1658-223">Voeg de volgende code toe aan de methode **Main** om de status van een gegevenssegment van de uitvoergegevensset te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="a1658-223">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="a1658-224">In dit voorbeeld wordt alleen een segment verwacht.</span><span class="sxs-lookup"><span data-stu-id="a1658-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="a1658-225">Voeg de volgende code toe om details van de uitvoering van een gegevenssegment naar de methode **Main** te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="a1658-225">Add the following code to get run details for a data slice to the **Main** method.</span></span>

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
            }
        );

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

14. <span data-ttu-id="a1658-226">Voeg de volgende Help-methode toe die door de methode **Main** wordt gebruikt voor de klasse **Program**.</span><span class="sxs-lookup"><span data-stu-id="a1658-226">Add the following helper method used by the **Main** method to the **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a1658-227">Wanneer u de volgende code kopieert en plakt, zorg er dan voor dat de gekopieerde code zich op hetzelfde niveau bevindt als de Main-methode.</span><span class="sxs-lookup"><span data-stu-id="a1658-227">When you copy and paste the following code, make sure that the copied code is at the same level as the Main method.</span></span>

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

15. <span data-ttu-id="a1658-228">Vouw in Solution Explorer het project (DataFactoryAPITestApp) uit, klik met de rechtermuisknop op **References** en klik vervolgens op **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="a1658-228">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="a1658-229">Schakel het selectievakje voor **System.Configuration**-assembly in.</span><span class="sxs-lookup"><span data-stu-id="a1658-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="a1658-230">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1658-230">and click **OK**.</span></span>
16. <span data-ttu-id="a1658-231">Bouw de consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="a1658-231">Build the console application.</span></span> <span data-ttu-id="a1658-232">Klik op **Build** in het menu en klik op **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="a1658-232">Click **Build** on the menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="a1658-233">Controleer of er ten minste één bestand in de **adftutorial**-container in uw Azure Blob Storage staat.</span><span class="sxs-lookup"><span data-stu-id="a1658-233">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="a1658-234">Als dit niet het geval is, maakt u in Kladblok het **Emp.txt**-bestand met de volgende inhoud en uploadt u het bestand naar de adftutorial-container.</span><span class="sxs-lookup"><span data-stu-id="a1658-234">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="a1658-235">Voer het voorbeeld uit door op **Debug** -> **Start Debugging** te klikken in het menu.</span><span class="sxs-lookup"><span data-stu-id="a1658-235">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="a1658-236">Als u **Getting run details of a data slice** ziet, wacht u een paar minuten en drukt u op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="a1658-236">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="a1658-237">Gebruik Azure Portal om te controleren of de gegevensfactory **APITutorialFactory** wordt gemaakt met de volgende artefacten:</span><span class="sxs-lookup"><span data-stu-id="a1658-237">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
   * <span data-ttu-id="a1658-238">Gekoppelde service: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="a1658-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="a1658-239">Gegevensset: **InputDataset** en **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="a1658-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="a1658-240">Pijplijn: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="a1658-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="a1658-241">Controleer of de twee werknemersrecords zijn gemaakt in de tabel **emp** in de opgegeven Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="a1658-241">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1658-242">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a1658-242">Next steps</span></span>
<span data-ttu-id="a1658-243">Zie [Naslaginformatie over de .NET API voor Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor volledige documentatie over .NET API voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a1658-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="a1658-244">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a1658-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="a1658-245">De volgende tabel bevat een lijst met gegevensarchieven die worden ondersteund als bron en doel voor de kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="a1658-245">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="a1658-246">Klik op de koppeling voor de gegevensopslag in de tabel voor meer informatie over het kopiëren van gegevens naar/uit een gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a1658-246">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>

