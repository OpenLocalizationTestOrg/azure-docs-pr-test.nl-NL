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
# <a name="troubleshoot-on-premises-vmwarephysical-server-replication-issues"></a><span data-ttu-id="07e1b-103">Problemen met lokale VMware of fysieke server replicatie</span><span class="sxs-lookup"><span data-stu-id="07e1b-103">Troubleshoot on-premises VMware/Physical server replication issues</span></span>
<span data-ttu-id="07e1b-104">U wordt een specifieke foutbericht weergegeven bij het beveiligen van uw virtuele VMware-machines of fysieke servers met Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="07e1b-104">You may receive a specific error message when protecting your VMware virtual machines or physical servers using Azure Site Recovery.</span></span> <span data-ttu-id="07e1b-105">De details van dit artikel enkele van de meestvoorkomende foutberichten die worden aangetroffen, samen met het oplossen van stappen tooresolve Hallo ze.</span><span class="sxs-lookup"><span data-stu-id="07e1b-105">This article details some of hello more common error messages encountered, along with troubleshooting steps tooresolve them.</span></span>


## <a name="initial-replication-is-stuck-at-0"></a><span data-ttu-id="07e1b-106">Initiële replicatie is vastgelopen bij % 0</span><span class="sxs-lookup"><span data-stu-id="07e1b-106">Initial replication is stuck at 0%</span></span>
<span data-ttu-id="07e1b-107">De meeste Hallo initiële replicatiefouten die we op ondersteuning optreden zijn vanwege problemen met de tooconnectivity tussen serverproces bronserver of proces server naar Azure.</span><span class="sxs-lookup"><span data-stu-id="07e1b-107">Most of hello initial replication failures that we encounter at support are due tooconnectivity issues between source server-to-process server or process server-to-Azure.</span></span>
<span data-ttu-id="07e1b-108">De meeste gevallen kunt u zelf kunt u deze problemen oplossen door onderstaande Hallo-stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="07e1b-108">For most cases, you can self troubleshoot these issues by following hello steps listed below.</span></span>

###<a name="check-hello-following-on-source-machine"></a><span data-ttu-id="07e1b-109">Controleer de volgende Hallo op BRONMACHINE</span><span class="sxs-lookup"><span data-stu-id="07e1b-109">Check hello following on SOURCE MACHINE</span></span>
* <span data-ttu-id="07e1b-110">Gebruik vanaf de opdrachtregel van de bronserver machine Telnet tooping Hallo processerver met https-poort (standaard 9443) zoals hieronder toosee wordt weergegeven als er problemen met de netwerkverbinding of de firewallpoort problemen worden geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="07e1b-110">From Source Server machine command line, use Telnet tooping hello Process Server with https port (default 9443) as shown below toosee if there are any network connectivity issues or firewall port blocking issues.</span></span>
     
    `telnet <PS IP address> <port>`
> [!NOTE]
    > <span data-ttu-id="07e1b-111">Telnet gebruiken, gebruik geen PING tootest connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="07e1b-111">Use Telnet, don’t use PING tootest connectivity.</span></span>  <span data-ttu-id="07e1b-112">Als Telnet niet is geïnstalleerd, voert u de lijst met Hallo [hier](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="07e1b-112">If Telnet is not installed, follow hello steps list [here](https://technet.microsoft.com/library/cc771275(v=WS.10).aspx)</span></span>

<span data-ttu-id="07e1b-113">Als er kan geen tooconnect toestaan van binnenkomende poort 9443 op Hallo processerver en Vink als hello wordt probleem nog steeds afgesloten.</span><span class="sxs-lookup"><span data-stu-id="07e1b-113">If unable tooconnect, allow inbound port 9443 on hello Process Server and check if hello problem still exits.</span></span> <span data-ttu-id="07e1b-114">Er zijn enkele gevallen waar de processerver is achter DMZ die dit probleem is veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="07e1b-114">There has been some cases where process server was behind DMZ, which was causing this problem.</span></span>

* <span data-ttu-id="07e1b-115">Controleer de status van service Hallo `InMage Scout VX Agent – Sentinel/OutpostStart` als het is niet uitgevoerd en Controleer als Hallo probleem blijft optreden.</span><span class="sxs-lookup"><span data-stu-id="07e1b-115">Check hello status of service `InMage Scout VX Agent – Sentinel/OutpostStart` if it is not running and check if hello problem still exists.</span></span>   
 
###<a name="check-hello-following-on-process-server"></a><span data-ttu-id="07e1b-116">Controleer de volgende Hallo op PROCESSERVER</span><span class="sxs-lookup"><span data-stu-id="07e1b-116">Check hello following on PROCESS SERVER</span></span>

* <span data-ttu-id="07e1b-117">**Controleer als processerver actief gegevens tooAzure pusht**</span><span class="sxs-lookup"><span data-stu-id="07e1b-117">**Check if process server is actively pushing data tooAzure**</span></span> 

<span data-ttu-id="07e1b-118">Open Hallo Taakbeheer (druk op Ctrl-Shift-Esc) van de processerver-machine.</span><span class="sxs-lookup"><span data-stu-id="07e1b-118">From Process Server machine, open hello Task Manager (press Ctrl-Shift-Esc ).</span></span> <span data-ttu-id="07e1b-119">Ga toohello prestaties tabblad en klik op de koppeling 'Open Broncontrole'.</span><span class="sxs-lookup"><span data-stu-id="07e1b-119">Go toohello Performance tab and click ‘Open Resource Monitor’ link.</span></span> <span data-ttu-id="07e1b-120">Van Resource Manager gaat tooNetwork tabblad. Controleer als cbengine.exe in 'Processen met netwerkactiviteit' actief grote hoeveelheid (in MB) gegevens verzendt.</span><span class="sxs-lookup"><span data-stu-id="07e1b-120">From Resource Manager, go tooNetwork tab. Check if cbengine.exe in ‘Processes with Network Activity’ is actively sending large volume (in Mbs) of data.</span></span>

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/cbengine.png)

<span data-ttu-id="07e1b-122">Als dat niet het Hallo stappen hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="07e1b-122">If not follow hello steps listed below:</span></span>

* <span data-ttu-id="07e1b-123">**Controleer of de processerver kunnen tooconnect Azure Blob**: Selecteer en toosee cbengine.exe tooview Hallo-TCP-verbindingen controleren als er verbinding van de URL voor proces server tooAzure Storage-blob.</span><span class="sxs-lookup"><span data-stu-id="07e1b-123">**Check if Process server is able tooconnect Azure Blob**: Select and check cbengine.exe tooview hello ‘TCP Connections’ toosee if there is connectivity from Process server tooAzure Storage blob URL.</span></span>

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/rmonitor.png)

<span data-ttu-id="07e1b-125">Als dat niet gaat tooControl Configuratiescherm > Services, Controleer of Hallo volgende services actief zijn:</span><span class="sxs-lookup"><span data-stu-id="07e1b-125">If not then go tooControl Panel > Services, check if hello following services are up and running:</span></span>

     * cxprocessserver
     * InMage Scout VX Agent – Sentinel/Outpost
     * Microsoft Azure Recovery Services Agent
     * Microsoft Azure Site Recovery Service
     * tmansvc
     * 
<span data-ttu-id="07e1b-126">(Re) Start alle services die niet wordt uitgevoerd en Controleer als Hallo probleem blijft optreden.</span><span class="sxs-lookup"><span data-stu-id="07e1b-126">(Re)Start any service which is not running and check if hello problem still exists.</span></span>

* <span data-ttu-id="07e1b-127">**Controleer of de processerver kunnen tooconnect tooAzure openbaar IP-adres met behulp van poort 443**</span><span class="sxs-lookup"><span data-stu-id="07e1b-127">**Check if Process server is able tooconnect tooAzure Public IP address using port 443**</span></span>

<span data-ttu-id="07e1b-128">Open Hallo nieuwste CBEngineCurr.errlog van `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` en zoek naar: 443 en verbinding poging is mislukt.</span><span class="sxs-lookup"><span data-stu-id="07e1b-128">Open hello latest CBEngineCurr.errlog from `%programfiles%\Microsoft Azure Recovery Services Agent\Temp` and search for :443  and connection attempt failed.</span></span>

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/logdetails1.png)

<span data-ttu-id="07e1b-130">Als er problemen zijn, vanaf de opdrachtregel processerver, gebruikt u telnet tooping uw Azure openbare IP-adres (gemaskeerd in bovenstaande afbeelding) gevonden in Hallo CBEngineCurr.currLog met poort 443.</span><span class="sxs-lookup"><span data-stu-id="07e1b-130">If there are issues, then from Process Server command line, use telnet tooping your Azure Public IP address (masked in above image) found in hello CBEngineCurr.currLog using port 443.</span></span>

      telnet <your Azure Public IP address as seen in CBEngineCurr.errlog>  443
<span data-ttu-id="07e1b-131">Als u tooconnect bent, controleert u als Hallo toegang probleem vervaldatum toofirewall of Proxy, zoals beschreven in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="07e1b-131">If you are unable tooconnect, then check if hello access issue is due toofirewall or Proxy as described in next step.</span></span>


* <span data-ttu-id="07e1b-132">**Controleer of IP-adressen gebaseerde firewall op de processerver zijn de toegang niet blokkeert**: als u een IP-adressen gebaseerde firewallregels op Hallo-server gebruikt, downloadt u Hallo volledige lijst van Microsoft Azure Datacenter IP-adresbereiken van [hier ](https://www.microsoft.com/download/details.aspx?id=41653) en voeg ze tooyour firewall configuratie tooensure staan ze dat communicatie tooAzure (en Hallo HTTPS (443)-poort).</span><span class="sxs-lookup"><span data-stu-id="07e1b-132">**Check if IP address-based firewall on Process server are not blocking access**: If you are using an IP address-based firewall rules on hello server, then download hello complete list of Microsoft Azure Datacenter IP Ranges from [here](https://www.microsoft.com/download/details.aspx?id=41653) and add them tooyour firewall configuration tooensure they allow communication tooAzure (and hello HTTPS (443) port).</span></span>  <span data-ttu-id="07e1b-133">IP-adresbereiken voor hello Azure-regio van uw abonnement en voor VS-West (gebruikt voor toegangsbeheer en identiteitsbeheer) toestaan.</span><span class="sxs-lookup"><span data-stu-id="07e1b-133">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

* <span data-ttu-id="07e1b-134">**Controleer of de URL gebaseerde firewall op de processerver toegang niet blokkeert**: als u van een firewall-regels voor URL gebaseerd op Hallo-server gebruikmaakt, controleert u Hallo volgende URL's toofirewall configuratie zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="07e1b-134">**Check if URL-based firewall on Process server is not blocking access**:  If you are using a URL based firewall rules on hello server, ensure hello following URLs are added toofirewall configuration.</span></span> 
     
  <span data-ttu-id="07e1b-135">`*.accesscontrol.windows.net:` Word gebruikt voor toegangs- en identiteitsbeheer</span><span class="sxs-lookup"><span data-stu-id="07e1b-135">`*.accesscontrol.windows.net:` Used for access control and identity management</span></span>

  <span data-ttu-id="07e1b-136">`*.backup.windowsazure.com:` Wordt gebruikt voor overdracht en indeling van replicatiegegevens</span><span class="sxs-lookup"><span data-stu-id="07e1b-136">`*.backup.windowsazure.com:` Used for replication data transfer and orchestration</span></span>

  <span data-ttu-id="07e1b-137">`*.blob.core.windows.net:`Gebruikt voor toegang tot toohello gerepliceerde storage-account dat wordt opgeslagen gegevens</span><span class="sxs-lookup"><span data-stu-id="07e1b-137">`*.blob.core.windows.net:` Used for access toohello storage account that stores replicated data</span></span>

  <span data-ttu-id="07e1b-138">`*.hypervrecoverymanager.windowsazure.com:` Wordt gebruikt voor bewerkingen en indeling in het kader van replicatiebeheer</span><span class="sxs-lookup"><span data-stu-id="07e1b-138">`*.hypervrecoverymanager.windowsazure.com:` Used for replication management operations and orchestration</span></span>

  <span data-ttu-id="07e1b-139">`time.nist.gov`en `time.windows.com`: toocheck synchronisatie tussen system en globale tijd gebruikt.</span><span class="sxs-lookup"><span data-stu-id="07e1b-139">`time.nist.gov` and `time.windows.com`: Used toocheck time synchronization between system and global time.</span></span>

<span data-ttu-id="07e1b-140">URL's voor **Azure Government Cloud**:</span><span class="sxs-lookup"><span data-stu-id="07e1b-140">URLs for **Azure Government Cloud**:</span></span>

`* .ugv.hypervrecoverymanager.windowsazure.us`

`* .ugv.backup.windowsazure.us`

`* .ugi.hypervrecoverymanager.windowsazure.us`

`* .ugi.backup.windowsazure.us` 

* <span data-ttu-id="07e1b-141">**Controleer als Proxy-instellingen op de processerver zijn de toegang niet blokkeert**.</span><span class="sxs-lookup"><span data-stu-id="07e1b-141">**Check if Proxy Settings on Process server are not blocking access**.</span></span>  <span data-ttu-id="07e1b-142">Als u een proxyserver gebruikt, zorg er Hallo proxyservernaam omzet door Hallo DNS-server.</span><span class="sxs-lookup"><span data-stu-id="07e1b-142">If you are using a Proxy Server, ensure hello proxy server name is resolving by hello DNS server.</span></span>
<span data-ttu-id="07e1b-143">toocheck wat u hebt opgegeven tijdens het Hallo van de installatie van de configuratieserver.</span><span class="sxs-lookup"><span data-stu-id="07e1b-143">toocheck what you have provided at hello time of Configuration Server setup.</span></span> <span data-ttu-id="07e1b-144">Ga tooregistry sleutel</span><span class="sxs-lookup"><span data-stu-id="07e1b-144">Go tooregistry key</span></span>

    `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Azure Site Recovery\ProxySettings`

<span data-ttu-id="07e1b-145">Nu u ervoor te zorgen dat dezelfde instellingen worden gebruikt door Azure Site Recovery agent toosend gegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="07e1b-145">Now ensure that hello same settings are being used by Azure Site Recovery agent toosend data.</span></span>
<span data-ttu-id="07e1b-146">Back-up van Microsoft Azure Search</span><span class="sxs-lookup"><span data-stu-id="07e1b-146">Search Microsoft Azure  Backup</span></span> 

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/mab.png)

<span data-ttu-id="07e1b-148">Open het en klik op actie > Eigenschappen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="07e1b-148">Open it and click on Action > Change Properties.</span></span> <span data-ttu-id="07e1b-149">U ziet onder het tabblad Proxy-configuratie Hallo proxy-adres, moet dezelfde zoals aangegeven in de registerinstellingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="07e1b-149">Under Proxy Configuration tab, you should see hello proxy address, which should be same as shown by hello registry settings.</span></span> <span data-ttu-id="07e1b-150">Als dit niet het geval is, wijzig het toohello hetzelfde adres.</span><span class="sxs-lookup"><span data-stu-id="07e1b-150">If not, please change it toohello same address.</span></span>

![Replicatie inschakelen](./media/site-recovery-protection-common-errors/mabproxy.png)

* <span data-ttu-id="07e1b-152">**Controleer als u bandbreedte niet op processerver beperkt**: Hallo bandbreedte vergroten en controleer of Hallo probleem nog bestaat.</span><span class="sxs-lookup"><span data-stu-id="07e1b-152">**Check if Throttle bandwidth is not constrained on Process server**:  Increase hello bandwidth  and check if hello problem still exists.</span></span>

##<a name="next-steps"></a><span data-ttu-id="07e1b-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07e1b-153">Next steps</span></span>
<span data-ttu-id="07e1b-154">Als u meer hulp nodig hebt, klikt u vervolgens boeken uw query te[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="07e1b-154">If you need more help, then post your query too[ASR forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).</span></span> <span data-ttu-id="07e1b-155">We hebben een actieve community en een van onze technici kunnen tooassist worden u.</span><span class="sxs-lookup"><span data-stu-id="07e1b-155">We have an active community and one of our engineers will be able tooassist you.</span></span>
