---
title: aaaAdd of wijzig Azure-abonnement beheerdersrollen | Microsoft Docs
description: Hierin wordt beschreven hoe tooadd of Medebeheerder van Azure, servicebeheerder en accountbeheerder wijzigen
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Toevoegen of wijzigen van de Azure-beheerdersrollen die Hallo abonnement of services beheren
U kunt wijzigen hello Azure-beheerder beheert uw Azure-abonnement of beheert hello Azure-services gebruikt in uw abonnement. tooview informatie over Azure facturering en abonnementen beheren, moet u zijn aangemeld toohello [Accountcentrum](https://account.windowsazure.com/Home/Index) als accountbeheerder Hallo. 

## <a name="add-an-admin-for-a-subscription"></a>Een beheerder voor een abonnement toevoegen
U kunt een Azure-beheerder toevoegen in hello Azure-portal of in Hallo klassieke Azure-portal.

**Azure Portal**

tooadd iemand als beheerder voor een abonnement in hello Azure-portal, geeft u deze rol van eigenaar Hallo. rol van eigenaar Hallo kan alleen Hallo resources in het Hallo-abonnement dat u hebt toegewezen beheren. Heeft geen toegang bevoegdheid tooother abonnementen. eigenaar u via Hallo toevoegen Hallo [Azure-portal](https://portal.azure.com) resource in Hallo niet beheren [klassieke Azure-portal](https://manage.windowsazure.com).

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Selecteer op de Hub-menu Hallo **abonnement** > *Hallo abonnement dat u wilt dat Hallo beheerder tooaccess*.

    ![Schermafbeelding ziet u het geselecteerde abonnement](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. Selecteer in de abonnementsblade hello **toegangsbeheer (IAM)**.
4. Selecteer **toevoegen** > **rol** > **eigenaar**. Typ de e-mailadres Hallo van Hallo gebruiker u wilt tooadd als eigenaar van een gebruiker selecteert hello, en selecteer vervolgens **opslaan**.

    ![Schermafbeelding van de rol van Hallo eigenaar is geselecteerd](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Als u tooadd Hallo eigenaarsaccount wilt gebruiken als medebeheerder in Hallo **toegangsbeheer (IAM)** pagina, met de rechtermuisknop op het Hallo-gebruiker en selecteer vervolgens **toevoegen als medebeheerder**. Deze functie is nu beschikbaar op [Azure preview-portal](https://preview.portal.azure.com/). 

     ![Schermafbeelding van medebeheerder voegt](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >U moet tooadd Hallo 'Eigenaar' gebruiker als medebeheerder als Hallo gebruiker toomanage hello Azure-services in [klassieke Azure-portal](https://manage.windowsazure.com/).

    tooremove hello medebeheerder machtiging met de rechtermuisknop op Hallo 'CO-beheerder' gebruiker en selecteer vervolgens **medebeheerder verwijderen**.

    ![Schermopname die medebeheerder verwijdert](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Klassieke Azure Portal**

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/).
2. Selecteer in het navigatiedeelvenster Hallo **instellingen**> **beheerders**> **toevoegen**. </br>

    ![Schermopname die laat zien hoe tooget toohello knop toevoegen](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Type Hallo e-mailadres van de gewenste Hallo persoon tooadd als medebeheerder en selecteer vervolgens Hallo-abonnement dat u wilt dat Hallo medebeheerder tooaccess.</br>

    ![Schermafbeelding van een abonnement dat is geselecteerd ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Hallo volgende e-mailadres kan worden toegevoegd als Medebeheerder:

* **Microsoft-Account** (voorheen Windows Live ID) </br>
  U kunt een Microsoft-Account toosign gebruiken in tooall consumer gerichte Microsoft-producten en cloudservices, zoals Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone en Xbox LIVE.
* **Organisatie-account**</br>
  Een organisatie-account is een account dat wordt gemaakt onder het Azure Active Directory. Hallo organisatieaccount adres heeft deze indeling:

    gebruiker @&lt;uw domein&gt;. onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Servicebeheerder voor een abonnement wijzigen
Alleen Hallo accountbeheerder kunt Hallo servicebeheerder voor een abonnement te wijzigen.

1. Aanmelden te[Azure-Accountcentrum](https://account.windowsazure.com/subscriptions) met behulp van Hallo accountbeheerder.
2. Hallo-abonnement u toochange wilt selecteren.
3. Selecteer aan de rechterzijde hello, **abonnement bewerken** details. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. In Hallo **SERVICEBEHEERDER** Hallo e-mailadres van Hallo Voer nieuwe-servicebeheerder. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Hallo accountbeheerder wijzigen
Zie tootransfer eigendom van Hallo-account Azure-account tooanother [overbrengen eigendom van een Azure-abonnement](billing-subscription-transfer.md).

Wij raden u niet verwijderen of wijzig de naam van het e-mailadres Hallo Account Administrator. Mogelijk ziet u onverwachte of ongewenst gedrag Hello Azure-account. U kunt niet worden tooAzure voor kunnen aanmelden met dat account, wijzigingen aanbrengen toohello account of -resources beheren met dat account. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Hallo beheerder van abonnement Hallo controleren
Als u niet zeker weet wie de accountbeheerder Hallo is voor uw abonnement, gebruikt u Hallo toofind uit stappen te volgen.

  1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
  2. Selecteer op de Hub-menu Hallo **abonnement**.
  3. Selecteer Hallo abonnement u wilt toocheck en ga vervolgens naar **instellingen**.
  4. Selecteer **eigenschappen**. de accountbeheerder Hallo van Hallo abonnement wordt weergegeven in Hallo **accountbeheerder** vak.  

## <a name="types-of-azure-admin-accounts"></a>Typen Azure beheerdersaccounts
 Accountbeheerder servicebeheerder en medebeheerder zijn drie soorten beheerdersrollen in Microsoft Azure Hallo. Hallo beschrijft volgende tabel Hallo verschil tussen deze drie beheerdersrollen.

| Administratieve rol | Limiet | Beschrijving |
| --- | --- | --- |
| De accountbeheerder (AA) |1 per Azure-account |Dit is Hallo persoon die zich heeft aangemeld of Azure-abonnementen hebt gekocht en geautoriseerde tooaccess hello [Accountcentrum](https://account.windowsazure.com/Home/Index) en verschillende beheertaken uit te voeren. Deze kunnen toocreate abonnementen zijn, abonnementen annuleren Hallo facturering voor een abonnement te wijzigen en Hallo servicebeheerder wijzigen. |
| Servicebeheerder (SA) |1 per Azure-abonnement |Deze rol is geautoriseerde toomanage services in Hallo [Azure-portal](https://portal.azure.com). Hallo beheerder is voor een nieuw abonnement wordt standaard ook Hallo servicebeheerder. |
| Medebeheerder (CA) in Hallo [klassieke Azure-portal](https://manage.windowsazure.com) |200 per abonnement |Deze rol Hallo heeft dezelfde toegangsrechten als Hallo servicebeheerder, maar Hallo koppeling met abonnementen tooAzure mappen niet wijzigen. |

Azure Active Directory-rol gebaseerde toegangsbeheer (RBAC) kunnen gebruikers toobe toomultiple functies toegevoegd. Zie voor meer informatie [toegangsbeheer op basis van een functie van Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Voorwaarden en beperkingen voor beheerdersaccounts
* Elk abonnement is gekoppeld aan een Azure AD-directory (ook wel bekend als hello standaarddirectory). toofind hello standaarddirectory Hallo abonnement is gekoppeld, Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com/), selecteer **instellingen** > **abonnementen**. Controleer Hallo abonnement-ID toofind Hallo standaarddirectory.
* Als u bent aangemeld bij een Microsoft-Account, kunt u alleen andere Microsoft-Accounts of gebruikers binnen Hallo standaarddirectory toevoegen als Medebeheerder.
* Als u bent aangemeld bij een organisatie-account, kunt u de andere organisatie-accounts in uw organisatie als Medebeheerder toevoegen. Bijvoorbeeld: abby@contoso.com kunt toevoegen bob@contoso.com als servicebeheerder of CO-beheerder, maar kan niet worden toegevoegd john@notcontoso.com tenzij john@notcontoso.com is in de map. Gebruikers die zijn aangemeld met organisatieaccounts tooadd Microsoft-Account gebruikers als servicebeheerder of CO-beheerder kunnen worden voortgezet.
* Nu dat het is mogelijk toosign in tooAzure met een organisatieaccount, zijn hier Hallo wijzigingen tooService beheerder en medebeheerder accountvereisten:

  | Meld u aan de methode | Microsoft-Account of gebruikers in de Directory standaard als CA of SA toevoegen? | Organisatie-account toevoegen in Hallo dezelfde organisatie als CA of SA? | Organisatie-account in een andere organisatie als CA of SA toevoegen? |
  | --- | --- | --- | --- |
  |  Microsoft-account |Ja |Nee |Nee |
  |  Organisatie-account |Ja |Ja |Nee |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Meer informatie over toegangsbeheer voor resource en Active Directory
* Zie toolearn meer informatie over hoe de toegang tot resources wordt beheerd in Microsoft Azure [informatie over toegang tot bronnen in Azure](../active-directory/active-directory-understanding-resource-access.md).
* Zie voor meer informatie over Azure Active Directory, [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) en [beheerdersrollen toewijzen in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget uw probleem snel worden opgelost.
