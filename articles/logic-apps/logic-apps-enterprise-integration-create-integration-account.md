---
title: aaaCreate, koppelen, verwijderen of verplaatsen van een account integratie in Azure logic apps | Microsoft Docs
description: Hoe een integratie toocreate account en een koppeling tooyour logic apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a>Wat is een integratie-account?

Een account integratie kunt enterprise integration apps toomanage artefacten, met inbegrip van schema's, kaarten, certificaten, partners en -overeenkomsten. Elke integratie-app die u gebruikt een account integratie tooaccess deze schema's, kaarten, certificaten, enzovoort.

## <a name="create-an-integration-account"></a>Een integratie-account maken

1.  Meld u aan toohello [Azure-portal](http://portal.azure.com "Azure-portal"). Selecteer in het linkermenu Hallo **meer services**.

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Typ in het zoekvak hello, '-integratie"voor uw filter. Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Kies bovenaan Hallo Hallo pagina, **toevoegen**.

    ![Kies toevoegen](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. Naam van uw account integratie en selecteer hello Azure-abonnement dat u wilt dat toouse. U kunt een nieuwe maken **resourcegroep** of Selecteer een bestaande resourcegroep. Selecteer vervolgens een **locatie** voor het hosten van uw account integratie en een **prijscategorie**. 

    Als u klaar bent, kiest u **maken**.

    ![Informatie opgeven voor uw account integratie](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    Azure richt uw account integratie in Hallo geselecteerd locatie, die moet worden voltooid binnen 1 minuut.

5. Hallo pagina vernieuwen. U ziet uw nieuwe integratie account weergegeven.

    ![Uw nieuwe account voor de integratie wordt weergegeven](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

Vervolgens koppel Hallo integratie-account dat u gemaakte tooyour logische app. 

## <a name="link-an-integration-account-tooa-logic-app"></a>Een integratie account tooa logische app koppelen

toogive uw logische apps toegang krijgen tot toomaps, schema's, overeenkomsten en andere artefacten in uw account integratie, koppeling Hallo integratie account tooyour logische app.

### <a name="prerequisites"></a>Vereisten

* Een account voor de integratie
* Een logische app

> [!NOTE] 
> Zorg ervoor dat uw account en logica app voor integratie in Hallo *dezelfde Azure-locatie* voordat u begint.


1. Selecteer uw logische app in hello Azure-portal, en controleer uw logische app locatie.

    ![Selecteer uw logische app, locatie controleren](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. Onder **instellingen**, selecteer **integratie Account**.

    ![Selecteer 'Integratie Account'](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. Van Hallo **selecteert u een account integratie** wilt weergeven, selecteer Hallo integratie account u wilt dat toolink tooyour logische app. toofinish koppelt, kies **opslaan**.

    ![Selecteer uw integratie-account](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    Krijgt u een melding dat uw integratie-account is gekoppeld tooyour logische app en alle artefacten in uw account integratie zijn nu beschikbaar tooyour logische app weergeeft.

    ![Uw logische app is gekoppeld tooyour integratie-account](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

Nu dat uw account integratie gekoppelde tooyour logic app is, kunt u Hallo B2B-connectors kunt gebruiken in logic apps. Sommige algemene B2B-connectors zijn XML-validatie en plat bestand coderen/decoderen.  

## <a name="delete-your-integration-account"></a>Uw account integratie verwijderen

1. Selecteer **meer services**.

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Typ in het zoekvak hello, '-integratie"voor uw filter. Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. Hallo-integratie-account dat u wilt dat toodelete selecteren.

    ![Integratie account toodelete selecteren](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. Kies Hallo menu **verwijderen**.

    ![Kies 'Verwijderen'](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. Bevestig uw keuze toodelete Hallo integratie-account.

## <a name="move-your-integration-account"></a>Uw account integratie verplaatsen

toomove een integratie account tooanother Azure-abonnement of de resource-groep, volg deze stappen.

> [!IMPORTANT]
> Nadat u een account integratie verplaatst, moet u alle scripts toouse Hallo nieuwe resource-id's bijwerken.

1. Selecteer **meer services**.

    !['Meer services' selecteren](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. Typ in het zoekvak hello, '-integratie"voor uw filter. Selecteer in de lijst met resultaten Hallo **Integratieaccounts**.

    ![Filteren op "-integratie", selecteert u 'Integratieaccounts'](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. Hallo-integratie-account dat u wilt dat toomove selecteren. Onder **instellingen**, kies **eigenschappen**.

    ![Selecteer integratie account toomove. Kies onder instellingen eigenschappen](./media/logic-apps-enterprise-integration-accounts/move.png)

5. Hallo resourcegroep of Azure-abonnement dat is gekoppeld aan uw account integratie wijzigen.

    ![Kies wijziging resourcegroep of abonnement wijzigen](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over de overeenkomsten](../logic-apps/logic-apps-enterprise-integration-agreements.md "meer informatie over enterprise integration-overeenkomsten")  

