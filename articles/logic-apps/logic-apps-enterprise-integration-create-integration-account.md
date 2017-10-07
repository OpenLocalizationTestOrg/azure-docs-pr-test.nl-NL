---
title: aaaCreate, koppelen, verwijderen of verplaatsen van een account integratie in Azure logic apps | Microsoft Docs
description: Hoe een integratie toocreate account en een koppeling tooyour logic apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="1a090-103">Wat is een integratie-account?</span><span class="sxs-lookup"><span data-stu-id="1a090-103">What is an integration account?</span></span>

<span data-ttu-id="1a090-104">Een account integratie kunt enterprise integration apps toomanage artefacten, met inbegrip van schema's, kaarten, certificaten, partners en -overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="1a090-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="1a090-105">Elke integratie-app die u gebruikt een account integratie tooaccess deze schema's, kaarten, certificaten, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="1a090-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="1a090-106">Een integratie-account maken</span><span class="sxs-lookup"><span data-stu-id="1a090-106">Create an integration account</span></span>

1.  <span data-ttu-id="1a090-107">Meld u aan toohello [Azure-portal](http://portal.azure.com "Azure-portal").</span><span class="sxs-lookup"><span data-stu-id="1a090-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="1a090-108">Selecteer in het linkermenu Hallo **meer services**.</span><span class="sxs-lookup"><span data-stu-id="1a090-108">From hello left menu, select **More services**.</span></span>

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1a090-110">Typ in het zoekvak hello, '-integratie"voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="1a090-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="1a090-111">Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="1a090-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1a090-113">Kies bovenaan Hallo Hallo pagina, **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1a090-113">At hello top of hello page, choose **Add**.</span></span>

    ![Kies toevoegen](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="1a090-115">Naam van uw account integratie en selecteer hello Azure-abonnement dat u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="1a090-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="1a090-116">U kunt een nieuwe maken **resourcegroep** of Selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1a090-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="1a090-117">Selecteer vervolgens een **locatie** voor het hosten van uw account integratie en een **prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="1a090-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="1a090-118">Als u klaar bent, kiest u **maken**.</span><span class="sxs-lookup"><span data-stu-id="1a090-118">When you're ready, choose **Create**.</span></span>

    ![Informatie opgeven voor uw account integratie](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="1a090-120">Azure richt uw account integratie in Hallo geselecteerd locatie, die moet worden voltooid binnen 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="1a090-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="1a090-121">Hallo pagina vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="1a090-121">Refresh hello page.</span></span> <span data-ttu-id="1a090-122">U ziet uw nieuwe integratie account weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1a090-122">You see your new integration account listed.</span></span>

    ![Uw nieuwe account voor de integratie wordt weergegeven](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="1a090-124">Vervolgens koppel Hallo integratie-account dat u gemaakte tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="1a090-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="1a090-125">Een integratie account tooa logische app koppelen</span><span class="sxs-lookup"><span data-stu-id="1a090-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="1a090-126">toogive uw logische apps toegang krijgen tot toomaps, schema's, overeenkomsten en andere artefacten in uw account integratie, koppeling Hallo integratie account tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="1a090-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1a090-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a090-127">Prerequisites</span></span>

* <span data-ttu-id="1a090-128">Een account voor de integratie</span><span class="sxs-lookup"><span data-stu-id="1a090-128">An integration account</span></span>
* <span data-ttu-id="1a090-129">Een logische app</span><span class="sxs-lookup"><span data-stu-id="1a090-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="1a090-130">Zorg ervoor dat uw account en logica app voor integratie in Hallo *dezelfde Azure-locatie* voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="1a090-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="1a090-131">Selecteer uw logische app in hello Azure-portal, en controleer uw logische app locatie.</span><span class="sxs-lookup"><span data-stu-id="1a090-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selecteer uw logische app, locatie controleren](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="1a090-133">Onder **instellingen**, selecteer **integratie Account**.</span><span class="sxs-lookup"><span data-stu-id="1a090-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selecteer 'Integratie Account'](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="1a090-135">Van Hallo **selecteert u een account integratie** wilt weergeven, selecteer Hallo integratie account u wilt dat toolink tooyour logische app.</span><span class="sxs-lookup"><span data-stu-id="1a090-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="1a090-136">toofinish koppelt, kies **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1a090-136">toofinish linking, choose **Save**.</span></span>

    ![Selecteer uw integratie-account](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="1a090-138">Krijgt u een melding dat uw integratie-account is gekoppeld tooyour logische app en alle artefacten in uw account integratie zijn nu beschikbaar tooyour logische app weergeeft.</span><span class="sxs-lookup"><span data-stu-id="1a090-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Uw logische app is gekoppeld tooyour integratie-account](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="1a090-140">Nu dat uw account integratie gekoppelde tooyour logic app is, kunt u Hallo B2B-connectors kunt gebruiken in logic apps.</span><span class="sxs-lookup"><span data-stu-id="1a090-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="1a090-141">Sommige algemene B2B-connectors zijn XML-validatie en plat bestand coderen/decoderen.</span><span class="sxs-lookup"><span data-stu-id="1a090-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="1a090-142">Uw account integratie verwijderen</span><span class="sxs-lookup"><span data-stu-id="1a090-142">Delete your integration account</span></span>

1. <span data-ttu-id="1a090-143">Selecteer **meer services**.</span><span class="sxs-lookup"><span data-stu-id="1a090-143">Select **More services**.</span></span>

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1a090-145">Typ in het zoekvak hello, '-integratie"voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="1a090-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="1a090-146">Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="1a090-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1a090-148">Hallo-integratie-account dat u wilt dat toodelete selecteren.</span><span class="sxs-lookup"><span data-stu-id="1a090-148">Select hello integration account that you want toodelete.</span></span>

    ![Integratie account toodelete selecteren](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="1a090-150">Kies Hallo menu **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1a090-150">On hello menu, choose **Delete**.</span></span>

    ![Kies 'Verwijderen'](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="1a090-152">Bevestig uw keuze toodelete Hallo integratie-account.</span><span class="sxs-lookup"><span data-stu-id="1a090-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="1a090-153">Uw account integratie verplaatsen</span><span class="sxs-lookup"><span data-stu-id="1a090-153">Move your integration account</span></span>

<span data-ttu-id="1a090-154">toomove een integratie account tooanother Azure-abonnement of de resource-groep, volg deze stappen.</span><span class="sxs-lookup"><span data-stu-id="1a090-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a090-155">Nadat u een account integratie verplaatst, moet u alle scripts toouse Hallo nieuwe resource-id's bijwerken.</span><span class="sxs-lookup"><span data-stu-id="1a090-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="1a090-156">Selecteer **meer services**.</span><span class="sxs-lookup"><span data-stu-id="1a090-156">Select **More services**.</span></span>

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1a090-158">Typ in het zoekvak hello, '-integratie"voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="1a090-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="1a090-159">Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="1a090-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="1a090-161">Hallo-integratie-account dat u wilt dat toomove selecteren.</span><span class="sxs-lookup"><span data-stu-id="1a090-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="1a090-162">Onder **instellingen**, kies **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="1a090-162">Under **Settings**, choose **Properties**.</span></span>

    ![Selecteer integratie account toomove.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="1a090-165">Hallo resourcegroep of Azure-abonnement dat is gekoppeld aan uw account integratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1a090-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Kies wijziging resourcegroep of abonnement wijzigen](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="1a090-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1a090-167">Next Steps</span></span>
* [<span data-ttu-id="1a090-168">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="1a090-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  

