---
title: Java-toepassingsserver uitgevoerd op een klassieke Azure-virtuele machine | Microsoft Docs
description: Deze zelfstudie maakt gebruik van resources die zijn gemaakt met het klassieke implementatiemodel en laat zien hoe een virtuele Windows-machine maken en configureren voor het uitvoeren van de Apache Tomcat-toepassingsserver.
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
ms.openlocfilehash: 6e02f42613808bcb13c0057e9f8fcc1c02273e77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-java-application-server-on-a-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="de78a-103">Een Java-toepassingsserver uitvoeren op een virtuele machine die is gemaakt volgens het klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="de78a-103">How to run a Java application server on a virtual machine created with the classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="de78a-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="de78a-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="de78a-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="de78a-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="de78a-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="de78a-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="de78a-107">Zie voor een Resource Manager-sjabloon voor het implementeren van een webapp met Java 8 en Tomcat [hier](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="de78a-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="de78a-108">Met Azure, kunt u een virtuele machine zodat u de server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="de78a-108">With Azure, you can use a virtual machine to provide server capabilities.</span></span> <span data-ttu-id="de78a-109">Als u bijvoorbeeld kunt een virtuele machine uitgevoerd op Azure worden geconfigureerd voor het hosten van Java-toepassingsserver, zoals Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="de78a-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="de78a-110">Na het voltooien van deze handleiding hebt u een goed begrip van hoe u een virtuele machine uitgevoerd op Azure maken en configureren voor het uitvoeren van Java-toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="de78a-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span></span> <span data-ttu-id="de78a-111">U leert en de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="de78a-111">You will learn and perform the following tasks:</span></span>

* <span data-ttu-id="de78a-112">Het maken van een virtuele machine waarvoor een Java Development Kit (JDK) al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="de78a-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="de78a-113">Klik hier voor meer informatie over het extern aanmelden met uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-113">How to remotely sign in to your virtual machine.</span></span>
* <span data-ttu-id="de78a-114">Klik hier voor meer informatie over het installeren van een Java-toepassingsserver--Apache Tomcat--op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="de78a-115">Het maken van een eindpunt voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-115">How to create an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="de78a-116">Klik hier voor meer informatie over het openen van een poort in de firewall voor de toepassingsserver.</span><span class="sxs-lookup"><span data-stu-id="de78a-116">How to open a port in the firewall for your application server.</span></span>

<span data-ttu-id="de78a-117">De resultaten van de installatie is voltooid in Tomcat uitgevoerd op een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-117">The completed installation results in Tomcat running on a virtual machine.</span></span>

![Virtuele machine met Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="de78a-119">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="de78a-119">To create a virtual machine</span></span>
1. <span data-ttu-id="de78a-120">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de78a-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="de78a-121">Klik op **nieuw**, klikt u op **Compute**, klikt u vervolgens op **alle** in de **aanbevolen apps**.</span><span class="sxs-lookup"><span data-stu-id="de78a-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span></span>
3. <span data-ttu-id="de78a-122">Klik op **JDK**, klikt u op **JDK 8** in de **JDK** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="de78a-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span></span>  
   <span data-ttu-id="de78a-123">Installatiekopieën van virtuele machine die ondersteuning bieden voor **JDK 6** en **JDK 7** beschikbaar zijn als u oudere toepassingen die niet gereed in JDK 8 uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="de78a-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span></span>
4. <span data-ttu-id="de78a-124">Selecteer in het deelvenster JDK 8 **klassieke**, klikt u vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="de78a-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="de78a-125">In de **basisbeginselen** blade:</span><span class="sxs-lookup"><span data-stu-id="de78a-125">In the **Basics** blade:</span></span>
   1. <span data-ttu-id="de78a-126">Geef een naam voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-126">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="de78a-127">Voer een naam voor de beheerder in de **gebruikersnaam** veld.</span><span class="sxs-lookup"><span data-stu-id="de78a-127">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="de78a-128">Houd er rekening mee deze naam en het bijbehorende wachtwoord dat volgt op in het volgende veld.</span><span class="sxs-lookup"><span data-stu-id="de78a-128">Remember this name and the associated password that follows in the next field.</span></span> <span data-ttu-id="de78a-129">U moet ze wanneer u extern op de virtuele machine aanmelden.</span><span class="sxs-lookup"><span data-stu-id="de78a-129">You need them when you remotely sign in to the virtual machine.</span></span>
   3. <span data-ttu-id="de78a-130">Voer een wachtwoord in de **nieuw wachtwoord** veld en Bevestig het in de **wachtwoord bevestigen** veld.</span><span class="sxs-lookup"><span data-stu-id="de78a-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span></span> <span data-ttu-id="de78a-131">Dit wachtwoord is voor de Administrator-account.</span><span class="sxs-lookup"><span data-stu-id="de78a-131">This password is for the Administrator account.</span></span>
   4. <span data-ttu-id="de78a-132">Selecteer de relevante **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="de78a-132">Select the appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="de78a-133">Voor de **resourcegroep**, klikt u op **nieuw** en voer de naam van een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="de78a-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span></span> <span data-ttu-id="de78a-134">Of klik op **gebruik bestaande** en selecteer een van de beschikbare resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="de78a-134">Or, click **Use existing** and select one of the available resource groups.</span></span>
   6. <span data-ttu-id="de78a-135">Selecteer een locatie waarin de virtuele machine zich, zoals bevindt **Zuid-centraal VS**.</span><span class="sxs-lookup"><span data-stu-id="de78a-135">Select a location where the virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="de78a-136">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="de78a-136">Click **Next**.</span></span>
7. <span data-ttu-id="de78a-137">In de **de grootte van de virtuele machine-installatiekopie** blade Selecteer **A1 standaard** of een andere juiste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="de78a-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="de78a-138">Klik op **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="de78a-138">Click **Select**.</span></span>

9. <span data-ttu-id="de78a-139">In de **instellingen** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="de78a-139">In the **Settings** blade, click **OK**.</span></span> <span data-ttu-id="de78a-140">U kunt de standaardwaarden die is verstrekt door Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="de78a-140">You can use the default values provided by Azure.</span></span>  
10. <span data-ttu-id="de78a-141">In de **samenvatting** blade, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="de78a-141">In the **Summary** blade, click **OK**.</span></span>

## <a name="to-remotely-sign-in-to-your-virtual-machine"></a><span data-ttu-id="de78a-142">Extern aanmelden bij uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="de78a-142">To remotely sign in to your virtual machine</span></span>
1. <span data-ttu-id="de78a-143">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de78a-143">Log on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de78a-144">Klik op **virtuele machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="de78a-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="de78a-145">Klik indien nodig op **meer services** in de linkerbenedenhoek onder de servicecategorieën.</span><span class="sxs-lookup"><span data-stu-id="de78a-145">If needed, click **More services** at the bottom left corner under the service categories.</span></span> <span data-ttu-id="de78a-146">De **virtuele machines (klassiek)** vermelding wordt vermeld in de **Compute** groep.</span><span class="sxs-lookup"><span data-stu-id="de78a-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span></span>
3. <span data-ttu-id="de78a-147">Klik op de naam van de virtuele machine die u aanmelden wilt bij.</span><span class="sxs-lookup"><span data-stu-id="de78a-147">Click the name of the virtual machine that you want to sign in to.</span></span>
4. <span data-ttu-id="de78a-148">Nadat de virtuele machine is gestart, wordt in een menu aan de bovenkant van het deelvenster verbindingen toestaat.</span><span class="sxs-lookup"><span data-stu-id="de78a-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span></span>
5. <span data-ttu-id="de78a-149">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="de78a-149">Click **Connect**.</span></span>
6. <span data-ttu-id="de78a-150">Reageren op de vragen naar behoefte verbinding maken met de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-150">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="de78a-151">Normaal gesproken opslaan of open het RDP-bestand dat de verbindingsgegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="de78a-151">Typically, you save or open the .rdp file that contains the connection details.</span></span> <span data-ttu-id="de78a-152">Mogelijk moet de url: poort als het laatste deel van de eerste regel van het RDP-bestand kopiëren en plakken in een toepassing voor externe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="de78a-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="to-install-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="de78a-153">Java-toepassingsserver installeren op uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="de78a-153">To install a Java application server on your virtual machine</span></span>
<span data-ttu-id="de78a-154">U kunt een Java-toepassingsserver kopiëren naar uw virtuele machine of kunt u een Java-toepassingsserver via een installatieprogramma installeren.</span><span class="sxs-lookup"><span data-stu-id="de78a-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="de78a-155">Deze zelfstudie wordt Tomcat als de Java-toepassingsserver installeren.</span><span class="sxs-lookup"><span data-stu-id="de78a-155">This tutorial uses Tomcat as the Java application server to install.</span></span>

1. <span data-ttu-id="de78a-156">Wanneer u bent aangemeld met uw virtuele machine, open een browsersessie op [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="de78a-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="de78a-157">Dubbelklik op de koppeling voor **32-bits/64-bits Windows-Service Installer**.</span><span class="sxs-lookup"><span data-stu-id="de78a-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="de78a-158">Met deze techniek kunnen installeert Tomcat als een Windows-service.</span><span class="sxs-lookup"><span data-stu-id="de78a-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="de78a-159">Wanneer u wordt gevraagd, kiest u het installatieprogramma uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="de78a-159">When prompted, choose to run the installer.</span></span>
4. <span data-ttu-id="de78a-160">Binnen de **Apache Tomcat Setup** wizard, volg de aanwijzingen voor het installeren van Tomcat.</span><span class="sxs-lookup"><span data-stu-id="de78a-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span></span> <span data-ttu-id="de78a-161">Voor de doeleinden van deze zelfstudie is het fijn accepteer de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="de78a-161">For the purposes of this tutorial, accepting the defaults is fine.</span></span> <span data-ttu-id="de78a-162">Wanneer u bereikt de **voltooien van de Wizard Setup van Apache Tomcat** in het dialoogvenster kunt u eventueel controleren **uitvoeren Apache Tomcat** hebben Tomcat nu starten.</span><span class="sxs-lookup"><span data-stu-id="de78a-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span></span> <span data-ttu-id="de78a-163">Klik op **voltooien** de Tomcat-installatieproces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="de78a-163">Click **Finish** to complete the Tomcat setup process.</span></span>

## <a name="to-start-tomcat"></a><span data-ttu-id="de78a-164">Tomcat starten</span><span class="sxs-lookup"><span data-stu-id="de78a-164">To start Tomcat</span></span>

<span data-ttu-id="de78a-165">U kunt Tomcat handmatig starten door te openen vanaf de opdrachtprompt op de virtuele machine en de opdracht uit te voeren **net&nbsp;start&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="de78a-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="de78a-166">Wanneer Tomcat wordt uitgevoerd, kunt u Tomcat openen door te voeren van de URL <http://localhost: 8080> in de browser van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span></span>

<span data-ttu-id="de78a-167">Om te zien Tomcat vanaf externe computers wordt uitgevoerd, moet u een eindpunt worden gemaakt en een poort openen.</span><span class="sxs-lookup"><span data-stu-id="de78a-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span></span>

## <a name="to-create-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="de78a-168">Een eindpunt voor uw virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="de78a-168">To create an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="de78a-169">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de78a-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="de78a-170">Klik op **virtuele machines (klassiek)**.</span><span class="sxs-lookup"><span data-stu-id="de78a-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="de78a-171">Klik op de naam van de virtuele machine die uw Java-toepassingsserver wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="de78a-171">Click the name of the virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="de78a-172">Klik op **Eindpunten**.</span><span class="sxs-lookup"><span data-stu-id="de78a-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="de78a-173">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="de78a-173">Click **Add**.</span></span>
6. <span data-ttu-id="de78a-174">In de **eindpunt toevoegen** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="de78a-174">In the **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="de78a-175">Geef een naam voor het eindpunt; bijvoorbeeld: **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="de78a-175">Specify a name for the endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="de78a-176">Selecteer **TCP** voor het protocol.</span><span class="sxs-lookup"><span data-stu-id="de78a-176">Select **TCP** for the protocol.</span></span>
   3. <span data-ttu-id="de78a-177">Geef **80** voor de openbare poort.</span><span class="sxs-lookup"><span data-stu-id="de78a-177">Specify **80** for the public port.</span></span>
   4. <span data-ttu-id="de78a-178">Geef **8080** voor de particuliere poort.</span><span class="sxs-lookup"><span data-stu-id="de78a-178">Specify **8080** for the private port.</span></span>
   5. <span data-ttu-id="de78a-179">Selecteer **uitgeschakelde** zwevend IP-adres.</span><span class="sxs-lookup"><span data-stu-id="de78a-179">Select **Disabled** for the floating IP address.</span></span>
   6. <span data-ttu-id="de78a-180">Laat de toegangsbeheerlijst is.</span><span class="sxs-lookup"><span data-stu-id="de78a-180">Leave the access control list as is.</span></span>
   7. <span data-ttu-id="de78a-181">Klik op de **OK** om het dialoogvenster sluiten en het eindpunt te maken.</span><span class="sxs-lookup"><span data-stu-id="de78a-181">Click the **OK** button to close the dialog box and create the endpoint.</span></span>

## <a name="to-open-a-port-in-the-firewall-for-your-virtual-machine"></a><span data-ttu-id="de78a-182">Een poort openen in de firewall voor uw virtuele machine</span><span class="sxs-lookup"><span data-stu-id="de78a-182">To open a port in the firewall for your virtual machine</span></span>
1. <span data-ttu-id="de78a-183">Meld u aan met uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="de78a-183">Sign in to your virtual machine.</span></span>
2. <span data-ttu-id="de78a-184">Klik op **Windows Start**.</span><span class="sxs-lookup"><span data-stu-id="de78a-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="de78a-185">Klik op **Configuratiescherm**.</span><span class="sxs-lookup"><span data-stu-id="de78a-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="de78a-186">Klik op **systeem en beveiliging**, klikt u op **Windows Firewall**, en klik vervolgens op **geavanceerde instellingen**.</span><span class="sxs-lookup"><span data-stu-id="de78a-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="de78a-187">Klik op **regels voor binnenkomende verbindingen**, en klik vervolgens op **nieuwe regel**.</span><span class="sxs-lookup"><span data-stu-id="de78a-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="de78a-188">![Nieuwe regel binnenkomende verbindingen][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="de78a-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="de78a-189">Voor de **regeltype**, selecteer **poort**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="de78a-189">For the **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="de78a-190">![Nieuwe regel voor binnenkomende verbindingen poort][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="de78a-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="de78a-191">Op de **protocollen en poorten** Schakel in het scherm **TCP**, geef **8080** als de **specifieke lokale poort**, en klik vervolgens op  **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="de78a-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="de78a-192">![Nieuwe regel binnenkomende verbindingen][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="de78a-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="de78a-193">Op de **actie** Schakel in het scherm **de verbinding toestaan**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="de78a-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span></span>
   <span data-ttu-id="de78a-194">![Nieuwe regel voor binnenkomende verbindingen actie][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="de78a-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="de78a-195">Op de **profiel** scherm **domein**, **persoonlijke**, en **openbare** zijn geselecteerd en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="de78a-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="de78a-196">![Nieuwe regel voor binnenkomende verbindingen profiel][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="de78a-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="de78a-197">Op de **naam** scherm, Geef een naam voor de regel, zoals **HttpIn** (naam van de regel is niet vereist echter aan de naam van het eindpunt), en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="de78a-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="de78a-198">![De naam van een nieuwe regel voor binnenkomende verbindingen][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="de78a-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="de78a-199">Op dit moment uw website Tomcat worden weergegeven op een externe browser.</span><span class="sxs-lookup"><span data-stu-id="de78a-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="de78a-200">Typ een URL van het formulier in de browser adres venster  **http://*uw\_DNS\_naam*. cloudapp.net**, waarbij ***uw\_DNS\_naam*** de DNS-naam die u hebt opgegeven toen u de virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="de78a-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="de78a-201">Toepassing lifecycle overwegingen</span><span class="sxs-lookup"><span data-stu-id="de78a-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="de78a-202">Kan u uw eigen toepassing webarchief (WAR) maken en toe te voegen aan de **webapps** map.</span><span class="sxs-lookup"><span data-stu-id="de78a-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span></span> <span data-ttu-id="de78a-203">Bijvoorbeeld, een elementaire Java Service pagina (JSP) dynamic webproject maken en exporteren als een WAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="de78a-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="de78a-204">Kopieer vervolgens het WAR naar de Apache Tomcat **webapps** map op de virtuele machine en vervolgens uit te voeren in een browser.</span><span class="sxs-lookup"><span data-stu-id="de78a-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="de78a-205">Wanneer de Tomcat-service is geïnstalleerd, is deze standaard ingesteld om handmatig te starten.</span><span class="sxs-lookup"><span data-stu-id="de78a-205">By default when the Tomcat service is installed, it is set to start manually.</span></span> <span data-ttu-id="de78a-206">U kunt deze automatisch wordt gestart met behulp van de module Services in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="de78a-206">You can switch it to start automatically by using the Services snap-in.</span></span> <span data-ttu-id="de78a-207">Start de Services-module door te klikken op **Start Windows**, **Systeembeheer**, en vervolgens **Services**.</span><span class="sxs-lookup"><span data-stu-id="de78a-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="de78a-208">Dubbelklik op de **Apache Tomcat** service en stel **opstarttype** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="de78a-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span></span>

    ![Instellen van een service op automatisch starten][service_automatic_startup]

    <span data-ttu-id="de78a-210">Het voordeel dat automatisch wordt gestart Tomcat is dat het wordt gestart wanneer de virtuele machine opnieuw wordt opgestart (bijvoorbeeld nadat software-updates waarvoor opnieuw opstarten zijn geïnstalleerd).</span><span class="sxs-lookup"><span data-stu-id="de78a-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de78a-211">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de78a-211">Next steps</span></span>
<span data-ttu-id="de78a-212">U kunt meer informatie over andere services die u wilt opnemen met uw Java-toepassingen (zoals Azure Storage, servicebus en SQL-Database).</span><span class="sxs-lookup"><span data-stu-id="de78a-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span></span> <span data-ttu-id="de78a-213">Bekijk de informatie die beschikbaar zijn op de [Java Developer Center](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="de78a-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from the "To create an ednpoint for your virtual mache" 3/17/2017,
     to use the new portal.
6. In the **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In the **New endpoint details** dialog box:
-->
