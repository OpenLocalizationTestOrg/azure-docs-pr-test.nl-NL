---
title: aaaIntegrate logboeken van Azure Sleutelkluis met behulp van Event Hubs | Microsoft Docs
description: Zelfstudie waarmee Hallo nodige toomake Sleutelkluis aanmeldt beschikbaar tooa SIEM met behulp van de integratie van Azure-logboek
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
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a><span data-ttu-id="b8106-103">Zelfstudie voor Azure Log-integratie: proces Azure Key Vault gebeurtenissen met behulp van Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b8106-103">Azure Log Integration tutorial: Process Azure Key Vault events by using Event Hubs</span></span>

<span data-ttu-id="b8106-104">U kunt gebruiken Azure Log integratiegebeurtenissen tooretrieve vastgelegd en zodat ze beschikbaar tooyour informatie en event management (SIEM) beveiligingssysteem.</span><span class="sxs-lookup"><span data-stu-id="b8106-104">You can use Azure Log Integration tooretrieve logged events and make them available tooyour security information and event management (SIEM) system.</span></span> <span data-ttu-id="b8106-105">Deze zelfstudie toont een voorbeeld van hoe Azure Log integratie gebruikte tooprocess logboeken die zijn verkregen via Azure Event Hubs kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="b8106-105">This tutorial shows an example of how Azure Log Integration can be used tooprocess logs that are acquired through Azure Event Hubs.</span></span>
 
<span data-ttu-id="b8106-106">Gebruik deze zelfstudie tooget te weten komen over hoe Azure Log-integratie en Event Hubs werk samen met de volgende voorbeelden van stappen Hallo en kennis van hoe elke stap Hallo-oplossing ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="b8106-106">Use this tutorial tooget acquainted with how Azure Log Integration and Event Hubs work together by following hello example steps and understanding how each step supports hello solution.</span></span> <span data-ttu-id="b8106-107">En u wat nemen kunt u hebt geleerd hier toocreate uw eigen toosupport stappen unieke vereisten van uw bedrijf.</span><span class="sxs-lookup"><span data-stu-id="b8106-107">Then you can take what you’ve learned here toocreate your own steps toosupport your company’s unique requirements.</span></span>

>[!WARNING]
<span data-ttu-id="b8106-108">Hallo stappen en opdrachten in deze zelfstudie zijn niet bedoeld toobe gekopieerd en geplakt.</span><span class="sxs-lookup"><span data-stu-id="b8106-108">hello steps and commands in this tutorial are not intended toobe copied and pasted.</span></span> <span data-ttu-id="b8106-109">Ze zijn alleen voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="b8106-109">They're examples only.</span></span> <span data-ttu-id="b8106-110">Gebruik geen Hallo PowerShell-opdrachten 'als zodanig' in uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b8106-110">Do not use hello PowerShell commands “as is” in your live environment.</span></span> <span data-ttu-id="b8106-111">U moet deze op basis van uw omgeving aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b8106-111">You must customize them based on your unique environment.</span></span>


<span data-ttu-id="b8106-112">Deze zelfstudie wordt u begeleid Hallo proces duurt Azure Key Vault activiteit vastgelegd tooan event hub en het beschikbaar als JSON-bestanden tooyour SIEM-systeem.</span><span class="sxs-lookup"><span data-stu-id="b8106-112">This tutorial walks you through hello process of taking Azure Key Vault activity logged tooan event hub and making it available as JSON files tooyour SIEM system.</span></span> <span data-ttu-id="b8106-113">Vervolgens kunt u uw SIEM-systeem tooprocess Hallo JSON-bestanden.</span><span class="sxs-lookup"><span data-stu-id="b8106-113">You can then configure your SIEM system tooprocess hello JSON files.</span></span>

>[!NOTE]
><span data-ttu-id="b8106-114">De meeste Hallo stappen in deze zelfstudie hebben betrekking op het configureren van sleutelkluizen, opslagaccounts en event hubs.</span><span class="sxs-lookup"><span data-stu-id="b8106-114">Most of hello steps in this tutorial involve configuring key vaults, storage accounts, and event hubs.</span></span> <span data-ttu-id="b8106-115">Hallo specifieke Azure Log integratiestappen zijn Hallo einde van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b8106-115">hello specific Azure Log Integration steps are at hello end of this tutorial.</span></span> <span data-ttu-id="b8106-116">Voer deze stappen niet uit in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="b8106-116">Do not perform these steps in a production environment.</span></span> <span data-ttu-id="b8106-117">Ze zijn bedoeld voor een testomgeving alleen.</span><span class="sxs-lookup"><span data-stu-id="b8106-117">They are intended for a lab environment only.</span></span> <span data-ttu-id="b8106-118">Voordat u ze in productie, moet u Hallo stappen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="b8106-118">You must customize hello steps before using them in production.</span></span>

<span data-ttu-id="b8106-119">Informatie verstrekt langs Hallo manier helpt dat u begrijpen Hallo redenen achter elke stap.</span><span class="sxs-lookup"><span data-stu-id="b8106-119">Information provided along hello way helps you understand hello reasons behind each step.</span></span> <span data-ttu-id="b8106-120">Koppelingen tooother artikelen kunnen u meer details op bepaalde onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="b8106-120">Links tooother articles give you more detail on certain topics.</span></span>

<span data-ttu-id="b8106-121">Zie voor meer informatie over Hallo-services die in deze zelfstudie wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="b8106-121">For more information about hello services that this tutorial mentions, see:</span></span> 

- [<span data-ttu-id="b8106-122">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="b8106-122">Azure Key Vault</span></span>](../key-vault/key-vault-whatis.md)
- [<span data-ttu-id="b8106-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b8106-123">Azure Event Hubs</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
- [<span data-ttu-id="b8106-124">Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="b8106-124">Azure Log Integration</span></span>](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a><span data-ttu-id="b8106-125">Eerste installatie</span><span class="sxs-lookup"><span data-stu-id="b8106-125">Initial setup</span></span>

<span data-ttu-id="b8106-126">Voordat u de stappen in dit artikel Hallo voltooien kunt, moet u Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="b8106-126">Before you can complete hello steps in this article, you need hello following:</span></span>

1. <span data-ttu-id="b8106-127">Een Azure-abonnement en de account op dat abonnement met beheerdersrechten.</span><span class="sxs-lookup"><span data-stu-id="b8106-127">An Azure subscription and account on that subscription with administrator rights.</span></span> <span data-ttu-id="b8106-128">Als u geen een abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="b8106-128">If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/).</span></span>
 
2. <span data-ttu-id="b8106-129">Een systeem met toegang toohello internet die voldoet aan vereisten voor het installeren van de integratie van Azure Log Hallo.</span><span class="sxs-lookup"><span data-stu-id="b8106-129">A system with access toohello internet that meets hello requirements for installing Azure Log Integration.</span></span> <span data-ttu-id="b8106-130">Hallo-systeem kan op een cloudservice of lokale gehost.</span><span class="sxs-lookup"><span data-stu-id="b8106-130">hello system can be on a cloud service or hosted on-premises.</span></span>

3. <span data-ttu-id="b8106-131">[Integratie van Azure Log](https://www.microsoft.com/download/details.aspx?id=53324) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b8106-131">[Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) installed.</span></span> <span data-ttu-id="b8106-132">tooinstall het:</span><span class="sxs-lookup"><span data-stu-id="b8106-132">tooinstall it:</span></span>

   <span data-ttu-id="b8106-133">a.</span><span class="sxs-lookup"><span data-stu-id="b8106-133">a.</span></span> <span data-ttu-id="b8106-134">Gebruik extern bureaublad tooconnect toohello system vermeld in stap 2.</span><span class="sxs-lookup"><span data-stu-id="b8106-134">Use Remote Desktop tooconnect toohello system mentioned in step 2.</span></span>   
   <span data-ttu-id="b8106-135">b.</span><span class="sxs-lookup"><span data-stu-id="b8106-135">b.</span></span> <span data-ttu-id="b8106-136">Kopieer hello Azure Log integratie installatieprogramma toohello system.</span><span class="sxs-lookup"><span data-stu-id="b8106-136">Copy hello Azure Log Integration installer toohello system.</span></span> <span data-ttu-id="b8106-137">U kunt [Hallo installatiebestanden downloaden](https://www.microsoft.com/download/details.aspx?id=53324).</span><span class="sxs-lookup"><span data-stu-id="b8106-137">You can [download hello installation files](https://www.microsoft.com/download/details.aspx?id=53324).</span></span>   
   <span data-ttu-id="b8106-138">c.</span><span class="sxs-lookup"><span data-stu-id="b8106-138">c.</span></span> <span data-ttu-id="b8106-139">Hallo-installatieprogramma start en Hallo-licentievoorwaarden voor Microsoft-Software accepteren.</span><span class="sxs-lookup"><span data-stu-id="b8106-139">Start hello installer and accept hello Microsoft Software License Terms.</span></span>   
   <span data-ttu-id="b8106-140">d.</span><span class="sxs-lookup"><span data-stu-id="b8106-140">d.</span></span> <span data-ttu-id="b8106-141">Als u telemetrie informatie opgeeft wordt, laat u Hallo selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b8106-141">If you will provide telemetry information, leave hello check box selected.</span></span> <span data-ttu-id="b8106-142">Schakel Hallo selectievakje uit als u gebruik van informatie tooMicrosoft in plaats daarvan niet verzenden.</span><span class="sxs-lookup"><span data-stu-id="b8106-142">If you'd rather not send usage information tooMicrosoft, clear hello check box.</span></span>
   
   <span data-ttu-id="b8106-143">Voor meer informatie over de integratie van Azure-logboek en hoe tooinstall, Zie [Azure Log integratie met Azure Diagnostics logboekregistratie en Windows Event Forwarding](security-azure-log-integration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b8106-143">For more information about Azure Log Integration and how tooinstall it, see [Azure Log Integration with Azure Diagnostics logging and Windows Event Forwarding](security-azure-log-integration-get-started.md).</span></span>

4. <span data-ttu-id="b8106-144">Hallo nieuwste PowerShell-versie.</span><span class="sxs-lookup"><span data-stu-id="b8106-144">hello latest PowerShell version.</span></span>
 
   <span data-ttu-id="b8106-145">Als u Windows Server 2016 geïnstalleerd hebt, hebt u ten minste PowerShell 5.0.</span><span class="sxs-lookup"><span data-stu-id="b8106-145">If you have Windows Server 2016 installed, then you have at least PowerShell 5.0.</span></span> <span data-ttu-id="b8106-146">Als u een andere versie van Windows Server, hebt u mogelijk een oudere versie van PowerShell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b8106-146">If you're using any other version of Windows Server, you might have an earlier version of PowerShell installed.</span></span> <span data-ttu-id="b8106-147">U kunt Hallo versie controleren door te voeren ```get-host``` in een PowerShell-venster.</span><span class="sxs-lookup"><span data-stu-id="b8106-147">You can check hello version by entering ```get-host``` in a PowerShell window.</span></span> <span data-ttu-id="b8106-148">Als er geen PowerShell 5.0 is geïnstalleerd, kunt u [downloaden](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="b8106-148">If you don't have PowerShell 5.0 installed, you can [download it](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>

   <span data-ttu-id="b8106-149">Nadat u ten minste hebt PowerShell 5.0, kunt u de meest recente versie van tooinstall Hallo doorgaan:</span><span class="sxs-lookup"><span data-stu-id="b8106-149">After you have at least PowerShell 5.0, you can proceed tooinstall hello latest version:</span></span>
   
   <span data-ttu-id="b8106-150">a.</span><span class="sxs-lookup"><span data-stu-id="b8106-150">a.</span></span> <span data-ttu-id="b8106-151">Voer in een PowerShell-venster Hallo ```Install-Module Azure``` opdracht.</span><span class="sxs-lookup"><span data-stu-id="b8106-151">In a PowerShell window, enter hello ```Install-Module Azure``` command.</span></span> <span data-ttu-id="b8106-152">Hallo installatiestappen voltooien.</span><span class="sxs-lookup"><span data-stu-id="b8106-152">Complete hello installation steps.</span></span>    
   <span data-ttu-id="b8106-153">b.</span><span class="sxs-lookup"><span data-stu-id="b8106-153">b.</span></span> <span data-ttu-id="b8106-154">Voer Hallo ```Install-Module AzureRM``` opdracht.</span><span class="sxs-lookup"><span data-stu-id="b8106-154">Enter hello ```Install-Module AzureRM``` command.</span></span> <span data-ttu-id="b8106-155">Hallo installatiestappen voltooien.</span><span class="sxs-lookup"><span data-stu-id="b8106-155">Complete hello installation steps.</span></span>

   <span data-ttu-id="b8106-156">Zie voor meer informatie [Azure PowerShell installeren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="b8106-156">For more information, see [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span>


## <a name="create-supporting-infrastructure-elements"></a><span data-ttu-id="b8106-157">Ondersteunende Infrastructuurelementen maken</span><span class="sxs-lookup"><span data-stu-id="b8106-157">Create supporting infrastructure elements</span></span>

1. <span data-ttu-id="b8106-158">Open een PowerShell-venster met verhoogde bevoegdheid en gaat u te**C:\Program Files\Microsoft Azure Log integratie**.</span><span class="sxs-lookup"><span data-stu-id="b8106-158">Open an elevated PowerShell window and go too**C:\Program Files\Microsoft Azure Log Integration**.</span></span>
2. <span data-ttu-id="b8106-159">Importeer Hallo AzLog cmdlets Hallo script LoadAzLogModule.ps1 uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b8106-159">Import hello AzLog cmdlets by running hello script LoadAzLogModule.ps1.</span></span> <span data-ttu-id="b8106-160">Voer Hallo `.\LoadAzLogModule.ps1` opdracht.</span><span class="sxs-lookup"><span data-stu-id="b8106-160">Enter hello `.\LoadAzLogModule.ps1` command.</span></span> <span data-ttu-id="b8106-161">(Kennisgeving Hallo ". \ ' in die opdracht.) Deze lijst ziet er ongeveer zo uit:</span><span class="sxs-lookup"><span data-stu-id="b8106-161">(Notice hello “.\” in that command.) You should see something like this:</span></span></br>

   ![Lijst met modules geladen](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. <span data-ttu-id="b8106-163">Voer Hallo `Login-AzureRmAccount` opdracht.</span><span class="sxs-lookup"><span data-stu-id="b8106-163">Enter hello `Login-AzureRmAccount` command.</span></span> <span data-ttu-id="b8106-164">Voer in Hallo aanmeldingsvenster Hallo referentie-informatie voor Hallo-abonnement dat u voor deze zelfstudie gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="b8106-164">In hello login window, enter hello credential information for hello subscription that you will use for this tutorial.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b8106-165">Als dit Hallo eerste keer is dat u in tooAzure van deze computer aanmeldt zich is, ziet u een bericht over het toestaan van gebruiksgegevens van Microsoft toocollect PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8106-165">If this is hello first time that you're logging in tooAzure from this machine, you will see a message about allowing Microsoft toocollect PowerShell usage data.</span></span> <span data-ttu-id="b8106-166">U wordt aangeraden deze gegevensverzameling in te schakelen omdat het gebruikte tooimprove Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8106-166">We recommend that you enable this data collection because it will be used tooimprove Azure PowerShell.</span></span>

4. <span data-ttu-id="b8106-167">U bent aangemeld en ziet u de informatie in de volgende schermafbeelding Hallo Hallo na een geslaagde authenticatie.</span><span class="sxs-lookup"><span data-stu-id="b8106-167">After successful authentication, you're logged in and you see hello information in hello following screenshot.</span></span> <span data-ttu-id="b8106-168">Let op Hallo abonnement-ID en -abonnement naam, omdat u moet deze stappen toocomplete later.</span><span class="sxs-lookup"><span data-stu-id="b8106-168">Take note of hello subscription ID and subscription name, because you'll need them toocomplete later steps.</span></span>

   ![PowerShell-venster](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. <span data-ttu-id="b8106-170">Variabelen toostore waarden maken die later worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b8106-170">Create variables toostore values that will be used later.</span></span> <span data-ttu-id="b8106-171">Geef alle Hallo volgende PowerShell-regels.</span><span class="sxs-lookup"><span data-stu-id="b8106-171">Enter each of hello following PowerShell lines.</span></span> <span data-ttu-id="b8106-172">Mogelijk moet u tooadjust Hallo waarden toomatch uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="b8106-172">You might need tooadjust hello values toomatch your environment.</span></span>
    - <span data-ttu-id="b8106-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(De abonnementsnaam van uw kan anders zijn.</span><span class="sxs-lookup"><span data-stu-id="b8106-173">```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (Your subscription name might be different.</span></span> <span data-ttu-id="b8106-174">U ziet het als onderdeel van de uitvoer van de vorige opdracht Hallo Hallo.)</span><span class="sxs-lookup"><span data-stu-id="b8106-174">You can see it as part of hello output of hello previous command.)</span></span>
    - <span data-ttu-id="b8106-175">```$location = 'West US'```(Deze variabele niet gebruikte toopass Hallo locatie waar de bronnen moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b8106-175">```$location = 'West US'``` (This variable will be used toopass hello location where resources should be created.</span></span> <span data-ttu-id="b8106-176">U kunt deze variabele toobe elke locatie wijzigen van uw keuze.)</span><span class="sxs-lookup"><span data-stu-id="b8106-176">You can change this variable toobe any location of your choosing.)</span></span>
    - ```$random = Get-Random```
    - <span data-ttu-id="b8106-177">``` $name = 'azlogtest' + $random```(Hallo-naam kan van alles zijn, maar deze alleen kleine letters en cijfers bevatten.)</span><span class="sxs-lookup"><span data-stu-id="b8106-177">``` $name = 'azlogtest' + $random``` (hello name can be anything, but it should include only lowercase letters and numbers.)</span></span>
    - <span data-ttu-id="b8106-178">``` $storageName = $name```(U kunt deze variabele wordt gebruikt voor de opslagaccountnaam Hallo.)</span><span class="sxs-lookup"><span data-stu-id="b8106-178">``` $storageName = $name``` (This variable will be used for hello storage account name.)</span></span>
    - <span data-ttu-id="b8106-179">```$rgname = $name ```(U kunt deze variabele wordt gebruikt voor naam resourcegroep Hallo.)</span><span class="sxs-lookup"><span data-stu-id="b8106-179">```$rgname = $name ``` (This variable will be used for hello resource group name.)</span></span>
    - <span data-ttu-id="b8106-180">``` $eventHubNameSpaceName = $name```(Dit is de naam Hallo van Hallo event hub-naamruimte.)</span><span class="sxs-lookup"><span data-stu-id="b8106-180">``` $eventHubNameSpaceName = $name``` (This is hello name of hello event hub namespace.)</span></span>
6. <span data-ttu-id="b8106-181">Geef Hallo-abonnement dat u met werkt:</span><span class="sxs-lookup"><span data-stu-id="b8106-181">Specify hello subscription that you will be working with:</span></span>
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. <span data-ttu-id="b8106-182">Een resourcegroep maken:</span><span class="sxs-lookup"><span data-stu-id="b8106-182">Create a resource group:</span></span>
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   <span data-ttu-id="b8106-183">Als u `$rg` op dit moment ziet u uitvoer vergelijkbare toothis schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="b8106-183">If you enter `$rg` at this point, you should see output similar toothis screenshot:</span></span>

   ![Uitvoer na het maken van een resourcegroep](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. <span data-ttu-id="b8106-185">Een opslagaccount die gebruikt tookeep bijhouden van informatie over de status worden maken:</span><span class="sxs-lookup"><span data-stu-id="b8106-185">Create a storage account that will be used tookeep track of state information:</span></span>
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. <span data-ttu-id="b8106-186">Hallo event hub-naamruimte maken.</span><span class="sxs-lookup"><span data-stu-id="b8106-186">Create hello event hub namespace.</span></span> <span data-ttu-id="b8106-187">Dit is vereiste toocreate een event hub.</span><span class="sxs-lookup"><span data-stu-id="b8106-187">This is required toocreate an event hub.</span></span>
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. <span data-ttu-id="b8106-188">Hallo regel-ID die wordt gebruikt met Hallo insights provider ophalen:</span><span class="sxs-lookup"><span data-stu-id="b8106-188">Get hello rule ID that will be used with hello insights provider:</span></span>
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. <span data-ttu-id="b8106-189">Ophalen van alle mogelijke Azure locaties en Hallo namen tooa variabele die kan worden gebruikt in een later stadium toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b8106-189">Get all possible Azure locations and add hello names tooa variable that can be used in a later step:</span></span>
    
    <span data-ttu-id="b8106-190">a.</span><span class="sxs-lookup"><span data-stu-id="b8106-190">a.</span></span> ```$locationObjects = Get-AzureRMLocation```    
    <span data-ttu-id="b8106-191">b.</span><span class="sxs-lookup"><span data-stu-id="b8106-191">b.</span></span> ```$locations = @('global') + $locationobjects.location```
    
    <span data-ttu-id="b8106-192">Als u `$locations` op dit moment ziet u Hallo locatienamen zonder Hallo aanvullende informatie die wordt geretourneerd door Get-AzureRmLocation.</span><span class="sxs-lookup"><span data-stu-id="b8106-192">If you enter `$locations` at this point, you see hello location names without hello additional information returned by Get-AzureRmLocation.</span></span>
12. <span data-ttu-id="b8106-193">Een Azure Resource Manager-logboek-profiel maken:</span><span class="sxs-lookup"><span data-stu-id="b8106-193">Create an Azure Resource Manager log profile:</span></span> 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    <span data-ttu-id="b8106-194">Zie voor meer informatie over Azure-logboekanalyse profiel Hallo [overzicht van hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="b8106-194">For more information about hello Azure log profile, see [Overview of hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b8106-195">U mogelijk een foutbericht weergegeven wanneer u een profiel voor een logboek toocreate probeert.</span><span class="sxs-lookup"><span data-stu-id="b8106-195">You might get an error message when you try toocreate a log profile.</span></span> <span data-ttu-id="b8106-196">U kunt vervolgens Hallo-documentatie voor Get-AzureRmLogProfile en verwijder AzureRmLogProfile bekijken.</span><span class="sxs-lookup"><span data-stu-id="b8106-196">You can then review hello documentation for Get-AzureRmLogProfile and Remove-AzureRmLogProfile.</span></span> <span data-ttu-id="b8106-197">Als u een Get-AzureRmLogProfile uitvoert, ziet u informatie over Hallo logboek profiel.</span><span class="sxs-lookup"><span data-stu-id="b8106-197">If you run Get-AzureRmLogProfile, you see information about hello log profile.</span></span> <span data-ttu-id="b8106-198">Kunt u het bestaande logboek profiel Hallo verwijderen door te voeren Hallo ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` opdracht.</span><span class="sxs-lookup"><span data-stu-id="b8106-198">You can delete hello existing log profile by entering hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` command.</span></span>
>
>![Fout bij het Resource Manager-profiel](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a><span data-ttu-id="b8106-200">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="b8106-200">Create a key vault</span></span>

1. <span data-ttu-id="b8106-201">Hallo sleutelkluis maakt:</span><span class="sxs-lookup"><span data-stu-id="b8106-201">Create hello key vault:</span></span>

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. <span data-ttu-id="b8106-202">Logboekregistratie voor sleutelkluis Hallo configureren:</span><span class="sxs-lookup"><span data-stu-id="b8106-202">Configure logging for hello key vault:</span></span>

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a><span data-ttu-id="b8106-203">Genereren van een activiteit</span><span class="sxs-lookup"><span data-stu-id="b8106-203">Generate log activity</span></span>

<span data-ttu-id="b8106-204">Aanvragen moeten toobe tooKey kluis toogenerate logboek activiteit verzonden.</span><span class="sxs-lookup"><span data-stu-id="b8106-204">Requests need toobe sent tooKey Vault toogenerate log activity.</span></span> <span data-ttu-id="b8106-205">Acties zoals genereren van sleutels, geheimen, opslaan of logboekvermeldingen lezen van geheimen van Sleutelkluis maakt.</span><span class="sxs-lookup"><span data-stu-id="b8106-205">Actions like key generation, storing secrets, or reading secrets from Key Vault will create log entries.</span></span>

1. <span data-ttu-id="b8106-206">De huidige opslagsleutels Hallo weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b8106-206">Display hello current storage keys:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. <span data-ttu-id="b8106-207">Genereren van een nieuwe **key2**:</span><span class="sxs-lookup"><span data-stu-id="b8106-207">Generate a new **key2**:</span></span>
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. <span data-ttu-id="b8106-208">Hallo sleutels opnieuw weergegeven en u ziet dat **key2** bevat een andere waarde:</span><span class="sxs-lookup"><span data-stu-id="b8106-208">Display hello keys again and see that **key2** holds a different value:</span></span>
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. <span data-ttu-id="b8106-209">Te stellen en een geheime toogenerate extra logboekvermeldingen lezen:</span><span class="sxs-lookup"><span data-stu-id="b8106-209">Set and read a secret toogenerate additional log entries:</span></span>
    
   <span data-ttu-id="b8106-210">a.</span><span class="sxs-lookup"><span data-stu-id="b8106-210">a.</span></span> <span data-ttu-id="b8106-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span><span class="sxs-lookup"><span data-stu-id="b8106-211">```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b.</span></span> ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Geheime geretourneerd](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a><span data-ttu-id="b8106-213">Azure-logboekanalyse-integratie configureren</span><span class="sxs-lookup"><span data-stu-id="b8106-213">Configure Azure Log Integration</span></span>

<span data-ttu-id="b8106-214">Nu u alle Hallo vereiste elementen toohave logboekregistratie van Sleutelkluis tooan event hub hebt geconfigureerd, moet u tooconfigure Azure Log integratie:</span><span class="sxs-lookup"><span data-stu-id="b8106-214">Now that you have configured all hello required elements toohave Key Vault logging tooan event hub, you need tooconfigure Azure Log Integration:</span></span>

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

<span data-ttu-id="b8106-215">Voer Hallo AzLog opdracht voor elke event hub:</span><span class="sxs-lookup"><span data-stu-id="b8106-215">Run hello AzLog command for each event hub:</span></span>

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

<span data-ttu-id="b8106-216">Na een minuut of dus Hallo laatste twee opdrachten uitgevoerd, ziet u JSON-bestanden die worden gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="b8106-216">After a minute or so of running hello last two commands, you should see JSON files being generated.</span></span> <span data-ttu-id="b8106-217">U hebt gecontroleerd of door de bewaking van Hallo directory **C:\users\AzLog\EventHubJson**.</span><span class="sxs-lookup"><span data-stu-id="b8106-217">You can confirm that by monitoring hello directory **C:\users\AzLog\EventHubJson**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8106-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b8106-218">Next steps</span></span>

- [<span data-ttu-id="b8106-219">Veelgestelde vragen over Azure-logboekanalyse-integratie</span><span class="sxs-lookup"><span data-stu-id="b8106-219">Azure Log Integration FAQ</span></span>](security-azure-log-integration-faq.md)
- [<span data-ttu-id="b8106-220">Aan de slag met Azure Log-integratie</span><span class="sxs-lookup"><span data-stu-id="b8106-220">Get started with Azure Log Integration</span></span>](security-azure-log-integration-get-started.md)
- [<span data-ttu-id="b8106-221">Logboeken van de Azure-resources integreren in uw SIEM-systemen</span><span class="sxs-lookup"><span data-stu-id="b8106-221">Integrate logs from Azure resources into your SIEM systems</span></span>](security-azure-log-integration-overview.md)
