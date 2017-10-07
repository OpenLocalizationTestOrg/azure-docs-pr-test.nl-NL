---
title: 'Azure Active Directory Domain Services: DNS op de beheerde domeinen beheren | Microsoft Docs'
description: DNS op Azure Active Directory Domain Services beheerde domeinen beheren
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
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>DNS op een beheerd domein van Azure AD Domain Services beheren
Azure Active Directory Domain Services bevat een DNS (Domain Name Resolution)-server waarmee u DNS-omzetting Hallo beheerd domein. In sommige gevallen moet u mogelijk tooconfigure DNS op Hallo beheerd domein. U moet mogelijk toocreate DNS-records voor de machines die geen lid toohello domein, virtuele IP-adressen voor load balancers te configureren of instellen van externe DNS-doorstuurservers. Om deze reden krijgen gebruikers die deel uitmaken van toohello ' AAD DC' beheerdersgroep DNS-beheer-machtigingen op Hallo beheerd domein.

## <a name="before-you-begin"></a>Voordat u begint
tooperform hello taken die in dit artikel worden vermeld, hebt u nodig:

1. Een geldige **Azure-abonnement**.
2. Een **Azure AD-directory** -ofwel gesynchroniseerd met een on-premises adreslijst of een map alleen in de cloud.
3. **Azure AD Domain Services** moet zijn ingeschakeld voor hello Azure AD-directory. Als u dit nog niet hebt gedaan, volgt u alle Hallo taken die worden beschreven in Hallo [handleiding](active-directory-ds-getting-started.md).
4. Een **domein virtuele machine** hello Azure AD Domain Services beheerd domein uit die u beheert. Als u dergelijke een virtuele machine geen hebt, volgt u alle Hallo taken die worden beschreven in artikel Hallo [lid worden van een beheerd domein voor Windows virtuele machine tooa](active-directory-ds-admin-guide-join-windows-vm.md).
5. U moet referenties op Hallo van een **account behoren toohello 'AAD DC-beheerders' gebruikersgroep** in uw directory tooadminister DNS voor uw beheerde domein.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Taak 1 - inrichten van een virtuele machine domein tooremotely DNS voor Hallo beheerd domein beheren
Azure AD Domain Services beheerde domeinen kunnen worden beheerd op afstand met vertrouwd Active Directory-beheerprogramma's zoals Hallo Active Directory-beheercentrum (ADAC) of AD PowerShell. DNS voor het beheerde domein Hallo kan op dezelfde manier worden beheerd op afstand met Hallo DNS-Server administration tools.

Beheerders in uw Azure AD-directory hebt geen rechten tooconnect toodomain controllers op Hallo beheerd domein via Extern bureaublad. Leden van Hallo ' AAD DC' beheerdersgroep beheren DNS voor de beheerde domeinen extern met hulpprogramma's voor DNS-Server vanaf een Windows-Server /-client-computer die is gekoppeld toohello beheerd domein. Hulpprogramma's voor DNS-Server kunnen worden geïnstalleerd als onderdeel van Hallo Remote Server Administration Tools (RSAT) optioneel onderdeel op Windows Server en client-computers die lid zijn van toohello beheerd domein.

de eerste taak Hallo is tooprovision een virtuele machine van Windows Server die is gekoppeld toohello beheerd domein. Voor instructies raadpleegt u artikel toohello [lid worden van een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Taak 2 - hulpprogramma's installeren DNS-Server op Hallo virtuele machine
Hallo stappen tooinstall Hallo DNS-beheerprogramma's te volgen op Hallo verbonden met het domein virtuele machine uitvoeren. Voor meer informatie over [installeren en gebruiken van Remote Server Administration Tools](https://technet.microsoft.com/library/hh831501.aspx), Zie Technet.

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
9. Op Hallo **functies** pagina, klikt u op tooexpand hello **Remote Server Administration Tools** knooppunt en klik vervolgens op tooexpand hello **functiebeheer** knooppunt. Selecteer **DNS-Server-hulpprogramma's** functie uit de lijst Hallo met beheerprogramma's voor rollen.

    ![Pagina onderdelen](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. Op Hallo **bevestiging** pagina, klikt u op **installeren** tooinstall Hallo DNS-Server-hulpprogramma's voor de functie op Hallo virtuele machine. Wanneer de functie-installatie is voltooid, klikt u op **sluiten** tooexit hello **functies en onderdelen toevoegen** wizard.

    ![Bevestigingspagina](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Taak 3 - Launch Hallo DNS management console tooadminister DNS
Nu Hallo DNS-Server Tools functie is geïnstalleerd op hello verbonden met het domein virtuele machine, kunnen we Hallo DNS-hulpprogramma's voor tooadminister DNS gebruiken op Hallo beheerd domein.

> [!NOTE]
> U moet lid zijn van Hallo ' AAD DC' beheerdersgroep, tooadminister DNS op Hallo beheerd domein toobe.
>
>

1. Vanuit het startscherm hello, klikt u op **Systeembeheer**. U ziet Hallo **DNS** console is geïnstalleerd op Hallo virtuele machine.

    ![Systeembeheer - DNS-Console](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Klik op **DNS** toolaunch Hallo DNS-beheerconsole.
3. In Hallo **tooDNS Server verbinding** dialoogvenster, klikt u op Hallo optie met de titel **Hallo na computer**, en Voer Hallo DNS-domeinnaam van Hallo beheerd domein (bijvoorbeeld, contoso100.com').

    ![DNS-Console - verbinding toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Hallo DNS-Console verbindt toohello beheerd domein.

    ![De Console DNS - domein beheren](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. U kunt nu Hallo DNS-console tooadd DNS-vermeldingen voor computers in Hallo virtuele netwerk waarin u AAD Domain Services hebt ingeschakeld.

> [!WARNING]
> Wees voorzichtig wanneer DNS beheren voor Hallo beheerd met behulp van beheerhulpprogramma's voor DNS-domein. Zorg ervoor dat u **niet verwijderen of wijzigen van het ingebouwde DNS-records hello, die worden gebruikt door Domain Services in Hallo domein**. Ingebouwde DNS-records zijn domein-DNS-records, naamserverrecords en andere records gebruikt voor de locatie van de domeincontroller. Als u deze records wijzigt, worden de domeinservices verstoord op Hallo virtueel netwerk.
>
>

Zie Hallo [DNS-hulpprogramma's op Technet artikel](https://technet.microsoft.com/library/cc753579.aspx) voor meer informatie over het beheren van DNS.

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Deelnemen aan een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
* [DNS-beheerprogramma 's](https://technet.microsoft.com/library/cc753579.aspx)
