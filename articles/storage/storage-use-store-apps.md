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
# <a name="how-to-use-azure-storage-in-windows-store-apps"></a>Het gebruik van Azure Storage in Windows Store-apps
## <a name="overview"></a>Overzicht
Deze handleiding wordt beschreven hoe u aan de slag met het ontwikkelen van een Windows Store-app die gebruikmaakt van Azure Storage.

## <a name="download-required-tools"></a>Vereiste hulpprogramma's downloaden
* [Visual Studio](https://www.visualstudio.com/downloads/) kunt u gemakkelijk bouwen, foutopsporing, localize, verpakken en Windows Store-apps implementeren. Visual Studio 2012 of hoger is vereist.
* De [Azure Storage-clientbibliotheek](https://www.nuget.org/packages/WindowsAzure.Storage) vindt u een Windows Runtime-klassenbibliotheek voor het werken met Azure Storage.
* [WCF Data Services hulpprogramma's voor Windows Store-Apps](http://www.microsoft.com/download/details.aspx?id=30714) breidt de ervaring voor de Serviceverwijzing toevoegen aan clientzijde OData-ondersteuning voor Windows Store-apps in Visual Studio.

## <a name="develop-apps"></a>Apps ontwikkelen
### <a name="getting-ready"></a>Voorbereiding
Maak een nieuwe Windows Store-app-project in Visual Studio 2012 of hoger:

![Store-apps-opslag-vs-project][store-apps-storage-vs-project]

Voeg een verwijzing naar de Azure Storage-clientbibliotheek vervolgens toe met de rechtermuisknop op **verwijzingen**, te klikken op **verwijzing toevoegen**, en vervolgens Bladeren naar de bibliotheek met Client-opslag voor Windows Runtime die u hebt gedownload:

![Store-apps-opslag-Kies-bibliotheek][store-apps-storage-choose-library]

### <a name="using-the-library-with-the-blob-and-queue-services"></a>Met behulp van de bibliotheek met de services Blob en wachtrij
Uw app is nu gereed voor aanroepen van de Azure-Blob en Queue-services. Voeg de volgende **met** instructies zodat Azure opslagtypen rechtstreeks kunnen worden verwezen:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
```

Voeg een knop vervolgens toe aan de pagina. Voeg de volgende code naar de **klikt u op** gebeurtenis en de gebeurtenis-handler-methode wijzigen met behulp van de [async sleutelwoord](http://msdn.microsoft.com/library/vstudio/hh156513.aspx):

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var blobClient = account.CreateCloudBlobClient();
var container = blobClient.GetContainerReference("container1");
await container.CreateIfNotExistsAsync();
```

Deze code wordt ervan uitgegaan dat u twee tekenreeksvariabelen hebt, *accountName* en *accountKey*. Ze staan voor de naam van uw storage-account en -sleutel die is gekoppeld aan dat account.

Ontwikkel en voer de toepassing. Op de knop wordt gecontroleerd of er een container met de naam *container1* bestaat in uw account en deze als dat niet maken.

### <a name="using-the-library-with-the-table-service"></a>Met behulp van de bibliotheek met de tabel-service
Typen die worden gebruikt om te communiceren met de Azure Table-service is afhankelijk van WCF Data Services voor de Windows Store-app-bibliotheek. Voeg een verwijzing naar de vereiste WCF-bibliotheken vervolgens toe met behulp van de Package Manager-Console:

![Store-apps-opslag-pakket-manager][store-apps-storage-package-manager]

Gebruik de volgende opdracht om punt Package Manager naar de locatie op uw computer:

    Install-Package Microsoft.Data.OData.WindowsStore -Source "C:\Program Files (x86)\Microsoft WCF Data Services\5.0\bin\NuGet"

Met deze opdracht worden automatisch toegevoegd aan alle vereiste referenties aan uw project. Als u niet de Package Manager-Console gebruiken wilt, kunt u de WCF Data Services NuGet-map op uw lokale computer toevoegen aan de lijst met bronnen van pakket en voegt u de verwijzing via de gebruikersinterface, zoals beschreven in [beheren NuGet-pakketten met behulp van het dialoogvenster ](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog).

Wanneer u verwijst naar het WCF Data Services NuGet-pakket, wijzigt u de code in uw knop **klikt u op** gebeurtenis:

```csharp
var credentials = new StorageCredentials(accountName, accountKey);
var account = new CloudStorageAccount(credentials, true);
var tableClient = account.CreateCloudTableClient();
var table = tableClient.GetTableReference("table1");
await table.CreateIfNotExistsAsync();
```

Deze code wordt gecontroleerd of een tabel met de naam *table1* bestaat in uw account en maakt als dit niet.

U kunt ook een verwijzing naar Microsoft.WindowsAzure.Storage.Table.dll, toevoegen die beschikbaar is in hetzelfde pakket die u hebt gedownload. Deze bibliotheek bevat aanvullende functionaliteit, zoals serialisatie op basis van reflectie en algemene query's. Houd er rekening mee dat deze bibliotheek geen JavaScript ondersteunt.

[store-apps-storage-vs-project]: ./media/storage-use-store-apps/store-apps-storage-vs-project.png
[store-apps-storage-choose-library]: ./media/storage-use-store-apps/store-apps-storage-choose-library.png
[store-apps-storage-package-manager]: ./media/storage-use-store-apps/store-apps-storage-package-manager.png
