---
title: aaaTroubleshoot beveiliging fouten VMware of fysieke tooAzure | Microsoft Docs
description: Dit artikel wordt beschreven Hallo algemene VMware machine replicatiefouten en hoe tootroubleshoot ze
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/26/2017
ms.author: asgang
ms.openlocfilehash: b821e9aa2610482ba1900645fb75e75744dc442f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a>Problemen met lokale VMware of fysieke server replicatie
U wordt een specifieke foutbericht weergegeven bij het beveiligen van uw virtuele VMware-machines of fysieke servers met Azure Site Recovery. De details van dit artikel enkele van de meestvoorkomende foutberichten die worden aangetroffen, samen met het oplossen van stappen tooresolve Hallo ze.


## <a name="initial-replication-is-stuck-at-0"></a>Initiële replicatie is vastgelopen bij % 0
De meeste Hallo initiële replicatiefouten die we op ondersteuning optreden zijn vanwege problemen met de tooconnectivity tussen serverproces bronserver of proces server naar Azure.
De meeste gevallen kunt u zelf kunt u deze problemen oplossen door onderstaande Hallo-stappen te volgen.

###<a name="check-hello-following-on-source-machine"></a>Controleer de volgende Hallo op BRONMACHINE
* Gebruik vanaf de opdrachtregel van de bronserver machine Telnet tooping Hallo processerver met https-poort (standaard 9443) zoals hieronder toosee wordt weergegeven als er problemen met de netwerkverbinding of de firewallpoort problemen worden geblokkeerd.
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > Telnet gebruiken, gebruik geen PING tootest connectiviteit.  Als Telnet niet is geïnstalleerd, voert u de lijst met Hallo [hier](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)

Als er kan geen tooconnect toestaan van binnenkomende poort 9443 op Hallo processerver en Vink als hello wordt probleem nog steeds afgesloten. Er zijn enkele gevallen waar de processerver is achter DMZ die dit probleem is veroorzaakt.

* Controleer de status van service Hallo `InMage Scout VX Agent – Sentinel/OutpostStart` als het is niet uitgevoerd en Controleer als Hallo probleem blijft optreden.   
 
###<a name="check-hello-following-on-process-server"></a>Controleer de volgende Hallo op PROCESSERVER

* **Controleer als processerver actief gegevens tooAzure pusht** 

Open Hallo Taakbeheer (druk op Ctrl-Shift-Esc) van de processerver-machine. Ga toohello prestaties tabblad en klik op de koppeling 'Open Broncontrole'. Van Resource Manager gaat tooNetwork tabblad. Controleer als cbengine.exe in 'Processen met netwerkactiviteit' actief grote hoeveelheid (in MB) gegevens verzendt.

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/cbengine.png)

Als dat niet het Hallo stappen hieronder weergegeven:

* **Controleer of de processerver kunnen tooconnect Azure Blob**: Selecteer en toosee cbengine.exe tooview Hallo-TCP-verbindingen controleren als er verbinding van de URL voor proces server tooAzure Storage-blob.

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/rmonitor.png)

Als dat niet gaat tooControl Configuratiescherm > Services, Controleer of Hallo volgende services actief zijn:

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
(Re) Start alle services die niet wordt uitgevoerd en Controleer als Hallo probleem blijft optreden.

* **Controleer of de processerver kunnen tooconnect tooAzure openbaar IP-adres met behulp van poort 443**

Open Hallo nieuwste CBEngineCurr.errlog van `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` en zoek naar: 443 en verbinding poging is mislukt.

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/logdetails1.png)

Als er problemen zijn, vanaf de opdrachtregel processerver, gebruikt u telnet tooping uw Azure openbare IP-adres (gemaskeerd in bovenstaande afbeelding) gevonden in Hallo CBEngineCurr.currLog met poort 443.

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
Als u tooconnect bent, controleert u als Hallo toegang probleem vervaldatum toofirewall of Proxy, zoals beschreven in de volgende stap.


* **Controleer of IP-adressen gebaseerde firewall op de processerver zijn de toegang niet blokkeert**: als u een IP-adressen gebaseerde firewallregels op Hallo-server gebruikt, downloadt u Hallo volledige lijst van Microsoft Azure Datacenter IP-adresbereiken van [hier ](https://www.microsoft.com/download/details.aspx?id=41653) en voeg ze tooyour firewall configuratie tooensure staan ze dat communicatie tooAzure (en Hallo HTTPS (443)-poort).  IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.

* **Controleer of de URL gebaseerde firewall op de processerver toegang niet blokkeert**: als u van een firewall-regels voor URL gebaseerd op Hallo-server gebruikmaakt, controleert u Hallo volgende URL's toofirewall configuratie zijn toegevoegd. 
     
  `*.accesscontrol.windows.net:` Word gebruikt voor toegangs- en identiteitsbeheer

  `*.backup.windowsazure.com:` Wordt gebruikt voor overdracht en indeling van replicatiegegevens

  `*.blob.core.windows.net:`Gebruikt voor toegang tot toohello gerepliceerde storage-account dat wordt opgeslagen gegevens

  `*.hypervrecoverymanager.windowsazure.com:` Wordt gebruikt voor bewerkingen en indeling in het kader van replicatiebeheer

  `time.nist.gov`en `time.windows.com`: toocheck synchronisatie tussen system en globale tijd gebruikt.

URL's voor **Azure Government Cloud**:

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* **Controleer als Proxy-instellingen op de processerver zijn de toegang niet blokkeert**.  Als u een proxyserver gebruikt, zorg er Hallo proxyservernaam omzet door Hallo DNS-server.
toocheck wat u hebt opgegeven tijdens het Hallo van de installatie van de configuratieserver. Ga tooregistry sleutel

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

Nu u ervoor te zorgen dat dezelfde instellingen worden gebruikt door Azure Site Recovery agent toosend gegevens Hallo.
Back-up van Microsoft Azure Search 

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/mab.png)

Open het en klik op actie > Eigenschappen wijzigen. U ziet onder het tabblad Proxy-configuratie Hallo proxy-adres, moet dezelfde zoals aangegeven in de registerinstellingen Hallo. Als dit niet het geval is, wijzig het toohello hetzelfde adres.

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/mabproxy.png)

* **Controleer als u bandbreedte niet op processerver beperkt**: Hallo bandbreedte vergroten en controleer of Hallo probleem nog bestaat.

##<a name="next-steps"></a>Volgende stappen
Als u meer hulp nodig hebt, klikt u vervolgens boeken uw query te[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr). We hebben een actieve community en een van onze technici kunnen tooassist worden u.
