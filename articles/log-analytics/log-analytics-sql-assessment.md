---
title: aaaOptimize uw SQL Server-omgeving met Azure Log Analytics | Microsoft Docs
description: U kunt met Azure Log Analytics Hallo SQL Assessment oplossing tooassess Hallo risico en status van uw SQL server-omgevingen met regelmatige tussenpozen.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="448bb-103">Optimalisatie van uw SQL Server-omgeving met Hallo beoordeling van de SQL-oplossing in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="448bb-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![Symbool van de SQL-evaluatie](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="448bb-105">U kunt Hallo SQL Assessment oplossing tooassess Hallo risico en status van uw server-omgevingen met regelmatige tussenpozen.</span><span class="sxs-lookup"><span data-stu-id="448bb-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="448bb-106">Dit artikel helpt u bij het installeren van Hallo oplossing zodat u corrigerende maatregelen op mogelijke problemen kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="448bb-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="448bb-107">Deze oplossing biedt een geprioriteerde lijst met aanbevelingen voor specifieke tooyour geïmplementeerde serverinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="448bb-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="448bb-108">Hallo aanbevelingen worden onderverdeeld in zes focus gebieden waarmee u snel inzicht Hallo risico en herstelacties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="448bb-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="448bb-109">Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring door Microsoft engineers van duizenden klant bezoeken.</span><span class="sxs-lookup"><span data-stu-id="448bb-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="448bb-110">Elke aanbeveling bevat richtlijnen over waarom een probleem tooyou mogelijk belang en hoe tooimplement Hallo voorgestelde wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="448bb-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="448bb-111">U kunt focusgebieden die belangrijkste tooyour organisatie en bijhouden van uw progressie ten opzichte van een omgeving met risico gratis en goed wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="448bb-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="448bb-112">Nadat u Hallo oplossing hebt toegevoegd en een beoordeling voltooid, samenvattende is informatie voor focusgebieden wordt weergegeven op Hallo **SQL Assessment** dashboard voor Hallo-infrastructuur in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="448bb-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="448bb-113">Hallo volgende secties wordt beschreven hoe toouse informatie over Hallo Hallo **SQL Assessment** dashboard, waar u kunt weergeven en vervolgens te aanbevolen acties voor de infrastructuur van de SQL-server.</span><span class="sxs-lookup"><span data-stu-id="448bb-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![afbeelding van de beoordeling van de SQL-tegel](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![afbeelding van de beoordeling van de SQL-dashboard](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="448bb-116">Installeren en configureren van Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="448bb-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="448bb-117">SQL-evaluatie werkt met alle ondersteunde versies van SQL Server voor Hallo Standard-, Developer- en Enterprise-edities.</span><span class="sxs-lookup"><span data-stu-id="448bb-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="448bb-118">Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.</span><span class="sxs-lookup"><span data-stu-id="448bb-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="448bb-119">Agents moeten worden geïnstalleerd op servers die SQL Server geïnstalleerd hebt.</span><span class="sxs-lookup"><span data-stu-id="448bb-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="448bb-120">Hallo SQL oplossing vereist een ondersteunde versie van .NET Framework 4 is geïnstalleerd op elke computer die een OMS-agent heeft.</span><span class="sxs-lookup"><span data-stu-id="448bb-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="448bb-121">In volgorde tooinstall Hallo oplossing Hallo gebruiker moet een beheerder of bijdrager toohello Azure-abonnement als Azure-portal met behulp van Hallo.</span><span class="sxs-lookup"><span data-stu-id="448bb-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="448bb-122">Hallo-gebruiker moet bovendien een lid van Hallo OMS werkruimte Inzender of administrator-rol in Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="448bb-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="448bb-123">Als u Operations Manager-agent Hallo met SQL Assessment, moet u een account van Operations Manager Run-As toouse.</span><span class="sxs-lookup"><span data-stu-id="448bb-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="448bb-124">Zie [Operations Manager run as-accounts voor OMS](#operations-manager-run-as-accounts-for-oms) hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="448bb-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="448bb-125">Hallo MMA agent biedt geen ondersteuning voor Operations Manager Run-As accounts.</span><span class="sxs-lookup"><span data-stu-id="448bb-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="448bb-126">Hallo SQL Assessment oplossing tooyour OMS-werkruimte met behulp van Hallo proces dat wordt beschreven in toevoegen [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="448bb-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="448bb-127">Er is geen verdere configuratie nodig.</span><span class="sxs-lookup"><span data-stu-id="448bb-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="448bb-128">Nadat u Hallo oplossing hebt toegevoegd, Hallo AdvisorAssessment.exe bestand tooservers waarop agents zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="448bb-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="448bb-129">Configuratiegegevens lezen en vervolgens verzonden toohello OMS-service in de cloud Hallo voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="448bb-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="448bb-130">Logica is toegepaste toohello ontvangen gegevens en Hallo cloudservice registreert Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="448bb-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="448bb-131">De verzameling Gegevensdetails SQL-evaluatie</span><span class="sxs-lookup"><span data-stu-id="448bb-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="448bb-132">SQL-evaluatie verzamelt gegevens van WMI, registergegevens, prestatiegegevens en resultaten SQL Server dynamische Beheerweergave weergeven met behulp van Hallo-agents die u hebt ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="448bb-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="448bb-133">Hallo volgende tabel ziet u de methoden van de collectie voor agents, of Operations Manager (SCOM) is vereist, en hoe vaak gegevens worden verzameld door een agent.</span><span class="sxs-lookup"><span data-stu-id="448bb-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="448bb-134">Platform</span><span class="sxs-lookup"><span data-stu-id="448bb-134">platform</span></span> | <span data-ttu-id="448bb-135">Directe Agent</span><span class="sxs-lookup"><span data-stu-id="448bb-135">Direct Agent</span></span> | <span data-ttu-id="448bb-136">SCOM-agents</span><span class="sxs-lookup"><span data-stu-id="448bb-136">SCOM agent</span></span> | <span data-ttu-id="448bb-137">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="448bb-137">Azure Storage</span></span> | <span data-ttu-id="448bb-138">SCOM vereist?</span><span class="sxs-lookup"><span data-stu-id="448bb-138">SCOM required?</span></span> | <span data-ttu-id="448bb-139">SCOM-agent gegevens die worden verzonden via de beheergroep</span><span class="sxs-lookup"><span data-stu-id="448bb-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="448bb-140">Frequentie van de verzameling</span><span class="sxs-lookup"><span data-stu-id="448bb-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="448bb-141">Windows</span><span class="sxs-lookup"><span data-stu-id="448bb-141">Windows</span></span> | <span data-ttu-id="448bb-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="448bb-142">&#8226;</span></span> | <span data-ttu-id="448bb-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="448bb-143">&#8226;</span></span> |  |  | <span data-ttu-id="448bb-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="448bb-144">&#8226;</span></span> |<span data-ttu-id="448bb-145">7 dagen</span><span class="sxs-lookup"><span data-stu-id="448bb-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="448bb-146">Operations Manager run as-accounts voor OMS</span><span class="sxs-lookup"><span data-stu-id="448bb-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="448bb-147">Log Analytics in OMS gebruikt Hallo Operations Manager-agent en management groep toocollect en verzenden van gegevens toohello OMS-service.</span><span class="sxs-lookup"><span data-stu-id="448bb-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="448bb-148">OMS builds van management packs voor werkbelastingen tooprovide toevoegen waarde-services.</span><span class="sxs-lookup"><span data-stu-id="448bb-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="448bb-149">Elke werkbelasting vereist werklastspecifiek bevoegdheden toorun management packs in een andere beveiligingscontext, zoals een domeinaccount.</span><span class="sxs-lookup"><span data-stu-id="448bb-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="448bb-150">Referentiegegevens tooprovide moet u een Operations Manager Run As-account voor configureren.</span><span class="sxs-lookup"><span data-stu-id="448bb-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="448bb-151">Gebruik Hallo na informatie tooset Hallo Operations Manager run as-account voor SQL-evaluatie.</span><span class="sxs-lookup"><span data-stu-id="448bb-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="448bb-152">Hallo Run As-account voor SQL beoordeling instellen</span><span class="sxs-lookup"><span data-stu-id="448bb-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="448bb-153">Als u al Hallo management pack voor SQL Server gebruikt, moet u de Run As-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="448bb-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="448bb-154">tooconfigure hello SQL Run As-account in Hallo Operations-console</span><span class="sxs-lookup"><span data-stu-id="448bb-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="448bb-155">Als u hello OMS directe agent in plaats van de SCOM-agents hello, Hallo management pack altijd in de beveiligingscontext Hallo Hallo lokale systeemaccount wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="448bb-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="448bb-156">Overslaan stappen 1-5 hieronder en Voer Hallo ofwel T-SQL- of Powershell-voorbeeld NT AUTHORITY\SYSTEM als Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="448bb-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="448bb-157">Open Hallo Operations-console in Operations Manager en klik vervolgens op **beheer**.</span><span class="sxs-lookup"><span data-stu-id="448bb-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="448bb-158">Onder **Run As-configuratie**, klikt u op **profielen**, en open **OMS SQL Assessment Run As-profiel**.</span><span class="sxs-lookup"><span data-stu-id="448bb-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="448bb-159">Op Hallo **Run As-Accounts** pagina, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="448bb-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="448bb-160">Selecteer een Windows Run As-account met Hallo-referenties die nodig zijn voor SQL Server, of klik op **nieuw** toocreate een.</span><span class="sxs-lookup"><span data-stu-id="448bb-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="448bb-161">Hallo Run As-accounttype moet Windows.</span><span class="sxs-lookup"><span data-stu-id="448bb-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="448bb-162">Hallo Run As-account moet ook deel uitmaken van de lokale groep Administrators op alle Windows-Servers die als host fungeert voor SQL Server-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="448bb-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="448bb-163">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="448bb-163">Click **Save**.</span></span>
6. <span data-ttu-id="448bb-164">Wijzigen en vervolgens Hallo T-SQL-voorbeeld te volgen op elke SQL Server-exemplaar toogrant minimale machtigingen vereist tooRun tooperform As-Account voor SQL-evaluatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="448bb-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="448bb-165">Echter, u hoeft niet toodo dit als een Run As-Account al deel uit van Hallo serverrol sysadmin voor SQL Server-exemplaren maakt.</span><span class="sxs-lookup"><span data-stu-id="448bb-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="448bb-166">tooconfigure hello SQL Run As-account met behulp van Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="448bb-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="448bb-167">Open een PowerShell-venster en Voer Hallo script volgen nadat u deze met uw gegevens hebt bijgewerkt:</span><span class="sxs-lookup"><span data-stu-id="448bb-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="448bb-168">Begrijpen hoe de aanbevelingen zijn geplaatst</span><span class="sxs-lookup"><span data-stu-id="448bb-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="448bb-169">Elke aanbeveling krijgt een weging-waarde die Hallo relatieve belang van Hallo aanbeveling aangeeft.</span><span class="sxs-lookup"><span data-stu-id="448bb-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="448bb-170">Alleen Hallo tien belangrijkste aanbevelingen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="448bb-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="448bb-171">Hoe gewichten worden berekend</span><span class="sxs-lookup"><span data-stu-id="448bb-171">How weights are calculated</span></span>
<span data-ttu-id="448bb-172">Wegingen zijn statistische waarden op basis van de drie belangrijkste factoren:</span><span class="sxs-lookup"><span data-stu-id="448bb-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="448bb-173">Hallo *kans* dat er een probleem vastgesteld problemen tot leidt.</span><span class="sxs-lookup"><span data-stu-id="448bb-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="448bb-174">Een grotere kans gelijkstaat tooa groter algemene score voor Hallo aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="448bb-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="448bb-175">Hallo *impact* van Hallo probleem van uw organisatie als dit leidt een probleem tot.</span><span class="sxs-lookup"><span data-stu-id="448bb-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="448bb-176">Een hogere impact gelijkstaat tooa groter algemene score voor Hallo aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="448bb-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="448bb-177">Hallo *inspanning* tooimplement Hallo aanbeveling vereist.</span><span class="sxs-lookup"><span data-stu-id="448bb-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="448bb-178">Een hogere inspanning gelijkstaat tooa kleinere totale score voor Hallo aanbeveling.</span><span class="sxs-lookup"><span data-stu-id="448bb-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="448bb-179">Hallo weging voor elke aanbeveling wordt uitgedrukt als percentage van totale score Hallo beschikbaar voor elke focusgebied.</span><span class="sxs-lookup"><span data-stu-id="448bb-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="448bb-180">Bijvoorbeeld, als een aanbeveling in Hallo beveiliging en naleving focusgebied heeft een score van 5%, wordt implementatie van deze aanbeveling verhoogd, uw algemene beveiliging en naleving score door 5%.</span><span class="sxs-lookup"><span data-stu-id="448bb-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="448bb-181">Focusgebieden</span><span class="sxs-lookup"><span data-stu-id="448bb-181">Focus areas</span></span>
<span data-ttu-id="448bb-182">**Beveiliging en naleving** -focus ziet u hier aanbevelingen voor potentiële beveiligingsrisico's en schendingen, bedrijfsbeleid en aan technische, juridische en wettelijke vereisten.</span><span class="sxs-lookup"><span data-stu-id="448bb-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="448bb-183">**Beschikbaarheid en zakelijke continuïteit** -focus ziet u hier aanbevelingen voor de beschikbaarheid van de service, de tolerantie van uw infrastructuur en de bescherming van zakelijke.</span><span class="sxs-lookup"><span data-stu-id="448bb-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="448bb-184">**Prestaties en schaalbaarheid** -focus ziet u hier aanbevelingen toohelp van uw organisatie IT-infrastructuur toenemen, zorg ervoor dat uw IT-omgeving voldoet aan de huidige prestatievereisten en kunnen toorespond toochanging infrastructuur nodig.</span><span class="sxs-lookup"><span data-stu-id="448bb-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="448bb-185">**Een upgrade uitvoert, migratie en implementatie van** - focus ziet u hier aanbevelingen toohelp u een upgrade uitvoert, migreren en implementeren van SQL Server tooyour bestaande infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="448bb-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="448bb-186">**Bewerkingen en bewaking** - focus ziet u hier aanbevelingen toohelp stroomlijnen uw IT-team implementeren preventief onderhoud en prestaties.</span><span class="sxs-lookup"><span data-stu-id="448bb-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="448bb-187">**Wijzigings- en Configuratiebeheer** -focus ziet u hier aanbevelingen toohelp beveiligen dagelijkse taken, zorg ervoor dat wijzigingen geen negatieve invloed zijn op uw infrastructuur, controleprocedures wijzigen, en tootrack instellen en controleren basissysteemconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="448bb-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="448bb-188">Moet u zijn gericht tooscore 100% in elk focusgebied?</span><span class="sxs-lookup"><span data-stu-id="448bb-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="448bb-189">Dat hoeft niet.</span><span class="sxs-lookup"><span data-stu-id="448bb-189">Not necessarily.</span></span> <span data-ttu-id="448bb-190">Hallo aanbevelingen zijn gebaseerd op Hallo kennis en ervaring opgedaan door Microsoft engineers in duizenden klant bezoeken.</span><span class="sxs-lookup"><span data-stu-id="448bb-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="448bb-191">Er is geen infrastructuren van twee servers zijn echter dezelfde Hallo en specifieke aanbevelingen mogelijk meer of minder relevante tooyou.</span><span class="sxs-lookup"><span data-stu-id="448bb-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="448bb-192">Enkele aanbevelingen voor beveiliging worden minder relevant als uw virtuele machines niet blootgestelde toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="448bb-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="448bb-193">Enkele aanbevelingen beschikbaarheid mogelijk minder relevant zijn voor services die de ad-hoc gegevensverzameling met lage prioriteit en rapportage bieden.</span><span class="sxs-lookup"><span data-stu-id="448bb-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="448bb-194">Problemen die belangrijke tooa volwassen bedrijven mogelijk minder belangrijke tooa opstarten.</span><span class="sxs-lookup"><span data-stu-id="448bb-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="448bb-195">U mogelijk wilt tooidentify welke focusgebieden uw prioriteiten zijn en bekijk hoe uw scores gedurende een bepaalde periode wijzigen.</span><span class="sxs-lookup"><span data-stu-id="448bb-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="448bb-196">Elke aanbeveling bevat richtlijnen over waarom het belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="448bb-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="448bb-197">U moet deze richtlijnen tooevaluate of implementeren van Hallo aanbeveling geschikt is voor u is, gezien Hallo aard van uw IT-services en Hallo zakelijke behoeften van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="448bb-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="448bb-198">Gebruik assessment focus gebied aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="448bb-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="448bb-199">Voordat u een oplossing voor evaluatie in OMS gebruiken kunt, moet u Hallo oplossing geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="448bb-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="448bb-200">tooread meer informatie over het installeren van oplossingen, Zie [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="448bb-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="448bb-201">Nadat deze is geïnstalleerd, kunt u Hallo overzicht van aanbevelingen bekijken met behulp van Hallo SQL Assessment tegel op de overzichtspagina Hallo in OMS.</span><span class="sxs-lookup"><span data-stu-id="448bb-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="448bb-202">Weergave Hallo samengevat beoordelingen van compatibiliteit voor uw infrastructuur en inzoomen in aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="448bb-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="448bb-203">tooview aanbevelingen voor een focus gebied en corrigerende actie ondernemen</span><span class="sxs-lookup"><span data-stu-id="448bb-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="448bb-204">Op Hallo **overzicht** pagina, klikt u op Hallo **SQL Assessment** tegel.</span><span class="sxs-lookup"><span data-stu-id="448bb-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="448bb-205">Op Hallo **SQL Assessment** pagina, Hallo samenvattingsinformatie in een Hallo focus gebied blades controleren en klik op een tooview aanbevelingen voor het desbetreffende focusgebied.</span><span class="sxs-lookup"><span data-stu-id="448bb-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="448bb-206">U kunt op elk van de Hallo focus gebiedspagina's kunt Hallo prioriteit aanbevelingen voor uw omgeving weergeven.</span><span class="sxs-lookup"><span data-stu-id="448bb-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="448bb-207">Klik op een aanbeveling onder **objecten van invloed op een** tooview om details over waarom het Hallo-aanbeveling wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="448bb-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="448bb-208">![afbeelding van SQL-evaluatie aanbevelingen](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="448bb-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="448bb-209">U kunt ondernemen corrigerende maatregelen voorgesteld in **voorgestelde acties**.</span><span class="sxs-lookup"><span data-stu-id="448bb-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="448bb-210">Wanneer het Hallo-item is opgelost, record hoger beoordelingen die aanbevolen acties zijn uitgevoerd en de naleving-score wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="448bb-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="448bb-211">Gecorrigeerde items worden weergegeven als **doorgegeven objecten**.</span><span class="sxs-lookup"><span data-stu-id="448bb-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="448bb-212">Aanbevelingen negeren</span><span class="sxs-lookup"><span data-stu-id="448bb-212">Ignore recommendations</span></span>
<span data-ttu-id="448bb-213">Als u de aanbevelingen die u tooignore wilt hebt, kunt u een tekstbestand dat OMS tooprevent aanbevelingen worden weergegeven in de resultaten van de beoordeling wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="448bb-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="448bb-214">tooidentify aanbevelingen die u worden genegeerd</span><span class="sxs-lookup"><span data-stu-id="448bb-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="448bb-215">Meld u in de werkruimte tooyour en logboek zoekopdracht openen.</span><span class="sxs-lookup"><span data-stu-id="448bb-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="448bb-216">Gebruik hello query toolist aanbevelingen die zijn mislukt voor computers in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="448bb-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="448bb-217">Hier volgt een schermopname die laat zien Hallo logboek zoekquery: ![aanbevelingen is mislukt](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="448bb-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="448bb-218">Kies de aanbevelingen die u tooignore wilt.</span><span class="sxs-lookup"><span data-stu-id="448bb-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="448bb-219">U in de volgende procedure Hallo Hallo waarden gebruikt voor RecommendationId.</span><span class="sxs-lookup"><span data-stu-id="448bb-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="448bb-220">toocreate en het gebruik van een tekstbestand IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="448bb-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="448bb-221">Maak een bestand met de naam IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="448bb-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="448bb-222">Plakken of typ elke RecommendationId voor elke aanbeveling dat u OMS tooignore op een afzonderlijke regel wilt en vervolgens opslaan en Hallo-bestand sluiten.</span><span class="sxs-lookup"><span data-stu-id="448bb-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="448bb-223">Hallo-bestand in de volgende map op elke computer waar u OMS tooignore aanbevelingen Hallo plaatsen.</span><span class="sxs-lookup"><span data-stu-id="448bb-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="448bb-224">Op computers met Microsoft Monitoring Agent (rechtstreeks of via de Operations Manager verbonden) - Hallo *SystemDrive*: \Program Files\Microsoft Agent\Agent bewaking</span><span class="sxs-lookup"><span data-stu-id="448bb-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="448bb-225">Op Hallo Operations Manager-beheerserver - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="448bb-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="448bb-226">tooverify dat aanbevelingen worden genegeerd</span><span class="sxs-lookup"><span data-stu-id="448bb-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="448bb-227">Nadat het Hallo volgende geplande evaluatie wordt uitgevoerd, wordt standaard elke 7 dagen opgegeven Hallo aanbevelingen zijn gemarkeerd genegeerd en worden niet weergegeven op Hallo assessment dashboard.</span><span class="sxs-lookup"><span data-stu-id="448bb-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="448bb-228">Kunt u Hallo logboek zoeken query's toolist na alle Hallo genegeerd aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="448bb-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="448bb-229">Als u later besluit dat u wilt dat de aanbevelingen toosee genegeerd, IgnoreRecommendations.txt bestanden verwijderen of u kunt RecommendationIDs verwijderen uit deze.</span><span class="sxs-lookup"><span data-stu-id="448bb-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="448bb-230">SQL-evaluatie oplossing Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="448bb-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="448bb-231">*Hoe vaak wordt een evaluatie uitgevoerd?*</span><span class="sxs-lookup"><span data-stu-id="448bb-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="448bb-232">Hallo beoordeling wordt uitgevoerd om de zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="448bb-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="448bb-233">*Is er een manier tooconfigure hoe vaak Hallo beoordeling wordt uitgevoerd?*</span><span class="sxs-lookup"><span data-stu-id="448bb-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="448bb-234">Momenteel niet.</span><span class="sxs-lookup"><span data-stu-id="448bb-234">Not at this time.</span></span>

<span data-ttu-id="448bb-235">*Als een andere server wordt gedetecteerd nadat ik Hallo SQL assessment oplossing hebt toegevoegd, wordt deze gecontroleerd?*</span><span class="sxs-lookup"><span data-stu-id="448bb-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="448bb-236">Ja, zodra deze is gedetecteerd. deze wordt beoordeeld van vervolgens, elke 7 dagen.</span><span class="sxs-lookup"><span data-stu-id="448bb-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="448bb-237">*Als een server buiten werking wordt gesteld, wanneer deze verwijderd uit Hallo assessment?*</span><span class="sxs-lookup"><span data-stu-id="448bb-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="448bb-238">Als een server komt niet met het verzenden van gegevens voor drie weken, wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="448bb-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="448bb-239">*Wat is de naam Hallo van Hallo-proces dat het verzamelen van gegevens Hallo?*</span><span class="sxs-lookup"><span data-stu-id="448bb-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="448bb-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="448bb-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="448bb-241">*Hoe lang duurt het voor gegevens toobe verzameld?*</span><span class="sxs-lookup"><span data-stu-id="448bb-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="448bb-242">Hallo werkelijke gegevensverzameling op Hallo server duurt ongeveer 1 uur.</span><span class="sxs-lookup"><span data-stu-id="448bb-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="448bb-243">Kan het langer duren op servers met een groot aantal SQL-exemplaren of -databases.</span><span class="sxs-lookup"><span data-stu-id="448bb-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="448bb-244">*Welk type gegevens worden verzameld?*</span><span class="sxs-lookup"><span data-stu-id="448bb-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="448bb-245">Hallo volgende typen gegevens zijn verzameld:</span><span class="sxs-lookup"><span data-stu-id="448bb-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="448bb-246">WMI</span><span class="sxs-lookup"><span data-stu-id="448bb-246">WMI</span></span>
  * <span data-ttu-id="448bb-247">Register</span><span class="sxs-lookup"><span data-stu-id="448bb-247">Registry</span></span>
  * <span data-ttu-id="448bb-248">Prestatiemeteritems</span><span class="sxs-lookup"><span data-stu-id="448bb-248">Performance counters</span></span>
  * <span data-ttu-id="448bb-249">SQL dynamische beheerweergaven (DMV).</span><span class="sxs-lookup"><span data-stu-id="448bb-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="448bb-250">*Is er een manier tooconfigure wanneer gegevens worden verzameld?*</span><span class="sxs-lookup"><span data-stu-id="448bb-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="448bb-251">Momenteel niet.</span><span class="sxs-lookup"><span data-stu-id="448bb-251">Not at this time.</span></span>

<span data-ttu-id="448bb-252">*Waarom heb ik tooconfigure uitvoeren als-Account?*</span><span class="sxs-lookup"><span data-stu-id="448bb-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="448bb-253">Voor SQL Server, worden een klein aantal SQL-query's uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="448bb-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="448bb-254">Zodat ze toorun, een Run As-Account met VIEW SERVER STATE machtigingen tooSQL moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="448bb-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="448bb-255">Bovendien zijn in de volgorde tooquery WMI, lokale beheerdersreferenties zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="448bb-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="448bb-256">*Waarom alleen Hallo top 10 aanbevelingen worden weergegeven?*</span><span class="sxs-lookup"><span data-stu-id="448bb-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="448bb-257">In plaats van zodat u overweldigend uitputtende lijst met taken, is het raadzaam dat u zich richten op Hallo prioriteit aanbevelingen eerst adressering.</span><span class="sxs-lookup"><span data-stu-id="448bb-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="448bb-258">Nadat u deze oplossen, wordt extra aanbevelingen beschikbaar worden.</span><span class="sxs-lookup"><span data-stu-id="448bb-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="448bb-259">Als u liever toosee Hallo gedetailleerde lijst, kunt u alle aanbevelingen Hallo OMS logboek zoekactie kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="448bb-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="448bb-260">*Is er een manier tooignore een aanbeveling?*</span><span class="sxs-lookup"><span data-stu-id="448bb-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="448bb-261">Ja, Zie [aanbevelingen negeren](#ignore-recommendations) sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="448bb-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="448bb-262">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="448bb-262">Next steps</span></span>
* <span data-ttu-id="448bb-263">[Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde gegevens voor de Nalevingsbeoordeling van de SQL- en aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="448bb-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
