---
title: aaaUse Azure storage in Windows Store-apps | Microsoft Docs
description: Meer informatie over hoe toocreate een Windows Store-app die gebruikmaakt van Azure Blob, Queue, Table of bestand opslag.
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
ms.openlocfilehash: ac21b0695c0d77c1d81c1b921718fb929945d45e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a><span data-ttu-id="c7dc9-103">Hoe toouse Azure Storage in Windows Store-apps</span><span class="sxs-lookup"><span data-stu-id="c7dc9-103">How toouse Azure Storage in Windows Store apps</span></span>
## <a name="overview"></a><span data-ttu-id="c7dc9-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c7dc9-104">Overview</span></span>
<span data-ttu-id="c7dc9-105">Deze handleiding wordt getoond hoe tooget gestart met het ontwikkelen van een Windows Store-app die gebruikmaakt van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-105">This guide shows how tooget started with developing a Windows Store app that makes use of Azure Storage.</span></span>

## <a name="download-required-tools"></a><span data-ttu-id="c7dc9-106">Vereiste hulpprogramma's downloaden</span><span class="sxs-lookup"><span data-stu-id="c7dc9-106">Download required tools</span></span>
* <span data-ttu-id="c7dc9-107">[Visual Studio](https://www.visualstudio.com/downloads/) maakt het eenvoudig toobuild voor foutopsporing, localize pakket- en Windows Store-apps implementeren.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-107">[Visual Studio](https://www.visualstudio.com/downloads/) makes it easy toobuild, debug, localize, package, and deploy Windows Store apps.</span></span> <span data-ttu-id="c7dc9-108">Visual Studio 2012 of hoger is vereist.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-108">Visual Studio 2012 or later is required.</span></span>
* <span data-ttu-id="c7dc9-109">Hallo [Azure Storage-clientbibliotheek](https://www.nuget.org/packages/WindowsAzure.Storage) vindt u een Windows Runtime-klassenbibliotheek voor het werken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-109">hello [Azure Storage Client Library](https://www.nuget.org/packages/WindowsAzure.Storage) provides a Windows Runtime class library for working with Azure Storage.</span></span>
* <span data-ttu-id="c7dc9-110">[WCF Data Services hulpprogramma's voor Windows Store-Apps](http://www.microsoft.com/download/details.aspx?id=30714) breidt Hallo Serviceverwijzing toevoegen ervaring met client-OData-ondersteuning voor Windows Store-apps in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-110">[WCF Data Services Tools for Windows Store Apps](http://www.microsoft.com/download/details.aspx?id=30714) extends hello Add Service Reference experience with client-side OData support for Windows Store apps in Visual Studio.</span></span>

## <a name="develop-apps"></a><span data-ttu-id="c7dc9-111">Apps ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="c7dc9-111">Develop apps</span></span>
### <a name="getting-ready"></a><span data-ttu-id="c7dc9-112">Voorbereiding</span><span class="sxs-lookup"><span data-stu-id="c7dc9-112">Getting ready</span></span>
<span data-ttu-id="c7dc9-113">Maak een nieuwe Windows Store-app-project in Visual Studio 2012 of hoger:</span><span class="sxs-lookup"><span data-stu-id="c7dc9-113">Create a new Windows Store app project in Visual Studio 2012 or later:</span></span>

![Store-apps-opslag-vs-project][store-apps-storage-vs-project]

<span data-ttu-id="c7dc9-115">Vervolgens voegt u een verwijzing toohello Azure Storage-clientbibliotheek met de rechtermuisknop op **verwijzingen**, te klikken op **verwijzing toevoegen**, en vervolgens Bladeren toohello Storage Client-bibliotheek voor Windows Runtime die u hebt gedownload:</span><span class="sxs-lookup"><span data-stu-id="c7dc9-115">Next, add a reference toohello Azure Storage Client Library by right-clicking **References**, clicking **Add Reference**, and then browsing toohello Storage Client Library for Windows Runtime that you downloaded:</span></span>

![Store-apps-opslag-Kies-bibliotheek][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a><span data-ttu-id="c7dc9-117">Gebruik Hallo Hallo Blob-bibliotheek en wachtrij-services</span><span class="sxs-lookup"><span data-stu-id="c7dc9-117">Using hello library with hello Blob and Queue services</span></span>
<span data-ttu-id="c7dc9-118">Uw app is nu gereed toocall hello Azure Blob en Queue-services.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-118">At this point, your app is ready toocall hello Azure Blob and Queue services.</span></span> <span data-ttu-id="c7dc9-119">Voeg de volgende Hallo **met** instructies zodat Azure opslagtypen rechtstreeks kunnen worden verwezen:</span><span class="sxs-lookup"><span data-stu-id="c7dc9-119">Add hello following **using** statements so that Azure Storage types can be referenced directly:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

<span data-ttu-id="c7dc9-120">Voeg vervolgens een knop tooyour pagina.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-120">Next, add a button tooyour page.</span></span> <span data-ttu-id="c7dc9-121">Hallo na code tooits toevoegen **klikt u op** gebeurtenis en de gebeurtenis-handler-methode wijzigen met behulp van Hallo [async sleutelwoord](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span><span class="sxs-lookup"><span data-stu-id="c7dc9-121">Add hello following code tooits **Click** event and modify your event handler method by using hello [async keyword](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

<span data-ttu-id="c7dc9-122">Deze code wordt ervan uitgegaan dat u twee tekenreeksvariabelen hebt, *accountName* en *accountKey*.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-122">This code assumes that you have two string variables, *accountName* and *accountKey*.</span></span> <span data-ttu-id="c7dc9-123">Ze staan Hallo-naam van uw account en Hallo opslagaccountsleutel die is gekoppeld aan dat account.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-123">They represent hello name of your storage account and hello account key that is associated with that account.</span></span>

<span data-ttu-id="c7dc9-124">Toepassing bouwen en uitvoeren Hallo.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-124">Build and run hello application.</span></span> <span data-ttu-id="c7dc9-125">Te klikken op Hallo-knop wordt gecontroleerd of er een container met de naam *container1* bestaat in uw account en deze als dat niet maken.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-125">Clicking hello button will check whether a container named *container1* exists in your account and then create it if not.</span></span>

### <a name="using-hello-library-with-hello-table-service"></a><span data-ttu-id="c7dc9-126">Met behulp van Hallo-bibliotheek Hello tabelservice</span><span class="sxs-lookup"><span data-stu-id="c7dc9-126">Using hello library with hello Table service</span></span>
<span data-ttu-id="c7dc9-127">Typen die gebruikte toocommunicate met hello Azure Table-service is afhankelijk van WCF Data Services voor Hallo Windows Store-app-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-127">Types that are used toocommunicate with hello Azure Table service depend on WCF Data Services for hello Windows Store app library.</span></span> <span data-ttu-id="c7dc9-128">Vervolgens voegt u dat een verwijzing toohello vereist WCF-bibliotheken via Hallo Package Manager-Console:</span><span class="sxs-lookup"><span data-stu-id="c7dc9-128">Next, add a reference toohello required WCF libraries by using hello Package Manager Console:</span></span>

![Store-apps-opslag-pakket-manager][store-apps-storage-package-manager]

<span data-ttu-id="c7dc9-130">Gebruik Hallo opdracht toopoint Package Manager toohello locatie op uw computer te volgen:</span><span class="sxs-lookup"><span data-stu-id="c7dc9-130">Use hello following command toopoint Package Manager toohello location on your machine:</span></span>

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

<span data-ttu-id="c7dc9-131">Met deze opdracht worden automatisch toegevoegd aan alle vereiste verwijzingen tooyour project.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-131">This command will automatically add all required references tooyour project.</span></span> <span data-ttu-id="c7dc9-132">Als u niet wilt dat toouse Hallo Package Manager-Console, kunt u Hallo WCF Data Services NuGet-map op uw lokale machine toohello lijst van pakket bronnen toevoegen en vervolgens Hallo verwijzing via Hallo-gebruikersinterface toevoegen, zoals beschreven in [beheren NuGet-pakketten gebruiken Hallo dialoogvenster](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span><span class="sxs-lookup"><span data-stu-id="c7dc9-132">If you do not want toouse hello Package Manager Console, you can add hello WCF Data Services NuGet folder on your local machine toohello list of package sources and then add hello reference through hello UI, as described in [Managing NuGet Packages Using hello Dialog](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).</span></span>

<span data-ttu-id="c7dc9-133">Wanneer u verwijst naar Hallo WCF Data Services NuGet-pakket, Hallo-code op de knop wijzigen **klikt u op** gebeurtenis:</span><span class="sxs-lookup"><span data-stu-id="c7dc9-133">When you have referenced hello WCF Data Services NuGet package, change hello code in your button's **Click** event:</span></span>

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

<span data-ttu-id="c7dc9-134">Deze code wordt gecontroleerd of een tabel met de naam *table1* bestaat in uw account en maakt als dit niet.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-134">This code checks whether a table named *table1* exists in your account, and then creates it if not.</span></span>

<span data-ttu-id="c7dc9-135">U kunt ook een tooMicrosoft.WindowsAzure.Storage.Table.dll verwijzing toevoegen die beschikbaar is in Hallo dezelfde pakket dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-135">You can also add a reference tooMicrosoft.WindowsAzure.Storage.Table.dll, which is available in hello same package that you downloaded.</span></span> <span data-ttu-id="c7dc9-136">Deze bibliotheek bevat aanvullende functionaliteit, zoals serialisatie op basis van reflectie en algemene query's.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-136">This library contains additional functionality, such as reflection-based serialization and generic queries.</span></span> <span data-ttu-id="c7dc9-137">Houd er rekening mee dat deze bibliotheek geen JavaScript ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="c7dc9-137">Note that this library does not support JavaScript.</span></span>

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
