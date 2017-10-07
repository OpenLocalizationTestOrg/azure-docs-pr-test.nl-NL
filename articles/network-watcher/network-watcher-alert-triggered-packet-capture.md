---
title: netwerk-aaaUse pakket vastleggen toodo proactieve controle met waarschuwingen en Azure Functions | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate een waarschuwing geactiveerd pakketopname met Azure-netwerk-Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="9e8e8-103">Pakketopname voor proactieve netwerkbewaking met waarschuwingen en Azure Functions gebruiken</span><span class="sxs-lookup"><span data-stu-id="9e8e8-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="9e8e8-104">Netwerk-Watcher pakketopname maakt vastleggen sessies tootrack verkeer naar en vanuit virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-104">Network Watcher packet capture creates capture sessions tootrack traffic in and out of virtual machines.</span></span> <span data-ttu-id="9e8e8-105">Hallo vastleggen bestand hebben een filter dat is gedefinieerd tootrack Hallo alleen verkeer dat u wilt dat toomonitor.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-105">hello capture file can have a filter that is defined tootrack only hello traffic that you want toomonitor.</span></span> <span data-ttu-id="9e8e8-106">Deze gegevens worden vervolgens opgeslagen in een blob storage of lokaal op de gastmachine Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-106">This data is then stored in a storage blob or locally on hello guest machine.</span></span>

<span data-ttu-id="9e8e8-107">Deze mogelijkheid kan op afstand worden gestart vanuit andere automation-scenario's zoals Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="9e8e8-108">Pakket vastleggen biedt die u de mogelijkheid toorun proactieve opnamen op basis van Hallo gedefinieerd netwerk afwijkingen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-108">Packet capture gives you hello capability toorun proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="9e8e8-109">Andere toepassingen zijn onder andere netwerkstatistieken, informatie ophalen over het netwerk beveiligingsrisico's en foutopsporing client-servercommunicaties verzamelen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="9e8e8-110">Resources die zijn geïmplementeerd in Azure 24/7 worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="9e8e8-111">U en uw medewerkers kan actief Hallo status van alle bronnen 24/7 niet bewaken.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-111">You and your staff cannot actively monitor hello status of all resources 24/7.</span></span> <span data-ttu-id="9e8e8-112">Wat gebeurt bijvoorbeeld als er een probleem optreedt op 2 uur?</span><span class="sxs-lookup"><span data-stu-id="9e8e8-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="9e8e8-113">Met behulp van de netwerk-Watcher, waarschuwingen en functies van binnen hello Azure ecosysteem, kunt u proactief reageren met Hallo gegevens en hulpprogramma's voor toosolve problemen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-113">By using Network Watcher, alerting, and functions from within hello Azure ecosystem, you can proactively respond with hello data and tools toosolve problems in your network.</span></span>

![Scenario][scenario]

## <a name="prerequisites"></a><span data-ttu-id="9e8e8-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9e8e8-115">Prerequisites</span></span>

* <span data-ttu-id="9e8e8-116">meest recente versie van Hallo [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-116">hello latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="9e8e8-117">Een bestaand exemplaar van netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="9e8e8-118">Als u nog geen hebt, [geen exemplaar maken van netwerk-Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="9e8e8-119">Een bestaande virtuele machine in Hallo dezelfde regio bevinden als de netwerk-Watcher Hello [Windows extensie](../virtual-machines/windows/extensions-nwa.md) of [extensie van de virtuele machine Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-119">An existing virtual machine in hello same region as Network Watcher with hello [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="9e8e8-120">Scenario</span><span class="sxs-lookup"><span data-stu-id="9e8e8-120">Scenario</span></span>

<span data-ttu-id="9e8e8-121">In dit voorbeeld wordt de virtuele machine verzendt TCP-segmenten meer dan normaal en gewenste toobe gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-121">In this example, your VM is sending more TCP segments than usual, and you want toobe alerted.</span></span> <span data-ttu-id="9e8e8-122">TCP-segmenten als voorbeeld hier worden gebruikt, maar u kunt meldingsvoorwaarde.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="9e8e8-123">Wanneer u wordt gewaarschuwd, wilt u tooreceive pakketniveau gegevens toounderstand waarom communicatie is toegenomen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-123">When you are alerted, you want tooreceive packet-level data toounderstand why communication has increased.</span></span> <span data-ttu-id="9e8e8-124">Vervolgens kunt u stappen ondernemen tooreturn Hallo virtuele machine tooregular communicatie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-124">Then you can take steps tooreturn hello virtual machine tooregular communication.</span></span>

<span data-ttu-id="9e8e8-125">Dit scenario wordt ervan uitgegaan dat u een bestaand exemplaar van de netwerk-Watcher en een resourcegroep met een geldige virtuele machine hebt.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="9e8e8-126">Hallo lijst volgende is een overzicht van Hallo werkstroom die uitgevoerd wordt:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-126">hello following list is an overview of hello workflow that takes place:</span></span>

1. <span data-ttu-id="9e8e8-127">Een waarschuwing wordt geactiveerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="9e8e8-128">Hallo waarschuwing aanroepen uw Azure-functie via een webhook.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-128">hello alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="9e8e8-129">Uw Azure-functie Hallo waarschuwing verwerkt en wordt een netwerk-Watcher pakket capture-sessie gestart.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-129">Your Azure function processes hello alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="9e8e8-130">Hallo pakketopname op Hallo VM wordt uitgevoerd en verzamelt verkeer.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-130">hello packet capture runs on hello VM and collects traffic.</span></span>
1. <span data-ttu-id="9e8e8-131">Hallo pakket vastleggen bestand wordt geüpload tooa opslagaccount voor controle en diagnose.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-131">hello packet capture file is uploaded tooa storage account for review and diagnosis.</span></span>

<span data-ttu-id="9e8e8-132">tooautomate dit proces we maken en een verbinding maken met een waarschuwing op onze tootrigger VM wanneer Hallo incident voordoet.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-132">tooautomate this process, we create and connect an alert on our VM tootrigger when hello incident occurs.</span></span> <span data-ttu-id="9e8e8-133">We ook maken een functie toocall in netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-133">We also create a function toocall into Network Watcher.</span></span>

<span data-ttu-id="9e8e8-134">Dit scenario Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-134">This scenario does hello following:</span></span>

* <span data-ttu-id="9e8e8-135">Hiermee maakt u een Azure-functie die een pakketopname begint.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="9e8e8-136">Een waarschuwingsregel maakt op een virtuele machine en Hallo waarschuwingsregel toocall hello Azure functie configureert.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-136">Creates an alert rule on a virtual machine and configures hello alert rule toocall hello Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="9e8e8-137">Een Azure-functie maken</span><span class="sxs-lookup"><span data-stu-id="9e8e8-137">Create an Azure function</span></span>

<span data-ttu-id="9e8e8-138">de eerste stap Hallo toocreate is een Azure-functie tooprocess Hallo waarschuwing en een pakketopname maken.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-138">hello first step is toocreate an Azure function tooprocess hello alert and create a packet capture.</span></span>

1. <span data-ttu-id="9e8e8-139">In Hallo [Azure-portal](https://portal.azure.com), selecteer **nieuw** > **Compute** > **functie-App**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-139">In hello [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Een functie-app maken][1-1]

2. <span data-ttu-id="9e8e8-141">Op Hallo **functie-App** blade Voer Hallo waarden te volgen en selecteer vervolgens **OK** toocreate Hallo app:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-141">On hello **Function App** blade, enter hello following values, and then select **OK** toocreate hello app:</span></span>

    |<span data-ttu-id="9e8e8-142">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-142">**Setting**</span></span> | <span data-ttu-id="9e8e8-143">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-143">**Value**</span></span> | <span data-ttu-id="9e8e8-144">**Details**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="9e8e8-145">**Naam van app**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-145">**App name**</span></span>|<span data-ttu-id="9e8e8-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="9e8e8-146">PacketCaptureExample</span></span>|<span data-ttu-id="9e8e8-147">Hallo-naam van Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-147">hello name of hello function app.</span></span>|
    |<span data-ttu-id="9e8e8-148">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-148">**Subscription**</span></span>|<span data-ttu-id="9e8e8-149">[Uw abonnement] Hallo abonnement voor welke toocreate Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-149">[Your subscription]hello subscription for which toocreate hello function app.</span></span>||
    |<span data-ttu-id="9e8e8-150">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-150">**Resource Group**</span></span>|<span data-ttu-id="9e8e8-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="9e8e8-151">PacketCaptureRG</span></span>|<span data-ttu-id="9e8e8-152">Hallo resource groep toocontain Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-152">hello resource group toocontain hello function app.</span></span>|
    |<span data-ttu-id="9e8e8-153">**Hosting-Plan**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-153">**Hosting Plan**</span></span>|<span data-ttu-id="9e8e8-154">Plan voor verbruik</span><span class="sxs-lookup"><span data-stu-id="9e8e8-154">Consumption Plan</span></span>| <span data-ttu-id="9e8e8-155">Hallo type plan uw app functie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-155">hello type of plan your function app uses.</span></span> <span data-ttu-id="9e8e8-156">Opties zijn verbruik of Azure App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="9e8e8-157">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-157">**Location**</span></span>|<span data-ttu-id="9e8e8-158">VS - midden</span><span class="sxs-lookup"><span data-stu-id="9e8e8-158">Central US</span></span>| <span data-ttu-id="9e8e8-159">Hallo regio in welke toocreate Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-159">hello region in which toocreate hello function app.</span></span>|
    |<span data-ttu-id="9e8e8-160">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-160">**Storage Account**</span></span>|<span data-ttu-id="9e8e8-161">{automatisch gegenereerde}</span><span class="sxs-lookup"><span data-stu-id="9e8e8-161">{autogenerated}</span></span>| <span data-ttu-id="9e8e8-162">Hallo-opslagaccount waarvoor Azure Functions voor opslagaccounts voor algemeen gebruik.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-162">hello storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="9e8e8-163">Op Hallo **PacketCaptureExample functie Apps** blade Selecteer **functies** > **aangepaste functie**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-163">On hello **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="9e8e8-164">Selecteer **HttpTrigger Powershell**, en voer vervolgens de resterende gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-164">Select **HttpTrigger-Powershell**, and then enter hello remaining information.</span></span> <span data-ttu-id="9e8e8-165">Ten slotte toocreate Hallo functie, selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-165">Finally, toocreate hello function, select **Create**.</span></span>

    |<span data-ttu-id="9e8e8-166">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-166">**Setting**</span></span> | <span data-ttu-id="9e8e8-167">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-167">**Value**</span></span> | <span data-ttu-id="9e8e8-168">**Details**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="9e8e8-169">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-169">**Scenario**</span></span>|<span data-ttu-id="9e8e8-170">experimentele</span><span class="sxs-lookup"><span data-stu-id="9e8e8-170">Experimental</span></span>|<span data-ttu-id="9e8e8-171">Type van scenario</span><span class="sxs-lookup"><span data-stu-id="9e8e8-171">Type of scenario</span></span>|
    |<span data-ttu-id="9e8e8-172">**Een naam voor de functie opgeven**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-172">**Name your function**</span></span>|<span data-ttu-id="9e8e8-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="9e8e8-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="9e8e8-174">Naam van de functie Hallo</span><span class="sxs-lookup"><span data-stu-id="9e8e8-174">Name of hello function</span></span>|
    |<span data-ttu-id="9e8e8-175">**Machtigingsniveau**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-175">**Authorization level**</span></span>|<span data-ttu-id="9e8e8-176">Functie</span><span class="sxs-lookup"><span data-stu-id="9e8e8-176">Function</span></span>|<span data-ttu-id="9e8e8-177">Autorisatieniveau voor Hallo-functie</span><span class="sxs-lookup"><span data-stu-id="9e8e8-177">Authorization level for hello function</span></span>|

![Voorbeeld van de functies][functions1]

> [!NOTE]
> <span data-ttu-id="9e8e8-179">Hallo PowerShell sjabloon experimentele is en geen volledige ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-179">hello PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="9e8e8-180">Aanpassingen zijn vereist voor dit voorbeeld en worden beschreven in Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-180">Customizations are required for this example and are explained in hello following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="9e8e8-181">Modules toevoegen</span><span class="sxs-lookup"><span data-stu-id="9e8e8-181">Add modules</span></span>

<span data-ttu-id="9e8e8-182">toouse netwerk-Watcher PowerShell-cmdlets Hallo nieuwste PowerShell-module toohello functie app uploaden.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-182">toouse Network Watcher PowerShell cmdlets, upload hello latest PowerShell module toohello function app.</span></span>

1. <span data-ttu-id="9e8e8-183">Voer op uw lokale computer met de Hallo nieuwste Azure PowerShell-modules geïnstalleerd Hallo volgende PowerShell-opdracht:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-183">On your local machine with hello latest Azure PowerShell modules installed, run hello following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="9e8e8-184">Dit voorbeeld kunt u het lokale pad naar uw Azure PowerShell-modules Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-184">This example gives you hello local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="9e8e8-185">Deze mappen worden gebruikt in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-185">These folders are used in a later step.</span></span> <span data-ttu-id="9e8e8-186">Hallo-modules die worden gebruikt in dit scenario zijn:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-186">hello modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="9e8e8-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="9e8e8-187">AzureRM.Network</span></span>

    * <span data-ttu-id="9e8e8-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="9e8e8-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="9e8e8-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="9e8e8-189">AzureRM.Resources</span></span>

    ![PowerShell-mappen][functions5]

1. <span data-ttu-id="9e8e8-191">Selecteer **werken app-instellingen** > **tooApp Service Editor gaat**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-191">Select **Function app settings** > **Go tooApp Service Editor**.</span></span>

    ![De functie app-instellingen][functions2]

1. <span data-ttu-id="9e8e8-193">Klik met de rechtermuisknop Hallo **AlertPacketCapturePowershell** map, en maak vervolgens een map met de naam **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-193">Right-click hello **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="9e8e8-194">Maak een submap voor elke module die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-194">Create a subfolder for each module that you need.</span></span>

    ![Map en submappen][functions3]

    * <span data-ttu-id="9e8e8-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="9e8e8-196">AzureRM.Network</span></span>

    * <span data-ttu-id="9e8e8-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="9e8e8-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="9e8e8-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="9e8e8-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="9e8e8-199">Klik met de rechtermuisknop Hallo **AzureRM.Network** submap en selecteer vervolgens **bestanden uploaden**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-199">Right-click hello **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="9e8e8-200">Ga tooyour Azure modules.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-200">Go tooyour Azure modules.</span></span> <span data-ttu-id="9e8e8-201">In de lokale Hallo **AzureRM.Network** map, selecteert u alle Hallo-bestanden in Hallo-map.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-201">In hello local **AzureRM.Network** folder, select all hello files in hello folder.</span></span> <span data-ttu-id="9e8e8-202">Selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="9e8e8-203">Herhaal deze stappen voor **AzureRM.Profile** en **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Bestanden uploaden][functions6]

1. <span data-ttu-id="9e8e8-205">Nadat u klaar bent, elke map moet Hallo PowerShell-module bestanden naar uw lokale machine hebben.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-205">After you've finished, each folder should have hello PowerShell module files from your local machine.</span></span>

    ![Bestanden met PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="9e8e8-207">Authentication</span><span class="sxs-lookup"><span data-stu-id="9e8e8-207">Authentication</span></span>

<span data-ttu-id="9e8e8-208">toouse hello PowerShell-cmdlets die u moet verifiëren.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-208">toouse hello PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="9e8e8-209">U configureren verificatie in Hallo functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-209">You configure authentication in hello function app.</span></span> <span data-ttu-id="9e8e8-210">tooconfigure verificatie, moet u omgevingsvariabelen configureren en een versleutelde sleutelbestand toohello functie-app uploaden.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-210">tooconfigure authentication, you must configure environment variables and upload an encrypted key file toohello function app.</span></span>

> [!NOTE]
> <span data-ttu-id="9e8e8-211">Dit scenario biedt één voorbeeld van hoe u tooimplement verificatie met Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-211">This scenario provides just one example of how tooimplement authentication with Azure Functions.</span></span> <span data-ttu-id="9e8e8-212">Er zijn andere manieren toodo dit.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-212">There are other ways toodo this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="9e8e8-213">Versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="9e8e8-213">Encrypted credentials</span></span>

<span data-ttu-id="9e8e8-214">Hallo volgende PowerShell-script maakt een sleutelbestand aangeroepen **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-214">hello following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="9e8e8-215">Het bevat ook een versleutelde versie van Hallo wachtwoord dat wordt meegeleverd.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-215">It also provides an encrypted version of hello password that's supplied.</span></span> <span data-ttu-id="9e8e8-216">Dit wachtwoord wordt Hallo hetzelfde wachtwoord dat is gedefinieerd voor hello Azure Active Directory-toepassing die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-216">This password is hello same password that is defined for hello Azure Active Directory application that's used for authentication.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

<span data-ttu-id="9e8e8-217">Maak een map met de naam in App Service-Editor van functie-app Hallo Hallo, **sleutels** onder **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-217">In hello App Service Editor of hello function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="9e8e8-218">Vervolgens uploaden Hallo **PassEncryptKey.key** -bestand dat u hebt gemaakt in de vorige PowerShell-voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-218">Then upload hello **PassEncryptKey.key** file that you created in hello previous PowerShell sample.</span></span>

![Functies sleutel][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="9e8e8-220">Waarden voor omgevingsvariabelen ophalen</span><span class="sxs-lookup"><span data-stu-id="9e8e8-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="9e8e8-221">de laatste vereiste Hallo is tooset up Hallo omgevingsvariabelen die nodig zijn tooaccess Hallo waarden voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-221">hello final requirement is tooset up hello environment variables that are necessary tooaccess hello values for authentication.</span></span> <span data-ttu-id="9e8e8-222">Hallo bevat volgende lijst Hallo omgevingsvariabelen die zijn gemaakt:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-222">hello following list shows hello environment variables that are created:</span></span>

* <span data-ttu-id="9e8e8-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="9e8e8-223">AzureClientID</span></span>

* <span data-ttu-id="9e8e8-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="9e8e8-224">AzureTenant</span></span>

* <span data-ttu-id="9e8e8-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="9e8e8-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="9e8e8-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="9e8e8-226">AzureClientID</span></span>

<span data-ttu-id="9e8e8-227">Hallo client-ID is Hallo toepassings-ID van een toepassing in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-227">hello client ID is hello Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="9e8e8-228">Als u een toepassing toouse nog geen hebt, een toepassing uitvoeren Hallo toocreate voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-228">If you don't already have an application toouse, run hello following example toocreate an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="9e8e8-229">Hallo-wachtwoord dat u bij het maken van de toepassing hello moet Hallo hetzelfde wachtwoord dat u eerder hebt gemaakt bij het opslaan van Hallo-sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-229">hello password that you use when creating hello application should be hello same password that you created earlier when saving hello key file.</span></span>

1. <span data-ttu-id="9e8e8-230">Selecteer in de Azure-portal hello, **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-230">In hello Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="9e8e8-231">Hallo abonnement toouse selecteren en selecteer vervolgens **toegangsbeheer (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-231">Select hello subscription toouse, and then select **Access control (IAM)**.</span></span>

    ![De IAM-functies][functions9]

1. <span data-ttu-id="9e8e8-233">Kies Hallo account toouse en selecteer vervolgens **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-233">Choose hello account toouse, and then select **Properties**.</span></span> <span data-ttu-id="9e8e8-234">Kopieer Hallo toepassing-ID.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-234">Copy hello Application ID.</span></span>

    ![Functies toepassings-ID][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="9e8e8-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="9e8e8-236">AzureTenant</span></span>

<span data-ttu-id="9e8e8-237">Hallo tenant-ID verkrijgen door het volgende PowerShell-voorbeeld Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-237">Obtain hello tenant ID  by running hello following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="9e8e8-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="9e8e8-238">AzureCredPassword</span></span>

<span data-ttu-id="9e8e8-239">Hallo-waarde van Hallo AzureCredPassword omgevingsvariabele is Hallo-waarde die u via de volgende PowerShell-voorbeeld Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-239">hello value of hello AzureCredPassword environment variable is hello value that you get from running hello following PowerShell sample.</span></span> <span data-ttu-id="9e8e8-240">In dit voorbeeld is dezelfde als die wordt weergegeven in de voorgaande Hallo Hallo **versleuteld referenties** sectie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-240">This example is hello same one that's shown in hello preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="9e8e8-241">Hallo-waarde die is er nodig is de uitvoer van de Hallo van Hallo `$Encryptedpassword` variabele.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-241">hello value that's needed is hello output of hello `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="9e8e8-242">Dit is Hallo service principal wachtwoord die u met behulp van PowerShell-script Hallo versleuteld.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-242">This is hello service principal password that you encrypted by using hello PowerShell script.</span></span>

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a><span data-ttu-id="9e8e8-243">Hallo omgevingsvariabelen opslaan</span><span class="sxs-lookup"><span data-stu-id="9e8e8-243">Store hello environment variables</span></span>

1. <span data-ttu-id="9e8e8-244">Ga toohello functie-app.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-244">Go toohello function app.</span></span> <span data-ttu-id="9e8e8-245">Selecteer vervolgens **werken app-instellingen** > **app-instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![App-instellingen configureren][functions11]

1. <span data-ttu-id="9e8e8-247">Hallo omgevingsvariabelen en hun waarden toohello app-instellingen toevoegen en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-247">Add hello environment variables and their values toohello app settings, and then select **Save**.</span></span>

    ![App-instellingen][functions12]

### <a name="add-powershell-toohello-function"></a><span data-ttu-id="9e8e8-249">PowerShell toohello functie toevoegen</span><span class="sxs-lookup"><span data-stu-id="9e8e8-249">Add PowerShell toohello function</span></span>

<span data-ttu-id="9e8e8-250">Het is nu tijd toomake in netwerk-Watcher van binnen hello Azure-functie aanroepen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-250">It's now time toomake calls into Network Watcher from within hello Azure function.</span></span> <span data-ttu-id="9e8e8-251">Afhankelijk van de vereisten voor Hallo kan Hallo uitvoering van deze functie variëren.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-251">Depending on hello requirements, hello implementation of this function can vary.</span></span> <span data-ttu-id="9e8e8-252">De algemene stroom Hallo Hallo code is echter als volgt:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-252">However, hello general flow of hello code is as follows:</span></span>

1. <span data-ttu-id="9e8e8-253">Proces-invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-253">Process input parameters.</span></span>
2. <span data-ttu-id="9e8e8-254">Het bestaande pakket query tooverify limieten vastgelegd en Naamconflicten oplossen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-254">Query existing packet captures tooverify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="9e8e8-255">Maak een pakketopname met toepasselijke parameters.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="9e8e8-256">Poll-pakket vastleggen periodiek totdat deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="9e8e8-257">Gebruiker een melding Hallo Hallo pakket opnamesessie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-257">Notify hello user that hello packet capture session is complete.</span></span>

<span data-ttu-id="9e8e8-258">Hallo is volgende voorbeeld PowerShell-code die kan worden gebruikt in Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-258">hello following example is PowerShell code that can be used in hello function.</span></span> <span data-ttu-id="9e8e8-259">Er zijn waarden die vervangen moeten voor toobe **subscriptionId**, **resourceGroupName**, en **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-259">There are values that need toobe replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a><span data-ttu-id="9e8e8-260">Hallo functie URL niet ophalen</span><span class="sxs-lookup"><span data-stu-id="9e8e8-260">Retrieve hello function URL</span></span> 
1. <span data-ttu-id="9e8e8-261">Nadat u uw functie hebt gemaakt, configureert u uw waarschuwing toocall Hallo-URL die is gekoppeld aan het Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-261">After you've created your function, configure your alert toocall hello URL that's associated with hello function.</span></span> <span data-ttu-id="9e8e8-262">tooget deze waarde kopiëren Hallo function URL van uw app functie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-262">tooget this value, copy hello function URL from your function app.</span></span>

    ![Hallo function URL zoeken][functions13]

2. <span data-ttu-id="9e8e8-264">Kopieer Hallo functie URL voor uw app functie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-264">Copy hello function URL for your function app.</span></span>

    ![Hallo function URL kopiëren][2]

<span data-ttu-id="9e8e8-266">Als u aangepaste eigenschappen in de nettolading Hallo van Hallo webhook POST-aanvraag nodig hebt, raadpleeg dan te[een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-266">If you require custom properties in hello payload of hello webhook POST request, refer too[Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="9e8e8-267">Een waarschuwing te configureren op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="9e8e8-267">Configure an alert on a VM</span></span>

<span data-ttu-id="9e8e8-268">Waarschuwingen geconfigureerde toonotify personen kunnen zijn wanneer specifieke metrische gegevens overschrijdt de drempelwaarde die toegewezen tooit.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-268">Alerts can be configured toonotify individuals when a specific metric crosses a threshold that's assigned tooit.</span></span> <span data-ttu-id="9e8e8-269">In dit voorbeeld Hallo waarschuwing is op Hallo van TCP-segmenten die worden verzonden, maar Hallo-waarschuwing voor veel andere metrische gegevens kan worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-269">In this example, hello alert is on hello TCP segments that are sent, but hello alert can be triggered for many other metrics.</span></span> <span data-ttu-id="9e8e8-270">In dit voorbeeld wordt een waarschuwing geconfigureerde toocall een webhook toocall Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-270">In this example, an alert is configured toocall a webhook toocall hello function.</span></span>

### <a name="create-hello-alert-rule"></a><span data-ttu-id="9e8e8-271">Hallo waarschuwingsregel maken</span><span class="sxs-lookup"><span data-stu-id="9e8e8-271">Create hello alert rule</span></span>

<span data-ttu-id="9e8e8-272">Ga tooan bestaande virtuele machine en vervolgens een waarschuwingsregel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-272">Go tooan existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="9e8e8-273">Meer gedetailleerde documentatie over het configureren van waarschuwingen kan worden gevonden op [waarschuwingen in de Azure-Monitor maken voor Azure-services - Azure-portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="9e8e8-274">Voer Hallo volgende waarden in Hallo **waarschuwingsregel** blade en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-274">Enter hello following values in hello **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="9e8e8-275">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-275">**Setting**</span></span> | <span data-ttu-id="9e8e8-276">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-276">**Value**</span></span> | <span data-ttu-id="9e8e8-277">**Details**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="9e8e8-278">**Naam**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-278">**Name**</span></span>|<span data-ttu-id="9e8e8-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="9e8e8-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="9e8e8-280">Naam van de waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-280">Name of hello alert rule.</span></span>|
  |<span data-ttu-id="9e8e8-281">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-281">**Description**</span></span>|<span data-ttu-id="9e8e8-282">TCP-segmenten verzonden drempelwaarde overschreden</span><span class="sxs-lookup"><span data-stu-id="9e8e8-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="9e8e8-283">Hallo beschrijving voor de waarschuwingsregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-283">hello description for hello alert rule.</span></span>||
  |<span data-ttu-id="9e8e8-284">**Gegevens**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-284">**Metric**</span></span>|<span data-ttu-id="9e8e8-285">TCP-segmenten die zijn verzonden</span><span class="sxs-lookup"><span data-stu-id="9e8e8-285">TCP segments sent</span></span>| <span data-ttu-id="9e8e8-286">Hallo metrische toouse tootrigger Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-286">hello metric toouse tootrigger hello alert.</span></span> |
  |<span data-ttu-id="9e8e8-287">**Voorwaarde**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-287">**Condition**</span></span>|<span data-ttu-id="9e8e8-288">Groter dan</span><span class="sxs-lookup"><span data-stu-id="9e8e8-288">Greater than</span></span>| <span data-ttu-id="9e8e8-289">Hallo voorwaarde toouse bij het evalueren van Hallo metriek.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-289">hello condition toouse when evaluating hello metric.</span></span>|
  |<span data-ttu-id="9e8e8-290">**Drempelwaarde**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-290">**Threshold**</span></span>|<span data-ttu-id="9e8e8-291">100</span><span class="sxs-lookup"><span data-stu-id="9e8e8-291">100</span></span>| <span data-ttu-id="9e8e8-292">Hallo-waarde van Hallo metriek die Hallo waarschuwing activeert.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-292">hello  value of hello metric that triggers hello alert.</span></span> <span data-ttu-id="9e8e8-293">Deze waarde moet worden ingesteld als tooa geldige waarde voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-293">This value should be set tooa valid value for your environment.</span></span>|
  |<span data-ttu-id="9e8e8-294">**Periode**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-294">**Period**</span></span>|<span data-ttu-id="9e8e8-295">Via Hallo laatste vijf minuten</span><span class="sxs-lookup"><span data-stu-id="9e8e8-295">Over hello last five minutes</span></span>| <span data-ttu-id="9e8e8-296">Hallo periode in welke toolook voor Hallo drempelwaarde op Hallo metriek bepaalt.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-296">Determines hello period in which toolook for hello threshold on hello metric.</span></span>|
  |<span data-ttu-id="9e8e8-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="9e8e8-297">**Webhook**</span></span>|<span data-ttu-id="9e8e8-298">[webhook-URL van de functie-app]</span><span class="sxs-lookup"><span data-stu-id="9e8e8-298">[webhook URL from function app]</span></span>| <span data-ttu-id="9e8e8-299">Hallo webhook-URL van Hallo functie-app die is gemaakt in de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-299">hello webhook URL from hello function app that was created in hello previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="9e8e8-300">Hallo TCP-segmenten metriek is niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-300">hello TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="9e8e8-301">Meer informatie over het tooenable aanvullende gegevens in via [inschakelen bewaking en diagnostische gegevens](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-301">Learn more about how tooenable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-hello-results"></a><span data-ttu-id="9e8e8-302">Bekijkt hello resultaten</span><span class="sxs-lookup"><span data-stu-id="9e8e8-302">Review hello results</span></span>

<span data-ttu-id="9e8e8-303">Na het Hallo-criteria voor de waarschuwing triggers hello, wordt het vastleggen van een pakket gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-303">After hello criteria for hello alert triggers, a packet capture is created.</span></span> <span data-ttu-id="9e8e8-304">Ga tooNetwork Watcher en selecteer vervolgens **pakketopname**.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-304">Go tooNetwork Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="9e8e8-305">Op deze pagina kunt u Hallo pakket vastleggen bestand koppeling toodownload hello pakketopname selecteren.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-305">On this page, you can select hello packet capture file link toodownload hello packet capture.</span></span>

![Weergave pakketopname][functions14]

<span data-ttu-id="9e8e8-307">Als Hallo vastleggen bestand lokaal is opgeslagen, kunt u deze ophalen door in toohello virtuele machine te ondertekenen.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-307">If hello capture file is stored locally, you can retrieve it by signing in toohello virtual machine.</span></span>

<span data-ttu-id="9e8e8-308">Zie voor instructies over het downloaden van bestanden van Azure storage-accounts [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="9e8e8-309">Een ander hulpprogramma kunt u is [Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="9e8e8-310">Nadat het vastleggen is gedownload, kunt u deze bekijken met behulp van een hulpprogramma dat gelezen kan een **CAP** bestand.</span><span class="sxs-lookup"><span data-stu-id="9e8e8-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="9e8e8-311">Hieronder vindt u koppelingen tootwo van deze hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="9e8e8-311">Following are links tootwo of these tools:</span></span>

- [<span data-ttu-id="9e8e8-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="9e8e8-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="9e8e8-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="9e8e8-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="9e8e8-314">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9e8e8-314">Next steps</span></span>

<span data-ttu-id="9e8e8-315">Meer informatie over hoe tooview uw pakket worden vastgelegd in via [pakket netwerkopname-analyse met Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="9e8e8-315">Learn how tooview your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
