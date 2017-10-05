---
title: Het apparaat met Azure IoT SDK voor C | Microsoft Docs
description: Aan de slag met het apparaat met Azure IoT SDK voor C en informatie over het maken van apps voor apparaten die communiceren met een IoT-hub.
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
ms.openlocfilehash: 459b630f28fe48064f4ba280974f3fdbdb82f0a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-iot-device-sdk-for-c"></a><span data-ttu-id="7a01e-103">Azure IoT-apparaat SDK voor C</span><span class="sxs-lookup"><span data-stu-id="7a01e-103">Azure IoT device SDK for C</span></span>

<span data-ttu-id="7a01e-104">De **Azure IoT-device SDK** is een set van bibliotheken die zijn ontworpen voor het vereenvoudigen van het proces van het verzenden van berichten naar en ontvangen van berichten uit de **Azure IoT Hub** service.</span><span class="sxs-lookup"><span data-stu-id="7a01e-104">The **Azure IoT device SDK** is a set of libraries designed to simplify the process of sending messages to and receiving messages from the **Azure IoT Hub** service.</span></span> <span data-ttu-id="7a01e-105">Er zijn verschillende variaties van de SDK, elke die gericht is op een specifiek platform, maar in dit artikel beschrijft de **Azure IoT-device SDK voor C**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-105">There are different variations of the SDK, each targeting a specific platform, but this article describes the **Azure IoT device SDK for C**.</span></span>

<span data-ttu-id="7a01e-106">Het apparaat met Azure IoT SDK voor C is geschreven in C ANSI (C99) om te maximaliseren draagbaarheid.</span><span class="sxs-lookup"><span data-stu-id="7a01e-106">The Azure IoT device SDK for C is written in ANSI C (C99) to maximize portability.</span></span> <span data-ttu-id="7a01e-107">Deze functie stelt de bibliotheken geschikt bewerkingen uitvoeren op meerdere platforms en apparaten, vooral wanneer het minimaliseren van schijf en geheugengebruik is een prioriteit.</span><span class="sxs-lookup"><span data-stu-id="7a01e-107">This feature makes the libraries well-suited to operate on multiple platforms and devices, especially where minimizing disk and memory footprint is a priority.</span></span>

<span data-ttu-id="7a01e-108">Er zijn een breed scala aan platforms waarop de SDK is getest (Zie de [Azure gecertificeerd voor IoT-apparaat catalogus](https://catalog.azureiotsuite.com/) voor meer informatie).</span><span class="sxs-lookup"><span data-stu-id="7a01e-108">There are a broad range of platforms on which the SDK has been tested (see the [Azure Certified for IoT device catalog](https://catalog.azureiotsuite.com/) for details).</span></span> <span data-ttu-id="7a01e-109">Hoewel dit artikel scenario's van voorbeeldcode uitgevoerd op het Windows-platform bevat, is de code die wordt beschreven in dit artikel is identiek in het bereik van de ondersteunde platforms.</span><span class="sxs-lookup"><span data-stu-id="7a01e-109">Although this article includes walkthroughs of sample code running on the Windows platform, the code described in this article is identical across the range of supported platforms.</span></span>

<span data-ttu-id="7a01e-110">In dit artikel maakt u kennis met de architectuur van het apparaat met Azure IoT SDK voor C. Dit laat zien hoe de apparaatbibliotheek initialiseren en berichten ontvangen gegevens verzenden naar IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-110">This article introduces you to the architecture of the Azure IoT device SDK for C. It demonstrates how to initialize the device library, send data to IoT Hub, and receive messages from it.</span></span> <span data-ttu-id="7a01e-111">De informatie in dit artikel moet voldoende aan de slag met de SDK, maar bevat ook koppelingen naar aanvullende informatie over de bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="7a01e-111">The information in this article should be enough to get started using the SDK, but also provides pointers to additional information about the libraries.</span></span>

## <a name="sdk-architecture"></a><span data-ttu-id="7a01e-112">SDK-architectuur</span><span class="sxs-lookup"><span data-stu-id="7a01e-112">SDK architecture</span></span>

<span data-ttu-id="7a01e-113">U vindt de [ **Azure IoT-device SDK voor C** ](https://github.com/Azure/azure-iot-sdk-c) GitHub-opslagplaats en de weergave details van de API in de [C-API-referentiemateriaal](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="7a01e-113">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

<span data-ttu-id="7a01e-114">De meest recente versie van de bibliotheken vindt u in de **master** branche van de opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="7a01e-114">The latest version of the libraries can be found in the **master** branch of the repository:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* <span data-ttu-id="7a01e-115">De core-implementatie van de SDK is in de **iothub\_client** map met de implementatie van de onderste laag API in de SDK: de **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7a01e-115">The core implementation of the SDK is in the **iothub\_client** folder that contains the implementation of the lowest API layer in the SDK: the **IoTHubClient** library.</span></span> <span data-ttu-id="7a01e-116">De **IoTHubClient** bibliotheek bevat API's implementeren onbewerkte berichten voor het verzenden van berichten naar IoT Hub en ontvangen van berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-116">The **IoTHubClient** library contains APIs implementing raw messaging for sending messages to IoT Hub and receiving messages from IoT Hub.</span></span> <span data-ttu-id="7a01e-117">Wanneer u deze bibliotheek, bent u verantwoordelijk voor het implementeren van bericht serialisatie, maar andere details voor de communicatie met IoT Hub worden afgehandeld.</span><span class="sxs-lookup"><span data-stu-id="7a01e-117">When using this library, you are responsible for implementing message serialization, but other details of communicating with IoT Hub are handled for you.</span></span>
* <span data-ttu-id="7a01e-118">De **serialisatiefunctie** map hulpfuncties en voorbeelden die laten hoe u gegevens serialiseren zien voordat naar Azure IoT Hub worden verzonden met behulp van de clientbibliotheek bevat.</span><span class="sxs-lookup"><span data-stu-id="7a01e-118">The **serializer** folder contains helper functions and samples that show you how to serialize data before sending to Azure IoT Hub using the client library.</span></span> <span data-ttu-id="7a01e-119">Het gebruik van de serializer is niet verplicht en uw gemak is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7a01e-119">The use of the serializer is not mandatory and is provided as a convenience.</span></span> <span data-ttu-id="7a01e-120">Gebruik de **serialisatiefunctie** wanneer u een model waarin de gegevens worden verzonden naar IoT Hub en de berichten die u verwacht te ontvangen van deze bibliotheek, definiëren.</span><span class="sxs-lookup"><span data-stu-id="7a01e-120">To use the **serializer** library, you define a model that specifies the data to send to IoT Hub and the messages you expect to receive from it.</span></span> <span data-ttu-id="7a01e-121">Als het model is gedefinieerd, biedt de SDK u een API-gebied waarmee u eenvoudig werken met de apparaat-naar-cloud-en cloud-naar-apparaat zonder dat u de details van de serialisatie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-121">Once the model is defined, the SDK provides you with an API surface that enables you to easily work with device-to-cloud and cloud-to-device messages without worrying about the serialization details.</span></span> <span data-ttu-id="7a01e-122">De bibliotheek is afhankelijk van andere open-source bibliotheken die implementeren met behulp van protocollen zoals MQTT en AMQP transport.</span><span class="sxs-lookup"><span data-stu-id="7a01e-122">The library depends on other open source libraries that implement transport using protocols such as MQTT and AMQP.</span></span>
* <span data-ttu-id="7a01e-123">De **IoTHubClient** bibliotheek, is afhankelijk van andere open-source bibliotheken:</span><span class="sxs-lookup"><span data-stu-id="7a01e-123">The **IoTHubClient** library depends on other open source libraries:</span></span>
  * <span data-ttu-id="7a01e-124">De [Azure C gedeeld hulpprogramma](https://github.com/Azure/azure-c-shared-utility) bibliotheek, waardoor algemene functionaliteit voor basistaken (zoals tekenreeksen, bewerkingen en i/o) over diverse Azure-gerelateerde C SDK's nodig.</span><span class="sxs-lookup"><span data-stu-id="7a01e-124">The [Azure C shared utility](https://github.com/Azure/azure-c-shared-utility) library, which provides common functionality for basic tasks (such as strings, list manipulation, and IO) needed across several Azure-related C SDKs.</span></span>
  * <span data-ttu-id="7a01e-125">De [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) bibliotheek die een client-side '-implementatie van AMQP die zijn geoptimaliseerd voor resource beperkte apparaten.</span><span class="sxs-lookup"><span data-stu-id="7a01e-125">The [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) library, which is a client-side implementation of AMQP optimized for resource constrained devices.</span></span>
  * <span data-ttu-id="7a01e-126">De [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) bibliotheek is een algemene bibliotheek implementatie van het protocol MQTT en geoptimaliseerd voor resource beperkte apparaten.</span><span class="sxs-lookup"><span data-stu-id="7a01e-126">The [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) library, which is a general-purpose library implementing the MQTT protocol and optimized for resource constrained devices.</span></span>

<span data-ttu-id="7a01e-127">Gebruik van deze bibliotheken is gemakkelijker te begrijpen door te kijken voorbeeldcode.</span><span class="sxs-lookup"><span data-stu-id="7a01e-127">Use of these libraries is easier to understand by looking at example code.</span></span> <span data-ttu-id="7a01e-128">De volgende secties helpt u stapsgewijs door verschillende van de voorbeeldtoepassingen die zijn opgenomen in de SDK.</span><span class="sxs-lookup"><span data-stu-id="7a01e-128">The following sections walk you through several of the sample applications that are included in the SDK.</span></span> <span data-ttu-id="7a01e-129">In dit scenario moet bieden u een goed idee voor de verschillende mogelijkheden van de architectuur van de SDK en een inleiding tot de werking van de API's.</span><span class="sxs-lookup"><span data-stu-id="7a01e-129">This walkthrough should give you a good feel for the various capabilities of the architectural layers of the SDK and an introduction to how the APIs work.</span></span>

## <a name="before-you-run-the-samples"></a><span data-ttu-id="7a01e-130">Voordat u de controles uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7a01e-130">Before you run the samples</span></span>

<span data-ttu-id="7a01e-131">Voordat u de voorbeelden in de Azure IoT-device SDK voor C uitvoeren kunt, moet u [geen exemplaar maken van de service IoT Hub](iot-hub-create-through-portal.md) in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7a01e-131">Before you can run the samples in the Azure IoT device SDK for C, you must [create an instance of the IoT Hub service](iot-hub-create-through-portal.md) in your Azure subscription.</span></span> <span data-ttu-id="7a01e-132">Voltooi de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="7a01e-132">Then complete the following tasks:</span></span>

* <span data-ttu-id="7a01e-133">Uw ontwikkelomgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7a01e-133">Prepare your development environment</span></span>
* <span data-ttu-id="7a01e-134">Apparaat-referenties ophalen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-134">Obtain device credentials.</span></span>

### <a name="prepare-your-development-environment"></a><span data-ttu-id="7a01e-135">Uw ontwikkelomgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7a01e-135">Prepare your development environment</span></span>

<span data-ttu-id="7a01e-136">Pakketten zijn beschikbaar voor algemene platforms (zoals NuGet voor Windows of apt_get voor Debian en Ubuntu) en de voorbeelden gebruiken deze pakketten indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7a01e-136">Packages are provided for common platforms (such as NuGet for Windows or apt_get for Debian and Ubuntu) and the samples use these packages when available.</span></span> <span data-ttu-id="7a01e-137">In sommige gevallen moet u Compileer de SDK voor of op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="7a01e-137">In some cases, you need to compile the SDK for or on your device.</span></span> <span data-ttu-id="7a01e-138">Als u Compileer de SDK wilt, Zie [uw ontwikkelingsomgeving voorbereiden](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in de GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="7a01e-138">If you need to compile the SDK, see [Prepare your development environment](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) in the GitHub repository.</span></span>

<span data-ttu-id="7a01e-139">Als u de voorbeeldcode van de toepassing, een kopie van de SDK te downloaden vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-139">To obtain the sample application code, download a copy of the SDK from GitHub.</span></span> <span data-ttu-id="7a01e-140">Een exemplaar van de bron van de **master** vertakking van de [GitHub-opslagplaats](https://github.com/Azure/azure-iot-sdk-c).</span><span class="sxs-lookup"><span data-stu-id="7a01e-140">Get your copy of the source from the **master** branch of the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c).</span></span>


### <a name="obtain-the-device-credentials"></a><span data-ttu-id="7a01e-141">De referenties van het apparaat ophalen</span><span class="sxs-lookup"><span data-stu-id="7a01e-141">Obtain the device credentials</span></span>

<span data-ttu-id="7a01e-142">Nu dat u de voorbeeldcode van de bron hebt, is het volgende wat te doen om op te halen van een set referenties apparaat.</span><span class="sxs-lookup"><span data-stu-id="7a01e-142">Now that you have the sample source code, the next thing to do is to get a set of device credentials.</span></span> <span data-ttu-id="7a01e-143">Voor een apparaat kunnen toegang krijgen tot een IoT-hub, moet u eerst het apparaat toevoegen aan de id-register van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-143">For a device to be able to access an IoT hub, you must first add the device to the IoT Hub identity registry.</span></span> <span data-ttu-id="7a01e-144">Als u uw apparaat toevoegt, krijgt u een set referenties voor apparaten die u nodig hebt voor het apparaat verbinding kunnen maken met de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-144">When you add your device, you get a set of device credentials that you need for the device to be able to connect to the IoT hub.</span></span> <span data-ttu-id="7a01e-145">De voorbeeldtoepassingen die wordt besproken in de volgende sectie verwacht dat deze referenties in de vorm van een **apparaat verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-145">The sample applications discussed in the next section expect these credentials in the form of a **device connection string**.</span></span>

<span data-ttu-id="7a01e-146">Er zijn verschillende open-source hulpprogramma's voor het beheren van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-146">There are several open source tools to help you manage your IoT hub.</span></span>

* <span data-ttu-id="7a01e-147">Een Windows-toepassing aangeroepen [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="7a01e-147">A Windows application called [device explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>
* <span data-ttu-id="7a01e-148">Een node.js platformoverschrijdende CLI-hulpprogramma aangeroepen [iothub explorer](https://github.com/azure/iothub-explorer).</span><span class="sxs-lookup"><span data-stu-id="7a01e-148">A cross-platform node.js CLI tool called [iothub-explorer](https://github.com/azure/iothub-explorer).</span></span>

<span data-ttu-id="7a01e-149">Deze zelfstudie wordt gebruikgemaakt van de grafische *apparaat explorer* hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7a01e-149">This tutorial uses the graphical *device explorer* tool.</span></span> <span data-ttu-id="7a01e-150">U kunt ook de *iothub explorer* hulpprogramma als u liever een CLI-hulpprogramma te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a01e-150">You can also use the *iothub-explorer* tool if you prefer to use a CLI tool.</span></span>

<span data-ttu-id="7a01e-151">Het programma voor apparaat explorer gebruikt de bibliotheken van de service Azure IoT voor diverse functies uitvoeren op IoT Hub, inclusief het toevoegen van apparaten.</span><span class="sxs-lookup"><span data-stu-id="7a01e-151">The device explorer tool uses the Azure IoT service libraries to perform various functions on IoT Hub, including adding devices.</span></span> <span data-ttu-id="7a01e-152">Als u het apparaat explorer-hulpprogramma gebruiken voor het toevoegen van een apparaat, krijgt u een verbindingsreeks voor uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="7a01e-152">If you use the device explorer tool to add a device, you get a connection string for your device.</span></span> <span data-ttu-id="7a01e-153">U moet deze verbindingsreeks om uit te voeren van de voorbeeldtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-153">You need this connection string to run the sample applications.</span></span>

<span data-ttu-id="7a01e-154">Als u niet bekend met het programma voor apparaat explorer bent, geeft de volgende procedure wordt beschreven hoe gebruikt om een apparaat toevoegt en een apparaat-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-154">If you're not familiar with the device explorer tool, the following procedure describes how to use it to add a device and obtain a device connection string.</span></span>

<span data-ttu-id="7a01e-155">Zie het installeren van het programma voor apparaat explorer [de Explorer-apparaat gebruiken voor IoT Hub-apparaten](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span><span class="sxs-lookup"><span data-stu-id="7a01e-155">To install the device explorer tool, see [How to use the Device Explorer for IoT Hub devices](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).</span></span>

<span data-ttu-id="7a01e-156">Wanneer u het programma uitvoert, ziet u deze interface:</span><span class="sxs-lookup"><span data-stu-id="7a01e-156">When you run the program, you see this interface:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

<span data-ttu-id="7a01e-157">Voer uw **IoT Hub-verbindingsreeks** in het eerste veld en klikt u op **Update**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-157">Enter your **IoT Hub Connection String** in the first field and click **Update**.</span></span> <span data-ttu-id="7a01e-158">Deze stap configureert u het hulpprogramma zodat deze met IoT Hub communiceren kan.</span><span class="sxs-lookup"><span data-stu-id="7a01e-158">This step configures the tool so that it can communicate with IoT Hub.</span></span>

<span data-ttu-id="7a01e-159">Wanneer de IoT Hub-verbindingsreeks is geconfigureerd, klikt u op de **Management** tabblad:</span><span class="sxs-lookup"><span data-stu-id="7a01e-159">When the IoT Hub connection string is configured, click the **Management** tab:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

<span data-ttu-id="7a01e-160">Dit tabblad is waar het beheren van de apparaten in uw IoT-hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="7a01e-160">This tab is where you manage the devices registered in your IoT hub.</span></span>

<span data-ttu-id="7a01e-161">U maakt een apparaat door te klikken op de **maken** knop.</span><span class="sxs-lookup"><span data-stu-id="7a01e-161">You create a device by clicking the **Create** button.</span></span> <span data-ttu-id="7a01e-162">Er wordt een dialoogvenster weergegeven met een reeks vooraf ingestelde sleutels (primair en secundair).</span><span class="sxs-lookup"><span data-stu-id="7a01e-162">A dialog displays with a set of pre-populated keys (primary and secondary).</span></span> <span data-ttu-id="7a01e-163">Voer een **apparaat-ID** en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-163">Enter a **Device ID** and then click **Create**.</span></span>

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

<span data-ttu-id="7a01e-164">Wanneer het apparaat is gemaakt, weergeven de apparaten updates met alle geregistreerde apparaten, inclusief de waarschuwing die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a01e-164">When the device is created, the Devices list updates with all the registered devices, including the one you just created.</span></span> <span data-ttu-id="7a01e-165">Als u met de rechtermuisknop op het nieuwe apparaat, ziet u dit menu:</span><span class="sxs-lookup"><span data-stu-id="7a01e-165">If you right-click your new device, you see this menu:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

<span data-ttu-id="7a01e-166">Als u ervoor kiest **Kopieer de verbindingsreeks voor geselecteerde apparaat**, de verbindingsreeks van het apparaat naar het Klembord is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="7a01e-166">If you choose **Copy connection string for selected device**, the device connection string is copied to the clipboard.</span></span> <span data-ttu-id="7a01e-167">Houd een kopie van de verbindingsreeks van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="7a01e-167">Keep a copy of the device connection string.</span></span> <span data-ttu-id="7a01e-168">U moet bij het uitvoeren van de voorbeeldtoepassingen die in de volgende secties beschreven.</span><span class="sxs-lookup"><span data-stu-id="7a01e-168">You need it when running the sample applications described in the following sections.</span></span>

<span data-ttu-id="7a01e-169">Wanneer u de bovenstaande stappen hebt voltooid, bent u klaar om te beginnen met het uitvoeren van sommige code.</span><span class="sxs-lookup"><span data-stu-id="7a01e-169">When you've completed the steps above, you're ready to start running some code.</span></span> <span data-ttu-id="7a01e-170">Beide voorbeelden hebben een constante aan de bovenkant van de belangrijkste bron-bestand waarmee u een verbindingsreeks invoeren.</span><span class="sxs-lookup"><span data-stu-id="7a01e-170">Both samples have a constant at the top of the main source file that enables you to enter a connection string.</span></span> <span data-ttu-id="7a01e-171">Bijvoorbeeld, de bijbehorende regel van de **iothub\_client\_voorbeeld\_mqtt** toepassing wordt weergegeven als volgt.</span><span class="sxs-lookup"><span data-stu-id="7a01e-171">For example, the corresponding line from the **iothub\_client\_sample\_mqtt** application appears as follows.</span></span>

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-the-iothubclient-library"></a><span data-ttu-id="7a01e-172">Gebruik de IoTHubClient-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="7a01e-172">Use the IoTHubClient library</span></span>

<span data-ttu-id="7a01e-173">Binnen de **iothub\_client** map in de [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) -opslagplaats, er is een **voorbeelden** map waarin een toepassing met de naam **iothub\_client\_voorbeeld\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-173">Within the **iothub\_client** folder in the [azure-iot-sdk-c](https://github.com/azure/azure-iot-sdk-c) repository, there is a **samples** folder that contains an application called **iothub\_client\_sample\_mqtt**.</span></span>

<span data-ttu-id="7a01e-174">De Windows-versie van de **iothub\_client\_voorbeeld\_mqtt** toepassing bevat de volgende Visual Studio-oplossing:</span><span class="sxs-lookup"><span data-stu-id="7a01e-174">The Windows version of the **iothub\_client\_sample\_mqtt** application includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="7a01e-175">Als u dit project in Visual Studio 2017 opent, accepteert u de aanwijzingen voor het stelt u het project naar de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-175">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="7a01e-176">Deze oplossing bevat een project.</span><span class="sxs-lookup"><span data-stu-id="7a01e-176">This solution contains a single project.</span></span> <span data-ttu-id="7a01e-177">Er zijn vier NuGet-pakketten in deze oplossing is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="7a01e-177">There are four NuGet packages installed in this solution:</span></span>

* <span data-ttu-id="7a01e-178">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="7a01e-178">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="7a01e-179">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="7a01e-179">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="7a01e-180">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="7a01e-180">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="7a01e-181">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="7a01e-181">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="7a01e-182">Moet u altijd de **Microsoft.Azure.C.SharedUtility** wanneer u met de SDK werkt-pakket.</span><span class="sxs-lookup"><span data-stu-id="7a01e-182">You always need the **Microsoft.Azure.C.SharedUtility** package when you are working with the SDK.</span></span> <span data-ttu-id="7a01e-183">Dit voorbeeld wordt de protocollen MQTT-protocol gebruikt, dus u moet bevatten de **Microsoft.Azure.umqtt** en **Microsoft.Azure.IoTHub.MqttTransport** pakketten (Er zijn equivalent pakketten voor AMQP en HTTP).</span><span class="sxs-lookup"><span data-stu-id="7a01e-183">This sample uses the MQTT protocol, therefore you must include the **Microsoft.Azure.umqtt** and **Microsoft.Azure.IoTHub.MqttTransport** packages (there are equivalent packages for AMQP and HTTP).</span></span> <span data-ttu-id="7a01e-184">Omdat in dit voorbeeld worden de **IoTHubClient** bibliotheek, moet u ook de **Microsoft.Azure.IoTHub.IoTHubClient** -pakket in uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="7a01e-184">Because the sample uses the **IoTHubClient** library, you must also include the **Microsoft.Azure.IoTHub.IoTHubClient** package in your solution.</span></span>

<span data-ttu-id="7a01e-185">U vindt de uitvoering voor de voorbeeldtoepassing in de **iothub\_client\_voorbeeld\_mqtt.c** bronbestand.</span><span class="sxs-lookup"><span data-stu-id="7a01e-185">You can find the implementation for the sample application in the **iothub\_client\_sample\_mqtt.c** source file.</span></span>

<span data-ttu-id="7a01e-186">De volgende stappen gebruikt deze voorbeeldtoepassing u stapsgewijs door het wat nodig is om het gebruik van de **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7a01e-186">The following steps use this sample application to walk you through what's required to use the **IoTHubClient** library.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="7a01e-187">De bibliotheek initialiseren</span><span class="sxs-lookup"><span data-stu-id="7a01e-187">Initialize the library</span></span>

> [!NOTE]
> <span data-ttu-id="7a01e-188">Voordat u begint te werken met de bibliotheken, moet u wellicht initialisaties platform-specifieke uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7a01e-188">Before you start working with the libraries, you may need to perform some platform-specific initialization.</span></span> <span data-ttu-id="7a01e-189">Als u wilt gebruiken AMQP op Linux moet u bijvoorbeeld de OpenSSL-bibliotheek initialiseren.</span><span class="sxs-lookup"><span data-stu-id="7a01e-189">For example, if you plan to use AMQP on Linux you must initialize the OpenSSL library.</span></span> <span data-ttu-id="7a01e-190">De voorbeelden in de [GitHub-opslagplaats](https://github.com/Azure/azure-iot-sdk-c) Roep de hulpprogrammafunctie **platform\_init** wanneer de client wordt gestart en roep de **platform\_deinit**functie voordat u afsluit.</span><span class="sxs-lookup"><span data-stu-id="7a01e-190">The samples in the [GitHub repository](https://github.com/Azure/azure-iot-sdk-c) call the utility function **platform\_init** when the client starts and call the **platform\_deinit** function before exiting.</span></span> <span data-ttu-id="7a01e-191">Deze functies zijn gedefinieerd in het platform.h header-bestand.</span><span class="sxs-lookup"><span data-stu-id="7a01e-191">These functions are declared in the platform.h header file.</span></span> <span data-ttu-id="7a01e-192">Bekijk de definities van deze functies voor uw doelplatform in de [opslagplaats](https://github.com/Azure/azure-iot-sdk-c) om te bepalen of u moet de van de platform-specifieke initialisatiecode opnemen in de client.</span><span class="sxs-lookup"><span data-stu-id="7a01e-192">Examine the definitions of these functions for your target platform in the [repository](https://github.com/Azure/azure-iot-sdk-c) to determine whether you need to include any platform-specific initialization code in your client.</span></span>

<span data-ttu-id="7a01e-193">Als u wilt werken met de bibliotheken, moet u eerst een IoT Hub client ingang toewijzen:</span><span class="sxs-lookup"><span data-stu-id="7a01e-193">To start working with the libraries, first allocate an IoT Hub client handle:</span></span>

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

<span data-ttu-id="7a01e-194">U doorgeven een kopie van de apparaat-verbindingsreeks die u hebt verkregen via het programma voor apparaat explorer aan deze functie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-194">You pass a copy of the device connection string you obtained from the device explorer tool to this function.</span></span> <span data-ttu-id="7a01e-195">U ook opgeven de te gebruiken communicatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="7a01e-195">You also designate the communications protocol to use.</span></span> <span data-ttu-id="7a01e-196">In dit voorbeeld wordt MQTT maar AMQP en HTTP zijn ook opties.</span><span class="sxs-lookup"><span data-stu-id="7a01e-196">This example uses MQTT, but AMQP and HTTP are also options.</span></span>

<span data-ttu-id="7a01e-197">Wanneer u hebt een geldige **IOTHUB\_CLIENT\_verwerken**, kunt u beginnen met het aanroepen van de API's om te verzenden en ontvangen van berichten naar en van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-197">When you have a valid **IOTHUB\_CLIENT\_HANDLE**, you can start calling the APIs to send and receive messages to and from IoT Hub.</span></span>

### <a name="send-messages"></a><span data-ttu-id="7a01e-198">Berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="7a01e-198">Send messages</span></span>

<span data-ttu-id="7a01e-199">De voorbeeldtoepassing stelt een lus berichten verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-199">The sample application sets up a loop to send messages to your IoT hub.</span></span> <span data-ttu-id="7a01e-200">Het volgende codefragment:</span><span class="sxs-lookup"><span data-stu-id="7a01e-200">The following snippet:</span></span>

- <span data-ttu-id="7a01e-201">Hiermee maakt u een bericht.</span><span class="sxs-lookup"><span data-stu-id="7a01e-201">Creates a message.</span></span>
- <span data-ttu-id="7a01e-202">Voegt een eigenschap toe aan het bericht.</span><span class="sxs-lookup"><span data-stu-id="7a01e-202">Adds a property to the message.</span></span>
- <span data-ttu-id="7a01e-203">Verzendt een bericht.</span><span class="sxs-lookup"><span data-stu-id="7a01e-203">Sends a message.</span></span>

<span data-ttu-id="7a01e-204">Maak eerst een bericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7a01e-204">First, create a message:</span></span>

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
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission to IoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

<span data-ttu-id="7a01e-205">Telkens wanneer u een bericht verzendt, Geef een verwijzing naar een callbackfunctie die wordt aangeroepen wanneer de gegevens worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="7a01e-205">Every time you send a message, you specify a reference to a callback function that's invoked when the data is sent.</span></span> <span data-ttu-id="7a01e-206">In dit voorbeeld wordt de callbackfunctie wordt aangeroepen **SendConfirmationCallback**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-206">In this example, the callback function is called **SendConfirmationCallback**.</span></span> <span data-ttu-id="7a01e-207">Het volgende fragment toont deze callback-functie:</span><span class="sxs-lookup"><span data-stu-id="7a01e-207">The following snippet shows this callback function:</span></span>

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

<span data-ttu-id="7a01e-208">Let op de aanroep van de **IoTHubMessage\_vernietigen** wanneer u klaar bent met het bericht.</span><span class="sxs-lookup"><span data-stu-id="7a01e-208">Note the call to the **IoTHubMessage\_Destroy** function when you're done with the message.</span></span> <span data-ttu-id="7a01e-209">Deze functie maakt tijdens het maken van het bericht toegewezen resources vrij.</span><span class="sxs-lookup"><span data-stu-id="7a01e-209">This function frees the resources allocated when you created the message.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="7a01e-210">Berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="7a01e-210">Receive messages</span></span>

<span data-ttu-id="7a01e-211">Het bericht is een asynchrone bewerking.</span><span class="sxs-lookup"><span data-stu-id="7a01e-211">Receiving a message is an asynchronous operation.</span></span> <span data-ttu-id="7a01e-212">Ten eerste kunt u de callback om aan te roepen wanneer het apparaat een bericht ontvangt registreren:</span><span class="sxs-lookup"><span data-stu-id="7a01e-212">First, you register the callback to invoke when the device receives a message:</span></span>

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

<span data-ttu-id="7a01e-213">De laatste parameter is een ongeldig aanwijzer naar elke gewenste.</span><span class="sxs-lookup"><span data-stu-id="7a01e-213">The last parameter is a void pointer to whatever you want.</span></span> <span data-ttu-id="7a01e-214">In het voorbeeld is een verwijzing naar een geheel getal, maar wordt een verwijzing naar een complexere gegevensstructuur.</span><span class="sxs-lookup"><span data-stu-id="7a01e-214">In the sample, it's a pointer to an integer but it could be a pointer to a more complex data structure.</span></span> <span data-ttu-id="7a01e-215">Deze parameter kunt de functie voor retouraanroepen bewerkingen uitvoeren op gedeelde staat met de aanroeper van deze functie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-215">This parameter enables the callback function to operate on shared state with the caller of this function.</span></span>

<span data-ttu-id="7a01e-216">Wanneer het apparaat een bericht ontvangt, wordt de geregistreerde callback-functie wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-216">When the device receives a message, the registered callback function is invoked.</span></span> <span data-ttu-id="7a01e-217">Deze functie voor retouraanroepen opgehaald:</span><span class="sxs-lookup"><span data-stu-id="7a01e-217">This callback function retrieves:</span></span>

* <span data-ttu-id="7a01e-218">De bericht-id en de correlatie-id van het bericht.</span><span class="sxs-lookup"><span data-stu-id="7a01e-218">The message id and correlation id from the message.</span></span>
* <span data-ttu-id="7a01e-219">De inhoud van het bericht.</span><span class="sxs-lookup"><span data-stu-id="7a01e-219">The message content.</span></span>
* <span data-ttu-id="7a01e-220">Alle aangepaste eigenschappen van het bericht.</span><span class="sxs-lookup"><span data-stu-id="7a01e-220">Any custom properties from the message.</span></span>

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
        (void)printf("unable to retrieve the message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive the work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from the message
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

<span data-ttu-id="7a01e-221">Gebruik de **IoTHubMessage\_GetByteArray** functie voor het ophalen van het bericht dat in dit voorbeeld een tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="7a01e-221">Use the **IoTHubMessage\_GetByteArray** function to retrieve the message, which in this example is a string.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="7a01e-222">Initialisatie van de bibliotheek</span><span class="sxs-lookup"><span data-stu-id="7a01e-222">Uninitialize the library</span></span>

<span data-ttu-id="7a01e-223">Wanneer u gebeurtenissen verzenden en ontvangen berichten bent klaar, kunt u initialisatie van de IoT-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7a01e-223">When you're done sending events and receiving messages, you can uninitialize the IoT library.</span></span> <span data-ttu-id="7a01e-224">Voert de volgende functie-oproep om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="7a01e-224">To do so, issue the following function call:</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="7a01e-225">Deze aanroep is vrijgemaakt van de resources die eerder zijn toegewezen door de **IoTHubClient\_CreateFromConnectionString** functie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-225">This call frees up the resources previously allocated by the **IoTHubClient\_CreateFromConnectionString** function.</span></span>

<span data-ttu-id="7a01e-226">Zoals u ziet, is het eenvoudig verzenden en ontvangen berichten met de **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7a01e-226">As you can see, it's easy to send and receive messages with the **IoTHubClient** library.</span></span> <span data-ttu-id="7a01e-227">De bibliotheek verwerkt de details van de communicatie met IoT Hub, met inbegrip van de te gebruiken protocol (vanuit het perspectief van de ontwikkelaar, is dit een eenvoudige configuratieoptie).</span><span class="sxs-lookup"><span data-stu-id="7a01e-227">The library handles the details of communicating with IoT Hub, including which protocol to use (from the perspective of the developer, this is a simple configuration option).</span></span>

<span data-ttu-id="7a01e-228">De **IoTHubClient** bibliotheek biedt ook nauwkeurige controle over hoe u voor het serialiseren van de gegevens die uw apparaat met IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="7a01e-228">The **IoTHubClient** library also provides precise control over how to serialize the data your device sends to IoT Hub.</span></span> <span data-ttu-id="7a01e-229">In sommige gevallen is dit niveau van controle een voordeel, maar er is een implementatie details die u niet wilt betrokken zijn bij.</span><span class="sxs-lookup"><span data-stu-id="7a01e-229">In some cases this level of control is an advantage, but in others it is an implementation detail that you don't want to be concerned with.</span></span> <span data-ttu-id="7a01e-230">Als dit het geval is, kunt u met behulp van de **serialisatiefunctie** bibliotheek, die in de volgende sectie wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="7a01e-230">If that's the case, you might consider using the **serializer** library, which is described in the next section.</span></span>

## <a name="use-the-serializer-library"></a><span data-ttu-id="7a01e-231">Gebruik de serialisatiefunctie-bibliotheek</span><span class="sxs-lookup"><span data-stu-id="7a01e-231">Use the serializer library</span></span>

<span data-ttu-id="7a01e-232">Conceptueel gezien de **serialisatiefunctie** bibliotheek bevindt zich boven de **IoTHubClient** bibliotheek in de SDK.</span><span class="sxs-lookup"><span data-stu-id="7a01e-232">Conceptually the **serializer** library sits on top of the **IoTHubClient** library in the SDK.</span></span> <span data-ttu-id="7a01e-233">Dit maakt gebruik van de **IoTHubClient** -bibliotheek voor de onderliggende communicatie met IoT Hub, maar het voegt modellering mogelijkheden die de last van omgaan met bericht serialisatie van de ontwikkelaar verwijderen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-233">It uses the **IoTHubClient** library for the underlying communication with IoT Hub, but it adds modeling capabilities that remove the burden of dealing with message serialization from the developer.</span></span> <span data-ttu-id="7a01e-234">Hoe deze bibliotheek werkt best wordt geïllustreerd door een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7a01e-234">How this library works is best demonstrated by an example.</span></span>

<span data-ttu-id="7a01e-235">In de **serialisatiefunctie** map in de [azure-iot-sdk-c-opslagplaats](https://github.com/Azure/azure-iot-sdk-c), is een **voorbeelden** map waarin een toepassing met de naam **simplesample\_mqtt**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-235">Inside the **serializer** folder in the [azure-iot-sdk-c repository](https://github.com/Azure/azure-iot-sdk-c), is a **samples** folder that contains an application called **simplesample\_mqtt**.</span></span> <span data-ttu-id="7a01e-236">De Windows-versie van dit voorbeeld bevat de volgende Visual Studio-oplossing:</span><span class="sxs-lookup"><span data-stu-id="7a01e-236">The Windows version of this sample includes the following Visual Studio solution:</span></span>

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> <span data-ttu-id="7a01e-237">Als u dit project in Visual Studio 2017 opent, accepteert u de aanwijzingen voor het stelt u het project naar de nieuwste versie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-237">If you open this project in Visual Studio 2017, accept the prompts to retarget the project to the latest version.</span></span>

<span data-ttu-id="7a01e-238">Net als bij het vorige voorbeeld, bevat deze een enkele NuGet-pakketten:</span><span class="sxs-lookup"><span data-stu-id="7a01e-238">As with the previous sample, this one includes several NuGet packages:</span></span>

* <span data-ttu-id="7a01e-239">Microsoft.Azure.C.SharedUtility</span><span class="sxs-lookup"><span data-stu-id="7a01e-239">Microsoft.Azure.C.SharedUtility</span></span>
* <span data-ttu-id="7a01e-240">Microsoft.Azure.IoTHub.MqttTransport</span><span class="sxs-lookup"><span data-stu-id="7a01e-240">Microsoft.Azure.IoTHub.MqttTransport</span></span>
* <span data-ttu-id="7a01e-241">Microsoft.Azure.IoTHub.IoTHubClient</span><span class="sxs-lookup"><span data-stu-id="7a01e-241">Microsoft.Azure.IoTHub.IoTHubClient</span></span>
* <span data-ttu-id="7a01e-242">Microsoft.Azure.IoTHub.Serializer</span><span class="sxs-lookup"><span data-stu-id="7a01e-242">Microsoft.Azure.IoTHub.Serializer</span></span>
* <span data-ttu-id="7a01e-243">Microsoft.Azure.umqtt</span><span class="sxs-lookup"><span data-stu-id="7a01e-243">Microsoft.Azure.umqtt</span></span>

<span data-ttu-id="7a01e-244">U kunt de meeste van deze pakketten in het vorige voorbeeld hebt gezien, maar **Microsoft.Azure.IoTHub.Serializer** is er nieuw.</span><span class="sxs-lookup"><span data-stu-id="7a01e-244">You've seen most of these packages in the previous sample, but **Microsoft.Azure.IoTHub.Serializer** is new.</span></span> <span data-ttu-id="7a01e-245">Dit pakket is vereist wanneer u de **serialisatiefunctie** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7a01e-245">This package is required when you use the **serializer** library.</span></span>

<span data-ttu-id="7a01e-246">U vindt de uitvoering van de voorbeeldtoepassing in de **simplesample\_mqtt.c** bestand.</span><span class="sxs-lookup"><span data-stu-id="7a01e-246">You can find the implementation of the sample application in the **simplesample\_mqtt.c** file.</span></span>

<span data-ttu-id="7a01e-247">De volgende secties vindt u via de belangrijkste onderdelen van dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7a01e-247">The following sections walk you through the key parts of this sample.</span></span>

### <a name="initialize-the-library"></a><span data-ttu-id="7a01e-248">De bibliotheek initialiseren</span><span class="sxs-lookup"><span data-stu-id="7a01e-248">Initialize the library</span></span>

<span data-ttu-id="7a01e-249">Aan de slag met de **serialisatiefunctie** bibliotheek, aanroepen van de initialisatie van de API's:</span><span class="sxs-lookup"><span data-stu-id="7a01e-249">To start working with the **serializer** library, call the initialization APIs:</span></span>

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

<span data-ttu-id="7a01e-250">De aanroep van de **serialisatiefunctie\_init** functie is een eenmalige aanroep en de onderliggende bibliotheek wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="7a01e-250">The call to the **serializer\_init** function is a one-time call and initializes the underlying library.</span></span> <span data-ttu-id="7a01e-251">Roep vervolgens de **IoTHubClient\_LLE\_CreateFromConnectionString** functie, die is de API hetzelfde als in de **IoTHubClient** voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7a01e-251">Then, you call the **IoTHubClient\_LL\_CreateFromConnectionString** function, which is the same API as in the **IoTHubClient** sample.</span></span> <span data-ttu-id="7a01e-252">Deze aanroep Hiermee stelt u de verbindingsreeks van uw apparaat (deze aanroep is ook waar u het protocol kiest u wilt gebruiken).</span><span class="sxs-lookup"><span data-stu-id="7a01e-252">This call sets your device connection string (this call is also where you choose the protocol you want to use).</span></span> <span data-ttu-id="7a01e-253">Dit voorbeeld MQTT als het transport gebruikt, maar kan AMQP of HTTP gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a01e-253">This sample uses MQTT as the transport, but could use AMQP or HTTP.</span></span>

<span data-ttu-id="7a01e-254">Tenslotte roept de **maken\_MODEL\_exemplaar** functie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-254">Finally, call the **CREATE\_MODEL\_INSTANCE** function.</span></span> <span data-ttu-id="7a01e-255">**WeatherStation** is de naamruimte van het model en **ContosoAnemometer** is de naam van het model.</span><span class="sxs-lookup"><span data-stu-id="7a01e-255">**WeatherStation** is the namespace of the model and **ContosoAnemometer** is the name of the model.</span></span> <span data-ttu-id="7a01e-256">Zodra de model-exemplaar is gemaakt, kunt u het verzenden en ontvangen van berichten.</span><span class="sxs-lookup"><span data-stu-id="7a01e-256">Once the model instance is created, you can use it to start sending and receiving messages.</span></span> <span data-ttu-id="7a01e-257">Het is echter belangrijk om te begrijpen wat een model is.</span><span class="sxs-lookup"><span data-stu-id="7a01e-257">However, it's important to understand what a model is.</span></span>

### <a name="define-the-model"></a><span data-ttu-id="7a01e-258">Het model definiëren</span><span class="sxs-lookup"><span data-stu-id="7a01e-258">Define the model</span></span>

<span data-ttu-id="7a01e-259">Een model in de **serialisatiefunctie** bibliotheek definieert de berichten die uw apparaat met IoT Hub verzenden kunt en de berichten, zogenaamde *acties* in de modelleertaal die het kan ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-259">A model in the **serializer** library defines the messages that your device can send to IoT Hub and the messages, called *actions* in the modeling language, which it can receive.</span></span> <span data-ttu-id="7a01e-260">U definieert een model met behulp van een set van C macro's als in de **simplesample\_mqtt** voorbeeldtoepassing:</span><span class="sxs-lookup"><span data-stu-id="7a01e-260">You define a model using a set of C macros as in the **simplesample\_mqtt** sample application:</span></span>

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

<span data-ttu-id="7a01e-261">De **BEGINT\_NAAMRUIMTE** en **END\_NAAMRUIMTE** macro's zowel de naamruimte van het model als een argument nemen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-261">The **BEGIN\_NAMESPACE** and **END\_NAMESPACE** macros both take the namespace of the model as an argument.</span></span> <span data-ttu-id="7a01e-262">Verwacht wordt dat alles tussen deze macro's is de definitie van het model of modellen en de gegevensstructuren die de modellen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a01e-262">It's expected that anything between these macros is the definition of your model or models, and the data structures that the models use.</span></span>

<span data-ttu-id="7a01e-263">In dit voorbeeld is een enkelvoudig model aangeroepen **ContosoAnemometer**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-263">In this example, there is a single model called **ContosoAnemometer**.</span></span> <span data-ttu-id="7a01e-264">Dit model definieert twee soorten gegevens waarmee u uw apparaat met IoT Hub verzenden kunt: **DeviceId** en **windsnelheid**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-264">This model defines two pieces of data that your device can send to IoT Hub: **DeviceId** and **WindSpeed**.</span></span> <span data-ttu-id="7a01e-265">Definieert ook drie acties (berichten) die het apparaat kan ontvangen: **TurnFanOn**, **TurnFanOff**, en **SetAirResistance**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-265">It also defines three actions (messages) that your device can receive: **TurnFanOn**, **TurnFanOff**, and **SetAirResistance**.</span></span> <span data-ttu-id="7a01e-266">Elk gegevenselement in de heeft een type en elke actie heeft een naam (en desgewenst een set parameters).</span><span class="sxs-lookup"><span data-stu-id="7a01e-266">Each data element has a type, and each action has a name (and optionally a set of parameters).</span></span>

<span data-ttu-id="7a01e-267">De gegevens en acties die zijn gedefinieerd in het model definiëren een API-gebied die u kunt gebruiken voor het verzenden van berichten naar IoT Hub en reageren op berichten die naar het apparaat verzonden.</span><span class="sxs-lookup"><span data-stu-id="7a01e-267">The data and actions defined in the model define an API surface that you can use to send messages to IoT Hub, and respond to messages sent to the device.</span></span> <span data-ttu-id="7a01e-268">Door een voorbeeld van het gebruik van dit model best begrijpen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-268">Use of this model is best understood through an example.</span></span>

### <a name="send-messages"></a><span data-ttu-id="7a01e-269">Berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="7a01e-269">Send messages</span></span>

<span data-ttu-id="7a01e-270">Het model definieert de gegevens die u met IoT Hub verzenden kunt.</span><span class="sxs-lookup"><span data-stu-id="7a01e-270">The model defines the data you can send to IoT Hub.</span></span> <span data-ttu-id="7a01e-271">In dit voorbeeld dat betekent een van de twee gegevensitems gedefinieerd met behulp van de **WITH_DATA** macro.</span><span class="sxs-lookup"><span data-stu-id="7a01e-271">In this example, that means one of the two data items defined using the **WITH_DATA** macro.</span></span> <span data-ttu-id="7a01e-272">Er zijn verschillende stappen nodig om te verzenden **DeviceId** en **windsnelheid** waarden naar een iothub.</span><span class="sxs-lookup"><span data-stu-id="7a01e-272">There are several steps required to send **DeviceId** and **WindSpeed** values to an IoT hub.</span></span> <span data-ttu-id="7a01e-273">De eerste is het instellen van de gegevens die u wilt verzenden:</span><span class="sxs-lookup"><span data-stu-id="7a01e-273">The first is to set the data you want to send:</span></span>

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

<span data-ttu-id="7a01e-274">Het model dat u eerder hebt gedefinieerd, kunt u de waarden instellen door leden van een **struct**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-274">The model you defined earlier enables you to set the values by setting members of a **struct**.</span></span> <span data-ttu-id="7a01e-275">Vervolgens serialiseren het bericht dat u wilt verzenden:</span><span class="sxs-lookup"><span data-stu-id="7a01e-275">Next, serialize the message you want to send:</span></span>

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed to serialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

<span data-ttu-id="7a01e-276">Deze code de apparaat-naar-cloud naar een buffer serialiseert (waarnaar wordt verwezen door **bestemming**).</span><span class="sxs-lookup"><span data-stu-id="7a01e-276">This code serializes the device-to-cloud to a buffer (referenced by **destination**).</span></span> <span data-ttu-id="7a01e-277">De code roept vervolgens de **sendMessage** functie het bericht te verzenden naar IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="7a01e-277">The code then invokes the **sendMessage** function to send the message to IoT Hub:</span></span>

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable to create a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed to hand over the message to IoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted the message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


<span data-ttu-id="7a01e-278">De tweede op de laatste parameter van **IoTHubClient\_LLE\_SendEventAsync** is een verwijzing naar een callback-functie die wordt aangeroepen wanneer de gegevens is verzonden.</span><span class="sxs-lookup"><span data-stu-id="7a01e-278">The second to last parameter of **IoTHubClient\_LL\_SendEventAsync** is a reference to a callback function that's called when the data is successfully sent.</span></span> <span data-ttu-id="7a01e-279">Hier volgt de callback-functie in de steekproef:</span><span class="sxs-lookup"><span data-stu-id="7a01e-279">Here's the callback function in the sample:</span></span>

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

<span data-ttu-id="7a01e-280">De tweede parameter is een aanwijzer naar gebruikerscontext; de aanwijzer dezelfde doorgegeven aan **IoTHubClient\_LLE\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-280">The second parameter is a pointer to user context; the same pointer passed to **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="7a01e-281">In dit geval de context is een eenvoudige Prestatiemeter gebruiken, maar dit alles kan zijn.</span><span class="sxs-lookup"><span data-stu-id="7a01e-281">In this case, the context is a simple counter, but it can be anything you want.</span></span>

<span data-ttu-id="7a01e-282">Dit is alles wat er is naar het verzenden van apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="7a01e-282">That's all there is to sending device-to-cloud messages.</span></span> <span data-ttu-id="7a01e-283">Het enige dat links ten aanzien van is berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-283">The only thing left to cover is how to receive messages.</span></span>

### <a name="receive-messages"></a><span data-ttu-id="7a01e-284">Berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="7a01e-284">Receive messages</span></span>

<span data-ttu-id="7a01e-285">Ontvangen een bericht werkt op dezelfde manier naar de berichten manier werken in de **IoTHubClient** bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="7a01e-285">Receiving a message works similarly to the way messages work in the **IoTHubClient** library.</span></span> <span data-ttu-id="7a01e-286">U registreert eerst een callback-functie van het bericht:</span><span class="sxs-lookup"><span data-stu-id="7a01e-286">First, you register a message callback function:</span></span>

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable to IoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

<span data-ttu-id="7a01e-287">U schrijft vervolgens de callbackfunctie die wordt aangeroepen wanneer een bericht wordt ontvangen:</span><span class="sxs-lookup"><span data-stu-id="7a01e-287">Then, you write the callback function that's invoked when a message is received:</span></span>

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
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

<span data-ttu-id="7a01e-288">Deze code is standaardtekst--hetzelfde is voor een oplossing.</span><span class="sxs-lookup"><span data-stu-id="7a01e-288">This code is boilerplate -- it's the same for any solution.</span></span> <span data-ttu-id="7a01e-289">Deze functie het bericht ontvangt, en zorgt voor de routering naar de betreffende functie via de aanroep van de het **EXECUTE\_opdracht**.</span><span class="sxs-lookup"><span data-stu-id="7a01e-289">This function receives the message and takes care of routing it to the appropriate function through the call to **EXECUTE\_COMMAND**.</span></span> <span data-ttu-id="7a01e-290">De aangeroepen functie is op dit moment hangt af van de definitie van de acties in uw model.</span><span class="sxs-lookup"><span data-stu-id="7a01e-290">The function called at this point depends on the definition of the actions in your model.</span></span>

<span data-ttu-id="7a01e-291">Wanneer u een actie in het model definieert, bent u verplicht voor het implementeren van een functie die wordt aangeroepen wanneer het apparaat het bijbehorende bericht ontvangt.</span><span class="sxs-lookup"><span data-stu-id="7a01e-291">When you define an action in your model, you're required to implement a function that's called when your device receives the corresponding message.</span></span> <span data-ttu-id="7a01e-292">Bijvoorbeeld, als het model is gedefinieerd met deze actie:</span><span class="sxs-lookup"><span data-stu-id="7a01e-292">For example, if your model defines this action:</span></span>

```c
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="7a01e-293">Een functie met deze handtekening definiëren:</span><span class="sxs-lookup"><span data-stu-id="7a01e-293">Define a function with this signature:</span></span>

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="7a01e-294">Houd er rekening mee hoe de naam van de functie overeenkomt met de naam van de actie in het model en dat de parameters van de functie overeenkomen met de opgegeven parameters voor de actie.</span><span class="sxs-lookup"><span data-stu-id="7a01e-294">Note how the name of the function matches the name of the action in the model and that the parameters of the function match the parameters specified for the action.</span></span> <span data-ttu-id="7a01e-295">De eerste parameter is altijd vereist en bevat een verwijzing naar het exemplaar van het model.</span><span class="sxs-lookup"><span data-stu-id="7a01e-295">The first parameter is always required and contains a pointer to the instance of your model.</span></span>

<span data-ttu-id="7a01e-296">Wanneer het apparaat een bericht dat overeenkomt met deze handtekening ontvangt, wordt de overeenkomende functie is aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7a01e-296">When the device receives a message that matches this signature, the corresponding function is called.</span></span> <span data-ttu-id="7a01e-297">Daarom in combinatie met de code van de standaardtekst opnemen **IoTHubMessage**, ontvangen van berichten is slechts een kwestie van het definiëren van een eenvoudige functie voor elke actie in het model is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="7a01e-297">Therefore, aside from having to include the boilerplate code from **IoTHubMessage**, receiving messages is just a matter of defining a simple function for each action defined in your model.</span></span>

### <a name="uninitialize-the-library"></a><span data-ttu-id="7a01e-298">Initialisatie van de bibliotheek</span><span class="sxs-lookup"><span data-stu-id="7a01e-298">Uninitialize the library</span></span>

<span data-ttu-id="7a01e-299">Wanneer u klaar bent met het verzenden van gegevens en berichten ontvangt kunt u initialisatie van de IoT-bibliotheek:</span><span class="sxs-lookup"><span data-stu-id="7a01e-299">When you're done sending data and receiving messages, you can uninitialize the IoT library:</span></span>

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

<span data-ttu-id="7a01e-300">Elk van deze drie functies wordt uitgelijnd met de drie initialisatie van de functies die eerder zijn beschreven.</span><span class="sxs-lookup"><span data-stu-id="7a01e-300">Each of these three functions aligns with the three initialization functions described previously.</span></span> <span data-ttu-id="7a01e-301">Het aanroepen van deze API's zorgt ervoor dat u eerder toegewezen resources vrij.</span><span class="sxs-lookup"><span data-stu-id="7a01e-301">Calling these APIs ensures that you free previously allocated resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a01e-302">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a01e-302">Next Steps</span></span>

<span data-ttu-id="7a01e-303">In dit artikel de basisbeginselen van het gebruik van de bibliotheken in waarvoor de **Azure IoT-device SDK voor C**. Dit u geleverd met voldoende gegevens om te begrijpen wat opgenomen in de SDK, de architectuur en hoe u aan de slag met de Windows-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="7a01e-303">This article covered the basics of using the libraries in the **Azure IoT device SDK for C**. It provided you with enough information to understand what's included in the SDK, its architecture, and how to get started working with the Windows samples.</span></span> <span data-ttu-id="7a01e-304">Het volgende artikel blijft de beschrijving van de SDK door uitleg over [meer informatie over de bibliotheek IoTHubClient](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="7a01e-304">The next article continues the description of the SDK by explaining [more about the IoTHubClient library](iot-hub-device-sdk-c-iothubclient.md).</span></span>

<span data-ttu-id="7a01e-305">Zie voor meer informatie over het ontwikkelen voor IoT Hub, de [Azure IoT SDK's][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="7a01e-305">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="7a01e-306">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="7a01e-306">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="7a01e-307">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="7a01e-307">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
