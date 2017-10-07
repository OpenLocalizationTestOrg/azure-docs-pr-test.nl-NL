---
title: aaaCreate Azure BizTalk Services in hello Azure-portal | Microsoft Docs
description: Meer informatie over hoe tooprovision of Azure BizTalk Services maken in hello Azure-portal; MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="e2706-103">BizTalk Services maken met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e2706-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="e2706-104">toosign in toohello Azure-portal, moet u een Azure-account en de Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e2706-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="e2706-105">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="e2706-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="e2706-106">Zie [Gratis proefversie van Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="e2706-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="e2706-107"><a name="CreateService"></a>Een BizTalk Service maken</span><span class="sxs-lookup"><span data-stu-id="e2706-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="e2706-108">Afhankelijk van het Hallo-versie die u kiest, kunnen niet alle BizTalk Service-instellingen beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="e2706-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="e2706-109">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="e2706-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="e2706-110">Selecteer in het onderste navigatievenster Hallo **nieuw**:</span><span class="sxs-lookup"><span data-stu-id="e2706-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="e2706-111">![Selecteer de nieuwe knop Hallo][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="e2706-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="e2706-112">Selecteer **APP SERVICES** > **BIZTALK SERVICE** > **AANGEPAST MAKEN**:</span><span class="sxs-lookup"><span data-stu-id="e2706-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="e2706-113">![Selecteer BizTalk Service en selecteer Aangepast maken][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="e2706-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="e2706-114">Voer Hallo BizTalk Service-instellingen:</span><span class="sxs-lookup"><span data-stu-id="e2706-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="e2706-115"><strong>De naam van de BizTalk Service</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="e2706-116">U kunt elke willekeurige naam invoeren, maar houd deze specifiek.</span><span class="sxs-lookup"><span data-stu-id="e2706-116">You can enter any name but be specific.</span></span> <span data-ttu-id="e2706-117">Voorbeelden zijn:</span><span class="sxs-lookup"><span data-stu-id="e2706-117">Some examples include:</span></span><br/><br/><span data-ttu-id="e2706-118">
    <em>mijnbedrijf</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2706-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="e2706-119">
    <em>mijnbedrijfmijntoepassing</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2706-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="e2706-120">
    <em>mijntoepassing</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="e2706-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="e2706-121">'. biztalk.windows.net ' wordt automatisch toegevoegd toohello naam die u invoert.</span><span class="sxs-lookup"><span data-stu-id="e2706-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="e2706-122">Hiermee maakt u een URL die is gebruikt tooaccess uw BizTalk Service, zoals <strong>https://<em>mijntoepassing</em>. biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="e2706-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-123"><strong>Editie</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="e2706-124">Als u zich in Hallo test-/ ontwikkelingsfase bevindt, kiest u <strong>Developer</strong>.</span><span class="sxs-lookup"><span data-stu-id="e2706-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="e2706-125">Als u zich in de productiefase hello, gebruikt u Hallo <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: grafiek van edities</a> toodetermine als <strong>Premium</strong>, <strong>standaard</strong>, of <strong>Basic</strong>hello juiste keuze is voor uw bedrijfsscenario.</span><span class="sxs-lookup"><span data-stu-id="e2706-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-126"><strong>Regio</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="e2706-127">Selecteer Hallo geografische regio toohost uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-128"><strong>Domein-URL</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="e2706-129"><strong>Optioneel</strong>.</span><span class="sxs-lookup"><span data-stu-id="e2706-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="e2706-130">Hallo domein-URL is standaard <em>Naamvanuwbiztalkservice</em>. biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="e2706-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="e2706-131">U kunt ook een aangepast domein invoeren.</span><span class="sxs-lookup"><span data-stu-id="e2706-131">A custom domain can also be entered.</span></span> <span data-ttu-id="e2706-132">Als uw domein bijvoorbeeld <em>contoso</em> is, kunt u het volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="e2706-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="e2706-133">
    <em>MijnBedrijf</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e2706-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="e2706-134">
    <em>MijnBedrijfMijnToepassing</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e2706-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="e2706-135">
    <em>MijnToepassing</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e2706-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="e2706-136">
    <em>NaamVanUwBizTalkService</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="e2706-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="e2706-137">Selecteer Hallo pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="e2706-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="e2706-138">5.</span><span class="sxs-lookup"><span data-stu-id="e2706-138">5.</span></span> <span data-ttu-id="e2706-139">Voer Hallo opslag en Database-instellingen:</span><span class="sxs-lookup"><span data-stu-id="e2706-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="e2706-140"><strong>Opslagaccount voor bewaken/archiveren</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="e2706-141">Selecteer een bestaand opslagaccount of maak een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e2706-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="e2706-142">Als u een nieuw opslagaccount maakt, voert u Hallo <strong>Opslagaccountnaam</strong>.</span><span class="sxs-lookup"><span data-stu-id="e2706-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-143"><strong>Traceringsdatabase</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="e2706-144">Als u een bestaande Azure SQL Database gebruikt, kan deze niet worden gebruikt door een andere BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="e2706-145">U moet het Hallo-aanmeldingsnaam en wachtwoord ingevoerd wanneer die Azure SQL Database-Server is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2706-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="e2706-146"><strong>TIP</strong> maken Hallo-traceringsdatabase en het opslagaccount voor bewaken/archiveren in dezelfde regio Hallo zoals Hallo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="e2706-147">Selecteer Hallo pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="e2706-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="e2706-148">6.</span><span class="sxs-lookup"><span data-stu-id="e2706-148">6.</span></span> <span data-ttu-id="e2706-149">Voer Hallo Database-instellingen:</span><span class="sxs-lookup"><span data-stu-id="e2706-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="e2706-150"><strong>Naam</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="e2706-151">Beschikbaar als <strong>Maak een nieuw exemplaar van SQL-Database</strong> is geselecteerd in het vorige scherm Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2706-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="e2706-152">Voer een SQL-Database de naam van toobe die wordt gebruikt door uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-153"><strong>Server</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="e2706-154">Beschikbaar als <strong>Maak een nieuw exemplaar van SQL-Database</strong> is geselecteerd in het vorige scherm Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2706-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="e2706-155">Selecteer een bestaande SQL Database-server of maak een nieuwe SQL Database-server.</span><span class="sxs-lookup"><span data-stu-id="e2706-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-156"><strong>Aanmeldingsnaam voor server</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="e2706-157">Voer Hallo aanmeldingsnaam in.</span><span class="sxs-lookup"><span data-stu-id="e2706-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-158"><strong>Aanmeldingswachtwoord voor server</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="e2706-159">Voer het aanmeldingswachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2706-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="e2706-160"><strong>Regio</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="e2706-161">Beschikbaar als <strong>Een nieuw SQL Database-exemplaar</strong> is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="e2706-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="e2706-162">Selecteer Hallo geografische regio toohost uw SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="e2706-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="e2706-163">Hallo vinkje toocomplete Hallo wizard selecteren.</span><span class="sxs-lookup"><span data-stu-id="e2706-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="e2706-164">Hallo voortgangspictogram wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e2706-164">hello progress icon appears:</span></span>  
![Het voortgangspictogram wordt weergegeven als u klaar bent][ProgressComplete]

<span data-ttu-id="e2706-166">Als u klaar is hello Azure BizTalk Service gemaakt en is klaar voor uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e2706-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="e2706-167">Hallo standaardinstellingen zijn voldoende.</span><span class="sxs-lookup"><span data-stu-id="e2706-167">hello default settings are sufficient.</span></span> <span data-ttu-id="e2706-168">Als u toochange Hallo standaardinstellingen wilt, selecteer **BIZTALK SERVICES** in Hallo navigatiedeelvenster links en selecteer vervolgens uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="e2706-169">Er worden extra instellingen weergegeven in Hallo [tabbladen Dashboard, bewaken en schalen](biztalk-dashboard-monitor-scale-tabs.md) Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="e2706-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="e2706-170">Afhankelijk van de status van de Hallo Hallo BizTalk Service zijn er bepaalde bewerkingen die kunnen niet worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="e2706-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="e2706-171">Voor een lijst van deze bewerkingen te gaan[Statusgrafiek van BizTalk Services](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="e2706-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="e2706-172">Stappen na de inrichting</span><span class="sxs-lookup"><span data-stu-id="e2706-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="e2706-173">Hallo-certificaat installeren op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="e2706-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="e2706-174">Een certificaat dat gereed is voor productie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e2706-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="e2706-175">Hallo Access Control-naamruimte ophalen</span><span class="sxs-lookup"><span data-stu-id="e2706-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="e2706-176"><a name="InstallCert"></a>Hallo-certificaat installeren op een lokale computer</span><span class="sxs-lookup"><span data-stu-id="e2706-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="e2706-177">Bij het inrichten van de BizTalk Service wordt er een zelfondertekend certificaat gemaakt en gekoppeld aan uw BizTalk Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e2706-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="e2706-178">U moet dit certificaat downloaden en installeren op computers waarop u BizTalk Service-toepassingen implementeren of verzenden van berichten tooa BizTalk Service-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="e2706-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="e2706-179">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="e2706-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="e2706-180">Selecteer **BIZTALK SERVICES** in het linkernavigatievenster Hallo en selecteer vervolgens uw BizTalk Service-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e2706-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="e2706-181">Selecteer Hallo **Dashboard** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e2706-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="e2706-182">Selecteer **SSL-certificaat downloaden**:</span><span class="sxs-lookup"><span data-stu-id="e2706-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="e2706-183">![SSL-certificaat wijzigen][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="e2706-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="e2706-184">Dubbelklik op Hallo-certificaat en doorloop Hallo wizard tooinstall Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="e2706-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="e2706-185">Zorg ervoor dat u Hallo certificaat installeert in Hallo **vertrouwde basiscertificeringsinstanties** opslaan.</span><span class="sxs-lookup"><span data-stu-id="e2706-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="e2706-186"><a name="AddCert"></a>Een certificaat dat gereed is voor productie toevoegen</span><span class="sxs-lookup"><span data-stu-id="e2706-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="e2706-187">Hallo zelfondertekend certificaat dat automatisch wordt gemaakt wanneer BizTalk Services maken is bedoeld voor gebruik in ontwikkelomgevingen alleen.</span><span class="sxs-lookup"><span data-stu-id="e2706-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="e2706-188">Vervang het in productiescenario's door een certificaat dat gereed is voor productie.</span><span class="sxs-lookup"><span data-stu-id="e2706-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="e2706-189">Op Hallo **Dashboard** tabblad **SSL-certificaat bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="e2706-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="e2706-190">Blader tooyour persoonlijke SSL-certificaat (*CertificateName*.pfx) die de naam van uw BizTalk Service bevat en klik vervolgens op het vinkje Hallo Hallo wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="e2706-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="e2706-191"><a name="ACS"></a>Hallo Access Control-naamruimte ophalen</span><span class="sxs-lookup"><span data-stu-id="e2706-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="e2706-192">Meld u aan toohello [Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="e2706-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="e2706-193">Selecteer **BIZTALK SERVICES** in Hallo navigatiedeelvenster links en selecteer vervolgens uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="e2706-194">Selecteer in de taakbalk Hallo **verbindingsgegevens**:</span><span class="sxs-lookup"><span data-stu-id="e2706-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="e2706-195">![Verbindingsgegevens selecteren][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="e2706-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="e2706-196">Kopieer Hallo Access Control-waarden.</span><span class="sxs-lookup"><span data-stu-id="e2706-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="e2706-197">Wanneer u een BizTalk Service-project implementeert vanuit Visual Studio, voert u deze Access Control-naamruimte in.</span><span class="sxs-lookup"><span data-stu-id="e2706-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="e2706-198">Hallo Access Control-naamruimte wordt automatisch gemaakt voor uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="e2706-199">Hallo Access Control-waarden kunnen worden gebruikt met elke toepassing.</span><span class="sxs-lookup"><span data-stu-id="e2706-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="e2706-200">Wanneer u Azure BizTalk Services maakt, bepaalt deze Access Control-naamruimte Hallo verificatie met uw BizTalk Service-implementatie.</span><span class="sxs-lookup"><span data-stu-id="e2706-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="e2706-201">Als u toochange Hallo abonnement of Hallo naamruimte wilt beheren, selecteert u **ACTIVE DIRECTORY** in Hallo navigatiedeelvenster links en selecteer vervolgens de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="e2706-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="e2706-202">Hallo taakbalk ziet u de opties.</span><span class="sxs-lookup"><span data-stu-id="e2706-202">hello task bar lists your options.</span></span>

<span data-ttu-id="e2706-203">Te klikken op **beheren** wordt geopend Hallo Access Control-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="e2706-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="e2706-204">Hallo BizTalk Service gebruikt in Hallo Access Control-beheerportal, **Service-identiteiten**:</span><span class="sxs-lookup"><span data-stu-id="e2706-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="e2706-205">![ACS-Service-identiteiten in Hallo Access Control-beheerportal][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="e2706-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="e2706-206">Hallo Access Control service-identiteit is een set referenties waarmee toepassingen of clients tooauthenticate rechtstreeks via Access Control en geen token ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e2706-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2706-207">Hallo BizTalk Service gebruikt **eigenaar** voor Hallo standaardservice-identiteit en Hallo **wachtwoord** waarde.</span><span class="sxs-lookup"><span data-stu-id="e2706-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="e2706-208">Als u de waarde symmetrische sleutel hello in plaats van Hallo waarde wachtwoord gebruiken, optreden hello volgende fout.</span><span class="sxs-lookup"><span data-stu-id="e2706-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="e2706-209">*Kan geen verbinding maken toohello Access Control-beheerserviceaccount met Hallo opgegeven referenties*</span><span class="sxs-lookup"><span data-stu-id="e2706-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="e2706-210">[Uw ACS-naamruimte beheren](https://msdn.microsoft.com/library/azure/hh674478.aspx) geeft een lijst weer met de volgende richtlijnen en aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="e2706-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="e2706-211">Uitleg van de vereisten</span><span class="sxs-lookup"><span data-stu-id="e2706-211">Requirements explained</span></span>
<span data-ttu-id="e2706-212">Deze vereisten zijn niet van toepassing toohello editie Free.</span><span class="sxs-lookup"><span data-stu-id="e2706-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="e2706-213"><strong>Wat u nodig hebt</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="e2706-214"><strong>Waarom u dit nodig hebt</strong></span><span class="sxs-lookup"><span data-stu-id="e2706-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="e2706-215">Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e2706-215">Azure subscription</span></span></td>
<td><span data-ttu-id="e2706-216">Hallo abonnement bepaalt wie toohello Azure-portal kunt aanmelden.</span><span class="sxs-lookup"><span data-stu-id="e2706-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="e2706-217">Hallo accounthouder maakt Hallo-abonnement op <a HREF="https://account.windowsazure.com/Subscriptions"> Azure-abonnementen</a>.</span><span class="sxs-lookup"><span data-stu-id="e2706-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="e2706-218">Hello Azure-account kan meerdere abonnementen hebben en kan worden beheerd door iedereen die is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="e2706-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="e2706-219">De houder van uw Azure-account maakt bijvoorbeeld een abonnement met de naam <em>Biztalkserviceabonnement</em> en biedt Hallo BizTalk-beheerders binnen uw bedrijf (bijvoorbeeld ContosoBTSAdmins@live.com) toegang tot toothis abonnement.</span><span class="sxs-lookup"><span data-stu-id="e2706-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="e2706-220">In dit scenario Hallo BizTalk-beheerders toohello Azure-portal aanmelden en hebben volledige beheerder rechten tooall Hallo gehoste services in Hallo abonnement, met inbegrip van Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="e2706-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="e2706-221">Hallo BizTalk-beheerders zijn niet hello Azure-account houders en daarom geen toegang tot tooany factureringsgegevens.</span><span class="sxs-lookup"><span data-stu-id="e2706-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="e2706-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Abonnementen en Opslagaccounts beheren in Azure-portal Hallo</a> vindt u meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2706-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="e2706-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e2706-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="e2706-224">Hallo-tabellen, weergaven en opgeslagen procedures die worden gebruikt door de BizTalk Service, inclusief de traceringsgegevens Hallo Hallo opslaat.</span><span class="sxs-lookup"><span data-stu-id="e2706-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="e2706-225">Wanneer u een BizTalk Service maakt, kunt u een bestaande Azure SQL Server of Azure SQL Database gebruiken. U kunt ook automatisch een nieuwe server of database maken.</span><span class="sxs-lookup"><span data-stu-id="e2706-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="e2706-226">Hallo schaal van de SQL-Database wordt automatisch geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e2706-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="e2706-227">Normaal gesproken is Hallo standaardschaal voldoende voor een BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="e2706-228">Veranderende Hallo schaal heeft impact op de prijzen.</span><span class="sxs-lookup"><span data-stu-id="e2706-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="e2706-229">Zie <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts en facturering in Azure SQL Database</a>
</span><span class="sxs-lookup"><span data-stu-id="e2706-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="e2706-230">
<strong>Opmerkingen</strong>
</span><span class="sxs-lookup"><span data-stu-id="e2706-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="e2706-231">Wanneer u een nieuwe Azure SQL Server en Database maakt, wordt Azure Services automatisch ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e2706-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="e2706-232">Hallo BizTalk Service vereist dat Azure Services zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e2706-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="e2706-233">Als u een nieuwe Azure SQL Database op een bestaande Azure SQL-Server maakt, Hallo firewallregels Hallo Server niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="e2706-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="e2706-234">Het is daarom mogelijk dat andere Azure-Services zijn niet toegestaan voor toegang tot toohello Server-databases.</span><span class="sxs-lookup"><span data-stu-id="e2706-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="e2706-235">Azure Access Control-naamruimte</span><span class="sxs-lookup"><span data-stu-id="e2706-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="e2706-236">Voert de verificatie met Azure BizTalk Services uit.</span><span class="sxs-lookup"><span data-stu-id="e2706-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="e2706-237">Wanneer u een BizTalk Service-project implementeert vanuit Visual Studio, voert u deze Access Control-naamruimte in.</span><span class="sxs-lookup"><span data-stu-id="e2706-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="e2706-238">Wanneer u een BizTalk Service maakt, wordt automatisch Hallo Access Control-naamruimte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2706-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="e2706-239">Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="e2706-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="e2706-240">Geeft toegang tot tootables, blobs en wachtrijen die door uw BizTalk Service toosave Hallo volgende gebruikt:</span><span class="sxs-lookup"><span data-stu-id="e2706-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="e2706-241">Logboekbestanden voor die monitor Hallo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="e2706-242">Hallo uitvoer bewaking wordt ook weergegeven in Hallo **bewaking** tabblad in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e2706-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="e2706-243">Bij het maken van een X12 of AS2-overeenkomst tussen partners, kunt u toostore berichteigenschappen voor Hallo archiveren functie inschakelen.</span><span class="sxs-lookup"><span data-stu-id="e2706-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="e2706-244">Deze gegevens worden opgeslagen in Hallo Storage-account.</span><span class="sxs-lookup"><span data-stu-id="e2706-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="e2706-245">Wanneer u een BizTalk Service maakt, kunt u een bestaand opslagaccount gebruiken of automatisch een nieuw opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="e2706-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="e2706-246">Hallo standaardinstellingen voor opslag zijn voldoende voor een BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="e2706-247">Wanneer u een opslagaccount maakt, worden automatisch een primaire en secundaire sleutel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2706-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="e2706-248">Deze sleutels beheren de toegang tooyour Storage-account.</span><span class="sxs-lookup"><span data-stu-id="e2706-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="e2706-249">Hallo BizTalk Service gebruikt automatisch Hallo primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="e2706-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="e2706-250">Zie <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Opslag</a> voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2706-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="e2706-251">Persoonlijk SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="e2706-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="e2706-252">Wanneer er een Azure BizTalk Service wordt gemaakt, wordt er ook een HTTPS-URL met de naam van uw BizTalk Service gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2706-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="e2706-253">Deze URL is automatisch geconfigureerde toouse een zelfondertekend certificaat voor de ontwikkeling van alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="e2706-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="e2706-254">Voor de productie hebt u een persoonlijk SSL-certificaat nodig.</span><span class="sxs-lookup"><span data-stu-id="e2706-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="e2706-255">
<strong>Belangrijke informatie over SSL-certificaten</strong>

</span><span class="sxs-lookup"><span data-stu-id="e2706-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="e2706-256">vervaldatum van certificaat Hallo moet kleiner zijn dan 5 jaar.</span><span class="sxs-lookup"><span data-stu-id="e2706-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="e2706-257">Voor alle persoonlijke certificaten is een wachtwoord vereist.</span><span class="sxs-lookup"><span data-stu-id="e2706-257">All private certificates require a password.</span></span> <span data-ttu-id="e2706-258">Onthoud dit wachtwoord. U doet er verstandig aan het wachtwoord te delen met uw beheerders.</span><span class="sxs-lookup"><span data-stu-id="e2706-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="e2706-259">Zelfondertekende certificaten worden gebruikt in een test-/ontwikkelingsomgeving.</span><span class="sxs-lookup"><span data-stu-id="e2706-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="e2706-260">Bij gebruik van zelfondertekende certificaten importeren Hallo certificaat tooyour persoonlijke certificaatarchief en Hallo certificaatarchief van vertrouwde basiscertificeringsinstanties.</span><span class="sxs-lookup"><span data-stu-id="e2706-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="e2706-261">Bij het verzenden van de certificeringsinstantie van Hallo productie certificaat aanvraag tooyour geven Hallo certificaateigenschappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e2706-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="e2706-262"><strong>Verbeterd sleutelgebruik</strong>: voor Azure BizTalk Services is minimaal serververificatie vereist.</span><span class="sxs-lookup"><span data-stu-id="e2706-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="e2706-263"><strong>Algemene naam</strong>: Hallo volledig gekwalificeerde domeinnaam (FQDN) van uw Azure BizTalk Service-URL invoeren.</span><span class="sxs-lookup"><span data-stu-id="e2706-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="e2706-264">Zie <a HREF="#CreateService">Een BizTalk Service maken</a> in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="e2706-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="e2706-265">Een nieuw of ander certificaat kan worden toegevoegd nadat Hallo BizTalk Service is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2706-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="e2706-266">Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="e2706-266">Hybrid Connections</span></span>
<span data-ttu-id="e2706-267">Wanneer u een Azure BizTalk Service maakt, Hallo **hybride verbindingen** tabblad is beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="e2706-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![Tabblad Hybride verbindingen][HybridConnectionTab]

<span data-ttu-id="e2706-269">Hybride verbindingen zijn gebruikte tooconnect een Azure-website of mobiele service van Azure tooany lokale resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's, Mobile Services en de meeste aangepaste webservices.</span><span class="sxs-lookup"><span data-stu-id="e2706-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="e2706-270">Hybride verbindingen en Hallo BizTalk Adapter Service zijn verschillend.</span><span class="sxs-lookup"><span data-stu-id="e2706-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="e2706-271">Hallo BizTalk Adapter Service is gebruikte tooconnect Azure BizTalk Services tooan on-premises regel van Business (LOB)-systeem.</span><span class="sxs-lookup"><span data-stu-id="e2706-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="e2706-272">Zie [hybride verbindingen](integration-hybrid-connection-overview.md) toolearn meer, inclusief het maken en beheren van hybride verbindingen.</span><span class="sxs-lookup"><span data-stu-id="e2706-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2706-273">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2706-273">Next steps</span></span>
<span data-ttu-id="e2706-274">Nu een BizTalk Service is gemaakt, tijd om uzelf bekend met verschillende Hallo [BizTalk Services: de tabbladen Dashboard, bewaken en schalen](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="e2706-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="e2706-275">U kunt nu toepassingen maken met uw BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="e2706-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="e2706-276">toostart te maken van toepassingen, ga[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="e2706-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="e2706-277">Zie ook</span><span class="sxs-lookup"><span data-stu-id="e2706-277">See also</span></span>
* [<span data-ttu-id="e2706-278">BizTalk Services: grafiek van edities</span><span class="sxs-lookup"><span data-stu-id="e2706-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="e2706-279">BizTalk Services: statusgrafiek</span><span class="sxs-lookup"><span data-stu-id="e2706-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="e2706-280">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="e2706-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="e2706-281">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="e2706-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="e2706-282">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="e2706-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="e2706-283">Hoe gaan gebruiken Azure BizTalk Services SDK Hallo</span><span class="sxs-lookup"><span data-stu-id="e2706-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="e2706-284">Hybride verbindingen</span><span class="sxs-lookup"><span data-stu-id="e2706-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
