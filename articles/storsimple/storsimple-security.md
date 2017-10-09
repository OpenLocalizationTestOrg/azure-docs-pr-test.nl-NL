---
title: aaaStorSimple 8000 series beveiliging | Microsoft Docs
description: Hierin wordt beschreven Hallo beveiliging en privacy-functies die uw StorSimple-service, het apparaat en de on-premises en in de cloud Hallo gegevens beveiligen.
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: a21d19c6-83b4-418c-9380-323bb9f76612
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/03/2016
ms.author: v-sharos
ms.openlocfilehash: b9e6c8b3371b4039549972cf507052312ed7cdaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-security-and-data-protection"></a>StorSimple-beveiliging en gegevensbescherming
## <a name="overview"></a>Overzicht
Beveiliging is van groot belang voor iedereen die met een nieuwe technologie werken gaat met name wanneer Hallo technologie met vertrouwelijke of persoonlijke gegevens gebruikt. Als u verschillende technologieën evalueren, moet u rekening houden met verhoogde risico's en -kosten voor gegevensbeveiliging. Microsoft Azure StorSimple biedt een beveiligings- en privacy-oplossing voor gegevensbeveiliging, tooensure helpen: 

* **Vertrouwelijkheid** : alleen geautoriseerde entiteiten kunnen inzien. 
* **Integriteit** – alleen geautoriseerde entiteiten kunnen wijzigen of verwijderen van uw gegevens.

Hallo Microsoft Azure StorSimple-oplossing bestaat uit vier belangrijke onderdelen met elkaar communiceren:

* **Gehost in Microsoft Azure StorSimple Manager-service** – Hallo management-service dat u tooconfigure en in te richten Hallo StorSimple-apparaat.
* **StorSimple-apparaat** – een fysiek apparaat geïnstalleerd in uw datacenter. Alle hosts en -clients die gegevens genereren verbinding toohello StorSimple-apparaat en Hallo apparaat Hallo gegevens beheert en verplaatst het toohello Azure-cloud zo nodig.
* **Clients/hosts verbonden apparaat toohello** : clients in uw infrastructuur die verbinding maken met de StorSimple-apparaat toohello Hallo en gegevens die moeten worden beveiligd toobe genereren.
* **Cloudopslag** – Hallo locatie in hello Azure-cloud waar gegevens worden opgeslagen.

Hallo beschrijven volgende secties Hallo StorSimple beveiligingsfuncties die beschermen elk van deze onderdelen en het Hallo-gegevens die zijn opgeslagen op deze. Dit omvat ook een lijst met vragen die u over Microsoft Azure StorSimple-beveiliging en bijbehorende Hallo-antwoorden wellicht.

## <a name="storsimple-manager-service-protection"></a>Beveiliging van StorSimple Manager-service
Hallo StorSimple Manager-service is een management-service gehost in Microsoft Azure en gebruikt toomanage alle StorSimple-apparaten die uw organisatie heeft aangeschaft. U kunt toegang tot Hallo StorSimple Manager-service met behulp van uw organisatie referenties toolog op toohello klassieke Azure-portal via een webbrowser. 

Toegang toohello StorSimple Manager-service vereist dat uw organisatie een Azure-abonnement met inbegrip van StorSimple. Uw abonnement beheerst Hallo-functies die u toegang hebt tot in Hallo klassieke Azure-portal. Als uw organisatie beschikt niet over een Azure-abonnement en u meer informatie hierover toolearn wilt, Zie [aanmelden voor Azure als een organisatie](../active-directory/sign-up-organization.md). 

Omdat Hallo StorSimple Manager-service wordt gehost in Azure, wordt het beveiligd door hello Azure beveiligingsfuncties. Ga voor meer informatie over beveiligingsfuncties Hallo geleverd door Microsoft Azure toohello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

## <a name="storsimple-device-protection"></a>Beveiliging van StorSimple-apparaat
Hallo StorSimple-apparaat is een on-premises hybride opslagapparaat die Solid-State-schijven (SSD's) en harde schijven (HDD's), samen met automatische failover-mogelijkheden en redundante controllers bevat. Hallo-controllers beheren opslag in lagen, het plaatsen van momenteel gebruikte (of hot) gegevens op de lokale opslag (in Hallo StorSimple-apparaat of lokale servers) tijdens het verplaatsen van minder vaak gebruikte gegevens toohello cloud.

Alleen geautoriseerde StorSimple apparaten toojoin hello StorSimple Manager-service die u hebt gemaakt in uw Azure-abonnement zijn toegestaan. tooauthorize een apparaat, moet u dit registreren met StorSimple Manager-service Hallo dankzij de serviceregistratiesleutel Hallo. Hallo-serviceregistratiesleutel is een willekeurige sleutel gegenereerd in de klassieke Azure-portal Hallo van 128-bits. 

![serviceregistratiesleutel](./media/storsimple-security/ServiceRegistrationKey.png)

Hoe krijgen een sleutel, gaat u service-registratie te toolearn[stap 2: Get Hallo serviceregistratiesleutel](storsimple-deployment-walkthrough.md#step-2-get-the-service-registration-key).

Hallo-serviceregistratiesleutel is een lange sleutel die 100 + tekens bevat. U kunt Hallo sleutel kopiëren en in een tekstbestand op een veilige locatie opslaan zodat u deze tooauthorize extra apparaten indien nodig kunt. Als de serviceregistratiesleutel Hallo verloren gegaan is nadat u uw eerste apparaat hebt geregistreerd, kunt u een nieuwe sleutel genereren van Hallo StorSimple Manager-service. Hallo-bewerking van bestaande apparaten worden hierdoor niet beïnvloed. 

Wanneer een apparaat is geregistreerd, gebruikt deze tokens toocommunicate met Microsoft Azure. Hallo-serviceregistratiesleutel wordt niet gebruikt na het registreren van apparaten.

> [!NOTE]
> U wordt aangeraden de serviceregistratiesleutel Hallo opnieuw te genereren na elke gebruik.
> 
> 

## <a name="protect-your-storsimple-solution-via-passwords"></a>Beveiligen van uw StorSimple-oplossing via wachtwoorden
Wachtwoorden zijn een belangrijk aspect van de beveiliging van de computer en grote schaal worden gebruikt in de StorSimple-oplossing Hallo toohelp ervoor te zorgen dat uw gegevens alleen toegankelijk tooauthorized voor gebruikers. StorSimple kunt u tooconfigure Hallo wachtwoorden te volgen:

* Beheerderswachtwoord voor StorSimple-apparaat
* Challenge Handshake Authentication Protocol (CHAP) en doel van de initiator wachtwoorden
* Wachtwoord StorSimple Snapshot Manager

### <a name="windows-powershell-for-storsimple-and-hello-storsimple-device-administrator-password"></a>Windows PowerShell voor StorSimple en Hallo beheerderswachtwoord StorSimple-apparaat
Windows PowerShell voor StorSimple is een opdrachtregelinterface die u toomanage hello StorSimple-apparaat kunt gebruiken. Windows PowerShell voor StorSimple functies waarmee u tooregister heeft uw apparaat, Hallo netwerkinterface configureren op uw apparaat, bepaalde typen updates installeren, het apparaat oplossen door het Hallo support-sessie openen en changedevicestate Hallo . U kunt Windows PowerShell voor StorSimple openen door de verbindende toohello seriële console op Hallo-apparaat of via Windows PowerShell op afstand.

Externe communicatie van PowerShell kan plaatsvinden via HTTPS of HTTP. Als u extern beheer via HTTPS is ingeschakeld, moet u extern beheer van toodownload Hallo van het certificaat van Hallo-apparaat en installeer het op Hallo externe client. Voor meer informatie over PowerShell voor externe toegang gaat te[tooyour StorSimple-apparaat op afstand verbinding maken](storsimple-remote-connect.md).

Nadat u Windows PowerShell voor StorSimple tooconnect toohello-apparaat gebruikt, moet u tooprovide Hallo apparaat beheerder wachtwoord toolog op toohello apparaat.

![Wachtwoord apparaatbeheerder](./media/storsimple-security/DeviceAdminPW.png)

Hallo volgende aanbevolen procedures rekening houden:

* Extern beheer is standaard uitgeschakeld. Hallo StorSimple Manager-service tooenable kunt u deze. Als een best practice bij beveiliging externe toegang moet worden ingeschakeld tijdens de Hallo tijdsperiode die daadwerkelijk nodig is.
* Als u Hallo wachtwoord wijzigt, worden toonotify ervoor dat alle externe gebruikers zodat ze zich een onverwachte verbinding wordt verbroken niet.
* Hallo StorSimple Manager-service kan de bestaande wachtwoorden niet ophalen: het ze alleen opnieuw kunt instellen. U wordt aangeraden dat u alle wachtwoorden opslaan op een veilige plaats, zodat er geen tooreset een wachtwoord als deze is vergeten. Als u tooreset een wachtwoord hoeft, zijn toonotify ervoor dat alle gebruikers voordat u het opnieuw instellen. 

Hallo Windows PowerShell-interface is toegankelijk via een seriële verbinding toohello-apparaat. U kunt ook toegang tot het op afstand via HTTP of HTTPS, die extra te beveiligen. HTTPS biedt een hoger niveau van beveiliging dan een serie- of HTTP-verbinding. Echter toouse HTTPS, moet u eerst een certificaat installeren op Hallo-clientcomputer die toegang hebben tot Hallo-apparaat. U kunt Hallo RAS-certificaat downloaden van Hallo apparaat configuratiepagina in Hallo StorSimple Manager-service. Als Hallo-certificaat voor externe toegang verbroken wordt, moet u een nieuw certificaat downloaden en deze tooall-clients die geautoriseerd toouse extern beheer zijn is doorgegeven.

### <a name="challenge-handshake-authentication-protocol-chap-initiator-and-target-passwords"></a>Challenge Handshake Authentication Protocol (CHAP) en doel van de initiator wachtwoorden
CHAP is een verificatieschema dat wordt gebruikt door Hallo StorSimple-apparaat toovalidate Hallo identiteit van externe clients. Hallo-verificatie is gebaseerd op een gedeelde wachtwoord. CHAP mag eenzijdige (Unidirectioneel) of onderlinge (bidirectioneel). Met één richting CHAP verifieert Hallo doel (Hallo StorSimple-apparaat) een initiator (host). Wederzijdse of reverse CHAP moet Hallo doel Hallo initiator verifiëren en vervolgens Hallo initiator Hallo doel te verifiëren. Uw StorSimple geconfigureerde toouse beide methoden kan worden.

Let op Hallo volgende als u CHAP configureren:

* Hallo CHAP-gebruikersnaam moet minder dan 233 tekens bevatten.
* Hallo CHAP-wachtwoord moet tussen 12 en 16 tekens. Toouse probeert leidt een langer gebruikersnaam of wachtwoord tot een verificatiefout opgetreden op Hallo Windows-host.
* U kunt geen hello gebruiken hetzelfde wachtwoord voor zowel Hallo CHAP-initiator als Hallo CHAP-doel.
* Nadat u Hallo wachtwoord hebt ingesteld, kan worden gewijzigd, maar kan niet worden opgehaald. Als Hallo wachtwoord is gewijzigd, worden toonotify ervoor dat alle externe gebruikers zodat ze verbinding toohello StorSimple-apparaat maken kunnen.

Voor meer informatie over CHAP en hoe tooconfigure voor uw StorSimple-oplossing gaat te[CHAP configureren voor uw StorSimple-apparaat](storsimple-configure-chap.md).

### <a name="storsimple-snapshot-manager-password"></a>Wachtwoord StorSimple Snapshot Manager
StorSimple Snapshot Manager is een module Microsoft Management Console (MMC) die gebruikmaakt van volume groepen en Hallo Windows Volume Shadow Copy Service toogenerate toepassingsconsistente back-ups. U kunt bovendien gebruiken StorSimple Snapshot Manager toocreate back-upschema en klonen of herstel van volumes.

Wanneer u een apparaat toouse StorSimple Snapshot Manager configureert, kunt u zich vereist tooprovide hello StorSimple Snapshot Manager-wachtwoord. Dit wachtwoord wordt eerst ingesteld in Windows PowerShell voor StorSimple tijdens de registratie. Hallo wachtwoord kan ook worden ingesteld en gewijzigd van Hallo StorSimple Manager-service. Dit wachtwoord wordt geverifieerd Hallo-apparaat met StorSimple Snapshot Manager.

![Wachtwoord StorSimple Snapshot Manager](./media/storsimple-security/SnapshotMgrPassword.png)

Hallo StorSimple Snapshot Manager-wachtwoord moet 14 too15 tekens en moet 3 of meer van een combinatie van hoofdletters, kleine letters, numerieke en speciale tekens bevatten. Nadat u Hallo StorSimple Snapshot Manager-wachtwoord hebt ingesteld, kan worden gewijzigd, maar kan niet worden opgehaald. Als u Hallo wachtwoord wijzigt, moet u ervoor dat toonotify alle externe gebruikers.

Voor meer informatie over het StorSimple Snapshot Manager gaat te[wat is er StorSimple Snapshot Manager?](storsimple-what-is-snapshot-manager.md)

### <a name="password-best-practices"></a>Aanbevolen procedures voor wachtwoord
Het is raadzaam dat u de volgende Hallo richtlijnen toohelp Zorg ervoor dat StorSimple-wachtwoorden sterk en goed beveiligd zijn:

* Uw wachtwoord wijzigen om de drie maanden. Hallo wachtwoorden wijzigen wordt jaarlijks afgedwongen.
* Sterke wachtwoorden gebruiken. Voor meer informatie gaat te[maken van sterke wachtwoorden en beveiligt u ze](http://blogs.microsoft.com/cybertrust/2014/08/25/create-stronger-passwords-and-protect-them/).
* Gebruik altijd verschillende wachtwoorden voor verschillende mechanismen voor; elk Hallo wachtwoorden die u opgeeft moet uniek zijn.
* Wachtwoorden niet delen met personen die geen geautoriseerde tooaccess hello StorSimple-apparaat.
* Geen uitspreken over een wachtwoord voor anderen of hint Hallo-indeling van een wachtwoord.
* Als u vermoedt dat een account of wachtwoord is ingebroken, rapport Hallo incident tooyour informatie beveiligingsafdeling.
* Alle wachtwoorden behandelen als gevoelige en vertrouwelijke informatie. 

## <a name="storsimple-data-protection"></a>Gegevensbeveiliging voor StorSimple
Deze sectie beschrijft Hallo StorSimple beveiligingsfuncties die gegevens onderweg en opgeslagen gegevens te beveiligen.

Zoals beschreven in andere secties, kunnen wachtwoorden gebruikte tooauthorize zijn en gebruikers te verifiëren voordat ze toegang tooyour StorSimple-oplossing krijgen. Een andere veiligheidsoverweging beveiligt gegevens tegen onbevoegde gebruikers terwijl deze wordt overgebracht tussen opslagsystemen en terwijl deze wordt opgeslagen. Hallo beschrijven volgende secties Hallo functies voor gegevensbeveiliging StorSimple voorzien.

> [!NOTE]
> Ontdubbeling biedt extra beveiliging voor gegevens die zijn opgeslagen op Hallo StorSimple-apparaat en in Microsoft Azure storage. Wanneer de gegevens is ontdubbeld, Hallo-gegevensobjecten worden gescheiden van Hallo metagegevens gebruikt toomap opgeslagen en deze kunt openen: Er zijn geen beschikbare opslagniveau context tooreconstruct Hallo gegevens op basis van volumestructuur heeft, bestandssysteem of bestandsnaam.
> 
> 

## <a name="protect-data-flowing-through-hello-service"></a>Beveiligen van gegevens die binnenkomen via Hallo-service
Hallo primaire doel van Hallo StorSimple Manager-service is toomanage en Hallo StorSimple-apparaat configureren. Hallo StorSimple Manager-service wordt uitgevoerd in Microsoft Azure. Gebruik van hello Azure classic portal tooenter apparaat configuratiegegevens en vervolgens Hallo StorSimple Manager-service toosend hello toohello apparaat maakt gebruik van Microsoft Azure. StorSimple maakt gebruik van een systeem van asymmetrische sleutelparen toohelp ervoor te zorgen dat een inbreuk op Hallo Azure-service niet leiden tot een inbreuk op de opgeslagen gegevens. 

![Versleuteling van gegevens tijdens de vlucht](./media/storsimple-security/DataEncryption.png)

Hallo asymmetrische sleutel system Hallo helpt gegevens te beschermen die via de service Hallo als volgt loopt:

1. Een versleutelingscertificaat voor gegevens die gebruikmaakt van een asymmetrisch openbare en persoonlijke sleutelpaar op Hallo-apparaat wordt gegenereerd en gebruikte tooprotect Hallo gegevens. Hallo-sleutels worden gegenereerd wanneer de eerste Hallo-apparaat is geregistreerd. 
2. Hallo gegevens certificaat versleutelingssleutels worden geëxporteerd naar een Personal Information Exchange (.pfx)-bestand dat wordt beveiligd door Hallo service gegevensversleutelingssleutel, namelijk een sterke 128-bits sleutel die wordt willekeurig gegenereerd door de eerste apparaat Hallo tijdens de registratie.
3. Hallo openbare sleutel van certificaat Hallo veilig gesteld beschikbaar toohello StorSimple Manager-service en de persoonlijke sleutel Hallo Hallo apparaat blijft.
4. Gegevens invoeren Hallo-service is versleuteld met de openbare sleutel Hallo en ontsleuteld met de persoonlijke sleutel Hallo opgeslagen op Hallo-apparaat, waarbij u ervoor zorgt dat hello Azure-service gegevens niet decoderen Hallo stromende toohello apparaat.

Hallo service gegevensversleutelingssleutel wordt alleen Hallo eerste apparaat geregistreerd bij Hallo-service gegenereerd. Alle latere apparaten die zijn geregistreerd bij service Hallo Hallo moeten gebruiken dezelfde gegevensversleutelingssleutel van service. 

> [!IMPORTANT]
> Het is heel belangrijk toomake een kopie van de gegevensversleutelingssleutel van Hallo-service en opslaan in een veilige locatie. Een kopie van de gegevensversleutelingssleutel van service Hallo moet zodanig dat het toegankelijk is voor een specifieke persoon en eenvoudig wordt gecommuniceerd toohello apparaatbeheerder mag worden opgeslagen.
> 
> Als de gegevensversleutelingssleutel van Hallo service verbroken wordt, kan een ondersteuningsmedewerker van Microsoft u helpen tooretrieve dit dat er ten minste één apparaat online is geleverd. U wordt aangeraden dat u Hallo service gegevensversleutelingssleutel wijzigt nadat deze is opgehaald. Voor instructies gaat te[wijziging Hallo service gegevensversleutelingssleutel](storsimple-service-dashboard.md#change-the-service-data-encryption-key).
> 
> 

U kunt Hallo gegevensversleutelingssleutel van service en de bijbehorende gegevens Hallo-versleutelingscertificaat wijzigen door Hallo **gegevensversleutelingssleutel van service wijzigen** optie op Hallo servicedashboard. tooensure dat beveiliging van gegevens niet worden gecompromitteerd, moet u een fysieke StorSimple-apparaat toochange Hallo service gegevensversleutelingssleutel gebruiken. Wijzigen van de versleutelingssleutels Hallo vereist dat alle apparaten worden bijgewerkt met nieuwe Hallo-sleutel. Daarom is het raadzaam Hallo sleutel te wijzigen, wanneer alle apparaten online zijn. Als er apparaten zijn offline is, kunnen de sleutels op een andere tijd worden gewijzigd. Hallo-apparaten met verouderde sleutels wordt nog steeds kunnen toorun back-ups, maar ze worden pas gegevens kunnen toorestore Hallo-sleutel wordt bijgewerkt. Voor meer informatie gaat te[gebruik Hallo StorSimple Manager servicedashboard](storsimple-service-dashboard.md).

Hallo service gegevensversleutelingssleutel en versleutelingscertificaat Hallo-gegevens verlopen niet. We raden u echter aan dat u gegevensversleuteling Hallo-service wijzigt sleutel jaarlijks toohelp te voorkomen dat inbreuk op de sleutel.

## <a name="protect-data-at-rest"></a>Beveiligen van gegevens in rust
Hallo StorSimple-apparaat beheert gegevens door op te slaan in categorieën, lokaal en in de cloud hello, afhankelijk van de frequentie van gebruik. Alle hosten computers die zijn verbonden toohello apparaat verzenden gegevens toohello apparaat, die vervolgens gegevens toohello cloud naar gelang van toepassing verplaatst. Gegevens worden overgebracht van Hallo apparaat toohello cloud veilig via Internet Hallo. Elk apparaat heeft een iSCSI-doel waarmee alle gedeelde volumes voor dat apparaat. Alle gegevens worden versleuteld voordat deze toocloud opslag wordt verzonden. 

![coderingssleutel voor cloudopslag](./media/storsimple-security/CloudStorageEncryption.png)

toohelp optimale Hallo beveiliging en integriteit van gegevens toohello cloud verplaatst, StorSimple kunt u versleutelingssleutels voor toodefine cloud-opslag als volgt:

* U geeft coderingssleutel voor cloudopslag Hallo wanneer u een volumecontainer maken. Hallo-sleutel kan niet worden gewijzigd of later worden toegevoegd. 
* Alle volumes op een share van de container volume Hallo dezelfde versleutelingssleutel. Als u een andere vorm van versleuteling voor een bepaald volume wilt, wordt u aangeraden dat u een nieuw volume container toohost dat volume maakt.
* Wanneer u de versleutelingssleutel voor cloudopslag Hallo in Hallo StorSimple Manager-service invoert, wordt Hallo-sleutel gecodeerd Hallo openbare deel van de gegevensversleutelingssleutel van Hallo-service gebruikt en vervolgens toohello apparaat verzonden.
* coderingssleutel voor cloudopslag Hello wordt niet opgeslagen in Hallo-service en bekend is alleen toohello apparaat.
* Een coderingssleutel voor cloudopslag opgeven is optioneel. U kunt de gegevens die zijn gecodeerd op Hallo host toohello apparaat verzenden.

### <a name="additional-security-best-practices"></a>Aanbevolen procedures voor extra beveiliging
* Verkeer wordt verdeeld: uw iSCSI-SAN van gebruikersverkeer op een LAN-netwerk isoleren door de implementatie van een volledig gescheiden netwerk en het gebruik van VLAN's waar fysieke isolatie kan niet worden gebruikt. Een speciaal netwerk voor iSCSI-opslag wordt gegarandeerd Hallo veiligheid en de prestaties van uw bedrijfskritieke gegevens. De combinatie van opslag- en -verkeer via een LAN-netwerk kan wordt niet aanbevolen en latentie vergroten en dat netwerkfouten.
* Gebruik voor netwerkbeveiliging hostzijde netwerkinterfaces die ondersteuning bieden voor TCP/IP-Offload Engine (TOE). CPU-belasting beperkt TOE door de verwerking van TCP op Hallo-netwerkadapter.

## <a name="protect-data-via-storage-accounts"></a>Bescherm gegevens via de storage-accounts
Elke Microsoft Azure-abonnement kunt maken van een of meer opslagaccounts. (Een opslagaccount biedt een unieke naamruimte voor het werken met gegevens die zijn opgeslagen in hello Azure-cloud.) Toegang tooa storage-account wordt beheerd door Hallo-abonnement en toegangssleutels die zijn gekoppeld aan dit opslagaccount. 

Wanneer u een opslagaccount maakt, genereert Microsoft Azure twee 512-bits opslagtoegangssleutels, waarvan er één wordt gebruikt voor verificatie wanneer Hallo StorSimple-apparaat Hallo storage-account opent. Houd er rekening mee dat er slechts één van deze sleutels gebruikt wordt. Hallo is andere sleutel ondergebracht in reserve, zodat u toorotate Hallo sleutels regelmatig. toorotate sleutels, u Hallo secundaire sleutel active en delete Hallo primaire sleutel. Vervolgens kunt u een nieuwe sleutel voor gebruik tijdens het volgende draaien Hallo maken. (Om veiligheidsredenen vereist veel datacenters sleutel worden gedraaid.) 

U wordt aangeraden dat u deze best practices voor belangrijke rotatie volgt:

* U moet de opslagaccountsleutels regelmatig toohelp zorgen dat uw storage-account niet toegankelijk is door onbevoegde gebruikers draaien.
* De Azure-beheerder moet regelmatig wijzigen of Hallo primaire of secundaire sleutel genereren met behulp van Hallo opslagsectie Hallo Azure classic portal toodirectly toegang Hallo storage-account.

## <a name="protect-data-via-encryption"></a>Bescherm gegevens via versleuteling
Hallo versleutelingsalgoritmen tooprotect gegevens opgeslagen in de volgende of onderweg tussen Hallo onderdelen van uw StorSimple-oplossing maakt gebruik van StorSimple.

| Algoritme | Sleutellengte | Toepassingen-protocollen/opmerkingen |
| --- | --- | --- |
| RSA |2048 |1 voor RSA-PKCS-v1.5 wordt gebruikt door hello Azure classic portal tooencrypt configuratiegegevens die toohello apparaat wordt verzonden: bijvoorbeeld opslag accountreferenties, configuratie van StorSimple-apparaat, en in de cloud van de versleutelingssleutels voor opslag. |
| AES |256 |AES met CBC is gebruikte tooencrypt Hallo openbare deel van de gegevensversleutelingssleutel van service Hallo voordat het toohello klassieke Azure-portal door Hallo StorSimple-apparaat wordt verzonden. Dit wordt ook gebruikt door gegevens tooencrypt hello StorSimple-apparaat voordat Hallo gegevens toohello cloudopslagaccount worden verzonden. |

## <a name="storsimple-virtual-device-security"></a>Beveiliging van StorSimple-apparaat
[!INCLUDE [storsimple virtual device security](../../includes/storsimple-virtual-device-security.md)]

## <a name="frequently-asked-questions-faq"></a>Veelgestelde vragen
Hallo Hier volgen enkele vragen en antwoorden over de beveiliging en Microsoft Azure StorSimple.

**V:** mijn service wordt aangetast. Wat moet de volgende stappen zijn?

**A:** u onmiddellijk Hallo service gegevensversleutelingssleutel en Hallo toegangscodes voor opslag voor Hallo storage-account dat wordt gebruikt voor lagen gegevens moet wijzigen. Voor instructies gaat u naar: 

* [De gegevensversleutelingssleutel van Hallo service wijzigen](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [Sleutel rotatie van de storage-accounts](storsimple-manage-storage-accounts.md#key-rotation-of-storage-accounts)

**V:** ik heb een nieuwe StorSimple-apparaat die om de serviceregistratiesleutel Hallo vraagt. Hoe krijg ik terug?

**A:** deze sleutel is gemaakt tijdens het maken van Hallo StorSimple Manager-service. Wanneer u Hallo StorSimple Manager-service tooconnect toohello apparaat gebruikt, kunt u tooview Hallo service snel starten-pagina of serviceregistratiesleutel Hallo opnieuw genereren. Genereren van een nieuwe registratiecode van de service heeft geen invloed op bestaande geregistreerde apparaten Hallo. Voor instructies gaat u naar:

* [Weergeven of Hallo serviceregistratiesleutel genereren](storsimple-service-dashboard.md#view-or-regenerate-the-service-registration-key)

**V:** mijn gegevensversleutelingssleutel van service is verbroken. Wat moet ik doen?

**A:** contact op met Microsoft ondersteuning. Ze kunnen zich aanmelden op tooa support-sessie op het apparaat en het Help-informatie ophalen van Hallo-sleutel (op voorwaarde dat ten minste één apparaat is online). Onmiddellijk nadat u de gegevensversleutelingssleutel van Hallo service verkregen, moet u deze tooensure die nieuwe sleutel Hallo alleen tooyou bekend. Voor instructies gaat u naar:

* [De gegevensversleutelingssleutel van Hallo service wijzigen](storsimple-service-dashboard.md#change-the-service-data-encryption-key)

**V:** gemachtigd een apparaat voor een service data encryption key wijziging, maar heeft het Hallo wijziging van proces niet starten. Wat moet ik doen?

**A:** als Hallo time-outperiode is verstreken, wordt u tooreauthorize Hallo apparaat Hallo data encryption key voor wijziging van service nodig en Hallo-proces opnieuw starten.

**V:** ik Hallo gegevensversleutelingssleutel van service gewijzigd, maar ik niet kon tooupdate Hallo andere apparaten binnen vier uur. Heb ik toostart opnieuw

**A:** Hallo 4 uur periode is alleen voor het initiëren van Hallo wijzigen. Nadat u het updateproces Hallo starten op Hallo geautoriseerd StorSimple-apparaat, Hallo autorisatie is geldig totdat alle apparaten worden bijgewerkt.

**V:** onze StorSimple beheerder Hallo bedrijf heeft verlaten. Wat moet ik doen?

**A:** wijzigings- en opnieuw instellen van wachtwoorden op dat toegang toohello StorSimple-apparaat toestaan en wijzig Hallo service gegevens encryption key tooensure Hallo nieuwe informatie is niet bekend toounauthorized personeel Hallo. Voor instructies gaat u naar:

* [Hallo StorSimple Manager-service toochange uw storsimple-wachtwoorden gebruiken](storsimple-change-passwords.md)
* [De gegevensversleutelingssleutel van Hallo service wijzigen](storsimple-service-dashboard.md#change-the-service-data-encryption-key)
* [CHAP configureren voor uw StorSimple-apparaat](storsimple-configure-chap.md)

**V:** ik wil tooprovide hello StorSimple Snapshot Manager wachtwoord tooa host dat verbinding toohello StorSimple-apparaat maakt, maar Hallo wachtwoord is niet beschikbaar. Wat kan ik doen?

**A:** als u Hallo wachtwoord vergeten bent, moet u een nieuwe maken. Vervolgens moet u tooinform alle bestaande gebruikers die Hallo wachtwoord is gewijzigd en dat ze hun toouse clients moeten bijwerken Hallo nieuwe wachtwoord. Voor instructies gaat u naar:

* [Hallo StorSimple Snapshot Manager wachtwoord wijzigen](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password)
* [Een apparaat verifiëren](storsimple-snapshot-manager-manage-devices.md#authenticate-a-device)

**V:** Hallo-certificaat voor externe toegang toohello Windows PowerShell voor StorSimple op Hallo-apparaat is gewijzigd. Hoe kan ik mijn RAS-clients bijwerken?

**A:** Hallo nieuwe certificaat downloaden van Hallo StorSimple Manager-service en geef vervolgens toobe geïnstalleerd in het certificaatarchief Hallo van uw RAS-clients. Voor instructies gaat u naar:

* [De cmdlet certificaat importeren](https://technet.microsoft.com/library/hh848630.aspx)

**V:** Is mijn gegevens beveiligd als Hallo StorSimple Manager-service is geknoeid?

**A:** configuratiegegevens van de Service wordt altijd versleuteld met uw openbare sleutel wanneer u deze in een webbrowser bekijken. Omdat het Hallo-service heeft geen toegang tot toohello persoonlijke sleutel, Hallo-service wordt niet kunnen toosee worden geen gegevens. Als Hallo StorSimple Manager-service is aangetast, zijn er geen gevolgen, omdat er geen sleutels zijn opgeslagen in Hallo StorSimple Manager-service.

**V:** als iemand toegang toohello gegevens versleutelingscertificaat krijgt, wordt mijn gegevens worden getroffen?

**A:** Microsoft Azure gegevensversleutelingssleutel van de klant hello (PFX-bestand) in een versleutelde indeling opgeslagen. Omdat Hallo pfx-bestand is versleuteld en Hallo StorSimple-service beschikt niet over Hallo service gegevens versleuteling sleutel toodecrypt Hallo pfx-bestand, wordt er bij het ophalen van gewoon toegang toohello pfx-bestand niet alle geheimen blootstellen.

**V:** wat er gebeurt als een overheidsinstelling Microsoft om mijn gegevens vraagt?

**A:** omdat alle Hallo gegevens worden versleuteld op Hallo-service en Hallo persoonlijke sleutel wordt gehouden met Hallo apparaat hello overheidsinstanties entiteit Hallo klant moet vragen voor Hallo-gegevens. 

## <a name="next-steps"></a>Volgende stappen
[StorSimple-apparaat implementeren](storsimple-deployment-walkthrough.md).

