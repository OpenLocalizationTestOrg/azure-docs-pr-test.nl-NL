---
title: aaaHow toostart een onderzoek toegang | Microsoft Docs
description: Meer informatie over hoe toocreate een toegang bekijken voor bevoegde identiteiten met Azure Privileged Identity Management-toepassing hello.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Hoe toostart een toegang controleren in Azure AD Privileged Identity Management
Roltoewijzingen worden 'verouderde' wanneer gebruikers uitgebreide toegang dat ze niet meer nodig hebt. In de volgorde tooreduce Hallo risico dat samenhangt met deze verouderde roltoewijzingen, neem bevoorrechte rol beheerders regelmatig Hallo-functies die gebruikers hebben gekregen. Dit document bevat informatie over Hallo stappen voor het starten van een onderzoek toegang in Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Een revisie toegang starten
> [!NOTE]
> Als u dit nog niet hebt Hallo PIM toepassingendashboard tooyour toegevoegd in hello Azure-portal, Zie Hallo stappen in [aan de slag met Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Hallo PIM toepassing hoofdpagina van zijn er drie manieren toostart een onderzoek toegang:

* **Toegang tot beoordelingen** > **toevoegen**
* **Rollen** > **revisie** knop
* Selecteer Hallo specifieke rol toobe verwijderd uit de lijst van de rollen Hallo > **revisie** knop

Wanneer u klikt op op Hallo **bekijken** knop hello **een revisie toegang starten** blade wordt weergegeven. Op deze blade u bent momenteel tooconfigure Hallo controleren met een naam en tijd limiet, kiest u een rol tooreview en beslissen wie verantwoordelijk is voor Hallo controleren.

![Starten van de evaluatie van een access - schermafbeelding][1]

### <a name="configure-hello-review"></a>Hallo controle configureren
toocreate een toegang controleren, moet u tooname deze en stel de begin- en datum.

![Configureren van de evaluatie - schermafbeelding][2]

Controleer de lengte van de Hallo Hallo bekijken lang genoeg zijn voor gebruikers toocomplete. Als u klaar voor de einddatum Hallo bent, kunt u Hallo controleren vroeg altijd stoppen.

### <a name="choose-a-role-tooreview"></a>Kies een tooreview rol
Iedere evaluatie is gericht op slechts één rol. Tenzij u Hallo toegang controleren vanuit een specifieke rolblade hebt gestart, moet u nu toochoose een rol.

1. Navigeer te**lidmaatschap van de gebruikersrol controleren**
   
    ![Bekijk rollidmaatschap - schermafbeelding][3]
2. Kies één rol uit Hallo-lijst.

### <a name="decide-who-will-perform-hello-review"></a>Bepalen wie verantwoordelijk is voor Hallo controleren
Er zijn drie opties voor het uitvoeren van een beoordeling. U kunt Hallo revisie toosomeone toewijzen anders toocomplete zelf doen, of u kunt elke gebruiker die hun eigen toegang controleren.

1. Navigeer te**revisoren selecteren**
   
    ![Selecteer revisoren - schermafbeelding][4]
2. Kies een van de Hallo opties:
   
   * **Selecteer revisor**: Gebruik deze optie als u niet weet die toegang nodig heeft. Met deze optie kunt u Hallo revisie tooa resource-eigenaar of groep manager toocomplete toewijzen.
   * **Mij**: handig als u wilt dat toopreview hoe toegang werk controleert of u wilt dat tooreview namens mensen die niet kan.
   * **Leden lees zelf**: Gebruik deze optie toohave Hallo-evaluatie met gebruikers hun eigen roltoewijzingen.

### <a name="start-hello-review"></a>Hallo revisie starten
U hebt ten slotte Hallo optie toorequire dat gebruikers een reden opgeven als ze hun toegang wordt goedgekeurd. Indien gewenst een beschrijving van Hallo Lees toevoegen en selecteer **Start**.

Zorg ervoor dat u uw gebruikers weten dat er een wachten tot ze toegang-controleren en te laten laten [hoe tooperform een toegang controleren](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Hallo toegang controleren beheren
U kunt Hallo voortgang volgen als Hallo revisoren hun beoordelingen in hello Azure AD PIM-dashboard hebt voltooid, in Hallo toegang sectie beoordeelt. Geen toegangsrechten worden gewijzigd in de map Hallo tot [Hallo controleren is voltooid](active-directory-privileged-identity-management-how-to-complete-review.md).

Totdat Hallo controleperiode afgelopen is, kunt u gebruikers toocomplete hun revisie herinneren of stop Hallo revisie vroeg tegen toegang Hallo beoordeelt sectie.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>PIM inhoudsopgave
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
