---
title: aaaRun Java-toepassingsserver op een klassieke Azure-virtuele machine | Microsoft Docs
description: Deze zelfstudie maakt gebruik van bronnen die zijn gemaakt met het klassieke implementatiemodel Hallo en toont hoe toocreate een Windows-virtuele machine en configureer deze toorun Apache Tomcat-toepassingsserver.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="8764f-103">Hoe toorun Java-toepassingsserver op een virtuele machine gemaakt met het klassieke implementatiemodel Hallo</span><span class="sxs-lookup"><span data-stu-id="8764f-103">How toorun a Java application server on a virtual machine created with hello classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8764f-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8764f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8764f-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="8764f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8764f-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8764f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="8764f-107">Zie voor toodeploy een webapp met Java 8 en Tomcat van een Resource Manager-sjabloon [hier](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="8764f-107">For a Resource Manager template toodeploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="8764f-108">U kunt een virtuele machine tooprovide server mogelijkheden kunt gebruiken met Azure.</span><span class="sxs-lookup"><span data-stu-id="8764f-108">With Azure, you can use a virtual machine tooprovide server capabilities.</span></span> <span data-ttu-id="8764f-109">Als u bijvoorbeeld mag een virtuele machine uitgevoerd op Azure geconfigureerde toohost Java-toepassingsserver, zoals Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="8764f-109">As an example, a virtual machine running on Azure can be configured toohost a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="8764f-110">Na het voltooien van deze handleiding hebt u een goed begrip van hoe u een virtuele machine toocreate uitgevoerd op Azure en configureer deze toorun Java-toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="8764f-110">After completing this guide, you will have an understanding of how toocreate a virtual machine running on Azure and configure it toorun a Java application server.</span></span> <span data-ttu-id="8764f-111">U leert en Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8764f-111">You will learn and perform hello following tasks:</span></span>

* <span data-ttu-id="8764f-112">Hoe toocreate een virtuele machine die heeft een Java Development Kit (JDK) al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8764f-112">How toocreate a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="8764f-113">Hoe tooremotely log in tooyour virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-113">How tooremotely sign in tooyour virtual machine.</span></span>
* <span data-ttu-id="8764f-114">Hoe tooinstall Java-toepassingsserver--Apache Tomcat--op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-114">How tooinstall a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="8764f-115">Hoe toocreate een eindpunt voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-115">How toocreate an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="8764f-116">Hoe een poort in Hallo tooopen firewall voor de toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="8764f-116">How tooopen a port in hello firewall for your application server.</span></span>

<span data-ttu-id="8764f-117">Hallo voltooid Installatieresultaten in Tomcat uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-117">hello completed installation results in Tomcat running on a virtual machine.</span></span>

![Virtuele machine met Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="8764f-119">toocreate een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8764f-119">toocreate a virtual machine</span></span>
1. <span data-ttu-id="8764f-120">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8764f-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="8764f-121">Klik op **nieuw**, klikt u op **Compute**, klikt u vervolgens op **alle** in Hallo **aanbevolen apps**.</span><span class="sxs-lookup"><span data-stu-id="8764f-121">Click **New**, click **Compute**, then click **See all** in hello **Featured apps**.</span></span>
3. <span data-ttu-id="8764f-122">Klik op **JDK**, klikt u op **JDK 8** in Hallo **JDK** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="8764f-122">Click **JDK**, click **JDK 8** in hello **JDK** pane.</span></span>  
   <span data-ttu-id="8764f-123">Installatiekopieën van virtuele machine die ondersteuning bieden voor **JDK 6** en **JDK 7** beschikbaar zijn als u oudere toepassingen die niet gereed toorun in JDK 8.</span><span class="sxs-lookup"><span data-stu-id="8764f-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready toorun in JDK 8.</span></span>
4. <span data-ttu-id="8764f-124">Selecteer in het deelvenster Hallo JDK 8 **klassieke**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="8764f-124">In hello JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="8764f-125">In Hallo **basisbeginselen** blade:</span><span class="sxs-lookup"><span data-stu-id="8764f-125">In hello **Basics** blade:</span></span>
   1. <span data-ttu-id="8764f-126">Geef een naam voor de Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-126">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="8764f-127">Voer een naam voor Hallo beheerder in Hallo **gebruikersnaam** veld.</span><span class="sxs-lookup"><span data-stu-id="8764f-127">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="8764f-128">Houd er rekening mee deze naam en bijbehorende wachtwoord dat volgt op in het volgende veld Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8764f-128">Remember this name and hello associated password that follows in hello next field.</span></span> <span data-ttu-id="8764f-129">U moet deze als u zich extern toohello virtuele machine aanmelden.</span><span class="sxs-lookup"><span data-stu-id="8764f-129">You need them when you remotely sign in toohello virtual machine.</span></span>
   3. <span data-ttu-id="8764f-130">Voer een wachtwoord in Hallo **nieuw wachtwoord** veld en voer deze opnieuw in Hallo **wachtwoord bevestigen** veld.</span><span class="sxs-lookup"><span data-stu-id="8764f-130">Enter a password in hello **New password** field, and reenter it in hello **Confirm password** field.</span></span> <span data-ttu-id="8764f-131">Dit wachtwoord is voor Hallo Administrator-account.</span><span class="sxs-lookup"><span data-stu-id="8764f-131">This password is for hello Administrator account.</span></span>
   4. <span data-ttu-id="8764f-132">Selecteer Hallo juiste **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8764f-132">Select hello appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="8764f-133">Voor Hallo **resourcegroep**, klikt u op **nieuw** en Voer Hallo-naam van een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8764f-133">For hello **Resource group**, click **Create new** and enter hello name of a new resource group.</span></span> <span data-ttu-id="8764f-134">Of klik op **gebruik bestaande** en selecteer een van de beschikbare resourcegroepen Hallo.</span><span class="sxs-lookup"><span data-stu-id="8764f-134">Or, click **Use existing** and select one of hello available resource groups.</span></span>
   6. <span data-ttu-id="8764f-135">Selecteer een locatie waarin Hallo virtuele machine zich, zoals bevindt **Zuid-centraal VS**.</span><span class="sxs-lookup"><span data-stu-id="8764f-135">Select a location where hello virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="8764f-136">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="8764f-136">Click **Next**.</span></span>
7. <span data-ttu-id="8764f-137">In Hallo **de grootte van de virtuele machine-installatiekopie** blade Selecteer **A1 standaard** of een andere juiste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8764f-137">In hello **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="8764f-138">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="8764f-138">Click **Select**.</span></span>

9. <span data-ttu-id="8764f-139">In Hallo **instellingen** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8764f-139">In hello **Settings** blade, click **OK**.</span></span> <span data-ttu-id="8764f-140">U kunt de standaardwaarden Hallo verstrekt door Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8764f-140">You can use hello default values provided by Azure.</span></span>  
10. <span data-ttu-id="8764f-141">In Hallo **samenvatting** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8764f-141">In hello **Summary** blade, click **OK**.</span></span>

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a><span data-ttu-id="8764f-142">tooremotely aanmelden tooyour virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8764f-142">tooremotely sign in tooyour virtual machine</span></span>
1. <span data-ttu-id="8764f-143">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8764f-143">Log on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8764f-144">Klik op **virtuele machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="8764f-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="8764f-145">Klik indien nodig op **meer services** in linkerbenedenhoek onder servicecategorieën Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="8764f-145">If needed, click **More services** at hello bottom left corner under hello service categories.</span></span> <span data-ttu-id="8764f-146">Hallo **virtuele machines (klassiek)** vermelding wordt vermeld in Hallo **Compute** groep.</span><span class="sxs-lookup"><span data-stu-id="8764f-146">hello **Virtual machines (classic)** entry is listed in hello **Compute** group.</span></span>
3. <span data-ttu-id="8764f-147">Klik op de naam Hallo van Hallo virtuele machine die u wilt toosign in.</span><span class="sxs-lookup"><span data-stu-id="8764f-147">Click hello name of hello virtual machine that you want toosign in to.</span></span>
4. <span data-ttu-id="8764f-148">Nadat Hallo virtuele machine is gestart, kunt een menu bovenaan Hallo Hallo deelvenster verbindingen.</span><span class="sxs-lookup"><span data-stu-id="8764f-148">After hello virtual machine has started, a menu at hello top of hello pane allows connections.</span></span>
5. <span data-ttu-id="8764f-149">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="8764f-149">Click **Connect**.</span></span>
6. <span data-ttu-id="8764f-150">Reageren op toohello prompts als benodigde tooconnect toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-150">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="8764f-151">Normaal gesproken opslaan of Hallo RDP-bestand met de Hallo verbindingsgegevens openen.</span><span class="sxs-lookup"><span data-stu-id="8764f-151">Typically, you save or open hello .rdp file that contains hello connection details.</span></span> <span data-ttu-id="8764f-152">U kunt toocopy Hallo url: poort als Hallo laatste deel van de eerste regel Hallo van Hallo RDP-bestand hebben en plak deze in een toepassing voor externe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="8764f-152">You might have toocopy hello url:port as hello last part of hello first line of hello .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="8764f-153">tooinstall Java-toepassingsserver op de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8764f-153">tooinstall a Java application server on your virtual machine</span></span>
<span data-ttu-id="8764f-154">U kunt een virtuele machine voor Java application server tooyour kopiëren of kunt u een Java-toepassingsserver via een installatieprogramma installeren.</span><span class="sxs-lookup"><span data-stu-id="8764f-154">You can copy a Java application server tooyour virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="8764f-155">Deze zelfstudie wordt Tomcat als Hallo Java application server tooinstall.</span><span class="sxs-lookup"><span data-stu-id="8764f-155">This tutorial uses Tomcat as hello Java application server tooinstall.</span></span>

1. <span data-ttu-id="8764f-156">Wanneer u bent aangemeld in tooyour virtuele machine, opent u een browsersessie te[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="8764f-156">When you are signed in tooyour virtual machine, open a browser session too[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="8764f-157">Dubbelklik op de koppeling Hallo voor **32-bits/64-bits Windows-Service Installer**.</span><span class="sxs-lookup"><span data-stu-id="8764f-157">Double-click hello link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="8764f-158">Met deze techniek kunnen installeert Tomcat als een Windows-service.</span><span class="sxs-lookup"><span data-stu-id="8764f-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="8764f-159">Wanneer u wordt gevraagd, kiest u toorun Hallo installatieprogramma.</span><span class="sxs-lookup"><span data-stu-id="8764f-159">When prompted, choose toorun hello installer.</span></span>
4. <span data-ttu-id="8764f-160">Binnen Hallo **Apache Tomcat Setup** , volg Hallo gevraagd tooinstall Tomcat.</span><span class="sxs-lookup"><span data-stu-id="8764f-160">Within hello **Apache Tomcat Setup** wizard, follow hello prompts tooinstall Tomcat.</span></span> <span data-ttu-id="8764f-161">Voor Hallo doel van deze zelfstudie is het fijn Hallo standaardinstellingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="8764f-161">For hello purposes of this tutorial, accepting hello defaults is fine.</span></span> <span data-ttu-id="8764f-162">Wanneer u Hallo bereikt **voltooien Hallo Apache Tomcat-installatiewizard** in het dialoogvenster kunt u eventueel controleren **uitvoeren Apache Tomcat** toohave nu Tomcat start.</span><span class="sxs-lookup"><span data-stu-id="8764f-162">When you reach hello **Completing hello Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** toohave Tomcat start now.</span></span> <span data-ttu-id="8764f-163">Klik op **voltooien** toocomplete Hallo Tomcat-installatieproces.</span><span class="sxs-lookup"><span data-stu-id="8764f-163">Click **Finish** toocomplete hello Tomcat setup process.</span></span>

## <a name="toostart-tomcat"></a><span data-ttu-id="8764f-164">toostart Tomcat</span><span class="sxs-lookup"><span data-stu-id="8764f-164">toostart Tomcat</span></span>

<span data-ttu-id="8764f-165">U kunt Tomcat handmatig starten via een opdrachtprompt op de virtuele machine en de actieve Hallo opdracht **net&nbsp;start&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="8764f-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running hello command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="8764f-166">Wanneer Tomcat wordt uitgevoerd, kunt u Tomcat openen door te voeren Hallo URL <http://localhost: 8080> in de browser Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-166">Once Tomcat is running, you can access Tomcat by entering hello URL <http://localhost:8080> in hello virtual machine's browser.</span></span>

<span data-ttu-id="8764f-167">toosee Tomcat vanaf externe computers wordt uitgevoerd, u toocreate een eindpunt nodig hebt en een poort openen.</span><span class="sxs-lookup"><span data-stu-id="8764f-167">toosee Tomcat running from external machines, you need toocreate an endpoint and open a port.</span></span>

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="8764f-168">toocreate een eindpunt voor uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8764f-168">toocreate an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="8764f-169">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8764f-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8764f-170">Klik op **virtuele machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="8764f-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="8764f-171">Klik op de naam Hallo van Hallo virtuele machine waarop uw Java-toepassingsserver wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8764f-171">Click hello name of hello virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="8764f-172">Klik op **Eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="8764f-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="8764f-173">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="8764f-173">Click **Add**.</span></span>
6. <span data-ttu-id="8764f-174">In Hallo **eindpunt toevoegen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="8764f-174">In hello **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="8764f-175">Geef een naam voor het eindpunt Hallo; bijvoorbeeld: **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="8764f-175">Specify a name for hello endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="8764f-176">Selecteer **TCP** voor het Hallo-protocol.</span><span class="sxs-lookup"><span data-stu-id="8764f-176">Select **TCP** for hello protocol.</span></span>
   3. <span data-ttu-id="8764f-177">Geef **80** voor Hallo openbare poort.</span><span class="sxs-lookup"><span data-stu-id="8764f-177">Specify **80** for hello public port.</span></span>
   4. <span data-ttu-id="8764f-178">Geef **8080** voor Hallo particuliere poort.</span><span class="sxs-lookup"><span data-stu-id="8764f-178">Specify **8080** for hello private port.</span></span>
   5. <span data-ttu-id="8764f-179">Selecteer **uitgeschakelde** voor Hallo zwevend IP-adres.</span><span class="sxs-lookup"><span data-stu-id="8764f-179">Select **Disabled** for hello floating IP address.</span></span>
   6. <span data-ttu-id="8764f-180">Laat Hallo toegangsbeheerlijst is.</span><span class="sxs-lookup"><span data-stu-id="8764f-180">Leave hello access control list as is.</span></span>
   7. <span data-ttu-id="8764f-181">Klik op Hallo **OK** tooclose Hallo dialoogvenster knop en Hallo-eindpunt worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8764f-181">Click hello **OK** button tooclose hello dialog box and create hello endpoint.</span></span>

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a><span data-ttu-id="8764f-182">tooopen een poort in de firewall Hallo voor uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8764f-182">tooopen a port in hello firewall for your virtual machine</span></span>
1. <span data-ttu-id="8764f-183">Meld u aan tooyour virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8764f-183">Sign in tooyour virtual machine.</span></span>
2. <span data-ttu-id="8764f-184">Klik op **Windows Start**.</span><span class="sxs-lookup"><span data-stu-id="8764f-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="8764f-185">Klik op **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="8764f-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="8764f-186">Klik op **systeem en beveiliging**, klikt u op **Windows Firewall**, en klik vervolgens op **geavanceerde instellingen**.</span><span class="sxs-lookup"><span data-stu-id="8764f-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="8764f-187">Klik op **regels voor binnenkomende verbindingen**, en klik vervolgens op **nieuwe regel**.</span><span class="sxs-lookup"><span data-stu-id="8764f-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="8764f-188">![Nieuwe regel binnenkomende verbindingen][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="8764f-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="8764f-189">Voor Hallo **regeltype**, selecteer **poort**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8764f-189">For hello **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="8764f-190">![Nieuwe regel voor binnenkomende verbindingen poort][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="8764f-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="8764f-191">Op Hallo **protocollen en poorten** Schakel in het scherm **TCP**, geef **8080** als Hallo **specifieke lokale poort**, en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="8764f-191">On hello **Protocol and Ports** screen, select **TCP**, specify **8080** as hello **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="8764f-192">![Nieuwe regel binnenkomende verbindingen][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="8764f-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="8764f-193">Op Hallo **actie** Schakel in het scherm **Hallo verbinding toestaan**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="8764f-193">On hello **Action** screen, select **Allow hello connection**, and then click **Next**.</span></span>
   <span data-ttu-id="8764f-194">![Nieuwe regel voor binnenkomende verbindingen actie][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="8764f-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="8764f-195">Op Hallo **profiel** scherm **domein**, **persoonlijke**, en **openbare** zijn geselecteerd en klik vervolgens op **volgende** .</span><span class="sxs-lookup"><span data-stu-id="8764f-195">On hello **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="8764f-196">![Nieuwe regel voor binnenkomende verbindingen profiel][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="8764f-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="8764f-197">Op Hallo **naam** scherm, Geef een naam voor de regel hello, zoals **HttpIn** (Hallo regelnaam is niet vereist toomatch Hallo eindpuntnaam, echter), en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="8764f-197">On hello **Name** screen, specify a name for hello rule, such as **HttpIn** (hello rule name is not required toomatch hello endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="8764f-198">![De naam van een nieuwe regel voor binnenkomende verbindingen][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="8764f-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="8764f-199">Op dit moment uw website Tomcat worden weergegeven op een externe browser.</span><span class="sxs-lookup"><span data-stu-id="8764f-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="8764f-200">Typ in het venster van de webbrowser van het Hallo-adres met Hallo URL  **http://*uw\_DNS\_naam*. cloudapp.net**, waarbij ***uw\_DNS\_naam*** Hallo DNS-naam die u hebt opgegeven toen u Hallo virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8764f-200">In hello browser's address window, type a URL of hello form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is hello DNS name you specified when you created hello virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="8764f-201">Toepassing lifecycle overwegingen</span><span class="sxs-lookup"><span data-stu-id="8764f-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="8764f-202">Kan u uw eigen toepassing webarchief (WAR) maken en toe te voegen toohello **webapps** map.</span><span class="sxs-lookup"><span data-stu-id="8764f-202">You could create your own web application archive (WAR) and add it toohello **webapps** folder.</span></span> <span data-ttu-id="8764f-203">Bijvoorbeeld, een elementaire Java Service pagina (JSP) dynamic webproject maken en exporteren als een WAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="8764f-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="8764f-204">Kopieer vervolgens Hallo WAR toohello Apache Tomcat **webapps** map Hallo voor virtuele machines vervolgens uit te voeren in een browser.</span><span class="sxs-lookup"><span data-stu-id="8764f-204">Next, copy hello WAR toohello Apache Tomcat **webapps** folder on hello virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="8764f-205">Wanneer Hallo Tomcat-service is geïnstalleerd, is deze standaard ingesteld toostart handmatig.</span><span class="sxs-lookup"><span data-stu-id="8764f-205">By default when hello Tomcat service is installed, it is set toostart manually.</span></span> <span data-ttu-id="8764f-206">U kunt schakelen deze toostart automatisch via Hallo-module Services.</span><span class="sxs-lookup"><span data-stu-id="8764f-206">You can switch it toostart automatically by using hello Services snap-in.</span></span> <span data-ttu-id="8764f-207">Hallo-module Services starten door te klikken op **Start Windows**, **Systeembeheer**, en vervolgens **Services**.</span><span class="sxs-lookup"><span data-stu-id="8764f-207">Start hello Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="8764f-208">Dubbelklik op Hallo **Apache Tomcat** service en stel **opstarttype** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="8764f-208">Double-click hello **Apache Tomcat** service and set **Startup type** too**Automatic**.</span></span>

    ![Een service toostart instellen automatisch][service_automatic_startup]

    <span data-ttu-id="8764f-210">Hallo is voordeel van Tomcat automatisch wordt gestart met dat het wordt gestart wanneer Hallo virtuele machine opnieuw wordt opgestart (bijvoorbeeld nadat software-updates waarvoor opnieuw opstarten zijn geïnstalleerd).</span><span class="sxs-lookup"><span data-stu-id="8764f-210">hello benefit of having Tomcat start automatically is that it starts running when hello virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8764f-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8764f-211">Next steps</span></span>
<span data-ttu-id="8764f-212">U kunt meer informatie over andere services (zoals Azure Storage, servicebus en SQL-Database) die u kunt tooinclude met uw Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8764f-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want tooinclude with your Java applications.</span></span> <span data-ttu-id="8764f-213">Hallo beschikbare informatie bekijken op Hallo [Java Developer Center](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="8764f-213">View hello information available at hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
