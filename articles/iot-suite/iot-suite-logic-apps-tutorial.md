---
title: Azure IoT Suite en Logic Apps | Microsoft Docs
description: Een zelfstudie over het aansluiten van Logic Apps Azure IoT Suite voor bedrijfsproces.
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
ms.openlocfilehash: 2e7997e2a8bdeeec6083d40acb55e653f87e140b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-connect-logic-app-to-your-azure-iot-suite-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="33faf-103">Zelfstudie: Logic App verbinden met uw Azure IoT Suite Remote Monitoring vooraf geconfigureerde oplossing</span><span class="sxs-lookup"><span data-stu-id="33faf-103">Tutorial: Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution</span></span>
<span data-ttu-id="33faf-104">De [Microsoft Azure IoT Suite] [ lnk-internetofthings] vooraf geconfigureerde oplossing voor externe controle is een uitstekende manier om snel aan de slag met een end-to-end-functieset die verklaart de IoT-oplossing.</span><span class="sxs-lookup"><span data-stu-id="33faf-104">The [Microsoft Azure IoT Suite][lnk-internetofthings] remote monitoring preconfigured solution is a great way to get started quickly with an end-to-end feature set that exemplifies an IoT solution.</span></span> <span data-ttu-id="33faf-105">Deze zelfstudie leert u hoe u logische App toevoegt aan uw vooraf geconfigureerde oplossing voor externe controle van Microsoft Azure IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="33faf-105">This tutorial walks you through how to add Logic App to your Microsoft Azure IoT Suite remote monitoring preconfigured solution.</span></span> <span data-ttu-id="33faf-106">Deze stappen laten zien hoe u uw IoT-oplossing nog verder door verbinding te maken aan een bedrijfsproces kunt nemen.</span><span class="sxs-lookup"><span data-stu-id="33faf-106">These steps demonstrate how you can take your IoT solution even further by connecting it to a business process.</span></span>

<span data-ttu-id="33faf-107">*Als u een overzicht over het inrichten van een externe controle vooraf geconfigureerde oplossing zoekt, Zie [zelfstudie: aan de slag met de vooraf geconfigureerde IoT-oplossingen][lnk-getstarted].*</span><span class="sxs-lookup"><span data-stu-id="33faf-107">*If you’re looking for a walkthrough on how to provision a remote monitoring preconfigured solution, see [Tutorial: Get started with the IoT preconfigured solutions][lnk-getstarted].*</span></span>

<span data-ttu-id="33faf-108">Voordat u deze zelfstudie begint, moet u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="33faf-108">Before you start this tutorial, you should:</span></span>

* <span data-ttu-id="33faf-109">De vooraf geconfigureerde oplossing voor externe controle in uw Azure-abonnement inrichten.</span><span class="sxs-lookup"><span data-stu-id="33faf-109">Provision the remote monitoring preconfigured solution in your Azure subscription.</span></span>
* <span data-ttu-id="33faf-110">Maak een account SendGrid zodat u een e-mailberichten die uw bedrijfsproces activeert.</span><span class="sxs-lookup"><span data-stu-id="33faf-110">Create a SendGrid account to enable you to send an email that triggers your business process.</span></span> <span data-ttu-id="33faf-111">U kunt zich aanmelden voor een gratis proefaccount op [SendGrid](https://sendgrid.com/) door te klikken op **Probeer gratis**.</span><span class="sxs-lookup"><span data-stu-id="33faf-111">You can sign up for a free trial account at [SendGrid](https://sendgrid.com/) by clicking **Try for Free**.</span></span> <span data-ttu-id="33faf-112">Nadat u hebt geregistreerd voor een gratis proefversie account, moet u maken een [API-sleutel](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid die machtigingen verleent voor het verzenden van e-mail.</span><span class="sxs-lookup"><span data-stu-id="33faf-112">After you have registered for your free trial account, you need to create an [API key](https://sendgrid.com/docs/User_Guide/Settings/api_keys.html) in SendGrid that grants permissions to send mail.</span></span> <span data-ttu-id="33faf-113">Verderop in de zelfstudie moet u deze API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="33faf-113">You need this API key later in the tutorial.</span></span>

<span data-ttu-id="33faf-114">Voor deze zelfstudie hebt voltooid, moet u Visual Studio 2015 of Visual Studio 2017 te wijzigen van de acties in de vooraf geconfigureerde oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="33faf-114">To complete this tutorial, you need Visual Studio 2015 or Visual Studio 2017 to modify the actions in the preconfigured solution back end.</span></span>

<span data-ttu-id="33faf-115">Ervan uitgaande dat u al hebt ingericht uw externe controle vooraf geconfigureerde oplossing, gaat u naar de resourcegroep voor deze oplossing in de [Azure-portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="33faf-115">Assuming you’ve already provisioned your remote monitoring preconfigured solution, navigate to the resource group for that solution in the [Azure portal][lnk-azureportal].</span></span> <span data-ttu-id="33faf-116">De resourcegroep heeft dezelfde naam als de oplossingsnaam van de u hebt gekozen wanneer u uw oplossing voor externe controle ingericht.</span><span class="sxs-lookup"><span data-stu-id="33faf-116">The resource group has the same name as the solution name you chose when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="33faf-117">In de resourcegroep ziet u alle ingerichte Azure-resources voor uw oplossing, met uitzondering van de Azure Active Directory-toepassing die u in de klassieke Azure-Portal vinden kunt.</span><span class="sxs-lookup"><span data-stu-id="33faf-117">In the resource group, you can see all the provisioned Azure resources for your solution except for the Azure Active Directory application that you can find in the Azure Classic Portal.</span></span> <span data-ttu-id="33faf-118">De volgende schermafbeelding ziet u een voorbeeld **resourcegroep** blade voor een externe controle vooraf geconfigureerde oplossing:</span><span class="sxs-lookup"><span data-stu-id="33faf-118">The following screenshot shows an example **Resource group** blade for a remote monitoring preconfigured solution:</span></span>

![](media/iot-suite-logic-apps-tutorial/resourcegroup.png)

<span data-ttu-id="33faf-119">Om te beginnen, de logic app instellen voor gebruik met de vooraf geconfigureerde oplossing.</span><span class="sxs-lookup"><span data-stu-id="33faf-119">To begin, set up the logic app to use with the preconfigured solution.</span></span>

## <a name="set-up-the-logic-app"></a><span data-ttu-id="33faf-120">De logische App instellen</span><span class="sxs-lookup"><span data-stu-id="33faf-120">Set up the Logic App</span></span>
1. <span data-ttu-id="33faf-121">Klik op **toevoegen** boven aan de blade met resourcegroepen in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="33faf-121">Click **Add** at the top of your resource group blade in the Azure portal.</span></span>
2. <span data-ttu-id="33faf-122">Zoeken naar **logische App**, selecteert u deze en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="33faf-122">Search for **Logic App**, select it and then click **Create**.</span></span>
3. <span data-ttu-id="33faf-123">Vul de **naam** en gebruik van dezelfde **abonnement** en **resourcegroep** die u hebt gebruikt bij het inrichten van uw oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="33faf-123">Fill out the **Name** and use the same **Subscription** and **Resource group** that you used when you provisioned your remote monitoring solution.</span></span> <span data-ttu-id="33faf-124">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="33faf-124">Click **Create**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/createlogicapp.png)
4. <span data-ttu-id="33faf-125">Wanneer uw implementatie is voltooid, ziet u dat de logische App wordt vermeld als een resource in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="33faf-125">When your deployment completes, you can see the Logic App is listed as a resource in your resource group.</span></span>
5. <span data-ttu-id="33faf-126">Klik op de logische App om te navigeren naar de blade logische App, selecteer de **lege logische App** sjabloon openen de **Logic Apps Designer**.</span><span class="sxs-lookup"><span data-stu-id="33faf-126">Click the Logic App to navigate to the Logic App blade, select the **Blank Logic App** template to open the **Logic Apps Designer**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappsdesigner.png)
6. <span data-ttu-id="33faf-127">Selecteer **aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="33faf-127">Select **Request**.</span></span> <span data-ttu-id="33faf-128">Deze actie geeft aan dat een inkomende HTTP-aanvraag met een specifieke JSON nettolading handelingen als een trigger opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="33faf-128">This action specifies that an incoming HTTP request with a specific JSON formatted payload acts as a trigger.</span></span>
7. <span data-ttu-id="33faf-129">Plak de volgende code in de aanvraag hoofdtekst JSON-Schema:</span><span class="sxs-lookup"><span data-stu-id="33faf-129">Paste the following code into the Request Body JSON Schema:</span></span>
   
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
   > <span data-ttu-id="33faf-130">Nadat u de logische app opslaan, maar u moet eerst een actie toevoegen, kunt u de URL voor het HTTP POST-protocol kopiëren.</span><span class="sxs-lookup"><span data-stu-id="33faf-130">You can copy the URL for the HTTP post after you save the logic app, but first you must add an action.</span></span>
   > 
   > 
8. <span data-ttu-id="33faf-131">Klik op **+ een nieuwe stap** onder de handmatige trigger.</span><span class="sxs-lookup"><span data-stu-id="33faf-131">Click **+ New step** under your manual trigger.</span></span> <span data-ttu-id="33faf-132">Klik vervolgens op **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="33faf-132">Then click **Add an action**.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappcode.png)
9. <span data-ttu-id="33faf-133">Zoeken naar **SendGrid - e-mailbericht verzenden** en klik erop.</span><span class="sxs-lookup"><span data-stu-id="33faf-133">Search for **SendGrid - Send email** and click it.</span></span>
   
    ![](media/iot-suite-logic-apps-tutorial/logicappaction.png)
10. <span data-ttu-id="33faf-134">Voer een naam voor de verbinding, zoals **SendGridConnection**, voer de **SendGrid-API-sleutel** u gemaakt wanneer u uw SendGrid-account instellen en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="33faf-134">Enter a name for the connection, such as **SendGridConnection**, enter the **SendGrid API Key** you created when you set up your SendGrid account, and click **Create**.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridconnection.png)
11. <span data-ttu-id="33faf-135">E-mailadressen die u voor beide bezit toevoegen de **van** en **naar** velden.</span><span class="sxs-lookup"><span data-stu-id="33faf-135">Add email addresses you own to both the **From** and **To** fields.</span></span> <span data-ttu-id="33faf-136">Voeg **externe controle waarschuwing [DeviceId]** naar de **onderwerp** veld.</span><span class="sxs-lookup"><span data-stu-id="33faf-136">Add **Remote monitoring alert [DeviceId]** to the **Subject** field.</span></span> <span data-ttu-id="33faf-137">In de **hoofdtekst van de E-mail** veld, het toevoegen van **apparaat [DeviceId] [measurementName] met de waarde [measuredValue] heeft gerapporteerd.**</span><span class="sxs-lookup"><span data-stu-id="33faf-137">In the **Email Body** field, add **Device [DeviceId] has reported [measurementName] with value [measuredValue].**</span></span> <span data-ttu-id="33faf-138">U kunt toevoegen **[DeviceId]**, **[measurementName]**, en **[measuredValue]** door te klikken in de **kunt u gegevens uit de vorige stappen** sectie.</span><span class="sxs-lookup"><span data-stu-id="33faf-138">You can add **[DeviceId]**, **[measurementName]**, and **[measuredValue]** by clicking in the **You can insert data from previous steps** section.</span></span>
    
    ![](media/iot-suite-logic-apps-tutorial/sendgridaction.png)
12. <span data-ttu-id="33faf-139">Klik op **opslaan** in het menu bovenaan.</span><span class="sxs-lookup"><span data-stu-id="33faf-139">Click **Save** in the top menu.</span></span>
13. <span data-ttu-id="33faf-140">Klik op de **aanvragen** trigger en kopieer de **Http Post naar deze URL** waarde.</span><span class="sxs-lookup"><span data-stu-id="33faf-140">Click the **Request** trigger and copy the **Http Post to this URL** value.</span></span> <span data-ttu-id="33faf-141">U moet deze URL verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="33faf-141">You need this URL later in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="33faf-142">Logic Apps kunnen u uitvoeren [veel verschillende soorten actie] [ lnk-logic-apps-actions] met inbegrip van acties in Office 365.</span><span class="sxs-lookup"><span data-stu-id="33faf-142">Logic Apps enable you to run [many different types of action][lnk-logic-apps-actions] including actions in Office 365.</span></span> 
> 
> 

## <a name="set-up-the-eventprocessor-web-job"></a><span data-ttu-id="33faf-143">De taak van de Web EventProcessor instellen</span><span class="sxs-lookup"><span data-stu-id="33faf-143">Set up the EventProcessor Web Job</span></span>
<span data-ttu-id="33faf-144">In deze sectie kunt u uw vooraf geconfigureerde oplossing verbinding met de logische App die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="33faf-144">In this section, you connect your preconfigured solution to the Logic App you created.</span></span> <span data-ttu-id="33faf-145">Voor het voltooien van deze taak kunt u de URL voor het activeren van de logische App aan de actie die wordt geactiveerd wanneer de waarde van een apparaat sensor een drempelwaarde overschrijdt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="33faf-145">To complete this task, you add the URL to trigger the Logic App to the action that fires when a device sensor value exceeds a threshold.</span></span>

1. <span data-ttu-id="33faf-146">De git-client gebruiken voor het klonen van de nieuwste versie van de [azure-iot-remote-monitoring github-opslagplaats][lnk-rmgithub].</span><span class="sxs-lookup"><span data-stu-id="33faf-146">Use your git client to clone the latest version of the [azure-iot-remote-monitoring github repository][lnk-rmgithub].</span></span> <span data-ttu-id="33faf-147">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="33faf-147">For example:</span></span>
   
    ```cmd
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```
2. <span data-ttu-id="33faf-148">Open in Visual Studio de **RemoteMonitoring.sln** uit de lokale kopie van de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="33faf-148">In Visual Studio, open the **RemoteMonitoring.sln** from the local copy of the repository.</span></span>
3. <span data-ttu-id="33faf-149">Open de **ActionRepository.cs** bestand de **infrastructuur\\opslagplaats** map.</span><span class="sxs-lookup"><span data-stu-id="33faf-149">Open the **ActionRepository.cs** file in the **Infrastructure\\Repository** folder.</span></span>
4. <span data-ttu-id="33faf-150">Update de **actionIds** woordenlijst met de **Http Post naar deze URL** hebt genoteerd uit uw logische App als volgt:</span><span class="sxs-lookup"><span data-stu-id="33faf-150">Update the **actionIds** dictionary with the **Http Post to this URL** you noted from your Logic App as follows:</span></span>
   
    ```csharp
    private Dictionary<string,string> actionIds = new Dictionary<string, string>()
    {
        { "Send Message", "<Http Post to this URL>" },
        { "Raise Alarm", "<Http Post to this URL>" }
    };
    ```
5. <span data-ttu-id="33faf-151">De wijzigingen opslaan in de oplossing en Visual Studio af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="33faf-151">Save the changes in solution and exit Visual Studio.</span></span>

## <a name="deploy-from-the-command-line"></a><span data-ttu-id="33faf-152">Implementeren vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="33faf-152">Deploy from the command line</span></span>
<span data-ttu-id="33faf-153">In deze sectie kunt u de bijgewerkte versie van de oplossing voor externe controle ter vervanging van de versie die momenteel worden uitgevoerd in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="33faf-153">In this section, you deploy your updated version of the remote monitoring solution to replace the version currently running in Azure.</span></span>

1. <span data-ttu-id="33faf-154">Na de [dev set-up] [ lnk-devsetup] instructies voor het instellen van uw omgeving voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="33faf-154">Following the [dev set-up][lnk-devsetup] instructions to set up your environment for deployment.</span></span>
2. <span data-ttu-id="33faf-155">Volg voor het lokaal implementeren de [lokale implementatie] [ lnk-localdeploy] instructies.</span><span class="sxs-lookup"><span data-stu-id="33faf-155">To deploy locally, follow the [local deployment][lnk-localdeploy] instructions.</span></span>
3. <span data-ttu-id="33faf-156">Als u wilt implementeren in de cloud en bijwerken van uw bestaande cloudimplementatie, volgt u de [cloud implementatie] [ lnk-clouddeploy] instructies.</span><span class="sxs-lookup"><span data-stu-id="33faf-156">To deploy to the cloud and update your existing cloud deployment, follow the [cloud deployment][lnk-clouddeploy] instructions.</span></span> <span data-ttu-id="33faf-157">De naam van uw oorspronkelijke implementatie gebruiken als de implementatienaam van de.</span><span class="sxs-lookup"><span data-stu-id="33faf-157">Use the name of your original deployment as the deployment name.</span></span> <span data-ttu-id="33faf-158">Bijvoorbeeld als de oorspronkelijke implementatie is aangeroepen **demologicapp**, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="33faf-158">For example if the original deployment was called **demologicapp**, use the following command:</span></span>
   
   ```cmd
   build.cmd cloud release demologicapp
   ```
   
   <span data-ttu-id="33faf-159">Wanneer het build-script wordt uitgevoerd, moet u de dezelfde Azure-account, abonnement, regio en u hebt gebruikt toen u de oplossing ingericht Active Directory-exemplaar te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33faf-159">When the build script runs, be sure to use the same Azure account, subscription, region, and Active Directory instance you used when you provisioned the solution.</span></span>

## <a name="see-your-logic-app-in-action"></a><span data-ttu-id="33faf-160">Zie uw logische App in actie</span><span class="sxs-lookup"><span data-stu-id="33faf-160">See your Logic App in action</span></span>
<span data-ttu-id="33faf-161">De vooraf geconfigureerde oplossing voor externe controle heeft twee regels standaard ingesteld wanneer u een oplossing inricht.</span><span class="sxs-lookup"><span data-stu-id="33faf-161">The remote monitoring preconfigured solution has two rules set up by default when you provision a solution.</span></span> <span data-ttu-id="33faf-162">Beide regels zijn op de **SampleDevice001** apparaat:</span><span class="sxs-lookup"><span data-stu-id="33faf-162">Both rules are on the **SampleDevice001** device:</span></span>

* <span data-ttu-id="33faf-163">Temperatuur > 38.00</span><span class="sxs-lookup"><span data-stu-id="33faf-163">Temperature > 38.00</span></span>
* <span data-ttu-id="33faf-164">Vochtigheid > 48,00</span><span class="sxs-lookup"><span data-stu-id="33faf-164">Humidity > 48.00</span></span>

<span data-ttu-id="33faf-165">De regel temperatuur triggers de **verhogen Alarm** actie en de vochtigheid regel triggers de **SendMessage** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="33faf-165">The temperature rule triggers the **Raise Alarm** action and the Humidity rule triggers the **SendMessage** action.</span></span> <span data-ttu-id="33faf-166">Ervan uitgaande dat u dezelfde URL voor beide acties gebruikt de **ActionRepository** klasse, uw logische app-triggers voor de regel.</span><span class="sxs-lookup"><span data-stu-id="33faf-166">Assuming you used the same URL for both actions the **ActionRepository** class, your logic app triggers for either rule.</span></span> <span data-ttu-id="33faf-167">Beide regels SendGrid gebruiken voor het verzenden van een e-mail naar de **naar** adres met details van de waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="33faf-167">Both rules use SendGrid to send an email to the **To** address with details of the alert.</span></span>

> [!NOTE]
> <span data-ttu-id="33faf-168">De logische App blijft om te activeren elke keer dat de drempelwaarde wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="33faf-168">The Logic App continues to trigger every time the threshold is met.</span></span> <span data-ttu-id="33faf-169">Om te voorkomen onnodige e-mailberichten, kunt u de regels in de oplossingsportal uitschakelen of uitschakelen van de logische App in de [Azure-portal][lnk-azureportal].</span><span class="sxs-lookup"><span data-stu-id="33faf-169">To avoid unnecessary emails, you can either disable the rules in your solution portal or disable the Logic App in the [Azure portal][lnk-azureportal].</span></span>
> 
> 

<span data-ttu-id="33faf-170">Naast het e-mailberichten ontvangt, kunt u ook zien wanneer de logische App in de portal wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="33faf-170">In addition to receiving emails, you can also see when the Logic App runs in the portal:</span></span>

![](media/iot-suite-logic-apps-tutorial/logicapprun.png)

## <a name="next-steps"></a><span data-ttu-id="33faf-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="33faf-171">Next steps</span></span>
<span data-ttu-id="33faf-172">Nu dat u een logische App verbinding maken met de vooraf geconfigureerde oplossing een bedrijfsproces gebruikt hebt, kunt u meer informatie over de opties voor het aanpassen van de vooraf geconfigureerde oplossingen:</span><span class="sxs-lookup"><span data-stu-id="33faf-172">Now that you've used a Logic App to connect the preconfigured solution to a business process, you can learn more about the options for customizing the preconfigured solutions:</span></span>

* <span data-ttu-id="33faf-173">[Dynamische telemetrie gebruiken met de vooraf geconfigureerde oplossing voor externe controle][lnk-dynamic]</span><span class="sxs-lookup"><span data-stu-id="33faf-173">[Use dynamic telemetry with the remote monitoring preconfigured solution][lnk-dynamic]</span></span>
* <span data-ttu-id="33faf-174">[Metagegevens van apparaten informatie in de vooraf geconfigureerde oplossing voor externe controle][lnk-devinfo]</span><span class="sxs-lookup"><span data-stu-id="33faf-174">[Device information metadata in the remote monitoring preconfigured solution][lnk-devinfo]</span></span>

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
