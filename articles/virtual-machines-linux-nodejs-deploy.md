---
title: aaaDeploy een Node.js-toepassing tooLinux virtuele Machines in Azure
description: Meer informatie over hoe een Node.js toodeploy toepassing tooLinux virtuele machines in Azure.
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
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="e42c1-103">Een Node.js-toepassing tooLinux virtuele Machines in Azure implementeren</span><span class="sxs-lookup"><span data-stu-id="e42c1-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="e42c1-104">Deze zelfstudie laat zien hoe tootake een Node.js-toepassing en implementeer het tooLinux virtuele machines in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="e42c1-105">Hallo-instructies in deze zelfstudie kunnen worden uitgevoerd op elk besturingssysteem waarmee Node.js uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="e42c1-106">U leert hoe:</span><span class="sxs-lookup"><span data-stu-id="e42c1-106">You'll learn how to:</span></span>

* <span data-ttu-id="e42c1-107">Fork- en kloon een GitHub-opslagplaats met een eenvoudige toepassing voor TODO;</span><span class="sxs-lookup"><span data-stu-id="e42c1-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="e42c1-108">Maken en configureren van twee virtuele Linux-machines in Azure toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e42c1-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="e42c1-109">De toepassing hello herhalen door te pushen updates toohello web frontend virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e42c1-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="e42c1-110">toocomplete deze zelfstudie maakt u een GitHub-account en een Microsoft Azure-account nodig en Hallo mogelijkheid toouse Git van een ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="e42c1-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="e42c1-111">Als u geen een GitHub-account hebt, kunt u zich aanmeldt [hier](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="e42c1-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="e42c1-112">Als u hebt een [Microsoft Azure](https://azure.microsoft.com/) -account, u kunt zich aanmelden voor een gratis proefversie [hier](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e42c1-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="e42c1-113">Dit ook loodst u door Hallo aanmeldingsproces voor een [Microsoft-Account](http://account.microsoft.com) als u nog geen een.</span><span class="sxs-lookup"><span data-stu-id="e42c1-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="e42c1-114">Als u een Visual Studio-abonnee bent, u kunt ook [activeren van uw voordelen als MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e42c1-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="e42c1-115">Als u geen git op uw ontwikkelcomputer, als u een Macintosh of Windows-machine, installeert u git van [hier](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="e42c1-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="e42c1-116">Als u van Linux gebruikmaakt, installeert u git met Hallo mechanisme meest geschikt is voor u, zoals `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="e42c1-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="e42c1-117">Vertakken en klonen Hallo TODO-toepassing</span><span class="sxs-lookup"><span data-stu-id="e42c1-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="e42c1-118">Hallo TODO-toepassing die wordt gebruikt door deze zelfstudie implementeert een eenvoudige web-front via een MongoDB-exemplaar waarin een takenlijsten wordt bijgehouden.</span><span class="sxs-lookup"><span data-stu-id="e42c1-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="e42c1-119">Ga na het aanmelden tooGitHub, [hier](https://github.com/stepro/node-todo) toofind toepassing hello en met behulp van Hallo-koppeling in de rechterbovenhoek Hallo vertakken.</span><span class="sxs-lookup"><span data-stu-id="e42c1-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="e42c1-120">Dit moet een opslagplaats maken in uw account met de naam *accountname*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="e42c1-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="e42c1-121">Nu op uw ontwikkelcomputer deze opslagplaats klonen:</span><span class="sxs-lookup"><span data-stu-id="e42c1-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="e42c1-122">We gebruiken deze lokale kloon van de opslagplaats Hallo enigszins hoger als u wijzigingen aanbrengt toohello broncode.</span><span class="sxs-lookup"><span data-stu-id="e42c1-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="e42c1-123">Maken en configureren van Hallo virtuele Linux-Machines</span><span class="sxs-lookup"><span data-stu-id="e42c1-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="e42c1-124">Azure biedt uitstekende ondersteuning voor onbewerkte compute gebruik van Linux virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e42c1-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="e42c1-125">Dit deel van Hallo zelfstudie ziet hoe u kunt eenvoudig ronddraaien van twee Linux virtuele machines en implementeert Hallo TODO toepassing toothem, actieve Hallo web frontend op één en Hallo MongoDB-exemplaar op Hallo andere.</span><span class="sxs-lookup"><span data-stu-id="e42c1-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="e42c1-126">Maken van virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="e42c1-126">Creating Virtual Machines</span></span>
<span data-ttu-id="e42c1-127">Hallo gemakkelijkste manier toocreate een nieuwe virtuele machine in Azure is toouse hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="e42c1-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="e42c1-128">Klik op [hier](https://portal.azure.com) toosign in en start hello Azure-Portal in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e42c1-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="e42c1-129">Nadat de hello Azure Portal is geladen, moet u Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e42c1-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="e42c1-130">Klik op Hallo plusteken (+ nieuw) koppelen;</span><span class="sxs-lookup"><span data-stu-id="e42c1-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="e42c1-131">Kies Hallo 'Compute' categorie en kiest u 'Ubuntu Server 14.04 TNS';</span><span class="sxs-lookup"><span data-stu-id="e42c1-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="e42c1-132">Hallo ' Resource Manager '-implementatiemodel selecteren en klik op 'Maken';</span><span class="sxs-lookup"><span data-stu-id="e42c1-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="e42c1-133">Vul Hallo basisbeginselen van deze richtlijnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e42c1-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="e42c1-134">Geef een naam die u later; eenvoudig kunt herkennen</span><span class="sxs-lookup"><span data-stu-id="e42c1-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="e42c1-135">Voor deze zelfstudie kiest wachtwoordverificatie;</span><span class="sxs-lookup"><span data-stu-id="e42c1-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="e42c1-136">Een nieuwe resourcegroep maken met de naam van een identificeerbaar.</span><span class="sxs-lookup"><span data-stu-id="e42c1-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="e42c1-137">Voor Hallo grootte van virtuele Machine is 'A1 standaard' een redelijke keuze voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e42c1-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="e42c1-138">Voor extra instellingen Zorg ervoor dat het schijftype Hallo 'Standaard' en accepteer dat alle overige standaardwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="e42c1-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="e42c1-139">Ere van Hallo maken op de overzichtspagina Hallo.</span><span class="sxs-lookup"><span data-stu-id="e42c1-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="e42c1-140">Uitvoeren van de bovenstaande Hallo tweemaal toocreate twee virtuele Linux-machines, één voor Hallo web frontend en één voor Hallo MongoDB-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e42c1-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="e42c1-141">Maken van virtuele machines van Hallo duurt ongeveer 5 tot 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="e42c1-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="e42c1-142">Een DNS-vermelding toe te wijzen voor virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="e42c1-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="e42c1-143">Virtuele machines in Azure gemaakt worden standaard alleen toegankelijk zijn via een openbaar IP-adres zoals 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="e42c1-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="e42c1-144">We maken door het toewijzen van DNS-vermeldingen Hallo machines meer gemakkelijk kan worden geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="e42c1-145">Zodra het Hallo-portal geeft aan dat Hallo virtuele machines zijn gemaakt, klikt u op Hallo 'Virtuele machines' koppeling in het linkerdeelvenster navigatiebalk Hallo en zoek uw machines.</span><span class="sxs-lookup"><span data-stu-id="e42c1-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="e42c1-146">Voor elke computer:</span><span class="sxs-lookup"><span data-stu-id="e42c1-146">For each machine:</span></span>

* <span data-ttu-id="e42c1-147">Zoek Hallo Essentials tabblad en klik op Hallo openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="e42c1-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="e42c1-148">Een label van DNS-naam toewijzen en sla in Hallo openbare IP-adresconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="e42c1-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="e42c1-149">Hallo portal zorgt ervoor dat u opgeeft Hallo-naam beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="e42c1-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="e42c1-150">Na het opslaan van Hallo configuratie uw virtuele machines hebben vergelijkbare hostnamen te`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="e42c1-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="e42c1-151">Verbinding maken met toohello virtuele Machines</span><span class="sxs-lookup"><span data-stu-id="e42c1-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="e42c1-152">Wanneer uw virtuele machines zijn ingericht, zijn ze vooraf geconfigureerde tooallow externe verbindingen via SSH.</span><span class="sxs-lookup"><span data-stu-id="e42c1-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="e42c1-153">Dit is Hallo-mechanisme gebruiken we tooconfigure Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="e42c1-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="e42c1-154">Als u van Windows voor de ontwikkeling gebruikmaakt, moet u een SSH-client tooget als u nog geen een.</span><span class="sxs-lookup"><span data-stu-id="e42c1-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="e42c1-155">Een algemene keuze hier is PuTTY dat kan worden gedownload van [hier](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="e42c1-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="e42c1-156">Macintosh- en Linux-OSes worden geleverd met een versie van SSH vooraf zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="e42c1-157">Hallo Web Frontend virtuele Machine configureren</span><span class="sxs-lookup"><span data-stu-id="e42c1-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="e42c1-158">SSH toohello web frontend machine hebt gemaakt met behulp PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="e42c1-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="e42c1-159">U ziet een welkomstbericht gevolgd door een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e42c1-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="e42c1-160">Eerst laten we controleren of git en knooppunt zijn beide geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="e42c1-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="e42c1-161">Omdat een van de toepassing hello web frontend vertrouwt op sommige systeemeigen Node.js-modules, moeten we ook tooinstall Hallo essentiële set build hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="e42c1-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="e42c1-162">Tot slot gaan we installeert u een Node.js-toepassing aangeroepen *permanent*, waarmee toorun Node.js server-toepassingen:</span><span class="sxs-lookup"><span data-stu-id="e42c1-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="e42c1-163">Dit zijn alle Hallo afhankelijkheden die op deze virtuele machine toobe kunnen toorun Hallo van de toepassing web frontend nodig, dus gaan we aan dat wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="e42c1-164">toodo, we gaan een bare kloon van de GitHub-opslagplaats Hallo u eerder forked zodat u eenvoudig updates toohello virtuele machine publiceren (komen aan bod in dit scenario update later) en vervolgens Hallo bare kloon tooprovide klonen een versie van Hallo eerst maken de opslagplaats die daadwerkelijk kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="e42c1-165">Hallo volgende opdrachten vanaf Hallo basismap (~), worden uitgevoerd (vervangen *accountname* met de naam van uw GitHub-gebruikersaccount):</span><span class="sxs-lookup"><span data-stu-id="e42c1-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="e42c1-166">Nu Hallo knooppunt todo-directory in en voer deze opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="e42c1-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="e42c1-167">Hallo van de toepassing web frontend wordt nu uitgevoerd, maar er is één stap voordat u toegang hebt tot de toepassing hello vanuit een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e42c1-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="e42c1-168">Hallo wordt virtuele machine die u hebt gemaakt beveiligd door een Azure-resource aangeroepen een *netwerkbeveiligingsgroep*, die voor u bij het inrichten van virtuele machine Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e42c1-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="e42c1-169">Deze resource kan momenteel alleen externe aanvragen tooport 22 toobe gerouteerd toohello virtuele machine, waardoor de SSH-communicatie met de Hallo machine maar niets anders.</span><span class="sxs-lookup"><span data-stu-id="e42c1-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="e42c1-170">Dus in volgorde tooview Hallo TODO-toepassing die geconfigureerd toorun op poort 8080 is, moet deze poort ook toobe die toegankelijk is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e42c1-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="e42c1-171">Ga terug toohello Azure-Portal en voltooien Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e42c1-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="e42c1-172">Klik op 'Resourcegroepen' in het linkerdeelvenster navigatiebalk Hallo;</span><span class="sxs-lookup"><span data-stu-id="e42c1-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="e42c1-173">Selecteer Hallo-resourcegroep met de virtuele machine;</span><span class="sxs-lookup"><span data-stu-id="e42c1-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="e42c1-174">Selecteer in de resulterende lijst met resources Hallo Hallo netwerkbeveiligingsgroep (hello een met een pictogram schild);</span><span class="sxs-lookup"><span data-stu-id="e42c1-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="e42c1-175">Kies in de eigenschappen van Hallo 'inkomende beveiligingsregels';</span><span class="sxs-lookup"><span data-stu-id="e42c1-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="e42c1-176">Klik in het Hallo-werkbalk op "Toevoegen";</span><span class="sxs-lookup"><span data-stu-id="e42c1-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="e42c1-177">Geef een naam op zoals 'standaard-toestaan-todo';</span><span class="sxs-lookup"><span data-stu-id="e42c1-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="e42c1-178">Hallo-protocol te instellen 'TCP';</span><span class="sxs-lookup"><span data-stu-id="e42c1-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="e42c1-179">Hallo doelpoortbereik ingesteld te '8080';</span><span class="sxs-lookup"><span data-stu-id="e42c1-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="e42c1-180">Klik op OK en wachten op Hallo beveiliging regel toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e42c1-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="e42c1-181">Nadat deze regel is gemaakt, Hallo TODO-toepassing is iedereen zichtbaar op Hallo van internet en u kunt bladeren tooit, bijvoorbeeld met een URL, zoals:</span><span class="sxs-lookup"><span data-stu-id="e42c1-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="e42c1-182">U ziet dat hoewel we Hallo MongoDB virtuele machine nog niet hebt geconfigureerd, Hallo TODO-toepassing wordt weergegeven toobe behoorlijk functioneel.</span><span class="sxs-lookup"><span data-stu-id="e42c1-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="e42c1-183">Dit is omdat Hallo bron opslagplaats hardcoded toouse vooraf geïmplementeerde MongoDB-exemplaar is.</span><span class="sxs-lookup"><span data-stu-id="e42c1-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="e42c1-184">Wanneer we Hallo MongoDB virtuele machine hebt geconfigureerd, wordt er Ga terug en wijzig Hallo source code tooutilize onze persoonlijke MongoDB-exemplaar in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="e42c1-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="e42c1-185">Hallo MongoDB virtuele Machine configureren</span><span class="sxs-lookup"><span data-stu-id="e42c1-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="e42c1-186">SSH toohello tweede machine hebt gemaakt met behulp PuTTY, ssh vanaf de opdrachtregel of uw andere favoriete SSH-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="e42c1-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="e42c1-187">Na de behandeling Welkom het Hallo-bericht en de opdrachtprompt, installeer MongoDB (deze instructies zijn genomen [hier](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="e42c1-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="e42c1-188">MongoDB is standaard geconfigureerd zodat deze alleen toegankelijk is lokaal.</span><span class="sxs-lookup"><span data-stu-id="e42c1-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="e42c1-189">Voor deze zelfstudie wordt we MongoDB configureren zodat deze kan worden geopend op van de toepassing hello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e42c1-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="e42c1-190">In een context sudo hello /etc/mongod.conf bestand openen en zoek Hallo `# network interfaces` sectie.</span><span class="sxs-lookup"><span data-stu-id="e42c1-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="e42c1-191">Wijziging Hallo `net.bindIp` configuratie waarde te`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="e42c1-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="e42c1-192">Deze configuratie is voor de toepassing hello van deze zelfstudie alleen.</span><span class="sxs-lookup"><span data-stu-id="e42c1-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="e42c1-193">Het is **niet** een aanbevolen beveiligingsprocedure en mag niet worden gebruikt in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="e42c1-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="e42c1-194">Nu moet Hallo MongoDB-service is gestart:</span><span class="sxs-lookup"><span data-stu-id="e42c1-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="e42c1-195">MongoDB werkt via poort 27017 standaard.</span><span class="sxs-lookup"><span data-stu-id="e42c1-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="e42c1-196">Dus in Hallo dezelfde manier dat we tooopen nodig poort 8080 op Hallo web frontend virtuele machine, moeten we tooopen poort 27017 op Hallo MongoDB virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e42c1-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="e42c1-197">Ga terug toohello Azure-Portal en voltooien Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e42c1-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="e42c1-198">Klik op 'Resourcegroepen' in het linkerdeelvenster navigatiebalk Hallo;</span><span class="sxs-lookup"><span data-stu-id="e42c1-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="e42c1-199">Selecteer Hallo-resourcegroep met Hallo MongoDB virtuele machine;</span><span class="sxs-lookup"><span data-stu-id="e42c1-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="e42c1-200">Selecteer in de resulterende lijst met resources Hallo Hallo netwerkbeveiligingsgroep (hello een met een pictogram schild) met dezelfde naam die u hebt gegeven toohello MongoDB virtuele machine; Hallo</span><span class="sxs-lookup"><span data-stu-id="e42c1-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="e42c1-201">Kies in de eigenschappen van Hallo 'inkomende beveiligingsregels';</span><span class="sxs-lookup"><span data-stu-id="e42c1-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="e42c1-202">Klik in het Hallo-werkbalk op "Toevoegen";</span><span class="sxs-lookup"><span data-stu-id="e42c1-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="e42c1-203">Geef een naam op zoals 'standaard-toestaan-mongo';</span><span class="sxs-lookup"><span data-stu-id="e42c1-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="e42c1-204">Hallo-protocol te instellen 'TCP';</span><span class="sxs-lookup"><span data-stu-id="e42c1-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="e42c1-205">Hallo doelpoortbereik ingesteld te '27017';</span><span class="sxs-lookup"><span data-stu-id="e42c1-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="e42c1-206">Klik op OK en wachten op Hallo beveiliging regel toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e42c1-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="e42c1-207">Sequentieel op Hallo TODO-toepassing</span><span class="sxs-lookup"><span data-stu-id="e42c1-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="e42c1-208">Tot nu toe hebben we twee virtuele Linux-machines ingericht: één die wordt uitgevoerd van de toepassing hello web frontend en één die MongoDB-exemplaar wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="e42c1-209">Maar er is een probleem - Hallo ingericht MongoDB-exemplaar is niet werkelijk nog gebruikmaakt van Hallo web frontend.</span><span class="sxs-lookup"><span data-stu-id="e42c1-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="e42c1-210">Laten we dit oplossen door Hallo web frontend code toouse bijwerken een omgevingsvariabele in plaats van een vastgelegde-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e42c1-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="e42c1-211">Hallo TODO toepassing wijzigen</span><span class="sxs-lookup"><span data-stu-id="e42c1-211">Changing hello TODO application</span></span>
<span data-ttu-id="e42c1-212">Open op uw ontwikkelcomputer waarop u eerst gekloond Hallo knooppunt todo-opslagplaats, Hallo `node-todo/config/database.js` -bestand in uw favoriete editor en Hallo url-waarde wijzigen van Hallo vastgelegde waarde zoals `mongodb://...` te`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="e42c1-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="e42c1-213">Uw wijzigingen en push toohello GitHub master:</span><span class="sxs-lookup"><span data-stu-id="e42c1-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="e42c1-214">Helaas publiceren niet dit Hallo wijzigen toohello frontend virtuele machine voor het web.</span><span class="sxs-lookup"><span data-stu-id="e42c1-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="e42c1-215">We maken een paar meer wijzigingen toothat virtuele machine tooenable een eenvoudige maar effectieve mechanisme voor het publiceren van updates, zodat u snel Hallo effect van wijzigingen in de productieomgeving Hallo Hallo kunt zien.</span><span class="sxs-lookup"><span data-stu-id="e42c1-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="e42c1-216">Hallo Web Frontend virtuele Machine configureren</span><span class="sxs-lookup"><span data-stu-id="e42c1-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="e42c1-217">Intrekken dat we eerder een bare kloon van Hallo knooppunt todo-opslagplaats op Hallo web frontend virtuele machine gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e42c1-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="e42c1-218">Het blijkt dat deze actie gemaakt met een nieuwe Git remote toowhich wijzigingen kunnen worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="e42c1-219">Eenvoudig pushen toothis externe geeft niet erg echter Hallo snelle herhaling model dat ontwikkelaars zoekt werkte op hun code.</span><span class="sxs-lookup"><span data-stu-id="e42c1-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="e42c1-220">Wat we wilt kunnen toodo toobe is ervoor Hallo actieve TODO-toepassing wordt automatisch bijgewerkt wanneer er een push toohello externe opslagplaats op Hallo virtuele machine optreedt, is.</span><span class="sxs-lookup"><span data-stu-id="e42c1-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="e42c1-221">Dit is gelukkig eenvoudig tooachieve met git.</span><span class="sxs-lookup"><span data-stu-id="e42c1-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="e42c1-222">GIT wordt een aantal hooks die worden aangeroepen op bepaalde tijden tooreact tooactions die zijn gemaakt op Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e42c1-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="e42c1-223">Deze worden opgegeven met behulp van de shell-scripts in Hallo-opslagplaats `hooks` map.</span><span class="sxs-lookup"><span data-stu-id="e42c1-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="e42c1-224">Hallo haakje dat meest van toepassing is voor automatische updates-scenario Hallo Hallo is `post-update` gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="e42c1-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="e42c1-225">Wijzig in een SSH-sessie toohello web frontend virtuele machine, toohello `~/node-todo.git/hooks` directory en toe te voegen inhoud tooa-bestand met de naam na Hallo `post-update` (vervangen `machinename` en `region` met uw gegevens van de virtuele machine MongoDB):</span><span class="sxs-lookup"><span data-stu-id="e42c1-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="e42c1-226">Zorg ervoor dat dit bestand door het uitvoeren van de volgende opdracht Hallo uitvoerbare bestand is:</span><span class="sxs-lookup"><span data-stu-id="e42c1-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="e42c1-227">Dit script zorgt ervoor dat de huidige server-toepassing hello is gestopt, Hallo-code in de gekloonde opslagplaats Hallo bijgewerkte toohello nieuwste is, eventuele bijgewerkte afhankelijkheden is voldaan en Hallo-server opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="e42c1-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="e42c1-228">Dit zorgt er ook voor dat die Hallo-omgeving is geconfigureerd als voorbereiding voor het ontvangen van onze eerste toepassing update tooget hello MongoDB-exemplaar van een omgevingsvariabele.</span><span class="sxs-lookup"><span data-stu-id="e42c1-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="e42c1-229">Configureren van uw ontwikkelcomputer</span><span class="sxs-lookup"><span data-stu-id="e42c1-229">Configuring your Development Machine</span></span>
<span data-ttu-id="e42c1-230">Nu gaan we aan uw ontwikkelcomputer aangesloten toohello web frontend virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e42c1-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="e42c1-231">Dit is net zo eenvoudig als het Hallo bare-opslagplaats op Hallo virtuele machine als een externe toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e42c1-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="e42c1-232">Hallo na toodo opdracht uitvoeren (vervangen *gebruiker* met de naam van de virtuele machine aanmelding voor uw web-frontend en *machinename* en *regio* indien nodig):</span><span class="sxs-lookup"><span data-stu-id="e42c1-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="e42c1-233">Dit is alles wat nodig tooenable pushen of publiceren van kracht is, verandert de toohello web frontend virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e42c1-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="e42c1-234">Publicatie-Updates</span><span class="sxs-lookup"><span data-stu-id="e42c1-234">Publishing Updates</span></span>
<span data-ttu-id="e42c1-235">We gaan publiceren Hallo een wijziging die tot nu toe is gemaakt zodat deze toepassing hello ons eigen MongoDB-exemplaar wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="e42c1-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="e42c1-236">Hier ziet u uitvoer vergelijkbare toothis:</span><span class="sxs-lookup"><span data-stu-id="e42c1-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
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
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="e42c1-237">Nadat u deze opdracht is voltooid, kunt u Vernieuw Hallo-toepassing in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e42c1-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="e42c1-238">U moet kunnen toosee dat Hallo takenlijsten die hier wordt gepresenteerd leeg is en niet langer gebonden toohello gedeeld geïmplementeerd MongoDB-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e42c1-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="e42c1-239">toocomplete hello zelfstudie gaan we een andere, meer zichtbare wijziging aanbrengt.</span><span class="sxs-lookup"><span data-stu-id="e42c1-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="e42c1-240">Open op uw ontwikkelcomputer Hallo node-todo/public/index.html bestand met behulp van uw favoriete editor.</span><span class="sxs-lookup"><span data-stu-id="e42c1-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="e42c1-241">Zoek Hallo jumbotron header en Hallo titel van het 'Ik ben een Todo-aholic' te 'Ik ben een Todo-aholic op Azure!' wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e42c1-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="e42c1-242">Nu gaan we doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="e42c1-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="e42c1-243">Deze tijd, gaan we Hallo wijziging tooAzure publiceren voordat u deze GitHub-repo-tooback toohello:</span><span class="sxs-lookup"><span data-stu-id="e42c1-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="e42c1-244">Wanneer u deze opdracht is voltooid, ziet webpagina Hallo vernieuwen en u Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="e42c1-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="e42c1-245">Omdat ze goed, push Hallo wijziging back toohello oorsprong externe:</span><span class="sxs-lookup"><span data-stu-id="e42c1-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="e42c1-246">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e42c1-246">Next Steps</span></span>
<span data-ttu-id="e42c1-247">In dit artikel hebt u geleerd hoe tootake een Node.js-toepassing en implementeer het tooLinux virtuele machines in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e42c1-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="e42c1-248">toolearn meer informatie over virtuele Linux-machines in Azure, Zie [tooLinux inleiding op Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="e42c1-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="e42c1-249">Voor meer informatie over het toodevelop Node.js-toepassingen in Azure, Zie Hallo [Node.js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="e42c1-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

