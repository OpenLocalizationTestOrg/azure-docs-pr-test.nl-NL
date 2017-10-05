---
title: Hoe beheert u gebruikersaccounts in Azure API Management | Microsoft Docs
description: Meer informatie over het maken of uitnodigen gebruikers in Azure API Management
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
ms.openlocfilehash: d3a50f6d22cbf1797f580078bc0d2cc9cefe5064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-user-accounts-in-azure-api-management"></a><span data-ttu-id="14bb8-103">Het beheren van gebruikersaccounts in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="14bb8-103">How to manage user accounts in Azure API Management</span></span>
<span data-ttu-id="14bb8-104">In API Management zijn ontwikkelaars de gebruikers van de API's die u met behulp van API Management.</span><span class="sxs-lookup"><span data-stu-id="14bb8-104">In API Management, developers are the users of the APIs that you expose using API Management.</span></span> <span data-ttu-id="14bb8-105">Deze handleiding wordt beschreven voor het maken en uit te nodigen ontwikkelaars met de API's en -producten te maken die voor hen beschikbaar met uw API Management-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="14bb8-105">This guide shows to how to create and invite developers to use the APIs and products that you make available to them with your API Management instance.</span></span> <span data-ttu-id="14bb8-106">Zie voor informatie over het beheren van gebruikersaccounts via een programma, het [entiteit gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentatie in de [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) verwijzing.</span><span class="sxs-lookup"><span data-stu-id="14bb8-106">For information on managing user accounts programmatically, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span>

## <span data-ttu-id="14bb8-107"><a name="create-developer"></a>Maken van een nieuwe ontwikkelaar</span><span class="sxs-lookup"><span data-stu-id="14bb8-107"><a name="create-developer"> </a>Create a new developer</span></span>
<span data-ttu-id="14bb8-108">Klik op om een nieuwe ontwikkelaar **publicatieportal** in de Azure-Portal voor uw API Management-service.</span><span class="sxs-lookup"><span data-stu-id="14bb8-108">To create a new developer, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="14bb8-109">Hiermee gaat u naar de publicatieportal van API Management.</span><span class="sxs-lookup"><span data-stu-id="14bb8-109">This takes you to the API Management publisher portal.</span></span> <span data-ttu-id="14bb8-110">Als u nog geen service-exemplaar van API Management hebt gemaakt, raadpleegt u [Service-exemplaar van API Management maken][Create an API Management service instance] in de zelfstudie [Aan de slag met Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="14bb8-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Publicatieportal][api-management-management-console]

<span data-ttu-id="14bb8-112">Klik op **gebruikers** van de **API Management** menu aan de linkerkant en klik vervolgens op **gebruiker toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-112">Click **Users** from the **API Management** menu on the left, and then click **add user**.</span></span>

![Ontwikkelaars maken][api-management-create-developer]

<span data-ttu-id="14bb8-114">Voer de **e**, **wachtwoord**, en **naam** voor de nieuwe ontwikkelaars en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-114">Enter the **Email**, **Password**, and **Name** for the new developer and click **Save**.</span></span>

![Ontwikkelaars maken][api-management-add-new-user]

<span data-ttu-id="14bb8-116">De van de zojuist gemaakte ontwikkelaarsaccounts zijn standaard **Active**, en die zijn gekoppeld aan de **ontwikkelaars** groep.</span><span class="sxs-lookup"><span data-stu-id="14bb8-116">By default, newly created developer accounts are **Active**, and associated with the **Developers** group.</span></span>

![Nieuwe ontwikkelaars][api-management-new-developer]

<span data-ttu-id="14bb8-118">Ontwikkelaarsaccounts die zich in een **active** status kan worden gebruikt voor toegang tot alle van de API's waarvoor ze abonnementen hebben.</span><span class="sxs-lookup"><span data-stu-id="14bb8-118">Developer accounts that are in an **active** state can be used to access all of the APIs for which they have subscriptions.</span></span> <span data-ttu-id="14bb8-119">De ontwikkelaar van de zojuist gemaakte koppelt u extra groepen, Zie [groepen koppelen aan ontwikkelaars][How to associate groups with developers].</span><span class="sxs-lookup"><span data-stu-id="14bb8-119">To associate the newly created developer with additional groups, see [How to associate groups with developers][How to associate groups with developers].</span></span>

## <span data-ttu-id="14bb8-120"><a name="invite-developer"></a>Een ontwikkelaar uitnodigen</span><span class="sxs-lookup"><span data-stu-id="14bb8-120"><a name="invite-developer"> </a>Invite a developer</span></span>
<span data-ttu-id="14bb8-121">Als u wilt een ontwikkelaar uitnodigen, klikt u op **gebruikers** van de **API Management** menu aan de linkerkant en klik vervolgens op **gebruiker uit te nodigen**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-121">To invite a developer, click **Users** from the **API Management** menu on the left, and then click **Invite User**.</span></span>

![Developer uit te nodigen][api-management-invite-developer]

<span data-ttu-id="14bb8-123">Voer de naam en e-mailadres van de ontwikkelaar, en klik op **uitnodigen**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-123">Enter the name and email address of the developer, and click **Invite**.</span></span>

![Developer uit te nodigen][api-management-invite-developer-window]

<span data-ttu-id="14bb8-125">Een bevestigingsbericht wordt weergegeven, maar de ontwikkelaar van de nieuwe uitgenodigde niet wordt weergegeven in de lijst pas nadat ze de uitnodiging accepteren.</span><span class="sxs-lookup"><span data-stu-id="14bb8-125">A confirmation message is displayed, but the newly invited developer does not appear in the list until after they accept the invitation.</span></span> 

![Bevestiging uitnodigen][api-management-invite-developer-confirmation]

<span data-ttu-id="14bb8-127">Wanneer een ontwikkelaar wordt verzocht, wordt een e-mailbericht verzonden naar de ontwikkelaar.</span><span class="sxs-lookup"><span data-stu-id="14bb8-127">When a developer is invited, an email is sent to the developer.</span></span> <span data-ttu-id="14bb8-128">Dit e-mailbericht met een sjabloon wordt gegenereerd en kan worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="14bb8-128">This email is generated using a template and is customizable.</span></span> <span data-ttu-id="14bb8-129">Zie voor meer informatie [e-mailsjablonen configureren][Configure email templates].</span><span class="sxs-lookup"><span data-stu-id="14bb8-129">For more information, see [Configure email templates][Configure email templates].</span></span>

<span data-ttu-id="14bb8-130">Zodra de uitnodiging is geaccepteerd, wordt het account actief.</span><span class="sxs-lookup"><span data-stu-id="14bb8-130">Once the invitation is accepted, the account becomes active.</span></span>

## <span data-ttu-id="14bb8-131"><a name="block-developer"></a> Deactiveren of opnieuw activeren een ontwikkelaarsaccount</span><span class="sxs-lookup"><span data-stu-id="14bb8-131"><a name="block-developer"> </a> Deactivate or reactivate a developer account</span></span>
<span data-ttu-id="14bb8-132">Gemaakte of uitgenodigde ontwikkelaarsaccounts zijn standaard **Active**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-132">By default, newly created or invited developer accounts are **Active**.</span></span> <span data-ttu-id="14bb8-133">U kunt een ontwikkelaarsaccount, klikt u op **blok**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-133">To deactivate a developer account, click **Block**.</span></span> <span data-ttu-id="14bb8-134">Als u wilt een geblokkeerde ontwikkelaarsaccount activeren, klikt u op **activeren**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-134">To reactivate a blocked developer account, click **Activate**.</span></span> <span data-ttu-id="14bb8-135">Een geblokkeerde ontwikkelaarsaccount kan geen toegang tot de portal voor ontwikkelaars of alle API's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="14bb8-135">A blocked developer account can not access the developer portal or call any APIs.</span></span> <span data-ttu-id="14bb8-136">Als u wilt verwijderen van een gebruikersaccount, klikt u op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="14bb8-136">To delete a user account, click **Delete**.</span></span>

![Blok-ontwikkelaars][api-management-new-developer]

## <a name="reset-a-user-password"></a><span data-ttu-id="14bb8-138">Een gebruikerswachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="14bb8-138">Reset a user password</span></span>
<span data-ttu-id="14bb8-139">Als u het wachtwoord voor een gebruikersaccount herstellen, klikt u op de naam van het account.</span><span class="sxs-lookup"><span data-stu-id="14bb8-139">To reset the password for a user account, click the name of the account.</span></span>

![Wachtwoord opnieuw instellen][api-management-view-developer]

<span data-ttu-id="14bb8-141">Klik op **wachtwoord opnieuw instellen** een koppeling naar de gebruiker om hun wachtwoord opnieuw in te verzenden.</span><span class="sxs-lookup"><span data-stu-id="14bb8-141">Click **Reset password** to send a link to the user to reset their password.</span></span>

![Wachtwoord opnieuw instellen][api-management-reset-password]

<span data-ttu-id="14bb8-143">Om te werken via een programma met een gebruikersaccount, Zie de [entiteit gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentatie in de [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) verwijzing.</span><span class="sxs-lookup"><span data-stu-id="14bb8-143">To programmatically work with user accounts, see the [User entity](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentation in the [API Management REST](https://msdn.microsoft.com/library/azure/dn776326.aspx) reference.</span></span> <span data-ttu-id="14bb8-144">Als u het wachtwoord van een gebruiker op een specifieke waarde herstellen, kunt u de [bijwerken van een gebruiker](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) bewerking en geef het gewenste wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="14bb8-144">To reset a user account password to a specific value, you can use the [Update a user](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operation and specify the desired password.</span></span>

## <a name="pending-verification"></a><span data-ttu-id="14bb8-145">Verificatie van in behandeling</span><span class="sxs-lookup"><span data-stu-id="14bb8-145">Pending verification</span></span>
![Verificatie van in behandeling][api-management-pending-verification]

## <span data-ttu-id="14bb8-147"><a name="next-steps"> </a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14bb8-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="14bb8-148">Zodra een ontwikkelaarsaccount is gemaakt, kunt u aan functies koppelen en deze zich te abonneren op producten en -API's.</span><span class="sxs-lookup"><span data-stu-id="14bb8-148">Once a developer account is created, you can associate it with roles and subscribe it to products and APIs.</span></span> <span data-ttu-id="14bb8-149">Zie voor meer informatie [maken en gebruiken van groepen][How to create and use groups].</span><span class="sxs-lookup"><span data-stu-id="14bb8-149">For more information, see [How to create and use groups][How to create and use groups].</span></span>

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
[How to create and use groups]: api-management-howto-create-groups.md
[How to associate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
