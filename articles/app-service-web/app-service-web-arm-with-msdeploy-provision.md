---
title: aaaDeploy een web-app met behulp van MSDeploy met hostnaam en ssl-certificaat
description: Een web-app met behulp van MSDeploy en het instellen van de aangepaste hostnaam en een SSL-certificaat van een toodeploy Azure Resource Manager-sjabloon gebruiken
services: app-service\web
manager: erikre
documentationcenter: 
author: jodehavi
ms.assetid: 66366a72-cef7-4d75-8779-f4d32ed33cf7
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/31/2016
ms.author: jodehavi
ms.openlocfilehash: ac13f4a7d14ae182e8e7ced5adff30491422d1e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a>Een web-app met MSDeploy, aangepaste hostnaam en SSL-certificaat implementeren
Deze handleiding helpt bij het maken van de implementatie van een end-to-end voor een Azure-Web-App, gebruik van MSDeploy, evenals een aangepaste hostnaam en een SSL-certificaat toohello ARM-sjabloon toe te voegen.

Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).

### <a name="create-sample-application"></a>Voorbeeld van een toepassing maken
U implementeert een ASP.NET-webtoepassing. de eerste stap Hallo is een eenvoudige webtoepassing toocreate (of kunt u toouse een bestaande - in dat geval kunt u deze stap overslaan).

Open Visual Studio 2015 en kies Bestand > Nieuw Project. Kies in het Hallo-dialoogvenster dat verschijnt Web > ASP.NET-webtoepassing. Kies Web onder sjablonen en Hallo MVC-sjabloon kiezen. Selecteer *verificatietype wijzigen* te*geen verificatie*. Dit is slechts toomake Hallo voorbeeldtoepassing zo eenvoudig mogelijk.

Op dit moment hebt u een eenvoudige ASP.Net web app gereed toouse als onderdeel van uw implementatie.

### <a name="create-msdeploy-package"></a>MSDeploy-pakket maken
Volgende stap is toocreate Hallo pakket toodeploy Hallo web app tooAzure. toodo dit, opslaan van uw project en voer de volgende Hallo vanaf de opdrachtregel Hallo:

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

Hiermee maakt u een ingepakte pakket onder Hallo PackageLocation map. Hallo toepassing is nu gereed toobe geïmplementeerd, die u nu van een Azure Resource Manager-sjabloon toodo bouwen kunt die.

### <a name="create-arm-template"></a>ARM-sjabloon maken
Eerst laten we beginnen met een eenvoudige ARM-sjabloon die u maakt een webtoepassing en een hosting plan (opmerking die parameters en variabelen niet als beknopt alternatief bevat weergegeven worden).

    {
        "name": "[parameters('appServicePlanName')]",
        "type": "Microsoft.Web/serverfarms",
        "location": "[resourceGroup().location]",
        "apiVersion": "2014-06-01",
        "dependsOn": [ ],
        "tags": {
            "displayName": "appServicePlan"
        },
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "sku": "[parameters('appServicePlanSKU')]",
            "workerSize": "[parameters('appServicePlanWorkerSize')]",
            "numberOfWorkers": 1
        }
    },
    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        }
    }

Vervolgens moet u toomodify Hallo web app resource tootake een geneste MSDeploy-resource. Hiermee wordt de toestaan dat u tooreference Hallo pakket eerder hebt gemaakt en u vertelt Azure Resource Manager toouse MSDeploy toodeploy Hallo pakket toohello Azure-Web-App. Hallo hieronder vindt u Hallo Microsoft.Web/sites resource met Hallo genest MSDeploy resource:

    {
        "name": "[variables('webAppName')]",
        "type": "Microsoft.Web/sites",
        "location": "[resourceGroup().location]",
        "apiVersion": "2015-08-01",
        "dependsOn": [
            "[concat('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        ],
        "tags": {
            "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]": "Resource",
            "displayName": "webApp"
        },
        "properties": {
            "name": "[variables('webAppName')]",
            "serverFarmId": "[resourceId('Microsoft.Web/serverfarms/', parameters('appServicePlanName'))]"
        },
        "resources": [
            {
                "name": "MSDeploy",
                "type": "extensions",
                "location": "[resourceGroup().location]",
                "apiVersion": "2015-08-01",
                "dependsOn": [
                    "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
                ],
                "tags": {
                    "displayName": "webDeploy"
                },
                "properties": {
                    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]",
                    "dbType": "None",
                    "connectionString": "",
                    "setParameters": {
                        "IIS Web Application Name": "[variables('webAppName')]"
                    }
                }
            }
        ]
    }

Nu ziet u dat Hallo MSDeploy resource heeft een **packageUri** eigenschap die is gedefinieerd als volgt:

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

Dit **packageUri** vergt Hallo storage-account-uri die wijst toohello storage-account waarin u uw postcode pakket aan wordt geüpload. Hello Azure Resource Manager worden benut als [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull Hallo pakket omlaag lokaal vanuit Hallo opslagaccount wanneer u Hallo sjabloon implementeert. Dit proces wordt uitgevoerd via een PowerShell-script die Hallo-pakket te uploaden en aanroepen hello Azure Management API toocreate Hallo-sleutels vereist en die in de sjabloon Hallo doorgeven als parameters (*_artifactsLocation* en *_artifactsLocationSasToken*). Moet u toodefine parameters voor Hallo-map en bestandsnaam Hallo pakket geüploade toounder Hallo storage-container is.

Vervolgens moet u tooadd in een andere geneste resource toosetup Hallo hostnaam bindingen tooleverage een aangepast domein. U gaat eerste nodig tooensure dat u Hallo-hostnaam bezit en toobe instellen geverifieerd door Azure dat jij de eigenaar ervan - Zie [een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md). Wanneer dat is gebeurd, kunt u Hallo tooyour sjabloon onder Hallo Microsoft.Web/sites resourcesectie volgende toevoegen:

    {
        "apiVersion": "2015-08-01",
        "type": "hostNameBindings",
        "name": "www.yourcustomdomain.com",
        "dependsOn": [
            "[concat('Microsoft.Web/sites/', variables('webAppName'))]"
        ],
        "properties": {
            "domainId": null,
            "hostNameType": "Verified",
            "siteName": "variables('webAppName')"
        }
    }

Tot slot moet u tooadd resource in een andere hoogste niveau, Microsoft.Web/certificates. Deze bron bevat uw SSL-certificaat en op hetzelfde niveau als uw web-app en hosting van plan bent Hallo aanwezig zal zijn.

    {
        "name": "[parameters('certificateName')]",
        "apiVersion": "2014-04-01",
        "type": "Microsoft.Web/certificates",
        "location": "[resourceGroup().location]",
        "properties": {
            "pfxBlob": "pfx base64 blob",
            "password": "some pass"
        }
    }

U moet een geldig SSL-certificaat in de volgorde tooset u deze bron toohave. Zodra u die geldig certificaat hebt moet u tooextract Hallo pfx bytes als een base64-tekenreeks. Een optie tooextract dit toouse Hallo volgende PowerShell-opdracht is:

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

U kan vervolgens doorgegeven als een parameter tooyour ARM-sjabloon voor implementatie.

Op dit moment is Hallo ARM-sjabloon gereed.

### <a name="deploy-template"></a>Sjabloon implementeren
Hallo laatste stappen zijn toopiece dit alles samenvoegen in een volledige end-to-end-implementatie. toomake implementatie gemakkelijker kunt u gebruikmaken van Hallo **implementeren AzureResourceGroup.ps1** PowerShell-script dat wordt toegevoegd wanneer u een Azure-resourcegroepproject in Visual Studio toohelp maken met uploaden van alle artefacten die zijn vereist in Hallo-sjabloon. Hiervoor moeten toohave u een opslagaccount dat u wilt dat toouse tevoren gemaakt. In dit voorbeeld moet ik een account met gedeelde opslag voor Hallo pakket.zip toobe geüpload gemaakt. Hallo-script wordt gebruikmaken van AzCopy tooupload Hallo pakket toohello storage-account. U doorgeeft bij de locatie van de artefacten en Hallo script worden alle bestanden in die map toohello storage-container met de naam automatisch uploaden. Na het aanroepen van implementeren AzureResourceGroup.ps1 hebt u toothen Hallo SSL-bindingen toomap Hallo aangepaste hostnaam voor uw SSL-certificaat.

Hallo PowerShell wordt weergegeven na volledige implementatie aanroepen Hallo implementeren Hallo-AzureResourceGroup.ps1:

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script toodeploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app toobind ssl certificate toohostname. This has toobe done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

Op dit moment uw toepassing moet zijn geïmplementeerd en u moet kunnen toobrowse tooit via https://www.yourcustomdomain.com

