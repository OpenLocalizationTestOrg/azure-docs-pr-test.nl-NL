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
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>Aan de slag met Azure Data Lake Store met .NET SDK
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET-SDK](data-lake-store-get-started-net-sdk.md)
> * [Java-SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Meer informatie over hoe toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basisbewerkingen zoals maken van mappen, uploaden en downloaden van gegevensbestanden, enzovoort. Zie [Azure Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake.

## <a name="prerequisites"></a>Vereisten
* **Visual Studio 2013, 2015 of 2017**. Hallo onderstaande instructies Gebruik Visual Studio 2015 Update 2.

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* **Azure Data Lake Store-account**. Voor instructies over het toocreate een account, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)

* **Een Azure Active Directory-toepassing maken**. U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD. Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**. Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Een .NET-toepassing maken
1. Open Visual Studio en maak een consoletoepassing.
2. Van Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.
3. Van **nieuw Project**typt of selecteert u Hallo volgende waarden:

   | Eigenschap | Waarde |
   | --- | --- |
   | Category |Templates/Visual C#/Windows |
   | Template |Console Application |
   | Name |CreateADLApplication |
4. Klik op **OK** toocreate Hallo project.
5. Hallo Nuget-pakketten tooyour project toevoegen.

   1. Met de rechtermuisknop op Hallo projectnaam in Solution Explorer Hallo en klik op **NuGet-pakketten beheren**.
   2. In Hallo **Nuget Package Manager** tabblad, zorg ervoor dat **pakketbron** te is ingesteld,**nuget.org** en die **Include prerelease** selectievakje is geselecteerd.
   3. Zoek en installeer Hallo NuGet-pakketten te volgen:

      * `Microsoft.Azure.Management.DataLake.Store`: in deze zelfstudie wordt gebruikgemaakt van v2.1.3-preview.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication`: in deze zelfstudie wordt gebruikgemaakt van v2.2.12.

        ![Een Nuget-bron toevoegen](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Een nieuw Azure Data Lake-account maken")
   4. Sluit Hallo **Nuget Package Manager**.
6. Open **Program.cs**, verwijder de bestaande code Hallo en neemt Hallo instructies tooadd verwijzingen toonamespaces te volgen.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Declareer Hallo variabelen zoals hieronder wordt weergegeven en Hallo waarden opgeven voor Data Lake Store-naam en het Hallo-Resourcegroepnaam die al bestaan. Zorg er ook Hallo lokale pad en de bestandsnaam die u hier opgeeft, moeten al bestaan op Hallo-computer. Hallo codefragment volgen na de naamruimtedeclaraties Hallo toevoegen.

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

In de Hallo resterende secties van Hallo artikel, ziet u hoe toouse Hallo beschikbare .NET methoden tooperform bewerkingen zoals verificatie, uploaden, enz.

## <a name="authentication"></a>Authentication

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>Als u gebruikmaakt van verificatie door eindgebruikers (aanbevolen voor deze zelfstudie)

Gebruik deze met een bestaande Azure AD systeemeigen toepassing tooauthenticate uw toepassing **interactief**, dit betekent dat u wordt gevraagd tooenter uw Azure-referenties.

Hallo codefragment hieronder worden de standaardwaarden voor eenvoudig te gebruiken gebruikt voor client-ID en omleidings-URI die is voor een Azure-abonnement geschikt. toohelp u deze zelfstudie sneller zijn voltooid, wordt aangeraden gebruik van deze benadering. Hallo-codefragment hieronder, geeft u alleen Hallo-waarde voor uw tenant-ID. U kunt ophalen met behulp van de instructies op Hallo [maken van een Active Directory-toepassing](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Een aantal dingen tooknow over deze bovenstaande codefragment:

* in dit fragment maakt gebruik van toohelp u Hallo zelfstudie sneller zijn voltooid, een an Azure AD-domein en de client-ID die is standaard beschikbaar voor alle Azure-abonnementen. U kunt **dit fragment dus in zijn huidige vorm in uw toepassing gebruiken**.
* Echter, als u wilt dat toouse uw eigen Azure AD-domein en client-ID van toepassing, moet u een systeemeigen Azure AD-toepassing maken en vervolgens gebruik hello Azure AD-tenant-ID, client-ID en omleidings-URI voor de toepassing hello u gemaakt. Zie [Een Active Directory-toepassing voor verificatie van eindgebruikers maken met Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) voor instructies.

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>Als u gebruikmaakt van service-naar-serviceverificatie met clientgeheim
Hallo volgende codefragment gebruikte tooauthenticate uw toepassing kan worden **niet-interactief**, met behulp van het clientgeheim Hallo / sleutel voor een toepassing / service-principal. Gebruik dit met een bestaande Azure AD-toepassing voor webtoepassingen. Voor instructies over hoe toocreate hello Azure AD-webtoepassing en hoe tooretrieve Hallo van client-ID en clientgeheim vereist in Hallo codefragment hieronder, Zie [een Active Directory-toepassing voor verificatie van de service-naar-service maken met gegevens Lake Store](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>Als u gebruikmaakt van service-naar-serviceverificatie met certificaat

Een derde optie, hello volgende codefragment kan worden gebruikt tooauthenticate uw toepassing **niet-interactief**, met behulp van Hallo-certificaat voor een Azure Active Directory-toepassing / service principal. Gebruik dit met een bestaande [Azure AD-toepassing met certificaten](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>Clientobjecten maken
Hallo volgende fragment maakt Hallo Data Lake Store-account en bestandssysteem clientobjecten die worden gebruikt tooissue toohello serviceaanvraag.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Alle Data Lake Store-accounts binnen een abonnement weergeven
Hallo bevat volgende fragment alle Data Lake Store-accounts binnen een bepaald Azure-abonnement.

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

## <a name="create-a-directory"></a>Een map maken
Hallo volgende codefragment bevat een `CreateDirectory` methode waarmee u toocreate een map in een Data Lake Store-account kunt.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Bestand uploaden
Hallo volgende codefragment bevat een `UploadFile` methode waarmee u tooupload kunt bestanden tooa Data Lake Store-account.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Hallo SDK biedt ondersteuning voor recursieve uploaden en downloaden tussen een lokaal pad en een pad naar een Data Lake Store.    

## <a name="get-file-or-directory-info"></a>Bestands- of mapinformatie ophalen
Hallo volgende codefragment bevat een `GetItemInfo` methode die u kunt tooretrieve informatie over een bestand of mapinformatie die beschikbaar is in Data Lake Store te gebruiken.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Bestanden of mappen weergeven
Hallo volgende codefragment bevat een `ListItem` methode die toolist Hallo bestanden en mappen in een Data Lake Store-account kunt gebruiken.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Bestanden samenvoegen
Hallo volgende codefragment bevat een `ConcatenateFiles` methode tooconcatenate bestanden te gebruiken.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Toevoegen van tooa
Hallo volgende codefragment bevat een `AppendToFile` methode die u gebruikt tooa gegevensbestand al opgeslagen in een Data Lake Store-account toevoegen.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Bestand downloaden
Hallo volgende codefragment bevat een `DownloadFile` methode toodownload een bestand van een Data Lake Store-account te gebruiken.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Volgende stappen
* [Gegevens in Data Lake Store beveiligen](data-lake-store-secure-data.md)
* [Azure Data Lake Analytics gebruiken met Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight gebruiken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Naslaginformatie over Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Naslaginformatie over Data Lake Store REST](https://msdn.microsoft.com/library/mt693424.aspx)
