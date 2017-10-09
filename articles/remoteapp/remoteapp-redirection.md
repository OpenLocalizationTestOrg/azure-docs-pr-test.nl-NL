---
title: aaaUsing omleiding in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooconfigure en gebruik omleiding in RemoteApp
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a>Met behulp van omleiding in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Omleiding van apparaten kan uw gebruikers communiceren met externe apps met Hallo apparaten gekoppelde tootheir lokale computer, telefoon of tablet. Als u Skype via Azure RemoteApp hebt opgegeven, moet de gebruiker Hallo camera op hun PC toowork met Skype geïnstalleerd. Dit geldt ook voor printers, luidsprekers, monitors en een bereik van USB-verbinding randapparatuur.

RemoteApp maakt gebruik van Hallo Remote Desktop Protocol (RDP) en RemoteFX tooprovide omleiding.

## <a name="what-redirection-is-enabled-by-default"></a>Welke omleiding is standaard ingeschakeld?
Wanneer u RemoteApp gebruikt, worden volgende omleidingen Hallo standaard ingeschakeld. Hallo informatie tussen haakjes weergegeven Hallo RDP-instelling.

* Geluid afspelen op de lokale computer hello (**op deze computer afspelen**). (audiomode:i:0)
* Geluid opnemen van de lokale computer Hallo en verzenden toohello externe computer (**Record van deze computer**). (audiocapturemode:i:1)
* Afdrukken toolocal-printers (redirectprinters:i:1)
* COM-poorten (redirectcomports:i:1)
* Smartcard-apparaat (redirectsmartcards:i:1)
* Klembord (mogelijkheid toocopy en plakken) (redirectclipboard:i:1)
* Schakel type lettertype-aanpassing (lettertype-aanpassing toestaan: i:1)
* Omleiden van alle ondersteunde Plug en Play-apparaten. (devicestoredirect:s: *)

## <a name="what-other-redirection-is-available"></a>Welke andere omleiding is beschikbaar?
Er zijn twee opties voor Mapomleiding standaard uitgeschakeld:

* Stationsomleiding (stationstoewijzing): de lokale computer-stations worden toegewezen stations in de externe sessie Hallo. Hiermee kunt u opslaat of geopende bestanden van de lokale vaste schijven terwijl u in de externe sessie Hallo werkt.
* USB-omleiding: U kunt Hallo USB-apparaten gekoppelde tooyour lokale computer gebruiken in de externe sessie Hallo.

## <a name="change-your-redirection-settings-in-remoteapp"></a>Wijzig de omleidingsinstellingen voor in RemoteApp
U kunt Hallo apparaatinstellingen omleiding voor een verzameling wijzigen met behulp van Microsoft Azure PowerShell Hallo met SDK. Nadat u Hallo nieuwe PowerShell- en SDK, moet u eerst toomanage uw abonnement als is beschreven in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

Gebruik vervolgens een opdracht vergelijkbare toohello volgende tooset Hallo aangepaste RDP-eigenschappen:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

(Houd er rekening mee dat  *`n*  wordt gebruikt als scheidingsteken tussen de afzonderlijke eigenschappen.)

tooget een lijst met welke aangepaste RDP-eigenschappen zijn geconfigureerd, Hallo volgende cmdlet uitvoeren. Houd er rekening mee dat alleen aangepaste eigenschappen worden weergegeven als de resultaten van de uitvoer en geen Hallo standaardeigenschappen:  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

Bij het instellen van aangepaste eigenschappen moet u alle aangepaste eigenschappen opgeven telkens; Hallo-instelling hersteld anders toodisabled.   

### <a name="common-examples"></a>Algemene voorbeelden
Hallo cmdlet tooenable stationsomleiding volgende gebruiken:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

Gebruik deze cmdlet tooenable omleiding van USB- en station:

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

Gebruik deze cmdlet toodisable Klembord delen:  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> Worden toocompletely ervoor dat alle gebruikers in de verzameling Hallo afmelden (en niet alleen verbreekt) voordat u gaat Hallo wijzigen testen. tooensure zijn volledig afgemeld, Ga toohello **sessies** tabblad in de verzameling Hallo in hello Azure-portal en afmelden van gebruikers die zijn verbroken of aangemeld. Soms kan het enkele seconden duren voor Hallo lokale stations tooshow in Verkenner binnen Hallo-sessie.
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a>Wijzig de instellingen van de USB-omleiding op uw Windows-client
Als u toouse USB-omleiding op een computer die verbinding tooRemoteApp wilt maakt, zijn er 2 acties die toohappen nodig. 1 - uw beheerder moet tooenable USB-omleiding op niveau van de verzameling Hallo met behulp van Azure PowerShell. 2 - op elk apparaat waarop toouse USB-omleiding, moet u een groepsbeleid waarmee het tooenable. Deze stap moet toobe gedaan voor elke gebruiker die wil toouse USB-omleiding.

> [!NOTE]
> USB-omleiding met Azure RemoteApp wordt alleen ondersteund voor Windows-computers.
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a>USB-omleiding voor RemoteApp-collectie Hallo inschakelen
Hallo cmdlet tooenable USB-omleiding op niveau van de verzameling Hallo volgende gebruiken:

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a>USB-omleiding voor Hallo client inschakelen
tooconfigure USB-instellingen voor mapomleiding op uw computer:

1. Open Hallo Editor voor lokaal groepsbeleid (GPEDIT. MSC). (Gpedit.msc uitvoeren vanaf een opdrachtprompt.)
2. Open **Computer Configuration\Policies\Administrative Templates\Windows onderdelen\Extern Desktop Services\Remote bureaubladverbinding Client\RemoteFX USB-apparaatomleiding**.
3. Dubbelklik op **toestaan RDP-omleiding van andere ondersteunde RemoteFX USB-apparaten van deze computer**.
4. Selecteer **ingeschakeld**, en selecteer vervolgens **beheerders en gebruikers in Hallo RemoteFX USB-omleiding toegangsrechten**.
5. Open een opdrachtprompt met beheerdersrechten en Voer Hallo volgende opdracht uit:
   
        gpupdate /force
6. Hallo-computer opnieuw opstarten.

U kunt ook Hallo Group Policy Management tool toocreate gebruiken en toepassen van Hallo USB-beleid voor omleiding voor alle computers in uw domein:

1. Meld u aan bij de domeincontroller Hallo als domeinbeheerder Hallo.
2. Open Hallo Group Policy Management Console. (Klik op **Start > beheerprogramma's > Groepsbeleidsbeheer**.)
3. Toohello domein of organisatie-eenheid waarvoor u toocreate Hallo beleid wilt navigeren.
4. Met de rechtermuisknop op **standaarddomeinbeleid**, en klik vervolgens op **bewerken**.
5. Open **Computer Configuration\Policies\Administrative Templates\Windows onderdelen\Extern Desktop Services\Remote bureaubladverbinding Client\RemoteFX USB-apparaatomleiding**.
6. Dubbelklik op **toestaan RDP-omleiding van andere ondersteunde RemoteFX USB-apparaten van deze computer**.
7. Selecteer **ingeschakeld**, en selecteer vervolgens **beheerders en gebruikers in Hallo RemoteFX USB-omleiding toegangsrechten**.
8. Klik op **OK**.  

