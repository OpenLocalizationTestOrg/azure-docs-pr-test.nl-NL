---
title: Azure Automation-account aaaManage | Microsoft Docs
description: Dit artikel wordt beschreven hoe toomanage Hallo configuratie van uw Automation-account zoals certificaatvernieuwing, verwijdering en onjuiste configuratie.
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/13/2017
ms.author: magoedte
ms.openlocfilehash: 75e41f601a138d4e8853aa79dcbab6696a5e9fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-automation-account"></a>Azure Automation-account beheren
Op een bepaald moment voordat uw Automation-account is verlopen, moet u toorenew Hallo certificaat. Als u dat Hallo Run As-account er inbreuk is gemaakt denkt, kunt u deze kunt verwijderen en opnieuw maken. Deze sectie wordt beschreven hoe tooperform deze bewerkingen.

## <a name="self-signed-certificate-renewal"></a>Zelfondertekend certificaat vernieuwen
Hallo zelfondertekend certificaat dat u hebt gemaakt voor Hallo Run As-account verloopt een jaar na de datum Hallo van maken. U kunt het certificaat op elk gewenst moment vernieuwen voordat het verloopt. Als u deze vernieuwt, wordt Hallo huidige geldig certificaat terugkerende tooensure dat alle runbooks die in de wachtrij staan actief of actief actief, en die zich verifiëren met Hallo Run As-account, niet nadelig worden beïnvloed. Hallo-certificaat is geldig tot de vervaldatum.

> [!NOTE]
> Als u uw Automation Run As-account toouse een certificaat dat is uitgegeven door de certificeringsinstantie van uw onderneming hebt geconfigureerd en u deze optie gebruikt, wordt de Hallo enterprise-certificaat worden vervangen door een zelfondertekend certificaat.

Hallo toorenew certificaat, Hallo te volgen:

1. Open in hello Azure-portal, Hallo Automation-account.

2. Op Hallo **Automation-Account** blade in Hallo **eigenschappen van Account** deelvenster onder **Accountinstellingen**, selecteer **Run As-Accounts**.

    ![Eigenschappendeelvenster voor Automation-account](media/automation-manage-account/automation-account-properties-pane.png)
3. Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of Hallo klassieke Run As-account die u wilt dat toorenew Hallo certificaat voor.

4. Op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **certificaat vernieuwen**.

    ![Certificaat vernieuwen voor Uitvoeren als-account](media/automation-manage-account/automation-account-renew-runas-certificate.png)

5. Tijdens het Hallo-certificaat wordt vernieuwd, kunt u de voortgang Hallo onder bijhouden **meldingen** in Hallo-menu.

## <a name="delete-a-run-as-or-classic-run-as-account"></a>Een Uitvoeren als- of klassiek Uitvoeren als-account verwijderen
Deze sectie wordt beschreven hoe toodelete en opnieuw maken van een Run As- of klassieke Run As-account. Wanneer u deze actie uitvoert, wordt Hallo Automation-account bewaard. Nadat u een Run As- of klassieke Run As-account verwijdert, kunt u het opnieuw maken in hello Azure-portal.

1. Open in hello Azure-portal, Hallo Automation-account.

2. Op Hallo **Automation-account** blade in Hallo account eigenschappendeelvenster selecteert **Run As-Accounts**.

3. Op Hallo **Run As-Accounts** eigenschappenblade, selecteer de Hallo Run As-account of klassieke Run As-account dat u wilt dat toodelete. Klik vervolgens op Hallo **eigenschappen** blade voor Hallo account hebt geselecteerd, klikt u op **verwijderen**.

 ![Uitvoeren als-account verwijderen](media/automation-manage-account/automation-account-delete-runas.png)

4. Tijdens het Hallo-account wordt verwijderd, u kunt de voortgang Hallo onder volgen **meldingen** in Hallo-menu.

5. Nadat het Hallo-account is verwijderd, kunt u opnieuw dit maken op Hallo **Run As-Accounts** eigenschappenblade door het selecteren van Hallo maken de optie **Azure uitvoeren als-Account**.

 ![Hallo Automation Run As-account opnieuw maken](media/automation-manage-account/automation-account-create-runas.png)

## <a name="misconfiguration"></a>Onjuiste configuratie
Bepaalde configuratie-items die nodig zijn voor Hallo Run As- of klassieke Run As-account toofunction goed mogelijk is verwijderd of niet goed worden gemaakt tijdens de eerste configuratie. Hallo-items omvatten:

* Certificaatasset
* Verbindingsasset
* Run As-account is verwijderd uit de rol Inzender Hallo
* Service-principal of toepassing in Azure AD

In de voorgaande Hallo en andere exemplaren van onjuiste configuratie, detecteert Hallo Automation-account Hallo wijzigingen en een status weer van *onvolledig* op Hallo **Run As-Accounts** eigenschappenblade voor Hallo account.

![Onvolledige Uitvoeren als-configuratiestatus](media/automation-manage-account/automation-account-runas-incomplete-config.png)

Wanneer u Hallo Run As-account selecteert, Hallo account **eigenschappen** deelvenster Hallo volgende foutbericht weergegeven:

![Waarschuwingsbericht Onvolledige Uitvoeren als-configuratie](media/automation-manage-account/automation-account-runas-incomplete-config-msg.png).

Deze problemen Run As-account kunt u snel oplossen door te verwijderen en opnieuw Hallo-account te maken.

## <a name="next-steps"></a>Volgende stappen
* Voor meer informatie over Service-Principals te verwijzen[toepassingsobjecten en Service-Principal objecten](../active-directory/active-directory-application-objects.md).
* Voor meer informatie over toegangsbeheer op basis van rollen in Azure Automation te verwijzen[toegangsbeheer op basis van rollen in Azure Automation](automation-role-based-access-control.md).
* Voor meer informatie over certificaten en Azure-services te verwijzen[certificaten voor Azure Cloud Services-overzicht](../cloud-services/cloud-services-certs-create.md).
