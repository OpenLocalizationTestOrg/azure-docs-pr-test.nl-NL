---
title: Gebruik pakketopname voor proactieve netwerkbewaking met waarschuwingen en Azure Functions | Microsoft Docs
description: Dit artikel wordt beschreven hoe u een waarschuwing geactiveerd pakketopname maakt met Azure-netwerk-Watcher
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
ms.openlocfilehash: b813172fc1fc1cc683f463f05370c95bfec10f8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a><span data-ttu-id="8d148-103">Pakketopname voor proactieve netwerkbewaking met waarschuwingen en Azure Functions gebruiken</span><span class="sxs-lookup"><span data-stu-id="8d148-103">Use packet capture for proactive network monitoring with alerts and Azure Functions</span></span>

<span data-ttu-id="8d148-104">Netwerk-Watcher pakketopname maakt vastleggen sessies om bij te houden van verkeer van en naar virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="8d148-104">Network Watcher packet capture creates capture sessions to track traffic in and out of virtual machines.</span></span> <span data-ttu-id="8d148-105">Het bestand vastleggen hebben een filter dat is gedefinieerd om bij te houden, alleen het verkeer dat u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="8d148-105">The capture file can have a filter that is defined to track only the traffic that you want to monitor.</span></span> <span data-ttu-id="8d148-106">Deze gegevens worden vervolgens opgeslagen in een blob storage of lokaal op de gastmachine.</span><span class="sxs-lookup"><span data-stu-id="8d148-106">This data is then stored in a storage blob or locally on the guest machine.</span></span>

<span data-ttu-id="8d148-107">Deze mogelijkheid kan op afstand worden gestart vanuit andere automation-scenario's zoals Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="8d148-107">This capability can be started remotely from other automation scenarios such as Azure Functions.</span></span> <span data-ttu-id="8d148-108">Pakketopname biedt u de mogelijkheid om uit te voeren proactieve opnamen op basis van gedefinieerde netwerk afwijkingen.</span><span class="sxs-lookup"><span data-stu-id="8d148-108">Packet capture gives you the capability to run proactive captures based on defined network anomalies.</span></span> <span data-ttu-id="8d148-109">Andere toepassingen zijn onder andere netwerkstatistieken, informatie ophalen over het netwerk beveiligingsrisico's en foutopsporing client-servercommunicaties verzamelen.</span><span class="sxs-lookup"><span data-stu-id="8d148-109">Other uses include gathering network statistics, getting information about network intrusions, debugging client-server communications, and more.</span></span>

<span data-ttu-id="8d148-110">Resources die zijn geïmplementeerd in Azure 24/7 worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8d148-110">Resources that are deployed in Azure run 24/7.</span></span> <span data-ttu-id="8d148-111">U en uw medewerkers kan niet de status van alle resources 24/7 actief bewaken.</span><span class="sxs-lookup"><span data-stu-id="8d148-111">You and your staff cannot actively monitor the status of all resources 24/7.</span></span> <span data-ttu-id="8d148-112">Wat gebeurt bijvoorbeeld als er een probleem optreedt op 2 uur?</span><span class="sxs-lookup"><span data-stu-id="8d148-112">For example, what happens if an issue occurs at 2 AM?</span></span>

<span data-ttu-id="8d148-113">Met behulp van de netwerk-Watcher, waarschuwingen en functies van binnen het Azure-ecosysteem, kunt u proactief reageren met de gegevens en hulpmiddelen voor het oplossen van problemen in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="8d148-113">By using Network Watcher, alerting, and functions from within the Azure ecosystem, you can proactively respond with the data and tools to solve problems in your network.</span></span>

![Scenario][scenario]

## <a name="prerequisites"></a><span data-ttu-id="8d148-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8d148-115">Prerequisites</span></span>

* <span data-ttu-id="8d148-116">De nieuwste versie van [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="8d148-116">The latest version of [Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
* <span data-ttu-id="8d148-117">Een bestaand exemplaar van netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="8d148-117">An existing instance of Network Watcher.</span></span> <span data-ttu-id="8d148-118">Als u nog geen hebt, [geen exemplaar maken van netwerk-Watcher](network-watcher-create.md).</span><span class="sxs-lookup"><span data-stu-id="8d148-118">If you don't already have one, [create an instance of Network Watcher](network-watcher-create.md).</span></span>
* <span data-ttu-id="8d148-119">Een bestaande virtuele machine in dezelfde regio bevinden als de netwerk-Watcher met de [Windows extensie](../virtual-machines/windows/extensions-nwa.md) of [extensie van de virtuele machine Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="8d148-119">An existing virtual machine in the same region as Network Watcher with the [Windows extension](../virtual-machines/windows/extensions-nwa.md) or [Linux virtual machine extension](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="scenario"></a><span data-ttu-id="8d148-120">Scenario</span><span class="sxs-lookup"><span data-stu-id="8d148-120">Scenario</span></span>

<span data-ttu-id="8d148-121">In dit voorbeeld wordt de virtuele machine verzendt TCP-segmenten meer dan normaal en u wilt worden gewaarschuwd.</span><span class="sxs-lookup"><span data-stu-id="8d148-121">In this example, your VM is sending more TCP segments than usual, and you want to be alerted.</span></span> <span data-ttu-id="8d148-122">TCP-segmenten als voorbeeld hier worden gebruikt, maar u kunt meldingsvoorwaarde.</span><span class="sxs-lookup"><span data-stu-id="8d148-122">TCP segments are used as an example here, but you can use any alert condition.</span></span>

<span data-ttu-id="8d148-123">Wanneer u wordt gewaarschuwd, die u wilt ontvangen pakketniveau gegevens om te begrijpen waarom communicatie is toegenomen.</span><span class="sxs-lookup"><span data-stu-id="8d148-123">When you are alerted, you want to receive packet-level data to understand why communication has increased.</span></span> <span data-ttu-id="8d148-124">U kunt vervolgens de stappen voor de virtuele machine terug naar normale communicatie nemen.</span><span class="sxs-lookup"><span data-stu-id="8d148-124">Then you can take steps to return the virtual machine to regular communication.</span></span>

<span data-ttu-id="8d148-125">Dit scenario wordt ervan uitgegaan dat u een bestaand exemplaar van de netwerk-Watcher en een resourcegroep met een geldige virtuele machine hebt.</span><span class="sxs-lookup"><span data-stu-id="8d148-125">This scenario assumes that you have an existing instance of Network Watcher and a resource group with a valid virtual machine.</span></span>

<span data-ttu-id="8d148-126">De volgende lijst bevat een overzicht van de werkstroom die uitgevoerd wordt:</span><span class="sxs-lookup"><span data-stu-id="8d148-126">The following list is an overview of the workflow that takes place:</span></span>

1. <span data-ttu-id="8d148-127">Een waarschuwing wordt geactiveerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d148-127">An alert is triggered on your VM.</span></span>
1. <span data-ttu-id="8d148-128">De waarschuwing aanroepen uw Azure-functie via een webhook.</span><span class="sxs-lookup"><span data-stu-id="8d148-128">The alert calls your Azure function via a webhook.</span></span>
1. <span data-ttu-id="8d148-129">Uw Azure-functie verwerkt de waarschuwing en wordt een netwerk-Watcher pakket capture-sessie gestart.</span><span class="sxs-lookup"><span data-stu-id="8d148-129">Your Azure function processes the alert and starts a Network Watcher packet capture session.</span></span>
1. <span data-ttu-id="8d148-130">Het vastleggen van het pakket wordt uitgevoerd op de virtuele machine en verzamelt verkeer.</span><span class="sxs-lookup"><span data-stu-id="8d148-130">The packet capture runs on the VM and collects traffic.</span></span>
1. <span data-ttu-id="8d148-131">Het pakket capture-bestand wordt geüpload naar een opslagaccount voor controle en diagnose.</span><span class="sxs-lookup"><span data-stu-id="8d148-131">The packet capture file is uploaded to a storage account for review and diagnosis.</span></span>

<span data-ttu-id="8d148-132">Als u wilt automatiseren, we maken en verbinding maken met een waarschuwing op onze VM voor het geval van het incident activeren.</span><span class="sxs-lookup"><span data-stu-id="8d148-132">To automate this process, we create and connect an alert on our VM to trigger when the incident occurs.</span></span> <span data-ttu-id="8d148-133">We ook maken een functie aan te roepen netwerk-Watcher.</span><span class="sxs-lookup"><span data-stu-id="8d148-133">We also create a function to call into Network Watcher.</span></span>

<span data-ttu-id="8d148-134">Dit scenario doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="8d148-134">This scenario does the following:</span></span>

* <span data-ttu-id="8d148-135">Hiermee maakt u een Azure-functie die een pakketopname begint.</span><span class="sxs-lookup"><span data-stu-id="8d148-135">Creates an Azure function that starts a packet capture.</span></span>
* <span data-ttu-id="8d148-136">Een waarschuwingsregel maakt op een virtuele machine en configureert u de waarschuwingsregel voor het aanroepen van de Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="8d148-136">Creates an alert rule on a virtual machine and configures the alert rule to call the Azure function.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="8d148-137">Een Azure-functie maken</span><span class="sxs-lookup"><span data-stu-id="8d148-137">Create an Azure function</span></span>

<span data-ttu-id="8d148-138">De eerste stap is het maken van een Azure-functie voor het verwerken van de waarschuwing en een pakketopname maken.</span><span class="sxs-lookup"><span data-stu-id="8d148-138">The first step is to create an Azure function to process the alert and create a packet capture.</span></span>

1. <span data-ttu-id="8d148-139">In de [Azure-portal](https://portal.azure.com), selecteer **nieuw** > **Compute** > **functie-App**.</span><span class="sxs-lookup"><span data-stu-id="8d148-139">In the [Azure portal](https://portal.azure.com), select **New** > **Compute** > **Function App**.</span></span>

    ![Een functie-app maken][1-1]

2. <span data-ttu-id="8d148-141">Op de **functie-App** blade, voer de volgende waarden en selecteer vervolgens **OK** om de app te maken:</span><span class="sxs-lookup"><span data-stu-id="8d148-141">On the **Function App** blade, enter the following values, and then select **OK** to create the app:</span></span>

    |<span data-ttu-id="8d148-142">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="8d148-142">**Setting**</span></span> | <span data-ttu-id="8d148-143">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="8d148-143">**Value**</span></span> | <span data-ttu-id="8d148-144">**Details**</span><span class="sxs-lookup"><span data-stu-id="8d148-144">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8d148-145">**Naam van app**</span><span class="sxs-lookup"><span data-stu-id="8d148-145">**App name**</span></span>|<span data-ttu-id="8d148-146">PacketCaptureExample</span><span class="sxs-lookup"><span data-stu-id="8d148-146">PacketCaptureExample</span></span>|<span data-ttu-id="8d148-147">De naam van de functie-app.</span><span class="sxs-lookup"><span data-stu-id="8d148-147">The name of the function app.</span></span>|
    |<span data-ttu-id="8d148-148">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="8d148-148">**Subscription**</span></span>|<span data-ttu-id="8d148-149">[Uw abonnement] Het abonnement waarvoor u de functie-app maken.</span><span class="sxs-lookup"><span data-stu-id="8d148-149">[Your subscription]The subscription for which to create the function app.</span></span>||
    |<span data-ttu-id="8d148-150">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="8d148-150">**Resource Group**</span></span>|<span data-ttu-id="8d148-151">PacketCaptureRG</span><span class="sxs-lookup"><span data-stu-id="8d148-151">PacketCaptureRG</span></span>|<span data-ttu-id="8d148-152">De resourcegroep bevat de functie-app.</span><span class="sxs-lookup"><span data-stu-id="8d148-152">The resource group to contain the function app.</span></span>|
    |<span data-ttu-id="8d148-153">**Hosting-Plan**</span><span class="sxs-lookup"><span data-stu-id="8d148-153">**Hosting Plan**</span></span>|<span data-ttu-id="8d148-154">Plan voor verbruik</span><span class="sxs-lookup"><span data-stu-id="8d148-154">Consumption Plan</span></span>| <span data-ttu-id="8d148-155">Het type plan uw app functie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8d148-155">The type of plan your function app uses.</span></span> <span data-ttu-id="8d148-156">Opties zijn verbruik of Azure App Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8d148-156">Options are Consumption or Azure App Service plan.</span></span> |
    |<span data-ttu-id="8d148-157">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="8d148-157">**Location**</span></span>|<span data-ttu-id="8d148-158">VS - midden</span><span class="sxs-lookup"><span data-stu-id="8d148-158">Central US</span></span>| <span data-ttu-id="8d148-159">De regio waarin u de functie-app maken.</span><span class="sxs-lookup"><span data-stu-id="8d148-159">The region in which to create the function app.</span></span>|
    |<span data-ttu-id="8d148-160">**Storage-Account**</span><span class="sxs-lookup"><span data-stu-id="8d148-160">**Storage Account**</span></span>|<span data-ttu-id="8d148-161">{automatisch gegenereerde}</span><span class="sxs-lookup"><span data-stu-id="8d148-161">{autogenerated}</span></span>| <span data-ttu-id="8d148-162">Het opslagaccount waarvoor Azure Functions voor opslagaccounts voor algemeen gebruik.</span><span class="sxs-lookup"><span data-stu-id="8d148-162">The storage account that Azure Functions needs for general-purpose storage.</span></span>|

3. <span data-ttu-id="8d148-163">Op de **PacketCaptureExample functie Apps** blade Selecteer **functies** > **aangepaste functie**  >  **+**.</span><span class="sxs-lookup"><span data-stu-id="8d148-163">On the **PacketCaptureExample Function Apps** blade, select **Functions** > **Custom function** >**+**.</span></span>

4. <span data-ttu-id="8d148-164">Selecteer **HttpTrigger Powershell**, en voer vervolgens de resterende gegevens.</span><span class="sxs-lookup"><span data-stu-id="8d148-164">Select **HttpTrigger-Powershell**, and then enter the remaining information.</span></span> <span data-ttu-id="8d148-165">Ten slotte selecteren voor het maken van de functie **maken**.</span><span class="sxs-lookup"><span data-stu-id="8d148-165">Finally, to create the function, select **Create**.</span></span>

    |<span data-ttu-id="8d148-166">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="8d148-166">**Setting**</span></span> | <span data-ttu-id="8d148-167">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="8d148-167">**Value**</span></span> | <span data-ttu-id="8d148-168">**Details**</span><span class="sxs-lookup"><span data-stu-id="8d148-168">**Details**</span></span> |
    |---|---|---|
    |<span data-ttu-id="8d148-169">**Scenario**</span><span class="sxs-lookup"><span data-stu-id="8d148-169">**Scenario**</span></span>|<span data-ttu-id="8d148-170">experimentele</span><span class="sxs-lookup"><span data-stu-id="8d148-170">Experimental</span></span>|<span data-ttu-id="8d148-171">Type van scenario</span><span class="sxs-lookup"><span data-stu-id="8d148-171">Type of scenario</span></span>|
    |<span data-ttu-id="8d148-172">**Een naam voor de functie opgeven**</span><span class="sxs-lookup"><span data-stu-id="8d148-172">**Name your function**</span></span>|<span data-ttu-id="8d148-173">AlertPacketCapturePowerShell</span><span class="sxs-lookup"><span data-stu-id="8d148-173">AlertPacketCapturePowerShell</span></span>|<span data-ttu-id="8d148-174">Naam van de functie</span><span class="sxs-lookup"><span data-stu-id="8d148-174">Name of the function</span></span>|
    |<span data-ttu-id="8d148-175">**Machtigingsniveau**</span><span class="sxs-lookup"><span data-stu-id="8d148-175">**Authorization level**</span></span>|<span data-ttu-id="8d148-176">Functie</span><span class="sxs-lookup"><span data-stu-id="8d148-176">Function</span></span>|<span data-ttu-id="8d148-177">Autorisatieniveau voor de functie</span><span class="sxs-lookup"><span data-stu-id="8d148-177">Authorization level for the function</span></span>|

![Voorbeeld van de functies][functions1]

> [!NOTE]
> <span data-ttu-id="8d148-179">De PowerShell-sjabloon is experimentele en heeft geen volledige ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="8d148-179">The PowerShell template is experimental and does not have full support.</span></span>

<span data-ttu-id="8d148-180">Aanpassingen zijn vereist voor dit voorbeeld en worden beschreven in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="8d148-180">Customizations are required for this example and are explained in the following steps.</span></span>

### <a name="add-modules"></a><span data-ttu-id="8d148-181">Modules toevoegen</span><span class="sxs-lookup"><span data-stu-id="8d148-181">Add modules</span></span>

<span data-ttu-id="8d148-182">Voor het gebruik van netwerk-Watcher PowerShell-cmdlets, de meest recente PowerShell-module naar de functie-app te uploaden.</span><span class="sxs-lookup"><span data-stu-id="8d148-182">To use Network Watcher PowerShell cmdlets, upload the latest PowerShell module to the function app.</span></span>

1. <span data-ttu-id="8d148-183">Voer de volgende PowerShell-opdracht op uw lokale computer met de meest recente Azure PowerShell-modules geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="8d148-183">On your local machine with the latest Azure PowerShell modules installed, run the following PowerShell command:</span></span>

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    <span data-ttu-id="8d148-184">In dit voorbeeld kunt u het lokale pad naar uw Azure PowerShell-modules.</span><span class="sxs-lookup"><span data-stu-id="8d148-184">This example gives you the local path of your Azure PowerShell modules.</span></span> <span data-ttu-id="8d148-185">Deze mappen worden gebruikt in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="8d148-185">These folders are used in a later step.</span></span> <span data-ttu-id="8d148-186">De modules die worden gebruikt in dit scenario zijn:</span><span class="sxs-lookup"><span data-stu-id="8d148-186">The modules that are used in this scenario are:</span></span>

    * <span data-ttu-id="8d148-187">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8d148-187">AzureRM.Network</span></span>

    * <span data-ttu-id="8d148-188">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8d148-188">AzureRM.Profile</span></span>

    * <span data-ttu-id="8d148-189">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8d148-189">AzureRM.Resources</span></span>

    ![PowerShell-mappen][functions5]

1. <span data-ttu-id="8d148-191">Selecteer **werken app-instellingen** > **Ga naar App Service Editor**.</span><span class="sxs-lookup"><span data-stu-id="8d148-191">Select **Function app settings** > **Go to App Service Editor**.</span></span>

    ![De functie app-instellingen][functions2]

1. <span data-ttu-id="8d148-193">Met de rechtermuisknop op de **AlertPacketCapturePowershell** map, en maak vervolgens een map met de naam **azuremodules**.</span><span class="sxs-lookup"><span data-stu-id="8d148-193">Right-click the **AlertPacketCapturePowershell** folder, and then create a folder called **azuremodules**.</span></span> 

4. <span data-ttu-id="8d148-194">Maak een submap voor elke module die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="8d148-194">Create a subfolder for each module that you need.</span></span>

    ![Map en submappen][functions3]

    * <span data-ttu-id="8d148-196">AzureRM.Network</span><span class="sxs-lookup"><span data-stu-id="8d148-196">AzureRM.Network</span></span>

    * <span data-ttu-id="8d148-197">AzureRM.Profile</span><span class="sxs-lookup"><span data-stu-id="8d148-197">AzureRM.Profile</span></span>

    * <span data-ttu-id="8d148-198">AzureRM.Resources</span><span class="sxs-lookup"><span data-stu-id="8d148-198">AzureRM.Resources</span></span>

1. <span data-ttu-id="8d148-199">Met de rechtermuisknop op de **AzureRM.Network** submap en selecteer vervolgens **bestanden uploaden**.</span><span class="sxs-lookup"><span data-stu-id="8d148-199">Right-click the **AzureRM.Network** subfolder, and then select **Upload Files**.</span></span> 

6. <span data-ttu-id="8d148-200">Ga naar uw Azure-modules.</span><span class="sxs-lookup"><span data-stu-id="8d148-200">Go to your Azure modules.</span></span> <span data-ttu-id="8d148-201">In de lokale **AzureRM.Network** map, selecteert u alle bestanden in de map.</span><span class="sxs-lookup"><span data-stu-id="8d148-201">In the local **AzureRM.Network** folder, select all the files in the folder.</span></span> <span data-ttu-id="8d148-202">Selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d148-202">Then select **OK**.</span></span> 

7. <span data-ttu-id="8d148-203">Herhaal deze stappen voor **AzureRM.Profile** en **AzureRM.Resources**.</span><span class="sxs-lookup"><span data-stu-id="8d148-203">Repeat these steps for **AzureRM.Profile** and **AzureRM.Resources**.</span></span>

    ![Bestanden uploaden][functions6]

1. <span data-ttu-id="8d148-205">Nadat u klaar bent, elke map moet hebben tot de bestanden van de PowerShell-module van uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8d148-205">After you've finished, each folder should have the PowerShell module files from your local machine.</span></span>

    ![Bestanden met PowerShell][functions7]

### <a name="authentication"></a><span data-ttu-id="8d148-207">Authentication</span><span class="sxs-lookup"><span data-stu-id="8d148-207">Authentication</span></span>

<span data-ttu-id="8d148-208">Voor het gebruik van de PowerShell-cmdlets, moet u verifiëren.</span><span class="sxs-lookup"><span data-stu-id="8d148-208">To use the PowerShell cmdlets, you must authenticate.</span></span> <span data-ttu-id="8d148-209">U configureren verificatie in de functie-app.</span><span class="sxs-lookup"><span data-stu-id="8d148-209">You configure authentication in the function app.</span></span> <span data-ttu-id="8d148-210">Als verificatie wilt configureren, moet u omgevingsvariabelen configureren en het bestand met een versleutelde sleutel uploaden naar de functie-app.</span><span class="sxs-lookup"><span data-stu-id="8d148-210">To configure authentication, you must configure environment variables and upload an encrypted key file to the function app.</span></span>

> [!NOTE]
> <span data-ttu-id="8d148-211">Dit scenario biedt slechts één voorbeeld van hoe u verificatie met Azure Functions implementeert.</span><span class="sxs-lookup"><span data-stu-id="8d148-211">This scenario provides just one example of how to implement authentication with Azure Functions.</span></span> <span data-ttu-id="8d148-212">Er zijn andere manieren om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="8d148-212">There are other ways to do this.</span></span>

#### <a name="encrypted-credentials"></a><span data-ttu-id="8d148-213">Versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="8d148-213">Encrypted credentials</span></span>

<span data-ttu-id="8d148-214">De volgende PowerShell-script maakt een sleutelbestand aangeroepen **PassEncryptKey.key**.</span><span class="sxs-lookup"><span data-stu-id="8d148-214">The following PowerShell script creates a key file called **PassEncryptKey.key**.</span></span> <span data-ttu-id="8d148-215">Het bevat ook een versleutelde versie van het wachtwoord dat wordt meegeleverd.</span><span class="sxs-lookup"><span data-stu-id="8d148-215">It also provides an encrypted version of the password that's supplied.</span></span> <span data-ttu-id="8d148-216">Dit wachtwoord wordt hetzelfde wachtwoord dat is gedefinieerd voor de Azure Active Directory-toepassing die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="8d148-216">This password is the same password that is defined for the Azure Active Directory application that's used for authentication.</span></span>

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

<span data-ttu-id="8d148-217">In de App Service-Editor van de functie-app maken in een map met de naam **sleutels** onder **AlertPacketCapturePowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8d148-217">In the App Service Editor of the function app, create a folder called **keys** under **AlertPacketCapturePowerShell**.</span></span> <span data-ttu-id="8d148-218">Upload de **PassEncryptKey.key** -bestand dat u hebt gemaakt in het vorige voorbeeld met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8d148-218">Then upload the **PassEncryptKey.key** file that you created in the previous PowerShell sample.</span></span>

![Functies sleutel][functions8]

### <a name="retrieve-values-for-environment-variables"></a><span data-ttu-id="8d148-220">Waarden voor omgevingsvariabelen ophalen</span><span class="sxs-lookup"><span data-stu-id="8d148-220">Retrieve values for environment variables</span></span>

<span data-ttu-id="8d148-221">De laatste vereiste is voor het instellen van de omgevingsvariabelen die nodig zijn voor toegang tot de waarden voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="8d148-221">The final requirement is to set up the environment variables that are necessary to access the values for authentication.</span></span> <span data-ttu-id="8d148-222">De volgende lijst bevat de omgevingsvariabelen die zijn gemaakt:</span><span class="sxs-lookup"><span data-stu-id="8d148-222">The following list shows the environment variables that are created:</span></span>

* <span data-ttu-id="8d148-223">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8d148-223">AzureClientID</span></span>

* <span data-ttu-id="8d148-224">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8d148-224">AzureTenant</span></span>

* <span data-ttu-id="8d148-225">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8d148-225">AzureCredPassword</span></span>


#### <a name="azureclientid"></a><span data-ttu-id="8d148-226">AzureClientID</span><span class="sxs-lookup"><span data-stu-id="8d148-226">AzureClientID</span></span>

<span data-ttu-id="8d148-227">De client-ID is de ID van een toepassing in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8d148-227">The client ID is the Application ID of an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="8d148-228">Als u geen al een toepassing te gebruiken, moet u het volgende voorbeeld voor het maken van een toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="8d148-228">If you don't already have an application to use, run the following example to create an application.</span></span>

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > <span data-ttu-id="8d148-229">Het wachtwoord dat u bij het maken van de toepassing moet hetzelfde wachtwoord dat u eerder hebt gemaakt bij het opslaan van het sleutelbestand.</span><span class="sxs-lookup"><span data-stu-id="8d148-229">The password that you use when creating the application should be the same password that you created earlier when saving the key file.</span></span>

1. <span data-ttu-id="8d148-230">Selecteer in de Azure-portal **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="8d148-230">In the Azure portal, select **Subscriptions**.</span></span> <span data-ttu-id="8d148-231">Selecteer het abonnement wilt gebruiken en selecteer vervolgens **toegangsbeheer (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="8d148-231">Select the subscription to use, and then select **Access control (IAM)**.</span></span>

    ![De IAM-functies][functions9]

1. <span data-ttu-id="8d148-233">Kies het account moet gebruiken en selecteer vervolgens **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="8d148-233">Choose the account to use, and then select **Properties**.</span></span> <span data-ttu-id="8d148-234">Kopieer de toepassings-ID.</span><span class="sxs-lookup"><span data-stu-id="8d148-234">Copy the Application ID.</span></span>

    ![Functies toepassings-ID][functions10]

#### <a name="azuretenant"></a><span data-ttu-id="8d148-236">AzureTenant</span><span class="sxs-lookup"><span data-stu-id="8d148-236">AzureTenant</span></span>

<span data-ttu-id="8d148-237">De tenant-ID verkrijgen door het uitvoeren van de volgende PowerShell-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8d148-237">Obtain the tenant ID  by running the following PowerShell sample:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a><span data-ttu-id="8d148-238">AzureCredPassword</span><span class="sxs-lookup"><span data-stu-id="8d148-238">AzureCredPassword</span></span>

<span data-ttu-id="8d148-239">De waarde van de omgevingsvariabele AzureCredPassword is de waarde die u via de volgende PowerShell-voorbeeld uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8d148-239">The value of the AzureCredPassword environment variable is the value that you get from running the following PowerShell sample.</span></span> <span data-ttu-id="8d148-240">In dit voorbeeld wordt hetzelfde account dat wordt weergegeven in de voorgaande **versleuteld referenties** sectie.</span><span class="sxs-lookup"><span data-stu-id="8d148-240">This example is the same one that's shown in the preceding **Encrypted credentials** section.</span></span> <span data-ttu-id="8d148-241">De waarde die nodig is, is de uitvoer van de `$Encryptedpassword` variabele.</span><span class="sxs-lookup"><span data-stu-id="8d148-241">The value that's needed is the output of the `$Encryptedpassword` variable.</span></span>  <span data-ttu-id="8d148-242">Dit is de service principal wachtwoord die u versleuteld met behulp van het PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="8d148-242">This is the service principal password that you encrypted by using the PowerShell script.</span></span>

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

### <a name="store-the-environment-variables"></a><span data-ttu-id="8d148-243">De omgevingsvariabelen opslaan</span><span class="sxs-lookup"><span data-stu-id="8d148-243">Store the environment variables</span></span>

1. <span data-ttu-id="8d148-244">Ga naar de functie-app.</span><span class="sxs-lookup"><span data-stu-id="8d148-244">Go to the function app.</span></span> <span data-ttu-id="8d148-245">Selecteer vervolgens **werken app-instellingen** > **app-instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="8d148-245">Then select **Function app settings** > **Configure app settings**.</span></span>

    ![App-instellingen configureren][functions11]

1. <span data-ttu-id="8d148-247">De omgevingsvariabelen en hun waarden toevoegen aan de app-instellingen en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="8d148-247">Add the environment variables and their values to the app settings, and then select **Save**.</span></span>

    ![App-instellingen][functions12]

### <a name="add-powershell-to-the-function"></a><span data-ttu-id="8d148-249">PowerShell toevoegen aan de functie</span><span class="sxs-lookup"><span data-stu-id="8d148-249">Add PowerShell to the function</span></span>

<span data-ttu-id="8d148-250">Het is nu tijd om aanroepen voor netwerk-Watcher uit vanuit de Azure-functie.</span><span class="sxs-lookup"><span data-stu-id="8d148-250">It's now time to make calls into Network Watcher from within the Azure function.</span></span> <span data-ttu-id="8d148-251">Afhankelijk van de vereisten, kan de implementatie van deze functie variëren.</span><span class="sxs-lookup"><span data-stu-id="8d148-251">Depending on the requirements, the implementation of this function can vary.</span></span> <span data-ttu-id="8d148-252">De algemene stroom van de code is echter als volgt:</span><span class="sxs-lookup"><span data-stu-id="8d148-252">However, the general flow of the code is as follows:</span></span>

1. <span data-ttu-id="8d148-253">Proces-invoerparameters.</span><span class="sxs-lookup"><span data-stu-id="8d148-253">Process input parameters.</span></span>
2. <span data-ttu-id="8d148-254">Bestaande pakket query worden vastgelegd om te verifiëren limieten en omzetten van de naam een conflict veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="8d148-254">Query existing packet captures to verify limits and resolve name conflicts.</span></span>
3. <span data-ttu-id="8d148-255">Maak een pakketopname met toepasselijke parameters.</span><span class="sxs-lookup"><span data-stu-id="8d148-255">Create a packet capture with appropriate parameters.</span></span>
4. <span data-ttu-id="8d148-256">Poll-pakket vastleggen periodiek totdat deze is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8d148-256">Poll packet capture periodically until it's complete.</span></span>
5. <span data-ttu-id="8d148-257">De gebruiker waarschuwen dat de opnamesessie pakket voltooid is.</span><span class="sxs-lookup"><span data-stu-id="8d148-257">Notify the user that the packet capture session is complete.</span></span>

<span data-ttu-id="8d148-258">Het volgende voorbeeld is een PowerShell-code die kan worden gebruikt in de functie.</span><span class="sxs-lookup"><span data-stu-id="8d148-258">The following example is PowerShell code that can be used in the function.</span></span> <span data-ttu-id="8d148-259">Er zijn waarden die worden vervangen moeten voor **subscriptionId**, **resourceGroupName**, en **storageAccountName**.</span><span class="sxs-lookup"><span data-stu-id="8d148-259">There are values that need to be replaced for **subscriptionId**, **resourceGroupName**, and **storageAccountName**.</span></span>

```powershell
            #Import Azure PowerShell modules required to make calls to Network Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID to save captures in
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


            #Get the VM that fired the alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get the Network Watcher in the VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by the function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on the VM that fired the alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-the-function-url"></a><span data-ttu-id="8d148-260">De URL van de functie niet ophalen</span><span class="sxs-lookup"><span data-stu-id="8d148-260">Retrieve the function URL</span></span> 
1. <span data-ttu-id="8d148-261">Nadat u de functie hebt gemaakt, configureert u de waarschuwing voor het aanroepen van de URL die is gekoppeld aan de functie.</span><span class="sxs-lookup"><span data-stu-id="8d148-261">After you've created your function, configure your alert to call the URL that's associated with the function.</span></span> <span data-ttu-id="8d148-262">Als u deze waarde, de URL van de functie van de functie-app te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="8d148-262">To get this value, copy the function URL from your function app.</span></span>

    ![De URL van de functie zoeken][functions13]

2. <span data-ttu-id="8d148-264">Kopieer de URL van de functie voor functie-app.</span><span class="sxs-lookup"><span data-stu-id="8d148-264">Copy the function URL for your function app.</span></span>

    ![De URL van de functie kopiëren][2]

<span data-ttu-id="8d148-266">Als u aangepaste eigenschappen in de nettolading van de webhook POST-aanvraag nodig hebt, raadpleegt u [een webhook configureren op een Azure metrische waarschuwing](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="8d148-266">If you require custom properties in the payload of the webhook POST request, refer to [Configure a webhook on an Azure metric alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

## <a name="configure-an-alert-on-a-vm"></a><span data-ttu-id="8d148-267">Een waarschuwing te configureren op een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="8d148-267">Configure an alert on a VM</span></span>

<span data-ttu-id="8d148-268">Waarschuwingen kunnen worden geconfigureerd om te personen melden wanneer specifieke metrische gegevens overschrijdt de drempelwaarde die toegewezen.</span><span class="sxs-lookup"><span data-stu-id="8d148-268">Alerts can be configured to notify individuals when a specific metric crosses a threshold that's assigned to it.</span></span> <span data-ttu-id="8d148-269">In dit voorbeeld wordt de waarschuwing wordt op de TCP-segmenten die worden verzonden, maar de waarschuwing voor veel andere metrische gegevens kan worden geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8d148-269">In this example, the alert is on the TCP segments that are sent, but the alert can be triggered for many other metrics.</span></span> <span data-ttu-id="8d148-270">In dit voorbeeld wordt een waarschuwing geconfigureerd voor het aanroepen van een webhook voor het aanroepen van de functie.</span><span class="sxs-lookup"><span data-stu-id="8d148-270">In this example, an alert is configured to call a webhook to call the function.</span></span>

### <a name="create-the-alert-rule"></a><span data-ttu-id="8d148-271">De waarschuwingsregel maken</span><span class="sxs-lookup"><span data-stu-id="8d148-271">Create the alert rule</span></span>

<span data-ttu-id="8d148-272">Ga naar een bestaande virtuele machine en vervolgens een waarschuwingsregel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8d148-272">Go to an existing virtual machine, and then add an alert rule.</span></span> <span data-ttu-id="8d148-273">Meer gedetailleerde documentatie over het configureren van waarschuwingen kan worden gevonden op [waarschuwingen in de Azure-Monitor maken voor Azure-services - Azure-portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8d148-273">More detailed documentation about configuring alerts can be found at [Create alerts in Azure Monitor for Azure services - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md).</span></span> <span data-ttu-id="8d148-274">Voer de volgende waarden in de **waarschuwingsregel** blade en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="8d148-274">Enter the following values in the **Alert rule** blade, and then select **OK**.</span></span>

  |<span data-ttu-id="8d148-275">**Instelling**</span><span class="sxs-lookup"><span data-stu-id="8d148-275">**Setting**</span></span> | <span data-ttu-id="8d148-276">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="8d148-276">**Value**</span></span> | <span data-ttu-id="8d148-277">**Details**</span><span class="sxs-lookup"><span data-stu-id="8d148-277">**Details**</span></span> |
  |---|---|---|
  |<span data-ttu-id="8d148-278">**Naam**</span><span class="sxs-lookup"><span data-stu-id="8d148-278">**Name**</span></span>|<span data-ttu-id="8d148-279">TCP_Segments_Sent_Exceeded</span><span class="sxs-lookup"><span data-stu-id="8d148-279">TCP_Segments_Sent_Exceeded</span></span>|<span data-ttu-id="8d148-280">Naam van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="8d148-280">Name of the alert rule.</span></span>|
  |<span data-ttu-id="8d148-281">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="8d148-281">**Description**</span></span>|<span data-ttu-id="8d148-282">TCP-segmenten verzonden drempelwaarde overschreden</span><span class="sxs-lookup"><span data-stu-id="8d148-282">TCP segments sent exceeded threshold</span></span>|<span data-ttu-id="8d148-283">De beschrijving van de waarschuwingsregel.</span><span class="sxs-lookup"><span data-stu-id="8d148-283">The description for the alert rule.</span></span>||
  |<span data-ttu-id="8d148-284">**Gegevens**</span><span class="sxs-lookup"><span data-stu-id="8d148-284">**Metric**</span></span>|<span data-ttu-id="8d148-285">TCP-segmenten die zijn verzonden</span><span class="sxs-lookup"><span data-stu-id="8d148-285">TCP segments sent</span></span>| <span data-ttu-id="8d148-286">De meetwaarde moet worden gebruikt om de waarschuwing te activeren.</span><span class="sxs-lookup"><span data-stu-id="8d148-286">The metric to use to trigger the alert.</span></span> |
  |<span data-ttu-id="8d148-287">**Voorwaarde**</span><span class="sxs-lookup"><span data-stu-id="8d148-287">**Condition**</span></span>|<span data-ttu-id="8d148-288">Groter dan</span><span class="sxs-lookup"><span data-stu-id="8d148-288">Greater than</span></span>| <span data-ttu-id="8d148-289">De voorwaarde moet worden gebruikt bij het evalueren van de metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="8d148-289">The condition to use when evaluating the metric.</span></span>|
  |<span data-ttu-id="8d148-290">**Drempelwaarde**</span><span class="sxs-lookup"><span data-stu-id="8d148-290">**Threshold**</span></span>|<span data-ttu-id="8d148-291">100</span><span class="sxs-lookup"><span data-stu-id="8d148-291">100</span></span>| <span data-ttu-id="8d148-292">De waarde van de metrische gegevens waarmee de waarschuwing wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8d148-292">The  value of the metric that triggers the alert.</span></span> <span data-ttu-id="8d148-293">Deze waarde moet worden ingesteld op een geldige waarde voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="8d148-293">This value should be set to a valid value for your environment.</span></span>|
  |<span data-ttu-id="8d148-294">**Periode**</span><span class="sxs-lookup"><span data-stu-id="8d148-294">**Period**</span></span>|<span data-ttu-id="8d148-295">In de afgelopen vijf minuten</span><span class="sxs-lookup"><span data-stu-id="8d148-295">Over the last five minutes</span></span>| <span data-ttu-id="8d148-296">Bepaalt de periode waarin er voor de drempelwaarde voor de metriek.</span><span class="sxs-lookup"><span data-stu-id="8d148-296">Determines the period in which to look for the threshold on the metric.</span></span>|
  |<span data-ttu-id="8d148-297">**Webhook**</span><span class="sxs-lookup"><span data-stu-id="8d148-297">**Webhook**</span></span>|<span data-ttu-id="8d148-298">[webhook-URL van de functie-app]</span><span class="sxs-lookup"><span data-stu-id="8d148-298">[webhook URL from function app]</span></span>| <span data-ttu-id="8d148-299">De webhook-URL van de functie-app die is gemaakt in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="8d148-299">The webhook URL from the function app that was created in the previous steps.</span></span>|

> [!NOTE]
> <span data-ttu-id="8d148-300">De TCP-segmenten metriek is niet standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="8d148-300">The TCP segments metric is not enabled by default.</span></span> <span data-ttu-id="8d148-301">Meer informatie over het inschakelen van aanvullende gegevens in via [inschakelen bewaking en diagnostische gegevens](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="8d148-301">Learn more about how to enable additional metrics by visiting [Enable monitoring and diagnostics](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).</span></span>

## <a name="review-the-results"></a><span data-ttu-id="8d148-302">Bekijk de resultaten</span><span class="sxs-lookup"><span data-stu-id="8d148-302">Review the results</span></span>

<span data-ttu-id="8d148-303">Nadat de criteria voor de waarschuwing triggers wordt een pakketopname gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8d148-303">After the criteria for the alert triggers, a packet capture is created.</span></span> <span data-ttu-id="8d148-304">Ga naar de netwerk-Watcher en selecteer vervolgens **pakketopname**.</span><span class="sxs-lookup"><span data-stu-id="8d148-304">Go to Network Watcher, and then select **Packet capture**.</span></span> <span data-ttu-id="8d148-305">Op deze pagina kunt u de koppeling pakket capture-bestand voor het downloaden van het pakket vastleggen.</span><span class="sxs-lookup"><span data-stu-id="8d148-305">On this page, you can select the packet capture file link to download the packet capture.</span></span>

![Weergave pakketopname][functions14]

<span data-ttu-id="8d148-307">Als het bestand vastleggen lokaal is opgeslagen, kunt u deze ophalen door de aanmelding bij de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8d148-307">If the capture file is stored locally, you can retrieve it by signing in to the virtual machine.</span></span>

<span data-ttu-id="8d148-308">Zie voor instructies over het downloaden van bestanden van Azure storage-accounts [aan de slag met Azure Blob storage met .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="8d148-308">For instructions about downloading files from Azure storage accounts, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="8d148-309">Een ander hulpprogramma kunt u is [Opslagverkenner](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8d148-309">Another tool you can use is [Storage Explorer](http://storageexplorer.com/).</span></span>

<span data-ttu-id="8d148-310">Nadat het vastleggen is gedownload, kunt u deze bekijken met behulp van een hulpprogramma dat gelezen kan een **CAP** bestand.</span><span class="sxs-lookup"><span data-stu-id="8d148-310">After your capture has been downloaded, you can view it by using any tool that can read a **.cap** file.</span></span> <span data-ttu-id="8d148-311">Hieronder volgen koppelingen naar twee van deze hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="8d148-311">Following are links to two of these tools:</span></span>

- [<span data-ttu-id="8d148-312">Microsoft Message Analyzer</span><span class="sxs-lookup"><span data-stu-id="8d148-312">Microsoft Message Analyzer</span></span>](https://technet.microsoft.com/library/jj649776.aspx)
- [<span data-ttu-id="8d148-313">WireShark</span><span class="sxs-lookup"><span data-stu-id="8d148-313">WireShark</span></span>](https://www.wireshark.org/)

## <a name="next-steps"></a><span data-ttu-id="8d148-314">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8d148-314">Next steps</span></span>

<span data-ttu-id="8d148-315">Meer informatie over het bekijken op de opnamen pakket [pakket netwerkopname-analyse met Wireshark](network-watcher-deep-packet-inspection.md).</span><span class="sxs-lookup"><span data-stu-id="8d148-315">Learn how to view your packet captures by visiting [Packet capture analysis with Wireshark](network-watcher-deep-packet-inspection.md).</span></span>


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
