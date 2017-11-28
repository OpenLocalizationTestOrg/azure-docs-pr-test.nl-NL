---
title: de gegevensbronnen aaaAccess on-premises voor Azure Logic Apps | Microsoft Docs
description: Hallo lokale gegevensgateway instellen, zodat u toegang hebt tot gegevensbronnen on-premises vanuit logic apps
keywords: toegang tot gegevens, op de lokale, gegevensoverdracht, versleuteling en gegevensbronnen
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="b2620-104">Toegang tot gegevensbronnen on-premises vanuit logic apps met Hallo lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="b2620-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="b2620-105">de gegevensbronnen tooaccess on-premises van logic apps, instellen van een lokale gegevensgateway die logische apps met ondersteunde connectors kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b2620-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="b2620-106">Hallo gateway fungeert als een brug waarmee snelle gegevensoverdracht en -versleuteling tussen gegevensbronnen on-premises en uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="b2620-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="b2620-107">Hallo gateway doorstuurt gegevens van lokale bronnen op gecodeerde kanalen via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="b2620-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="b2620-108">Al het verkeer afkomstig is als beveiligde uitgaand verkeer van Hallo gateway agent.</span><span class="sxs-lookup"><span data-stu-id="b2620-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="b2620-109">Meer informatie over [de werking van de gegevensgateway Hallo](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="b2620-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="b2620-110">Hallo-gateway ondersteunt verbindingen toothese gegevensbronnen on-premises:</span><span class="sxs-lookup"><span data-stu-id="b2620-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="b2620-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="b2620-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="b2620-112">DB2</span><span class="sxs-lookup"><span data-stu-id="b2620-112">DB2</span></span>  
*   <span data-ttu-id="b2620-113">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="b2620-113">File System</span></span>
*   <span data-ttu-id="b2620-114">Informix</span><span class="sxs-lookup"><span data-stu-id="b2620-114">Informix</span></span>
*   <span data-ttu-id="b2620-115">MQ</span><span class="sxs-lookup"><span data-stu-id="b2620-115">MQ</span></span>
*   <span data-ttu-id="b2620-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="b2620-116">MySQL</span></span>
*   <span data-ttu-id="b2620-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="b2620-117">Oracle Database</span></span>
*   <span data-ttu-id="b2620-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b2620-118">PostgreSQL</span></span>
*   <span data-ttu-id="b2620-119">SAP-toepassingsserver</span><span class="sxs-lookup"><span data-stu-id="b2620-119">SAP Application Server</span></span> 
*   <span data-ttu-id="b2620-120">SAP-berichtenserver</span><span class="sxs-lookup"><span data-stu-id="b2620-120">SAP Message Server</span></span>
*   <span data-ttu-id="b2620-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="b2620-121">SharePoint</span></span>
*   <span data-ttu-id="b2620-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="b2620-122">SQL Server</span></span>
*   <span data-ttu-id="b2620-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="b2620-123">Teradata</span></span>

<span data-ttu-id="b2620-124">Deze stappen laten zien hoe tooset up Hallo lokale gegevens gateway toowork met uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="b2620-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="b2620-125">Zie voor meer informatie over ondersteunde connectors [Connectors voor Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b2620-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="b2620-126">Zie voor informatie over hoe toouse Hallo gateway met andere services, deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="b2620-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="b2620-127">Microsoft Power BI lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="b2620-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="b2620-128">Azure Analysis Services op locatie gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="b2620-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="b2620-129">Microsoft-Flow lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="b2620-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="b2620-130">Microsoft PowerApps lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="b2620-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="b2620-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b2620-131">Requirements</span></span>

* <span data-ttu-id="b2620-132">U moet al hebben [Hallo data gateway geïnstalleerd op een lokale computer](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="b2620-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="b2620-133">Wanneer u zich aanmeldt toohello Azure-portal, hebt u toouse Hallo dezelfde werk- of schoolaccount dat is gebruikt te[Hallo lokale gegevensgateway installeren](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="b2620-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="b2620-134">Uw account moet ook een Azure-abonnement toouse hebben wanneer u een gateway-resource in hello Azure-portal voor uw gateway-installatie maakt.</span><span class="sxs-lookup"><span data-stu-id="b2620-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="b2620-135">De gateway-installatie kan niet al door een Azure-gateway-resource wordt geclaimd.</span><span class="sxs-lookup"><span data-stu-id="b2620-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="b2620-136">U kunt uw gateway installatie tooonly één Azure-gateway resource koppelen.</span><span class="sxs-lookup"><span data-stu-id="b2620-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="b2620-137">Claim gebeurt wanneer u Hallo gateway resource maken zodat Hallo-installatie niet beschikbaar voor andere bronnen is.</span><span class="sxs-lookup"><span data-stu-id="b2620-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="b2620-138">Hallo data gateway-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="b2620-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="b2620-139">1. Hallo lokale gegevensgateway installeren</span><span class="sxs-lookup"><span data-stu-id="b2620-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="b2620-140">Als u nog niet gedaan hebt, volgt u Hallo [stappen tooinstall Hallo lokale gegevensgateway](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="b2620-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="b2620-141">Voordat u met de Hallo doorgaat andere stappen, zorgt u ervoor dat u Hallo data gateway geïnstalleerd op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="b2620-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="b2620-142">2. Een Azure-resource voor Hallo lokale gegevensgateway maken</span><span class="sxs-lookup"><span data-stu-id="b2620-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="b2620-143">Nadat u Hallo gateway geïnstalleerd op een lokale computer, moet u uw data gateway maken als een resource in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2620-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="b2620-144">Uw gateway-resource koppelt in deze stap ook aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b2620-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="b2620-145">Meld u aan toohello [Azure-portal](https://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="b2620-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="b2620-146">Zorg ervoor dat toouse Hallo dezelfde Azure werk of school e-mailadres tooinstall Hallo gateway gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b2620-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="b2620-147">Op Hallo linkermenu in Azure, kiest u **nieuw** > **Enterprise Integration** > **On-premises gegevensgateway** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="b2620-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   !['On-premises data gateway' vinden](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="b2620-149">Op Hallo **verbinding-gateway maken** blade bieden deze toocreate details van uw data gateway resource:</span><span class="sxs-lookup"><span data-stu-id="b2620-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="b2620-150">**Naam**: Voer een naam voor uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="b2620-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="b2620-151">**Abonnement**: Selecteer Hallo tooassociate Azure-abonnement met uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="b2620-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="b2620-152">Dit abonnement moet hetzelfde abonnement als uw logische app Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2620-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="b2620-153">Hallo standaardabonnement is gebaseerd op Hallo Azure-account waarmee u toosign in.</span><span class="sxs-lookup"><span data-stu-id="b2620-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="b2620-154">**Resourcegroep**: een resourcegroep maken of een bestaande resourcegroep selecteren voor het implementeren van uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="b2620-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="b2620-155">Resourcegroepen kunnen u gerelateerde Azure activa beheren als een verzameling.</span><span class="sxs-lookup"><span data-stu-id="b2620-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="b2620-156">**Locatie**: Azure beperkt deze locatie toohello dezelfde regio die is geselecteerd voor het gateway-cloudservice Hallo tijdens [gateway-installatie](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="b2620-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="b2620-157">Zorg ervoor dat Hallo gateway Resourcelocatie overeenkomt met Hallo gateway cloud servicelocatie.</span><span class="sxs-lookup"><span data-stu-id="b2620-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="b2620-158">De gateway-installatie mogelijk anders niet weergegeven in de lijst met de Hallo geïnstalleerd gateways voor u tooselect in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="b2620-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="b2620-159">U kunt verschillende regio's gebruiken voor uw gateway-resource en voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="b2620-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="b2620-160">**De naam van de installatie**: als uw gateway-installatie niet is geselecteerd, selecteert u Hallo-gateway die u eerder hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b2620-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="b2620-161">tooadd hello gateway resource tooyour Azure-dashboard, kies **pincode toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="b2620-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="b2620-162">Als u bent klaar, kiest u **maken**.</span><span class="sxs-lookup"><span data-stu-id="b2620-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="b2620-163">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b2620-163">For example:</span></span>

    ![Geef details toocreate uw on-premises gegevensgateway](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="b2620-165">toofind of weergave uw data gateway op elk gewenst moment in hello Azure links hoofdmenu te gaan **meer Services** > **Enterprise Integration** > **On-premises gegevens Gateways**.</span><span class="sxs-lookup"><span data-stu-id="b2620-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Ga te 'Meer services', 'Enterprise Integration', 'On-premises gegevensgateways'](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="b2620-167">3. Verbinding maken met uw logische app toohello lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="b2620-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="b2620-168">Nu dat u hebt uw data gateway resource gemaakt en die uw Azure-abonnement is gekoppeld aan deze resource, maak een verbinding tussen uw logische app en Hallo data gateway.</span><span class="sxs-lookup"><span data-stu-id="b2620-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="b2620-169">De locatie van uw gateway verbinding moet aanwezig zijn in Hallo dezelfde regio bevinden als uw logische app, maar u kunt een data gateway die voorkomt in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="b2620-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="b2620-170">Maak in hello Azure-portal, of open uw logische app in Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="b2620-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="b2620-171">Toevoegen van een connector die ondersteuning biedt voor lokale verbindingen, zoals SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b2620-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="b2620-172">Hallo-volgorde wordt weergegeven, selecteert u **verbinden via lokale gegevensgateway**, Geef een unieke verbindingsnaam Hallo vereiste informatie en selecteer Hallo data gateway resource die u toouse wilt.</span><span class="sxs-lookup"><span data-stu-id="b2620-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="b2620-173">Als u bent klaar, kiest u **maken**.</span><span class="sxs-lookup"><span data-stu-id="b2620-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="b2620-174">Een unieke verbindingsnaam kunt u gemakkelijk herkennen die verbinding later, vooral wanneer u meerdere verbindingen maken.</span><span class="sxs-lookup"><span data-stu-id="b2620-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="b2620-175">Indien van toepassing, moet u ook Hallo gekwalificeerde domeinnaam voor uw gebruikersnaam bevatten.</span><span class="sxs-lookup"><span data-stu-id="b2620-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Verbinding maken tussen logic app en data gateway](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="b2620-177">Gefeliciteerd, uw gatewayverbinding is nu gereed voor uw logische app toouse.</span><span class="sxs-lookup"><span data-stu-id="b2620-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="b2620-178">De instellingen voor de gateway-verbinding bewerken</span><span class="sxs-lookup"><span data-stu-id="b2620-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="b2620-179">Nadat u een gatewayverbinding voor uw logische app maakt, kunt u toolater update Hallo-instellingen voor die specifieke verbinding.</span><span class="sxs-lookup"><span data-stu-id="b2620-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="b2620-180">toofind hello gatewayverbinding:</span><span class="sxs-lookup"><span data-stu-id="b2620-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="b2620-181">Op Hallo logic app blade onder **ontwikkelingsprogramma's**, selecteer **API verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="b2620-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="b2620-182">Hallo **API verbindingen** deelvenster ziet u alle API-verbindingen die zijn gekoppeld aan uw logische app, inclusief gatewayverbindingen.</span><span class="sxs-lookup"><span data-stu-id="b2620-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Ga tooyour logische app, selecteert u 'API verbindingen'](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="b2620-184">Of Ga te hello Azure links hoofdmenu en **meer Services** > **Web- en Mobile Services** > **API verbindingen** voor alle API-verbindingen inclusief gatewayverbindingen die gekoppeld aan uw Azure-abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="b2620-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="b2620-185">Of Ga te op Hallo belangrijkste Azure linkermenu**alle resources** voor alle API-verbindingen, inclusief gatewayverbindingen die gekoppeld aan uw Azure-abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="b2620-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="b2620-186">Selecteer Hallo gatewayverbinding wilt tooview of bewerken en kies **API bewerken verbinding**.</span><span class="sxs-lookup"><span data-stu-id="b2620-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="b2620-187">Als u de updates worden niet doorgevoerd, probeert u [stoppen en opnieuw starten van de gatewayservice Windows hello](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="b2620-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="b2620-188">Schakelt u of uw lokale gegevens gateway bron verwijderen</span><span class="sxs-lookup"><span data-stu-id="b2620-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="b2620-189">toocreate een andere gateway-resource, uw gateway koppelen aan een andere resource of Hallo gateway resource verwijdert, kunt u Hallo gateway resource verwijderen zonder gevolgen voor Hallo gateway-installatie.</span><span class="sxs-lookup"><span data-stu-id="b2620-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="b2620-190">Hello Azure links hoofdmenu en ga te**alle resources**.</span><span class="sxs-lookup"><span data-stu-id="b2620-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="b2620-191">Zoek en selecteer uw data gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="b2620-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="b2620-192">Kies **On-premises Data Gateway**, en kies op Hallo resource werkbalk **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="b2620-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="b2620-193">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="b2620-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="b2620-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2620-194">Next steps</span></span>

* [<span data-ttu-id="b2620-195">Uw logische apps beveiligen</span><span class="sxs-lookup"><span data-stu-id="b2620-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="b2620-196">Algemene voorbeelden en scenario's voor logic apps</span><span class="sxs-lookup"><span data-stu-id="b2620-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
