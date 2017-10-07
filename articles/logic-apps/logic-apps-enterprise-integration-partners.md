---
title: aaaCreate partners voor berichten in business-to-business (B2B) - Azure Logic Apps | Microsoft Docs
description: Meer informatie over hoe tooadd partners tooyour integratie met Enterprise Integration Pack Hallo en Logic Apps-account
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
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="3895c-103">Toevoegen of bijwerken van partners in uw werkstroom business-to-business-overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="3895c-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="3895c-104">Partners zijn entiteiten die deelnemen aan business-to-business (B2B) transacties en uitwisselen van berichten tussen elkaar.</span><span class="sxs-lookup"><span data-stu-id="3895c-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="3895c-105">Voordat u partners die u en een andere organisatie deze transacties vertegenwoordigen maken kunt, moet u beide delen van gegevens die u identificeert en berichten is verzonden door elkaar worden gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="3895c-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="3895c-106">Nadat u deze gegevens worden behandeld en u klaar toostart uw zakelijke relatie bent, kunt u partners in uw account integratie toorepresent u beide.</span><span class="sxs-lookup"><span data-stu-id="3895c-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="3895c-107">Welke rollen hebt partners in uw integratie-account?</span><span class="sxs-lookup"><span data-stu-id="3895c-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="3895c-108">toodefine informatie over het Hallo-berichten uitgewisseld tussen partners, maakt u overeenkomsten tussen de partners.</span><span class="sxs-lookup"><span data-stu-id="3895c-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="3895c-109">Echter, voordat u een overeenkomst maken kunt, moet u hebben toegevoegd ten minste twee partners tooyour integratie-account.</span><span class="sxs-lookup"><span data-stu-id="3895c-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="3895c-110">Uw organisatie moet deel uitmaken van de overeenkomst Hallo als Hallo **host partner**.</span><span class="sxs-lookup"><span data-stu-id="3895c-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="3895c-111">Hallo andere partner of **Gast partner** vertegenwoordigt Hallo organisatie die berichten met uw organisatie worden uitgewisseld.</span><span class="sxs-lookup"><span data-stu-id="3895c-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="3895c-112">Hallo Gast partner kan zijn van een ander bedrijf, of zelfs een afdeling in uw eigen organisatie.</span><span class="sxs-lookup"><span data-stu-id="3895c-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="3895c-113">Nadat u deze partners hebt toegevoegd, kunt u een overeenkomst kunt maken.</span><span class="sxs-lookup"><span data-stu-id="3895c-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="3895c-114">Ontvangen en verzenden van de instellingen zijn gericht uit oogpunt Hallo Hallo gehoste Partner.</span><span class="sxs-lookup"><span data-stu-id="3895c-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="3895c-115">Bijvoorbeeld, Hallo instellingen in een overeenkomst ontvangen bepalen hoe Hallo gehost partner ontvangt berichten die worden verzonden vanaf een partner Gast.</span><span class="sxs-lookup"><span data-stu-id="3895c-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="3895c-116">Op dezelfde manier Hallo verzendinstellingen op Hallo overeenkomst aangeven hoe Hallo gehost partner verzendt berichten toohello Gast partner.</span><span class="sxs-lookup"><span data-stu-id="3895c-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="3895c-117">Hoe toocreate een partner?</span><span class="sxs-lookup"><span data-stu-id="3895c-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="3895c-118">Selecteer in de Azure-portal hello, **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="3895c-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="3895c-119">Voer in het zoekvak Hallo-filter, **integratie**, selecteer daarna **Integratieaccounts** in de lijst met resultaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="3895c-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="3895c-120">Selecteer Hallo integratie account waar u tooadd uw partners.</span><span class="sxs-lookup"><span data-stu-id="3895c-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="3895c-121">Selecteer Hallo **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="3895c-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="3895c-122">Kies in de blade Hallo Partners **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3895c-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="3895c-123">Voer een naam voor uw partner en selecteer vervolgens een **kwalificatie**.</span><span class="sxs-lookup"><span data-stu-id="3895c-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="3895c-124">Voer ten slotte een **waarde** toohelp documenten die worden geleverd in uw apps bepalen.</span><span class="sxs-lookup"><span data-stu-id="3895c-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="3895c-125">toosee hello uitgevoerd voor uw partner-maakproces Selecteer Hallo *bel* meldingspictogram.</span><span class="sxs-lookup"><span data-stu-id="3895c-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="3895c-126">tooconfirm die uw nieuwe partners zijn toegevoegd, selecteer Hallo **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="3895c-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="3895c-127">Nadat u Hallo Partners tegel selecteert, ziet u ook toegevoegde partners Hallo Partners blade.</span><span class="sxs-lookup"><span data-stu-id="3895c-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="3895c-128">Hoe tooedit bestaande partners in uw account integratie</span><span class="sxs-lookup"><span data-stu-id="3895c-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="3895c-129">Selecteer Hallo **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="3895c-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="3895c-130">Nadat het Hallo Partners blade wordt geopend, selecteert u Hallo partner die u wilt dat tooedit.</span><span class="sxs-lookup"><span data-stu-id="3895c-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="3895c-131">Op Hallo **Update Partner** tegel, breng uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="3895c-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="3895c-132">Nadat u bent klaar, kiest u **opslaan**, of selecteert u uw wijzigingen toocancel **negeren**.</span><span class="sxs-lookup"><span data-stu-id="3895c-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="3895c-133">Hoe toodelete een partner</span><span class="sxs-lookup"><span data-stu-id="3895c-133">How toodelete a partner</span></span>

1. <span data-ttu-id="3895c-134">Selecteer Hallo **Partners** tegel.</span><span class="sxs-lookup"><span data-stu-id="3895c-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="3895c-135">Nadat het Hallo Partner blade wordt geopend, selecteert u Hallo partner die u toodelete wilt.</span><span class="sxs-lookup"><span data-stu-id="3895c-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="3895c-136">Kies **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="3895c-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="3895c-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3895c-137">Next steps</span></span>
* [<span data-ttu-id="3895c-138">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="3895c-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  

