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
# <a name="how-toouse-azure-storage-in-windows-store-apps"></a>Hoe toouse Azure Storage in Windows Store-apps
## <a name="overview"></a>Overzicht
Deze handleiding wordt getoond hoe tooget gestart met het ontwikkelen van een Windows Store-app die gebruikmaakt van Azure Storage.

## <a name="download-required-tools"></a>Vereiste hulpprogramma's downloaden
* [Visual Studio](https://www.visualstudio.com/downloads/) maakt het eenvoudig toobuild voor foutopsporing, localize pakket- en Windows Store-apps implementeren. Visual Studio 2012 of hoger is vereist.
* Hallo [Azure Storage-clientbibliotheek](https://www.nuget.org/packages/WindowsAzure.Storage) vindt u een Windows Runtime-klassenbibliotheek voor het werken met Azure Storage.
* [WCF Data Services hulpprogramma's voor Windows Store-Apps](http://www.microsoft.com/download/details.aspx?id=30714) breidt Hallo Serviceverwijzing toevoegen ervaring met client-OData-ondersteuning voor Windows Store-apps in Visual Studio.

## <a name="develop-apps"></a>Apps ontwikkelen
### <a name="getting-ready"></a>Voorbereiding
Maak een nieuwe Windows Store-app-project in Visual Studio 2012 of hoger:

![Store-apps-opslag-vs-project][store-apps-storage-vs-project]

Vervolgens voegt u een verwijzing toohello Azure Storage-clientbibliotheek met de rechtermuisknop op **verwijzingen**, te klikken op **verwijzing toevoegen**, en vervolgens Bladeren toohello Storage Client-bibliotheek voor Windows Runtime die u hebt gedownload:

![Store-apps-opslag-Kies-bibliotheek][store-apps-storage-choose-library]

### <a name="using-hello-library-with-hello-blob-and-queue-services"></a>Gebruik Hallo Hallo Blob-bibliotheek en wachtrij-services
Uw app is nu gereed toocall hello Azure Blob en Queue-services. Voeg de volgende Hallo **met** instructies zodat Azure opslagtypen rechtstreeks kunnen worden verwezen:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Voeg vervolgens een knop tooyour pagina. Hallo na code tooits toevoegen **klikt u op** gebeurtenis en de gebeurtenis-handler-methode wijzigen met behulp van Hallo [async sleutelwoord](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Deze code wordt ervan uitgegaan dat u twee tekenreeksvariabelen hebt, *accountName* en *accountKey*. Ze staan Hallo-naam van uw account en Hallo opslagaccountsleutel die is gekoppeld aan dat account.

Toepassing bouwen en uitvoeren Hallo. Te klikken op Hallo-knop wordt gecontroleerd of er een container met de naam *container1* bestaat in uw account en deze als dat niet maken.

### <a name="using-hello-library-with-hello-table-service"></a>Met behulp van Hallo-bibliotheek Hello tabelservice
Typen die gebruikte toocommunicate met hello Azure Table-service is afhankelijk van WCF Data Services voor Hallo Windows Store-app-bibliotheek. Vervolgens voegt u dat een verwijzing toohello vereist WCF-bibliotheken via Hallo Package Manager-Console:

![Store-apps-opslag-pakket-manager][store-apps-storage-package-manager]

Gebruik Hallo opdracht toopoint Package Manager toohello locatie op uw computer te volgen:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Met deze opdracht worden automatisch toegevoegd aan alle vereiste verwijzingen tooyour project. Als u niet wilt dat toouse Hallo Package Manager-Console, kunt u Hallo WCF Data Services NuGet-map op uw lokale machine toohello lijst van pakket bronnen toevoegen en vervolgens Hallo verwijzing via Hallo-gebruikersinterface toevoegen, zoals beschreven in [beheren NuGet-pakketten gebruiken Hallo dialoogvenster](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Wanneer u verwijst naar Hallo WCF Data Services NuGet-pakket, Hallo-code op de knop wijzigen **klikt u op** gebeurtenis:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Deze code wordt gecontroleerd of een tabel met de naam *table1* bestaat in uw account en maakt als dit niet.

U kunt ook een tooMicrosoft.WindowsAzure.Storage.Table.dll verwijzing toevoegen die beschikbaar is in Hallo dezelfde pakket dat u hebt gedownload. Deze bibliotheek bevat aanvullende functionaliteit, zoals serialisatie op basis van reflectie en algemene query's. Houd er rekening mee dat deze bibliotheek geen JavaScript ondersteunt.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
