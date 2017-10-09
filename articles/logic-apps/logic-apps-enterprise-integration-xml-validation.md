---
title: aaaValidate XML is - Azure Logic Apps | Microsoft Docs
description: XML-validatie met schema's voor Azure Logic Apps en B2B-scenario's met behulp van Enterprise Integration Pack Hallo
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
ms.openlocfilehash: 81f662d0ddf908657b54de8af0a75fff55782ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-for-enterprise-integration"></a><span data-ttu-id="2d417-103">XML-validatie voor enterprise-integratie</span><span class="sxs-lookup"><span data-stu-id="2d417-103">Validate XML for enterprise integration</span></span>

<span data-ttu-id="2d417-104">Vaak in B2B-scenario's, moeten Hallo partners in een overeenkomst ervoor zorgen dat Hallo-berichten ze wisselen geldig zijn voordat u kunt beginnen met het verwerken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2d417-104">Often in B2B scenarios, hello partners in an agreement must make sure that hello messages they exchange are valid before data processing can start.</span></span> <span data-ttu-id="2d417-105">U kunt documenten tegen een vooraf gedefinieerd schema valideren met behulp van Hallo gebruik Hallo XML-validatie-connector in Hallo Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="2d417-105">You can validate documents against a predefined schema by using hello use hello XML Validation connector in hello Enterprise Integration Pack.</span></span>

## <a name="validate-a-document-with-hello-xml-validation-connector"></a><span data-ttu-id="2d417-106">Een document met Hallo XML-validatie connector valideren</span><span class="sxs-lookup"><span data-stu-id="2d417-106">Validate a document with hello XML Validation connector</span></span>

1. <span data-ttu-id="2d417-107">Een logische app maken en [Hallo app toohello integratie account koppelen](../logic-apps/logic-apps-enterprise-integration-accounts.md "toolink een integratie account tooa logische app meer") waarvoor Hallo schema gewenste toouse voor het valideren van XML-gegevens.</span><span class="sxs-lookup"><span data-stu-id="2d417-107">Create a logic app, and [link hello app toohello integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn toolink an integration account tooa Logic app") that has hello schema you want toouse for validating XML data.</span></span>

2. <span data-ttu-id="2d417-108">Voeg een **aanvraag: wanneer een HTTP-aanvraag wordt ontvangen** trigger tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="2d417-108">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1.png)

3. <span data-ttu-id="2d417-109">Hallo tooadd **XML-validatie** actie, kies **een actie toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2d417-109">tooadd hello **XML Validation** action, choose **Add an action**.</span></span>

4. <span data-ttu-id="2d417-110">alle acties toohello die u wilt, Hallo toofilter Voer *xml* in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d417-110">toofilter all hello actions toohello one that you want, enter *xml* in hello search box.</span></span> <span data-ttu-id="2d417-111">Kies **XML-validatie**.</span><span class="sxs-lookup"><span data-stu-id="2d417-111">Choose **XML Validation**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-2.png)

5. <span data-ttu-id="2d417-112">Selecteer toospecify Hallo XML-inhoud die u toovalidate wilt, **inhoud**.</span><span class="sxs-lookup"><span data-stu-id="2d417-112">toospecify hello XML content that you want toovalidate, select **CONTENT**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-1-5.png)

6. <span data-ttu-id="2d417-113">Hallo hoofdtekst label als Hallo inhoud die u wilt dat toovalidate selecteren.</span><span class="sxs-lookup"><span data-stu-id="2d417-113">Select hello body tag as hello content that you want toovalidate.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-3.png)

7. <span data-ttu-id="2d417-114">toospecify hello schema gewenste toouse voor het valideren van de vorige Hallo *inhoud* invoeren, kies **SCHEMANAAM**.</span><span class="sxs-lookup"><span data-stu-id="2d417-114">toospecify hello schema you want toouse for validating hello previous *content* input, choose **SCHEMA NAME**.</span></span>

    ![](./media/logic-apps-enterprise-integration-xml/xml-4.png)

8. <span data-ttu-id="2d417-115">Sla uw werk</span><span class="sxs-lookup"><span data-stu-id="2d417-115">Save your work</span></span>  

    ![](./media/logic-apps-enterprise-integration-xml/xml-5.png)

<span data-ttu-id="2d417-116">Nu bent u klaar met het instellen van uw validatie-connector.</span><span class="sxs-lookup"><span data-stu-id="2d417-116">You are now done with setting up your validation connector.</span></span> <span data-ttu-id="2d417-117">U kunt in een toepassing concrete toostore Hallo gevalideerd gegevens in een line-of-business (LOB)-app zoals SalesForce.</span><span class="sxs-lookup"><span data-stu-id="2d417-117">In a real world application, you might want toostore hello validated data in a line-of-business (LOB) app like SalesForce.</span></span> <span data-ttu-id="2d417-118">toosend Hallo geverifieerde uitvoer tooSalesforce, een actie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2d417-118">toosend hello validated output tooSalesforce, add an action.</span></span>

<span data-ttu-id="2d417-119">tootest uw actie validatie maken van een aanvraag toohello HTTP-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="2d417-119">tootest your validation action, make a request toohello HTTP endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d417-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d417-120">Next steps</span></span>
[<span data-ttu-id="2d417-121">Meer informatie over Enterprise Integration Pack Hallo</span><span class="sxs-lookup"><span data-stu-id="2d417-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "meer informatie over Enterprise Integration Pack")   

