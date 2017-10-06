---
title: aaaConfigure Secure LDAP (LDAPS) in Azure AD Domain Services | Microsoft Docs
description: Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a>Beveiligde LDAP (LDAPS) voor een beheerd domein van Azure AD Domain Services configureren

## <a name="before-you-begin"></a>Voordat u begint
Zorg ervoor dat u hebt voltooid [taak 2 - export Hallo beveiligde LDAP certificaat tooa. PFX-bestand](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).

Kiezen of toouse Hallo preview-ervaring met Azure portal of hello Azure classic portal toocomplete deze taak.
> [!div class="op_single_selector"]
> * **Azure-portal (Preview)**: [inschakelen secure LDAP hello Azure-portal gebruiken](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)
> * **Klassieke Azure-portal**: [inschakelen met behulp van de klassieke Azure portal Hallo LDAP beveiligen](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a>Taak 3: beveiligde LDAP voor Hallo beheerde domein met de klassieke Azure portal Hallo inschakelen
tooenable beveiligde LDAP, voert u Hallo configuratiestappen te volgen:

1. Navigeer toohello  **[klassieke Azure-portal](https://manage.windowsazure.com)**.
2. Selecteer Hallo **Active Directory** knooppunt in het linkerdeelvenster Hallo.
3. Selecteer hello Azure AD-directory (ook waarnaar wordt verwezen tooas 'tenant'), waarvoor u Azure AD Domain Services hebt ingeschakeld.

    ![Azure AD-directory selecteren](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Klik op Hallo **configureren** tabblad.

    ![Tabblad Configureren van directory](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. Schuif omlaag in het gedeelte van toohello **domeinservices**. U ziet een optie met de titel **beveiligde LDAP (LDAPS)** zoals weergegeven in de volgende schermafbeelding Hallo:

    ![Configuratiesectie Domeinservices](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. Klik op Hallo **certificaat configureren...**  knop toobring up Hallo **certificaat configureren voor Secure LDAP** dialoogvenster.

    ![Certificaat voor veilige LDAP configureren](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. Klik op Hallo map pictogram volgende **PFX-bestand met certificaat** toospecify Hallo PFX-bestand dat u wenst dat toouse voor beveiligde LDAP toegang toohello Hallo-certificaat bevat beheerd domein. Ook Hallo wachtwoord die u hebt opgegeven bij het exporteren van Hallo toohello PFX-certificaatbestand invoeren. Klik vervolgens op Hallo knop op Hallo onder gedaan.

    ![Beveiligde LDAP PFX-bestand en een wachtwoord opgeven](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. Hallo **domeinservices** sectie Hallo **configureren** tabblad moet ophalen lichter gekleurd weergegeven en in Hallo **in behandeling...**  staat zijn voor een paar minuten. Tijdens deze periode Hallo LDAPS-certificaat is geverifieerd voor nauwkeurigheid en beveiligde LDAP is geconfigureerd voor uw beheerde domein.

    ![Beveiligde LDAP - status in behandeling](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > Het duurt ongeveer 10 too15 minuten tooenable beveiligde LDAP voor uw beheerde domein. Hallo opgegeven beveiligde LDAP-certificaat komt niet overeen met Hallo vereist criteria, beveiligde LDAP is niet ingeschakeld voor uw directory als er een fout. Bijvoorbeeld Hallo domeinnaam is onjuist, Hallo-certificaat is al verlopen of verloopt binnenkort.
   >
   >

9. Wanneer u beveiligde LDAP is ingeschakeld voor uw beheerde domein, Hallo **in behandeling...**  bericht verdwijnt. U ziet Hallo vingerafdruk van certificaat dat Hallo weergegeven.

    ![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a>Taak 4: het inschakelen van beveiligde LDAP toegang via Hallo internet
**Optionele taak** : als u niet van plan bent tooaccess Hallo beheerde domein LDAPS met meer dan Hallo internet, deze configuratietaak overslaan.

Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).

1. U ziet een optie te**Hallo inschakelen SECURE LDAP toegang via INTERNET** in Hallo **domeinservices** sectie Hallo **configureren** pagina. Deze optie is ingesteld, te**Nee** standaard omdat internet toegang toohello beheerd domein via beveiligde LDAP is standaard uitgeschakeld.

    ![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. Wisselknop **Hallo inschakelen SECURE LDAP toegang via INTERNET** te**Ja**. Klik op Hallo **opslaan** knop op Hallo onderpaneel.
    ![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)
3. Hallo **domeinservices** sectie Hallo **configureren** tabblad moet ophalen lichter gekleurd weergegeven en in Hallo **in behandeling...**  staat zijn voor een paar minuten. Na enige tijd is toegang tooyour beheerde internetdomein via beveiligde LDAP ingeschakeld.

    ![Beveiligde LDAP - status in behandeling](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > Het duurt ongeveer 10 minuten tooenable toegang tot internet via beveiligde LDAP voor uw beheerde domein.
   >
   >
4. Wanneer beveiligde LDAP toegang tooyour beheerd domein via Hallo internet is ingeschakeld, Hallo **in behandeling...**  bericht verdwijnt. U ziet Hallo extern IP-adres dat kan worden gebruikt tooaccess uw directory via LDAPS in Hallo veld **externe IP-adres voor LDAPS toegang**.

    ![Beveiligde LDAP ingeschakeld](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Taak 5: configureer DNS-tooaccess Hallo beheerde domein van Hallo internet
**Optionele taak** : als u niet van plan bent tooaccess Hallo beheerde domein LDAPS met meer dan Hallo internet, deze configuratietaak overslaan.

Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 4](#task-4---enable-secure-ldap-access-over-the-internet).

Wanneer u beveiligde LDAP toegang hebt ingeschakeld via internet Hallo voor uw beheerde domein, moet u tooupdate DNS zodat clientcomputers dit beheerde domein vindt. Aan het einde van de Hallo van taak 4, een externe IP-adres wordt weergegeven op Hallo **configureren** tabblad **externe IP-adres voor LDAPS toegang**.

Uw externe DNS-provider configureren voor DNS-naam Hallo Hallo beheerd domein (bijvoorbeeld ' ldaps.contoso100.com') punten toothis externe IP-adres. In ons voorbeeld moeten we toocreate Hallo DNS-vermelding te volgen:

    ldaps.contoso100.com  -> 52.165.38.113

Dat is alles: u bent nu klaar tooconnect toohello beheerd domein met beveiligde LDAP via internet Hallo.

> [!WARNING]
> Houd er rekening mee dat clientcomputers is Hallo verlener van Hallo LDAPS certificaat toobe kunnen tooconnect moeten vertrouwen toohello beheerd domein LDAPS wordt gebruikt. Als u gebruikmaakt van een certificeringsinstantie voor ondernemingen of een openbaar vertrouwde certificeringsinstantie (CA), hoeft u niet toodo iets omdat deze certificaatverleners clientcomputers worden vertrouwd. Als u een zelfondertekend certificaat gebruikt, moet u tooinstall Hallo openbare deel van de zelf-ondertekend certificaat Hallo in Hallo vertrouwde certificaatarchief op de clientcomputer Hallo.
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Vergrendeling LDAPS via Hallo tooyour beheerd domein toegang krijgen tot internet
> [!NOTE]
> **Optionele taak** : als u niet hebt ingeschakeld LDAPS toegang toohello beheerd domein meer dan internet hello, deze configuratietaak overslaan.
>
>

Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 4](#task-4---enable-secure-ldap-access-over-the-internet).

Het blootstellen van uw beheerde domein voor LDAPS toegang via Hallo vertegenwoordigt internet een beveiligingsrisico. Hallo beheerd domein is bereikbaar is vanaf Hallo internet op Hallo-poort die wordt gebruikt voor beveiligde LDAP (dat wil zeggen, poort 636). U kunt daarom toorestrict toegang toohello beheerd domein toospecific bekende IP-adressen. Voor betere beveiliging, een netwerkbeveiligingsgroep (NSG) maken en deze koppelen aan Hallo subnet waar u Azure AD Domain Services hebt ingeschakeld.

Hallo volgende tabel ziet u een voorbeeld van een NSG u configureren kunt, toolock omlaag beveiligde LDAP toegang via Hallo internet. Hallo NSG bevat een reeks regels waarmee binnenkomende LDAPS toegang via TCP-poort 636 alleen uit een opgegeven set van IP-adressen. Hallo 'DenyAll' standaardregel geldt tooall andere binnenkomend verkeer van Hallo internet. Hallo NSG regel tooallow LDAPS toegang via Hallo internet vanaf de opgegeven IP-adressen heeft een hogere prioriteit dan Hallo DenyAll NSG-regel.

![Voorbeeld NSG toosecure LDAPS toegang via internet Hallo](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

**Meer informatie** - [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).

<br>

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
* [Groepsbeleid voor een Azure AD Domain Services beheerd domein beheren](active-directory-ds-admin-guide-administer-group-policy.md)
* [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md)
* [Een Netwerkbeveiligingsgroep maken](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
