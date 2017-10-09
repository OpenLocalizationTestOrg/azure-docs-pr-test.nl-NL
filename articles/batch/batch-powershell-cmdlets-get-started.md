---
title: aaaGet gestart met PowerShell voor Azure Batch | Microsoft Docs
description: Een korte inleiding toohello Azure PowerShell-cmdlets kunt u toomanage Batch-resources.
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: f9ad62c5-27bf-4e6b-a5bf-c5f5914e6199
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: powershell
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3e4d12e9c1e52a5b2db2dd44346edda93b7ef92b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-powershell-cmdlets"></a>Batch-resources beheren met PowerShell-cmdlets

Hello Azure Batch PowerShell-cmdlets, kunt u uitvoeren en veel van Hallo script dezelfde taken die u uitvoert met de Batch-API's Hallo hello Azure-portal en hello Azure-opdrachtregelinterface (CLI). Dit is een korte inleiding toohello-cmdlets kunt u gebruiken toomanage uw Batch-accounts en werken met uw Batch-resources zoals pools, jobs en taken.

Zie voor een volledige lijst van Batch-cmdlets en gedetailleerde cmdlet-syntaxis Hallo [naslaginformatie over Azure Batch-cmdlets](/powershell/module/azurerm.batch/#batch).

Dit artikel is gebaseerd op cmdlets in Azure PowerShell versie 3.0.0. We bevelen aan dat u uw Azure PowerShell regelmatig tootake profiteren van de service-updates en verbeteringen.

## <a name="prerequisites"></a>Vereisten
Hallo operations toouse Azure PowerShell toomanage na uw Batch-resources uitvoeren.

* [Azure PowerShell installeren en configureren ](/powershell/azure/overview)
* Voer Hallo **Login-AzureRmAccount** cmdlet tooconnect tooyour abonnement (hello Azure Batch-cmdlets verzenden in hello Azure Resource Manager-module):
  
    `Login-AzureRmAccount`
* **Registreren bij de naamruimte van de provider Batch Hallo**. Deze bewerking hoeft slechts toobe uitgevoerd **eenmaal per abonnement**.
  
    `Register-AzureRMResourceProvider -ProviderNamespace Microsoft.Batch`

## <a name="manage-batch-accounts-and-keys"></a>Batch-accounts en -sleutels beheren
### <a name="create-a-batch-account"></a>Batch-account maken
Met **New-AzureRmBatchAccount** wordt een Batch-account in een opgegeven resourcegroep gemaakt. Als u nog een resourcegroep hebt, maakt een door Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet. Geef een hello Azure gebieden in Hallo **locatie** parameter, zoals 'VS-midden'. Bijvoorbeeld:

    New-AzureRmResourceGroup –Name MyBatchResourceGroup –location "Central US"

Maak een Batch-account in de resourcegroep hello, Hallo-account in een naam geven <*account_name*> en Hallo locatie en naam van de resourcegroep. Hallo Batch-account maken kan sommige toocomplete tijd in beslag nemen. Bijvoorbeeld:

    New-AzureRmBatchAccount –AccountName <account_name> –Location "Central US" –ResourceGroupName <res_group_name>

> [!NOTE]
> Hallo Batch-account is de naam moet uniek toohello Azure-regio voor de resourcegroep Hallo tussen 3 en 24 tekens bevatten en gebruik alleen kleine letters en cijfers.
> 
> 

### <a name="get-account-access-keys"></a>Toegangssleutels van account ophalen
**Get-AzureRmBatchAccountKeys** toont Hallo toegangstoetsen die zijn gekoppeld aan een Azure Batch-account. Bijvoorbeeld uitvoeren Hallo na tooget Hallo primaire en secundaire sleutels van Hallo-account voor die u gemaakt.

    $Account = Get-AzureRmBatchAccountKeys –AccountName <account_name>

    $Account.PrimaryAccountKey

    $Account.SecondaryAccountKey

### <a name="generate-a-new-access-key"></a>Een nieuwe toegangssleutel genereren
Met **New-AzureRmBatchAccountKey** wordt een nieuwe primaire of secundaire accountsleutel voor een Azure Batch-account gegenereerd. Typ bijvoorbeeld toogenerate een nieuwe primaire sleutel voor uw Batch-account:

    New-AzureRmBatchAccountKey -AccountName <account_name> -KeyType Primary

> [!NOTE]
> een nieuwe secundaire sleutel toogenerate 'Secundair' opgeeft voor Hallo **KeyType** parameter. U hebben tooregenerate Hallo primaire en secundaire sleutels afzonderlijk.
> 
> 

### <a name="delete-a-batch-account"></a>Batch-account verwijderen
Met **Remove-AzureRmBatchAccount** wordt een Batch-account verwijderd. Bijvoorbeeld:

    Remove-AzureRmBatchAccount -AccountName <account_name>

Wanneer u wordt gevraagd, bevestig gewenste tooremove Hallo-account. Account is verwijderd, kan sommige toocomplete tijd duren.

## <a name="create-a-batchaccountcontext-object"></a>Een BatchAccountContext-object maken
met behulp van tooauthenticate Batch PowerShell-cmdlets hello, wanneer u maken en beheren van Batch-pools, jobs, taken en andere resources, maak eerst een BatchAccountContext-object toostore uw accountnaam en sleutels:

    $context = Get-AzureRmBatchAccountKeys -AccountName <account_name>

U die gebruik Hallo Hallo BatchAccountContext-object in cmdlets doorgeven **BatchContext** parameter.

> [!NOTE]
> Standaard de primaire sleutel van het Hallo-account wordt gebruikt voor verificatie, maar u kunt Hallo sleutel toouse expliciet selecteren door te wijzigen van het object BatchAccountContext **KeyInUse** eigenschap: `$context.KeyInUse = "Secondary"`.
> 
> 

## <a name="create-and-modify-batch-resources"></a>Batch-resources maken en wijzigen
Gebruik cmdlets zoals **New-AzureBatchPool**, **New-AzureBatchJob**, en **New-AzureBatchTask** toocreate resources onder een Batch-account. Er zijn overeenkomende **Get -** en **Set -** cmdlets tooupdate Hallo eigenschappen van bestaande bronnen, en **Remove -** cmdlets tooremove resources onder een Batch-account.

Wanneer u veel van deze cmdlets in toevoeging toopassing een BatchContext-object, of u kunt toocreate objecten die gedetailleerde broninstellingen bevatten, zoals wordt weergegeven in het volgende voorbeeld Hallo doorgeeft. Zie Hallo gedetailleerde Help-informatie voor elke cmdlet voor meer voorbeelden.

### <a name="create-a-batch-pool"></a>Batch-pool maken
Bij het maken of bijwerken van een Batch-pool, u Hallo cloud serviceconfiguratie of virtuele-machineconfiguratie Hallo selecteren voor hello besturingssysteem op Hallo rekenknooppunten (Zie [overzicht Batch-functies](batch-api-basics.md#pool)). Als u de configuratie voor cloud service Hallo opgeeft, uw rekenknooppunten installatiekopie gemaakt wordt met een Hallo [Azure Gast OS releases](../cloud-services/cloud-services-guestos-update-matrix.md#releases). Als u de configuratie van de virtuele machine Hallo opgeeft, kunt u opgeven of installatiekopieën van virtuele machine van Windows hello opgenomen in een van de Hallo Linux ondersteund [Azure Virtual Machines Marketplace][vm_marketplace], of geef een aangepaste afbeelding die u hebt voorbereid.

Bij het uitvoeren van **New-AzureBatchPool**, besturingssysteeminstellingen Hallo doorgeven in een PSCloudServiceConfiguration of PSVirtualMachineConfiguration object. Bijvoorbeeld: hello volgende cmdlet maakt een nieuwe Batch-pool met grootte klein rekenknooppunten in Hallo cloud service-configuratie, wordt een installatiekopie gemaakt met de Hallo nieuwste besturingssysteemversie van type 3 (Windows Server 2012). Hier Hallo **CloudServiceConfiguration** parameter geeft u op Hallo *$configuration* variabele als Hallo PSCloudServiceConfiguration object. Hallo **BatchContext** parameter geeft u een eerder gedefinieerde variabele *$context* als Hallo BatchAccountContext-object.

    $configuration = New-Object -TypeName "Microsoft.Azure.Commands.Batch.Models.PSCloudServiceConfiguration" -ArgumentList @(4,"*")

    New-AzureBatchPool -Id "AutoScalePool" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -AutoScaleFormula '$TargetDedicated=4;' -BatchContext $context

Hallo doelaantal rekenknooppunten in de nieuwe groep hello wordt bepaald door een formule voor automatisch schalen. In dit geval Hallo formule is gewoon **$TargetDedicated = 4**, maximaal die het aantal rekenknooppunten in de pool Hallo Hallo aangeeft is 4.

## <a name="query-for-pools-jobs-tasks-and-other-details"></a>Query voor pools, jobs, taken en andere details
Gebruik cmdlets zoals **Get-AzureBatchPool**, **Get-AzureBatchJob**, en **Get-AzureBatchTask** tooquery voor entiteiten die zijn gemaakt onder een Batch-account.

### <a name="query-for-data"></a>Query voor gegevens
Gebruik bijvoorbeeld **Get-AzureBatchPools** toofind uw pools. Deze query voor alle pools onder uw account standaard, ervan uitgaande dat u al opgeslagen Hallo BatchAccountContext-object in *$context*:

    Get-AzureBatchPool -BatchContext $context

### <a name="use-an-odata-filter"></a>Een OData-filter gebruiken
U kunt opgeven dat een OData-filter met de Hallo **Filter** parameter toofind Hallo alleen objecten die u geïnteresseerd bent in. U kunt bijvoorbeeld alle pools zoeken met id's die beginnen met 'myPool':

    $filter = "startswith(id,'myPool')"

    Get-AzureBatchPool -Filter $filter -BatchContext $context

Deze methode is niet zo flexibel als het gebruik van een 'Where-Object' in een lokale pijplijn. Hallo query opgehaald toohello Batch-service rechtstreeks verzonden zodat al het filteren aan de serverzijde hello, waardoor er internetbandbreedte gebeurt.

### <a name="use-hello-id-parameter"></a>Hallo-Id-parameter gebruiken
Een alternatieve tooan OData-filter is toouse hello **Id** parameter. tooquery voor een specifieke pool met id 'myPool':

    Get-AzureBatchPool -Id "myPool" -BatchContext $context

Hallo **Id** parameter ondersteunt alleen volledige id zoeken, geen jokertekens of filters voor OData-type.

### <a name="use-hello-maxcount-parameter"></a>Gebruik de parameter MaxCount Hallo
Standaard worden met elke cmdlet maximaal 1000 objecten geretourneerd. Als u deze limiet is bereikt, is uw toobring filter verfijnen er minder objecten of expliciet ingesteld met behulp van Hallo maximaal **MaxCount** parameter. Bijvoorbeeld:

    Get-AzureBatchTask -MaxCount 2500 -BatchContext $context

bovengrens tooremove hello, stel **MaxCount** too0 of minder.

### <a name="use-hello-powershell-pipeline"></a>Gebruik Hallo PowerShell-pipeline
Hallo PowerShell pijplijn toosend gegevens tussen cmdlets kunt gebruikmaken van batch-cmdlets. Dit heeft hetzelfde effect als het opgeven van een parameter, maar zorgt ervoor dat werken met meerdere entiteiten eenvoudiger Hallo.

Zo kunt u bijvoorbeeld alle taken onder uw account zoeken en weergeven:

    Get-AzureBatchJob -BatchContext $context | Get-AzureBatchTask -BatchContext $context

Start elk computerknooppunt in een groep opnieuw op:

    Get-AzureBatchComputeNode -PoolId "myPool" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

## <a name="application-package-management"></a>Beheer van toepassingspakketten
Toepassingspakketten bieden een eenvoudige manier toodeploy toepassingen toohello rekenknooppunten in uw pools. Met Hallo Batch PowerShell-cmdlets, kunt u uploaden en toepassingspakketten in uw Batch-account beheren en implementeren van pakket versies toocompute knooppunten.

Een toepassing **maken**:

    New-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

Een toepassingspakket **toevoegen**:

    New-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0" -Format zip -FilePath package001.zip

Set Hallo **standaardversie** voor Hallo toepassing:

    Set-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -DefaultVersion "1.0"

**Geeft een overzicht van** de pakketten van een toepassing

    $application = Get-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

    $application.ApplicationPackages

Een toepassingspakket **verwijderen**

    Remove-AzureRmBatchApplicationPackage -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication" -ApplicationVersion "1.0"

Een toepassing **verwijderen**

    Remove-AzureRmBatchApplication -AccountName <account_name> -ResourceGroupName <res_group_name> -ApplicationId "MyBatchApplication"

> [!NOTE]
> U moet alle toepassingspakketversies van een toepassing verwijderen voordat u de toepassing hello verwijderen. U ontvangt een foutbericht als u probeert een toepassing die momenteel toepassingspakketten is toodelete.
> 
> 

### <a name="deploy-an-application-package"></a>Een toepassingspakket implementeren
U kunt een of meer toepassingspakketten voor implementatie opgeven wanneer u een groep maakt. Wanneer u een pakket tijdens het maken van toepassingen opgeeft, is het geïmplementeerde tooeach knooppunt als Hallo knooppunt joins groep. Pakketten worden ook geïmplementeerd als een knooppunt opnieuw wordt gestart of teruggezet.

Geef Hallo `-ApplicationPackageReference` optie bij het maken van een groep toodeploy knooppunten van een pakket toohello van groep van toepassingen als ze Hallo adresgroep toevoegen. Maak eerst een **PSApplicationPackageReference** object en deze configureren met Hallo Id en pakketnaam toepassingsversie gewenste toodeploy toohello pool van rekenknooppunten:

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "1.0"

Nu Hallo-pool maken en Hallo pakket reference-object opgeven als argument toohello Hallo `ApplicationPackageReferences` optie:

    New-AzureBatchPool -Id "PoolWithAppPackage" -VirtualMachineSize "Small" -CloudServiceConfiguration $configuration -BatchContext $context -ApplicationPackageReferences $appPackageReference

U vindt meer informatie over toepassingspakketten in [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).

> [!IMPORTANT]
> U moet [een Azure Storage-account koppelen](#linked-storage-account-autostorage) tooyour Batch-account toouse toepassingspakketten.
> 
> 

### <a name="update-a-pools-application-packages"></a>De toepassingspakketten van een groep bijwerken
tooupdate hello toepassingen die zijn toegewezen tooan bestaande groep, worden eerst een PSApplicationPackageReference-object maken met Hallo gewenst eigenschappen (Id en pakketnaam toepassingsversie):

    $appPackageReference = New-Object Microsoft.Azure.Commands.Batch.Models.PSApplicationPackageReference

    $appPackageReference.ApplicationId = "MyBatchApplication"

    $appPackageReference.Version = "2.0"

Vervolgens Hallo van toepassingen niet ophalen uit de Batch, eventuele bestaande pakketten wissen onze nieuwe pakket verwijzing toevoegen en Hallo Batch-service bijwerken met nieuwe groepsinstellingen Hallo:

    $pool = Get-AzureBatchPool -BatchContext $context -Id "PoolWithAppPackage"

    $pool.ApplicationPackageReferences.Clear()

    $pool.ApplicationPackageReferences.Add($appPackageReference)

    Set-AzureBatchPool -BatchContext $context -Pool $pool

U hebt nu Hallo van groepseigenschappen in Hallo Batch-service bijgewerkt. tooactually implementeren Hallo nieuwe toepassing pakket toocompute knooppunten in de groep hello, u moet echter opnieuw opstart of installatiekopie die knooppunten. U kunt elk knooppunt in een adresgroep met de volgende opdracht opnieuw starten:

    Get-AzureBatchComputeNode -PoolId "PoolWithAppPackage" -BatchContext $context | Restart-AzureBatchComputeNode -BatchContext $context

> [!TIP]
> U kunt meerdere toepassing pakketten toohello-rekenknooppunten in een pool implementeren. Als u te wilt*toevoegen* toepassingspakketten in plaats van het vervangen van momenteel geïmplementeerd hello-pakketten weglaten Hallo `$pool.ApplicationPackageReferences.Clear()` bovenstaande regel.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Zie [Naslaginformatie over Azure Batch-cmdlets](/powershell/module/azurerm.batch/#batch) voor gedetailleerde cmdlet-syntaxis en voorbeelden.
* Zie voor meer informatie over de toepassingen en in een Batch-toepassingspakketten [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/