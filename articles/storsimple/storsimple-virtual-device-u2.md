---
title: aaaStorSimple virtueel apparaat Update 2 | Microsoft Docs
description: Informatie over hoe toocreate, implementeren en beheren van een virtueel StorSimple-apparaat in een Microsoft Azure virtual network. (Geldt tooStorSimple Update 2).
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Een virtueel StorSimple-apparaat implementeren en beheren in Azure
## <a name="overview"></a>Overzicht
Hallo StorSimple 8000 series virtueel apparaat is een extra functionaliteit die wordt geleverd met uw Microsoft Azure StorSimple-oplossing. Hallo virtuele StorSimple-apparaat wordt uitgevoerd op een virtuele machine in een virtueel netwerk van Microsoft Azure en kunt u tooback up- en kloon-gegevens van uw hosts. Deze zelfstudie wordt beschreven hoe toodeploy en beheren van een virtueel apparaat in Azure en is van toepassing tooall Hallo virtuele apparaten met softwareversie Update 2 en lager.

#### <a name="virtual-device-model-comparison"></a>Vergelijking van de verschillende modellen virtuele apparaten
Hallo StorSimple-apparaat beschikbaar in twee modellen standard 8010 is (voorheen bekend als Hallo 1100) en de premium 8020 (geïntroduceerd bij Update 2). Hieronder wordt een vergelijking van Hallo twee modellen in een tabel.

| Apparaatmodel | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maximale capaciteit** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 kerngeheugens, 7 GB geheugen) |Standard_DS3 (4 kerngeheugens, 14 GB geheugen) |
| **Versiecompatibiliteit** |Versies met Update 2 of oudere of nieuwere software |Versies met Update 2 of nieuwere software |
| **Beschikbaarheid in regio’s** |Alle Azure-regio's |Alle Azure-regio's waar ondersteuning wordt geboden voor Premium Storage en Azure-VM’s met DS3<br></br> Gebruik [deze lijst](https://azure.microsoft.com/en-us/regions/services) toosee als beide *virtuele Machines > DS-serie* en *opslag > schijfruimte* beschikbaar zijn in uw regio. |
| **Opslagtype** |Maakt gebruik van Azure Standard-opslag voor lokale schijven<br></br> Meer informatie over hoe te[een Standard-opslagaccount maken](../storage/common/storage-create-storage-account.md) |Maakt gebruik van Azure Premium Storage voor lokale schijven<sup>2</sup> <br></br>Meer informatie over hoe te[een Premium Storage-account maken](../storage/common/storage-premium-storage.md) |
| **Richtlijnen voor de workload** |Bestanden ophalen uit back-ups op itemniveau |Cloudontwikkelings- en testscenario’s, lage latentie en werkbelasting met hogere prestaties <br></br>Secundair apparaat voor herstel na noodgevallen |

<sup>1</sup> *voorheen bekend als Hallo 1100*.

<sup>2</sup> *beide 8010 Hallo en 8020 Azure Standard-opslag gebruiken voor Hallo cloud laag. Hallo verschil zit hem alleen in de lokale laag Hallo binnen Hallo apparaat*.

Dit artikel wordt stapsgewijs Hallo-proces voor het implementeren van een virtueel StorSimple-apparaat in Azure. Wanneer u dit artikel hebt gelezen:

* Begrijpen hoe Hallo virtuele apparaat verschilt van het fysieke apparaat Hallo.
* Kan toocreate worden en Hallo virtuele apparaat configureren.
* Verbinding maken met een virtueel apparaat toohello.
* Meer informatie over hoe toowork met Hallo virtuele apparaat.

Deze zelfstudie geldt tooall Hallo virtuele StorSimple-apparaten met Update 2 en hoger.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Hoe Hallo virtuele apparaat verschilt van het fysieke apparaat Hallo
Hallo virtuele StorSimple-apparaat is een softwarematige versie van StorSimple die wordt uitgevoerd op één knooppunt in een Microsoft Azure virtuele Machine. Hallo virtueel apparaat ondersteunt herstel na noodgevallen waarbij uw fysieke apparaat is niet beschikbaar en is geschikt voor gebruik in op itemniveau voor het ophalen van de back-ups, on-premises herstel na noodgevallen en cloudontwikkelings en scenario's testen.

#### <a name="differences-from-hello-physical-device"></a>Verschillen met het fysieke apparaat Hallo
Hallo bevat volgende tabel enkele belangrijke verschillen tussen Hallo virtuele StorSimple-apparaat en het fysieke StorSimple-apparaat Hallo.

|  | Fysiek apparaat | Virtueel apparaat |
| --- | --- | --- |
| **Locatie** |Bevindt zich in Hallo datacenter. |Wordt uitgevoerd in Azure. |
| **Netwerkinterfaces** |Heeft zes netwerkinterfaces: DATA 0 t/m DATA 5. |Heeft slechts één netwerkinterface: DATA 0 |
| **Registratie** |Geregistreerd tijdens de configuratiestap Hallo. |Registratie is een afzonderlijke taak. |
| **Gegevensversleutelingssleutel van service** |Opnieuw genereren op Hallo fysieke apparaat en werk vervolgens Hallo virtueel apparaat met de nieuwe sleutel Hallo. |Kan niet opnieuw genereren van het virtuele apparaat Hallo. |

## <a name="prerequisites-for-hello-virtual-device"></a>Vereisten voor het virtuele apparaat Hallo
Hallo volgende secties worden de configuratievereisten Hallo voor uw virtuele StorSimple-apparaat. Eerdere toodeploying een virtueel apparaat controleren Hallo [beveiligingsoverwegingen voor het gebruik van een virtueel apparaat](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Azure-vereisten
Voordat u Hallo virtuele apparaat inricht, moet u toomake Hallo voorbereidingen in uw Azure-omgeving te volgen:

* Voor het virtuele apparaat hello, [een virtueel netwerk configureren in Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Als u Premium-opslag gebruikt, moet u een virtueel netwerk maken in een Azure-regio die ondersteuning biedt voor Premium-opslag. Premium-opslagregio Hallo zijn regio's die overeenkomen met toohello rij voor *schijfruimte,* in de lijst met Hallo [Azure-Services per regio](https://azure.microsoft.com/en-us/regions/services).
* Het is aangeraden toouse Hallo standaard DNS-server van Azure in plaats van de naam van uw eigen DNS-server opgeven. Als uw DNS-servernaam niet geldig is of als Hallo DNS-server wordt niet kunnen tooresolve IP-adressen correct is, mislukt het maken van het virtuele apparaat Hallo Hallo.
* Punt-naar-site en site-naar-site zijn optioneel, maar niet vereist. Als u wilt, kunt u deze opties configureren in meer geavanceerde scenario's.
* U kunt maken [Azure Virtual Machines](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (hostservers) in het virtuele netwerk Hallo die Hallo volumes die worden weergegeven door het virtuele apparaat Hallo kunt gebruiken. Deze servers moeten voldoen aan Hallo volgens de vereisten:                             

  * Het moeten virtuele Windows- of Linux-machines zijn waarop de iSCSI-initiatorsoftware is geïnstalleerd.
  * Wordt uitgevoerd in Hallo hetzelfde virtuele netwerk als het virtuele apparaat Hallo.
  * Kan tooconnect toohello iSCSI-doel van het virtuele apparaat Hallo via Hallo interne IP-adres van het virtuele apparaat Hallo worden.
* Zorg ervoor dat u ondersteuning hebt geconfigureerd voor iSCSI- en cloud-verkeer op Hallo hetzelfde virtuele netwerk.

#### <a name="storsimple-requirements"></a>StorSimple-vereisten
Controleer Hallo na updates tooyour Azure StorSimple-service voordat u een virtueel apparaat maakt:

* Voeg [toegang tot control records](storsimple-manage-acrs.md) voor Hallo virtuele machines die worden toobe hostservers voor uw virtuele apparaat.
* Gebruik een [opslagaccount](storsimple-manage-storage-accounts.md#add-a-storage-account) in Hallo dezelfde regio als het virtuele apparaat Hallo. Als u opslagaccounts in andere regio's gebruikt, kan dat leiden tot slechte prestaties. U kunt een Standard of Premium-opslag-account gebruiken met het virtuele apparaat Hallo. Meer informatie over het toocreate een [Standard-opslagaccount](../storage/common/storage-create-storage-account.md) of een [Premium Storage-account](../storage/common/storage-premium-storage.md)
* Gebruik een ander opslagaccount voor het virtuele apparaat maken van Hallo gebruikt voor uw gegevens. Met behulp van Hallo hetzelfde opslagaccount tot slechte prestaties leiden kan.

Zorg ervoor dat er Hallo volgende informatie voordat u begint:

* Uw account voor de klassieke Azure Portal met referenties voor toegang.
* Een kopie van Hallo gegevensversleutelingssleutel van service van uw fysieke apparaat.

## <a name="create-and-configure-hello-virtual-device"></a>Maken en configureren van het virtuele apparaat Hallo
Voordat u deze procedures uitvoert, controleert u of u Hallo hebt voldaan [vereisten voor het virtuele apparaat Hallo](#prerequisites-for-the-virtual-device).

Nadat u hebt gemaakt van een virtueel netwerk, een StorSimple Manager-service hebt geconfigureerd en uw fysieke StorSimple-apparaat geregistreerd bij Hallo-service, kunt u gebruiken Hallo toocreate stappen te volgen en configureren van een virtueel StorSimple-apparaat.

### <a name="step-1-create-a-virtual-device"></a>Stap 1: een virtueel apparaat maken
Volgende stappen toocreate Hallo virtueel StorSimple-apparaat Hallo uitvoeren.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Als Hallo maken van een virtueel apparaat Hallo in deze stap mislukt, mag u geen verbinding toohello Internet hebben. Voor meer informatie gaat te[problemen met Internet](#troubleshoot-internet-connectivity-errors) bij het maken van een virtueel apparaat.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>Stap 2: Configureren en registreren van het virtuele apparaat Hallo
Voordat u deze procedure begint, zorg ervoor dat er een kopie van de gegevensversleutelingssleutel van Hallo-service. Hallo gegevensversleutelingssleutel van service is gemaakt toen u uw eerste StorSimple-apparaat hebt geconfigureerd en u gebruiksaanwijzing toosave zijn in een veilige locatie. Als u een kopie van de gegevensversleutelingssleutel van Hallo-service niet hebt, moet u contact op met Microsoft Support voor hulp.

Hallo tooconfigure stappen te volgen en virtuele StorSimple-apparaat te registeren.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Stap 3: (Optioneel) Wijzig Hallo configuratie-instellingen
Hallo volgende sectie wordt beschreven Hallo configuratie-instellingen voor apparaten die nodig zijn voor Hallo virtuele StorSimple-apparaat als u wilt dat toouse CHAP, StorSimple Snapshot Manager of Hallo Apparaatbeheerder wachtwoord wijzigen.

#### <a name="configure-hello-chap-initiator"></a>Hallo CHAP-initiator configureren
Deze parameter bevat Hallo-referenties die uw virtuele apparaat (doel) verwacht te ontvangen van Hallo initiators (servers) die tooaccess Hallo volumes probeert. Hallo initiators bieden een CHAP-gebruikersnaam en een CHAP-wachtwoord tooidentify zelf tooyour apparaat tijdens de verificatie. Voor gedetailleerde stappen gaat te[CHAP configureren voor uw apparaat](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Hallo CHAP-doel configureren
Deze parameter bevat Hallo referenties in die uw virtuele apparaat gebruikt wanneer een initiator CHAP ingeschakeld wederzijdse of bidirectionele verificatie aanvraagt. Uw virtuele apparaat wordt een gebruikersnaam omgekeerde CHAP en omgekeerde CHAP wachtwoord tooidentify zelf toohello initiator gebruiken tijdens het verificatieproces. De CHAP-doelinstellingen zijn algemene instellingen. Wanneer deze worden toegepast, wordt alle Hallo volumes verbonden toohello virtuele opslagapparaat CHAP-verificatie gebruiken. Voor gedetailleerde stappen gaat te[CHAP configureren voor uw apparaat](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Hallo StorSimple Snapshot Manager wachtwoord configureren
StorSimple Snapshot Manager-software bevindt zich op uw Windows-host en kan beheerders toomanage back-ups van uw StorSimple-apparaat in Hallo vorm van lokale en cloudmomentopnamen.

> [!NOTE]
> Voor het virtuele apparaat hello is uw Windows-host een virtuele machine van Azure.
>
>

Bij het configureren van een apparaat in Hallo StorSimple Snapshot Manager, wordt u gevraagd tooprovide Hallo StorSimple-apparaat IP-adres en het wachtwoord tooauthenticate uw opslagapparaat. Voor gedetailleerde stappen gaat te[wachtwoord StorSimple Snapshot Manager configureren](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Wachtwoord apparaatbeheerder Hallo wijzigen
Wanneer u Hallo Windows PowerShell-interface tooaccess Hallo virtueel apparaat, kunt u vereiste tooenter het beheerderswachtwoord voor een apparaat. Voor Hallo beveiliging van uw gegevens, zijn de vereiste toochange dit wachtwoord voordat Hallo virtueel apparaat kan worden gebruikt. Voor gedetailleerde stappen gaat te[wachtwoord apparaatbeheerder configureren](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-virtual-device"></a>Toohello virtueel apparaat op afstand verbinding maken
Externe toegang tooyour virtuele apparaat via Windows PowerShell-interface Hallo is niet standaard ingeschakeld. U moet extern beheer op het virtuele apparaat Hallo tooenable eerst en daarna inschakelen op Hallo-client die wordt gebruikt tooaccess uw virtuele apparaat.

Hallo in twee stappen proces tooconnect wordt op afstand hieronder beschreven.

### <a name="step-1-configure-remote-management"></a>Stap 1: extern beheer configureren
Volgende stappen tooconfigure extern beheer voor virtuele StorSimple-apparaat Hallo uitvoeren.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>Stap 2: Extern toegang tot het virtuele apparaat Hallo
Nadat u extern beheer op de pagina configuratie Hallo StorSimple-apparaat hebt ingeschakeld, kunt u Windows PowerShell voor externe toegang tooconnect toohello virtuele apparaat vanaf een andere virtuele machine in hello gebruiken hetzelfde virtuele netwerk; bijvoorbeeld, u verbinding kunt maken van de host Hallo VM die u hebt geconfigureerd en tooconnect iSCSI gebruikt. In de meeste implementaties wordt u al hebt geopend een openbaar eindpunt tooaccess uw virtuele machine die u gebruiken kunt voor toegang tot het virtuele apparaat Hallo-host.

> [!WARNING]
> **Voor een betere beveiliging wordt aangeraden dat u HTTPS gebruikt bij het verbinden van toohello eindpunten en verwijder vervolgens de Hallo eindpunten nadat u uw externe PowerShell-sessie hebt voltooid.**
>
>

U moet volgen Hallo procedures in [tooyour StorSimple-apparaat extern verbinding maakt](storsimple-remote-connect.md) tooset van externe toegang tot uw virtuele apparaat.

## <a name="connect-directly-toohello-virtual-device"></a>Maak rechtstreeks verbinding toohello virtueel apparaat
U kunt ook rechtstreeks verbinding gemaakt toohello virtueel apparaat. Als u tooconnect wilt direct toohello virtuele apparaat vanaf een andere computer buiten het virtuele netwerk Hallo of buiten Hallo Microsoft Azure-omgeving, moet u extra eindpunten toocreate zoals beschreven in Hallo procedure te volgen.

Hallo stappen toocreate een openbaar eindpunt te volgen op het virtuele apparaat Hallo uitvoeren.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

Het is raadzaam dat u verbinding vanaf een andere virtuele machine in Hallo dezelfde virtuele maakt netwerk omdat hierdoor Hallo aantal openbare eindpunten in het virtuele netwerk minimaliseert. Wanneer u deze methode gebruikt, kunt u gewoon toohello virtuele machine verbinding via een extern bureaublad-sessie en vervolgens configureren voor gebruik dat de virtuele machine net als andere Windows-clients op een lokale netwerk. U hoeft niet tooappend Hallo openbare poortnummer omdat Hallo poort al bekend.

## <a name="work-with-hello-storsimple-virtual-device"></a>Werken met Hallo virtuele StorSimple-apparaat
Nu dat u hebt gemaakt en geconfigureerd Hallo virtuele StorSimple-apparaat, bent u klaar toostart ermee te werken. U kunt werken met volumecontainers, volumes en back-upbeleid op een virtueel apparaat net zoals u zou op een fysieke StorSimple-apparaat doen; Hallo enige verschil is dat u toomake ervoor dat u Hallo virtueel apparaat in de lijst van uw apparaat selecteert. Raadpleeg te[hello StorSimple Manager-service toomanage een virtueel apparaat gebruiken](storsimple-manager-service-administration.md) voor stapsgewijze instructies voor verschillende voor het virtuele apparaat Hallo beheertaken Hallo.

Hallo volgende secties worden enkele van Hallo verschillen die u tegenkomt wanneer u werkt met Hallo virtueel apparaat.

### <a name="maintain-a-storsimple-virtual-device"></a>Een virtueel StorSimple-apparaat onderhouden
Omdat het een apparaat alleen uit software, onderhoud voor het virtuele apparaat Hallo is minimaal wanneer toomaintenance voor het fysieke apparaat Hallo vergeleken. Hebt u Hallo volgende opties:

* **Software-updates** – u kunt Hallo datum weergeven waarop Hallo software samen met statusberichten update het laatst is bijgewerkt. U kunt Hallo **updates scannen** knop onderaan Hallo Hallo pagina tooperform handmatig als u wilt dat toocheck op nieuwe updates. Als er updates beschikbaar zijn, klikt u op **Updates installeren** tooinstall. Omdat er slechts één interface op het virtuele apparaat hello, betekent dit dat er een korte serviceonderbreking wanneer updates worden toegepast. Hallo virtueel apparaat afsluiten en opnieuw opstarten (indien nodig) tooapply eventuele updates die zijn uitgebracht. Voor een stapsgewijze procedure gaat te[uw apparaat bijwerken](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Ondersteuningspakket** : U kunt maken en uploaden van een pakket toohelp voor ondersteuning van Microsoft Support oplossen van problemen met uw virtuele apparaat. Voor een stapsgewijze procedure gaat te[maken en beheren van een ondersteuningspakket](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Opslagaccounts voor een virtueel apparaat
Storage-accounts worden gemaakt voor gebruik door Hallo StorSimple Manager-service, Hallo virtueel apparaat en het fysieke apparaat Hallo. Wanneer u uw opslagaccounts maakt, wordt aangeraden dat u een regio-id in Hallo beschrijvende naam toohelp Zorg ervoor dat Hallo regio consistent wordt gebruikt in alle systeemonderdelen Hallo. Voor een virtueel apparaat is het belangrijk dat alle Hallo onderdelen zich in dezelfde regio tooprevent prestatieproblemen met Hallo.

Voor een stapsgewijze procedure gaat te[een opslagaccount toevoegen](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>Een virtueel StorSimple-apparaat deactiveren
Een virtueel apparaat deactiveren en worden verwijderd Hallo VM Hallo-resources die zijn gemaakt tijdens het inrichten. Nadat het virtuele apparaat Hallo is gedeactiveerd, kan niet worden hersteld tooits eerdere status. Voordat u Hallo virtueel apparaat deactiveert, zorg ervoor dat toostop of verwijderen van clients en hosts die afhankelijk zijn.

Als een virtueel apparaat deactiveert, resulteert in Hallo van de volgende activiteiten:

* Hallo virtuele apparaat wordt verwijderd.
* Hallo OS-schijf- en gegevensschijven die zijn gemaakt voor het virtuele apparaat Hallo worden verwijderd.
* Hallo gehoste service en virtuele netwerken die zijn gemaakt tijdens het inrichten, blijven behouden. Als u deze niet gebruikt, moet u ze handmatig verwijderen.
* Cloudmomentopnamen die zijn gemaakt voor het virtuele apparaat Hallo worden bewaard.

Voor een stapsgewijze procedure gaat te[deactiveren en verwijderen van uw StorSimple-apparaat](storsimple-deactivate-and-delete-device.md).

Zodra de Hallo virtueel apparaat wordt weergegeven als gedeactiveerd op pagina Hallo StorSimple Manager-service, kunt u Hallo virtueel apparaat verwijderen uit de lijst met apparaten op Hallo **apparaten** pagina.

### <a name="start-stop-and-restart-a-virtual-device"></a>Een virtueel apparaat starten, stoppen en opnieuw opstarten
In tegenstelling tot Hallo fysieke StorSimple-apparaat is er geen stroom / uit-knop toopush op een virtueel StorSimple-apparaat. Echter, kunnen er gevallen waarbij u toostop nodig hebt en Hallo virtueel apparaat opnieuw opstarten. Sommige updates moet bijvoorbeeld die Hallo die VM zijn toofinish Hallo updateproces opnieuw gestart. Hallo gemakkelijkste manier waarop u toostart, stoppen en opnieuw opstarten van een virtueel apparaat is toouse Hallo beheerconsole voor virtuele Machines.

Wanneer u bekijkt hello beheerconsole in, is het Hallo virtueel Apparaatstatus **met** omdat deze standaard wordt gestart nadat deze is gemaakt. U kunt virtuele machines te allen tijde starten, stoppen en opnieuw opstarten.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Toofactory beginwaarden
Als u besluit dat u zojuist hebt wilt toostart via met uw virtuele apparaat, deactiveert en verwijdert en vervolgens een nieuwe maken. Net als bij uw fysieke apparaat opnieuw wordt ingesteld, wordt uw nieuwe virtuele apparaat nog geen updates geïnstalleerd. Zorg ervoor dat toocheck voor updates voordat u deze gebruikt.

## <a name="fail-over-toohello-virtual-device"></a>Failover toohello virtueel apparaat
Noodherstel (DR) is een van de belangrijkste scenario's voor een Hallo die Hallo virtueel apparaat is ontworpen voor StorSimple. In dit scenario Hallo fysieke StorSimple-apparaat of zelfs het gehele datacenter mogelijk niet beschikbaar. Gelukkig kunt u een virtueel apparaat toorestore bewerkingen in een andere locatie. Tijdens de DR, Hallo volumecontainers van het bronvolume Hallo eigendom wijzigen en zijn overgedragen toohello van het virtuele apparaat. Hallo vereisten voor herstel na Noodgevallen zijn dat Hallo virtueel apparaat is gemaakt en geconfigureerd, alle Hallo volumes binnen Hallo volumecontainer offline is gezet en Hallo volumecontainer een bijbehorende heeft cloudmomentopname.

> [!NOTE]
> * Wanneer u een virtueel apparaat als secundair apparaat Hallo voor herstel na Noodgevallen, houd er rekening mee dat Hallo 8010 30 TB Standard-opslag heeft en de 8020 64 TB aan Premium-opslag. Hallo hogere capaciteit 8020 virtueel apparaat is mogelijk beter geschikt voor een herstel na noodgevallen.
> * U kunt geen failover of klonen vanaf een apparaat met bijwerken 2 tooa apparaat vóór Update 1 software die wordt uitgevoerd. U kunt echter wel een apparaat met Update 2 tooa apparaat met Update 1 (1.1 of 1.2) een failover
>
>

Voor een stapsgewijze procedure gaat te[failover tooa virtueel apparaat](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-hello-virtual-device"></a>Uitschakelen of verwijderen van het virtuele apparaat Hallo
Als u eerder hebt geconfigureerd en gebruikt een virtueel StorSimple apparaat maar nu wil toostop lopen de compute-kosten voor het gebruik ervan, kunt u Hallo virtueel apparaat afsluiten. Hallo virtueel apparaat afsluiten wordt het besturingssysteem en gegevensschijven in de opslag niet verwijderd. Kosten doorberekend voor uw abonnement kosten meer, maar de opslagkosten voor Hallo OS en de gegevensschijven blijven.

Als u verwijdert of Hallo virtueel apparaat uitschakelt, wordt deze weergegeven als **Offline** op Hallo apparaten pagina Hallo StorSimple Manager-service. U kunt kiezen toodeactivate of Hallo apparaat verwijderen als u ook toodelete Hallo back-ups die zijn gemaakt door Hallo virtueel apparaat. Zie [Een StorSimple-apparaat deactiveren en verwijderen](storsimple-deactivate-and-delete-device.md) voor meer informatie.

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Problemen met internetverbinding oplossen
Als er geen toohello verbinding met Internet, wordt tijdens het maken van een virtueel apparaat Hallo Hallo maken stap mislukt. tootroubleshoot als is Hallo is mislukt vanwege de verbinding met Internet, voert u stappen te volgen in de klassieke Azure-portal Hallo Hallo:

1. Maak een virtuele Windows Server 2012-machine in Azure. Deze virtuele machine moet gebruiken Hallo hetzelfde opslagaccount, VNet en subnet gebruikt door uw virtuele apparaat. Als u al een bestaande Windows Server-host in met behulp van Azure Hallo hetzelfde opslagaccount, Vnet en subnet, kunt u ook gebruiken deze tootroubleshoot Hallo verbinding met Internet.
2. Meld u aan externe bij Hallo virtuele machine is gemaakt in de voorgaande stap Hallo.
3. Open een opdrachtvenster in Hallo virtuele machine (Win + R en typ `cmd`).
4. Hallo na cmd Hallo opdrachtprompt worden uitgevoerd.

    `nslookup windows.net`
5. Als `nslookup` mislukt, en vervolgens de Internet-verbindingsfout verhindert Hallo virtueel apparaat registreren toohello StorSimple Manager-service.
6. Wijzig Hallo vereist tooyour virtueel netwerk tooensure die Hallo virtueel apparaat is kunnen tooaccess Azure sites zoals 'windows.net'.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[hello StorSimple Manager-service toomanage een virtueel apparaat gebruiken](storsimple-manager-service-administration.md).
* Begrijpen hoe te[een StorSimple-volume herstelt vanuit een back-upset](storsimple-restore-from-backup-set.md).
