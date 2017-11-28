---
title: Implementeer de mobiliteit van Site Recovery-service met Azure Automation DSC | Microsoft Docs
description: Hierin wordt beschreven hoe u automatisch de Azure Site Recovery Mobility-service en de Azure-agent implementeren voor VM VMware en fysieke server-replicatie naar Azure met Azure Automation DSC
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
ms.openlocfilehash: bcc5f11afbecac8fe63935f3401dd3e2d767e8aa
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-the-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a><span data-ttu-id="7b3cf-103">De Mobility-service met Azure Automation DSC voor replicatie van de virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="7b3cf-103">Deploy the Mobility service with Azure Automation DSC for replication of VM</span></span>
<span data-ttu-id="7b3cf-104">In de Operations Management Suite bieden wij u met een uitgebreide back-up en noodherstel die u als onderdeel van uw bedrijfscontinuïteitsplan kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-104">In Operations Management Suite, we provide you with a comprehensive backup and disaster recovery solution that you can use as part of your business continuity plan.</span></span>

<span data-ttu-id="7b3cf-105">We deze reis samen met Hyper-V gestart met behulp van Hyper-V Replica.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-105">We started this journey together with Hyper-V by using Hyper-V Replica.</span></span> <span data-ttu-id="7b3cf-106">Maar we zijn uitgebreid ter ondersteuning van een heterogene setup omdat klanten hebben van meerdere hypervisors en platforms in hun clouds.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-106">But we have expanded to support a heterogeneous setup because customers have multiple hypervisors and platforms in their clouds.</span></span>

<span data-ttu-id="7b3cf-107">Als u VMware werkbelastingen en/of fysieke servers vandaag, een beheerserver alle Azure Site Recovery-onderdelen wordt uitgevoerd in uw omgeving voor het afhandelen van de communicatie- en replicatie met Azure, wanneer Azure de bestemming is.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-107">If you are running VMware workloads and/or physical servers today, a management server runs all of the Azure Site Recovery components in your environment to handle the communication and data replication with Azure, when Azure is your destination.</span></span>

## <a name="deploy-the-site-recovery-mobility-service-by-using-automation-dsc"></a><span data-ttu-id="7b3cf-108">De Site Recovery Mobility-service implementeren met behulp van Automation DSC</span><span class="sxs-lookup"><span data-stu-id="7b3cf-108">Deploy the Site Recovery Mobility service by using Automation DSC</span></span>
<span data-ttu-id="7b3cf-109">Laten we beginnen als volgt een snel overzicht van de werking van deze beheerserver.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-109">Let's start by doing a quick breakdown of what this management server does.</span></span>

<span data-ttu-id="7b3cf-110">De beheerserver wordt uitgevoerd voor verschillende serverfuncties.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-110">The management server runs several server roles.</span></span> <span data-ttu-id="7b3cf-111">Een van deze functies is *configuratie*, die coördineert de communicatie en processen voor replicatie en herstel van gegevens beheert.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-111">One of these roles is *configuration*, which coordinates communication and manages data replication and recovery processes.</span></span>

<span data-ttu-id="7b3cf-112">Bovendien de *proces* rol fungeert als replicatiegateway.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-112">In addition, the *process* role acts as a replication gateway.</span></span> <span data-ttu-id="7b3cf-113">Deze rol ontvangt replicatiegegevens van beveiligde bronmachines, optimaliseert met caching, compressie en codering en stuurt deze naar Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-113">This role receives replication data from protected source machines, optimizes it with caching, compression, and encryption, and then sends it to an Azure storage account.</span></span> <span data-ttu-id="7b3cf-114">Een van de functies voor de Procesrol is ook voor push-installatie van de Mobility-service naar beveiligde computers en het uitvoeren van automatische detectie van virtuele VMware-machines.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-114">One of the functions for the process role is also to push installation of the Mobility service to protected machines and perform automatic discovery of VMware VMs.</span></span>

<span data-ttu-id="7b3cf-115">Als er een failback vanuit Azure, de *hoofddoel* rol de replicatiegegevens als onderdeel van deze bewerking wordt afgehandeld.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-115">If there's a failback from Azure, the *master target* role will handle the replication data as part of this operation.</span></span>

<span data-ttu-id="7b3cf-116">Voor de beveiligde machines we zijn afhankelijk van de *Mobility-service*.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-116">For the protected machines, we rely on the *Mobility service*.</span></span> <span data-ttu-id="7b3cf-117">Dit onderdeel wordt geïmplementeerd op elke machine (VM VMware of fysieke server) die u wilt repliceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-117">This component is deployed to every machine (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="7b3cf-118">Deze gegevens schrijfbewerkingen op de machine vastgelegd en stuurt deze door naar de beheerserver (Procesrol).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-118">It captures data writes on the machine and forwards them to the management server (process role).</span></span>

<span data-ttu-id="7b3cf-119">U bent betreft de bedrijfscontinuïteit, is het belangrijk om te begrijpen uw werkbelastingen, uw infrastructuur en de betrokken onderdelen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-119">When you're dealing with business continuity, it's important to understand your workloads, your infrastructure, and the components involved.</span></span> <span data-ttu-id="7b3cf-120">U kunt vervolgens voldoet aan de vereisten voor de beoogde hersteltijd (RTO) als het beoogde herstelpunt (RPO).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-120">You can then meet the requirements for your recovery time objective (RTO) and recovery point objective (RPO).</span></span> <span data-ttu-id="7b3cf-121">De Mobility-service is in deze context sleutel om ervoor te zorgen dat uw werkbelastingen zijn beveiligd, zoals u zou verwachten.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-121">In this context, the Mobility service is key to ensuring that your workloads are protected as you would expect.</span></span>

<span data-ttu-id="7b3cf-122">Hoe kunt u, op een geoptimaliseerde manier ervoor zorgen dat u een betrouwbare beveiligde ingesteld met behulp van een aantal onderdelen van Operations Management Suite hebt?</span><span class="sxs-lookup"><span data-stu-id="7b3cf-122">So how can you, in an optimized way, ensure that you have a reliable protected setup with help from some Operations Management Suite components?</span></span>

<span data-ttu-id="7b3cf-123">In dit artikel bevat een voorbeeld van hoe u Azure Automation Desired State Configuration (DSC), samen met Site Recovery gebruiken kunt om ervoor te zorgen dat:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-123">This article provides an example of how you can use Azure Automation Desired State Configuration (DSC), together with Site Recovery, to ensure that:</span></span>

* <span data-ttu-id="7b3cf-124">De Mobility-service en de Azure VM-agent zijn geïmplementeerd met de Windows-machines die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-124">The Mobility service and Azure VM agent are deployed to the Windows machines that you want to protect.</span></span>
* <span data-ttu-id="7b3cf-125">De Mobility-service en de Azure VM-agent worden altijd uitgevoerd wanneer Azure het replicatiedoel is.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-125">The Mobility service and Azure VM agent are always running when Azure is the replication target.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b3cf-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b3cf-126">Prerequisites</span></span>
* <span data-ttu-id="7b3cf-127">Een opslagplaats voor het opslaan van de vereiste instellingen</span><span class="sxs-lookup"><span data-stu-id="7b3cf-127">A repository to store the required setup</span></span>
* <span data-ttu-id="7b3cf-128">Een opslagplaats voor het opslaan van de vereiste wachtwoordzin te registreren met de beheerserver</span><span class="sxs-lookup"><span data-stu-id="7b3cf-128">A repository to store the required passphrase to register with the management server</span></span>

  > [!NOTE]
  > <span data-ttu-id="7b3cf-129">Een unieke wachtwoordzin wordt gegenereerd voor elke beheerserver.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-129">A unique passphrase is generated for each management server.</span></span> <span data-ttu-id="7b3cf-130">Als u implementeren meerdere beheerservers wilt, hebt u om ervoor te zorgen dat de juiste wachtwoordzin is opgeslagen in het bestand passphrase.txt.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-130">If you are going to deploy multiple management servers, you have to ensure that the correct passphrase is stored in the passphrase.txt file.</span></span>
  >
  >
* <span data-ttu-id="7b3cf-131">Windows Management Framework (WMF) 5.0 geïnstalleerd op de computers die u wilt inschakelen voor beveiliging (een vereiste voor Automation DSC)</span><span class="sxs-lookup"><span data-stu-id="7b3cf-131">Windows Management Framework (WMF) 5.0 installed on the machines that you want to enable for protection (a requirement for Automation DSC)</span></span>

  > [!NOTE]
  > <span data-ttu-id="7b3cf-132">Als u gebruiken DSC voor Windows-machines waarvoor WMF 4.0 is geïnstalleerd wilt, Zie de sectie [DSC gebruiken in niet-verbonden omgevingen](## Use DSC in disconnected environments).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-132">If you want to use DSC for Windows machines that have WMF 4.0 installed, see the section [Use DSC in disconnected environments](## Use DSC in disconnected environments).</span></span>
  

<span data-ttu-id="7b3cf-133">De Mobility-service kan worden geïnstalleerd via de opdrachtregel en verschillende argumenten.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-133">The Mobility service can be installed through the command line and accepts several arguments.</span></span> <span data-ttu-id="7b3cf-134">Daarom moet u de binaire bestanden (nadat ze het uitpakken van uw instellingen) hebben en deze opslaan op een locatie waar u ze ophalen kunt met behulp van een DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-134">That’s why you need to have the binaries (after extracting them from your setup) and store them in a place where you can retrieve them by using a DSC configuration.</span></span>

## <a name="step-1-extract-binaries"></a><span data-ttu-id="7b3cf-135">Stap 1: De binaire bestanden uitpakken</span><span class="sxs-lookup"><span data-stu-id="7b3cf-135">Step 1: Extract binaries</span></span>
1. <span data-ttu-id="7b3cf-136">De bestanden die u nodig hebt om deze installatie wilt uitpakken, blader naar de volgende map op de beheerserver:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-136">To extract the files that you need for this setup, browse to the following directory on your management server:</span></span>

    <span data-ttu-id="7b3cf-137">**\Microsoft azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span><span class="sxs-lookup"><span data-stu-id="7b3cf-137">**\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**</span></span>

    <span data-ttu-id="7b3cf-138">In deze map ziet u een MSI-bestand met de naam:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-138">In this folder, you should see an MSI file named:</span></span>

    <span data-ttu-id="7b3cf-139">**Microsoft ASR_UA_version_Windows_GA_date_Release.exe**</span><span class="sxs-lookup"><span data-stu-id="7b3cf-139">**Microsoft-ASR_UA_version_Windows_GA_date_Release.exe**</span></span>

    <span data-ttu-id="7b3cf-140">Gebruik de volgende opdracht om op te halen van het installatieprogramma:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-140">Use the following command to extract the installer:</span></span>

    <span data-ttu-id="7b3cf-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span><span class="sxs-lookup"><span data-stu-id="7b3cf-141">**.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**</span></span>
2. <span data-ttu-id="7b3cf-142">Selecteer alle bestanden en ze verzenden naar een gecomprimeerde map (ingepakte).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-142">Select all files and send them to a compressed (zipped) folder.</span></span>

<span data-ttu-id="7b3cf-143">U hebt nu de binaire bestanden die u de installatie van de Mobility-service automatiseren moet met behulp van Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-143">You now have the binaries that you need to automate the setup of the Mobility service by using Automation DSC.</span></span>

### <a name="passphrase"></a><span data-ttu-id="7b3cf-144">Wachtwoordzin</span><span class="sxs-lookup"><span data-stu-id="7b3cf-144">Passphrase</span></span>
<span data-ttu-id="7b3cf-145">Vervolgens moet u bepalen waar u deze gecomprimeerde map geplaatst.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-145">Next, you need to determine where you want to place this zipped folder.</span></span> <span data-ttu-id="7b3cf-146">U kunt een Azure storage-account gebruiken zoals later, voor het opslaan van de wachtwoordzin op die u nodig hebt voor de installatie.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-146">You can use an Azure storage account, as shown later, to store the passphrase that you need for the setup.</span></span> <span data-ttu-id="7b3cf-147">De agent wordt vervolgens geregistreerd met de beheerserver als onderdeel van het proces.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-147">The agent will then register with the management server as part of the process.</span></span>

<span data-ttu-id="7b3cf-148">De wachtwoordzin op die u hebt verkregen tijdens de implementatie van de beheerserver kan als passphrase.txt naar een tekstbestand worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-148">The passphrase that you got when you deployed the management server can be saved to a text file as passphrase.txt.</span></span>

<span data-ttu-id="7b3cf-149">Plaats de gecomprimeerde map en de wachtwoordzin in een specifieke container in Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-149">Place both the zipped folder and the passphrase in a dedicated container in the Azure storage account.</span></span>

![Locatie van de map](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

<span data-ttu-id="7b3cf-151">Als u liever om deze bestanden op een share op uw netwerk te houden, kunt u dit doet.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-151">If you prefer to keep these files on a share on your network, you can do so.</span></span> <span data-ttu-id="7b3cf-152">Alleen moet u ervoor zorgen dat de DSC-resource die u later gaat gebruiken toegang heeft en de installatie en wachtwoordzin kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-152">You just need to ensure that the DSC resource that you will be using later has access and can get the setup and passphrase.</span></span>

## <a name="step-2-create-the-dsc-configuration"></a><span data-ttu-id="7b3cf-153">Stap 2: De DSC-configuratie maken</span><span class="sxs-lookup"><span data-stu-id="7b3cf-153">Step 2: Create the DSC configuration</span></span>
<span data-ttu-id="7b3cf-154">De installatie, is afhankelijk van WMF 5.0.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-154">The setup depends on WMF 5.0.</span></span> <span data-ttu-id="7b3cf-155">WMF 5.0 moet aanwezig zijn voor de machine niet toepassen op de configuratie via Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-155">For the machine to successfully apply the configuration through Automation DSC, WMF 5.0 needs to be present.</span></span>

<span data-ttu-id="7b3cf-156">De omgeving de volgende voorbeeld DSC-configuratie gebruikt:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-156">The environment uses the following example DSC configuration:</span></span>

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
<span data-ttu-id="7b3cf-157">De configuratie wordt het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-157">The configuration will do the following:</span></span>

* <span data-ttu-id="7b3cf-158">De variabelen vertelt de configuratie waar u de binaire bestanden voor de Mobility-service en de Azure VM-agent, waar u de wachtwoordzin en waar de uitvoer wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-158">The variables will tell the configuration where to get the binaries for the Mobility service and the Azure VM agent, where to get the passphrase, and where to store the output.</span></span>
* <span data-ttu-id="7b3cf-159">De configuratie importeert de xPSDesiredStateConfiguration DSC-resource, zodat u kunt `xRemoteFile` de bestanden te downloaden uit de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-159">The configuration will import the xPSDesiredStateConfiguration DSC resource, so that you can use `xRemoteFile` to download the files from the repository.</span></span>
* <span data-ttu-id="7b3cf-160">De configuratie maakt een map waar u wilt opslaan van de binaire bestanden.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-160">The configuration will create a directory where you want to store the binaries.</span></span>
* <span data-ttu-id="7b3cf-161">De resource archief wordt Pak de bestanden van de gecomprimeerde map.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-161">The archive resource will extract the files from the zipped folder.</span></span>
* <span data-ttu-id="7b3cf-162">De bron van de installatie van het pakket installeert de Mobility-service van de UNIFIEDAGENT. EXE-installatieprogramma met de specifieke argumenten.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-162">The package Install resource will install the Mobility service from the UNIFIEDAGENT.EXE installer with the specific arguments.</span></span> <span data-ttu-id="7b3cf-163">(De variabelen die samenstellen van de argumenten moeten worden gewijzigd naar aanleiding van uw omgeving.)</span><span class="sxs-lookup"><span data-stu-id="7b3cf-163">(The variables that construct the arguments need to be changed to reflect your environment.)</span></span>
* <span data-ttu-id="7b3cf-164">Het pakket AzureAgent resource installeert de Azure VM-agent, die wordt aanbevolen voor elke virtuele machine die wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-164">The package AzureAgent resource will install the Azure VM agent, which is recommended on every VM that runs in Azure.</span></span> <span data-ttu-id="7b3cf-165">De Azure VM-agent maakt het ook mogelijk extensies toevoegen aan de virtuele machine na een failover.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-165">The Azure VM agent also makes it possible to add extensions to the VM after failover.</span></span>
* <span data-ttu-id="7b3cf-166">De service of meer resources zorgt ervoor dat de bijbehorende Mobility-services en de Azure-services altijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-166">The service resource or resources will ensure that the related Mobility services and the Azure services are always running.</span></span>

<span data-ttu-id="7b3cf-167">De configuratie opslaan als **ASRMobilityService**.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-167">Save the configuration as **ASRMobilityService**.</span></span>

> [!NOTE]
> <span data-ttu-id="7b3cf-168">Vergeet niet ter vervanging van de CSIP in uw configuratie zodat de werkelijke-beheerserver, zodat de agent goed zijn verbonden en de juiste wachtwoordzin die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-168">Remember to replace the CSIP in your configuration to reflect the actual management server, so that the agent will be connected correctly and will use the correct passphrase.</span></span>
>
>

## <a name="step-3-upload-to-automation-dsc"></a><span data-ttu-id="7b3cf-169">Stap 3: Upload naar Automation DSC</span><span class="sxs-lookup"><span data-stu-id="7b3cf-169">Step 3: Upload to Automation DSC</span></span>
<span data-ttu-id="7b3cf-170">Omdat de DSC-configuratie die u hebt aangebracht, een vereiste resource DSC-module (xPSDesiredStateConfiguration) importeren wordt, moet u die module in Automation importeren voordat u de DSC-configuratie uploadt.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-170">Because the DSC configuration that you made will import a required DSC resource module (xPSDesiredStateConfiguration), you need to import that module in Automation before you upload the DSC configuration.</span></span>

<span data-ttu-id="7b3cf-171">Aanmelden bij uw Automation-account, blader naar **activa** > **Modules**, en klik op **bladeren galerie**.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-171">Sign in to your Automation account, browse to **Assets** > **Modules**, and click **Browse Gallery**.</span></span>

<span data-ttu-id="7b3cf-172">Hier kunt u zoeken naar de module en importeer ze in uw account.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-172">Here you can search for the module and import it to your account.</span></span>

![Module importeren](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

<span data-ttu-id="7b3cf-174">Wanneer u klaar bent, gaat u naar de computer waar u de Azure Resource Manager-modules geïnstalleerd hebt en gaat u verder met het importeren van de zojuist gemaakte DSC-configuratie.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-174">When you finish this, go to your machine where you have the Azure Resource Manager modules installed and proceed to import the newly created DSC configuration.</span></span>

### <a name="import-cmdlets"></a><span data-ttu-id="7b3cf-175">Cmdlets voor importeren</span><span class="sxs-lookup"><span data-stu-id="7b3cf-175">Import cmdlets</span></span>
<span data-ttu-id="7b3cf-176">In PowerShell, moet u zich aanmelden bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-176">In PowerShell, sign in to your Azure subscription.</span></span> <span data-ttu-id="7b3cf-177">Wijzig de cmdlets voor overeenstemming met uw omgeving en uw Automation-accountgegevens in een variabele vastleggen:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-177">Modify the cmdlets to reflect your environment and capture your Automation account information in a variable:</span></span>

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

<span data-ttu-id="7b3cf-178">Uploaden van de configuratie van Automation DSC met behulp van de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-178">Upload the configuration to Automation DSC by using the following cmdlet:</span></span>

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-the-configuration-in-automation-dsc"></a><span data-ttu-id="7b3cf-179">De Automation DSC-configuratie compileren</span><span class="sxs-lookup"><span data-stu-id="7b3cf-179">Compile the configuration in Automation DSC</span></span>
<span data-ttu-id="7b3cf-180">Vervolgens moet u de Automation DSC-configuratie compileren zodat u beginnen kunt met knooppunten te registreren.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-180">Next, you need to compile the configuration in Automation DSC, so that you can start to register nodes to it.</span></span> <span data-ttu-id="7b3cf-181">U bereiken die door de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-181">You achieve that by running the following cmdlet:</span></span>

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

<span data-ttu-id="7b3cf-182">Dit kan enkele minuten duren, omdat u de configuratie in feite naar de gehoste service voor DSC-pull implementeert.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-182">This can take a few minutes, because you're basically deploying the configuration to the hosted DSC pull service.</span></span>

<span data-ttu-id="7b3cf-183">Nadat u de configuratie compileren, kunt u de informatie over de taak ophalen met behulp van PowerShell (Get-AzureRmAutomationDscCompilationJob) of met behulp van de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-183">After you compile the configuration, you can retrieve the job information by using PowerShell (Get-AzureRmAutomationDscCompilationJob) or by using the [Azure portal](https://portal.azure.com/).</span></span>

![Taak ophalen](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

<span data-ttu-id="7b3cf-185">U hebt nu gepubliceerd en DSC-configuratie geüpload naar Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-185">You have now successfully published and uploaded your DSC configuration to Automation DSC.</span></span>

## <a name="step-4-onboard-machines-to-automation-dsc"></a><span data-ttu-id="7b3cf-186">Stap 4: Vrijgeven machines Automation DSC</span><span class="sxs-lookup"><span data-stu-id="7b3cf-186">Step 4: Onboard machines to Automation DSC</span></span>
> [!NOTE]
> <span data-ttu-id="7b3cf-187">Een van de vereisten voor het voltooien van dit scenario is dat uw Windows-machines worden bijgewerkt met de nieuwste versie van WMF.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-187">One of the prerequisites for completing this scenario is that your Windows machines are updated with the latest version of WMF.</span></span> <span data-ttu-id="7b3cf-188">U kunt downloaden en installeren van de juiste versie voor uw platform van de [Downloadcentrum](https://www.microsoft.com/download/details.aspx?id=50395).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-188">You can download and install the correct version for your platform from the [Download Center](https://www.microsoft.com/download/details.aspx?id=50395).</span></span>
>
>

<span data-ttu-id="7b3cf-189">U maakt nu een metaconfig voor DSC die u op de knooppunten worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-189">You will now create a metaconfig for DSC that you will apply to your nodes.</span></span> <span data-ttu-id="7b3cf-190">Als u wilt dit is gelukt, moet u voor het ophalen van de eindpunt-URL en de primaire sleutel voor uw geselecteerde Automation-account in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-190">To succeed with this, you need to retrieve the endpoint URL and the primary key for your selected Automation account in Azure.</span></span> <span data-ttu-id="7b3cf-191">U vindt deze waarden onder **sleutels** op de **alle instellingen** blade voor het Automation-account.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-191">You can find these values under **Keys** on the **All settings** blade for the Automation account.</span></span>

![Sleutelwaarden](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

<span data-ttu-id="7b3cf-193">In dit voorbeeld hebt u een fysieke Windows Server 2012 R2-server die u beveiligen wilt met behulp van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-193">In this example, you have a Windows Server 2012 R2 physical server that you want to protect by using Site Recovery.</span></span>

### <a name="check-for-any-pending-file-rename-operations-in-the-registry"></a><span data-ttu-id="7b3cf-194">Controleren of er bestandsbewerkingen wijzigen in het register</span><span class="sxs-lookup"><span data-stu-id="7b3cf-194">Check for any pending file rename operations in the registry</span></span>
<span data-ttu-id="7b3cf-195">Voordat u begint met de server aan de Automation DSC-eindpunt kunt koppelen, wordt u aangeraden te controleren of in behandeling zijnde bewerkingen voor een bestandsserver wijzigen in het register.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-195">Before you start to associate the server with the Automation DSC endpoint, we recommend that you check for any pending file rename operations in the registry.</span></span> <span data-ttu-id="7b3cf-196">Ze mogelijk de installatie verbieden vanwege een opnieuw opstarten in behandeling is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-196">They might prohibit the setup from finishing due to a pending reboot.</span></span>

<span data-ttu-id="7b3cf-197">Voer de volgende cmdlet om te controleren of er geen opnieuw opstarten in behandeling op de server:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-197">Run the following cmdlet to verify that there’s no pending reboot on the server:</span></span>

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
<span data-ttu-id="7b3cf-198">Als u dit leeg ziet, bent u OK om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-198">If this shows empty, you are OK to proceed.</span></span> <span data-ttu-id="7b3cf-199">Als dat niet het geval is, moet u dit oplossen door de server opnieuw opstarten tijdens een onderhoudsvenster.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-199">If not, you should address this by rebooting the server during a maintenance window.</span></span>

<span data-ttu-id="7b3cf-200">De configuratie toepassen op de server, start PowerShell Integrated Scripting Environment (ISE) en voer het volgende script.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-200">To apply the configuration on the server, start the PowerShell Integrated Scripting Environment (ISE) and run the following script.</span></span> <span data-ttu-id="7b3cf-201">Dit is in wezen een DSC lokale configuratie waarmee de lokale Configuration Manager-engine registreren bij de Automation DSC-service en de specifieke configuratie (ASRMobilityService.localhost) op te halen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-201">This is essentially a DSC local configuration that will instruct the Local Configuration Manager engine to register with the Automation DSC service and retrieve the specific configuration (ASRMobilityService.localhost).</span></span>

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

<span data-ttu-id="7b3cf-202">Deze configuratie zorgt ervoor dat de lokale Configuration Manager-engine zelf registreren bij Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-202">This configuration will cause the Local Configuration Manager engine to register itself with Automation DSC.</span></span> <span data-ttu-id="7b3cf-203">Dit wordt ook bepalen hoe de engine moet worden toegepast, wat dit moet doen als er een configuratie-afwijking (ApplyAndAutoCorrect) en hoe dit moet doorgaan met de configuratie als een herstart vereist is.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-203">It will also determine how the engine should operate, what it should do if there's a configuration drift (ApplyAndAutoCorrect), and how it should proceed with the configuration if a reboot is required.</span></span>

<span data-ttu-id="7b3cf-204">Nadat u hebt dit script uitvoert, moet het knooppunt eerst registreren bij Automation DSC.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-204">After you run this script, the node should start to register with Automation DSC.</span></span>

![Knooppunt-registratie in voortgang](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

<span data-ttu-id="7b3cf-206">Als u terug naar de Azure-portal gaat, ziet u dat het nieuw ingeschreven knooppunt nu is gepubliceerd in de portal.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-206">If you go back to the Azure portal, you can see that the newly registered node has now appeared in the portal.</span></span>

![Geregistreerde knooppunt in de portal](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

<span data-ttu-id="7b3cf-208">U kunt de volgende PowerShell-cmdlet om te controleren of het knooppunt juist is geregistreerd kunt uitvoeren op de server:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-208">On the server, you can run the following PowerShell cmdlet to verify that the node has been registered correctly:</span></span>

```powershell
Get-DscLocalConfigurationManager
```

<span data-ttu-id="7b3cf-209">Nadat de configuratie is opgehaald en toegepast op de server, kunt u dit controleren door de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-209">After the configuration has been pulled and applied to the server, you can verify this by running the following cmdlet:</span></span>

```powershell
Get-DscConfigurationStatus
```

<span data-ttu-id="7b3cf-210">De uitvoer ziet u dat de server heeft de configuratie is opgehaald:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-210">The output shows that the server has successfully pulled its configuration:</span></span>

![Uitvoer](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

<span data-ttu-id="7b3cf-212">Bovendien de installatie van de Mobility-service heeft een eigen logboekbestanden die kan worden gevonden op *SystemDrive*\ProgramData\ASRSetupLogs.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-212">In addition, the Mobility service setup has its own log that can be found at *SystemDrive*\ProgramData\ASRSetupLogs.</span></span>

<span data-ttu-id="7b3cf-213">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-213">That’s it.</span></span> <span data-ttu-id="7b3cf-214">U hebt nu geïmplementeerd en geregistreerd van de Mobility-service op de computer die u beveiligen wilt met behulp van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-214">You have now successfully deployed and registered the Mobility service on the machine that you want to protect by using Site Recovery.</span></span> <span data-ttu-id="7b3cf-215">DSC ervoor dat de vereiste services altijd worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-215">DSC will make sure that the required services are always running.</span></span>

![Geslaagde implementatie](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

<span data-ttu-id="7b3cf-217">Nadat de beheerserver de geslaagde implementatie detecteert, kunt u beveiliging configureren en inschakelen van replicatie op de machine met behulp van Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-217">After the management server detects the successful deployment, you can configure protection and enable replication on the machine by using Site Recovery.</span></span>

## <a name="use-dsc-in-disconnected-environments"></a><span data-ttu-id="7b3cf-218">Gebruik van DSC in niet-verbonden omgevingen</span><span class="sxs-lookup"><span data-stu-id="7b3cf-218">Use DSC in disconnected environments</span></span>
<span data-ttu-id="7b3cf-219">Als uw machines zijn niet met Internet verbonden, kunt u nog steeds zijn afhankelijk van de DSC implementeren en configureren van de Mobility-service op de werkbelastingen die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-219">If your machines aren’t connected to the Internet, you can still rely on DSC to deploy and configure the Mobility service on the workloads that you want to protect.</span></span>

<span data-ttu-id="7b3cf-220">U kunt uw eigen DSC-pull-server in uw omgeving te bieden in wezen dezelfde mogelijkheden die u via Automation DSC instantiëren.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-220">You can instantiate your own DSC pull server in your environment to essentially provide the same capabilities that you get from Automation DSC.</span></span> <span data-ttu-id="7b3cf-221">Dat wil zeggen, wordt de clients klikt, de configuratie het eindpunt van de DSC (nadat deze geregistreerd).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-221">That is, the clients will pull the configuration (after it's registered) to the DSC endpoint.</span></span> <span data-ttu-id="7b3cf-222">Een andere optie is echter handmatig pushen van de DSC-configuratie op uw computers, lokaal of extern.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-222">However, another option is to manually push the DSC configuration to your machines, either locally or remotely.</span></span>

<span data-ttu-id="7b3cf-223">Houd er rekening mee dat in dit voorbeeld, wordt er een extra parameter voor de computernaam.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-223">Note that in this example, there's an added parameter for the computer name.</span></span> <span data-ttu-id="7b3cf-224">De externe bestanden zich nu op een externe share die toegankelijk moet zijn door de machines die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-224">The remote files are now located on a remote share that should be accessible by the machines that you want to protect.</span></span> <span data-ttu-id="7b3cf-225">Het einde van het script enacts van de configuratie en start vervolgens de DSC-configuratie toepassen op de doelcomputer.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-225">The end of the script enacts the configuration and then starts to apply the DSC configuration to the target computer.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7b3cf-226">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b3cf-226">Prerequisites</span></span>
<span data-ttu-id="7b3cf-227">Zorg ervoor dat de xPSDesiredStateConfiguration PowerShell-module is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-227">Make sure that the xPSDesiredStateConfiguration PowerShell module is installed.</span></span> <span data-ttu-id="7b3cf-228">Voor Windows-computers waarop WMF 5.0 wordt geïnstalleerd, kunt u de module xPSDesiredStateConfiguration door de volgende cmdlet wordt uitgevoerd op de doelcomputers te installeren:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-228">For Windows machines where WMF 5.0 is installed, you can install the xPSDesiredStateConfiguration module by running the following cmdlet on the target machines:</span></span>

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

<span data-ttu-id="7b3cf-229">U kunt ook downloaden en opslaan van de module als u wilt distribueren naar de Windows-machines waarvoor WMF 4.0.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-229">You can also download and save the module in case you need to distribute it to Windows machines that have WMF 4.0.</span></span> <span data-ttu-id="7b3cf-230">Deze cmdlet uitvoeren op een machine waarin PowerShellGet (WMF 5.0) aanwezig is:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-230">Run this cmdlet on a machine where PowerShellGet (WMF 5.0) is present:</span></span>

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

<span data-ttu-id="7b3cf-231">Voor WMF 4.0, zorg er ook voor dat de [update voor Windows 8.1 KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) op de computers is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-231">Also for WMF 4.0, ensure that the [Windows 8.1 update KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) is installed on the machines.</span></span>

<span data-ttu-id="7b3cf-232">De volgende configuratie kan worden geactiveerd met Windows-machines waarvoor WMF 5.0 en WMF 4.0:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-232">The following configuration can be pushed to Windows machines that have WMF 5.0 and WMF 4.0:</span></span>

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

<span data-ttu-id="7b3cf-233">Als u wilt het instantiëren van uw eigen DSC-pull-server in uw bedrijfsnetwerk om na te bootsen van de mogelijkheden die u kunt via Automation DSC, Zie [instellen van een DSC-webserver pull](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-233">If you want to instantiate your own DSC pull server on your corporate network to mimic the capabilities that you can get from Automation DSC, see [Setting up a DSC web pull server](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).</span></span>

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a><span data-ttu-id="7b3cf-234">Optioneel: Een DSC-configuratie met behulp van een Azure Resource Manager-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="7b3cf-234">Optional: Deploy a DSC configuration by using an Azure Resource Manager template</span></span>
<span data-ttu-id="7b3cf-235">In dit artikel is gericht op hoe kunt u uw eigen DSC-configuratie om automatisch te implementeren van de Mobility-service en de Azure VM-Agent-- en ervoor te zorgen dat ze worden uitgevoerd op de machines die u wilt beveiligen.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-235">This article has focused on how you can create your own DSC configuration to automatically deploy the Mobility service and the Azure VM Agent--and ensure that they are running on the machines that you want to protect.</span></span> <span data-ttu-id="7b3cf-236">We hebben ook een Azure Resource Manager-sjabloon die u deze DSC-configuratie naar een nieuwe of bestaande Azure Automation-account implementeert.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-236">We also have an Azure Resource Manager template that will deploy this DSC configuration to a new or existing Azure Automation account.</span></span> <span data-ttu-id="7b3cf-237">De sjabloon wordt invoerparameters gebruiken om Automation activa waarin u de variabelen voor uw omgeving te maken.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-237">The template will use input parameters to create Automation assets that will contain the variables for your environment.</span></span>

<span data-ttu-id="7b3cf-238">Nadat u de sjabloon implementeert, kunt u gewoon verwijzen naar stap 4 in deze handleiding om vrij te geven uw machines.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-238">After you deploy the template, you can simply refer to step 4 in this guide to onboard your machines.</span></span>

<span data-ttu-id="7b3cf-239">De sjabloon wordt het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-239">The template will do the following:</span></span>

1. <span data-ttu-id="7b3cf-240">Gebruik een bestaand automatiseringsaccount of een nieuwe maken</span><span class="sxs-lookup"><span data-stu-id="7b3cf-240">Use an existing Automation account or create a new one</span></span>
2. <span data-ttu-id="7b3cf-241">Invoerparameters voor nemen:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-241">Take input parameters for:</span></span>
   * <span data-ttu-id="7b3cf-242">ASRRemoteFile--de locatie waar u de Mobility-service-instellingen hebt opgeslagen</span><span class="sxs-lookup"><span data-stu-id="7b3cf-242">ASRRemoteFile--the location where you have stored the Mobility service setup</span></span>
   * <span data-ttu-id="7b3cf-243">ASRPassphrase--de locatie waar u het bestand passphrase.txt hebt opgeslagen</span><span class="sxs-lookup"><span data-stu-id="7b3cf-243">ASRPassphrase--the location where you have stored the passphrase.txt file</span></span>
   * <span data-ttu-id="7b3cf-244">ASRCSEndpoint--het IP-adres van de beheerserver</span><span class="sxs-lookup"><span data-stu-id="7b3cf-244">ASRCSEndpoint--the IP address of your management server</span></span>
3. <span data-ttu-id="7b3cf-245">Importeer de PowerShell-module xPSDesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="7b3cf-245">Import the xPSDesiredStateConfiguration PowerShell module</span></span>
4. <span data-ttu-id="7b3cf-246">Maken en de DSC-configuratie compileren</span><span class="sxs-lookup"><span data-stu-id="7b3cf-246">Create and compile the DSC configuration</span></span>

<span data-ttu-id="7b3cf-247">De voorgaande stappen vindt plaats in de juiste volgorde, zodat u uw computers voor beveiliging voor onboarding starten kunt.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-247">All the preceding steps will happen in the right order, so that you can start onboarding your machines for protection.</span></span>

<span data-ttu-id="7b3cf-248">De sjabloon met instructies voor implementatie bevindt zich op [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span><span class="sxs-lookup"><span data-stu-id="7b3cf-248">The template, with instructions for deployment, is located on [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).</span></span>

<span data-ttu-id="7b3cf-249">De sjabloon implementeren met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7b3cf-249">Deploy the template by using PowerShell:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7b3cf-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b3cf-250">Next steps</span></span>
<span data-ttu-id="7b3cf-251">Nadat u de Mobility-service-agents te implementeren, kunt u [replicatie inschakelen](site-recovery-vmware-to-azure.md) voor de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="7b3cf-251">After you deploy the Mobility service agents, you can [enable replication](site-recovery-vmware-to-azure.md) for the virtual machines.</span></span>
