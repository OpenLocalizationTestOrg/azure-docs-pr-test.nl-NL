---
title: aaaService kaart integratie met System Center Operations Manager | Microsoft Docs
description: Serviceoverzicht is een Operations Management Suite-oplossing die automatisch de onderdelen van toepassing op Windows detecteert en Linux-systemen en maps Hallo communicatie tussen services. Dit artikel wordt beschreven met behulp van Serviceoverzicht tooautomatically diagrammen voor gedistribueerde toepassing maken in Operations Manager.
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a><span data-ttu-id="9b25c-104">Serviceoverzicht integratie met System Center Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9b25c-104">Service Map integration with System Center Operations Manager</span></span>
  > [!NOTE]
  > <span data-ttu-id="9b25c-105">Deze functie is openbare preview.</span><span class="sxs-lookup"><span data-stu-id="9b25c-105">This feature is in public preview.</span></span>
  > 
  
<span data-ttu-id="9b25c-106">Operations Management Suite Serviceoverzicht automatisch detecteert de onderdelen van toepassing op Windows- en Linux-systemen en Hallo communicatie tussen services wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="9b25c-106">Operations Management Suite Service Map automatically discovers application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="9b25c-107">Serviceoverzicht kunt u uw servers Hallo manier u ze, beschouwen als onderling verbonden systemen die essentiële services leveren tooview.</span><span class="sxs-lookup"><span data-stu-id="9b25c-107">Service Map allows you tooview your servers hello way you think of them, as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="9b25c-108">Serviceoverzicht toont verbindingen tussen servers, processen en poorten voor elke architectuur TCP-verbinding zonder configuratie naast het Hallo-installatie van een agent vereist.</span><span class="sxs-lookup"><span data-stu-id="9b25c-108">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture, with no configuration required besides hello installation of an agent.</span></span> <span data-ttu-id="9b25c-109">Zie voor meer informatie, Hallo [Serviceoverzicht documentatie](operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="9b25c-109">For more information, see hello [Service Map documentation](operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="9b25c-110">Met deze integratie tussen Serviceoverzicht en System Center Operations Manager, kunt u automatisch diagrammen voor gedistribueerde toepassing maken in Operations Manager die zijn gebaseerd op Hallo dynamische afhankelijkheid maps in Serviceoverzicht.</span><span class="sxs-lookup"><span data-stu-id="9b25c-110">With this integration between Service Map and System Center Operations Manager, you can automatically create distributed application diagrams in Operations Manager that are based on hello dynamic dependency maps in Service Map.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b25c-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9b25c-111">Prerequisites</span></span>
* <span data-ttu-id="9b25c-112">Een Operations Manager-beheergroep die wordt beheerd door een reeks servers.</span><span class="sxs-lookup"><span data-stu-id="9b25c-112">An Operations Manager management group that is managing a set of servers.</span></span>
* <span data-ttu-id="9b25c-113">Een Operations Management Suite-werkruimte Hello Serviceoverzicht oplossing is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9b25c-113">An Operations Management Suite workspace with hello Service Map solution enabled.</span></span>
* <span data-ttu-id="9b25c-114">Een set servers (ten minste één) die worden beheerd door Operations Manager en verzenden gegevens tooService kaart.</span><span class="sxs-lookup"><span data-stu-id="9b25c-114">A set of servers (at least one) that are being managed by Operations Manager and sending data tooService Map.</span></span> <span data-ttu-id="9b25c-115">Windows en Linux-servers worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9b25c-115">Windows and Linux servers are supported.</span></span>
* <span data-ttu-id="9b25c-116">Een service-principal met toegang toohello Azure-abonnement dat is gekoppeld aan Hallo Operations Management Suite-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="9b25c-116">A service principal with access toohello Azure subscription that is associated with hello Operations Management Suite workspace.</span></span> <span data-ttu-id="9b25c-117">Voor meer informatie gaat te[maken van een service-principal](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="9b25c-117">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

## <a name="install-hello-service-map-management-pack"></a><span data-ttu-id="9b25c-118">Hallo Serviceoverzicht management pack installeren</span><span class="sxs-lookup"><span data-stu-id="9b25c-118">Install hello Service Map management pack</span></span>
<span data-ttu-id="9b25c-119">U inschakelen Hallo integratie tussen Operations Manager en Serviceoverzicht door het importeren van Hallo Microsoft.SystemCenter.ServiceMap management pack-bundel (Microsoft.SystemCenter.ServiceMap.mpb).</span><span class="sxs-lookup"><span data-stu-id="9b25c-119">You enable hello integration between Operations Manager and Service Map by importing hello Microsoft.SystemCenter.ServiceMap management pack bundle (Microsoft.SystemCenter.ServiceMap.mpb).</span></span> <span data-ttu-id="9b25c-120">Hallo-bundel bevat Hallo management packs te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b25c-120">hello bundle contains hello following management packs:</span></span>
* <span data-ttu-id="9b25c-121">Microsoft Service kaart Toepassingweergaven</span><span class="sxs-lookup"><span data-stu-id="9b25c-121">Microsoft Service Map Application Views</span></span>
* <span data-ttu-id="9b25c-122">Microsoft System Center Serviceoverzicht interne</span><span class="sxs-lookup"><span data-stu-id="9b25c-122">Microsoft System Center Service Map Internal</span></span>
* <span data-ttu-id="9b25c-123">Microsoft System Center Service kaart onderdrukkingen</span><span class="sxs-lookup"><span data-stu-id="9b25c-123">Microsoft System Center Service Map Overrides</span></span>
* <span data-ttu-id="9b25c-124">Microsoft System Center-Serviceoverzicht</span><span class="sxs-lookup"><span data-stu-id="9b25c-124">Microsoft System Center Service Map</span></span>

## <a name="configure-hello-service-map-integration"></a><span data-ttu-id="9b25c-125">Hallo Serviceoverzicht integratie configureren</span><span class="sxs-lookup"><span data-stu-id="9b25c-125">Configure hello Service Map integration</span></span>
<span data-ttu-id="9b25c-126">Nadat u Hallo Serviceoverzicht management pack, een nieuw knooppunt **Serviceoverzicht**, wordt weergegeven onder **Operations Management Suite** in Hallo **beheer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="9b25c-126">After you install hello Service Map management pack, a new node, **Service Map**, is displayed under **Operations Management Suite** in hello **Administration** pane.</span></span> 

<span data-ttu-id="9b25c-127">tooconfigure Serviceoverzicht integratie, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="9b25c-127">tooconfigure Service Map integration, do hello following:</span></span>

1. <span data-ttu-id="9b25c-128">tooopen hello configuratiewizard in Hallo **kaart Serviceoverzicht** deelvenster, klikt u op **werkruimte toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9b25c-128">tooopen hello configuration wizard, in hello **Service Map Overview** pane, click **Add workspace**.</span></span>  

    ![Deelvenster Overzicht van de service-kaart](media/oms-service-map/scom-configuration.png)

2. <span data-ttu-id="9b25c-130">In Hallo **verbindingsconfiguratie** venster Hallo tenantnaam of -ID, toepassings-ID (ook wel bekend als Hallo gebruikersnaam of clientID) en wachtwoord van de service-principal Hallo invoeren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9b25c-130">In hello **Connection Configuration** window, enter hello tenant name or ID, application ID (also known as hello username or clientID), and password of hello service principal, and then click **Next**.</span></span> <span data-ttu-id="9b25c-131">Voor meer informatie gaat te[maken van een service-principal](#creating-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="9b25c-131">For more information, go too[Create a service principal](#creating-a-service-principal).</span></span>

    ![Hallo verbindingsconfiguratie venster](media/oms-service-map/scom-config-spn.png)

3. <span data-ttu-id="9b25c-133">In Hallo **abonnement selectie** venster hello Azure-abonnement, Azure-resourcegroep (Hallo Hallo Operations Management Suite-werkruimte met) en Operations Management Suite-werkruimte selecteren en klik vervolgens op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9b25c-133">In hello **Subscription Selection** window, select hello Azure subscription, Azure resource group (hello one that contains hello Operations Management Suite workspace), and Operations Management Suite workspace, and then click **Next**.</span></span>

    ![Hallo werkruimte van Operations Manager-configuratie](media/oms-service-map/scom-config-workspace.png)

4. <span data-ttu-id="9b25c-135">In Hallo **groepsselectie Machine** venster u kiezen welke Service kaart Machine groepen gewenste toosync tooOperations Manager.</span><span class="sxs-lookup"><span data-stu-id="9b25c-135">In hello **Machine Group Selection** window, you choose which Service Map Machine Groups you want toosync tooOperations Manager.</span></span> <span data-ttu-id="9b25c-136">Klik op **computergroepen toevoegen/verwijderen**, kies de groepen uit Hallo lijst met **beschikbaar computergroepen**, en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9b25c-136">Click **Add/Remove Machine Groups**, choose groups from hello list of **Available Machine Groups**, and click **Add**.</span></span>  <span data-ttu-id="9b25c-137">Wanneer u klaar bent met groepen te selecteren, klikt u op **Ok** toofinish.</span><span class="sxs-lookup"><span data-stu-id="9b25c-137">When you are finished selecting groups, click **Ok** toofinish.</span></span>
    
    ![Hallo computergroepen voor Operations Manager-configuratie](media/oms-service-map/scom-config-machine-groups.png)
    
5. <span data-ttu-id="9b25c-139">In Hallo **serverselectie** venster u Hallo servicegroep kaart Servers configureren met Hallo-servers die u wilt dat toosync tussen Operations Manager en Service-kaart.</span><span class="sxs-lookup"><span data-stu-id="9b25c-139">In hello **Server Selection** window, you configure hello Service Map Servers Group with hello servers that you want toosync between Operations Manager and Service Map.</span></span> <span data-ttu-id="9b25c-140">Klik op **Servers toevoegen of verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="9b25c-140">Click **Add/Remove Servers**.</span></span>   
    
    <span data-ttu-id="9b25c-141">Voor Hallo integratie toobuild een gedistribueerde toepassing diagram voor een server moet de Hallo-server:</span><span class="sxs-lookup"><span data-stu-id="9b25c-141">For hello integration toobuild a distributed application diagram for a server, hello server must be:</span></span>

    * <span data-ttu-id="9b25c-142">Beheerd door Operations Manager</span><span class="sxs-lookup"><span data-stu-id="9b25c-142">Managed by Operations Manager</span></span>
    * <span data-ttu-id="9b25c-143">Beheerd door Serviceoverzicht</span><span class="sxs-lookup"><span data-stu-id="9b25c-143">Managed by Service Map</span></span>
    * <span data-ttu-id="9b25c-144">Vermeld in het Hallo-kaart Servers servicegroep</span><span class="sxs-lookup"><span data-stu-id="9b25c-144">Listed in hello Service Map Servers Group</span></span>

    ![Hallo Operations Manager Configuration-servicegroep](media/oms-service-map/scom-config-group.png)

6. <span data-ttu-id="9b25c-146">Optioneel: Schakel Hallo beheerserver resource pool toocommunicate met Operations Management Suite en klik vervolgens op **werkruimte toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9b25c-146">Optional: Select hello Management Server resource pool toocommunicate with Operations Management Suite, and then click **Add Workspace**.</span></span>

    ![Hallo resourcegroep van Operations Manager-configuratie](media/oms-service-map/scom-config-pool.png)

    <span data-ttu-id="9b25c-148">Het kan een minuut tooconfigure nemen en registreer Hallo Operations Management Suite-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="9b25c-148">It might take a minute tooconfigure and register hello Operations Management Suite workspace.</span></span> <span data-ttu-id="9b25c-149">Nadat deze is geconfigureerd, initieert Operations Manager Hallo eerste Serviceoverzicht synchronisatie vanaf Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="9b25c-149">After it is configured, Operations Manager initiates hello first Service Map sync from Operations Management Suite.</span></span>

    ![Hallo resourcegroep van Operations Manager-configuratie](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a><span data-ttu-id="9b25c-151">Monitor Serviceoverzicht</span><span class="sxs-lookup"><span data-stu-id="9b25c-151">Monitor Service Map</span></span>
<span data-ttu-id="9b25c-152">Nadat Hallo Operations Management Suite-werkruimte is aangesloten, een nieuwe map Serviceoverzicht wordt weergegeven in Hallo **bewaking** deelvenster van Hallo Operations Manager-console.</span><span class="sxs-lookup"><span data-stu-id="9b25c-152">After hello Operations Management Suite workspace is connected, a new folder, Service Map, is displayed in hello **Monitoring** pane of hello Operations Manager console.</span></span>

![Hallo Operations Manager Monitoring deelvenster](media/oms-service-map/scom-monitoring.png)

<span data-ttu-id="9b25c-154">Hallo Serviceoverzicht map bevat vier knooppunten:</span><span class="sxs-lookup"><span data-stu-id="9b25c-154">hello Service Map folder has four nodes:</span></span>
* <span data-ttu-id="9b25c-155">**Actieve waarschuwingen**: geeft een lijst van alle Hallo actieve waarschuwingen over Hallo communicatie tussen Operations Manager en Service-kaart.</span><span class="sxs-lookup"><span data-stu-id="9b25c-155">**Active Alerts**: Lists all hello active alerts about hello communication between Operations Manager and Service Map.</span></span>  <span data-ttu-id="9b25c-156">Houd er rekening mee dat deze waarschuwingen niet gesynchroniseerde tooOperations Manager wordt Operations Management Suite-waarschuwingen zijn.</span><span class="sxs-lookup"><span data-stu-id="9b25c-156">Note that these alerts are not Operations Management Suite alerts being synced tooOperations Manager.</span></span> 

* <span data-ttu-id="9b25c-157">**Servers**: lijsten Hallo bewaakte servers die zijn geconfigureerd toosync van Serviceoverzicht.</span><span class="sxs-lookup"><span data-stu-id="9b25c-157">**Servers**: Lists hello monitored servers that are configured toosync from Service Map.</span></span>

    ![Hallo Operations Manager Monitoring beheerservers deelvenster](media/oms-service-map/scom-monitoring-servers.png)

* <span data-ttu-id="9b25c-159">**Afhankelijkheid Groepsweergaven machine**: geeft een lijst van alle computergroepen die vanuit Serviceoverzicht worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="9b25c-159">**Machine Group Dependency Views**: Lists all machine groups that are synced from Service Map.</span></span> <span data-ttu-id="9b25c-160">U kunt klikken op een groep tooview diagram van de gedistribueerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b25c-160">You can click any group tooview its distributed application diagram.</span></span>

    ![diagram van de gedistribueerde toepassing Hello Operations Manager](media/oms-service-map/scom-group-dad.png)

* <span data-ttu-id="9b25c-162">**Server-weergaven voor afhankelijkheid**: geeft een lijst van alle servers die vanuit Serviceoverzicht worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="9b25c-162">**Server Dependency Views**: Lists all servers that are synced from Service Map.</span></span> <span data-ttu-id="9b25c-163">U kunt klikken op elke server tooview diagram van de gedistribueerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b25c-163">You can click any server tooview its distributed application diagram.</span></span>

    ![diagram van de gedistribueerde toepassing Hello Operations Manager](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a><span data-ttu-id="9b25c-165">Bewerken of verwijderen van Hallo-werkruimte</span><span class="sxs-lookup"><span data-stu-id="9b25c-165">Edit or delete hello workspace</span></span>
<span data-ttu-id="9b25c-166">U kunt bewerken of verwijderen van de werkruimte Hallo geconfigureerd via Hallo **kaart Serviceoverzicht** deelvenster (**beheer** deelvenster > **Operations Management Suite**  >  **Service kaart**).</span><span class="sxs-lookup"><span data-stu-id="9b25c-166">You can edit or delete hello configured workspace through hello **Service Map Overview** pane (**Administration** pane > **Operations Management Suite** > **Service Map**).</span></span> <span data-ttu-id="9b25c-167">U kunt slechts één Operations Management Suite-werkruimte nu configureren.</span><span class="sxs-lookup"><span data-stu-id="9b25c-167">You can configure only one Operations Management Suite workspace for now.</span></span>

![Hallo Operations Manager bewerken werkruimte](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a><span data-ttu-id="9b25c-169">Regels en overschrijvingen configureren</span><span class="sxs-lookup"><span data-stu-id="9b25c-169">Configure rules and overrides</span></span>
<span data-ttu-id="9b25c-170">Een regel _Microsoft.SystemCenter.ServiceMapImport.Rule_, tooperiodically ophalen informatie wordt gemaakt van Serviceoverzicht.</span><span class="sxs-lookup"><span data-stu-id="9b25c-170">A rule, _Microsoft.SystemCenter.ServiceMapImport.Rule_, is created tooperiodically fetch information from Service Map.</span></span> <span data-ttu-id="9b25c-171">toochange sync tijdsinstellingen, kunt u onderdrukkingen van Hallo regel configureren (**ontwerpen** deelvenster > **regels** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span><span class="sxs-lookup"><span data-stu-id="9b25c-171">toochange sync timings, you can configure overrides of hello rule (**Authoring** pane > **Rules** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).</span></span>

![eigenschappenvenster van Hallo Operations Manager-onderdrukkingen](media/oms-service-map/scom-overrides.png)

* <span data-ttu-id="9b25c-173">**Ingeschakeld**: in- of uitschakelen van automatische updates.</span><span class="sxs-lookup"><span data-stu-id="9b25c-173">**Enabled**: Enable or disable automatic updates.</span></span> 
* <span data-ttu-id="9b25c-174">**IntervalMinutes**: Hallo tijd tussen updates opnieuw ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9b25c-174">**IntervalMinutes**: Reset hello time between updates.</span></span> <span data-ttu-id="9b25c-175">Hallo interval is standaard een uur.</span><span class="sxs-lookup"><span data-stu-id="9b25c-175">hello default interval is one hour.</span></span> <span data-ttu-id="9b25c-176">Als u vaker toosync server maps wilt, kunt u Hallo waarde wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9b25c-176">If you want toosync server maps more frequently, you can change hello value.</span></span>
* <span data-ttu-id="9b25c-177">**TimeoutSeconds**: Hallo tijdsduur voordat een optreedt Hallo aanvraag time-out opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9b25c-177">**TimeoutSeconds**: Reset hello length of time before hello request times out.</span></span> 
* <span data-ttu-id="9b25c-178">**TimeWindowMinutes**: Reset Hallo tijdvenster voor het opvragen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="9b25c-178">**TimeWindowMinutes**: Reset hello time window for querying data.</span></span> <span data-ttu-id="9b25c-179">Standaard is een venster 60 minuten.</span><span class="sxs-lookup"><span data-stu-id="9b25c-179">Default is a 60-minute window.</span></span> <span data-ttu-id="9b25c-180">Hallo toegestane maximumwaarde door Serviceoverzicht is 60 minuten.</span><span class="sxs-lookup"><span data-stu-id="9b25c-180">hello maximum value allowed by Service Map is 60 minutes.</span></span>

## <a name="known-issues-and-limitations"></a><span data-ttu-id="9b25c-181">Bekende problemen en beperkingen</span><span class="sxs-lookup"><span data-stu-id="9b25c-181">Known issues and limitations</span></span>

<span data-ttu-id="9b25c-182">Hallo huidige ontwerp geeft volgende Hallo problemen en beperkingen:</span><span class="sxs-lookup"><span data-stu-id="9b25c-182">hello current design presents hello following issues and limitations:</span></span>
* <span data-ttu-id="9b25c-183">U kunt alleen verbinding tooa één Operations Management Suite-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="9b25c-183">You can only connect tooa single Operations Management Suite workspace.</span></span>
* <span data-ttu-id="9b25c-184">Hoewel u kunt servers toohello servicegroep kaart Servers handmatig via Hallo toevoegen **ontwerpen** deelvenster Hallo kaarten voor deze servers niet onmiddellijk worden gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="9b25c-184">Although you can add servers toohello Service Map Servers Group manually through hello **Authoring** pane, hello maps for those servers are not synced immediately.</span></span>  <span data-ttu-id="9b25c-185">Ze worden gesynchroniseerd vanuit Serviceoverzicht tijdens de volgende synchronisatiecyclus Hallo.</span><span class="sxs-lookup"><span data-stu-id="9b25c-185">They will be synced from Service Map during hello next sync cycle.</span></span>
* <span data-ttu-id="9b25c-186">Als u wijzigingen aanbrengt toohello gedistribueerde toepassing diagrammen die zijn gemaakt door Hallo management pack, worden deze wijzigingen op de volgende synchronisatie Hallo met Serviceoverzicht waarschijnlijk worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="9b25c-186">If you make any changes toohello Distributed Application Diagrams created by hello management pack, those changes will likely be overwritten on hello next sync with Service Map.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="9b25c-187">Een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="9b25c-187">Create a service principal</span></span>
<span data-ttu-id="9b25c-188">Zie voor de officiële Azure-documentatie over het maken van een service principal:</span><span class="sxs-lookup"><span data-stu-id="9b25c-188">For official Azure documentation about creating a service principal, see:</span></span>
* [<span data-ttu-id="9b25c-189">Een service-principal maken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b25c-189">Create a service principal by using PowerShell</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="9b25c-190">Een service-principal maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b25c-190">Create a service principal by using Azure CLI</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [<span data-ttu-id="9b25c-191">Een service-principal maken met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9b25c-191">Create a service principal by using hello Azure portal</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a><span data-ttu-id="9b25c-192">Feedback</span><span class="sxs-lookup"><span data-stu-id="9b25c-192">Feedback</span></span>
<span data-ttu-id="9b25c-193">Hebt u feedback voor ons over Serviceoverzicht of deze documentatie?</span><span class="sxs-lookup"><span data-stu-id="9b25c-193">Do you have any feedback for us about Service Map or this documentation?</span></span> <span data-ttu-id="9b25c-194">Ga naar onze [User Voice pagina](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), kunt u functies aanbevelen of over bestaande suggesties stemmen.</span><span class="sxs-lookup"><span data-stu-id="9b25c-194">Visit our [User Voice page](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), where you can suggest features or vote on existing suggestions.</span></span>
