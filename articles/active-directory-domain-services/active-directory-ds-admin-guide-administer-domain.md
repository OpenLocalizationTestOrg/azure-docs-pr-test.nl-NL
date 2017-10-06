---
title: 'Azure Active Directory Domain Services: Een beheerd domein beheren | Microsoft Docs'
description: Azure Active Directory Domain Services beheerde domeinen beheren
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4fdbc75-3e6b-4e20-8494-5dcc3bf2220a
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 11acc79e06163e3193b1aa981f2cd28af812789d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="administer-an-azure-active-directory-domain-services-managed-domain"></a>Een beheerd domein van Azure AD Domain Services beheren
Dit artikel laat zien hoe tooadminister een Azure Active Directory (AD) Domain Services beheerd domein.

## <a name="before-you-begin"></a>Voordat u begint
tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:

1. Een geldige **Azure-abonnement**.
2. Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.
3. **Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory. Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).
4. Een **domein virtuele machine** hello Azure AD Domain Services beheerd domein uit die u beheert. Als u dergelijke een virtuele machine geen hebt, volgt u alle Hallo taken die worden beschreven in artikel Hallo [lid worden van een beheerd domein voor Windows virtuele machine tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. U moet referenties op Hallo van een **account behoren toohello 'AAD DC-beheerders' gebruikersgroep** in uw directory tooadminister uw beheerde domein.

<br>

## <a name="administrative-tasks-you-can-perform-on-a-managed-domain"></a>Administratieve taken die u op een beheerd domein uitvoeren kunt
Leden van Hallo ' AAD DC' beheerdersgroep krijgen bevoegdheden op Hallo beheerd domein waarmee ze tooperform taken, zoals:

* Lid worden machines toohello beheerde domein.
* Hallo ingebouwde GPO voor Hallo 'AADDC Computers' en 'AADDC gebruikers' containers in Hallo beheerd domein configureren.
* DNS op Hallo beheerd domein beheren.
* Maken en beheren van aangepaste organisatie-eenheden (OE's) op Hallo beheerde domein.
* Voordeel beheerderstoegang toocomputers deel toohello beheerde domein.

## <a name="administrative-privileges-you-do-not-have-on-a-managed-domain"></a>U niet op een beheerd domein hebt beheerdersbevoegdheden
Hallo domein wordt beheerd door Microsoft, met inbegrip van activiteiten zoals patchen, bewaking en, back-ups maken. Daarom Hallo domein is vergrendeld en u hebt geen rechten tooperform bepaalde beheertaken op Hallo-domein. Er zijn enkele voorbeelden van taken die u niet kunt uitvoeren onder.

* U domeinbeheerder of ondernemingsbeheerder bevoegdheden voor Hallo beheerde domein niet krijgen.
* U kunt Hallo-schema van het beheerde domein Hallo niet uitbreiden.
* U kunt toodomain controllers voor Hallo beheerde domein maken met extern bureaublad geen verbinding maken.
* U kunt geen domain controllers toohello beheerd domein toevoegen.

## <a name="task-1---provision-a-domain-joined-windows-server-virtual-machine-tooremotely-administer-hello-managed-domain"></a>Taak 1 - inrichten van een domein Windows Server virtuele machine tooremotely Hallo beheerd domein beheren
Azure AD Domain Services beheerde domeinen kunnen worden beheerd met vertrouwd Active Directory-beheerprogramma's zoals Hallo Active Directory-beheercentrum (ADAC) of AD PowerShell. Tenantbeheerders hebt geen rechten tooconnect toodomain controllers op Hallo beheerd domein via Extern bureaublad. Leden van Hallo ' AAD DC' beheerdersgroep kunt beheren beheerd daarom domeinen op afstand met AD-beheerprogramma's vanaf een Windows-Server /-client-computer die is gekoppeld toohello beheerd domein. AD-beheerprogramma's kunnen worden geïnstalleerd als onderdeel van Hallo Remote Server Administration Tools (RSAT) optioneel onderdeel op Windows Server en client-computers die lid zijn van toohello beheerd domein.

de eerste stap Hallo is tooset een virtuele machine van Windows Server die is gekoppeld toohello beheerd domein. Voor instructies raadpleegt u artikel toohello [lid worden van een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md).

### <a name="remotely-administer-hello-managed-domain-from-a-client-computer-for-example-windows-10"></a>Hallo beheerd domein op afstand te beheren vanaf een clientcomputer (bijvoorbeeld Windows 10)
Hallo-instructies in dit artikel gebruik een Windows Server virtuele machine tooadminister Hallo AAD-DS beheerd domein. Echter, u kunt ook toouse een Windows-client (bijvoorbeeld Windows 10) virtuele machine toodo dus.

U kunt [Remote Server Administration Tools (RSAT) installeren](http://social.technet.microsoft.com/wiki/contents/articles/2202.remote-server-administration-tools-rsat-for-windows-client-and-windows-server-dsforum2wiki.aspx) op een Windows-client virtuele machine door Hallo instructies te volgen op TechNet.

## <a name="task-2---install-active-directory-administration-tools-on-hello-virtual-machine"></a>Taak 2 - Install Active Directory-beheerprogramma's op Hallo virtuele machine
Hallo stappen tooinstall Hallo Active Directory-beheerprogramma's te volgen op Hallo verbonden met het domein virtuele machine uitvoeren. Zie Technet voor meer [informatie over het installeren en gebruiken van Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx).

1. Navigeer te**virtuele Machines** knooppunt in Hallo klassieke Azure-portal. Selecteer Hallo virtuele machine die u in taak 1 hebt gemaakt en klik op **Connect** op de opdrachtbalk Hallo HALLO hallo venster onderaan in.

    ![Verbinding maken met tooWindows virtuele machine](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. klassieke portal Hallo tooopen wordt u gevraagd of een bestand met de extensie '.rdp' opslaan die gebruikte tooconnect toohello virtuele machine is. Klik op tooopen Hallo bestand wanneer het downloaden is voltooid.
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
9. Op Hallo **functies** pagina, klikt u op tooexpand hello **Remote Server Administration Tools** knooppunt en klik vervolgens op tooexpand hello **functiebeheer** knooppunt. Selecteer **AD DS en AD LDS-hulpprogramma** functie uit de lijst Hallo met beheerprogramma's voor rollen.

    ![Pagina onderdelen](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-ad-tools.png)
10. Op Hallo **bevestiging** pagina, klikt u op **installeren** tooinstall hello AD- en AD LDS-hulpprogramma's voor de functie op Hallo virtuele machine. Wanneer de functie-installatie is voltooid, klikt u op **sluiten** tooexit hello **functies en onderdelen toevoegen** wizard.

    ![Bevestigingspagina](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-confirmation.png)

## <a name="task-3---connect-tooand-explore-hello-managed-domain"></a>Taak 3: verbinding maken met tooand verkennen Hallo beheerd domein
Nu Hallo AD beheerprogramma's zijn geïnstalleerd op Hallo domein virtuele machine, we kunnen deze hulpprogramma's voor tooexplore gebruiken en Hallo beheerd domein beheren.

> [!NOTE]
> U moet toobe lid van Hallo ' AAD DC' beheerdersgroep tooadminister Hallo beheerd domein.
>
>

1. Vanuit het startscherm hello, klikt u op **Systeembeheer**. U ziet Systeembeheer Hallo AD op Hallo virtuele machine geïnstalleerd.

    ![Beheerprogramma's geïnstalleerd op server](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Klik op **Active Directory-beheercentrum**.

    ![Active Directory-beheercentrum](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. tooexplore hello domein, klikt u op Hallo-domeinnaam in het linkerdeelvenster hello (bijvoorbeeld, contoso100.com'). U ziet twee containers respectievelijk 'AADDC Computers' en 'AADDC gebruikers' genoemd.

    ![Active Directory-Beheercentrum - domein weergeven](./media/active-directory-domain-services-admin-guide/adac-domain-view.png)
4. Klik op Hallo zogenaamd **AADDC gebruikers** toosee alle gebruikers en groepen die behoren toohello beheerd domein. Ziet u gebruikersaccounts en groepen in uw Azure AD tenant weergeven om in deze container. In dit voorbeeld ziet, een gebruikersaccount voor Hallo gebruiker met de naam "bob" en een groep genaamd 'AAD DC-beheerders' zijn beschikbaar in deze container.

    ![Active Directory-Beheercentrum - domeingebruikers](./media/active-directory-domain-services-admin-guide/adac-aaddc-users.png)
5. Klik op Hallo zogenaamd **AADDC Computers** toosee Hallo computers die lid zijn van toothis beheerd domein. Hier ziet u een vermelding voor Hallo huidige virtuele machine, die gekoppeld toohello domein is. Computeraccounts voor alle computers die lid zijn van toohello Azure AD Domain Services beheerd domein worden opgeslagen in deze container AADDC-Computers.

    ![Active Directory-Beheercentrum - computers die lid van domein](./media/active-directory-domain-services-admin-guide/adac-aaddc-computers.png)

<br>

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Deelnemen aan een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md)
* [Remote Server Administration Tools implementeren](https://technet.microsoft.com/library/hh831501.aspx)
