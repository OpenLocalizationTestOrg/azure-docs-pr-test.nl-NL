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
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="aceaa-103">Een web-app met MSDeploy, aangepaste hostnaam en SSL-certificaat implementeren</span><span class="sxs-lookup"><span data-stu-id="aceaa-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="aceaa-104">Deze handleiding helpt bij het maken van de implementatie van een end-to-end voor een Azure-Web-App, gebruik van MSDeploy, evenals een aangepaste hostnaam en een SSL-certificaat toohello ARM-sjabloon toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="aceaa-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate toohello ARM template.</span></span>

<span data-ttu-id="aceaa-105">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="aceaa-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="aceaa-106">Voorbeeld van een toepassing maken</span><span class="sxs-lookup"><span data-stu-id="aceaa-106">Create Sample Application</span></span>
<span data-ttu-id="aceaa-107">U implementeert een ASP.NET-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="aceaa-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="aceaa-108">de eerste stap Hallo is een eenvoudige webtoepassing toocreate (of kunt u toouse een bestaande - in dat geval kunt u deze stap overslaan).</span><span class="sxs-lookup"><span data-stu-id="aceaa-108">hello first step is toocreate a simple web application (or you could choose toouse an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="aceaa-109">Open Visual Studio 2015 en kies Bestand > Nieuw Project.</span><span class="sxs-lookup"><span data-stu-id="aceaa-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="aceaa-110">Kies in het Hallo-dialoogvenster dat verschijnt Web > ASP.NET-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="aceaa-110">On hello dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="aceaa-111">Kies Web onder sjablonen en Hallo MVC-sjabloon kiezen.</span><span class="sxs-lookup"><span data-stu-id="aceaa-111">Under Templates choose Web and choose hello MVC template.</span></span> <span data-ttu-id="aceaa-112">Selecteer *verificatietype wijzigen* te*geen verificatie*.</span><span class="sxs-lookup"><span data-stu-id="aceaa-112">Select *Change authentication type* too*No Authentication*.</span></span> <span data-ttu-id="aceaa-113">Dit is slechts toomake Hallo voorbeeldtoepassing zo eenvoudig mogelijk.</span><span class="sxs-lookup"><span data-stu-id="aceaa-113">This is just toomake hello sample application as simple as possible.</span></span>

<span data-ttu-id="aceaa-114">Op dit moment hebt u een eenvoudige ASP.Net web app gereed toouse als onderdeel van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="aceaa-114">At this point you will have a basic ASP.Net web app ready toouse as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="aceaa-115">MSDeploy-pakket maken</span><span class="sxs-lookup"><span data-stu-id="aceaa-115">Create MSDeploy package</span></span>
<span data-ttu-id="aceaa-116">Volgende stap is toocreate Hallo pakket toodeploy Hallo web app tooAzure.</span><span class="sxs-lookup"><span data-stu-id="aceaa-116">Next step is toocreate hello package toodeploy hello web app tooAzure.</span></span> <span data-ttu-id="aceaa-117">toodo dit, opslaan van uw project en voer de volgende Hallo vanaf de opdrachtregel Hallo:</span><span class="sxs-lookup"><span data-stu-id="aceaa-117">toodo this, save your project and then run hello following from hello command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="aceaa-118">Hiermee maakt u een ingepakte pakket onder Hallo PackageLocation map.</span><span class="sxs-lookup"><span data-stu-id="aceaa-118">This will create a zipped package under hello PackageLocation folder.</span></span> <span data-ttu-id="aceaa-119">Hallo toepassing is nu gereed toobe geïmplementeerd, die u nu van een Azure Resource Manager-sjabloon toodo bouwen kunt die.</span><span class="sxs-lookup"><span data-stu-id="aceaa-119">hello application is now ready toobe deployed, which you can now build out an Azure Resource Manager template toodo that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="aceaa-120">ARM-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="aceaa-120">Create ARM Template</span></span>
<span data-ttu-id="aceaa-121">Eerst laten we beginnen met een eenvoudige ARM-sjabloon die u maakt een webtoepassing en een hosting plan (opmerking die parameters en variabelen niet als beknopt alternatief bevat weergegeven worden).</span><span class="sxs-lookup"><span data-stu-id="aceaa-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="aceaa-122">Vervolgens moet u toomodify Hallo web app resource tootake een geneste MSDeploy-resource.</span><span class="sxs-lookup"><span data-stu-id="aceaa-122">Next, you will need toomodify hello web app resource tootake a nested MSDeploy resource.</span></span> <span data-ttu-id="aceaa-123">Hiermee wordt de toestaan dat u tooreference Hallo pakket eerder hebt gemaakt en u vertelt Azure Resource Manager toouse MSDeploy toodeploy Hallo pakket toohello Azure-Web-App.</span><span class="sxs-lookup"><span data-stu-id="aceaa-123">This will allow you tooreference hello package created earlier and tell Azure Resource Manager toouse MSDeploy toodeploy hello package toohello Azure WebApp.</span></span> <span data-ttu-id="aceaa-124">Hallo hieronder vindt u Hallo Microsoft.Web/sites resource met Hallo genest MSDeploy resource:</span><span class="sxs-lookup"><span data-stu-id="aceaa-124">hello following shows hello Microsoft.Web/sites resource with hello nested MSDeploy resource:</span></span>

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

<span data-ttu-id="aceaa-125">Nu ziet u dat Hallo MSDeploy resource heeft een **packageUri** eigenschap die is gedefinieerd als volgt:</span><span class="sxs-lookup"><span data-stu-id="aceaa-125">Now you will notice that hello MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="aceaa-126">Dit **packageUri** vergt Hallo storage-account-uri die wijst toohello storage-account waarin u uw postcode pakket aan wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="aceaa-126">This **packageUri** takes hello storage account uri which points toohello storage account where you will upload your package zip to.</span></span> <span data-ttu-id="aceaa-127">Hello Azure Resource Manager worden benut als [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull Hallo pakket omlaag lokaal vanuit Hallo opslagaccount wanneer u Hallo sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="aceaa-127">hello Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) toopull hello package down locally from hello storage account when you deploy hello template.</span></span> <span data-ttu-id="aceaa-128">Dit proces wordt uitgevoerd via een PowerShell-script die Hallo-pakket te uploaden en aanroepen hello Azure Management API toocreate Hallo-sleutels vereist en die in de sjabloon Hallo doorgeven als parameters (*_artifactsLocation* en *_artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="aceaa-128">This process will be automated via a PowerShell script that will upload hello package and call hello Azure Management API toocreate hello keys required and pass those into hello template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="aceaa-129">Moet u toodefine parameters voor Hallo-map en bestandsnaam Hallo pakket geüploade toounder Hallo storage-container is.</span><span class="sxs-lookup"><span data-stu-id="aceaa-129">You will need toodefine parameters for hello folder and filename hello package is uploaded toounder hello storage container.</span></span>

<span data-ttu-id="aceaa-130">Vervolgens moet u tooadd in een andere geneste resource toosetup Hallo hostnaam bindingen tooleverage een aangepast domein.</span><span class="sxs-lookup"><span data-stu-id="aceaa-130">Next you need tooadd in another nested resource toosetup hello hostname bindings tooleverage a custom domain.</span></span> <span data-ttu-id="aceaa-131">U gaat eerste nodig tooensure dat u Hallo-hostnaam bezit en toobe instellen geverifieerd door Azure dat jij de eigenaar ervan - Zie [een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="aceaa-131">You will first need tooensure that you own hello hostname and set it up toobe verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="aceaa-132">Wanneer dat is gebeurd, kunt u Hallo tooyour sjabloon onder Hallo Microsoft.Web/sites resourcesectie volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="aceaa-132">Once that is done you can add hello following tooyour template under hello Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="aceaa-133">Tot slot moet u tooadd resource in een andere hoogste niveau, Microsoft.Web/certificates.</span><span class="sxs-lookup"><span data-stu-id="aceaa-133">Finally you need tooadd another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="aceaa-134">Deze bron bevat uw SSL-certificaat en op hetzelfde niveau als uw web-app en hosting van plan bent Hallo aanwezig zal zijn.</span><span class="sxs-lookup"><span data-stu-id="aceaa-134">This resource will contain your SSL certificate and will exist at hello same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="aceaa-135">U moet een geldig SSL-certificaat in de volgorde tooset u deze bron toohave.</span><span class="sxs-lookup"><span data-stu-id="aceaa-135">You will need toohave a valid SSL certificate in order tooset up this resource.</span></span> <span data-ttu-id="aceaa-136">Zodra u die geldig certificaat hebt moet u tooextract Hallo pfx bytes als een base64-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="aceaa-136">Once you have that valid certificate then you need tooextract hello pfx bytes as a base64 string.</span></span> <span data-ttu-id="aceaa-137">Een optie tooextract dit toouse Hallo volgende PowerShell-opdracht is:</span><span class="sxs-lookup"><span data-stu-id="aceaa-137">One option tooextract this is toouse hello following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="aceaa-138">U kan vervolgens doorgegeven als een parameter tooyour ARM-sjabloon voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="aceaa-138">You could then pass this as a parameter tooyour ARM deployment template.</span></span>

<span data-ttu-id="aceaa-139">Op dit moment is Hallo ARM-sjabloon gereed.</span><span class="sxs-lookup"><span data-stu-id="aceaa-139">At this point hello ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="aceaa-140">Sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="aceaa-140">Deploy Template</span></span>
<span data-ttu-id="aceaa-141">Hallo laatste stappen zijn toopiece dit alles samenvoegen in een volledige end-to-end-implementatie.</span><span class="sxs-lookup"><span data-stu-id="aceaa-141">hello final steps are toopiece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="aceaa-142">toomake implementatie gemakkelijker kunt u gebruikmaken van Hallo **implementeren AzureResourceGroup.ps1** PowerShell-script dat wordt toegevoegd wanneer u een Azure-resourcegroepproject in Visual Studio toohelp maken met uploaden van alle artefacten die zijn vereist in Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="aceaa-142">toomake deployment easier you can leverage hello **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio toohelp with uploading of any artifacts required in hello template.</span></span> <span data-ttu-id="aceaa-143">Hiervoor moeten toohave u een opslagaccount dat u wilt dat toouse tevoren gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aceaa-143">It requires you toohave created a storage account you want toouse ahead of time.</span></span> <span data-ttu-id="aceaa-144">In dit voorbeeld moet ik een account met gedeelde opslag voor Hallo pakket.zip toobe geüpload gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aceaa-144">For this example, I created a shared storage account for hello package.zip toobe uploaded.</span></span> <span data-ttu-id="aceaa-145">Hallo-script wordt gebruikmaken van AzCopy tooupload Hallo pakket toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="aceaa-145">hello script will leverage AzCopy tooupload hello package toohello storage account.</span></span> <span data-ttu-id="aceaa-146">U doorgeeft bij de locatie van de artefacten en Hallo script worden alle bestanden in die map toohello storage-container met de naam automatisch uploaden.</span><span class="sxs-lookup"><span data-stu-id="aceaa-146">You pass in your artifact folder location and hello script will automatically upload all files within that directory toohello named storage container.</span></span> <span data-ttu-id="aceaa-147">Na het aanroepen van implementeren AzureResourceGroup.ps1 hebt u toothen Hallo SSL-bindingen toomap Hallo aangepaste hostnaam voor uw SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="aceaa-147">After calling Deploy-AzureResourceGroup.ps1 you have toothen update hello SSL bindings toomap hello custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="aceaa-148">Hallo PowerShell wordt weergegeven na volledige implementatie aanroepen Hallo implementeren Hallo-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="aceaa-148">hello following PowerShell shows hello complete deployment calling hello Deploy-AzureResourceGroup.ps1:</span></span>

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

<span data-ttu-id="aceaa-149">Op dit moment uw toepassing moet zijn geïmplementeerd en u moet kunnen toobrowse tooit via https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="aceaa-149">At this point your application should have been deployed and you should be able toobrowse tooit via https://www.yourcustomdomain.com</span></span>

