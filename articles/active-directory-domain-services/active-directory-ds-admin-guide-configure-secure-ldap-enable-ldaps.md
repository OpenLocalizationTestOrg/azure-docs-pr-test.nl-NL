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
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
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


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a>Taak 3: Schakel veilige LDAP voor Hallo beheerde domein met hello Azure-portal (Preview)
tooenable beveiligde LDAP, voert u Hallo configuratiestappen te volgen:

1. Navigeer toohello  **[Azure-portal](https://portal.azure.com)**.

2. Zoeken naar domain services in Hallo **zoeken bronnen** zoekvak. Selecteer **Azure AD Domain Services** van Hallo zoekresultaat. Hallo **Azure AD Domain Services** blade geeft een lijst van uw beheerde domein.

    ![Zoeken naar beheerde domein wordt ingericht](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. Klik op Hallo-naam van Hallo beheerd domein (bijvoorbeeld, contoso100.com') toosee meer informatie over het Hallo-domein.

    ![Domain Services - status voor inrichten heeft](./media/getting-started/domain-services-provisioning-state.png)

3. Klik op **beveiligde LDAP** op Hallo navigatiedeelvenster.

    ![Domain Services - blade beveiligde LDAP](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. Beveiligde LDAP toegang tooyour beheerd domein is standaard uitgeschakeld. Wisselknop **beveiligde LDAP** te**inschakelen**.

    ![Beveiligde LDAP inschakelen](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. Standaard beheerde beveiligde LDAP toegang tooyour domein via Hallo die Internet is uitgeschakeld. Wisselknop **beveiligde LDAP-toegang toestaan via internet Hallo** te**inschakelen**, indien gewenst. 

6. Klik op Hallo map pictogram volgende **. PFX-bestand met LDAP om certificaten veilig**. Hallo pad toohello PFX-bestand met de Hallo-certificaat voor beveiligde LDAP toegang toohello beheerde domein opgeven.

7. Geef Hallo **toodecrypt wachtwoord. PFX-bestand**. Hallo bieden hetzelfde wachtwoord dat u hebt gebruikt bij het exporteren van Hallo toohello PFX-certificaatbestand.

8. Wanneer u klaar bent, klikt u op Hallo **opslaan** knop.

9. U ziet een melding dat informeert u dat beveiligde LDAP wordt geconfigureerd voor Hallo beheerde domein. Totdat deze bewerking voltooid is, kunt u andere instellingen voor Hallo domein niet wijzigen.

    ![Beveiligde LDAP voor Hallo beheerde domein configureren](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> Het duurt ongeveer 10 too15 minuten tooenable beveiligde LDAP voor uw beheerde domein. Hallo opgegeven beveiligde LDAP-certificaat komt niet overeen met Hallo vereist criteria, beveiligde LDAP is niet ingeschakeld voor uw directory als er een fout. Bijvoorbeeld Hallo domeinnaam is onjuist, Hallo-certificaat is al verlopen of verloopt binnenkort. In dit geval, probeer het opnieuw met een geldig certificaat.
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a>Taak 4: configureer DNS-tooaccess Hallo beheerde domein van Hallo internet
> [!NOTE]
> **Optionele taak** : als u niet van plan bent tooaccess Hallo beheerde domein LDAPS met meer dan Hallo internet, deze configuratietaak overslaan.
>
>

Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

Wanneer u beveiligde LDAP toegang hebt ingeschakeld via internet Hallo voor uw beheerde domein, moet u tooupdate DNS zodat clientcomputers dit beheerde domein vindt. Aan het einde van de Hallo van taak 3, een externe IP-adres wordt weergegeven op Hallo **eigenschappen** blade in **externe IP-adres voor LDAPS toegang**.

Uw externe DNS-provider configureren voor DNS-naam Hallo Hallo beheerd domein (bijvoorbeeld ' ldaps.contoso100.com') punten toothis externe IP-adres. In ons voorbeeld moeten we toocreate Hallo DNS-vermelding te volgen:

    ldaps.contoso100.com  -> 52.165.38.113

Dat is alles: u bent nu klaar tooconnect toohello beheerd domein met beveiligde LDAP via internet Hallo.

> [!WARNING]
> Houd er rekening mee dat clientcomputers is Hallo verlener van Hallo LDAPS certificaat toobe kunnen tooconnect moeten vertrouwen toohello beheerd domein LDAPS wordt gebruikt. Als u een openbaar vertrouwde certificeringsinstantie (CA) gebruikt, hoeft u niet toodo iets omdat deze certificaatverleners clientcomputers worden vertrouwd. Als u een zelfondertekend certificaat gebruikt, installeert u Hallo openbare deel van de zelf-ondertekend certificaat Hallo in Hallo vertrouwde certificaatarchief op de clientcomputer Hallo.
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a>Taak 5 - vergrendeling LDAPS tooyour beheerde toegang tot het domein via internet Hallo
> [!NOTE]
> **Optionele taak** : als u niet hebt ingeschakeld LDAPS toegang toohello beheerd domein meer dan internet hello, deze configuratietaak overslaan.
>
>

Voordat u deze taak, zorg ervoor dat u hebt voltooid Hallo stappen in [taak 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).

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
