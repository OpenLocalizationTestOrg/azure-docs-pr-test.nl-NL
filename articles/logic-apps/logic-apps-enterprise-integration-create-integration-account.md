---
title: Maken, koppelen, verwijderen of verplaatsen van een account integratie in Azure logic apps | Microsoft Docs
description: Het maken van een account integratie en koppel deze aan uw logische apps
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
ms.openlocfilehash: 716e7b5bab8725dea0fd2b760d0e46e8e892c5b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="a159d-103">Wat is een integratie-account?</span><span class="sxs-lookup"><span data-stu-id="a159d-103">What is an integration account?</span></span>

<span data-ttu-id="a159d-104">Een account integratie kunt enterprise integratie-apps voor het beheren van artefacten, met inbegrip van schema's, kaarten, certificaten, partners en -overeenkomsten.</span><span class="sxs-lookup"><span data-stu-id="a159d-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="a159d-105">Integratie van apps die hebt u gebruikmaakt van een integratie-account voor toegang tot deze schema's, kaarten, certificaten, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="a159d-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="a159d-106">Een integratie-account maken</span><span class="sxs-lookup"><span data-stu-id="a159d-106">Create an integration account</span></span>

1.  <span data-ttu-id="a159d-107">Meld u aan bij [Azure Portal](http://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="a159d-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="a159d-108">Selecteer in het menu links **meer services**.</span><span class="sxs-lookup"><span data-stu-id="a159d-108">From the left menu, select **More services**.</span></span>

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="a159d-110">Typ in het zoekvak '-integratie"voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="a159d-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="a159d-111">Selecteer in de lijst met resultaten **Integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="a159d-111">In the results list, select **Integration Accounts**.</span></span>

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="a159d-113">Kies aan de bovenkant van de pagina **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a159d-113">At the top of the page, choose **Add**.</span></span>

    ![Kies toevoegen](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="a159d-115">Naam van uw account integratie en selecteer de Azure-abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a159d-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="a159d-116">U kunt een nieuwe maken **resourcegroep** of Selecteer een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a159d-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="a159d-117">Selecteer vervolgens een **locatie** voor het hosten van uw account integratie en een **prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="a159d-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="a159d-118">Als u klaar bent, kiest u **maken**.</span><span class="sxs-lookup"><span data-stu-id="a159d-118">When you're ready, choose **Create**.</span></span>

    ![Informatie opgeven voor uw account integratie](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="a159d-120">Azure richt uw integratie-account in de geselecteerde locatie, die moet worden voltooid binnen 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="a159d-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="a159d-121">Vernieuw de pagina.</span><span class="sxs-lookup"><span data-stu-id="a159d-121">Refresh the page.</span></span> <span data-ttu-id="a159d-122">U ziet uw nieuwe integratie account weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a159d-122">You see your new integration account listed.</span></span>

    ![Uw nieuwe account voor de integratie wordt weergegeven](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="a159d-124">Koppel vervolgens de integratie-account dat u aan uw logische app hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a159d-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="a159d-125">Een integratie-account koppelen aan een logische app</span><span class="sxs-lookup"><span data-stu-id="a159d-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="a159d-126">Uw logische apps om toegang te verlenen aan maps, schema's, overeenkomsten en andere artefacten in uw account integratie, door de integratie-account te koppelen aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="a159d-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a159d-127">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a159d-127">Prerequisites</span></span>

* <span data-ttu-id="a159d-128">Een account voor de integratie</span><span class="sxs-lookup"><span data-stu-id="a159d-128">An integration account</span></span>
* <span data-ttu-id="a159d-129">Een logische app</span><span class="sxs-lookup"><span data-stu-id="a159d-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="a159d-130">Zorg ervoor dat uw account en logica app voor integratie zijn in de *dezelfde Azure-locatie* voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="a159d-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="a159d-131">In de Azure portal, selecteer uw logische app en uw logische app locatie controleren.</span><span class="sxs-lookup"><span data-stu-id="a159d-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selecteer uw logische app, locatie controleren](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="a159d-133">Onder **instellingen**, selecteer **integratie Account**.</span><span class="sxs-lookup"><span data-stu-id="a159d-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selecteer 'Integratie Account'](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="a159d-135">Van de **selecteert u een account integratie** , selecteert u de integratie-account dat u wilt koppelen aan uw logische app.</span><span class="sxs-lookup"><span data-stu-id="a159d-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="a159d-136">Kies voor het voltooien van de koppeling **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="a159d-136">To finish linking, choose **Save**.</span></span>

    ![Selecteer uw integratie-account](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="a159d-138">Krijgt u een melding dat uw integratie account is gekoppeld aan uw logische app en alle artefacten in uw account integratie zijn nu beschikbaar voor uw logische app weergeeft.</span><span class="sxs-lookup"><span data-stu-id="a159d-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![Uw logische app is gekoppeld aan uw account integratie](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="a159d-140">Nu uw integratie-account is gekoppeld aan uw logische app, kunt u de B2B-connectors gebruiken in logic apps.</span><span class="sxs-lookup"><span data-stu-id="a159d-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="a159d-141">Sommige algemene B2B-connectors zijn XML-validatie en plat bestand coderen/decoderen.</span><span class="sxs-lookup"><span data-stu-id="a159d-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="a159d-142">Uw account integratie verwijderen</span><span class="sxs-lookup"><span data-stu-id="a159d-142">Delete your integration account</span></span>

1. <span data-ttu-id="a159d-143">Selecteer **meer services**.</span><span class="sxs-lookup"><span data-stu-id="a159d-143">Select **More services**.</span></span>

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="a159d-145">Typ in het zoekvak '-integratie"voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="a159d-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="a159d-146">Selecteer in de lijst met resultaten **Integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="a159d-146">In the results list, select **Integration Accounts**.</span></span>

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="a159d-148">Selecteer de integratie-account dat u wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a159d-148">Select the integration account that you want to delete.</span></span>

    ![Selecteer integratie-account verwijderen](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="a159d-150">Kies in het menu **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="a159d-150">On the menu, choose **Delete**.</span></span>

    ![Kies 'Verwijderen'](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="a159d-152">Bevestig uw keuze om de integratie-account te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a159d-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="a159d-153">Uw account integratie verplaatsen</span><span class="sxs-lookup"><span data-stu-id="a159d-153">Move your integration account</span></span>

<span data-ttu-id="a159d-154">Volg deze stappen om een account integratie naar een andere Azure-abonnement of resourcegroep groep verplaatst.</span><span class="sxs-lookup"><span data-stu-id="a159d-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a159d-155">Alle scripts voor het gebruik van de nieuwe resource-id nadat u een account integratie verplaatst, moet u bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a159d-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="a159d-156">Selecteer **meer services**.</span><span class="sxs-lookup"><span data-stu-id="a159d-156">Select **More services**.</span></span>

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="a159d-158">Typ in het zoekvak '-integratie"voor uw filter.</span><span class="sxs-lookup"><span data-stu-id="a159d-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="a159d-159">Selecteer in de lijst met resultaten **Integratieaccounts**.</span><span class="sxs-lookup"><span data-stu-id="a159d-159">In the results list, select **Integration Accounts**.</span></span>

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="a159d-161">Selecteer de integratie-account dat u wilt verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="a159d-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="a159d-162">Onder **instellingen**, kies **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a159d-162">Under **Settings**, choose **Properties**.</span></span>

    ![Selecteer de account integratie te verplaatsen.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="a159d-165">De resourcegroep of een Azure-abonnement dat is gekoppeld aan uw account integratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a159d-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Kies wijziging resourcegroep of abonnement wijzigen](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="a159d-167">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a159d-167">Next Steps</span></span>
* [<span data-ttu-id="a159d-168">Meer informatie over de overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="a159d-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  

