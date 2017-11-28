---
title: aaaTroubleshoot Azure Data Factory-problemen
description: Meer informatie over hoe tootroubleshoot problemen met het gebruik van Azure Data Factory.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a><span data-ttu-id="a35dd-103">Problemen met Data Factory oplossen</span><span class="sxs-lookup"><span data-stu-id="a35dd-103">Troubleshoot Data Factory issues</span></span>
<span data-ttu-id="a35dd-104">Dit artikel bevat tips voor probleemoplossing voor problemen bij het gebruik van Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a35dd-104">This article provides troubleshooting tips for issues when using Azure Data Factory.</span></span> <span data-ttu-id="a35dd-105">In dit artikel niet wordt vermeld in alle Hallo mogelijke problemen bij het gebruik Hallo-service, maar bevat informatie over sommige problemen en algemene tips voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="a35dd-105">This article does not list all hello possible issues when using hello service, but it covers some issues and general troubleshooting tips.</span></span>   

## <a name="troubleshooting-tips"></a><span data-ttu-id="a35dd-106">Tips voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="a35dd-106">Troubleshooting tips</span></span>
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a><span data-ttu-id="a35dd-107">Fout: Hallo-abonnement is niet geregistreerd toouse naamruimte 'Microsoft.DataFactory'</span><span class="sxs-lookup"><span data-stu-id="a35dd-107">Error: hello subscription is not registered toouse namespace 'Microsoft.DataFactory'</span></span>
<span data-ttu-id="a35dd-108">Als u dit foutbericht ontvangt, is niet hello Azure Data Factory-resourceprovider geregistreerd op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a35dd-108">If you receive this error, hello Azure Data Factory resource provider has not been registered on your machine.</span></span> <span data-ttu-id="a35dd-109">Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="a35dd-109">Do hello following:</span></span>

1. <span data-ttu-id="a35dd-110">Start Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a35dd-110">Launch Azure PowerShell.</span></span>
2. <span data-ttu-id="a35dd-111">Tooyour aanmelden met Azure-account met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="a35dd-111">Log in tooyour Azure account using hello following command.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="a35dd-112">Voer Hallo opdracht tooregister hello Azure Data Factory-provider te volgen.</span><span class="sxs-lookup"><span data-stu-id="a35dd-112">Run hello following command tooregister hello Azure Data Factory provider.</span></span>

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a><span data-ttu-id="a35dd-113">Probleem: Niet-geautoriseerde fout bij het uitvoeren van een Data Factory-cmdlet</span><span class="sxs-lookup"><span data-stu-id="a35dd-113">Problem: Unauthorized error when running a Data Factory cmdlet</span></span>
<span data-ttu-id="a35dd-114">U waarschijnlijk niet Hallo rechts Azure-account of -abonnement met hello Azure PowerShell gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a35dd-114">You are probably not using hello right Azure account or subscription with hello Azure PowerShell.</span></span> <span data-ttu-id="a35dd-115">Hallo na cmdlets tooselect Hallo rechts Azure-account en abonnement toouse Hello Azure PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a35dd-115">Use hello following cmdlets tooselect hello right Azure account and subscription toouse with hello Azure PowerShell.</span></span>

1. <span data-ttu-id="a35dd-116">Login-AzureRmAccount - gebruik Hallo juiste gebruikersnaam en wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a35dd-116">Login-AzureRmAccount - Use hello right user ID and password</span></span>
2. <span data-ttu-id="a35dd-117">Get-AzureRmSubscription - weergave alle abonnementen voor account Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a35dd-117">Get-AzureRmSubscription - View all hello subscriptions for hello account.</span></span>
3. <span data-ttu-id="a35dd-118">SELECT-AzureRmSubscription &lt;abonnementsnaam&gt; -Selecteer het juiste abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="a35dd-118">Select-AzureRmSubscription &lt;subscription name&gt; - Select hello right subscription.</span></span> <span data-ttu-id="a35dd-119">Gebruik Hallo dezelfde is als die u toocreate een gegevensfactory op Hallo Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a35dd-119">Use hello same one you use toocreate a data factory on hello Azure portal.</span></span>

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a><span data-ttu-id="a35dd-120">Probleem: Mislukken toolaunch Express-installatie van Data Management Gateway vanuit Azure-portal</span><span class="sxs-lookup"><span data-stu-id="a35dd-120">Problem: Fail toolaunch Data Management Gateway Express Setup from Azure portal</span></span>
<span data-ttu-id="a35dd-121">Hallo snelle installatie voor Hallo Data Management Gateway vereist Internet Explorer of een compatibel webbrowser Microsoft ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="a35dd-121">hello Express setup for hello Data Management Gateway requires Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span> <span data-ttu-id="a35dd-122">Als Hallo snelle installatie toostart mislukt, voert u een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="a35dd-122">If hello Express Setup fails toostart, do one of hello following:</span></span>

* <span data-ttu-id="a35dd-123">Internet Explorer of een webbrowser die Microsoft ClickOnce compatibel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a35dd-123">Use Internet Explorer or a Microsoft ClickOnce compatible web browser.</span></span>

    <span data-ttu-id="a35dd-124">Als u Chrome gebruikt, gaat u toohello [Chrome web store](https://chrome.google.com/webstore/), zoeken met het sleutelwoord 'ClickOnce', kies een van de ClickOnce-extensies Hallo en deze installeren.</span><span class="sxs-lookup"><span data-stu-id="a35dd-124">If you are using Chrome, go toohello [Chrome web store](https://chrome.google.com/webstore/), search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>

    <span data-ttu-id="a35dd-125">Hallo dezelfde voor Firefox (install-invoegtoepassing).</span><span class="sxs-lookup"><span data-stu-id="a35dd-125">Do hello same for Firefox (install add-in).</span></span> <span data-ttu-id="a35dd-126">Klik op de knop Menu openen op Hallo werkbalk (drie horizontale lijnen in de rechterbovenhoek Hallo), invoegtoepassingen, zoeken met het sleutelwoord 'ClickOnce', kies een van de ClickOnce-extensies Hallo en deze installeren.</span><span class="sxs-lookup"><span data-stu-id="a35dd-126">Click Open Menu button on hello toolbar (three horizontal lines in hello top-right corner), click Add-ons, search with "ClickOnce" keyword, choose one of hello ClickOnce extensions, and install it.</span></span>
* <span data-ttu-id="a35dd-127">Gebruik Hallo **handmatige installatie** koppeling weergegeven op Hallo van dezelfde blade in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="a35dd-127">Use hello **Manual Setup** link shown on hello same blade in hello portal.</span></span> <span data-ttu-id="a35dd-128">U gebruikt deze benadering toodownload-bestand voor installatie en het handmatig uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a35dd-128">You use this approach toodownload installation file and run it manually.</span></span> <span data-ttu-id="a35dd-129">Nadat het Hallo-installatie is voltooid, ziet u in het dialoogvenster van Hallo Data Management Gateway Configuration.</span><span class="sxs-lookup"><span data-stu-id="a35dd-129">After hello installation is successful, you see hello Data Management Gateway Configuration dialog box.</span></span> <span data-ttu-id="a35dd-130">Kopiëren Hallo **sleutel** uit portal welkomstscherm en het gebruik ervan in Hallo configuration manager toomanually Hallo gateway registreren bij Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="a35dd-130">Copy hello **key** from hello portal screen and use it in hello configuration manager toomanually register hello gateway with hello service.</span></span>  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a><span data-ttu-id="a35dd-131">Probleem: Mislukken tooconnect tooon-premises SQL Server</span><span class="sxs-lookup"><span data-stu-id="a35dd-131">Problem: Fail tooconnect tooon-premises SQL Server</span></span>
<span data-ttu-id="a35dd-132">Start **Data Management Gateway Configuration Manager** op Hallo van gateway-apparaat en gebruik Hallo **probleemoplossing** tootest Hallo verbinding tooSQL Server van de gatewaycomputer Hallo tabblad.</span><span class="sxs-lookup"><span data-stu-id="a35dd-132">Launch **Data Management Gateway Configuration Manager** on hello gateway machine and use hello **Troubleshooting** tab tootest hello connection tooSQL Server from hello gateway machine.</span></span> <span data-ttu-id="a35dd-133">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="a35dd-133">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a><span data-ttu-id="a35dd-134">Probleem: Invoer segmenten zijn in het wacht voor ooit op status</span><span class="sxs-lookup"><span data-stu-id="a35dd-134">Problem: Input slices are in Waiting state for ever</span></span>
<span data-ttu-id="a35dd-135">Hallo segmenten mogelijk **wachten** status vanwege toovarious redenen.</span><span class="sxs-lookup"><span data-stu-id="a35dd-135">hello slices could be in **Waiting** state due toovarious reasons.</span></span> <span data-ttu-id="a35dd-136">Een veelvoorkomende redenen Hallo die Hallo is **externe** eigenschap is niet ingesteld te**true**.</span><span class="sxs-lookup"><span data-stu-id="a35dd-136">One of hello common reasons is that hello **external** property is not set too**true**.</span></span> <span data-ttu-id="a35dd-137">Een gegevensset die is geproduceerd buiten Hallo omvang van Azure Data Factory moet worden gemarkeerd met **externe** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a35dd-137">Any dataset that is produced outside hello scope of Azure Data Factory should be marked with **external** property.</span></span> <span data-ttu-id="a35dd-138">Deze eigenschap geeft aan dat gegevens Hallo externe en niet door pijplijnen binnen Hallo gegevensfactory back-ups.</span><span class="sxs-lookup"><span data-stu-id="a35dd-138">This property indicates that hello data is external and not backed by any pipelines within hello data factory.</span></span> <span data-ttu-id="a35dd-139">Hallo gegevenssegmenten zijn gemarkeerd als **gereed** nadat Hallo gegevens Hallo respectieve store beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="a35dd-139">hello data slices are marked as **Ready** once hello data is available in hello respective store.</span></span>

<span data-ttu-id="a35dd-140">Zie de volgende voorbeeld voor het gebruik van Hallo HALLO hallo **externe** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a35dd-140">See hello following example for hello usage of hello **external** property.</span></span> <span data-ttu-id="a35dd-141">U kunt optioneel opgeven **externalData*** als u externe tootrue instelt.</span><span class="sxs-lookup"><span data-stu-id="a35dd-141">You can optionally specify **externalData*** when you set external tootrue.</span></span>

<span data-ttu-id="a35dd-142">Zie [gegevenssets](data-factory-create-datasets.md) artikel voor meer informatie over deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a35dd-142">See [Datasets](data-factory-create-datasets.md) article for more details about this property.</span></span>

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

<span data-ttu-id="a35dd-143">tooresolve Hallo fout, Hallo toevoegen **externe** eigenschap en optionele Hallo **externalData** toohello JSON-definitie van de invoertabel Hallo sectie en maak deze opnieuw Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="a35dd-143">tooresolve hello error, add hello **external** property and hello optional **externalData** section toohello JSON definition of hello input table and recreate hello table.</span></span>

### <a name="problem-hybrid-copy-operation-fails"></a><span data-ttu-id="a35dd-144">Probleem: Hybride kopieerbewerking mislukt</span><span class="sxs-lookup"><span data-stu-id="a35dd-144">Problem: Hybrid copy operation fails</span></span>
<span data-ttu-id="a35dd-145">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor stappen tootroubleshoot problemen met het kopiëren van/naar een on-premises gegevens opslaan met behulp van Data Management Gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="a35dd-145">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for steps tootroubleshoot issues with copying to/from an on-premises data store using hello Data Management Gateway.</span></span>

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a><span data-ttu-id="a35dd-146">Probleem: On-demand HDInsight inrichten mislukt</span><span class="sxs-lookup"><span data-stu-id="a35dd-146">Problem: On-demand HDInsight provisioning fails</span></span>
<span data-ttu-id="a35dd-147">Wanneer u een gekoppelde service van het type HDInsightOnDemand gebruikt, moet u toospecify een linkedServiceName die tooan Azure Blob Storage verwijst.</span><span class="sxs-lookup"><span data-stu-id="a35dd-147">When using a linked service of type HDInsightOnDemand, you need toospecify a linkedServiceName that points tooan Azure Blob Storage.</span></span> <span data-ttu-id="a35dd-148">Data Factory-service gebruikt deze opslag toostore logboeken en de ondersteunende bestanden voor uw HDInsight-cluster op aanvraag.</span><span class="sxs-lookup"><span data-stu-id="a35dd-148">Data Factory service uses this storage toostore logs and supporting files for your on-demand HDInsight cluster.</span></span>  <span data-ttu-id="a35dd-149">Soms het inrichten van een HDInsight-cluster op aanvraag is mislukt met de volgende fout Hallo:</span><span class="sxs-lookup"><span data-stu-id="a35dd-149">Sometimes provisioning of an on-demand HDInsight cluster fails with hello following error:</span></span>

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

<span data-ttu-id="a35dd-150">Deze fout geeft meestal aan dat Hallo-locatie van Hallo storage-account opgegeven in Hallo linkedServiceName zich niet in Hallo hetzelfde datacentrum locatie waar Hallo HDInsight inrichten er gebeurt.</span><span class="sxs-lookup"><span data-stu-id="a35dd-150">This error usually indicates that hello location of hello storage account specified in hello linkedServiceName is not in hello same data center location where hello HDInsight provisioning is happening.</span></span> <span data-ttu-id="a35dd-151">Voorbeeld: als uw gegevensfactory in VS-West en hello Azure-opslag bevindt zich in VS-Oost, Hallo inrichting mislukt op aanvraag in VS-West.</span><span class="sxs-lookup"><span data-stu-id="a35dd-151">Example: if your data factory is in West US and hello Azure storage is in East US, hello on-demand provisioning fails in West US.</span></span>

<span data-ttu-id="a35dd-152">Daarnaast is er een tweede JSON-eigenschap, additionalLinkedServiceNames, waar extra opslagaccounts in HDInsight op aanvraag kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a35dd-152">Additionally, there is a second JSON property additionalLinkedServiceNames where additional storage accounts may be specified in on-demand HDInsight.</span></span> <span data-ttu-id="a35dd-153">Deze extra gekoppelde opslagaccounts moet Hallo dezelfde locatie als Hallo HDInsight-cluster, of het is mislukt met de Hallo dezelfde fout.</span><span class="sxs-lookup"><span data-stu-id="a35dd-153">Those additional linked storage accounts should be in hello same location as hello HDInsight cluster, or it fails with hello same error.</span></span>

### <a name="problem-custom-net-activity-fails"></a><span data-ttu-id="a35dd-154">Probleem: Aangepaste activiteit .NET mislukt</span><span class="sxs-lookup"><span data-stu-id="a35dd-154">Problem: Custom .NET activity fails</span></span>
<span data-ttu-id="a35dd-155">Zie [fouten opsporen in een pijplijn met een aangepaste activiteit](data-factory-use-custom-activities.md#troubleshoot-failures) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="a35dd-155">See [Debug a pipeline with custom activity](data-factory-use-custom-activities.md#troubleshoot-failures) for detailed steps.</span></span>

## <a name="use-azure-portal-tootroubleshoot"></a><span data-ttu-id="a35dd-156">Azure portal tootroubleshoot gebruiken</span><span class="sxs-lookup"><span data-stu-id="a35dd-156">Use Azure portal tootroubleshoot</span></span>
### <a name="using-portal-blades"></a><span data-ttu-id="a35dd-157">Met de portal-blades</span><span class="sxs-lookup"><span data-stu-id="a35dd-157">Using portal blades</span></span>
<span data-ttu-id="a35dd-158">Zie [pijplijn bewaken](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) voor stappen.</span><span class="sxs-lookup"><span data-stu-id="a35dd-158">See [Monitor pipeline](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) for steps.</span></span>

### <a name="using-monitor-and-manage-app"></a><span data-ttu-id="a35dd-159">App voor controle en beheer gebruiken</span><span class="sxs-lookup"><span data-stu-id="a35dd-159">Using Monitor and Manage App</span></span>
<span data-ttu-id="a35dd-160">Zie [bewaken en beheren van de data factory-pijplijnen bewaken en beheren van App met](data-factory-monitor-manage-app.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a35dd-160">See [Monitor and manage data factory pipelines using Monitor and Manage App](data-factory-monitor-manage-app.md) for details.</span></span>

## <a name="use-azure-powershell-tootroubleshoot"></a><span data-ttu-id="a35dd-161">Azure PowerShell tootroubleshoot gebruiken</span><span class="sxs-lookup"><span data-stu-id="a35dd-161">Use Azure PowerShell tootroubleshoot</span></span>
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a><span data-ttu-id="a35dd-162">Gebruik Azure PowerShell tootroubleshoot een fout opgetreden</span><span class="sxs-lookup"><span data-stu-id="a35dd-162">Use Azure PowerShell tootroubleshoot an error</span></span>
<span data-ttu-id="a35dd-163">Zie [Monitor Data Factory-pijplijnen met Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a35dd-163">See [Monitor Data Factory pipelines using Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline) for details.</span></span>

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
