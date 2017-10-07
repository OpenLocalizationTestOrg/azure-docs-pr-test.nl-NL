---
title: aaaSet van Apache Tomcat op een virtuele Linux-machine | Microsoft Docs
description: Meer informatie over hoe tooset van Apache Tomcat7 met behulp van Azure Virtual Machines waarop Linux wordt uitgevoerd.
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 45ecc89c-1cb0-4e80-8944-bd0d0bbedfdc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: ningk
ms.openlocfilehash: b837a73e91fcb25d5459d993a0e93ceef1a1fc8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-tomcat7-on-a-linux-virtual-machine-with-azure"></a><span data-ttu-id="30ad2-103">Tomcat7 instellen op een virtuele Linux-machine met Azure</span><span class="sxs-lookup"><span data-stu-id="30ad2-103">Set up Tomcat7 on a Linux virtual machine with Azure</span></span>
<span data-ttu-id="30ad2-104">Apache Tomcat (of gewoon Tomcat, ook voorheen ondersteuning Tomcat) is een open-source-webserver en de servlet-container die is ontwikkeld door Hallo Apache Software Foundation (AVP).</span><span class="sxs-lookup"><span data-stu-id="30ad2-104">Apache Tomcat (or simply Tomcat, also formerly called Jakarta Tomcat) is an open source web server and servlet container developed by hello Apache Software Foundation (ASF).</span></span> <span data-ttu-id="30ad2-105">Tomcat implementeert Hallo Java Servlet en Hallo Java Server Pages (JSP) specificaties van Sun Microsystems.</span><span class="sxs-lookup"><span data-stu-id="30ad2-105">Tomcat implements hello Java Servlet and hello JavaServer Pages (JSP) specifications from Sun Microsystems.</span></span> <span data-ttu-id="30ad2-106">Tomcat biedt een pure HTTP Java web server-omgeving in welke toorun Java-code.</span><span class="sxs-lookup"><span data-stu-id="30ad2-106">Tomcat provides a pure Java HTTP web server environment in which toorun Java code.</span></span> <span data-ttu-id="30ad2-107">In de eenvoudigste configuratie hello, Tomcat uitgevoerd in een proces één besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="30ad2-107">In hello simplest configuration, Tomcat runs in a single operating system process.</span></span> <span data-ttu-id="30ad2-108">Dit proces wordt uitgevoerd voor een virtuele Java-machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="30ad2-108">This process runs a Java virtual machine (JVM).</span></span> <span data-ttu-id="30ad2-109">Alle HTTP-aanvragen van een browser tooTomcat wordt verwerkt als een afzonderlijke thread in Hallo Tomcat-proces.</span><span class="sxs-lookup"><span data-stu-id="30ad2-109">Every HTTP request from a browser tooTomcat is processed as a separate thread in hello Tomcat process.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="30ad2-110">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Azure Resource Manager en classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="30ad2-110">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="30ad2-111">In dit artikel bevat informatie over hoe toouse Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="30ad2-111">This article covers how toouse hello classic deployment model.</span></span> <span data-ttu-id="30ad2-112">U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken.</span><span class="sxs-lookup"><span data-stu-id="30ad2-112">We recommend that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="30ad2-113">toouse een Resource Manager-sjabloon toodeploy een VM Ubuntu met Open JDK en Tomcat, Zie [in dit artikel](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span><span class="sxs-lookup"><span data-stu-id="30ad2-113">toouse a Resource Manager template toodeploy an Ubuntu VM with Open JDK and Tomcat, see [this article](https://azure.microsoft.com/documentation/templates/openjdk-tomcat-ubuntu-vm/).</span></span>

<span data-ttu-id="30ad2-114">In dit artikel leert u Tomcat7 installeren op een Linux-installatiekopie en deze implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="30ad2-114">In this article, you will install Tomcat7 on a Linux image and deploy it in Azure.</span></span>  

<span data-ttu-id="30ad2-115">U leert:</span><span class="sxs-lookup"><span data-stu-id="30ad2-115">You will learn:</span></span>  

* <span data-ttu-id="30ad2-116">Hoe toocreate een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="30ad2-116">How toocreate a virtual machine in Azure.</span></span>
* <span data-ttu-id="30ad2-117">Hoe hello tooprepare virtuele machine voor Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="30ad2-117">How tooprepare hello virtual machine for Tomcat7.</span></span>
* <span data-ttu-id="30ad2-118">Hoe tooinstall Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="30ad2-118">How tooinstall Tomcat7.</span></span>

<span data-ttu-id="30ad2-119">Ervan wordt uitgegaan dat u al een Azure-abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="30ad2-119">It is assumed that you already have an Azure subscription.</span></span>  <span data-ttu-id="30ad2-120">Als u niet, u kunt zich aanmelden voor een gratis proefversie op [hello Azure-website](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="30ad2-120">If not, you can sign up for a free trial at [hello Azure website](https://azure.microsoft.com/).</span></span> <span data-ttu-id="30ad2-121">Als u een MSDN-abonnement hebt, raadpleegt u [speciale prijzen voor Microsoft Azure: MSDN, MPN en BizSpark voordelen](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span><span class="sxs-lookup"><span data-stu-id="30ad2-121">If you have an MSDN subscription, see [Microsoft Azure Special Pricing: MSDN, MPN, and BizSpark Benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/?c=14-39).</span></span> <span data-ttu-id="30ad2-122">toolearn meer informatie over Azure, Zie [wat is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span><span class="sxs-lookup"><span data-stu-id="30ad2-122">toolearn more about Azure, see [What is Azure?](https://azure.microsoft.com/overview/what-is-azure/).</span></span>

<span data-ttu-id="30ad2-123">In dit artikel wordt ervan uitgegaan dat u een werkende basiskennis hebben van Tomcat- en Linux.</span><span class="sxs-lookup"><span data-stu-id="30ad2-123">This article assumes that you have a basic working knowledge of Tomcat and Linux.</span></span>  

## <a name="phase-1-create-an-image"></a><span data-ttu-id="30ad2-124">Fase 1: Een installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="30ad2-124">Phase 1: Create an image</span></span>
<span data-ttu-id="30ad2-125">In deze fase maakt u een virtuele machine met behulp van een Linux-installatiekopie in Azure.</span><span class="sxs-lookup"><span data-stu-id="30ad2-125">In this phase, you will create a virtual machine by using a Linux image in Azure.</span></span>  

### <a name="step-1-generate-an-ssh-authentication-key"></a><span data-ttu-id="30ad2-126">Stap 1: Een SSH-sleutel voor verificatie genereren</span><span class="sxs-lookup"><span data-stu-id="30ad2-126">Step 1: Generate an SSH authentication key</span></span>
<span data-ttu-id="30ad2-127">SSH is een belangrijk hulpprogramma voor systeembeheerders.</span><span class="sxs-lookup"><span data-stu-id="30ad2-127">SSH is an important tool for system administrators.</span></span> <span data-ttu-id="30ad2-128">Configureren van de toegangsbeveiliging op basis van een wachtwoord human bepaald wordt echter niet aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-128">However, configuring access security based on a human-determined password is not recommended.</span></span> <span data-ttu-id="30ad2-129">Kwaadwillende gebruikers kunnen in uw systeem op basis van een gebruikersnaam en een zwak wachtwoord verbreken.</span><span class="sxs-lookup"><span data-stu-id="30ad2-129">Malicious users can break into your system based on a username and a weak password.</span></span>

<span data-ttu-id="30ad2-130">goed nieuws Hello, is er een manier tooleave RAS openen en u geen zorgen over wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="30ad2-130">hello good news is that there is a way tooleave remote access open and not worry about passwords.</span></span> <span data-ttu-id="30ad2-131">Deze methode bestaat van verificatie met asymmetrische cryptografie.</span><span class="sxs-lookup"><span data-stu-id="30ad2-131">This method consists of authentication with asymmetric cryptography.</span></span> <span data-ttu-id="30ad2-132">Hallo is persoonlijke sleutel van de gebruiker Hallo die Hallo-verificatie verleent.</span><span class="sxs-lookup"><span data-stu-id="30ad2-132">hello user’s private key is hello one that grants hello authentication.</span></span> <span data-ttu-id="30ad2-133">U kunt zelfs Hallo gebruikersaccount vergrendelen toonot wachtwoord authenticatie toestaan.</span><span class="sxs-lookup"><span data-stu-id="30ad2-133">You can even lock hello user’s account toonot allow password authentication.</span></span>

<span data-ttu-id="30ad2-134">Een ander voordeel van deze methode is dat u niet verschillende wachtwoorden toosign in toodifferent servers hoeft.</span><span class="sxs-lookup"><span data-stu-id="30ad2-134">Another advantage of this method is that you do not need different passwords toosign in toodifferent servers.</span></span> <span data-ttu-id="30ad2-135">U kunt verifiëren met behulp van Hallo persoonlijke persoonlijke sleutel op alle servers, waarmee wordt voorkomen dat u tooremember met verschillende wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="30ad2-135">You can authenticate by using hello personal private key on all servers, which prevents you from having tooremember several passwords.</span></span>



<span data-ttu-id="30ad2-136">Volg deze stappen toogenerate Hallo SSH-verificatiesleutel.</span><span class="sxs-lookup"><span data-stu-id="30ad2-136">Follow these steps toogenerate hello SSH authentication key.</span></span>

1. <span data-ttu-id="30ad2-137">Download en installeer PuTTYgen van Hallo volgende locatie: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span><span class="sxs-lookup"><span data-stu-id="30ad2-137">Download and install PuTTYgen from hello following location: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)</span></span>
2. <span data-ttu-id="30ad2-138">Puttygen.exe worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="30ad2-138">Run Puttygen.exe.</span></span>
3. <span data-ttu-id="30ad2-139">Klik op **genereren** toogenerate Hallo sleutels.</span><span class="sxs-lookup"><span data-stu-id="30ad2-139">Click **Generate** toogenerate hello keys.</span></span> <span data-ttu-id="30ad2-140">U kunt in Hallo-proces aanvraaggrootte vergroten door bewegende Hallo muis over Hallo leeg gebied in Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="30ad2-140">In hello process, you can increase randomness by moving hello mouse over hello blank area in hello window.</span></span>  
   <span data-ttu-id="30ad2-141">![PuTTY sleutel Generator schermafbeelding Hallo nieuwe sleutel knop genereren][1]</span><span class="sxs-lookup"><span data-stu-id="30ad2-141">![PuTTY Key Generator screenshot that shows hello generate new key button][1]</span></span>
4. <span data-ttu-id="30ad2-142">Nadat het Hallo proces genereren, wordt Puttygen.exe uw nieuwe openbare sleutel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="30ad2-142">After hello generate process, Puttygen.exe will show your new public key.</span></span>  
   ![PuTTY sleutel Generator schermafbeelding van de nieuwe openbare sleutel Hallo en Hallo persoonlijke sleutel knop Opslaan][2]
5. <span data-ttu-id="30ad2-144">Selecteer en kopieer de openbare sleutel Hallo en opslaan in een bestand met de naam publicKey.pem.</span><span class="sxs-lookup"><span data-stu-id="30ad2-144">Select and copy hello public key, and save it in a file named publicKey.pem.</span></span> <span data-ttu-id="30ad2-145">Klik niet op **openbare sleutel opslaan**, omdat Hallo opgeslagen bestandsindeling van de openbare sleutel verschilt van de openbare sleutel Hallo we willen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-145">Don’t click **Save public key**, because hello saved public key’s file format is different from hello public key we want.</span></span>
6. <span data-ttu-id="30ad2-146">Klik op **persoonlijke sleutel opslaan**, en opslaan in een bestand met de naam privateKey.ppk.</span><span class="sxs-lookup"><span data-stu-id="30ad2-146">Click **Save private key**, and save it in a file named privateKey.ppk.</span></span>

### <a name="step-2-create-hello-image-in-hello-azure-portal"></a><span data-ttu-id="30ad2-147">Stap 2: Maak Hallo afbeelding in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="30ad2-147">Step 2: Create hello image in hello Azure portal</span></span>
1. <span data-ttu-id="30ad2-148">In Hallo [portal](https://portal.azure.com/), klikt u op **nieuw** in Hallo taak balk toocreate een afbeelding.</span><span class="sxs-lookup"><span data-stu-id="30ad2-148">In hello [portal](https://portal.azure.com/), click **New** in hello task bar toocreate an image.</span></span> <span data-ttu-id="30ad2-149">Kies vervolgens Hallo Linux installatiekopie die is gebaseerd op uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="30ad2-149">Then choose hello Linux image that is based on your needs.</span></span> <span data-ttu-id="30ad2-150">Hallo wordt volgende voorbeeld Hallo Ubuntu 14.04 installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="30ad2-150">hello following example uses hello Ubuntu 14.04 image.</span></span>
<span data-ttu-id="30ad2-151">![Schermopname van het Hallo-portal die ziet u de nieuwe knop Hallo][3]</span><span class="sxs-lookup"><span data-stu-id="30ad2-151">![Screenshot of hello portal that shows hello New button][3]</span></span>

2. <span data-ttu-id="30ad2-152">Voor **hostnaam**, geef de naam Hallo voor Hallo URL dat u en Internet-clients tooaccess deze virtuele machine gebruiken.</span><span class="sxs-lookup"><span data-stu-id="30ad2-152">For **Host Name**, specify hello name for hello URL that you and Internet clients will use tooaccess this virtual machine.</span></span> <span data-ttu-id="30ad2-153">Hallo laatste deel van Hallo DNS-naam, bijvoorbeeld tomcatdemo definiëren.</span><span class="sxs-lookup"><span data-stu-id="30ad2-153">Define hello last part of hello DNS name, for example, tomcatdemo.</span></span> <span data-ttu-id="30ad2-154">Azure wordt Hallo URL vervolgens als tomcatdemo.cloudapp.net gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="30ad2-154">Azure will then generate hello URL as tomcatdemo.cloudapp.net.</span></span>  

3. <span data-ttu-id="30ad2-155">Voor **SSH verificatiesleutel**, Hallo sleutelwaarde van Hallo publicKey.pem bestand de openbare sleutel Hallo gegenereerd door PuTTYgen bevat kopiëren.</span><span class="sxs-lookup"><span data-stu-id="30ad2-155">For **SSH Authentication Key**, copy hello key value from hello publicKey.pem file, which contains hello public key generated by PuTTYgen.</span></span>  
<span data-ttu-id="30ad2-156">![Sleutel voor SSH-gebruikersverificatie vak Hallo-portal][4]</span><span class="sxs-lookup"><span data-stu-id="30ad2-156">![SSH Authentication Key box in hello portal][4]</span></span>

4. <span data-ttu-id="30ad2-157">Andere instellingen naar wens configureren en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-157">Configure other settings as needed, and then click **Create**.</span></span>  

## <a name="phase-2-prepare-your-virtual-machine-for-tomcat7"></a><span data-ttu-id="30ad2-158">Fase 2: Uw virtuele machine voorbereiden voor Tomcat7</span><span class="sxs-lookup"><span data-stu-id="30ad2-158">Phase 2: Prepare your virtual machine for Tomcat7</span></span>
<span data-ttu-id="30ad2-159">In deze fase wordt u een eindpunt voor Tomcat verkeer configureren en vervolgens verbinding tooyour nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="30ad2-159">In this phase, you will configure an endpoint for Tomcat traffic, and then connect tooyour new virtual machine.</span></span>

### <a name="step-1-open-hello-http-port-tooallow-web-access"></a><span data-ttu-id="30ad2-160">Stap 1: Open Hallo HTTP-poort tooallow-webtoegang</span><span class="sxs-lookup"><span data-stu-id="30ad2-160">Step 1: Open hello HTTP port tooallow web access</span></span>
<span data-ttu-id="30ad2-161">Eindpunten in Azure bestaan uit een protocol TCP of UDP, samen met een openbare en particuliere poort.</span><span class="sxs-lookup"><span data-stu-id="30ad2-161">Endpoints in Azure consist of a TCP or UDP protocol, along with a public and private port.</span></span> <span data-ttu-id="30ad2-162">Hallo is persoonlijke Hallo poort Hallo service luistert tooon Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="30ad2-162">hello private port is hello port that hello service is listening tooon hello virtual machine.</span></span> <span data-ttu-id="30ad2-163">Hallo openbare poort is Hallo-poort die hello Azure cloudservice luistert tooexternally voor binnenkomend verkeer op basis van het Internet.</span><span class="sxs-lookup"><span data-stu-id="30ad2-163">hello public port is hello port that hello Azure cloud service listens tooexternally for incoming, Internet-based traffic.</span></span>  

<span data-ttu-id="30ad2-164">TCP-poort 8080 is Hallo standaardpoortnummer dat Tomcat toolisten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="30ad2-164">TCP port 8080 is hello default port number that Tomcat uses toolisten.</span></span> <span data-ttu-id="30ad2-165">Als deze poort wordt geopend met een Azure-eindpunt, u en andere internetclients hebben toegang tot Tomcat-pagina's.</span><span class="sxs-lookup"><span data-stu-id="30ad2-165">If this port is opened with an Azure endpoint, you and other Internet clients can access Tomcat pages.</span></span>  

1. <span data-ttu-id="30ad2-166">Klik in de portal Hallo op **Bladeren** > **virtuele machines**, en klik vervolgens op Hallo virtuele machine die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="30ad2-166">In hello portal, click **Browse** > **Virtual machines**, and then click hello virtual machine that you created.</span></span>  
   <span data-ttu-id="30ad2-167">![Schermafbeelding van de map van de virtuele machines Hallo][5]</span><span class="sxs-lookup"><span data-stu-id="30ad2-167">![Screenshot of hello Virtual machines directory][5]</span></span>
2. <span data-ttu-id="30ad2-168">tooadd een eindpunt tooyour virtuele machine, klikt u op Hallo **eindpunten** vak.</span><span class="sxs-lookup"><span data-stu-id="30ad2-168">tooadd an endpoint tooyour virtual machine, click hello **Endpoints** box.</span></span>
   <span data-ttu-id="30ad2-169">![Schermafbeelding van Hallo eindpunten vak][6]</span><span class="sxs-lookup"><span data-stu-id="30ad2-169">![Screenshot that shows hello Endpoints box][6]</span></span>
3. <span data-ttu-id="30ad2-170">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-170">Click **Add**.</span></span>  

   1. <span data-ttu-id="30ad2-171">Voor het Hallo-eindpunt, voer een naam voor Hallo eindpunt in **eindpunt**, en voer dan 80 in **openbare poort**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-171">For hello endpoint, enter a name for hello endpoint in **Endpoint**, and then enter 80 in **Public Port**.</span></span>  

      <span data-ttu-id="30ad2-172">Als u deze too80 instellen, hoeft u geen tooinclude Hallo poortnummer in Hallo-URL die is gebruikt tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="30ad2-172">If you set it too80, you don’t need tooinclude hello port number in hello URL that is used tooaccess Tomcat.</span></span> <span data-ttu-id="30ad2-173">Bijvoorbeeld: http://tomcatdemo.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="30ad2-173">For example, http://tomcatdemo.cloudapp.net.</span></span>    

      <span data-ttu-id="30ad2-174">Als u instellen dat deze tooanother waarde, zoals 81, moet u tooadd Hallo poort nummer toohello URL tooaccess Tomcat.</span><span class="sxs-lookup"><span data-stu-id="30ad2-174">If you set it tooanother value, such as 81, you need tooadd hello port number toohello URL tooaccess Tomcat.</span></span> <span data-ttu-id="30ad2-175">Bijvoorbeeld: http://tomcatdemo.cloudapp.net:81 /.</span><span class="sxs-lookup"><span data-stu-id="30ad2-175">For example,  http://tomcatdemo.cloudapp.net:81/.</span></span>
   2. <span data-ttu-id="30ad2-176">Voer 8080 in **particuliere poort**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-176">Enter 8080 in **Private Port**.</span></span> <span data-ttu-id="30ad2-177">Standaard luistert Tomcat op TCP-poort 8080.</span><span class="sxs-lookup"><span data-stu-id="30ad2-177">By default, Tomcat listens on TCP port 8080.</span></span> <span data-ttu-id="30ad2-178">Als u Hallo standaard listen-poort Tomcat hebt gewijzigd, moet u bijwerken **particuliere poort** toobe Hallo hetzelfde als het Hallo Tomcat listen-poort.</span><span class="sxs-lookup"><span data-stu-id="30ad2-178">If you changed hello default listen port of Tomcat, you should update **Private Port** toobe hello same as hello Tomcat listen port.</span></span>  
      <span data-ttu-id="30ad2-179">![Schermopname van gebruikersinterface waarin de opdracht, de openbare poort en het particuliere poort toevoegen][7]</span><span class="sxs-lookup"><span data-stu-id="30ad2-179">![Screenshot of UI that shows Add command, Public Port, and Private Port][7]</span></span>
4. <span data-ttu-id="30ad2-180">Klik op **OK** tooadd Hallo eindpunt tooyour virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="30ad2-180">Click **OK** tooadd hello endpoint tooyour virtual machine.</span></span>

### <a name="step-2-connect-toohello-image-you-created"></a><span data-ttu-id="30ad2-181">Stap 2: Verbinding maken met toohello-installatiekopie die u hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="30ad2-181">Step 2: Connect toohello image you created</span></span>
<span data-ttu-id="30ad2-182">U kunt een SSH-hulpprogramma tooconnect tooyour virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="30ad2-182">You can choose any SSH tool tooconnect tooyour virtual machine.</span></span> <span data-ttu-id="30ad2-183">In dit voorbeeld gebruiken we PuTTY.</span><span class="sxs-lookup"><span data-stu-id="30ad2-183">In this example, we use PuTTY.</span></span>  

1. <span data-ttu-id="30ad2-184">Hallo DNS-naam van uw virtuele machine ophalen van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="30ad2-184">Get hello DNS name of your virtual machine from hello portal.</span></span>
    1. <span data-ttu-id="30ad2-185">Klik op **Bladeren** > **virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-185">Click **Browse** > **Virtual machines**.</span></span>
    2. <span data-ttu-id="30ad2-186">Hallo-naam van uw virtuele machine selecteren en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-186">Select hello name of your virtual machine, and then click **Properties**.</span></span>
    3. <span data-ttu-id="30ad2-187">In Hallo **eigenschappen** tegel, kijkt u in Hallo **domeinnaam** tooget Hallo DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="30ad2-187">In hello **Properties** tile, look in hello **Domain Name** box tooget hello DNS name.</span></span>  

2. <span data-ttu-id="30ad2-188">Hallo-poortnummer voor SSH-verbindingen van Hallo ophalen **SSH** vak.</span><span class="sxs-lookup"><span data-stu-id="30ad2-188">Get hello port number for SSH connections from hello **SSH** box.</span></span>  
<span data-ttu-id="30ad2-189">![Schermafbeelding van Hallo SSH-verbinding-poortnummer][8]</span><span class="sxs-lookup"><span data-stu-id="30ad2-189">![Screenshot that shows hello SSH connection port number][8]</span></span>

3. <span data-ttu-id="30ad2-190">Download [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="30ad2-190">Download [PuTTY](http://www.putty.org/).</span></span>  

4. <span data-ttu-id="30ad2-191">Nadat u hebt gedownload, klikt u op Hallo uitvoerbaar bestand Putty.exe.</span><span class="sxs-lookup"><span data-stu-id="30ad2-191">After downloading, click hello executable file Putty.exe.</span></span> <span data-ttu-id="30ad2-192">In de PuTTY-configuratie, Hallo basisopties configureren met de hostnaam Hallo en het poortnummer dat is verkregen van Hallo eigenschappen van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="30ad2-192">In PuTTY configuration, configure hello basic options with hello host name and port number that is obtained from hello properties of your virtual machine.</span></span>   
![Schermafbeelding van Hallo PuTTY-configuratie host naam en het poortnummer opties][9]

5. <span data-ttu-id="30ad2-194">Klik in het linkerdeelvenster Hallo **verbinding** > **SSH** > **Auth**, en klik vervolgens op **Bladeren** toospecify Hallo-locatie van Hallo privateKey.ppk bestand.</span><span class="sxs-lookup"><span data-stu-id="30ad2-194">In hello left pane, click **Connection** > **SSH** > **Auth**, and then click **Browse** toospecify hello location of hello privateKey.ppk file.</span></span> <span data-ttu-id="30ad2-195">Hallo privateKey.ppk bestand bevat Hallo persoonlijke sleutel die wordt gegenereerd door PuTTYgen eerder in Hallo ' stap 1: een installatiekopie maken ' sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="30ad2-195">hello privateKey.ppk file contains hello private key that is generated by PuTTYgen earlier in hello "Phase 1: Create an image" section of this article.</span></span>  
<span data-ttu-id="30ad2-196">![Schermafbeelding van Hallo verbinding directory-hiërarchie en de knop Bladeren][10]</span><span class="sxs-lookup"><span data-stu-id="30ad2-196">![Screenshot that shows hello Connection directory hierarchy and Browse button][10]</span></span>

6. <span data-ttu-id="30ad2-197">Klik op **Open**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-197">Click **Open**.</span></span> <span data-ttu-id="30ad2-198">U wordt mogelijk door een berichtvenster gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="30ad2-198">You might be alerted by a message box.</span></span> <span data-ttu-id="30ad2-199">Als u hebt geconfigureerd Hallo DNS-naam en het poortnummer juist, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="30ad2-199">If you have configured hello DNS name and port number correctly, click **Yes**.</span></span>
<span data-ttu-id="30ad2-200">![Schermafbeelding van Hallo-melding][11]</span><span class="sxs-lookup"><span data-stu-id="30ad2-200">![Screenshot that shows hello notification][11]</span></span>

7. <span data-ttu-id="30ad2-201">U na vragen aan gebruiker tooenter zijn uw gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="30ad2-201">You are prompted tooenter your username.</span></span>  
![Schermopname die laat waar zien tooenter gebruikersnaam][12]

8. <span data-ttu-id="30ad2-203">Hallo-gebruikersnaam die u hebt toocreate Hallo virtuele machine in Hallo gebruikt invoeren ' stap 1: een installatiekopie maken '-rubriek eerder in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="30ad2-203">Enter hello username that you used toocreate hello virtual machine in hello "Phase 1: Create an image" section earlier in this article.</span></span> <span data-ttu-id="30ad2-204">U ziet ongeveer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="30ad2-204">You will see something like hello following:</span></span>  
![Schermafbeelding van Hallo verificatie bevestigen][13]

## <a name="phase-3-install-software"></a><span data-ttu-id="30ad2-206">Fase 3: Installeren van software</span><span class="sxs-lookup"><span data-stu-id="30ad2-206">Phase 3: Install software</span></span>
<span data-ttu-id="30ad2-207">In deze fase installeert u Hallo Java runtime environment, Tomcat7 en andere onderdelen Tomcat7.</span><span class="sxs-lookup"><span data-stu-id="30ad2-207">In this phase, you install hello Java runtime environment, Tomcat7, and other Tomcat7 components.</span></span>  

### <a name="java-runtime-environment"></a><span data-ttu-id="30ad2-208">Java runtime-omgeving</span><span class="sxs-lookup"><span data-stu-id="30ad2-208">Java runtime environment</span></span>
<span data-ttu-id="30ad2-209">Tomcat is geschreven in Java.</span><span class="sxs-lookup"><span data-stu-id="30ad2-209">Tomcat is written in Java.</span></span> <span data-ttu-id="30ad2-210">Er zijn twee soorten Java Development Kit (JDKs), OpenJDK en Oracle JDK.</span><span class="sxs-lookup"><span data-stu-id="30ad2-210">There are two kinds of Java Development Kits (JDKs), OpenJDK and Oracle JDK.</span></span> <span data-ttu-id="30ad2-211">U kunt Hallo gewenste.</span><span class="sxs-lookup"><span data-stu-id="30ad2-211">You can choose hello one you want.</span></span>  

> [!NOTE]
> <span data-ttu-id="30ad2-212">Beide JDKs bijna Hallo dezelfde voor Hallo klassen in Hallo Java API-code hebben, maar Hallo code voor de virtuele machine van Hallo verschilt.</span><span class="sxs-lookup"><span data-stu-id="30ad2-212">Both JDKs have almost hello same code for hello classes in hello Java API, but hello code for hello virtual machine is different.</span></span> <span data-ttu-id="30ad2-213">OpenJDK doorgaans toouse open bibliotheken, terwijl Oracle JDK doorgaans toouse zijn gesloten.</span><span class="sxs-lookup"><span data-stu-id="30ad2-213">OpenJDK tends toouse open libraries, while Oracle JDK tends toouse closed ones.</span></span> <span data-ttu-id="30ad2-214">Oracle JDK heeft meer klassen en enkele fouten opgelost en Oracle JDK stabieler dan OpenJDK is.</span><span class="sxs-lookup"><span data-stu-id="30ad2-214">Oracle JDK has more classes and some fixed bugs, and Oracle JDK is more stable than OpenJDK.</span></span>

#### <a name="install-openjdk"></a><span data-ttu-id="30ad2-215">OpenJDK installeren</span><span class="sxs-lookup"><span data-stu-id="30ad2-215">Install OpenJDK</span></span>  

<span data-ttu-id="30ad2-216">Gebruik hello opdracht toodownload OpenJDK te volgen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-216">Use hello following command toodownload OpenJDK.</span></span>   

    sudo apt-get update  
    sudo apt-get install openjdk-7-jre  


* <span data-ttu-id="30ad2-217">een directory toocontain toocreate Hallo JDK-bestanden:</span><span class="sxs-lookup"><span data-stu-id="30ad2-217">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="30ad2-218">tooextract hello JDK bestanden naar Hallo/usr/lib/jvm/map:</span><span class="sxs-lookup"><span data-stu-id="30ad2-218">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/

#### <a name="install-oracle-jdk"></a><span data-ttu-id="30ad2-219">Oracle JDK installeren</span><span class="sxs-lookup"><span data-stu-id="30ad2-219">Install Oracle JDK</span></span>


<span data-ttu-id="30ad2-220">Hallo volgende opdracht toodownload Oracle JDK uit Hallo Oracle-website gebruiken.</span><span class="sxs-lookup"><span data-stu-id="30ad2-220">Use hello following command toodownload Oracle JDK from hello Oracle website.</span></span>  

     wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz  
* <span data-ttu-id="30ad2-221">een directory toocontain toocreate Hallo JDK-bestanden:</span><span class="sxs-lookup"><span data-stu-id="30ad2-221">toocreate a directory toocontain hello JDK files:</span></span>  

        sudo mkdir /usr/lib/jvm  
* <span data-ttu-id="30ad2-222">tooextract hello JDK bestanden naar Hallo/usr/lib/jvm/map:</span><span class="sxs-lookup"><span data-stu-id="30ad2-222">tooextract hello JDK files into hello /usr/lib/jvm/ directory:</span></span>  

        sudo tar -zxf jdk-8u5-linux-x64.tar.gz  -C /usr/lib/jvm/  
* <span data-ttu-id="30ad2-223">tooset Oracle JDK als de standaard virtuele Java-machine Hallo:</span><span class="sxs-lookup"><span data-stu-id="30ad2-223">tooset Oracle JDK as hello default Java virtual machine:</span></span>  

        sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_05/bin/java 100  

        sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_05/bin/javac 100  

#### <a name="confirm-that-java-installation-is-successful"></a><span data-ttu-id="30ad2-224">Bevestig dat de Java-installatie geslaagd is</span><span class="sxs-lookup"><span data-stu-id="30ad2-224">Confirm that Java installation is successful</span></span>
<span data-ttu-id="30ad2-225">U kunt een opdracht zoals Hallo tootest volgen als Hallo Java runtime environment juist is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="30ad2-225">You can use a command like hello following tootest if hello Java runtime environment is installed correctly:</span></span>  

    java -version  

<span data-ttu-id="30ad2-226">Als u OpenJDK hebt geïnstalleerd, ziet u een bericht zoals volgende Hallo: ![geslaagde OpenJDK installatie bericht][14]</span><span class="sxs-lookup"><span data-stu-id="30ad2-226">If you installed OpenJDK, you should see a message like hello following: ![Successful OpenJDK installation message][14]</span></span>

<span data-ttu-id="30ad2-227">Als u Oracle JDK hebt geïnstalleerd, ziet u een bericht zoals volgende Hallo: ![geslaagde Oracle JDK installatie bericht][15]</span><span class="sxs-lookup"><span data-stu-id="30ad2-227">If you installed Oracle JDK, you should see a message like hello following: ![Successful Oracle JDK installation message][15]</span></span>

### <a name="install-tomcat7"></a><span data-ttu-id="30ad2-228">Tomcat7 installeren</span><span class="sxs-lookup"><span data-stu-id="30ad2-228">Install Tomcat7</span></span>
<span data-ttu-id="30ad2-229">Gebruik hello opdracht tooinstall Tomcat7 te volgen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-229">Use hello following command tooinstall Tomcat7.</span></span>  

    sudo apt-get install tomcat7  

<span data-ttu-id="30ad2-230">Als u Tomcat7 niet gebruikt, gebruikt u de juiste variatie Hallo van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="30ad2-230">If you are not using Tomcat7, use hello appropriate variation of this command.</span></span>  

#### <a name="confirm-that-tomcat7-installation-is-successful"></a><span data-ttu-id="30ad2-231">Bevestig dat Tomcat7 installatie geslaagd is</span><span class="sxs-lookup"><span data-stu-id="30ad2-231">Confirm that Tomcat7 installation is successful</span></span>
<span data-ttu-id="30ad2-232">toocheck als Tomcat7 is geïnstalleerd, bladert u tooyour Tomcat-server van DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="30ad2-232">toocheck if Tomcat7 is successfully installed, browse tooyour Tomcat server’s DNS name.</span></span> <span data-ttu-id="30ad2-233">In dit artikel is Hallo voorbeeld-URL http://tomcatexample.cloudapp.net/.</span><span class="sxs-lookup"><span data-stu-id="30ad2-233">In this article, hello example URL is http://tomcatexample.cloudapp.net/.</span></span> <span data-ttu-id="30ad2-234">Als u een bericht zoals Hallo volgende ziet, is Tomcat7 juist geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="30ad2-234">If you see a message like hello following, Tomcat7 is installed correctly.</span></span>
<span data-ttu-id="30ad2-235">![Bericht Tomcat7 installatie is voltooid][16]</span><span class="sxs-lookup"><span data-stu-id="30ad2-235">![Successful Tomcat7 installation message][16]</span></span>

### <a name="install-other-tomcat7-components"></a><span data-ttu-id="30ad2-236">Andere onderdelen Tomcat7 installeren</span><span class="sxs-lookup"><span data-stu-id="30ad2-236">Install other Tomcat7 components</span></span>
<span data-ttu-id="30ad2-237">Er zijn andere optionele Tomcat-onderdelen die u kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="30ad2-237">There are other optional Tomcat components that you can install.</span></span>  

<span data-ttu-id="30ad2-238">Gebruik Hallo **sudo apt cache zoeken tomcat7** opdracht toosee alle beschikbare Hallo-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-238">Use hello **sudo apt-cache search tomcat7** command toosee all of hello available components.</span></span> <span data-ttu-id="30ad2-239">Hallo opdrachten tooinstall volgen enkele nuttige onderdelen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="30ad2-239">Use hello following commands tooinstall some useful components.</span></span>  

    sudo apt-get install tomcat7-admin      #admin web applications

    sudo apt-get install tomcat7-user         #tools toocreate user instances  

## <a name="phase-4-configure-tomcat7"></a><span data-ttu-id="30ad2-240">Fase 4: Tomcat7 configureren</span><span class="sxs-lookup"><span data-stu-id="30ad2-240">Phase 4: Configure Tomcat7</span></span>
<span data-ttu-id="30ad2-241">In deze fase, moet u Tomcat beheren.</span><span class="sxs-lookup"><span data-stu-id="30ad2-241">In this phase, you administer Tomcat.</span></span>

### <a name="start-and-stop-tomcat7"></a><span data-ttu-id="30ad2-242">Starten en stoppen Tomcat7</span><span class="sxs-lookup"><span data-stu-id="30ad2-242">Start and stop Tomcat7</span></span>
<span data-ttu-id="30ad2-243">Hallo Tomcat7 server wordt automatisch gestart wanneer u deze installeert.</span><span class="sxs-lookup"><span data-stu-id="30ad2-243">hello Tomcat7 server automatically starts when you install it.</span></span> <span data-ttu-id="30ad2-244">U kunt deze ook starten met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="30ad2-244">You can also start it with hello following command:</span></span>   

    sudo /etc/init.d/tomcat7 start

<span data-ttu-id="30ad2-245">toostop Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="30ad2-245">toostop Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 stop

<span data-ttu-id="30ad2-246">status van de tooview Hallo van Tomcat7:</span><span class="sxs-lookup"><span data-stu-id="30ad2-246">tooview hello status of Tomcat7:</span></span>

    sudo /etc/init.d/tomcat7 status

<span data-ttu-id="30ad2-247">toorestart Tomcat-services:</span><span class="sxs-lookup"><span data-stu-id="30ad2-247">toorestart Tomcat services:</span></span> 

    sudo /etc/init.d/tomcat7 restart

### <a name="tomcat7-administration"></a><span data-ttu-id="30ad2-248">Tomcat7 beheer</span><span class="sxs-lookup"><span data-stu-id="30ad2-248">Tomcat7 administration</span></span>
<span data-ttu-id="30ad2-249">U kunt Hallo Tomcat gebruiker configuration file tooset bewerken van uw beheerdersreferenties.</span><span class="sxs-lookup"><span data-stu-id="30ad2-249">You can edit hello Tomcat user configuration file tooset up your admin credentials.</span></span> <span data-ttu-id="30ad2-250">Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="30ad2-250">Use hello following command:</span></span>  

    sudo vi  /etc/tomcat7/tomcat-users.xml   

<span data-ttu-id="30ad2-251">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="30ad2-251">Here is an example:</span></span>  
![Schermafbeelding van Hallo sudo vi opdrachtuitvoer][17]  

> [!NOTE]
> <span data-ttu-id="30ad2-253">Maak een sterk wachtwoord voor de gebruikersnaam van de Hallo beheerder.</span><span class="sxs-lookup"><span data-stu-id="30ad2-253">Create a strong password for hello admin username.</span></span>  

<span data-ttu-id="30ad2-254">Na het bewerken van dit bestand, moet u Tomcat7 services opnieuw starten met Hallo opdracht tooensure dat Hallo wijzigingen van kracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="30ad2-254">After editing this file, you should restart Tomcat7 services with hello following command tooensure that hello changes take effect:</span></span>  

    sudo /etc/init.d/tomcat7 restart  

<span data-ttu-id="30ad2-255">Open uw browser en voer **http://<your tomcat server DNS name>manager/html** zoals Hallo URL.</span><span class="sxs-lookup"><span data-stu-id="30ad2-255">Open your browser, and enter **http://<your tomcat server DNS name>/manager/html** as hello URL.</span></span> <span data-ttu-id="30ad2-256">Hallo-URL is bijvoorbeeld Hallo in dit artikel http://tomcatexample.cloudapp.net/manager/html.</span><span class="sxs-lookup"><span data-stu-id="30ad2-256">For hello example in this article, hello URL is http://tomcatexample.cloudapp.net/manager/html.</span></span>  

<span data-ttu-id="30ad2-257">Nadat u verbinding maakt ziet u iets dergelijks toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="30ad2-257">After connecting, you should see something similar toohello following:</span></span>  
![Schermopname van Hallo Tomcat Web Application Manager][18]

## <a name="common-issues"></a><span data-ttu-id="30ad2-259">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="30ad2-259">Common issues</span></span>
### <a name="cant-access-hello-virtual-machine-with-tomcat-and-moodle-from-hello-internet"></a><span data-ttu-id="30ad2-260">Geen toegang tot Hallo virtuele machine met Tomcat en Moodle vanaf Internet Hallo</span><span class="sxs-lookup"><span data-stu-id="30ad2-260">Can't access hello virtual machine with Tomcat and Moodle from hello Internet</span></span>
#### <a name="symptom"></a><span data-ttu-id="30ad2-261">Symptoom</span><span class="sxs-lookup"><span data-stu-id="30ad2-261">Symptom</span></span>  
  <span data-ttu-id="30ad2-262">Tomcat wordt uitgevoerd, maar u Hallo Tomcat standaardpagina met uw browser niet zien.</span><span class="sxs-lookup"><span data-stu-id="30ad2-262">Tomcat is running but you can’t see hello Tomcat default page with your browser.</span></span>
#### <a name="possible-root-cause"></a><span data-ttu-id="30ad2-263">Mogelijke hoofdoorzaken</span><span class="sxs-lookup"><span data-stu-id="30ad2-263">Possible root cause</span></span>   

  * <span data-ttu-id="30ad2-264">Hallo Tomcat listen-poort is niet hetzelfde als de particuliere poort van de virtuele machine-eindpunt voor Tomcat verkeer Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="30ad2-264">hello Tomcat listen port is not hello same as hello private port of your virtual machine's endpoint for Tomcat traffic.</span></span>  

     <span data-ttu-id="30ad2-265">Controleer uw openbare poort en de persoonlijke eindpunt poortinstellingen en zorg ervoor dat Hallo particuliere poort is hetzelfde als Tomcat Hallo Hallo poort luistert.</span><span class="sxs-lookup"><span data-stu-id="30ad2-265">Check your public port and private port endpoint settings and make sure hello private port is hello same as hello Tomcat listen port.</span></span> <span data-ttu-id="30ad2-266">Zie ' stap 1: een installatiekopie maken ' sectie van dit artikel voor instructies over het configureren van eindpunten voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="30ad2-266">See "Phase 1: Create an image" section of this article for instructions on configuring endpoints for your virtual machine.</span></span>  

     <span data-ttu-id="30ad2-267">toodetermine Hallo Tomcat poort luisteren, open /etc/httpd/conf/httpd.conf (Red Hat release) of /etc/tomcat7/server.xml (Debian-versie).</span><span class="sxs-lookup"><span data-stu-id="30ad2-267">toodetermine hello Tomcat listen port, open /etc/httpd/conf/httpd.conf (Red Hat release), or /etc/tomcat7/server.xml (Debian release).</span></span> <span data-ttu-id="30ad2-268">Standaard is Hallo Tomcat listen-poort 8080.</span><span class="sxs-lookup"><span data-stu-id="30ad2-268">By default, hello Tomcat listen port is 8080.</span></span> <span data-ttu-id="30ad2-269">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="30ad2-269">Here is an example:</span></span>  

        <Connector port="8080" protocol="HTTP/1.1"  connectionTimeout="20000"   URIEncoding="UTF-8"            redirectPort="8443" />  

     <span data-ttu-id="30ad2-270">Als u een virtuele machine zoals Debian of Ubuntu en u wilt dat toochange Hallo standaard poort van Tomcat luisteren (bijvoorbeeld 8081) gebruikt, moet u ook Hallo-poort voor het besturingssysteem Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-270">If you are using a virtual machine like Debian or Ubuntu and you want toochange hello default port of Tomcat Listen (for example 8081), you should also open hello port for hello operating system.</span></span> <span data-ttu-id="30ad2-271">Open eerst Hallo-profiel:</span><span class="sxs-lookup"><span data-stu-id="30ad2-271">First, open hello profile:</span></span>  

        sudo vi /etc/default/tomcat7  

     <span data-ttu-id="30ad2-272">Vervolgens Opmerkingen bij de laatste regel Hallo en wijzigt u 'Nee' te 'Ja'.</span><span class="sxs-lookup"><span data-stu-id="30ad2-272">Then uncomment hello last line and change “no” too“yes”.</span></span>  

        AUTHBIND=yes
  2. <span data-ttu-id="30ad2-273">Hallo-firewall is uitgeschakeld door Hallo listen-poort van Tomcat.</span><span class="sxs-lookup"><span data-stu-id="30ad2-273">hello firewall has disabled hello listen port of Tomcat.</span></span>

     <span data-ttu-id="30ad2-274">U kunt alleen Hallo Tomcat standaardpagina van de lokale host Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="30ad2-274">You can only see hello Tomcat default page from hello local host.</span></span> <span data-ttu-id="30ad2-275">Hallo-probleem is waarschijnlijk dat Hallo-poort geluisterd tooby Tomcat is, door Hallo-firewall is geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="30ad2-275">hello problem is most likely that hello port, which is listened tooby Tomcat, is blocked by hello firewall.</span></span> <span data-ttu-id="30ad2-276">U kunt Hallo w3m hulpprogramma toobrowse Hallo webpagina gebruiken.</span><span class="sxs-lookup"><span data-stu-id="30ad2-276">You can use hello w3m tool toobrowse hello webpage.</span></span> <span data-ttu-id="30ad2-277">Hallo volgende opdrachten installeren w3m en toohello Tomcat standaardpagina bladeren:</span><span class="sxs-lookup"><span data-stu-id="30ad2-277">hello following commands install w3m and browse toohello Tomcat default page:</span></span>  


        <span data-ttu-id="30ad2-278">sudo yum installeren w3m w3m-img</span><span class="sxs-lookup"><span data-stu-id="30ad2-278">sudo yum  install w3m w3m-img</span></span>


        <span data-ttu-id="30ad2-279">w3m http://localhost: 8080</span><span class="sxs-lookup"><span data-stu-id="30ad2-279">w3m http://localhost:8080</span></span>  
#### <a name="solution"></a><span data-ttu-id="30ad2-280">Oplossing</span><span class="sxs-lookup"><span data-stu-id="30ad2-280">Solution</span></span>

  * <span data-ttu-id="30ad2-281">Als Hallo Tomcat listen-poort is niet dezelfde als de particuliere poort Hallo van Hallo-eindpunt voor verkeer toohello virtuele machine hello, hoeft u particuliere poort Hallo wijzigen toobe Hallo hetzelfde als het Hallo Tomcat listen-poort.</span><span class="sxs-lookup"><span data-stu-id="30ad2-281">If hello Tomcat listen port is not hello same as hello private port of hello endpoint for traffic toohello virtual machine, you need change hello private port toobe hello same as hello Tomcat listen port.</span></span>   
  2. <span data-ttu-id="30ad2-282">Als Hallo probleem wordt veroorzaakt door een firewall/iptables, voegt u Hallo regels te/etc/sysconfig/iptables te volgen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-282">If hello issue is caused by firewall/iptables, add hello following lines too/etc/sysconfig/iptables.</span></span> <span data-ttu-id="30ad2-283">de tweede regel Hallo is alleen nodig voor https-verkeer:</span><span class="sxs-lookup"><span data-stu-id="30ad2-283">hello second line is only needed for https traffic:</span></span>  

      <span data-ttu-id="30ad2-284">-A -p tcp -m tcp--port 80 -j accepteren invoer</span><span class="sxs-lookup"><span data-stu-id="30ad2-284">-A INPUT -p tcp -m tcp --dport 80 -j ACCEPT</span></span>

      <span data-ttu-id="30ad2-285">-A -p tcp -m tcp--Port 443 -j accepteren invoer</span><span class="sxs-lookup"><span data-stu-id="30ad2-285">-A INPUT -p tcp -m tcp --dport 443 -j ACCEPT</span></span>  

     > [!IMPORTANT]
     > <span data-ttu-id="30ad2-286">Zorg Hallo voorgaande regels boven alle regels die u zou toegang, zoals de volgende Hallo globaal beperken: - een invoer -j afwijzen--afwijzen-met icmp host verboden</span><span class="sxs-lookup"><span data-stu-id="30ad2-286">Make sure hello previous lines are positioned above any lines that would globally restrict access, such as hello following: -A INPUT -j REJECT --reject-with icmp-host-prohibited</span></span>



<span data-ttu-id="30ad2-287">tooreload hello iptables, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="30ad2-287">tooreload hello iptables, run hello following command:</span></span>

    service iptables restart

<span data-ttu-id="30ad2-288">Dit is getest op CentOS 6.3.</span><span class="sxs-lookup"><span data-stu-id="30ad2-288">This has been tested on CentOS 6.3.</span></span>

### <a name="permission-denied-when-you-upload-project-files-toovarlibtomcat7webapps"></a><span data-ttu-id="30ad2-289">De toegang is geweigerd tijdens het uploaden van project-bestanden te/var/lib/tomcat7/webapps /</span><span class="sxs-lookup"><span data-stu-id="30ad2-289">Permission denied when you upload project files too/var/lib/tomcat7/webapps/</span></span>
#### <a name="symptom"></a><span data-ttu-id="30ad2-290">Symptoom</span><span class="sxs-lookup"><span data-stu-id="30ad2-290">Symptom</span></span>
  <span data-ttu-id="30ad2-291">Als u een virtuele machine voor SFTP-client (zoals FileZilla) tooconnect tooyour gebruiken en navigeer te/var/lib/tomcat7/webapps/toopublish uw site, krijgt u een fout bericht vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="30ad2-291">When you use an SFTP client (such as FileZilla) tooconnect tooyour virtual machine and navigate too/var/lib/tomcat7/webapps/ toopublish your site, you get an error message similar toohello following:</span></span>  

     status:    Listing directory /var/lib/tomcat7/webapps
     Command:    put "C:\Users\liang\Desktop\info.jsp" "info.jsp"
     Error:    /var/lib/tomcat7/webapps/info.jsp: open for write: permission denied
     Error:    File transfer failed
#### <a name="possible-root-cause"></a><span data-ttu-id="30ad2-292">Mogelijke hoofdoorzaken</span><span class="sxs-lookup"><span data-stu-id="30ad2-292">Possible root cause</span></span>
  <span data-ttu-id="30ad2-293">U hebt geen machtigingen tooaccess hello /var/lib/tomcat7/webapps map.</span><span class="sxs-lookup"><span data-stu-id="30ad2-293">You have no permissions tooaccess hello /var/lib/tomcat7/webapps folder.</span></span>  
#### <a name="solution"></a><span data-ttu-id="30ad2-294">Oplossing</span><span class="sxs-lookup"><span data-stu-id="30ad2-294">Solution</span></span>  
  <span data-ttu-id="30ad2-295">U moet de machtiging tooget van Hallo root-account.</span><span class="sxs-lookup"><span data-stu-id="30ad2-295">You need tooget permission from hello root account.</span></span> <span data-ttu-id="30ad2-296">U kunt Hallo eigendom van die map wijzigen via hoofdmap toohello gebruikersnaam die u hebt gebruikt toen u Hallo machine ingericht.</span><span class="sxs-lookup"><span data-stu-id="30ad2-296">You can change hello ownership of that folder from root toohello username you used when you provisioned hello machine.</span></span> <span data-ttu-id="30ad2-297">Hier volgt een voorbeeld met Hallo azureuser accountnaam:</span><span class="sxs-lookup"><span data-stu-id="30ad2-297">Here is an example with hello azureuser account name:</span></span>  

     sudo chown azureuser -R /var/lib/tomcat7/webapps

  <span data-ttu-id="30ad2-298">Hallo -R optie tooapply Hallo machtigingen voor alle bestanden in een map te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="30ad2-298">Use hello -R option tooapply hello permissions for all files inside of a directory too.</span></span>  

  <span data-ttu-id="30ad2-299">Met deze opdracht werkt ook voor mappen.</span><span class="sxs-lookup"><span data-stu-id="30ad2-299">This command also works for directories.</span></span> <span data-ttu-id="30ad2-300">Hallo -R-optie wijzigingen Hallo machtigingen voor alle bestanden en mappen in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="30ad2-300">hello -R option changes hello permissions for all files and directories inside hello directory.</span></span> <span data-ttu-id="30ad2-301">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="30ad2-301">Here is an example:</span></span>  

     sudo chown -R username:group directory  

  <span data-ttu-id="30ad2-302">Deze opdracht wijzigt eigendom (gebruiker en groep) voor alle bestanden en mappen die zich binnen het Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="30ad2-302">This command changes ownership (both user and group) for all files and directories that are inside hello directory.</span></span>  

  <span data-ttu-id="30ad2-303">Hallo volgende opdracht alleen wijzigt Hallo machtiging Hallo mapdirectory.</span><span class="sxs-lookup"><span data-stu-id="30ad2-303">hello following command only changes hello permission of hello folder directory.</span></span> <span data-ttu-id="30ad2-304">Hallo-bestanden en mappen in de directory Hallo worden niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="30ad2-304">hello files and folders inside hello directory are not changed.</span></span>  

     sudo chown username:group directory

[1]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-01.png
[2]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-02.png
[3]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-03.png
[4]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-04.png
[5]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-05.png
[6]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-06.png
[7]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-07.png
[8]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-08.png
[9]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-09.png
[10]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-10.png
[11]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-11.png
[12]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-12.png
[13]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-13.png
[14]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-14.png
[15]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-15.png
[16]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-16.png
[17]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-17.png
[18]:media/setup-tomcat/virtual-machines-linux-setup-tomcat7-linux-18.png
