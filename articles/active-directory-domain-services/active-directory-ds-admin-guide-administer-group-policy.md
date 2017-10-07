---
title: 'Azure Active Directory Domain Services: Groepsbeleid op de beheerde domeinen beheren | Microsoft Docs'
description: Groepsbeleid beheren op Azure Active Directory Domain Services beheerde domeinen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Groepsbeleid voor een Azure AD Domain Services beheerd domein beheren
Azure Active Directory Domain Services omvat ingebouwde groepsbeleidsobjecten (GPO's) voor Hallo 'AADDC gebruikers' en 'AADDC Computers' containers. U kunt deze ingebouwde groepsbeleidsobjecten tooconfigure Groepsbeleid op Hallo beheerd domein. Leden van Hallo ' AAD DC' beheerdersgroep kunnen bovendien hun eigen aangepaste OE's maken in Hallo beheerde domein. Ze kunnen ook aangepaste groepsbeleidsobjecten maken, en koppel deze toothese aangepaste organisatie-eenheden. Gebruikers die deel uitmaken van toohello ' AAD DC' beheerdersgroep krijgen beheerprivileges heeft Groepsbeleid op Hallo beheerde domein.

## <a name="before-you-begin"></a>Voordat u begint
tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:

1. Een geldige **Azure-abonnement**.
2. Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.
3. **Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory. Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).
4. Een **domein virtuele machine** hello Azure AD Domain Services beheerd domein uit die u beheert. Als u dergelijke een virtuele machine geen hebt, volgt u alle Hallo taken die worden beschreven in artikel Hallo [lid worden van een beheerd domein voor Windows virtuele machine tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. U moet referenties op Hallo van een **account behoren toohello 'AAD DC-beheerders' gebruikersgroep** in uw directory tooadminister Groepsbeleid voor uw beheerde domein.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Taak 1 - inrichten van een virtuele machine domein tooremotely Groepsbeleid voor Hallo beheerd domein beheren
Azure AD Domain Services beheerde domeinen kunnen worden beheerd op afstand met vertrouwd Active Directory-beheerprogramma's zoals Hallo Active Directory-beheercentrum (ADAC) of AD PowerShell. Groepsbeleid voor het beheerde domein Hallo kan ook worden beheerd extern met beheerhulpprogramma's voor Groepsbeleid Hallo.

Beheerders in uw Azure AD-directory hebt geen rechten tooconnect toodomain controllers op Hallo beheerd domein via Extern bureaublad. Leden van Hallo ' AAD DC' beheerdersgroep kunnen extern Groepsbeleid voor beheerde domeinen beheren. Hulpprogramma's voor Groepsbeleid kan worden gebruikt op een Windows-Server /-client computer lid toohello beheerd domein. Hulpprogramma's voor groep kunnen worden geïnstalleerd als onderdeel van Hallo Group Policy Management optioneel onderdeel op Windows Server en client-computers die lid zijn van toohello beheerd domein.

de eerste taak Hallo is tooprovision een virtuele machine van Windows Server die is gekoppeld toohello beheerd domein. Voor instructies raadpleegt u artikel toohello [lid worden van een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Taak 2 - hulpprogramma's voor Groepsbeleid voor installatie op Hallo virtuele machine
Hallo stappen tooinstall Hallo Groepsbeleid beheerprogramma's te volgen op Hallo verbonden met het domein virtuele machine uitvoeren.

1. Navigeer te**virtuele Machines** knooppunt in Hallo klassieke Azure-portal. Selecteer Hallo virtuele machine die u in taak 1 hebt gemaakt en klik op **Connect** op de opdrachtbalk Hallo HALLO hallo venster onderaan in.

    ![Verbinding maken met tooWindows virtuele machine](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. klassieke portal Hallo tooopen wordt u gevraagd of een bestand met de extensie '.rdp' opslaan die gebruikte tooconnect toohello virtuele machine is. Wanneer het downloaden is voltooid, klikt u op Hallo-bestand.
3. Op Hallo aanmeldprompt weergegeven, gebruiken Hallo referenties van een gebruiker die toohello ' AAD DC' beheerdersgroep hoort. Bijvoorbeeld, gebruiken we 'bob@domainservicespreview.onmicrosoft.com' in ons geval.
4. Open in het startscherm hello, **Serverbeheer**. Klik op **functies en onderdelen toevoegen** in de centrale deelvenster Hallo van Hallo venster in Serverbeheer.

    ![Serverbeheer starten op de virtuele machine](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Op Hallo **voordat u begint** pagina Hallo **Wizard Functies toevoegen en onderdelen**, klikt u op **volgende**.

    ![Voordat u begint met pagina](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Op Hallo **installatietype** pagina, laat u Hallo **op basis van functie of onderdeel gebaseerde installatie** optie ingeschakeld en klik op **volgende**.

    ![Pagina Type installatie](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Op Hallo **serverselectie** pagina, Hallo huidige virtuele machine uit de servergroep Hallo selecteren en op **volgende**.

    ![Pagina voor serverselectie](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Op Hallo **serverfuncties** pagina, klikt u op **volgende**. We overslaan deze pagina omdat we niet alle functies op Hallo server installeert.
9. Op Hallo **functies** pagina, selecteer Hallo **Group Policy Management** functie.

    ![Pagina onderdelen](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. Op Hallo **bevestiging** pagina, klikt u op **installeren** tooinstall Hallo-functie voor Groepsbeleidsbeheer op Hallo virtuele machine. Wanneer de functie-installatie is voltooid, klikt u op **sluiten** tooexit hello **functies en onderdelen toevoegen** wizard.

    ![Bevestigingspagina](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Taak 3 - Launch Hallo Group Policy management console tooadminister Groepsbeleid
U kunt Hallo Group Policy management console op Hallo domein virtuele machine tooadminister Groepsbeleid op Hallo beheerd domein gebruiken.

> [!NOTE]
> U moet lid zijn van Hallo ' AAD DC' beheerdersgroep, tooadminister Groepsbeleid op Hallo beheerd domein toobe.
>
>

1. Vanuit het startscherm hello, klikt u op **Systeembeheer**. U ziet Hallo **Group Policy Management** console is geïnstalleerd op Hallo virtuele machine.

    ![Groepsbeleidsbeheer starten](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Klik op **Group Policy Management** toolaunch Hallo Group Policy Management console.

    ![Group Policy Console](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Taak 4: groepsbeleidsobjecten ingebouwde aanpassen
Er zijn twee ingebouwde groepsbeleidsobjecten (GPO's) - één voor Hallo 'AADDC Computers' en 'AADDC gebruikers' containers in uw beheerde domein. U kunt deze groepsbeleidsobjecten tooconfigure Groepsbeleid op Hallo beheerde domein.

1. In Hallo **Group Policy Management** console, klikt u op tooexpand hello **Forest: contoso100.com** en **domeinen** knooppunten toosee Hallo-Groepsbeleid voor uw beheerde domein.

    ![Ingebouwde GPO 's](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. U kunt deze ingebouwde groepsbeleidsobjecten tooconfigure Groepsbeleid op uw beheerde domein. Met de rechtermuisknop op Hallo groepsbeleidsobject en klik op **bewerken...**  toocustomize Hallo ingebouwde GPO. Hallo configuratie Groepsbeleidsobjecteditor hulpprogramma kunt u toocustomize Hallo GPO.

    ![Ingebouwde GPO bewerken](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. U kunt nu Hallo **Editor voor Groepsbeleidsbeheer** console tooedit Hallo ingebouwde GPO. Bijvoorbeeld ziet Hallo volgende schermafbeelding u hoe toocustomize Hallo ingebouwde AADDC-Computers GPO.

    ![Groepsbeleidsobject aanpassen](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Taak 5: Maak een aangepaste Object GPO (Group Policy)
U kunt maken of importeren van uw eigen aangepaste groepsbeleidsobjecten. U kunt ook aangepaste groepsbeleidsobjecten tooa aangepaste koppelen organisatie-eenheid die u hebt gemaakt in uw beheerde domein. Zie voor meer informatie over het maken van aangepaste organisatie-eenheden [een aangepaste organisatie-eenheid maken op een beheerd domein](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> U moet lid zijn van Hallo ' AAD DC' beheerdersgroep, tooadminister Groepsbeleid op Hallo beheerd domein toobe.
>
>

1. In Hallo **Group Policy Management** console, klikt u op tooselect uw aangepaste organisatie-eenheid (OE). Met de rechtermuisknop op Hallo organisatie-eenheid en klik op **een groepsbeleidsobject in dit domein maken en hier een koppeling...** .

    ![Een aangepaste groepsbeleidsobject maken](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Geef een naam voor het nieuwe groepsbeleidsobject Hallo en klikt u op **OK**.

    ![Geef een naam voor de GPO](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Een nieuw GPO wordt gemaakt en gekoppeld tooyour aangepaste organisatie-eenheid. Met de rechtermuisknop op Hallo groepsbeleidsobject en klik op **bewerken...**  in Hallo-menu.

    ![Een nieuw gemaakt groepsbeleidsobject](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. U kunt aanpassen Hallo nieuw gemaakt groepsbeleidsobject met Hallo **Editor voor Groepsbeleidsbeheer**.

    ![Nieuw groepsbeleidsobject aanpassen](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Meer informatie over het gebruik van [Group Policy Management Console](https://technet.microsoft.com/library/cc753298.aspx) is beschikbaar op Technet.

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Deelnemen aan een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
* [Console Groepsbeleidsbeheer](https://technet.microsoft.com/library/cc753298.aspx)
