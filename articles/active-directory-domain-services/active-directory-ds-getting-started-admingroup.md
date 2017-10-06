---
title: 'Azure Active Directory Domain Services: Aan de slag | Microsoft Docs'
description: Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 8bde872a13bc9960d1e62c74017ff78a8953a0a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Azure Active Directory Domain Services met behulp van hello Azure-portal (Preview) inschakelen


## <a name="task-3-configure-administrative-group"></a>Taak 3: beheergroep configureren
In deze taak voor de configuratie maakt u een beheergroep in uw Azure AD-directory. Deze speciale beheerdersgroep heet *AAD DC beheerders*. Leden van deze groep worden beheerdersmachtigingen op de computers die lid zijn van een domein toohello beheerd domein zijn verleend. Deze groep wordt de groep administrators toohello toegevoegd op domein machines. Leden van deze groep kunnen ook op afstand toodomain die lid zijn van computers met extern bureaublad tooconnect gebruiken.

> [!NOTE]
> U bent niet gemachtigd domeinbeheerder of ondernemingsbeheerder op Hallo beheerde domein dat u hebt gemaakt met behulp van Azure Active Directory Domain Services. Op de beheerde domeinen deze machtigingen zijn gereserveerd door het Hallo-service en zijn niet beschikbaar toousers binnen Hallo-tenant. U kunt echter gebruiken Hallo speciale beheergroep gemaakt in deze configuratie taak tooperform bevoegde enkele bewerkingen. Deze bewerkingen behoren lid te worden computers toohello domein, die deel uitmaken van de beheergroep toohello op machines domein en het configureren van Groepsbeleid.
>

Hallo-beheergroep maakt Hallo wizard automatisch in uw Azure AD-directory. Deze groep wordt 'AAD DC-beheerders' genoemd. Als u een bestaande groep met deze naam in uw Azure AD-directory hebt, geselecteerd Hallo wizard deze groep. U kunt configureren met behulp van Hallo groepslidmaatschap **beheerdersgroep** wizardpagina.

1. groepslidmaatschap tooconfigure, klikt u op **AAD DC beheerders**.

    ![Groepslidmaatschap configureren](./media/getting-started/domain-services-blade-admingroup.png)

2. Klik op Hallo **leden toevoegen** knop tooadd gebruikers van uw Azure AD directory toohello administrator-groep.

3. Wanneer u klaar bent, klikt u op **OK** toomove op toohello **samenvatting** pagina van wizard Hallo.

4. Op Hallo **samenvatting** pagina van wizard Hallo, bekijk Hallo configuratie-instellingen voor Hallo beheerd domein. U kunt teruggaan tooany stap Hallo wizard toomake wijzigingen indien nodig. Wanneer u klaar bent, klikt u op **OK** toocreate Hallo nieuw beheerd domein.

    ![Samenvatting](./media/getting-started/domain-services-blade-summary.png)

5. U ziet een melding dat de voortgang Hallo van uw Azure AD Domain Services-implementatie geeft. Klik op Hallo melding toosee gedetailleerde uitgevoerd voor Hallo-implementatie.

    ![Melding - implementatie wordt uitgevoerd](./media/getting-started/domain-services-blade-deployment-in-progress.png)


## <a name="provision-your-managed-domain"></a>Inrichten van uw beheerde domein
Hallo-proces voor het leveren van uw beheerde domein kan tooan uur duren.

1. Tijdens de implementatie uitgevoerd wordt, kunt u zoeken naar domain services in Hallo **zoeken bronnen** zoekvak. Selecteer **Azure AD Domain Services** van Hallo zoekresultaat. Hallo **Azure AD Domain Services** blade bevat Hallo beheerde domein dat wordt ingericht.

    ![Zoeken naar beheerde domein wordt ingericht](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Klik op Hallo-naam van Hallo beheerd domein (bijvoorbeeld, contoso100.com') toosee meer informatie over het Hallo-domein.

    ![Domain Services - status voor inrichten heeft](./media/getting-started/domain-services-provisioning-state.png)

3. Hallo **overzicht** tabblad ziet u dat domein Hallo momenteel wordt ingericht. U kunt Hallo beheerd domein niet configureren, totdat deze volledig is ingericht. Het kan uw beheerde domein toobe volledig is ingericht tooan uur duren.

    ![Domain Services - tabblad Overzicht tijdens Hallo Inrichtingsstatus ](./media/getting-started/domain-services-provisioning-state-details.png)

4. Wanneer het beheerde domein Hallo volledig is ingericht, Hallo **overzicht** tabblad ziet u Hallo domein status als **met**.

    ![Domain Services: tabblad Overzicht nadat het domein volledig is ingericht](./media/getting-started/domain-services-provisioned.png)

5. Op Hallo **eigenschappen** tabblad ziet u twee IP-adressen op welk domein domeincontrollers beschikbaar voor Hallo virtueel netwerk zijn.

    ![Domain Services - tabblad Eigenschappen nadat het volledig is ingericht](./media/getting-started/domain-services-provisioned-properties.png)


## <a name="next-step"></a>Volgende stap
[Taak 4: Hallo DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk](active-directory-ds-getting-started-dns.md)
