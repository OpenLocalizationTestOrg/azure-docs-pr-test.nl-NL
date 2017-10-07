---
title: aaaUse Azure Batch-API's en hulpprogramma's toodevelop grootschalige parallelle verwerking oplossingen | Microsoft Docs
description: Meer informatie over Hallo API's en hulpprogramma's voor het ontwikkelen van oplossingen met hello Azure Batch-service.
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: get-started-article
ms.date: 03/08/2017
ms.author: tamram
ms.openlocfilehash: ca75a1a63b3e7e6b0805e79a63685bc49aaaca8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-batch-apis-and-tools"></a>Overzicht van Batch-API's en -hulpprogramma's

Verwerking van parallelle workloads met Azure Batch gewoonlijk wordt uitgevoerd via een programma met behulp van een Hallo [Batch-API's](#batch-development-apis). Uw clienttoepassing of service kunt Hallo Batch-API's toocommunicate met Hallo Batch-service gebruiken. Met de Hallo Batch-API's, kunt u maken en beheren van pools van rekenknooppunten, virtuele machines of cloudservices. Vervolgens kunt u jobs en taken toorun op die knooppunten plannen. 

U kunt efficiënt grootschalige workloads verwerken voor uw organisatie of bieden een service-front-end tooyour klanten, zodat ze kunnen worden uitgevoerd jobs en taken--op aanvraag of volgens een schema--op één, honderden of zelfs duizenden knooppunten. U kunt Azure Batch ook gebruiken als onderdeel van een grotere werkstroom, beheerd door hulpprogramma's zoals [Azure Data Factory](../data-factory/data-factory-data-processing-using-batch.md?toc=%2fazure%2fbatch%2ftoc.json).

> [!TIP]
> Wanneer u klaar bent toodig in toohello Batch-API voor een uitgebreidere kennis van Hallo deze functies biedt, bekijk Hallo [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md).
> 
> 

## <a name="azure-accounts-for-batch-development"></a>Azure-accounts voor Batch-ontwikkeling
Wanneer u Batch-oplossingen ontwikkelt, gebruikt u Hallo accounts in Microsoft Azure te volgen.

* **Azure-account en -abonnement**: als u nog geen Azure-abonnement hebt, kunt u uw [voordelen als MSDN-abonnee][msdn_benefits] activeren of u aanmelden voor een [gratis Azure-account][free_account]. Wanneer u een account maakt, wordt voor u een standaardabonnement gemaakt.
* **Batch-account**: Batch-resources zoals pools, rekenknooppunten, jobs en taken worden aan een Azure Batch-account gekoppeld. Wanneer uw toepassing een aanvraag in voor Hallo Batch-service maakt, verifieert het Hallo-aanvraag met hello Azure Batch-accountnaam, URL op Hallo van Hallo-account en een toegangssleutel. U kunt [Batch-account maken](batch-account-create-portal.md) in hello Azure-portal.
* **Storage-account**: Batch bevat ingebouwde ondersteuning voor het werken met bestanden in [Azure Storage][azure_storage]. Vrijwel elk Batch-scenario gebruikt Azure Blob-opslag voor het Faseren van Hallo-programma's die de taken worden uitgevoerd en Hallo-gegevens die zij verwerken, en voor Hallo opslag van uitvoergegevens die zij genereren. een opslagaccount toocreate Zie [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).

## <a name="batch-service-apis"></a>API’s voor Batch-service

Uw toepassingen en services kunnen rechtstreekse REST-API-aanroepen uitgeven of een of meer van de volgende client-bibliotheken toorun hello gebruiken en beheren van uw Azure Batch-workloads.

| API | API-verwijzing | Download | Zelfstudie | Codevoorbeelden | Meer informatie |
| --- | --- | --- | --- | --- | --- |
| **Batch REST** |[MSDN][batch_rest] |N.v.t. |- |- | [Ondersteunde versies](https://docs.microsoft.com/rest/api/batchservice/batch-service-rest-api-versioning) |
| **Batch .NET** |[docs.microsoft.com][api_net] |[NuGet ][api_net_nuget] |[Zelfstudie](batch-dotnet-get-started.md) |[GitHub][api_sample_net] | [Releaseopmerkingen](http://aka.ms/batch-net-dataplane-changelog) |
| **Batch Python** |[readthedocs.io][api_python] |[PyPI][api_python_pypi] |[Zelfstudie](batch-python-tutorial.md)|[GitHub][api_sample_python] | [Leesmij](https://github.com/Azure/azure-sdk-for-python/blob/master/doc/batch.rst) |
| **Batch Node.js** |[github.io][api_nodejs] |[npm][api_nodejs_npm] |- |- | [Leesmij](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/batch) |
| **Batch Java** |[github.io][api_java] |[Maven][api_java_jar] |- |[Leesmij][api_sample_java] | [Leesmij](https://github.com/Azure/azure-batch-sdk-for-java)|

## <a name="batch-management-apis"></a>API’s voor Batch Management

Hello Azure Resource Manager-API's voor Batch bieden toegang op programmeerniveau tooBatch accounts. Met deze API's kunt u programmatisch Batch-accounts, quota en toepassingspakketten beheren.  

| API | API-verwijzing | Download | Zelfstudie | Codevoorbeelden |
| --- | --- | --- | --- | --- |
| **Batch Resource Manager REST** |[docs.microsoft.com][api_rest_mgmt] |N.v.t. |- |[GitHub](https://github.com/Azure-Samples/batch-dotnet-manage-batch-accounts) |
| **Batch Resource Manager .NET** |[docs.microsoft.com][api_net_mgmt] |[NuGet ][api_net_mgmt_nuget] | [Zelfstudie](batch-management-dotnet.md) |[GitHub][api_sample_net] |

## <a name="batch-command-line-tools"></a>Batch-opdrachtregelprogramma's

Deze opdrachtregelprogramma's bieden dezelfde functionaliteit Hallo zoals Hallo Batch-service en de Batch-API's voor beheer: 

* [Batch PowerShell-cmdlets][batch_ps]: Azure Batch-cmdlets in Hallo Hallo [Azure PowerShell](/powershell/azure/overview) module kunt u toomanage Batch-resources met PowerShell.
* [Azure CLI](/cli/azure/overview): hello Azure-opdrachtregelinterface (Azure CLI) is een platformoverschrijdende hulpmiddelenset die shellopdrachten biedt voor interactie met vele Azure-services, waaronder Hallo Batch-service en de Batch-Management-service. Zie [beheren Batch-resources met Azure CLI](batch-cli-get-started.md) voor meer informatie over het gebruik van Azure CLI Hallo met Batch.

## <a name="other-tools-for-application-development"></a>Andere hulpmiddelen voor toepassingsontwikkeling

Hier volgen enkele extra hulpprogramma's die mogelijk nuttig zijn voor het bouwen van uw Batch-toepassingen en -services en het opsporen van fouten daarin:

* [Azure-portal][portal]: U kunt maken, bewaken en verwijderen van de Batch-pools, jobs en taken in hello Azure-portal-blades voor Batch. U kunt Hallo statusinformatie over deze en andere resources bekijken terwijl u uw taken uitvoeren, en zelfs bestanden van Hallo rekenknooppunten in uw pools downloaden. U kunt bijvoorbeeld de `stderr.txt` van een taak downloaden bij het oplossen van problemen. U kunt ook Remote Desktop (RDP)-bestanden waarmee u toolog in toocompute knooppunten kunt downloaden.
* [Azure Batch Explorer][batch_explorer]: Batch Explorer vergelijkbare functionaliteit biedt als Batch resource management zoals hello Azure-portal, maar in een zelfstandige toepassing voor Windows Presentation Foundation (WPF)-client. Een van de Hallo Batch .NET-voorbeeldtoepassingen beschikbaar op [GitHub][github_samples], kunt u samenstellen met Visual Studio 2015 of hoger en toobrowse gebruiken en beheren van Hallo resources in uw Batch-account bij het ontwikkelen van en fouten opsporen in uw Batch-oplossingen. Taak weergeven, toepassingen en taakdetails, download bestanden van rekenknooppunten en toonodes op afstand verbinding maken met behulp van extern bureaublad (RDP)-bestanden die kunt u downloaden met Batch Explorer.
* [Microsoft Azure Storage Explorer][storage_explorer]: tijdens het niet strikt in een Azure Batch-hulpprogramma Hallo Storage Explorer een ander waardevol hulpmiddel toohave is bij de ontwikkeling en foutopsporing van uw Batch-oplossingen.

## <a name="additional-resources"></a>Aanvullende bronnen

- Zie toolearn over het vastleggen van gebeurtenissen van uw toepassing Batch [gebeurtenissen voor diagnostische evaluatie en bewaking van Batch-oplossingen](batch-diagnostics.md). Zie voor een overzicht van gebeurtenissen die worden gegenereerd door de Batch-service Hallo [Batch Analytics](batch-analytics.md).
- Zie [Omgevingsvariabelen van Azure Batch-rekenknooppunten](batch-compute-node-environment-variables.md) voor meer informatie over omgevingsvariabelen voor rekenknooppunten.

## <a name="next-steps"></a>Volgende stappen

* Lees Hallo [overzicht van de Batch-functies voor ontwikkelaars](batch-api-basics.md), essentiële informatie voor iedereen toouse Batch voorbereiden. Hallo artikel bevat meer gedetailleerde informatie over Batch-service-resources zoals pools, knooppunten, jobs en taken en Hallo veel API-functies die u tijdens het bouwen van uw Batch-toepassing kunt gebruiken.
* [Aan de slag met hello Azure Batch-bibliotheek voor .NET](batch-dotnet-get-started.md) toolearn hoe toouse C# en Hallo Batch .NET-bibliotheek tooexecute een eenvoudige werkbelasting gebruik van een algemene Batch-werkstroom. In dit artikel moet een van uw eerste reageert tijdens het leren hoe toouse Hallo Batch-service. Er is ook een [Python-versie](batch-python-tutorial.md) van Hallo zelfstudie.
* Hallo downloaden [codevoorbeelden op GitHub] [ github_samples] toosee hoe zowel C# en Python kan verbinding maken met de Batch tooschedule en proces voorbeeld werkbelastingen.
* Bekijk Hallo [Batch-Leertraject] [ learning_path] tooget een idee van Hallo resources beschikbaar tooyou als u meer informatie over toowork met Batch.


[azure_storage]: https://azure.microsoft.com/services/storage/
[api_java]: http://azure.github.io/azure-sdk-for-java/
[api_java_jar]: http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-batch%22
[api_net]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_nuget]: https://www.nuget.org/packages/Azure.Batch/
[api_rest_mgmt]: https://docs.microsoft.com/\rest/api/batchmanagement/
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_net_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[api_nodejs]: http://azure.github.io/azure-sdk-for-node/azure-batch/latest/
[api_nodejs_npm]: https://www.npmjs.com/package/azure-batch
[api_python]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html
[api_python_pypi]: https://pypi.python.org/pypi/azure-batch
[api_sample_net]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp
[api_sample_python]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[api_sample_java]: https://github.com/Azure/azure-batch-samples/tree/master/Java/
[batch_ps]: /powershell/resourcemanager/azurerm.batch/v2.7.0/azurerm.batch
[batch_rest]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[free_account]: https://azure.microsoft.com/free/
[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[msdn_benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[storage_explorer]: http://storageexplorer.com/
[portal]: https://portal.azure.com
