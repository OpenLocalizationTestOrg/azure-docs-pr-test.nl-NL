---
title: aaaThe Azure IoT-device SDK voor C | Microsoft Docs
description: Aan de slag met hello Azure IoT-device SDK voor C en meer informatie over hoe toocreate apps op apparaten die communiceren met een IoT-hub.
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="929c3-103">Azure IoT-apparaat SDK voor C</span><span class="sxs-lookup"><span data-stu-id="929c3-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="929c3-104">Hallo **Azure IoT-device SDK** is een set van bibliotheken ontworpen toosimplify Hallo proces voor het verzenden van berichten tooand die berichten ontvangt van Hallo **Azure IoT Hub** service.</span><span class="sxs-lookup"><span data-stu-id="929c3-104">hello **Azure IoT device SDK** is a set of libraries designed toosimplify hello process of sending messages tooand receiving messages from hello **Azure IoT Hub** service.</span></span> <span data-ttu-id="929c3-105">Er zijn verschillende variaties Hallo SDK, elke die gericht is op een specifiek platform, maar dit artikel wordt beschreven Hallo **Azure IoT-device SDK voor C**.</span><span class="sxs-lookup"><span data-stu-id="929c3-105">There are different variations of hello SDK, each targeting a specific platform, but this article describes hello **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="929c3-106">Hello Azure IoT-device SDK voor C is geschreven in C ANSI (C99) toomaximize draagbaarheid.</span><span class="sxs-lookup"><span data-stu-id="929c3-106">hello Azure IoT device SDK for C is written in ANSI C (C99) toomaximize portability.</span></span> <span data-ttu-id="929c3-107">Deze functie stelt Hallo bibliotheken geschikt toooperate op meerdere platforms en apparaten, vooral wanneer het minimaliseren van schijf- en geheugengebruik is een prioriteit.</span><span class="sxs-lookup"><span data-stu-id="929c3-107">This feature makes hello libraries well-suited toooperate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="929c3-108">Er zijn een breed scala aan op welke Hallo SDK is getest platforms (Zie Hallo [Azure gecertificeerd voor IoT-apparaat catalogus](https://catalog.azureiotsuite.com/) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="929c3-108">There are a broad range of platforms on which hello SDK has been tested (see hello [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="929c3-109">Hoewel dit artikel scenario's van voorbeeldcode uitgevoerd op Windows-platform hello bevat, is Hallo-code die wordt beschreven in dit artikel is identiek voor Hallo bereik van de ondersteunde platforms.</span><span class="sxs-lookup"><span data-stu-id="929c3-109">Although this article includes walkthroughs of sample code running on hello Windows platform, hello code described in this article is identical across hello range of supported platforms.</span></span>

<span data-ttu-id="929c3-110">In dit artikel vindt u toohello architectuur van hello Azure IoT-device SDK voor C. Dit laat zien hoe tooinitialize Hallo apparaatbibliotheek gegevens tooIoT Hub te verzenden en berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="929c3-110">This article introduces you toohello architecture of hello Azure IoT device SDK for C. It demonstrates how tooinitialize hello device library, send data tooIoT Hub, and receive messages from it.</span></span> <span data-ttu-id="929c3-111">Hallo-informatie in dit artikel moet voldoende tooget gestart met behulp van Hallo SDK, maar bevat ook aanwijzers tooadditional informatie over Hallo-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="929c3-111">hello information in this article should be enough tooget started using hello SDK, but also provides pointers tooadditional information about hello libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="929c3-112">SDK-architectuur</span><span class="sxs-lookup"><span data-stu-id="929c3-112">SDK architecture</span></span>

<span data-ttu-id="929c3-113">U vindt Hallo [ **Azure IoT-device SDK voor C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub-opslagplaats en de weergave details van Hallo API in Hallo [C-API-referentiemateriaal](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="929c3-113">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="929c3-114">meest recente versie van bibliotheken Hallo Hallo vindt u in Hallo **master** branche van Hallo opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="929c3-114">hello latest version of hello libraries can be found in hello **master** branch of hello repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="929c3-115">Hallo core Hallo SDK wordt Hallo **iothub\_client** map waarin het Hallo-implementatie van Hallo API laag in Hallo SDK: Hallo **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="929c3-115">hello core implementation of hello SDK is in hello **iothub\_client** folder that contains hello implementation of hello lowest API layer in hello SDK: hello **IoTHubClient** library.</span></span> <span data-ttu-id="929c3-116">Hallo **IoTHubClient** bibliotheek bevat API's implementeren onbewerkte messaging voor berichten tooIoT Hub verzenden en ontvangen van berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="929c3-116">hello **IoTHubClient** library contains APIs implementing raw messaging for sending messages tooIoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="929c3-117">Wanneer u deze bibliotheek, bent u verantwoordelijk voor het implementeren van bericht serialisatie, maar andere details voor de communicatie met IoT Hub worden afgehandeld.</span><span class="sxs-lookup"><span data-stu-id="929c3-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="929c3-118">Hallo **serialisatiefunctie** map hulpfuncties en voorbeelden waarin u kunt hoe gegevens zien voor het verzenden van Iothub met behulp van tooAzure tooserialize Hallo-clientbibliotheek bevat.</span><span class="sxs-lookup"><span data-stu-id="929c3-118">hello **serializer** folder contains helper functions and samples that show you how tooserialize data before sending tooAzure IoT Hub using hello client library.</span></span> <span data-ttu-id="929c3-119">Hallo-gebruik van Hallo serialisatiefunctie is niet verplicht en uw gemak is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="929c3-119">hello use of hello serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="929c3-120">Hallo toouse **serialisatiefunctie** bibliotheek, definieert u een model waarmee hello gegevens toosend tooIoT Hub en Hallo-berichten tooreceive hieruit verwacht.</span><span class="sxs-lookup"><span data-stu-id="929c3-120">toouse hello **serializer** library, you define a model that specifies hello data toosend tooIoT Hub and hello messages you expect tooreceive from it.</span></span> <span data-ttu-id="929c3-121">Zodra het Hallo-model is gedefinieerd, Hallo SDK biedt u een API-gebied waarmee u tooeasily werk met apparaat-naar-cloud en cloud-naar-apparaatberichten zonder dat u Hallo serialisatie details.</span><span class="sxs-lookup"><span data-stu-id="929c3-121">Once hello model is defined, hello SDK provides you with an API surface that enables you tooeasily work with device-to-cloud and cloud-to-device messages without worrying about hello serialization details.</span></span> <span data-ttu-id="929c3-122">Hallo-bibliotheek is afhankelijk van andere open-source bibliotheken die implementeren met behulp van protocollen zoals MQTT en AMQP transport.</span><span class="sxs-lookup"><span data-stu-id="929c3-122">hello library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="929c3-123">Hallo **IoTHubClient** bibliotheek, is afhankelijk van andere open-source bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="929c3-123">hello **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="929c3-124">Hallo [Azure C gedeeld hulpprogramma](https://github.com/Azure/azure-c-shared-utility) bibliotheek, waardoor algemene functionaliteit voor basistaken (zoals tekenreeksen, bewerkingen en i/o) over diverse Azure-gerelateerde C SDK's nodig.</span><span class="sxs-lookup"><span data-stu-id="929c3-124">hello [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="929c3-125">Hallo [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) bibliotheek die een client-side '-implementatie van AMQP die zijn geoptimaliseerd voor resource beperkte apparaten.</span><span class="sxs-lookup"><span data-stu-id="929c3-125">hello [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="929c3-126">Hallo [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) bibliotheek is een algemene bibliotheek implementatie Hallo MQTT-protocol en geoptimaliseerd voor resource beperkte apparaten.</span><span class="sxs-lookup"><span data-stu-id="929c3-126">hello [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing hello MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="929c3-127">Gebruik van deze bibliotheken is eenvoudiger toounderstand door te kijken voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="929c3-127">Use of these libraries is easier toounderstand by looking at example code.</span></span> <span data-ttu-id="929c3-128">Hallo uit te voeren doorlopen diverse Hallo voorbeeldtoepassingen die zijn opgenomen in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="929c3-128">hello following sections walk you through several of hello sample applications that are included in hello SDK.</span></span> <span data-ttu-id="929c3-129">In dit scenario geeft u een goede voor Hallo kunt u verschillende mogelijkheden van Hallo architectuur lagen van Hallo SDK en een inleiding toohow Hallo-API's werken.</span><span class="sxs-lookup"><span data-stu-id="929c3-129">This walkthrough should give you a good feel for hello various capabilities of hello architectural layers of hello SDK and an introduction toohow hello APIs work.</span></span>

## <a name="before-you-run-hello-samples"></a><span data-ttu-id="929c3-130">Voordat u voorbeelden van Hallo uitvoeren</span><span class="sxs-lookup"><span data-stu-id="929c3-130">Before you run hello samples</span></span>

<span data-ttu-id="929c3-131">Voordat u Hallo voorbeelden in hello Azure IoT-device SDK voor C uitvoeren kunt, moet u [geen exemplaar maken van Hallo service IoT Hub](iot-hub-create-through-portal.md) in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="929c3-131">Before you can run hello samples in hello Azure IoT device SDK for C, you must [create an instance of hello IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="929c3-132">Voltooi Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="929c3-132">Then complete hello following tasks:</span></span>

* <span data-ttu-id="929c3-133">Uw ontwikkelomgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="929c3-133">Prepare your development environment</span></span>
* <span data-ttu-id="929c3-134">Apparaat-referenties ophalen.</span><span class="sxs-lookup"><span data-stu-id="929c3-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="929c3-135">Uw ontwikkelomgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="929c3-135">Prepare your development environment</span></span>

<span data-ttu-id="929c3-136">Pakketten zijn beschikbaar voor algemene platforms (zoals NuGet voor Windows of apt_get voor Debian en Ubuntu) en Hallo voorbeelden gebruiken deze pakketten indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="929c3-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and hello samples use these packages when available.</span></span> <span data-ttu-id="929c3-137">In sommige gevallen moet u toocompile Hallo SDK voor of op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="929c3-137">In some cases, you need toocompile hello SDK for or on your device.</span></span> <span data-ttu-id="929c3-138">Als u toocompile Hallo SDK moet, Zie [uw ontwikkelingsomgeving voorbereiden](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in Hallo GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="929c3-138">If you need toocompile hello SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in hello GitHub repository.</span></span>

<span data-ttu-id="929c3-139">tooobtain hello toepassing voorbeeldcode, download een exemplaar van Hallo SDK vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="929c3-139">tooobtain hello sample application code, download a copy of hello SDK from GitHub.</span></span> <span data-ttu-id="929c3-140">Uw exemplaar van Hallo bron ophalen van Hallo **master** vertakking van Hallo [GitHub-opslagplaats](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="929c3-140">Get your copy of hello source from hello **master** branch of hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-hello-device-credentials"></a><span data-ttu-id="929c3-141">Hallo apparaat referenties ophalen</span><span class="sxs-lookup"><span data-stu-id="929c3-141">Obtain hello device credentials</span></span>

<span data-ttu-id="929c3-142">Nu dat u de voorbeeldcode Hallo hebt, is de volgende dingen toodo hello tooget een set referenties apparaat.</span><span class="sxs-lookup"><span data-stu-id="929c3-142">Now that you have hello sample source code, hello next thing toodo is tooget a set of device credentials.</span></span> <span data-ttu-id="929c3-143">Voor een apparaat toobe kunnen tooaccess een IoT-hub, moet u eerst Hallo apparaat toohello id-register IoT Hub toevoegen.</span><span class="sxs-lookup"><span data-stu-id="929c3-143">For a device toobe able tooaccess an IoT hub, you must first add hello device toohello IoT Hub identity registry.</span></span> <span data-ttu-id="929c3-144">Als u uw apparaat toevoegt, krijgt u een set referenties voor apparaten die u nodig hebt voor Hallo apparaat toobe kunnen tooconnect toohello iothub.</span><span class="sxs-lookup"><span data-stu-id="929c3-144">When you add your device, you get a set of device credentials that you need for hello device toobe able tooconnect toohello IoT hub.</span></span> <span data-ttu-id="929c3-145">Hallo-voorbeeldtoepassingen die is beschreven in de volgende sectie Hallo verwachten deze referenties in Hallo vorm van een **apparaat verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="929c3-145">hello sample applications discussed in hello next section expect these credentials in hello form of a **device connection string**.</span></span>

<span data-ttu-id="929c3-146">Er zijn verschillende open-source hulpprogramma's voor toohelp beheren van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="929c3-146">There are several open source tools toohelp you manage your IoT hub.</span></span>

* <span data-ttu-id="929c3-147">Een Windows-toepassing aangeroepen [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="929c3-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="929c3-148">Een node.js platformoverschrijdende CLI-hulpprogramma aangeroepen [iothub explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="929c3-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="929c3-149">Deze zelfstudie wordt een grafische Hallo *apparaat explorer* hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="929c3-149">This tutorial uses hello graphical *device explorer* tool.</span></span> <span data-ttu-id="929c3-150">U kunt ook Hallo *iothub explorer* hulpprogramma als u liever toouse een CLI-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="929c3-150">You can also use hello *iothub-explorer* tool if you prefer toouse a CLI tool.</span></span>

<span data-ttu-id="929c3-151">Hallo apparaat explorer hulpprogramma gebruikt hello Azure IoT service bibliotheken tooperform diverse functies op IoT Hub, inclusief het toevoegen van apparaten.</span><span class="sxs-lookup"><span data-stu-id="929c3-151">hello device explorer tool uses hello Azure IoT service libraries tooperform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="929c3-152">Als u Hallo apparaat explorer hulpprogramma tooadd een apparaat gebruikt, krijgt u een verbindingsreeks voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="929c3-152">If you use hello device explorer tool tooadd a device, you get a connection string for your device.</span></span> <span data-ttu-id="929c3-153">U moet deze verbinding tekenreeks toorun Hallo voorbeeldtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="929c3-153">You need this connection string toorun hello sample applications.</span></span>

<span data-ttu-id="929c3-154">Als u niet bekend met Hallo apparaat explorer hulpprogramma bent, Hallo na procedure beschrijft hoe toouse het tooadd een apparaat en een apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="929c3-154">If you're not familiar with hello device explorer tool, hello following procedure describes how toouse it tooadd a device and obtain a device connection string.</span></span>

<span data-ttu-id="929c3-155">hulpprogramma voor tooinstall Hallo apparaat explorer, Zie [hoe toouse apparaat Explorer Hallo voor IoT Hub-apparaten](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="929c3-155">tooinstall hello device explorer tool, see [How toouse hello Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="929c3-156">Wanneer u Hallo-programma uitvoert, ziet u deze interface:</span><span class="sxs-lookup"><span data-stu-id="929c3-156">When you run hello program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="929c3-157">Voer uw **IoT Hub-verbindingsreeks** in Hallo eerst veld en klikt u op **Update**.</span><span class="sxs-lookup"><span data-stu-id="929c3-157">Enter your **IoT Hub Connection String** in hello first field and click **Update**.</span></span> <span data-ttu-id="929c3-158">Deze stap Hallo hulpprogramma zodanig geconfigureerd dat met IoT Hub communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="929c3-158">This step configures hello tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="929c3-159">Wanneer Hallo IoT Hub-verbindingsreeks is geconfigureerd, klikt u op Hallo **Management** tabblad:</span><span class="sxs-lookup"><span data-stu-id="929c3-159">When hello IoT Hub connection string is configured, click hello **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="929c3-160">Dit tabblad is waar het beheer van Hallo-apparaten die zijn geregistreerd in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="929c3-160">This tab is where you manage hello devices registered in your IoT hub.</span></span>

<span data-ttu-id="929c3-161">U maakt een apparaat door te klikken op Hallo **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="929c3-161">You create a device by clicking hello **Create** button.</span></span> <span data-ttu-id="929c3-162">Er wordt een dialoogvenster weergegeven met een reeks vooraf ingestelde sleutels (primair en secundair).</span><span class="sxs-lookup"><span data-stu-id="929c3-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="929c3-163">Voer een **apparaat-ID** en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="929c3-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="929c3-164">Wanneer het Hallo-apparaat is gemaakt, weergeven Hallo apparaten updates met alle Hallo ingeschreven apparaten, met inbegrip van Hallo die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="929c3-164">When hello device is created, hello Devices list updates with all hello registered devices, including hello one you just created.</span></span> <span data-ttu-id="929c3-165">Als u met de rechtermuisknop op het nieuwe apparaat, ziet u dit menu:</span><span class="sxs-lookup"><span data-stu-id="929c3-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="929c3-166">Als u ervoor kiest **Kopieer de verbindingsreeks voor geselecteerde apparaat**, Hallo apparaat-verbindingsreeks is gekopieerde toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="929c3-166">If you choose **Copy connection string for selected device**, hello device connection string is copied toohello clipboard.</span></span> <span data-ttu-id="929c3-167">Houd een kopie van de verbindingsreeks Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="929c3-167">Keep a copy of hello device connection string.</span></span> <span data-ttu-id="929c3-168">U moet bij het uitvoeren van de voorbeeldtoepassingen Hallo beschreven in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="929c3-168">You need it when running hello sample applications described in hello following sections.</span></span>

<span data-ttu-id="929c3-169">Wanneer u Hallo bovenstaande stappen hebt voltooid, bent u klaar toostart waarop bepaalde code wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="929c3-169">When you've completed hello steps above, you're ready toostart running some code.</span></span> <span data-ttu-id="929c3-170">Beide voorbeelden hebben een constante Hallo Hallo belangrijkste bron-bestand waarmee u een verbindingsreeks tooenter bovenaan in.</span><span class="sxs-lookup"><span data-stu-id="929c3-170">Both samples have a constant at hello top of hello main source file that enables you tooenter a connection string.</span></span> <span data-ttu-id="929c3-171">Bijvoorbeeld Hallo bijbehorende regel van Hallo **iothub\_client\_voorbeeld\_mqtt** toepassing wordt weergegeven als volgt.</span><span class="sxs-lookup"><span data-stu-id="929c3-171">For example, hello corresponding line from hello **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a><span data-ttu-id="929c3-172">Hallo IoTHubClient library gebruiken</span><span class="sxs-lookup"><span data-stu-id="929c3-172">Use hello IoTHubClient library</span></span>

<span data-ttu-id="929c3-173">Binnen Hallo **iothub\_client** map in Hallo [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) -opslagplaats, er is een **voorbeelden** map waarin een toepassing met de naam **iothub\_client\_voorbeeld\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="929c3-173">Within hello **iothub\_client** folder in hello [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="929c3-174">versie van Windows Hello Hallo **iothub\_client\_voorbeeld\_mqtt** toepassing bevat Hallo Visual Studio-oplossing te volgen:</span><span class="sxs-lookup"><span data-stu-id="929c3-174">hello Windows version of hello **iothub\_client\_sample\_mqtt** application includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="929c3-175">Als u dit project in Visual Studio 2017 openen, Hallo prompts tooretarget Hallo project toohello meest recente versie accepteren.</span><span class="sxs-lookup"><span data-stu-id="929c3-175">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="929c3-176">Deze oplossing bevat een project.</span><span class="sxs-lookup"><span data-stu-id="929c3-176">This solution contains a single project.</span></span> <span data-ttu-id="929c3-177">Er zijn vier NuGet-pakketten in deze oplossing is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="929c3-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="929c3-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="929c3-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="929c3-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="929c3-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="929c3-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="929c3-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="929c3-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="929c3-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="929c3-182">Moet u altijd Hallo **Microsoft.Azure.C.SharedUtility** wanneer u met Hallo SDK werkt-pakket.</span><span class="sxs-lookup"><span data-stu-id="929c3-182">You always need hello **Microsoft.Azure.C.SharedUtility** package when you are working with hello SDK.</span></span> <span data-ttu-id="929c3-183">Dit voorbeeld Hallo MQTT protocol gebruikt, moet u daarom Hallo opnemen **Microsoft.Azure.umqtt** en **Microsoft.Azure.IoTHub.MqttTransport** pakketten (Er zijn equivalent pakketten voor AMQP en HTTP ).</span><span class="sxs-lookup"><span data-stu-id="929c3-183">This sample uses hello MQTT protocol, therefore you must include hello **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="929c3-184">Omdat Hallo-voorbeeld Hallo gebruikt **IoTHubClient** bibliotheek, moet u ook Hallo **Microsoft.Azure.IoTHub.IoTHubClient** -pakket in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="929c3-184">Because hello sample uses hello **IoTHubClient** library, you must also include hello **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="929c3-185">U vindt Hallo-implementatie voor de voorbeeldtoepassing Hallo in Hallo **iothub\_client\_voorbeeld\_mqtt.c** bronbestand.</span><span class="sxs-lookup"><span data-stu-id="929c3-185">You can find hello implementation for hello sample application in hello **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="929c3-186">Hallo volgende stappen wordt gebruikt in dit voorbeeld toepassing toowalk u via wat is vereist toouse hello **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="929c3-186">hello following steps use this sample application toowalk you through what's required toouse hello **IoTHubClient** library.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="929c3-187">Hallo-bibliotheek initialiseren</span><span class="sxs-lookup"><span data-stu-id="929c3-187">Initialize hello library</span></span>

> [!NOTE]
> <span data-ttu-id="929c3-188">Voordat u begint te werken met Hallo-bibliotheken, moet u mogelijk tooperform initialisaties platform-specifieke.</span><span class="sxs-lookup"><span data-stu-id="929c3-188">Before you start working with hello libraries, you may need tooperform some platform-specific initialization.</span></span> <span data-ttu-id="929c3-189">Als u van plan toouse AMQP Linux bent moet u bijvoorbeeld Hallo OpenSSL bibliotheek initialiseren.</span><span class="sxs-lookup"><span data-stu-id="929c3-189">For example, if you plan toouse AMQP on Linux you must initialize hello OpenSSL library.</span></span> <span data-ttu-id="929c3-190">voorbeelden in Hallo Hallo [GitHub-opslagplaats](https://github.com/Azure/azure-iot-sdk-c) Hallo hulpprogrammafunctie aanroepen **platform\_init** wanneer Hallo van client wordt gestart en roep Hallo **platform\_deinit**  functie voordat u afsluit.</span><span class="sxs-lookup"><span data-stu-id="929c3-190">hello samples in hello [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call hello utility function **platform\_init** when hello client starts and call hello **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="929c3-191">Deze functies zijn gedefinieerd in Hallo platform.h header-bestand.</span><span class="sxs-lookup"><span data-stu-id="929c3-191">These functions are declared in hello platform.h header file.</span></span> <span data-ttu-id="929c3-192">Hallo definities van deze functies voor uw doelplatform in Hallo onderzoeken [opslagplaats](https://github.com/Azure/azure-iot-sdk-c) toodetermine noodzaak tooinclude van de platform-specifieke initialisatiecode in de client.</span><span class="sxs-lookup"><span data-stu-id="929c3-192">Examine hello definitions of these functions for your target platform in hello [repository](https://github.com/Azure/azure-iot-sdk-c) toodetermine whether you need tooinclude any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="929c3-193">werkt met bibliotheken hello, toostart toewijzen eerst een client-ingang van IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="929c3-193">toostart working with hello libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="929c3-194">U doorgeven een kopie van de verbindingsreeks voor Hallo apparaat die u hebt verkregen via Hallo apparaat explorer hulpprogramma toothis functie.</span><span class="sxs-lookup"><span data-stu-id="929c3-194">You pass a copy of hello device connection string you obtained from hello device explorer tool toothis function.</span></span> <span data-ttu-id="929c3-195">U ook opgeven Hallo communicatie protocol toouse.</span><span class="sxs-lookup"><span data-stu-id="929c3-195">You also designate hello communications protocol toouse.</span></span> <span data-ttu-id="929c3-196">In dit voorbeeld wordt MQTT maar AMQP en HTTP zijn ook opties.</span><span class="sxs-lookup"><span data-stu-id="929c3-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="929c3-197">Wanneer u hebt een geldige **IOTHUB\_CLIENT\_verwerken**, u kunt beginnen met het aanroepen van Hallo-API's toosend en tooand berichten uit IoT Hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="929c3-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling hello APIs toosend and receive messages tooand from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="929c3-198">Berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="929c3-198">Send messages</span></span>

<span data-ttu-id="929c3-199">Hallo-voorbeeldtoepassing stelt u een lus toosend berichten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="929c3-199">hello sample application sets up a loop toosend messages tooyour IoT hub.</span></span> <span data-ttu-id="929c3-200">Hallo codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="929c3-200">hello following snippet:</span></span>

- <span data-ttu-id="929c3-201">Hiermee maakt u een bericht.</span><span class="sxs-lookup"><span data-stu-id="929c3-201">Creates a message.</span></span>
- <span data-ttu-id="929c3-202">Voegt een eigenschap toohello-bericht.</span><span class="sxs-lookup"><span data-stu-id="929c3-202">Adds a property toohello message.</span></span>
- <span data-ttu-id="929c3-203">Verzendt een bericht.</span><span class="sxs-lookup"><span data-stu-id="929c3-203">Sends a message.</span></span>

<span data-ttu-id="929c3-204">Maak eerst een bericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="929c3-204">First, create a message:</span></span>

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="929c3-205">Telkens wanneer u een bericht verzendt, Geef een verwijzing tooa callback-functie die wordt aangeroepen wanneer het Hallo-gegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="929c3-205">Every time you send a message, you specify a reference tooa callback function that's invoked when hello data is sent.</span></span> <span data-ttu-id="929c3-206">In dit voorbeeld Hallo callback-functie is aangeroepen **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="929c3-206">In this example, hello callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="929c3-207">Hallo volgende fragment toont deze callback-functie:</span><span class="sxs-lookup"><span data-stu-id="929c3-207">hello following snippet shows this callback function:</span></span>

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

<span data-ttu-id="929c3-208">Houd er rekening mee Hallo aanroep toohello **IoTHubMessage\_vernietigen** werkt wanneer u met het Hallo-bericht bent klaar.</span><span class="sxs-lookup"><span data-stu-id="929c3-208">Note hello call toohello **IoTHubMessage\_Destroy** function when you're done with hello message.</span></span> <span data-ttu-id="929c3-209">Deze functie wordt vrijgemaakt Hallo-resources toegewezen tijdens het maken van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="929c3-209">This function frees hello resources allocated when you created hello message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="929c3-210">Berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="929c3-210">Receive messages</span></span>

<span data-ttu-id="929c3-211">Het bericht is een asynchrone bewerking.</span><span class="sxs-lookup"><span data-stu-id="929c3-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="929c3-212">Eerst registreren Hallo callback tooinvoke wanneer Hallo apparaat een bericht weergegeven ontvangt:</span><span class="sxs-lookup"><span data-stu-id="929c3-212">First, you register hello callback tooinvoke when hello device receives a message:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

<span data-ttu-id="929c3-213">de laatste parameter Hallo is een aanwijzer void toowhatever die u wilt.</span><span class="sxs-lookup"><span data-stu-id="929c3-213">hello last parameter is a void pointer toowhatever you want.</span></span> <span data-ttu-id="929c3-214">In Hallo voorbeeld is een aanwijzer tooan geheel getal, maar het mogelijk een wijzer tooa complexere gegevensstructuur.</span><span class="sxs-lookup"><span data-stu-id="929c3-214">In hello sample, it's a pointer tooan integer but it could be a pointer tooa more complex data structure.</span></span> <span data-ttu-id="929c3-215">Deze parameter kunt Hallo callback functie toooperate op gedeelde staat met Hallo aanroeper van deze functie.</span><span class="sxs-lookup"><span data-stu-id="929c3-215">This parameter enables hello callback function toooperate on shared state with hello caller of this function.</span></span>

<span data-ttu-id="929c3-216">Wanneer het Hallo-apparaat een bericht ontvangt, is hello geregistreerde callback-functie aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="929c3-216">When hello device receives a message, hello registered callback function is invoked.</span></span> <span data-ttu-id="929c3-217">Deze functie voor retouraanroepen opgehaald:</span><span class="sxs-lookup"><span data-stu-id="929c3-217">This callback function retrieves:</span></span>

* <span data-ttu-id="929c3-218">Hallo-bericht-id en correlatie-id van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="929c3-218">hello message id and correlation id from hello message.</span></span>
* <span data-ttu-id="929c3-219">Hallo-berichtinhoud.</span><span class="sxs-lookup"><span data-stu-id="929c3-219">hello message content.</span></span>
* <span data-ttu-id="929c3-220">Alle aangepaste eigenschappen van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="929c3-220">Any custom properties from hello message.</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="929c3-221">Gebruik Hallo **IoTHubMessage\_GetByteArray** functie tooretrieve Hallo-bericht, die in dit voorbeeld een tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="929c3-221">Use hello **IoTHubMessage\_GetByteArray** function tooretrieve hello message, which in this example is a string.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="929c3-222">Initialisatie Hallo-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="929c3-222">Uninitialize hello library</span></span>

<span data-ttu-id="929c3-223">Wanneer u klaar bent met gebeurtenissen verzenden en ontvangen van berichten, kunt u Hallo IoT bibliotheek initialisatie.</span><span class="sxs-lookup"><span data-stu-id="929c3-223">When you're done sending events and receiving messages, you can uninitialize hello IoT library.</span></span> <span data-ttu-id="929c3-224">toodo uitgeven dus Hallo functieaanroep te volgen:</span><span class="sxs-lookup"><span data-stu-id="929c3-224">toodo so, issue hello following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="929c3-225">Deze aanroep Hallo-resources eerder toegewezen door Hallo vrijgemaakt **IoTHubClient\_CreateFromConnectionString** functie.</span><span class="sxs-lookup"><span data-stu-id="929c3-225">This call frees up hello resources previously allocated by hello **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="929c3-226">Zoals u ziet het is gemakkelijk toosend en berichten ontvangen met Hallo **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="929c3-226">As you can see, it's easy toosend and receive messages with hello **IoTHubClient** library.</span></span> <span data-ttu-id="929c3-227">Hallo-bibliotheek verwerkt Hallo details voor de communicatie met IoT Hub, met inbegrip van welke toouse protocol (dit is vanuit het perspectief van de Hallo Hallo Developer wordt een eenvoudige configuratieoptie).</span><span class="sxs-lookup"><span data-stu-id="929c3-227">hello library handles hello details of communicating with IoT Hub, including which protocol toouse (from hello perspective of hello developer, this is a simple configuration option).</span></span>

<span data-ttu-id="929c3-228">Hallo **IoTHubClient** bibliotheek biedt ook nauwkeurige controle over hoe tooserialize Hallo gegevens uw apparaat tooIoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="929c3-228">hello **IoTHubClient** library also provides precise control over how tooserialize hello data your device sends tooIoT Hub.</span></span> <span data-ttu-id="929c3-229">In sommige gevallen is dit niveau van controle een voordeel, maar is de details van een implementatie die u niet toobe betrokken wilt bij.</span><span class="sxs-lookup"><span data-stu-id="929c3-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want toobe concerned with.</span></span> <span data-ttu-id="929c3-230">Als dit Hallo geval is, kunt u met behulp van Hallo **serialisatiefunctie** bibliotheek die wordt beschreven in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="929c3-230">If that's hello case, you might consider using hello **serializer** library, which is described in hello next section.</span></span>

## <a name="use-hello-serializer-library"></a><span data-ttu-id="929c3-231">Hallo serialisatiefunctie bibliotheek gebruiken</span><span class="sxs-lookup"><span data-stu-id="929c3-231">Use hello serializer library</span></span>

<span data-ttu-id="929c3-232">Conceptueel Hallo **serialisatiefunctie** bibliotheek bevindt zich bovenaan Hallo **IoTHubClient** bibliotheek in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="929c3-232">Conceptually hello **serializer** library sits on top of hello **IoTHubClient** library in hello SDK.</span></span> <span data-ttu-id="929c3-233">Hierbij Hallo **IoTHubClient** -bibliotheek voor communicatie met IoT Hub, maar de onderliggende hello modellering mogelijkheden die Hallo last van omgaan met bericht serialisatie van de ontwikkelaar Hallo verwijderen toevoegt.</span><span class="sxs-lookup"><span data-stu-id="929c3-233">It uses hello **IoTHubClient** library for hello underlying communication with IoT Hub, but it adds modeling capabilities that remove hello burden of dealing with message serialization from hello developer.</span></span> <span data-ttu-id="929c3-234">Hoe deze bibliotheek werkt best wordt geïllustreerd door een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="929c3-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="929c3-235">Hallo binnen **serialisatiefunctie** map in Hallo [azure-iot-sdk-c-opslagplaats](https://github.com/Azure/azure-iot-sdk-c), is een **voorbeelden** map waarin een toepassing met de naam **simplesample \_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="929c3-235">Inside hello **serializer** folder in hello [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="929c3-236">Hallo Windows-versie van dit voorbeeld bevat Hallo Visual Studio-oplossing te volgen:</span><span class="sxs-lookup"><span data-stu-id="929c3-236">hello Windows version of this sample includes hello following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="929c3-237">Als u dit project in Visual Studio 2017 openen, Hallo prompts tooretarget Hallo project toohello meest recente versie accepteren.</span><span class="sxs-lookup"><span data-stu-id="929c3-237">If you open this project in Visual Studio 2017, accept hello prompts tooretarget hello project toohello latest version.</span></span>

<span data-ttu-id="929c3-238">Net als bij het vorige voorbeeld hello, bevat deze een enkele NuGet-pakketten:</span><span class="sxs-lookup"><span data-stu-id="929c3-238">As with hello previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="929c3-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="929c3-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="929c3-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="929c3-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="929c3-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="929c3-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="929c3-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="929c3-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="929c3-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="929c3-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="929c3-244">U hebt gezien de meeste van deze pakketten in de vorige steekproef hello, maar **Microsoft.Azure.IoTHub.Serializer** is er nieuw.</span><span class="sxs-lookup"><span data-stu-id="929c3-244">You've seen most of these packages in hello previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="929c3-245">Dit pakket is vereist wanneer u Hallo **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="929c3-245">This package is required when you use hello **serializer** library.</span></span>

<span data-ttu-id="929c3-246">U vindt implementatie van de voorbeeldtoepassing Hallo Hallo in Hallo **simplesample\_mqtt.c** bestand.</span><span class="sxs-lookup"><span data-stu-id="929c3-246">You can find hello implementation of hello sample application in hello **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="929c3-247">Hallo volgende secties helpt u stapsgewijs door Hallo sleutel delen van dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="929c3-247">hello following sections walk you through hello key parts of this sample.</span></span>

### <a name="initialize-hello-library"></a><span data-ttu-id="929c3-248">Hallo-bibliotheek initialiseren</span><span class="sxs-lookup"><span data-stu-id="929c3-248">Initialize hello library</span></span>

<span data-ttu-id="929c3-249">werken met Hallo toostart **serialisatiefunctie** bibliotheek aanroep Hallo initialisatie API's:</span><span class="sxs-lookup"><span data-stu-id="929c3-249">toostart working with hello **serializer** library, call hello initialization APIs:</span></span>

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

<span data-ttu-id="929c3-250">Hallo aanroep toohello **serialisatiefunctie\_init** functie is een eenmalige aanroep en initialiseert Hallo onderliggende bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="929c3-250">hello call toohello **serializer\_init** function is a one-time call and initializes hello underlying library.</span></span> <span data-ttu-id="929c3-251">Roep vervolgens Hallo **IoTHubClient\_LLE\_CreateFromConnectionString** functie, die is dezelfde API zoals in Hallo Hallo **IoTHubClient** voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="929c3-251">Then, you call hello **IoTHubClient\_LL\_CreateFromConnectionString** function, which is hello same API as in hello **IoTHubClient** sample.</span></span> <span data-ttu-id="929c3-252">Deze aanroep Hiermee stelt u de verbindingsreeks van uw apparaat (deze aanroep is ook waarin u Hallo protocol kiezen gewenste toouse).</span><span class="sxs-lookup"><span data-stu-id="929c3-252">This call sets your device connection string (this call is also where you choose hello protocol you want toouse).</span></span> <span data-ttu-id="929c3-253">Dit voorbeeld MQTT als Hallo transport gebruikt, maar kan AMQP of HTTP gebruiken.</span><span class="sxs-lookup"><span data-stu-id="929c3-253">This sample uses MQTT as hello transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="929c3-254">Tenslotte roept Hallo **maken\_MODEL\_exemplaar** functie.</span><span class="sxs-lookup"><span data-stu-id="929c3-254">Finally, call hello **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="929c3-255">**WeatherStation** is Hallo-naamruimte van Hallo model en **ContosoAnemometer** Hallo-naam van het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="929c3-255">**WeatherStation** is hello namespace of hello model and **ContosoAnemometer** is hello name of hello model.</span></span> <span data-ttu-id="929c3-256">Zodra Hallo model exemplaar is gemaakt, kunt u deze toostart verzenden en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="929c3-256">Once hello model instance is created, you can use it toostart sending and receiving messages.</span></span> <span data-ttu-id="929c3-257">Het is echter belangrijk toounderstand welk model is.</span><span class="sxs-lookup"><span data-stu-id="929c3-257">However, it's important toounderstand what a model is.</span></span>

### <a name="define-hello-model"></a><span data-ttu-id="929c3-258">Hallo model definiëren</span><span class="sxs-lookup"><span data-stu-id="929c3-258">Define hello model</span></span>

<span data-ttu-id="929c3-259">Een model in Hallo **serialisatiefunctie** bibliotheek definieert Hallo-berichten dat uw apparaat tooIoT Hub en Hallo-berichten verzenden kunt, zogenaamde *acties* in Hallo modelleertaal op het kan ontvangen.</span><span class="sxs-lookup"><span data-stu-id="929c3-259">A model in hello **serializer** library defines hello messages that your device can send tooIoT Hub and hello messages, called *actions* in hello modeling language, which it can receive.</span></span> <span data-ttu-id="929c3-260">U definieert een model met behulp van een set van C macro's zoals Hallo in **simplesample\_mqtt** voorbeeldtoepassing:</span><span class="sxs-lookup"><span data-stu-id="929c3-260">You define a model using a set of C macros as in hello **simplesample\_mqtt** sample application:</span></span>

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="929c3-261">Hallo **BEGINT\_NAAMRUIMTE** en **END\_NAAMRUIMTE** macro's beide Hallo-naamruimte van Hallo model als een argument nemen.</span><span class="sxs-lookup"><span data-stu-id="929c3-261">hello **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take hello namespace of hello model as an argument.</span></span> <span data-ttu-id="929c3-262">Verwacht wordt dat is alles tussen deze macro's Hallo definitie van uw model of modellen en Hallo-gegevensstructuren die Hallo modellen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="929c3-262">It's expected that anything between these macros is hello definition of your model or models, and hello data structures that hello models use.</span></span>

<span data-ttu-id="929c3-263">In dit voorbeeld is een enkelvoudig model aangeroepen **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="929c3-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="929c3-264">Dit model definieert twee soorten gegevens kan uw apparaat tooIoT Hub verzenden: **DeviceId** en **windsnelheid**.</span><span class="sxs-lookup"><span data-stu-id="929c3-264">This model defines two pieces of data that your device can send tooIoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="929c3-265">Definieert ook drie acties (berichten) die het apparaat kan ontvangen: **TurnFanOn**, **TurnFanOff**, en **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="929c3-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="929c3-266">Elk gegevenselement in de heeft een type en elke actie heeft een naam (en desgewenst een set parameters).</span><span class="sxs-lookup"><span data-stu-id="929c3-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="929c3-267">Hallo-gegevens en acties die zijn gedefinieerd in Hallo model definiëren een API-gebied dat u gebruik kunt toosend berichten tooIoT Hub en toomessages verzonden toohello apparaat reageren.</span><span class="sxs-lookup"><span data-stu-id="929c3-267">hello data and actions defined in hello model define an API surface that you can use toosend messages tooIoT Hub, and respond toomessages sent toohello device.</span></span> <span data-ttu-id="929c3-268">Door een voorbeeld van het gebruik van dit model best begrijpen.</span><span class="sxs-lookup"><span data-stu-id="929c3-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="929c3-269">Berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="929c3-269">Send messages</span></span>

<span data-ttu-id="929c3-270">Hallo model definieert Hallo gegevens u tooIoT Hub kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="929c3-270">hello model defines hello data you can send tooIoT Hub.</span></span> <span data-ttu-id="929c3-271">In dit voorbeeld dit betekent dat een Hallo twee gegevensitems die zijn gedefinieerd met behulp van Hallo **WITH_DATA** macro.</span><span class="sxs-lookup"><span data-stu-id="929c3-271">In this example, that means one of hello two data items defined using hello **WITH_DATA** macro.</span></span> <span data-ttu-id="929c3-272">Er zijn verschillende stappen vereist toosend **DeviceId** en **windsnelheid** waarden tooan IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="929c3-272">There are several steps required toosend **DeviceId** and **WindSpeed** values tooan IoT hub.</span></span> <span data-ttu-id="929c3-273">Hallo is eerst tooset Hallo gegevens die u wilt dat toosend:</span><span class="sxs-lookup"><span data-stu-id="929c3-273">hello first is tooset hello data you want toosend:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="929c3-274">Hallo model dat u eerder hebt gedefinieerd kunt u tooset Hallo waarden door leden van een **struct**.</span><span class="sxs-lookup"><span data-stu-id="929c3-274">hello model you defined earlier enables you tooset hello values by setting members of a **struct**.</span></span> <span data-ttu-id="929c3-275">Vervolgens serialiseren gewenste toosend Hallo-bericht:</span><span class="sxs-lookup"><span data-stu-id="929c3-275">Next, serialize hello message you want toosend:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="929c3-276">Deze code serialiseert Hallo apparaat-naar-cloud tooa buffer (waarnaar wordt verwezen door **bestemming**).</span><span class="sxs-lookup"><span data-stu-id="929c3-276">This code serializes hello device-to-cloud tooa buffer (referenced by **destination**).</span></span> <span data-ttu-id="929c3-277">Hallo code roept vervolgens Hallo **sendMessage** toosend Hallo-bericht tooIoT Hub werken:</span><span class="sxs-lookup"><span data-stu-id="929c3-277">hello code then invokes hello **sendMessage** function toosend hello message tooIoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="929c3-278">tweede toolast-parameter van Hallo **IoTHubClient\_LLE\_SendEventAsync** is een verwijzing tooa callback-functie die wordt aangeroepen wanneer het Hallo-gegevens is verzonden.</span><span class="sxs-lookup"><span data-stu-id="929c3-278">hello second toolast parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference tooa callback function that's called when hello data is successfully sent.</span></span> <span data-ttu-id="929c3-279">Hier volgt Hallo callback-functie in Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="929c3-279">Here's hello callback function in hello sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="929c3-280">de tweede parameter Hallo is een aanwijzer toouser context; Hallo dezelfde aanwijzer te doorgegeven**IoTHubClient\_LLE\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="929c3-280">hello second parameter is a pointer toouser context; hello same pointer passed too**IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="929c3-281">In dit geval Hallo-context is een eenvoudige Prestatiemeter gebruiken, maar dit alles kan zijn.</span><span class="sxs-lookup"><span data-stu-id="929c3-281">In this case, hello context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="929c3-282">Dit is alles wat er is toosending apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="929c3-282">That's all there is toosending device-to-cloud messages.</span></span> <span data-ttu-id="929c3-283">Hallo alleen wat toocover links, is hoe tooreceive berichten.</span><span class="sxs-lookup"><span data-stu-id="929c3-283">hello only thing left toocover is how tooreceive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="929c3-284">Berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="929c3-284">Receive messages</span></span>

<span data-ttu-id="929c3-285">Ontvangen van een bericht werkt op dezelfde manier toohello werkwijze berichten in Hallo **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="929c3-285">Receiving a message works similarly toohello way messages work in hello **IoTHubClient** library.</span></span> <span data-ttu-id="929c3-286">U registreert eerst een callback-functie van het bericht:</span><span class="sxs-lookup"><span data-stu-id="929c3-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="929c3-287">U schrijft vervolgens Hallo callbackfunctie die wordt aangeroepen wanneer een bericht wordt ontvangen:</span><span class="sxs-lookup"><span data-stu-id="929c3-287">Then, you write hello callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="929c3-288">Deze code is standaardtekst--deze heeft dezelfde Hallo voor een oplossing.</span><span class="sxs-lookup"><span data-stu-id="929c3-288">This code is boilerplate -- it's hello same for any solution.</span></span> <span data-ttu-id="929c3-289">Deze functie het Hallo-bericht ontvangt, en zorgt voor routering toohello juiste functie via Hallo aanroep te**EXECUTE\_opdracht**.</span><span class="sxs-lookup"><span data-stu-id="929c3-289">This function receives hello message and takes care of routing it toohello appropriate function through hello call too**EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="929c3-290">aangeroepen Hallo-functie is op dit moment hangt af van het Hallo-definitie van Hallo-acties in uw model.</span><span class="sxs-lookup"><span data-stu-id="929c3-290">hello function called at this point depends on hello definition of hello actions in your model.</span></span>

<span data-ttu-id="929c3-291">Wanneer u een actie in het model definiëren, bent u klaar vereist tooimplement een functie die wordt aangeroepen wanneer het apparaat het bijbehorende Hallo-bericht ontvangt.</span><span class="sxs-lookup"><span data-stu-id="929c3-291">When you define an action in your model, you're required tooimplement a function that's called when your device receives hello corresponding message.</span></span> <span data-ttu-id="929c3-292">Bijvoorbeeld, als het model is gedefinieerd met deze actie:</span><span class="sxs-lookup"><span data-stu-id="929c3-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="929c3-293">Een functie met deze handtekening definiëren:</span><span class="sxs-lookup"><span data-stu-id="929c3-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="929c3-294">Houd er rekening mee hoe Hallo-naam van de functie Hallo overeenkomt met Hallo-naam van Hallo actie in Hallo model en dat Hallo parameters van functie Hallo Hallo parameters opgegeven voor de Hallo actie.</span><span class="sxs-lookup"><span data-stu-id="929c3-294">Note how hello name of hello function matches hello name of hello action in hello model and that hello parameters of hello function match hello parameters specified for hello action.</span></span> <span data-ttu-id="929c3-295">de eerste parameter Hallo is altijd vereist en een exemplaar van de wijzer toohello van uw model bevat.</span><span class="sxs-lookup"><span data-stu-id="929c3-295">hello first parameter is always required and contains a pointer toohello instance of your model.</span></span>

<span data-ttu-id="929c3-296">Wanneer Hallo apparaat een bericht dat overeenkomt met deze handtekening ontvangt, wordt de overeenkomende functie Hallo genoemd.</span><span class="sxs-lookup"><span data-stu-id="929c3-296">When hello device receives a message that matches this signature, hello corresponding function is called.</span></span> <span data-ttu-id="929c3-297">Daarom in combinatie met tooinclude Hallo standaardtekst code uit **IoTHubMessage**, ontvangen van berichten is slechts een kwestie van het definiëren van een eenvoudige functie voor elke actie in het model is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="929c3-297">Therefore, aside from having tooinclude hello boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-hello-library"></a><span data-ttu-id="929c3-298">Initialisatie Hallo-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="929c3-298">Uninitialize hello library</span></span>

<span data-ttu-id="929c3-299">Wanneer u klaar bent met gegevens verzenden en ontvangen van berichten, kunt u Hallo IoT bibliotheek initialisatie:</span><span class="sxs-lookup"><span data-stu-id="929c3-299">When you're done sending data and receiving messages, you can uninitialize hello IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="929c3-300">Elk van deze drie functies wordt uitgelijnd met Hallo drie initialisatie van de functies die eerder zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="929c3-300">Each of these three functions aligns with hello three initialization functions described previously.</span></span> <span data-ttu-id="929c3-301">Het aanroepen van deze API's zorgt ervoor dat u eerder toegewezen resources vrij.</span><span class="sxs-lookup"><span data-stu-id="929c3-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="929c3-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="929c3-302">Next Steps</span></span>

<span data-ttu-id="929c3-303">In dit artikel gedekt Hallo grondbeginselen van het gebruik van Hallo-bibliotheken in Hallo **Azure IoT-device SDK voor C**. Dit u geleverd met voldoende informatie toounderstand wat opgenomen in Hallo SDK, de architectuur en hoe het werken met Hallo Windows voorbeelden van tooget wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="929c3-303">This article covered hello basics of using hello libraries in hello **Azure IoT device SDK for C**. It provided you with enough information toounderstand what's included in hello SDK, its architecture, and how tooget started working with hello Windows samples.</span></span> <span data-ttu-id="929c3-304">het volgende artikel Hallo Hallo beschrijving van Hallo SDK blijft door waarin wordt uitgelegd [meer over Hallo IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="929c3-304">hello next article continues hello description of hello SDK by explaining [more about hello IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="929c3-305">toolearn meer informatie over het ontwikkelen voor IoT Hub, Zie Hallo [Azure IoT SDK's][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="929c3-305">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="929c3-306">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="929c3-306">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="929c3-307">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="929c3-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
