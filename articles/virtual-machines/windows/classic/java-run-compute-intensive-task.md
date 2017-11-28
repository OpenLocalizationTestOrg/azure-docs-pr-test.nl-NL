---
title: Java-toepassing op een virtuele machine aaaCompute-intensieve | Microsoft Docs
description: Meer informatie over hoe toocreate Azure een virtuele machine die een rekenintensieve Java-toepassing wordt uitgevoerd door een andere Java-toepassing kan worden bewaakt.
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a><span data-ttu-id="49db1-103">Hoe een rekenintensieve toorun taak Java op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="49db1-103">How toorun a compute-intensive task in Java on a virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="49db1-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="49db1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="49db1-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="49db1-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="49db1-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49db1-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="49db1-107">Met Azure, kunt u een virtuele machine toohandle rekenintensieve taken.</span><span class="sxs-lookup"><span data-stu-id="49db1-107">With Azure, you can use a virtual machine toohandle compute-intensive tasks.</span></span> <span data-ttu-id="49db1-108">Bijvoorbeeld: een virtuele machine verwerkt taken en leveren resultaten tooclient computers of mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="49db1-108">For example, a virtual machine can handle tasks and deliver results tooclient machines or mobile applications.</span></span> <span data-ttu-id="49db1-109">Na het lezen van dit artikel hebt u een goed begrip van hoe toocreate een virtuele machine die een rekenintensieve Java-toepassing wordt uitgevoerd door een andere Java-toepassing kan worden bewaakt.</span><span class="sxs-lookup"><span data-stu-id="49db1-109">After reading this article, you will have an understanding of how toocreate a virtual machine that runs a compute-intensive Java application that can be monitored by another Java application.</span></span>

<span data-ttu-id="49db1-110">Deze zelfstudie wordt ervan uitgegaan dat u weet hoe toocreate Java-consoletoepassingen bibliotheken tooyour Java-toepassing kunt importeren en een Java-archief (JAR) kunt genereren.</span><span class="sxs-lookup"><span data-stu-id="49db1-110">This tutorial assumes you know how toocreate Java console applications, can import libraries tooyour Java application, and can generate a Java archive (JAR).</span></span> <span data-ttu-id="49db1-111">Er is geen kennis van Microsoft Azure wordt verondersteld.</span><span class="sxs-lookup"><span data-stu-id="49db1-111">No knowledge of Microsoft Azure is assumed.</span></span>

<span data-ttu-id="49db1-112">U leert:</span><span class="sxs-lookup"><span data-stu-id="49db1-112">You will learn:</span></span>

* <span data-ttu-id="49db1-113">Hoe toocreate een virtuele machine met een Java Development Kit (JDK) al is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-113">How toocreate a virtual machine with a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="49db1-114">Hoe meld tooremotely in tooyour virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49db1-114">How tooremotely log in tooyour virtual machine.</span></span>
* <span data-ttu-id="49db1-115">Hoe toocreate een service bus naamruimte.</span><span class="sxs-lookup"><span data-stu-id="49db1-115">How toocreate a service bus namespace.</span></span>
* <span data-ttu-id="49db1-116">Hoe toocreate een Java-toepassing die een taak rekenintensieve uitvoert.</span><span class="sxs-lookup"><span data-stu-id="49db1-116">How toocreate a Java application that performs a compute-intensive task.</span></span>
* <span data-ttu-id="49db1-117">Hoe Hallo toocreate een Java-toepassing bewaakt de voortgang van Hallo rekenintensieve taak.</span><span class="sxs-lookup"><span data-stu-id="49db1-117">How toocreate a Java application that monitors hello progress of hello compute-intensive task.</span></span>
* <span data-ttu-id="49db1-118">Hoe Hallo toorun Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="49db1-118">How toorun hello Java applications.</span></span>
* <span data-ttu-id="49db1-119">Hoe Hallo toostop Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="49db1-119">How toostop hello Java applications.</span></span>

<span data-ttu-id="49db1-120">Deze zelfstudie gebruikt Hallo Traveling verkoper probleem voor Hallo rekenintensieve taak.</span><span class="sxs-lookup"><span data-stu-id="49db1-120">This tutorial will use hello Traveling Salesman Problem for hello compute-intensive task.</span></span> <span data-ttu-id="49db1-121">Hallo Hieronder volgt een voorbeeld van Hallo Java-toepassing uitgevoerd Hallo rekenintensieve taak.</span><span class="sxs-lookup"><span data-stu-id="49db1-121">hello following is an example of hello Java application running hello compute-intensive task.</span></span>

![Traveling verkoper probleem solver][solver_output]

<span data-ttu-id="49db1-123">Hallo Hier volgt een voorbeeld van een Java-toepassing hello rekenintensieve bewakingstaak Hallo.</span><span class="sxs-lookup"><span data-stu-id="49db1-123">hello following is an example of hello Java application monitoring hello compute-intensive task.</span></span>

![Traveling verkoper probleem client][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="49db1-125">toocreate een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="49db1-125">toocreate a virtual machine</span></span>
1. <span data-ttu-id="49db1-126">Meld u bij toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="49db1-126">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="49db1-127">Klik op **nieuw**, klikt u op **Compute**, klikt u op **virtuele machine**, en klik vervolgens op **uit galerie**.</span><span class="sxs-lookup"><span data-stu-id="49db1-127">Click **New**, click **Compute**, click **Virtual machine**, and then click **From Gallery**.</span></span>
3. <span data-ttu-id="49db1-128">In Hallo **virtuele machine-installatiekopie selecteert** dialoogvenster, **JDK 7 Windows Server 2012**.</span><span class="sxs-lookup"><span data-stu-id="49db1-128">In hello **Virtual machine image select** dialog box, select **JDK 7 Windows Server 2012**.</span></span>
   <span data-ttu-id="49db1-129">Houd er rekening mee dat **JDK 6 Windows Server 2012** beschikbaar is voor het geval u oudere toepassingen die nog niet klaar toorun in JDK 7 hebt.</span><span class="sxs-lookup"><span data-stu-id="49db1-129">Note that **JDK 6 Windows Server 2012** is available in case you have legacy applications that are not yet ready toorun in JDK 7.</span></span>
4. <span data-ttu-id="49db1-130">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="49db1-130">Click **Next**.</span></span>
5. <span data-ttu-id="49db1-131">In Hallo **Virtuele-machineconfiguratie** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="49db1-131">In hello **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="49db1-132">Geef een naam voor de Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49db1-132">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="49db1-133">Geef Hallo grootte toouse voor Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49db1-133">Specify hello size toouse for hello virtual machine.</span></span>
   3. <span data-ttu-id="49db1-134">Voer een naam voor Hallo beheerder in Hallo **gebruikersnaam** veld.</span><span class="sxs-lookup"><span data-stu-id="49db1-134">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="49db1-135">Deze naam en het Hallo-wachtwoord u naast voert, gebruikt u deze wanneer u op afstand toohello virtuele machine aanmelden.</span><span class="sxs-lookup"><span data-stu-id="49db1-135">Remember this name and hello password you will enter next, you will use them when you remotely log in toohello virtual machine.</span></span>
   4. <span data-ttu-id="49db1-136">Voer een wachtwoord in Hallo **nieuw wachtwoord** veld en voer deze opnieuw in Hallo **bevestigen** veld.</span><span class="sxs-lookup"><span data-stu-id="49db1-136">Enter a password in hello **New password** field, and re-enter it in hello **Confirm** field.</span></span> <span data-ttu-id="49db1-137">Dit is wachtwoord Hallo Administrator-account.</span><span class="sxs-lookup"><span data-stu-id="49db1-137">This is hello Administrator account password.</span></span>
   5. <span data-ttu-id="49db1-138">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="49db1-138">Click **Next**.</span></span>
6. <span data-ttu-id="49db1-139">In Hallo volgende **Virtuele-machineconfiguratie** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="49db1-139">In hello next **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="49db1-140">Voor **Cloudservice**, standaard-Hallo **Maak een nieuwe cloudservice**.</span><span class="sxs-lookup"><span data-stu-id="49db1-140">For **Cloud service**, use hello default **Create a new cloud service**.</span></span>
   2. <span data-ttu-id="49db1-141">waarde voor Hallo **Cloud service DNS-naam** uniek zijn binnen cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="49db1-141">hello value for **Cloud service DNS name** must be unique across cloudapp.net.</span></span> <span data-ttu-id="49db1-142">Indien nodig, wijzigt u deze waarde zodat deze Azure geeft dat deze uniek is.</span><span class="sxs-lookup"><span data-stu-id="49db1-142">If needed, modify this value so that Azure indicates it is unique.</span></span>
   3. <span data-ttu-id="49db1-143">Geef een regio, een affiniteitsgroep of een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="49db1-143">Specify a region, affinity group, or virtual network.</span></span> <span data-ttu-id="49db1-144">Geef voor deze zelfstudie een regio zoals **VS-West**.</span><span class="sxs-lookup"><span data-stu-id="49db1-144">For purposes of this tutorial, specify a region such as **West US**.</span></span>
   4. <span data-ttu-id="49db1-145">Voor **Opslagaccount**, selecteer **een automatisch gegenereerde opslagaccount gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="49db1-145">For **Storage Account**, select **Use an automatically generated storage account**.</span></span>
   5. <span data-ttu-id="49db1-146">Voor **Beschikbaarheidsset**, selecteer **(geen)**.</span><span class="sxs-lookup"><span data-stu-id="49db1-146">For **Availability Set**, select **(None)**.</span></span>
   6. <span data-ttu-id="49db1-147">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="49db1-147">Click **Next**.</span></span>
7. <span data-ttu-id="49db1-148">In de laatste Hallo **Virtuele-machineconfiguratie** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="49db1-148">In hello final **Virtual machine configuration** dialog box:</span></span>
   1. <span data-ttu-id="49db1-149">Hallo eindpunt standaardvermeldingen accepteren.</span><span class="sxs-lookup"><span data-stu-id="49db1-149">Accept hello default endpoint entries.</span></span>
   2. <span data-ttu-id="49db1-150">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="49db1-150">Click **Complete**.</span></span>

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a><span data-ttu-id="49db1-151">tooremotely aanmelden tooyour virtuele machine</span><span class="sxs-lookup"><span data-stu-id="49db1-151">tooremotely log in tooyour virtual machine</span></span>
1. <span data-ttu-id="49db1-152">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="49db1-152">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="49db1-153">Klik op **virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="49db1-153">Click **Virtual machines**.</span></span>
3. <span data-ttu-id="49db1-154">Klik op de naam Hallo van Hallo virtuele machine die u wilt toolog in.</span><span class="sxs-lookup"><span data-stu-id="49db1-154">Click hello name of hello virtual machine that you want toolog in to.</span></span>
4. <span data-ttu-id="49db1-155">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="49db1-155">Click **Connect**.</span></span>
5. <span data-ttu-id="49db1-156">Reageren op toohello prompts als benodigde tooconnect toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49db1-156">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="49db1-157">Desgevraagd Hallo beheerdersnaam en wachtwoord gebruiken Hallo-waarden die u hebt opgegeven toen u Hallo virtuele machine hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="49db1-157">When prompted for hello administrator name and password, use hello values that you provided when you created hello virtual machine.</span></span>

<span data-ttu-id="49db1-158">Opmerking die hello Azure Service Bus-functionaliteit vereist Hallo Baltimore CyberTrust Root certificate toobe geïnstalleerd als onderdeel van uw Java Runtime Environment **cacerts** opslaan.</span><span class="sxs-lookup"><span data-stu-id="49db1-158">Note that hello Azure Service Bus functionality requires hello Baltimore CyberTrust Root certificate toobe installed as part of your JRE's **cacerts** store.</span></span> <span data-ttu-id="49db1-159">Dit certificaat wordt automatisch opgenomen in Hallo Java Runtime Environment (JRE) die wordt gebruikt door deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="49db1-159">This certificate is automatically included in hello Java Runtime Environment (JRE) used by this tutorial.</span></span> <span data-ttu-id="49db1-160">Als u nog geen dit certificaat in uw JRE **cacerts** opslaat, Zie [toevoegen van een certificaat toohello Java CA-certificaatarchief] [ add_ca_cert] voor meer informatie over deze toe te voegen (evenals informatie over het Hallo-certificaten weergeven in uw archief cacerts).</span><span class="sxs-lookup"><span data-stu-id="49db1-160">If you do not have this certificate in your JRE **cacerts** store, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert] for information on adding it (as well as information on viewing hello certificates in your cacerts store).</span></span>

## <a name="how-toocreate-a-service-bus-namespace"></a><span data-ttu-id="49db1-161">Hoe toocreate een service bus naamruimte</span><span class="sxs-lookup"><span data-stu-id="49db1-161">How toocreate a service bus namespace</span></span>
<span data-ttu-id="49db1-162">toobegin met Service Bus-wachtrijen in Azure, moet u eerst een Servicenaamruimte maken.</span><span class="sxs-lookup"><span data-stu-id="49db1-162">toobegin using Service Bus queues in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="49db1-163">Een Servicenaamruimte biedt een scoping container voor het adresseren van Service Bus-resources in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="49db1-163">A service namespace provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="49db1-164">een Servicenaamruimte toocreate:</span><span class="sxs-lookup"><span data-stu-id="49db1-164">toocreate a service namespace:</span></span>

1. <span data-ttu-id="49db1-165">Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="49db1-165">Log on toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="49db1-166">Klik in het Hallo linksonder navigatiedeelvenster Hallo klassieke Azure-portal op **Service Bus, Access Control & opslaan in cache**.</span><span class="sxs-lookup"><span data-stu-id="49db1-166">In hello lower-left navigation pane of hello Azure classic portal, click **Service Bus, Access Control & Caching**.</span></span>
3. <span data-ttu-id="49db1-167">Klik in Hallo linksboven deelvenster Hallo klassieke Azure-portal op Hallo **Service Bus** knooppunt en klik vervolgens op Hallo **nieuw** knop.</span><span class="sxs-lookup"><span data-stu-id="49db1-167">In hello upper-left pane of hello Azure classic portal, click hello **Service Bus** node, and then click hello **New** button.</span></span>  
   <span data-ttu-id="49db1-168">![Schermafbeelding van de service Bus-knooppunt][svc_bus_node]</span><span class="sxs-lookup"><span data-stu-id="49db1-168">![Service Bus Node screenshot][svc_bus_node]</span></span>
4. <span data-ttu-id="49db1-169">In Hallo **maken van een nieuwe Service-Namespace** dialoogvenster Voer een **Namespace**, en klik vervolgens toomake ervoor dat deze uniek zijn, op de **beschikbaarheid controleren** knop.</span><span class="sxs-lookup"><span data-stu-id="49db1-169">In hello **Create a new Service Namespace** dialog box, enter a **Namespace**, and then toomake sure that it is unique, click the **Check Availability** button.</span></span>  
   <span data-ttu-id="49db1-170">![Maak een nieuwe Namespace-schermafbeelding][create_namespace]</span><span class="sxs-lookup"><span data-stu-id="49db1-170">![Create a New Namespace screenshot][create_namespace]</span></span>
5. <span data-ttu-id="49db1-171">Nadat u ervoor zorgt dat Hallo naamruimtenaam beschikbaar is, kiest u het land of regio waarin uw naamruimte moet worden gehost, en klik vervolgens op Hallo **Namespace maken** knop.</span><span class="sxs-lookup"><span data-stu-id="49db1-171">After making sure hello namespace name is available, choose the country or region in which your namespace should be hosted, and then click hello **Create Namespace** button.</span></span>  
   
   <span data-ttu-id="49db1-172">Hallo-naamruimte die u hebt gemaakt wordt vervolgens in de klassieke Azure-portal Hallo weergegeven en een tooactivate even duurt.</span><span class="sxs-lookup"><span data-stu-id="49db1-172">hello namespace you created will then appear in hello Azure classic portal and takes a moment tooactivate.</span></span> <span data-ttu-id="49db1-173">Wacht totdat de status Hallo **Active** voordat u doorgaat met de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="49db1-173">Wait until hello status is **Active** before continuing with hello next step.</span></span>

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a><span data-ttu-id="49db1-174">Hallo standaard Standaardbeheerreferenties voor Hallo-naamruimte ophalen</span><span class="sxs-lookup"><span data-stu-id="49db1-174">Obtain hello Default Management Credentials for hello namespace</span></span>
<span data-ttu-id="49db1-175">In de volgorde tooperform beheerbewerkingen, zoals het maken van een wachtrij op de nieuwe naamruimte hello, moet u tooobtain hello beheerreferenties voor de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="49db1-175">In order tooperform management operations, such as creating a queue, on hello new namespace, you need tooobtain hello management credentials for the namespace.</span></span>

1. <span data-ttu-id="49db1-176">Klik in de Hallo navigatiedeelvenster links op Hallo **Service Bus** knooppunt om Hallo lijst met beschikbare naamruimten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="49db1-176">In hello left navigation pane, click hello **Service Bus** node to display hello list of available namespaces.</span></span>
   <span data-ttu-id="49db1-177">![Schermafbeelding met beschikbare naamruimten][avail_namespaces]</span><span class="sxs-lookup"><span data-stu-id="49db1-177">![Available Namespaces screenshot][avail_namespaces]</span></span>
2. <span data-ttu-id="49db1-178">Selecteer Hallo naamruimte die u zojuist hebt gemaakt in Hallo lijst weergegeven.</span><span class="sxs-lookup"><span data-stu-id="49db1-178">Select hello namespace you just created from hello list shown.</span></span>
   <span data-ttu-id="49db1-179">![Lijst met Namespace-schermafbeelding][namespace_list]</span><span class="sxs-lookup"><span data-stu-id="49db1-179">![Namespace List screenshot][namespace_list]</span></span>
3. <span data-ttu-id="49db1-180">Hallo rechter **eigenschappen** deelvenster bevat Hallo-eigenschappen voor de nieuwe naamruimte.</span><span class="sxs-lookup"><span data-stu-id="49db1-180">hello right-hand **Properties** pane lists hello properties for the new namespace.</span></span>
   <span data-ttu-id="49db1-181">![Schermopname van eigenschappen deelvenster][properties_pane]</span><span class="sxs-lookup"><span data-stu-id="49db1-181">![Properties Pane screenshot][properties_pane]</span></span>
4. <span data-ttu-id="49db1-182">Hallo **standaard sleutel** wordt verborgen.</span><span class="sxs-lookup"><span data-stu-id="49db1-182">hello **Default Key** is hidden.</span></span> <span data-ttu-id="49db1-183">Klik op Hallo **weergave** knop toodisplay Hallo beveiligingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="49db1-183">Click hello **View** button toodisplay hello security credentials.</span></span>
   <span data-ttu-id="49db1-184">![Standaard-sleutel-schermafbeelding][default_key]</span><span class="sxs-lookup"><span data-stu-id="49db1-184">![Default Key screenshot][default_key]</span></span>
5. <span data-ttu-id="49db1-185">Maak een notitie van Hallo **verlener standaard** en Hallo **standaard sleutel** als u deze informatie hieronder tooperform operations met de naamruimte gebruiken gaat.</span><span class="sxs-lookup"><span data-stu-id="49db1-185">Make a note of hello **Default Issuer** and hello **Default Key** as you will use this information below tooperform operations with the namespace.</span></span>

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a><span data-ttu-id="49db1-186">Hoe toocreate een Java-toepassing die een taak rekenintensieve uitvoert</span><span class="sxs-lookup"><span data-stu-id="49db1-186">How toocreate a Java application that performs a compute-intensive task</span></span>
1. <span data-ttu-id="49db1-187">Op uw ontwikkelcomputer (waarvoor geen toobe Hallo virtuele machine die u hebt gemaakt), download Hallo [Azure SDK voor Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="49db1-187">On your development machine (which does not have toobe hello virtual machine that you created), download hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/).</span></span>
2. <span data-ttu-id="49db1-188">Maak een Java-consoletoepassing met voorbeeldcode Hallo aan Hallo einde van deze sectie.</span><span class="sxs-lookup"><span data-stu-id="49db1-188">Create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="49db1-189">In deze zelfstudie gebruiken we **TSPSolver.java** als Hallo Java-bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="49db1-189">In this tutorial, we'll use **TSPSolver.java** as hello Java file name.</span></span> <span data-ttu-id="49db1-190">Hallo wijzigen **uw\_service\_bus\_naamruimte**, **uw\_service\_bus\_eigenaar**, en **uw\_service\_bus\_sleutel** toouse tijdelijke aanduidingen voor uw servicebus **naamruimte**, **standaard verlener** en  **Standaard sleutel** waarden, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="49db1-190">Modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
3. <span data-ttu-id="49db1-191">Nadat de codering vereist export Hallo toepassing tooa uitvoerbare Java-archief (JAR) en pakket Hallo bibliotheken in Hallo JAR gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-191">After coding, export hello application tooa runnable Java archive (JAR), and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="49db1-192">In deze zelfstudie gebruiken we **TSPSolver.jar** als de naam van de JAR Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-192">In this tutorial, we'll use **TSPSolver.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a><span data-ttu-id="49db1-193">Hoe toocreate een Java-toepassing bewaakt de voortgang van Hallo rekenintensieve taak Hallo</span><span class="sxs-lookup"><span data-stu-id="49db1-193">How toocreate a Java application that monitors hello progress of hello compute-intensive task</span></span>
1. <span data-ttu-id="49db1-194">Maak een Java-consoletoepassing met voorbeeldcode Hallo op Hallo einde van dit gedeelte op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="49db1-194">On your development machine, create a Java console application using hello example code at hello end of this section.</span></span> <span data-ttu-id="49db1-195">In deze zelfstudie gebruiken we **TSPClient.java** als Hallo Java-bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="49db1-195">In this tutorial, we'll use **TSPClient.java** as hello Java file name.</span></span> <span data-ttu-id="49db1-196">Zoals eerder besproken, Hallo wijzigen **uw\_service\_bus\_naamruimte**, **uw\_service\_bus\_eigenaar**, en **uw\_service\_bus\_sleutel** toouse tijdelijke aanduidingen voor uw servicebus **naamruimte**, **standaard verlener**en **standaard sleutel** waarden, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="49db1-196">As shown earlier, modify hello **your\_service\_bus\_namespace**, **your\_service\_bus\_owner**, and **your\_service\_bus\_key** placeholders toouse your service bus **namespace**, **Default Issuer** and **Default Key** values, respectively.</span></span>
2. <span data-ttu-id="49db1-197">Hallo toepassing tooa exporteren uitvoerbare JAR en pakket Hallo vereist bibliotheken in Hallo JAR gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-197">Export hello application tooa runnable JAR, and package hello required libraries into hello generated JAR.</span></span> <span data-ttu-id="49db1-198">In deze zelfstudie gebruiken we **TSPClient.jar** als de naam van de JAR Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-198">In this tutorial, we'll use **TSPClient.jar** as hello generated JAR name.</span></span>

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a><span data-ttu-id="49db1-199">Hoe toorun Hallo Java-toepassingen</span><span class="sxs-lookup"><span data-stu-id="49db1-199">How toorun hello Java applications</span></span>
<span data-ttu-id="49db1-200">Hallo rekenintensieve toepassing uitvoert, Hallo eerste toocreate Hallo wachtrij vervolgens toosolve onderweg Saleseman probleem, waardoor Hallo huidige beste route toohello service bus-wachtrij wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="49db1-200">Run hello compute-intensive application, first toocreate hello queue, then toosolve hello Traveling Saleseman Problem, which will add hello current best route toohello service bus queue.</span></span> <span data-ttu-id="49db1-201">Tijdens het Hallo is rekenintensieve toepassing uitgevoerd (of later), Voer Hallo client toodisplay resultaten van Hallo service bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="49db1-201">While hello compute-intensive application is running (or afterwards), run hello client toodisplay results from hello service bus queue.</span></span>

### <a name="toorun-hello-compute-intensive-application"></a><span data-ttu-id="49db1-202">toorun hello rekenintensieve toepassing</span><span class="sxs-lookup"><span data-stu-id="49db1-202">toorun hello compute-intensive application</span></span>
1. <span data-ttu-id="49db1-203">Meld u aan tooyour virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="49db1-203">Log on tooyour virtual machine.</span></span>
2. <span data-ttu-id="49db1-204">Maak een map waar u uw toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-204">Create a folder where you will run your application.</span></span> <span data-ttu-id="49db1-205">Bijvoorbeeld: **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="49db1-205">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="49db1-206">Kopiëren **TSPSolver.jar** te**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="49db1-206">Copy **TSPSolver.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="49db1-207">Maak een bestand met de naam **c:\TSP\cities.txt** Hello inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="49db1-207">Create a file named **c:\TSP\cities.txt** with hello following contents.</span></span>
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. <span data-ttu-id="49db1-208">Wijzig de mappen tooc:\TSP bij een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="49db1-208">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="49db1-209">Zorg ervoor dat Hallo JRE de bin-map in omgevingsvariabele Hallo-PATH.</span><span class="sxs-lookup"><span data-stu-id="49db1-209">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
7. <span data-ttu-id="49db1-210">U moet toocreate Hallo service bus-wachtrij voordat u het aantal permutaties Hallo TSP solver uitvoert.</span><span class="sxs-lookup"><span data-stu-id="49db1-210">You'll need toocreate hello service bus queue before you run hello TSP solver permutations.</span></span> <span data-ttu-id="49db1-211">Hallo na de opdracht toocreate Hallo service bus-wachtrij worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-211">Run hello following command toocreate hello service bus queue.</span></span>
   
        java -jar TSPSolver.jar createqueue
8. <span data-ttu-id="49db1-212">Nu dat hello wachtrij wordt gemaakt, kunt u het aantal permutaties Hallo TSP solver kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="49db1-212">Now that hello queue is created, you can run hello TSP solver permutations.</span></span> <span data-ttu-id="49db1-213">Bijvoorbeeld: uitvoeren Hallo opdracht toorun Hallo solver voor 8 steden te volgen.</span><span class="sxs-lookup"><span data-stu-id="49db1-213">For example, run hello following command toorun hello solver for 8 cities.</span></span>
   
        java -jar TSPSolver.jar 8
   
   <span data-ttu-id="49db1-214">Als u niet een getal opgeeft, wordt deze uitgevoerd voor 10 steden.</span><span class="sxs-lookup"><span data-stu-id="49db1-214">If you don't specify a number, it will run for 10 cities.</span></span> <span data-ttu-id="49db1-215">Als Hallo solver huidige kortste routes wordt gevonden, wordt deze deze toohello wachtrij toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="49db1-215">As hello solver finds current shortest routes, it will add them toohello queue.</span></span>

> [!NOTE]
> <span data-ttu-id="49db1-216">Hallo groter Hallo nummer dat u opgeeft, Hallo langer Hallo solver wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-216">hello larger hello number that you specify, hello longer hello solver will run.</span></span> <span data-ttu-id="49db1-217">Bijvoorbeeld, actief 14 steden kunnen enkele minuten duren, en wordt uitgevoerd voor 15 steden kan enkele uren duren.</span><span class="sxs-lookup"><span data-stu-id="49db1-217">For example, running for 14 cities could take several minutes, and running for 15 cities could take several hours.</span></span> <span data-ttu-id="49db1-218">Verhogen too16 of meer plaatsen kan leiden tot dagen van de runtime (uiteindelijk weken, maanden en jaren).</span><span class="sxs-lookup"><span data-stu-id="49db1-218">Increasing too16 or more cities could result in days of runtime (eventually weeks, months, and years).</span></span> <span data-ttu-id="49db1-219">Dit is vanwege toohello snelle toename van het aantal permutaties geëvalueerd door Hallo solver als het aantal steden toeneemt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="49db1-219">This is due toohello rapid increase in hello number of permutations evaluated by hello solver as hello number of cities increases.</span></span>
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a><span data-ttu-id="49db1-220">Hoe toorun Hallo bewaking clienttoepassing</span><span class="sxs-lookup"><span data-stu-id="49db1-220">How toorun hello monitoring client application</span></span>
1. <span data-ttu-id="49db1-221">Meld u aan tooyour computer waar u de clienttoepassing hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-221">Log on tooyour machine where you will run hello client application.</span></span> <span data-ttu-id="49db1-222">Dit hoeft geen toobe dezelfde machine uitgevoerd Hallo Hallo **TSPSolver** toepassing, maar het kan zijn.</span><span class="sxs-lookup"><span data-stu-id="49db1-222">This does not need toobe hello same machine running hello **TSPSolver** application, although it can be.</span></span>
2. <span data-ttu-id="49db1-223">Maak een map waar u uw toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-223">Create a folder where you will run your application.</span></span> <span data-ttu-id="49db1-224">Bijvoorbeeld: **c:\TSP**.</span><span class="sxs-lookup"><span data-stu-id="49db1-224">For example, **c:\TSP**.</span></span>
3. <span data-ttu-id="49db1-225">Kopiëren **TSPClient.jar** te**c:\TSP**,</span><span class="sxs-lookup"><span data-stu-id="49db1-225">Copy **TSPClient.jar** too**c:\TSP**,</span></span>
4. <span data-ttu-id="49db1-226">Zorg ervoor dat Hallo JRE de bin-map in omgevingsvariabele Hallo-PATH.</span><span class="sxs-lookup"><span data-stu-id="49db1-226">Ensure hello JRE's bin folder is in hello PATH environment variable.</span></span>
5. <span data-ttu-id="49db1-227">Wijzig de mappen tooc:\TSP bij een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="49db1-227">At a command prompt, change directories tooc:\TSP.</span></span>
6. <span data-ttu-id="49db1-228">Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="49db1-228">Run hello following command.</span></span>
   
        java -jar TSPClient.jar
   
    <span data-ttu-id="49db1-229">Geef desgewenst Hallo aantal minuten toosleep bij het Hallo-wachtrij door door te geven in een opdrachtregelargument controleren.</span><span class="sxs-lookup"><span data-stu-id="49db1-229">Optionally, specify hello number of minutes toosleep in between checking hello queue, by passing in a command-line argument.</span></span> <span data-ttu-id="49db1-230">Hallo slaapstand standaardperiode voor het controleren van de wachtrij Hallo is 3 minuten, die wordt gebruikt als er geen opdrachtregelargument wordt doorgegeven, te**TSPClient**.</span><span class="sxs-lookup"><span data-stu-id="49db1-230">hello default sleep period for checking hello queue is 3 minutes, which is used if no command-line argument is passed too**TSPClient**.</span></span> <span data-ttu-id="49db1-231">Als u een andere waarde toouse voor hello slaapstand-interval wilt, bijvoorbeeld één minuut Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="49db1-231">If you want toouse a different value for hello sleep interval, for example, one minute, run hello following command.</span></span>
   
        java -jar TSPClient.jar 1
   
    <span data-ttu-id="49db1-232">Hallo-client wordt uitgevoerd totdat deze een wachtrijbericht van 'Voltooi' ziet.</span><span class="sxs-lookup"><span data-stu-id="49db1-232">hello client will run until it sees a queue message of "Complete".</span></span> <span data-ttu-id="49db1-233">Houd er rekening mee dat als u meerdere exemplaren van Hallo solver uitvoert zonder het Hallo-client uitvoert, u toorun Hallo client meerdere keren toocompletely leeg Hallo wachtrij moet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="49db1-233">Note that if you run multiple occurrences of hello solver without running hello client, you may need toorun hello client multiple times toocompletely empty hello queue.</span></span> <span data-ttu-id="49db1-234">U kunt ook Hallo wachtrij verwijderen en opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="49db1-234">Alternatively, you can delete hello queue and then create it again.</span></span> <span data-ttu-id="49db1-235">toodelete hello wachtrij op en voer de volgende Hallo **TSPSolver** (geen **TSPClient**) opdracht.</span><span class="sxs-lookup"><span data-stu-id="49db1-235">toodelete hello queue, run hello following **TSPSolver** (not **TSPClient**)  command.</span></span>
   
        java -jar TSPSolver.jar deletequeue
   
    <span data-ttu-id="49db1-236">Hallo solver wordt uitgevoerd totdat het klaar is met het onderzoeken van alle routes.</span><span class="sxs-lookup"><span data-stu-id="49db1-236">hello solver will run until it finishes examining all routes.</span></span>

## <a name="how-toostop-hello-java-applications"></a><span data-ttu-id="49db1-237">Hoe toostop Hallo Java-toepassingen</span><span class="sxs-lookup"><span data-stu-id="49db1-237">How toostop hello Java applications</span></span>
<span data-ttu-id="49db1-238">Voor Hallo solver en clienttoepassingen, drukt u op **Ctrl + C** tooexit als u wilt dat tooend voorafgaande toonormal voltooiing.</span><span class="sxs-lookup"><span data-stu-id="49db1-238">For both hello solver and client applications, you can press **Ctrl+C** tooexit if you want tooend prior toonormal completion.</span></span>

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md
