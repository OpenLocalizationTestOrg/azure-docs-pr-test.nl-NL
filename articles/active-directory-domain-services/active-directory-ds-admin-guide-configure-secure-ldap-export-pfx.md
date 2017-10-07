---
title: aaaConfigure Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: 356b28f8392b0e203df9c81177ec842d52866c4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren

## <a name="before-you-begin"></a>Voordat u begint
Zorg ervoor dat u hebt voltooid [taak 1: een certificaat verkrijgen voor beveiligde LDAP](active-directory-ds-admin-guide-configure-secure-ldap.md).


## <a name="task-2---export-hello-secure-ldap-certificate-tooa-pfx-file"></a>Taak 2: Hallo beveiligde LDAP certificaat tooa exporteren. PFX-bestand
Voordat u deze taak, zorg ervoor dat u Hallo beveiligde LDAP-certificaat hebt verkregen van een openbare certificeringsinstantie (CA) of een zelfondertekend certificaat hebt gemaakt.

Hallo stappen uitvoert, tooexport Hallo LDAPS tooa van het certificaat. PFX-bestand.

1. Druk op Hallo **Start** knop en het type **R**. In Hallo **uitvoeren** dialoogvenster, type **mmc** en klik op **OK**.

    ![Hallo MMC-console starten](./media/active-directory-domain-services-admin-guide/secure-ldap-start-run.png)
2. Op Hallo **User Account Control** gevraagd, klikt u op **Ja** toolaunch MMC (Microsoft Management Console) als administrator.
3. Van Hallo **bestand** menu, klikt u op **module toevoegen/verwijderen...** .

    ![Console-module tooMMC toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-snapin.png)
4. In Hallo **toevoegen of verwijderen van modules** dialoogvenster, selecteer Hallo **certificaten** -module en klikt u op Hallo **toevoegen >** knop.

    ![De console tooMMC-module Certificaten toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin.png)
5. In Hallo **-module Certificaten** wizard selecteert u **computeraccount** en klik op **volgende**.

    ![Module Certificaten voor computeraccount toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-computer-account.png)
6. Op Hallo **Computer selecteren** pagina **lokale computer: (Hallo-computer waarop deze console wordt uitgevoerd)** en klik op **voltooien**.

    ![Module Certificaten - Selecteer computer toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-local-computer.png)
7. In Hallo **toevoegen of verwijderen van modules** dialoogvenster, klikt u op **OK** tooadd Hallo certificaten module tooMMC.

    ![Certificaten-module tooMMC - gedaan toevoegen](./media/active-directory-domain-services-admin-guide/secure-ldap-add-certificates-snapin-done.png)
8. Klik in de MMC-venster Hallo tooexpand **consolebasis**. U ziet Hallo module Certificaten geladen. Klik op **certificaten (lokale Computer)** tooexpand. Klik op tooexpand hello **persoonlijke** knooppunt, gevolgd door Hallo **certificaten** knooppunt.

    ![Archief met persoonlijke certificaten openen](./media/active-directory-domain-services-admin-guide/secure-ldap-open-personal-store.png)
9. U ziet Hallo zelfondertekend certificaat gemaakt. U kunt nagaan Hallo eigenschappen van Hallo certificaat tooensure Hallo vingerafdruk overeenkomt met die voor de PowerShell-vensters Hallo gerapporteerd tijdens het Hallo-certificaat is gemaakt.
10. Selecteer Hallo zelfondertekend certificaat en **met de rechtermuisknop op**. Selecteer in het contextmenu hello, **alle taken** en selecteer **exporteren...** .

    ![Certificaat exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert.png)
11. In Hallo **Wizard Certificaat exporteren**, klikt u op **volgende**.

    ![Certificaatwizard exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-cert-wizard.png)
12. Op Hallo **persoonlijke sleutel exporteren** pagina **Ja, Hallo persoonlijke sleutel exporteren**, en klik op **volgende**.

    ![De persoonlijke certificaatsleutel exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-export-private-key.png)

    > [!WARNING]
    > De persoonlijke sleutel Hallo samen met de Hallo certificaat, moet u exporteren. Als u een PFX die bevat geen persoonlijke sleutel van de Hallo voor Hallo certificaat opgeeft, mislukt beveiligde LDAP voor uw beheerde domein inschakelen.
    >
    >
13. Op Hallo **bestandsindeling voor Export** pagina **Personal Information Exchange - PKCS #12 (. (PFX)** als Hallo-bestandsindeling voor Hallo certificaat geëxporteerd.

    ![Certificaat-bestandsindeling voor export](./media/active-directory-domain-services-admin-guide/secure-ldap-export-to-pfx.png)

    > [!NOTE]
    > Alleen hello. PFX-indeling wordt ondersteund. Hallo certificaat toohello niet exporteren. CER-bestandsindeling.
    >
    >
14. Op Hallo **beveiliging** pagina, selecteer Hallo **wachtwoord** optie en typt u een wachtwoord tooprotect Hallo. PFX-bestand. Onthoud dit wachtwoord omdat in de volgende taak Hallo wel vereist. Klik op **volgende** tooproceed.

    ![Wachtwoord voor het exporteren van certificaat ](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-password.png)

    > [!NOTE]
    > Noteer dit wachtwoord. U moet deze tijdens het inschakelen van beveiligde LDAP voor dit beheerde domein in [taak 3 - beveiligde LDAP voor Hallo beheerde domein inschakelen](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
    >
    >
15. Op Hallo **bestand tooExport** pagina, Hallo-bestandsnaam en locatie waar u tooexport Hallo certificaat wilt opgeven.

    ![Pad voor het exporteren van certificaat](./media/active-directory-domain-services-admin-guide/secure-ldap-export-select-path.png)
16. Klik op Hallo volgende pagina op **voltooien** tooexport hello tooa PFX-certificaatbestand. U ziet bevestigingsvenster wanneer Hallo-certificaat is geëxporteerd.

    ![Gedaan certificaat exporteren](./media/active-directory-domain-services-admin-guide/secure-ldap-exported-as-pfx.png)


## <a name="next-step"></a>Volgende stap
[Taak 3: het inschakelen van beveiligde LDAP voor Hallo beheerd domein](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
