---
title: MSDeploy met hostnaam en ssl-certificaat met een web-app implementeren
description: Een Azure Resource Manager-sjabloon gebruiken voor het implementeren van een web-app met behulp van MSDeploy en aangepaste hostnaam en een SSL-certificaat instellen
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
ms.openlocfilehash: a0e944d0d74ecb72a919538d54db330cbbdeef64
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-web-app-with-msdeploy-custom-hostname-and-ssl-certificate"></a><span data-ttu-id="70f2b-103">Een web-app met MSDeploy, aangepaste hostnaam en SSL-certificaat implementeren</span><span class="sxs-lookup"><span data-stu-id="70f2b-103">Deploy a web app with MSDeploy, custom hostname and SSL certificate</span></span>
<span data-ttu-id="70f2b-104">Deze handleiding helpt bij het maken van de implementatie van een end-to-end voor een Azure-Web-App, gebruik van MSDeploy, evenals een aangepaste hostnaam en een SSL-certificaat toevoegen aan de ARM-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="70f2b-104">This guide walks through creating an end-to-end deployment for an Azure Web App, leveraging MSDeploy as well as adding a custom hostname and an SSL certificate to the ARM template.</span></span>

<span data-ttu-id="70f2b-105">Zie voor meer informatie over het maken van sjablonen [Azure Resource Manager-sjablonen ontwerpen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="70f2b-105">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

### <a name="create-sample-application"></a><span data-ttu-id="70f2b-106">Voorbeeld van een toepassing maken</span><span class="sxs-lookup"><span data-stu-id="70f2b-106">Create Sample Application</span></span>
<span data-ttu-id="70f2b-107">U implementeert een ASP.NET-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="70f2b-107">You will be deploying an ASP.NET web application.</span></span> <span data-ttu-id="70f2b-108">De eerste stap is om een eenvoudige webtoepassing te maken (of kunt u het gebruik van een bestaande - in dat geval kunt u deze stap overslaan).</span><span class="sxs-lookup"><span data-stu-id="70f2b-108">The first step is to create a simple web application (or you could choose to use an existing one - in which case you can skip this step).</span></span>

<span data-ttu-id="70f2b-109">Open Visual Studio 2015 en kies Bestand > Nieuw Project.</span><span class="sxs-lookup"><span data-stu-id="70f2b-109">Open Visual Studio 2015 and choose File > New Project.</span></span> <span data-ttu-id="70f2b-110">Kies in het dialoogvenster dat verschijnt Web > ASP.NET-webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="70f2b-110">On the dialog that appears choose Web > ASP.NET Web Application.</span></span> <span data-ttu-id="70f2b-111">Kies Web onder sjablonen en kies de MVC-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="70f2b-111">Under Templates choose Web and choose the MVC template.</span></span> <span data-ttu-id="70f2b-112">Selecteer *verificatietype wijzigen* naar *geen verificatie*.</span><span class="sxs-lookup"><span data-stu-id="70f2b-112">Select *Change authentication type* to *No Authentication*.</span></span> <span data-ttu-id="70f2b-113">Dit dient alleen voor de voorbeeldtoepassing zo eenvoudig mogelijk te maken.</span><span class="sxs-lookup"><span data-stu-id="70f2b-113">This is just to make the sample application as simple as possible.</span></span>

<span data-ttu-id="70f2b-114">Op dit moment hebt u een eenvoudige ASP.Net web-app gereed om te gebruiken als onderdeel van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="70f2b-114">At this point you will have a basic ASP.Net web app ready to use as part of your deployment process.</span></span>

### <a name="create-msdeploy-package"></a><span data-ttu-id="70f2b-115">MSDeploy-pakket maken</span><span class="sxs-lookup"><span data-stu-id="70f2b-115">Create MSDeploy package</span></span>
<span data-ttu-id="70f2b-116">Volgende stap is het maken van het pakket voor het implementeren van de web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="70f2b-116">Next step is to create the package to deploy the web app to Azure.</span></span> <span data-ttu-id="70f2b-117">Om dit te doen, sla het project en voer de volgende vanaf de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="70f2b-117">To do this, save your project and then run the following from the command line:</span></span>

    msbuild yourwebapp.csproj /t:Package /p:PackageLocation="path\to\package.zip"

<span data-ttu-id="70f2b-118">Hiermee wordt een gecomprimeerde pakket onder de map PackageLocation gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70f2b-118">This will create a zipped package under the PackageLocation folder.</span></span> <span data-ttu-id="70f2b-119">De toepassing is nu gereed om te worden geïmplementeerd, die u kunt nu opbouwen uit een Azure Resource Manager-sjabloon dat doet.</span><span class="sxs-lookup"><span data-stu-id="70f2b-119">The application is now ready to be deployed, which you can now build out an Azure Resource Manager template to do that.</span></span>

### <a name="create-arm-template"></a><span data-ttu-id="70f2b-120">ARM-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="70f2b-120">Create ARM Template</span></span>
<span data-ttu-id="70f2b-121">Eerst laten we beginnen met een eenvoudige ARM-sjabloon die u maakt een webtoepassing en een hosting plan (opmerking die parameters en variabelen niet als beknopt alternatief bevat weergegeven worden).</span><span class="sxs-lookup"><span data-stu-id="70f2b-121">First, let's start with a basic ARM template that will create a web application and a hosting plan (note that parameters and variables are not shown for brevity).</span></span>

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

<span data-ttu-id="70f2b-122">Vervolgens moet u de resource voor de web-app om een geneste MSDeploy-resource te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="70f2b-122">Next, you will need to modify the web app resource to take a nested MSDeploy resource.</span></span> <span data-ttu-id="70f2b-123">Hierdoor kunt u om te verwijzen naar het pakket eerder hebt gemaakt en Azure Resource Manager het pakket naar de Azure-Web-App implementeren met MSDeploy zien.</span><span class="sxs-lookup"><span data-stu-id="70f2b-123">This will allow you to reference the package created earlier and tell Azure Resource Manager to use MSDeploy to deploy the package to the Azure WebApp.</span></span> <span data-ttu-id="70f2b-124">Hieronder ziet u de bron Microsoft.Web/sites met de geneste MSDeploy-resource:</span><span class="sxs-lookup"><span data-stu-id="70f2b-124">The following shows the Microsoft.Web/sites resource with the nested MSDeploy resource:</span></span>

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

<span data-ttu-id="70f2b-125">Nu u ziet dat de resource MSDeploy duurt voordat een **packageUri** eigenschap die is gedefinieerd als volgt:</span><span class="sxs-lookup"><span data-stu-id="70f2b-125">Now you will notice that the MSDeploy resource takes a **packageUri** property which is defined as follows:</span></span>

    "packageUri": "[concat(parameters('_artifactsLocation'), '/', parameters('webDeployPackageFolder'), '/', parameters('webDeployPackageFileName'), parameters('_artifactsLocationSasToken'))]"

<span data-ttu-id="70f2b-126">Dit **packageUri** neemt de storage-account-uri die verwijst naar het opslagaccount waar u zult uploaden uw postcode pakket op.</span><span class="sxs-lookup"><span data-stu-id="70f2b-126">This **packageUri** takes the storage account uri which points to the storage account where you will upload your package zip to.</span></span> <span data-ttu-id="70f2b-127">De Azure Resource Manager worden benut [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) voor het ophalen van het pakket naar beneden lokaal vanuit het opslagaccount wanneer u de sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="70f2b-127">The Azure Resource Manager will leverage [Shared Access Signatures](../storage/common/storage-dotnet-shared-access-signature-part-1.md) to pull the package down locally from the storage account when you deploy the template.</span></span> <span data-ttu-id="70f2b-128">Dit proces wordt uitgevoerd via een PowerShell-script die uploaden van het pakket en roept u de Azure Management-API voor het maken van de vereiste sleutels en geef die naar de sjabloon als parameters (*_artifactsLocation* en *_ artifactsLocationSasToken*).</span><span class="sxs-lookup"><span data-stu-id="70f2b-128">This process will be automated via a PowerShell script that will upload the package and call the Azure Management API to create the keys required and pass those into the template as parameters (*_artifactsLocation* and *_artifactsLocationSasToken*).</span></span> <span data-ttu-id="70f2b-129">U moet de parameters definiëren voor de map en bestandsnaam van het pakket is geüpload naar onder de storage-container.</span><span class="sxs-lookup"><span data-stu-id="70f2b-129">You will need to define parameters for the folder and filename the package is uploaded to under the storage container.</span></span>

<span data-ttu-id="70f2b-130">Vervolgens moet u in een andere geneste resource voor het instellen van de hostnaambindings wilt gebruiken voor een aangepast domein toevoegen.</span><span class="sxs-lookup"><span data-stu-id="70f2b-130">Next you need to add in another nested resource to setup the hostname bindings to leverage a custom domain.</span></span> <span data-ttu-id="70f2b-131">Moet u eerst om ervoor te zorgen dat u de hostnaam en het kan worden gecontroleerd door Azure dat jij de eigenaar ervan - Zie eigenaar [een aangepaste domeinnaam configureren in Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="70f2b-131">You will first need to ensure that you own the hostname and set it up to be verified by Azure that you own it - see [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span> <span data-ttu-id="70f2b-132">Wanneer dat is gebeurd, kunt u het volgende kunt toevoegen aan de sjabloon onder de sectie Microsoft.Web/sites resource:</span><span class="sxs-lookup"><span data-stu-id="70f2b-132">Once that is done you can add the following to your template under the Microsoft.Web/sites resource section:</span></span>

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

<span data-ttu-id="70f2b-133">Tot slot moet u een andere bovenste niveau resource, Microsoft.Web/certificates toevoegen.</span><span class="sxs-lookup"><span data-stu-id="70f2b-133">Finally you need to add another top level resource, Microsoft.Web/certificates.</span></span> <span data-ttu-id="70f2b-134">Deze bron uw SSL-certificaat bevat en wordt aangelegd op hetzelfde niveau als uw web-app en hosting plannen.</span><span class="sxs-lookup"><span data-stu-id="70f2b-134">This resource will contain your SSL certificate and will exist at the same level as your web app and hosting plan.</span></span>

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

<span data-ttu-id="70f2b-135">U moet een geldig SSL-certificaat hebben om het instellen van deze resource.</span><span class="sxs-lookup"><span data-stu-id="70f2b-135">You will need to have a valid SSL certificate in order to set up this resource.</span></span> <span data-ttu-id="70f2b-136">Zodra u die geldig certificaat hebt moet u het pfx-bytes extraheren als een base64-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="70f2b-136">Once you have that valid certificate then you need to extract the pfx bytes as a base64 string.</span></span> <span data-ttu-id="70f2b-137">Een optie om op te halen dit is het gebruik van de volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="70f2b-137">One option to extract this is to use the following PowerShell command:</span></span>

    $fileContentBytes = get-content 'C:\path\to\cert.pfx' -Encoding Byte

    [System.Convert]::ToBase64String($fileContentBytes) | Out-File 'pfx-bytes.txt'

<span data-ttu-id="70f2b-138">U kan vervolgens dit als een parameter doorgeven aan de ARM-sjabloon voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="70f2b-138">You could then pass this as a parameter to your ARM deployment template.</span></span>

<span data-ttu-id="70f2b-139">De ARM-sjabloon is nu gereed.</span><span class="sxs-lookup"><span data-stu-id="70f2b-139">At this point the ARM template is ready.</span></span>

### <a name="deploy-template"></a><span data-ttu-id="70f2b-140">Sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="70f2b-140">Deploy Template</span></span>
<span data-ttu-id="70f2b-141">De laatste stappen zijn om dit alles samenvoegen in een volledige end-to-end-implementatie.</span><span class="sxs-lookup"><span data-stu-id="70f2b-141">The final steps are to piece this all together into a full end-to-end deployment.</span></span> <span data-ttu-id="70f2b-142">Om ervoor te implementatie gemakkelijker u gebruikmaken van kunt de **implementeren AzureResourceGroup.ps1** PowerShell-script dat wordt toegevoegd wanneer u een Azure-resourcegroepproject in Visual Studio om u te helpen maken bij het uploaden van alle artefacten die zijn vereist in de de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="70f2b-142">To make deployment easier you can leverage the **Deploy-AzureResourceGroup.ps1** PowerShell script that is added when you create an Azure Resource Group project in Visual Studio to help with uploading of any artifacts required in the template.</span></span> <span data-ttu-id="70f2b-143">Deze moet u een opslagaccount dat u wilt gebruiken tevoren hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70f2b-143">It requires you to have created a storage account you want to use ahead of time.</span></span> <span data-ttu-id="70f2b-144">In dit voorbeeld gemaakt ik een account met gedeelde opslag voor de pakket.zip worden geüpload.</span><span class="sxs-lookup"><span data-stu-id="70f2b-144">For this example, I created a shared storage account for the package.zip to be uploaded.</span></span> <span data-ttu-id="70f2b-145">Het script wordt gebruikmaken van AzCopy om het uploaden van het pakket naar het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="70f2b-145">The script will leverage AzCopy to upload the package to the storage account.</span></span> <span data-ttu-id="70f2b-146">U doorgeeft bij de locatie van de artefacten en het script worden alle bestanden in die map automatisch uploaden naar de benoemde storage-container.</span><span class="sxs-lookup"><span data-stu-id="70f2b-146">You pass in your artifact folder location and the script will automatically upload all files within that directory to the named storage container.</span></span> <span data-ttu-id="70f2b-147">U hebt na het aanroepen van implementeren AzureResourceGroup.ps1 en werk vervolgens de SSL-bindingen als u wilt toewijzen van de aangepaste hostnaam vervolgens met de SSL-certificaat.</span><span class="sxs-lookup"><span data-stu-id="70f2b-147">After calling Deploy-AzureResourceGroup.ps1 you have to then update the SSL bindings to map the custom hostname with your SSL certificate.</span></span>

<span data-ttu-id="70f2b-148">De volledige implementatie aanroepen van de implementeren ziet u de volgende PowerShell-AzureResourceGroup.ps1:</span><span class="sxs-lookup"><span data-stu-id="70f2b-148">The following PowerShell shows the complete deployment calling the Deploy-AzureResourceGroup.ps1:</span></span>

    #Set resource group name
    $rgName = "Name-of-resource-group"

    #call deploy-azureresourcegroup script to deploy web app

    .\Deploy-AzureResourceGroup.ps1 -ResourceGroupLocation "East US" `
                                    -ResourceGroupName $rgName `
                                    -UploadArtifacts `
                                    -StorageAccountName "name-of-storage-acct-for-package" `
                                    -StorageAccountResourceGroupName "resource-group-name-storage-acct" `
                                    -TemplateFile "web-app-deploy.json" `
                                    -TemplateParametersFile "web-app-deploy-parameters.json" `
                                    -ArtifactStagingDirectory "C:\path\to\packagefolder\"

    #update web app to bind ssl certificate to hostname. This has to be done after creation above.

    $cert = Get-PfxCertificate -FilePath C:\path\to\certificate.pfx

    $ar = Get-AzureRmResource -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -ApiVersion 2014-11-01

    $props = $ar.Properties

    $props.HostNameSslStates[2].'SslState' = 1
    $props.HostNameSslStates[2].'thumbprint' = $cert.Thumbprint
    $props.hostNameSslStates[2].'toUpdate' = $true

    Set-AzureRmResource -ApiVersion 2014-11-01 -Name nameofwebsite -ResourceGroupName $rgName -ResourceType Microsoft.Web/sites -PropertyObject $props

<span data-ttu-id="70f2b-149">Op dit moment uw toepassing moet zijn geïmplementeerd en moet u kunnen te bladeren via https://www.yourcustomdomain.com</span><span class="sxs-lookup"><span data-stu-id="70f2b-149">At this point your application should have been deployed and you should be able to browse to it via https://www.yourcustomdomain.com</span></span>

