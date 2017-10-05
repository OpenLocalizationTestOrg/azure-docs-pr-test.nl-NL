---
title: 'Azure Active Directory Domain Services: Een virtuele machine van Windows Server toevoegen aan een beheerd domein | Microsoft Docs'
description: Virtuele machine met Windows Server toevoegen aan Azure AD Domain Services
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
ms.openlocfilehash: 9f8d21f6964d26a2e17e31d1f2947e7eb07c177d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain"></a>Een virtuele Windows Server-machine toevoegen aan een beheerd domein
> [!div class="op_single_selector"]
> * [Klassieke Azure-portal - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

In dit artikel laat zien hoe een virtuele machine met Windows Server 2012 R2 naar een beheerd domein van Azure AD Domain Services, met de klassieke Azure portal toevoegen.

## <a name="step-1-create-the-windows-server-virtual-machine"></a>Stap 1: Maak de virtuele machine van Windows Server
Volg de instructies die worden beschreven in de [maken van een virtuele machine waarop Windows wordt uitgevoerd in de klassieke Azure portal](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) zelfstudie. Het is belangrijk om ervoor te zorgen dat de nieuwe virtuele machine wordt gekoppeld aan hetzelfde virtuele netwerk waarin u Azure AD Domain Services hebt ingeschakeld. De optie snel maken schakelt u de virtuele machine toevoegen aan een virtueel netwerk niet. Daarom moet u de optie uit galerie gebruiken voor het maken van de virtuele machine.

Voer de volgende stappen uit voor het maken van een virtuele Windows-computer die lid zijn van het virtuele netwerk waarin u Azure AD Domain Services hebt ingeschakeld.

1. Klik in de klassieke Azure-portal op de opdrachtbalk aan de onderkant van het venster op **nieuw**.
2. Onder **Compute**, klikt u op **virtuele Machine**, klikt u vervolgens op **uit galerie**.
3. Het eerste scherm kunt u **een afbeelding kiezen die** voor uw virtuele machine uit de lijst met beschikbare installatiekopieën. Kies de juiste installatiekopie.

    ![Selecteer de installatiekopie](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. Het tweede scherm kunt u een computernaam, de grootte, en de naam van de gebruiker met beheerdersrechten en het wachtwoord kiezen. Gebruik de laag en de vereiste grootte voor het uitvoeren van uw app of de werkbelasting. De naam van de gebruiker die u hier kiest, is een lokale beheerder op de machine. Geef geen referenties voor een domeingebruikersaccount hier.

    ![Virtuele machine configureren](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. Het derde scherm kunt u resources voor netwerken, opslag en beschikbaarheid te configureren. Zorg ervoor dat u het virtuele netwerk waarin u Azure AD Domain Services van ingeschakeld selecteert de **regio/affiniteit groep/virtueel netwerk** vervolgkeuzelijst. Geef een **Cloud Service DNS-naam** afhankelijk van wat geschikt is voor de virtuele machine.

    ![Virtueel netwerk voor virtuele machine selecteren](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Zorg ervoor dat u de virtuele machine toevoegen aan hetzelfde virtuele netwerk waarin u Azure AD Domain Services hebt ingeschakeld. Als gevolg hiervan kunnen de virtuele machine Zie het domein en taken uitvoeren, zoals lidmaatschap van het domein. Als u maken van de virtuele machine in een ander virtueel netwerk wilt, moet u die virtueel netwerk verbinden met het virtuele netwerk waarin u Azure AD Domain Services hebt ingeschakeld.
   >
   >
6. Het vierde scherm kunt u de VM-Agent installeren en configureren van enkele van de beschikbare uitbreidingen.

    ![Klaar](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Nadat de virtuele machine is gemaakt, de klassieke portal bevat de nieuwe virtuele machine onder de **virtuele Machines** knooppunt. Zowel de virtuele machine als de cloudservice wordt automatisch gestart. Deze krijgen de status **Actief**.

    ![Virtuele machine is actief](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-to-the-windows-server-virtual-machine-using-the-local-administrator-account"></a>Stap 2: Verbinding maken met de Windows Server-virtuele machine met behulp van het lokale administrator-account
Nu we verbinding maken met de nieuwe Windows Server virtuele machine, aan het domein toevoegen. Gebruik de lokale administrator-referenties die hebt opgegeven toen u de virtuele machine, tot stand te brengen.

Voer de volgende stappen uit verbinding maken met de virtuele machine.

1. Navigeer naar **virtuele Machines** knooppunt in de klassieke portal. Selecteer de virtuele machine die u in stap 1 hebt gemaakt en klik op **Connect** op de opdrachtbalk aan de onderkant van het venster.

    ![Verbinding maken met virtuele Windows-computer](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. De klassieke portal vraagt u om te openen of opslaan van een bestand met een extensie 'RDP-', die wordt gebruikt voor het verbinding maken met de virtuele machine. Klik op het bestand te openen wanneer het downloaden is voltooid.
3. Voer bij de aanmeldingsprompt uw **lokale beheerdersreferenties**, die u hebt opgegeven tijdens het maken van de virtuele machine. Bijvoorbeeld, hebben we 'localhost\mahesh' in dit voorbeeld gebruikt.

Op dit moment moet u worden aangemeld bij de zojuist gemaakte virtuele Windows-computer met lokale Administrator-referenties. De volgende stap is de virtuele machine toevoegen aan het domein.

## <a name="step-3-join-the-windows-server-virtual-machine-to-the-aad-ds-managed-domain"></a>Stap 3: Join, de virtuele machine van Windows Server aan de beheerde AAD-DS-domein
Voer de volgende stappen voor de virtuele machine met Windows Server toevoegen aan de beheerde AAD-DS-domein.

1. Verbinding maken met de Windows-Server zoals u in stap 2. Open in het startscherm **Serverbeheer**.
2. Klik op **lokale Server** in het linkerdeelvenster van het venster Server Manager.

    ![Serverbeheer starten op de virtuele machine](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Klik op **werkgroep** onder de **eigenschappen** sectie. In de **Systeemeigenschappen** eigenschappenpagina, klikt u op **wijziging** aan het domein.

    ![De pagina eigenschappen van systeem](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Geef de domeinnaam van uw beheerde domein van Azure AD Domain Services in de **domein** tekstvak en klik op **OK**.

    ![Geef het domein worden toegevoegd](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. U wordt gevraagd uw referenties voor deelname aan het domein op te geven. Zorg ervoor dat u **geeft u de referenties voor een gebruiker die horen bij de AAD-DC-beheerders** groep. Alleen leden van deze groep hebben bevoegdheden voor machines toevoegen aan het beheerde domein.

    ![Geef de referenties voor domein](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. U kunt referenties opgeven in een van de volgende manieren:

   * UPN-indeling: Geef het UPN-achtervoegsel voor de gebruikersaccount, zoals geconfigureerd in Azure AD. In dit voorbeeld is het het UPN-achtervoegsel van de gebruiker "bob" 'bob@domainservicespreview.onmicrosoft.com'.
   * SAMAccountName indeling: U kunt de accountnaam opgeven in de indeling SAMAccountName. In dit voorbeeld moet de gebruiker "bob" zou 'CONTOSO100\bob' invoeren.

     > [!NOTE]
     > **U kunt het beste de UPN-indeling gebruikt referenties opgeven.** De SAMAccountName kan worden automatisch gegenereerd als de UPN-voorvoegsel van een gebruiker is te lang (bijvoorbeeld 'joereallylongnameuser'). Als meerdere gebruikers het voorvoegsel met dezelfde UPN (bijvoorbeeld "bob") in uw Azure AD-tenant hebben, mogelijk de indeling van hun SAMAccountName automatisch gegenereerd door de service. In dergelijke gevallen kan de UPN-indeling op betrouwbare wijze worden gebruikt voor aanmelding bij het domein.
     >
     >
7. Nadat het domein is geslaagd, ziet u het volgende bericht Verwelkom u aan het domein. Start opnieuw op de virtuele machine voor het domein join-bewerking te voltooien.

    ![Welkom bij het domein](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Het oplossen van problemen aan domein toevoegen
### <a name="connectivity-issues"></a>Connectiviteitsproblemen
Als de virtuele machine niet gevonden van het domein is, raadpleegt u de volgende stappen:

* Zorg ervoor dat de virtuele machine is verbonden met hetzelfde virtuele netwerk als u Domain Services in hebt ingeschakeld. Zo niet, de virtuele machine is geen verbinding maken met het domein en daarom kan niet aan het domein.
* Als de virtuele machine met een ander virtueel netwerk is verbonden, zorg ervoor dat dit virtuele netwerk is verbonden met het virtuele netwerk waarin u Domain Services hebt ingeschakeld.
* Probeer te pingen van het domein met de domeinnaam van het beheerde domein (bijvoorbeeld ping contoso100.com). Als u niet lukt om dit te doen, probeert te pingen van de IP-adressen voor het domein dat wordt weergegeven op de pagina waarop u Azure AD Domain Services hebt ingeschakeld (bijvoorbeeld ' ping 10.0.0.4'). Als u kunnen ping het IP-adres, maar niet het domein bent, DNS mogelijk niet juist geconfigureerd. Mogelijk hebt u de IP-adressen van het domein als de DNS-servers voor het virtuele netwerk niet geconfigureerd.
* Probeer de DNS-resolver cache op de virtuele machine (' ipconfig/flushdns).

Als u in het dialoogvenster waarin u wordt gevraagd om referenties krijgt aan het domein, hebt u geen problemen met de netwerkverbinding.

### <a name="credentials-related-issues"></a>Problemen met de referenties
Raadpleeg de volgende stappen uit als u problemen met de referenties ondervindt en kan niet deelnemen aan het domein zijn.

* Probeer de UPN-indeling met referenties opgeven. De SAMAccountName voor uw account mogelijk automatisch gegenereerd als er meerdere gebruikers met hetzelfde voorvoegsel UPN in uw tenant of als de UPN-voorvoegsel te lang is. Daarom kan de indeling SAMAccountName voor uw account afwijken van wat u verwacht, of gebruik in uw lokale domein.
* Probeer de referenties van een gebruikersaccount die deel uitmaakt van de groep 'AAD DC Administrators' machines toevoegen aan het beheerde domein gebruiken.
* Zorg ervoor dat u [wachtwoordsynchronisatie hebt ingeschakeld](active-directory-ds-getting-started-password-sync.md) volgens de stappen beschreven in de handleiding.
* Zorg dat u de UPN van de gebruiker gebruikt zoals geconfigureerd in Azure AD (bijvoorbeeld 'bob@domainservicespreview.onmicrosoft.com') aan te melden.
* Zorg ervoor dat u lang genoeg voor Wachtwoordsynchronisatie voltooid zoals opgegeven in de handleiding hebt gewacht.

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Een beheerd domein van Azure AD Domain Services beheren](active-directory-ds-admin-guide-administer-domain.md)
