---
title: aaaUsing Windows PowerShell-Scripts tooPublish tooDev en testomgevingen | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell scripts vanuit Visual Studio toopublish toodevelopment en testomgevingen.
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
ms.openlocfilehash: 491a058f96255576afa74f6156f20ae9559bb9f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-powershell-scripts-toopublish-toodev-and-test-environments"></a><span data-ttu-id="8534c-103">Met Windows PowerShell scripts toopublish toodev en testomgevingen</span><span class="sxs-lookup"><span data-stu-id="8534c-103">Using Windows PowerShell scripts toopublish toodev and test environments</span></span>
<span data-ttu-id="8534c-104">Wanneer u een webtoepassing in Visual Studio maakt, kunt u een Windows PowerShell-script dat u later tooautomate Hallo-publicatie van uw website tooAzure als een Web-App in Azure App Service- of een virtuele machine gebruiken kunt genereren.</span><span class="sxs-lookup"><span data-stu-id="8534c-104">When you create a web application in Visual Studio, you can generate a Windows PowerShell script that you can use later tooautomate hello publishing of your website tooAzure as a Web App in Azure App Service or a virtual machine.</span></span> <span data-ttu-id="8534c-105">U kunt bewerken en uw vereisten voor Windows PowerShell-script in Hallo Visual Studio-editor toosuit Hallo uitbreiden of Hallo script integreren met bestaande bouwen, testen en publiceren scripts.</span><span class="sxs-lookup"><span data-stu-id="8534c-105">You can edit and extend hello Windows PowerShell script in hello Visual Studio editor toosuit your requirements, or integrate hello script with existing build, test, and publishing scripts.</span></span>

<span data-ttu-id="8534c-106">Deze scripts kunt u aangepaste versies (ook wel bekend als dev- en testomgevingen) van uw site voor tijdelijk gebruik inrichten.</span><span class="sxs-lookup"><span data-stu-id="8534c-106">Using these scripts, you can provision customized versions (also known as dev and test environments) of your site for temporary use.</span></span> <span data-ttu-id="8534c-107">U kan bijvoorbeeld instellen van een bepaalde versie van uw website op een virtuele machine van Azure of op Hallo staging site op een website toorun een test-suite, een bug reproduceren, een bug correctie proefversie test een voorgestelde wijziging of instellen van een aangepaste omgeving voor een demo of presentatie.</span><span class="sxs-lookup"><span data-stu-id="8534c-107">For example, you might set up a particular version of your website on an Azure virtual machine or on hello staging slot on a website toorun a test suite, reproduce a bug, test a bug fix, trial a proposed change, or set up a custom environment for a demo or presentation.</span></span> <span data-ttu-id="8534c-108">Nadat u een script dat uw project publiceert hebt gemaakt, kunt u identieke omgevingen door Hallo script opnieuw uit te voeren indien nodig opnieuw of Hallo script uitgevoerd met uw eigen build van uw toepassing web toocreate een aangepaste omgeving voor het testen.</span><span class="sxs-lookup"><span data-stu-id="8534c-108">After you've created a script that publishes your project, you can recreate identical environments by re-running hello script as needed, or run hello script with your own build of your web application toocreate a custom environment for testing.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8534c-109">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="8534c-109">What you need</span></span>
* <span data-ttu-id="8534c-110">Azure SDK 2.3 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8534c-110">Azure SDK 2.3 or later.</span></span> <span data-ttu-id="8534c-111">Zie [Visual Studio-Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8534c-111">See [Visual Studio Downloads](http://go.microsoft.com/fwlink/?LinkID=624384) for more information.</span></span>

<span data-ttu-id="8534c-112">U hoeft niet hello Azure SDK toogenerate Hallo scripts voor webprojecten.</span><span class="sxs-lookup"><span data-stu-id="8534c-112">You do not need hello Azure SDK toogenerate hello scripts for web projects.</span></span> <span data-ttu-id="8534c-113">Deze functie is voor webprojecten, niet webrollen in cloudservices.</span><span class="sxs-lookup"><span data-stu-id="8534c-113">This feature is for web projects, not web roles in cloud services.</span></span>

* <span data-ttu-id="8534c-114">Azure PowerShell 0.7.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8534c-114">Azure PowerShell 0.7.4 or later.</span></span> <span data-ttu-id="8534c-115">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8534c-115">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="8534c-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) of hoger.</span><span class="sxs-lookup"><span data-stu-id="8534c-116">[Windows PowerShell 3.0](http://go.microsoft.com/?linkid=9811175) or later.</span></span>

## <a name="additional-tools"></a><span data-ttu-id="8534c-117">Extra hulpprogramma 's</span><span class="sxs-lookup"><span data-stu-id="8534c-117">Additional tools</span></span>
<span data-ttu-id="8534c-118">Extra hulpprogramma's en bronnen voor het werken met PowerShell in Visual Studio voor het ontwikkelen van Azure zijn beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="8534c-118">Additional tools and resources for working with PowerShell in Visual Studio for Azure development are available.</span></span> <span data-ttu-id="8534c-119">Zie [PowerShell-Tools voor Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span><span class="sxs-lookup"><span data-stu-id="8534c-119">See [PowerShell Tools for Visual Studio](http://go.microsoft.com/fwlink/?LinkId=404012).</span></span>

## <a name="generating-hello-publish-scripts"></a><span data-ttu-id="8534c-120">Scripts genereren Hallo publiceren</span><span class="sxs-lookup"><span data-stu-id="8534c-120">Generating hello publish scripts</span></span>
<span data-ttu-id="8534c-121">U kunt genereren Hallo publiceren scripts voor een virtuele machine die als host fungeert voor uw website wanneer u een nieuw project met de volgende maakt [deze instructies](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8534c-121">You can generate hello publish scripts for a virtual machine that hosts your website when you create a new project by following [these instructions](virtual-machines/windows/classic/web-app-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="8534c-122">U kunt ook [genereren van scripts voor web-apps publiceren in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="8534c-122">You can also [generate publish scripts for web apps in Azure App Service](app-service-web/app-service-web-get-started-dotnet.md).</span></span>

## <a name="scripts-that-visual-studio-generates"></a><span data-ttu-id="8534c-123">Scripts die door Visual Studio gegenereerd</span><span class="sxs-lookup"><span data-stu-id="8534c-123">Scripts that Visual Studio generates</span></span>
<span data-ttu-id="8534c-124">Visual Studio-oplossing niveau map met de naam gegenereerd **PublishScripts** die twee Windows PowerShell-bestanden bevat een script publiceren voor de virtuele machine of website en een module die bevat functies die u kunt in hello gebruiken scripts.</span><span class="sxs-lookup"><span data-stu-id="8534c-124">Visual Studio generates a solution-level folder called **PublishScripts** that contains two Windows PowerShell files, a publish script for your virtual machine or website, and a module that contains functions that you can use in hello scripts.</span></span> <span data-ttu-id="8534c-125">Een bestand Visual Studio ook gegenereerd in JSON-indeling voor Hallo waarmee Hallo-details van Hallo-project die u implementeert.</span><span class="sxs-lookup"><span data-stu-id="8534c-125">Visual Studio also generates a file in hello JSON format that specifies hello details of hello project you are deploying.</span></span>

### <a name="windows-powershell-publish-script"></a><span data-ttu-id="8534c-126">Windows PowerShell publiceren script</span><span class="sxs-lookup"><span data-stu-id="8534c-126">Windows PowerShell publish script</span></span>
<span data-ttu-id="8534c-127">Hallo publiceren script bevat specifieke stappen voor het implementeren van tooa website of virtuele machine te publiceren.</span><span class="sxs-lookup"><span data-stu-id="8534c-127">hello publish script contains specific publish steps for deploying tooa website or virtual machine.</span></span> <span data-ttu-id="8534c-128">Visual Studio biedt syntaxis kleuren voor de ontwikkeling van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8534c-128">Visual Studio provides syntax coloring for Windows PowerShell development.</span></span> <span data-ttu-id="8534c-129">Help voor Hallo functies beschikbaar is en u kunt Hallo-functies in Hallo script toosuit uw veranderende vereisten vrijelijk bewerken.</span><span class="sxs-lookup"><span data-stu-id="8534c-129">Help for hello functions is available, and you can freely edit hello functions in hello script toosuit your changing requirements.</span></span>

### <a name="windows-powershell-module"></a><span data-ttu-id="8534c-130">Windows PowerShell-module</span><span class="sxs-lookup"><span data-stu-id="8534c-130">Windows PowerShell module</span></span>
<span data-ttu-id="8534c-131">Windows PowerShell-module die Visual Studio gegenereerd bevat functies die Hallo Hallo publiceren script gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8534c-131">hello Windows PowerShell module that Visual Studio generates contains functions that hello publish script uses.</span></span> <span data-ttu-id="8534c-132">Dit zijn functies van Azure PowerShell en geen beoogde toobe gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8534c-132">These are Azure PowerShell functions and are not intended toobe modified.</span></span> <span data-ttu-id="8534c-133">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8534c-133">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>

### <a name="json-configuration-file"></a><span data-ttu-id="8534c-134">JSON-configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="8534c-134">JSON configuration file</span></span>
<span data-ttu-id="8534c-135">Hallo JSON-bestand wordt gemaakt in Hallo **configuraties** map en configuratiegegevens die Hiermee geeft u precies welke resources toodeploy tooAzure bevat.</span><span class="sxs-lookup"><span data-stu-id="8534c-135">hello JSON file is created in hello **Configurations** folder and contains configuration data that specifies exactly which resources toodeploy tooAzure.</span></span> <span data-ttu-id="8534c-136">Hallo-naam van Hallo-bestand dat door Visual Studio gegenereerd is project-naam-WAWS-dev.json als u een website of project de naam van VM dev.json gemaakt als u een virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8534c-136">hello name of hello file that Visual Studio generates is project-name-WAWS-dev.json if you created a website, or project name-VM-dev.json if you created a virtual machine.</span></span> <span data-ttu-id="8534c-137">Hier volgt een voorbeeld van een JSON-configuratiebestand die wordt gegenereerd wanneer u een website hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8534c-137">Here's an example of a JSON configuration file that's generated when you create a website.</span></span> <span data-ttu-id="8534c-138">De meeste waarden Hallo behoeven geen uitleg.</span><span class="sxs-lookup"><span data-stu-id="8534c-138">Most of hello values are self-explanatory.</span></span> <span data-ttu-id="8534c-139">naam van de website Hello wordt gegenereerd door Azure, zodat deze mogelijk niet overeen met de projectnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="8534c-139">hello website name is generated by Azure, so it might not match your project name.</span></span>

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
<span data-ttu-id="8534c-140">Wanneer u een virtuele machine maakt, lijkt de JSON-configuratiebestand Hallo vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="8534c-140">When you create a virtual machine, hello JSON configuration file looks similar toohello following.</span></span> <span data-ttu-id="8534c-141">Houd er rekening mee dat een service in de cloud als een container voor Hallo virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8534c-141">Note that a cloud service is created as a container for hello virtual machine.</span></span> <span data-ttu-id="8534c-142">Hallo virtuele machine bevat Hallo gebruikelijke eindpunten voor internettoegang via HTTP en HTTPS, evenals de eindpunten voor Web Deploy waarmee u toohello website vanuit uw lokale computer, extern bureaublad en Windows PowerShell publiceren.</span><span class="sxs-lookup"><span data-stu-id="8534c-142">hello virtual machine contains hello usual endpoints for web access through HTTP and HTTPS, as well as endpoints for Web Deploy, which lets you publish toohello website from your local machine, Remote Desktop, and Windows PowerShell.</span></span>

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

<span data-ttu-id="8534c-143">U kunt bewerken Hallo JSON configuratie toochange wat er gebeurt tijdens het uitvoeren van Hallo scripts publiceren.</span><span class="sxs-lookup"><span data-stu-id="8534c-143">You can edit hello JSON configuration toochange what happens when you run hello publish scripts.</span></span> <span data-ttu-id="8534c-144">Hallo `cloudService` en `virtualMachine` secties zijn vereist, maar u kunt verwijderen Hallo `databases` sectie als u deze niet nodig.</span><span class="sxs-lookup"><span data-stu-id="8534c-144">hello `cloudService` and `virtualMachine` sections are required, but you can delete hello `databases` section if you don't need it.</span></span> <span data-ttu-id="8534c-145">Hallo-eigenschappen die zijn leeg in het configuratiebestand van het Hallo-standaard die door Visual Studio gegenereerd zijn optioneel. die waarden in het standaardconfiguratiebestand Hallo zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="8534c-145">hello properties that are empty in hello default configuration file that Visual Studio generates are optional; those that have values in hello default configuration file are required.</span></span>

<span data-ttu-id="8534c-146">Als u een website met meerdere implementatieomgevingen (bekend als sleuven) in plaats van een productiesite één in Azure hebt, kunt u de naam van de site Hallo in Hallo-naam van Hallo-website in JSON-configuratiebestand Hallo kunt opnemen.</span><span class="sxs-lookup"><span data-stu-id="8534c-146">If you have a website that has multiple deployment environments (known as slots) instead of a single production site in Azure, you can include hello slot name in hello name of hello website in hello JSON configuration file.</span></span> <span data-ttu-id="8534c-147">Bijvoorbeeld, als er een website met de naam **persoonlijke site** en een site voor deze met de naam **testen** vervolgens Hallo URI persoonlijke site test.cloudapp.net is, maar Hallo juiste naam toouse in Hallo-configuratiebestand mysite(test) is .</span><span class="sxs-lookup"><span data-stu-id="8534c-147">For example, if you have a website that's named **mysite** and a slot for it named **test** then hello URI is mysite-test.cloudapp.net, but hello correct name toouse in hello configuration file is mysite(test).</span></span> <span data-ttu-id="8534c-148">U kunt dit alleen doen als het Hallo-website en sleuven al in uw abonnement bestaat.</span><span class="sxs-lookup"><span data-stu-id="8534c-148">You can only do this if hello website and slots already exist in your subscription.</span></span> <span data-ttu-id="8534c-149">Als deze nog niet bestaan, Hallo website maken met een Hallo script zonder op te geven Hallo sleuf en maak vervolgens Hallo sleuf in Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), en daarna Hallo script uitgevoerd met de naam van de aangepaste website Hallo.</span><span class="sxs-lookup"><span data-stu-id="8534c-149">If they don't exist, create hello website by running hello script without specifying hello slot, then create hello slot in hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), and thereafter run hello script with hello modified website name.</span></span> <span data-ttu-id="8534c-150">Zie voor meer informatie over implementatiesites voor web-apps, [faseringsomgevingen voor web-apps in Azure App Service instellen](app-service-web/web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8534c-150">For more information about deployment slots for web apps, see [Set up staging environments for web apps in Azure App Service](app-service-web/web-sites-staged-publishing.md).</span></span>

## <a name="how-toorun-hello-publish-scripts"></a><span data-ttu-id="8534c-151">Hoe toorun Hallo scripts publiceren</span><span class="sxs-lookup"><span data-stu-id="8534c-151">How toorun hello publish scripts</span></span>
<span data-ttu-id="8534c-152">Als u een Windows PowerShell-script voordat nooit hebt uitgevoerd, moet u eerst Hallo uitvoering beleid tooenable scripts toorun instellen.</span><span class="sxs-lookup"><span data-stu-id="8534c-152">If you have never run a Windows PowerShell script before, you must first set hello execution policy tooenable scripts toorun.</span></span> <span data-ttu-id="8534c-153">Dit is een functie voor beveiliging tooprevent gebruikers Windows PowerShell-scripts worden uitgevoerd als ze kwetsbaar toomalware of virussen die betrekking hebben op het uitvoeren van scripts.</span><span class="sxs-lookup"><span data-stu-id="8534c-153">This is a security feature tooprevent users from running Windows PowerShell scripts if they're vulnerable toomalware or viruses that involve executing scripts.</span></span>

### <a name="run-hello-script"></a><span data-ttu-id="8534c-154">Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8534c-154">Run hello script</span></span>
1. <span data-ttu-id="8534c-155">Web Deploy Hallo-pakket voor uw project maken.</span><span class="sxs-lookup"><span data-stu-id="8534c-155">Create hello Web Deploy package for your project.</span></span> <span data-ttu-id="8534c-156">Een Web Deploy-pakket is een gecomprimeerd archief (ZIP-bestand) met bestanden die u wilt toocopy tooyour website of virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8534c-156">A Web Deploy package is a compressed archive (.zip file) that contain files that you want toocopy tooyour website or virtual machine.</span></span> <span data-ttu-id="8534c-157">U kunt Web Deploy-pakketten in Visual Studio maken voor een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="8534c-157">You can create Web Deploy packages in Visual Studio for any web application.</span></span>

![Maken van webinhoud pakket implementeren](./media/vs-azure-tools-publishing-using-powershell-scripts/IC767885.png)

<span data-ttu-id="8534c-159">Zie voor meer informatie [procedure: een Web-implementatiepakket maken in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span><span class="sxs-lookup"><span data-stu-id="8534c-159">For more information, see [How to: Create a Web Deployment Package in Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx).</span></span> <span data-ttu-id="8534c-160">U kunt ook Hallo maken van uw Web Deploy-pakket, automatiseren zoals beschreven in de sectie Hallo **aanpassen en uitbreiden van Hallo publiceren scripts** verderop in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="8534c-160">You can also automate hello creation of your Web Deploy package, as described in hello section **Customizing and extending hello publish scripts** later in this topic.</span></span>

1. <span data-ttu-id="8534c-161">In **Solution Explorer**, open Hallo contextmenu voor Hallo script en kies vervolgens **openen met de PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="8534c-161">In **Solution Explorer**, open hello context menu for hello script, and then choose **Open with PowerShell ISE**.</span></span>
2. <span data-ttu-id="8534c-162">Als dit Hallo eerst die u Windows PowerShell-scripts op deze computer uitvoeren hebt, open een opdrachtpromptvenster met Administrator-bevoegdheden en type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8534c-162">If this is hello first time you've run Windows PowerShell scripts on this computer, open a command prompt window with Administrator privileges and type hello following command:</span></span>

    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```

3. <span data-ttu-id="8534c-163">Meld u tooAzure met behulp van de volgende opdracht Hallo.</span><span class="sxs-lookup"><span data-stu-id="8534c-163">Sign in tooAzure by using hello following command.</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="8534c-164">Als u wordt gevraagd, geeft u uw gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8534c-164">When prompted, supply your username and password.</span></span>

    <span data-ttu-id="8534c-165">Houd er rekening mee dat wanneer u Hallo script automatiseren, deze methode van het bieden van Azure-referenties werken niet.</span><span class="sxs-lookup"><span data-stu-id="8534c-165">Note that when you automate hello script, this method of providing Azure credentials won't work.</span></span> <span data-ttu-id="8534c-166">In plaats daarvan moet u Hallo .publishsettings-bestand tooprovide referenties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8534c-166">Instead, you should use hello .publishsettings file tooprovide credentials.</span></span> <span data-ttu-id="8534c-167">Één keer alleen u Hallo-opdracht gebruiken **Get-AzurePublishSettingsFile** toodownload Hallo bestand van Azure, en gebruik daarna **importeren AzurePublishSettingsFile** tooimport Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="8534c-167">One time only, you use hello command **Get-AzurePublishSettingsFile** toodownload hello file from Azure, and thereafter use **Import-AzurePublishSettingsFile** tooimport hello file.</span></span> <span data-ttu-id="8534c-168">Zie voor gedetailleerde instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8534c-168">For detailed instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

4. <span data-ttu-id="8534c-169">(Optioneel) Als u wilt dat toocreate Azure-resources, zoals Hallo virtuele machine, database en website zonder het publiceren van uw webtoepassing hello gebruiken **publiceren WebApplication.ps1** opdracht Hello **-configuratie** argument ingesteld toohello JSON-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="8534c-169">(Optional) If you want toocreate Azure resources such as hello virtual machine, database, and website without publishing your web application, use hello **Publish-WebApplication.ps1** command with hello **-Configuration** argument set toohello JSON configuration file.</span></span> <span data-ttu-id="8534c-170">Met deze opdrachtregel wordt Hallo JSON configuration file toodetermine welke resources toocreate gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8534c-170">This command line uses hello JSON configuration file toodetermine which resources toocreate.</span></span> <span data-ttu-id="8534c-171">Omdat Hallo standaardinstellingen worden gebruikt voor andere opdrachtregelargumenten, Hallo resources maakt, maar uw webtoepassing niet publiceren.</span><span class="sxs-lookup"><span data-stu-id="8534c-171">Because it uses hello default settings for other command-line arguments, it creates hello resources, but doesn't publish your web application.</span></span> <span data-ttu-id="8534c-172">Hallo-biedt optie Verbose u meer informatie over wat er gebeurt.</span><span class="sxs-lookup"><span data-stu-id="8534c-172">hello –Verbose option gives you more information about what's happening.</span></span>

    ```powershell
    Publish-WebApplication.ps1 -Verbose –Configuration C:\Path\WebProject-WAWS-dev.json
    ```

5. <span data-ttu-id="8534c-173">Gebruik Hallo **publiceren WebApplication.ps1** opdracht zoals weergegeven in een van de Hallo voorbeelden tooinvoke Hallo script volgen en publiceren van uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="8534c-173">Use hello **Publish-WebApplication.ps1** command as shown in one of hello following examples tooinvoke hello script and publish your web application.</span></span> <span data-ttu-id="8534c-174">Als u andere argumenten, zoals de naam voor het abonnement van Hallo toooverride Hallo standaardinstellingen voor alle Hallo moet publiceren pakketnaam, de referenties van de virtuele machine of de referenties voor de database, kunt u deze parameters opgeven.</span><span class="sxs-lookup"><span data-stu-id="8534c-174">If you need toooverride hello default settings for any of hello other arguments, such as hello subscription name, publish package name, virtual machine credentials, or database server credentials, you can specify those parameters.</span></span> <span data-ttu-id="8534c-175">Gebruik Hallo **– uitgebreid** optie toosee meer informatie over de voortgang van Hallo Hallo publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="8534c-175">Use hello **–Verbose** option toosee more information about hello progress of hello publishing process.</span></span>

    ```powershell
    Publish-WebApplication.ps1 –Configuration C:\Path\WebProject-WAWS-dev-json `
    –SubscriptionName Contoso `
    -WebDeployPackage C:\Documents\Azure\ADWebApp.zip `
    -DatabaseServerPassword @{Name="dbServerName";Password="adminPassword"} `
    -Verbose
    ```

    <span data-ttu-id="8534c-176">Als u een virtuele machine maakt, eruit Hallo opdracht Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="8534c-176">If you're creating a virtual machine, hello command looks like hello following.</span></span> <span data-ttu-id="8534c-177">In dit voorbeeld ziet ook hoe toospecify Hallo-referenties voor meerdere databases.</span><span class="sxs-lookup"><span data-stu-id="8534c-177">This example also shows how toospecify hello credentials for multiple databases.</span></span> <span data-ttu-id="8534c-178">Hallo virtuele machines die deze scripts maken, is Hallo SSL-certificaat niet van een vertrouwde basiscertificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="8534c-178">For hello virtual machines that these scripts create, hello SSL certificate is not from a trusted root authority.</span></span> <span data-ttu-id="8534c-179">Daarom moet u toouse hello **– AllowUntrusted** optie.</span><span class="sxs-lookup"><span data-stu-id="8534c-179">Therefore, you need toouse hello **–AllowUntrusted** option.</span></span>

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

    <span data-ttu-id="8534c-180">Hallo script databases kunt maken, maar het database-servers niet maken.</span><span class="sxs-lookup"><span data-stu-id="8534c-180">hello script can create databases, but it doesn't create database servers.</span></span> <span data-ttu-id="8534c-181">Als u een databaseserver toocreate wilt, kunt u Hallo **nieuw AzureSqlDatabaseServer** functie in hello Azure-module.</span><span class="sxs-lookup"><span data-stu-id="8534c-181">If you want toocreate a database server, you can use hello **New-AzureSqlDatabaseServer** function in hello Azure module.</span></span>

## <a name="customizing-and-extending-hello-publish-scripts"></a><span data-ttu-id="8534c-182">Aanpassen en uitbreiden Hallo publiceren scripts</span><span class="sxs-lookup"><span data-stu-id="8534c-182">Customizing and extending hello publish scripts</span></span>
<span data-ttu-id="8534c-183">U kunt aanpassen Hallo script en JSON-configuratiebestand publiceren.</span><span class="sxs-lookup"><span data-stu-id="8534c-183">You can customize hello publish script and JSON configuration file.</span></span> <span data-ttu-id="8534c-184">functies in Windows PowerShell-module Hallo Hallo **AzureWebAppPublishModule.psm1** zijn niet bedoeld toobe gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8534c-184">hello functions in hello Windows PowerShell module **AzureWebAppPublishModule.psm1** are not intended toobe modified.</span></span> <span data-ttu-id="8534c-185">Als u alleen toospecify een andere database of bepaalde Hallo eigenschappen van Hallo virtuele machine wijzigen, moet u Hallo JSON-configuratiebestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="8534c-185">If you just want toospecify a different database or change some of hello properties of hello virtual machine, edit hello JSON configuration file.</span></span> <span data-ttu-id="8534c-186">Als u wilt dat tooextend Hallo functionaliteit van Hallo script tooautomate maken en testen van uw project, kunt u de functie stubs in implementeren **publiceren WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="8534c-186">If you want tooextend hello functionality of hello script tooautomate building and testing your project, you can implement function stubs in **Publish-WebApplication.ps1**.</span></span>

<span data-ttu-id="8534c-187">het bouwen van uw project tooautomate code toevoegen die MSBuild-aanroepen te`New-WebDeployPackage` zoals in dit codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8534c-187">tooautomate building your project, add code that calls MSBuild too`New-WebDeployPackage` as shown in this code example.</span></span> <span data-ttu-id="8534c-188">Hallo pad toohello MSBuild-opdracht is verschillend, afhankelijk van het Hallo-versie van Visual Studio die u hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-188">hello path toohello MSBuild command is different depending on hello version of Visual Studio you have installed.</span></span> <span data-ttu-id="8534c-189">tooget Hallo juiste pad, kunt u de functie Hallo **Get-MSBuildCmd**, zoals wordt weergegeven in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8534c-189">tooget hello correct path, you can use hello function **Get-MSBuildCmd**, as shown in this example.</span></span>

### <a name="tooautomate-building-your-project"></a><span data-ttu-id="8534c-190">tooautomate bouwen van uw project</span><span class="sxs-lookup"><span data-stu-id="8534c-190">tooautomate building your project</span></span>
1. <span data-ttu-id="8534c-191">Hallo toevoegen `$ProjectFile` parameter in Hallo globale param sectie.</span><span class="sxs-lookup"><span data-stu-id="8534c-191">Add hello `$ProjectFile` parameter in hello global param section.</span></span>

    ```powershell
    [Parameter(Mandatory = $false)]
    [ValidateScript({Test-Path $_ -PathType Leaf})]
    [String]
    $ProjectFile,
    ```

2. <span data-ttu-id="8534c-192">Hallo functie kopiëren `Get-MSBuildCmd` in het scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="8534c-192">Copy hello function `Get-MSBuildCmd` into your script file.</span></span>

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

3. <span data-ttu-id="8534c-193">Vervang `New-WebDeployPackage` Hello volgende code en vervang de tijdelijke aanduidingen Hallo bij het maken van de regel Hallo `$msbuildCmd`.</span><span class="sxs-lookup"><span data-stu-id="8534c-193">Replace `New-WebDeployPackage` with hello following code and replace hello placeholders in hello line constructing `$msbuildCmd`.</span></span> <span data-ttu-id="8534c-194">Deze code is voor Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="8534c-194">This code is for Visual Studio 2015.</span></span> <span data-ttu-id="8534c-195">Als u Visual Studio 2013, wijzigt u Hallo **VisualStudioVersion** eigenschap hieronder te`12.0`.</span><span class="sxs-lookup"><span data-stu-id="8534c-195">If you're using Visual Studio 2013, change hello **VisualStudioVersion** property below too`12.0`.</span></span>

    ```powershell
    function New-WebDeployPackage
    {
        #Write a function toobuild and package your web application
    ```

    <span data-ttu-id="8534c-196">toobuild uw webtoepassing, MsBuild.exe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8534c-196">toobuild your web application, use MsBuild.exe.</span></span> <span data-ttu-id="8534c-197">Zie voor informatie over MSBuild-Naslaggids op: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span><span class="sxs-lookup"><span data-stu-id="8534c-197">For help, see MSBuild Command-Line Reference at: [http://go.microsoft.com/fwlink/?LinkId=391339](http://go.microsoft.com/fwlink/?LinkId=391339)</span></span>

    ```powershell
    Write-VerboseWithTime 'Build-WebDeployPackage: Start'

    $msbuildCmd = '"{0}" "{1}" /T:Rebuild;Package /P:VisualStudioVersion=14.0 /p:OutputPath="{2}\MSBuildOutputPath" /flp:logfile=msbuild.log,v=d' -f (Get-MSBuildCmd), $ProjectFile, $scriptDirectory

    Write-VerboseWithTime ('Build-WebDeployPackage: ' + $msbuildCmd)
    ```

### <a name="start-execution-of-hello-build-command"></a><span data-ttu-id="8534c-198">Uitvoering van de opdracht build Hallo starten</span><span class="sxs-lookup"><span data-stu-id="8534c-198">Start execution of hello build command</span></span>

```powershell
$job = Start-Process cmd.exe -ArgumentList('/C "' + $msbuildCmd + '"') -WindowStyle Normal -Wait -PassThru

if ($job.ExitCode -ne 0) {
    throw('MsBuild exited with an error. ExitCode:' + $job.ExitCode)
}

#Obtain hello project name
$projectName = (Get-Item $ProjectFile).BaseName

#Construct hello path tooweb deploy zip package
$DeployPackageDir =  '.\MSBuildOutputPath\_PublishedWebsites\{0}_Package\{0}.zip' -f $projectName

#Get hello full path for hello web deploy zip package. This is required for MSDeploy toowork
$WebDeployPackage = Resolve-Path –LiteralPath $DeployPackageDir

Write-VerboseWithTime 'Build-WebDeployPackage: End'

return $WebDeployPackage
}
```

1. <span data-ttu-id="8534c-199">Hallo aanroepen `New-WebDeployPackage` functie voordat deze regel: `$Config = Read-ConfigFile $Configuration` voor web-apps of `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8534c-199">Call hello `New-WebDeployPackage` function before this line: `$Config = Read-ConfigFile $Configuration` for web apps or `$Config = Read-ConfigFile $Configuration -HasWebDeployPackage:([Bool]$WebDeployPackage)` for virtual machines.</span></span>

    ```powershell
    if($ProjectFile)
    {
    $WebDeployPackage = New-WebDeployPackage
    }
    ```

2. <span data-ttu-id="8534c-200">Hallo aangepast script vanaf de opdrachtregel met doorgeven Hallo aanroepen `$Project` argument, zoals in Hallo opdrachtregel voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="8534c-200">Invoke hello customized script from command line using passing hello `$Project` argument, as in hello following example command line.</span></span>

    ```powershell
    .\Publish-WebApplicationVM.ps1 -Configuration .\Configurations\WebApplication5-VM-dev.json `
    -ProjectFile ..\WebApplication5\WebApplication5.csproj `
    -VMPassword @{Name="VMUser";Password="Test.123"} `
    -AllowUntrusted `
    -Verbose
    ```

    <span data-ttu-id="8534c-201">code te tooautomate testen van uw toepassing toevoegen`Test-WebApplication`.</span><span class="sxs-lookup"><span data-stu-id="8534c-201">tooautomate testing of your application, add code too`Test-WebApplication`.</span></span> <span data-ttu-id="8534c-202">Worden ervoor toouncomment Hallo regels in **publiceren WebApplication.ps1** waar deze functies worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="8534c-202">Be sure toouncomment hello lines in **Publish-WebApplication.ps1** where these functions are called.</span></span> <span data-ttu-id="8534c-203">Als u een implementatie niet opgeeft, kunt u uw project met Visual Studio handmatig maken en vervolgens uitvoeren Hallo script toopublish tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="8534c-203">If you don't provide an implementation, you can manually build your project with Visual Studio, and then run hello publish script toopublish tooAzure.</span></span>

## <a name="publishing-function-summary"></a><span data-ttu-id="8534c-204">Publishing functie samenvatting</span><span class="sxs-lookup"><span data-stu-id="8534c-204">Publishing function summary</span></span>
<span data-ttu-id="8534c-205">tooget help voor functies die u bij Hallo Windows PowerShell-opdrachtprompt gebruiken kunt, gebruik Hallo opdracht `Get-Help function-name`.</span><span class="sxs-lookup"><span data-stu-id="8534c-205">tooget help for functions you can use at hello Windows PowerShell command prompt, use hello command `Get-Help function-name`.</span></span> <span data-ttu-id="8534c-206">Hallo help bevat parameter help en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8534c-206">hello help includes parameter help and examples.</span></span> <span data-ttu-id="8534c-207">Hallo dezelfde help-tekst ook in Hallo-scriptbestanden bron is **AzureWebAppPublishModule.psm1** en **publiceren WebApplication.ps1**.</span><span class="sxs-lookup"><span data-stu-id="8534c-207">hello same help text is also in hello script source files, **AzureWebAppPublishModule.psm1** and **Publish-WebApplication.ps1**.</span></span> <span data-ttu-id="8534c-208">Hallo-script en de help worden in uw taal Visual Studio gelokaliseerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-208">hello script and help are localized in your Visual Studio language.</span></span>

<span data-ttu-id="8534c-209">**AzureWebAppPublishModule**</span><span class="sxs-lookup"><span data-stu-id="8534c-209">**AzureWebAppPublishModule**</span></span>

| <span data-ttu-id="8534c-210">Functienaam</span><span class="sxs-lookup"><span data-stu-id="8534c-210">Function name</span></span> | <span data-ttu-id="8534c-211">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8534c-211">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8534c-212">Voeg AzureSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="8534c-212">Add-AzureSQLDatabase</span></span> |<span data-ttu-id="8534c-213">Maakt een nieuwe Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="8534c-213">Creates a new Azure SQL database.</span></span> |
| <span data-ttu-id="8534c-214">Voeg AzureSQLDatabases</span><span class="sxs-lookup"><span data-stu-id="8534c-214">Add-AzureSQLDatabases</span></span> |<span data-ttu-id="8534c-215">Maakt Azure SQL-databases van Hallo-waarden in Hallo JSON-configuratiebestand dat Visual Studio gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-215">Creates Azure SQL databases from hello values in hello JSON configuration file that Visual Studio generates.</span></span> |
| <span data-ttu-id="8534c-216">-AzureVM</span><span class="sxs-lookup"><span data-stu-id="8534c-216">Add-AzureVM</span></span> |<span data-ttu-id="8534c-217">Hiermee maakt u een virtuele machine van Azure en retourneert dat Hallo-URL van Hallo VM geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-217">Creates a Azure virtual machine and returns hello URL of hello deployed VM.</span></span> <span data-ttu-id="8534c-218">Hallo functie stelt vereisten Hallo en vervolgens aanroepen Hallo **New-AzureVM** toocreate (Azure module) een nieuwe virtuele machine werkt.</span><span class="sxs-lookup"><span data-stu-id="8534c-218">hello function sets up hello prerequisites and then calls hello **New-AzureVM** function (Azure module) toocreate a new virtual machine.</span></span> |
| <span data-ttu-id="8534c-219">Voeg AzureVMEndpoints</span><span class="sxs-lookup"><span data-stu-id="8534c-219">Add-AzureVMEndpoints</span></span> |<span data-ttu-id="8534c-220">Nieuwe virtuele machine van de invoereindpunten tooa toegevoegd en Hallo virtuele machine met het nieuwe eindpunt Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="8534c-220">Adds new input endpoints tooa virtual machine and returns hello virtual machine with hello new endpoint.</span></span> |
| <span data-ttu-id="8534c-221">Voeg AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="8534c-221">Add-AzureVMStorage</span></span> |<span data-ttu-id="8534c-222">Maakt een nieuwe Azure storage-account in het huidige abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="8534c-222">Creates a new Azure storage account in hello current subscription.</span></span> <span data-ttu-id="8534c-223">Hallo-naam van Hallo account begint met 'devtest' gevolgd door een unieke alfanumerieke tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="8534c-223">hello name of hello account begins with "devtest" followed by a unique alphanumeric string.</span></span> <span data-ttu-id="8534c-224">Hallo-functie retourneert Hallo-naam van nieuw opslagaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="8534c-224">hello function returns hello name of hello new storage account.</span></span> <span data-ttu-id="8534c-225">U moet een locatie of een affiniteitsgroep voor Hallo nieuwe opslagaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="8534c-225">You must specify either a location or an affinity group for hello new storage account.</span></span> |
| <span data-ttu-id="8534c-226">Voeg AzureWebsite</span><span class="sxs-lookup"><span data-stu-id="8534c-226">Add-AzureWebsite</span></span> |<span data-ttu-id="8534c-227">Hiermee maakt een website met Hallo opgegeven naam en locatie.</span><span class="sxs-lookup"><span data-stu-id="8534c-227">Creates a website with hello specified name and location.</span></span> <span data-ttu-id="8534c-228">Deze functie aanroepen Hallo **nieuw AzureWebsite** functie in hello Azure-module.</span><span class="sxs-lookup"><span data-stu-id="8534c-228">This function calls hello **New-AzureWebsite** function in hello Azure module.</span></span> <span data-ttu-id="8534c-229">Als het Hallo-abonnement niet al een website met de opgegeven naam Hallo bevat, wordt deze functie Hallo website maakt en retourneert een object van de website.</span><span class="sxs-lookup"><span data-stu-id="8534c-229">If hello subscription doesn't already include a website with hello specified name, this function creates hello website and returns a website object.</span></span> <span data-ttu-id="8534c-230">Anders is het resultaat `$null`.</span><span class="sxs-lookup"><span data-stu-id="8534c-230">Otherwise, it returns `$null`.</span></span> |
| <span data-ttu-id="8534c-231">Back-up-abonnement</span><span class="sxs-lookup"><span data-stu-id="8534c-231">Backup-Subscription</span></span> |<span data-ttu-id="8534c-232">Slaat de huidige Azure-abonnement in Hallo Hallo `$Script:originalSubscription` variabele in script-bereik. Hiermee slaat u deze functie Hallo huidige Azure-abonnement (verkregen met `Get-AzureSubscription -Current`) en de storage-account en Hallo-abonnement dat door dit script wordt gewijzigd (opgeslagen in variabele Hallo `$UserSpecifiedSubscription`) en de opslagaccount in script-bereik.</span><span class="sxs-lookup"><span data-stu-id="8534c-232">Saves hello current Azure subscription in hello `$Script:originalSubscription` variable in script scope.This function saves hello current Azure subscription (as obtained by `Get-AzureSubscription -Current`) and its storage account, and hello subscription that is changed by this script (stored in hello variable `$UserSpecifiedSubscription`) and its storage account, in script scope.</span></span> <span data-ttu-id="8534c-233">Hallo waarden opslaat, kunt u een functie, zoals `Restore-Subscription`, toorestore Hallo oorspronkelijke huidige abonnement en opslag toocurrent accountstatus als Hallo huidige status is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="8534c-233">By saving hello values, you can use a function, such as `Restore-Subscription`, toorestore hello original current subscription and storage account toocurrent status if hello current status has changed.</span></span> |
| <span data-ttu-id="8534c-234">Zoek-AzureVM</span><span class="sxs-lookup"><span data-stu-id="8534c-234">Find-AzureVM</span></span> |<span data-ttu-id="8534c-235">Hallo opgehaald opgegeven virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="8534c-235">Gets hello specified Azure virtual machine.</span></span> |
| <span data-ttu-id="8534c-236">Indeling DevTestMessageWithTime</span><span class="sxs-lookup"><span data-stu-id="8534c-236">Format-DevTestMessageWithTime</span></span> |<span data-ttu-id="8534c-237">Voegt Hallo datum en tijd tooa bericht toe.</span><span class="sxs-lookup"><span data-stu-id="8534c-237">Prepends hello date and time tooa message.</span></span> <span data-ttu-id="8534c-238">Deze functie is ontworpen voor berichten die de fout en uitgebreid streams toohello worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="8534c-238">This function is designed for messages written toohello Error and Verbose streams.</span></span> |
| <span data-ttu-id="8534c-239">Get-AzureSQLDatabaseConnectionString</span><span class="sxs-lookup"><span data-stu-id="8534c-239">Get-AzureSQLDatabaseConnectionString</span></span> |<span data-ttu-id="8534c-240">Een verbinding tekenreeks tooconnect tooan Azure SQL database ophaalprotocol.</span><span class="sxs-lookup"><span data-stu-id="8534c-240">Assembles a connection string tooconnect tooan Azure SQL database.</span></span> |
| <span data-ttu-id="8534c-241">Get-AzureVMStorage</span><span class="sxs-lookup"><span data-stu-id="8534c-241">Get-AzureVMStorage</span></span> |<span data-ttu-id="8534c-242">Retourneert de naam van eerste opslagaccount met naampatroon Hallo HALLO hallo ' devtest*' (hoofdlettergevoelig) in de opgegeven locatie of affiniteit groep Hallo. Als Hallo ' devtest*' storage-account komt niet overeen met Hallo locatie of affiniteitsgroep, Hallo functie negeert deze.</span><span class="sxs-lookup"><span data-stu-id="8534c-242">Returns hello name of hello first storage account with hello name pattern "devtest*" (case insensitive) in hello specified location or affinity group. If hello "devtest*" storage account doesn't match hello location or affinity group, hello function ignores it.</span></span> <span data-ttu-id="8534c-243">U moet een locatie of een affiniteitsgroep opgeven.</span><span class="sxs-lookup"><span data-stu-id="8534c-243">You must specify either a location or an affinity group.</span></span> |
| <span data-ttu-id="8534c-244">Get-MSDeployCmd</span><span class="sxs-lookup"><span data-stu-id="8534c-244">Get-MSDeployCmd</span></span> |<span data-ttu-id="8534c-245">Retourneert een opdracht toorun hello MsDeploy.exe hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="8534c-245">Returns a command toorun hello MsDeploy.exe tool.</span></span> |
| <span data-ttu-id="8534c-246">Nieuwe AzureVMEnvironment</span><span class="sxs-lookup"><span data-stu-id="8534c-246">New-AzureVMEnvironment</span></span> |<span data-ttu-id="8534c-247">Zoeken naar of maakt een virtuele machine in Hallo-abonnement dat overeenkomt met de waarden in de JSON-configuratiebestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8534c-247">Finds or creates a virtual machine in hello subscription that matches hello values in hello JSON configuration file.</span></span> |
| <span data-ttu-id="8534c-248">Publiceren WebPackage</span><span class="sxs-lookup"><span data-stu-id="8534c-248">Publish-WebPackage</span></span> |<span data-ttu-id="8534c-249">Maakt gebruik van MsDeploy.exe en een web-pakket niet publiceren. Het ZIP-bestand toodeploy resources tooa website.</span><span class="sxs-lookup"><span data-stu-id="8534c-249">Uses MsDeploy.exe and a web publish package .Zip file toodeploy resources tooa website.</span></span> <span data-ttu-id="8534c-250">Deze functie biedt geen uitvoer gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-250">This function doesn't generate any output.</span></span> <span data-ttu-id="8534c-251">Als Hallo aanroep tooMSDeploy.exe mislukt, er Hallo functie een uitzondering gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-251">If hello call tooMSDeploy.exe fails, hello function throws an exception.</span></span> <span data-ttu-id="8534c-252">meer gedetailleerde uitvoer, gebruik Hallo tooget **-uitgebreide** optie.</span><span class="sxs-lookup"><span data-stu-id="8534c-252">tooget more detailed output, use hello **-Verbose** option.</span></span> |
| <span data-ttu-id="8534c-253">Publiceren WebPackageToVM</span><span class="sxs-lookup"><span data-stu-id="8534c-253">Publish-WebPackageToVM</span></span> |<span data-ttu-id="8534c-254">Controleert of de parameterwaarden Hallo en roept vervolgens Hallo **publiceren WebPackage** functie.</span><span class="sxs-lookup"><span data-stu-id="8534c-254">Verifies hello parameter values, and then calls hello **Publish-WebPackage** function.</span></span> |
| <span data-ttu-id="8534c-255">Lees ConfigFile</span><span class="sxs-lookup"><span data-stu-id="8534c-255">Read-ConfigFile</span></span> |<span data-ttu-id="8534c-256">Hallo JSON-configuratiebestand valideert en retourneert een hashtabel met geselecteerde waarden.</span><span class="sxs-lookup"><span data-stu-id="8534c-256">Validates hello JSON configuration file and returns a hash table of selected values.</span></span> |
| <span data-ttu-id="8534c-257">Restore-abonnement</span><span class="sxs-lookup"><span data-stu-id="8534c-257">Restore-Subscription</span></span> |<span data-ttu-id="8534c-258">Hiermee stelt u Hallo huidige abonnement toohello oorspronkelijke abonnement.</span><span class="sxs-lookup"><span data-stu-id="8534c-258">Resets hello current subscription toohello original subscription.</span></span> |
| <span data-ttu-id="8534c-259">Test AzureModule</span><span class="sxs-lookup"><span data-stu-id="8534c-259">Test-AzureModule</span></span> |<span data-ttu-id="8534c-260">Retourneert `$true` als geïnstalleerd hello Azure moduleversie 0.7.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8534c-260">Returns `$true` if hello installed Azure module version is 0.7.4 or later.</span></span> <span data-ttu-id="8534c-261">Retourneert `$false` als Hallo-module is niet geïnstalleerd of een eerdere versie.</span><span class="sxs-lookup"><span data-stu-id="8534c-261">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="8534c-262">Deze functie heeft geen parameters.</span><span class="sxs-lookup"><span data-stu-id="8534c-262">This function has no parameters.</span></span> |
| <span data-ttu-id="8534c-263">Test AzureModuleVersion</span><span class="sxs-lookup"><span data-stu-id="8534c-263">Test-AzureModuleVersion</span></span> |<span data-ttu-id="8534c-264">Retourneert `$true` als Hallo-versie van hello Azure-module 0.7.4 is of hoger.</span><span class="sxs-lookup"><span data-stu-id="8534c-264">Returns `$true` if hello version of hello Azure module is 0.7.4 or later.</span></span> <span data-ttu-id="8534c-265">Retourneert `$false` als Hallo-module is niet geïnstalleerd of een eerdere versie.</span><span class="sxs-lookup"><span data-stu-id="8534c-265">Returns `$false` if hello module isn't installed or is an earlier version.</span></span> <span data-ttu-id="8534c-266">Deze functie heeft geen parameters.</span><span class="sxs-lookup"><span data-stu-id="8534c-266">This function has no parameters.</span></span> |
| <span data-ttu-id="8534c-267">Test HttpsUrl</span><span class="sxs-lookup"><span data-stu-id="8534c-267">Test-HttpsUrl</span></span> |<span data-ttu-id="8534c-268">Converteert Hallo invoer-URL tooa System.Uri-object.</span><span class="sxs-lookup"><span data-stu-id="8534c-268">Converts hello input URL tooa System.Uri object.</span></span> <span data-ttu-id="8534c-269">Retourneert `$True` als Hallo-URL absoluut is en het bijbehorende schema https is.</span><span class="sxs-lookup"><span data-stu-id="8534c-269">Returns `$True` if hello URL is absolute and its scheme is https.</span></span> <span data-ttu-id="8534c-270">Retourneert `$false` als Hallo URL relatief is, het schema is niet HTTPS of Hallo invoerreeks geconverteerde tooa URL mag niet.</span><span class="sxs-lookup"><span data-stu-id="8534c-270">Returns `$false` if hello URL is relative, its scheme isn't HTTPS, or hello input string can't be converted tooa URL.</span></span> |
| <span data-ttu-id="8534c-271">Test-lid</span><span class="sxs-lookup"><span data-stu-id="8534c-271">Test-Member</span></span> |<span data-ttu-id="8534c-272">Retourneert `$true` als een eigenschap of methode lid is van Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="8534c-272">Returns `$true` if a property or method is a member of hello object.</span></span> <span data-ttu-id="8534c-273">Anders retourneert `$false`.</span><span class="sxs-lookup"><span data-stu-id="8534c-273">Otherwise, returns `$false`.</span></span> |
| <span data-ttu-id="8534c-274">Schrijven ErrorWithTime</span><span class="sxs-lookup"><span data-stu-id="8534c-274">Write-ErrorWithTime</span></span> |<span data-ttu-id="8534c-275">Schrijft een foutbericht dat wordt voorafgegaan door Hallo huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="8534c-275">Writes an error message prefixed with hello current time.</span></span> <span data-ttu-id="8534c-276">Deze functie aanroepen Hallo **indeling DevTestMessageWithTime** functie tooprepend Hallo altijd vóór het Hallo-bericht toohello foutstroom schrijven.</span><span class="sxs-lookup"><span data-stu-id="8534c-276">This function calls hello **Format-DevTestMessageWithTime** function tooprepend hello time before writing hello message toohello Error stream.</span></span> |
| <span data-ttu-id="8534c-277">Schrijven HostWithTime</span><span class="sxs-lookup"><span data-stu-id="8534c-277">Write-HostWithTime</span></span> |<span data-ttu-id="8534c-278">Een bericht toohello hostprogramma schrijft (**Write-Host**) voorafgegaan door Hallo huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="8534c-278">Writes a message toohello host program (**Write-Host**) prefixed with hello current time.</span></span> <span data-ttu-id="8534c-279">Hallo effect van het schrijven van toohello hostprogramma varieert.</span><span class="sxs-lookup"><span data-stu-id="8534c-279">hello effect of writing toohello host program varies.</span></span> <span data-ttu-id="8534c-280">De meeste programma's die als host fungeren voor Windows PowerShell deze berichten toostandard uitvoer schrijven.</span><span class="sxs-lookup"><span data-stu-id="8534c-280">Most programs that host Windows PowerShell write these messages toostandard output.</span></span> |
| <span data-ttu-id="8534c-281">Schrijven VerboseWithTime</span><span class="sxs-lookup"><span data-stu-id="8534c-281">Write-VerboseWithTime</span></span> |<span data-ttu-id="8534c-282">Schrijft een uitgebreid bericht voorafgegaan door Hallo huidige tijd.</span><span class="sxs-lookup"><span data-stu-id="8534c-282">Writes a verbose message prefixed with hello current time.</span></span> <span data-ttu-id="8534c-283">Omdat deze wordt aangeroepen **Write-Verbose**, het Hallo-bericht geeft alleen wanneer Hallo script wordt uitgevoerd met Hallo **uitgebreid** parameter of wanneer Hallo **VerbosePreference** voorkeur is Stel te**doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="8534c-283">Because it calls **Write-Verbose**, hello message displays only when hello script runs with hello **Verbose** parameter or when hello **VerbosePreference** preference is set too**Continue**.</span></span> |

<span data-ttu-id="8534c-284">**Publiceren WebApplication**</span><span class="sxs-lookup"><span data-stu-id="8534c-284">**Publish-WebApplication**</span></span>

| <span data-ttu-id="8534c-285">Functienaam</span><span class="sxs-lookup"><span data-stu-id="8534c-285">Function name</span></span> | <span data-ttu-id="8534c-286">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8534c-286">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8534c-287">Nieuwe AzureWebApplicationEnvironment</span><span class="sxs-lookup"><span data-stu-id="8534c-287">New-AzureWebApplicationEnvironment</span></span> |<span data-ttu-id="8534c-288">Azure-resources, zoals een website of virtuele machine maakt.</span><span class="sxs-lookup"><span data-stu-id="8534c-288">Creates Azure resources, such as a website or virtual machine.</span></span> |
| <span data-ttu-id="8534c-289">Nieuwe WebDeployPackage</span><span class="sxs-lookup"><span data-stu-id="8534c-289">New-WebDeployPackage</span></span> |<span data-ttu-id="8534c-290">Deze functie is niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-290">This function isn't implemented.</span></span> <span data-ttu-id="8534c-291">U kunt opdrachten toevoegen in deze functie toobuild uw project.</span><span class="sxs-lookup"><span data-stu-id="8534c-291">You can add commands in this function toobuild your project.</span></span> |
| <span data-ttu-id="8534c-292">Publiceren AzureWebApplication</span><span class="sxs-lookup"><span data-stu-id="8534c-292">Publish-AzureWebApplication</span></span> |<span data-ttu-id="8534c-293">Een web application tooAzure publiceert.</span><span class="sxs-lookup"><span data-stu-id="8534c-293">Publishes a web application tooAzure.</span></span> |
| <span data-ttu-id="8534c-294">Publiceren WebApplication</span><span class="sxs-lookup"><span data-stu-id="8534c-294">Publish-WebApplication</span></span> |<span data-ttu-id="8534c-295">Maakt en Web-Apps, virtuele machines, SQL-databases en storage-accounts voor een Visual Studio-webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="8534c-295">Creates and deploys Web Apps, virtual machines, SQL databases, and storage accounts for a Visual Studio web project.</span></span> |
| <span data-ttu-id="8534c-296">Test-WebApplication</span><span class="sxs-lookup"><span data-stu-id="8534c-296">Test-WebApplication</span></span> |<span data-ttu-id="8534c-297">Deze functie is niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8534c-297">This function isn't implemented.</span></span> <span data-ttu-id="8534c-298">U kunt opdrachten toevoegen in deze functie tootest uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="8534c-298">You can add commands in this function tootest your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8534c-299">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8534c-299">Next steps</span></span>
<span data-ttu-id="8534c-300">Meer informatie over PowerShell-scripts door te lezen [met Windows PowerShell-scripts](https://technet.microsoft.com/library/bb978526.aspx) en Zie andere Azure PowerShell-scripts op Hallo [Script Center](https://azure.microsoft.com/documentation/scripts/).</span><span class="sxs-lookup"><span data-stu-id="8534c-300">Learn more about PowerShell scripting by reading [Scripting with Windows PowerShell](https://technet.microsoft.com/library/bb978526.aspx) and see other Azure PowerShell scripts at hello [Script Center](https://azure.microsoft.com/documentation/scripts/).</span></span>
