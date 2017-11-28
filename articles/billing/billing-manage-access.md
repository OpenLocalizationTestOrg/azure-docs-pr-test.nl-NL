---
title: aaaManage toegang tooAzure facturering rollen | Microsoft Docs
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
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="9630f-102">Toegang tot toobilling gegevens van Azure met behulp van op rollen gebaseerde toegangsbeheer beheren</span><span class="sxs-lookup"><span data-stu-id="9630f-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="9630f-103">U kunt de toegang voor Azure facturering informatie toomembers van uw team verlenen door toe te wijzen op een van de volgende gebruiker rollen tooyour abonnement Hallo: accountbeheerder, servicebeheerder medebeheerder, eigenaar, bijdrager, lezer en facturering Reader.</span><span class="sxs-lookup"><span data-stu-id="9630f-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="9630f-104">Ze toegang krijgen tot toobilling informatie zou hebben in Hallo [Azure-portal](https://portal.azure.com/), en ze kunnen gebruiken Hallo [facturering API's](billing-usage-rate-card-overview.md) tooprogrammatically ophalen facturen (eenmaal heeft gekozen-in) en informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="9630f-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="9630f-105">Voor meer informatie over wie rollen kunt toewijzen, en welke rollen kan wat te doen, Zie [rollen in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9630f-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="9630f-106"><a name="opt-in"></a>Extra gebruikers tooaccess facturen toestaan</span><span class="sxs-lookup"><span data-stu-id="9630f-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="9630f-107">Hallo accountbeheerder moet aanmelden met behulp van Hallo [Azure-portal](https://portal.azure.com/) tooinvoices toegang toestaan voor andere gebruikers en via de API.</span><span class="sxs-lookup"><span data-stu-id="9630f-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="9630f-108">Als accountbeheerder hello, selecteer uw abonnement uit Hallo [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9630f-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="9630f-109">Selecteer **facturen** en vervolgens **toegang tot tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="9630f-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Schermafbeelding ziet u hoe toodelegate toegang krijgen tot tooinvoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="9630f-111">Schakel **op** Hallo toegang wordt gevolgd door het opslaan van wijzigingen in hello, tooallow gebruikers in abonnement bereik rollen toodownload factuur.</span><span class="sxs-lookup"><span data-stu-id="9630f-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Schermafbeelding ziet-off toodelegate toegang tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="9630f-113">Kiest servicebeheerder, medebeheerder eigenaar, bijdrager, lezer en facturering lezer, kan op Hallo abonnement toodownload PDF facturen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9630f-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="9630f-114">Facturen die ouder zijn dan December 2016 zijn echter beschikbaar alleen toohello accountbeheerder nu.</span><span class="sxs-lookup"><span data-stu-id="9630f-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="9630f-115">Hallo beheerder kan ook toohave facturen verzonden via e-mail configureren.</span><span class="sxs-lookup"><span data-stu-id="9630f-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="9630f-116">toolearn meer, Zie [uw factuur ophalen in e-mailbericht](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="9630f-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="9630f-117">Het toevoegen van gebruikers toohello facturering lezer rol</span><span class="sxs-lookup"><span data-stu-id="9630f-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="9630f-118">met de rol Lezer facturering Hallo heeft alleen-lezentoegang toosubscription factureringsgegevens in Azure-portal en er is geen tooservices toegang zoals virtuele machines en opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="9630f-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="9630f-119">Hallo facturering lezer rol toosomeone die u moet toegang tot factureringsgegevens toohello-abonnement, maar niet de mogelijkheid toomanage Azure Hallo toewijzen services.</span><span class="sxs-lookup"><span data-stu-id="9630f-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="9630f-120">Deze rol is geschikt voor gebruikers in een organisatie die alleen financiële en kosten-beheer voor Azure-abonnementen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9630f-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="9630f-121">Selecteer uw abonnement uit Hallo [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9630f-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="9630f-122">Selecteer **toegangsbeheer (IAM)** en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="9630f-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Schermafbeelding ziet u IAM Hallo abonnement blade](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="9630f-124">Kies **facturering lezer** in Hallo **Selecteer een rol** pagina.</span><span class="sxs-lookup"><span data-stu-id="9630f-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Schermafbeelding ziet u lezer facturering in Hallo pop-weergave](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="9630f-126">Typ Hallo e-mailadres voor Hallo gebruiker u wilt dat tooinvite en klik vervolgens op **OK** toosend Hallo uitnodiging.</span><span class="sxs-lookup"><span data-stu-id="9630f-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Schermafbeelding van tooenter e tooinvite iemand](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="9630f-128">Volg de instructies in Hallo uitnodiging e toolog in als een lezer facturering.</span><span class="sxs-lookup"><span data-stu-id="9630f-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Schermopname die laat zien wat de lezer facturering Hallo kunt zien in Azure-portal](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="9630f-130">Hallo facturering Reader-functie is in preview en ondersteunt nog geen enterprise (EA) abonnementen of niet-algemene clouds.</span><span class="sxs-lookup"><span data-stu-id="9630f-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="9630f-131">Gebruikers tooother rollen toevoegen</span><span class="sxs-lookup"><span data-stu-id="9630f-131">Adding users tooother roles</span></span>

<span data-ttu-id="9630f-132">Gebruikers in andere rollen, zoals eigenaar of bijdrager, hebben toegang tot niet alleen factureringsgegevens, maar ook Azure services.</span><span class="sxs-lookup"><span data-stu-id="9630f-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="9630f-133">toomanage deze rollen Zie [toevoegen of wijzigen Azure-beheerdersrollen die Hallo abonnement of services beheren](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="9630f-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="9630f-134">Wie toegang heeft tot Hallo [Accountcentrum](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="9630f-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="9630f-135">Alleen Hallo accountbeheerder kan zich aanmelden in toohello-accountcentrum.</span><span class="sxs-lookup"><span data-stu-id="9630f-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="9630f-136">Hallo accountbeheerder is Hallo juridische eigenaar van het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="9630f-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="9630f-137">Hallo persoon die zich heeft aangemeld of gekocht hello Azure-abonnement is Hallo accountbeheerder, tenzij Hallo [eigendom van het abonnement is overgezet](billing-subscription-transfer.md) toosomebody anders.</span><span class="sxs-lookup"><span data-stu-id="9630f-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="9630f-138">Hallo accountbeheerder kunt maken van abonnementen, abonnementen annuleren Hallo factuuradres voor een abonnement en toegangsbeleid voor Hallo abonnement beheren.</span><span class="sxs-lookup"><span data-stu-id="9630f-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="9630f-139">Hulp nodig?</span><span class="sxs-lookup"><span data-stu-id="9630f-139">Need help?</span></span> <span data-ttu-id="9630f-140">Neem contact op met ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="9630f-140">Contact support.</span></span>

<span data-ttu-id="9630f-141">Als u nog steeds meer vragen hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.</span><span class="sxs-lookup"><span data-stu-id="9630f-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
