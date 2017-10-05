---
title: Maken van partners voor berichten in business-to-business (B2B) - Azure Logic Apps | Microsoft Docs
description: Meer informatie over het toevoegen van partners aan uw account integratie met de Enterprise-integratiepakket en Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="c28c4-103">Toevoegen of bijwerken van partners in uw werkstroom business-to-business-overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="c28c4-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="c28c4-104">Partners zijn entiteiten die deelnemen aan business-to-business (B2B) transacties en uitwisselen van berichten tussen elkaar.</span><span class="sxs-lookup"><span data-stu-id="c28c4-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="c28c4-105">Voordat u partners die u en een andere organisatie deze transacties vertegenwoordigen maken kunt, moet u beide delen van gegevens die u identificeert en berichten is verzonden door elkaar worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="c28c4-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="c28c4-106">Nadat u deze gegevens worden behandeld en klaar bent om uw zakelijke relatie te, kunt u partners in uw account integratie te vertegenwoordigen u beide.</span><span class="sxs-lookup"><span data-stu-id="c28c4-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="c28c4-107">Welke rollen hebt partners in uw integratie-account?</span><span class="sxs-lookup"><span data-stu-id="c28c4-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="c28c4-108">Als u meer informatie over de berichten die worden uitgewisseld tussen partners definieert, maakt u overeenkomsten tussen de partners.</span><span class="sxs-lookup"><span data-stu-id="c28c4-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="c28c4-109">Echter, voordat u een overeenkomst maken kunt, moet u hebben toegevoegd ten minste twee partners aan uw account integratie.</span><span class="sxs-lookup"><span data-stu-id="c28c4-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="c28c4-110">Uw organisatie moet deel uitmaken van de overeenkomst als de **host partner**.</span><span class="sxs-lookup"><span data-stu-id="c28c4-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="c28c4-111">De andere partner of **Gast partner** vertegenwoordigt de organisatie die berichten met uw organisatie uitwisselt.</span><span class="sxs-lookup"><span data-stu-id="c28c4-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="c28c4-112">De Gast-partner kan zijn van een ander bedrijf, of zelfs een afdeling in uw eigen organisatie.</span><span class="sxs-lookup"><span data-stu-id="c28c4-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="c28c4-113">Nadat u deze partners hebt toegevoegd, kunt u een overeenkomst kunt maken.</span><span class="sxs-lookup"><span data-stu-id="c28c4-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="c28c4-114">Ontvangen en verzenden van de instellingen zijn gericht vanuit het oogpunt van de Partner die worden gehost.</span><span class="sxs-lookup"><span data-stu-id="c28c4-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="c28c4-115">Bijvoorbeeld, bepalen de receive-instellingen in een overeenkomst hoe de gehoste partner ontvangt berichten die worden verzonden vanaf een partner Gast.</span><span class="sxs-lookup"><span data-stu-id="c28c4-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="c28c4-116">Op dezelfde manier de instellingen voor uitgaande berichten op de overeenkomst aangeven hoe de gehoste partner-berichten verzendt naar de Gast-partner.</span><span class="sxs-lookup"><span data-stu-id="c28c4-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="c28c4-117">Het maken van een partner?</span><span class="sxs-lookup"><span data-stu-id="c28c4-117">How to create a partner?</span></span>

1. <span data-ttu-id="c28c4-118">Selecteer in de Azure-portal **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="c28c4-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="c28c4-119">Voer in het zoekvak filter **integratie**, selecteer daarna **Integratieaccounts** in de lijst met resultaten.</span><span class="sxs-lookup"><span data-stu-id="c28c4-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="c28c4-120">De integratie rekening waar u uw partners wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="c28c4-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="c28c4-121">Selecteer de **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="c28c4-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="c28c4-122">Kies in de blade Partners **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c28c4-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="c28c4-123">Voer een naam voor uw partner en selecteer vervolgens een **kwalificatie**.</span><span class="sxs-lookup"><span data-stu-id="c28c4-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="c28c4-124">Voer ten slotte een **waarde** om documenten die worden geleverd in uw apps te identificeren.</span><span class="sxs-lookup"><span data-stu-id="c28c4-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="c28c4-125">Overzicht van de voortgang van een proces voor het maken van uw partner, selecteer de *bel* meldingspictogram.</span><span class="sxs-lookup"><span data-stu-id="c28c4-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="c28c4-126">Om te bevestigen dat uw nieuwe partners zijn toegevoegd, selecteer de **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="c28c4-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="c28c4-127">Nadat u de tegel Partners selecteert, ziet u ook toegevoegde partners in de blade Partners.</span><span class="sxs-lookup"><span data-stu-id="c28c4-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="c28c4-128">Het bewerken van bestaande partners in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="c28c4-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="c28c4-129">Selecteer de **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="c28c4-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="c28c4-130">Nadat de Partners blade wordt geopend, selecteert u de partner die u wilt bewerken.</span><span class="sxs-lookup"><span data-stu-id="c28c4-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="c28c4-131">Op de **Update Partner** tegel, breng uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="c28c4-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="c28c4-132">Nadat u bent klaar, kiest u **opslaan**, of om uw wijzigingen annuleren, selecteer **negeren**.</span><span class="sxs-lookup"><span data-stu-id="c28c4-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="c28c4-133">Het verwijderen van een partner</span><span class="sxs-lookup"><span data-stu-id="c28c4-133">How to delete a partner</span></span>

1. <span data-ttu-id="c28c4-134">Selecteer de **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="c28c4-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="c28c4-135">Nadat de Partner-blade wordt geopend, selecteert u de partner die u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="c28c4-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="c28c4-136">Kies **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="c28c4-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="c28c4-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c28c4-137">Next steps</span></span>
* [<span data-ttu-id="c28c4-138">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="c28c4-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  

