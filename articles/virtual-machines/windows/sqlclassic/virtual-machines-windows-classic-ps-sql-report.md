---
title: aaaUse PowerShell tooCreate een virtuele machine met een Native modus rapportserver | Microsoft Docs
description: 'In dit onderwerp wordt beschreven en wordt u begeleid bij Hallo-implementatie en configuratie van een SQL Server Reporting Services native modus rapportserver in een virtuele Machine van Azure. '
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a>Gebruik PowerShell tooCreate een Azure VM met een Native modus Report Server
> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

In dit onderwerp wordt beschreven en wordt u begeleid bij Hallo-implementatie en configuratie van een SQL Server Reporting Services native modus rapportserver in een virtuele Machine van Azure. Hallo stappen in dit document een combinatie van handmatige stappen toocreate Hallo virtuele machine en een Windows PowerShell-script voor tooconfigure Reporting Services op Hallo VM. Hallo-configuratiescript bevat een firewallpoort worden geopend voor HTTP of HTTPs.

> [!NOTE]
> Als u geen vereist **HTTPS** op Hallo rapportserver **slaat u stap 2**.
> 
> Ga nadat Hallo VM is gemaakt in stap 1, toohello sectie gebruik script tooconfigure Hallo report server- en HTTP. Nadat u Hallo script uitvoert, is de rapportserver Hallo gereed toouse.

## <a name="prerequisites-and-assumptions"></a>Vereisten en veronderstellingen
* **Azure-abonnement**: Controleer of het aantal kernen dat beschikbaar is in uw Azure-abonnement Hallo. Als u VM-grootte van aanbevolen Hallo maakt **A3**, moet u **4** beschikbaar kernen. Als u een VM-grootte van **A2**, moet u **2** beschikbaar kernen.
  
  * tooverify hello core limiet van uw abonnement op Hallo klassieke Azure-portal, klik op instellingen in het linkerdeelvenster Hallo en vervolgens klikt u op informatie over het gebruik in het bovenste menu Hallo.
  * tooincrease hello quotum voor kernen, neem contact op met [ondersteuning van Azure](https://azure.microsoft.com/support/options/). Zie voor informatie over de grootte van virtuele machine [grootten van virtuele machines voor Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* **Windows PowerShell-scripts**: Hallo onderwerp wordt ervan uitgegaan dat u een werkende basiskennis hebben van Windows PowerShell. Zie voor meer informatie over het gebruik van Windows PowerShell Hallo volgende:
  
  * [Windows PowerShell op WindowsServer wordt gestart](https://technet.microsoft.com/library/hh847814.aspx)
  * [Aan de slag met Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a>Stap 1: Een Azure-Machine inrichten
1. Blader toohello klassieke Azure-portal.
2. Klik op **virtuele Machines** in het linkerdeelvenster Hallo.
   
    ![Microsoft azure virtuele machines](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. Klik op **Nieuw**.
   
    ![Knop Nieuw](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. Klik op **vanuit galerie**.
   
    ![nieuwe virtuele machine vanuit galerie](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. Klik op **SQL Server 2014 RTM Standard – Windows Server 2012 R2** en klik vervolgens op Hallo pijl toocontinue.
   
    ![Volgende](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    Als u Hallo Reporting Services gegevensgestuurde abonnementen functie nodig hebt, kiest u **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**. Zie voor meer informatie over SQL Server-edities en functieondersteuning [functies ondersteund door het Hallo-edities van SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).
6. Op Hallo **Virtuele-machineconfiguratie** pagina, Hallo volgende velden te bewerken:
   
   * Als er meer dan één **versie RELEASEDATUM**, selecteer Hallo meest recente versie.
   * **Naam van virtuele Machine**: naam van de machine Hallo wordt ook gebruikt op de volgende configuratiepagina Hallo als Hallo standaard Cloud Service DNS-naam. Hallo DNS-naam moet uniek zijn in hello Azure-service. Overweeg het Hallo VM configureren met de computernaam van een die wordt beschreven welke Hallo VM wordt gebruikt voor. Bijvoorbeeld ssrsnativecloud.
   * **Laag**: standaard
   * **Grootte: A3** wordt aanbevolen Hallo VM-grootte voor SQL Server-werkbelastingen. Als een virtuele machine alleen als een rapportserver gebruikt wordt, is een VM-grootte van A2 voldoende tenzij Hallo rapportserver optreedt in een grote werkbelasting. Zie voor een VM prijsgegevens, [prijzen van virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/).
   * **Nieuwe gebruikersnaam**: Hallo die u opgeeft als een beheerder op Hallo VM wordt gemaakt.
   * **Nieuw wachtwoord** en **bevestigen**. Dit wachtwoord wordt gebruikt voor nieuwe Hallo-administrator-account en het wordt aanbevolen dat een sterk wachtwoord te gebruiken.
   * Klik op **Volgende**. ![volgende](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
7. Op de volgende pagina Hallo Hallo volgende velden te bewerken:
   
   * **Cloudservice**: Selecteer **Maak een nieuwe Cloudservice**.
   * **Cloud-Service DNS-naam**: dit Hallo openbare DNS-naam van Hallo Cloudservice die is gekoppeld aan Hallo VM is. Hallo is standaard Hallo naam die u hebt getypt voor Hallo VM-naam. Als in latere stappen van Hallo onderwerp u een vertrouwd certificaat voor SSL maakt en vervolgens Hallo DNS-naam wordt gebruikt voor de waarde Hallo Hallo '**verleend aan**' hello certificaat.
   * **Regio/affiniteit groep/virtueel netwerk**: Kies Hallo regio dichtstbijzijnde tooyour eindgebruikers.
   * **Storage-Account**: een automatisch gegenereerde opslagaccount gebruiken.
   * **Beschikbaarheidsset**: geen.
   * **EINDPUNTEN** behouden Hallo **extern bureaublad** en **PowerShell** eindpunten en voeg vervolgens een HTTP- of HTTPS-eindpunt, afhankelijk van uw omgeving.
     
     * **HTTP**: openbare en particuliere poorten zijn standaard Hallo **80**. Let op: als u een particuliere poort dan 80, wijzigt u **$HTTPport = 80** in Hallo HTTP-script.
     * **HTTPS**: openbare en particuliere poorten zijn standaard Hallo **443**. Een best practice bij beveiliging wordt toochange Hallo particuliere poort en uw firewall en Hallo report server toouse Hallo particuliere poort configureren. Zie voor meer informatie over eindpunten [hoe tooSet van communicatie met een virtuele Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Let op: als u een andere poort dan 443, wijzigt u de parameter Hallo **$HTTPsport = 443** in Hallo HTTPS-script.
   * Klik op volgende. ![Volgende](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. Op de laatste pagina van wizard Hallo Hallo houden Hallo standaard **Hallo VM-agent installeren** geselecteerde. Hallo stappen in dit onderwerp, maken geen gebruik Hallo VM-agent, maar als u van plan tookeep deze virtuele machine bent, VM-agent Hallo en -extensies kunt u tooenhance hij CM.  Zie voor meer informatie over de VM-agent Hallo [VM-Agent en -extensies – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/). Een Hallo standaard extensies geïnstalleerd ad met Hallo 'BGINFO'-extensie die wordt weergegeven op de VM-bureaublad hello, systeemgegevens zoals intern IP-adres en de vrije ruimte station.
9. Klik op voltooien. ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. Hallo **Status** Hallo VM wordt weergegeven als **starten (inrichten)** tijdens Hallo inrichten proces en vervolgens wordt weergegeven, **met** wanneer Hallo VM is ingericht en gereed toouse.

## <a name="step-2-create-a-server-certificate"></a>Stap 2: Een servercertificaat maken
> [!NOTE]
> Als u HTTPS niet op de rapportserver hello vereist, kunt u **slaat u stap 2** en ga toohello sectie **script tooconfigure Hallo report server- en HTTP gebruiken**. Gebruik Hallo HTTP script tooquickly Hallo rapportserver en Hallo report server bevindt zich nu toouse configureren.

In de volgorde toouse HTTPS op Hallo VM moet u een vertrouwd certificaat voor SSL. Afhankelijk van uw scenario kunt u een van de volgende twee methoden hello gebruiken:

* Een geldig SSL-certificaat uitgegeven door een certificeringsinstantie (CA) en wordt vertrouwd door Microsoft. Hallo CA-basiscertificaten zijn vereiste toobe gedistribueerd via Hallo Microsoft Root Certificate Program. Zie voor meer informatie over dit programma [Windows en Windows Phone 8 SSL Root Certificate Program (lid CA's)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) en [inleiding toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).
* Een zelfondertekend certificaat. Zelfondertekende certificaten worden niet aanbevolen voor productieomgevingen.

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a>toouse een certificaat gemaakt door een vertrouwde certificeringsinstantie (CA)
1. **Vraag een servercertificaat voor de website van de Hallo van een certificeringsinstantie**. 
   
    U kunt beide toogenerate een certificaataanvraagbestand (Certreq.txt) te sturen tooa certificeringsinstantie (CA) of toogenerate een aanvraag voor een online-certificeringsinstantie Hallo Wizard Webservercertificaat. Bijvoorbeeld: Microsoft Certificate Services in Windows Server 2012. Afhankelijk van Hallo identificatie zekerheidsniveau die worden aangeboden door uw servercertificaat, is enkele dagen tooseveral maanden voor Hallo certification authority tooapprove uw aanvraag en verzendt u een certificaatbestand. 
   
    Zie voor meer informatie over het aanvragen van een servercertificaten Hallo volgende: 
   
   * Gebruik [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).
   * Security Tools tooAdminister Windows Server 2012.
     
     [Security Tools tooAdminister Windows Server 2012](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > Hallo **verleend aan** veld Hallo vertrouwde SSL-certificaat moet worden Hallo dezelfde als Hallo **Cloud Service DNS-naam** u hebt gebruikt voor nieuwe VM Hallo.

2. **Hallo-servercertificaat installeren op de webserver Hallo**. Hallo-webserver is in dit geval Hallo VM dat hosts Hallo rapportserver en Hallo-website is gemaakt in latere stappen bij het configureren van Reporting Services. Zie voor meer informatie over het Hallo-servercertificaat installeren op Hallo-webserver met behulp van Hallo MMC-module certificaat [een servercertificaat installeren](https://technet.microsoft.com/library/cc740068).
   
    Als u wilt dat toouse Hallo script is opgenomen in dit onderwerp, rapportserver tooconfigure hello, waarde van de certificaten Hallo Hallo **vingerafdruk** is vereist als een parameter van het Hallo-script. Zie Hallo volgende sectie voor meer informatie over hoe tooobtain vingerafdruk van certificaat Hallo Hallo.
3. Hallo server certificaat toohello-rapportserver toewijzen. Hallo-toewijzing is voltooid in de volgende sectie Hallo bij het configureren van Hallo-rapportserver.

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a>toouse hello zelfondertekende certificaten voor virtuele Machines
Een zelfondertekend certificaat is gemaakt op Hallo VM wanneer Hallo VM is ingericht. Hallo-certificaat heeft dezelfde naam als Hallo VM DNS-naam Hallo. In de volgorde tooavoid certificaatfouten, is het vereist dat Hallo-certificaat wordt vertrouwd op Hallo VM zichzelf en voor alle gebruikers van Hallo-site.

1. tootrust hello basis-CA van Hallo-certificaat op Hallo lokale VM toevoegen Hallo certificaat toohello **Trusted Root Certification Authorities**. Hallo Hieronder volgt een samenvatting van Hallo stappen vereist. Zie voor gedetailleerde stappen op hoe tootrust CA Hallo [een servercertificaat installeren](https://technet.microsoft.com/library/cc740068).
   
   1. Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden. Afhankelijk van de browserconfiguratie van uw, hebt u mogelijk na vragen aan gebruiker toosave een RDP-bestand voor het verbinden van toohello VM.
      
       ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Hallo VM gebruikersnaam, gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken. 
      
       In Hallo installatiekopie te volgen, Hallo VM-naam is bijvoorbeeld **ssrsnativecloud** en gebruikersnaam Hallo **testgebruiker**.
      
       ![aanmeldingsnaam opgenomen vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. Mmc.exe worden uitgevoerd. Zie voor meer informatie [hoe: certificaten weergeven met Hallo MMC-module](https://msdn.microsoft.com/library/ms788967.aspx).
   3. In de consoletoepassing Hallo **bestand** menu toevoegen Hallo **certificaten** -module, selecteer **computeraccount** wanneer u wordt gevraagd en klik vervolgens op **volgende**.
   4. Selecteer **lokale Computer** toomanage en klik vervolgens op **voltooien**.
   5. Klik op **Ok** en vouw vervolgens Hallo **certificaten - persoonlijke** knooppunten en klik vervolgens op **certificaten**. Hallo certificaat Hallo DNS-naam van Hallo VM heeft de naam en eindigt op **cloudapp.net**. Met de rechtermuisknop op de certificaatnaam Hallo en klik op **kopie**.
   6. Vouw Hallo **Trusted Root Certification Authorities** knooppunt en klik met de rechtermuisknop **certificaten** en klik vervolgens op **plakken**.
   7. toovalidate dubbele klikt u op de certificaatnaam Hallo onder **Trusted Root Certification Authorities** en controleer of er zijn geen fouten ziet u uw certificaat. Als u wilt dat toouse Hallo HTTPS script is opgenomen in dit onderwerp, rapportserver tooconfigure hello, waarde van de certificaten Hallo Hallo **vingerafdruk** is vereist als een parameter van het Hallo-script. **tooget hello vingerafdrukwaarde**, Hallo volgende voltooien. Er is ook een PowerShell-voorbeeld tooretrieve Hallo vingerafdruk in sectie [script tooconfigure Hallo report server- en HTTPS gebruiken](#use-script-to-configure-the-report-server-and-HTTPS).
      
      1. Dubbelklik op Hallo van Hallo certificaat, bijvoorbeeld ssrsnativecloud.cloudapp.net.
      2. Klik op Hallo **Details** tabblad.
      3. Klik op **vingerafdruk**. Hallo-waarde van de vingerafdruk van het Hallo wordt weergegeven in het veld Hallo details, bijvoorbeeld a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.
      4. Kopieer de vingerafdruk Hallo en Hallo waarde opslaan voor later of Hallo script nu bewerken.
      5. (*) Voordat u Hallo script uitvoert, verwijdert u Hallo spaties tussen Hallo-waardeparen. Hallo-vingerafdruk die al eerder is vermeld zou bijvoorbeeld nu a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f zijn.
      6. Hallo server certificaat toohello-rapportserver toewijzen. Hallo-toewijzing is voltooid in de volgende sectie Hallo bij het configureren van Hallo-rapportserver.

Als u een zelfondertekend SSL-certificaat gebruikt, overeenkomt met met Hallo-naam op Hallo certificaat al Hallo-hostnaam van Hallo VM. Daarom Hallo Hallo machine DNS is al geregistreerd globaal en toegankelijk zijn vanaf elke client.

## <a name="step-3-configure-hello-report-server"></a>Stap 3: Hallo Report Server configureren
Deze sectie helpt u bij het Hallo VM als een rapportserver voor native-modus van Reporting Services configureren. U kunt een Hallo methoden tooconfigure Hallo rapportserver volgende gebruiken:

* Hallo script tooconfigure Hallo-rapportserver gebruiken
* Gebruik Configuration Manager tooConfigure hello Report Server.

Zie voor meer stappen gedetailleerde, Hallo sectie [toohello verbinding maken met virtuele Machine en Start de Reporting Services Configuration Manager Hallo](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).

**Verificatie-Opmerking:** Windows-verificatie is de aanbevolen methode voor netwerkverificatie Hallo en het Hallo-standaardverificatie Reporting Services is. Alleen gebruikers die zijn geconfigureerd op Hallo VM toegankelijk Reporting Services en toegewezen tooReporting Services-functies.

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a>Script tooconfigure Hallo report server- en HTTP gebruiken
toouse hello Windows PowerShell-script tooconfigure Hallo rapportserver, volledige Hallo stappen te volgen. Hallo-configuratie bevat HTTP, niet HTTPS:

1. Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden. Afhankelijk van de browserconfiguratie van uw, hebt u mogelijk na vragen aan gebruiker toosave een RDP-bestand voor het verbinden van toohello VM.
   
    ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Hallo VM gebruikersnaam, gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken. 
   
    In Hallo installatiekopie te volgen, Hallo VM-naam is bijvoorbeeld **ssrsnativecloud** en gebruikersnaam Hallo **testgebruiker**.
   
    ![aanmeldingsnaam opgenomen vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Open op Hallo VM, **Windows PowerShell ISE** met beheerdersbevoegdheden. Hallo PowerShell ISE is standaard geïnstalleerd op WindowsServer 2012. Het verdient aanbeveling dat u Hallo ISE gebruiken in plaats van een standaard Windows PowerShell-venster zodat Hallo script in Hallo ISE te plakken, Hallo script wijzigen en vervolgens Hallo-script uitvoeren.
3. Klik in Windows PowerShell ISE op Hallo **weergave** menu en klik vervolgens op **scriptvenster weergeven**.
4. Hallo volgende script kopiëren en plakken van Hallo script in Windows PowerShell ISE-scriptvenster Hallo.
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. Als u Hallo VM met een HTTP-poort 80 gemaakt, wijzigt u Hallo parameter $HTTPport = 80.
6. Hallo-script is momenteel geconfigureerd voor Reporting Services. Als u toorun Hallo script voor Reporting Services wilt, wijzigt u Hallo versie gedeelte van Hallo pad toohello naamruimte te 'v11' op Hallo Get-WmiObject-instructie.
7. Hallo-script uitvoeren.

**Validatie**: tooverify die Hallo standaardrapport serverfunctionaliteit werkt, Zie Hallo [controleren Hallo configuratie](#verify-the-configuration) verderop in dit onderwerp.

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a>Script tooconfigure Hallo report server- en HTTPS gebruiken
toouse Windows PowerShell tooconfigure Hallo rapportserver, volledige Hallo stappen te volgen. Hallo configuratie omvat HTTPS, niet HTTP.

1. Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden. Afhankelijk van de browserconfiguratie van uw, hebt u mogelijk na vragen aan gebruiker toosave een RDP-bestand voor het verbinden van toohello VM.
   
    ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) Hallo VM gebruikersnaam, gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken. 
   
    In Hallo installatiekopie te volgen, Hallo VM-naam is bijvoorbeeld **ssrsnativecloud** en gebruikersnaam Hallo **testgebruiker**.
   
    ![aanmeldingsnaam opgenomen vm](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. Open op Hallo VM, **Windows PowerShell ISE** met beheerdersbevoegdheden. Hallo PowerShell ISE is standaard geïnstalleerd op WindowsServer 2012. Het verdient aanbeveling dat u Hallo ISE gebruiken in plaats van een standaard Windows PowerShell-venster zodat Hallo script in Hallo ISE te plakken, Hallo script wijzigen en vervolgens Hallo-script uitvoeren.
3. tooenable uitvoeren van scripts, Hallo volgende Windows PowerShell-opdracht uitvoeren:
   
        Set-ExecutionPolicy RemoteSigned
   
    Vervolgens kunt u de volgende tooverify Hallo beleid Hallo uitvoeren:
   
        Get-ExecutionPolicy
4. In **Windows PowerShell ISE**, klikt u op Hallo **weergave** menu en klik vervolgens op **scriptvenster weergeven**.
5. Hallo volgende script en plak deze in Windows PowerShell ISE-scriptvenster Hallo kopiëren.
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. Hallo wijzigen **$certificatehash** parameter in Hallo script:
   
   * Dit is een **vereist** parameter. Als u de waarde van de Hallo-certificaat niet uit de vorige stappen Hallo hebt opgeslagen, gebruikt u een van de volgende methoden toocopy Hallo certificaat-hash-waarde uit Hallo certificaten vingerafdruk Hallo.:
     
       Open Windows PowerShell ISE op Hallo VM, en Hallo volgende opdracht uitvoeren:
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       Hallo-uitvoer ziet er vergelijkbare toohello volgende. Als het Hallo-script retourneert een lege regel, Hallo VM heeft geen een certificaat dat zo is geconfigureerd, Zie de sectie Hallo [toouse Hallo virtuele Machines zelfondertekende certificaten](#to-use-the-virtual-machines-self-signed-certificate).
     
     OF
   * Op Hallo van mmc.exe VM worden uitgevoerd en voeg vervolgens Hallo **certificaten** -module.
   * Onder Hallo **vertrouwde basiscertificeringsinstanties** knooppunt dubbelklikt u op de certificaatnaam van uw. Als u zelf-ondertekend certificaat Hallo Hallo VM Hallo certificaat Hallo DNS-naam van Hallo VM heeft de naam en eindigt op **cloudapp.net**.
   * Klik op Hallo **Details** tabblad.
   * Klik op **vingerafdruk**. Hallo-waarde van de vingerafdruk van het Hallo wordt weergegeven in het veld Hallo details, bijvoorbeeld af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6 ter a9 c3 66 4f 31 90 48
   * **Voordat u Hallo-script uitvoeren**, Hallo spaties tussen Hallo-waardeparen verwijderen. Bijvoorbeeld af1160b64b288d890a8212ff6ba9c3664f319048
7. Hallo wijzigen **$httpsport** parameter: 
   
   * Als u poort 443 voor HTTPS-eindpunt Hallo gebruikt, hoeft niet u tooupdate deze parameter in Hallo-script. Anders gebruiken Hallo poortwaarde die u hebt geselecteerd toen u persoonlijke Hallo HTTPS-eindpunt op Hallo VM geconfigureerd.
8. Hallo wijzigen **$DNSName** parameter: 
   
   * Hallo-script is geconfigureerd voor een certificaat met wild card $DNSName = '+'. Als u geen tooconfigure wilt voor een jokerteken certificaatbinding doen, uitcommentariëren $DNSName = ' + 'en inschakelen van de volgende regel, Hallo volledige $DNSNAme referentie, ## $DNSName="$server.cloudapp.net Hallo'.
     
       Hallo $DNSName waarde wijzigen als u niet dat de DNS-naam toouse Hallo van virtuele machine voor Reporting Services wilt. Als u Hallo-parameter gebruikt, Hallo certificaat moet ook gebruiken voor deze naam en de naam van de Hallo globaal op een DNS-server te registreren.
9. Hallo-script is momenteel geconfigureerd voor Reporting Services. Als u toorun Hallo script voor Reporting Services wilt, wijzigt u Hallo versie gedeelte van Hallo pad toohello naamruimte te 'v11' op Hallo Get-WmiObject-instructie.
10. Hallo-script uitvoeren.

**Validatie**: tooverify die Hallo standaardrapport serverfunctionaliteit werkt, Zie Hallo [controleren Hallo configuratie](#verify-the-connection) verderop in dit onderwerp. tooverify hello certificaatbinding open een opdrachtprompt met beheerdersbevoegdheden en Voer Hallo volgende opdracht:

    netsh http show sslcert

Hallo resultaat wordt Hallo volgende zijn:

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a>Gebruik Configuration Manager tooConfigure Hallo Report Server
Als u geen toorun Hallo PowerShell script tooconfigure Hallo report server, volgt u de Hallo stappen in deze sectie toouse Hallo Reporting Services native modus configuration manager tooconfigure Hallo rapportserver.

1. Selecteer in de klassieke Azure-portal hello, Hallo VM en klik op verbinden. Hallo-gebruikersnaam en wachtwoord die u hebt geconfigureerd tijdens het maken van VM hello gebruiken.
   
    ![verbinding maken met tooazure virtuele machine](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. Voer Windows update en installeer updates toohello VM. Als een herstart van Hallo VM vereist is, Hallo VM starten en verbinding toohello VM van Hallo klassieke Azure-portal.
3. Typ vanuit het startmenu Hallo op Hallo VM, **Reporting Services** en open **Reporting Services Configuration Manager**.
4. Laat de standaardwaarden Hallo voor **servernaam** en **rapportserverexemplaar**. Klik op **Verbinden**.
5. Klik in het linkerdeelvenster Hallo **URL van webservice**.
6. RS is standaard geconfigureerd voor HTTP poort 80 met IP-adres 'Alle toegewezen'. tooadd HTTPS:
   
   1. In **SSL-certificaat**: Selecteer Hallo certificaat dat u toouse, bijvoorbeeld [VM name]. cloudapp.net. Als er geen certificaten worden vermeld, raadpleegt u Hallo sectie **stap 2: Maak een servercertificaat** voor meer informatie over hoe Hallo certificaat op Hallo VM tooinstall en vertrouwt.
   2. Onder **SSL-poort**: 443 kiezen. Als u persoonlijke Hallo HTTPS-eindpunt geconfigureerd in Hallo VM met een andere particuliere poort, hier die waarde gebruiken.
   3. Klik op **toepassen** en wachten op Hallo bewerking toocomplete.
7. Klik in het linkerdeelvenster Hallo **Database**.
   
   1. Klik op **wijzigen Databas**e.
   2. Klik op **maken van een nieuw report server-database** en klik vervolgens op **volgende**.
   3. Laat de standaardwaarde Hallo **servernaam**: Hallo VM de naam en laat de standaardwaarde Hallo **verificatietype** als **huidige gebruiker** – **geïntegreerde beveiliging**. Klik op **Volgende**.
   4. Laat de standaardwaarde Hallo **databasenaam** als **ReportServer** en klik op **volgende**.
   5. Laat de standaardwaarde Hallo **verificatietype** als **Servicereferenties** en klik op **volgende**.
   6. Klik op **volgende** op Hallo **samenvatting** pagina.
   7. Wanneer het Hallo-configuratie is voltooid, klikt u op **voltooien**.
8. Klik in het linkerdeelvenster Hallo **URL van Report Manager**. Laat de standaardwaarde Hallo **virtuele map** als **rapporten** en klik op **toepassen**.
9. Klik op **afsluiten** tooclose Hallo Reporting Services Configuration Manager.

## <a name="step-4-open-windows-firewall-port"></a>Stap 4: Open Windows Firewall-poort
> [!NOTE]
> Als u een van de rapportserver voor Hallo scripts tooconfigure Hallo gebruikt, kunt u deze sectie overslaan. Hallo script een firewallpoort stap tooopen Hallo opgenomen. Hallo standaardwaarde is poort 80 voor HTTP en poort 443 voor HTTPS.
> 
> 

tooconnect op afstand tooReport Manager of Hallo melden Server op Hallo virtuele machine, een TCP-eindpunt is vereist op Hallo VM. Het is vereiste tooopen Hallo dezelfde in de firewall Hallo van de virtuele machine poort. Hallo-eindpunt is gemaakt toen Hallo VM is ingericht.

In deze sectie bevat algemene informatie over hoe tooopen firewallpoort Hallo. Zie voor meer informatie [een Firewall configureren voor toegang tot de Server van rapporten](https://technet.microsoft.com/library/bb934283.aspx)

> [!NOTE]
> Als u Hallo script tooconfigure Hallo-rapportserver gebruikt, kunt u deze sectie overslaan. Hallo script een firewallpoort stap tooopen Hallo opgenomen.
> 
> 

Als u een particuliere poort geconfigureerd voor HTTPS dan 443, wijzig Hallo script op de juiste wijze te volgen. poort tooopen **443** op Hallo Windows Firewall, Hallo volgende voltooien:

1. Open een Windows PowerShell-venster met beheerdersbevoegdheden.
2. Als u een andere poort dan 443 gebruikt wanneer u HTTPS-eindpunt Hallo geconfigureerd op Hallo VM, werk de poort in de volgende opdracht Hallo Hallo en Voer Hallo-opdracht:
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. Wanneer het Hallo-opdracht is voltooid, **Ok** wordt weergegeven in het Hallo-opdrachtprompt.

tooverify dat Hallo-poort is geopend, open een Windows PowerShell-venster en Voer Hallo volgende opdracht:

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a>Hallo-configuratie verifiëren
tooverify die Hallo standaardrapport serverfunctionaliteit nu werkt, open uw browser met beheerdersbevoegdheden en vervolgens de server ad-Rapportbeheer URL's voor het rapporteren van bladeren toohello volgende:

* Blader op Hallo VM, toohello report server-URL:
  
        http://localhost/reportserver
* Blader op Hallo VM, toohello report Manager-URL:
  
        http://localhost/Reports
* Bladeren naar uw lokale computer toohello **externe** report Manager op Hallo VM. Hallo DNS-naam in het volgende voorbeeld naar gelang van toepassing hello bijwerken. Als u wordt gevraagd om een wachtwoord, gebruik Hallo-beheerdersreferenties die u hebt gemaakt tijdens het Hallo VM is ingericht. Hallo-gebruikersnaam is in Hallo [domein]\[gebruikersnaam]-indeling, waarbij Hallo domein Hallo VM computernaam, bijvoorbeeld ssrsnativecloud\testuser is. Als u geen van HTTP gebruikmaakt**S**, verwijder Hallo **s** in Hallo-URL. Zie Hallo volgende sectie voor informatie over het maken van extra gebruikers op virtuele machine.
  
        https://ssrsnativecloud.cloudapp.net/Reports
* Blader toohello externe report server-URL van de lokale computer. Hallo DNS-naam in het volgende voorbeeld naar gelang van toepassing hello bijwerken. Als u HTTPS niet gebruikt, verwijdert u Hallo s in Hallo-URL.
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a>Gebruikers maken en toewijzen van rollen
Nadat rapporteren server configureren en controleren van hello, wordt een algemene beheertaak toocreate is een of meer gebruikers en gebruikers tooReporting Services rollen toewijzen. Zie voor meer informatie de volgende Hallo:

* [Een lokale gebruikersaccount maken](https://technet.microsoft.com/library/cc770642.aspx)
* [Toegang van de gebruiker verlenen tooa Report Server (Rapportbeheer)](https://msdn.microsoft.com/library/ms156034.aspx))
* [Maken en beheren van roltoewijzingen](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate en rapporten publiceren toohello Azure virtuele Machine
Hallo volgende tabel ziet u enkele Hallo opties beschikbaar toopublish bestaande rapporten uit een on-premises computer toohello rapportserver gehost op Hallo van Microsoft Azure Virtual Machine:

* **RS.exe script**: gebruik RS.exe script toocopy rapportitems uit en bestaande report server tooyour Microsoft Azure virtuele Machine. Zie voor meer informatie Hallo sectie 'Native modus tooNative Mode – Microsoft Azure virtuele Machine' in [voorbeeld Reporting Services rs.exe Script tooMigrate inhoud tussen rapportservers](https://msdn.microsoft.com/library/dn531017.aspx).
* **Report Builder**: Hallo virtuele machine bevat Hallo Klik-eenmaal versie van Microsoft SQL Server Report Builder. toostart Report builder Hallo eerst op Hallo virtuele machine:
  
  1. Start uw browser met beheerdersbevoegdheden.
  2. Blader tooreport manager op Hallo virtuele machine en klik op **Report Builder** in Hallo-lint.
     
     Zie voor meer informatie [installeren, verwijderen en ondersteunende Report Builder](https://technet.microsoft.com/library/dd207038.aspx).
* **SQL Server Data Tools: VM**: als u Hallo VM met SQL Server 2012 gemaakt, wordt SQL Server Data Tools op Hallo virtuele machine is geïnstalleerd en kan worden gebruikt toocreate **Report Server-projecten** en rapporten op Hallo virtuele machine. SQL Server Data Tools kunt publiceren Hallo rapporten toohello-rapportserver op Hallo virtuele machine.
  
    Als u met SQL server 2014 Hallo VM hebt gemaakt, kunt u SQL Server Data Tools - BI voor visual Studio installeren. Zie voor meer informatie de volgende Hallo:
  
  * [Microsoft SQL Server Data Tools - Business Intelligence voor Visual Studio 2013](https://www.microsoft.com/download/details.aspx?id=42313)
  * [Microsoft SQL Server Data Tools - Business Intelligence voor Visual Studio 2012](https://www.microsoft.com/download/details.aspx?id=36843)
  * [SQL Server Data Tools en SQL Server Business Intelligence (BI SSDT)](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* **SQL Server Data Tools: Extern**: op uw lokale computer, kunt u een Reporting Services-project maken in SQL Server Data Tools met Reporting Services-rapporten. Hallo project tooconnect toohello URL van webservice configureren.
  
    ![de Projecteigenschappen SSDT voor SQL Server Reporting Services-project](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* **Script gebruiken**: script toocopy rapportinhoud server gebruiken. Zie voor meer informatie [voorbeeld Reporting Services rs.exe Script tooMigrate inhoud tussen rapportservers](https://msdn.microsoft.com/library/dn531017.aspx).

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a>Als u geen van Hallo VM gebruikmaakt kosten minimaliseren
> [!NOTE]
> toominimize kosten voor uw Azure Virtual Machines als deze niet in gebruik is, sluit de Hallo VM van Hallo klassieke Azure-portal. Als u Energiebeheer van Windows hello binnen een VM-tooshut omlaag Hallo VM gebruikt, er zijn nog steeds in rekening gebracht Hallo dezelfde bedrag voor Hallo VM. tooreduce kosten, moet u tooshut omlaag Hallo VM in Hallo klassieke Azure-portal. Als u niet langer Hallo VM, toodelete Hallo VM onthouden en Hallo gekoppelde VHD-bestanden tooavoid opslagkosten. Zie voor meer informatie, veelgestelde vragen over het Hallo-sectie op [prijsinformatie voor virtuele Machines](https://azure.microsoft.com/pricing/details/virtual-machines/).

## <a name="more-information"></a>Meer informatie
### <a name="resources"></a>Resources
* Voor vergelijkbare inhoud gerelateerde tooa single server-implementatie van SQL Server Business Intelligence en SharePoint 2013, Zie [tooCreate gebruik Windows PowerShell een Azure virtuele machine met SQL Server BI en SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).
* Zie voor vergelijkbare inhoud gerelateerde tooa implementatie met meerdere servers van SQL Server Business Intelligence en SharePoint 2013 [implementeren SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).
* Raadpleeg voor algemene informatie gerelateerde toodeployments van SQL Server Business Intelligence in Azure Virtual Machines [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).
* Zie voor meer informatie over Hallo kosten van Azure compute-kosten, tabblad van de virtuele Machines Hallo van [Azure prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).

### <a name="community-content"></a>Inhoud van de community
* Zie voor stapsgewijze instructies voor het hoe een Reporting Services Native modus toocreate server melden zonder script te gebruiken, [hosten van SQL Reporting Service op Azure virtuele Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a>Koppelingen tooother resources voor SQL Server in Azure VM 's
[SQL Server op Azure Virtual Machines-overzicht](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

