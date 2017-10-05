---
title: Logboeken van Azure Sleutelkluis integreert met behulp van Event Hubs | Microsoft Docs
description: Zelfstudie waarmee u de benodigde stappen voor Sleutelkluis-logboeken beschikbaar te maken voor een SIEM met behulp van de integratie van Azure-logboek
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: 3cd80817bf8b2ef2f66e9942eddc186a3eb5b5e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="3f721-103">Zelfstudie voor Azure Log-integratie: proces Azure Key Vault gebeurtenissen met behulp van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3f721-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="3f721-104">Integratie van Azure Log kunt u geregistreerde gebeurtenissen ophalen en deze beschikbaar aan uw informatie en event management (SIEM) beveiligingssysteem.</span><span class="sxs-lookup"><span data-stu-id="3f721-104">You can use Azure Log Integration to retrieve logged events and make them available to your security information and event management (SIEM) system.</span></span> <span data-ttu-id="3f721-105">Deze zelfstudie toont een voorbeeld van hoe Azure Log-integratie kunnen worden gebruikt voor het verwerken van logboeken die zijn verkregen via Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3f721-105">This tutorial shows an example of how Azure Log Integration can be used to process logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="3f721-106">Gebruik deze zelfstudie om bekend te raken met hoe Azure Log-integratie en Event Hubs samen werken met de voorbeeld-stappen te volgen en kennis van hoe de oplossing biedt ondersteuning voor elke stap.</span><span class="sxs-lookup"><span data-stu-id="3f721-106">Use this tutorial to get acquainted with how Azure Log Integration and Event Hubs work together by following the example steps and understanding how each step supports the solution.</span></span> <span data-ttu-id="3f721-107">U kunt vervolgens nemen wat u hebt geleerd hier uw eigen stappen ter ondersteuning van de unieke vereisten van uw bedrijf maken.</span><span class="sxs-lookup"><span data-stu-id="3f721-107">Then you can take what you’ve learned here to create your own steps to support your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="3f721-108">De stappen en de opdrachten in deze zelfstudie zijn niet bedoeld om te worden gekopieerd en geplakt.</span><span class="sxs-lookup"><span data-stu-id="3f721-108">The steps and commands in this tutorial are not intended to be copied and pasted.</span></span> <span data-ttu-id="3f721-109">Ze zijn alleen voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3f721-109">They're examples only.</span></span> <span data-ttu-id="3f721-110">Gebruik de PowerShell-opdrachten 'als zodanig' niet in uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f721-110">Do not use the PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="3f721-111">U moet deze op basis van uw omgeving aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3f721-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="3f721-112">Deze zelfstudie wordt u door het proces van nemen Azure Key Vault activiteit vastgelegd in een event hub en het beschikbaar maken als JSON-bestanden naar uw SIEM-systeem.</span><span class="sxs-lookup"><span data-stu-id="3f721-112">This tutorial walks you through the process of taking Azure Key Vault activity logged to an event hub and making it available as JSON files to your SIEM system.</span></span> <span data-ttu-id="3f721-113">Vervolgens kunt u uw SIEM-systeem voor het verwerken van de JSON-bestanden configureren.</span><span class="sxs-lookup"><span data-stu-id="3f721-113">You can then configure your SIEM system to process the JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="3f721-114">De meeste van de stappen in deze zelfstudie hebben betrekking op het configureren van sleutelkluizen, opslagaccounts en event hubs.</span><span class="sxs-lookup"><span data-stu-id="3f721-114">Most of the steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="3f721-115">De specifieke Azure-logboek integratiestappen zijn aan het einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3f721-115">The specific Azure Log Integration steps are at the end of this tutorial.</span></span> <span data-ttu-id="3f721-116">Voer deze stappen niet uit in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="3f721-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="3f721-117">Ze zijn bedoeld voor een testomgeving alleen.</span><span class="sxs-lookup"><span data-stu-id="3f721-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="3f721-118">Voordat u ze in productie, moet u de stappen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3f721-118">You must customize the steps before using them in production.</span></span>

<span data-ttu-id="3f721-119">Informatie over de manier helpt u begrijpen van de redenen achter elke stap.</span><span class="sxs-lookup"><span data-stu-id="3f721-119">Information provided along the way helps you understand the reasons behind each step.</span></span> <span data-ttu-id="3f721-120">Koppelingen naar andere artikelen kunnen u meer details op bepaalde onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="3f721-120">Links to other articles give you more detail on certain topics.</span></span>

<span data-ttu-id="3f721-121">Zie voor meer informatie over de services die in deze zelfstudie wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="3f721-121">For more information about the services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="3f721-122">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3f721-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="3f721-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3f721-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="3f721-124">Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="3f721-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="3f721-125">Eerste installatie</span><span class="sxs-lookup"><span data-stu-id="3f721-125">Initial setup</span></span>

<span data-ttu-id="3f721-126">Voordat u de stappen in dit artikel voltooien kunt, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="3f721-126">Before you can complete the steps in this article, you need the following:</span></span>

1. <span data-ttu-id="3f721-127">Een Azure-abonnement en de account op dat abonnement met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="3f721-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="3f721-128">Als u geen een abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3f721-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="3f721-129">Een systeem met toegang tot het internet die voldoet aan de vereisten voor het installeren van de integratie van Azure-logboek.</span><span class="sxs-lookup"><span data-stu-id="3f721-129">A system with access to the internet that meets the requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="3f721-130">Het systeem kan op een cloudservice of lokaal wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="3f721-130">The system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="3f721-131">[Integratie van Azure Log](https://www.microsoft.com/download/details.aspx?id=53324) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3f721-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="3f721-132">Om deze te installeren:</span><span class="sxs-lookup"><span data-stu-id="3f721-132">To install it:</span></span>

   <span data-ttu-id="3f721-133">a.</span><span class="sxs-lookup"><span data-stu-id="3f721-133">a.</span></span> <span data-ttu-id="3f721-134">Extern bureaublad gebruiken voor verbinding met het systeem dat wordt vermeld in stap 2.</span><span class="sxs-lookup"><span data-stu-id="3f721-134">Use Remote Desktop to connect to the system mentioned in step 2.</span></span>   
   <span data-ttu-id="3f721-135">b.</span><span class="sxs-lookup"><span data-stu-id="3f721-135">b.</span></span> <span data-ttu-id="3f721-136">Kopieer het installatieprogramma van de integratie van Azure Log naar het systeem.</span><span class="sxs-lookup"><span data-stu-id="3f721-136">Copy the Azure Log Integration installer to the system.</span></span> <span data-ttu-id="3f721-137">U kunt [downloaden van de installatiebestanden](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="3f721-137">You can [download the installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="3f721-138">c.</span><span class="sxs-lookup"><span data-stu-id="3f721-138">c.</span></span> <span data-ttu-id="3f721-139">Het installatieprogramma start en accepteer de licentievoorwaarden voor Microsoft-Software.</span><span class="sxs-lookup"><span data-stu-id="3f721-139">Start the installer and accept the Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="3f721-140">d.</span><span class="sxs-lookup"><span data-stu-id="3f721-140">d.</span></span> <span data-ttu-id="3f721-141">Als u telemetrie informatie opgeeft wordt, laat u het selectievakje ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3f721-141">If you will provide telemetry information, leave the check box selected.</span></span> <span data-ttu-id="3f721-142">Schakel het selectievakje in als u zou in plaats daarvan niet gebruiksgegevens naar Microsoft verzonden.</span><span class="sxs-lookup"><span data-stu-id="3f721-142">If you'd rather not send usage information to Microsoft, clear the check box.</span></span>
   
   <span data-ttu-id="3f721-143">Zie voor meer informatie over Azure Log-integratie en hoe u deze installeert [Azure Log integratie met Azure Diagnostics logboekregistratie en Windows Event Forwarding](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3f721-143">For more information about Azure Log Integration and how to install it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="3f721-144">De nieuwste versie van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f721-144">The latest PowerShell version.</span></span>
 
   <span data-ttu-id="3f721-145">Als u Windows Server 2016 geïnstalleerd hebt, hebt u ten minste PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="3f721-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="3f721-146">Als u een andere versie van Windows Server, hebt u mogelijk een oudere versie van PowerShell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3f721-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="3f721-147">U kunt controleren welke versie door in te voeren ```get-host``` in een PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="3f721-147">You can check the version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="3f721-148">Als er geen PowerShell 5.0 is geïnstalleerd, kunt u [downloaden](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="3f721-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="3f721-149">Nadat u ten minste hebt PowerShell 5.0, kunt u doorgaan met de meest recente versie te installeren:</span><span class="sxs-lookup"><span data-stu-id="3f721-149">After you have at least PowerShell 5.0, you can proceed to install the latest version:</span></span>
   
   <span data-ttu-id="3f721-150">a.</span><span class="sxs-lookup"><span data-stu-id="3f721-150">a.</span></span> <span data-ttu-id="3f721-151">Voer in een PowerShell-venster de ```Install-Module Azure``` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f721-151">In a PowerShell window, enter the ```Install-Module Azure``` command.</span></span> <span data-ttu-id="3f721-152">Voltooi de installatiestappen.</span><span class="sxs-lookup"><span data-stu-id="3f721-152">Complete the installation steps.</span></span>    
   <span data-ttu-id="3f721-153">b.</span><span class="sxs-lookup"><span data-stu-id="3f721-153">b.</span></span> <span data-ttu-id="3f721-154">Voer de ```Install-Module AzureRM``` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f721-154">Enter the ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="3f721-155">Voltooi de installatiestappen.</span><span class="sxs-lookup"><span data-stu-id="3f721-155">Complete the installation steps.</span></span>

   <span data-ttu-id="3f721-156">Zie voor meer informatie [Azure PowerShell installeren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="3f721-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="3f721-157">Ondersteunende Infrastructuurelementen maken</span><span class="sxs-lookup"><span data-stu-id="3f721-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="3f721-158">Open een PowerShell-venster met verhoogde bevoegdheid en Ga naar **C:\Program Files\Microsoft Azure Log integratie**.</span><span class="sxs-lookup"><span data-stu-id="3f721-158">Open an elevated PowerShell window and go to **C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="3f721-159">Importeer de cmdlets AzLog LoadAzLogModule.ps1 van het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3f721-159">Import the AzLog cmdlets by running the script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="3f721-160">Voer de `.\LoadAzLogModule.ps1` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f721-160">Enter the `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="3f721-161">(U ziet de '. \ ' in die opdracht.) Deze lijst ziet er ongeveer zo uit:</span><span class="sxs-lookup"><span data-stu-id="3f721-161">(Notice the “.\” in that command.) You should see something like this:</span></span></br>

   ![Lijst met modules geladen](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="3f721-163">Voer de `Login-AzureRmAccount` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f721-163">Enter the `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="3f721-164">Geef de referentie-informatie voor het abonnement dat u voor deze zelfstudie gebruiken wilt in het aanmeldingsvenster.</span><span class="sxs-lookup"><span data-stu-id="3f721-164">In the login window, enter the credential information for the subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="3f721-165">Als dit de eerste keer dat u bent aangemeld bij Azure vanaf deze computer is, ziet u een bericht over het toestaan van Microsoft voor het verzamelen van gebruiksgegevens van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f721-165">If this is the first time that you're logging in to Azure from this machine, you will see a message about allowing Microsoft to collect PowerShell usage data.</span></span> <span data-ttu-id="3f721-166">U wordt aangeraden deze gegevensverzameling in te schakelen omdat deze wordt gebruikt voor het verbeteren van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f721-166">We recommend that you enable this data collection because it will be used to improve Azure PowerShell.</span></span>

4. <span data-ttu-id="3f721-167">U bent aangemeld na een geslaagde authenticatie en u de informatie in de volgende schermafbeelding ziet.</span><span class="sxs-lookup"><span data-stu-id="3f721-167">After successful authentication, you're logged in and you see the information in the following screenshot.</span></span> <span data-ttu-id="3f721-168">Noteer de abonnements-ID en de naam van het abonnement, omdat moet u ze later stappen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3f721-168">Take note of the subscription ID and subscription name, because you'll need them to complete later steps.</span></span>

   ![PowerShell-venster](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="3f721-170">Variabelen voor het opslaan van de waarden die wordt later gebruikt maken.</span><span class="sxs-lookup"><span data-stu-id="3f721-170">Create variables to store values that will be used later.</span></span> <span data-ttu-id="3f721-171">Voer de volgende PowerShell-regels.</span><span class="sxs-lookup"><span data-stu-id="3f721-171">Enter each of the following PowerShell lines.</span></span> <span data-ttu-id="3f721-172">Mogelijk moet u de waarden voor uw omgeving aanpassen.</span><span class="sxs-lookup"><span data-stu-id="3f721-172">You might need to adjust the values to match your environment.</span></span>
    - <span data-ttu-id="3f721-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(De abonnementsnaam van uw kan anders zijn.</span><span class="sxs-lookup"><span data-stu-id="3f721-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="3f721-174">U ziet het als onderdeel van de uitvoer van de vorige opdracht.)</span><span class="sxs-lookup"><span data-stu-id="3f721-174">You can see it as part of the output of the previous command.)</span></span>
    - <span data-ttu-id="3f721-175">```$location = 'West US'```(Deze variabele wordt gebruikt om door te geven van de locatie waar de bronnen moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f721-175">```$location = 'West US'``` (This variable will be used to pass the location where resources should be created.</span></span> <span data-ttu-id="3f721-176">U kunt deze variabele om te worden van een willekeurige locatie van uw keuze worden wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="3f721-176">You can change this variable to be any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="3f721-177">``` $name = 'azlogtest' + $random```(De naam kan van alles zijn, maar deze alleen kleine letters en cijfers bevatten.)</span><span class="sxs-lookup"><span data-stu-id="3f721-177">``` $name = 'azlogtest' + $random``` (The name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="3f721-178">``` $storageName = $name```(U kunt deze variabele wordt gebruikt voor de opslagaccountnaam.)</span><span class="sxs-lookup"><span data-stu-id="3f721-178">``` $storageName = $name``` (This variable will be used for the storage account name.)</span></span>
    - <span data-ttu-id="3f721-179">```$rgname = $name ```(U kunt deze variabele wordt gebruikt voor naam van de resourcegroep.)</span><span class="sxs-lookup"><span data-stu-id="3f721-179">```$rgname = $name ``` (This variable will be used for the resource group name.)</span></span>
    - <span data-ttu-id="3f721-180">``` $eventHubNameSpaceName = $name```(Dit is de naam van de event hub-naamruimte.)</span><span class="sxs-lookup"><span data-stu-id="3f721-180">``` $eventHubNameSpaceName = $name``` (This is the name of the event hub namespace.)</span></span>
6. <span data-ttu-id="3f721-181">Geef het abonnement dat u met werkt:</span><span class="sxs-lookup"><span data-stu-id="3f721-181">Specify the subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="3f721-182">Een resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="3f721-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="3f721-183">Als u `$rg` op dit moment ziet u uitvoer die vergelijkbaar is met deze schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="3f721-183">If you enter `$rg` at this point, you should see output similar to this screenshot:</span></span>

   ![Uitvoer na het maken van een resourcegroep](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="3f721-185">Maak een opslagaccount dat wordt gebruikt om informatie over de status bij te houden:</span><span class="sxs-lookup"><span data-stu-id="3f721-185">Create a storage account that will be used to keep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="3f721-186">Maak de event hub-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="3f721-186">Create the event hub namespace.</span></span> <span data-ttu-id="3f721-187">Dit is vereist voor het maken van een event hub.</span><span class="sxs-lookup"><span data-stu-id="3f721-187">This is required to create an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="3f721-188">De regel-ID die wordt gebruikt met de insights-provider niet ophalen:</span><span class="sxs-lookup"><span data-stu-id="3f721-188">Get the rule ID that will be used with the insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="3f721-189">Ophalen van alle mogelijke Azure locaties en de namen toevoegen aan een variabele die kan worden gebruikt in een latere stap:</span><span class="sxs-lookup"><span data-stu-id="3f721-189">Get all possible Azure locations and add the names to a variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="3f721-190">a.</span><span class="sxs-lookup"><span data-stu-id="3f721-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="3f721-191">b.</span><span class="sxs-lookup"><span data-stu-id="3f721-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="3f721-192">Als u `$locations` op dit moment ziet u de locatienamen van de zonder de aanvullende informatie die wordt geretourneerd door Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="3f721-192">If you enter `$locations` at this point, you see the location names without the additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="3f721-193">Een Azure Resource Manager-logboek-profiel maken:</span><span class="sxs-lookup"><span data-stu-id="3f721-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="3f721-194">Zie voor meer informatie over het profiel van de Azure-logboekanalyse [overzicht van de Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="3f721-194">For more information about the Azure log profile, see [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="3f721-195">U mogelijk een foutbericht weergegeven wanneer u probeert een logboek-profiel maken.</span><span class="sxs-lookup"><span data-stu-id="3f721-195">You might get an error message when you try to create a log profile.</span></span> <span data-ttu-id="3f721-196">Vervolgens kunt u de documentatie voor Get-AzureRmLogProfile en verwijder AzureRmLogProfile bekijken.</span><span class="sxs-lookup"><span data-stu-id="3f721-196">You can then review the documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="3f721-197">Als u een Get-AzureRmLogProfile uitvoert, ziet u informatie over het profiel van het logboek.</span><span class="sxs-lookup"><span data-stu-id="3f721-197">If you run Get-AzureRmLogProfile, you see information about the log profile.</span></span> <span data-ttu-id="3f721-198">U kunt het bestaande profiel voor het logboek verwijderen door te voeren de ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3f721-198">You can delete the existing log profile by entering the ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Fout bij het Resource Manager-profiel](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="3f721-200">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="3f721-200">Create a key vault</span></span>

1. <span data-ttu-id="3f721-201">De sleutelkluis maken:</span><span class="sxs-lookup"><span data-stu-id="3f721-201">Create the key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="3f721-202">Logboekregistratie voor de sleutelkluis configureren:</span><span class="sxs-lookup"><span data-stu-id="3f721-202">Configure logging for the key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="3f721-203">Genereren van een activiteit</span><span class="sxs-lookup"><span data-stu-id="3f721-203">Generate log activity</span></span>

<span data-ttu-id="3f721-204">Aanvragen moeten worden verzonden naar de Sleutelkluis voor het genereren van een activiteit.</span><span class="sxs-lookup"><span data-stu-id="3f721-204">Requests need to be sent to Key Vault to generate log activity.</span></span> <span data-ttu-id="3f721-205">Acties zoals genereren van sleutels, geheimen, opslaan of logboekvermeldingen lezen van geheimen van Sleutelkluis maakt.</span><span class="sxs-lookup"><span data-stu-id="3f721-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="3f721-206">De huidige opslagsleutels weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3f721-206">Display the current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="3f721-207">Genereren van een nieuwe **key2**:</span><span class="sxs-lookup"><span data-stu-id="3f721-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="3f721-208">De sleutels opnieuw weergegeven en u ziet dat **key2** bevat een andere waarde:</span><span class="sxs-lookup"><span data-stu-id="3f721-208">Display the keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="3f721-209">Stel en een geheim voor het genereren van aanvullende logboekvermeldingen lezen:</span><span class="sxs-lookup"><span data-stu-id="3f721-209">Set and read a secret to generate additional log entries:</span></span>
    
   <span data-ttu-id="3f721-210">a.</span><span class="sxs-lookup"><span data-stu-id="3f721-210">a.</span></span> <span data-ttu-id="3f721-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="3f721-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Geheime geretourneerd](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="3f721-213">Azure-logboekanalyse-integratie configureren</span><span class="sxs-lookup"><span data-stu-id="3f721-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="3f721-214">Nu dat u hebt de vereiste elementen voor Sleutelkluis naar een event hub-logboekregistratie hebt geconfigureerd, moet u Azure Log-integratie configureren:</span><span class="sxs-lookup"><span data-stu-id="3f721-214">Now that you have configured all the required elements to have Key Vault logging to an event hub, you need to configure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="3f721-215">Voer de opdracht AzLog voor elke event hub:</span><span class="sxs-lookup"><span data-stu-id="3f721-215">Run the AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="3f721-216">Na een minuut of dat van de laatste twee opdrachten uit te voeren, ziet u JSON-bestanden die worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3f721-216">After a minute or so of running the last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="3f721-217">U hebt gecontroleerd of door de bewaking van de map **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="3f721-217">You can confirm that by monitoring the directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f721-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f721-218">Next steps</span></span>

- [<span data-ttu-id="3f721-219">Veelgestelde vragen over Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="3f721-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="3f721-220">Aan de slag met Azure Log-integratie</span><span class="sxs-lookup"><span data-stu-id="3f721-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="3f721-221">Logboeken van de Azure-resources integreren in uw SIEM-systemen</span><span class="sxs-lookup"><span data-stu-id="3f721-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
