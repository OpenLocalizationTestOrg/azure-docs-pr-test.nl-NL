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
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Toegang tot toobilling gegevens van Azure met behulp van op rollen gebaseerde toegangsbeheer beheren

U kunt de toegang voor Azure facturering informatie toomembers van uw team verlenen door toe te wijzen op een van de volgende gebruiker rollen tooyour abonnement Hallo: accountbeheerder, servicebeheerder medebeheerder, eigenaar, bijdrager, lezer en facturering Reader. Ze toegang krijgen tot toobilling informatie zou hebben in Hallo [Azure-portal](https://portal.azure.com/), en ze kunnen gebruiken Hallo [facturering API's](billing-usage-rate-card-overview.md) tooprogrammatically ophalen facturen (eenmaal heeft gekozen-in) en informatie over het gebruik. Voor meer informatie over wie rollen kunt toewijzen, en welke rollen kan wat te doen, Zie [rollen in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Extra gebruikers tooaccess facturen toestaan

Hallo accountbeheerder moet aanmelden met behulp van Hallo [Azure-portal](https://portal.azure.com/) tooinvoices toegang toestaan voor andere gebruikers en via de API.

1. Als accountbeheerder hello, selecteer uw abonnement uit Hallo [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure-portal.

1. Selecteer **facturen** en vervolgens **toegang tot tooinvoices**.

    ![Schermafbeelding ziet u hoe toodelegate toegang krijgen tot tooinvoices](./media/billing-manage-access/AA-optin.png)

1. Schakel **op** Hallo toegang wordt gevolgd door het opslaan van wijzigingen in hello, tooallow gebruikers in abonnement bereik rollen toodownload factuur.

    ![Schermafbeelding ziet-off toodelegate toegang tooinvoice](./media/billing-manage-access/AA-optinAllow.png)

Kiest servicebeheerder, medebeheerder eigenaar, bijdrager, lezer en facturering lezer, kan op Hallo abonnement toodownload PDF facturen in hello Azure-portal. Facturen die ouder zijn dan December 2016 zijn echter beschikbaar alleen toohello accountbeheerder nu.

Hallo beheerder kan ook toohave facturen verzonden via e-mail configureren. toolearn meer, Zie [uw factuur ophalen in e-mailbericht](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Het toevoegen van gebruikers toohello facturering lezer rol

met de rol Lezer facturering Hallo heeft alleen-lezentoegang toosubscription factureringsgegevens in Azure-portal en er is geen tooservices toegang zoals virtuele machines en opslagaccounts. Hallo facturering lezer rol toosomeone die u moet toegang tot factureringsgegevens toohello-abonnement, maar niet de mogelijkheid toomanage Azure Hallo toewijzen services. Deze rol is geschikt voor gebruikers in een organisatie die alleen financiële en kosten-beheer voor Azure-abonnementen uitvoeren.

1. Selecteer uw abonnement uit Hallo [abonnementen blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure-portal.

1. Selecteer **toegangsbeheer (IAM)** en klik vervolgens op **toevoegen**.

    ![Schermafbeelding ziet u IAM Hallo abonnement blade](./media/billing-manage-access/select-iam.PNG)

1. Kies **facturering lezer** in Hallo **Selecteer een rol** pagina.

    ![Schermafbeelding ziet u lezer facturering in Hallo pop-weergave](./media/billing-manage-access/select-roles.PNG)

1. Typ Hallo e-mailadres voor Hallo gebruiker u wilt dat tooinvite en klik vervolgens op **OK** toosend Hallo uitnodiging.

    ![Schermafbeelding van tooenter e tooinvite iemand](./media/billing-manage-access/add-user.PNG)

1. Volg de instructies in Hallo uitnodiging e toolog in als een lezer facturering.

    ![Schermopname die laat zien wat de lezer facturering Hallo kunt zien in Azure-portal](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> Hallo facturering Reader-functie is in preview en ondersteunt nog geen enterprise (EA) abonnementen of niet-algemene clouds.

## <a name="adding-users-tooother-roles"></a>Gebruikers tooother rollen toevoegen

Gebruikers in andere rollen, zoals eigenaar of bijdrager, hebben toegang tot niet alleen factureringsgegevens, maar ook Azure services. toomanage deze rollen Zie [toevoegen of wijzigen Azure-beheerdersrollen die Hallo abonnement of services beheren](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Wie toegang heeft tot Hallo [Accountcentrum](https://account.windowsazure.com)?

Alleen Hallo accountbeheerder kan zich aanmelden in toohello-accountcentrum. Hallo accountbeheerder is Hallo juridische eigenaar van het Hallo-abonnement. Hallo persoon die zich heeft aangemeld of gekocht hello Azure-abonnement is Hallo accountbeheerder, tenzij Hallo [eigendom van het abonnement is overgezet](billing-subscription-transfer.md) toosomebody anders. Hallo accountbeheerder kunt maken van abonnementen, abonnementen annuleren Hallo factuuradres voor een abonnement en toegangsbeleid voor Hallo abonnement beheren.

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.

Als u nog steeds meer vragen hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
