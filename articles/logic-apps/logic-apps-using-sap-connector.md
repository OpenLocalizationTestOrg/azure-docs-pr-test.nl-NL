---
title: Verbinding maken met een on-premises SAP-systeem in Azure Logic Apps | Microsoft Docs
description: Verbinding maken met een on-premises SAP-systeem van uw werkstroom logic app via de gateway van de lokale gegevens
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 3fea93f558d5a4ef62550fd1f6486903cb812930
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-on-premises-sap-system-from-logic-apps-with-the-sap-connector"></a><span data-ttu-id="47d53-103">Verbinding maken met een on-premises SAP-systeem van logische apps met de SAP-connector</span><span class="sxs-lookup"><span data-stu-id="47d53-103">Connect to an on-premises SAP system from logic apps with the SAP connector</span></span> 

<span data-ttu-id="47d53-104">De lokale data gateway kunt u gegevens beheren en veilige toegang tot resources die zich on-premises.</span><span class="sxs-lookup"><span data-stu-id="47d53-104">The on-premises data gateway enables you to manage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="47d53-105">Dit onderwerp wordt beschreven hoe u logic apps kunt verbinden met een on-premises SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="47d53-105">This topic shows how you can connect logic apps to an on-premises SAP system.</span></span> <span data-ttu-id="47d53-106">In dit voorbeeld uw logische app een IDOC via HTTP-aanvragen en verzendt het antwoord terug.</span><span class="sxs-lookup"><span data-stu-id="47d53-106">In this example, your logic app requests an IDOC over HTTP and sends the response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="47d53-107">Huidige beperkingen:</span><span class="sxs-lookup"><span data-stu-id="47d53-107">Current limitations:</span></span> 
> - <span data-ttu-id="47d53-108">Uw logische app een time-out optreedt als alle stappen die nodig zijn voor het antwoord is niet voltooid binnen de [aanvraag time-outlimiet](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="47d53-108">Your logic app times out if all steps required for the response don't finish within the [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="47d53-109">In dit scenario mogelijk aanvragen worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="47d53-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="47d53-110">De bestandskiezer worden niet weergegeven voor alle beschikbare velden.</span><span class="sxs-lookup"><span data-stu-id="47d53-110">The file picker does not display all the available fields.</span></span> <span data-ttu-id="47d53-111">In dit scenario kunt u paden handmatig toevoegen.</span><span class="sxs-lookup"><span data-stu-id="47d53-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47d53-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="47d53-112">Prerequisites</span></span>

- <span data-ttu-id="47d53-113">Installeren en configureren van de meest recente [lokale gegevensgateway](https://www.microsoft.com/download/details.aspx?id=53127) versie 1.15.6150.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="47d53-113">Install and configure the latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="47d53-114">[Verbinding maken met de lokale data gateway in een logische app](http://aka.ms/logicapps-gateway) vermeldt de stappen.</span><span class="sxs-lookup"><span data-stu-id="47d53-114">[How to connect to the on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists the steps.</span></span> <span data-ttu-id="47d53-115">De gateway moet worden geïnstalleerd op een on-premises machine voordat u verder kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="47d53-115">The gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="47d53-116">Download en installeer de meest recente SAP-clientbibliotheek op dezelfde computer waarop u de data gateway hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="47d53-116">Download and install the latest SAP client library on the same machine where you installed the data gateway.</span></span> <span data-ttu-id="47d53-117">Gebruik een van de volgende SAP-versies:</span><span class="sxs-lookup"><span data-stu-id="47d53-117">Use any of the following SAP versions:</span></span> 
    - <span data-ttu-id="47d53-118">SAP-Server</span><span class="sxs-lookup"><span data-stu-id="47d53-118">SAP Server</span></span>
        - <span data-ttu-id="47d53-119">Een SAP-Server die ondersteuning bieden voor de .NET-Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="47d53-119">Any SAP Server that support the .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="47d53-120">SAP-Client</span><span class="sxs-lookup"><span data-stu-id="47d53-120">SAP Client</span></span>
        - <span data-ttu-id="47d53-121">SAP .NET-Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="47d53-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-to-your-sap-system"></a><span data-ttu-id="47d53-122">Triggers en acties voor het verbinden met uw SAP-systeem toevoegen</span><span class="sxs-lookup"><span data-stu-id="47d53-122">Add triggers and actions for connecting to your SAP system</span></span>

<span data-ttu-id="47d53-123">De SAP-connector heeft acties, maar geen triggers.</span><span class="sxs-lookup"><span data-stu-id="47d53-123">The SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="47d53-124">We hebben dus gebruik een andere trigger aan het begin van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="47d53-124">So, we have to use another trigger at the start of the workflow.</span></span> 

1. <span data-ttu-id="47d53-125">De aanvraag/antwoord-trigger toevoegen en selecteer vervolgens **nieuwe stap**.</span><span class="sxs-lookup"><span data-stu-id="47d53-125">Add the Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="47d53-126">Selecteer **een actie toevoegen**, en selecteer vervolgens de SAP-connector door te typen `SAP` in het zoekveld:</span><span class="sxs-lookup"><span data-stu-id="47d53-126">Select **Add an action**, and then select the SAP connector by typing `SAP` in the search field:</span></span>    

     ![SAP-toepassingsserver of SAP berichtenserver selecteren](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="47d53-128">Selecteer [ **SAP-toepassingsserver** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) of [ **SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), op basis van uw SAP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="47d53-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="47d53-129">Als u een bestaande verbinding geen hebt, wordt u gevraagd een maken.</span><span class="sxs-lookup"><span data-stu-id="47d53-129">If you don't have an existing connection, you are prompted to create one.</span></span>

   1. <span data-ttu-id="47d53-130">Selecteer **verbinden via lokale gegevensgateway**, en voer de details voor uw SAP-systeem:</span><span class="sxs-lookup"><span data-stu-id="47d53-130">Select **Connect via on-premises data gateway**, and enter the details for your SAP system:</span></span>   

       ![Verbindingsreeks SAP toevoegen](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="47d53-132">Onder **Gateway**, selecteert u een bestaande gateway of selecteren voor het installeren van een nieuwe gateway **Gateway installeren**.</span><span class="sxs-lookup"><span data-stu-id="47d53-132">Under **Gateway**, select an existing gateway, or to install a new gateway, select **Install Gateway**.</span></span>

        ![Een nieuwe gateway installeren](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="47d53-134">Nadat u alle gegevens invoeren, selecteert u **maken**.</span><span class="sxs-lookup"><span data-stu-id="47d53-134">After you enter all the details, select **Create**.</span></span> 
   <span data-ttu-id="47d53-135">Logic Apps configureert en test u de verbinding, om ervoor te zorgen dat de verbinding goed werkt.</span><span class="sxs-lookup"><span data-stu-id="47d53-135">Logic Apps configures and tests the connection, making sure that the connection works properly.</span></span>

4. <span data-ttu-id="47d53-136">Voer een naam voor uw SAP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="47d53-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="47d53-137">De verschillende opties voor SAP zijn nu beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="47d53-137">The different SAP options are now available.</span></span> <span data-ttu-id="47d53-138">Selecteer de categorie IDOC vindt in de lijst.</span><span class="sxs-lookup"><span data-stu-id="47d53-138">To find your IDOC category, select from the list.</span></span> <span data-ttu-id="47d53-139">Of geef het pad handmatig en selecteer het HTTP-antwoord in de **hoofdtekst** veld:</span><span class="sxs-lookup"><span data-stu-id="47d53-139">Or manually type in the path, and select the HTTP response in the **body** field:</span></span>

     ![SAP-actie](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="47d53-141">Voeg de actie voor het maken van een **HTTP-antwoord**.</span><span class="sxs-lookup"><span data-stu-id="47d53-141">Add the action for creating an **HTTP Response**.</span></span> <span data-ttu-id="47d53-142">Het antwoordbericht moet uit de SAP-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="47d53-142">The response message should be from the SAP output.</span></span>

7. <span data-ttu-id="47d53-143">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="47d53-143">Save your logic app.</span></span> <span data-ttu-id="47d53-144">Testen door te sturen een IDOC via de URL van de HTTP-trigger.</span><span class="sxs-lookup"><span data-stu-id="47d53-144">Test it by sending an IDOC through the HTTP trigger URL.</span></span> <span data-ttu-id="47d53-145">Nadat de IDOC is verzonden, wacht u totdat de reactie van de logische app:</span><span class="sxs-lookup"><span data-stu-id="47d53-145">After the IDOC is sent, wait for the response from the logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="47d53-146">Bekijk hoe [uw logische Apps bewaken](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="47d53-146">Check out how to [monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="47d53-147">Nu dat de SAP-connector wordt toegevoegd aan uw logische app, start u de andere functionaliteiten verkennen:</span><span class="sxs-lookup"><span data-stu-id="47d53-147">Now that the SAP connector is added to your logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="47d53-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="47d53-148">BAPI</span></span>
- <span data-ttu-id="47d53-149">RFC</span><span class="sxs-lookup"><span data-stu-id="47d53-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="47d53-150">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="47d53-150">Get help</span></span>

<span data-ttu-id="47d53-151">Ga naar het [Forum voor Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) om vragen te stellen, vragen te beantwoorden en te zien wat andere gebruikers van Azure Logic Apps aan het doen zijn.</span><span class="sxs-lookup"><span data-stu-id="47d53-151">To ask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="47d53-152">Ter verbetering van Azure Logic Apps en connectors kunt u stemmen op ideeën of ideeën indien op de [site voor gebruikersfeedback van Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="47d53-152">To help improve Azure Logic Apps and connectors, vote on or submit ideas at the [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47d53-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="47d53-153">Next steps</span></span>

- <span data-ttu-id="47d53-154">Informatie over het valideren, transformeren en andere functies BizTalk-achtige in de [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47d53-154">Learn how to validate, transform, and other BizTalk-like functions in the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="47d53-155">[Verbinding maken met on-premises gegevens](../logic-apps/logic-apps-gateway-connection.md) vanuit logic apps</span><span class="sxs-lookup"><span data-stu-id="47d53-155">[Connect to on-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
