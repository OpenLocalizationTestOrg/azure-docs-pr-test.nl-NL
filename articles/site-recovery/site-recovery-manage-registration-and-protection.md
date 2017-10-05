---
title: Verwijderen van servers en schakel de beveiliging | Microsoft Docs
description: Dit artikel wordt beschreven hoe u servers vanaf een Site Recovery-kluis registratie en beveiliging voor virtuele machines en fysieke servers uit te schakelen.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: ef1f31d5-285b-4a0f-89b5-0123cd422d80
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 03/27/2017
ms.author: raynew
ms.openlocfilehash: 43f92a35dc9b04584badd1c9f1152470246b5012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="remove-servers-and-disable-protection"></a>Servers verwijderen en beveiliging uitschakelen

De Azure Site Recovery-service draagt bij aan uw strategie voor zakelijke continuïteit en noodherstel herstel (BCDR). De service regelt de replicatie, failover en herstel van virtuele machines en fysieke servers. Machines kunnen worden gerepliceerd naar Azure of een secundaire on-premises datacentrum. Lees voor een snel overzicht [Wat is Azure Site Recovery?](site-recovery-overview.md)

Dit artikel wordt beschreven hoe u servers vanaf een Recovery Services-kluis in de Azure portal voor registratie en hoe schakel de beveiliging voor de machines die beveiligd zijn door Site Recovery.

U kunt onder aan dit artikel of op het [Azure Recovery Services-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr) opmerkingen of vragen plaatsen.

## <a name="unregister-a-connected-configuration-server"></a>Hef de registratie van een server verbonden configuration

Als u virtuele VMware-machines of fysieke Windows of Linux-servers naar Azure repliceren, kunt u de registratie van een configuratieserver verbonden uit een kluis als volgt ongedaan maken:

1. Schakel de machinebeveiliging. In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.
2. Elk beleid loskoppelen. In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **replicatiebeleid**, dubbelklik op het bijbehorende beleid. Met de rechtermuisknop op de configuratieserver > **koppeling verbreken**.
3. Verwijder alle aanvullende on-premises proces of het hoofddoelservers. In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, met de rechtermuisknop op de server > **verwijderen**.
4. Verwijder de configuratieserver.
5. Handmatig verwijderen van de Mobility-service uitgevoerd op de hoofddoelserver (dit is ofwel een afzonderlijke server of op de configuratieserver wordt uitgevoerd).
6. Verwijder eventuele aanvullende processen beheerservers.
7. Verwijder de configuratieserver.
8. Verwijder het exemplaar van MySQL die is geïnstalleerd met Site Recovery op de configuratieserver.
9. Verwijder de sleutel in het register van de configuratieserver ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Hef de registratie van een niet-verbonden configuratieserver

Als u virtuele VMware-machines of fysieke Windows of Linux-servers naar Azure repliceren, kunt u de registratie van een niet-verbonden configuratieserver uit een kluis als volgt ongedaan maken:

1. Schakel de machinebeveiliging. In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**. Selecteer **stoppen met het beheer van de machine**.
2. Verwijder alle aanvullende on-premises proces of het hoofddoelservers. In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, met de rechtermuisknop op de server > **verwijderen**.
3. Verwijder de configuratieserver.
4. Handmatig verwijderen van de Mobility-service uitgevoerd op de hoofddoelserver (dit is ofwel een afzonderlijke server of op de configuratieserver wordt uitgevoerd).
5. Verwijder eventuele aanvullende processen beheerservers.
6. Verwijder de configuratieserver.
7. Verwijder het exemplaar van MySQL die is geïnstalleerd met Site Recovery op de configuratieserver.
8. Verwijder de sleutel in het register van de configuratieserver ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Hef de registratie van een verbonden VMM-beheerserver

Als een best practice is het raadzaam dat u de VMM-server registratie ongedaan maken wanneer deze verbonden met Azure. Dit zorgt ervoor dat de instellingen op de VMM-servers (en op andere VMM-servers met gekoppelde clouds) juist worden opgeschoond. U moet een niet-verbonden server alleen verwijderen als er een permanente probleem met de connectiviteit. Als de VMM-server niet is verbonden, moet u een script om de instellingen op te schonen handmatig uitvoeren.

1. Stoppen met het repliceren van virtuele machines in clouds op de VMM-server die u wilt verwijderen.
2. Verwijder eventuele Netwerktoewijzingen gebruikt door clouds op de VMM-server die u wilt verwijderen. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing > **verwijderen**.
3. Loskoppelen van beleidsregels voor replicatie van clouds op de VMM-server die u wilt verwijderen.  In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op het bijbehorende beleid. Met de rechtermuisknop op de cloud > **koppeling verbreken**.
4. Verwijder de VMM-server of het actieve VMM-knooppunt. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, met de rechtermuisknop op de server > **verwijderen**.
5. De Provider op de VMM-server handmatig verwijderen. Als u een cluster hebt, verwijderen van alle knooppunten.
6. Als u naar Azure repliceert, verwijdert u de Microsoft Recovery Services-agent handmatig van de Hyper-V-hosts in de verwijderde clouds.



### <a name="unregister-an-unconnected-vmm-server"></a>Hef de registratie van een niet-verbonden VMM-server

1. Stoppen met het repliceren van virtuele machines in clouds op de VMM-server die u wilt verwijderen.
2. Verwijder eventuele Netwerktoewijzingen gebruikt door clouds op de VMM-server die u wilt verwijderen. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing > **verwijderen**.
3. Noteer de ID van de VMM-server.
4. Loskoppelen van beleidsregels voor replicatie van clouds op de VMM-server die u wilt verwijderen.  In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op het bijbehorende beleid. Met de rechtermuisknop op de cloud > **koppeling verbreken**.
5. Verwijder de VMM-server of het actieve knooppunt. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, met de rechtermuisknop op de server > **verwijderen**.
6. Downloaden en uitvoeren van de [script voor opschoning](http://aka.ms/asr-cleanup-script-vmm) op de VMM-server. Open PowerShell met de **als Administrator uitvoeren** optie, het uitvoeringsbeleid voor het standaardbereik (LocalMachine) wijzigen. Geef in het script wordt de ID van de VMM-beheerserver die u wilt verwijderen. Het script wordt verwijderd voor registratie en cloud koppelen van gegevens van de server.
5. Het script voor opschoning uitvoeren op een andere VMM-servers met clouds die zijn gekoppeld aan clouds op de VMM-server die u wilt verwijderen.
6. Het script voor opschoning uitvoeren op een andere passieve VMM-clusterknooppunten die de Provider geïnstalleerd hebben.
7. De Provider op de VMM-server handmatig verwijderen. Als u een cluster hebt, verwijderen van alle knooppunten.
8. Als u repliceren naar Azure, kunt u de Microsoft Recovery Services-agent van Hyper-V-hosts in de verwijderde clouds.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Hef de registratie van een Hyper-V-host in een Hyper-V-Site

Hyper-V-hosts die niet worden beheerd door VMM worden verzameld in een Hyper-V-site. Verwijder een host in een Hyper-V-site als volgt:

1. Schakel replicatie voor Hyper-V virtuele machines zich bevinden op de host uit.
2. Maak beleid voor de Hyper-V-site. In **Site Recovery-infrastructuur** > **voor Hyper-V-Sites** >  **replicatiebeleid**, dubbelklik op het bijbehorende beleid. Met de rechtermuisknop op de site > **koppeling verbreken**.
3. Verwijder de Hyper-V-hosts. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Hosts**, met de rechtermuisknop op de server > **verwijderen**.
4. De Hyper-V-site verwijderen nadat alle hosts uit deze zijn verwijderd. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Sites**, met de rechtermuisknop op de site > **verwijderen**.
5. Voer het volgende script op elke Hyper-V-host die u hebt verwijderd. Het script ruimt instellingen op de server en het deregistreren bij de kluis.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run the script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove the old Azure Site Recovery Provider related properties. Do you want to continue (Y/N) ?"
            $choice =  Read-Host

            if (!($choice -eq 'Y' -or $choice -eq 'y'))
            {
            "Stopping cleanup."
            return;
            }

            $serviceName = "dra"
            $service = Get-Service -Name $serviceName
            if ($service.Status -eq "Running")
            {
                "Stopping the Azure Site Recovery service..."
                net stop $serviceName
            }

            $asrHivePath = "HKLM:\SOFTWARE\Microsoft\Azure Site Recovery"
            $registrationPath = $asrHivePath + '\Registration'
            $proxySettingsPath = $asrHivePath + '\ProxySettings'
            $draIdvalue = 'DraID'

            if (Test-Path $asrHivePath)
            {
                if (Test-Path $registrationPath)
                {
                    "Removing registration related registry keys."    
                    Remove-Item -Recurse -Path $registrationPath
                }

                if (Test-Path $proxySettingsPath)
            {
                    "Removing proxy settings"
                    Remove-Item -Recurse -Path $proxySettingsPath
                }

                $regNode = Get-ItemProperty -Path $asrHivePath
                if($regNode.DraID -ne $null)
                {            
                    "Removing DraId"
                    Remove-ItemProperty -Path $asrHivePath -Name $draIdValue
                }
                "Registry keys removed."
            }

            # First retrive all the certificates to be deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete the certs
            "Removing all related certificates"
            foreach ($cert in $ASRcerts)
            {
                $store.Remove($cert)
            }
        }catch
        {    
            [system.exception]
            Write-Host "Error occured" -ForegroundColor "Red"
            $error[0]
            Write-Host "FAILED" -ForegroundColor "Red"
        }
        popd``



## <a name="disable-protection-for-a-vmware-vm-or-physical-server"></a>Schakel de beveiliging voor een VMware-VM of de fysieke server

1. In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.
2. In **Machine verwijderen**, selecteer een van de volgende opties:
    - **Schakel de beveiliging voor de machine (aanbevolen)**. Gebruik deze optie om te stoppen met het repliceren van de machine. Site Recovery-instellingen worden automatisch worden opgeruimd. Alleen ziet u deze optie in de volgende omstandigheden:
        - **U hebt gewijzigd dat het VM-volume**: wanneer u de grootte van een volume dat de virtuele machine naar een kritieke status verplaatst. Selecteer deze optie schakelt beveiliging behoud herstelpunten in Azure. Wanneer u beveiliging voor de computer opnieuw inschakelt, worden de gegevens voor het formaat is gewijzigd volume wordt overgedragen naar Azure.
        - **U hebt onlangs een failover uitvoert**: nadat u een failover wilt testen van uw omgeving hebt uitgevoerd, selecteer deze optie om te beginnen met het lokale computers opnieuw beveiligen. Elke virtuele machine wordt uitgeschakeld en moet u beveiliging voor deze opnieuw in te schakelen. Het uitschakelen van de machine met deze instelling heeft geen invloed op de replica virtuele machine in Azure. De Mobility-service niet worden verwijderd van de machine.
    - **Stoppen met het beheer van de machine**. Als u deze optie selecteert, wordt de machine alleen worden verwijderd uit de kluis. Lokale beveiligingsinstellingen voor de machine worden niet beïnvloed. Om instellingen op de computer te verwijderen en de machine verwijderen uit het Azure-abonnement, moet u het opschonen van de instellingen met het verwijderen van de Mobility-service.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Schakel de beveiliging voor een virtuele Hyper-V-machine in een VMM-cloud

1. In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.
2. In **Machine verwijderen**, selecteer een van de volgende opties:

    - **Schakel de beveiliging voor de machine (aanbevolen)**. Gebruik deze optie om te stoppen met het repliceren van de machine. Site Recovery-instellingen worden automatisch worden opgeruimd.
    - **Stoppen met het beheer van de machine**. Als u deze optie selecteert, wordt de machine alleen worden verwijderd uit de kluis. Lokale beveiligingsinstellingen voor de machine worden niet beïnvloed. Om instellingen op de computer te verwijderen en de machine verwijderen uit het Azure-abonnement, moet u de instellingen handmatig opschonen met de onderstaande instructies. Houd er rekening mee dat als u selecteert om de virtuele machine en de harde schijven te verwijderen, ze moeten worden verwijderd uit de doellocatie.

### <a name="clean-up-protection-settings---replication-to-a-secondary-vmm-site"></a>Opschonen van de beveiligingsinstellingen - replicatie naar een secundaire VMM-site

Als u hebt geselecteerd **stoppen met het beheer van de machine** en repliceren van een secundaire site, dit script uitvoert op de primaire server om de instellingen voor de primaire virtuele machine op te schonen. Klik op de knop PowerShell om de VMM PowerShell-console te openen in de VMM-console. SQLVM1 vervangen door de naam van de virtuele machine.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Voer dit script om de instellingen voor de secundaire virtuele machine op te schonen op de secundaire VMM-server:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Vernieuwen op de secundaire VMM-beheerserver, de virtuele machines op de Hyper-V-hostserver, zodat de secundaire virtuele machine opnieuw wordt gedetecteerd in de VMM-console.
4. De bovenstaande stappen wissen om de replicatie-instellingen op de VMM-server. Als u wilt om replicatie stoppen voor de virtuele machine, voer het volgende script geselecteerd de primaire en secundaire virtuele machines. SQLVM1 vervangen door de naam van de virtuele machine.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-to-azure"></a>Opschonen van de beveiligingsinstellingen - replicatie naar Azure

1. Als u hebt geselecteerd **stoppen met het beheer van de machine** en u repliceert naar Azure, dit script uitvoert op de bron-VMM-server, met behulp van PowerShell uit de VMM-console.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. De bovenstaande stappen schakelt u de replicatie-instellingen op de VMM-server. Om replicatie stoppen voor de virtuele machine op de Hyper-V-hostserver, moet u dit script uitvoert. SQLVM1 vervangen door de naam van uw virtuele machine en host01.contoso.com met de naam van de Hyper-V-hostserver.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Schakel de beveiliging voor een virtuele Hyper-V-machine in een Hyper-V-Site

Gebruik deze procedure als u Hyper-V-machines naar Azure zonder een VMM-server repliceert.

1. In **beveiligde Items** > **gerepliceerde Items**, met de rechtermuisknop op de machine > **verwijderen**.
2. In **Machine verwijderen**, kunt u de volgende opties selecteren:

   - **Schakel de beveiliging voor de machine (aanbevolen)**. Gebruik deze optie om te stoppen met het repliceren van de machine. Site Recovery-instellingen worden automatisch worden opgeruimd.
   - **Stoppen met het beheer van de machine**. Als u deze optie wordt alleen de machine worden verwijderd uit de kluis. Lokale beveiligingsinstellingen voor de machine worden niet beïnvloed. Om instellingen op de computer te verwijderen en de virtuele machine verwijderen uit het Azure-abonnement, moet u de instellingen handmatig opschonen. Als u de virtuele machine en de harde schijven die ze worden verwijderd uit de doellocatie te verwijderen.
3. Als u hebt geselecteerd **stoppen met het beheer van de machine**, dit script uitvoert op de Hyper-V-host bronserver replicatie voor de virtuele machine verwijderen. SQLVM1 vervangen door de naam van de virtuele machine.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
