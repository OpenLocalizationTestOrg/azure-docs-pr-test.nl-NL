---
title: aaaIoT externe controle en meldingen met Azure Logic Apps | Microsoft Docs
description: Gebruik Azure Logic Apps voor IoT Temperatuurbewaking op uw IoT-hub en automatisch verzenden van meldingen tooyour postvak voor eventuele afwijkingen gedetecteerd.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: bewaking, iot-meldingen IOT iot Temperatuurbewaking
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="6e150-104">Externe controle IoT en meldingen met Azure Logic Apps die gebruikmaken van uw IoT-hub en Postvak</span><span class="sxs-lookup"><span data-stu-id="6e150-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="6e150-106">Logische Apps van Azure biedt een manier tooautomate processen als een reeks stappen.</span><span class="sxs-lookup"><span data-stu-id="6e150-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="6e150-107">Een logische app kan verbinding maken tussen verschillende services en protocollen.</span><span class="sxs-lookup"><span data-stu-id="6e150-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="6e150-108">Deze begint met een trigger, zoals 'Wanneer een account is toegevoegd', en gevolgd door een combinatie van acties zoals het verzenden van een pushmelding.</span><span class="sxs-lookup"><span data-stu-id="6e150-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="6e150-109">Deze functie stelt Logic Apps een perfecte IoT-oplossing voor IoT bewaking, zoals de waarschuwing op afwijkingen is vereist, onder andere gebruiksscenario's bijwerkt.</span><span class="sxs-lookup"><span data-stu-id="6e150-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="6e150-110">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="6e150-110">What you learn</span></span>

<span data-ttu-id="6e150-111">U leert hoe toocreate een logische app die verbinding maakt van uw IoT-hub en uw postvak voor het controleren van de temperatuur en meldingen.</span><span class="sxs-lookup"><span data-stu-id="6e150-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="6e150-112">Wanneer Hallo temperatuur hoger dan 30 C is, markeert voor client-toepassing hello `temperatureAlert = "true"` in Hallo-bericht van het tooyour iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="6e150-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="6e150-113">Hallo-bericht triggers Hallo logic app toosend u een e-mailbericht.</span><span class="sxs-lookup"><span data-stu-id="6e150-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="6e150-114">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="6e150-114">What you do</span></span>

* <span data-ttu-id="6e150-115">Een service bus-naamruimte maken en toevoegen van een wachtrij tooit.</span><span class="sxs-lookup"><span data-stu-id="6e150-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="6e150-116">Voeg een eindpunt en een routering regel tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6e150-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="6e150-117">Maken, configureren en testen van een logische app.</span><span class="sxs-lookup"><span data-stu-id="6e150-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="6e150-118">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="6e150-118">What you need</span></span>

* <span data-ttu-id="6e150-119">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="6e150-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="6e150-120">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e150-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="6e150-121">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="6e150-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="6e150-122">Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="6e150-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="6e150-123">Service bus-naamruimte maken en toevoegen van een wachtrij tooit</span><span class="sxs-lookup"><span data-stu-id="6e150-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="6e150-124">Een service bus-naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="6e150-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="6e150-125">Op Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Enterprise Integration** > **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="6e150-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="6e150-126">Hallo volgende informatie bevatten:</span><span class="sxs-lookup"><span data-stu-id="6e150-126">Provide hello following information:</span></span>

   <span data-ttu-id="6e150-127">**Naam**: Hallo-naam van Hallo servicebus.</span><span class="sxs-lookup"><span data-stu-id="6e150-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="6e150-128">**Prijscategorie**: klik op **Basic** > **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="6e150-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="6e150-129">Hallo Basic laag is voldoende voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6e150-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="6e150-130">**Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6e150-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="6e150-131">**Locatie**: gebruik Hallo dezelfde locatie die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6e150-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="6e150-132">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e150-132">Click **Create**.</span></span>

   ![Maken van een service bus-naamruimte in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="6e150-134">Toevoegen van een service bus-wachtrij</span><span class="sxs-lookup"><span data-stu-id="6e150-134">Add a service bus queue</span></span>

1. <span data-ttu-id="6e150-135">Hallo service bus-naamruimte openen en klik vervolgens op **+ wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="6e150-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="6e150-136">Voer een naam voor de wachtrij Hallo en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6e150-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="6e150-137">Hallo service bus-wachtrij te openen en klik vervolgens op **gedeeld toegangsbeleid** > **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6e150-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="6e150-138">Voer een naam voor het Hallo-beleid, selectievakje **beheren**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6e150-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Toevoegen van een service bus-wachtrij in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="6e150-140">Voeg een eindpunt en een routering regel tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="6e150-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="6e150-141">Een eindpunt toevoegen</span><span class="sxs-lookup"><span data-stu-id="6e150-141">Add an endpoint</span></span>

1. <span data-ttu-id="6e150-142">Uw IoT-hub te openen, klikt u op eindpunten > + toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6e150-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="6e150-143">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="6e150-143">Enter hello following information:</span></span>

   <span data-ttu-id="6e150-144">**Naam**: Hallo-naam van het Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="6e150-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="6e150-145">**Eindpunttype**: Selecteer **Service Bus-wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="6e150-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="6e150-146">**Service Bus-naamruimte**: Selecteer Hallo-naamruimte die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e150-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="6e150-147">**Service Bus-wachtrij**: Selecteer Hallo wachtrij die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e150-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="6e150-148">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e150-148">Click **OK**.</span></span>

   ![Toevoegen van een eindpunt tooyour IoT-hub in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="6e150-150">Toevoegen van een regel voor doorsturen</span><span class="sxs-lookup"><span data-stu-id="6e150-150">Add a routing rule</span></span>

1. <span data-ttu-id="6e150-151">Klik op in uw IoT-hub **Routes** > **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6e150-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="6e150-152">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="6e150-152">Enter hello following information:</span></span>

   <span data-ttu-id="6e150-153">**Naam**: Hallo-naam van regel voor het doorsturen van Hallo.</span><span class="sxs-lookup"><span data-stu-id="6e150-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="6e150-154">**Gegevensbron**: Selecteer **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="6e150-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="6e150-155">**Eindpunt**: Selecteer Hallo eindpunt die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e150-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="6e150-156">**Querytekenreeks**: Voer `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="6e150-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="6e150-157">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e150-157">Click **Save**.</span></span>

   ![Toevoegen van een regel voor doorsturen in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="6e150-159">Maken en configureren van een logische app</span><span class="sxs-lookup"><span data-stu-id="6e150-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="6e150-160">Een logische app maken</span><span class="sxs-lookup"><span data-stu-id="6e150-160">Create a logic app</span></span>

1. <span data-ttu-id="6e150-161">In Hallo [Azure-portal](https://portal.azure.com/), klikt u op **nieuw** > **Enterprise Integration** > **logische App**.</span><span class="sxs-lookup"><span data-stu-id="6e150-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="6e150-162">Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="6e150-162">Enter hello following information:</span></span>

   <span data-ttu-id="6e150-163">**Naam**: Hallo-naam van Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="6e150-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="6e150-164">**Resourcegroep**: gebruik Hallo dezelfde resourcegroep die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6e150-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="6e150-165">**Locatie**: gebruik Hallo dezelfde locatie die gebruikmaakt van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6e150-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="6e150-166">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="6e150-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="6e150-167">Hallo logic app configureren</span><span class="sxs-lookup"><span data-stu-id="6e150-167">Configure hello logic app</span></span>

1. <span data-ttu-id="6e150-168">Hallo logische app dat wordt geopend in Hallo Logic Apps Designer openen.</span><span class="sxs-lookup"><span data-stu-id="6e150-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="6e150-169">In Hallo Logic Apps Designer, klikt u op **lege logische App**.</span><span class="sxs-lookup"><span data-stu-id="6e150-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Beginnen met een lege logische app in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="6e150-171">Klik op **Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="6e150-171">Click **Service Bus**.</span></span>

   ![Selecteer de Service Bus toostart uw logische app maken in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="6e150-173">Klik op **Service Bus-bij een of meer in een wachtrij (automatisch aanvullen berichten)**.</span><span class="sxs-lookup"><span data-stu-id="6e150-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="6e150-174">Een service bus-verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="6e150-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="6e150-175">Voer een verbindingsnaam.</span><span class="sxs-lookup"><span data-stu-id="6e150-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="6e150-176">Klik op service bus-naamruimte Hallo > Hallo service bus-beleid > **maken**.</span><span class="sxs-lookup"><span data-stu-id="6e150-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Een service bus-verbinding voor uw logische app maken in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="6e150-178">Klik op **doorgaan** nadat Hallo service bus-verbinding is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="6e150-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="6e150-179">Selecteer Hallo wachtrij die u hebt gemaakt en voer `175` voor **maximumaantal bericht**</span><span class="sxs-lookup"><span data-stu-id="6e150-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Hallo maximale aantal voor Hallo service bus-verbinding in uw logische app opgeven](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="6e150-181">Klik op knop toosave Hallo wijzigingen ' opgeslagen'.</span><span class="sxs-lookup"><span data-stu-id="6e150-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="6e150-182">Maak een SMTP-service-verbinding.</span><span class="sxs-lookup"><span data-stu-id="6e150-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="6e150-183">Klik op **nieuwe stap** > **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6e150-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="6e150-184">Type `SMTP`, klikt u op Hallo **SMTP** service in de zoekresultaten Hallo en klik vervolgens op **SMTP - e-mailbericht verzenden**.</span><span class="sxs-lookup"><span data-stu-id="6e150-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Een SMTP-verbinding maken in uw logische app in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="6e150-186">Voer Hallo SMTP-gegevens van uw postvak in en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="6e150-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Voer SMTP-verbindingsgegevens in uw logische app in hello Azure-portal](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="6e150-188">Hallo SMTP-informatie ophalen voor [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), en [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="6e150-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="6e150-189">Voer uw e-mailadres voor **van** en **naar**, en `High temperature detected` voor **onderwerp** en **hoofdtekst**.</span><span class="sxs-lookup"><span data-stu-id="6e150-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="6e150-190">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6e150-190">Click **Save**.</span></span>

<span data-ttu-id="6e150-191">Hallo logische app is defect wanneer u deze opslaat.</span><span class="sxs-lookup"><span data-stu-id="6e150-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="6e150-192">Test Hallo logische app</span><span class="sxs-lookup"><span data-stu-id="6e150-192">Test hello logic app</span></span>

1. <span data-ttu-id="6e150-193">Hallo-clienttoepassing die u implementeert tooyour apparaat in Start [ESP8266 verbinding tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e150-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="6e150-194">Hallo omgeving temperatuur rond Hallo SensorTag toobe hierboven 30 C. verhogen Bijvoorbeeld, een kaars rond de SensorTag lichten.</span><span class="sxs-lookup"><span data-stu-id="6e150-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="6e150-195">U ontvangt een e-mailmelding verzonden door Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="6e150-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6e150-196">Uw e-provider moet mogelijk tooverify Hallo afzender identiteit toomake afbeelding moet u die Hallo e-mailbericht verzendt.</span><span class="sxs-lookup"><span data-stu-id="6e150-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e150-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6e150-197">Next steps</span></span>

<span data-ttu-id="6e150-198">U hebt gemaakt aan een logische app die verbinding maakt van uw IoT-hub en uw postvak voor het controleren van de temperatuur en meldingen.</span><span class="sxs-lookup"><span data-stu-id="6e150-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
