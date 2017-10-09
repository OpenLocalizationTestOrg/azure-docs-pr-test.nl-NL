---
title: Toegangsbeheer op basis van aaaRole in hello Azure-portal | Microsoft Docs
description: In het beheer van toegang aan de slag met toegangsbeheer op basis van rollen in hello Azure-Portal. Rol toewijzingen tooassign machtigingen tooyour resources gebruiken.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Toegangsbeheer op basis van rollen toomanage toegang tooyour Azure-abonnementresources gebruiken
> [!div class="op_single_selector"]
> * [Toegang beheren per gebruiker of groep](role-based-access-control-manage-assignments.md)
> * [Toegang beheren per resource](role-based-access-control-configure.md)

Met op rollen gebaseerd toegangsbeheer (RBAC) beschikt u over geavanceerd toegangsbeheer voor Azure. Met RBAC kunt verleent u alleen Hallo hoeveelheid toegang die gebruikers nodig tooperform hun werk hebben. In dit artikel helpt u bij leren werken met RBAC in hello Azure-portal. Zie [Wat is op rollen gebaseerd toegangsbeheer](role-based-access-control-what-is.md) als u meer informatie wilt over het beheren van toegang met RBAC.

U kunt binnen elk abonnement verlenen up too2000 roltoewijzingen. 

## <a name="view-access"></a>Toegang voor weergeven
U kunt zien wie heeft toegang tot tooa resource, resourcegroep of abonnement op de hoofdblade in Hallo [Azure-portal](https://portal.azure.com). We willen bijvoorbeeld toosee wie toegang tot tooone van onze resourcegroepen heeft:

1. Selecteer **resourcegroepen** Hallo navigatiebalk aan de linkerkant Hallo aan.  
    ![Resourcegroepen - pictogram](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Selecteer Hallo-naam van de resourcegroep Hallo van Hallo **resourcegroepen** blade.
3. Selecteer **toegangsbeheer (IAM)** in het linkermenu Hallo.  
4. Hallo Access control-blade geeft een lijst van alle gebruikers, groepen en toepassingen die toegang toohello resourcegroep hebben gekregen.  
   
    ![Schermafbeelding van de blade Gebruikers - overgenomen en toegewezen toegang](./media/role-based-access-control-configure/view-access.png)

U ziet dat sommige rollen zijn binnen het bereik te**deze resource** terwijl andere **overgenomen** vanuit een ander bereik. Toegang is specifiek toohello resourcegroep toegewezen of overgenomen van een toewijzing toohello bovenliggende abonnement.

> [!NOTE]
> Klassieke abonnementsbeheerders en co-beheerders worden beschouwd als eigenaar van het Hallo-abonnement in Hallo nieuwe RBAC-model.

## <a name="add-access"></a>Toegang voor toevoegen
U verleent toegang vanuit het Hallo-resource, resourcegroep of abonnement dat is Hallo omvang van de roltoewijzing Hallo.

1. Selecteer **toevoegen** op Hallo Access control-blade.  
2. Selecteer Hallo rol desgewenst tooassign van Hallo **Selecteer een rol** blade.
3. Hallo-gebruiker, groep of toepassing selecteren in uw directory die u toegang tot toogrant wilt. Hallo-directory met weergavenamen, e-mailadressen en object-id's, kunt u zoeken.  
   
    ![Schermafbeelding van de blade Gebruikers toevoegen - zoeken](./media/role-based-access-control-configure/grant-access2.png)
4. Selecteer **OK** toocreate Hallo toewijzing. Hallo **gebruiker toevoegen** pop Hallo voortgang bijgehouden.  
    ![Schermafbeelding van de voortgangsbalk Gebruiker toevoegen](./media/role-based-access-control-configure/addinguser_popup.png)

Nadat een roltoewijzing is toegevoegd, wordt deze weergegeven op Hallo **gebruikers** blade.

## <a name="remove-access"></a>Toegang verwijderen
1. Houd de cursor boven het Hallo-naam van de gewenste tooremove Hallo-toewijzing. Een selectievakje weergegeven naam van de volgende toohello.
2. Hallo selectievakjes tooselect gebruiken een of meer roltoewijzingen.
2. Selecteer **Verwijderen**.  
3. Selecteer **Ja** tooconfirm Hallo verwijderen.

Overgenomen toewijzingen kunnen niet worden verwijderd. Als u een overgenomen toewijzing tooremove nodig hebt, moet u toodo op het Hallo bereik waarin Hallo roltoewijzing is gemaakt. In Hallo **bereik** kolom, het volgende te**overgenomen** er is een koppeling waarmee u toohello resources waaraan deze rol is toegewezen. Ga toohello resource vermeld tooremove Hallo roltoewijzing.

![Schermafbeelding van de blade Gebruikers - bij overgenomen toegang is knop Verwijderen uitgeschakeld](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Andere hulpprogramma's voor toomanage toegang
U kunt rollen toewijzen en toegang beheren met Azure RBAC-opdrachten in hulpprogramma's dan hello Azure-portal.  Volg Hallo koppelingen toolearn meer over Hallo vereisten en aan de slag met hello Azure RBAC-opdrachten.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Azure-opdrachtregelinterface](role-based-access-control-manage-access-azure-cli.md)
* [REST API](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Volgende stappen
* [Een geschiedenisrapport voor gewijzigde toegang maken](role-based-access-control-access-change-history-report.md)
* Zie Hallo [ingebouwde RBAC-rollen](role-based-access-built-in-roles.md)
* Definieer uw eigen [Aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md)

