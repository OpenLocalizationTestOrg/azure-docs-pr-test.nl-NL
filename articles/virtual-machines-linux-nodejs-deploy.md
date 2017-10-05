---
title: Een Node.js-toepassing voor virtuele Linux-Machines in Azure implementeren
description: Informatie over het implementeren van een Node.js-toepassing voor virtuele Linux-machines in Azure.
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: d3d9fecfafb9ba422420230716b9c985481d1e24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-nodejs-application-to-linux-virtual-machines-in-azure"></a><span data-ttu-id="8ea15-103">Een Node.js-toepassing voor virtuele Linux-Machines in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="8ea15-103">Deploy a Node.js application to Linux Virtual Machines in Azure</span></span>
<span data-ttu-id="8ea15-104">Deze zelfstudie ziet een Node.js-toepassing maken en implementeren op Linux virtuele machines in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-104">This tutorial shows how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="8ea15-105">De instructies in deze zelfstudie kunnen worden uitgevoerd in elk besturingssysteem waarmee Node.js kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-105">The instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="8ea15-106">U leert hoe:</span><span class="sxs-lookup"><span data-stu-id="8ea15-106">You'll learn how to:</span></span>

* <span data-ttu-id="8ea15-107">Fork- en kloon een GitHub-opslagplaats met een eenvoudige toepassing voor TODO;</span><span class="sxs-lookup"><span data-stu-id="8ea15-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="8ea15-108">Maken en configureren van twee virtuele Linux-machines in Azure om het starten van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ea15-108">Create and configure two Linux virtual machines in Azure to run the application;</span></span>
* <span data-ttu-id="8ea15-109">De toepassing door om updates te pushen naar de virtuele machine van de webserver-frontend herhalen.</span><span class="sxs-lookup"><span data-stu-id="8ea15-109">Iterate on the application by pushing updates to the web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="8ea15-110">Voor deze zelfstudie hebt voltooid, moet u een GitHub-account en een Microsoft Azure-account en de mogelijkheid om met Git van een ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="8ea15-110">To complete this tutorial, you need a GitHub account and a Microsoft Azure account, and the ability to use Git from a development machine.</span></span>
> 
> <span data-ttu-id="8ea15-111">Als u geen een GitHub-account hebt, kunt u zich aanmeldt [hier](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="8ea15-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="8ea15-112">Als u hebt een [Microsoft Azure](https://azure.microsoft.com/) -account, u kunt zich aanmelden voor een gratis proefversie [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ea15-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="8ea15-113">Dit ook loodst u door het registratieproces voor een [Microsoft-Account](http://account.microsoft.com) als u nog geen een.</span><span class="sxs-lookup"><span data-stu-id="8ea15-113">This will also lead you through the sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="8ea15-114">Als u een Visual Studio-abonnee bent, u kunt ook [activeren van uw voordelen als MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8ea15-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="8ea15-115">Als u geen git op uw ontwikkelcomputer, als u een Macintosh of Windows-machine, installeert u git van [hier](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="8ea15-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="8ea15-116">Als u Linux installeren met het meest geschikt is voor u, mechanisme, zoals git `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="8ea15-116">If you are using Linux, install git using the mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-the-todo-application"></a><span data-ttu-id="8ea15-117">Vertakken en klonen de TODO-toepassing</span><span class="sxs-lookup"><span data-stu-id="8ea15-117">Forking and Cloning the TODO Application</span></span>
<span data-ttu-id="8ea15-118">De TODO-toepassing die wordt gebruikt door deze zelfstudie implementeert een eenvoudige web-front via een MongoDB-exemplaar waarin een takenlijsten wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="8ea15-118">The TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="8ea15-119">Ga na het aanmelden met GitHub, [hier](https://github.com/stepro/node-todo) te vinden van de toepassing en vertakken met behulp van de koppeling in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="8ea15-119">After signing in to GitHub, go [here](https://github.com/stepro/node-todo) to find the application and fork it using the link in the top right.</span></span> <span data-ttu-id="8ea15-120">Dit moet een opslagplaats maken in uw account met de naam *accountname*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="8ea15-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="8ea15-121">Nu op uw ontwikkelcomputer deze opslagplaats klonen:</span><span class="sxs-lookup"><span data-stu-id="8ea15-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="8ea15-122">We gebruiken deze lokale kloon van de opslagplaats enigszins hoger als u wijzigingen aanbrengt aan de broncode.</span><span class="sxs-lookup"><span data-stu-id="8ea15-122">We'll use this local clone of the repository a little later when making changes to the source code.</span></span>

## <a name="creating-and-configuring-the-linux-virtual-machines"></a><span data-ttu-id="8ea15-123">Maken en configureren van de virtuele Linux-Machines</span><span class="sxs-lookup"><span data-stu-id="8ea15-123">Creating and Configuring the Linux Virtual Machines</span></span>
<span data-ttu-id="8ea15-124">Azure biedt uitstekende ondersteuning voor onbewerkte compute gebruik van Linux virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8ea15-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="8ea15-125">Dit deel van de zelfstudie ziet u hoe u kunt eenvoudig ronddraaien van twee Linux virtuele machines en implementeert de TODO-toepassing, de front-end web uitgevoerd op één en het MongoDB-exemplaar op de andere.</span><span class="sxs-lookup"><span data-stu-id="8ea15-125">This part of the tutorial shows how you can easily spin up two Linux virtual machines and deploy the TODO application to them, running the web frontend on one and the MongoDB instance on the other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="8ea15-126">Maken van virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="8ea15-126">Creating Virtual Machines</span></span>
<span data-ttu-id="8ea15-127">De eenvoudigste manier om een nieuwe virtuele machine maken in Azure is de Azure Portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ea15-127">The easiest way to create a new virtual machine in Azure is to use the Azure Portal.</span></span> <span data-ttu-id="8ea15-128">Klik op [hier](https://portal.azure.com) aanmelden en starten van de Azure-Portal in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8ea15-128">Click [here](https://portal.azure.com) to sign in and launch the Azure Portal in your web browser.</span></span> <span data-ttu-id="8ea15-129">Nadat de Azure Portal is geladen, kunt u de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="8ea15-129">Once the Azure Portal has loaded, complete the following steps:</span></span>

* <span data-ttu-id="8ea15-130">Klik op de koppeling '+ Nieuw';</span><span class="sxs-lookup"><span data-stu-id="8ea15-130">Click the "+ New" link;</span></span>
* <span data-ttu-id="8ea15-131">De categorie "Compute" kiest en kiest u 'Ubuntu Server 14.04 TNS';</span><span class="sxs-lookup"><span data-stu-id="8ea15-131">Pick the "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="8ea15-132">Selecteer het implementatiemodel ' Resource Manager ' en klik op 'Maken';</span><span class="sxs-lookup"><span data-stu-id="8ea15-132">Select the "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="8ea15-133">Vul in de basisbeginselen deze richtlijnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ea15-133">Fill in the basics following these guidelines:</span></span>
  * <span data-ttu-id="8ea15-134">Geef een naam die u later; eenvoudig kunt herkennen</span><span class="sxs-lookup"><span data-stu-id="8ea15-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="8ea15-135">Voor deze zelfstudie kiest wachtwoordverificatie;</span><span class="sxs-lookup"><span data-stu-id="8ea15-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="8ea15-136">Een nieuwe resourcegroep maken met de naam van een identificeerbaar.</span><span class="sxs-lookup"><span data-stu-id="8ea15-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="8ea15-137">Voor de grootte van de virtuele Machine is 'A1 standaard' een redelijke keuze voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8ea15-137">For the Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="8ea15-138">Zorg ervoor dat het schijftype is 'Standaard' voor extra instellingen en de overige standaardinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="8ea15-138">For additional settings, ensure the disk type is "Standard" and accept all the remaining defaults.</span></span>
* <span data-ttu-id="8ea15-139">Ere van het maken op de pagina overzicht.</span><span class="sxs-lookup"><span data-stu-id="8ea15-139">Kick off the creation on the summary page.</span></span>

<span data-ttu-id="8ea15-140">Voer de bovenstaande procedure tweemaal voor het maken van twee virtuele Linux-machines, één voor de web-frontend en één voor de MongoDB-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8ea15-140">Perform the above process twice to create two Linux virtual machines, one for the web frontend and one for the MongoDB instance.</span></span> <span data-ttu-id="8ea15-141">Maken van de virtuele machines duurt ongeveer 5 tot 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="8ea15-141">Creation of the virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="8ea15-142">Een DNS-vermelding toe te wijzen voor virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="8ea15-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="8ea15-143">Virtuele machines in Azure gemaakt worden standaard alleen toegankelijk zijn via een openbaar IP-adres zoals 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="8ea15-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="8ea15-144">We maken de machines meer gemakkelijk kan worden geïdentificeerd door toe te wijzen DNS-vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="8ea15-144">Let's make the machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="8ea15-145">Zodra de portal geeft aan dat de virtuele machines zijn gemaakt, klik op de koppeling 'Virtuele machines' in de navigatiebalk links en zoek uw machines.</span><span class="sxs-lookup"><span data-stu-id="8ea15-145">Once the portal indicates that the virtual machines have been created, click on the "Virtual machines" link in the left navbar and locate your machines.</span></span> <span data-ttu-id="8ea15-146">Voor elke computer:</span><span class="sxs-lookup"><span data-stu-id="8ea15-146">For each machine:</span></span>

* <span data-ttu-id="8ea15-147">Zoek de Essentials-tabblad en klik op het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8ea15-147">Locate the Essentials tab and click on the Public IP Address;</span></span>
* <span data-ttu-id="8ea15-148">Toewijzen van een label van DNS-naam in de openbare IP-adresconfiguratie en opslaan.</span><span class="sxs-lookup"><span data-stu-id="8ea15-148">In the public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="8ea15-149">De portal zorgt ervoor dat de opgegeven naam beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="8ea15-149">The portal will ensure that the name you specify is available.</span></span> <span data-ttu-id="8ea15-150">Na het opslaan van de configuratie van uw virtuele machines hebben hostnamen vergelijkbaar met `machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="8ea15-150">After saving the configuration, your virtual machines will have host names similar to `machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-to-the-virtual-machines"></a><span data-ttu-id="8ea15-151">Verbinding maken met de virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="8ea15-151">Connecting to the Virtual Machines</span></span>
<span data-ttu-id="8ea15-152">Wanneer uw virtuele machines zijn ingericht, zijn ze vooraf geconfigureerd voor het toestaan van externe verbindingen via SSH.</span><span class="sxs-lookup"><span data-stu-id="8ea15-152">When your virtual machines were provisioned, they were pre-configured to allow remote connections over SSH.</span></span> <span data-ttu-id="8ea15-153">Dit is het mechanisme dat wordt gebruikt om de virtuele machines configureren.</span><span class="sxs-lookup"><span data-stu-id="8ea15-153">This is the mechanism we will use to configure the virtual machines.</span></span> <span data-ttu-id="8ea15-154">Als u van Windows voor de ontwikkeling gebruikmaakt, moet u een SSH-client krijgen als u nog geen een.</span><span class="sxs-lookup"><span data-stu-id="8ea15-154">If you are using Windows for your development, you will need to get an SSH client if you do not already have one.</span></span> <span data-ttu-id="8ea15-155">Een algemene keuze hier is PuTTY dat kan worden gedownload van [hier](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="8ea15-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="8ea15-156">Macintosh- en Linux-OSes worden geleverd met een versie van SSH vooraf zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="8ea15-157">De virtuele Machine van de webserver-Frontend configureren</span><span class="sxs-lookup"><span data-stu-id="8ea15-157">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="8ea15-158">SSH met de web frontend-machine die u hebt gemaakt met PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="8ea15-158">SSH to the web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="8ea15-159">U ziet een welkomstbericht gevolgd door een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="8ea15-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="8ea15-160">Eerst laten we controleren of git en knooppunt zijn beide geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="8ea15-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="8ea15-161">Sinds de toepassing web frontend op sommige systeemeigen Node.js-modules vertrouwt, moeten we ook installeert de essentiële van build-hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="8ea15-161">Since the application's web frontend relies on some native Node.js modules, we also need to install the essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="8ea15-162">Tot slot gaan we installeert u een Node.js-toepassing aangeroepen *permanent*, waarmee Node.js servertoepassingen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="8ea15-162">Finally, let's install a Node.js application called *forever*, which helps to run Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="8ea15-163">Dit zijn alle afhankelijkheden die nodig zijn op deze virtuele machine moeten kunnen maken van de toepassing web frontend uitvoeren, dus gaan we aan dat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-163">These are all the dependencies needed on this virtual machine to be able to run the application's web frontend, so let's get that running.</span></span> <span data-ttu-id="8ea15-164">We gaan een bare kloon van de GitHub-opslagplaats die u eerder forked zodat u eenvoudig updates aan de virtuele machine publiceren (komen aan bod in dit scenario update later) en de bare kloon zodat deze versie van de opslagplaats die daadwerkelijk kan worden uitgevoerd te klonen maken om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="8ea15-164">To do this, we will first create a bare clone of the GitHub repository you previously forked so that you can easily publish updates to the virtual machine (we'll cover this update scenario later), and then clone the bare clone to provide a version of the repository that can actually be executed.</span></span>

<span data-ttu-id="8ea15-165">Vanaf basismap (~), voer de volgende opdrachten (vervangen *accountname* met de naam van uw GitHub-gebruikersaccount):</span><span class="sxs-lookup"><span data-stu-id="8ea15-165">Starting from the home (~) directory, run the following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="8ea15-166">Nu de knooppunt-todo-map en voert u deze opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="8ea15-166">Now enter the node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="8ea15-167">Web-frontend van de toepassing nu wordt uitgevoerd, maar er is één stap voordat u toegang hebt tot de toepassing van een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8ea15-167">The application's web frontend is now running, however there is one more step before you can access the application from a web browser.</span></span> <span data-ttu-id="8ea15-168">De virtuele machine die u hebt gemaakt, wordt beveiligd door een Azure-resource aangeroepen een *netwerkbeveiligingsgroep*, die voor u is gemaakt bij het inrichten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8ea15-168">The virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned the virtual machine.</span></span> <span data-ttu-id="8ea15-169">Deze bron kan op dit moment alleen externe aanvragen op poort 22 worden doorgestuurd naar de virtuele machine, waardoor de SSH-communicatie met de computer, maar niets anders.</span><span class="sxs-lookup"><span data-stu-id="8ea15-169">Currently, this resource only allows external requests to port 22 to be routed to the virtual machine, which enables SSH communication with the machine but nothing else.</span></span> <span data-ttu-id="8ea15-170">Dus als u wilt weergeven van de TODO-toepassing die is geconfigureerd om uit te voeren op poort 8080, moet deze poort ook worden geopend.</span><span class="sxs-lookup"><span data-stu-id="8ea15-170">So in order to view the TODO application, which is configured to run on port 8080, this port also needs to be opened up.</span></span>

<span data-ttu-id="8ea15-171">Ga terug naar de Azure Portal en de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ea15-171">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="8ea15-172">Klik op 'Resourcegroepen' in de navigatiebalk links;</span><span class="sxs-lookup"><span data-stu-id="8ea15-172">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="8ea15-173">Selecteer de resourcegroep met de virtuele machine;</span><span class="sxs-lookup"><span data-stu-id="8ea15-173">Select the resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="8ea15-174">Selecteer in de resulterende lijst met resources de netwerkbeveiligingsgroep (één met een pictogram schild);</span><span class="sxs-lookup"><span data-stu-id="8ea15-174">In the resulting list of resources, select the network security group (the one with a shield icon);</span></span>
* <span data-ttu-id="8ea15-175">Kies in de eigenschappen 'inkomende beveiligingsregels';</span><span class="sxs-lookup"><span data-stu-id="8ea15-175">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="8ea15-176">Klik in de werkbalk op "Toevoegen";</span><span class="sxs-lookup"><span data-stu-id="8ea15-176">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="8ea15-177">Geef een naam op zoals 'standaard-toestaan-todo';</span><span class="sxs-lookup"><span data-stu-id="8ea15-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="8ea15-178">Stel het protocol op de 'TCP';</span><span class="sxs-lookup"><span data-stu-id="8ea15-178">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="8ea15-179">Stel het doelpoortbereik naar '8080';</span><span class="sxs-lookup"><span data-stu-id="8ea15-179">Set the destination port range to "8080";</span></span>
* <span data-ttu-id="8ea15-180">Klik op OK en wacht totdat de beveiligingsregel moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ea15-180">Click OK and wait for the security rule to be created.</span></span>

<span data-ttu-id="8ea15-181">Nadat deze regel is gemaakt, de toepassing TODO iedereen op internet zichtbaar is en u kunt bladeren, bijvoorbeeld met een URL, zoals:</span><span class="sxs-lookup"><span data-stu-id="8ea15-181">After creating this security rule, the TODO application is publically visible on the internet and you can browse to it, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="8ea15-182">U ziet dat hoewel we de MongoDB-virtuele machine nog niet hebt geconfigureerd, de TODO-toepassing wordt weergegeven behoorlijk functioneel te laten.</span><span class="sxs-lookup"><span data-stu-id="8ea15-182">You will notice that even though we have not yet configured the MongoDB virtual machine, the TODO application appears to be quite functional.</span></span> <span data-ttu-id="8ea15-183">Dit is omdat de bron-opslagplaats is vastgelegd om een vooraf geïmplementeerde MongoDB-exemplaar te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8ea15-183">This is because the source repository is hardcoded to use a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="8ea15-184">Wanneer we de MongoDB-virtuele machine hebt geconfigureerd, wordt er Ga terug en wijzig de broncode voor het gebruik van onze persoonlijke MongoDB-exemplaar in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="8ea15-184">Once we have configured the MongoDB virtual machine, we will go back and change the source code to utilize our private MongoDB instance instead.</span></span>

### <a name="configuring-the-mongodb-virtual-machine"></a><span data-ttu-id="8ea15-185">De MongoDB-virtuele Machine configureren</span><span class="sxs-lookup"><span data-stu-id="8ea15-185">Configuring the MongoDB Virtual Machine</span></span>
<span data-ttu-id="8ea15-186">SSH met de tweede computer die u hebt gemaakt met PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="8ea15-186">SSH to the second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="8ea15-187">Na de behandeling van het welkomstbericht en een opdrachtprompt, installeer MongoDB (deze instructies zijn genomen [hier](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="8ea15-187">After seeing the welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="8ea15-188">MongoDB is standaard geconfigureerd zodat deze alleen toegankelijk is lokaal.</span><span class="sxs-lookup"><span data-stu-id="8ea15-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="8ea15-189">Voor deze zelfstudie wordt we MongoDB configureren zodat deze kan worden geopend op de virtuele machine van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8ea15-189">For this tutorial, we will configure MongoDB so it can be accessed from the application's virtual machine.</span></span> <span data-ttu-id="8ea15-190">Open het bestand /etc/mongod.conf in een context sudo en zoek de `# network interfaces` sectie.</span><span class="sxs-lookup"><span data-stu-id="8ea15-190">In a sudo context, open the /etc/mongod.conf file and locate the `# network interfaces` section.</span></span> <span data-ttu-id="8ea15-191">Wijzig de `net.bindIp` configuratiewaarde voor `0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="8ea15-191">Change the `net.bindIp` configuration value to `0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="8ea15-192">Deze configuratie is voor de doeleinden van deze zelfstudie alleen.</span><span class="sxs-lookup"><span data-stu-id="8ea15-192">This configuration is for the purposes of this tutorial only.</span></span> <span data-ttu-id="8ea15-193">Het is **niet** een aanbevolen beveiligingsprocedure en mag niet worden gebruikt in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8ea15-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="8ea15-194">Nu moet u de MongoDB-service is gestart:</span><span class="sxs-lookup"><span data-stu-id="8ea15-194">Now ensure the MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="8ea15-195">MongoDB werkt via poort 27017 standaard.</span><span class="sxs-lookup"><span data-stu-id="8ea15-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="8ea15-196">Op dezelfde manier die we nodig om te open poort 8080 op de virtuele machine van de webserver-frontend, moeten we dus open poort 27017 op de virtuele machine van MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8ea15-196">So, in the same way that we needed to open port 8080 on the web frontend virtual machine, we need to open port 27017 on the MongoDB virtual machine.</span></span>

<span data-ttu-id="8ea15-197">Ga terug naar de Azure Portal en de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8ea15-197">Return to the Azure Portal and complete the following steps:</span></span>

* <span data-ttu-id="8ea15-198">Klik op 'Resourcegroepen' in de navigatiebalk links;</span><span class="sxs-lookup"><span data-stu-id="8ea15-198">Click on "Resource groups" in the left navbar;</span></span>
* <span data-ttu-id="8ea15-199">Selecteer de resourcegroep met de virtuele machine van MongoDB;</span><span class="sxs-lookup"><span data-stu-id="8ea15-199">Select the resource group that contains the MongoDB virtual machine;</span></span>
* <span data-ttu-id="8ea15-200">Selecteer in de resulterende lijst met resources de netwerkbeveiligingsgroep (één met een pictogram schild) met dezelfde naam die u hebt opgegeven op de virtuele machine van MongoDB;</span><span class="sxs-lookup"><span data-stu-id="8ea15-200">In the resulting list of resources, select the network security group (the one with a shield icon) with the same name that you gave to the MongoDB virtual machine;</span></span>
* <span data-ttu-id="8ea15-201">Kies in de eigenschappen 'inkomende beveiligingsregels';</span><span class="sxs-lookup"><span data-stu-id="8ea15-201">In the properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="8ea15-202">Klik in de werkbalk op "Toevoegen";</span><span class="sxs-lookup"><span data-stu-id="8ea15-202">In the toolbar, click "Add";</span></span>
* <span data-ttu-id="8ea15-203">Geef een naam op zoals 'standaard-toestaan-mongo';</span><span class="sxs-lookup"><span data-stu-id="8ea15-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="8ea15-204">Stel het protocol op de 'TCP';</span><span class="sxs-lookup"><span data-stu-id="8ea15-204">Set the protocol to "TCP";</span></span>
* <span data-ttu-id="8ea15-205">Stel het doelpoortbereik naar '27017';</span><span class="sxs-lookup"><span data-stu-id="8ea15-205">Set the destination port range to "27017";</span></span>
* <span data-ttu-id="8ea15-206">Klik op OK en wacht totdat de beveiligingsregel moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ea15-206">Click OK and wait for the security rule to be created.</span></span>

## <a name="iterating-on-the-todo-application"></a><span data-ttu-id="8ea15-207">Doorlopen van de TODO-toepassing</span><span class="sxs-lookup"><span data-stu-id="8ea15-207">Iterating on the TODO application</span></span>
<span data-ttu-id="8ea15-208">Tot nu toe hebben we twee virtuele Linux-machines ingericht: één met de toepassing web frontend en één die MongoDB-exemplaar wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-208">So far, we have provisioned two Linux virtual machines: one that is running the application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="8ea15-209">Maar er is een probleem - ingerichte MongoDB-exemplaar is niet werkelijk nog gebruikmaakt van de web-frontend.</span><span class="sxs-lookup"><span data-stu-id="8ea15-209">But there is a problem - the web frontend isn't actually using the provisioned MongoDB instance yet.</span></span> <span data-ttu-id="8ea15-210">Laten we dit oplossen door web-front-code voor het gebruik van een omgevingsvariabele in plaats van een exemplaar vastgelegde bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8ea15-210">Let's fix that by updating the web frontend code to use an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-the-todo-application"></a><span data-ttu-id="8ea15-211">Het wijzigen van de TODO-toepassing</span><span class="sxs-lookup"><span data-stu-id="8ea15-211">Changing the TODO application</span></span>
<span data-ttu-id="8ea15-212">Open op uw ontwikkelcomputer waarop u eerst de opslagplaats knooppunt todo hebt gekloond, de `node-todo/config/database.js` -bestand in uw favoriete editor en wijzig de waarde van de url van de vastgelegde waarde zoals `mongodb://...` naar `process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="8ea15-212">On your development machine where you first cloned the node-todo repository, open the `node-todo/config/database.js` file in your favorite editor and change the url value from the hard-coded value like `mongodb://...` to `process.env.MONGODB`.</span></span>

<span data-ttu-id="8ea15-213">Uw wijzigingen en push naar de GitHub-master:</span><span class="sxs-lookup"><span data-stu-id="8ea15-213">Commit your changes and push to the GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="8ea15-214">Helaas publiceren niet dit de wijziging op de virtuele machine van de webserver-frontend.</span><span class="sxs-lookup"><span data-stu-id="8ea15-214">Unfortunately, this doesn't publish the change to the web frontend virtual machine.</span></span> <span data-ttu-id="8ea15-215">Laten we enkele meer wijzigingen aanbrengen aan dat de virtuele machine om in te schakelen van een eenvoudige maar effectieve mechanisme voor het publiceren van updates, zodat u snel het effect van de wijzigingen in de productieomgeving kunt zien.</span><span class="sxs-lookup"><span data-stu-id="8ea15-215">Let's make a few more changes to that virtual machine to enable a simple but effective mechanism for publishing updates so you can quickly observe the effect of the changes in the live environment.</span></span>

### <a name="configuring-the-web-frontend-virtual-machine"></a><span data-ttu-id="8ea15-216">De virtuele Machine van de webserver-Frontend configureren</span><span class="sxs-lookup"><span data-stu-id="8ea15-216">Configuring the Web Frontend Virtual Machine</span></span>
<span data-ttu-id="8ea15-217">Intrekken dat we eerder een bare kloon van de opslagplaats knooppunt todo op de virtuele machine van de webserver-frontend gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8ea15-217">Recall that we previously created a bare clone of the node-todo repository on the web frontend virtual machine.</span></span> <span data-ttu-id="8ea15-218">Het blijkt dat deze actie gemaakt met een nieuwe externe Git waarvoor wijzigingen kunnen worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-218">It turns out that this action created a new Git remote to which changes can be pushed.</span></span> <span data-ttu-id="8ea15-219">Eenvoudig pushen naar dit externe geeft niet erg echter het model snelle herhaling die ontwikkelaars zoekt werkte op hun code.</span><span class="sxs-lookup"><span data-stu-id="8ea15-219">However, simply pushing to this remote doesn't quite give the rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="8ea15-220">Wat we willen graag kunnen doen is Zorg ervoor dat de actieve TODO-toepassing wordt automatisch bijgewerkt wanneer er een push naar de externe opslagplaats op de virtuele machine optreedt, is.</span><span class="sxs-lookup"><span data-stu-id="8ea15-220">What we would like to be able to do is ensure that when a push to the remote repository on the virtual machine occurs, the running TODO application is automatically updated.</span></span> <span data-ttu-id="8ea15-221">Dit is gelukkig gemakkelijk te bereiken met git.</span><span class="sxs-lookup"><span data-stu-id="8ea15-221">Fortunately, this is easy to achieve with git.</span></span>

<span data-ttu-id="8ea15-222">GIT wordt een aantal hooks die worden aangeroepen op bepaalde tijden om te reageren op in de opslagplaats uitgevoerde acties.</span><span class="sxs-lookup"><span data-stu-id="8ea15-222">Git exposes a number of hooks that are called at particular times to react to actions taken on the repository.</span></span> <span data-ttu-id="8ea15-223">Deze worden opgegeven met behulp van de shell-scripts in de opslagplaats `hooks` map.</span><span class="sxs-lookup"><span data-stu-id="8ea15-223">These are specified using shell scripts in the repository's `hooks` folder.</span></span> <span data-ttu-id="8ea15-224">De hook dat meest van toepassing is voor het scenario met automatische updates is het `post-update` gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="8ea15-224">The hook that is most applicable for the auto-update scenario is the `post-update` event.</span></span>

<span data-ttu-id="8ea15-225">In een SSH-sessie op de virtuele machine van de webserver-frontend, wijzigt u in de `~/node-todo.git/hooks` directory en voegt u de volgende inhoud naar een bestand met de naam `post-update` (vervangen `machinename` en `region` met uw gegevens van de virtuele machine MongoDB):</span><span class="sxs-lookup"><span data-stu-id="8ea15-225">In a SSH session to the web frontend virtual machine, change to the `~/node-todo.git/hooks` directory and add the following content to a file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="8ea15-226">Zorg ervoor dat dit bestand is uitvoerbaar bestand met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8ea15-226">Ensure this file is executable by running the following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="8ea15-227">Dit script zorgt ervoor dat de huidige servertoepassing is gestopt, de code in de gekloonde opslagplaats wordt bijgewerkt naar de meest recente bijgewerkte afhankelijkheden is voldaan en de server opnieuw is opgestart.</span><span class="sxs-lookup"><span data-stu-id="8ea15-227">This script ensures that the current server application is stopped, the code in the cloned repository is updated to the latest, any updated dependencies are satisfied, and the server is restarted.</span></span> <span data-ttu-id="8ea15-228">Ook zorgt ervoor dat de omgeving in voorbereiding voor het ontvangen van de eerste toepassingsupdate om de MongoDB-exemplaar van een omgevingsvariabele is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-228">It also ensures that the environment has been configured in preparation for receiving our first application update to get the MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="8ea15-229">Configureren van uw ontwikkelcomputer</span><span class="sxs-lookup"><span data-stu-id="8ea15-229">Configuring your Development Machine</span></span>
<span data-ttu-id="8ea15-230">Nu gaan we aan uw ontwikkelcomputer aangesloten op de virtuele machine van de webserver-frontend.</span><span class="sxs-lookup"><span data-stu-id="8ea15-230">Now let's get your development machine hooked up to the web frontend virtual machine.</span></span> <span data-ttu-id="8ea15-231">Dit is net zo eenvoudig als het toevoegen van de bare-opslagplaats op de virtuele machine als een externe.</span><span class="sxs-lookup"><span data-stu-id="8ea15-231">This is as simple as adding the bare repository on the virtual machine as a remote.</span></span> <span data-ttu-id="8ea15-232">Voer de volgende opdracht om dit te doen (vervangen *gebruiker* met de naam van de virtuele machine aanmelding voor uw web-frontend en *machinename* en *regio* indien nodig):</span><span class="sxs-lookup"><span data-stu-id="8ea15-232">Run the following command to do this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="8ea15-233">Dit is alles dat nodig is om in te schakelen pushen of wijzigingen van kracht publiceert, van de virtuele machine van de webserver-frontend.</span><span class="sxs-lookup"><span data-stu-id="8ea15-233">This is all that is needed to enable pushing, or in effect publishing, changes to the web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="8ea15-234">Publicatie-Updates</span><span class="sxs-lookup"><span data-stu-id="8ea15-234">Publishing Updates</span></span>
<span data-ttu-id="8ea15-235">Laten we de een wijziging die is gedaan tot nu toe zodat ons eigen MongoDB-exemplaar wordt gebruikt door de toepassing publiceren:</span><span class="sxs-lookup"><span data-stu-id="8ea15-235">Let's publish the one change that has been made so far so that the application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="8ea15-236">U ziet de uitvoer is vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="8ea15-236">You should see output similar to this:</span></span>

    Counting objects: 4, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    To username@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="8ea15-237">Nadat deze opdracht is voltooid, probeert u het vernieuwen van de toepassing in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8ea15-237">After this command completes, try refreshing the application in a web browser.</span></span> <span data-ttu-id="8ea15-238">U moet mogelijk dat de takenlijst die hier wordt gepresenteerd is leeg en niet langer gebonden aan het gedeelde geïmplementeerde MongoDB-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="8ea15-238">You should be able to see that the TODO list presented here is empty and no longer tied to the shared deployed MongoDB instance.</span></span>

<span data-ttu-id="8ea15-239">Zorg voor het voltooien van de zelfstudie, wijziging van een andere, beter zichtbaar.</span><span class="sxs-lookup"><span data-stu-id="8ea15-239">To complete the tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="8ea15-240">Open het node-todo/public/index.html-bestand met behulp van uw favoriete editor op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="8ea15-240">On your development machine, open the node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="8ea15-241">Zoek de header jumbotron en wijzig de titel van het 'Ik ben een Todo-aholic' naar 'Ik ben een Todo-aholic op Azure!'.</span><span class="sxs-lookup"><span data-stu-id="8ea15-241">Locate the jumbotron header and change  the title from "I'm a Todo-aholic" to "I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="8ea15-242">Nu gaan we doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="8ea15-242">Now let's commit:</span></span>

    git commit -am "Azurify the title"

<span data-ttu-id="8ea15-243">Deze tijd, de wijziging gaat publiceren naar Azure voordat u deze terug naar de GitHub-repo:</span><span class="sxs-lookup"><span data-stu-id="8ea15-243">This time, let's publish the change to Azure before pushing it to back to the GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="8ea15-244">Zodra deze opdracht is voltooid, vernieuw de webpagina en ziet u de wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="8ea15-244">Once this command completes, refresh the web page and you will see the changes.</span></span> <span data-ttu-id="8ea15-245">Omdat ze er goed uitziet, push de wijziging terug naar de oorsprong externe:</span><span class="sxs-lookup"><span data-stu-id="8ea15-245">Since they look good, push the change back to the origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="8ea15-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ea15-246">Next Steps</span></span>
<span data-ttu-id="8ea15-247">In dit artikel hebt u geleerd hoe een Node.js-toepassing uitvoeren en deze implementeren op Linux-machines in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8ea15-247">This article showed how to take a Node.js application and deploy it to Linux virtual machines running in Azure.</span></span> <span data-ttu-id="8ea15-248">Zie voor meer informatie over virtuele Linux-machines in Azure, [Inleiding tot Linux op Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="8ea15-248">To learn more about Linux virtual machines in Azure, see [Introduction to Linux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="8ea15-249">In het [Node.js Developer Center](/develop/nodejs/) vindt u meer informatie over het ontwikkelen van Node.js-toepassingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="8ea15-249">For more information about how to develop Node.js applications on Azure, see the [Node.js Developer Center](/develop/nodejs/).</span></span>

