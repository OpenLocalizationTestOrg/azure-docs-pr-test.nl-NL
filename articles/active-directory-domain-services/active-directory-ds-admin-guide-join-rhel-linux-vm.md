---
title: 'Azure Active Directory Domain Services: Deelnemen aan een beheerd domein van RHEL VM tooa | Microsoft Docs'
description: Virtuele machine met Red Hat Enterprise Linux toevoegen tooAzure AD Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 87291c47-1280-43f8-8fb2-da1bd61a4942
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 41ca2aaf2eefbf9c403d2b834d61a1aa0943d950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-tooa-managed-domain"></a>Lid worden van een beheerd domein van Red Hat Enterprise Linux 7 virtuele machine tooa
Dit artikel laat zien hoe toojoin een Red Hat Enterprise Linux (RHEL) 7 virtuele machine tooan Azure AD Domain Services beheerd domein.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Een Red Hat Enterprise Linux-machine inrichten
Volgende stappen tooprovision een RHEL 7 virtuele machine met behulp van Azure-portal Hallo Hallo uitvoeren.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

    ![Azure-portaldashboard](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Klik op **nieuw** op Hallo deelvenster en type **Red Hat** in de zoekbalk Hallo zoals weergegeven in de volgende schermafbeelding Hallo. Vermeldingen voor Red Hat Enterprise Linux worden weergegeven in zoekresultaten Hallo. Klik op **Red Hat Enterprise Linux 7.2**.

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. zoekresultaten in Hallo Hallo **Alles** deelvenster Hallo Red Hat Enterprise Linux 7.2 installatiekopie moet aanbieden. Klik op **Red Hat Enterprise Linux 7.2** tooview meer informatie over de installatiekopie van de virtuele machine Hallo.

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. In Hallo **Red Hat Enterprise Linux 7.2** deelvenster ziet u meer informatie over de installatiekopie van de virtuele machine Hallo. In Hallo **een implementatiemodel selecteren** vervolgkeuzelijst, selecteer **klassieke**. Klik vervolgens op Hallo **maken** knop.

    ![Details van de afbeelding weergeven](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. In Hallo **basisbeginselen** pagina Hallo **virtuele machine maken** wizard Voer Hallo **hostnaam** voor Hallo nieuwe virtuele machine. Ook de gebruikersnaam van een lokale beheerder opgeven in Hallo **gebruikersnaam** veld en een **wachtwoord**. U kunt desgewenst ook toouse gebruiker SSH sleutel tooauthenticate Hallo lokale beheerder. Selecteert u ook een **prijscategorie** voor Hallo virtuele machine.

    ![VM - basisbeginselen pagina maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. In Hallo **grootte** pagina Hallo **virtuele machine maken** grootte van de wizard, selecteer Hallo voor Hallo virtuele machine.

    ![Maken van VM - grootte selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. In Hallo **instellingen** pagina Hallo **virtuele machine maken** wizard, selecteer Hallo storage-account voor Hallo virtuele machine. Klik op **virtueel netwerk** tooselect Hallo virtueel netwerk toowhich Hallo Linux VM moeten worden geïmplementeerd. In Hallo **virtueel netwerk** blade, selecteer Hallo virtueel netwerk waarin Azure AD Domain Services beschikbaar is. In dit voorbeeld kiest u Hallo 'MyPreviewVNet' virtueel netwerk.

    ![Maken van VM - virtuele netwerk selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Op Hallo **samenvatting** pagina Hallo **virtuele machine maken** wizard controleren en op Hallo **OK** knop.

    ![Maken van VM - virtuele netwerk zijn geselecteerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Implementatie van Hallo nieuwe virtuele machine op basis van Hallo RHEL 7.2 afbeelding moet worden gestart.

    ![Maken van VM - implementatie is gestart](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Na een paar minuten moet Hallo virtuele machine is geïmplementeerd en klaar voor gebruik.

    ![Maken van VM - geïmplementeerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-toohello-newly-provisioned-linux-virtual-machine"></a>Extern verbinding maken met toohello nieuw ingerichte virtuele Linux-machine
Hallo RHEL 7.2 virtuele machine is ingericht in Azure. de volgende taak Hallo tooconnect op afstand is toohello virtuele machine.

**Verbinding maken met toohello RHEL 7.2 virtuele machine** Hallo-instructies in Hallo artikel [hoe toolog op tooa virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hallo rest Hallo stappen wordt ervan uitgegaan dat u Hallo PuTTY SSH client tooconnect toohello RHEL virtuele machine gebruiken. Zie voor meer informatie, Hallo [PuTTY-downloadpagina](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Open Hallo PuTTY programma.
2. Voer Hallo **hostnaam** voor Hallo RHEL virtuele machine van een nieuw gemaakt. In dit voorbeeld is de virtuele machine Hallo host-naam 'contoso-rhel.cloudapp .net'. Als u de hostnaam Hallo van uw virtuele machine niet weet, raadpleegt u toohello VM dashboard op Hallo Azure-portal.

    ![PuTTY verbinding maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Meld u aan toohello virtuele machine met lokale beheerdersreferenties Hallo die u hebt opgegeven bij Hallo virtuele machine is gemaakt. In dit voorbeeld hebben we Hallo lokale administrator-account 'mahesh' gebruikt.

    ![PuTTY-aanmelding](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-hello-linux-virtual-machine"></a>Installeert de vereiste pakketten op Hallo Linux virtuele machine
Na het maken van verbinding toohello virtuele machine is de volgende taak Hallo tooinstall pakketten die zijn vereist voor domeinlidmaatschap op Hallo virtuele machine. Voer Hallo stappen te volgen:

1. **Installeer realmd:** hello realmd pakket wordt gebruikt voor het domein. Typ in de PuTTY terminal Hallo volgende opdracht:

    sudo yum installeren realmd

    ![Realmd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Na een paar minuten moet Hallo realmd pakket ophalen geïnstalleerd op Hallo virtuele machine.

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Installeer sssd:** hello realmd pakket, is afhankelijk van sssd tooperform domain join-bewerkingen. Typ in de PuTTY terminal Hallo volgende opdracht:

    sudo yum installeren sssd

    ![Sssd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Na een paar minuten moet Hallo sssd pakket ophalen geïnstalleerd op Hallo virtuele machine.

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Kerberos installeren:** Typ In de PuTTY terminal Hallo volgende opdracht:

    sudo yum installeren krb5 werkstation krb5-bibliotheken

    ![Kerberos installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Na een paar minuten moet Hallo realmd pakket ophalen geïnstalleerd op Hallo virtuele machine.

    ![Kerberos is geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-hello-linux-virtual-machine-toohello-managed-domain"></a>Hallo Linux virtuele machine toohello beheerd domein koppelen
Nu vereist hello-pakketten op Hallo virtuele Linux-machine zijn geïnstalleerd, de volgende taak Hallo is toojoin Hallo virtuele machine toohello beheerd domein.

1. Hallo AAD Domain Services beheerd domein detecteren. Typ in de PuTTY terminal Hallo volgende opdracht:

    sudo realm CONTOSO100.COM detecteren

    ![Realm detecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Als **realm detecteren** niet kan toofind is uw beheerde domein, zorg ervoor dat domein Hallo bereikbaar is vanaf Hallo virtuele machine (probeer ping). Zorg er ook voor dat de virtuele machine Hallo geïmplementeerde toohello inderdaad is hetzelfde virtuele netwerk in welke Hallo beheerde domein beschikbaar is.
2. Initialiseren van kerberos. Typ in de PuTTY terminal Hallo opdracht te volgen. Zorg ervoor dat u opgeeft dat een gebruiker die lid is van toohello ' AAD DC' beheerdersgroep. Alleen deze gebruikers kunnen computers toohello beheerd domein toevoegen.

    kinitbob@CONTOSO100.COM

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Zorg dat u Hallo-domeinnaam opgeven in hoofdletters, anders kinit is mislukt.
3. Lid worden Hallo machine toohello domein. Typ in de PuTTY terminal Hallo opdracht te volgen. Geef Hallo dezelfde gebruiker die u hebt opgegeven in de voorgaande stap (kinit) Hallo.

    sudo realm join--uitgebreide CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Realm join](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

U krijgt een bericht ('is ingeschreven machine in de realm') als Hallo machine neemt deel toohello beheerd domein is.

## <a name="verify-domain-join"></a>Controleer of aan domein toevoegen
U kunt snel te controleren of Hallo machine neemt deel toohello beheerd domein is. Verbinding maken met toohello nieuw domein RHEL VM die gebruikmaakt van SSH en een domeingebruikersaccount en vervolgens selectievakje toosee als gebruikersaccount Hallo correct is opgelost.

1. In uw terminal PuTTY type Hallo na opdracht tooconnect toohello nieuw domein RHEL virtuele machine via SSH. Een domeinaccount die deel uitmaakt van het beheerde domein toohello gebruiken (bijvoorbeeld 'bob@CONTOSO100.COM' in dit geval.)

    SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net
2. Typ in de PuTTY terminal Hallo opdracht toosee volgen als basismap Hallo correct is geïnitialiseerd.

    pwd
3. Typ in de PuTTY terminal Hallo opdracht toosee volgen als Hallo groepslidmaatschappen correct worden herleid.

    id

Hier volgt een voorbeeld van uitvoer van deze opdrachten:

![Controleer of aan domein toevoegen](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Het oplossen van problemen aan domein toevoegen
Raadpleeg toohello [probleemoplossing domein](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artikel.

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Deelnemen aan een Windows Server virtuele machine tooan Azure AD Domain Services beheerd domein](active-directory-ds-admin-guide-join-windows-vm.md)
* [Hoe toolog op tooa virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Kerberos installeren](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - handleiding voor Windows-integratie](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
