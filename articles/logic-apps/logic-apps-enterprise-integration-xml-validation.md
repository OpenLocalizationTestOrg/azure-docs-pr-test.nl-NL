---
title: Valideren van XML is - Azure Logic Apps | Microsoft Docs
description: XML-validatie met schema's voor Azure Logic Apps en B2B-scenario's met behulp van het Enterprise-integratiepakket
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: d700588f-2d8a-4c92-93eb-e1e6e250e760
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8558efffa354cc4bb93820c837077ee997924c95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="2b7a4-103">XML-validatie voor enterprise-integratie</span><span class="sxs-lookup"><span data-stu-id="2b7a4-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="2b7a4-104">Vaak in B2B-scenario's, moeten de partners in een overeenkomst ervoor zorgen dat de wisselen ze berichten geldig zijn voordat u kunt beginnen met het verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-104">Often in B2B scenarios, the partners in an agreement must make sure that the messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="2b7a4-105">U kunt documenten tegen een vooraf gedefinieerd schema valideren met behulp van het gebruik van de XML-validatie-connector in de Enterprise-integratiepakket.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-105">You can validate documents against a predefined schema by using the use the XML Validation connector in the Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-the-xml-validation-connector"></a><span data-ttu-id="2b7a4-106">Een document met de XML-validatie-connector valideren</span><span class="sxs-lookup"><span data-stu-id="2b7a4-106">Validate a document with the XML Validation connector</span></span>

1. <span data-ttu-id="2b7a4-107">Een logische app maken en [de app koppelen aan het account integratie](../logic-apps/logic-apps-enterprise-integration-accounts.md "informatie over het koppelen van een integratie-account aan een logische app") is met het schema dat u gebruiken wilt voor het valideren van XML-gegevens.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-107">Create a logic app, and [link the app to the integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that has the schema you want to use for validating XML data.</span></span>

2. <span data-ttu-id="2b7a4-108">Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-108">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="2b7a4-109">Om toe te voegen de **XML-validatie** actie, kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-109">To add the **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="2b7a4-110">De acties met de fout die u wilt filteren, voeren *xml* in het zoekvak.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-110">To filter all the actions to the one that you want, enter *xml* in the search box.</span></span> <span data-ttu-id="2b7a4-111">Kies **XML-validatie**.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="2b7a4-112">Als u de XML-inhoud die u wilt valideren, schakelt u **inhoud**.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-112">To specify the XML content that you want to validate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="2b7a4-113">Selecteer de label body als de inhoud die u wilt valideren.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-113">Select the body tag as the content that you want to validate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="2b7a4-114">Om op te geven van het schema dat u gebruiken wilt voor het valideren van de vorige *inhoud* invoeren, kies **SCHEMANAAM**.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-114">To specify the schema you want to use for validating the previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="2b7a4-115">Sla uw werk</span><span class="sxs-lookup"><span data-stu-id="2b7a4-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="2b7a4-116">Nu bent u klaar met het instellen van uw validatie-connector.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="2b7a4-117">In een toepassing werkelijkheid is het raadzaam de gevalideerde gegevens opslaan in een line-of-business (LOB)-app zoals SalesForce.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-117">In a real world application, you might want to store the validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="2b7a4-118">De uitvoer van de gevalideerde om naar te verzenden Salesforce, moet u een actie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-118">To send the validated output to Salesforce, add an action.</span></span>

<span data-ttu-id="2b7a4-119">Als u wilt testen uw actie validatie, maak een aanvraag met het HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="2b7a4-119">To test your validation action, make a request to the HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b7a4-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b7a4-120">Next steps</span></span>
[<span data-ttu-id="2b7a4-121">Meer informatie over het Enterprise-integratiepakket</span><span class="sxs-lookup"><span data-stu-id="2b7a4-121">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")   

