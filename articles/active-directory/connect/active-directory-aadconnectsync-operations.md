---
title: 'Azure AD Connect-synchronisatie: operationele taken en overwegingen | Microsoft Docs'
description: Dit onderwerp beschrijft operationele taken voor Azure AD Connect-synchronisatie en hoe tooprepare voor de werking van dit onderdeel.
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
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="cf347-103">Azure AD Connect-synchronisatie: operationele taken en afweging</span><span class="sxs-lookup"><span data-stu-id="cf347-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="cf347-104">Hallo-doel van dit onderwerp is toodescribe operationele taken voor Azure AD Connect-synchronisatie.</span><span class="sxs-lookup"><span data-stu-id="cf347-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="cf347-105">Faseringsmodus</span><span class="sxs-lookup"><span data-stu-id="cf347-105">Staging mode</span></span>
<span data-ttu-id="cf347-106">De faseringsmodus kan worden gebruikt voor verschillende scenario's, waaronder:</span><span class="sxs-lookup"><span data-stu-id="cf347-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="cf347-107">Hoge beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="cf347-107">High availability.</span></span>
* <span data-ttu-id="cf347-108">Testen en implementeren van nieuwe wijzigingen in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="cf347-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="cf347-109">Introduceert een nieuwe server en uit bedrijf nemen Hallo oude.</span><span class="sxs-lookup"><span data-stu-id="cf347-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="cf347-110">Met een server in de faseringsmodus kunt u wijzigingen toohello configuratie en preview Hallo wijzigingen voordat u Hallo-server actief maken.</span><span class="sxs-lookup"><span data-stu-id="cf347-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="cf347-111">U kunt er ook toorun volledige import en een volledige synchronisatie tooverify dat alle wijzigingen worden verwacht, voordat u deze wijzigingen naar uw productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="cf347-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="cf347-112">Tijdens de installatie, selecteert u Hallo server toobe in **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="cf347-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="cf347-113">Deze actie wordt Hallo-server actief is voor de import en synchronisatie, maar eventuele uitvoer kan niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cf347-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="cf347-114">Een server in de faseringsmodus is Wachtwoordsynchronisatie of wachtwoord terugschrijven niet actief, zelfs als u deze functies ingeschakeld tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="cf347-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="cf347-115">Wanneer u de faseringsmodus uitschakelt, Hallo-server is, wordt het exporteren wordt gestart, schakelt Wachtwoordsynchronisatie en wachtwoord terugschrijven maakt.</span><span class="sxs-lookup"><span data-stu-id="cf347-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="cf347-116">U kunt nog steeds exporteren van een afdwingen met behulp van Hallo synchronisatie servicemanager.</span><span class="sxs-lookup"><span data-stu-id="cf347-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="cf347-117">Een server in de faseringsmodus blijft tooreceive wijzigingen van Active Directory en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf347-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="cf347-118">Heeft altijd een kopie van de meest recente wijzigingen Hallo en kunnen zeer snel nemen via Hallo verantwoordelijkheden van een andere server.</span><span class="sxs-lookup"><span data-stu-id="cf347-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="cf347-119">Als u wijzigingen tooyour primaire configuratieserver maakt, is uw verantwoordelijkheid toomake Hallo dezelfde wijzigingen toohello server in de faseringsmodus.</span><span class="sxs-lookup"><span data-stu-id="cf347-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="cf347-120">Voor mensen met kennis van de oudere synchronisatie-technologieën verschilt Hallo faseringsmodus omdat Hallo server een eigen SQL-database heeft.</span><span class="sxs-lookup"><span data-stu-id="cf347-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="cf347-121">Deze architectuur kunnen Hallo staging-modus server toobe zich in een ander datacenter.</span><span class="sxs-lookup"><span data-stu-id="cf347-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="cf347-122">Hallo-configuratie van een server controleren</span><span class="sxs-lookup"><span data-stu-id="cf347-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="cf347-123">tooapply deze methode als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="cf347-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="cf347-124">Voorbereiden</span><span class="sxs-lookup"><span data-stu-id="cf347-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="cf347-125">Configuratie</span><span class="sxs-lookup"><span data-stu-id="cf347-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="cf347-126">Importeren en synchroniseren</span><span class="sxs-lookup"><span data-stu-id="cf347-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="cf347-127">Controleer of</span><span class="sxs-lookup"><span data-stu-id="cf347-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="cf347-128">Actieve switchserver</span><span class="sxs-lookup"><span data-stu-id="cf347-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="cf347-129">Voorbereiden</span><span class="sxs-lookup"><span data-stu-id="cf347-129">Prepare</span></span>
1. <span data-ttu-id="cf347-130">Azure AD Connect installeert, selecteert u **faseringsmodus**, en deselecteren **synchronisatie starten** op Hallo laatste pagina van de installatiewizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="cf347-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="cf347-131">Deze modus kunt u toorun Hallo synchronisatie-engine handmatig.</span><span class="sxs-lookup"><span data-stu-id="cf347-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="cf347-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="cf347-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="cf347-133">Meld u af/aanmeldingsnaam en op Hallo start menu selecteren **synchronisatieservice**.</span><span class="sxs-lookup"><span data-stu-id="cf347-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="cf347-134">Configuratie</span><span class="sxs-lookup"><span data-stu-id="cf347-134">Configuration</span></span>
<span data-ttu-id="cf347-135">Als u aangebrachte wijzigingen toohello primaire server en gewenste toocompare Hallo configuratie Hello staging-server, gebruikt u [documentatie voor Azure AD Connect-configuratie](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="cf347-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="cf347-136">Importeren en synchroniseren</span><span class="sxs-lookup"><span data-stu-id="cf347-136">Import and Synchronize</span></span>
1. <span data-ttu-id="cf347-137">Selecteer **Connectors**, en selecteer eerste Connector is met type Hallo Hallo **Active Directory Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="cf347-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="cf347-138">Klik op **uitvoeren**, selecteer **volledige import**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf347-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="cf347-139">Voer deze stappen uit voor alle Connectors van dit type.</span><span class="sxs-lookup"><span data-stu-id="cf347-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="cf347-140">Selecteer Hallo Connector met het type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="cf347-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="cf347-141">Klik op **uitvoeren**, selecteer **volledige import**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf347-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="cf347-142">Zorg ervoor dat Hallo tabblad Connectors nog steeds is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="cf347-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="cf347-143">Voor elke Connector met het type **Active Directory Domain Services**, klikt u op **uitvoeren**, selecteer **Deltasynchronisatie**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf347-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="cf347-144">Selecteer Hallo Connector met het type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="cf347-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="cf347-145">Klik op **uitvoeren**, selecteer **Deltasynchronisatie**, en **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf347-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="cf347-146">U hebt nu gefaseerde export tooAzure AD wijzigingen en on-premises AD (als u hybride implementatie voor Exchange).</span><span class="sxs-lookup"><span data-stu-id="cf347-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="cf347-147">de volgende stappen Hallo kunnen u tooinspect wat over toochange is voordat u daadwerkelijk Hallo toohello exportmappen.</span><span class="sxs-lookup"><span data-stu-id="cf347-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="cf347-148">Verifiëren</span><span class="sxs-lookup"><span data-stu-id="cf347-148">Verify</span></span>
1. <span data-ttu-id="cf347-149">Start een opdrachtprompt en te gaan`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="cf347-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="cf347-150">Voer: `csexport "Name of Connector" %temp%\export.xml /f:x` Hallo-naam van Connector Hallo vindt u in de synchronisatieservice.</span><span class="sxs-lookup"><span data-stu-id="cf347-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="cf347-151">Heeft een naam vergelijkbare too"contoso.com – AAD' voor Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf347-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="cf347-152">Hallo PowerShell-script kopiëren van Hallo sectie [CSAnalyzer](#appendix-csanalyzer) tooa-bestand met de naam `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="cf347-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="cf347-153">Open een PowerShell-venster en blader toohello map waar u de PowerShell-script Hallo hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cf347-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="cf347-154">Voer: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="cf347-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="cf347-155">U hebt nu een bestand met de naam **processedusers1.csv** die kan worden onderzocht in Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="cf347-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="cf347-156">Alle wijzigingen gefaseerde toobe geëxporteerd tooAzure AD vindt u in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="cf347-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="cf347-157">Breng wijzigingen toohello gegevens of configuratie en voer deze stappen opnieuw (importeren en synchroniseren en controleer of) pas Hallo wijzigingen die over toobe geëxporteerd zijn worden verwacht.</span><span class="sxs-lookup"><span data-stu-id="cf347-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="cf347-158">Actieve switchserver</span><span class="sxs-lookup"><span data-stu-id="cf347-158">Switch active server</span></span>
1. <span data-ttu-id="cf347-159">Op de huidige actieve server Hallo Hallo-server (FIM-DirSync/Azure AD Sync) uitschakelen zodat deze niet tooAzure AD exporteert of stel deze in de faseringsmodus (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="cf347-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="cf347-160">Hallo-installatiewizard uitgevoerd op Hallo-server in **faseringsmodus** en uitschakelen **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="cf347-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="cf347-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="cf347-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="cf347-162">Herstel na noodgevallen</span><span class="sxs-lookup"><span data-stu-id="cf347-162">Disaster recovery</span></span>
<span data-ttu-id="cf347-163">Deel van Hallo implementatieontwerp is tooplan voor welke toodo als er een ramp optreedt waarbij u Hallo synchronisatieserver verliezen.</span><span class="sxs-lookup"><span data-stu-id="cf347-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="cf347-164">Er zijn verschillende modellen toouse en welke één toouse is afhankelijk van verschillende factoren, waaronder:</span><span class="sxs-lookup"><span data-stu-id="cf347-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="cf347-165">Wat is de tolerantie voor tooobjects niet wordt kunnen Zorg in Azure AD tijdens Hallo uitvaltijd wijzigt?</span><span class="sxs-lookup"><span data-stu-id="cf347-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="cf347-166">Als u synchronisatie van wachtwoorden, Hallo gebruikers accepteert dat ze toouse Hallo oud wachtwoord in Azure AD hebben als ze deze lokale wijzigen?</span><span class="sxs-lookup"><span data-stu-id="cf347-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="cf347-167">Hebt u een afhankelijkheid op realtime bewerkingen, zoals wachtwoord terugschrijven?</span><span class="sxs-lookup"><span data-stu-id="cf347-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="cf347-168">Afhankelijk van Hallo antwoorden toothese vragen en beleid van uw organisatie, kan een van de volgende strategieën Hallo worden geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="cf347-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="cf347-169">Opnieuw opbouwen wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="cf347-169">Rebuild when needed.</span></span>
* <span data-ttu-id="cf347-170">Een ongebruikte stand-by-server, ook wel **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="cf347-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="cf347-171">Gebruik virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="cf347-171">Use virtual machines.</span></span>

<span data-ttu-id="cf347-172">Als u geen Hallo ingebouwde SQL Express-database gebruikt, wordt ook rekening met het Hallo [SQL maximale beschikbaarheid](#sql-high-availability) sectie.</span><span class="sxs-lookup"><span data-stu-id="cf347-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="cf347-173">Opnieuw opbouwen wanneer deze nodig is</span><span class="sxs-lookup"><span data-stu-id="cf347-173">Rebuild when needed</span></span>
<span data-ttu-id="cf347-174">Een strategie voor een praktische is tooplan voor de server opnieuw opbouwen wanneer deze nodig.</span><span class="sxs-lookup"><span data-stu-id="cf347-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="cf347-175">Normaal gesproken installeren Hallo synchronisatie-engine en importeren in eerste instantie Hallo en synchronisatie kan worden uitgevoerd binnen een paar uur.</span><span class="sxs-lookup"><span data-stu-id="cf347-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="cf347-176">Als er niet een vervangende server beschikbaar is, is het mogelijk tootemporarily gebruik een domain controller toohost Hallo synchronisatie-engine.</span><span class="sxs-lookup"><span data-stu-id="cf347-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="cf347-177">Hallo synchronisatie-engine-server slaat geen geen status over Hallo objecten zodat Hallo-database kan worden gemaakt van Hallo-gegevens in Active Directory en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf347-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="cf347-178">Hallo **sourceAnchor** kenmerk is gebruikte toojoin Hallo objecten van on-premises en Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="cf347-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="cf347-179">Als u opnieuw opbouwen Hallo van server met bestaande objecten on-premises en Hallo cloud, en vervolgens Hallo synchronisatie-engine overeenkomt met deze objecten samen nogmaals op opnieuw installeren.</span><span class="sxs-lookup"><span data-stu-id="cf347-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="cf347-180">Hallo zaken die u nodig hebt toodocument en opslaan zijn Hallo wijzigingen in configuratie toohello-server, zoals filteren en synchronisatieregels.</span><span class="sxs-lookup"><span data-stu-id="cf347-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="cf347-181">Deze aangepaste configuraties moeten opnieuw worden toegepast voordat u begint te synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="cf347-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="cf347-182">Een ongebruikte stand-by-server - faseringsmodus</span><span class="sxs-lookup"><span data-stu-id="cf347-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="cf347-183">Als u een meer complexe omgeving hebt, wordt klikt u vervolgens met een of meer stand-by-servers aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="cf347-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="cf347-184">Tijdens de installatie, kunt u een server toobe in **faseringsmodus**.</span><span class="sxs-lookup"><span data-stu-id="cf347-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="cf347-185">Zie voor meer informatie [faseringsmodus](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="cf347-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="cf347-186">Gebruik virtuele machines</span><span class="sxs-lookup"><span data-stu-id="cf347-186">Use virtual machines</span></span>
<span data-ttu-id="cf347-187">Een veelvoorkomende en ondersteunde methode is toorun Hallo synchronisatie-engine in een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="cf347-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="cf347-188">Als Hallo host een probleem heeft, kan Hallo installatiekopie met de synchronisatieserver engine Hallo gemigreerde tooanother server zijn.</span><span class="sxs-lookup"><span data-stu-id="cf347-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="cf347-189">Hoge beschikbaarheid van SQL</span><span class="sxs-lookup"><span data-stu-id="cf347-189">SQL High Availability</span></span>
<span data-ttu-id="cf347-190">Als u SQL Server Express die wordt geleverd met Azure AD Connect Hallo niet gebruikt, moet vervolgens hoge beschikbaarheid voor SQL Server ook worden overwogen.</span><span class="sxs-lookup"><span data-stu-id="cf347-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="cf347-191">Hallo hoge beschikbaarheidsoplossingen ondersteund omvatten SQL-clustering en AOA (AlwaysOn-beschikbaarheidsgroepen).</span><span class="sxs-lookup"><span data-stu-id="cf347-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="cf347-192">Niet-ondersteunde oplossingen bevatten mirroring.</span><span class="sxs-lookup"><span data-stu-id="cf347-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="cf347-193">Ondersteuning voor SQL AOA is toegevoegd tooAzure AD verbinden in versie 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="cf347-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="cf347-194">Voordat u Azure AD Connect installeert, moet u SQL AOA inschakelen.</span><span class="sxs-lookup"><span data-stu-id="cf347-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="cf347-195">Tijdens de installatie van detecteert Azure AD Connect of Hallo opgegeven SQL-exemplaar is ingeschakeld voor SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="cf347-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="cf347-196">Als SQL AOA is ingeschakeld, wordt Azure AD Connect meer cijfers uit als SQL AOA geconfigureerde toouse synchrone replicatie of asynchrone replicatie is.</span><span class="sxs-lookup"><span data-stu-id="cf347-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="cf347-197">Bij het instellen van Hallo beschikbaarheidsgroep-Listener, verdient het aanbeveling Hallo RegisterAllProvidersIP eigenschap too0 in te stellen.</span><span class="sxs-lookup"><span data-stu-id="cf347-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="cf347-198">Dit is omdat Azure AD Connect momenteel SQL Native Client tooconnect tooSQL gebruikt en SQL Native Client biedt geen ondersteuning voor Hallo gebruik van de MultiSubNetFailover-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cf347-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="cf347-199">Bijlage CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="cf347-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="cf347-200">Zie de sectie Hallo [controleren](#verify) over het toouse dit script.</span><span class="sxs-lookup"><span data-stu-id="cf347-200">See hello section [verify](#verify) on how toouse this script.</span></span>

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

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
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

    #now that we have hello basics, go get hello details

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

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="cf347-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cf347-201">Next steps</span></span>
<span data-ttu-id="cf347-202">**Overzichtsonderwerpen**</span><span class="sxs-lookup"><span data-stu-id="cf347-202">**Overview topics**</span></span>  

* [<span data-ttu-id="cf347-203">Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="cf347-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="cf347-204">Uw on-premises identiteiten integreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf347-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
