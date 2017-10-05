---
title: Azure storage in Windows Store-apps gebruiken | Microsoft Docs
description: Informatie over het maken van een Windows Store-app die gebruikmaakt van Azure Blob, Queue, Table of bestand opslag.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 63c4b29d-b2f2-4d7c-b164-a0d38f4d14f6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 43d38584270fbbbe6fa4e4ff8cef72ca44e14acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a><span data-ttu-id="90645-103">Het gebruik van Azure Storage in Windows Store-apps</span><span class="sxs-lookup"><span data-stu-id="90645-103">How to use Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="90645-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="90645-104">Overview</span></span>
<span data-ttu-id="90645-105">Deze handleiding wordt beschreven hoe u aan de slag met het ontwikkelen van een Windows Store-app die gebruikmaakt van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="90645-105">This guide shows how to get started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="90645-106">Vereiste hulpprogramma's downloaden</span><span class="sxs-lookup"><span data-stu-id="90645-106">Download required tools</span></span>
* <span data-ttu-id="90645-107">[Visual Studio](https://www.visualstudio.com/downloads/) kunt u gemakkelijk bouwen, foutopsporing, localize, verpakken en Windows Store-apps implementeren.</span><span class="sxs-lookup"><span data-stu-id="90645-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy to build, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="90645-108">Visual Studio 2012 of hoger is vereist.</span><span class="sxs-lookup"><span data-stu-id="90645-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="90645-109">De [Azure Storage-clientbibliotheek](https://www.nuget.org/packages/WindowsAzure.Storage) vindt u een Windows Runtime-klassenbibliotheek voor het werken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="90645-109">The [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="90645-110">[WCF Data Services hulpprogramma's voor Windows Store-Apps](http://www.microsoft.com/download/details.aspx?id=30714) breidt de ervaring voor de Serviceverwijzing toevoegen aan clientzijde OData-ondersteuning voor Windows Store-apps in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90645-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends the Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="90645-111">Apps ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="90645-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="90645-112">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="90645-112">Getting ready</span></span>
<span data-ttu-id="90645-113">Maak een nieuwe Windows Store-app-project in Visual Studio 2012 of hoger:</span><span class="sxs-lookup"><span data-stu-id="90645-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![Store-apps-opslag-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="90645-115">Voeg een verwijzing naar de Azure Storage-clientbibliotheek vervolgens toe met de rechtermuisknop op **verwijzingen**, te klikken op **verwijzing toevoegen**, en vervolgens Bladeren naar de bibliotheek met Client-opslag voor Windows Runtime die u hebt gedownload:</span><span class="sxs-lookup"><span data-stu-id="90645-115">Next, add a reference to the Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing to the Storage Client Library for Windows Runtime that you downloaded:</span></span>

![Store-apps-opslag-Kies-bibliotheek][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a><span data-ttu-id="90645-117">Met behulp van de bibliotheek met de services Blob en wachtrij</span><span class="sxs-lookup"><span data-stu-id="90645-117">Using the library with the Blob and Queue services</span></span>
<span data-ttu-id="90645-118">Uw app is nu gereed voor aanroepen van de Azure-Blob en Queue-services.</span><span class="sxs-lookup"><span data-stu-id="90645-118">At this point, your app is ready to call the Azure Blob and Queue services.</span></span> <span data-ttu-id="90645-119">Voeg de volgende **met** instructies zodat Azure opslagtypen rechtstreeks kunnen worden verwezen:</span><span class="sxs-lookup"><span data-stu-id="90645-119">Add the following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="90645-120">Voeg een knop vervolgens toe aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="90645-120">Next, add a button to your page.</span></span> <span data-ttu-id="90645-121">Voeg de volgende code naar de **klikt u op** gebeurtenis en de gebeurtenis-handler-methode wijzigen met behulp van de [async sleutelwoord](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="90645-121">Add the following code to its **Click** event and modify your event handler method by using the [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="90645-122">Deze code wordt ervan uitgegaan dat u twee tekenreeksvariabelen hebt, *accountName* en *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="90645-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="90645-123">Ze staan voor de naam van uw storage-account en -sleutel die is gekoppeld aan dat account.</span><span class="sxs-lookup"><span data-stu-id="90645-123">They represent the name of your storage account and the account key that is associated with that account.</span></span>

<span data-ttu-id="90645-124">Ontwikkel en voer de toepassing.</span><span class="sxs-lookup"><span data-stu-id="90645-124">Build and run the application.</span></span> <span data-ttu-id="90645-125">Op de knop wordt gecontroleerd of er een container met de naam *container1* bestaat in uw account en deze als dat niet maken.</span><span class="sxs-lookup"><span data-stu-id="90645-125">Clicking the button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-the-library-with-the-table-service"></a><span data-ttu-id="90645-126">Met behulp van de bibliotheek met de tabel-service</span><span class="sxs-lookup"><span data-stu-id="90645-126">Using the library with the Table service</span></span>
<span data-ttu-id="90645-127">Typen die worden gebruikt om te communiceren met de Azure Table-service is afhankelijk van WCF Data Services voor de Windows Store-app-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="90645-127">Types that are used to communicate with the Azure Table service depend on WCF Data Services for the Windows Store app library.</span></span> <span data-ttu-id="90645-128">Voeg een verwijzing naar de vereiste WCF-bibliotheken vervolgens toe met behulp van de Package Manager-Console:</span><span class="sxs-lookup"><span data-stu-id="90645-128">Next, add a reference to the required WCF libraries by using the Package Manager Console:</span></span>

![Store-apps-opslag-pakket-manager][store-apps-storage-package-manager]

<span data-ttu-id="90645-130">Gebruik de volgende opdracht om punt Package Manager naar de locatie op uw computer:</span><span class="sxs-lookup"><span data-stu-id="90645-130">Use the following command to point Package Manager to the location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="90645-131">Met deze opdracht worden automatisch toegevoegd aan alle vereiste referenties aan uw project.</span><span class="sxs-lookup"><span data-stu-id="90645-131">This command will automatically add all required references to your project.</span></span> <span data-ttu-id="90645-132">Als u niet de Package Manager-Console gebruiken wilt, kunt u de WCF Data Services NuGet-map op uw lokale computer toevoegen aan de lijst met bronnen van pakket en voegt u de verwijzing via de gebruikersinterface, zoals beschreven in [beheren NuGet-pakketten met behulp van het dialoogvenster ](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="90645-132">If you do not want to use the Package Manager Console, you can add the WCF Data Services NuGet folder on your local machine to the list of package sources and then add the reference through the UI, as described in [Managing NuGet Packages Using the Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="90645-133">Wanneer u verwijst naar het WCF Data Services NuGet-pakket, wijzigt u de code in uw knop **klikt u op** gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="90645-133">When you have referenced the WCF Data Services NuGet package, change the code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="90645-134">Deze code wordt gecontroleerd of een tabel met de naam *table1* bestaat in uw account en maakt als dit niet.</span><span class="sxs-lookup"><span data-stu-id="90645-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="90645-135">U kunt ook een verwijzing naar Microsoft.WindowsAzure.Storage.Table.dll, toevoegen die beschikbaar is in hetzelfde pakket die u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="90645-135">You can also add a reference to Microsoft.WindowsAzure.Storage.Table.dll, which is available in the same package that you downloaded.</span></span> <span data-ttu-id="90645-136">Deze bibliotheek bevat aanvullende functionaliteit, zoals serialisatie op basis van reflectie en algemene query's.</span><span class="sxs-lookup"><span data-stu-id="90645-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="90645-137">Houd er rekening mee dat deze bibliotheek geen JavaScript ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="90645-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
