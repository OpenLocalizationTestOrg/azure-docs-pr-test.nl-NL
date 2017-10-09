---
title: setup van iSCSI-aaaMicrosoft Azure StorSimple virtuele matrix | Microsoft Docs
description: "Hierin wordt beschreven hoe de initiële installatie tooperform, uw StorSimple iSCSI-server registreren en Apparaatinstelling."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 4db116d1-978b-48e8-b572-a719a8425dbc
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: b4ff6391cb2af69d4e83dcdac5e027f8498005b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array--set-up-as-an-iscsi-server-via-azure-portal"></a>Matrix van de virtuele StorSimple-Set up als implementeert een iSCSI-server via de Azure-portal

![Processtroom voor iSCSI-installatie](./media/storsimple-virtual-array-deploy3-iscsi-setup/iscsi4.png)

## <a name="overview"></a>Overzicht

Deze zelfstudie implementatie geldt toohello Microsoft Azure StorSimple virtuele matrix. Deze zelfstudie wordt beschreven hoe tooperform Hallo initiële installatie, uw StorSimple iSCSI-server, Apparaatinstelling voltooien hello, registreren en vervolgens maken, koppelen, initialiseren en volumes op uw virtuele StorSimple-matrix geconfigureerd als een server met iSCSI-indeling. 

Hallo procedures beschreven nemen hier ongeveer 30 minuten too1 uur toocomplete. Hallo-informatie in dit artikel wordt gepubliceerd geldt alleen tooStorSimple virtuele matrices.

## <a name="setup-prerequisites"></a>Vereisten voor installatie

Voordat u configureren en van uw virtuele StorSimple-matrix instellen, zorg ervoor dat:

* U hebt een virtuele-matrix ingericht en verbonden tooit zoals beschreven in [implementeren StorSimple virtuele matrix - inrichten van een virtuele-matrix in Hyper-V](storsimple-ova-deploy2-provision-hyperv.md) of [implementeren StorSimple virtuele matrix - inrichten van een virtuele-matrix in VMware ](storsimple-virtual-array-deploy2-provision-vmware.md).
* U hebt de serviceregistratiesleutel Hallo van Hallo Apparaatbeheer StorSimple-service die u hebt gemaakt toomanage uw virtuele StorSimple-matrices. Zie voor meer informatie **stap 2: Get Hallo serviceregistratiesleutel** in [implementeren StorSimple virtuele matrix - voorbereiden Hallo portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
* Als dit Hallo tweede of volgende virtuele matrix dat u met een bestaande Apparaatbeheer StorSimple-service registreren wilt, moet u de gegevensversleutelingssleutel van Hallo service hebben. Deze sleutel is gegenereerd nadat Hallo eerste apparaat is geregistreerd met deze service. Als u deze sleutel hebt verloren, Zie **Get Hallo service gegevensversleutelingssleutel** in [gebruik Hallo Webgebruikersinterface tooadminister uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key).

## <a name="step-by-step-setup"></a>Stapsgewijze setup

Gebruik Hallo tooset voor stapsgewijze instructies opvolgen en uw virtuele StorSimple-matrix te configureren:

* [Stap 1: Hallo lokale web UI-installatie te voltooien en Registreer uw apparaat](#step-1-complete-the-local-web-ui-setup-and-register-your-device)
* [Stap 2: Volledige Hallo vereist apparaat instellen](#step-2-complete-the-required-device-setup)
* [Stap 3: Een volume toevoegen](#step-3-add-a-volume)
* [Stap 4: Koppelen, initialiseren en formatteren van een volume](#step-4-mount-initialize-and-format-a-volume)

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Stap 1: Hallo lokale web UI-installatie te voltooien en Registreer uw apparaat

#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Hallo setup en Hallo-apparaat registreren

1. Open een browservenster. tooconnect toohello web UI-type:
   
    `https://<ip-address of network interface>`
   
    Gebruik Hallo verbindings-URL in de vorige stap Hallo hebt genoteerd. U ziet een melding dat er een probleem met het beveiligingscertificaat van de website Hallo is fout. Klik op **doorgaan toothis webpagina**.
   
    ![Fout in beveiligingscertificaat](./media/storsimple-virtual-array-deploy3-iscsi-setup/image3.png)
2. Meld u aan toohello-webgebruikersinterface van uw virtuele apparaat als **StorSimpleAdmin**. Voer beheerderswachtwoord van het Hallo-apparaat die u hebt gewijzigd in stap 3: begin Hallo virtueel apparaat in [implementeren StorSimple virtuele matrix - inrichten van een virtueel apparaat in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) of [implementeren StorSimple virtuele matrix - Inrichten van een virtueel apparaat in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
    ![Aanmeldingspagina](./media/storsimple-virtual-array-deploy3-iscsi-setup/image4.png)
3. U gaat toohello **Start** pagina. Deze pagina beschrijft Hallo verschillende instellingen die vereist zijn tooconfigure en registreer Hallo virtueel apparaat met Hallo Apparaatbeheer StorSimple-service. Houd er rekening mee dat Hallo **instellingen**, **Web proxy-instellingen**, en **tijdinstellingen** zijn optioneel. alleen instellingen zijn vereist Hallo **apparaatinstellingen** en **Cloudinstellingen**.
   
    ![startpagina](./media/storsimple-virtual-array-deploy3-iscsi-setup/image5.png)
4. Op Hallo **instellingen** pagina onder **netwerkinterfaces**, DATA 0 wordt automatisch voor u geconfigureerd. Elke netwerkinterface is ingesteld door standaard tooget een IP-adres automatisch (DHCP). Daarom wordt een IP-adres, subnetmasker en gateway automatisch toegewezen (voor IPv4 en IPv6).
   
    Als u van plan bent toodeploy uw apparaat als iSCSI-server (tooprovision blokopslag), het is raadzaam dat u Hallo uitschakelen **IP-adres automatisch ophalen** optie en statische IP-adressen configureren.
   
    ![De pagina met netwerkinstellingen](./media/storsimple-virtual-array-deploy3-iscsi-setup/image6.png)
   
    Als u meer dan één netwerkinterface tijdens het Hallo inrichten van Hallo-apparaat hebt toegevoegd, kunt u ze hier configureren. Houd er rekening mee dat kunt u de netwerkinterface configureren als IPv4 alleen of als zowel IPv4 als IPv6. Alleen IPv6-configuraties worden niet ondersteund.
5. DNS-servers zijn vereist, omdat ze worden gebruikt wanneer het apparaat toocommunicate met uw cloudserviceproviders opslag of tooresolve probeert uw apparaat met de naam als deze is geconfigureerd als een bestandsserver. Op Hallo **instellingen** pagina onder Hallo **DNS-servers**:
   
   1. Een primaire en secundaire DNS-server automatisch geconfigureerd. Als u tooconfigure statische IP-adressen kiest, kunt u DNS-servers. U wordt aangeraden dat u een primaire en secundaire DNS-server configureren voor hoge beschikbaarheid.
   2. Klik op **Toepassen**. Hiermee wordt de van toepassing en Hallo netwerkinstellingen valideren.
6. Op Hallo **apparaatinstellingen** pagina:
   
   1. Wijs een uniek **naam** tooyour apparaat. Deze naam mag 1-15 tekens lang zijn en mag letter, cijfers en afbreekstreepjes bevatten.
   2. Klik op Hallo **iSCSI-server** pictogram ![serverpictogram iSCSI-](./media/storsimple-virtual-array-deploy3-iscsi-setup/image7.png) voor Hallo **Type** van apparaten die u maakt. Een iSCSI-server kunt u tooprovision blokopslag.
   3. Opgeven of u dit apparaat toobe domein wilt. Als uw apparaat is een server met iSCSI-, is lid worden van domein Hallo optioneel. Als u het iSCSI-serverdomein tooa toonot join besluit, klikt u op **toepassen**, wacht Hallo instellingen toobe toegepast en sla de volgende stap toohello.
      
       Als u wilt dat domein tooa toojoin Hallo-apparaat. Voer een **domeinnaam**, en klik vervolgens op **toepassen**.
      
      > [!NOTE]
      > Als het lidmaatschap van de iSCSI-server tooa domein, zorg ervoor dat uw virtuele matrix in de eigen organisatie-eenheid (OE) voor Microsoft Azure Active Directory en geen groepsbeleidsobjecten (GPO) zijn toegepaste tooit.
      > 
      > 
   4. Een dialoogvenster wordt weergegeven. Geef uw domeinreferenties in de opgegeven indeling Hallo. Klik op het vinkje Hallo ![vinkje](./media/storsimple-virtual-array-deploy3-iscsi-setup/image15.png). Hallo domeinreferenties zal worden gecontroleerd. U ziet een foutbericht weergegeven als Hallo referenties onjuist zijn.
      
       ![referenties](./media/storsimple-virtual-array-deploy3-iscsi-setup/image8.png)
   5. Klik op **Toepassen**. Hiermee wordt de van toepassing en Hallo apparaatinstellingen valideren.
7. (Optioneel) uw webproxyserver configureren. Hoewel webproxyconfiguratie optioneel is, worden op de hoogte gebracht als u een webproxy gebruikt, u alleen deze hier configureren kunt.
   
    ![webproxy configureren](./media/storsimple-virtual-array-deploy3-iscsi-setup/image9.png)
   
    Op Hallo **Web proxy** pagina:
   
   1. Geef Hallo **Web-URL voor proxy** in deze indeling: *http://host-IP adres* of *FDQN:Port nummer*. Houd er rekening mee dat HTTPS-URL's worden niet ondersteund.
   2. Geef **verificatie** als **Basic** of **geen**.
   3. Als u verificatie gebruikt, moet u ook tooprovide een **gebruikersnaam** en **wachtwoord**.
   4. Klik op **Toepassen**. Hiermee wordt valideren en Hallo geconfigureerd web proxy-instellingen toegepast.
8. (Optioneel) Configureer Hallo tijdinstellingen voor uw apparaat, zoals tijdzone en Hallo primaire en secundaire NTP-servers. NTP-servers zijn vereist, omdat uw apparaat de tijd synchroniseren moet zodat verificatie met uw cloudserviceproviders.
   
    ![Tijdinstellingen](./media/storsimple-virtual-array-deploy3-iscsi-setup/image10.png)
   
    Op Hallo **tijdinstellingen** pagina:
   
   1. Selecteer in de vervolgkeuzelijst hello, Hallo **tijdzone** op basis van de geografische locatie Hallo in welke Hallo apparaat wordt geïmplementeerd. Hallo standaardtijdzone voor uw apparaat is PST. Het apparaat zal deze tijdzone gebruiken voor alle geplande bewerkingen.
   2. Geef een **primaire NTP-server** voor uw apparaat of accepteer de standaardwaarde Hallo van time.windows.com. Zorg ervoor dat uw netwerk NTP-verkeer toopass van uw datacenter toohello Internet toestaat.
   3. Geef desgewenst een **secundaire NTP-server** voor uw apparaat.
   4. Klik op **Toepassen**. Zo valideren en past u tijdinstellingen Hallo geconfigureerd.
9. Hallo cloudinstellingen configureren voor uw apparaat. In deze stap maakt u Hallo lokale apparaatconfiguratie voltooien en vervolgens Hallo-apparaat registreren bij uw StorSimple-apparaat Manager-service.
   
   1. Voer Hallo **serviceregistratiesleutel** die u hebt verkregen **stap 2: Get Hallo serviceregistratiesleutel** in [implementeren StorSimple virtuele matrix - voorbereiden Hallo Portal](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key).
   2. Als dit geen eerste Hallo-apparaat dat u met deze service registreren is wilt, moet u tooprovide hello **gegevensversleutelingssleutel van Service**. Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple-apparaat Manager-service. Voor meer informatie raadpleegt u te[Get Hallo service gegevensversleutelingssleutel](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) op uw lokale webgebruikersinterface.
   3. Klik op **registreren**. Dit wordt opnieuw opgestart Hallo-apparaat. U moet mogelijk toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd. Nadat het Hallo-apparaat opnieuw is opgestart, gaat u toohello aanmelding op de pagina.
      
      ![Apparaat registreren](./media/storsimple-virtual-array-deploy3-iscsi-setup/image11.png)
10. Azure-portal toohello retourneren.
11. Navigeer toohello **apparaten** blade van uw service. Als u een groot aantal bronnen hebt, klikt u op **alle resources**, klikt u op de naam van uw service (zoek deze indien nodig) en klik vervolgens op **apparaten**.
12. Op Hallo **apparaten** blade Hallo apparaat verbinding heeft met toohello service door het opzoeken van Hallo status controleren. Hallo Apparaatstatus moet **tooset gereed**.
    
    ![Apparaat registreren](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png)

## <a name="step-2-configure-hello-device-as-iscsi-server"></a>Stap 2: Hallo-apparaat als iSCSI-server configureren

Volgende stappen uit in Azure portal toocomplete Hallo vereist Apparaatinstelling Hallo Hallo uitvoeren.

#### <a name="tooconfigure-hello-device-as-iscsi-server"></a>tooconfigure hello apparaat als iSCSI-server

1. Ga tooyour Apparaatbeheer StorSimple-service en ga vervolgens te**Management > apparaten**. In Hallo **apparaten** blade, selecteer Hallo-apparaat die u zojuist hebt gemaakt. Dit apparaat wordt weergegeven als **tooset gereed**.
   
    ![Apparaat configureren als iSCSI-server](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis1m.png) 
2. Klik op Hallo-apparaat en u een bannerbericht te zien die aangeeft dat het Hallo-apparaat klaar toosetup.
   
    ![Apparaat configureren als iSCSI-server](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis2m.png)  
3. Klik op **configureren** op Hallo apparaat opdrachtbalk klikken. Hiermee opent u up Hallo **configureren** blade. In Hallo **configureren** blade Hallo te volgen:
   
   * Hallo iSCSI-servernaam wordt automatisch gevuld.
   * Zorg ervoor dat de versleuteling van cloudopslag hello te is ingesteld**ingeschakeld**. Dit zorgt ervoor dat verzonden hello apparaat toohello cloud Hallo-gegevens worden versleuteld.
   * Geef een versleutelingssleutel van 32 tekens en opnemen in een app Sleutelbeheer voor toekomstig gebruik.
   * Selecteer een storage account toobe gebruikt met uw apparaat. In dit abonnement, kunt u een bestaand opslagaccount selecteren, u kunt ook op **toevoegen** toochoose een account van een ander abonnement.
     
     ![Apparaat configureren als iSCSI-server](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis4m.png)
4. Klik op **configureren** toocomplete Hallo iSCSI-server instellen.
   
    ![Apparaat configureren als iSCSI-server](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis5m.png) 
5. U wordt gewaarschuwd dat het maken van de iSCSI-hello uitgevoerd wordt. Nadat het Hallo iSCSI-server is gemaakt, Hallo **apparaten** blade wordt bijgewerkt en de bijbehorende Apparaatstatus Hallo is **Online**.
   
    ![Apparaat configureren als iSCSI-server](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis9m.png)

## <a name="step-3-add-a-volume"></a>Stap 3: Een volume toevoegen

1. In Hallo **apparaten** blade, selecteer Hallo-apparaat die u zojuist hebt geconfigureerd als een server met iSCSI. Klik op **...**  (u kunt ook met de rechtermuisknop op in deze rij) en selecteer in het contextmenu hello, **volume toevoegen**. U kunt ook klikken op **+ volume toevoegen** uit Hallo opdrachtbalk. Hiermee opent u up Hallo **volume toevoegen** blade.
   
    ![Een volume toevoegen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis10m.png)
2. In Hallo **volume toevoegen** blade Hallo te volgen:
   
   * In Hallo **volumenaam** en voer een unieke naam voor het volume. Hallo-naam moet een tekenreeks die 3 too127 tekens bevat.
   * In Hallo **Type** dropdown lijst, opgeven of toocreate een **tiers verdeelde** of **lokaal vastgemaakt** volume. Selecteer voor workloads waarvoor lokale garanties, lage latenties en betere prestaties, **lokaal vastgemaakt** **volume**. Voor alle overige gegevens selecteert **tiers verdeelde** **volume**.
   * In Hallo **capaciteit** veld, Hallo grootte van Hallo volume opgeven. Een gelaagd volume moet liggen tussen 500 GB en 5 TB en een lokaal vastgemaakt volume moet tussen 50 en 500 GB.
     
     Een lokaal vastgemaakt volume is compact ingericht en zorgt ervoor dat Hallo primaire gegevens in Hallo volume op Hallo apparaat blijft en heeft geen toohello cloud worden gelekt.
     
     Een gelaagd volume op Hallo is daarentegen dun ingericht. Wanneer u een gelaagd volume maakt, wordt ongeveer 10% van Hallo ruimte is ingericht op de lokale laag Hallo en 90% van Hallo ruimte in de cloud Hallo is ingericht. Hallo bijvoorbeeld gegevenslagen op als u een volume 1 TB ingericht, 100 GB zou bevinden zich in de lokale ruimte Hallo en 900 GB wordt gebruikt in de cloud Hallo wanneer. Dit betekent op zijn beurt is dat als u tekort aan alle Hallo lokale ruimte op Hallo-apparaat kan niet u een gelaagde share inrichten (omdat Hallo 10% niet meer beschikbaar).
     
     ![Een volume toevoegen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis12.png)
   * Klik op **verbonden hosts**, selecteert u een access control record (ACR) bijbehorende toohello iSCSI-initiator wilt tooconnect toothis volume en klik vervolgens op **Selecteer**. <br><br> 
3. tooadd nieuwe verbonden host, klikt u op **nieuwe toevoegen**, voer een naam voor het Hallo-host en de iSCSI Qualified Name (IQN) en klik vervolgens op **toevoegen**. Als u Hallo IQN niet hebt, gaat u verder te[bijlage A: ophalen Hallo IQN van een Windows Server-host](#appendix-a-get-the-iqn-of-a-windows-server-host).
   
      ![Een volume toevoegen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis15m.png)
4. Wanneer u klaar bent voor het configureren van het volume, klikt u op **OK**. Een volume wordt gemaakt met de opgegeven Hallo instellingen en u ziet een melding. Standaard worden controle- en back-up ingeschakeld voor Hallo volume.
   
     ![Een volume toevoegen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis18m.png)
5. tooconfirm die Hallo volume is gemaakt, gaat u toohello is **Volumes** blade. U ziet Hallo volume dat wordt vermeld.
   
   ![Een volume toevoegen](./media/storsimple-virtual-array-deploy3-iscsi-setup/deployis20m.png)

## <a name="step-4-mount-initialize-and-format-a-volume"></a>Stap 4: Koppelen, initialiseren en formatteren van een volume

Hallo uitvoeren na stappen toomount, initialiseren en formatteren van uw StorSimple-volumes op een Windows Server-host.

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, initialiseren en formatteren van een volume

1. Open Hallo **iSCSI-initiator** app op de juiste server Hallo.
2. In Hallo **eigenschappen iSCSI-Initiator** venster op Hallo **detectie** tabblad **Portal detecteren**.
   
    ![portal detecteren](./media/storsimple-virtual-array-deploy3-iscsi-setup/image22.png)
3. In Hallo **doelportaal detecteren** in het dialoogvenster Hallo IP-adres van de netwerkinterface met iSCSI-functionaliteit leveren en klik vervolgens op **OK**.
   
    ![IP-adres](./media/storsimple-virtual-array-deploy3-iscsi-setup/image23.png)
4. In Hallo **eigenschappen iSCSI-Initiator** venster op Hallo **doelen** tabblad, zoek Hallo **gedetecteerde doelen**. (Elk volume wordt een gedetecteerde doel zijn.) de apparaatstatus Hallo moet worden weergegeven als **inactief**.
   
    ![Gedetecteerde doelen](./media/storsimple-virtual-array-deploy3-iscsi-setup/image24.png)
5. Selecteer een apparaat en klik vervolgens op **Connect**. Nadat het Hallo-apparaat is verbonden, Hallo moet statuswijziging te**verbonden**. (Zie voor meer informatie over het gebruik van Hallo Microsoft iSCSI-initiator [installeren en configureren van Microsoft iSCSI-Initiator][1].
   
    ![Selecteer doelapparaat](./media/storsimple-virtual-array-deploy3-iscsi-setup/image25.png)
6. Druk op uw Windows-host op Hallo Windows-toets + X en klik vervolgens op **uitvoeren**.
7. In Hallo **uitvoeren** in het dialoogvenster, type **Diskmgmt.msc**. Klik op **OK**, en Hallo **Schijfbeheer** dialoogvenster wordt weergegeven. Hallo rechterdeelvenster wordt Hallo volumes op uw host weergeven.
8. In Hallo **Schijfbeheer** venster hello gekoppelde volumes weergegeven zoals in de volgende illustratie Hallo. Met de rechtermuisknop op Hallo gedetecteerde volume (Klik op de naam van de schijf Hallo), en klik vervolgens op **Online**.
   
    ![Schijfbeheer](./media/storsimple-virtual-array-deploy3-iscsi-setup/image26.png)
9. Met de rechtermuisknop en selecteer **schijf initialiseren**.
   
    ![Initialiseer de schijf 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image27.png)
10. In het dialoogvenster Hallo Hallo een of meer schijven tooinitialize selecteren en klik vervolgens op **OK**.
    
    ![Initialiseer de schijf 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image28.png)
11. de wizard Nieuw eenvoudig Volume Hello wordt gestart. Selecteer de schijfgrootte van een en klik vervolgens op **volgende**.
    
    ![wizard Nieuw volume 1](./media/storsimple-virtual-array-deploy3-iscsi-setup/image29.png)
12. Een stationsletter toohello volume toewijzen en klik vervolgens op **volgende**.
    
    ![wizard Nieuw volume 2](./media/storsimple-virtual-array-deploy3-iscsi-setup/image30.png)
13. Voer Hallo parameters tooformat Hallo volume. **Op Windows Server wordt alleen NTFS ondersteund.** Hallo toewijzing eenheid grootte too64K ingesteld. Geef een label voor het volume. Het is een aanbevolen procedure voor deze naam toobe identieke toohello volumenaam die u op uw virtuele StorSimple-matrix. Klik op **Volgende**.
    
    ![wizard Nieuw volume 3](./media/storsimple-virtual-array-deploy3-iscsi-setup/image31.png)
14. Controleer Hallo waarden voor het volume en klik vervolgens op **voltooien**.
    
    ![wizard Nieuw volume 4](./media/storsimple-virtual-array-deploy3-iscsi-setup/image32.png)
    
    Hallo-volumes worden weergegeven als **Online** op Hallo **Schijfbeheer** pagina.
    
    ![volumes online](./media/storsimple-virtual-array-deploy3-iscsi-setup/image33.png)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe Hallo toouse lokale webgebruikersinterface te[beheren van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).

## <a name="appendix-a-get-hello-iqn-of-a-windows-server-host"></a>Bijlage A: Get Hallo IQN van een Windows Server-host

Uitvoeren hello te volgen stappen tooget Hallo iSCSI Qualified Name (IQN) van een Windows-host waarop Windows Server 2012 wordt uitgevoerd.

#### <a name="tooget-hello-iqn-of-a-windows-host"></a>tooget hello IQN van een Windows-host

1. Start Hallo Microsoft iSCSI-initiator op uw Windows-host.
2. In Hallo **eigenschappen iSCSI-Initiator** venster op Hallo **configuratie** tabblad Selecteer en kopieer Hallo tekenreeks van Hallo **initiatornaam** veld.
   
    ![Eigenschappen iSCSI-initiator](./media/storsimple-virtual-array-deploy3-iscsi-setup/image34.png)
3. Bewaar deze tekenreeks.

<!--Reference link-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx



