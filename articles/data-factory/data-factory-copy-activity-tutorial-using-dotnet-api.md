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
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="65925-103">Zelfstudie: een pijplijn maken met de kopieeractiviteit in .NET API</span><span class="sxs-lookup"><span data-stu-id="65925-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="65925-104">Overzicht en vereisten</span><span class="sxs-lookup"><span data-stu-id="65925-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="65925-105">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="65925-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="65925-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="65925-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="65925-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="65925-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="65925-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65925-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="65925-109">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="65925-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="65925-110">REST API</span><span class="sxs-lookup"><span data-stu-id="65925-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="65925-111">.NET API</span><span class="sxs-lookup"><span data-stu-id="65925-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="65925-112">In dit artikel leert u hoe toouse [.NET API](https://portal.azure.com) toocreate een gegevensfactory met een pijplijn waarmee gegevens worden gekopieerd van een Azure blob storage tooan Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="65925-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="65925-113">Als u nieuwe tooAzure Data Factory, lees Hallo [inleiding tooAzure Data Factory](data-factory-introduction.md) artikel voordat u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="65925-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="65925-114">In deze zelfstudie maakt u een pijplijn met één activiteit erin: kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="65925-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="65925-115">Hallo kopieeractiviteit kopieert gegevens van een gegevensarchief voor ondersteunde gegevens store tooa ondersteunde sink.</span><span class="sxs-lookup"><span data-stu-id="65925-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="65925-116">Zie [Ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) voor een lijst met gegevensarchieven die worden ondersteund als bron en als sink.</span><span class="sxs-lookup"><span data-stu-id="65925-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="65925-117">Hallo-activiteit wordt mogelijk gemaakt door een wereldwijd beschikbare service waarmee gegevens tussen verschillende gegevensarchieven op een manier veilig, betrouwbaar en schaalbaar kan worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="65925-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="65925-118">Zie voor meer informatie over Hallo Kopieeractiviteit [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="65925-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="65925-119">Een pijplijn kan meer dan één activiteit hebben.</span><span class="sxs-lookup"><span data-stu-id="65925-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="65925-120">En u kunt twee activiteiten (één activiteit uitgevoerd na de andere) koppelen door de uitvoergegevensset Hallo van een activiteit instellen als de Hallo invoergegevensset Hallo andere activiteit.</span><span class="sxs-lookup"><span data-stu-id="65925-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="65925-121">Zie [Meerdere activiteiten in een pijplijn](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="65925-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="65925-122">Zie [Naslaginformatie over de .NET API voor Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor volledige documentatie over .NET API voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="65925-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="65925-123">Hallo data pipeline in deze zelfstudie worden gegevens gekopieerd van een bron data store tooa doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="65925-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="65925-124">Voor een zelfstudie over het tootransform van gegevens met behulp van Azure Data Factory, Zie [zelfstudie: een pijplijn tootransform gegevens met Hadoop-cluster bouwen](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="65925-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65925-125">Vereisten</span><span class="sxs-lookup"><span data-stu-id="65925-125">Prerequisites</span></span>
* <span data-ttu-id="65925-126">Doorloop [overzicht van de zelfstudie en vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget een overzicht van de zelfstudie Hallo en volledige Hallo **vereiste** stappen.</span><span class="sxs-lookup"><span data-stu-id="65925-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="65925-127">Visual Studio 2012 of 2013 of 2015</span><span class="sxs-lookup"><span data-stu-id="65925-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="65925-128">Download en installeer [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="65925-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="65925-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="65925-129">Azure PowerShell.</span></span> <span data-ttu-id="65925-130">Volg de instructies in [hoe tooinstall en configureren van Azure PowerShell](../powershell-install-configure.md) artikel tooinstall Azure PowerShell op uw computer.</span><span class="sxs-lookup"><span data-stu-id="65925-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="65925-131">U Azure PowerShell toocreate een Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="65925-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="65925-132">Een toepassing maken in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="65925-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="65925-133">Een Azure Active Directory-toepassing maken, een service-principal voor de toepassing hello maken en toewijzen toohello **Data Factory Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="65925-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="65925-134">Start **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="65925-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="65925-135">Voer Hallo volgende opdracht en Voer Hallo-gebruikersnaam en wachtwoord toosign in toohello Azure-portal te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65925-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="65925-136">Hallo opdracht tooview na alle Hallo abonnementen voor dit account uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65925-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="65925-137">Hallo opdracht tooselect Hallo abonnement dat u wilt dat toowork met volgende worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65925-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="65925-138">Vervang  **&lt;NameOfAzureSubscription** &gt; met Hallo-naam van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="65925-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="65925-139">Noteer **SubscriptionId** en **TenantId** van Hallo-uitvoer van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="65925-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="65925-140">Maak een Azure-resourcegroep met de naam **ADFTutorialResourceGroup** door het uitvoeren van de volgende opdracht in PowerShell Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="65925-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="65925-141">Als de resourcegroep Hallo al bestaat, die u opgeeft of tooupdate deze (Y) of als (N).</span><span class="sxs-lookup"><span data-stu-id="65925-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="65925-142">Als u een andere resourcegroep gebruikt, moet u toouse Hallo-naam van de resourcegroep in plaats van ADFTutorialResourceGroup in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="65925-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="65925-143">Maak een Azure Active Directory-toepassing.</span><span class="sxs-lookup"><span data-stu-id="65925-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="65925-144">Als u krijgt de volgende fout hello, Geef een andere URL en voer de opdracht Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="65925-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="65925-145">Hallo AD-service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="65925-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="65925-146">Toevoegen van de service principal toohello **Data Factory Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="65925-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="65925-147">Ophalen van Hallo toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="65925-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="65925-148">Noteer Hallo toepassings-ID (applicationID) van Hallo-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="65925-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="65925-149">U moet na deze stappen beschikken over de volgende vier waarden:</span><span class="sxs-lookup"><span data-stu-id="65925-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="65925-150">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="65925-150">Tenant ID</span></span>
* <span data-ttu-id="65925-151">Abonnements-id</span><span class="sxs-lookup"><span data-stu-id="65925-151">Subscription ID</span></span>
* <span data-ttu-id="65925-152">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="65925-152">Application ID</span></span>
* <span data-ttu-id="65925-153">Wachtwoord (opgegeven in de eerste opdracht Hallo)</span><span class="sxs-lookup"><span data-stu-id="65925-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="65925-154">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="65925-154">Walkthrough</span></span>
1. <span data-ttu-id="65925-155">Maak met behulp van Visual Studio 2012/2013/2015 een C# .NET-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="65925-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="65925-156">Open **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="65925-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="65925-157">Klik op **bestand**, wijst u te**nieuw**, en klik op **Project**.</span><span class="sxs-lookup"><span data-stu-id="65925-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="65925-158">Vouw **Templates** uit en selecteer **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="65925-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="65925-159">Tijdens deze walkthrough gebruikt u C#, maar u kunt een willekeurige .NET-taal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65925-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="65925-160">Selecteer **consoletoepassing** uit de lijst Hallo van projecttypen op Hallo rechts.</span><span class="sxs-lookup"><span data-stu-id="65925-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="65925-161">Voer **DataFactoryAPITestApp** voor Hallo naam.</span><span class="sxs-lookup"><span data-stu-id="65925-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="65925-162">Selecteer **C:\ADFGetStarted** voor Hallo locatie.</span><span class="sxs-lookup"><span data-stu-id="65925-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="65925-163">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="65925-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="65925-164">Klik op **extra**, wijst u te**NuGet Package Manager**, en klik op **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="65925-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="65925-165">In Hallo **Package Manager Console**, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="65925-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="65925-166">Voer Hallo opdracht tooinstall Data Factory-pakket te volgen:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="65925-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="65925-167">Voer Hallo opdracht tooinstall Azure Active Directory-pakket (Active Directory-API in gebruikt Hallo code) te volgen:`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="65925-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="65925-168">Voeg de volgende Hallo **appSetttings** sectie toohello **App.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="65925-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="65925-169">Deze instellingen worden gebruikt door Hallo Help-methode: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="65925-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="65925-170">Vervang de waarden voor **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** en **&lt;Tenant ID&gt;** door uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="65925-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="65925-171">Voeg de volgende Hallo **met** instructies toohello bronbestand (Program.cs) in het Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="65925-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="65925-172">Toevoegen na de code die u een exemplaar van maakt Hallo **DataPipelineManagementClient** klasse toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="65925-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="65925-173">U kunt dit object toocreate gebruiken een gegevensfactory, een gekoppelde service, invoer- en uitvoergegevenssets en een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="65925-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="65925-174">U kunt ook dit object toomonitor segmenten van een gegevensset gebruiken tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="65925-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="65925-175">Vervang de waarde Hallo van **resourceGroupName** met Hallo-naam van uw Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="65925-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="65925-176">Naam van de data factory (dataFactoryName) toobe Hallo unieke bijwerken.</span><span class="sxs-lookup"><span data-stu-id="65925-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="65925-177">Naam van Hallo-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="65925-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="65925-178">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="65925-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="65925-179">Toevoegen Hallo code die wordt gemaakt na een **gegevensfactory** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="65925-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="65925-180">Een gegevensfactory kan één of meer pijplijnen hebben.</span><span class="sxs-lookup"><span data-stu-id="65925-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="65925-181">Een pijplijn kan één of meer activiteiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="65925-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="65925-182">Bijvoorbeeld invoergegevens een Kopieeractiviteit toocopy-gegevens van een doelgegevensopslagplaats tooa bron en het toorun in een HDInsight Hive-activiteit een Hive-script tootransform gegevens tooproduct uitvoer.</span><span class="sxs-lookup"><span data-stu-id="65925-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="65925-183">Laten we beginnen met het maken van de gegevensfactory Hallo in deze stap.</span><span class="sxs-lookup"><span data-stu-id="65925-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="65925-184">Toevoegen Hallo code die wordt gemaakt na een **gekoppelde Azure Storage-service** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="65925-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="65925-185">Vervang **storageaccountname** en **accountkey** door de naam en sleutel van uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="65925-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="65925-186">U maken gekoppelde services in een data factory-toolink uw gegevens worden opgeslagen en compute services toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="65925-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="65925-187">In deze zelfstudie gebruikt u niet een willekeurige compute-service, zoals Azure HDInsight of Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="65925-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="65925-188">U gebruikt twee gegevensarchieven van het type Azure Storage (bron) en Azure SQL Database (doel).</span><span class="sxs-lookup"><span data-stu-id="65925-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="65925-189">Daarom maakt u twee gekoppelde services met de naam AzureStorageLinkedService en AzureSqlLinkedService van het type: AzureStorage en AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="65925-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="65925-190">Hallo AzureStorageLinkedService koppelt u uw Azure storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="65925-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="65925-191">Dit opslagaccount wordt Hallo een waarop u container gemaakt en Hallo gegevens geüpload als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="65925-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="65925-192">Toevoegen Hallo code die wordt gemaakt na een **Azure SQL gekoppelde service** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="65925-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="65925-193">Vervang **servername**, **databasename**, **username** en **password** door de namen van uw Azure SQL-server, database, gebruiker en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="65925-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

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

    <span data-ttu-id="65925-194">Azuresqllinkedservice wordt uw Azure SQL database toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="65925-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="65925-195">Hallo-gegevens die worden gekopieerd van de blob-opslag hello wordt opgeslagen in deze database.</span><span class="sxs-lookup"><span data-stu-id="65925-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="65925-196">Hallo emp-tabel in deze database wordt gemaakt als onderdeel van [vereisten](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="65925-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="65925-197">Hallo code die wordt gemaakt na toevoegen **invoer- en uitvoergegevenssets** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="65925-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

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
    
    <span data-ttu-id="65925-198">In de vorige stap Hallo gemaakt gekoppelde services toolink uw Azure Storage-account en de Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="65925-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="65925-199">In deze stap definieert u twee gegevenssets met de naam InputDataset en OutputDataset die vertegenwoordigen de invoer- en uitvoergegevens die zijn opgeslagen in Hallo gegevensarchieven waarnaar wordt verwezen door de AzureStorageLinkedService en AzureSqlLinkedService respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="65925-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="65925-200">Hallo gekoppelde Azure storage-service geeft Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op uitvoeringstijd tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="65925-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="65925-201">En Hallo blob-invoerbron gegevensset (InputDataset) geeft Hallo-container en Hallo-map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="65925-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="65925-202">Op deze manier geeft hello Azure SQL Database gekoppeld service Hallo verbindingsreeks die gebruikmaakt van de Data Factory-service op de runtime tooconnect tooyour Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="65925-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="65925-203">En Hallo uitvoer gegevensset met SQL-tabel (OututDataset) geeft Hallo tabel in Hallo database toowhich Hallo gegevens uit Hallo blob-opslag worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="65925-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="65925-204">In deze stap maakt u een gegevensset met de naam InputDataset die tooa blob-bestand (emp.txt) verwijst in de hoofdmap Hallo van een blob-container (adftutorial) in hello Azure Storage dat wordt vertegenwoordigd door Hallo gekoppelde AzureStorageLinkedService-service.</span><span class="sxs-lookup"><span data-stu-id="65925-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="65925-205">Als u niet een waarde voor fileName hello opgeven (of overslaan), zijn gegevens uit alle blobs in de invoermap Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="65925-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="65925-206">In deze zelfstudie maakt opgeven u een waarde voor Hallo fileName.</span><span class="sxs-lookup"><span data-stu-id="65925-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="65925-207">In deze stap maakt u een uitvoergegevensset met de naam **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="65925-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="65925-208">Deze gegevensset verwijst tooa SQL-tabel in hello Azure SQL-database dat wordt vertegenwoordigd door **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="65925-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="65925-209">Voeg Hallo volgende code die **wordt gemaakt en wordt geactiveerd op een pijplijn** toohello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="65925-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="65925-210">In deze stap maakt u een pijplijn met een **kopieeractiviteit** die gebruikmaakt van **InputDataset** als invoer en **OutputDataset** als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="65925-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

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

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

    <span data-ttu-id="65925-211">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="65925-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="65925-212">In Hallo gedeelte activiteiten is er slechts één activiteit waarvan **type** te is ingesteld,**kopie**.</span><span class="sxs-lookup"><span data-stu-id="65925-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="65925-213">Zie voor meer informatie over de kopieeractiviteit hello [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="65925-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="65925-214">In Data Factory-oplossingen kunt u ook [activiteiten voor gegevenstransformatie](data-factory-data-transformation-activities.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65925-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="65925-215">Invoer voor Hallo-activiteit is ingesteld, te**InputDataset** en de uitvoer voor Hallo activiteit te is ingesteld**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="65925-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="65925-216">In Hallo **typeProperties** sectie **BlobSource** is opgegeven als Hallo brontype en **SqlSink** is opgegeven als Hallo sink-type.</span><span class="sxs-lookup"><span data-stu-id="65925-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="65925-217">Zie voor een volledige lijst van gegevensarchieven die worden ondersteund door Hallo kopieeractiviteit als bronnen en put [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="65925-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="65925-218">toolearn hoe toouse een specifieke ondersteunde gegevens opslaan als een bron/sink, klikt u op Hallo-koppeling in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="65925-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="65925-219">Uitvoergegevensset is momenteel welke stations Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="65925-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="65925-220">In deze zelfstudie is uitvoergegevensset geconfigureerde tooproduce een segment eens per uur.</span><span class="sxs-lookup"><span data-stu-id="65925-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="65925-221">Hallo pijplijn heeft een begintijd en eindtijd die één dag uit elkaar liggen, wat is 24 uur zijn.</span><span class="sxs-lookup"><span data-stu-id="65925-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="65925-222">Daarom worden 24 segmenten van uitvoergegevensset geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="65925-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="65925-223">Hallo na code toohello toevoegen **Main** methode tooget Hallo status van een gegevenssegment Hallo uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="65925-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="65925-224">In dit voorbeeld wordt alleen een segment verwacht.</span><span class="sxs-lookup"><span data-stu-id="65925-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="65925-225">Toevoegen van de volgende code tooget Voer details voor een segment gegevens toohello hello **Main** methode.</span><span class="sxs-lookup"><span data-stu-id="65925-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="65925-226">Toevoegen van de volgende Help-methode die wordt gebruikt door Hallo Hallo **Main** methode toohello **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="65925-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="65925-227">Wanneer u kopieert en plakt Hallo code te volgen, zorg ervoor dat Hallo gekopieerde code is op hetzelfde niveau als Hallo Main-methode Hallo.</span><span class="sxs-lookup"><span data-stu-id="65925-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="65925-228">In Solution Explorer hello, vouw Hallo-project (DataFactoryAPITestApp), met de rechtermuisknop op **verwijzingen**, en klik op **verwijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="65925-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="65925-229">Schakel het selectievakje voor **System.Configuration**-assembly in.</span><span class="sxs-lookup"><span data-stu-id="65925-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="65925-230">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="65925-230">and click **OK**.</span></span>
16. <span data-ttu-id="65925-231">Hallo-consoletoepassing bouwen.</span><span class="sxs-lookup"><span data-stu-id="65925-231">Build hello console application.</span></span> <span data-ttu-id="65925-232">Klik op **bouwen** op en klik op Hallo **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="65925-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="65925-233">Controleer of er ten minste één bestand in Hallo **adftutorial** container in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="65925-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="65925-234">Als dit niet het geval is, maakt **Emp.txt** in Kladblok het bestand met de Hallo inhoud te volgen en upload het toohello adftutorial container.</span><span class="sxs-lookup"><span data-stu-id="65925-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="65925-235">Hallo-voorbeeld uitvoeren door te klikken op **Debug** -> **foutopsporing starten** Hallo-menu.</span><span class="sxs-lookup"><span data-stu-id="65925-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="65925-236">Wanneer er Hallo **details van een gegevenssegment ophalen uitvoeren**, wacht een paar minuten en druk op **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="65925-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="65925-237">Gebruik hello Azure portal tooverify die gegevensfactory hello **APITutorialFactory** wordt gemaakt met de Hallo artefacten te volgen:</span><span class="sxs-lookup"><span data-stu-id="65925-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="65925-238">Gekoppelde service: **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="65925-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="65925-239">Gegevensset: **InputDataset** en **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="65925-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="65925-240">Pijplijn: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="65925-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="65925-241">Controleer of Hallo twee werknemerrecords worden gemaakt in Hallo **emp** tabel in Hallo opgegeven Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="65925-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65925-242">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="65925-242">Next steps</span></span>
<span data-ttu-id="65925-243">Zie [Naslaginformatie over de .NET API voor Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) voor volledige documentatie over .NET API voor Data Factory.</span><span class="sxs-lookup"><span data-stu-id="65925-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="65925-244">In deze zelfstudie hebt u voor een kopieerbewerking een Azure Blob-opslag gebruikt als brongegevensarchief en een Azure SQL-database als doelgegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="65925-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="65925-245">Hallo bevat volgende tabel een lijst met gegevensarchieven als bronnen en bestemmingen wordt ondersteund door Hallo kopieeractiviteit:</span><span class="sxs-lookup"><span data-stu-id="65925-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="65925-246">toolearn over hoe gegevens uit een data toocopy opslaan, klikt u op Hallo-koppeling voor de gegevensopslag Hallo in Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="65925-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

