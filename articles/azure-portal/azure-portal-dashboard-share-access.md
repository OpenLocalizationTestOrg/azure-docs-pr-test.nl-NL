---
title: aaaShare Azure portal dashboards met behulp van RBAC | Microsoft Docs
description: Dit artikel wordt uitgelegd hoe tooshare een dashboard in Azure-portal Hallo met toegangsbeheer op basis van rollen.
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>Azure dashboards delen met toegangsbeheer op basis van rollen
U kunt na het configureren van een dashboard, publiceren en delen met andere gebruikers in uw organisatie. Toestaan dat anderen tooview uw dashboard met behulp van Azure [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-configure.md). U wijst een gebruiker of groep van gebruikers tooa rol en die rol definieert of deze gebruikers kunnen weergeven of Hallo gepubliceerde dashboard wijzigen. 

Alle gepubliceerde dashboards worden geïmplementeerd als Azure-resources, wat betekent dat ze bestaan als beheerbare objecten binnen uw abonnement en zijn opgenomen in een resourcegroep.  Dashboards zijn vanuit een access control-perspectief niet anders dan andere resources, zoals een virtuele machine of een opslagaccount.

> [!TIP]
> Afzonderlijke tegels op Hallo dashboard afdwingen hun eigen vereisten voor toegangsbeheer op basis van Hallo bronnen die ze weergeven.  Daarom kunt u een dashboard dat globaal wordt gedeeld terwijl beveiligd blijven Hallo gegevens op afzonderlijke tegels ontwerpen.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>Wat is toegangsbeheer voor dashboards
Met op rollen gebaseerde toegangsbeheer (RBAC), kunt u gebruikers tooroles op drie verschillende niveaus van scope toewijzen:

* abonnement
* resourcegroep
* Resource

Hallo machtigingen die u toewijst, worden overgenomen van abonnement omlaag toohello resource. Hallo gepubliceerde dashboard is een resource. Daarom mogelijk hebt u al gebruikers toegewezen tooroles voor Hallo abonnement die ook werken voor gepubliceerde Hallo-dashboard. 

Hier volgt een voorbeeld.  Stel dat u hebt een Azure-abonnement en verschillende leden van uw team zijn toegewezen rollen Hallo van **eigenaar**, **Inzender**, of **lezer** voor Hallo-abonnement. Gebruikers die eigenaar of inzenders kunnen toolist, weergave zijn, maken, wijzigen of verwijderen van dashboards binnen Hallo-abonnement.  Gebruikers die lezers zijn kunnen toolist en bekijk de dashboards zijn, maar kunnen niet worden gewijzigd of verwijderd.  Gebruikers met leestoegang hebben kunnen toomake lokale bewerkingen tooa gepubliceerde dashboard zijn (zoals wanneer een probleem moet oplossen), maar er kan geen toopublish zijn die wijzigingen back toohello-server.  Hebben Hallo optie toomake een persoonlijke kopie van Hallo dashboard voor zichzelf

U kan echter ook machtigingen toohello resourcegroep met verschillende dashboards of afzonderlijke dashboard tooan toewijzen. U kunt bijvoorbeeld besluiten dat een groep gebruikers moet hebben beperkte machtigingen over Hallo abonnement maar groter toegang tooa bepaalde dashboard. U toewijzen de rol van deze gebruikers tooa voor dit dashboard. 

## <a name="publish-dashboard"></a>dashboard publiceren
Stel dat u hebt een dashboard dat u tooshare met een groep gebruikers in uw abonnement wilt configureren. Hallo onderstaande stappen weer een aangepaste groep opslag Managers aangeroepen, maar u kunt uw groep naam wat u wilt. Zie voor meer informatie over het maken van een Active Directory-groep en gebruikers toothat groep toe te voegen [groepen beheren in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

1. Selecteer in het Hallo-dashboard **Share**.
   
     ![Selecteer share](./media/azure-portal-dashboard-share-access/select-share.png)
2. Alvorens toegang toe te wijzen, moet u Hallo dashboard publiceren. Standaard worden Hallo dashboard gepubliceerde tooa resourcegroep met de naam **dashboards**. Selecteer **publiceren**.
   
     ![publish](./media/azure-portal-dashboard-share-access/publish.png)

Uw dashboard is nu gepubliceerd. Als Hallo machtigingen die zijn overgenomen uit het abonnement Hallo geschikt zijn, hoeft u niet toodo iets meer. Andere gebruikers in uw organisatie wordt kunnen tooaccess en Hallo-dashboard op basis van hun abonnement niveau rol wijzigen. Echter, voor deze zelfstudie gaan we een groep van gebruikers tooa rol voor dit dashboard worden toegewezen.

## <a name="assign-access-tooa-dashboard"></a>Toegang tooa dashboard toewijzen
1. Nadat u hebt gepubliceerd Hallo dashboard, selecteert u **gebruikers beheren**.
   
     ![gebruikers beheren](./media/azure-portal-dashboard-share-access/manage-users.png)
2. U ziet een lijst met bestaande gebruikers die een rol voor dit dashboard al zijn toegewezen. De lijst met bestaande gebruikers is anders dan Hallo in onderstaande afbeelding. Zeer waarschijnlijk worden Hallo toewijzingen overgenomen van Hallo-abonnement. tooadd een nieuwe gebruiker of groep, selecteert u **toevoegen**.
   
     ![gebruiker toevoegen](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Selecteer Hallo-rol die Hallo machtigingen die u wilt dat toogrant vertegenwoordigt. Selecteer voor dit voorbeeld **Inzender**.
   
     ![rol selecteren](./media/azure-portal-dashboard-share-access/select-role.png)
4. Hallo-gebruiker of groep die u wenst dat tooassign toohello rol selecteren. Als u Hallo-gebruiker of groep die u in de lijst Hallo zoekt niet ziet, moet u Hallo zoekvak gebruiken. Uw lijst met beschikbare groepen afhankelijk Hallo-groepen die u hebt gemaakt in uw Active Directory.
   
     ![gebruiker selecteren](./media/azure-portal-dashboard-share-access/select-user.png) 
5. Wanneer u klaar bent met het toevoegen van gebruikers of groepen selecteren **OK**. 
6. nieuwe toewijzing Hallo toegevoegd toohello lijst met gebruikers. U ziet dat de **toegang** wordt vermeld als **toegewezen** plaats **overgenomen**.
   
     ![toegewezen rollen](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>Volgende stappen
* Zie voor een lijst met rollen [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).
* toolearn over het beheren van resources, Zie [beheren Azure-resources via de portal](resource-group-portal.md).

