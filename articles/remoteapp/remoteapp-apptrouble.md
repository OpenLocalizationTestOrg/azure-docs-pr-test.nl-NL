---
title: RemoteApp-probleemoplossing - aaaAzure voor starten en verbinding toepassingsfouten | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot problemen met een begin- en verbinding maken met tooapplications in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: e5cf7171-d1c2-4053-a38b-5af7821305e1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e51d480c9d3fa1f2076f95b63c7a8cd2f6956a4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-remoteapp---application-launch-and-connection-failures"></a>Problemen met Azure RemoteApp - toepassingsfouten voor starten en verbinding
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

Toepassingen die worden gehost in Azure RemoteApp kunnen toolaunch om een paar verschillende redenen mislukken. Dit artikel wordt beschreven diverse redenen en foutberichten die gebruikers mogelijk ontvangen wanneer het toolaunch toepassingen proberen. Het is ook wordt gesproken over verbindingsfouten. (Maar in dit artikel wordt niet beschreven hoe problemen bij het ondertekenen van hello Azure RemoteApp-client.)  

Lees verder voor meer informatie over algemene foutberichten vanwege tooapp voor starten en verbinding fouten.

## <a name="were-getting-you-set-up-try-again-in-10-minutes"></a>Wij krijgen instellen... Probeer het over 10 minuten opnieuw.
Deze fout betekent dat Azure RemoteApp wordt geschaald up toomeet Hallo capaciteit behoeften van uw gebruikers. Op de achtergrond Hallo worden meer exemplaren van de virtuele machine in Azure RemoteApp gemaakt toohandle Hallo capaciteitsbehoeften van uw gebruikers. Meestal dit duurt ongeveer vijf minuten maar too10 minuten kan duren. Soms wordt dit gebeurt niet snel genoeg en resources onmiddellijk nodig. Bijvoorbeeld een 9: 00 uur scenario waar veel gebruikers toouse uw app in Azure RemoteAppn op Hallo moeten hetzelfde moment. Als dit tooyou gebeurt schakelen we **capaciteit modus** op Hallo back-end. toodo dat openen ticket van een Azure-ondersteuning. Bepaalde tooinclude uw abonnements-ID in Hallo-aanvraag niet.  

![Wij krijgen instellen](./media/remoteapp-apptrouble/ra-apptrouble1.png)

## <a name="could-not-auto-reconnect-tooyour-applications-please-re-launch-your-application"></a>Kan niet automatisch verbinding maken tooyour-toepassingen opnieuw start uw toepassing
Dit foutbericht wordt vaak gezien als u Azure RemoteApp en zet u uw PC toosleep langer zijn dan 4 uur gebruikt en vervolgens uw PC woke up en hello Azure RemoteApp-client poging tooauto opnieuw verbinding maken en time-out is overschreden.  Gebruikers toonavigate back toohello toepassing instrueren en tooopen proberen via hello Azure RemoteApp-client.

![Kan niet automatisch verbinding maken tooyour toepassingen](./media/remoteapp-apptrouble/ra-apptrouble2.png) 

## <a name="problems-with-hello-temp-profile"></a>Problemen met tijdelijke profielen Hallo
Deze fout treedt op wanneer het gebruikersprofiel (Gebruikersprofielschijf) is mislukt toomount en Hallo gebruiker een tijdelijk profiel ontvangen.  Beheerders moeten navigeren toohello verzameling in hello Azure-portal en gaat u toohello **sessies** tabblad en proberen te**Afmelden** Hallo-gebruiker. Hiermee wordt een volledige logboek af gebruikerssessie Hallo - force vervolgens Hallo gebruiker poging toolaunch opnieuw een app hebt. Als dat Neem contact op met de ondersteuning van Azure mislukt.

## <a name="azure-remoteapp-has-stopped-working"></a>Azure RemoteApp werkt niet
Dit foutbericht geeft hello Azure RemoteApp-client heeft een probleem en moet toobe opnieuw gestart. Gebruikers tooclose instrueren: Selecteer **programma afsluiten** en hello Azure RemoteApp-client vervolgens opnieuw te starten.  Als Hallo probleem blijft openen en de Azure-ondersteuningsticket optreden.

![Azure RemoteApp werkt niet](./media/remoteapp-apptrouble/ra-apptrouble3.png)  

## <a name="an-error-occurred-while-remote-desktop-connection-was-accessing-this-resource-retry-hello-connection-or-contact-your-system-administrator"></a>Er is een fout opgetreden tijdens het verbinding met extern bureaublad is toegang tot deze bron. Hallo-verbinding opnieuw of neem contact op met uw systeembeheerder
Dit is een algemene foutmelding: Neem contact op met de ondersteuning van Azure zodat we kunt onderzoeken. 

![Algemene Azure RemoteApp-bericht](./media/remoteapp-apptrouble/ra-apptrouble4.png) 

