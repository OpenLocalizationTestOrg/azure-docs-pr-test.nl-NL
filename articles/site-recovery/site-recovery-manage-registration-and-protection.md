---
title: aaaRemove servers en schakel de beveiliging | Microsoft Docs
description: Dit artikel wordt beschreven hoe toounregister servers vanaf een Site Recovery-kluis en toodisable beveiliging voor virtuele machines en fysieke servers.
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
ms.openlocfilehash: 95f20433f782c93685ad4bae93c6bc0e2d2f2356
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-servers-and-disable-protection"></a>Servers verwijderen en beveiliging uitschakelen

Hello Azure Site Recovery-service draagt bij tooyour zakelijke continuïteit en noodherstelplan (BCDR). Hallo service regelt de replicatie, failover en herstel van virtuele machines en fysieke servers. Machines kunnen gerepliceerde tooAzure of tooa secundaire on-premises datacenter zijn. Lees voor een snel overzicht [Wat is Azure Site Recovery?](site-recovery-overview.md)

Dit artikel wordt beschreven hoe toounregister servers vanaf een Recovery Services-kluis in hello Azure-portal en hoe toodisable beveiliging voor machines beveiligd door Site Recovery.

Eventuele opmerkingen of vragen plaatsen onderin Hallo van dit artikel of op Hallo [Azure Recovery Services-Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="unregister-a-connected-configuration-server"></a>Hef de registratie van een server verbonden configuration

Als u VMware-machines of fysieke servers tooAzure van Windows of Linux repliceert, kunt u de registratie van een configuratieserver verbonden uit een kluis als volgt ongedaan maken:

1. Schakel de machinebeveiliging. In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.
2. Elk beleid loskoppelen. In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **replicatiebeleid**, dubbelklikt u op Hallo het beleid is gekoppeld. Klik met de rechtermuisknop Hallo configuratieserver > **koppeling verbreken**.
3. Verwijder alle aanvullende on-premises proces of het hoofddoelservers. In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, klik met de rechtermuisknop Hallo server > **Verwijderen**.
4. Hallo configuratieserver verwijderen.
5. Hallo Mobility-service wordt uitgevoerd op de hoofddoelserver Hallo handmatig te verwijderen (dit is ofwel een afzonderlijke server of configuratieserver Hallo uitgevoerd).
6. Verwijder eventuele aanvullende processen beheerservers.
7. Hallo configuratieserver verwijderen.
8. Verwijderen op de configuratieserver hello, Hallo exemplaar van MySQL die is geïnstalleerd met Site Recovery.
9. In het register van de configuratieserver Hallo HALLO hallo sleutel verwijderen ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-unconnected-configuration-server"></a>Hef de registratie van een niet-verbonden configuratieserver

Als u VMware-machines of fysieke servers tooAzure van Windows of Linux repliceert, kunt u de registratie van een niet-verbonden configuratieserver uit een kluis als volgt ongedaan maken:

1. Schakel de machinebeveiliging. In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**. Selecteer **stoppen met het beheer van Hallo machine**.
2. Verwijder alle aanvullende on-premises proces of het hoofddoelservers. In **Site Recovery-infrastructuur** > **voor VMWare en fysieke Machines** > **configuratieservers**, klik met de rechtermuisknop Hallo server > **Verwijderen**.
3. Hallo configuratieserver verwijderen.
4. Hallo Mobility-service wordt uitgevoerd op de hoofddoelserver Hallo handmatig te verwijderen (dit is ofwel een afzonderlijke server of configuratieserver Hallo uitgevoerd).
5. Verwijder eventuele aanvullende processen beheerservers.
6. Hallo configuratieserver verwijderen.
7. Verwijderen op de configuratieserver hello, Hallo exemplaar van MySQL die is geïnstalleerd met Site Recovery.
8. In het register van de configuratieserver Hallo HALLO hallo sleutel verwijderen ``HKEY_LOCAL_MACHINE\Software\Microsoft\Azure Site Recovery``.

## <a name="unregister-a-connected-vmm-server"></a>Hef de registratie van een verbonden VMM-beheerserver

Als een best practice is het raadzaam Hallo VMM-server wanneer deze is verbonden tooAzure registratie ongedaan te maken. Dit zorgt ervoor dat de instellingen op Hallo VMM-servers (en op andere VMM-servers met gekoppelde clouds) juist worden opgeschoond. U moet een niet-verbonden server alleen verwijderen als er een permanente probleem met de connectiviteit. Als het Hallo-VMM-server niet is verbonden, moet u toomanually een script tooclean instellingen uitvoeren.

1. Stoppen met het repliceren van virtuele machines in clouds op Hallo gewenste tooremove VMM-server.
2. Verwijder eventuele Netwerktoewijzingen door clouds op Hallo VMM-server die u wilt dat toodelete gebruikt. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing Hallo >  **Verwijder**.
3. Beleidsregels voor replicatie van clouds op de VMM-server die u wilt dat tooremove Hallo loskoppelen.  In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op Hallo gekoppeld beleid. Met de rechtermuisknop op Hallo cloud > **koppeling verbreken**.
4. Hallo VMM-server of actieve VMM-knooppunt verwijderen. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, klik met de rechtermuisknop Hallo server >  **Verwijder**.
5. Hallo Provider handmatig op Hallo VMM-server verwijderen. Als u een cluster hebt, verwijderen van alle knooppunten.
6. Als u tooAzure repliceert, verwijdert u Hallo Microsoft Recovery Services agent handmatig van de Hyper-V-hosts in de clouds Hallo verwijderd.



### <a name="unregister-an-unconnected-vmm-server"></a>Hef de registratie van een niet-verbonden VMM-server

1. Stoppen met het repliceren van virtuele machines in clouds op Hallo gewenste tooremove VMM-server.
2. Verwijder eventuele Netwerktoewijzingen door clouds op Hallo VMM-server die u wilt dat toodelete gebruikt. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **netwerktoewijzing**, met de rechtermuisknop op de netwerktoewijzing Hallo >  **Verwijder**.
3. Houd er rekening mee Hallo-ID van Hallo VMM-server.
4. Beleidsregels voor replicatie van clouds op de VMM-server die u wilt dat tooremove Hallo loskoppelen.  In **Site Recovery-infrastructuur** > **voor System Center VMM** >  **replicatiebeleid**, dubbelklik op Hallo gekoppeld beleid. Met de rechtermuisknop op Hallo cloud > **koppeling verbreken**.
5. Hallo VMM-server of actief knooppunt verwijderen. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **VMM-Servers**, klik met de rechtermuisknop Hallo server >  **Verwijder**.
6. Downloaden en uitvoeren van Hallo [script voor opschoning](http://aka.ms/asr-cleanup-script-vmm) op Hallo VMM-server. Open PowerShell met Hallo **als Administrator uitvoeren** optie, toochange Hallo-uitvoeringsbeleid voor het Hallo-standaardbereik (LocalMachine). Geef Hallo-ID van VMM-server die u wilt dat tooremove Hallo in Hallo-script. Hallo script verwijderd registratie en cloud koppelingsgegevens van Hallo-server.
5. Hallo-script voor opschoning uitvoeren op een andere VMM-servers die clouds die zijn gekoppeld aan clouds op Hallo VMM-server die u wilt dat tooremove bevatten.
6. Hallo-script voor opschoning uitvoeren op een andere passieve VMM-clusterknooppunten die Hallo die provider geïnstalleerd hebben.
7. Hallo Provider handmatig op Hallo VMM-server verwijderen. Als u een cluster hebt, verwijderen van alle knooppunten.
8. Als u tooAzure repliceren, kunt u Hallo Microsoft Recovery Services-agent van Hyper-V-hosts in clouds Hallo verwijderd.

## <a name="unregister-a-hyper-v-host-in-a-hyper-v-site"></a>Hef de registratie van een Hyper-V-host in een Hyper-V-Site

Hyper-V-hosts die niet worden beheerd door VMM worden verzameld in een Hyper-V-site. Verwijder een host in een Hyper-V-site als volgt:

1. Replicatie voor Hyper-V-machines bevindt zich op Hallo host uitschakelen.
2. Beleid voor Hyper-V-site Hallo loskoppelen. In **Site Recovery-infrastructuur** > **voor Hyper-V-Sites** >  **replicatiebeleid**, dubbelklik op Hallo gekoppeld beleid. Klik met de rechtermuisknop Hallo site > **koppeling verbreken**.
3. Verwijder de Hyper-V-hosts. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Hosts**, klik met de rechtermuisknop Hallo server >  **Verwijder**.
4. Hallo Hyper-V-site verwijderen nadat alle hosts uit deze zijn verwijderd. In **Site Recovery-infrastructuur** > **voor System Center VMM** > **Hyper-V-Sites**, klik met de rechtermuisknop Hallo site >  **Verwijder**.
5. Voer Hallo script volgen op elke Hyper-V-host die u hebt verwijderd. Hallo script ruimt instellingen op Hallo-server en het deregistreren bij Hallo kluis.


        `` pushd .
        try
        {
             $windowsIdentity=[System.Security.Principal.WindowsIdentity]::GetCurrent()
             $principal=new-object System.Security.Principal.WindowsPrincipal($windowsIdentity)
             $administrators=[System.Security.Principal.WindowsBuiltInRole]::Administrator
             $isAdmin=$principal.IsInRole($administrators)
             if (!$isAdmin)
             {
                "Please run hello script as an administrator in elevated mode."
                $choice = Read-Host
                return;       
             }

            $error.Clear()    
            "This script will remove hello old Azure Site Recovery Provider related properties. Do you want toocontinue (Y/N) ?"
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
                "Stopping hello Azure Site Recovery service..."
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

            # First retrive all hello certificates toobe deleted
            $ASRcerts = Get-ChildItem -Path cert:\localmachine\my | where-object {$_.friendlyname.startswith('ASR_SRSAUTH_CERT_KEY_CONTAINER') -or $_.friendlyname.startswith('ASR_HYPER_V_HOST_CERT_KEY_CONTAINER')}
            # Open a cert store object
            $store = New-Object System.Security.Cryptography.X509Certificates.X509Store("My","LocalMachine")
            $store.Open('ReadWrite')
            # Delete hello certs
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

1. In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.
2. In **Machine verwijderen**, selecteer een van de volgende opties:
    - **Schakel de beveiliging voor Hallo-machine (aanbevolen)**. Gebruik deze optie toostop Hallo machine repliceren. Site Recovery-instellingen worden automatisch worden opgeruimd. Alleen ziet u deze optie in de volgende omstandigheden Hallo:
        - **U hebt het formaat gewijzigd Hallo VM volume**: wanneer u de grootte van een volume Hallo virtuele machine een kritieke status krijgt. Selecteer deze optie toodisables beveiliging behoud herstelpunten in Azure. Wanneer u beveiliging voor Hallo machine opnieuw inschakelt, Hallo voor Hallo aangepast volume worden overgedragen tooAzure.
        - **U hebt onlangs een failover uitvoert**: nadat u hebt een tootest failover uitgevoerd op uw omgeving, selecteert u deze optie toostart lokale machines opnieuw beveiligen. Elke virtuele machine wordt uitgeschakeld en moet u tooenable beveiliging voor deze opnieuw. Uitschakelen Hallo-machine met deze instelling heeft geen invloed op Hallo replica virtuele machine in Azure. Geen Hallo Mobility-service niet verwijderen van Hallo-machine.
    - **Stoppen met het beheer van Hallo machine**. Als u deze optie selecteert, worden Hallo-machine uit kluis Hallo alleen worden verwijderd. Beveiligingsinstellingen van de lokale voor Hallo machine worden niet beïnvloed. instellingen voor tooremove op Hallo-machine en tooremove Hallo machine van Azure-abonnement hello, moet u tooclean Hallo instellingen met het verwijderen van de Mobility-service Hallo.

## <a name="disable-protection-for-a-hyper-v-vm-in-a-vmm-cloud"></a>Schakel de beveiliging voor een virtuele Hyper-V-machine in een VMM-cloud

1. In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.
2. In **Machine verwijderen**, selecteer een van de volgende opties:

    - **Schakel de beveiliging voor Hallo-machine (aanbevolen)**. Gebruik deze optie toostop Hallo machine repliceren. Site Recovery-instellingen worden automatisch worden opgeruimd.
    - **Stoppen met het beheer van Hallo machine**. Als u deze optie selecteert, worden Hallo-machine uit kluis Hallo alleen worden verwijderd. Beveiligingsinstellingen van de lokale voor Hallo machine worden niet beïnvloed. tooremove instellingen op Hallo-machine en tooremove Hallo machine van Azure-abonnement Hallo, moet u tooclean Hallo instellingen handmatig met Hallo onderstaande instructies. Houd er rekening mee dat als u toodelete Hallo virtuele machine en de harde schijven selecteert, ze moeten worden verwijderd uit Hallo target-locatie.

### <a name="clean-up-protection-settings---replication-tooa-secondary-vmm-site"></a>Opschonen van de beveiligingsinstellingen - replicatie tooa secundaire VMM-site

Als u hebt geselecteerd **stoppen met het beheer van Hallo machine** en u tooa secundaire site repliceren dit script uitvoert op Hallo primaire server tooclean Hallo instellingen opgeven voor Hallo primaire virtuele machine. Klik in de VMM-console Hallo Hallo PowerShell knop tooopen Hallo VMM PowerShell-console. SQLVM1 vervangen door Hallo-naam van uw virtuele machine.

         ``$vm = get-scvirtualmachine -Name "SQLVM1"
         Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Voer dit script tooclean Hallo instellingen opgeven voor Hallo secundaire virtuele machine op Hallo secundaire VMM-server:

        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Remove-SCVirtualMachine -VM $vm -Force``
3. Vernieuwen op Hallo secundaire VMM-server Hallo virtuele machines op Hallo Hyper-V-hostserver, zodat hello secundaire virtuele machine opnieuw in Hallo VMM-console detecteren opgehaald.
4. replicatie-instellingen op de VMM-server Hallo HALLO hallo bovenstaande stappen gewist. Als u wilt dat replicatie toostop Hallo virtuele machine uitvoeren na script geselecteerd Hallo Hallo primaire en secundaire virtuele machines. SQLVM1 vervangen door Hallo-naam van uw virtuele machine.

        ``Remove-VMReplication –VMName “SQLVM1”``

### <a name="clean-up-protection-settings---replication-tooazure"></a>Beveiligingsinstellingen voor - replicatie tooAzure opschonen

1. Als u hebt geselecteerd **stoppen met het beheer van Hallo machine** en u tooAzure repliceren, dit script uitvoert op Hallo bron VMM-server met behulp van PowerShell vanaf Hallo VMM-console.
        ``$vm = get-scvirtualmachine -Name "SQLVM1"
        Set-SCVirtualMachine -VM $vm -ClearDRProtection``
2. Hallo bovenstaande stappen schakelt Hallo replicatie-instellingen op Hallo VMM-server. toostop replicatie voor Hallo virtuele machine Hallo Hyper-V-hostserver waarop dit script uitvoert. SQLVM1 vervangen door Hallo-naam van uw virtuele machine en host01.contoso.com met Hallo van Hallo Hyper-V-hostserver.

        ``$vmName = "SQLVM1"
        $hostName  = "host01.contoso.com"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'" -computername $hostName
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"  -computername $hostName
        $replicationService.RemoveReplicationRelationship($vm.__PATH)``


## <a name="disable-protection-for-a-hyper-v-vm-in-a-hyper-v-site"></a>Schakel de beveiliging voor een virtuele Hyper-V-machine in een Hyper-V-Site

Gebruik deze procedure als u Hyper-V-machines tooAzure zonder een VMM-server repliceert.

1. In **beveiligde Items** > **gerepliceerde Items**, klik met de rechtermuisknop Hallo machine > **verwijderen**.
2. In **Machine verwijderen**, kunt u Hallo volgende opties selecteren:

   - **Schakel de beveiliging voor Hallo-machine (aanbevolen)**. Gebruik deze optie toostop Hallo machine repliceren. Site Recovery-instellingen worden automatisch worden opgeruimd.
   - **Stoppen met het beheer van Hallo machine**. Als u deze optie selecteert Hallo machine wordt alleen verwijderd uit het Hallo-kluis. Beveiligingsinstellingen van de lokale voor Hallo machine worden niet beïnvloed. instellingen voor tooremove op Hallo-machine en tooremove Hallo virtuele machine van Azure-abonnement hello, moet u tooclean Hallo instellingen handmatig. Als u toodelete Hallo virtuele machine en de harde schijven die ze worden verwijderd uit de doellocatie Hallo selecteert.
3. Als u hebt geselecteerd **stoppen met het beheer van Hallo machine**, voer dit script op Hallo bron Hyper-V-hostserver, tooremove replicatie voor Hallo virtuele machine. SQLVM1 vervangen door Hallo-naam van uw virtuele machine.

        $vmName = "SQLVM1"
        $vm = Get-WmiObject -Namespace "root\virtualization\v2" -Query "Select * From Msvm_ComputerSystem Where ElementName = '$vmName'"
        $replicationService = Get-WmiObject -Namespace "root\virtualization\v2"  -Query "Select * From Msvm_ReplicationService"
        $replicationService.RemoveReplicationRelationship($vm.__PATH)
