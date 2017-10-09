---
title: 'Azure Active Directory Domain Services: Deelnemen aan een beheerd domein van Windows Server-VM tooa | Microsoft Docs'
description: Windows Server een virtuele machine toevoegen tooAzure AD Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Lid worden van een beheerd domein voor Windows Server virtuele machine tooa
> [!div class="op_single_selector"]
> * [Klassieke Azure-portal - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

Dit artikel laat zien hoe toojoin een virtuele machine met Windows Server 2012 R2 tooan Azure AD Domain Services beheerd domein, met Hallo klassieke Azure-portal.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Stap 1: Hallo Windows Server-virtuele machine maken
Hallo instructies die worden beschreven in Hallo [maken van een virtuele machine waarop Windows wordt uitgevoerd in de klassieke Azure-portal Hallo](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) zelfstudie. Het is belangrijk tooensure die deze nieuwe virtuele machine is gekoppeld toohello hetzelfde virtuele netwerk waarin u Azure AD Domain Services hebt ingeschakeld. Hallo snelle invoer optie schakelt u toojoin hello tooa virtueel netwerk voor virtuele machines niet. Daarom moet u toouse Hallo uit galerie optie toocreate Hallo virtuele machine.

Voer Hallo volgende stappen toocreate een Windows virtuele machine gekoppelde toohello virtueel netwerk waarin u Azure AD Domain Services hebt ingeschakeld.

1. Klik in de klassieke Azure-portal op de opdrachtbalk Hallo HALLO hallo venster onderaan in Hallo op **nieuw**.
2. Onder **Compute**, klikt u op **virtuele Machine**, klikt u vervolgens op **uit galerie**.
3. Hallo eerste scherm kunt u **een afbeelding kiezen die** voor uw virtuele machine uit Hallo lijst met beschikbare installatiekopieën. Kies de juiste installatiekopie Hallo.

    ![Selecteer de installatiekopie](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. tweede welkomstscherm kunt u een computernaam, de grootte, en de naam van de gebruiker met beheerdersrechten en het wachtwoord kiezen. Uw app of de werkbelasting Hallo-laag en de vereiste grootte toorun gebruiken. Hallo-gebruikersnaam die u hier kiest, is een lokale beheerder op Hallo machine. Geef geen referenties voor een domeingebruikersaccount hier.

    ![Virtuele machine configureren](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. Hallo derde scherm kunt u resources voor netwerken, opslag en beschikbaarheid te configureren. Zorg ervoor dat u selecteert Hallo virtueel netwerk waarin u Azure AD Domain Services van Hallo ingeschakeld **regio/affiniteit groep/virtueel netwerk** vervolgkeuzelijst. Geef een **Cloud Service DNS-naam** afhankelijk van wat geschikt is voor Hallo virtuele machine.

    ![Virtueel netwerk voor virtuele machine selecteren](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Zorg ervoor dat u deelnemen aan de virtuele machine-toohello Hallo hetzelfde virtuele netwerk waarin u Azure AD Domain Services hebt ingeschakeld. Als gevolg hiervan Hallo virtuele machine 'Zie' Hallo-domein en taken uitvoeren, zoals lidmaatschap van domein Hallo. U kunt eventueel toocreate Hallo virtuele machine in een ander virtueel netwerk verbinding maken met dit virtuele netwerk toohello virtuele netwerk waarin u Azure AD Domain Services hebt ingeschakeld.
   >
   >
6. Hallo vierde scherm kunt u Hallo VM-Agent installeren en configureren van enkele van de beschikbare uitbreidingen Hallo.

    ![Klaar](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Nadat Hallo virtuele machine is gemaakt, Hallo klassieke portal een lijst met nieuwe virtuele machine onder Hallo Hallo **virtuele Machines** knooppunt. Zowel Hallo virtuele machine en cloudservice automatisch gestart en hun status wordt vermeld als **met**.

    ![Virtuele machine is actief](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Stap 2: Verbinding maken met toohello Windows Server virtuele machine met Hallo lokale administrator-account
Nu we verbinding maken met toohello nieuwe Windows Server virtuele machine, toojoin het toohello domein. Hallo lokale beheerdersreferenties die hebt opgegeven toen u Hallo virtuele machine, tooconnect tooit gebruiken.

Hallo te volgen stappen tooconnect toohello virtuele machine uitvoeren.

1. Navigeer te**virtuele Machines** knooppunt in de klassieke portal Hallo. Selecteer Hallo virtuele machine die u in stap 1 hebt gemaakt en klik op **Connect** op de opdrachtbalk Hallo HALLO hallo venster onderaan in.

    ![Verbinding maken met tooWindows virtuele machine](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. klassieke portal Hallo tooopen wordt u gevraagd of een bestand met de extensie '.rdp' opslaan die gebruikte tooconnect toohello virtuele machine is. Klik op tooopen Hallo bestand wanneer het downloaden is voltooid.
3. Hallo aanmeldprompt weergegeven, Voer uw **lokale beheerdersreferenties**, die u hebt opgegeven tijdens het maken van Hallo virtuele machine. Bijvoorbeeld, hebben we 'localhost\mahesh' in dit voorbeeld gebruikt.

Op dit moment moet u zijn aangemeld in toohello nieuw gemaakte virtuele Windows-computer met lokale Administrator-referenties. de volgende stap Hallo is toojoin Hallo virtuele machine toohello domein.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Stap 3: Lid worden van beheerde toohello AAD-DS-domein van de Hallo Windows Server-virtuele machine
Hallo te volgen stappen toojoin Hallo Windows Server virtuele machine toohello AAD-DS beheerd domein uitvoeren.

1. Verbinding maken met Windows Server toohello zoals u in stap 2. Open in het startscherm hello, **Serverbeheer**.
2. Klik op **lokale Server** in Hallo linker deelvenster van Hallo venster in Serverbeheer.

    ![Serverbeheer starten op de virtuele machine](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Klik op **werkgroep** onder Hallo **eigenschappen** sectie. In Hallo **Systeemeigenschappen** eigenschappenpagina, klikt u op **wijziging** toojoin Hallo domein.

    ![De pagina eigenschappen van systeem](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Hallo-domeinnaam van uw beheerde domein van Azure AD Domain Services opgeven in Hallo **domein** tekstvak en klik op **OK**.

    ![Geef Hallo domein toobe lid](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. U na vragen aan gebruiker tooenter uw referenties toojoin Hallo domein zijn. Zorg ervoor dat u **Hallo referenties voor een gebruiker die behoren toohello AAD DC-beheerders opgeven** groep. Alleen leden van deze groep hebben bevoegdheden toojoin machines toohello beheerd domein.

    ![Geef de referenties voor domein](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. U kunt referenties opgeven in een van de volgende manieren Hallo:

   * UPN-indeling: Hallo UPN-achtervoegsel opgeven voor Hallo gebruikersaccount, zoals geconfigureerd in Azure AD. In dit voorbeeld Hallo UPN-achtervoegsel van gebruiker Hallo 'bob' is 'bob@domainservicespreview.onmicrosoft.com'.
   * SAMAccountName indeling: kunt u de accountnaam Hallo Hallo SAMAccountName indeling. In dit voorbeeld moet gebruiker Hallo "bob" tooenter 'CONTOSO100\bob'.

     > [!NOTE]
     > **U kunt het beste Hallo UPN-indeling toospecify referenties gebruikt.** Hallo SAMAccountName mogelijk automatisch gegenereerd als de UPN-voorvoegsel van een gebruiker is te lang (bijvoorbeeld 'joereallylongnameuser'). Als meerdere gebruikers Hallo dezelfde UPN-voorvoegsel (bijvoorbeeld "bob") in uw Azure AD-tenant, hun SAMAccountName-indeling worden automatisch gegenereerde door Hallo-service hebt kan. In dergelijke gevallen Hallo UPN-indeling op betrouwbare wijze kan worden gebruikt toolog in toohello domein.
     >
     >
7. Nadat het domein is geslaagd, ziet u Hallo welkomstbericht toohello domein te volgen. Hallo virtuele machine voor toocomplete Hallo domain join-bewerking opnieuw te starten.

    ![Welkom toohello domein](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Het oplossen van problemen aan domein toevoegen
### <a name="connectivity-issues"></a>Connectiviteitsproblemen
Raadpleeg als Hallo virtuele machine kan niet toofind Hallo domein toohello stappen te volgen:

* Zorg ervoor dat de virtuele machine Hallo verbonden toohello hetzelfde virtuele netwerk als die u kunt Domain Services in hebt ingeschakeld. Zo niet, Hallo virtuele machine kan niet tooconnect toohello domein en is daarom toojoin Hallo domein.
* Als Hallo virtuele machine verbonden tooanother virtueel netwerk is, zorg ervoor dat dit virtuele netwerk verbonden toohello virtueel netwerk waarin u Domain Services hebt ingeschakeld.
* Probeer tooping Hallo domein met de domeinnaam Hallo van Hallo beheerde domein (bijvoorbeeld ping contoso100.com). Als u dus niet kan toodo, probeert u tooping Hallo IP-adressen voor Hallo domein op Hallo pagina weergegeven waarin u Azure AD Domain Services ingeschakeld (bijvoorbeeld ' ping 10.0.0.4'). Als u kunnen tooping Hallo IP-adres, maar niet Hallo domein bent, DNS mogelijk niet juist geconfigureerd. Mogelijk hebt u Hallo IP-adressen van Hallo domein als de DNS-servers voor het virtuele netwerk Hallo niet geconfigureerd.
* Probeer leegmaken Hallo cache van de DNS-resolver op Hallo virtuele machine (' ipconfig/flushdns).

Als u toohello dialoogvenster waarin u wordt gevraagd referenties toojoin Hallo domein krijgt, hebt u geen problemen met de netwerkverbinding.

### <a name="credentials-related-issues"></a>Problemen met de referenties
Raadpleeg de volgende stappen uit als u problemen met de referenties ondervindt en kan niet toojoin Hallo domein toohello.

* Probeer Hallo UPN-indeling toospecify referenties te gebruiken. Hallo SAMAccountName voor uw account kan worden automatisch gegenereerd als er meerdere gebruikers met Hallo dezelfde UPN-voorvoegsel in uw tenant of als de UPN-voorvoegsel is te lang zijn. Daarom kan Hallo SAMAccountName indeling voor uw account afwijken van wat u verwacht, of gebruik in uw lokale domein.
* Probeer toouse Hallo referenties van een gebruikersaccount dat toohello 'AAD DC-beheerders' groep toojoin machines toohello beheerd domein behoort.
* Zorg ervoor dat er [ingeschakeld Wachtwoordsynchronisatie](active-directory-ds-getting-started-password-sync.md) in overeenstemming met Hallo stappen in Hallo handleiding aan de slag.
* Zorg dat u Hallo UPN van de gebruiker Hallo gebruikt zoals geconfigureerd in Azure AD (bijvoorbeeld 'bob@domainservicespreview.onmicrosoft.com') toosign in.
* Zorg ervoor dat u lang genoeg zijn voor wachtwoord synchronisatie toocomplete zoals opgegeven in Hallo handleiding hebt gewacht.

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
