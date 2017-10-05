---
title: Implementatie van de virtuele machine van Azure met Chef | Microsoft Docs
description: Meer informatie over het gebruik van Chef voor implementatie van geautomatiseerde virtuele machine en de configuratie op Microsoft Azure
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: b6db0fbb4e0de896994954974ddcc39daad9c125
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="ed82c-103">Implementatie van virtuele Azure-machine automatiseren met Chef</span><span class="sxs-lookup"><span data-stu-id="ed82c-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ed82c-104">Chef is een uitstekend hulpprogramma voor het leveren van automation en gewenste status configuraties.</span><span class="sxs-lookup"><span data-stu-id="ed82c-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="ed82c-105">Met de meest recente versie van de cloud-api biedt Chef naadloze integratie met Azure, zodat u de mogelijkheid voor het inrichten en implementeren van configuratiestatussen via één opdracht.</span><span class="sxs-lookup"><span data-stu-id="ed82c-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you the ability to provision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="ed82c-106">In dit artikel ziet ik u het instellen van uw omgeving Chef inrichten van virtuele machines in Azure en helpt u bij het maken van een beleid of "CookBook" en vervolgens deze cookbook implementeert op een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="ed82c-106">In this article, I’ll show you how to set up your Chef environment to provision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook to an Azure virtual machine.</span></span>

<span data-ttu-id="ed82c-107">We begint!</span><span class="sxs-lookup"><span data-stu-id="ed82c-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="ed82c-108">Chef basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="ed82c-108">Chef basics</span></span>
<span data-ttu-id="ed82c-109">Voordat u begint, voorgesteld ik dat u de basisconcepten van Chef bekijken.</span><span class="sxs-lookup"><span data-stu-id="ed82c-109">Before you begin, I suggest you review the basic concepts of Chef.</span></span> <span data-ttu-id="ed82c-110">Er is geweldige materiaal <a href="http://www.chef.io/chef" target="_blank">hier</a> en ik het beste hebt u een snelle Lees voordat u deze stapsgewijze kennismaking.</span><span class="sxs-lookup"><span data-stu-id="ed82c-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="ed82c-111">Ik zal echter de basisbeginselen samenvatting voordat we aan de slag.</span><span class="sxs-lookup"><span data-stu-id="ed82c-111">I will however recap the basics before we get started.</span></span>

<span data-ttu-id="ed82c-112">Het volgende diagram illustreert de op hoog niveau Chef-architectuur.</span><span class="sxs-lookup"><span data-stu-id="ed82c-112">The following diagram depicts the high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="ed82c-113">Chef heeft drie architectuur hoofdonderdelen: Chef-Server, Chef-Client (knooppunt) en Chef-werkstation.</span><span class="sxs-lookup"><span data-stu-id="ed82c-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="ed82c-114">De Chef Server onze beheerpunt en er zijn twee opties voor de Chef Server: een gehoste oplossing of een on-premises-oplossing.</span><span class="sxs-lookup"><span data-stu-id="ed82c-114">The Chef Server is our management point and there are two options for the Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="ed82c-115">We gebruiken een gehoste oplossing.</span><span class="sxs-lookup"><span data-stu-id="ed82c-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="ed82c-116">De Chef Client (knooppunt) is de agent die zich op de servers die u beheert.</span><span class="sxs-lookup"><span data-stu-id="ed82c-116">The Chef Client (node) is the agent that sits on the servers you are managing.</span></span>

<span data-ttu-id="ed82c-117">Het werkstation Chef is onze beheerwerkstation waar we onze beleid maken en onze management-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ed82c-117">The Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="ed82c-118">We voeren de **mes** opdracht van het werkstation Chef om onze infrastructuur te beheren.</span><span class="sxs-lookup"><span data-stu-id="ed82c-118">We run the **knife** command from the Chef Workstation to manage our infrastructure.</span></span>

<span data-ttu-id="ed82c-119">Er is ook het concept van 'Cookbooks' en 'Recepten'.</span><span class="sxs-lookup"><span data-stu-id="ed82c-119">There is also the concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="ed82c-120">Dit zijn effectief de beleidsregels die we definiëren en toepassen op onze servers.</span><span class="sxs-lookup"><span data-stu-id="ed82c-120">These are effectively the policies we define and apply to our servers.</span></span>

## <a name="preparing-the-workstation"></a><span data-ttu-id="ed82c-121">Het werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="ed82c-121">Preparing the workstation</span></span>
<span data-ttu-id="ed82c-122">Ten eerste kunt het werkstation voorbereiden.</span><span class="sxs-lookup"><span data-stu-id="ed82c-122">First, lets prep the workstation.</span></span> <span data-ttu-id="ed82c-123">Ik gebruik een standaard Windows-werkstation.</span><span class="sxs-lookup"><span data-stu-id="ed82c-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="ed82c-124">Er moet een map voor het opslaan van onze configuratiebestanden en cookbooks maken.</span><span class="sxs-lookup"><span data-stu-id="ed82c-124">We need to create a directory to store our config files and cookbooks.</span></span>

<span data-ttu-id="ed82c-125">Eerst een map met de naam C:\chef maken.</span><span class="sxs-lookup"><span data-stu-id="ed82c-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="ed82c-126">Vervolgens maakt u een tweede directory c:\chef\cookbooks aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ed82c-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="ed82c-127">Nu moeten we ons Azure-instellingen-bestand downloaden zodat Chef met ons Azure-abonnement communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="ed82c-127">We now need to download our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="ed82c-128">Download uw publicatie-instellingen met behulp van de PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) opdracht.</span><span class="sxs-lookup"><span data-stu-id="ed82c-128">Download your publish settings using the PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="ed82c-129">Sla het bestand van de instellingen voor publiceren in C:\chef.</span><span class="sxs-lookup"><span data-stu-id="ed82c-129">Save the publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="ed82c-130">Een beheerde Chef-account maken</span><span class="sxs-lookup"><span data-stu-id="ed82c-130">Creating a managed Chef account</span></span>
<span data-ttu-id="ed82c-131">Aanmelden voor een gehoste Chef account [hier](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="ed82c-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="ed82c-132">Tijdens het aanmeldingsproces, wordt u gevraagd een nieuwe organisatie maken.</span><span class="sxs-lookup"><span data-stu-id="ed82c-132">During the signup process, you will be asked to create a new organization.</span></span>

![][3]

<span data-ttu-id="ed82c-133">Nadat uw organisatie is gemaakt, downloadt u de starterskit.</span><span class="sxs-lookup"><span data-stu-id="ed82c-133">Once your organization is created, download the starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="ed82c-134">Als u gevraagd waarschuwing wordt dat uw sleutels worden opnieuw ingesteld, is het ok om door te gaan als er geen bestaande infrastructuur nog geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ed82c-134">If you receive a prompt warning you that your keys will be reset, it’s ok to proceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="ed82c-135">Deze starter kit zip-bestand bevat de configuratiebestanden van de organisatie en de sleutels.</span><span class="sxs-lookup"><span data-stu-id="ed82c-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-the-chef-workstation"></a><span data-ttu-id="ed82c-136">Het werkstation Chef configureren</span><span class="sxs-lookup"><span data-stu-id="ed82c-136">Configuring the Chef workstation</span></span>
<span data-ttu-id="ed82c-137">Pak de inhoud van de chef-starter.zip naar C:\chef.</span><span class="sxs-lookup"><span data-stu-id="ed82c-137">Extract the content of the chef-starter.zip to C:\chef.</span></span>

<span data-ttu-id="ed82c-138">Kopieer alle bestanden onder chef-starter\chef-opslagplaats\.chef aan uw directory c:\chef.</span><span class="sxs-lookup"><span data-stu-id="ed82c-138">Copy all files under chef-starter\chef-repo\.chef to your c:\chef directory.</span></span>

<span data-ttu-id="ed82c-139">Uw directory ziet er nu ongeveer het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ed82c-139">Your directory should now look something like the following example.</span></span>

![][5]

<span data-ttu-id="ed82c-140">U hebt nu vier bestanden met inbegrip van het Azure publishing bestand in de hoofdmap van c:\chef.</span><span class="sxs-lookup"><span data-stu-id="ed82c-140">You should now have four files including the Azure publishing file in the root of c:\chef.</span></span>

<span data-ttu-id="ed82c-141">Het PEM-bestanden bevatten van uw organisatie en persoonlijke sleutels van de beheerder voor communicatie terwijl het bestand knife.rb de configuratie van uw mes bevat.</span><span class="sxs-lookup"><span data-stu-id="ed82c-141">The PEM files contain your organization and admin private keys for communication while the knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="ed82c-142">Bewerk het bestand knife.rb moet.</span><span class="sxs-lookup"><span data-stu-id="ed82c-142">We will need to edit the knife.rb file.</span></span>

<span data-ttu-id="ed82c-143">Open het bestand in uw editor naar keuze en de 'cookbook_path' wijzigen door het verwijderen van de /... / van het pad, zodat deze wordt weergegeven zoals volgende.</span><span class="sxs-lookup"><span data-stu-id="ed82c-143">Open the file in your editor of choice and modify the “cookbook_path” by removing the /../ from the path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="ed82c-144">Voeg ook de volgende regel als gevolg van de naam van uw Azure bestand publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ed82c-144">Also add the following line reflecting the name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="ed82c-145">Uw bestand knife.rb nu zijn vergelijkbaar met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ed82c-145">Your knife.rb file should now look similar to the following example.</span></span>

![][6]

<span data-ttu-id="ed82c-146">Deze regels zorgt ervoor dat mes verwijst naar de map cookbooks onder c:\chef\cookbooks en ook onze Azure Publish Settings-bestand tijdens de Azure-bewerkingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed82c-146">These lines will ensure that Knife references the cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-the-chef-development-kit"></a><span data-ttu-id="ed82c-147">De Chef Development Kit installeren</span><span class="sxs-lookup"><span data-stu-id="ed82c-147">Installing the Chef Development Kit</span></span>
<span data-ttu-id="ed82c-148">Volgende [downloaden en installeren](http://downloads.getchef.com/chef-dk/windows) de ChefDK (Chef Development Kit) voor het instellen van uw Chef-werkstation.</span><span class="sxs-lookup"><span data-stu-id="ed82c-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) the ChefDK (Chef Development Kit) to set up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="ed82c-149">In de standaardlocatie van c:\opscode installeren.</span><span class="sxs-lookup"><span data-stu-id="ed82c-149">Install in the default location of c:\opscode.</span></span> <span data-ttu-id="ed82c-150">Deze installatie duurt ongeveer 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="ed82c-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="ed82c-151">Bevestig dat uw padvariabele bevat vermeldingen voor C:\opscode\chefdk\bin; C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="ed82c-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="ed82c-152">Als ze niet er zijn, zorg er dan voor dat u deze paden toevoegt.</span><span class="sxs-lookup"><span data-stu-id="ed82c-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="ed82c-153">*HOUD ER REKENING MEE DAT DE VOLGORDE VAN HET PAD IS BELANGRIJK!*</span><span class="sxs-lookup"><span data-stu-id="ed82c-153">*NOTE THE ORDER OF THE PATH IS IMPORTANT!*</span></span> <span data-ttu-id="ed82c-154">Als uw opscode-paden niet in de juiste volgorde zijn hebt u problemen.</span><span class="sxs-lookup"><span data-stu-id="ed82c-154">If your opscode paths are not in the correct order you will have issues.</span></span>

<span data-ttu-id="ed82c-155">Start opnieuw op uw werkstation voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="ed82c-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="ed82c-156">Vervolgens wordt de extensie mes Azure installeert.</span><span class="sxs-lookup"><span data-stu-id="ed82c-156">Next, we will install the Knife Azure extension.</span></span> <span data-ttu-id="ed82c-157">Dit biedt mes met de invoegtoepassing' Azure'.</span><span class="sxs-lookup"><span data-stu-id="ed82c-157">This provides Knife with the “Azure Plugin”.</span></span>

<span data-ttu-id="ed82c-158">Voer de volgende opdracht.</span><span class="sxs-lookup"><span data-stu-id="ed82c-158">Run the following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="ed82c-159">Het argument – pre zorgt ervoor dat u de meest recente RC-versie van de Azure-invoegtoepassing voor mes dat toegang tot de meest recente set API's biedt ontvangt.</span><span class="sxs-lookup"><span data-stu-id="ed82c-159">The –pre argument ensures you are receiving the latest RC version of the Knife Azure Plugin which provides access to the latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="ed82c-160">Is het waarschijnlijk dat een aantal afhankelijkheden ook worden geïnstalleerd op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="ed82c-160">It’s likely that a number of dependencies will also be installed at the same time.</span></span>

![][8]

<span data-ttu-id="ed82c-161">Voer de volgende opdracht om te controleren of dat alles correct is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ed82c-161">To ensure everything is configured correctly, run the following command.</span></span>

    knife azure image list

<span data-ttu-id="ed82c-162">Als alles correct is geconfigureerd, ziet u een lijst met beschikbare Azure installatiekopieën door te bladeren.</span><span class="sxs-lookup"><span data-stu-id="ed82c-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="ed82c-163">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="ed82c-163">Congratulations.</span></span> <span data-ttu-id="ed82c-164">Het werkstation is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ed82c-164">The workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="ed82c-165">Maken van een Cookbook</span><span class="sxs-lookup"><span data-stu-id="ed82c-165">Creating a Cookbook</span></span>
<span data-ttu-id="ed82c-166">Een Cookbook wordt gebruikt door Chef voor het definiëren van een reeks opdrachten die u wilt uitvoeren op uw beheerde client.</span><span class="sxs-lookup"><span data-stu-id="ed82c-166">A Cookbook is used by Chef to define a set of commands that you wish to execute on your managed client.</span></span> <span data-ttu-id="ed82c-167">Het maken van een Cookbook is eenvoudig en gebruiken we de **chef genereren cookbook** opdracht voor het genereren van onze Cookbook-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ed82c-167">Creating a Cookbook is straightforward and we use the **chef generate cookbook** command to generate our Cookbook template.</span></span> <span data-ttu-id="ed82c-168">Ik zal worden aanroepen van mijn webserver Cookbook als ik een beleid dat automatisch wordt geïmplementeerd IIS zou willen.</span><span class="sxs-lookup"><span data-stu-id="ed82c-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="ed82c-169">Voer de volgende opdracht in uw map C:\Chef.</span><span class="sxs-lookup"><span data-stu-id="ed82c-169">Under your C:\Chef directory run the following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="ed82c-170">Hierdoor wordt een aantal bestanden in de map C:\Chef\cookbooks\webserver gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ed82c-170">This will generate a set of files under the directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="ed82c-171">Nu moeten we de reeks opdrachten die we onze Chef-client wilt uitvoeren op onze beheerde virtuele machine wilt definiëren.</span><span class="sxs-lookup"><span data-stu-id="ed82c-171">We now need to define the set of commands we would like our Chef client to execute on our managed virtual machine.</span></span>

<span data-ttu-id="ed82c-172">De opdrachten worden opgeslagen in het bestand default.rb.</span><span class="sxs-lookup"><span data-stu-id="ed82c-172">The commands are stored in the file default.rb.</span></span> <span data-ttu-id="ed82c-173">In dit bestand moet ik een verzameling opdrachten die IIS is geïnstalleerd, start IIS en een sjabloonbestand kopieert naar de wwwroot-map definiëren.</span><span class="sxs-lookup"><span data-stu-id="ed82c-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file to the wwwroot folder.</span></span>

<span data-ttu-id="ed82c-174">Wijzigen van het bestand C:\chef\cookbooks\webserver\recipes\default.rb en voeg de volgende regels.</span><span class="sxs-lookup"><span data-stu-id="ed82c-174">Modify the C:\chef\cookbooks\webserver\recipes\default.rb file and add the following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="ed82c-175">Sla het bestand als u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="ed82c-175">Save the file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="ed82c-176">Maken van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="ed82c-176">Creating a template</span></span>
<span data-ttu-id="ed82c-177">Zoals we eerder vermeld, moeten we een sjabloonbestand dat wordt gebruikt als onze pagina met default.html genereren.</span><span class="sxs-lookup"><span data-stu-id="ed82c-177">As we mentioned previously, we need to generate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="ed82c-178">Voer de volgende opdracht voor het genereren van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="ed82c-178">Run the following command to generate the template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="ed82c-179">Nu gaat u naar het bestand C:\chef\cookbooks\webserver\templates\default\Default.htm.erb.</span><span class="sxs-lookup"><span data-stu-id="ed82c-179">Now navigate to the C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="ed82c-180">Bewerk het bestand door enkele eenvoudige 'Hallo wereld' HTML-code toe te voegen en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="ed82c-180">Edit the file by adding some simple “Hello World” HTML code, and then save the file.</span></span>

## <a name="upload-the-cookbook-to-the-chef-server"></a><span data-ttu-id="ed82c-181">Het Cookbook uploaden naar de Chef-Server</span><span class="sxs-lookup"><span data-stu-id="ed82c-181">Upload the Cookbook to the Chef Server</span></span>
<span data-ttu-id="ed82c-182">We zijn een kopie van het Cookbook die er op de lokale computer gemaakt en uploaden naar de Server van de gehoste Chef in deze stap.</span><span class="sxs-lookup"><span data-stu-id="ed82c-182">In this step, we are taking a copy of the Cookbook that we have created on our local machine and uploading it to the Chef Hosted Server.</span></span> <span data-ttu-id="ed82c-183">Na het uploaden, het Cookbook wordt weergegeven onder de **beleid** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ed82c-183">Once uploaded, the Cookbook will appear under the **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="ed82c-184">Een virtuele machine met Mes Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="ed82c-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="ed82c-185">We nu implementeren van een virtuele machine van Azure en toepassen van de 'Webserver' Cookbook die onze IIS web service en de standaard webpagina wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ed82c-185">We will now deploy an Azure virtual machine and apply the “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="ed82c-186">Gebruik hiervoor de **mes azure-server maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="ed82c-186">In order to do this, use the **knife azure server create** command.</span></span>

<span data-ttu-id="ed82c-187">Ben voorbeeld van de opdracht volgende weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ed82c-187">Am example of the command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="ed82c-188">De parameters behoeven geen uitleg.</span><span class="sxs-lookup"><span data-stu-id="ed82c-188">The parameters are self-explanatory.</span></span> <span data-ttu-id="ed82c-189">Vervangen door uw specifieke variabelen en uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ed82c-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="ed82c-190">Via de de opdrachtregel, ik ben ook automatiseren mijn filterregels endpoint-netwerk met behulp van de parameter – tcp-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="ed82c-190">Through the the command line, I’m also automating my endpoint network filter rules by using the –tcp-endpoints parameter.</span></span> <span data-ttu-id="ed82c-191">Ik hebt up poorten 80 en 3389 voor toegang tot mijn webpagina's en RDP-sessie geopend.</span><span class="sxs-lookup"><span data-stu-id="ed82c-191">I’ve opened up ports 80 and 3389 to provide access to my web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="ed82c-192">Zodra u de opdracht uitvoert, gaat u naar de Azure-portal en ziet u de computer die begint met het inrichten.</span><span class="sxs-lookup"><span data-stu-id="ed82c-192">Once you run the command, go to the Azure portal and you will see your machine begin to provision.</span></span>

![][13]

<span data-ttu-id="ed82c-193">Er verschijnt de opdrachtprompt volgende.</span><span class="sxs-lookup"><span data-stu-id="ed82c-193">The command prompt appears next.</span></span>

![][10]

<span data-ttu-id="ed82c-194">Zodra de implementatie voltooid is, moet er verbinding maken met de web-service via poort 80 als we had de poort geopend wanneer we de virtuele machine met de opdracht mes Azure ingericht.</span><span class="sxs-lookup"><span data-stu-id="ed82c-194">Once the deployment is complete, we should be able to connect to the web service over port 80 as we had opened the port when we provisioned the virtual machine with the Knife Azure command.</span></span> <span data-ttu-id="ed82c-195">Als deze virtuele machine de virtuele machine die alleen in mijn cloudservice is, moet ik het verbinding maken met de cloud service-url.</span><span class="sxs-lookup"><span data-stu-id="ed82c-195">As this virtual machine is the only virtual machine in my cloud service, I’ll connect it with the cloud service url.</span></span>

![][11]

<span data-ttu-id="ed82c-196">Zoals u ziet, krijg ik creative met mijn HTML-code.</span><span class="sxs-lookup"><span data-stu-id="ed82c-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="ed82c-197">Vergeet niet dat we kunnen ook verbinding maken via een RDP-sessie vanaf de Azure portal via poort 3389.</span><span class="sxs-lookup"><span data-stu-id="ed82c-197">Don’t forget we can also connect through an RDP session from the Azure portal via port 3389.</span></span>

<span data-ttu-id="ed82c-198">Ik hopen dat u dat dit is handig zijn.</span><span class="sxs-lookup"><span data-stu-id="ed82c-198">I hope this has been helpful!</span></span> <span data-ttu-id="ed82c-199">Ga en uw infrastructuur vandaag starten als code reis met Azure.</span><span class="sxs-lookup"><span data-stu-id="ed82c-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
