---
title: de resultaten van aaaPersist of Logboeken van jobs en taken tooa van gegevens voltooid store - Azure Batch | Microsoft Docs
description: Meer informatie over verschillende opties voor persistent maken uitvoergegevens van Batch-taken en taken. U kunt deze persistent maken gegevens tooAzure opslag of tooanother gegevens opslaan.
services: batch
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0b11e387f1694e1ce3e9573db7f6013f0154cad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-output"></a>Taken persistent maken

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Algemene voorbeelden van de taakuitvoer zijn:

- Bestanden die zijn gemaakt bij het Hallo taak processen invoergegevens.
- De logboekbestanden die zijn gekoppeld aan de uitvoering van de taak. 

In dit artikel beschrijft de verschillende opties voor persistent maken taak uitvoer en Hallo scenario's waarvoor elke optie is het meest geschikt.   

## <a name="about-hello-batch-file-conventions-standard"></a>Over Hallo Batch bestand conventies standaard

Batch definieert een optionele set conventies voor het benoemen van bestanden van de taak uitvoer in Azure Storage. Hallo [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) beschrijft deze overeenkomsten. Hallo bestand conventies standaard bepaalt Hallo namen van Hallo-container en blob doelpad in Azure Storage voor een bepaalde uitvoerbestand op basis van Hallo namen van de taak Hallo en.

Is tooyou of u toouse Hallo bestand conventies standard besluit voor de naamgeving van uw gegevens uitvoerbestanden. U kunt ook Hallo doelcontainer en blob naam, maar u wilt. Als u Hallo bestand conventies standaard gebruikt voor het benoemen van uitvoerbestanden, wordt de uitvoerbestanden beschikbaar voor weergave in Hallo zijn [Azure-portal][portal].

Er zijn enkele verschillende manieren waarop u Hallo bestand conventies standard kunt gebruiken:

- Als u Hallo Batch-service API toopersist uitvoerbestanden gebruikt, kunt u tooname bestemming containers en blobs op basis van toohello bestand conventies standaard. Hallo API van Batch-service kunt u de uitvoerbestanden toopersist van clientcode, zonder te wijzigen van uw taaktoepassing.
- Als u met .NET ontwikkelt, kunt u Hallo [bestand conventies van Azure Batch-bibliotheek voor .NET][nuget_package]. Een voordeel van het gebruik van deze bibliotheek is dat deze ondersteuning biedt voor het opvragen van de uitvoerbestanden op basis van tootheir-ID of het doel. Hallo ingebouwde opvragen functionaliteit maakt het eenvoudig tooaccess uitvoerbestanden van een clienttoepassing of van andere taken. Uw taaktoepassing moet echter gewijzigde toocall bestand Conventions-bibliotheek. Zie voor meer informatie, Hallo-verwijzing voor Hallo [bestand Conventions-bibliotheek voor .NET](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.aspx).
- Als u met een andere taal dan .NET ontwikkelt, kunt u Hallo bestand conventies standaard in uw toepassing implementeren.

## <a name="design-considerations-for-persisting-output"></a>Ontwerpoverwegingen voor het persistent maken uitvoer 

Overweeg bij het ontwerpen van uw Batch-oplossing Hallo volgende factoren gerelateerde toojob en taakuitvoer.

* **Levensduur van COMPUTE**: Compute knooppunten zijn vaak tijdelijke, met name in groepen voor automatisch schalen die zijn ingeschakeld. De uitvoer van een taak die wordt uitgevoerd op een knooppunt is alleen beschikbaar als Hallo knooppunt bestaat en alleen binnen de bewaarperiode van het Hallo die u hebt ingesteld voor het Hallo-taak. Als een taak wordt de uitvoer die u moet uitvoeren mogelijk nadat het Hallo-taak is voltooid, moet de uitvoer bestanden tooa duurzame store, zoals Azure Storage uploaden op Hallo-taak.

* **Opslag uitvoer**: Azure Storage wordt aanbevolen als gegevensopslag voor uitvoer van de taak, maar u kunt een duurzame opslag gebruiken. Schrijven van de taak uitvoer tooAzure is opslag geïntegreerd in Hallo API van Batch-service. Als u een andere vorm van duurzame opslag gebruikt, moet u toowrite Hallo toepassing logica toopersist uitvoer van de taak zelf.   

* **Ophalen van de uitvoer**: U kunt uitvoer van de taak ophalen rechtstreeks vanuit het Hallo-rekenknooppunten in uw pool, of van Azure Storage of een ander gegevensarchief als u taakuitvoer persistent hebt gemaakt. een taak tooretrieve-uitvoer rechtstreeks vanuit een rekenknooppunt moet u Hallo-bestandsnaam en de uitvoerlocatie op Hallo-knooppunt. Als u deze taak uitvoer tooAzure opslag persistent maken, moet u Hallo volledig pad toohello bestand in Azure Storage toodownload Hallo uitvoerbestanden Hello Azure-opslag-SDK.

* **Uitvoer weergeven**: wanneer u Batch-taak tooa in Azure portal en selecteert u een Hallo navigeert **bestanden op knooppunt**, krijgt u alle bestanden die zijn gekoppeld aan taak hello, niet alleen Hallo uitvoerbestanden u geïnteresseerd bent in. Bestanden op rekenknooppunten zijn weer beschikbaar terwijl Hallo knooppunt bestaat en alleen binnen Hallo bewaartijd voor bestanden die u hebt ingesteld voor de taak Hallo. tooview taak uitvoer dat u tooAzure opslag persistent hebt gemaakt, kunt u hello Azure-portal of een Azure Storage client-toepassing zoals Hallo [Azure Opslagverkenner][storage_explorer]. tooview uitvoergegevens in Azure Storage met Hallo portal of een ander hulpprogramma, moet u weten Hallo bestandslocatie en tooit rechtstreeks te navigeren.

## <a name="options-for-persisting-output"></a>Opties voor het persistent maken uitvoer

Afhankelijk van uw scenario moet u er een aantal verschillende manieren toopersist taakuitvoer zijn:

- Hallo Batch-service API gebruiken.  
- Gebruik Hallo bestand conventies van Batch-bibliotheek voor .NET.  
- Hallo Batch bestand conventies standaard in uw toepassing implementeren.
- Een aangepast bestand gegevensverplaatsing oplossing implementeren.

Hallo volgende secties wordt elke methode in meer detail beschreven.

### <a name="use-hello-batch-service-api"></a>Hallo Batch-service API gebruiken

Met versie 2017-05-01, Hallo Batch-service wordt ondersteuning toegevoegd voor uitvoerbestanden opgeven in Azure Storage voor taakgegevens wanneer u [toevoegen van een taak tooa](https://docs.microsoft.com/rest/api/batchservice/add-a-task-to-a-job) of [toevoegen van een verzameling taken tooa taak](https://docs.microsoft.com/rest/api/batchservice/add-a-collection-of-tasks-to-a-job).

Hallo API van Batch-service ondersteunt Azure Storage-account van de groepen die zijn gemaakt met de configuratie van de virtuele machine Hallo persistent maken taak gegevens tooan. Met Hallo API van Batch-service, kunt u taakgegevens behouden zonder te wijzigen Hallo-toepassing die de taak wordt uitgevoerd. U kunt eventueel voldoen toohello [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) voor het benoemen van bestanden Hallo dat u deze persistent maken tooAzure opslag. 

Gebruik Hallo API van Batch-service toopersist taak uitvoer wanneer:

- U wilt gegevens van Batch-taken en jobbeheertaken in groepen die zijn gemaakt met de configuratie van de virtuele machine Hallo toopersist.
- Wilt u gegevens tooan Azure Storage-container met een willekeurige naam toopersist.
- Gewenste toopersist gegevens tooan Azure Storage-container met de naam volgens toohello [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

> [!NOTE]
> Hallo API van Batch-service biedt geen ondersteuning voor vastleggen van gegevens van de taken die worden uitgevoerd in groepen die zijn gemaakt met Hallo cloud service-configuratie. Zie voor meer informatie over persistent maken taak de uitvoer van groepen met Hallo cloud services-configuratie [taak en gegevens tooAzure opslag met Hallo Batch bestand Conventions-bibliotheek voor .NET toopersist behouden](batch-task-output-file-conventions.md)
> 
> 

Zie voor meer informatie over persistent maken uitvoer van de taak met Batch-service API Hallo [taak gegevens tooAzure opslag Hello API van Batch-service behouden](batch-task-output-files.md). Zie ook Hallo [PersistOutputs] [github_persistoutputs] steekproef project op GitHub, waaruit blijkt hoe toouse Hallo Batch-clientbibliotheek voor .NET toopersist taak toodurable opslag uitvoer.

### <a name="use-hello-batch-file-conventions-library-for-net"></a>Gebruik Hallo bestand conventies van Batch-bibliotheek voor .NET

Batch-oplossingen met C# en .NET-ontwikkelaars kunnen gebruiken Hallo [bestand Conventions-bibliotheek voor .NET] [ nuget_package] toopersist taak gegevens tooan Azure Storage-account op basis van toohello [batchbestand Standaard conventies](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Hallo bestand Conventions-bibliotheek verplaatsen uitvoer bestanden tooAzure opslag en naming bestemming containers en blobs op een bekende manier verwerkt.

Hallo bestand conventies bibliotheek ondersteunt uitvoerbestanden met ID of doel opvragen, voltooien zodat u eenvoudig toolocate ze zonder Hallo bestand URI's. 

Gebruik Hallo bestand conventies van Batch-bibliotheek voor .NET toopersist taak uitvoer wanneer:

- Gewenste toostream gegevens tooAzure opslag terwijl Hallo taak nog actief.
- Wilt u toopersist gegevens uit toepassingen die zijn gemaakt met Hallo cloud serviceconfiguratie of Hallo Virtuele-machineconfiguratie.
- Uw clienttoepassing of andere taken in Hallo van behoeften toolocate taken en downloaden van de taak uitvoerbestanden ID of met het doel. 
- Wilt u tooperform selectievakje wijzen of vroeg uploaden van de eerste resultaten.
- Wilt u de taakuitvoer tooview in hello Azure-portal.

Zie voor meer informatie over persistent maken van de taakuitvoer met Hallo bestand Conventions-bibliotheek voor .NET [behouden van de taak en gegevens tooAzure opslag met Hallo Batch bestand Conventions-bibliotheek voor .NET toopersist ](batch-task-output-file-conventions.md). Zie ook Hallo [PersistOutputs] [github_persistoutputs] steekproef project op GitHub, waaruit blijkt hoe toouse Hallo bestand Conventions-bibliotheek voor .NET toopersist taak toodurable opslag uitvoer.

Hallo [PersistOutputs] [github_persistoutputs]-voorbeeldproject op GitHub laat zien hoe toouse Hallo Batch-clientbibliotheek voor .NET toopersist taak toodurable opslag uitvoer.

### <a name="implement-hello-batch-file-conventions-standard"></a>Hallo Batch bestand conventies standaard implementeren

Als u een andere taal dan .NET gebruikt, kunt u Hallo implementeren [Batch bestand conventies standaard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) in uw eigen toepassing. 

U kunt tooimplement Hallo bestand conventies naamgevingsnorm zelf als u wilt dat een schematische naam beproefde of als u wilt dat de taakuitvoer tooview in hello Azure-portal.

### <a name="implement-a-custom-file-movement-solution"></a>Een aangepast bestand gegevensverplaatsing oplossing implementeren

U kunt ook uw eigen volledig bestand gegevensverplaatsing oplossing implementeren. Gebruik deze benadering wanneer:

- Wilt u toopersist taak gegevens tooa ander gegevensarchief dan Azure Storage. tooupload bestanden tooa gegevensarchief zoals Azure SQL- of Azure DataLake, kunt u een aangepast script of uitvoerbare tooupload toothat locatie. U kunt deze vervolgens aanroepen op Hallo vanaf de opdrachtregel na het uitvoeren van uw primaire uitvoerbaar bestand. Bijvoorbeeld op een knooppunt Windows kunt u deze twee opdrachten aanroepen:`doMyWork.exe && uploadMyFilesToSql.exe`
- Wilt u tooperform selectievakje wijzen of vroeg uploaden van de eerste resultaten.
- Wilt u toomaintain gedetailleerde controle over het afhandelen van fouten. U kunt bijvoorbeeld uw eigen oplossing als u wilt dat toouse taak afhankelijkheid acties tootake bepaalde acties op basis van specifieke taak afsluitcodes uploaden tooimplement. Zie voor meer informatie over afhankelijkheid Taakacties [taakafhankelijkheden toorun taken maken die afhankelijk van andere taken zijn](batch-task-dependencies.md). 

## <a name="next-steps"></a>Volgende stappen

- Gebruik van de nieuwe functies Hallo in Hallo API van Batch-service toopersist taakgegevens verkennen [taak gegevens tooAzure opslag Hello API van Batch-service behouden](batch-task-output-files.md).
- Meer informatie over het gebruik van Hallo bestand conventies van Batch-bibliotheek voor .NET in [behouden van de taak en gegevens tooAzure opslag met Hallo Batch bestand Conventions-bibliotheek voor .NET toopersist ](batch-task-output-file-conventions.md).
- Hallo [PersistOutputs] [github_persistoutputs] Zie voorbeeldproject op GitHub, waaruit blijkt hoe toouse beide Hallo Batch-clientbibliotheek voor .NET en Hallo bestand Conventions-bibliotheek voor .NET toopersist taak uitvoer toodurable opslag.

[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/
