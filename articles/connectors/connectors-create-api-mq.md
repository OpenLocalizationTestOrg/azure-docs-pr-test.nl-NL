---
title: aaaLearn hoe toouse Hallo MQ-connector in Azure Logic Apps | Microsoft Docs
description: Verbinding maken met tooan on-premises of Azure MQ server van uw logische app werkstroom toobrowse, ontvangen en verzenden van berichten tooWebSphere MQ
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="53254-103">Verbinding maken met IBM MQ server tooan vanuit logic apps met behulp van Hallo MQ-connector</span><span class="sxs-lookup"><span data-stu-id="53254-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="53254-104">Microsoft-Connector voor MQ verzendt en berichten die zijn opgeslagen in een MQ Server on-premises of in Azure ophaalt.</span><span class="sxs-lookup"><span data-stu-id="53254-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="53254-105">Deze connector omvat een Microsoft-MQ-client die met een externe IBM MQ-server via een TCP/IP-netwerk communiceert.</span><span class="sxs-lookup"><span data-stu-id="53254-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="53254-106">Dit document is een connector starter handleiding toouse Hallo MQ.</span><span class="sxs-lookup"><span data-stu-id="53254-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="53254-107">Raden wij u beginnen door te bladeren door een enkel bericht in een wachtrij en probeert u het Hallo andere acties.</span><span class="sxs-lookup"><span data-stu-id="53254-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="53254-108">Hallo MQ connector bevat Hallo van de volgende activiteiten.</span><span class="sxs-lookup"><span data-stu-id="53254-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="53254-109">Er zijn geen triggers.</span><span class="sxs-lookup"><span data-stu-id="53254-109">There are no triggers.</span></span>

-   <span data-ttu-id="53254-110">Een enkel bericht zonder te verwijderen van het Hallo-bericht van Hallo IBM MQ Server bladeren</span><span class="sxs-lookup"><span data-stu-id="53254-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="53254-111">Berichten batchgewijs zoeken zonder het Hallo-berichten verwijderen uit IBM MQ Server Hallo</span><span class="sxs-lookup"><span data-stu-id="53254-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="53254-112">Een enkel bericht ontvangen en het Hallo-bericht verwijderen uit IBM MQ Server Hallo</span><span class="sxs-lookup"><span data-stu-id="53254-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="53254-113">Ontvangen berichten batchgewijs en Hallo-berichten uit Hallo IBM MQ Server verwijderen</span><span class="sxs-lookup"><span data-stu-id="53254-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="53254-114">Een enkel bericht toohello IBM MQ Server verzenden</span><span class="sxs-lookup"><span data-stu-id="53254-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="53254-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="53254-115">Prerequisites</span></span>

* <span data-ttu-id="53254-116">Als u een on-premises MQ server, [Hallo lokale gegevensgateway installeren](../logic-apps/logic-apps-gateway-install.md) op een server in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="53254-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="53254-117">Als Hallo MQ Server openbaar beschikbaar is of beschikbaar is in Azure, vervolgens Hallo data gateway is niet gebruikt of nodig.</span><span class="sxs-lookup"><span data-stu-id="53254-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="53254-118">Hallo-server waar Hallo On-Premises Data Gateway is geïnstalleerd moet ook beschikken over .net Framework 4.6 voor Hallo MQ Connector toofunction geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="53254-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="53254-119">Maken van hello Azure-resource voor Hallo lokale gegevensgateway - [Hallo data gateway-verbinding instellen](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="53254-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="53254-120">IBM WebSphere MQ versies officieel ondersteund:</span><span class="sxs-lookup"><span data-stu-id="53254-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="53254-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="53254-121">MQ 7.5</span></span>
   * <span data-ttu-id="53254-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="53254-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="53254-123">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="53254-123">Create a logic app</span></span>

1. <span data-ttu-id="53254-124">In Hallo **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.</span><span class="sxs-lookup"><span data-stu-id="53254-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="53254-125">Voer Hallo **naam**, zoals MQTestApp, **abonnement**, **resourcegroep**, en **locatie** (gebruik Hallo locatie waar hello lokale Data Gateway verbinding is geconfigureerd).</span><span class="sxs-lookup"><span data-stu-id="53254-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="53254-126">Selecteer **pincode toodashboard**, en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="53254-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="53254-127">![Logische App maken](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="53254-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="53254-128">Een trigger toevoegen</span><span class="sxs-lookup"><span data-stu-id="53254-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="53254-129">Hallo MQ-Connector heeft geen geen triggers bestaan.</span><span class="sxs-lookup"><span data-stu-id="53254-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="53254-130">Dus uw logische app, zoals hello gebruiken een ander trigger toostart **terugkeerpatroon** trigger.</span><span class="sxs-lookup"><span data-stu-id="53254-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="53254-131">Hallo **Logic Apps Designer** wordt geopend, selecteer **terugkeerpatroon** in Hallo lijst met algemene triggers.</span><span class="sxs-lookup"><span data-stu-id="53254-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="53254-132">Selecteer **bewerken** binnen Hallo terugkeerpatroon Trigger.</span><span class="sxs-lookup"><span data-stu-id="53254-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="53254-133">Set Hallo **frequentie** te**dag**, en set Hallo **Interval** te**7**.</span><span class="sxs-lookup"><span data-stu-id="53254-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="53254-134">Een enkel bericht bladeren</span><span class="sxs-lookup"><span data-stu-id="53254-134">Browse a single message</span></span>
1. <span data-ttu-id="53254-135">Selecteer **+ een nieuwe stap**, en selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="53254-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="53254-136">Typ in het zoekvak Hallo `mq`, en selecteer vervolgens **MQ - bladeren bericht**.</span><span class="sxs-lookup"><span data-stu-id="53254-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="53254-137">![Bericht bladeren](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="53254-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="53254-138">Als er geen een bestaande MQ-verbinding, klikt u vervolgens Hallo verbinding te maken:</span><span class="sxs-lookup"><span data-stu-id="53254-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="53254-139">Selecteer **verbinden via lokale gegevensgateway**, en Voer Hallo eigenschappen van uw server MQ.</span><span class="sxs-lookup"><span data-stu-id="53254-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="53254-140">Voor **Server**, Voer Hallo MQ-servernaam of Voer Hallo IP-adres, gevolgd door een dubbele punt en Hallo-poortnummer.</span><span class="sxs-lookup"><span data-stu-id="53254-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="53254-141">Hallo **gateway** dropdown geeft een lijst van de bestaande gatewayverbindingen die zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="53254-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="53254-142">Selecteer uw gateway.</span><span class="sxs-lookup"><span data-stu-id="53254-142">Select your gateway.</span></span>
    3. <span data-ttu-id="53254-143">Selecteer **maken** na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="53254-143">Select **Create** when finished.</span></span> <span data-ttu-id="53254-144">Uw verbinding lijkt vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="53254-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="53254-145">![Verbindingseigenschappen](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="53254-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="53254-146">U kunt in de eigenschappen van Hallo actie:</span><span class="sxs-lookup"><span data-stu-id="53254-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="53254-147">Gebruik Hallo **wachtrij** eigenschap tooaccess een andere wachtrijnaam heeft dan de waarde die is gedefinieerd in Hallo verbinding</span><span class="sxs-lookup"><span data-stu-id="53254-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="53254-148">Gebruik Hallo **MessageId**, **CorrelationId**, **GroupId**, en andere toobrowse eigenschappen voor een bericht op basis van verschillende MQ Hallo-berichteigenschappen</span><span class="sxs-lookup"><span data-stu-id="53254-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="53254-149">Stel **IncludeInfo** te**True** tooinclude extra berichtinformatie in Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="53254-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="53254-150">Of stel deze in te**False** toonot aanvullend berichtinformatie opnemen in Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="53254-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="53254-151">Voer een **time-out** waarde toodetermine hoe lang toowait voor een tooarrive bericht in een lege wachtrij.</span><span class="sxs-lookup"><span data-stu-id="53254-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="53254-152">Als er niets wordt opgegeven, eerste bericht in de wachtrij Hallo Hallo is opgehaald er is geen tijd besteed aan het wachten op een bericht tooappear.</span><span class="sxs-lookup"><span data-stu-id="53254-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="53254-153">![Berichteigenschappen bladeren](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="53254-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="53254-154">**Sla** uw wijzigingen en vervolgens **uitvoeren** uw logische app:</span><span class="sxs-lookup"><span data-stu-id="53254-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="53254-155">![Opslaan en uitvoeren](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="53254-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="53254-156">Na enkele seconden Hallo stappen Hallo uitgevoerd worden weergegeven en kunt u Hallo uitvoer bekijkt.</span><span class="sxs-lookup"><span data-stu-id="53254-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="53254-157">Selecteer Hallo groen vinkje toosee details van elke stap.</span><span class="sxs-lookup"><span data-stu-id="53254-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="53254-158">Selecteer **Zie ruwe uitvoer** toosee meer informatie over het Hallo uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="53254-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="53254-159">![Bericht uitvoer bladeren](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="53254-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="53254-160">Onbewerkte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="53254-160">Raw output:</span></span>  
    ![Bericht onbewerkte uitvoer bladeren](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="53254-162">Wanneer Hallo **IncludeInfo** optie tootrue is ingesteld, Hallo volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="53254-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="53254-163">![Bladeren bericht bevatten info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="53254-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="53254-164">Meerdere berichten bladeren</span><span class="sxs-lookup"><span data-stu-id="53254-164">Browse multiple messages</span></span>
<span data-ttu-id="53254-165">Hallo **berichten Bladeren** actie bevat een **BatchSize** optie tooindicate hoeveel berichten moeten worden geretourneerd uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="53254-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="53254-166">Als **BatchSize** heeft geen vermelding alle berichten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="53254-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="53254-167">Hallo geretourneerd uitvoer is een matrix van berichten.</span><span class="sxs-lookup"><span data-stu-id="53254-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="53254-168">Bij het toevoegen van Hallo **berichten Bladeren** actie eerste Hallo-verbinding die is geconfigureerd, is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="53254-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="53254-169">Selecteer **verbinding wijzigen** toocreate een nieuwe verbinding, of Selecteer een andere verbinding.</span><span class="sxs-lookup"><span data-stu-id="53254-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="53254-170">Hallo-uitvoer van bladeren berichten wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="53254-170">hello output of Browse messages shows:</span></span>  
![Berichten uitvoer bladeren](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="53254-172">Een enkel bericht ontvangen</span><span class="sxs-lookup"><span data-stu-id="53254-172">Receive a single message</span></span>
<span data-ttu-id="53254-173">Hallo **ontvangen van berichten** actie heeft dezelfde in- en uitgangen als Hallo Hallo **bladeren bericht** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="53254-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="53254-174">Wanneer u **ontvangen van berichten**, het Hallo-bericht is verwijderd uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="53254-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="53254-175">Meerdere berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="53254-175">Receive multiple messages</span></span>
<span data-ttu-id="53254-176">Hallo **berichten ontvangen** actie heeft dezelfde in- en uitgangen als Hallo Hallo **berichten Bladeren** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="53254-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="53254-177">Wanneer u **berichten ontvangen**, Hallo-berichten worden verwijderd uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="53254-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="53254-178">Als er geen berichten in wachtrij Hallo zijn bij het uitvoeren van een bladeren of een ontvangen, wordt Hallo stap mislukt met de Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="53254-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![MQ Nee bericht fout](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="53254-180">Een bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="53254-180">Send a message</span></span>
1. <span data-ttu-id="53254-181">Bij het toevoegen van Hallo **bericht verzenden** actie eerste Hallo-verbinding die is geconfigureerd, is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="53254-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="53254-182">Selecteer **verbinding wijzigen** toocreate een nieuwe verbinding, of Selecteer een andere verbinding.</span><span class="sxs-lookup"><span data-stu-id="53254-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="53254-183">Hallo geldig **berichttypen** zijn **Datagram**, **antwoord**, of **aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="53254-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="53254-184">![Eigenschappen van bericht verzenden](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="53254-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="53254-185">Hallo uitvoer van een bericht verzenden ziet eruit als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="53254-185">hello output of Send message looks like hello following:</span></span>  
![De uitvoer bericht verzenden](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="53254-187">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="53254-187">Connector-specific details</span></span>

<span data-ttu-id="53254-188">Alle triggers en acties die zijn gedefinieerd in swagger Hallo bekijken en ook bekijken in Hallo beperkingen [connector details](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="53254-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="53254-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53254-189">Next steps</span></span>
<span data-ttu-id="53254-190">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="53254-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="53254-191">Verken Hallo van andere beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="53254-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
