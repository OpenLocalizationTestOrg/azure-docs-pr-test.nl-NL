---
title: aaaDeploy hello Site Recovery Mobility-service met Azure Automation DSC | Microsoft Docs
description: Beschrijft hoe toouse Azure Automation DSC tooautomatically hello Azure Site Recovery Mobility-service en Azure-agent implementeren voor VM VMware en fysieke server replicatie tooAzure
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="99560-103">Hallo Mobility-service met Azure Automation DSC voor replicatie van de virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="99560-103">Deploy hello Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="99560-104">In de Operations Management Suite bieden wij u met een uitgebreide back-up en noodherstel die u als onderdeel van uw bedrijfscontinuïteitsplan kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="99560-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="99560-105">We deze reis samen met Hyper-V gestart met behulp van Hyper-V Replica.</span><span class="sxs-lookup"><span data-stu-id="99560-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="99560-106">Maar er is uitgevouwen toosupport een heterogene setup omdat klanten hebben van meerdere hypervisors en platforms in hun clouds.</span><span class="sxs-lookup"><span data-stu-id="99560-106">But we have expanded toosupport a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="99560-107">Als u VMware werkbelastingen en/of fysieke servers vandaag, een beheerserver wordt uitgevoerd alle hello Azure Site Recovery-onderdelen in uw omgeving toohandle Hallo communicatie- en replicatie met Azure, als Azure de bestemming is.</span><span class="sxs-lookup"><span data-stu-id="99560-107">If you are running VMware workloads and/or physical servers today, a management server runs all of hello Azure Site Recovery components in your environment toohandle hello communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="99560-108">Hallo Site Recovery Mobility-service implementeren met behulp van Automation DSC</span><span class="sxs-lookup"><span data-stu-id="99560-108">Deploy hello Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="99560-109">Laten we beginnen als volgt een snel overzicht van de werking van deze beheerserver.</span><span class="sxs-lookup"><span data-stu-id="99560-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="99560-110">Hallo-beheerserver wordt uitgevoerd voor verschillende serverfuncties.</span><span class="sxs-lookup"><span data-stu-id="99560-110">hello management server runs several server roles.</span></span> <span data-ttu-id="99560-111">Een van deze functies is *configuratie*, die coördineert de communicatie en processen voor replicatie en herstel van gegevens beheert.</span><span class="sxs-lookup"><span data-stu-id="99560-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="99560-112">Bovendien Hallo *proces* rol fungeert als replicatiegateway.</span><span class="sxs-lookup"><span data-stu-id="99560-112">In addition, hello *process* role acts as a replication gateway.</span></span> <span data-ttu-id="99560-113">Deze rol ontvangt replicatiegegevens van beveiligde bronmachines, optimaliseert met caching, compressie en codering en stuurt vervolgens tooan Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="99560-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it tooan Azure storage account.</span></span> <span data-ttu-id="99560-114">Een van de functies voor Hallo Procesrol Hallo is ook toopush installatie van de machines tooprotected Hallo Mobility-service en uitvoeren van automatische detectie van virtuele VMware-machines.</span><span class="sxs-lookup"><span data-stu-id="99560-114">One of hello functions for hello process role is also toopush installation of hello Mobility service tooprotected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="99560-115">Als er een failback vanuit Azure, Hallo *hoofddoel* rol Hallo replicatiegegevens als onderdeel van deze bewerking wordt afgehandeld.</span><span class="sxs-lookup"><span data-stu-id="99560-115">If there's a failback from Azure, hello *master target* role will handle hello replication data as part of this operation.</span></span>

<span data-ttu-id="99560-116">Voor Hallo beveiligde machines moeten we afhankelijk zijn van Hallo *Mobility-service*.</span><span class="sxs-lookup"><span data-stu-id="99560-116">For hello protected machines, we rely on hello *Mobility service*.</span></span> <span data-ttu-id="99560-117">Dit onderdeel is geïmplementeerde tooevery machine (VM VMware of fysieke server) die u wilt dat tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="99560-117">This component is deployed tooevery machine (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="99560-118">Deze gegevens schrijfbewerkingen op Hallo machine vastgelegd en stuurt ze toohello managementserver (Procesrol).</span><span class="sxs-lookup"><span data-stu-id="99560-118">It captures data writes on hello machine and forwards them toohello management server (process role).</span></span>

<span data-ttu-id="99560-119">Wanneer u de bedrijfscontinuïteit betreft bent, is het belangrijk toounderstand uw werkbelastingen, uw infrastructuur en Hallo onderdelen betrokken.</span><span class="sxs-lookup"><span data-stu-id="99560-119">When you're dealing with business continuity, it's important toounderstand your workloads, your infrastructure, and hello components involved.</span></span> <span data-ttu-id="99560-120">U kunt vervolgens voldoen aan Hallo-vereisten voor uw beoogde hersteltijd (RTO) en een beoogd herstelpunt (RPO).</span><span class="sxs-lookup"><span data-stu-id="99560-120">You can then meet hello requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="99560-121">In deze context Hallo Mobility-service is sleutel tooensuring die uw workloads worden beveiligd, zoals u zou verwachten.</span><span class="sxs-lookup"><span data-stu-id="99560-121">In this context, hello Mobility service is key tooensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="99560-122">Hoe kunt u, op een geoptimaliseerde manier ervoor zorgen dat u een betrouwbare beveiligde ingesteld met behulp van een aantal onderdelen van Operations Management Suite hebt?</span><span class="sxs-lookup"><span data-stu-id="99560-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="99560-123">In dit artikel bevat een voorbeeld van hoe u Azure Automation Desired State Configuration (DSC), samen met de Site is hersteld, tooensure kunt die:</span><span class="sxs-lookup"><span data-stu-id="99560-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, tooensure that:</span></span>

* <span data-ttu-id="99560-124">Hallo Mobility-service en Azure VM-agent zijn geïmplementeerde toohello Windows-machines dat u wilt dat tooprotect.</span><span class="sxs-lookup"><span data-stu-id="99560-124">hello Mobility service and Azure VM agent are deployed toohello Windows machines that you want tooprotect.</span></span>
* <span data-ttu-id="99560-125">Hallo Mobility-service en Azure VM-agent worden altijd uitgevoerd als Azure Hallo replicatiedoel.</span><span class="sxs-lookup"><span data-stu-id="99560-125">hello Mobility service and Azure VM agent are always running when Azure is hello replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99560-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="99560-126">Prerequisites</span></span>
* <span data-ttu-id="99560-127">Een opslagplaats toostore Hallo vereiste installatie</span><span class="sxs-lookup"><span data-stu-id="99560-127">A repository toostore hello required setup</span></span>
* <span data-ttu-id="99560-128">Een opslagplaats toostore Hallo vereist wachtwoordzin tooregister met Hallo managementserver</span><span class="sxs-lookup"><span data-stu-id="99560-128">A repository toostore hello required passphrase tooregister with hello management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="99560-129">Een unieke wachtwoordzin wordt gegenereerd voor elke beheerserver.</span><span class="sxs-lookup"><span data-stu-id="99560-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="99560-130">Als u toodeploy meerdere beheerservers gaat, hebt u tooensure die Hallo juist wachtwoordzin in Hallo passphrase.txt bestand is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="99560-130">If you are going toodeploy multiple management servers, you have tooensure that hello correct passphrase is stored in hello passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="99560-131">Windows Management Framework (WMF) 5.0 is geïnstalleerd op Hallo-machines wilt u tooenable voor beveiliging (een vereiste voor Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="99560-131">Windows Management Framework (WMF) 5.0 installed on hello machines that you want tooenable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="99560-132">Als u wilt dat toouse DSC voor Windows-machines waarvoor WMF 4.0 is geïnstalleerd, raadpleegt u Hallo sectie [gebruik DSC in niet-verbonden omgevingen](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="99560-132">If you want toouse DSC for Windows machines that have WMF 4.0 installed, see hello section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="99560-133">Hallo Mobility-service kan worden geïnstalleerd via de opdrachtregel Hallo en verschillende argumenten.</span><span class="sxs-lookup"><span data-stu-id="99560-133">hello Mobility service can be installed through hello command line and accepts several arguments.</span></span> <span data-ttu-id="99560-134">Daarom wordt u toohave Hallo binaire bestanden (nadat ze het uitpakken van uw instellingen) nodig hebt en deze opslaan op een locatie waar u ze met behulp van een DSC-configuratie kunt terugvinden.</span><span class="sxs-lookup"><span data-stu-id="99560-134">That’s why you need toohave hello binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="99560-135">Stap 1: De binaire bestanden uitpakken</span><span class="sxs-lookup"><span data-stu-id="99560-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="99560-136">tooextract hello bestanden die u nodig hebt om deze installatie bladeren toohello directory op de beheerserver te volgen:</span><span class="sxs-lookup"><span data-stu-id="99560-136">tooextract hello files that you need for this setup, browse toohello following directory on your management server:</span></span>

    <span data-ttu-id="99560-137">**\Microsoft azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="99560-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="99560-138">In deze map ziet u een MSI-bestand met de naam:</span><span class="sxs-lookup"><span data-stu-id="99560-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="99560-139">**Microsoft ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="99560-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="99560-140">Hallo opdracht tooextract Hallo installatieprogramma volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="99560-140">Use hello following command tooextract hello installer:</span></span>

    <span data-ttu-id="99560-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="99560-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="99560-142">Selecteer alle bestanden en verzend deze tooa gecomprimeerde map.</span><span class="sxs-lookup"><span data-stu-id="99560-142">Select all files and send them tooa compressed (zipped) folder.</span></span>

<span data-ttu-id="99560-143">U hebt nu Hallo binaire bestanden moet u tooautomate Hallo setup Hallo Mobility-service met behulp van Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="99560-143">You now have hello binaries that you need tooautomate hello setup of hello Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="99560-144">Wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="99560-144">Passphrase</span></span>
<span data-ttu-id="99560-145">Vervolgens moet u toodetermine waar u tooplace deze gecomprimeerde map.</span><span class="sxs-lookup"><span data-stu-id="99560-145">Next, you need toodetermine where you want tooplace this zipped folder.</span></span> <span data-ttu-id="99560-146">U kunt een Azure storage-account gebruiken als weergegeven hoger toostore Hallo wachtwoordzin die u nodig hebt voor Hallo setup.</span><span class="sxs-lookup"><span data-stu-id="99560-146">You can use an Azure storage account, as shown later, toostore hello passphrase that you need for hello setup.</span></span> <span data-ttu-id="99560-147">Hallo-agent wordt vervolgens registreren met Hallo managementserver als onderdeel van het Hallo-proces.</span><span class="sxs-lookup"><span data-stu-id="99560-147">hello agent will then register with hello management server as part of hello process.</span></span>

<span data-ttu-id="99560-148">Hallo wachtwoordzin die u hebt verkregen tijdens de implementatie van de beheerserver Hallo kan tooa tekstbestand als passphrase.txt worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="99560-148">hello passphrase that you got when you deployed hello management server can be saved tooa text file as passphrase.txt.</span></span>

<span data-ttu-id="99560-149">Zowel de gecomprimeerde map Hallo en Hallo wachtwoordzin plaatsen in een specifieke container in hello Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="99560-149">Place both hello zipped folder and hello passphrase in a dedicated container in hello Azure storage account.</span></span>

![Locatie van de map](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="99560-151">Als u liever tookeep deze bestanden op een share op uw netwerk, kunt u dit doet.</span><span class="sxs-lookup"><span data-stu-id="99560-151">If you prefer tookeep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="99560-152">U hoeft alleen maar tooensure dat Hallo DSC-resource die u later gaat gebruiken toegang heeft en Hallo setup en wachtwoordzin krijgt.</span><span class="sxs-lookup"><span data-stu-id="99560-152">You just need tooensure that hello DSC resource that you will be using later has access and can get hello setup and passphrase.</span></span>

## <a name="step-2-create-hello-dsc-configuration"></a><span data-ttu-id="99560-153">Stap 2: Maak Hallo DSC-configuratie</span><span class="sxs-lookup"><span data-stu-id="99560-153">Step 2: Create hello DSC configuration</span></span>
<span data-ttu-id="99560-154">Hallo-installatie, is afhankelijk van WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="99560-154">hello setup depends on WMF 5.0.</span></span> <span data-ttu-id="99560-155">Hallo machine toosuccessfully toepassing hello configuratie via Automation DSC, WMF 5.0 moet toobe aanwezig.</span><span class="sxs-lookup"><span data-stu-id="99560-155">For hello machine toosuccessfully apply hello configuration through Automation DSC, WMF 5.0 needs toobe present.</span></span>

<span data-ttu-id="99560-156">Hallo-omgeving maakt gebruik van Hallo voorbeeld DSC-configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="99560-156">hello environment uses hello following example DSC configuration:</span></span>

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
<span data-ttu-id="99560-157">Hallo configuratie doet Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="99560-157">hello configuration will do hello following:</span></span>

* <span data-ttu-id="99560-158">Hallo variabelen vertelt Hallo-configuratie waarbij tooget Hallo binaire bestanden voor Hallo Mobility-service en hello Azure VM-agent, waarbij tooget Hallo wachtwoordzin en toostore Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="99560-158">hello variables will tell hello configuration where tooget hello binaries for hello Mobility service and hello Azure VM agent, where tooget hello passphrase, and where toostore hello output.</span></span>
* <span data-ttu-id="99560-159">Hallo configuratie importeert Hallo xPSDesiredStateConfiguration DSC-resource, zodat u kunt `xRemoteFile` toodownload Hallo bestanden uit de opslagplaats Hallo.</span><span class="sxs-lookup"><span data-stu-id="99560-159">hello configuration will import hello xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` toodownload hello files from hello repository.</span></span>
* <span data-ttu-id="99560-160">Hallo configuratie maakt een map waar u toostore Hallo binaire bestanden.</span><span class="sxs-lookup"><span data-stu-id="99560-160">hello configuration will create a directory where you want toostore hello binaries.</span></span>
* <span data-ttu-id="99560-161">Hallo archief resource wordt Hallo-bestanden in Hallo gecomprimeerde map uitpakken.</span><span class="sxs-lookup"><span data-stu-id="99560-161">hello archive resource will extract hello files from hello zipped folder.</span></span>
* <span data-ttu-id="99560-162">Hallo-pakket installeren resource installeren uit Hallo UNIFIEDAGENT Hallo Mobility-service. EXE-installatieprogramma met specifieke Hallo-argumenten.</span><span class="sxs-lookup"><span data-stu-id="99560-162">hello package Install resource will install hello Mobility service from hello UNIFIEDAGENT.EXE installer with hello specific arguments.</span></span> <span data-ttu-id="99560-163">(Hallo variabelen die Hallo argumenten samenstellen moeten toobe gewijzigd tooreflect uw omgeving.)</span><span class="sxs-lookup"><span data-stu-id="99560-163">(hello variables that construct hello arguments need toobe changed tooreflect your environment.)</span></span>
* <span data-ttu-id="99560-164">Hallo pakket AzureAgent resource installeert hello Azure VM-agent, die wordt aanbevolen voor elke virtuele machine die wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="99560-164">hello package AzureAgent resource will install hello Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="99560-165">Hello Azure VM-agent maakt het ook mogelijk tooadd extensies toohello VM na een failover.</span><span class="sxs-lookup"><span data-stu-id="99560-165">hello Azure VM agent also makes it possible tooadd extensions toohello VM after failover.</span></span>
* <span data-ttu-id="99560-166">Hallo zorgt service of meer resources ervoor dat Hallo Mobility-services gerelateerde en hello Azure-services worden altijd uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99560-166">hello service resource or resources will ensure that hello related Mobility services and hello Azure services are always running.</span></span>

<span data-ttu-id="99560-167">Hallo configuratie opslaan als **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="99560-167">Save hello configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="99560-168">Houd er rekening mee tooreplace hello CSIP in uw configuratie tooreflect Hallo werkelijke-beheerserver, zodat hello agent goed zijn verbonden en het gebruik van de juiste wachtwoordzin Hallo.</span><span class="sxs-lookup"><span data-stu-id="99560-168">Remember tooreplace hello CSIP in your configuration tooreflect hello actual management server, so that hello agent will be connected correctly and will use hello correct passphrase.</span></span>
>
>

## <a name="step-3-upload-tooautomation-dsc"></a><span data-ttu-id="99560-169">Stap 3: TooAutomation DSC uploaden</span><span class="sxs-lookup"><span data-stu-id="99560-169">Step 3: Upload tooAutomation DSC</span></span>
<span data-ttu-id="99560-170">Omdat Hallo DSC-configuratie die u hebt aangebracht, een vereiste resource DSC-module (xPSDesiredStateConfiguration) importeren wordt, moet u tooimport die module in Automation voordat u Hallo DSC-configuratie uploadt.</span><span class="sxs-lookup"><span data-stu-id="99560-170">Because hello DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need tooimport that module in Automation before you upload hello DSC configuration.</span></span>

<span data-ttu-id="99560-171">Meld u aan tooyour Automation-account te bladeren**activa** > **Modules**, en klik op **bladeren galerie**.</span><span class="sxs-lookup"><span data-stu-id="99560-171">Sign in tooyour Automation account, browse too**Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="99560-172">Hier kunt u zoeken naar Hallo-module en importeer het tooyour-account.</span><span class="sxs-lookup"><span data-stu-id="99560-172">Here you can search for hello module and import it tooyour account.</span></span>

![Module importeren](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="99560-174">Wanneer u klaar bent, gaat u tooyour machine waar u hello Azure Resource Manager-modules geïnstalleerd hebt en doorgaan tooimport Hallo nieuw gemaakte DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="99560-174">When you finish this, go tooyour machine where you have hello Azure Resource Manager modules installed and proceed tooimport hello newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="99560-175">Cmdlets voor importeren</span><span class="sxs-lookup"><span data-stu-id="99560-175">Import cmdlets</span></span>
<span data-ttu-id="99560-176">Aanmelden in PowerShell tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="99560-176">In PowerShell, sign in tooyour Azure subscription.</span></span> <span data-ttu-id="99560-177">Wijzig Hallo cmdlets tooreflect uw omgeving en uw Automation-accountgegevens in een variabele vastleggen:</span><span class="sxs-lookup"><span data-stu-id="99560-177">Modify hello cmdlets tooreflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="99560-178">Hallo configuratie tooAutomation DSC met behulp van de volgende cmdlet Hallo uploaden:</span><span class="sxs-lookup"><span data-stu-id="99560-178">Upload hello configuration tooAutomation DSC by using hello following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a><span data-ttu-id="99560-179">Hallo-configuratie in Automation DSC compileren</span><span class="sxs-lookup"><span data-stu-id="99560-179">Compile hello configuration in Automation DSC</span></span>
<span data-ttu-id="99560-180">Vervolgens moet u toocompile Hallo configuratie in Automation DSC, zodat u tooregister knooppunten tooit kunt starten.</span><span class="sxs-lookup"><span data-stu-id="99560-180">Next, you need toocompile hello configuration in Automation DSC, so that you can start tooregister nodes tooit.</span></span> <span data-ttu-id="99560-181">U bereiken die door het uitvoeren van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="99560-181">You achieve that by running hello following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="99560-182">Dit kan enkele minuten duren, omdat u in feite Hallo configuration toohello gehost DSC-pull service implementeert.</span><span class="sxs-lookup"><span data-stu-id="99560-182">This can take a few minutes, because you're basically deploying hello configuration toohello hosted DSC pull service.</span></span>

<span data-ttu-id="99560-183">Nadat u Hallo configuratie compileren, kunt u Hallo taakinformatie ophalen met behulp van PowerShell (Get-AzureRmAutomationDscCompilationJob) of met behulp van Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="99560-183">After you compile hello configuration, you can retrieve hello job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using hello [Azure portal](https://portal.azure.com/).</span></span>

![Taak ophalen](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="99560-185">U hebt nu gepubliceerd en uw DSC-configuratie tooAutomation DSC geüpload.</span><span class="sxs-lookup"><span data-stu-id="99560-185">You have now successfully published and uploaded your DSC configuration tooAutomation DSC.</span></span>

## <a name="step-4-onboard-machines-tooautomation-dsc"></a><span data-ttu-id="99560-186">Stap 4: Vrijgeven machines tooAutomation DSC</span><span class="sxs-lookup"><span data-stu-id="99560-186">Step 4: Onboard machines tooAutomation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="99560-187">Een van de Hallo-vereisten voor het voltooien van dit scenario is dat uw Windows-machines worden bijgewerkt met de meest recente versie van WMF Hallo.</span><span class="sxs-lookup"><span data-stu-id="99560-187">One of hello prerequisites for completing this scenario is that your Windows machines are updated with hello latest version of WMF.</span></span> <span data-ttu-id="99560-188">U kunt downloaden en installeer de juiste versie van Hallo voor uw platform van Hallo [Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="99560-188">You can download and install hello correct version for your platform from hello [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="99560-189">U maakt nu een metaconfig voor DSC dat u tooyour knooppunten toepast.</span><span class="sxs-lookup"><span data-stu-id="99560-189">You will now create a metaconfig for DSC that you will apply tooyour nodes.</span></span> <span data-ttu-id="99560-190">toosucceed hierbij moet u tooretrieve Hallo eindpunt-URL en Hallo primaire sleutel voor uw geselecteerde Automation-account in Azure.</span><span class="sxs-lookup"><span data-stu-id="99560-190">toosucceed with this, you need tooretrieve hello endpoint URL and hello primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="99560-191">U vindt deze waarden onder **sleutels** op Hallo **alle instellingen** blade voor Hallo Automation-account.</span><span class="sxs-lookup"><span data-stu-id="99560-191">You can find these values under **Keys** on hello **All settings** blade for hello Automation account.</span></span>

![Sleutelwaarden](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="99560-193">In dit voorbeeld hebt u een fysieke server van Windows Server 2012 R2 waarop tooprotect met behulp van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="99560-193">In this example, you have a Windows Server 2012 R2 physical server that you want tooprotect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a><span data-ttu-id="99560-194">Controleren of er bestandsbewerkingen rename in Hallo register</span><span class="sxs-lookup"><span data-stu-id="99560-194">Check for any pending file rename operations in hello registry</span></span>
<span data-ttu-id="99560-195">Voordat u tooassociate Hallo server met Hallo Automation DSC-eindpunt, wordt u aangeraden te controleren of in behandeling zijnde rename bestandsbewerkingen in Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="99560-195">Before you start tooassociate hello server with hello Automation DSC endpoint, we recommend that you check for any pending file rename operations in hello registry.</span></span> <span data-ttu-id="99560-196">Ze mogelijk verbieden Hallo setup is voltooid vanwege tooa opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="99560-196">They might prohibit hello setup from finishing due tooa pending reboot.</span></span>

<span data-ttu-id="99560-197">Voer Hallo cmdlet tooverify er is geen opnieuw opstarten in behandeling op Hallo-server te volgen:</span><span class="sxs-lookup"><span data-stu-id="99560-197">Run hello following cmdlet tooverify that there’s no pending reboot on hello server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="99560-198">Als u dit leeg ziet, bent u OK tooproceed.</span><span class="sxs-lookup"><span data-stu-id="99560-198">If this shows empty, you are OK tooproceed.</span></span> <span data-ttu-id="99560-199">Als dat niet het geval is, moet u dit oplossen door het Hallo-server opnieuw opstarten tijdens een onderhoudsvenster.</span><span class="sxs-lookup"><span data-stu-id="99560-199">If not, you should address this by rebooting hello server during a maintenance window.</span></span>

<span data-ttu-id="99560-200">tooapply Hallo-configuratie op Hallo van server, start Hallo PowerShell Integrated Scripting Environment (ISE) en Voer Hallo script volgen.</span><span class="sxs-lookup"><span data-stu-id="99560-200">tooapply hello configuration on hello server, start hello PowerShell Integrated Scripting Environment (ISE) and run hello following script.</span></span> <span data-ttu-id="99560-201">Dit is in wezen een DSC lokale configuratie die Hallo Local Configuration Manager-engine tooregister Hello Automation DSC-service zoekt en Hallo specifieke configuratie (ASRMobilityService.localhost) ophalen.</span><span class="sxs-lookup"><span data-stu-id="99560-201">This is essentially a DSC local configuration that will instruct hello Local Configuration Manager engine tooregister with hello Automation DSC service and retrieve hello specific configuration (ASRMobilityService.localhost).</span></span>

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

<span data-ttu-id="99560-202">Deze configuratie wordt Hallo Local Configuration Manager engine tooregister zelf met Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="99560-202">This configuration will cause hello Local Configuration Manager engine tooregister itself with Automation DSC.</span></span> <span data-ttu-id="99560-203">Ook wordt vastgesteld hoe Hallo engine moet worden toegepast, wat dit moet doen als er een configuratie-afwijking (ApplyAndAutoCorrect) en hoe dit moet doorgaan met Hallo configuratie als een herstart vereist is.</span><span class="sxs-lookup"><span data-stu-id="99560-203">It will also determine how hello engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with hello configuration if a reboot is required.</span></span>

<span data-ttu-id="99560-204">Nadat u dit script uitvoert, mag Hallo knooppunt tooregister beginnen met Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="99560-204">After you run this script, hello node should start tooregister with Automation DSC.</span></span>

![Knooppunt-registratie in voortgang](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="99560-206">Als u terug toohello Azure-portal gaat, ziet u dat zojuist geregistreerde Hallo-knooppunt is nu verschenen in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="99560-206">If you go back toohello Azure portal, you can see that hello newly registered node has now appeared in hello portal.</span></span>

![Geregistreerde knooppunt in het Hallo-portal](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="99560-208">Op Hallo van server, kunt u de volgende PowerShell-cmdlet tooverify die Hallo knooppunt is correct geregistreerd Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="99560-208">On hello server, you can run hello following PowerShell cmdlet tooverify that hello node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="99560-209">Nadat het Hallo-configuratie is opgehaalde en toegepaste toohello server, kunt u dit controleren door het uitvoeren van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="99560-209">After hello configuration has been pulled and applied toohello server, you can verify this by running hello following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="99560-210">Hallo-uitvoer ziet dat die Hallo-server heeft de configuratie is opgehaald:</span><span class="sxs-lookup"><span data-stu-id="99560-210">hello output shows that hello server has successfully pulled its configuration:</span></span>

![Uitvoer](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="99560-212">Bovendien setup Hallo Mobility-service heeft een eigen logboekbestanden die kan worden gevonden op *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="99560-212">In addition, hello Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="99560-213">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="99560-213">That’s it.</span></span> <span data-ttu-id="99560-214">U hebt nu geïmplementeerd en geregistreerd Hallo Mobility-service op de gewenste tooprotect met behulp van Site Recovery Hallo-machine.</span><span class="sxs-lookup"><span data-stu-id="99560-214">You have now successfully deployed and registered hello Mobility service on hello machine that you want tooprotect by using Site Recovery.</span></span> <span data-ttu-id="99560-215">DSC ervoor dat er altijd Hallo vereist-services worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="99560-215">DSC will make sure that hello required services are always running.</span></span>

![Geslaagde implementatie](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="99560-217">Nadat het Hallo-beheerserver detecteert Hallo geslaagde implementatie, kunt u beveiliging configureren en replicatie op Hallo machine inschakelen met behulp van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="99560-217">After hello management server detects hello successful deployment, you can configure protection and enable replication on hello machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="99560-218">Gebruik van DSC in niet-verbonden omgevingen</span><span class="sxs-lookup"><span data-stu-id="99560-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="99560-219">Als uw machines niet verbonden toohello Internet, kunt u nog steeds zijn afhankelijk van de DSC-toodeploy en Hallo Mobility-service configureren op Hallo werkbelastingen die u tooprotect wilt.</span><span class="sxs-lookup"><span data-stu-id="99560-219">If your machines aren’t connected toohello Internet, you can still rely on DSC toodeploy and configure hello Mobility service on hello workloads that you want tooprotect.</span></span>

<span data-ttu-id="99560-220">U kunt uw eigen DSC-pull-server in uw omgeving instantiëren tooessentially Hallo bieden dezelfde mogelijkheden die u via Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="99560-220">You can instantiate your own DSC pull server in your environment tooessentially provide hello same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="99560-221">Dat wil zeggen, Hallo clients haalt binnen Hallo-configuratie (nadat deze geregistreerd) toohello DSC-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="99560-221">That is, hello clients will pull hello configuration (after it's registered) toohello DSC endpoint.</span></span> <span data-ttu-id="99560-222">Een andere optie is echter toomanually push Hallo DSC configuration tooyour machines, lokaal of extern.</span><span class="sxs-lookup"><span data-stu-id="99560-222">However, another option is toomanually push hello DSC configuration tooyour machines, either locally or remotely.</span></span>

<span data-ttu-id="99560-223">Houd er rekening mee dat in dit voorbeeld, wordt er een extra parameter voor Hallo-computernaam.</span><span class="sxs-lookup"><span data-stu-id="99560-223">Note that in this example, there's an added parameter for hello computer name.</span></span> <span data-ttu-id="99560-224">Hallo externe bestanden zich nu op een externe share die toegankelijk moet zijn door Hallo-machines dat u wilt dat tooprotect.</span><span class="sxs-lookup"><span data-stu-id="99560-224">hello remote files are now located on a remote share that should be accessible by hello machines that you want tooprotect.</span></span> <span data-ttu-id="99560-225">Hallo-einde van het Hallo-script enacts Hallo-configuratie en start vervolgens tooapply Hallo DSC configuration toohello target-computer.</span><span class="sxs-lookup"><span data-stu-id="99560-225">hello end of hello script enacts hello configuration and then starts tooapply hello DSC configuration toohello target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="99560-226">Vereisten</span><span class="sxs-lookup"><span data-stu-id="99560-226">Prerequisites</span></span>
<span data-ttu-id="99560-227">Zorg ervoor dat Hallo xPSDesiredStateConfiguration PowerShell-module is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="99560-227">Make sure that hello xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="99560-228">Voor Windows-computers waarop WMF 5.0 wordt geïnstalleerd, kunt u Hallo xPSDesiredStateConfiguration module installeren door het uitvoeren van de volgende cmdlet op de doelmachines Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="99560-228">For Windows machines where WMF 5.0 is installed, you can install hello xPSDesiredStateConfiguration module by running hello following cmdlet on hello target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="99560-229">U kunt ook downloaden en opslaan Hallo-module voor het geval u toodistribute moet het tooWindows machines waarvoor WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="99560-229">You can also download and save hello module in case you need toodistribute it tooWindows machines that have WMF 4.0.</span></span> <span data-ttu-id="99560-230">Deze cmdlet uitvoeren op een machine waarin PowerShellGet (WMF 5.0) aanwezig is:</span><span class="sxs-lookup"><span data-stu-id="99560-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="99560-231">Zorg er ook voor WMF 4.0 die Hallo [update voor Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) op Hallo computers is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="99560-231">Also for WMF 4.0, ensure that hello [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on hello machines.</span></span>

<span data-ttu-id="99560-232">Hallo kan volgende configuratie worden geactiveerd tooWindows machines waarvoor WMF 5.0 en WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="99560-232">hello following configuration can be pushed tooWindows machines that have WMF 5.0 and WMF 4.0:</span></span>

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

<span data-ttu-id="99560-233">Als u uw eigen DSC-pull-server tooinstantiate op uw bedrijfsnetwerk toomimic Hallo mogelijkheden u krijgen via Automation DSC wilt kunt, Zie [instellen van een DSC-webserver pull](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="99560-233">If you want tooinstantiate your own DSC pull server on your corporate network toomimic hello capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="99560-234">Optioneel: Een DSC-configuratie met behulp van een Azure Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="99560-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="99560-235">In dit artikel is gericht op hoe u uw eigen tooautomatically DSC-configuratie kunt maken implementeren Hallo Mobility-service en hello Azure VM-Agent-- en ervoor te zorgen dat ze worden uitgevoerd op Hallo machines dat u wilt dat tooprotect.</span><span class="sxs-lookup"><span data-stu-id="99560-235">This article has focused on how you can create your own DSC configuration tooautomatically deploy hello Mobility service and hello Azure VM Agent--and ensure that they are running on hello machines that you want tooprotect.</span></span> <span data-ttu-id="99560-236">We hebben ook een Azure Resource Manager-sjabloon die u deze DSC-configuratie tooa nieuwe of bestaande Azure Automation-account implementeert.</span><span class="sxs-lookup"><span data-stu-id="99560-236">We also have an Azure Resource Manager template that will deploy this DSC configuration tooa new or existing Azure Automation account.</span></span> <span data-ttu-id="99560-237">Hallo-sjabloon gebruikt invoerparameters toocreate Automation activa met Hallo variabelen voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="99560-237">hello template will use input parameters toocreate Automation assets that will contain hello variables for your environment.</span></span>

<span data-ttu-id="99560-238">Nadat u de sjabloon Hallo implementeert, kunt u gewoon verwijzen toostep 4 in deze handleiding tooonboard uw machines.</span><span class="sxs-lookup"><span data-stu-id="99560-238">After you deploy hello template, you can simply refer toostep 4 in this guide tooonboard your machines.</span></span>

<span data-ttu-id="99560-239">Hallo-sjabloon wordt gedaan Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="99560-239">hello template will do hello following:</span></span>

1. <span data-ttu-id="99560-240">Gebruik een bestaand automatiseringsaccount of een nieuwe maken</span><span class="sxs-lookup"><span data-stu-id="99560-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="99560-241">Invoerparameters voor nemen:</span><span class="sxs-lookup"><span data-stu-id="99560-241">Take input parameters for:</span></span>
   * <span data-ttu-id="99560-242">ASRRemoteFile--Hallo-locatie waar u Hallo Mobility-service-instellingen hebt opgeslagen</span><span class="sxs-lookup"><span data-stu-id="99560-242">ASRRemoteFile--hello location where you have stored hello Mobility service setup</span></span>
   * <span data-ttu-id="99560-243">ASRPassphrase--Hallo-locatie waar u Hallo passphrase.txt bestand hebt opgeslagen</span><span class="sxs-lookup"><span data-stu-id="99560-243">ASRPassphrase--hello location where you have stored hello passphrase.txt file</span></span>
   * <span data-ttu-id="99560-244">ASRCSEndpoint--Hallo IP-adres van de beheerserver</span><span class="sxs-lookup"><span data-stu-id="99560-244">ASRCSEndpoint--hello IP address of your management server</span></span>
3. <span data-ttu-id="99560-245">Hallo xPSDesiredStateConfiguration PowerShell-module importeren</span><span class="sxs-lookup"><span data-stu-id="99560-245">Import hello xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="99560-246">Maken en Hallo DSC-configuratie compileren</span><span class="sxs-lookup"><span data-stu-id="99560-246">Create and compile hello DSC configuration</span></span>

<span data-ttu-id="99560-247">Alle Hallo vorige stappen vindt plaats in de juiste volgorde hello, zodat u uw computers voor beveiliging voor onboarding starten kunt.</span><span class="sxs-lookup"><span data-stu-id="99560-247">All hello preceding steps will happen in hello right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="99560-248">Hallo-sjabloon met instructies voor implementatie bevindt zich op [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="99560-248">hello template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="99560-249">Hallo-sjabloon implementeren met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="99560-249">Deploy hello template by using PowerShell:</span></span>

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a><span data-ttu-id="99560-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99560-250">Next steps</span></span>
<span data-ttu-id="99560-251">Nadat u Hallo Mobility service agents implementeert, kunt u [replicatie inschakelen](site-recovery-vmware-to-azure.md) voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="99560-251">After you deploy hello Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for hello virtual machines.</span></span>
