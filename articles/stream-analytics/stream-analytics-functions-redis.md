---
title: aaaStream Analytics realtime verwerking voor Azure Functions | Microsoft Docs
description: Meer informatie over hoe een Azure-functie toouse verbonden met een Service Bus-wachtrij toopopulate een Azure Redis-Cache van Hallo-uitvoer van een Stream Analytics-taak.
keywords: gegevensstroom, redis-cache, service bus-wachtrij
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="87e22-104">Hoe toostore gegevens uit Azure Stream Analytics in een Azure Redis-Cache met behulp van Azure Functions</span><span class="sxs-lookup"><span data-stu-id="87e22-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="87e22-105">Azure Stream Analytics kunt u snel ontwikkelen en implementeren van oplossingen voor goedkope toogain realtime-inzichten van apparaten, sensoren, infrastructuur en -toepassingen of elke andere stroom van gegevens.</span><span class="sxs-lookup"><span data-stu-id="87e22-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="87e22-106">Hiermee kunt verschillende gebruiksvoorbeelden zoals realtime management en opdracht en controle, fraude te detecteren, verbonden auto's en nog veel meer.</span><span class="sxs-lookup"><span data-stu-id="87e22-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="87e22-107">In veel dergelijke scenario's kunt u toostore gegevens in Azure Stream Analytics output in een gedistribueerde gegevensarchief, zoals een Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="87e22-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="87e22-108">Stel dat u deel uitmaken van een bedrijf telecommunicatie.</span><span class="sxs-lookup"><span data-stu-id="87e22-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="87e22-109">U probeert toodetect SIM fraude waarbij meerdere aanroepen afkomstig zijn van dezelfde identiteit hello, Hallo op dezelfde tijd, maar in verschillende geografische locaties.</span><span class="sxs-lookup"><span data-stu-id="87e22-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="87e22-110">U wordt opgedragen alle Hallo mogelijke frauduleuze telefoongesprekken opslaan in een Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="87e22-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="87e22-111">In deze blog bieden we hulp bij hoe kunt u eenvoudig uw taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="87e22-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="87e22-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="87e22-112">Prerequisites</span></span>
<span data-ttu-id="87e22-113">Volledige Hallo [realtime-Fraudedetectie] [ fraud-detection] procedure voor ASA</span><span class="sxs-lookup"><span data-stu-id="87e22-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="87e22-114">Overzicht van de architectuur</span><span class="sxs-lookup"><span data-stu-id="87e22-114">Architecture Overview</span></span>
![Schermopname van architectuur](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="87e22-116">Zoals in Hallo voorgaande afbeelding wordt weergegeven, kunt u Stream Analytics streaming invoergegevens toobe opgevraagd en tooan uitvoer verzonden.</span><span class="sxs-lookup"><span data-stu-id="87e22-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="87e22-117">Op basis van de uitvoer hello, kan Azure Functions vervolgens resulteren in een soort gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="87e22-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="87e22-118">In deze blog er zich richten op Hallo Azure Functions deel van deze pipeline of meer specifiek Hallo activering van een gebeurtenis die frauduleuze-gegevens in Hallo-cache opslaat.</span><span class="sxs-lookup"><span data-stu-id="87e22-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="87e22-119">Na het voltooien van Hallo [realtime-Fraudedetectie] [ fraud-detection] zelfstudie hebt u een invoer (een event hub), een query en uitvoer (blobopslag) al is geconfigureerd en actief.</span><span class="sxs-lookup"><span data-stu-id="87e22-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="87e22-120">In deze blog wijzigen we Hallo uitvoer toouse een Service Bus-wachtrij in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="87e22-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="87e22-121">Daarna we verbinding maken met een Azure-functie toothis wachtrij.</span><span class="sxs-lookup"><span data-stu-id="87e22-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="87e22-122">Maken en koppelen van een Service Bus-wachtrij-uitvoer</span><span class="sxs-lookup"><span data-stu-id="87e22-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="87e22-123">een Service Bus-wachtrij toocreate stappen 1 en 2 van Hallo .NET-sectie in [aan de slag met Service Bus-wachtrijen][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="87e22-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="87e22-124">Nu gaan we verbinding Hallo wachtrij toohello Stream Analytics-taak die is gemaakt in Hallo eerdere fraude detectie procedure.</span><span class="sxs-lookup"><span data-stu-id="87e22-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="87e22-125">Ga in de Azure-portal hello, toohello **uitvoer** blade van uw project en selecteer **toevoegen** bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="87e22-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![Uitvoer toevoegen](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="87e22-127">Kies **Service Bus-wachtrij** als Hallo **Sink** en volg Hallo-instructies op het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="87e22-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="87e22-128">U hebt gemaakt of toochoose Hallo naamruimte Hallo Service Bus-wachtrij worden in [aan de slag met Service Bus-wachtrijen][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="87e22-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="87e22-129">Klik op Hallo 'juiste' wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="87e22-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="87e22-130">Geef Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="87e22-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="87e22-131">**Gebeurtenis serialisatiefunctie indeling**: JSON</span><span class="sxs-lookup"><span data-stu-id="87e22-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="87e22-132">**Codering**: UTF8</span><span class="sxs-lookup"><span data-stu-id="87e22-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="87e22-133">**INDELING**: regels gescheiden</span><span class="sxs-lookup"><span data-stu-id="87e22-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="87e22-134">Klik op Hallo **maken** tooadd knop deze bron- en tooverify dat Stream Analytics verbinding toohello storage-account maken kan.</span><span class="sxs-lookup"><span data-stu-id="87e22-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="87e22-135">In Hallo **Query** tabblad, de huidige query Hallo vervangen door de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="87e22-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="87e22-136">Vervang * [uw SERVICE BUS NAME] * met Hallo uitvoer naam die u in stap 3 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="87e22-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="87e22-137">Maak een Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="87e22-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="87e22-138">Maken van een Azure Redis-cache door de volgende sectie van de Hallo .NET in [hoe tooUse Azure Redis-Cache] [ use-rediscache] totdat Hallo sectie aangeroepen ***hello cacheclients configureren***.</span><span class="sxs-lookup"><span data-stu-id="87e22-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="87e22-139">Hierna kunt hebt u een nieuwe Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="87e22-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="87e22-140">Onder **alle instellingen**, selecteer **toegangssleutels** en noteer Hallo ***primaire verbindingsreeks***.</span><span class="sxs-lookup"><span data-stu-id="87e22-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![Schermopname van architectuur](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="87e22-142">Een Azure-functie maken</span><span class="sxs-lookup"><span data-stu-id="87e22-142">Create an Azure Function</span></span>
<span data-ttu-id="87e22-143">Ga als volgt [uw eerste Azure-functie maken] [ functions-getstarted] zelfstudie tooget de slag met Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="87e22-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="87e22-144">Als u al een Azure-functie zou u toouse, zoals vervolgens gaat u verder te[tooRedis Cache schrijven](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="87e22-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="87e22-145">Hallo-portal, selecteer App Services in de linkernavigatiebalk Hallo vervolgens klikt u op de website van uw Azure-functie app name tooget toohello van functie-app.</span><span class="sxs-lookup"><span data-stu-id="87e22-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="87e22-146">![Schermafbeelding van de lijst met de functie van de app services](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="87e22-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="87e22-147">Klik op **nieuwe functie > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="87e22-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="87e22-148">Voor Hallo volgende velden als volgt:</span><span class="sxs-lookup"><span data-stu-id="87e22-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="87e22-149">**Wachtrijnaam**: Hallo dezelfde naam als Hallo-naam die u hebt opgegeven tijdens het maken van de wachtrij Hallo in [aan de slag met Service Bus-wachtrijen] [ servicebus-getstarted] (niet Hallo naam van Hallo servicebus).</span><span class="sxs-lookup"><span data-stu-id="87e22-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="87e22-150">Zorg ervoor dat u Hallo wachtrij die is verbonden toohello uitvoer van de Stream Analytics gebruiken.</span><span class="sxs-lookup"><span data-stu-id="87e22-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="87e22-151">**Service Bus-verbinding**: Selecteer **een verbindingsreeks toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="87e22-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="87e22-152">toofind hello verbindingsreeks, Ga toohello klassieke portal, selecteer **Service Bus**, Hallo servicebus die u hebt gemaakt, en **VERBINDINGSGEGEVENS** Hallo onder welkomstscherm aan.</span><span class="sxs-lookup"><span data-stu-id="87e22-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="87e22-153">Zorg ervoor dat u zich op de belangrijkste welkomstscherm op deze pagina.</span><span class="sxs-lookup"><span data-stu-id="87e22-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="87e22-154">Kopieer en plak de verbindingsreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="87e22-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="87e22-155">De naam van een verbinding met gratis tooenter vertrouwen.</span><span class="sxs-lookup"><span data-stu-id="87e22-155">Feel free tooenter any connection name.</span></span>
     
       ![Schermopname van service bus-verbinding](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="87e22-157">**AccessRights**: kies **beheren**</span><span class="sxs-lookup"><span data-stu-id="87e22-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="87e22-158">Klik op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="87e22-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="87e22-159">Schrijven tooRedis Cache</span><span class="sxs-lookup"><span data-stu-id="87e22-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="87e22-160">Wij hebben nu een Azure-functie die van een Service Bus-wachtrij wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="87e22-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="87e22-161">Alles wat toodo blijft onze toowrite functie gebruiken deze gegevens toohello Redis-Cache is.</span><span class="sxs-lookup"><span data-stu-id="87e22-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="87e22-162">Selecteer de zojuist gemaakte **ServiceBusQueueTrigger**, en klik op **werken app-instellingen** op Hallo rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="87e22-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="87e22-163">Selecteer **Ga tooApp Service-instellingen > Instellingen > Toepassingsinstellingen**</span><span class="sxs-lookup"><span data-stu-id="87e22-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="87e22-164">In Hallo sectie Connection-tekenreeksen, maakt u een naam in Hallo **naam** sectie.</span><span class="sxs-lookup"><span data-stu-id="87e22-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="87e22-165">Primaire verbindingsreeks Hallo u in Hallo gevonden plakken **een Redis-Cache maken** stap naar Hallo **waarde** sectie.</span><span class="sxs-lookup"><span data-stu-id="87e22-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="87e22-166">Selecteer **aangepaste** aanduiding **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="87e22-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="87e22-167">Klik op **opslaan** Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="87e22-167">Click **Save** at hello top.</span></span>
   
    ![Schermopname van service bus-verbinding](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="87e22-169">Nu gaat u terug toohello App Service-instellingen en selecteer **Extra > App Service-Editor (Preview) > op > Ga**.</span><span class="sxs-lookup"><span data-stu-id="87e22-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Schermopname van service bus-verbinding](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="87e22-171">Maak een JSON-bestand met de naam in een editor naar keuze, **project.json** met Hallo volgen en sla het tooyour lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="87e22-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="87e22-172">Dit bestand niet uploaden naar de hoofdmap Hallo van de functie (geen WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="87e22-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="87e22-173">Er is een bestand met de naam **project.lock.json** automatisch wordt weergegeven, waarin wordt bevestigd dat Hallo Nuget pakketten 'StackExchange.Redis' en 'Newtonsoft.Json' zijn geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="87e22-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="87e22-174">In Hallo **run.csx** bestand, Hallo vooraf gegenereerde code vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="87e22-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="87e22-175">In de functie lazyConnection Hallo naam vervangen door "CONN ' Hallo-naam die u hebt gemaakt in stap 2 van **gegevens opslaan in de Redis-cache Hallo**.</span><span class="sxs-lookup"><span data-stu-id="87e22-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="87e22-176">Hallo Stream Analytics-taak starten</span><span class="sxs-lookup"><span data-stu-id="87e22-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="87e22-177">Hallo telcodatagen.exe toepassing starten.</span><span class="sxs-lookup"><span data-stu-id="87e22-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="87e22-178">Hallo-gebruik is als volgt:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="87e22-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="87e22-179">Hallo Stream Analytics-taak blade in Hallo-portal klikt u op **Start** bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="87e22-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![Schermafbeelding van de taak is gestart](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="87e22-181">In Hallo **starttaak** blade die wordt weergegeven, selecteer **nu** en klik vervolgens op Hallo **Start** knop Hallo onder welkomstscherm aan.</span><span class="sxs-lookup"><span data-stu-id="87e22-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="87e22-182">Hallo taakstatus verandert tooStarting en na enige tijd wijzigingen tooRunning.</span><span class="sxs-lookup"><span data-stu-id="87e22-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![Schermopname van start tijd Functieselectie](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="87e22-184">Oplossing en de resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="87e22-184">Run solution and check results</span></span>
<span data-ttu-id="87e22-185">Ga terug tooyour **ServiceBusQueueTrigger** pagina u ziet nu aanmelden instructies.</span><span class="sxs-lookup"><span data-stu-id="87e22-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="87e22-186">Deze logboeken weergeven die u hebt gekregen iets Hallo Service Bus-wachtrij plaatsen in Hallo-database, en het Hallo-tijd gebruikt als Hallo sleutel opgehaald.</span><span class="sxs-lookup"><span data-stu-id="87e22-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="87e22-187">tooverify dat uw gegevens in uw Redis-cache, gaat u tooyour Redis-cache-pagina in de nieuwe portal hello (zoals weergegeven in de voorgaande Hallo [maken van een Azure Redis-Cache](#Create-an-Azure-Redis-Cache) stap) en selecteer de Console.</span><span class="sxs-lookup"><span data-stu-id="87e22-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="87e22-188">Nu kunt u schrijven Redis opdrachten tooconfirm gegevens zich in feite in Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="87e22-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Schermopname van Redis-Console](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="87e22-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87e22-190">Next steps</span></span>
<span data-ttu-id="87e22-191">We zijn blij Hallo nieuwe dingen Azure Functions en we hopen dat u dat dit nieuwe mogelijkheden voor u ontgrendelt Stream analytics samen kunt doen.</span><span class="sxs-lookup"><span data-stu-id="87e22-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="87e22-192">Als u feedback wilt naast hebt, kunt u gratis toouse hello [Azure UserVoice-site](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="87e22-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="87e22-193">Als u nieuwe Microsoft Azure, we nodigen u tootry deze door zich aanmelden voor een [gratis proefaccount voor Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87e22-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="87e22-194">Als u nieuwe tooStream Analytics zijn, en vervolgens we u uit te nodigen[maken van uw eerste Stream Analytics-taak](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="87e22-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="87e22-195">Als u een moet helpen of vragen hebt, post een bericht op [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) of [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span><span class="sxs-lookup"><span data-stu-id="87e22-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="87e22-196">U ziet ook Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="87e22-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="87e22-197">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="87e22-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="87e22-198">Azure Functions C# referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="87e22-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="87e22-199">Azure Functions F # referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="87e22-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="87e22-200">Azure Functions NodeJS-referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="87e22-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="87e22-201">Azure Functions-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="87e22-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="87e22-202">Hoe toomonitor Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="87e22-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="87e22-203">toostay op de hoogte van alle Hallo laatste nieuws en -functies, volg [ @AzureStreaming ](https://twitter.com/AzureStreaming) op Twitter.</span><span class="sxs-lookup"><span data-stu-id="87e22-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
