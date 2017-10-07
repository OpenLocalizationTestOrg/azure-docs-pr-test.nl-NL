---
title: aaaUse hello .NET SDK toodevelop toepassingen in Azure Data Lake Store | Microsoft Docs
description: Gebruik van Azure Data Lake Store .NET SDK toocreate een Data Lake Store-account en uitvoeren van basisbewerkingen in Data Lake Store Hallo
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="f6e05-103">Aan de slag met Azure Data Lake Store met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f6e05-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6e05-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f6e05-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="f6e05-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6e05-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="f6e05-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="f6e05-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="f6e05-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="f6e05-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="f6e05-108">REST API</span><span class="sxs-lookup"><span data-stu-id="f6e05-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="f6e05-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f6e05-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="f6e05-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="f6e05-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="f6e05-111">Python</span><span class="sxs-lookup"><span data-stu-id="f6e05-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="f6e05-112">Meer informatie over hoe toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basisbewerkingen zoals maken van mappen, uploaden en downloaden van gegevensbestanden, enzovoort. Zie [Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f6e05-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6e05-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f6e05-113">Prerequisites</span></span>
* <span data-ttu-id="f6e05-114">**Visual Studio 2013, 2015 of 2017**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="f6e05-115">Hallo onderstaande instructies Gebruik Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="f6e05-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="f6e05-116">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-116">**An Azure subscription**.</span></span> <span data-ttu-id="f6e05-117">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f6e05-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="f6e05-118">**Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="f6e05-119">Voor instructies over het toocreate een account, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f6e05-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="f6e05-120">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="f6e05-121">U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f6e05-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="f6e05-122">Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="f6e05-123">Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f6e05-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="f6e05-124">Een .NET-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f6e05-124">Create a .NET application</span></span>
1. <span data-ttu-id="f6e05-125">Open Visual Studio en maak een consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="f6e05-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="f6e05-126">Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="f6e05-127">Van **nieuw Project**typt of selecteert u Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="f6e05-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="f6e05-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f6e05-128">Property</span></span> | <span data-ttu-id="f6e05-129">Waarde</span><span class="sxs-lookup"><span data-stu-id="f6e05-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="f6e05-130">Category</span><span class="sxs-lookup"><span data-stu-id="f6e05-130">Category</span></span> |<span data-ttu-id="f6e05-131">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="f6e05-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="f6e05-132">Template</span><span class="sxs-lookup"><span data-stu-id="f6e05-132">Template</span></span> |<span data-ttu-id="f6e05-133">Console Application</span><span class="sxs-lookup"><span data-stu-id="f6e05-133">Console Application</span></span> |
   | <span data-ttu-id="f6e05-134">Name</span><span class="sxs-lookup"><span data-stu-id="f6e05-134">Name</span></span> |<span data-ttu-id="f6e05-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="f6e05-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="f6e05-136">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="f6e05-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="f6e05-137">Hallo Nuget-pakketten tooyour project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f6e05-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="f6e05-138">Met de rechtermuisknop op Hallo projectnaam in Solution Explorer Hallo en klik op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="f6e05-139">In Hallo **Nuget Package Manager** tabblad, zorg ervoor dat **pakketbron** te is ingesteld,**nuget.org** en die **Include prerelease** selectievakje is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f6e05-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="f6e05-140">Zoek en installeer Hallo NuGet-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="f6e05-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="f6e05-141">`Microsoft.Azure.Management.DataLake.Store`: in deze zelfstudie wordt gebruikgemaakt van v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="f6e05-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="f6e05-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication`: in deze zelfstudie wordt gebruikgemaakt van v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="f6e05-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="f6e05-143">![Een Nuget-bron toevoegen](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Een nieuw Azure Data Lake-account maken")</span><span class="sxs-lookup"><span data-stu-id="f6e05-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="f6e05-144">Sluit Hallo **Nuget Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="f6e05-145">Open **Program.cs**, verwijder de bestaande code Hallo en neemt Hallo instructies tooadd verwijzingen toonamespaces te volgen.</span><span class="sxs-lookup"><span data-stu-id="f6e05-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="f6e05-146">Declareer Hallo variabelen zoals hieronder wordt weergegeven en Hallo waarden opgeven voor Data Lake Store-naam en het Hallo-Resourcegroepnaam die al bestaan.</span><span class="sxs-lookup"><span data-stu-id="f6e05-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="f6e05-147">Zorg er ook Hallo lokale pad en de bestandsnaam die u hier opgeeft, moeten al bestaan op Hallo-computer.</span><span class="sxs-lookup"><span data-stu-id="f6e05-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="f6e05-148">Hallo codefragment volgen na de naamruimtedeclaraties Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f6e05-148">Add hello following code snippet after hello namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="f6e05-149">In de Hallo resterende secties van Hallo artikel, ziet u hoe toouse Hallo beschikbare .NET methoden tooperform bewerkingen zoals verificatie, uploaden, enz.</span><span class="sxs-lookup"><span data-stu-id="f6e05-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="f6e05-150">Authentication</span><span class="sxs-lookup"><span data-stu-id="f6e05-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="f6e05-151">Als u gebruikmaakt van verificatie door eindgebruikers (aanbevolen voor deze zelfstudie)</span><span class="sxs-lookup"><span data-stu-id="f6e05-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="f6e05-152">Gebruik deze met een bestaande Azure AD systeemeigen toepassing tooauthenticate uw toepassing **interactief**, dit betekent dat u wordt gevraagd tooenter uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="f6e05-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="f6e05-153">Hallo codefragment hieronder worden de standaardwaarden voor eenvoudig te gebruiken gebruikt voor client-ID en omleidings-URI die is voor een Azure-abonnement geschikt.</span><span class="sxs-lookup"><span data-stu-id="f6e05-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="f6e05-154">toohelp u deze zelfstudie sneller zijn voltooid, wordt aangeraden gebruik van deze benadering.</span><span class="sxs-lookup"><span data-stu-id="f6e05-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="f6e05-155">Hallo-codefragment hieronder, geeft u alleen Hallo-waarde voor uw tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="f6e05-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="f6e05-156">U kunt ophalen met behulp van de instructies op Hallo [maken van een Active Directory-toepassing](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f6e05-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="f6e05-157">Een aantal dingen tooknow over deze bovenstaande codefragment:</span><span class="sxs-lookup"><span data-stu-id="f6e05-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="f6e05-158">in dit fragment maakt gebruik van toohelp u Hallo zelfstudie sneller zijn voltooid, een an Azure AD-domein en de client-ID die is standaard beschikbaar voor alle Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="f6e05-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="f6e05-159">U kunt **dit fragment dus in zijn huidige vorm in uw toepassing gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="f6e05-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="f6e05-160">Echter, als u wilt dat toouse uw eigen Azure AD-domein en client-ID van toepassing, moet u een systeemeigen Azure AD-toepassing maken en vervolgens gebruik hello Azure AD-tenant-ID, client-ID en omleidings-URI voor de toepassing hello u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f6e05-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="f6e05-161">Zie [Een Active Directory-toepassing voor verificatie van eindgebruikers maken met Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="f6e05-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="f6e05-162">Als u gebruikmaakt van service-naar-serviceverificatie met clientgeheim</span><span class="sxs-lookup"><span data-stu-id="f6e05-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="f6e05-163">Hallo volgende codefragment gebruikte tooauthenticate uw toepassing kan worden **niet-interactief**, met behulp van het clientgeheim Hallo / sleutel voor een toepassing / service-principal.</span><span class="sxs-lookup"><span data-stu-id="f6e05-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="f6e05-164">Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="f6e05-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="f6e05-165">Voor instructies over hoe toocreate hello Azure AD-webtoepassing en hoe tooretrieve Hallo van client-ID en clientgeheim vereist in Hallo codefragment hieronder, Zie [een Active Directory-toepassing voor verificatie van de service-naar-service maken met gegevens Lake Store](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="f6e05-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="f6e05-166">Als u gebruikmaakt van service-naar-serviceverificatie met certificaat</span><span class="sxs-lookup"><span data-stu-id="f6e05-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="f6e05-167">Een derde optie, hello volgende codefragment kan worden gebruikt tooauthenticate uw toepassing **niet-interactief**, met behulp van Hallo-certificaat voor een Azure Active Directory-toepassing / service principal.</span><span class="sxs-lookup"><span data-stu-id="f6e05-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="f6e05-168">Gebruik dit met een bestaande [Azure AD-toepassing met certificaten](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="f6e05-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="f6e05-169">Clientobjecten maken</span><span class="sxs-lookup"><span data-stu-id="f6e05-169">Create client objects</span></span>
<span data-ttu-id="f6e05-170">Hallo volgende fragment maakt Hallo Data Lake Store-account en bestandssysteem clientobjecten die worden gebruikt tooissue toohello serviceaanvraag.</span><span class="sxs-lookup"><span data-stu-id="f6e05-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="f6e05-171">Alle Data Lake Store-accounts binnen een abonnement weergeven</span><span class="sxs-lookup"><span data-stu-id="f6e05-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="f6e05-172">Hallo bevat volgende fragment alle Data Lake Store-accounts binnen een bepaald Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="f6e05-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="f6e05-173">Een map maken</span><span class="sxs-lookup"><span data-stu-id="f6e05-173">Create a directory</span></span>
<span data-ttu-id="f6e05-174">Hallo volgende codefragment bevat een `CreateDirectory` methode waarmee u toocreate een map in een Data Lake Store-account kunt.</span><span class="sxs-lookup"><span data-stu-id="f6e05-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="f6e05-175">Bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="f6e05-175">Upload a file</span></span>
<span data-ttu-id="f6e05-176">Hallo volgende codefragment bevat een `UploadFile` methode waarmee u tooupload kunt bestanden tooa Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="f6e05-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="f6e05-177">Hallo SDK biedt ondersteuning voor recursieve uploaden en downloaden tussen een lokaal pad en een pad naar een Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f6e05-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="f6e05-178">Bestands- of mapinformatie ophalen</span><span class="sxs-lookup"><span data-stu-id="f6e05-178">Get file or directory info</span></span>
<span data-ttu-id="f6e05-179">Hallo volgende codefragment bevat een `GetItemInfo` methode die u kunt tooretrieve informatie over een bestand of mapinformatie die beschikbaar is in Data Lake Store te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6e05-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="f6e05-180">Bestanden of mappen weergeven</span><span class="sxs-lookup"><span data-stu-id="f6e05-180">List file or directories</span></span>
<span data-ttu-id="f6e05-181">Hallo volgende codefragment bevat een `ListItem` methode die toolist Hallo bestanden en mappen in een Data Lake Store-account kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6e05-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="f6e05-182">Bestanden samenvoegen</span><span class="sxs-lookup"><span data-stu-id="f6e05-182">Concatenate files</span></span>
<span data-ttu-id="f6e05-183">Hallo volgende codefragment bevat een `ConcatenateFiles` methode tooconcatenate bestanden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6e05-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="f6e05-184">Toevoegen van tooa</span><span class="sxs-lookup"><span data-stu-id="f6e05-184">Append tooa file</span></span>
<span data-ttu-id="f6e05-185">Hallo volgende codefragment bevat een `AppendToFile` methode die u gebruikt tooa gegevensbestand al opgeslagen in een Data Lake Store-account toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f6e05-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="f6e05-186">Bestand downloaden</span><span class="sxs-lookup"><span data-stu-id="f6e05-186">Download a file</span></span>
<span data-ttu-id="f6e05-187">Hallo volgende codefragment bevat een `DownloadFile` methode toodownload een bestand van een Data Lake Store-account te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6e05-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="f6e05-188">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6e05-188">Next steps</span></span>
* [<span data-ttu-id="f6e05-189">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="f6e05-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="f6e05-190">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f6e05-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f6e05-191">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f6e05-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="f6e05-192">Naslaginformatie over Data Lake Store .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f6e05-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="f6e05-193">Naslaginformatie over Data Lake Store REST</span><span class="sxs-lookup"><span data-stu-id="f6e05-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
