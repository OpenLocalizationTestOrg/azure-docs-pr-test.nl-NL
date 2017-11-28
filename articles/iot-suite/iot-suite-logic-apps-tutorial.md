---
title: aaaAzure IoT Suite en Logic Apps | Microsoft Docs
description: Een zelfstudie over het toohook van Logic Apps tooAzure IoT Suite voor bedrijfsproces.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 4629a7af-56ca-4b21-a769-5fa18bc3ab07
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: corywink
ms.openlocfilehash: 6ef7311ac38f4e2ddb032cff0fb73591da5f76c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-connect-logic-app-tooyour-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ea43a-103">Zelfstudie: Logische App tooyour Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing verbinden</span><span class="sxs-lookup"><span data-stu-id="ea43a-103">Tutorial: Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="ea43a-104">Hallo [Microsoft Azure IoT Suite] [ lnk-internetofthings] vooraf geconfigureerde oplossing voor externe controle is een uitstekende manier tooget snel de slag met een end-to-end-functieset die verklaart de IoT-oplossing.</span><span class="sxs-lookup"><span data-stu-id="ea43a-104">hello [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way tooget started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="ea43a-105">Deze zelfstudie leert u hoe tooadd logische App tooyour Microsoft Azure IoT Suite remote monitoring vooraf oplossing geconfigureerde.</span><span class="sxs-lookup"><span data-stu-id="ea43a-105">This tutorial walks you through how tooadd Logic App tooyour Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="ea43a-106">Deze stappen laten zien hoe u uw IoT-oplossing nog verder door verbinding te maken dit bedrijfsproces tooa kunt nemen.</span><span class="sxs-lookup"><span data-stu-id="ea43a-106">These steps demonstrate how you can take your IoT solution even further by connecting it tooa business process.</span></span>

<span data-ttu-id="ea43a-107">*Als u een overzicht over hoe een externe controle tooprovision vooraf oplossing geconfigureerde zoekt, Zie [zelfstudie: aan de slag met vooraf geconfigureerde IoT-oplossingen Hallo][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="ea43a-107">*If you’re looking for a walkthrough on how tooprovision a remote monitoring preconfigured solution, see [Tutorial: Get started with hello IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="ea43a-108">Voordat u deze zelfstudie begint, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="ea43a-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="ea43a-109">Inrichten Hallo externe controle vooraf geconfigureerde oplossing in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ea43a-109">Provision hello remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="ea43a-110">Maken van een account SendGrid tooenable toosend een e-mailbericht uw bedrijfsproces activeert.</span><span class="sxs-lookup"><span data-stu-id="ea43a-110">Create a SendGrid account tooenable you toosend an email that triggers your business process.</span></span> <span data-ttu-id="ea43a-111">U kunt zich aanmelden voor een gratis proefaccount op [SendGrid](https://sendgrid.com/) door te klikken op **Probeer gratis**.</span><span class="sxs-lookup"><span data-stu-id="ea43a-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="ea43a-112">Nadat u hebt geregistreerd voor een gratis proefversie account, moet u toocreate een [API-sleutel](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid die machtigingen toosend mail verleent.</span><span class="sxs-lookup"><span data-stu-id="ea43a-112">After you have registered for your free trial account, you need toocreate an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions toosend mail.</span></span> <span data-ttu-id="ea43a-113">Deze API-sleutel moet u later in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="ea43a-113">You need this API key later in hello tutorial.</span></span>

<span data-ttu-id="ea43a-114">toocomplete in deze zelfstudie, moet u Visual Studio 2015 of Visual Studio 2017 toomodify Hallo-acties in Hallo vooraf geconfigureerde oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="ea43a-114">toocomplete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 toomodify hello actions in hello preconfigured solution back end.</span></span>

<span data-ttu-id="ea43a-115">Ervan uitgaande dat u al hebt ingericht uw externe controle vooraf geconfigureerde oplossing, gaat u de resourcegroep toohello voor deze oplossing in Hallo [Azure-portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="ea43a-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate toohello resource group for that solution in hello [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="ea43a-116">Hallo resourcegroep heeft Hallo dezelfde naam als hello oplossing servernaam die u hebt gekozen wanneer u uw oplossing voor externe controle ingericht.</span><span class="sxs-lookup"><span data-stu-id="ea43a-116">hello resource group has hello same name as hello solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ea43a-117">In de resourcegroep hello ziet u alle hello Azure-resources voor uw oplossing, met uitzondering van Azure Active Directory-toepassing die u in de klassieke Azure-Portal Hallo vinden kunt Hallo ingericht.</span><span class="sxs-lookup"><span data-stu-id="ea43a-117">In hello resource group, you can see all hello provisioned Azure resources for your solution except for hello Azure Active Directory application that you can find in hello Azure Classic Portal.</span></span> <span data-ttu-id="ea43a-118">Hallo volgende schermafbeelding ziet u een voorbeeld **resourcegroep** blade voor een externe controle vooraf geconfigureerde oplossing:</span><span class="sxs-lookup"><span data-stu-id="ea43a-118">hello following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="ea43a-119">toobegin, instellen van de Hallo logic app toouse Hello vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="ea43a-119">toobegin, set up hello logic app toouse with hello preconfigured solution.</span></span>

## <a name="set-up-hello-logic-app"></a><span data-ttu-id="ea43a-120">Hallo logische App instellen</span><span class="sxs-lookup"><span data-stu-id="ea43a-120">Set up hello Logic App</span></span>
1. <span data-ttu-id="ea43a-121">Klik op **toevoegen** Hallo boven aan de blade met resourcegroepen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ea43a-121">Click **Add** at hello top of your resource group blade in hello Azure portal.</span></span>
2. <span data-ttu-id="ea43a-122">Zoeken naar **logische App**, selecteert u deze en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ea43a-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="ea43a-123">Hallo invullen **naam** en gebruik dezelfde Hallo **abonnement** en **resourcegroep** die u hebt gebruikt bij het inrichten van uw oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="ea43a-123">Fill out hello **Name** and use hello same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="ea43a-124">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea43a-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="ea43a-125">Wanneer uw implementatie is voltooid, ziet u Hallo die logische App wordt vermeld als een resource in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ea43a-125">When your deployment completes, you can see hello Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="ea43a-126">Klik op Hallo logische App toonavigate toohello logische App blade Selecteer Hallo **lege logische App** sjabloon tooopen hello **Logic Apps Designer**.</span><span class="sxs-lookup"><span data-stu-id="ea43a-126">Click hello Logic App toonavigate toohello Logic App blade, select hello **Blank Logic App** template tooopen hello **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="ea43a-127">Selecteer **aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="ea43a-127">Select **Request**.</span></span> <span data-ttu-id="ea43a-128">Deze actie geeft aan dat een inkomende HTTP-aanvraag met een specifieke JSON nettolading handelingen als een trigger opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="ea43a-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="ea43a-129">Plak de volgende code in de aanvraag hoofdtekst JSON-Schema Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="ea43a-129">Paste hello following code into hello Request Body JSON Schema:</span></span>
   
    ```json
    {
      "$schema": "http://json-schema.org/draft-04/schema#",
      "id": "/",
      "properties": {
        "DeviceId": {
          "id": "DeviceId",
          "type": "string"
        },
        "measuredValue": {
          "id": "measuredValue",
          "type": "integer"
        },
        "measurementName": {
          "id": "measurementName",
          "type": "string"
        }
      },
      "required": [
        "DeviceId",
        "measurementName",
        "measuredValue"
      ],
      "type": "object"
    }
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ea43a-130">Nadat u opslaan Hallo logische app, maar u moet eerst een actie toevoegen, kunt u Hallo-URL voor Hallo HTTP post kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ea43a-130">You can copy hello URL for hello HTTP post after you save hello logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="ea43a-131">Klik op **+ een nieuwe stap** onder de handmatige trigger.</span><span class="sxs-lookup"><span data-stu-id="ea43a-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="ea43a-132">Klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ea43a-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="ea43a-133">Zoeken naar **SendGrid - e-mailbericht verzenden** en klik erop.</span><span class="sxs-lookup"><span data-stu-id="ea43a-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="ea43a-134">Voer een naam voor de verbinding hello, zoals **SendGridConnection**, Voer Hallo **SendGrid-API-sleutel** u gemaakt wanneer u uw SendGrid-account instellen en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="ea43a-134">Enter a name for hello connection, such as **SendGridConnection**, enter hello **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="ea43a-135">Toevoegen van e-mailadressen u eigen tooboth hello **van** en **naar** velden.</span><span class="sxs-lookup"><span data-stu-id="ea43a-135">Add email addresses you own tooboth hello **From** and **To** fields.</span></span> <span data-ttu-id="ea43a-136">Voeg **externe controle waarschuwing [DeviceId]** toohello **onderwerp** veld.</span><span class="sxs-lookup"><span data-stu-id="ea43a-136">Add **Remote monitoring alert [DeviceId]** toohello **Subject** field.</span></span> <span data-ttu-id="ea43a-137">In Hallo **hoofdtekst van de E-mail** veld, het toevoegen van **apparaat [DeviceId] [measurementName] met de waarde [measuredValue] heeft gerapporteerd.**</span><span class="sxs-lookup"><span data-stu-id="ea43a-137">In hello **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="ea43a-138">U kunt toevoegen **[DeviceId]**, **[measurementName]**, en **[measuredValue]** door te klikken in Hallo **kunt u gegevens uit de vorige stappen**sectie.</span><span class="sxs-lookup"><span data-stu-id="ea43a-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in hello **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="ea43a-139">Klik op **opslaan** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="ea43a-139">Click **Save** in hello top menu.</span></span>
13. <span data-ttu-id="ea43a-140">Klik op Hallo **aanvragen** trigger en kopieer Hallo **Http Post toothis URL** waarde.</span><span class="sxs-lookup"><span data-stu-id="ea43a-140">Click hello **Request** trigger and copy hello **Http Post toothis URL** value.</span></span> <span data-ttu-id="ea43a-141">U moet deze URL verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ea43a-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="ea43a-142">Logic Apps kunnen u toorun [veel verschillende soorten actie] [ lnk-logic-apps-actions] met inbegrip van acties in Office 365.</span><span class="sxs-lookup"><span data-stu-id="ea43a-142">Logic Apps enable you toorun [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-hello-eventprocessor-web-job"></a><span data-ttu-id="ea43a-143">Hallo EventProcessor Web Project instellen</span><span class="sxs-lookup"><span data-stu-id="ea43a-143">Set up hello EventProcessor Web Job</span></span>
<span data-ttu-id="ea43a-144">In deze sectie maakt u verbinding maken uw vooraf geconfigureerde oplossing toohello logische App die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ea43a-144">In this section, you connect your preconfigured solution toohello Logic App you created.</span></span> <span data-ttu-id="ea43a-145">toocomplete deze taak u Hallo URL tootrigger Hallo logische App toohello actie toevoegen die wordt geactiveerd wanneer de waarde van een apparaat sensor een drempelwaarde overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="ea43a-145">toocomplete this task, you add hello URL tootrigger hello Logic App toohello action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="ea43a-146">Gebruik uw git tooclone Hallo meest recente clientversie van Hallo [azure-iot-remote-monitoring github-opslagplaats][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="ea43a-146">Use your git client tooclone hello latest version of hello [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="ea43a-147">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ea43a-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="ea43a-148">Open in Visual Studio Hallo **RemoteMonitoring.sln** van een lokale kopie van de Hallo van Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ea43a-148">In Visual Studio, open hello **RemoteMonitoring.sln** from hello local copy of hello repository.</span></span>
3. <span data-ttu-id="ea43a-149">Open Hallo **ActionRepository.cs** bestand in Hallo **infrastructuur\\opslagplaats** map.</span><span class="sxs-lookup"><span data-stu-id="ea43a-149">Open hello **ActionRepository.cs** file in hello **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="ea43a-150">Update Hallo **actionIds** woordenlijst met de Hallo **Http Post toothis URL** hebt genoteerd uit uw logische App als volgt:</span><span class="sxs-lookup"><span data-stu-id="ea43a-150">Update hello **actionIds** dictionary with hello **Http Post toothis URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post toothis URL>" },
        { "Raise Alarm", "<Http Post toothis URL>" }
    };
    ```
5. <span data-ttu-id="ea43a-151">Hallo wijzigingen opslaan in de oplossing en Visual Studio af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="ea43a-151">Save hello changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-hello-command-line"></a><span data-ttu-id="ea43a-152">Implementeren vanaf de opdrachtregel Hallo</span><span class="sxs-lookup"><span data-stu-id="ea43a-152">Deploy from hello command line</span></span>
<span data-ttu-id="ea43a-153">In deze sectie kunt u de bijgewerkte versie van Hallo externe controle oplossing tooreplace Hallo versie die momenteel worden uitgevoerd in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="ea43a-153">In this section, you deploy your updated version of hello remote monitoring solution tooreplace hello version currently running in Azure.</span></span>

1. <span data-ttu-id="ea43a-154">Volgende Hallo [dev set-up] [ lnk-devsetup] instructies tooset van uw omgeving voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="ea43a-154">Following hello [dev set-up][lnk-devsetup] instructions tooset up your environment for deployment.</span></span>
2. <span data-ttu-id="ea43a-155">toodeploy lokaal, volg Hallo [lokale implementatie] [ lnk-localdeploy] instructies.</span><span class="sxs-lookup"><span data-stu-id="ea43a-155">toodeploy locally, follow hello [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="ea43a-156">toodeploy toohello cloud en bijwerken van uw bestaande cloudimplementatie, volgt u Hallo [cloud implementatie] [ lnk-clouddeploy] instructies.</span><span class="sxs-lookup"><span data-stu-id="ea43a-156">toodeploy toohello cloud and update your existing cloud deployment, follow hello [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="ea43a-157">Hallo-naam van uw oorspronkelijke implementatie als de naam van de implementatie hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ea43a-157">Use hello name of your original deployment as hello deployment name.</span></span> <span data-ttu-id="ea43a-158">Bijvoorbeeld als de oorspronkelijke implementatie Hallo is aangeroepen **demologicapp**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ea43a-158">For example if hello original deployment was called **demologicapp**, use hello following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="ea43a-159">Wanneer Hallo bouwen script wordt uitgevoerd, moet u toouse Hallo dezelfde Azure-account, abonnement, regio en Active Directory-exemplaar die u hebt gebruikt toen u Hallo oplossing hebt ingericht.</span><span class="sxs-lookup"><span data-stu-id="ea43a-159">When hello build script runs, be sure toouse hello same Azure account, subscription, region, and Active Directory instance you used when you provisioned hello solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="ea43a-160">Zie uw logische App in actie</span><span class="sxs-lookup"><span data-stu-id="ea43a-160">See your Logic App in action</span></span>
<span data-ttu-id="ea43a-161">Hallo vooraf geconfigureerde oplossing voor externe controle heeft twee regels standaard ingesteld wanneer u een oplossing inricht.</span><span class="sxs-lookup"><span data-stu-id="ea43a-161">hello remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="ea43a-162">Beide regels zijn op Hallo **SampleDevice001** apparaat:</span><span class="sxs-lookup"><span data-stu-id="ea43a-162">Both rules are on hello **SampleDevice001** device:</span></span>

* <span data-ttu-id="ea43a-163">Temperatuur > 38.00</span><span class="sxs-lookup"><span data-stu-id="ea43a-163">Temperature > 38.00</span></span>
* <span data-ttu-id="ea43a-164">Vochtigheid > 48,00</span><span class="sxs-lookup"><span data-stu-id="ea43a-164">Humidity > 48.00</span></span>

<span data-ttu-id="ea43a-165">Hallo temperatuur regel activeert Hallo **verhogen Alarm** actie en Hallo vochtigheid regel activeert Hallo **SendMessage** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="ea43a-165">hello temperature rule triggers hello **Raise Alarm** action and hello Humidity rule triggers hello **SendMessage** action.</span></span> <span data-ttu-id="ea43a-166">Ervan uitgaande dat u gebruikt dezelfde URL voor beide acties Hallo Hallo **ActionRepository** klasse, uw logische app-triggers voor de regel.</span><span class="sxs-lookup"><span data-stu-id="ea43a-166">Assuming you used hello same URL for both actions hello **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="ea43a-167">Beide regels gebruiken SendGrid toosend een e-toohello **naar** adres met details van Hallo waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="ea43a-167">Both rules use SendGrid toosend an email toohello **To** address with details of hello alert.</span></span>

> [!NOTE]
> <span data-ttu-id="ea43a-168">Hallo logische App blijft tootrigger telkens Hallo drempelwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="ea43a-168">hello Logic App continues tootrigger every time hello threshold is met.</span></span> <span data-ttu-id="ea43a-169">tooavoid onnodige e-mailberichten, kunt u ofwel Hallo regels uitschakelen in uw oplossing portal- of uitschakelen Hallo logische App in Hallo [Azure-portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="ea43a-169">tooavoid unnecessary emails, you can either disable hello rules in your solution portal or disable hello Logic App in hello [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="ea43a-170">Bovendien tooreceiving e-mailberichten, kunt u ook zien wanneer Hallo logische App in Hallo portal wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ea43a-170">In addition tooreceiving emails, you can also see when hello Logic App runs in hello portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="ea43a-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea43a-171">Next steps</span></span>
<span data-ttu-id="ea43a-172">Nu dat u een bedrijfsproces logische App tooconnect Hallo vooraf geconfigureerde oplossing tooa gebruikt hebt, kunt u meer informatie over opties voor het aanpassen van Hallo vooraf geconfigureerde oplossingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="ea43a-172">Now that you've used a Logic App tooconnect hello preconfigured solution tooa business process, you can learn more about hello options for customizing hello preconfigured solutions:</span></span>

* <span data-ttu-id="ea43a-173">[Gebruik dynamische telemetrie Hello vooraf geconfigureerde oplossing voor externe controle][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="ea43a-173">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="ea43a-174">[Metagegevens van apparaten informatie in Hallo vooraf geconfigureerde oplossing voor externe controle][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="ea43a-174">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo]</span></span>

[lnk-dynamic]: iot-suite-dynamic-telemetry.md
[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk-internetofthings]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-getstarted]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-azureportal]: https://portal.azure.com
[lnk-logic-apps-actions]: ../connectors/apis-list.md
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-devsetup]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/dev-setup.md
[lnk-localdeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/local-deployment.md
[lnk-clouddeploy]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
