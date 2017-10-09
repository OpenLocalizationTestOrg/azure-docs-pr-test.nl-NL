---
title: aaaConnect tooan on-premises SAP systeem in Azure Logic Apps | Microsoft Docs
description: Verbinding maken met tooan on-premises SAP-systeem van uw werkstroom logic app via Hallo lokale gegevensgateway
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
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="82866-103">Verbinding maken met on-premises SAP-systeem tooan vanuit logic apps met Hallo SAP-connector</span><span class="sxs-lookup"><span data-stu-id="82866-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="82866-104">Hallo lokale gegevensgateway kunt u gegevens toomanage en veilige toegang tot resources die zich on-premises.</span><span class="sxs-lookup"><span data-stu-id="82866-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="82866-105">Dit onderwerp wordt beschreven hoe u verbinding kunt maken van logic apps tooan on-premises SAP-systeem.</span><span class="sxs-lookup"><span data-stu-id="82866-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="82866-106">In dit voorbeeld wordt met uw logische app een IDOC via HTTP-aanvragen en stuurt Hallo antwoord terug.</span><span class="sxs-lookup"><span data-stu-id="82866-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="82866-107">Huidige beperkingen:</span><span class="sxs-lookup"><span data-stu-id="82866-107">Current limitations:</span></span> 
> - <span data-ttu-id="82866-108">Uw logische app een time-out optreedt als u alle stappen die nodig zijn voor antwoord Hallo niet voltooid binnen de Hallo [aanvraag time-outlimiet](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="82866-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="82866-109">In dit scenario mogelijk aanvragen worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="82866-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="82866-110">Hallo-bestandskiezer worden niet weergegeven voor alle Hallo beschikbare velden.</span><span class="sxs-lookup"><span data-stu-id="82866-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="82866-111">In dit scenario kunt u paden handmatig toevoegen.</span><span class="sxs-lookup"><span data-stu-id="82866-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82866-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="82866-112">Prerequisites</span></span>

- <span data-ttu-id="82866-113">Installeer en configureer Hallo nieuwste [lokale gegevensgateway](https://www.microsoft.com/download/details.aspx?id=53127) versie 1.15.6150.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="82866-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="82866-114">[Hoe tooconnect toohello lokale gegevensgateway in een logische app](http://aka.ms/logicapps-gateway) lijsten Hallo stappen.</span><span class="sxs-lookup"><span data-stu-id="82866-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="82866-115">Hallo-gateway moet worden geïnstalleerd op een on-premises machine voordat u verder kunt gaan.</span><span class="sxs-lookup"><span data-stu-id="82866-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="82866-116">Download en installeer Hallo nieuwste SAP-clientbibliotheek op Hallo van de computer dezelfde waar u de gegevensgateway Hallo hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="82866-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="82866-117">Een van volgende SAP-versies hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="82866-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="82866-118">SAP-Server</span><span class="sxs-lookup"><span data-stu-id="82866-118">SAP Server</span></span>
        - <span data-ttu-id="82866-119">Een SAP-Server die ondersteuning Hallo .NET-Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="82866-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="82866-120">SAP-Client</span><span class="sxs-lookup"><span data-stu-id="82866-120">SAP Client</span></span>
        - <span data-ttu-id="82866-121">SAP .NET-Connector (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="82866-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="82866-122">Triggers en acties voor het verbinden van tooyour SAP-systeem toevoegen</span><span class="sxs-lookup"><span data-stu-id="82866-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="82866-123">Hallo SAP-connector heeft acties, maar geen triggers.</span><span class="sxs-lookup"><span data-stu-id="82866-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="82866-124">Dus hebben we toouse een andere trigger op Hallo Hallo workflow is gestart.</span><span class="sxs-lookup"><span data-stu-id="82866-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="82866-125">Hallo aanvraag/antwoord-trigger toevoegen en selecteer vervolgens **nieuwe stap**.</span><span class="sxs-lookup"><span data-stu-id="82866-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="82866-126">Selecteer **een actie toevoegen**, en selecteer vervolgens Hallo SAP-connector door te typen `SAP` in Hallo zoekveld:</span><span class="sxs-lookup"><span data-stu-id="82866-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![SAP-toepassingsserver of SAP berichtenserver selecteren](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="82866-128">Selecteer [ **SAP-toepassingsserver** ](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) of [ **SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), op basis van uw SAP-instellingen.</span><span class="sxs-lookup"><span data-stu-id="82866-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="82866-129">Als u een bestaande verbinding geen hebt, bent u na vragen aan gebruiker toocreate een.</span><span class="sxs-lookup"><span data-stu-id="82866-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="82866-130">Selecteer **verbinden via lokale gegevensgateway**, en geef Hallo-gegevens voor uw SAP-systeem:</span><span class="sxs-lookup"><span data-stu-id="82866-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Verbinding tekenreeks tooSAP toevoegen](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="82866-132">Onder **Gateway**, selecteer een bestaande gateway of een nieuwe gateway tooinstall, selecteert u **Gateway installeren**.</span><span class="sxs-lookup"><span data-stu-id="82866-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Een nieuwe gateway installeren](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="82866-134">Nadat u alle Hallo gegevens invoeren, selecteert u **maken**.</span><span class="sxs-lookup"><span data-stu-id="82866-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="82866-135">Logic Apps configureert en test de verbinding hello, om ervoor te zorgen dat connection Hallo goed werkt.</span><span class="sxs-lookup"><span data-stu-id="82866-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="82866-136">Voer een naam voor uw SAP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="82866-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="82866-137">Hallo verschillende SAP-opties zijn nu beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="82866-137">hello different SAP options are now available.</span></span> <span data-ttu-id="82866-138">toofind uw IDOC categorie, selecteert u een van de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="82866-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="82866-139">Of typ handmatig Hallo pad, en selecteer Hallo HTTP-antwoord in Hallo **hoofdtekst** veld:</span><span class="sxs-lookup"><span data-stu-id="82866-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![SAP-actie](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="82866-141">Voeg Hallo-actie voor het maken van een **HTTP-antwoord**.</span><span class="sxs-lookup"><span data-stu-id="82866-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="82866-142">Hallo response-bericht moet van Hallo SAP-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="82866-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="82866-143">Sla uw logische app.</span><span class="sxs-lookup"><span data-stu-id="82866-143">Save your logic app.</span></span> <span data-ttu-id="82866-144">Testen door een IDOC via HTTP Hallo trigger URL verzenden.</span><span class="sxs-lookup"><span data-stu-id="82866-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="82866-145">Na Hallo die IDOC wordt verzonden, wacht u Hallo reactie van Hallo logische app:</span><span class="sxs-lookup"><span data-stu-id="82866-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="82866-146">Te zoeken over[uw logische Apps bewaken](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="82866-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="82866-147">Hallo SAP-connector is tooyour logische app toegevoegd, start u de andere functionaliteiten verkennen:</span><span class="sxs-lookup"><span data-stu-id="82866-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="82866-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="82866-148">BAPI</span></span>
- <span data-ttu-id="82866-149">RFC</span><span class="sxs-lookup"><span data-stu-id="82866-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="82866-150">Help opvragen</span><span class="sxs-lookup"><span data-stu-id="82866-150">Get help</span></span>

<span data-ttu-id="82866-151">tooask vragen beantwoorden van vragen en meer informatie over welke andere Azure Logic Apps gebruikers doen, gaat u naar Hallo [Azure Logic Apps-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="82866-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="82866-152">toohelp Azure Logic Apps en connectors verbeteren, stem of ideeën op Hallo indienen [Azure Logic Apps gebruiker feedback site](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="82866-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82866-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82866-153">Next steps</span></span>

- <span data-ttu-id="82866-154">Meer informatie over hoe toovalidate, transformeren en andere functies BizTalk-achtige in Hallo [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="82866-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="82866-155">[Verbinding maken met tooon-premises gegevens](../logic-apps/logic-apps-gateway-connection.md) vanuit logic apps</span><span class="sxs-lookup"><span data-stu-id="82866-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
