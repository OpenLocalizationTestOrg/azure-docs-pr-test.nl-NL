---
title: 'Azure Active Directory Domain Services: Een RHEL VM toevoegen aan een beheerd domein | Microsoft Docs'
description: Red Hat Enterprise Linux virtuele machine toevoegen aan Azure AD Domain Services
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
ms.openlocfilehash: 69f1850bfed90392e9a4695e2443ffaa6bfc746d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-red-hat-enterprise-linux-7-virtual-machine-to-a-managed-domain"></a>Een virtuele Red Hat Enterprise Linux 7-machine toevoegen aan een beheerd domein
In dit artikel laat zien hoe een virtuele machine met Red Hat Enterprise Linux (RHEL) 7 toevoegen aan een beheerd domein van Azure AD Domain Services.

## <a name="provision-a-red-hat-enterprise-linux-virtual-machine"></a>Een Red Hat Enterprise Linux-machine inrichten
Voer de volgende stappen uit voor het inrichten van een RHEL 7 virtuele machine met de Azure portal.

1. Meld u aan bij [Azure Portal](https://portal.azure.com).

    ![Azure-portaldashboard](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-dashboard.png)
2. Klik op **nieuw** in het linkerdeelvenster en typ **Red Hat** in de zoekbalk, zoals wordt weergegeven in de volgende schermafbeelding. Vermeldingen voor Red Hat Enterprise Linux worden weergegeven in de zoekresultaten. Klik op **Red Hat Enterprise Linux 7.2**.

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-find-rhel-image.png)
3. De zoekresultaten de **Alles** deelvenster moet de installatiekopie van het Red Hat Enterprise Linux 7.2 lijst. Klik op **Red Hat Enterprise Linux 7.2** voor meer informatie over de installatiekopie van de virtuele machine.

    ![Selecteer RHEL in resultaten](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-rhel-image.png)
4. In de **Red Hat Enterprise Linux 7.2** deelvenster ziet u meer informatie over de installatiekopie van de virtuele machine. In de **een implementatiemodel selecteren** vervolgkeuzelijst, selecteer **klassieke**. Klik vervolgens op de **maken** knop.

    ![Details van de afbeelding weergeven](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-clicked.png)
5. In de **basisbeginselen** pagina van de **virtuele machine maken** wizard voert de **hostnaam** voor de nieuwe virtuele machine. Geef ook de gebruikersnaam van een lokale beheerder in de **gebruikersnaam** veld en een **wachtwoord**. U kunt ook een SSH-sleutel gebruiken om te verifiëren van de lokale beheerder-gebruiker. Selecteert u ook een **prijscategorie** voor de virtuele machine.

    ![VM - basisbeginselen pagina maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-basic-details.png)
6. In de **grootte** pagina van de **virtuele machine maken** wizard, selecteer de grootte voor de virtuele machine.

    ![Maken van VM - grootte selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-select-vm-size.png)

7. In de **instellingen** pagina van de **virtuele machine maken** wizard selecteert u de storage-account voor de virtuele machine. Klik op **virtueel netwerk** selecteren van het virtuele netwerk waartoe de Linux-VM moeten worden geïmplementeerd. In de **virtueel netwerk** blade, selecteer het virtuele netwerk in welke Azure AD Domain Services beschikbaar is. In dit voorbeeld kiest u het virtuele netwerk 'MyPreviewVNet'.

    ![Maken van VM - virtuele netwerk selecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-select-vnet.png)
8. Op de **samenvatting** pagina van de **virtuele machine maken** wizard controleren en op de **OK** knop.

    ![Maken van VM - virtuele netwerk zijn geselecteerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-vnet-selected.png)
9. Implementatie van de nieuwe virtuele machine op basis van de installatiekopie van het RHEL 7.2 moet worden gestart.

    ![Maken van VM - implementatie is gestart](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployment-started.png)
10. Na een paar minuten, moeten de virtuele machine worden geïmplementeerd met succes en klaar voor gebruik.

    ![Maken van VM - geïmplementeerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-create-vm-deployed.png)

## <a name="connect-remotely-to-the-newly-provisioned-linux-virtual-machine"></a>Extern verbinding maken met de nieuw ingerichte virtuele Linux-machine
De RHEL 7.2 virtuele machine is ingericht in Azure. De volgende taak is het op afstand verbinding maken met de virtuele machine.

**Verbinding maken met de virtuele machine van RHEL 7.2** Volg de instructies in het artikel [aanmelden met een virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

De rest van de stappen wordt ervan uitgegaan dat u de PuTTY SSH-client verbinding maken met de RHEL virtuele machine gebruiken. Zie voor meer informatie de [PuTTY-downloadpagina](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

1. Open het PuTTY programma.
2. Voer de **hostnaam** voor de zojuist gemaakte RHEL virtuele machine. In dit voorbeeld is de virtuele machine de host-naam 'contoso-rhel.cloudapp .net'. Als u de hostnaam van uw virtuele machine niet weet, raadpleegt u het VM-dashboard in de Azure portal.

    ![PuTTY verbinding maken](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-connect.png)
3. Meld u bij de virtuele machine met de lokale administrator-referenties die u hebt opgegeven toen de virtuele machine is gemaakt. In dit voorbeeld hebben we het lokale administrator-account 'mahesh' gebruikt.

    ![PuTTY-aanmelding](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-login.png)

## <a name="install-required-packages-on-the-linux-virtual-machine"></a>Installeert de vereiste pakketten op de virtuele Linux-machine
Nadat u verbinding maakt met de virtuele machine, is de volgende taak voor het installeren van pakketten die zijn vereist voor domeinlidmaatschap op de virtuele machine. De volgende stappen uitvoeren:

1. **Installeer realmd:** het pakket realmd wordt gebruikt voor het domein. Typ de volgende opdracht in de PuTTY terminal:

    sudo yum installeren realmd

    ![Realmd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-realmd.png)

    Na een paar minuten moet het pakket realmd geïnstalleerd op de virtuele machine.

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-installed.png)
2. **Installeer sssd:** het pakket realmd is afhankelijk van sssd domain join-bewerkingen uit te voeren. Typ de volgende opdracht in de PuTTY terminal:

    sudo yum installeren sssd

    ![Sssd installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-sssd.png)

    Na een paar minuten moet het pakket sssd geïnstalleerd op de virtuele machine.

    ![realmd geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-sssd-installed.png)
3. **Kerberos installeren:** In uw terminal PuTTY, typ de volgende opdracht:

    sudo yum installeren krb5 werkstation krb5-bibliotheken

    ![Kerberos installeren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-install-kerberos.png)

    Na een paar minuten moet het pakket realmd geïnstalleerd op de virtuele machine.

    ![Kerberos is geïnstalleerd](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kerberos-installed.png)

## <a name="join-the-linux-virtual-machine-to-the-managed-domain"></a>De virtuele Linux-machine toevoegen aan het beheerde domein
Nu de vereiste pakketten zijn geïnstalleerd op de virtuele Linux-machine, de volgende taak is de virtuele machine toevoegen aan het beheerde domein.

1. Ontdek het beheerde domein met AAD Domain Services. Typ de volgende opdracht in de PuTTY terminal:

    sudo realm CONTOSO100.COM detecteren

    ![Realm detecteren](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-discover.png)

    Als **realm detecteren** kan niet zoeken naar uw beheerde domein, zorg ervoor dat het domein van de virtuele machine (probeer ping) bereikbaar is. Zorg er ook voor dat de virtuele machine inderdaad is geïmplementeerd voor hetzelfde virtuele netwerk waarin het beheerde domein beschikbaar is.
2. Initialiseren van kerberos. Typ de volgende opdracht in de PuTTY terminal. Zorg ervoor dat u een gebruiker die lid is van de groep 'AAD DC Administrators' opgeven. Alleen deze gebruikers kunnen computers toevoegen aan het beheerde domein.

    kinitbob@CONTOSO100.COM

    ![Kinit](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-kinit.png)

    Zorg dat u de domeinnaam in hoofdletters opgeven, anders kinit is mislukt.
3. De machine toevoegen aan het domein. Typ de volgende opdracht in de PuTTY terminal. Geef dezelfde gebruiker die u hebt opgegeven in de vorige stap (kinit).

    sudo realm join--uitgebreide CONTOSO100.COM -U 'bob@CONTOSO100.COM'

    ![Realm join](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-realmd-join.png)

U krijgt een bericht ('is ingeschreven machine in de realm') wanneer de computer met succes is toegevoegd aan het beheerde domein.

## <a name="verify-domain-join"></a>Controleer of aan domein toevoegen
U kunt snel te controleren of de machine is toegevoegd aan het beheerde domein. Verbinding maken met het nieuwe domein RHEL VM die gebruikmaakt van SSH en een domeingebruikersaccount en controleer om te zien of het gebruikersaccount correct is opgelost.

1. In de PuTTY terminal, typ de volgende opdracht verbinding maken met het nieuwe domein RHEL virtuele machine via SSH. Gebruik een domeinaccount die deel uitmaakt van het beheerde domein (bijvoorbeeld 'bob@CONTOSO100.COM' in dit geval.)

    SSH -l bob@CONTOSO100.COM contoso rhel.cloudapp.net
2. Typ de volgende opdracht om te zien of de basismap correct is geïnitialiseerd in de PuTTY terminal.

    pwd
3. Typ de volgende opdracht om te zien als het groepslidmaatschap correct wordt opgelost in de PuTTY terminal.

    id

Hier volgt een voorbeeld van uitvoer van deze opdrachten:

![Controleer of aan domein toevoegen](./media/active-directory-domain-services-admin-guide/rhel-join-azure-portal-putty-verify-domain-join.png)

## <a name="troubleshooting-domain-join"></a>Het oplossen van problemen aan domein toevoegen
Raadpleeg de [probleemoplossing domein](active-directory-ds-admin-guide-join-windows-vm.md#troubleshooting-domain-join) artikel.

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Virtuele machine met Windows Server toevoegen aan een beheerd domein van Azure AD Domain Services](active-directory-ds-admin-guide-join-windows-vm.md)
* [Aanmelden met een virtuele machine met Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* [Kerberos installeren](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Smart_Cards/installing-kerberos.html)
* [Red Hat Enterprise Linux 7 - handleiding voor Windows-integratie](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Windows_Integration_Guide/index.html)
