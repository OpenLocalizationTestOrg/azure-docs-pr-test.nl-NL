---
title: Toegang tot Azure-facturering rollen beheren | Microsoft Docs
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: c70904097f139bc2178feed83f1cf1274f3c738d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="2293c-102">Toegang tot factureringsgegevens voor Azure met behulp van op rollen gebaseerde toegangsbeheer beheren</span><span class="sxs-lookup"><span data-stu-id="2293c-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="2293c-103">U kunt de toegang voor Azure factureringsgegevens voor leden van uw team verlenen door een van de volgende gebruikersrollen toewijzen aan uw abonnement: accountbeheerder, servicebeheerder medebeheerder, eigenaar, bijdrager, lezer en facturering Reader.</span><span class="sxs-lookup"><span data-stu-id="2293c-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="2293c-104">Ze zou hebben toegang tot factureringsgegevens in de [Azure-portal](https://portal.azure.com/), en ze kunnen gebruiken de [facturering API's](billing-usage-rate-card-overview.md) programmatisch ophalen facturen (eenmaal heeft gekozen-in) en informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="2293c-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="2293c-105">Voor meer informatie over wie rollen kunt toewijzen, en welke rollen kan wat te doen, Zie [rollen in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="2293c-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="2293c-106"><a name="opt-in"></a>Deze extra gebruikers toegang krijgen tot facturen</span><span class="sxs-lookup"><span data-stu-id="2293c-106"><a name="opt-in"></a> Allowing additional users to access invoices</span></span>

<span data-ttu-id="2293c-107">De accountbeheerder moet aanmelden met behulp van de [Azure-portal](https://portal.azure.com/) toegang toestaan tot facturen voor andere gebruikers en via de API.</span><span class="sxs-lookup"><span data-stu-id="2293c-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="2293c-108">Als de accountbeheerder, selecteer uw abonnement uit de [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2293c-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="2293c-109">Selecteer **facturen** en vervolgens **toegang tot facturen**.</span><span class="sxs-lookup"><span data-stu-id="2293c-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![Schermafbeelding ziet u hoe u toegang tot facturen delegeren](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="2293c-111">Schakel **op** rollen factuur downloaden binnen het bereik van de toegang gevolgd door het opslaan van de wijzigingen, zodat gebruikers in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="2293c-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![Schermafbeelding ziet u op uit een gemachtigde naar factuur](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="2293c-113">Kiest servicebeheerder, medebeheerder eigenaar, bijdrager, lezer en facturering lezer, kan voor het abonnement voor het downloaden van facturen PDF-bestand in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2293c-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="2293c-114">Facturen die ouder zijn dan December 2016 zijn echter beschikbaar alleen naar de accountbeheerder nu.</span><span class="sxs-lookup"><span data-stu-id="2293c-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="2293c-115">De accountbeheerder kan ook configureren als u wilt dat facturen verzonden via e-mail.</span><span class="sxs-lookup"><span data-stu-id="2293c-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="2293c-116">Zie voor meer informatie, [uw factuur ophalen in e-mailbericht](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="2293c-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="2293c-117">Gebruikers toevoegen aan de rol Lezer facturering</span><span class="sxs-lookup"><span data-stu-id="2293c-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="2293c-118">De rol Lezer facturering heeft alleen-lezen toegang tot de factureringsgegevens abonnement in Azure-portal en geen toegang tot services, zoals virtuele machines en opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="2293c-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="2293c-119">De rol Lezer facturering toewijzen aan iemand die toegang tot de factureringsgegevens abonnement, maar niet de mogelijkheid voor het beheren van Azure-services nodig.</span><span class="sxs-lookup"><span data-stu-id="2293c-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="2293c-120">Deze rol is geschikt voor gebruikers in een organisatie die alleen financiële en kosten-beheer voor Azure-abonnementen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2293c-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="2293c-121">Selecteer uw abonnement uit de [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2293c-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="2293c-122">Selecteer **toegangsbeheer (IAM)** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2293c-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Schermafbeelding ziet u IAM in de abonnementsblade](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="2293c-124">Kies **facturering lezer** in de **Selecteer een rol** pagina.</span><span class="sxs-lookup"><span data-stu-id="2293c-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![Schermafbeelding ziet u lezer facturering in het pop-weergave](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="2293c-126">Typ het e-mailadres voor de gebruiker die u wilt uitnodigen en klik vervolgens op **OK** de uitnodiging te verzenden.</span><span class="sxs-lookup"><span data-stu-id="2293c-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![Schermafbeelding van e-mailadres om uit te nodigen iemand invoeren](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="2293c-128">Volg de instructies in de e-mail uitnodiging voor aanmelden als een lezer facturering.</span><span class="sxs-lookup"><span data-stu-id="2293c-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![Schermopname die laat zien wat de lezer facturering kunnen zien in Azure-portal](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="2293c-130">De functie facturering lezer is in preview en ondersteunt nog geen enterprise (EA) abonnementen of niet-algemene clouds.</span><span class="sxs-lookup"><span data-stu-id="2293c-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="2293c-131">Gebruikers toevoegen aan andere functies</span><span class="sxs-lookup"><span data-stu-id="2293c-131">Adding users to other roles</span></span>

<span data-ttu-id="2293c-132">Gebruikers in andere rollen, zoals eigenaar of bijdrager, hebben toegang tot niet alleen factureringsgegevens, maar ook Azure services.</span><span class="sxs-lookup"><span data-stu-id="2293c-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="2293c-133">Zie voor het beheren van deze rollen [toevoegen of wijzigen Azure-beheerdersrollen die het abonnement of de services beheren](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="2293c-133">To manage these roles, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="2293c-134">Wie toegang heeft tot de [Accountcentrum](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="2293c-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="2293c-135">Alleen de accountbeheerder kunt aanmelden bij de accountcentrum.</span><span class="sxs-lookup"><span data-stu-id="2293c-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="2293c-136">De accountbeheerder is de juridische eigenaar van het abonnement.</span><span class="sxs-lookup"><span data-stu-id="2293c-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="2293c-137">De persoon die zich heeft aangemeld of het Azure-abonnement hebt gekocht is de accountbeheerder, tenzij de [eigendom van het abonnement is overgezet](billing-subscription-transfer.md) naar iemand anders.</span><span class="sxs-lookup"><span data-stu-id="2293c-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="2293c-138">De accountbeheerder kan abonnementen maken, abonnementen annuleren, het factuuradres voor een abonnement te wijzigen en -beleid voor het abonnement te beheren.</span><span class="sxs-lookup"><span data-stu-id="2293c-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="2293c-139">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="2293c-139">Need help?</span></span> <span data-ttu-id="2293c-140">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="2293c-140">Contact support.</span></span>

<span data-ttu-id="2293c-141">Als u nog steeds meer vragen hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="2293c-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
