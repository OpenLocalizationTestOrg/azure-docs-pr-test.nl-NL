---
title: 'Azure AD Connect-synchronisatie: operationele taken en overwegingen | Microsoft Docs'
description: Dit onderwerp beschrijft operationele taken voor Azure AD Connect-synchronisatie en voorbereiden voor de werking van dit onderdeel.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="fb1c0-103">Azure AD Connect-synchronisatie: operationele taken en afweging</span><span class="sxs-lookup"><span data-stu-id="fb1c0-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="fb1c0-104">Het doel van dit onderwerp is om operationele taken voor Azure AD Connect-synchronisatie te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="fb1c0-105">Faseringsmodus</span><span class="sxs-lookup"><span data-stu-id="fb1c0-105">Staging mode</span></span>
<span data-ttu-id="fb1c0-106">De faseringsmodus kan worden gebruikt voor verschillende scenario's, waaronder:</span><span class="sxs-lookup"><span data-stu-id="fb1c0-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="fb1c0-107">Hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-107">High availability.</span></span>
* <span data-ttu-id="fb1c0-108">Testen en implementeren van nieuwe wijzigingen in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="fb1c0-109">Introduceert een nieuwe server en de oude uit bedrijf nemen.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="fb1c0-110">U kunt wijzigingen aanbrengen in de configuratie en de wijzigingen bekijken voordat u de server actief maken met een server in de faseringsmodus.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="fb1c0-111">Ook kunt u volledige import en een volledige synchronisatie om te verifiëren dat alle wijzigingen worden verwacht, voordat u deze wijzigingen in uw productieomgeving aanbrengt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="fb1c0-112">Tijdens de installatie, kunt u de server zich in **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="fb1c0-113">Hiermee wordt de server actief is voor de import en synchronisatie, maar eventuele uitvoer kan niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="fb1c0-114">Een server in de faseringsmodus is Wachtwoordsynchronisatie of wachtwoord terugschrijven niet actief, zelfs als u deze functies ingeschakeld tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="fb1c0-115">Wanneer u de faseringsmodus uitschakelt, de server is, wordt het exporteren wordt gestart, schakelt Wachtwoordsynchronisatie en wachtwoord terugschrijven maakt.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="fb1c0-116">U kunt nog steeds exporteren van een afdwingen met behulp van synchronization servicemanager.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="fb1c0-117">Een server in de faseringsmodus blijft ontvangen van wijzigingen van Active Directory en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="fb1c0-118">Heeft altijd een kopie van de meest recente wijzigingen en kunnen zeer snel uitvoeren via de verantwoordelijkheden van een andere server.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="fb1c0-119">Als u configuratiewijzigingen in de primaire server aanbrengt, is uw verantwoordelijkheid om dezelfde wijzigingen aanbrengen op de server in de faseringsmodus.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="fb1c0-120">De faseringsmodus is voor mensen met kennis van de oudere synchronisatie-technologieën, anders omdat de server een eigen SQL-database heeft.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="fb1c0-121">Deze architectuur kan de modus server met tijdelijke bestanden zich bevinden in een ander datacenter.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="fb1c0-122">Controleer de configuratie van een server</span><span class="sxs-lookup"><span data-stu-id="fb1c0-122">Verify the configuration of a server</span></span>
<span data-ttu-id="fb1c0-123">Als u wilt toepassen op deze methode, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="fb1c0-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="fb1c0-124">Voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fb1c0-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="fb1c0-125">Configuratie</span><span class="sxs-lookup"><span data-stu-id="fb1c0-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="fb1c0-126">Importeren en synchroniseren</span><span class="sxs-lookup"><span data-stu-id="fb1c0-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="fb1c0-127">Controleer of</span><span class="sxs-lookup"><span data-stu-id="fb1c0-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="fb1c0-128">Actieve switchserver</span><span class="sxs-lookup"><span data-stu-id="fb1c0-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="fb1c0-129">Voorbereiden</span><span class="sxs-lookup"><span data-stu-id="fb1c0-129">Prepare</span></span>
1. <span data-ttu-id="fb1c0-130">Azure AD Connect installeert, selecteert u **faseringsmodus**, en deselecteren **synchronisatie starten** op de laatste pagina van de installatiewizard.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="fb1c0-131">Deze modus kunt u de synchronisatie-engine handmatig uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="fb1c0-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="fb1c0-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="fb1c0-133">Meld u af/aanmelding in en selecteer menu start in **synchronisatieservice**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="fb1c0-134">Configuratie</span><span class="sxs-lookup"><span data-stu-id="fb1c0-134">Configuration</span></span>
<span data-ttu-id="fb1c0-135">Als u aangepaste wijzigingen hebt aangebracht in de primaire server en u wilt vergelijken van de configuratie met de staging-server, gebruikt u [documentatie voor Azure AD Connect-configuratie](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="fb1c0-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="fb1c0-136">Importeren en synchroniseren</span><span class="sxs-lookup"><span data-stu-id="fb1c0-136">Import and Synchronize</span></span>
1. <span data-ttu-id="fb1c0-137">Selecteer **Connectors**, en selecteer de eerste Connector met het type **Active Directory Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="fb1c0-138">Klik op **uitvoeren**, selecteer **volledige import**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="fb1c0-139">Voer deze stappen uit voor alle Connectors van dit type.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="fb1c0-140">Selecteer de Connector met het type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="fb1c0-141">Klik op **uitvoeren**, selecteer **volledige import**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="fb1c0-142">Zorg ervoor dat het tabblad Connectors nog steeds is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="fb1c0-143">Voor elke Connector met het type **Active Directory Domain Services**, klikt u op **uitvoeren**, selecteer **Deltasynchronisatie**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="fb1c0-144">Selecteer de Connector met het type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="fb1c0-145">Klik op **uitvoeren**, selecteer **Deltasynchronisatie**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="fb1c0-146">U hebt nu gefaseerde export wijzigingen naar Azure AD en on-premises AD (als u hybride implementatie voor Exchange).</span><span class="sxs-lookup"><span data-stu-id="fb1c0-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="fb1c0-147">De volgende stappen kunnen u controleren wat bijna wordt gewijzigd voordat u de uitvoer naar de mappen daadwerkelijk wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="fb1c0-148">Verifiëren</span><span class="sxs-lookup"><span data-stu-id="fb1c0-148">Verify</span></span>
1. <span data-ttu-id="fb1c0-149">Start een opdrachtprompt en Ga naar`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="fb1c0-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="fb1c0-150">Voer: `csexport "Name of Connector" %temp%\export.xml /f:x` de naam van de Connector vindt u in de synchronisatieservice.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="fb1c0-151">Een naam die vergelijkbaar is met 'contoso.com – AAD' voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="fb1c0-152">Kopieer het PowerShell-script uit de sectie [CSAnalyzer](#appendix-csanalyzer) naar een bestand met de naam `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="fb1c0-153">Open een PowerShell-venster en blader naar de map waar u het PowerShell-script hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="fb1c0-154">Voer: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="fb1c0-155">U hebt nu een bestand met de naam **processedusers1.csv** die kan worden onderzocht in Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="fb1c0-156">Alle wijzigingen die zijn voorbereid om te worden geëxporteerd naar Azure AD zijn gevonden in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="fb1c0-157">Noodzakelijke wijzigingen aanbrengen in de gegevens of configuratie en voer deze stappen opnieuw (importeren en synchroniseren en controleer of) totdat de wijzigingen die zijn geëxporteerd worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="fb1c0-158">Actieve switchserver</span><span class="sxs-lookup"><span data-stu-id="fb1c0-158">Switch active server</span></span>
1. <span data-ttu-id="fb1c0-159">Op de momenteel actieve server uitschakelen (FIM-DirSync/Azure AD Sync) van de server zodat deze niet worden geëxporteerd naar Azure AD of stel deze in de faseringsmodus (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="fb1c0-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="fb1c0-160">De installatiewizard uitvoeren op de server in **faseringsmodus** en uitschakelen **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="fb1c0-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="fb1c0-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="fb1c0-162">Herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="fb1c0-162">Disaster recovery</span></span>
<span data-ttu-id="fb1c0-163">Onderdeel van het implementatieontwerp is het plannen voor wat te doen als er een ramp optreedt waarbij u de synchronisatieserver verliezen.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="fb1c0-164">Er zijn verschillende modellen moet gebruiken en welke een om te gebruiken is afhankelijk van verschillende factoren, waaronder:</span><span class="sxs-lookup"><span data-stu-id="fb1c0-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="fb1c0-165">Wat is uw tolerantie voor niet dat deze wijzigingen kunnen aanbrengen op objecten in Azure AD tijdens de uitvaltijd?</span><span class="sxs-lookup"><span data-stu-id="fb1c0-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="fb1c0-166">Als u synchronisatie van wachtwoorden, de gebruikers accepteert dat ze hebben het oude wachtwoord in Azure AD gebruiken als ze deze lokale wijzigen?</span><span class="sxs-lookup"><span data-stu-id="fb1c0-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="fb1c0-167">Hebt u een afhankelijkheid op realtime bewerkingen, zoals wachtwoord terugschrijven?</span><span class="sxs-lookup"><span data-stu-id="fb1c0-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="fb1c0-168">Afhankelijk van de antwoorden op deze vragen en beleid van uw organisatie, kan een van de volgende strategieën worden geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="fb1c0-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="fb1c0-169">Opnieuw opbouwen wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-169">Rebuild when needed.</span></span>
* <span data-ttu-id="fb1c0-170">Een ongebruikte stand-by-server, ook wel **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="fb1c0-171">Gebruik virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-171">Use virtual machines.</span></span>

<span data-ttu-id="fb1c0-172">Als u niet de ingebouwde SQL Express-database gebruikt, wordt ook rekening met de [SQL maximale beschikbaarheid](#sql-high-availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="fb1c0-173">Opnieuw opbouwen wanneer deze nodig is</span><span class="sxs-lookup"><span data-stu-id="fb1c0-173">Rebuild when needed</span></span>
<span data-ttu-id="fb1c0-174">Een strategie voor een praktische is voor het plannen van de server opnieuw opbouwen wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="fb1c0-175">Normaal gesproken installeert het synchronisatie-engine en voert u die de initiële importeren en de synchronisatie kunnen worden uitgevoerd binnen een paar uur.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="fb1c0-176">Als er niet een vervangende server beschikbaar is, is het mogelijk om tijdelijk met een domeincontroller voor het hosten van de synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="fb1c0-177">De synchronisatie-engine-server worden niet opgeslagen voor elke status over de objecten zodat de database kan worden gemaakt van de gegevens in Active Directory en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="fb1c0-178">De **sourceAnchor** kenmerk wordt gebruikt om lid van de objecten uit de on-premises en de cloud.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="fb1c0-179">Als u de server met bestaande objecten on-premises en de cloud opnieuw maken, klikt u vervolgens de synchronisatie-engine komt overeen met die objecten samen opnieuw op opnieuw installeren.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="fb1c0-180">De zaken die u wilt vastleggen en opslaan zijn de configuratiewijzigingen van de server, zoals filteren en synchronisatieregels.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="fb1c0-181">Deze aangepaste configuraties moeten opnieuw worden toegepast voordat u begint te synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="fb1c0-182">Een ongebruikte stand-by-server - faseringsmodus</span><span class="sxs-lookup"><span data-stu-id="fb1c0-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="fb1c0-183">Als u een meer complexe omgeving hebt, wordt klikt u vervolgens met een of meer stand-by-servers aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="fb1c0-184">Tijdens de installatie, kunt u een server in **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="fb1c0-185">Zie voor meer informatie [faseringsmodus](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="fb1c0-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="fb1c0-186">Gebruik virtuele machines</span><span class="sxs-lookup"><span data-stu-id="fb1c0-186">Use virtual machines</span></span>
<span data-ttu-id="fb1c0-187">Een veelvoorkomende en ondersteunde methode is het uitvoeren van de synchronisatie-engine in een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="fb1c0-188">Als de host een probleem heeft, kan de installatiekopie met de synchronisatie-engine-server kan worden gemigreerd naar een andere server.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="fb1c0-189">Hoge beschikbaarheid van SQL</span><span class="sxs-lookup"><span data-stu-id="fb1c0-189">SQL High Availability</span></span>
<span data-ttu-id="fb1c0-190">Als u niet de SQL Server Express die wordt geleverd met Azure AD Connect, moet vervolgens hoge beschikbaarheid voor SQL Server ook worden overwogen.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="fb1c0-191">De hoge beschikbaarheid-oplossingen die ondersteund zijn SQL-clustering en AOA (AlwaysOn-beschikbaarheidsgroepen).</span><span class="sxs-lookup"><span data-stu-id="fb1c0-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="fb1c0-192">Niet-ondersteunde oplossingen bevatten mirroring.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="fb1c0-193">Ondersteuning voor SQL AOA is toegevoegd aan Azure AD Connect in versie 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="fb1c0-194">Voordat u Azure AD Connect installeert, moet u SQL AOA inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="fb1c0-195">Tijdens de installatie van detecteert Azure AD Connect of de opgegeven SQL-exemplaar is ingeschakeld voor SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="fb1c0-196">Als SQL AOA is ingeschakeld, wordt Azure AD Connect meer cijfers uit als SQL AOA is geconfigureerd voor gebruik van replicatie van synchrone of asynchrone replicatie.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="fb1c0-197">Bij het instellen van de beschikbaarheidsgroep-Listener, is het raadzaam dat u de eigenschap RegisterAllProvidersIP ingesteld op 0.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="fb1c0-198">Dit is omdat Azure AD Connect momenteel SQL Native Client verbinding maakt met SQL en SQL Native Client biedt geen ondersteuning voor het gebruik van de MultiSubNetFailover-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="fb1c0-199">Bijlage CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="fb1c0-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="fb1c0-200">Zie de sectie [controleren](#verify) over het gebruik van dit script.</span><span class="sxs-lookup"><span data-stu-id="fb1c0-200">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="fb1c0-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fb1c0-201">Next steps</span></span>
<span data-ttu-id="fb1c0-202">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="fb1c0-202">**Overview topics**</span></span>  

* [<span data-ttu-id="fb1c0-203">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="fb1c0-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="fb1c0-204">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb1c0-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
