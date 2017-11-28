---
title: implementatie van de virtuele machine aaaAzure met Chef | Microsoft Docs
description: Meer informatie over hoe toouse Chef toodo geautomatiseerde implementatie van virtuele machines en configuratie op Microsoft Azure
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
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="9ef4e-103">Implementatie van virtuele Azure-machine automatiseren met Chef</span><span class="sxs-lookup"><span data-stu-id="9ef4e-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="9ef4e-104">Chef is een uitstekend hulpprogramma voor het leveren van automation en gewenste status configuraties.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="9ef4e-105">Met de meest recente versie van de cloud-api Chef biedt naadloze integratie met Azure, zodat u Hallo mogelijkheid tooprovision en configuratiestatussen via één opdracht implementeren.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="9ef4e-106">In dit artikel ik, ziet u hoe tooset van uw Chef omgeving tooprovision Azure virtuele machines en helpt u bij het maken van een beleid of 'CookBook' en het implementeren van deze cookbook tooan virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="9ef4e-107">We begint!</span><span class="sxs-lookup"><span data-stu-id="9ef4e-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="9ef4e-108">Chef basisbeginselen</span><span class="sxs-lookup"><span data-stu-id="9ef4e-108">Chef basics</span></span>
<span data-ttu-id="9ef4e-109">Voordat u begint, voorgesteld ik dat u Hallo basisconcepten van Chef bekijken.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="9ef4e-110">Er is geweldige materiaal <a href="http://www.chef.io/chef" target="_blank">hier</a> en ik het beste hebt u een snelle Lees voordat u deze stapsgewijze kennismaking.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="9ef4e-111">Ik zal echter Hallo basisbeginselen samenvatting voordat we aan de slag.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="9ef4e-112">Hallo volgende diagram ziet u Hallo op hoog niveau Chef-architectuur.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="9ef4e-113">Chef heeft drie architectuur hoofdonderdelen: Chef-Server, Chef-Client (knooppunt) en Chef-werkstation.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="9ef4e-114">Hallo Chef Server onze beheerpunt is en er zijn twee opties voor Hallo Chef-Server: een gehoste oplossing of een on-premises-oplossing.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="9ef4e-115">We gebruiken een gehoste oplossing.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="9ef4e-116">Hallo Chef-Client is (knooppunt) Hallo-agent die zich bevindt op Hallo-servers die u beheert.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="9ef4e-117">Hallo Chef-werkstation is onze beheerwerkstation waar we onze beleid maken en onze management-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="9ef4e-118">We Hallo uitvoeren **mes** opdracht van Hallo Chef werkstation toomanage onze infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="9ef4e-119">Er is ook Hallo concept van 'Cookbooks' en 'Recepten'.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="9ef4e-120">Dit zijn effectief Hallo beleidsregels die we definiëren en tooour servers toepassen.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="9ef4e-121">Hallo-werkstation voorbereiden</span><span class="sxs-lookup"><span data-stu-id="9ef4e-121">Preparing hello workstation</span></span>
<span data-ttu-id="9ef4e-122">Ten eerste kunt prep Hallo werkstation.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="9ef4e-123">Ik gebruik een standaard Windows-werkstation.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="9ef4e-124">Een directory toostore toocreate moeten we onze configuratiebestanden en cookbooks.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="9ef4e-125">Eerst een map met de naam C:\chef maken.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="9ef4e-126">Vervolgens maakt u een tweede directory c:\chef\cookbooks aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="9ef4e-127">Nu moet toodownload ons Azure instellingenbestand zodat Chef met ons Azure-abonnement communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="9ef4e-128">Download uw publicatie-instellingen met behulp van PowerShell Azure Hallo [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) opdracht.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="9ef4e-129">Sla Hallo bestand publicatie-instellingen in C:\chef.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="9ef4e-130">Een beheerde Chef-account maken</span><span class="sxs-lookup"><span data-stu-id="9ef4e-130">Creating a managed Chef account</span></span>
<span data-ttu-id="9ef4e-131">Aanmelden voor een gehoste Chef account [hier](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="9ef4e-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="9ef4e-132">Tijdens het aanmeldingsproces hello, kunt u zich toocreate gevraagd een nieuwe organisatie.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="9ef4e-133">Nadat uw organisatie is gemaakt, downloadt u Hallo starterskit.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="9ef4e-134">Als u gevraagd waarschuwing wordt dat uw sleutels worden opnieuw ingesteld, is ok tooproceed omdat er geen bestaande infrastructuur nog geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="9ef4e-135">Deze starter kit zip-bestand bevat de configuratiebestanden van de organisatie en de sleutels.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="9ef4e-136">Hallo Chef werkstation configureren</span><span class="sxs-lookup"><span data-stu-id="9ef4e-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="9ef4e-137">Hallo-inhoud van het Hallo chef starter.zip tooC:\chef extraheren.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="9ef4e-138">Kopieer alle bestanden onder chef-starter\chef-opslagplaats\.chef tooyour c:\chef directory.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="9ef4e-139">Uw directory ziet er ongeveer als volgt Hallo nu.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="9ef4e-140">U hebt nu vier bestanden met inbegrip van hello Azure publishing bestand in de hoofdmap Hallo van c:\chef.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="9ef4e-141">Hallo PEM-bestanden bevatten van uw organisatie en persoonlijke sleutels van de beheerder voor communicatie terwijl Hallo knife.rb bestand de configuratie van uw mes bevat.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="9ef4e-142">Moeten we tooedit hello knife.rb bestand.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="9ef4e-143">Hallo-bestand openen in uw editor naar keuze en Hallo 'cookbook_path' wijzigen door het verwijderen van Hallo /... / van Hallo pad zodat deze wordt weergegeven zoals volgende.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="9ef4e-144">Ook toevoegen Hallo volgende regel reflecterende Hallo-naam van uw Azure bestand publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="9ef4e-145">Uw knife.rb-bestand ziet er nu vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="9ef4e-146">Deze regels zorgt ervoor dat mes verwijst naar Hallo cookbooks map onder c:\chef\cookbooks en ook onze Azure Publish Settings-bestand tijdens de Azure-bewerkingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="9ef4e-147">Hallo Chef Development Kit installeren</span><span class="sxs-lookup"><span data-stu-id="9ef4e-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="9ef4e-148">Volgende [downloaden en installeren](http://downloads.getchef.com/chef-dk/windows) Hallo tooset uw werkstation Chef ChefDK (Chef Development Kit).</span><span class="sxs-lookup"><span data-stu-id="9ef4e-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="9ef4e-149">In de standaardlocatie Hallo van c:\opscode installeren.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="9ef4e-150">Deze installatie duurt ongeveer 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="9ef4e-151">Bevestig dat uw padvariabele bevat vermeldingen voor C:\opscode\chefdk\bin; C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="9ef4e-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="9ef4e-152">Als ze niet er zijn, zorg er dan voor dat u deze paden toevoegt.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="9ef4e-153">*Houd er rekening mee Hallo volgorde van de Hallo pad IS belangrijk!*</span><span class="sxs-lookup"><span data-stu-id="9ef4e-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="9ef4e-154">Als uw opscode-paden niet in de juiste volgorde Hallo zijn hebt u problemen.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="9ef4e-155">Start opnieuw op uw werkstation voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="9ef4e-156">Vervolgens installeert we Hallo mes Azure-extensie.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="9ef4e-157">Dit biedt mes Hallo 'Azure invoegtoepassing'.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="9ef4e-158">Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="9ef4e-159">Hallo – pre-argument zorgt ervoor dat u ontvangt Hallo nieuwste RC-versie van Hallo mes Azure invoegtoepassing waarmee toegang toohello meest recente set API's.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="9ef4e-160">Is het waarschijnlijk dat een aantal afhankelijkheden ook worden geïnstalleerd op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="9ef4e-161">tooensure die alles is geconfigureerd, Voer Hallo na de opdracht.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="9ef4e-162">Als alles correct is geconfigureerd, ziet u een lijst met beschikbare Azure installatiekopieën door te bladeren.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="9ef4e-163">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-163">Congratulations.</span></span> <span data-ttu-id="9ef4e-164">Hallo-werkstation is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="9ef4e-165">Maken van een Cookbook</span><span class="sxs-lookup"><span data-stu-id="9ef4e-165">Creating a Cookbook</span></span>
<span data-ttu-id="9ef4e-166">Een Cookbook wordt gebruikt door Chef toodefine een reeks opdrachten die u wilt dat tooexecute op uw beheerde client.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="9ef4e-167">Het maken van een Cookbook is eenvoudig en gebruiken we Hallo **chef genereren cookbook** opdracht toogenerate onze Cookbook-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="9ef4e-168">Ik zal worden aanroepen van mijn webserver Cookbook als ik een beleid dat automatisch wordt geïmplementeerd IIS zou willen.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="9ef4e-169">In de map C:\Chef Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="9ef4e-170">Hierdoor wordt een reeks van bestanden onder Hallo directory C:\Chef\cookbooks\webserver gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="9ef4e-171">Nu moet toodefine Hallo reeks opdrachten dat willen we graag onze client Chef tooexecute op onze beheerde virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="9ef4e-172">Hallo-opdrachten worden opgeslagen in Hallo bestand default.rb.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="9ef4e-173">In dit bestand moet ik een verzameling opdrachten die IIS is geïnstalleerd, start IIS en een sjabloon toohello wwwroot-map kopieert definiëren.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="9ef4e-174">Hallo C:\chef\cookbooks\webserver\recipes\default.rb bestand wijzigen en Hallo volgende regels toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

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

<span data-ttu-id="9ef4e-175">Hallo-bestand opslaan als u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="9ef4e-176">Maken van een sjabloon</span><span class="sxs-lookup"><span data-stu-id="9ef4e-176">Creating a template</span></span>
<span data-ttu-id="9ef4e-177">Zoals we eerder vermeld, moet een sjabloonbestand dat wordt gebruikt als onze pagina met default.html toogenerate.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="9ef4e-178">Hallo na de opdracht toogenerate Hallo sjabloon worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="9ef4e-179">Ga nu toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb bestand.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="9ef4e-180">Hallo-bestand bewerken door enkele eenvoudige 'Hallo wereld' HTML-code toe te voegen en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="9ef4e-181">Hallo Cookbook toohello Chef Server uploaden</span><span class="sxs-lookup"><span data-stu-id="9ef4e-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="9ef4e-182">We zijn in deze stap duurt een kopie van Hallo Cookbook die er op de lokale computer gemaakt en toohello Chef gehoste Server uploaden.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="9ef4e-183">Na het uploaden Hallo Cookbook wordt weergegeven onder Hallo **beleid** tabblad.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="9ef4e-184">Een virtuele machine met Mes Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="9ef4e-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="9ef4e-185">We nu implementeren van een virtuele machine van Azure en toepassing hello 'Webserver' Cookbook die onze IIS web service en de standaard webpagina wordt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="9ef4e-186">In volgorde van toodo dit, gebruikt u Hallo **mes azure-server maken** opdracht.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="9ef4e-187">Ben voorbeeld van de opdracht Hallo volgende verschijnt.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="9ef4e-188">Hallo parameters behoeven geen uitleg.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="9ef4e-189">Vervangen door uw specifieke variabelen en uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="9ef4e-190">Via Hallo Hallo-opdrachtregel, ben ik mijn filterregels voor eindpunt netwerk ook automatiseren met behulp van Hallo – tcp-eindpunten parameter.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="9ef4e-191">Ik hebt poorten 80 en 3389 tooprovide toegang toomy webpagina en RDP-sessie geopend.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="9ef4e-192">Zodra u Hallo-opdracht uitvoert, gaat u toohello Azure portal en u ziet uw machine tooprovision begint.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="9ef4e-193">Hallo-opdrachtprompt verschijnt volgende.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="9ef4e-194">Zodra het Hallo-implementatie is voltooid, moet we kunnen tooconnect toohello web-service via poort 80 we had Hallo poort geopend wanneer we Hallo virtuele machine met de Hallo mes Azure opdracht ingericht.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="9ef4e-195">Als deze virtuele machine Hallo virtuele machine die alleen in mijn cloudservice is, moet ik het verbinding maken met Hallo cloud service-url.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="9ef4e-196">Zoals u ziet, krijg ik creative met mijn HTML-code.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="9ef4e-197">Vergeet niet dat we kunnen ook verbinding maken via een RDP-sessie vanaf hello Azure-portal via poort 3389.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="9ef4e-198">Ik hopen dat u dat dit is handig zijn.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-198">I hope this has been helpful!</span></span> <span data-ttu-id="9ef4e-199">Ga en uw infrastructuur vandaag starten als code reis met Azure.</span><span class="sxs-lookup"><span data-stu-id="9ef4e-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

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
