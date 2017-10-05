---
title: Een functie maken die verbinding met Azure-services maakt | Microsoft Docs
description: Azure Functions gebruiken om een toepassing zonder server te maken die verbinding maakt met andere Azure-services.
services: functions
documentationcenter: dev-center-name
author: yochay
manager: manager-alias
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: ab86065d-6050-46c9-a336-1bfc1fa4b5a1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 65964a322f0adab4f648fb350bedb77b46bf9054
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-functions-to-create-a-function-that-connects-to-other-azure-services"></a><span data-ttu-id="54029-104">Azure Functions gebruiken om een toepassing te maken die verbinding maakt met andere Azure-services</span><span class="sxs-lookup"><span data-stu-id="54029-104">Use Azure Functions to create a function that connects to other Azure services</span></span>

<span data-ttu-id="54029-105">In dit onderwerp leert u hoe u een functie maakt in Azure Functions die luistert naar berichten in een Azure Storage-wachtrij en die berichten naar rijen in een Azure Storage-tabel kopieert.</span><span class="sxs-lookup"><span data-stu-id="54029-105">This topic shows you how to create a function in Azure Functions that listens to messages on an Azure Storage queue and copies the messages to rows in an Azure Storage table.</span></span> <span data-ttu-id="54029-106">Een door een timer geactiveerde functie wordt gebruikt voor het laden van berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="54029-106">A timer triggered function is used to load messages into the queue.</span></span> <span data-ttu-id="54029-107">Een tweede functie leest uit de wachtrij en schrijft berichten naar de tabel.</span><span class="sxs-lookup"><span data-stu-id="54029-107">A second function reads from the queue and writes messages to the table.</span></span> <span data-ttu-id="54029-108">De wachtrij en de tabel worden voor u gemaakt door Azure Functions op basis van de bindingsdefinities.</span><span class="sxs-lookup"><span data-stu-id="54029-108">Both the queue and the table are created for you by Azure Functions based on the binding definitions.</span></span> 

<span data-ttu-id="54029-109">Daarnaast wordt één functie in JavaScript geschreven en de andere in C#-script.</span><span class="sxs-lookup"><span data-stu-id="54029-109">To make things more interesting, one function is written in JavaScript and the other is written in C# script.</span></span> <span data-ttu-id="54029-110">Dit laat zien hoe een functie-app functies in verschillende talen kan hebben.</span><span class="sxs-lookup"><span data-stu-id="54029-110">This demonstrates how a function app can have functions in various languages.</span></span> 

<span data-ttu-id="54029-111">Dit scenario wordt uitgebeeld in een [video op kanaal 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span><span class="sxs-lookup"><span data-stu-id="54029-111">You can see this scenario demonstrated in a [video on Channel 9](https://channel9.msdn.com/Series/Windows-Azure-Web-Sites-Tutorials/Create-an-Azure-Function-which-binds-to-an-Azure-service/player).</span></span>

## <a name="create-a-function-that-writes-to-the-queue"></a><span data-ttu-id="54029-112">Een functie die naar de wachtrij schrijft maken</span><span class="sxs-lookup"><span data-stu-id="54029-112">Create a function that writes to the queue</span></span>

<span data-ttu-id="54029-113">Voordat u verbinding met een opslagwachtrij kunt maken, moet u een functie maken die de berichtenwachtrij laadt.</span><span class="sxs-lookup"><span data-stu-id="54029-113">Before you can connect to a storage queue, you need to create a function that loads the message queue.</span></span> <span data-ttu-id="54029-114">Deze JavaScript-functie maakt gebruik van een timeractivering die ervoor zorgt dat er elke 10 seconden een bericht naar de wachtrij wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="54029-114">This JavaScript function uses a timer trigger that writes a message to the queue every 10 seconds.</span></span> <span data-ttu-id="54029-115">Als u nog geen Azure-account hebt, kunt u [Try Azure Functions](https://functions.azure.com/try) (Azure Functions proberen) bekijken of [een gratis Azure-account maken](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="54029-115">If you don't already have an Azure account, check out the [Try Azure Functions](https://functions.azure.com/try) experience, or [create your free Azure account](https://azure.microsoft.com/free/).</span></span>

1. <span data-ttu-id="54029-116">Ga naar Azure Portal en zoek de functie-app.</span><span class="sxs-lookup"><span data-stu-id="54029-116">Go to the Azure portal and locate your function app.</span></span>

2. <span data-ttu-id="54029-117">Klik op **Nieuwe functie** > **TimerTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="54029-117">Click **New Function** > **TimerTrigger-JavaScript**.</span></span> 

3. <span data-ttu-id="54029-118">Geef de functie de naam **FunctionsBindingsDemo1**, voer een Cron-expressiewaarde in van `0/10 * * * * *` voor **Planning** en klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="54029-118">Name the function **FunctionsBindingsDemo1**, enter a cron expression value of `0/10 * * * * *` for **Schedule**, and then click **Create**.</span></span>
   
    ![Een door een timer geactiveerde functie toevoegen](./media/functions-create-an-azure-connected-function/new-trigger-timer-function.png)

    <span data-ttu-id="54029-120">U hebt nu een door een timer geactiveerde functie gemaakt die elke 10 seconden wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54029-120">You have now created a timer triggered function that runs every 10 seconds.</span></span>

5. <span data-ttu-id="54029-121">Klik in het tabblad **Ontwikkelen** op **Logboeken** en bekijk de activiteit in het logboek.</span><span class="sxs-lookup"><span data-stu-id="54029-121">On the **Develop** tab, click **Logs** and view the activity in the log.</span></span> <span data-ttu-id="54029-122">U ziet dat er elke 10 seconden een logboekvermelding wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="54029-122">You see a log entry written every 10 seconds.</span></span>
   
    ![Controleer in het logboek of de functie werkt](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-view-log.png)

## <a name="add-a-message-queue-output-binding"></a><span data-ttu-id="54029-124">Een uitvoerbinding voor de berichtenwachtrij toevoegen</span><span class="sxs-lookup"><span data-stu-id="54029-124">Add a message queue output binding</span></span>

1. <span data-ttu-id="54029-125">Kies op het tabblad **Integreren** **Nieuwe uitvoer** > **Azure Queue Storage** > **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="54029-125">On the **Integrate** tab, choose **New Output** > **Azure Queue Storage** > **Select**.</span></span>

    ![Een door een timer geactiveerde functie toevoegen](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab.png)

2. <span data-ttu-id="54029-127">Voer `myQueueItem` in voor **Naam van de berichtparameter** en `functions-bindings` voor **Wachtrijnaam**, selecteer een bestaande **Opslagaccountverbinding** of klik op **Nieuw** om een opslagaccountverbinding te maken, en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="54029-127">Enter `myQueueItem` for **Message parameter name** and `functions-bindings` for **Queue name**, select an existing **Storage account connection** or click **new** to create a storage account connection, and then click **Save**.</span></span>  

    ![De uitvoerbinding naar de opslagwachtrij maken](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab2.png)

1. <span data-ttu-id="54029-129">Ga terug naar het tabblad **Ontwikkelen** en voeg de volgende code toe aan de functie:</span><span class="sxs-lookup"><span data-stu-id="54029-129">Back in the **Develop** tab, append the following code to the function:</span></span>
   
    ```javascript
   
    function myQueueItem() 
    {
        return {
            msg: "some message goes here",
            time: "time goes here"
        }
    }
   
    ```
2. <span data-ttu-id="54029-130">Zoek de *Als*-instructie rond regel 9 van de functie en voer de volgende code in achter deze instructie.</span><span class="sxs-lookup"><span data-stu-id="54029-130">Locate the *if* statement around line 9 of the function, and insert the following code after that statement.</span></span>
   
    ```javascript
   
    var toBeQed = myQueueItem();
    toBeQed.time = timeStamp;
    context.bindings.myQueueItem = toBeQed;
   
    ```  
   
    <span data-ttu-id="54029-131">Met deze code maakt u een **myQueueItem** en stelt u de eigenschap **tijd** daarvan in op de huidige tijdstempel.</span><span class="sxs-lookup"><span data-stu-id="54029-131">This code creates a **myQueueItem** and sets its **time** property to the current timeStamp.</span></span> <span data-ttu-id="54029-132">Vervolgens wordt het nieuwe wachtrij-item toegevoegd aan de **myQueueItem**-binding van de context.</span><span class="sxs-lookup"><span data-stu-id="54029-132">It then adds the new queue item to the context's **myQueueItem** binding.</span></span>

3. <span data-ttu-id="54029-133">Klik op **Opslaan en uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="54029-133">Click **Save and Run**.</span></span>

## <a name="view-storage-updates-by-using-storage-explorer"></a><span data-ttu-id="54029-134">Opslagupdates weergeven met behulp van Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="54029-134">View storage updates by using Storage Explorer</span></span>
<span data-ttu-id="54029-135">U kunt controleren of de functie werkt door berichten te bekijken in de wachtrij die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="54029-135">You can verify that your function is working by viewing messages in the queue you created.</span></span>  <span data-ttu-id="54029-136">U kunt verbinding maken met uw opslagwachtrij met behulp van Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54029-136">You can connect to your storage queue by using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="54029-137">Via de portal kun u echter gemakkelijk verbinding maken met uw opslagaccount met behulp van Microsoft Azure Opslagverkenner.</span><span class="sxs-lookup"><span data-stu-id="54029-137">However, the portal makes it easy to connect to your storage account by using Microsoft Azure Storage Explorer.</span></span>

1. <span data-ttu-id="54029-138">Klik in het tabblad **Integreren** op de uitvoerbinding van uw wachtrij > **Documentatie**. Maak vervolgens de verbindingsreeks voor uw opslagaccount zichtbaar en kopieer de waarde.</span><span class="sxs-lookup"><span data-stu-id="54029-138">In the **Integrate** tab, click your queue output binding > **Documentation**, then unhide the Connection String for your storage account and copy the value.</span></span> <span data-ttu-id="54029-139">Met deze waarde kunt u verbinding maken met uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="54029-139">You use this value to connect to your storage account.</span></span>

    ![Azure Opslagverkenner downloaden](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-integrate-tab3.png)


2. <span data-ttu-id="54029-141">Als u dat nog niet hebt gedaan, downloadt en installeert u [Microsoft Azure Opslagverkenner](http://storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="54029-141">If you haven't already done so, download and install [Microsoft Azure Storage Explorer](http://storageexplorer.com).</span></span> 
 
3. <span data-ttu-id="54029-142">Klik in Opslagverkenner op het pictogram voor verbinding maken met Azure Storage, plak de verbindingsreeks in het veld en voltooi de wizard.</span><span class="sxs-lookup"><span data-stu-id="54029-142">In Storage Explorer, click the connect to Azure Storage icon, paste the connection string in the field, and complete the wizard.</span></span>

    ![Een verbinding toevoegen in Opslagverkenner](./media/functions-create-an-azure-connected-function/functionsbindingsdemo1-storage-explorer.png)

4. <span data-ttu-id="54029-144">Vouw onder **Local and attached** (Lokaal en gekoppeld) **Opslagaccounts** > uw opslagaccount > **Wachtrijen** > **functions-bindings** uit en controleer of berichten naar de wachtrij worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="54029-144">Under **Local and attached**, expand **Storage Accounts** > your storage account > **Queues** > **functions-bindings** and verify that messages are written to the queue.</span></span>

    ![Weergave van berichten in de wachtrij](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer.png)

    <span data-ttu-id="54029-146">Als de wachtrij niet bestaat of leeg is, is er waarschijnlijk een probleem met uw functiebinding of code.</span><span class="sxs-lookup"><span data-stu-id="54029-146">If the queue does not exist or is empty, there is most likely a problem with your function binding or code.</span></span>

## <a name="create-a-function-that-reads-from-the-queue"></a><span data-ttu-id="54029-147">Een functie die van de wachtrij leest maken</span><span class="sxs-lookup"><span data-stu-id="54029-147">Create a function that reads from the queue</span></span>

<span data-ttu-id="54029-148">Nu dat er berichten aan de wachtrij worden toegevoegd, kunt u een functie maken die van de wachtrij leest en de berichten permanent naar een Azure Storage-tabel schrijft.</span><span class="sxs-lookup"><span data-stu-id="54029-148">Now that you have messages being added to the queue, you can create another function that reads from the queue and writes the messages permanently to an Azure Storage table.</span></span>

1. <span data-ttu-id="54029-149">Klik op **Nieuwe functie** > **QueueTrigger-CSharp**.</span><span class="sxs-lookup"><span data-stu-id="54029-149">Click **New Function** > **QueueTrigger-CSharp**.</span></span> 
 
2. <span data-ttu-id="54029-150">Geef de functie de naam `FunctionsBindingsDemo2`, voer **functions-bindings** in het veld **Wachtrijnaam** in, selecteer een bestaand opslagaccount of maak een nieuwe, en klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="54029-150">Name the function `FunctionsBindingsDemo2`, enter **functions-bindings** in the **Queue name** field, select an existing storage account or create one, and then click **Create**.</span></span>

    ![Een timerfunctie voor de uitvoerwachtrij toevoegen](./media/functions-create-an-azure-connected-function/function-demo2-new-function.png) 

3. <span data-ttu-id="54029-152">(Optioneel) U kunt controleren of de nieuwe functie werkt door de nieuwe wachtrij zoals eerder uitgelegd in Opslagverkenner te bekijken.</span><span class="sxs-lookup"><span data-stu-id="54029-152">(Optional) You can verify that the new function works by viewing the new queue in Storage Explorer as before.</span></span> <span data-ttu-id="54029-153">U kunt ook Cloud Explorer gebruiken in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54029-153">You can also use Cloud Explorer in Visual Studio.</span></span>  

4. <span data-ttu-id="54029-154">(Optioneel) Vernieuw de wachtrij **functions-bindings** en kijk of er items zijn verwijderd uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="54029-154">(Optional) Refresh the **functions-bindings** queue and notice that items have been removed from the queue.</span></span> <span data-ttu-id="54029-155">De verwijdering doet zich voor omdat de functie als een invoeractivering is gebonden aan de wachtrij **functions-bindings** en de functie de wachtrij leest.</span><span class="sxs-lookup"><span data-stu-id="54029-155">The removal occurs because the function is bound to the **functions-bindings** queue as an input trigger and the function reads the queue.</span></span> 
 
## <a name="add-a-table-output-binding"></a><span data-ttu-id="54029-156">Een uitvoerverbinding voor de tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="54029-156">Add a table output binding</span></span>

1. <span data-ttu-id="54029-157">Klik in FunctionsBindingsDemo2 op **Integreren** > **Nieuwe uitvoer** > **Azure Table Storage** > **Selecteren**.</span><span class="sxs-lookup"><span data-stu-id="54029-157">In FunctionsBindingsDemo2, click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

    ![Een binding aan een Azure Storage-tabel toevoegen](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab.png) 

2. <span data-ttu-id="54029-159">Voer `functionbindings` in voor **Tabelnaam** en `myTable` voor **Naam van de tabelparameter**, kies een **Opslagaccountverbinding** of maak een nieuwe, en klik vervolgens op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="54029-159">Enter `functionbindings` for **Table name** and `myTable` for **Table parameter name**, choose a **Storage account connection** or create a new one, and then click **Save**.</span></span>

    ![De binding van de Storage-tabel configureren](./media/functions-create-an-azure-connected-function/functionsbindingsdemo2-integrate-tab2.png)
   
3. <span data-ttu-id="54029-161">Vervang in het tabblad **Ontwikkelen** de bestaande functiecode door het volgende:</span><span class="sxs-lookup"><span data-stu-id="54029-161">In the **Develop** tab, replace the existing function code with the following:</span></span>
   
    ```cs
    
    using System;
    
    public static void Run(QItem myQueueItem, ICollector<TableItem> myTable, TraceWriter log)
    {    
        TableItem myItem = new TableItem
        {
            PartitionKey = "key",
            RowKey = Guid.NewGuid().ToString(),
            Time = DateTime.Now.ToString("hh.mm.ss.ffffff"),
            Msg = myQueueItem.Msg,
            OriginalTime = myQueueItem.Time    
        };
        
        // Add the item to the table binding collection.
        myTable.Add(myItem);
    
        log.Verbose($"C# Queue trigger function processed: {myItem.RowKey} | {myItem.Msg} | {myItem.Time}");
    }
    
    public class TableItem
    {
        public string PartitionKey {get; set;}
        public string RowKey {get; set;}
        public string Time {get; set;}
        public string Msg {get; set;}
        public string OriginalTime {get; set;}
    }
    
    public class QItem
    {
        public string Msg { get; set;}
        public string Time { get; set;}
    }
    ```
    <span data-ttu-id="54029-162">De klasse **TableItem** vertegenwoordigt een rij in de opslagtabel. U voegt het item toe aan de verzameling `myTable` van **TableItem**-objecten.</span><span class="sxs-lookup"><span data-stu-id="54029-162">The **TableItem** class represents a row in the storage table, and you add the item to the `myTable` collection of **TableItem** objects.</span></span> <span data-ttu-id="54029-163">Stel de eigenschappen **PartitionKey** en **RowKey** in om in de tabel te kunnen invoegen.</span><span class="sxs-lookup"><span data-stu-id="54029-163">You must set the **PartitionKey** and **RowKey** properties to be able to insert into the table.</span></span>

4. <span data-ttu-id="54029-164">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="54029-164">Click **Save**.</span></span>  <span data-ttu-id="54029-165">Ten slotte kunt u controleren of de functie werkt door de tabel te bekijken in Opslagverkenner of Cloud Explorer van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54029-165">Finally, you can verify the function works by viewing the table in Storage explorer or Visual Studio Cloud Explorer.</span></span>

5. <span data-ttu-id="54029-166">(Optioneel) Vouw in uw opslagaccount in Opslagverkenner **Tabellen** > **functionsbindings** uit en controleer of er rijen worden toegevoegd aan de tabel.</span><span class="sxs-lookup"><span data-stu-id="54029-166">(Optional) In your storage account in Storage Explorer, expand **Tables** > **functionsbindings** and verify that rows are added to the table.</span></span> <span data-ttu-id="54029-167">U kunt hetzelfde doen met Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54029-167">You can do the same in Cloud Explorer in Visual Studio.</span></span>

    ![Weergave van de rijen in de tabel](./media/functions-create-an-azure-connected-function/functionsbindings-azure-storage-explorer2.png)

    <span data-ttu-id="54029-169">Als de tabel niet bestaat of leeg is, is er waarschijnlijk een probleem met uw functiebinding of code.</span><span class="sxs-lookup"><span data-stu-id="54029-169">If the table does not exist or is empty, there is most likely a problem with your function binding or code.</span></span> 
 
[!INCLUDE [More binding information](../../includes/functions-bindings-next-steps.md)]

## <a name="next-steps"></a><span data-ttu-id="54029-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54029-170">Next steps</span></span>
<span data-ttu-id="54029-171">Raadpleeg de volgende onderwerpen voor meer informatie over Azure Functions:</span><span class="sxs-lookup"><span data-stu-id="54029-171">For more information about Azure Functions, see the following topics:</span></span>

* [<span data-ttu-id="54029-172">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="54029-172">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="54029-173">Naslaginformatie voor programmeurs over het coderen van functies en het definiëren van triggers en bindingen.</span><span class="sxs-lookup"><span data-stu-id="54029-173">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="54029-174">Azure Functions testen</span><span class="sxs-lookup"><span data-stu-id="54029-174">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="54029-175">Beschrijft de verschillende hulpprogramma’s en technieken voor het testen van uw functies.</span><span class="sxs-lookup"><span data-stu-id="54029-175">Describes various tools and techniques for testing your functions.</span></span>
* [<span data-ttu-id="54029-176">Azure Functions schalen</span><span class="sxs-lookup"><span data-stu-id="54029-176">How to scale Azure Functions</span></span>](functions-scale.md)  
  <span data-ttu-id="54029-177">Beschrijft de serviceabonnementen die beschikbaar zijn voor Azure Functions, zoals het hostingabonnement Consumption, en helpt u bij het kiezen van het juiste abonnement.</span><span class="sxs-lookup"><span data-stu-id="54029-177">Discusses service plans available with Azure Functions, including the Consumption hosting plan, and how to choose the right plan.</span></span> 

[!INCLUDE [Getting help note](../../includes/functions-get-help.md)]

