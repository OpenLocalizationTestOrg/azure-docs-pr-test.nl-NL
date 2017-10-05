---
title: Windows PowerShell-Scripts gebruiken om te publiceren naar de ontwikkeling en testomgevingen | Microsoft Docs
description: Informatie over het Windows PowerShell-scripts vanuit Visual Studio gebruiken om te publiceren naar de ontwikkeling en testen van omgevingen.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5fff1301-5469-4d97-be88-c85c30f837c1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d4c39eb7a8bc97a980061872ba0f32f375e6976f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-windows-powershell-scripts-to-publish-to-dev-and-test-environments"></a><span data-ttu-id="adc5e-103">Windows PowerShell-scripts gebruiken om ontwikkel- en testomgevingen te publiceren</span><span class="sxs-lookup"><span data-stu-id="adc5e-103">Using Windows PowerShell scripts to publish to dev and test environments</span></span>
<span data-ttu-id="adc5e-104">Wanneer u een webtoepassing in Visual Studio maakt, kunt u een Windows PowerShell-script dat u later gebruiken kunt voor het automatiseren van de publicatie van uw website naar Azure als een Web-App in Azure App Service- of een virtuele machine genereren.</span><span class="sxs-lookup"><span data-stu-id="adc5e-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later to automate the publishing of your website to Azure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="adc5e-105">U kunt bewerken en de Windows PowerShell-script in de Visual Studio-editor om te voldoen aan uw vereisten uitbreiden of het script integreren met bestaande bouwen, testen en publiceren van scripts.</span><span class="sxs-lookup"><span data-stu-id="adc5e-105">You can edit and extend the Windows PowerShell script in the Visual Studio editor to suit your requirements, or integrate the script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="adc5e-106">Deze scripts kunt u aangepaste versies (ook wel bekend als dev- en testomgevingen) van uw site voor tijdelijk gebruik inrichten.</span><span class="sxs-lookup"><span data-stu-id="adc5e-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="adc5e-107">U kunt bijvoorbeeld een bepaalde versie van uw website op een virtuele machine van Azure of op de faseringssleuf op een website op een test-suite uitvoeren, reproduceren een bug, een bug correctie proefversie test een voorgestelde wijziging of instellen van een aangepaste omgeving voor een demo of presentatie instellen.</span><span class="sxs-lookup"><span data-stu-id="adc5e-107">For example, you might set up a particular version of your website on an Azure virtual machine or on the staging slot on a website to run a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="adc5e-108">Nadat u een script dat uw project publiceert hebt gemaakt, kunt u identieke omgevingen door het script opnieuw uit te voeren indien nodig opnieuw of Voer het script met uw eigen build van uw webtoepassing te maken van een aangepaste omgeving voor het testen.</span><span class="sxs-lookup"><span data-stu-id="adc5e-108">After you've created a script that publishes your project, you can recreate identical environments by re-running the script as needed, or run the script with your own build of your web application to create a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="adc5e-109">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="adc5e-109">What you need</span></span>
* <span data-ttu-id="adc5e-110">Azure SDK 2.3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="adc5e-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="adc5e-111">Zie [Visual Studio-Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="adc5e-112">U hoeft niet in de Azure SDK met de scripts voor webprojecten genereren.</span><span class="sxs-lookup"><span data-stu-id="adc5e-112">You do not need the Azure SDK to generate the scripts for web projects.</span></span> <span data-ttu-id="adc5e-113">Deze functie is voor webprojecten, niet webrollen in cloudservices.</span><span class="sxs-lookup"><span data-stu-id="adc5e-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="adc5e-114">Azure PowerShell 0.7.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="adc5e-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="adc5e-115">Zie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-115">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="adc5e-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) of hoger.</span><span class="sxs-lookup"><span data-stu-id="adc5e-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="adc5e-117">Extra hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="adc5e-117">Additional tools</span></span>
<span data-ttu-id="adc5e-118">Extra hulpprogramma's en bronnen voor het werken met PowerShell in Visual Studio voor het ontwikkelen van Azure zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="adc5e-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="adc5e-119">Zie [PowerShell-Tools voor Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="adc5e-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-the-publish-scripts"></a><span data-ttu-id="adc5e-120">Genereren van de scripts publiceren</span><span class="sxs-lookup"><span data-stu-id="adc5e-120">Generating the publish scripts</span></span>
<span data-ttu-id="adc5e-121">U kunt de scripts publiceren voor een virtuele machine die als host fungeert voor uw website wanneer u een nieuw project met de volgende maakt genereren [deze instructies](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="adc5e-121">You can generate the publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="adc5e-122">U kunt ook [genereren van scripts voor web-apps publiceren in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="adc5e-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="adc5e-123">Scripts die door Visual Studio gegenereerd</span><span class="sxs-lookup"><span data-stu-id="adc5e-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="adc5e-124">Visual Studio-oplossing niveau map met de naam gegenereerd **PublishScripts** die bevat twee bestanden van Windows PowerShell, een script publiceren voor de virtuele machine of website en een module die functies die u kunt gebruiken bevat in de scripts.</span><span class="sxs-lookup"><span data-stu-id="adc5e-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in the scripts.</span></span> <span data-ttu-id="adc5e-125">Visual Studio gegenereerd ook een bestand in de JSON-indeling die Hiermee geeft u de details van het project dat u implementeert.</span><span class="sxs-lookup"><span data-stu-id="adc5e-125">Visual Studio also generates a file in the JSON format that specifies the details of the project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="adc5e-126">Windows PowerShell publiceren script</span><span class="sxs-lookup"><span data-stu-id="adc5e-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="adc5e-127">Het script publiceren bevat specifieke Publiceren stappen voor het implementeren van een website of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="adc5e-127">The publish script contains specific publish steps for deploying to a website or virtual machine.</span></span> <span data-ttu-id="adc5e-128">Visual Studio biedt syntaxis kleuren voor de ontwikkeling van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="adc5e-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="adc5e-129">Help voor de functies die beschikbaar is en u de functies in het script wilt aanpassen aan uw veranderende vereisten vrijelijk kunt bewerken.</span><span class="sxs-lookup"><span data-stu-id="adc5e-129">Help for the functions is available, and you can freely edit the functions in the script to suit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="adc5e-130">Windows PowerShell-module</span><span class="sxs-lookup"><span data-stu-id="adc5e-130">Windows PowerShell module</span></span>
<span data-ttu-id="adc5e-131">De Windows PowerShell-module die Visual Studio gegenereerd bevat functies die gebruikmaakt van het script publiceren.</span><span class="sxs-lookup"><span data-stu-id="adc5e-131">The Windows PowerShell module that Visual Studio generates contains functions that the publish script uses.</span></span> <span data-ttu-id="adc5e-132">Deze Azure PowerShell-functies zijn en zijn niet bedoeld om te worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-132">These are Azure PowerShell functions and are not intended to be modified.</span></span> <span data-ttu-id="adc5e-133">Zie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-133">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="adc5e-134">JSON-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="adc5e-134">JSON configuration file</span></span>
<span data-ttu-id="adc5e-135">Het JSON-bestand wordt gemaakt in de **configuraties** map en bevat configuratiegegevens die Hiermee geeft u precies welke resources te implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="adc5e-135">The JSON file is created in the **Configurations** folder and contains configuration data that specifies exactly which resources to deploy to Azure.</span></span> <span data-ttu-id="adc5e-136">De naam van het bestand dat door Visual Studio gegenereerd is project-naam-WAWS-dev.json als u een website of project de naam van VM dev.json gemaakt als u een virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="adc5e-136">The name of the file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="adc5e-137">Hier volgt een voorbeeld van een JSON-configuratiebestand die wordt gegenereerd wanneer u een website hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="adc5e-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="adc5e-138">De meeste van de waarden behoeven geen uitleg.</span><span class="sxs-lookup"><span data-stu-id="adc5e-138">Most of the values are self-explanatory.</span></span> <span data-ttu-id="adc5e-139">Naam van de website wordt gegenereerd door Azure, zodat deze mogelijk niet overeen met de projectnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="adc5e-139">The website name is generated by Azure, so it might not match your project name.</span></span>

```json
{
    "environmentSettings": {
        "webSite": {
            "name": "WebApplication26632",
            "location": "West US"
        },
        "databases": [{
            "connectionStringName": "DefaultConnection",
            "databaseName": "WebApplication26632_db",
            "serverName": "YourDatabaseServerName",
            "user": "sqluser2",
            "password": "",
            "edition": "",
            "size": "",
            "collation": "",
            "location": "West US"
        }]
    }
}
```
<span data-ttu-id="adc5e-140">Wanneer u een virtuele machine maakt, wordt het JSON-configuratiebestand lijkt op het volgende.</span><span class="sxs-lookup"><span data-stu-id="adc5e-140">When you create a virtual machine, the JSON configuration file looks similar to the following.</span></span> <span data-ttu-id="adc5e-141">Houd er rekening mee dat een service in de cloud als een container voor de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="adc5e-141">Note that a cloud service is created as a container for the virtual machine.</span></span> <span data-ttu-id="adc5e-142">De virtuele machine bevat de gebruikelijke eindpunten voor internettoegang via HTTP en HTTPS, evenals de eindpunten voor Web Deploy waarmee u vanuit uw lokale computer, extern bureaublad en Windows PowerShell publiceren naar de website.</span><span class="sxs-lookup"><span data-stu-id="adc5e-142">The virtual machine contains the usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish to the website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

```json
{
    "environmentSettings": {
        "cloudService": {
            "name": "myusernamevm1",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myusernamevm1",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Win2K8R2SP1-Datacenter-201403.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [{
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [{
            "connectionStringName": "",
            "databaseName": "",
            "serverName": "",
            "user": "",
            "password": ""
        }],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

<span data-ttu-id="adc5e-143">U kunt de JSON-configuratie om te wijzigen wat er gebeurt wanneer het uitvoeren van scripts publiceren bewerken.</span><span class="sxs-lookup"><span data-stu-id="adc5e-143">You can edit the JSON configuration to change what happens when you run the publish scripts.</span></span> <span data-ttu-id="adc5e-144">De `cloudService` en `virtualMachine` secties zijn vereist, maar u kunt verwijderen de `databases` sectie als u deze niet nodig.</span><span class="sxs-lookup"><span data-stu-id="adc5e-144">The `cloudService` and `virtualMachine` sections are required, but you can delete the `databases` section if you don't need it.</span></span> <span data-ttu-id="adc5e-145">De eigenschappen die zijn leeg in het configuratiebestand dat Visual Studio gegenereerd zijn optioneel. die waarden in het configuratiebestand zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="adc5e-145">The properties that are empty in the default configuration file that Visual Studio generates are optional; those that have values in the default configuration file are required.</span></span>

<span data-ttu-id="adc5e-146">Als u een website met meerdere implementatieomgevingen (bekend als sleuven) in plaats van een productiesite één in Azure hebt, kunt u de naam van de site op de naam van de website kunt opnemen in het JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="adc5e-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include the slot name in the name of the website in the JSON configuration file.</span></span> <span data-ttu-id="adc5e-147">Bijvoorbeeld, als er een website met de naam **persoonlijke site** en een site voor deze met de naam **testen** en vervolgens de URI persoonlijke site test.cloudapp.net is, maar de juiste naam te gebruiken in het configuratiebestand mysite(test) is.</span><span class="sxs-lookup"><span data-stu-id="adc5e-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then the URI is mysite-test.cloudapp.net, but the correct name to use in the configuration file is mysite(test).</span></span> <span data-ttu-id="adc5e-148">U kunt dit als de website alleen doen en sleuven bestaat al in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="adc5e-148">You can only do this if the website and slots already exist in your subscription.</span></span> <span data-ttu-id="adc5e-149">Als deze nog niet bestaan, maakt u de website door het script zonder op te geven van de sleuf, maak vervolgens de sleuf in de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), en daarna het script uitgevoerd met de naam van de aangepaste website.</span><span class="sxs-lookup"><span data-stu-id="adc5e-149">If they don't exist, create the website by running the script without specifying the slot, then create the slot in the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run the script with the modified website name.</span></span> <span data-ttu-id="adc5e-150">Zie voor meer informatie over implementatiesites voor web-apps, [faseringsomgevingen voor web-apps in Azure App Service instellen](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="adc5e-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-to-run-the-publish-scripts"></a><span data-ttu-id="adc5e-151">Het uitvoeren van de scripts publiceren</span><span class="sxs-lookup"><span data-stu-id="adc5e-151">How to run the publish scripts</span></span>
<span data-ttu-id="adc5e-152">Als u een Windows PowerShell-script voordat nooit hebt uitgevoerd, moet u eerst het uitvoeringsbeleid voor het uitvoeren van scripts inschakelen instellen.</span><span class="sxs-lookup"><span data-stu-id="adc5e-152">If you have never run a Windows PowerShell script before, you must first set the execution policy to enable scripts to run.</span></span> <span data-ttu-id="adc5e-153">Dit is een beveiligingsfunctie om te voorkomen dat gebruikers Windows PowerShell-scripts uitgevoerd als ze kwetsbaar voor schadelijke software en virussen die betrekking hebben op het uitvoeren van scripts.</span><span class="sxs-lookup"><span data-stu-id="adc5e-153">This is a security feature to prevent users from running Windows PowerShell scripts if they're vulnerable to malware or viruses that involve executing scripts.</span></span>

### <a name="run-the-script"></a><span data-ttu-id="adc5e-154">Het script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="adc5e-154">Run the script</span></span>
1. <span data-ttu-id="adc5e-155">Het Web Deploy-pakket voor uw project maken.</span><span class="sxs-lookup"><span data-stu-id="adc5e-155">Create the Web Deploy package for your project.</span></span> <span data-ttu-id="adc5e-156">Een Web Deploy-pakket is een gecomprimeerd archief (ZIP-bestand) met bestanden die u wilt kopiëren naar uw website of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="adc5e-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want to copy to your website or virtual machine.</span></span> <span data-ttu-id="adc5e-157">U kunt Web Deploy-pakketten in Visual Studio maken voor een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="adc5e-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Maken van webinhoud pakket implementeren](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="adc5e-159">Zie voor meer informatie [procedure: een Web-implementatiepakket maken in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="adc5e-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="adc5e-160">U kunt ook het maken van uw pakket Web Deploy automatiseren zoals beschreven in de sectie **aanpassen en uitbreiden van de scripts publiceren** verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="adc5e-160">You can also automate the creation of your Web Deploy package, as described in the section **Customizing and extending the publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="adc5e-161">In **Solution Explorer**, opent u het snelmenu voor het script en kies vervolgens **openen met de PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="adc5e-161">In **Solution Explorer**, open the context menu for the script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="adc5e-162">Als dit de eerste keer dat u Windows PowerShell-scripts op deze computer uitvoeren hebt, open een opdrachtpromptvenster met Administrator-bevoegdheden en typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="adc5e-162">If this is the first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type the following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="adc5e-163">Aanmelden bij Azure met behulp van de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="adc5e-163">Sign in to Azure by using the following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="adc5e-164">Als u wordt gevraagd, geeft u uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="adc5e-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="adc5e-165">Houd er rekening mee dat wanneer u het script automatiseren, deze methode van het bieden van Azure-referenties werken niet.</span><span class="sxs-lookup"><span data-stu-id="adc5e-165">Note that when you automate the script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="adc5e-166">In plaats daarvan moet u de .publishsettings-bestand gebruiken om referenties te verstrekken.</span><span class="sxs-lookup"><span data-stu-id="adc5e-166">Instead, you should use the .publishsettings file to provide credentials.</span></span> <span data-ttu-id="adc5e-167">Één keer alleen u de opdracht gebruiken **Get-AzurePublishSettingsFile** downloaden van het bestand in Azure, en daarna gebruiken **importeren AzurePublishSettingsFile** het bestand te importeren.</span><span class="sxs-lookup"><span data-stu-id="adc5e-167">One time only, you use the command **Get-AzurePublishSettingsFile** to download the file from Azure, and thereafter use **Import-AzurePublishSettingsFile** to import the file.</span></span> <span data-ttu-id="adc5e-168">Zie voor gedetailleerde instructies [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="adc5e-168">For detailed instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="adc5e-169">(Optioneel) Als u maken van Azure-resources, zoals de virtuele machine wilt, database en een website zonder het publiceren van uw webtoepassing gebruikt het **publiceren WebApplication.ps1** opdracht met de **-configuratie**argument ingesteld op het JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="adc5e-169">(Optional) If you want to create Azure resources such as the virtual machine, database, and website without publishing your web application, use the **Publish-WebApplication.ps1** command with the **-Configuration** argument set to the JSON configuration file.</span></span> <span data-ttu-id="adc5e-170">Met deze opdrachtregel maakt gebruik van het JSON-configuratiebestand om te bepalen welke resources om te maken.</span><span class="sxs-lookup"><span data-stu-id="adc5e-170">This command line uses the JSON configuration file to determine which resources to create.</span></span> <span data-ttu-id="adc5e-171">Omdat deze gebruikmaakt van de standaardinstellingen voor andere opdrachtregelargumenten, maakt u de resources, maar uw webtoepassing niet publiceren.</span><span class="sxs-lookup"><span data-stu-id="adc5e-171">Because it uses the default settings for other command-line arguments, it creates the resources, but doesn't publish your web application.</span></span> <span data-ttu-id="adc5e-172">De uitgebreide optie vindt u meer informatie over wat er gebeurt.</span><span class="sxs-lookup"><span data-stu-id="adc5e-172">The –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="adc5e-173">Gebruik de **publiceren WebApplication.ps1** opdracht zoals weergegeven in een van de volgende voorbeelden voor het aanroepen van het script en publiceren van uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="adc5e-173">Use the **Publish-WebApplication.ps1** command as shown in one of the following examples to invoke the script and publish your web application.</span></span> <span data-ttu-id="adc5e-174">Als u wilt overschrijven de standaardinstellingen voor een van de argumenten, zoals de naam van het abonnement, publiceren pakketnaam, de referenties van de virtuele machine of de referenties voor de database, kunt u deze parameters opgeven.</span><span class="sxs-lookup"><span data-stu-id="adc5e-174">If you need to override the default settings for any of the other arguments, such as the subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="adc5e-175">Gebruik de **– uitgebreid** optie voor meer informatie over de voortgang van het publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="adc5e-175">Use the **–Verbose** option to see more information about the progress of the publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="adc5e-176">Als u een virtuele machine maakt, wordt de opdracht ziet er als volgt.</span><span class="sxs-lookup"><span data-stu-id="adc5e-176">If you're creating a virtual machine, the command looks like the following.</span></span> <span data-ttu-id="adc5e-177">Dit voorbeeld toont ook de referenties voor meerdere databases opgeven.</span><span class="sxs-lookup"><span data-stu-id="adc5e-177">This example also shows how to specify the credentials for multiple databases.</span></span> <span data-ttu-id="adc5e-178">Voor de virtuele machines die deze scripts maken, is het SSL-certificaat niet uit een vertrouwde basiscertificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-178">For the virtual machines that these scripts create, the SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="adc5e-179">Daarom moet u gebruiken de **– AllowUntrusted** optie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-179">Therefore, you need to use the **–AllowUntrusted** option.</span></span>

    ```powershell
    Publish-WebApplication.ps1 `
    -Configuration C:\Path\ADVM-VM-test.json `
    -SubscriptionName Contoso `
    -WebDeployPackage C:\Path\ADVM.zip `
    -AllowUntrusted `
    -VMPassword @{name = "vmUserName"; password = "YourPasswordHere"} `
    -DatabaseServerPassword @{Name="server1";Password="adminPassword1"}, @{Name="server2";Password="adminPassword2"} `
    -Verbose
    ```

    <span data-ttu-id="adc5e-180">Het script databases kunt maken, maar het database-servers niet maken.</span><span class="sxs-lookup"><span data-stu-id="adc5e-180">The script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="adc5e-181">Als u maken van een databaseserver wilt, kunt u de **nieuw AzureSqlDatabaseServer** functie in de Azure-module.</span><span class="sxs-lookup"><span data-stu-id="adc5e-181">If you want to create a database server, you can use the **New-AzureSqlDatabaseServer** function in the Azure module.</span></span>

## <a name="customizing-and-extending-the-publish-scripts"></a><span data-ttu-id="adc5e-182">Aanpassen en uitbreiden van de scripts publiceren</span><span class="sxs-lookup"><span data-stu-id="adc5e-182">Customizing and extending the publish scripts</span></span>
<span data-ttu-id="adc5e-183">U kunt het script voor publiceren en de JSON-configuratiebestand aanpassen.</span><span class="sxs-lookup"><span data-stu-id="adc5e-183">You can customize the publish script and JSON configuration file.</span></span> <span data-ttu-id="adc5e-184">De functies in de Windows PowerShell-module **AzureWebAppPublishModule.psm1** zijn niet bedoeld om te worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-184">The functions in the Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended to be modified.</span></span> <span data-ttu-id="adc5e-185">Als u alleen wilt opgeven van een andere database of enkele van de eigenschappen van de virtuele machine wijzigen, bewerkt u het JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="adc5e-185">If you just want to specify a different database or change some of the properties of the virtual machine, edit the JSON configuration file.</span></span> <span data-ttu-id="adc5e-186">Als u uitbreiden van de functies van het script wilt te maken en testen van uw project te automatiseren, kunt u de functie stubs in implementeren **publiceren WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="adc5e-186">If you want to extend the functionality of the script to automate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="adc5e-187">Voor het automatiseren van uw project te bouwen, voeg code MSBuild naar roept `New-WebDeployPackage` zoals in dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="adc5e-187">To automate building your project, add code that calls MSBuild to `New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="adc5e-188">Het pad naar de MSBuild-opdracht is verschillend, afhankelijk van de versie van Visual Studio die u hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-188">The path to the MSBuild command is different depending on the version of Visual Studio you have installed.</span></span> <span data-ttu-id="adc5e-189">Als u het juiste pad, kunt u de functie **Get-MSBuildCmd**, zoals wordt weergegeven in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="adc5e-189">To get the correct path, you can use the function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="to-automate-building-your-project"></a><span data-ttu-id="adc5e-190">Voor het automatiseren van uw project te bouwen</span><span class="sxs-lookup"><span data-stu-id="adc5e-190">To automate building your project</span></span>
1. <span data-ttu-id="adc5e-191">Voeg de `$ProjectFile` parameter in de sectie globale param.</span><span class="sxs-lookup"><span data-stu-id="adc5e-191">Add the `$ProjectFile` parameter in the global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="adc5e-192">Kopieer de functie `Get-MSBuildCmd` in het scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="adc5e-192">Copy the function `Get-MSBuildCmd` into your script file.</span></span>

    ```powershell
    function Get-MSBuildCmd
    {
            process
    {

                $path =  Get-ChildItem "HKLM:\SOFTWARE\Microsoft\MSBuild\ToolsVersions\" |
                                    Sort-Object {[double]$_.PSChildName} -Descending |
                                    Select-Object -First 1 |
                                    Get-ItemProperty -Name MSBuildToolsPath |
                                    Select -ExpandProperty MSBuildToolsPath

                $path = (Join-Path -Path $path -ChildPath 'msbuild.exe')

            return Get-Item $path
        }
    }
    ```

3. <span data-ttu-id="adc5e-193">Vervang `New-WebDeployPackage` met de volgende code en vervang de tijdelijke aanduidingen in het construeren van de regel `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="adc5e-193">Replace `New-WebDeployPackage` with the following code and replace the placeholders in the line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="adc5e-194">Deze code is voor Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="adc5e-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="adc5e-195">Als u Visual Studio 2013, wijzigt u de **VisualStudioVersion** eigenschap hieronder `12.0`.</span><span class="sxs-lookup"><span data-stu-id="adc5e-195">If you're using Visual Studio 2013, change the **VisualStudioVersion** property below to `12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function to build and package your web application
    ```

    <span data-ttu-id="adc5e-196">Gebruik voor het bouwen van uw webtoepassing, MsBuild.exe.</span><span class="sxs-lookup"><span data-stu-id="adc5e-196">To build your web application, use MsBuild.exe.</span></span> <span data-ttu-id="adc5e-197">Zie voor informatie over MSBuild-Naslaggids op: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="adc5e-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-the-build-command"></a><span data-ttu-id="adc5e-198">Uitvoering van de opdracht build starten</span><span class="sxs-lookup"><span data-stu-id="adc5e-198">Start execution of the build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain the project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct the path to web deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get the full path for the web deploy zip package. This is required for MSDeploy to work
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="adc5e-199">Roep de `New-WebDeployPackage` functie voordat deze regel: `$Config = Read-ConfigFile $Configuration` voor web-apps of `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="adc5e-199">Call the `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="adc5e-200">Aanroepen van het aangepaste script vanaf de opdrachtregel doorgegeven met de `$Project` argument, zoals in het volgende voorbeeld-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="adc5e-200">Invoke the customized script from command line using passing the `$Project` argument, as in the following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="adc5e-201">Voor het automatiseren van uw toepassing testen, voeg code toe aan `Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="adc5e-201">To automate testing of your application, add code to `Test-WebApplication`.</span></span> <span data-ttu-id="adc5e-202">Zorg ervoor dat de regels in opmerking verwijderen **publiceren WebApplication.ps1** waar deze functies worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="adc5e-202">Be sure to uncomment the lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="adc5e-203">Als u een implementatie niet opgeeft, kunt u handmatig bouwen van uw project met Visual Studio en voer het script publiceren om te publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="adc5e-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run the publish script to publish to Azure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="adc5e-204">Publishing functie samenvatting</span><span class="sxs-lookup"><span data-stu-id="adc5e-204">Publishing function summary</span></span>
<span data-ttu-id="adc5e-205">Voor informatie over functies die u bij de opdrachtprompt van Windows PowerShell gebruiken kunt, gebruikt u de opdracht `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="adc5e-205">To get help for functions you can use at the Windows PowerShell command prompt, use the command `Get-Help function-name`.</span></span> <span data-ttu-id="adc5e-206">De help bevat parameter help en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="adc5e-206">The help includes parameter help and examples.</span></span> <span data-ttu-id="adc5e-207">De dezelfde help-tekst is ook in de script-bronbestanden **AzureWebAppPublishModule.psm1** en **publiceren WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="adc5e-207">The same help text is also in the script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="adc5e-208">Het script en de help worden in uw taal Visual Studio gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-208">The script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="adc5e-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="adc5e-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="adc5e-210">Functienaam</span><span class="sxs-lookup"><span data-stu-id="adc5e-210">Function name</span></span> | <span data-ttu-id="adc5e-211">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="adc5e-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="adc5e-212">Voeg AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="adc5e-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="adc5e-213">Maakt een nieuwe Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="adc5e-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="adc5e-214">Voeg AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="adc5e-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="adc5e-215">Azure SQL-databases maakt van de waarden in het JSON-configuratiebestand dat Visual Studio gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-215">Creates Azure SQL databases from the values in the JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="adc5e-216">-AzureVM</span><span class="sxs-lookup"><span data-stu-id="adc5e-216">Add-AzureVM</span></span> |<span data-ttu-id="adc5e-217">Een virtuele machine in Azure maakt en retourneert de URL van de geïmplementeerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="adc5e-217">Creates a Azure virtual machine and returns the URL of the deployed VM.</span></span> <span data-ttu-id="adc5e-218">De functie stelt u de vereisten en roept vervolgens de **New-AzureVM** functie (Azure module) voor het maken van een nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="adc5e-218">The function sets up the prerequisites and then calls the **New-AzureVM** function (Azure module) to create a new virtual machine.</span></span> |
| <span data-ttu-id="adc5e-219">Voeg AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="adc5e-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="adc5e-220">Nieuwe invoereindpunten toegevoegd aan een virtuele machine en de virtuele machine met het nieuwe eindpunt retourneert.</span><span class="sxs-lookup"><span data-stu-id="adc5e-220">Adds new input endpoints to a virtual machine and returns the virtual machine with the new endpoint.</span></span> |
| <span data-ttu-id="adc5e-221">Voeg AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="adc5e-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="adc5e-222">Maakt een nieuwe Azure storage-account in het huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="adc5e-222">Creates a new Azure storage account in the current subscription.</span></span> <span data-ttu-id="adc5e-223">De naam van het account begint met 'devtest' gevolgd door een unieke alfanumerieke tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="adc5e-223">The name of the account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="adc5e-224">De functie retourneert de naam van het nieuwe opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="adc5e-224">The function returns the name of the new storage account.</span></span> <span data-ttu-id="adc5e-225">U moet een locatie of een affiniteitsgroep voor het nieuwe opslagaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="adc5e-225">You must specify either a location or an affinity group for the new storage account.</span></span> |
| <span data-ttu-id="adc5e-226">Voeg AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="adc5e-226">Add-AzureWebsite</span></span> |<span data-ttu-id="adc5e-227">Hiermee maakt een website met de opgegeven naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-227">Creates a website with the specified name and location.</span></span> <span data-ttu-id="adc5e-228">Deze functie roept de **nieuw AzureWebsite** functie in de Azure-module.</span><span class="sxs-lookup"><span data-stu-id="adc5e-228">This function calls the **New-AzureWebsite** function in the Azure module.</span></span> <span data-ttu-id="adc5e-229">Als het abonnement niet al een website met de opgegeven naam bevat, wordt deze functie wordt gemaakt van de website en een website-object geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-229">If the subscription doesn't already include a website with the specified name, this function creates the website and returns a website object.</span></span> <span data-ttu-id="adc5e-230">Anders is het resultaat `$null`.</span><span class="sxs-lookup"><span data-stu-id="adc5e-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="adc5e-231">Back-up-abonnement</span><span class="sxs-lookup"><span data-stu-id="adc5e-231">Backup-Subscription</span></span> |<span data-ttu-id="adc5e-232">Hiermee slaat u het huidige Azure-abonnement in de `$Script:originalSubscription` variabele in script-bereik. Deze functie slaat de huidige Azure-abonnement (verkregen met `Get-AzureSubscription -Current`) en de storage-account en het abonnement dat door dit script wordt gewijzigd (opgeslagen in de variabele `$UserSpecifiedSubscription`) en de opslagaccount in script-bereik.</span><span class="sxs-lookup"><span data-stu-id="adc5e-232">Saves the current Azure subscription in the `$Script:originalSubscription` variable in script scope.This function saves the current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and the subscription that is changed by this script (stored in the variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="adc5e-233">Als u de waarden opslaat, kunt u een functie, zoals `Restore-Subscription`, om te herstellen van de oorspronkelijke huidige abonnement en storage-account naar de huidige status als de huidige status is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-233">By saving the values, you can use a function, such as `Restore-Subscription`, to restore the original current subscription and storage account to current status if the current status has changed.</span></span> |
| <span data-ttu-id="adc5e-234">Zoek-AzureVM</span><span class="sxs-lookup"><span data-stu-id="adc5e-234">Find-AzureVM</span></span> |<span data-ttu-id="adc5e-235">Hiermee haalt u de opgegeven virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="adc5e-235">Gets the specified Azure virtual machine.</span></span> |
| <span data-ttu-id="adc5e-236">Indeling DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="adc5e-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="adc5e-237">Voegt toe de datum en tijd aan een bericht.</span><span class="sxs-lookup"><span data-stu-id="adc5e-237">Prepends the date and time to a message.</span></span> <span data-ttu-id="adc5e-238">Deze functie is ontworpen voor berichten die naar de fout en uitgebreid stromen worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="adc5e-238">This function is designed for messages written to the Error and Verbose streams.</span></span> |
| <span data-ttu-id="adc5e-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="adc5e-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="adc5e-240">Ophaalprotocol een verbindingsreeks verbinding maken met een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="adc5e-240">Assembles a connection string to connect to an Azure SQL database.</span></span> |
| <span data-ttu-id="adc5e-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="adc5e-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="adc5e-242">Retourneert de naam van het eerste storage-account met het naampatroon ' devtest*' (hoofdlettergevoelig) in de opgegeven locatie of affiniteitsgroep. Als de "devtest*' storage-account komt niet overeen met de locatie of affiniteitsgroep, de functie negeert deze.</span><span class="sxs-lookup"><span data-stu-id="adc5e-242">Returns the name of the first storage account with the name pattern "devtest*" (case insensitive) in the specified location or affinity group. If the "devtest*" storage account doesn't match the location or affinity group, the function ignores it.</span></span> <span data-ttu-id="adc5e-243">U moet een locatie of een affiniteitsgroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="adc5e-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="adc5e-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="adc5e-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="adc5e-245">Retourneert een opdracht voor het hulpprogramma MsDeploy.exe uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="adc5e-245">Returns a command to run the MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="adc5e-246">Nieuwe AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="adc5e-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="adc5e-247">Zoeken naar of maakt een virtuele machine in het abonnement dat overeenkomt met de waarden in het JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="adc5e-247">Finds or creates a virtual machine in the subscription that matches the values in the JSON configuration file.</span></span> |
| <span data-ttu-id="adc5e-248">Publiceren WebPackage</span><span class="sxs-lookup"><span data-stu-id="adc5e-248">Publish-WebPackage</span></span> |<span data-ttu-id="adc5e-249">Maakt gebruik van MsDeploy.exe en een web-pakket niet publiceren. ZIP-bestand voor het implementeren van resources met een website.</span><span class="sxs-lookup"><span data-stu-id="adc5e-249">Uses MsDeploy.exe and a web publish package .Zip file to deploy resources to a website.</span></span> <span data-ttu-id="adc5e-250">Deze functie biedt geen uitvoer gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-250">This function doesn't generate any output.</span></span> <span data-ttu-id="adc5e-251">Als de aanroep van MSDeploy.exe mislukt, wordt de functie genereert een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="adc5e-251">If the call to MSDeploy.exe fails, the function throws an exception.</span></span> <span data-ttu-id="adc5e-252">Als u meer gedetailleerde uitvoer, gebruikt de **-uitgebreide** optie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-252">To get more detailed output, use the **-Verbose** option.</span></span> |
| <span data-ttu-id="adc5e-253">Publiceren WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="adc5e-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="adc5e-254">Controleert of de parameterwaarden en roept vervolgens de **publiceren WebPackage** functie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-254">Verifies the parameter values, and then calls the **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="adc5e-255">Lees ConfigFile</span><span class="sxs-lookup"><span data-stu-id="adc5e-255">Read-ConfigFile</span></span> |<span data-ttu-id="adc5e-256">Valideert het JSON-configuratiebestand en retourneert een hashtabel met geselecteerde waarden.</span><span class="sxs-lookup"><span data-stu-id="adc5e-256">Validates the JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="adc5e-257">Restore-abonnement</span><span class="sxs-lookup"><span data-stu-id="adc5e-257">Restore-Subscription</span></span> |<span data-ttu-id="adc5e-258">Hiermee stelt het huidige abonnement op het oorspronkelijke abonnement.</span><span class="sxs-lookup"><span data-stu-id="adc5e-258">Resets the current subscription to the original subscription.</span></span> |
| <span data-ttu-id="adc5e-259">Test AzureModule</span><span class="sxs-lookup"><span data-stu-id="adc5e-259">Test-AzureModule</span></span> |<span data-ttu-id="adc5e-260">Retourneert `$true` als de versie van de geïnstalleerde Azure module 0.7.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="adc5e-260">Returns `$true` if the installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="adc5e-261">Retourneert `$false` als de module is niet geïnstalleerd of een eerdere versie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-261">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="adc5e-262">Deze functie heeft geen parameters.</span><span class="sxs-lookup"><span data-stu-id="adc5e-262">This function has no parameters.</span></span> |
| <span data-ttu-id="adc5e-263">Test AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="adc5e-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="adc5e-264">Retourneert `$true` als de versie van de Azure-module 0.7.4 is of hoger.</span><span class="sxs-lookup"><span data-stu-id="adc5e-264">Returns `$true` if the version of the Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="adc5e-265">Retourneert `$false` als de module is niet geïnstalleerd of een eerdere versie.</span><span class="sxs-lookup"><span data-stu-id="adc5e-265">Returns `$false` if the module isn't installed or is an earlier version.</span></span> <span data-ttu-id="adc5e-266">Deze functie heeft geen parameters.</span><span class="sxs-lookup"><span data-stu-id="adc5e-266">This function has no parameters.</span></span> |
| <span data-ttu-id="adc5e-267">Test HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="adc5e-267">Test-HttpsUrl</span></span> |<span data-ttu-id="adc5e-268">De invoer-URL wordt omgezet in een System.Uri-object.</span><span class="sxs-lookup"><span data-stu-id="adc5e-268">Converts the input URL to a System.Uri object.</span></span> <span data-ttu-id="adc5e-269">Retourneert `$True` als de URL absoluut is en het bijbehorende schema https is.</span><span class="sxs-lookup"><span data-stu-id="adc5e-269">Returns `$True` if the URL is absolute and its scheme is https.</span></span> <span data-ttu-id="adc5e-270">Retourneert `$false` als de URL relatief is, het schema is niet HTTPS of de ingevoerde tekenreeks kan niet worden geconverteerd naar een URL.</span><span class="sxs-lookup"><span data-stu-id="adc5e-270">Returns `$false` if the URL is relative, its scheme isn't HTTPS, or the input string can't be converted to a URL.</span></span> |
| <span data-ttu-id="adc5e-271">Test-lid</span><span class="sxs-lookup"><span data-stu-id="adc5e-271">Test-Member</span></span> |<span data-ttu-id="adc5e-272">Retourneert `$true` als een eigenschap of methode lid is van het object.</span><span class="sxs-lookup"><span data-stu-id="adc5e-272">Returns `$true` if a property or method is a member of the object.</span></span> <span data-ttu-id="adc5e-273">Anders retourneert `$false`.</span><span class="sxs-lookup"><span data-stu-id="adc5e-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="adc5e-274">Schrijven ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="adc5e-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="adc5e-275">Schrijft een foutbericht dat wordt voorafgegaan door de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-275">Writes an error message prefixed with the current time.</span></span> <span data-ttu-id="adc5e-276">Deze functie roept de **indeling DevTestMessageWithTime** functie toevoegen van de tijd voordat het bericht schrijven naar de stroom van de fout aan.</span><span class="sxs-lookup"><span data-stu-id="adc5e-276">This function calls the **Format-DevTestMessageWithTime** function to prepend the time before writing the message to the Error stream.</span></span> |
| <span data-ttu-id="adc5e-277">Schrijven HostWithTime</span><span class="sxs-lookup"><span data-stu-id="adc5e-277">Write-HostWithTime</span></span> |<span data-ttu-id="adc5e-278">Schrijft u een bericht naar het hostprogramma (**Write-Host**) voorafgegaan door de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-278">Writes a message to the host program (**Write-Host**) prefixed with the current time.</span></span> <span data-ttu-id="adc5e-279">Het effect van het schrijven naar het hostprogramma varieert.</span><span class="sxs-lookup"><span data-stu-id="adc5e-279">The effect of writing to the host program varies.</span></span> <span data-ttu-id="adc5e-280">De meeste programma's die als host fungeren voor Windows PowerShell deze berichten schrijven naar de standaarduitvoer.</span><span class="sxs-lookup"><span data-stu-id="adc5e-280">Most programs that host Windows PowerShell write these messages to standard output.</span></span> |
| <span data-ttu-id="adc5e-281">Schrijven VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="adc5e-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="adc5e-282">Schrijft een uitgebreid bericht voorafgegaan door de huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-282">Writes a verbose message prefixed with the current time.</span></span> <span data-ttu-id="adc5e-283">Omdat deze wordt aangeroepen **Write-Verbose**, het bericht geeft alleen wanneer het script wordt uitgevoerd met de **uitgebreid** parameter of wanneer de **VerbosePreference** voorkeur is ingesteld op  **Doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="adc5e-283">Because it calls **Write-Verbose**, the message displays only when the script runs with the **Verbose** parameter or when the **VerbosePreference** preference is set to **Continue**.</span></span> |

<span data-ttu-id="adc5e-284">**Publiceren WebApplication**</span><span class="sxs-lookup"><span data-stu-id="adc5e-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="adc5e-285">Functienaam</span><span class="sxs-lookup"><span data-stu-id="adc5e-285">Function name</span></span> | <span data-ttu-id="adc5e-286">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="adc5e-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="adc5e-287">Nieuwe AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="adc5e-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="adc5e-288">Azure-resources, zoals een website of virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="adc5e-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="adc5e-289">Nieuwe WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="adc5e-289">New-WebDeployPackage</span></span> |<span data-ttu-id="adc5e-290">Deze functie is niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-290">This function isn't implemented.</span></span> <span data-ttu-id="adc5e-291">In deze functie om uw project te bouwen, kunt u opdrachten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="adc5e-291">You can add commands in this function to build your project.</span></span> |
| <span data-ttu-id="adc5e-292">Publiceren AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="adc5e-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="adc5e-293">Een webtoepassing naar Azure publiceert.</span><span class="sxs-lookup"><span data-stu-id="adc5e-293">Publishes a web application to Azure.</span></span> |
| <span data-ttu-id="adc5e-294">Publiceren WebApplication</span><span class="sxs-lookup"><span data-stu-id="adc5e-294">Publish-WebApplication</span></span> |<span data-ttu-id="adc5e-295">Maakt en Web-Apps, virtuele machines, SQL-databases en storage-accounts voor een Visual Studio-webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="adc5e-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="adc5e-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="adc5e-296">Test-WebApplication</span></span> |<span data-ttu-id="adc5e-297">Deze functie is niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="adc5e-297">This function isn't implemented.</span></span> <span data-ttu-id="adc5e-298">U kunt de opdrachten in deze functie voor het testen van uw toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="adc5e-298">You can add commands in this function to test your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="adc5e-299">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="adc5e-299">Next steps</span></span>
<span data-ttu-id="adc5e-300">Meer informatie over PowerShell-scripts door te lezen [met Windows PowerShell-scripts](https://technet.microsoft.com/library/bb978526.aspx) en Zie andere Azure PowerShell-scripts op de [Script Center](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="adc5e-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at the [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
