---
title: aaaHow beheren van gebruikersaccounts in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toocreate of uitnodiging gebruikers in Azure API Management
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a><span data-ttu-id="7a204-103">Hoe toomanage gebruikersaccounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7a204-103">How toomanage user accounts in Azure API Management</span></span>
<span data-ttu-id="7a204-104">In API Management zijn ontwikkelaars Hallo gebruikers Hallo API's die u met behulp van API Management.</span><span class="sxs-lookup"><span data-stu-id="7a204-104">In API Management, developers are hello users of hello APIs that you expose using API Management.</span></span> <span data-ttu-id="7a204-105">Deze handleiding bevat toohow toocreate en uitnodiging ontwikkelaars toouse Hallo API's en producten toothem beschikbaar te maken met uw API Management-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="7a204-105">This guide shows toohow toocreate and invite developers toouse hello APIs and products that you make available toothem with your API Management instance.</span></span> <span data-ttu-id="7a204-106">Zie voor informatie over het beheren van gebruikersaccounts programmatisch Hallo [entiteit gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentatie in Hallo [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) verwijzing.</span><span class="sxs-lookup"><span data-stu-id="7a204-106">For information on managing user accounts programmatically, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="7a204-107"><a name="create-developer"></a>Maken van een nieuwe ontwikkelaar</span><span class="sxs-lookup"><span data-stu-id="7a204-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="7a204-108">een nieuwe ontwikkelaar toocreate klikt u op **publicatieportal** in hello Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="7a204-108">toocreate a new developer, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="7a204-109">Hiermee gaat u toohello API Management-publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="7a204-109">This takes you toohello API Management publisher portal.</span></span> <span data-ttu-id="7a204-110">Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [aan de slag met Azure API Management] [ Get started with Azure API Management] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7a204-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="7a204-112">Klik op **gebruikers** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7a204-112">Click **Users** from hello **API Management** menu on hello left, and then click **add user**.</span></span>

![Ontwikkelaars maken][api-management-create-developer]

<span data-ttu-id="7a204-114">Voer Hallo **e**, **wachtwoord**, en **naam** voor nieuwe developer Hallo en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7a204-114">Enter hello **Email**, **Password**, and **Name** for hello new developer and click **Save**.</span></span>

![Ontwikkelaars maken][api-management-add-new-user]

<span data-ttu-id="7a204-116">De van de zojuist gemaakte ontwikkelaarsaccounts zijn standaard **Active**, en die zijn gekoppeld aan Hallo **ontwikkelaars** groep.</span><span class="sxs-lookup"><span data-stu-id="7a204-116">By default, newly created developer accounts are **Active**, and associated with hello **Developers** group.</span></span>

![Nieuwe ontwikkelaars][api-management-new-developer]

<span data-ttu-id="7a204-118">Ontwikkelaarsaccounts die zich in een **active** status gebruikte tooaccess kan worden alle Hallo-API's waarvoor ze abonnementen hebben.</span><span class="sxs-lookup"><span data-stu-id="7a204-118">Developer accounts that are in an **active** state can be used tooaccess all of hello APIs for which they have subscriptions.</span></span> <span data-ttu-id="7a204-119">Zie tooassociate Hallo nieuw gemaakte developer met extra groepen [hoe tooassociate groepen met ontwikkelaars][How tooassociate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="7a204-119">tooassociate hello newly created developer with additional groups, see [How tooassociate groups with developers][How tooassociate groups with developers].</span></span>

## <span data-ttu-id="7a204-120"><a name="invite-developer"></a>Een ontwikkelaar uitnodigen</span><span class="sxs-lookup"><span data-stu-id="7a204-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="7a204-121">tooinvite een ontwikkelaar, klikt u op **gebruikers** van Hallo **API Management** menu op Hallo links en klik vervolgens op **gebruiker uit te nodigen**.</span><span class="sxs-lookup"><span data-stu-id="7a204-121">tooinvite a developer, click **Users** from hello **API Management** menu on hello left, and then click **Invite User**.</span></span>

![Developer uit te nodigen][api-management-invite-developer]

<span data-ttu-id="7a204-123">Voer Hallo naam en e-mailadres van de ontwikkelaar Hallo van, en klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="7a204-123">Enter hello name and email address of hello developer, and click **Invite**.</span></span>

![Developer uit te nodigen][api-management-invite-developer-window]

<span data-ttu-id="7a204-125">Een bevestigingsbericht wordt weergegeven, maar Hallo zojuist uitgenodigd developer niet wordt weergegeven in lijst Hallo pas nadat ze Hallo uitnodiging accepteren.</span><span class="sxs-lookup"><span data-stu-id="7a204-125">A confirmation message is displayed, but hello newly invited developer does not appear in hello list until after they accept hello invitation.</span></span> 

![Bevestiging uitnodigen][api-management-invite-developer-confirmation]

<span data-ttu-id="7a204-127">Als een ontwikkelaar uitgenodigd is, wordt een e-mailbericht toohello developer verzonden.</span><span class="sxs-lookup"><span data-stu-id="7a204-127">When a developer is invited, an email is sent toohello developer.</span></span> <span data-ttu-id="7a204-128">Dit e-mailbericht met een sjabloon wordt gegenereerd en kan worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="7a204-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="7a204-129">Zie voor meer informatie [e-mailsjablonen configureren][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="7a204-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="7a204-130">Zodra het Hallo-uitnodiging is geaccepteerd, actief Hallo account.</span><span class="sxs-lookup"><span data-stu-id="7a204-130">Once hello invitation is accepted, hello account becomes active.</span></span>

## <span data-ttu-id="7a204-131"><a name="block-developer"></a> Deactiveren of opnieuw activeren een ontwikkelaarsaccount</span><span class="sxs-lookup"><span data-stu-id="7a204-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="7a204-132">Gemaakte of uitgenodigde ontwikkelaarsaccounts zijn standaard **Active**.</span><span class="sxs-lookup"><span data-stu-id="7a204-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="7a204-133">een ontwikkelaarsaccount toodeactivate klikt u op **blok**.</span><span class="sxs-lookup"><span data-stu-id="7a204-133">toodeactivate a developer account, click **Block**.</span></span> <span data-ttu-id="7a204-134">tooreactivate een geblokkeerde ontwikkelaarsaccount, klikt u op **activeren**.</span><span class="sxs-lookup"><span data-stu-id="7a204-134">tooreactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="7a204-135">Een geblokkeerde ontwikkelaarsaccount kan geen toegang tot de ontwikkelaarsportal Hallo of alle API's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="7a204-135">A blocked developer account can not access hello developer portal or call any APIs.</span></span> <span data-ttu-id="7a204-136">toodelete een gebruikersaccount, klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="7a204-136">toodelete a user account, click **Delete**.</span></span>

![Blok-ontwikkelaars][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="7a204-138">Een gebruikerswachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="7a204-138">Reset a user password</span></span>
<span data-ttu-id="7a204-139">tooreset hello wachtwoord voor een gebruikersaccount, klik op Hallo-naam van het Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="7a204-139">tooreset hello password for a user account, click hello name of hello account.</span></span>

![Wachtwoord opnieuw instellen][api-management-view-developer]

<span data-ttu-id="7a204-141">Klik op **wachtwoord opnieuw instellen** toosend een koppeling toohello gebruiker tooreset hun wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7a204-141">Click **Reset password** toosend a link toohello user tooreset their password.</span></span>

![Wachtwoord opnieuw instellen][api-management-reset-password]

<span data-ttu-id="7a204-143">tooprogrammatically werken met gebruikersaccounts, Zie Hallo [entiteit gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentatie in Hallo [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) verwijzing.</span><span class="sxs-lookup"><span data-stu-id="7a204-143">tooprogrammatically work with user accounts, see hello [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in hello [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="7a204-144">een gebruiker account wachtwoord tooa specifieke waarde tooreset, kunt u Hallo [bijwerken van een gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) bewerking en geef de gewenste wachtwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a204-144">tooreset a user account password tooa specific value, you can use hello [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify hello desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="7a204-145">Verificatie van in behandeling</span><span class="sxs-lookup"><span data-stu-id="7a204-145">Pending verification</span></span>
![Verificatie van in behandeling][api-management-pending-verification]

## <span data-ttu-id="7a204-147"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a204-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="7a204-148">Zodra een ontwikkelaarsaccount is gemaakt, kunt u aan functies koppelen en het abonneren tooproducts en API's.</span><span class="sxs-lookup"><span data-stu-id="7a204-148">Once a developer account is created, you can associate it with roles and subscribe it tooproducts and APIs.</span></span> <span data-ttu-id="7a204-149">Zie voor meer informatie [hoe toocreate en gebruik groepen][How toocreate and use groups].</span><span class="sxs-lookup"><span data-stu-id="7a204-149">For more information, see [How toocreate and use groups][How toocreate and use groups].</span></span>

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
