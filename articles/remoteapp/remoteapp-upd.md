---
title: aaaHow biedt Azure RemoteApp gebruikersgegevens en -instellingen opslaan? | Microsoft Docs
description: Meer informatie over hoe Hallo gebruikersprofielschijf met gebruikersgegevens worden opgeslagen in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: e125af62-5c1a-4186-a238-52f537f7bb34
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: dccebc7861e8a0d87cb3ee174f399a2df7fe023c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-remoteapp-save-user-data-and-settings"></a>Hoe Azure RemoteApp gebruikersgegevens en -instellingen opslaan?
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Azure RemoteApp slaat gebruikersidentiteit en aanpassingen over apparaten en sessies. De gegevens van deze gebruiker wordt opgeslagen in een per gebruiker per-verzameling schijf, een gebruikersprofielschijf (UDP) genoemd. Hallo schijf Hallo gebruiker volgt en garandeert Hallo gebruiker heeft een consistente ervaring, ongeacht waar ze zich aanmelden.

Gebruikersprofielschijven zijn volledig transparant toohello gebruiker – gebruikers documentenmap tootheir documenten opslaan (op wat wordt weergegeven voor een lokaal station toobe) en hun appinstellingen gebruikelijke manier te wijzigen. AT Hallo dezelfde tijd, worden alle persoonlijke instellingen behouden bij het verbinden van tooAzure RemoteApp vanaf elk apparaat. Alle Hallo gebruiker ziet, is de gegevens in Hallo dezelfde plaats.

Elke UPD is 50GB aan permanente opslag en beide gebruikersinstellingen voor gegevens en toepassingen bevat. 

Lees verder voor foutopsporingsgegevens op gebruikersprofielgegevens.

> [!NOTE]
> Moet toodisable UPD Hallo? U kunt doen die nu - controle uit van de Pavithra blogbericht [uitschakelen Gebruikersprofielschijven (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/), voor meer informatie.
> 
> 

## <a name="how-can-an-admin-get-toohello-data"></a>Hoe kan een beheerder toohello gegevens krijgen?
Als u tooaccess Hallo gegevens nodig voor een van uw gebruikers (voor herstel na noodgevallen of als de gebruiker Hallo Hallo bedrijf verlaat), neem contact op met ondersteuning van Azure en abonnementsgegevens Hallo voor Hallo verzameling en Hallo gebruikers-id. Hello Azure RemoteApp-team bieden u een URL toohello VHD. Download deze VHD en ophalen van alle documenten of bestanden die u nodig hebt. Houd er rekening mee dat Hallo VHD 50GB, dus er is een toodownload bits deze.

## <a name="is-hello-data-backed-up"></a>Is Hallo gegevens back-up gemaakt?
Ja, er een back-up van de gebruikersgegevens Hallo per geografische locatie opslaan. Hallo gegevens is alleen-lezen en kan worden geopend in Hallo dezelfde manier als normale Hallo-gegevens niet (Neem contact op met Azure RemoteApp tooget deze), als het primaire Datacenter Hallo niet actief is. Hallo gegevens gekopieerde realtime toohello back-uplocatie en we u geen exemplaren van verschillende versies van bewaart. Dus op beschadiging van gegevens wordt niet meer worden kunnen toorestore het tooa voorheen bekend goed versie, maar als het primaire Datacenter Hallo niet actief is, kunt u zich kunt tooget gebruikersgegevens van Hallo andere locatie.

## <a name="how-do-users-see-hello-upd-on-hello-server-side"></a>Hoe kunnen gebruikers Hallo UPD aan serverzijde Hallo zien?
Elke gebruiker hebben hun eigen directory op Hallo-server die is toegewezen tootheir UPD: c:\Users\username.

## <a name="whats-hello-best-way-toouse-outlook-and-upd"></a>Wat is Hallo aanbevolen manier toouse Outlook en UPD?
Azure RemoteApp slaat Hallo Outlook status (postvakken PST-bestanden) tussen sessies. tooenable, moeten we PST toobe opgeslagen in gebruikersprofielgegevens Hallo Hallo (c:\users\<username >). Dit is de standaardlocatie Hallo Hallo gegevens, dus zolang u niet Hallo locatie te wijzigen, Hallo gegevens bewaard tussen sessies.

Ook wordt aangeraden dat u ' ' cachemodus in Outlook gebruiken en ' server / ' onlinemodus om te zoeken gebruiken.

Bekijk [in dit artikel](remoteapp-outlook.md) voor meer informatie over het gebruik van Outlook en Azure RemoteApp.

## <a name="what-about-redirection"></a>Hoe zit het omleiding?
U kunt Azure RemoteApp toolet gebruikers toegang krijgen tot lokale apparaten in te stellen [omleiding](remoteapp-redirection.md). Lokale apparaten zijn vervolgens kunnen tooaccess Hallo gegevens op Hallo UPD.

## <a name="can-i-use-my-upd-as-a-network-share"></a>Kan ik mijn UPD gebruiken als een netwerkshare?
Nee. UPDs kan niet worden gebruikt als een netwerkshare. Een UPD is alleen beschikbaar toohello gebruiker wanneer de gebruiker Hallo actief verbonden tooAzure RemoteApp.

## <a name="if-i-delete-a-user-from-a-collection-is-their-upd-deleted"></a>Als ik een gebruiker uit een verzameling verwijdert, wordt hun UPD dan verwijderd?
Nee, wanneer u een gebruiker verwijdert, we Hallo UPD niet automatisch verwijderd - in plaats daarvan we gegevensopslag Hallo totdat u Hallo verzameling verwijderen. negentig dagen na het verwijderen van de verzameling Hallo, verwijderen we alle UPDs. 

Als u een UPD uit een verzameling toodelete moet, neem contact op met Azure RemoteApp - UPD kan worden verwijderd van onze kant.

## <a name="can-i-access-my-users-upds-either-current-or-deleted-users"></a>Ik toegang tot de Mijn gebruikers UPDs (huidige of verwijderde gebruikers)?
Ja, als u contact opnemen met [Azure RemoteApp](mailto:remoteappforum@microsoft.com), we kunnen instellen u met een URL-tooaccess Hallo-gegevens. U hebt over 10 uur toodownload alle gegevens of de bestanden van Hallo UPD voordat Hallo toegang verloopt.

## <a name="are-upds-available-offline"></a>UPDs offline beschikbaar te zijn?
Op dit moment wij niet offline toegang tooUPDs, afgezien van Hallo 10 uur toegang venster die hierboven worden beschreven. Dit betekent dat er momenteel geen een manier tooprovide u met toegang voor lang genoeg toocomplete ingewikkelder taken tot, zoals antivirussoftware uitvoeren op Hallo UPDs of toegang tot gegevens voor een controle.

## <a name="do-registry-key-settings-persist"></a>Blijven ze registersleutelinstellingen behouden?
Ja, iets geschreven tooHKEY_Current_User maakt deel uit van Hallo UPD.

## <a name="can-i-disable-upds-for-a-collection"></a>Kan ik UPDs uitschakelen voor een verzameling?
Ja, kunt u Azure RemoteApp toodisable UPDs vragen voor een abonnement, maar is niet mogelijk die zelf. Dit betekent dat UPDs wordt uitgeschakeld voor alle collecties in Hallo-abonnement.

U kunt toodisable UPDs in een van de volgende situaties Hallo: 

* U moet toegang tot en beheer van gebruikersgegevens voltooid (voor controle en de analyse, zoals financiële instellingen).
* U hebben 3rd derden gebruiker profiel oplossingen lokaal beheer en toocontinue gebruik ervan in uw domein Azure RemoteApp-implementatie wilt. Hiervoor moeten Hallo profiel agent toobe geladen in Hallo gouden installatiekopie. 
* U hoeft geen lokale gegevensopslag niet of u alle gegevens in de cloud of bestandsshare Hallo hebt en wilt toocontrol het opslaan van gegevens die lokaal via Azure RemoteApp.

Zie [uitschakelen Gebruikersprofielschijven (UPDs) in Azure RemoteApp](https://blogs.technet.microsoft.com/enterprisemobility/2015/11/11/disable-user-profile-disks-upds-in-azure-remoteapp/) voor meer informatie.

## <a name="can-i-restrict-users-from-saving-data-toohello-system-drive"></a>Kan ik voorkomen dat gebruikers kunnen gegevens toohello systeemstation opslaan?
Ja, maar moet u tooset die omhoog in de sjabloon Hallo voordat u Hallo verzameling maakt een installatiekopie. Volgende stappen tooblock toegang toohello-systeemstation Hallo gebruiken:

1. Voer **gpedit.msc** op Hallo-sjablooninstallatiekopie.
2. Navigeer te**Gebruikersconfiguratie > Beheersjablonen > Windows-onderdelen > Explorer**.
3. Hallo volgende opties selecteren:
   * **De opgegeven stations in deze Computer verbergen**
   * **Voorkomen dat toegang toodrives vanaf deze Computer**

## <a name="can-i-seed-upds-i-want-tooput-some-data-in-hello-upd-thats-available-hello-first-time-hello-user-signs-in"></a>Kan ik seed-UPDs? Ik wil tooput sommige gegevens in Hallo UPD die beschikbaar Hallo eerste tijd Hallo gebruiker zich aanmeldt.
Wanneer u een installatiekopie Hallo-sjabloon maakt, kunt u Ja, informatie toohello standaardprofiel toevoegen. Deze informatie wordt vervolgens toegevoegd aan toohello UPD.

## <a name="can-i-change-hello-size-of-hello-upd-depending-on-how-much-data-i-want-toostore"></a>Kan ik Hallo grootte van Hallo UPD wijzigen, afhankelijk van hoeveel gegevens wil toostore?
Nee, alle UPDs hebben 50 GB aan opslagruimte. Als u wilt dat andere hoeveelheden gegevens toostore, probeert u Hallo volgende:

1. UPDs voor Hallo verzameling uitschakelen.
2. Een bestandsshare voor tooaccess gebruikers instellen.
3. Load Hallo bestandsshare met behulp van een opstartscript. Zie hieronder voor meer informatie over opstartscripts in Azure RemoteApp.
4. Directe toosave gebruikers alle gegevens toohello-bestandsshare.

## <a name="how-do-i-run-a-startup-script-in-azure-remoteapp"></a>Hoe kan ik een opstartscript uitvoeren in Azure RemoteApp?
Als u een opstartscript toorun wilt, starten door een geplande taak maken in de sjablooninstallatiekopie Hallo u toouse voor Hallo verzameling gaat. (Hiervoor *voordat* u sysprep uitvoeren.) 

![Een systeemtaak maken](./media/remoteapp-upd/upd1.png)

![Maken van een systeemtaak die wordt uitgevoerd wanneer een gebruiker zich aanmeldt](./media/remoteapp-upd/upd2.png)

Op Hallo **algemene** tabblad, kunnen ervoor toochange hello **gebruikersaccount** onder beveiliging te "BUILTIN\Users."

![Account Hallo-tooa gebruikersgroep wijzigen](./media/remoteapp-upd/upd4.png)

Hallo geplande taak wordt gestart, het opstartscript met Hallo gebruikersreferenties. Hallo taak toorun plannen om een wanneer een gebruiker zich aanmeldt.

![Set Hallo trigger voor de taak 'Op aanmelden' Hallo](./media/remoteapp-upd/upd3.png)

U kunt ook [op basis van Groepsbeleid opstartscripts](https://technet.microsoft.com/library/cc779329%28v=ws.10%29.aspx). 

## <a name="what-about-placing-a-startup-script-in-hello-start-menu-would-that-work"></a>Hoe zit een opstartscript plaatsen in Hallo menu Start? Zou die in zijn werk?
Met andere woorden, kan ik een bat-bestand met een script config-venster maken toohello c:\ProgramData\Microsoft\Windows\Start s\Opstarten opslaan en hebt script uitgevoerd wanneer een gebruiker een RemoteApp-sessie start?

Nee, die wordt niet ondersteund met Azure RemoteApp, dat gebruikmaakt van RDSH, die ook geen ondersteuning biedt opstartscripts in Hallo startmenu.

## <a name="can-i-use-mstscexe-hello-remote-desktop-program-tooconfigure-logon-scripts"></a>Kan ik mstsc.exe (extern bureaublad-programma Hallo) tooconfigure aanmeldingsscripts gebruiken?
Nee, ondersteund niet door Azure RemoteApp.

## <a name="can-i-store-data-on-hello-vm-locally"></a>Kan ik gegevens op Hallo VM lokaal opslaan?
Nee, overal op Hallo VM anders dan in Hallo UPD opgeslagen gegevens niet verloren. Er is een hoge kans Hallo gebruiker krijgt geen Hallo dezelfde VM Hallo volgende keer dat ze zich bij Azure RemoteApp aanmelden. We geen gebruiker VM persistentie, onderhouden zodat Hallo gebruiker wordt niet aanmelden bij Hallo dezelfde virtuele machine, en de Hallo gegevens gaan verloren. Bovendien wanneer we Hallo verzameling bijwerken, is bestaande virtuele machines worden vervangen door een nieuwe set van virtuele machines - waardoor alle gegevens die zijn opgeslagen op de virtuele machine zelf Hallo Hallo verloren. Hallo-aanbeveling is toostore gegevens in Hallo UDP, gedeelde opslag, zoals Azure-bestanden, een bestandsserver die binnen een VNET of op Hallo cloud met behulp van een cloud-opslagsysteem zoals DropBox.

## <a name="how-do-i-mount-an-azure-file-share-on-a-vm-using-powershell"></a>Hoe ik een Azure-bestandsshare op een virtuele machine met behulp van PowerShell koppelen?
U kunt als volgt Hallo Net PSDrive cmdlet toomount Hallo-station gebruiken:

    New-PSDrive -Name <drive-name> -PSProvider FileSystem -Root \\<storage-account-name>.file.core.windows.net\<share-name> -Credential :<storage-account-name>


U kunt ook uw referenties door het uitvoeren van de volgende Hallo opslaan:

    cmdkey /add:<storage-account-name>.file.core.windows.net /user:<storage-account-name> /pass:<storage-account-key>


Waarmee u overslaan Hallo - parameter in de cmdlet New-PSDrive Hallo Credential.

