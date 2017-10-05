---
title: Informatie over het gebruik van de connector MQ in Azure Logic Apps | Microsoft Docs
description: Verbinding maken met een on-premises of Azure MQ server van uw werkstroom logic app bladeren, ontvangen en berichten verzenden naar WebSphere MQ
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
ms.openlocfilehash: 17c651585b56dae186286f5d8c68c363ae9c524d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="3cb4d-103">Verbinding maken met een IBM MQ server vanuit logic apps met behulp van de connector MQ</span><span class="sxs-lookup"><span data-stu-id="3cb4d-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="3cb4d-104">Microsoft-Connector voor MQ verzendt en berichten die zijn opgeslagen in een MQ Server on-premises of in Azure ophaalt.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="3cb4d-105">Deze connector omvat een Microsoft-MQ-client die met een externe IBM MQ-server via een TCP/IP-netwerk communiceert.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="3cb4d-106">Dit document is een starter-handleiding voor het gebruik van de connector MQ.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="3cb4d-107">Wij raden dat u begint met bladeren door een enkel bericht in een wachtrij en probeert u de andere acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="3cb4d-108">De connector MQ omvat de volgende acties.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="3cb4d-109">Er zijn geen triggers.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-109">There are no triggers.</span></span>

-   <span data-ttu-id="3cb4d-110">Een enkel bericht bladeren zonder dat het bericht is verwijderd van de IBM MQ-Server</span><span class="sxs-lookup"><span data-stu-id="3cb4d-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="3cb4d-111">Berichten batchgewijs zoeken zonder het verwijderen van de berichten van de IBM MQ-Server</span><span class="sxs-lookup"><span data-stu-id="3cb4d-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="3cb4d-112">Een enkel bericht ontvangen en verwijderen van het bericht uit de IBM MQ-Server</span><span class="sxs-lookup"><span data-stu-id="3cb4d-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="3cb4d-113">Een batch met berichten ontvangen en berichten van de IBM MQ Server verwijderen</span><span class="sxs-lookup"><span data-stu-id="3cb4d-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="3cb4d-114">Een enkel bericht verzenden naar de IBM MQ-Server</span><span class="sxs-lookup"><span data-stu-id="3cb4d-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3cb4d-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3cb4d-115">Prerequisites</span></span>

* <span data-ttu-id="3cb4d-116">Als u een on-premises MQ server, [installeren van de lokale data gateway](../logic-apps/logic-apps-gateway-install.md) op een server in uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="3cb4d-117">Als de Server MQ openbaar beschikbaar, of beschikbaar is in Azure, is klikt u vervolgens de gegevensgateway niet gebruikt of nodig.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3cb4d-118">De server waarop de On-Premises Data Gateway is geïnstalleerd, moet ook beschikken over .net Framework 4.6 is geïnstalleerd voor de Connector MQ functie.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="3cb4d-119">Maken van de Azure-resource voor de lokale data gateway - [instellen van de gateway gegevensverbinding](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="3cb4d-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="3cb4d-120">IBM WebSphere MQ versies officieel ondersteund:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="3cb4d-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="3cb4d-121">MQ 7.5</span></span>
   * <span data-ttu-id="3cb4d-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="3cb4d-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="3cb4d-123">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="3cb4d-123">Create a logic app</span></span>

1. <span data-ttu-id="3cb4d-124">In de **Azure start board**, selecteer  **+**  (plusteken) **Web en mobiel**, en vervolgens **logische App**.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="3cb4d-125">Voer de **naam**, zoals MQTestApp, **abonnement**, **resourcegroep**, en **locatie** (gebruikt u de locatie waar de lokale Data Gateway-verbinding is geconfigureerd).</span><span class="sxs-lookup"><span data-stu-id="3cb4d-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="3cb4d-126">Selecteer **vastmaken aan dashboard**, en selecteer **maken**.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="3cb4d-127">![Logische App maken](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="3cb4d-128">Een trigger toevoegen</span><span class="sxs-lookup"><span data-stu-id="3cb4d-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="3cb4d-129">De MQ-Connector heeft geen geen triggers bestaan.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="3cb4d-130">Dus een andere trigger te gebruiken om te beginnen uw logische app, zoals de **terugkeerpatroon** trigger.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="3cb4d-131">De **Logic Apps Designer** wordt geopend, selecteer **terugkeerpatroon** in de lijst met algemene triggers.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="3cb4d-132">Selecteer **bewerken** binnen de Trigger terugkeerpatroon.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="3cb4d-133">Instellen de **frequentie** naar **dag**, en stel de **Interval** naar **7**.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="3cb4d-134">Een enkel bericht bladeren</span><span class="sxs-lookup"><span data-stu-id="3cb4d-134">Browse a single message</span></span>
1. <span data-ttu-id="3cb4d-135">Selecteer **+ een nieuwe stap**, en selecteer **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="3cb4d-136">Typ in het zoekvak `mq`, en selecteer vervolgens **MQ - bladeren bericht**.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="3cb4d-137">![Bericht bladeren](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="3cb4d-138">Als er geen een bestaande MQ-verbinding, klikt u vervolgens de verbinding te maken:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="3cb4d-139">Selecteer **verbinden via lokale gegevensgateway**, en voert u de eigenschappen van uw server MQ.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="3cb4d-140">Voor **Server**, voer de naam van de server MQ of geef het IP-adres gevolgd door een dubbelepunt en het poortnummer.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="3cb4d-141">De **gateway** dropdown geeft een lijst van de bestaande gatewayverbindingen die zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="3cb4d-142">Selecteer uw gateway.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-142">Select your gateway.</span></span>
    3. <span data-ttu-id="3cb4d-143">Selecteer **maken** na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-143">Select **Create** when finished.</span></span> <span data-ttu-id="3cb4d-144">Uw verbinding ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="3cb4d-145">![Verbindingseigenschappen](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="3cb4d-146">U kunt in de actie-eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="3cb4d-147">Gebruik de **wachtrij** eigenschap voor toegang tot een andere wachtrijnaam heeft dan de waarde die is gedefinieerd in de verbinding</span><span class="sxs-lookup"><span data-stu-id="3cb4d-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="3cb4d-148">Gebruik de **MessageId**, **CorrelationId**, **GroupId**, en andere eigenschappen om te bladeren naar een bericht op basis van de verschillende eigenschappen voor MQ-bericht</span><span class="sxs-lookup"><span data-stu-id="3cb4d-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="3cb4d-149">Stel **IncludeInfo** naar **waar** aanvullend berichtinformatie in de uitvoer wilt opnemen.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="3cb4d-150">Of stel deze in op **False** niet op te nemen informatie aanvullende berichten in de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="3cb4d-151">Voer een **time-out** waarde om te bepalen hoe lang moet worden gewacht voor een bericht moet worden uitgevoerd in een lege wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="3cb4d-152">Als er niets wordt opgegeven, wordt het eerste bericht in de wachtrij opgehaald en er is geen tijd besteed aan het wachten op een bericht wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="3cb4d-153">![Berichteigenschappen bladeren](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="3cb4d-154">**Sla** uw wijzigingen en vervolgens **uitvoeren** uw logische app:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="3cb4d-155">![Opslaan en uitvoeren](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="3cb4d-156">Na enkele seconden, de stappen van de uitvoering worden weergegeven en kunt u de uitvoer bekijken.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="3cb4d-157">Selecteer in het groen vinkje details van elke stap.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="3cb4d-158">Selecteer **Zie ruwe uitvoer** voor aanvullende informatie over de uitvoergegevens.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="3cb4d-159">![Bericht uitvoer bladeren](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="3cb4d-160">Onbewerkte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-160">Raw output:</span></span>  
    ![Bericht onbewerkte uitvoer bladeren](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="3cb4d-162">Wanneer de **IncludeInfo** optie is ingesteld op true, wordt de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="3cb4d-163">![Bladeren bericht bevatten info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="3cb4d-164">Meerdere berichten bladeren</span><span class="sxs-lookup"><span data-stu-id="3cb4d-164">Browse multiple messages</span></span>
<span data-ttu-id="3cb4d-165">De **berichten Bladeren** actie bevat een **BatchSize** optie om aan te geven hoeveel berichten uit de wachtrij moeten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="3cb4d-166">Als **BatchSize** heeft geen vermelding alle berichten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="3cb4d-167">De resulterende uitvoer is een matrix van berichten.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="3cb4d-168">Bij het toevoegen van de **berichten Bladeren** actie voor de eerste verbinding die is geconfigureerd, is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="3cb4d-169">Selecteer **verbinding wijzigen** een nieuwe verbinding maken of Selecteer een andere verbinding.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="3cb4d-170">De uitvoer van bladeren berichten wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-170">The output of Browse messages shows:</span></span>  
![Berichten uitvoer bladeren](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="3cb4d-172">Een enkel bericht ontvangen</span><span class="sxs-lookup"><span data-stu-id="3cb4d-172">Receive a single message</span></span>
<span data-ttu-id="3cb4d-173">De **ontvangen van berichten** actie heeft de dezelfde invoer en uitvoer als de **bladeren bericht** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="3cb4d-174">Wanneer u **ontvangen van berichten**, het bericht is verwijderd uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="3cb4d-175">Meerdere berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="3cb4d-175">Receive multiple messages</span></span>
<span data-ttu-id="3cb4d-176">De **berichten ontvangen** actie heeft de dezelfde invoer en uitvoer als de **berichten Bladeren** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="3cb4d-177">Wanneer u **berichten ontvangen**, worden de berichten uit de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="3cb4d-178">Als er geen berichten in de wachtrij zijn bij het uitvoeren van een bladeren of een ontvangen, wordt de stap mislukt met de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![MQ Nee bericht fout](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="3cb4d-180">Een bericht verzenden</span><span class="sxs-lookup"><span data-stu-id="3cb4d-180">Send a message</span></span>
1. <span data-ttu-id="3cb4d-181">Bij het toevoegen van de **bericht verzenden** actie voor de eerste verbinding die is geconfigureerd, is standaard geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="3cb4d-182">Selecteer **verbinding wijzigen** een nieuwe verbinding maken of Selecteer een andere verbinding.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="3cb4d-183">Het geldige **berichttypen** zijn **Datagram**, **antwoord**, of **aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="3cb4d-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="3cb4d-184">![Eigenschappen van bericht verzenden](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="3cb4d-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="3cb4d-185">De uitvoer van een bericht verzenden ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="3cb4d-185">The output of Send message looks like the following:</span></span>  
![De uitvoer bericht verzenden](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="3cb4d-187">Connector-specifieke details</span><span class="sxs-lookup"><span data-stu-id="3cb4d-187">Connector-specific details</span></span>

<span data-ttu-id="3cb4d-188">Alle triggers en acties die zijn gedefinieerd in de swagger bekijken en ziet u ook de beperkingen in de [connector details](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="3cb4d-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3cb4d-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cb4d-189">Next steps</span></span>
<span data-ttu-id="3cb4d-190">[Een logische app maken](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3cb4d-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3cb4d-191">Bekijk de beschikbare connectors in Logic Apps op onze [API's lijst](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3cb4d-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
