---
title: Toegang tot on-premises gegevensbronnen voor Azure Logic Apps | Microsoft Docs
description: De lokale data gateway instellen, zodat u toegang hebt tot gegevensbronnen on-premises vanuit logic apps
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
ms.openlocfilehash: 24793b83ca284fe9510fe21bc2d13b0589209d36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-the-on-premises-data-gateway"></a><span data-ttu-id="8cc5b-104">Toegang tot gegevensbronnen on-premises vanuit logic apps met de lokale data gateway</span><span class="sxs-lookup"><span data-stu-id="8cc5b-104">Access data sources on premises from logic apps with the on-premises data gateway</span></span>

<span data-ttu-id="8cc5b-105">Instellen voor toegang tot gegevensbronnen on-premises van uw logische apps moet een lokale gegevensgateway die logische apps met ondersteunde connectors kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-105">To access data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="8cc5b-106">De gateway fungeert als een brug waarmee snelle gegevensoverdracht en -versleuteling tussen gegevensbronnen on-premises en uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-106">The gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="8cc5b-107">De gateway stuurt gegevens van lokale bronnen op gecodeerde kanalen via de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="8cc5b-108">Al het verkeer afkomstig is als beveiligde uitgaand verkeer van de gateway-agent.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="8cc5b-109">Meer informatie over [de werking van de gegevensgateway](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="8cc5b-109">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="8cc5b-110">De gateway ondersteunt verbindingen met deze gegevensbronnen on-premises:</span><span class="sxs-lookup"><span data-stu-id="8cc5b-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="8cc5b-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="8cc5b-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="8cc5b-112">DB2</span><span class="sxs-lookup"><span data-stu-id="8cc5b-112">DB2</span></span>  
*   <span data-ttu-id="8cc5b-113">Bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="8cc5b-113">File System</span></span>
*   <span data-ttu-id="8cc5b-114">Informix</span><span class="sxs-lookup"><span data-stu-id="8cc5b-114">Informix</span></span>
*   <span data-ttu-id="8cc5b-115">MQ</span><span class="sxs-lookup"><span data-stu-id="8cc5b-115">MQ</span></span>
*   <span data-ttu-id="8cc5b-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="8cc5b-116">MySQL</span></span>
*   <span data-ttu-id="8cc5b-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="8cc5b-117">Oracle Database</span></span>
*   <span data-ttu-id="8cc5b-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="8cc5b-118">PostgreSQL</span></span>
*   <span data-ttu-id="8cc5b-119">SAP-toepassingsserver</span><span class="sxs-lookup"><span data-stu-id="8cc5b-119">SAP Application Server</span></span> 
*   <span data-ttu-id="8cc5b-120">SAP-berichtenserver</span><span class="sxs-lookup"><span data-stu-id="8cc5b-120">SAP Message Server</span></span>
*   <span data-ttu-id="8cc5b-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="8cc5b-121">SharePoint</span></span>
*   <span data-ttu-id="8cc5b-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8cc5b-122">SQL Server</span></span>
*   <span data-ttu-id="8cc5b-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="8cc5b-123">Teradata</span></span>

<span data-ttu-id="8cc5b-124">Deze stappen laten zien hoe de gegevens op de lokale gateway instellen om te werken met uw logische apps.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-124">These steps show how to set up the on-premises data gateway to work with your logic apps.</span></span> <span data-ttu-id="8cc5b-125">Zie voor meer informatie over ondersteunde connectors [Connectors voor Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8cc5b-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="8cc5b-126">Zie voor informatie over het gebruik van de gateway met andere services, deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="8cc5b-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="8cc5b-127">Microsoft Power BI lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="8cc5b-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="8cc5b-128">Azure Analysis Services op locatie gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="8cc5b-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="8cc5b-129">Microsoft-Flow lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="8cc5b-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="8cc5b-130">Microsoft PowerApps lokale gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="8cc5b-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="8cc5b-131">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8cc5b-131">Requirements</span></span>

* <span data-ttu-id="8cc5b-132">U moet al hebben [data gateway geïnstalleerd op een lokale computer](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="8cc5b-132">You must have already [installed the data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="8cc5b-133">Wanneer u zich bij de Azure-portal aanmelden, hebt u dezelfde werk of schoolaccount dat is gebruikt om te gebruiken [installeren van de lokale data gateway](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="8cc5b-133">When you sign in to the Azure portal, you have to use the same work or school account that was used to [install the on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="8cc5b-134">Uw account aanmelden moet ook beschikken over een Azure-abonnement moet worden gebruikt wanneer u een gateway-resource in de Azure-portal voor uw gateway-installatie maken.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-134">Your sign-in account must also have an Azure subscription to use when you create a gateway resource in the Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="8cc5b-135">De gateway-installatie kan niet al door een Azure-gateway-resource wordt geclaimd.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="8cc5b-136">U kunt de gateway-installatie slechts aan één Azure-gateway resource koppelen.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-136">You can associate your gateway installation to only one Azure gateway resource.</span></span> <span data-ttu-id="8cc5b-137">Claim gebeurt wanneer u de gateway-resource maken, zodat de installatie niet beschikbaar voor andere bronnen is.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-137">Claim happens when you create the gateway resource so that the installation is unavailable for other resources.</span></span>

## <a name="set-up-the-data-gateway-connection"></a><span data-ttu-id="8cc5b-138">De data gateway-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="8cc5b-138">Set up the data gateway connection</span></span>

### <a name="1-install-the-on-premises-data-gateway"></a><span data-ttu-id="8cc5b-139">1. De on-premises gegevensgateway installeren</span><span class="sxs-lookup"><span data-stu-id="8cc5b-139">1. Install the on-premises data gateway</span></span>

<span data-ttu-id="8cc5b-140">Als u nog niet gedaan hebt, volgt u de [stappen voor het installeren van de lokale data gateway](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="8cc5b-140">If you haven't already, follow the [steps to install the on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="8cc5b-141">Voordat u met de andere stappen doorgaat, zorg er dan voor dat u de data gateway geïnstalleerd op een lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-141">Before you continue with the other steps, make sure that you installed the data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-the-on-premises-data-gateway"></a><span data-ttu-id="8cc5b-142">2. Een Azure-resource voor de lokale data gateway maken</span><span class="sxs-lookup"><span data-stu-id="8cc5b-142">2. Create an Azure resource for the on-premises data gateway</span></span>

<span data-ttu-id="8cc5b-143">Nadat u de gateway op een lokale computer installeert, maakt u uw data gateway als een resource in Azure.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-143">After you install the gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="8cc5b-144">Uw gateway-resource koppelt in deze stap ook aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="8cc5b-145">Meld u aan bij [Azure Portal](https://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="8cc5b-145">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="8cc5b-146">Zorg ervoor dat voor het gebruik van hetzelfde Azure werk of school e-mailadres gebruikt voor het installeren van de gateway.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-146">Make sure to use the same Azure work or school email address used to install the gateway.</span></span>

2. <span data-ttu-id="8cc5b-147">Kies in het menu links in Azure **nieuw** > **Enterprise Integration** > **On-premises gegevensgateway** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="8cc5b-147">On the left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   !['On-premises data gateway' vinden](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="8cc5b-149">Op de **verbinding-gateway maken** blade vindt deze informatie om de bron van uw data gateway te maken:</span><span class="sxs-lookup"><span data-stu-id="8cc5b-149">On the **Create connection gateway** blade, provide these details to create your data gateway resource:</span></span>

    * <span data-ttu-id="8cc5b-150">**Naam**: Voer een naam voor uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="8cc5b-151">**Abonnement**: Selecteer de Azure-abonnement wilt koppelen aan uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-151">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="8cc5b-152">Dit abonnement moet hetzelfde abonnement als uw logische app.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-152">This subscription should be the same subscription as your logic app.</span></span>
   
      <span data-ttu-id="8cc5b-153">Het standaardabonnement is gebaseerd op het Azure-account dat u gebruikt voor aanmelden.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-153">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="8cc5b-154">**Resourcegroep**: een resourcegroep maken of een bestaande resourcegroep selecteren voor het implementeren van uw gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="8cc5b-155">Resourcegroepen kunnen u gerelateerde Azure activa beheren als een verzameling.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="8cc5b-156">**Locatie**: Azure beperkt deze locatie bij dezelfde regio die is geselecteerd voor de gateway-cloudservice tijdens [gateway-installatie](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="8cc5b-156">**Location**: Azure restricts this location to the same region that was selected for the gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="8cc5b-157">Zorg ervoor dat de locatie van de resource gateway overeenkomt met de gateway cloud service-locatie.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-157">Make sure that the gateway resource location matches the gateway cloud service location.</span></span> <span data-ttu-id="8cc5b-158">De gateway-installatie mogelijk anders niet weergegeven in de lijst Geïnstalleerde gateways voor selectie in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-158">Otherwise, your gateway installation might not appear in the installed gateways list for you to select in the next step.</span></span>
      > 
      > <span data-ttu-id="8cc5b-159">U kunt verschillende regio's gebruiken voor uw gateway-resource en voor uw logische app.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="8cc5b-160">**De naam van de installatie**: als uw gateway-installatie niet is geselecteerd, selecteert u de gateway die u eerder hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-160">**Installation Name**: If your gateway installation isn't already selected, select the gateway that you previously installed.</span></span> 

    <span data-ttu-id="8cc5b-161">Als u wilt de bron van de gateway toevoegen aan uw Azure-dashboard, kies **vastmaken aan dashboard**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-161">To add the gateway resource to your Azure dashboard, choose **Pin to dashboard**.</span></span> 
    <span data-ttu-id="8cc5b-162">Als u bent klaar, kiest u **maken**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="8cc5b-163">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8cc5b-163">For example:</span></span>

    ![Geef details op uw on-premises gegevensgateway maken](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="8cc5b-165">Als u wilt zoeken of weergeven van uw data gateway op elk gewenst moment, de belangrijkste Azure linkermenu, gaat u naar **meer Services** > **Enterprise Integration** > **On-premises gegevensgateways**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-165">To find or view your data gateway at any time,  from the main Azure left menu, go to  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Ga naar 'Meer services', 'Enterprise Integration', 'On-premises gegevensgateways'](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-to-the-on-premises-data-gateway"></a><span data-ttu-id="8cc5b-167">3. Uw logische app verbinden met de lokale data gateway</span><span class="sxs-lookup"><span data-stu-id="8cc5b-167">3. Connect your logic app to the on-premises data gateway</span></span>

<span data-ttu-id="8cc5b-168">Nu dat u hebt uw data gateway resource gemaakt en die uw Azure-abonnement is gekoppeld aan deze resource, maak een verbinding tussen uw logische app en de data gateway.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and the data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="8cc5b-169">De locatie van uw gateway verbinding moet aanwezig zijn in dezelfde regio bevinden als uw logische app, maar u kunt een data gateway die voorkomt in een andere regio.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-169">Your gateway connection location must exist in the same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="8cc5b-170">In de Azure portal maken of openen van uw logische app in Logic App-ontwerper.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-170">In the Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="8cc5b-171">Toevoegen van een connector die ondersteuning biedt voor lokale verbindingen, zoals SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="8cc5b-172">Na de aangegeven volgorde en selecteer **verbinden via lokale gegevensgateway**, Geef een unieke verbindingsnaam en de vereiste gegevens in en selecteert u de gateway-resource voor gegevens die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-172">Following the order shown, select **Connect via on-premises data gateway**, provide a unique connection name and the required information, and select the data gateway resource that you want to use.</span></span> <span data-ttu-id="8cc5b-173">Als u bent klaar, kiest u **maken**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="8cc5b-174">Een unieke verbindingsnaam kunt u gemakkelijk herkennen die verbinding later, vooral wanneer u meerdere verbindingen maken.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="8cc5b-175">Indien van toepassing, moet u ook de gekwalificeerde domeinnaam voor uw gebruikersnaam bevatten.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-175">If applicable, also include the qualified domain for your username.</span></span> 

   ![Verbinding maken tussen logic app en data gateway](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="8cc5b-177">Gefeliciteerd, uw gatewayverbinding is nu gereed voor uw logische app te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-177">Congratulations, your gateway connection is now ready for your logic app to use.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="8cc5b-178">De instellingen voor de gateway-verbinding bewerken</span><span class="sxs-lookup"><span data-stu-id="8cc5b-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="8cc5b-179">Nadat u een gatewayverbinding voor uw logische app maakt, kunt u later de instellingen voor die specifieke verbinding bijwerken.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-179">After you create a gateway connection for your logic app, you might want to later update the settings for that specific connection.</span></span>

1. <span data-ttu-id="8cc5b-180">De gatewayverbinding vinden:</span><span class="sxs-lookup"><span data-stu-id="8cc5b-180">To find the gateway connection:</span></span>

   * <span data-ttu-id="8cc5b-181">Op de blade logic app onder **ontwikkelingsprogramma's**, selecteer **API verbindingen**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-181">On the logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="8cc5b-182">De **API verbindingen** deelvenster ziet u alle API-verbindingen die zijn gekoppeld aan uw logische app, inclusief gatewayverbindingen.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-182">The **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Ga naar uw logische app, selecteert u 'API verbindingen'](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="8cc5b-184">Of Ga naar in het belangrijkste Azure linkermenu **meer Services** > **Web- en Mobile Services** > **API verbindingen** voor alle API-verbindingen, inclusief gatewayverbindingen die gekoppeld aan uw Azure-abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-184">Or, from the main Azure left menu, go to **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="8cc5b-185">Of op het belangrijkste Azure linkermenu, gaat u naar **alle resources** voor alle API-verbindingen, inclusief gatewayverbindingen die gekoppeld aan uw Azure-abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-185">Or, on the main Azure left menu, go to **All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="8cc5b-186">Selecteer de gatewayverbinding die u wilt weergeven of bewerken en kies **API bewerken verbinding**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-186">Select the gateway connection that you want to view or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="8cc5b-187">Als u de updates worden niet doorgevoerd, probeert u [stoppen en opnieuw starten van de gateway Windows-service](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="8cc5b-187">If your updates don't take effect, try [stopping and restarting the gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="8cc5b-188">Schakelt u of uw lokale gegevens gateway bron verwijderen</span><span class="sxs-lookup"><span data-stu-id="8cc5b-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="8cc5b-189">Als u wilt maken van een andere gateway-resource, uw gateway koppelen aan een andere resource of verwijder de gateway-resource, kunt u de bron van de gateway verwijderen zonder gevolgen voor de installatie van de gateway.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-189">To create a different gateway resource, associate your gateway with a different resource, or remove the gateway resource, you can delete the gateway resource without affecting the gateway installation.</span></span> 

1. <span data-ttu-id="8cc5b-190">In het belangrijkste Azure linkermenu, gaat u naar **alle resources**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-190">From the main Azure left menu, go to **All resources**.</span></span> 
2. <span data-ttu-id="8cc5b-191">Zoek en selecteer uw data gateway-resource.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="8cc5b-192">Kies **On-premises Data Gateway**, en kies op de werkbalk resource **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="8cc5b-192">Choose **On-premises Data Gateway**, and on the resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="8cc5b-193">Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="8cc5b-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="8cc5b-194">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8cc5b-194">Next steps</span></span>

* [<span data-ttu-id="8cc5b-195">Uw logische apps beveiligen</span><span class="sxs-lookup"><span data-stu-id="8cc5b-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="8cc5b-196">Algemene voorbeelden en scenario's voor logic apps</span><span class="sxs-lookup"><span data-stu-id="8cc5b-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
