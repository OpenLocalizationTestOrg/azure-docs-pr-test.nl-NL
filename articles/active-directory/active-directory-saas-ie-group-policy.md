---
title: Azure Access Configuratiescherm extensie voor IE met behulp van een groepsbeleidsobject aaaDeploy | Microsoft Docs
description: Hoe groepeert toouse beleid toodeploy Hallo Internet Explorer-invoegtoepassing voor Hallo mijn Apps portal.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 7c2d49c8-5be0-4e7e-abac-332f9dfda736
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: asteen
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 926f15950bbe81d2fbfe1b0b856470da40880d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-hello-access-panel-extension-for-internet-explorer-using-group-policy"></a>Hoe tooDeploy uitbreiding voor toegang tot Configuratiescherm Hallo voor Internet Explorer met behulp van Groepsbeleid
Deze zelfstudie laat zien hoe toouse Groepsbeleid tooremotely Hallo Toegangsvenster extensie voor Internet Explorer op uw gebruikers, computers installeren. Deze uitbreiding is vereist voor Internet Explorer-gebruikers hoeven te toosign in apps die zijn geconfigureerd met [op basis van wachtwoorden eenmalige aanmelding](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).

Het is raadzaam dat beheerders Hallo-implementatie van deze extensie automatiseren. Anders gebruikers toodownload hebben en Hallo extensie zelf installeren, die foutgevoelig toouser fout en zijn beheerdersrechten vereist. Deze zelfstudie bevat één methode voor het software-implementaties automatiseren met behulp van Groepsbeleid. [Meer informatie over Groepsbeleid.](https://technet.microsoft.com/windowsserver/bb310732.aspx)

Hallo Toegangsvenster uitbreiding is ook beschikbaar voor [Chrome](https://go.microsoft.com/fwLink/?LinkID=311859) en [Firefox](https://go.microsoft.com/fwLink/?LinkID=626998), geen van beide beheerder machtigingen tooinstall vereisen.

## <a name="prerequisites"></a>Vereisten
* U hebt ingesteld [Active Directory Domain Services](https://msdn.microsoft.com/library/aa362244%28v=vs.85%29.aspx), en u uw gebruikers machines tooyour domein hebt toegevoegd.
* Hallo 'Instellingen bewerken' machtiging tooedit Hallo groepsbeleidsobject (GPO), moet u hebben. Standaard hebben leden van beveiligingsgroepen na Hallo deze machtiging: Domeinadministrators, Ondernemingsadministrators en Maker Eigenaar Groepsbeleid. [Meer informatie.](https://technet.microsoft.com/library/cc781991%28v=ws.10%29.aspx)

## <a name="step-1-create-hello-distribution-point"></a>Stap 1: Maak Hallo-distributiepunt
U moet eerst Hallo installer-pakket op een netwerklocatie die toegankelijk zijn voor het Hallo-machines die u wilt dat tooremotely installeren Hallo-extensie op plaatsen. toodo dit als volgt te werk:

1. Meld u als beheerder op de server toohello
2. In Hallo **Serverbeheer** venster te gaan**bestanden- en opslagservices**.
   
    ![Geopende bestanden- en opslagservices](./media/active-directory-saas-ie-group-policy/files-services.png)
3. Ga toohello **Shares** tabblad. Klik vervolgens op **taken** > **nieuwe Share...**
   
    ![Geopende bestanden- en opslagservices](./media/active-directory-saas-ie-group-policy/shares.png)
4. Volledige Hallo **Wizard Nieuwe Share** en set machtigingen tooensure dat deze kan worden geopend op uw gebruikers-machines. [Meer informatie over shares.](https://technet.microsoft.com/library/cc753175.aspx)
5. Downloaden van Microsoft Windows Installer-pakket (MSI-bestand) te volgen Hallo: [toegang Configuratiescherm Extension.msi](https://account.activedirectory.windowsazure.com/Applications/Installers/x64/Access Panel Extension.msi)
6. Kopiëren Hallo installer-pakket tooa gewenste locatie op Hallo-share.
   
    ![Hallo MSI-bestandsshare toohello kopiëren.](./media/active-directory-saas-ie-group-policy/copy-package.png)
7. Controleer of uw clientcomputers kunnen tooaccess Hallo installer-pakket van Hallo-share. 

## <a name="step-2-create-hello-group-policy-object"></a>Stap 2: Hallo Group Policy Object maken
1. Meld u aan toohello-server die als host fungeert voor de installatie van Active Directory Domain Services (AD DS).
2. Ga te in Hallo Serverbeheer,**extra** > **Group Policy Management**.
   
    ![Ga tooTools > Group Policy Management](./media/active-directory-saas-ie-group-policy/tools-gpm.png)
3. In het linkerdeelvenster van Hallo Hallo **Group Policy Management** venster weergeven van uw hiërarchie van organisatie-eenheid (OE) en bepalen bij welke bereik gewenst tooapply Hallo-Groepsbeleid. Bijvoorbeeld, kunt u beslissen toopick een kleine organisatie-eenheid toodeploy tooa enkele gebruikers voor het testen of kiest u een site op het hoogste organisatie-eenheid toodeploy tooyour hele organisatie.
   
   > [!NOTE]
   > Als u wilt wel toocreate en bewerken van uw organisatie-eenheden (OE's), overschakelen back toohello Serverbeheer en gaat u te**extra** > **Active Directory: gebruikers en Computers**.
   > 
   > 
4. Nadat u een organisatie-eenheid hebt geselecteerd, met de rechtermuisknop en selecteer **een groepsbeleidsobject in dit domein maken en hier een koppeling...**
   
    ![Een nieuw groepsbeleidsobject maken](./media/active-directory-saas-ie-group-policy/create-gpo.png)
5. In Hallo **nieuw groepsbeleidsobject** gevraagd, typt u een naam op voor nieuwe Group Policy Object Hallo.
   
    ![Naam Hallo nieuw groepsbeleidsobject](./media/active-directory-saas-ie-group-policy/name-gpo.png)
6. Klik met de rechtermuisknop Hallo Group Policy Object dat u maakte en selecteer **bewerken**.
   
    ![Hallo nieuw groepsbeleidsobject te bewerken](./media/active-directory-saas-ie-group-policy/edit-gpo.png)

## <a name="step-3-assign-hello-installation-package"></a>Stap 3: Hallo installatiepakket toewijzen
1. Bepalen of u toodeploy Hallo-extensie op basis wilt van **Computerconfiguratie** of **Gebruikersconfiguratie**. Wanneer u [Computerconfiguratie](https://technet.microsoft.com/library/cc736413%28v=ws.10%29.aspx), Hallo-extensie op Hallo computer ongeacht welke gebruikers zich tooit aanmelden is geïnstalleerd. Met [Gebruikersconfiguratie](https://technet.microsoft.com/library/cc781953%28v=ws.10%29.aspx), gebruikers hebben geïnstalleerd voor deze ongeacht welke computers ze zich aanmelden op Hallo-extensie.
2. In het linkerdeelvenster van Hallo Hallo **Editor voor Groepsbeleidsbeheer** venster Ga tooeither Hallo mappaden, afhankelijk van welk type van de configuratie die u hebt gekozen te volgen:
   
   * `Computer Configuration/Policies/Software Settings/`
   * `User Configuration/Policies/Software Settings/`
3. Met de rechtermuisknop op **Software-installatie**, selecteer daarna **nieuw** > **pakket...**
   
    ![Maak een nieuw pakket van de software-installatie](./media/active-directory-saas-ie-group-policy/new-package.png)
4. Ga toohello gedeelde map met Hallo installer-pakket van [stap 1: Hallo distributiepunt maakt](#step-1-create-the-distribution-point), selecteer Hallo MSI-bestand en klik op **Open**.
   
   > [!IMPORTANT]
   > Als Hallo-share bevindt zich op deze server, controleert u of u via Hallo netwerk bestandspad in plaats van het lokale bestandspad Hallo Hallo .msi opent.
   > 
   > 
   
    ![Selecteer Hallo-installatiepakket uit Hallo gedeelde map.](./media/active-directory-saas-ie-group-policy/select-package.png)
5. In Hallo **Software distribueren** vragen, selecteer **toegewezen** voor uw implementatiemethode. Klik vervolgens op **OK**.
   
    ![Selecteer toegewezen en klik op OK.](./media/active-directory-saas-ie-group-policy/deployment-method.png)

Hallo-extensie is nu geïmplementeerde toohello organisatie-eenheid die u hebt geselecteerd. [Meer informatie over Software-installatie.](https://technet.microsoft.com/library/cc738858%28v=ws.10%29.aspx)

## <a name="step-4-auto-enable-hello-extension-for-internet-explorer"></a>Stap 4: Auto-Enable Hallo-extensie voor Internet Explorer
Bovendien toorunning Hallo installatieprogramma van alle uitbreidingen voor Internet Explorer moet ingeschakeld zijn voordat deze kan worden gebruikt. Volg de stappen Hallo hieronder tooenable Hallo uitbreiding voor toegang tot Configuratiescherm met behulp van Groepsbeleid:

1. In Hallo **Editor voor Groepsbeleidsbeheer** venster Ga tooeither Hallo paden, afhankelijk van welk type van de configuratie die u kiest in volgende [stap 3: toewijzen Hallo installatiepakket](#step-3-assign-the-installation-package):
   
   * `Computer Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/Security Features/Add-on Management`
2. Met de rechtermuisknop op **lijst met invoegtoepassingen**, en selecteer **bewerken**.
    ![Invoegtoepassing lijst niet bewerken.](./media/active-directory-saas-ie-group-policy/edit-add-on-list.png)
3. In Hallo **lijst met invoegtoepassingen** Selecteer **ingeschakeld**. Klik vervolgens onder Hallo **opties** sectie, klikt u op **weergeven...** .
   
    ![Klik op inschakelen en klik vervolgens op weergeven...](./media/active-directory-saas-ie-group-policy/edit-add-on-list-window.png)
4. In Hallo **inhoud weergeven** venster Hallo volgende stappen uit te voeren:
   
   1. Voor de eerste kolom hello (Hallo **waardenaam** veld), kopiëren en plakken Hallo volgende klasse-ID:`{030E9A3F-7B18-4122-9A60-B87235E4F59E}`
   2. Voor de tweede kolom hello (Hallo **waarde** veld), typt u Hallo waarde te volgen:`1`
   3. Klik op **OK** tooclose hello **inhoud weergeven** venster.
      
      ![Vul Hallo waarden zoals hierboven.](./media/active-directory-saas-ie-group-policy/show-contents.png)
5. Klik op **OK** tooapply uw wijzigingen en sluiten Hallo **lijst met invoegtoepassingen** venster.

Hallo extensie moet nu worden ingeschakeld voor Hallo-machines in Hallo geselecteerd organisatie-eenheid. [Meer informatie over het gebruik van de Groepsbeleid tooenable- of uitschakelen van invoegtoepassingen voor Internet Explorer.](https://technet.microsoft.com/library/dn454941.aspx)

## <a name="step-5-optional-disable-remember-password-prompt"></a>Stap 5 (optioneel): 'Wachtwoord onthouden' Prompt uitschakelen
Wanneer gebruikers aanmelden toowebsites met Hallo uitbreiding voor toegang tot Configuratiescherm, Internet Explorer mogelijk weergeven Hallo volgende gevraagd gevraagd "wilt u toostore uw wachtwoord?"

![](./media/active-directory-saas-ie-group-policy/remember-password-prompt.png)

Als u wenst dat tooprevent uw gebruikers kunnen deze vraag te zien, stappen Hallo hieronder tooprevent automatisch aanvullen van onthouden wachtwoorden:

1. In Hallo **Editor voor Groepsbeleidsbeheer** venster, Ga toohello pad hieronder vermeld. Deze configuratieinstelling is alleen beschikbaar onder **Gebruikersconfiguratie**.
   
   * `User Configuration/Policies/Administrative Templates/Windows Components/Internet Explorer/`
2. Hallo-instelling met de naam zoeken **Hallo automatisch aanvullen functie voor gebruikersnamen en wachtwoorden op formulieren inschakelen**.
   
   > [!NOTE]
   > Eerdere versies van Active Directory kunnen deze instelling met de naam van de Hallo lijst **niet toestaan dat wachtwoorden voor automatisch aanvullen toosave**. Hallo-configuratie voor de instelling verschilt van het Hallo instelling beschreven in deze zelfstudie.
   > 
   > 
   
    ![Vergeet niet toolook voor dit onder gebruikersinstellingen.](./media/active-directory-saas-ie-group-policy/disable-auto-complete.png)
3. Hallo hierboven instelling klik met de rechtermuisknop en selecteer **bewerken**.
4. Hallo-venster met de titel **Hallo automatisch aanvullen functie voor gebruikersnamen en wachtwoorden op formulieren inschakelen**, selecteer **uitgeschakelde**.
   
    ![Selecteer uitschakelen](./media/active-directory-saas-ie-group-policy/disable-passwords.png)
5. Klik op **OK** tooapply deze wijzigingen en het venster sluiten Hallo.

Gebruikers wordt niet meer kunnen toostore hun referenties of automatisch aanvullen tooaccess eerder opgeslagen referenties gebruiken. Echter, dit beleid staat toe dat gebruikers toocontinue toouse automatisch aanvullen voor andere soorten formuliervelden, zoals zoekvelden.

> [!WARNING]
> Als dit beleid is ingeschakeld, nadat gebruikers hebt gekozen toostore sommige referenties, dit beleid wordt *niet* wissen Hallo-referenties die al zijn opgeslagen.
> 
> 

## <a name="step-6-testing-hello-deployment"></a>Stap 6: Hallo implementatie testen
Voer onderstaande tooverify Hallo stappen als Hallo extensie implementatie geslaagd is:

1. Als u hebt geïmplementeerd met behulp van **Computerconfiguratie**, meld u aan bij een clientcomputer die deel uitmaakt van de organisatie-eenheid die u hebt geselecteerd in toohello [stap 2: Maak Hallo Group Policy Object](#step-2-create-the-group-policy-object). Als u hebt geïmplementeerd met behulp van **Gebruikersconfiguratie**, zorg ervoor dat toosign in als een gebruiker die lid is van toothat organisatie-eenheid.
2. Het duurt een paar aanmelding modules voor Groepsbeleid Hallo toofully update wijzigingen aan deze machine. tooforce hello update, open een **opdrachtprompt** venster en Voer Hallo volgende opdracht:`gpupdate /force`
3. Hallo-machine voor Hallo installatie tootake plaats, moet u opnieuw. Wanneer kan aanzienlijk langer duren dan normaal tijdens het Hallo-extensie wordt geïnstalleerd.
4. Start opnieuw op en open **Internet Explorer**. Op Hallo rechterbovenhoek van Hallo-venster, klikt u op **extra** (Hallo tandwielpictogram pictogram) en selecteer vervolgens **invoegtoepassingen beheren**.
   
    ![Ga tooTools > invoegtoepassingen beheren](./media/active-directory-saas-ie-group-policy/manage-add-ons.png)
5. In Hallo **invoegtoepassingen beheren** venster controleren die Hallo **Configuratiescherm-uitbreiding voor toegang tot** is geïnstalleerd en dat de **Status** te is ingesteld**ingeschakeld**.
   
    ![Controleer of deze Hallo uitbreiding van het Configuratiescherm toegang is geïnstalleerd en ingeschakeld.](./media/active-directory-saas-ie-group-policy/verify-install.png)

## <a name="related-articles"></a>Verwante artikelen
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md) (Artikelindex voor toepassingsbeheer in Azure Active Directory)
* [Toegang tot toepassingen en eenmalige aanmelding bij Azure Active Directory](active-directory-appssoaccess-whatis.md)
* [Hallo Configuratiescherm-uitbreiding voor toegang tot het oplossen van problemen voor Internet Explorer](active-directory-saas-ie-troubleshooting.md)

