---
title: Azure-abonnement eigendom overdragen aan een ander account | Microsoft Docs
description: Hierin wordt beschreven hoe u een Azure-abonnement overbrengen naar een andere gebruiker en enkele veelgestelde vragen (FAQ) over het proces
keywords: azure-abonnement, azure-overdracht abonnement overdraagt, azure-abonnement verplaatsen naar een ander abonnement eigenaar van de account, azure wijzigen, azure-abonnement overbrengen naar een ander account
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: c8ecdc1e-c9c5-468c-a024-94ae41e64702
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8a856c39eb11546f35cb4e8c21e6bdcce98857a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="transfer-ownership-of-an-azure-subscription-to-another-account"></a>Eigendom van een Azure-abonnement overdragen aan een ander account

U kunt uw abonnement overbrengen naar een andere gebruiker voor betalen per gebruik, Visual Studio, actie Pack of BizSpark abonnementen in het midden van het Account. We bieden ondersteuning voor de overdracht van de externe Azure-services voor deze abonnement-typen. 

U kunt het eigendom overdraagt van een Azure-abonnement als u:

* Om facturering eigendom van iemand anders uw Azure-abonnement nodig.
* Wilt u het account dat wordt gebruikt om u te registreren voor Azure wijzigen. Misschien u uw Microsoft-Account gebruikt, maar bedoeld voor gebruik van uw werk- of schoolaccount in plaats daarvan.
* Wilt u uw Azure-abonnement vanuit een map verplaatsen naar een andere.
* Azure en Office 365 in verschillende tenants hebt en wilt consolideren.

Zie voor informatie over het wijzigen van uw abonnement op een andere aanbieding [overschakelen van uw Azure-abonnement op een andere aanbieding](billing-how-to-switch-azure-offer.md). 

## <a name="transfer-ownership-of-an-azure-subscription"></a>Het eigendom overdraagt van een Azure-abonnement
> [!VIDEO https://channel9.msdn.com/Series/Microsoft-Azure-Tutorials/Transfer-an-Azure-subscription/player]
>
>

1. Meld u aan bij <https://account.windowsazure.com/Subscriptions>. U moet de beheerder van de Account een eigendom overdraagt. Als u wilt weten wie de accountbeheerder van het abonnement is, Zie de [Veelgestelde vragen over](#faq).

2. Selecteer het abonnement om over te dragen.

3. Klik op de **abonnement overbrengen** optie. Zie [Veelgestelde vragen over](#no-button) als u de knop niet ziet.

   ![Tabblad account voor Azure-abonnementen](./media/billing-subscription-transfer/image1.png)
4. Geef de ontvanger op.

   ![Dialoogvenster overdracht-abonnement](./media/billing-subscription-transfer/image2.PNG)
5. De ontvanger ontvangt automatisch een e-mail met een acceptatielink.

   ![Abonnement overdracht e-mailbericht naar ontvanger](./media/billing-subscription-transfer/image3.png)
6. De ontvanger klikt op de link en volgt de instructies, waaronder het invoeren van zijn of haar betaalgegevens.

   ![Eerste abonnement overdracht webpagina](./media/billing-subscription-transfer/image4.png)

   ![Tweede abonnement overdracht webpagina 's](./media/billing-subscription-transfer/image5.png)
7. Success! Het abonnement worden nu overgedragen.

## <a name="transfer-subscription-ownership-for-enterprise-agreement-ea-customers"></a>Het abonnement eigendom overdraagt voor klanten met Enterprise Agreement (EA)
De Enterprise-beheerder kan het eigendom overdraagt van abonnementen binnen een inschrijving. Om te beginnen, Zie [accounteigendom overdragen](https://ea.azure.com/helpdocs/changeAccountOwnerForASubscription) in de portal EA.

## <a name="next-steps-after-accepting-ownership-of-a-subscription"></a>Volgende stappen na het eigendom van een abonnement accepteren
1. U bent nu de accountbeheerder. Controleren en bijwerken van de servicebeheerder en Medebeheerders. Beheren van beheerders in de [klassieke Azure-portal](https://manage.windowsazure.com) door naar instellingen te gaan. [Meer informatie over beheerdersrollen](billing-add-change-azure-subscription-administrator.md).

2. U kunt ook op rollen gebaseerde toegangsbeheer (RBAC) gebruiken voor uw abonnement en services. Ga naar [Azure Portal](https://portal.azure.com). [Meer informatie over RBAC](../active-directory/role-based-access-control-configure.md)

3. Werk de referenties die zijn gekoppeld met dit abonnement services, waaronder:
   
   * Van beheercertificaten die de gebruiker Administrator-rechten aan abonnementresources toewijzen. Zie voor meer informatie [maken en uploaden een beheer van het certificaat voor Azure](../cloud-services/cloud-services-certs-create.md)
   
   * Sneltoetsen voor services zoals opslag. Zie voor meer informatie [over Azure storage-accounts](../storage/common/storage-create-storage-account.md)
   
   * Referenties voor externe toegang voor services zoals Azure Virtual Machines. 

4. [Factureringsmeldingen bijwerken voor dit abonnement](billing-set-up-alerts.md) op de [Azure-Accountcentrum](https://account.windowsazure.com/Subscriptions). 

5. Als u met een partner werkt, kunt u het bijwerken van de partner-ID voor dit abonnement. U kunt bijwerken de partner-ID in de [Azure-Accountcentrum](https://account.windowsazure.com/Subscriptions).

<a id="faq"></a>

## <a name="frequently-asked-questions-faq"></a>Veelgestelde vragen
* <a name="whoisaa"></a>**Wie de accountbeheerder van het abonnement is?**

  De accountbeheerder is de persoon die zich heeft aangemeld of het Azure-abonnement hebt aangeschaft. Ze bevoegd zijn voor toegang tot de [Accountcentrum](https://account.windowsazure.com/Home/Index) en uitvoeren van verschillende beheertaken, zoals het maken van abonnementen, abonnementen annuleren, de facturering voor een abonnement te wijzigen of wijzigen van de servicebeheerder. Als u niet zeker weet wie de accountbeheerder is voor een abonnement, gebruikt u de volgende stappen uit om erachter te komen.

  1. Meld u aan bij [Azure Portal](https://portal.azure.com).
  2. Selecteer in het menu Hub **abonnement**.
  3. Selecteer het abonnement dat u wilt controleren, en ga vervolgens naar **instellingen**.
  4. Selecteer **eigenschappen**. De accountbeheerder van het abonnement wordt weergegeven in de **accountbeheerder** vak.  

* **Alles overbrengen? Met inbegrip van resourcegroepen, virtuele machines, schijven en andere actieve services?**

  Ja, al uw resources, zoals virtuele machines, schijven en websites overdracht naar de nieuwe eigenaar. Echter [beheerdersrollen](billing-add-change-azure-subscription-administrator.md) en [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) beleidsregels die u hebt ingesteld, worden niet overgedragen op andere mappen.

* <a id="no-button"></a>**Waarom zie ik niet de knop abonnement overbrengen?**

  Als er geen de **overdracht abonnement** knop, en vervolgens de overdracht van abonnement voor uw aanbieding niet ondersteund. [Neem contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

* **Resulteert overdracht van het abonnement in alle services actief blijven?**

  Er zijn geen gevolgen voor de service. Het abonnement overdragen Hiermee annuleert u het abonnement onder de huidige Account Administrator en maakt u een abonnement onder de account van de geadresseerde. Het nieuwe abonnement is gekoppeld aan de onderliggende Azure-services. De abonnements-ID blijft hetzelfde.

* **Hoe gebruik ik dit proces de map voor het abonnement wilt wijzigen?**

  Een Azure-abonnement wordt gemaakt in de map die de accountbeheerder behoort. Als u de map, moet u het abonnement overbrengen naar een gebruikersaccount in de doelmap. Als die gebruiker de stappen voor het accepteren van overdracht voltooit, wordt het abonnement automatisch verplaatst naar de doelmap.

* **Als ik eigendom van een abonnement van een andere organisatie overneemt, ze toegang hebben tot mijn resources blijven?**

  Als het abonnement is overgebracht naar een andere tenant, verliest de gebruikers die zijn gekoppeld aan de vorige tenant toegang tot het abonnement. Zelfs als een gebruiker niet een servicebeheerder is of Co-beheerder voordoet, die nog steeds toegang tot het abonnement via andere beveiligingsmechanismen hebben mogelijk, met inbegrip van:

  * Van beheercertificaten die de gebruiker Administrator-rechten aan abonnementresources toewijzen. Zie voor meer informatie [maken en uploaden van een Beheercertificaat voor Azure](../cloud-services/cloud-services-certs-create.md).
  * Sneltoetsen voor services zoals opslag. Zie voor meer informatie [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).
  * Referenties voor externe toegang voor services zoals Azure Virtual Machines.

 Als de ontvanger moet toegang tot hun bronnen te beperken, overwegen ze geen geheimen die zijn gekoppeld aan de service bijwerken. De meeste bronnen kunnen worden bijgewerkt met behulp van de volgende stappen uit:

    1. Ga naar de [Azure Portal](https://portal.azure.com).
    2. Selecteer in het menu Hub **alle resources**.
    3. Selecteer de resource. 
    4. Klik op de resourceblade **instellingen**. Hier kunt u weergeven en bijwerken van bestaande geheimen.

* **Als ik het abonnement in het midden van de factureringscyclus overdraagt, de ontvanger betalen voor de hele facturering-cyclus?**

  De afzender is verantwoordelijk voor de betaling voor enig gebruik die is gerapporteerd naar het punt dat de overdracht is voltooid. De ontvanger is verantwoordelijk voor het gebruik gerapporteerd na het tijdstip van de overdracht en hoger. Mogelijk zijn er enkele verbruik dat heeft plaatsgevonden vóór overdracht maar later is gerapporteerd. Het gebruik is opgenomen in de ontvanger factuur.

* **De ontvanger toegang hebben tot gebruiks- en factureringsgeschiedenis?**

  De enige informatie die beschikbaar zijn voor de ontvanger het bedrag van de laatste factuur is of als het abonnement is overgebracht voordat de eerste factuur is gegenereerd, het huidige saldo. De rest van de gebruiks- en factureringsgeschiedenis niet kan worden overgedragen aan het abonnement.

* **Kan de aanbieding worden gewijzigd tijdens een overdracht?**

  De aanbieding moet hetzelfde blijven. Zie het wijzigen van uw aanbieding [overschakelen van uw Azure-abonnement op een andere aanbieding](billing-how-to-switch-azure-offer.md).

* **Kan ik een abonnement overbrengen naar een gebruikersaccount in een ander land**

  Nee, een abonnement overbrengen naar een gebruikersaccount in een ander land wordt niet ondersteund. Het account van de geadresseerde gebruiker moet zich in hetzelfde land.

* **Kan de ontvanger een andere betalingsmethode gebruiken?**

  Ja. Maar de abonnement-factureringsgeschiedenis verdeeld is over twee accounts.  

* **Is de betalingsmethode gevolgen nadat ik een Azure-abonnement hebt overgebracht?**

  Voor het accepteren van de overdracht van het abonnement, een creditcard of betaling vergelijkbaar dient methode moet worden opgegeven om te betalen voor het abonnement. Als Bob een abonnement naar ANS overdraagt en ANS de overdracht accepteert, moet ANS een betalingswijze om te betalen voor het abonnement opgeven. Nadat de overdracht voltooid is, wordt voor het abonnement niet Bob ANS gefactureerd.

* **Hoe ik gegevens en services voor mijn Azure-abonnement migreren naar nieuw abonnement?**

  Als u niet kunt abonnement overdragen, kunt u handmatig migreren uw resources. Zie [resources verplaatsen naar de nieuwe resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md).



## <a name="need-help-contact-support"></a>Hulp nodig? Neem contact op met ondersteuning.
Als u nog hulp nodig hebt, [contact op met ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) ophalen van uw probleem snel worden opgelost. 


