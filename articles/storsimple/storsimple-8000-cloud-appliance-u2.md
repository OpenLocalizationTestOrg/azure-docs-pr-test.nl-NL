---
title: aaaStorSimple Cloud toestel Update 3 | Microsoft Docs
description: Informatie over hoe toocreate, implementeren en beheren van een StorSimple-Cloud-apparaat in een Microsoft Azure virtual network. (Geldt tooStorSimple Update 3 en hoger).
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Een StorSimple-cloudapparaat implementeren en beheren in Azure (Update 3 en hoger)

## <a name="overview"></a>Overzicht

Hallo StorSimple 8000 Series Cloud toestel is een extra functionaliteit die wordt geleverd met uw Microsoft Azure StorSimple-oplossing. Hallo StorSimple Cloud toestel wordt uitgevoerd op een virtuele machine in een virtueel netwerk van Microsoft Azure en kunt u tooback up- en kloon-gegevens van uw hosts.

In dit artikel beschrijft Hallo stapsgewijs toodeploy en beheren van een StorSimple-Cloud-toestel in Azure. Wanneer u dit artikel hebt gelezen:

* Begrijpen hoe Hallo cloud toestel verschilt van het fysieke apparaat Hallo.
* Kan toocreate zijn en Hallo cloud toestel configureren.
* Sluit toohello cloud toestel.
* Meer informatie over hoe toowork Hello toestel cloud.

Deze zelfstudie geldt tooall hello StorSimple Cloud apparaten met Update 3 en hoger.

#### <a name="cloud-appliance-model-comparison"></a>Vergelijking van cloudapparaatmodellen

Hallo StorSimple Cloud toestel is beschikbaar in twee modellen standard 8010 (voorheen bekend als Hallo 1100) en de premium 8020 (geïntroduceerd bij Update 2). Hallo volgende tabel geeft een vergelijking van de twee modellen Hallo.

| Apparaatmodel | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Maximale capaciteit** |30 TB |64 TB |
| **Azure VM** |Standard_A3 (4 kerngeheugens, 7 GB geheugen)| Standard_DS3 (4 kerngeheugens, 14 GB geheugen)|
| **Beschikbaarheid in regio’s** |Alle Azure-regio's |Azure-regio's waar ondersteuning wordt geboden voor Premium Storage en Azure-VM’s met DS3<br></br>Gebruik [deze lijst](https://azure.microsoft.com/regions/services/) toosee als beide **virtuele Machines > DS-serie** en **opslag > schijfruimte** beschikbaar zijn in uw regio. |
| **Opslagtype** |Maakt gebruik van Azure Standard-opslag voor lokale schijven<br></br> Meer informatie over hoe te[een Standard-opslagaccount maken](../storage/common/storage-create-storage-account.md) |Maakt gebruik van Azure Premium Storage voor lokale schijven<sup>2</sup> <br></br>Meer informatie over hoe te[een Premium Storage-account maken](../storage/common/storage-premium-storage.md) |
| **Richtlijnen voor de workload** |Bestanden ophalen uit back-ups op itemniveau |Ontwikkelings- en testscenario’s voor cloudapparaten <br></br>Lage latentie en workloads met hogere prestaties<br></br>Secundair apparaat voor herstel na noodgevallen |

<sup>1</sup> *voorheen bekend als Hallo 1100*.

<sup>2</sup> *beide 8010 Hallo en 8020 Azure Standard-opslag gebruiken voor Hallo cloud laag. Hallo verschil zit hem alleen in de lokale laag Hallo binnen Hallo apparaat*.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Hoe Hallo cloud toestel verschilt van het fysieke apparaat Hallo

Hallo StorSimple Cloud toestel is een softwarematige versie van StorSimple die wordt uitgevoerd op één knooppunt in een Microsoft Azure virtuele Machine. Hallo cloud toestel ondersteunt herstel na noodgevallen waarbij uw fysieke apparaat niet beschikbaar is. Hallo cloud toestel is geschikt voor gebruik in op itemniveau voor het ophalen van de back-ups op premises herstel na noodgevallen en scenario's voor ontwikkeling en tests.

#### <a name="differences-from-hello-physical-device"></a>Verschillen met het fysieke apparaat Hallo

Hallo bevat volgende tabel enkele belangrijke verschillen tussen Hallo StorSimple Cloud toestel en fysieke Hallo StorSimple-apparaat.

|  | Fysiek apparaat | Cloudapparaat |
| --- | --- | --- |
| **Locatie** |Bevindt zich in Hallo datacenter. |Wordt uitgevoerd in Azure. |
| **Netwerkinterfaces** |Heeft zes netwerkinterfaces: DATA 0 t/m DATA 5. |Heeft slechts één netwerkinterface: DATA 0 |
| **Registratie** |Geregistreerd tijdens de stap in de eerste configuratie Hallo. |Registratie is een afzonderlijke taak. |
| **Gegevensversleutelingssleutel van service** |Opnieuw genereren op Hallo fysieke apparaat en werk vervolgens Hallo cloud toestel met Hallo nieuwe sleutel. |Kan niet opnieuw genereren van Hallo cloud toestel. |
| **Ondersteunde volumetypen** |Ondersteunt zowel lokaal vastgemaakte als gelaagde volumes. |Ondersteunt alleen gelaagde volumes. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Vereisten voor Hallo cloud toestel

Hallo volgende secties worden de configuratievereisten Hallo voor uw StorSimple-Cloud-toestel. Voordat u een cloud-apparaat implementeert, bekijk Hallo beveiligingsoverwegingen voor het gebruik van een cloud-apparaat.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Azure-vereisten

Voordat u Hallo cloud apparaat inricht, moet u toomake Hallo voorbereidingen in uw Azure-omgeving te volgen:

* Zorg ervoor dat er een fysiek StorSimple-apparaat uit de 8000-serie (model 8100 of 8600) is geïmplementeerd en wordt uitgevoerd in uw datacenter. Registreer dit apparaat bij dezelfde Apparaatbeheer StorSimple-service die u van plan bent Hallo toocreate een StorSimple Cloud toestel voor.
* Voor Hallo cloud toestel, [een virtueel netwerk configureren in Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Als u Premium-opslag gebruikt, moet u een virtueel netwerk maken in een Azure-regio die ondersteuning biedt voor Premium-opslag. Premium-opslagregio Hallo zijn regio's die overeenkomen met toohello rij voor schijfopslag in Hallo [lijst met Azure-Services per regio](https://azure.microsoft.com/regions/services/).
* Het is raadzaam dat u Hallo standaard DNS-server van Azure in plaats van de naam van uw eigen DNS-server opgeven. Als uw DNS-servernaam niet geldig is of als Hallo DNS-server wordt niet kunnen tooresolve IP-adressen correct is, mislukt het maken van Hallo van Hallo cloud toestel.
* Punt-naar-site en site-naar-site zijn optioneel, maar niet vereist. Als u wilt, kunt u deze opties configureren in meer geavanceerde scenario's.
* U kunt maken [Azure Virtual Machines](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (hostservers) in het virtuele netwerk Hallo die Hallo volumes die worden weergegeven door Hallo cloud toestel kunt gebruiken. Deze servers moeten voldoen aan Hallo volgens de vereisten:

  * Het moeten virtuele Windows- of Linux-machines zijn waarop de iSCSI-initiatorsoftware is geïnstalleerd.
  * Wordt uitgevoerd in Hallo hetzelfde virtuele netwerk als Hallo cloud toestel.
  * Niet kunnen tooconnect toohello iSCSI-doel van Hallo cloud toestel via Hallo interne IP-adres van het Hallo-cloud-apparaat.
  * Zorg ervoor dat u ondersteuning hebt geconfigureerd voor iSCSI- en cloud-verkeer op Hallo hetzelfde virtuele netwerk.

#### <a name="storsimple-requirements"></a>StorSimple-vereisten

Controleer Hallo na updates tooyour Apparaatbeheer StorSimple-service voordat u een cloud-apparaat maakt:

* Voeg [toegang tot control records](storsimple-8000-manage-acrs.md) voor Hallo VM's die momenteel toobe Hallo-hostservers voor uw toestel cloud.
* Gebruik een [opslagaccount](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) in Hallo dezelfde regio bevinden als Hallo cloud toestel. Als u opslagaccounts in andere regio's gebruikt, kan dat leiden tot slechte prestaties. U kunt een Standard of Premium-opslag-account gebruiken met Hallo cloud toestel. Meer informatie over het toocreate een [Standard-opslagaccount](../storage/common/storage-create-storage-account.md) of een [Premium Storage-account](../storage/common/storage-premium-storage.md)
* Gebruik een ander opslagaccount voor het maken van de cloud toestel van Hallo gebruikt voor uw gegevens. Met behulp van Hallo hetzelfde opslagaccount tot slechte prestaties leiden kan.

Zorg ervoor dat er Hallo volgende informatie voordat u begint:

* Uw account voor Azure Portal met referenties voor toegang.
* Een kopie van Hallo gegevensversleutelingssleutel van service van uw fysieke apparaat geregistreerd toohello Apparaatbeheer StorSimple-service.

## <a name="create-and-configure-hello-cloud-appliance"></a>Maak en configureer Hallo cloud toestel

Voordat u deze procedures uitvoert, controleert u of u Hallo hebt voldaan [vereisten voor Hallo cloud toestel](#prerequisites-for-the-cloud-appliance).

Hallo te volgen stappen toocreate een StorSimple-apparaat met Cloud uitvoeren.

### <a name="step-1-create-a-cloud-appliance"></a>Stap 1: Een cloudapparaat maken

Volgende stappen toocreate hello StorSimple Cloud toestel Hallo uitvoeren.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

Als Hallo maken van Hallo cloud toestel in deze stap mislukt, mag u geen verbinding toohello Internet hebben. Voor meer informatie gaat te[problemen met Internet](#troubleshoot-internet-connectivity-errors) bij het maken van een cloud-apparaat.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>Stap 2: Configureren en registreren Hallo cloud toestel

Voordat u deze procedure begint, zorg ervoor dat er een kopie van de gegevensversleutelingssleutel van Hallo-service. Hallo service gegevensversleutelingssleutel wordt gemaakt wanneer u uw eerste fysieke StorSimple-apparaat bij Hallo StorSimple-apparaat Manager-service geregistreerd. U zou gebruiksaanwijzing toosave in een veilige locatie. Als u een kopie van de gegevensversleutelingssleutel van Hallo-service niet hebt, moet u contact op met Microsoft Support voor hulp.

Hallo tooconfigure stappen te volgen en uw StorSimple-Cloud-apparaat registeren.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Stap 3: (Optioneel) Wijzig Hallo configuratie-instellingen

Hallo volgende sectie wordt beschreven Hallo configuratie-instellingen voor apparaten die nodig zijn voor Hallo StorSimple Cloud toestel als u toouse CHAP, StorSimple Snapshot Manager wilt of wachtwoord apparaatbeheerder Hallo wijzigt.

#### <a name="configure-hello-chap-initiator"></a>Hallo CHAP-initiator configureren

Deze parameter bevat Hallo-referenties die uw cloud-apparaat (doel) verwacht te ontvangen van Hallo initiators (servers) die tooaccess Hallo volumes probeert. Hallo initiators bieden een CHAP-gebruikersnaam en een CHAP-wachtwoord tooidentify zelf tooyour apparaat tijdens de verificatie. Voor gedetailleerde stappen gaat te[CHAP configureren voor uw apparaat](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Hallo CHAP-doel configureren

Deze parameter bevat Hallo referenties in die uw toestel cloud gebruikt als een initiator CHAP ingeschakeld wederzijdse of bidirectionele-verificatie vraagt. Uw toestel cloud gebruikt een gebruikersnaam omgekeerde CHAP en omgekeerde CHAP wachtwoord tooidentify zelf toohello initiator tijdens het verificatieproces.

> [!NOTE]
> De CHAP-doelinstellingen zijn algemene instellingen. Wanneer deze instellingen worden toegepast, verbonden alle Hallo volumes toohello cloud toestel gebruik CHAP-verificatie.

Voor gedetailleerde stappen gaat te[CHAP configureren voor uw apparaat](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Hallo StorSimple Snapshot Manager wachtwoord configureren

StorSimple Snapshot Manager-software bevindt zich op uw Windows-host en kan beheerders toomanage back-ups van uw StorSimple-apparaat in Hallo vorm van lokale en cloudmomentopnamen.

> [!NOTE]
> Voor Hallo cloud toestel is uw Windows-host een virtuele machine van Azure.

Wanneer een apparaat wordt geconfigureerd in Hallo StorSimple Snapshot Manager, wordt u gevraagd tooprovide Hallo StorSimple-apparaat IP-adres en het wachtwoord tooauthenticate uw opslagapparaat. Voor gedetailleerde stappen gaat te[wachtwoord StorSimple Snapshot Manager configureren](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Wachtwoord apparaatbeheerder Hallo wijzigen

Wanneer u Hallo Windows PowerShell-interface tooaccess Hallo cloud toestel, bent u vereiste tooenter het beheerderswachtwoord voor een apparaat. Voor Hallo beveiliging van uw gegevens, moet u dit wachtwoord wijzigen voordat Hallo cloud apparaat kan worden gebruikt. Voor gedetailleerde stappen gaat te[wachtwoord apparaatbeheerder configureren](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-cloud-appliance"></a>Toohello cloud apparaat op afstand verbinding maken

Externe toegang tooyour cloud toestel via Hallo Windows PowerShell-interface is niet standaard ingeschakeld. U moet eerst extern beheer op Hallo cloud toestel inschakelen en vervolgens op Hallo client tooaccess Hallo cloud toestel gebruikt.

Hallo na de procedure in twee stappen wordt beschreven hoe tooconnect op afstand tooyour cloud toestel.

### <a name="step-1-configure-remote-management"></a>Stap 1: extern beheer configureren

Volgende stappen tooconfigure extern beheer voor uw StorSimple Cloud toestel Hallo uitvoeren.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>Stap 2: Extern toegang tot Hallo cloud toestel

Nadat u extern beheer op Hallo cloud toestel inschakelen, gebruikt u Windows PowerShell voor externe toegang tooconnect toohello toestel vanuit een andere virtuele machine in Hallo hetzelfde virtuele netwerk. Bijvoorbeeld, u verbinding kunt maken van de host Hallo VM die u hebt geconfigureerd en tooconnect iSCSI gebruikt. In de meeste implementaties opent u een openbaar eindpunt tooaccess uw virtuele machine die u gebruiken kunt voor toegang tot Hallo cloud toestel-host.

> [!WARNING]
> **Voor een betere beveiliging wordt aangeraden dat u HTTPS gebruikt bij het verbinden van toohello eindpunten en verwijder vervolgens de Hallo eindpunten nadat u uw externe PowerShell-sessie hebt voltooid.**

U moet volgen Hallo procedures in [tooyour StorSimple-apparaat extern verbinding maakt](storsimple-8000-remote-connect.md) tooset van externe toegang tot uw toestel cloud.

## <a name="connect-directly-toohello-cloud-appliance"></a>Maak rechtstreeks verbinding toohello cloud toestel

U kunt ook rechtstreeks verbinding gemaakt toohello cloud toestel. tooconnect direct toohello cloud toestel vanaf een andere computer buiten Hallo virtueel netwerk of buiten Hallo Microsoft Azure-omgeving, moet u extra eindpunten maken.

Volgende stappen toocreate een openbaar eindpunt op Hallo cloud toestel Hallo uitvoeren.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

Het is raadzaam dat u verbinding vanaf een andere virtuele machine in Hallo dezelfde virtuele maakt netwerk omdat hierdoor Hallo aantal openbare eindpunten in het virtuele netwerk minimaliseert. In dit geval toohello virtuele machine verbinding via een extern bureaublad-sessie en configureer vervolgens de virtuele machine voor gebruik net als andere Windows-clients op een lokale netwerk. U hoeft niet tooappend Hallo openbare poortnummer omdat Hallo poort al bekend is.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>Werken met Hallo StorSimple Cloud toestel

Nu dat u hebt gemaakt en geconfigureerd Hallo StorSimple Cloud toestel, bent u klaar toostart ermee te werken. U kunt werken met volumecontainers, volumes en back-upbeleid op een cloudapparaat net zoals u op een fysiek StorSimple-apparaat zou doen. Hallo enige verschil is dat u toomake ervoor dat u Hallo cloud apparaat in de lijst van uw apparaat selecteert. Raadpleeg te[hello StorSimple Apparaatbeheer service toomanage een cloud-apparaat gebruiken](storsimple-8000-manager-service-administration.md) voor stapsgewijze instructies voor verschillende voor Hallo cloud toestel beheertaken Hallo.

Hallo volgende secties worden enkele van Hallo verschillen die u tegenkomt wanneer u werkt met Hallo cloud toestel.

### <a name="maintain-a-storsimple-cloud-appliance"></a>Een StorSimple-cloudapparaat onderhouden

Omdat het een apparaat alleen uit software, onderhoud voor Hallo cloud toestel is minimaal wanneer toomaintenance voor het fysieke apparaat Hallo vergeleken.

Een cloudapparaat kan niet worden bijgewerkt. Hallo meest recente versie van software toocreate een nieuw cloud toestel gebruiken.


### <a name="storage-accounts-for-a-cloud-appliance"></a>Opslagaccounts voor een cloudapparaat

Storage-accounts worden gemaakt voor gebruik door Hallo StorSimple-apparaat Manager-service, Hallo cloud toestel en Hallo fysieke apparaat. Wanneer u uw opslagaccounts maakt, wordt u aangeraden een regio-id in de beschrijvende naam hello te gebruiken. Dit zorgt ervoor dat Hallo regio consistent wordt gebruikt in alle systeemonderdelen Hallo is. Voor een cloud-apparaat, is het belangrijk dat alle Hallo-onderdelen in Hallo zijn dezelfde regio tooprevent prestatieproblemen kunnen voordoen.

Voor een stapsgewijze procedure gaat te[een opslagaccount toevoegen](storsimple-8000-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-cloud-appliance"></a>Een StorSimple-cloudapparaat deactiveren

Wanneer u een cloud-apparaat deactiveert, worden Hallo VM en Hallo-resources die zijn gemaakt tijdens het inrichten Hallo actie verwijderd. Nadat Hallo cloud toestel is gedeactiveerd, kan niet worden hersteld tooits eerdere status. Voordat u Hallo cloud apparaat deactiveert, zorg ervoor dat toostop of te verwijderen van clients en hosts die afhankelijk zijn.

Een cloud-apparaat deactiveren resulteert in het Hallo van de volgende activiteiten:

* Hallo cloud toestel is verwijderd.
* Hallo OS schijf- en gegevensschijven die zijn gemaakt voor Hallo cloud apparaat worden verwijderd.
* Hallo gehoste service en virtuele netwerken die zijn gemaakt tijdens het inrichten, blijven behouden. Als u deze niet gebruikt, moet u ze handmatig verwijderen.
* Cloudmomentopnamen die zijn gemaakt voor Hallo cloud toestel worden bewaard.

Voor een stapsgewijze procedure gaat te[deactiveren en verwijderen van uw StorSimple-apparaat](storsimple-8000-deactivate-and-delete-device.md).

Zodra de Hallo cloud toestel wordt weergegeven als gedeactiveerd op de blade Hallo Apparaatbeheer StorSimple-service, kunt u Hallo cloud toestel verwijderen uit de lijst met apparaten op Hallo **apparaten** blade.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>Een cloudapparaat starten, stoppen en opnieuw opstarten
In tegenstelling tot Hallo fysieke StorSimple-apparaat is er geen stroom / uit-knop toopush op een StorSimple-apparaat met Cloud. Echter, kunnen er gevallen waarbij u toostop nodig hebt en Hallo cloud toestel opnieuw opstarten.

Hallo gemakkelijkste manier waarop u toostart, stoppen en opnieuw opstarten van een cloud-toestel is via Hallo service-blade virtuele Machines. Ga Hallo Virtual machine-service. Hallo-lijst van virtuele machines, identificeren Hallo VM bijbehorende tooyour cloud toestel (dezelfde naam), en klik op Hallo VM-naam. Wanneer u uw virtuele machine-blade bekijkt, is het Hallo cloud toestel status **met** omdat deze standaard wordt gestart nadat deze is gemaakt. U kunt virtuele machines te allen tijde starten, stoppen en opnieuw opstarten.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Toofactory beginwaarden
Als u besluit dat u wilt dat toostart via met uw toestel cloud, deactiveren en verwijderen en een nieuwe maken.

## <a name="fail-over-toohello-cloud-appliance"></a>Toohello cloud toestel failover
Herstel na noodgeval (DR) is een Hallo belangrijke scenario's die Hallo StorSimple Cloud toestel is ontworpen voor. In dit scenario Hallo fysieke StorSimple-apparaat of zelfs het gehele datacenter mogelijk niet beschikbaar. Gelukkig kunt u een cloud toestel toorestore bewerkingen in een andere locatie. Tijdens de DR, Hallo volumecontainers van het bronvolume Hallo eigendom wijzigen en overgebrachte toohello cloud toestel zijn.

Hallo-vereisten voor herstel na Noodgevallen zijn:

* Hallo cloud toestel is gemaakt en geconfigureerd.
* Alle Hallo volumes binnen Hallo volumecontainer zijn offline.
* Hallo volumecontainer waarin u een failover uitvoert, heeft een bijbehorende cloudmomentopname.

> [!NOTE]
> * Wanneer u een cloud-apparaat als secundair apparaat Hallo voor herstel na Noodgevallen, houd er rekening mee dat Hallo 8010 30 TB Standard-opslag heeft en de 8020 64 TB aan Premium-opslag. Hallo hogere capaciteit 8020 cloud toestel is mogelijk beter geschikt voor een herstel na noodgevallen.

Voor een stapsgewijze procedure gaat te[tooa cloud toestel failover](storsimple-8000-device-failover-cloud-appliance.md).

## <a name="delete-hello-cloud-appliance"></a>Hallo cloud toestel verwijderen
Als u eerder hebt geconfigureerd en gebruikt een StorSimple-apparaat met Cloud maar nu wil toostop lopen de compute-kosten voor het gebruik ervan, moet u Hallo cloud toestel stoppen. Stoppen Hallo cloud toestel deallocates Hallo VM. Met deze actie wordt voorkomen dat de kosten voor uw abonnement oplopen. Hallo opslagkosten voor Hallo OS en de gegevensschijven blijven echter.

alle Hallo toostop kosten, moet u Hallo cloud toestel verwijderen. toodelete hello back-ups gemaakt door Hallo cloud toestel, die u kunt deactiveren of verwijderen Hallo-apparaat. Zie [Een StorSimple-apparaat deactiveren en verwijderen](storsimple-8000-deactivate-and-delete-device.md) voor meer informatie.

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Problemen met internetverbinding oplossen
Tijdens het maken van een cloud-toestel Hallo als er geen toohello verbinding met Internet, Hallo maken stap mislukt. verbindingsfouten tootroubleshoot Internet, voert u Hallo stappen te volgen in hello Azure-portal:

1. [Maak een virtuele Windows Server 2012-machine in Azure](/articles/virtual-machines/windows/quick-create-portal.md). Deze virtuele machine moet gebruiken hetzelfde opslagaccount en VNet subnet gebruikt door uw toestel cloud Hallo. Als er een bestaande Windows Server-host in met behulp van Azure Hallo hetzelfde opslagaccount en VNet subnet, kunt u ook gebruiken deze tootroubleshoot Hallo verbinding met Internet.
2. Meld u aan externe bij Hallo virtuele machine is gemaakt in de voorgaande stap Hallo.
3. Open een opdrachtvenster in Hallo virtuele machine (Win + R en typ `cmd`).
4. Hallo na cmd Hallo opdrachtprompt worden uitgevoerd.

    `nslookup windows.net`
5. Als `nslookup` mislukt, en vervolgens de Internet-verbindingsfout houdt Hallo cloud toestel toohello Apparaatbeheer StorSimple-service wordt geregistreerd.
6. Aanbrengen Hallo vereist tooyour virtueel netwerk tooensure die Hallo cloud toestel is kunnen tooaccess Azure sites zoals _windows.net_.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[hello StorSimple Apparaatbeheer service toomanage een cloud-apparaat gebruiken](storsimple-8000-manager-service-administration.md).
* Begrijpen hoe te[een StorSimple-volume herstelt vanuit een back-upset](storsimple-8000-restore-from-backup-set-u2.md).
