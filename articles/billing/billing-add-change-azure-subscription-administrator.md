---
title: Toevoegen of wijzigen van de Azure-abonnement beheerdersrollen | Microsoft Docs
description: Hierin wordt beschreven hoe u Azure Medebeheerder, servicebeheerder en accountbeheerder toevoegen of wijzigen
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
ms.openlocfilehash: da5995535d42ed52772cb09e0f4da51bbf878748
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-the-subscription-or-services"></a>Toevoegen of wijzigen van de Azure-beheerdersrollen die het abonnement of de services beheren
U kunt de Azure-beheerder die uw Azure-abonnement beheert of de Azure-services in uw abonnement beheert wijzigen. Als u wilt weergeven Azure informatie over facturering en abonnementen beheren, moet u zich aanmelden bij de [Accountcentrum](https://account.windowsazure.com/Home/Index) als accountbeheerder. 

## <a name="add-an-admin-for-a-subscription"></a>Een beheerder voor een abonnement toevoegen
U kunt een Azure-beheerder toevoegen in de Azure-portal of in de klassieke Azure portal.

**Azure Portal**

Als u iemand toevoegen als beheerder voor een abonnement in de Azure-portal, wilt geven u ze de rol van eigenaar. De rol van eigenaar kan alleen beheren voor de resources in het abonnement dat u hebt toegewezen. Heeft geen toegangsrechten naar andere abonnementen. De eigenaar u via toevoegen de [Azure-portal](https://portal.azure.com) niet beheren resource in de [klassieke Azure-portal](https://manage.windowsazure.com).

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Selecteer in het menu Hub **abonnement** > *het abonnement dat u wilt dat de beheerder voor toegang tot*.

    ![Schermafbeelding ziet u het geselecteerde abonnement](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. Selecteer in de abonnementsblade **toegangsbeheer (IAM)**.
4. Selecteer **toevoegen** > **rol** > **eigenaar**. Typ de e-mailadres van de gebruiker die u wilt toevoegen als eigenaar, selecteert u de gebruiker en selecteer vervolgens **opslaan**.

    ![Schermafbeelding van de rol van eigenaar geselecteerd](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Als u de eigenaarsaccount toevoegen als medebeheerder wilt, in de **toegangsbeheer (IAM)** pagina, met de rechtermuisknop op de gebruiker en selecteer vervolgens **toevoegen als medebeheerder**. Deze functie is nu beschikbaar op [Azure preview-portal](https://preview.portal.azure.com/). 

     ![Schermafbeelding van medebeheerder voegt](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >U moet de 'Eigenaar'-gebruiker toevoegen als medebeheerder als de gebruiker voor het beheren van de Azure-services in [klassieke Azure-portal](https://manage.windowsazure.com/).

    Als u wilt verwijderen van de machtiging medebeheerder, met de rechtermuisknop op de gebruiker 'CO-beheerder' en selecteer vervolgens **medebeheerder verwijderen**.

    ![Schermopname die medebeheerder verwijdert](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Klassieke Azure Portal**

1. Meld u aan bij de [klassieke Azure-portal](https://manage.windowsazure.com/).
2. Selecteer in het navigatiedeelvenster **instellingen**> **beheerders**> **toevoegen**. </br>

    ![Schermopname die laat zien hoe u naar de knop toevoegen](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Typ het e-mailadres van degene die u wilt toevoegen als medebeheerder en selecteer vervolgens het abonnement dat u wilt dat de medebeheerder voor toegang tot.</br>

    ![Schermafbeelding van een abonnement dat is geselecteerd ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

De volgende e-mailadres kan worden toegevoegd als Medebeheerder:

* **Microsoft-Account** (voorheen Windows Live ID) </br>
  U kunt een Microsoft-Account gebruiken om te melden bij alle consumer gerichte Microsoft-producten en cloudservices, zoals Outlook (Hotmail), Skype (MSN), OneDrive, Windows Phone en Xbox LIVE.
* **Organisatie-account**</br>
  Een organisatie-account is een account dat wordt gemaakt onder het Azure Active Directory. Het accountadres van de organisatie-heeft deze indeling:

    gebruiker @&lt;uw domein&gt;. onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Servicebeheerder voor een abonnement wijzigen
Alleen de accountbeheerder kan de servicebeheerder voor een abonnement kunt wijzigen.

1. Aanmelden bij [Azure-Accountcentrum](https://account.windowsazure.com/subscriptions) met behulp van de accountbeheerder.
2. Selecteer het abonnement dat u wilt wijzigen.
3. Selecteer aan de rechterkant **abonnement bewerken** details. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. In de **SERVICEBEHEERDER** Voer het e-mailadres van de nieuwe Service-beheerder. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-the-account-administrator"></a>De accountbeheerder wijzigen
Aan het eigendom overdraagt van het Azure-account aan een andere account Zie [overbrengen eigendom van een Azure-abonnement](billing-subscription-transfer.md).

Wij raden u niet verwijderen of wijzig de naam van de accountbeheerder e-mailadres. Mogelijk ziet u onverwachte of ongewenst gedrag met de Azure-account. U kunt niet kunnen aanmelden bij Azure met dat account worden, wijzigingen aanbrengen aan het account of beheer van resources met dat account. 

## <a name="check-the-account-administrator-of-the-subscription"></a>Controleer de accountbeheerder van het abonnement
Als u niet zeker weet wie de accountbeheerder is voor uw abonnement, gebruikt u de volgende stappen uit om erachter te komen.

  1. Meld u aan bij [Azure Portal](https://portal.azure.com).
  2. Selecteer in het menu Hub **abonnement**.
  3. Selecteer het abonnement dat u wilt controleren, en ga vervolgens naar **instellingen**.
  4. Selecteer **eigenschappen**. De accountbeheerder van het abonnement wordt weergegeven in de **accountbeheerder** vak.  

## <a name="types-of-azure-admin-accounts"></a>Typen Azure beheerdersaccounts
 Accountbeheerder servicebeheerder en medebeheerder zijn de drie soorten beheerdersrollen in Microsoft Azure. De volgende tabel beschrijft het verschil tussen deze drie beheerdersrollen.

| Administratieve rol | Limiet | Beschrijving |
| --- | --- | --- |
| De accountbeheerder (AA) |1 per Azure-account |Dit is de persoon die zich heeft aangemeld of Azure-abonnementen hebt gekocht en is geautoriseerd voor toegang tot de [Accountcentrum](https://account.windowsazure.com/Home/Index) en verschillende beheertaken uit te voeren. Hierbij kunnen maken van abonnementen, abonnementen annuleren, de facturering voor een abonnement te wijzigen en wijzigen van de servicebeheerder. |
| Servicebeheerder (SA) |1 per Azure-abonnement |Deze rol is geautoriseerd voor het beheren van services in de [Azure-portal](https://portal.azure.com). De accountbeheerder is voor een nieuw abonnement wordt standaard ook de servicebeheerder. |
| Medebeheerder (CA) in de [klassieke Azure-portal](https://manage.windowsazure.com) |200 per abonnement |Deze rol heeft dezelfde toegangsrechten als de Servicebeheerder, maar kan de koppeling van abonnementen aan Azure-directory's niet wijzigen. |

Azure Active Directory-rol gebaseerde toegangsbeheer (RBAC) kunnen gebruikers worden toegevoegd aan meerdere rollen. Zie voor meer informatie [toegangsbeheer op basis van een functie van Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Voorwaarden en beperkingen voor beheerdersaccounts
* Elk abonnement is gekoppeld aan een Azure AD-directory (ook wel bekend als de map standaard). Als u het abonnement is gekoppeld aan standaarddirectory zoekt, gaat u naar de [klassieke Azure-portal](https://manage.windowsazure.com/), selecteer **instellingen** > **abonnementen**. Controleer de abonnements-ID voor de map standaard zoeken.
* Als u bent aangemeld bij een Microsoft-Account, kunt u andere Microsoft-Accounts of gebruikers in de map standaard alleen toevoegen als Medebeheerder.
* Als u bent aangemeld bij een organisatie-account, kunt u de andere organisatie-accounts in uw organisatie als Medebeheerder toevoegen. Bijvoorbeeld: abby@contoso.com kunt toevoegen bob@contoso.com als servicebeheerder of CO-beheerder, maar kan niet worden toegevoegd john@notcontoso.com tenzij john@notcontoso.com is in de map. Gebruikers die zijn aangemeld met organisatieaccounts kunnen blijven gebruikers van Microsoft-Account toevoegen als servicebeheerder of CO-beheerder.
* Nu dat het is mogelijk aan te melden bij Azure met een organisatieaccount, vindt hier u de wijzigingen aan servicebeheerder en medebeheerder accountvereisten:

  | Meld u aan de methode | Microsoft-Account of gebruikers in de Directory standaard als CA of SA toevoegen? | Organisatie-account binnen dezelfde organisatie als CA of SA toevoegen? | Organisatie-account in een andere organisatie als CA of SA toevoegen? |
  | --- | --- | --- | --- |
  |  Microsoft-account |Ja |Nee |Nee |
  |  Organisatie-account |Ja |Ja |Nee |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Meer informatie over toegangsbeheer voor resource en Active Directory
* Zie voor meer informatie over hoe de toegang tot bronnen in Microsoft Azure wordt beheerd, [informatie over toegang tot bronnen in Azure](../active-directory/active-directory-understanding-resource-access.md).
* Zie voor meer informatie over Azure Active Directory, [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) en [beheerdersrollen toewijzen in Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost.
