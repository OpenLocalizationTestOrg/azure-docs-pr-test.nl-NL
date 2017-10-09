---
title: bij de bezorging van continue foutopsporing op afstand aaaEnable | Microsoft Docs
description: Meer informatie over hoe tooenable foutopsporing op afstand bij gebruik van doorlopende levering toodeploy tooAzure
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a><span data-ttu-id="15860-103">Foutopsporing op afstand inschakelen wanneer u doorlopende levering toopublish tooAzure</span><span class="sxs-lookup"><span data-stu-id="15860-103">Enable remote debugging when using continuous delivery toopublish tooAzure</span></span>
<span data-ttu-id="15860-104">U kunt foutopsporing op afstand inschakelen in Azure, voor cloudservices of virtuele machines, wanneer u [continue levering](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="15860-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="15860-105">Foutopsporing op afstand voor cloudservices inschakelen</span><span class="sxs-lookup"><span data-stu-id="15860-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="15860-106">Op Hallo build-agent, Hallo initiële omgeving instellen voor Azure zoals wordt beschreven in [Command-Line bouwen voor Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="15860-106">On hello build agent, set up hello initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="15860-107">Omdat Hallo foutopsporing op afstand runtime (msvsmon.exe) vereist voor Hallo pakket is, installeert u Hallo **externe hulpprogramma's voor Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="15860-107">Because hello remote debug runtime (msvsmon.exe) is required for hello package, install hello **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="15860-108">Externe hulpprogramma's voor Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="15860-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="15860-109">Externe hulpprogramma's voor Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="15860-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="15860-110">Externe hulpprogramma's voor Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="15860-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="15860-111">U kunt als alternatief kunt Hallo foutopsporing op afstand binaire bestanden kopiëren van een systeem met Visual Studio is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="15860-111">As an alternative, you can copy hello remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="15860-112">Een certificaat te maken, zoals wordt beschreven in [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="15860-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="15860-113">Hallo pfx en RDP-certificaatvingerafdruk houden en upload Hallo certificaat toohello target cloud-service.</span><span class="sxs-lookup"><span data-stu-id="15860-113">Keep hello .pfx and RDP certificate thumbprint and upload hello certificate toohello target cloud service.</span></span>
4. <span data-ttu-id="15860-114">Gebruik Hallo volgend op opties in Hallo MSBuild opdrachtregel toobuild en het pakket met foutopsporing op afstand is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="15860-114">Use hello following options in hello MSBuild command line toobuild and package with remote debug enabled.</span></span> <span data-ttu-id="15860-115">(Vervangen door feitelijke paden tooyour systeem- en bestanden voor Hallo hoek tussen items.)</span><span class="sxs-lookup"><span data-stu-id="15860-115">(Substitute actual paths tooyour system and project files for hello angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    <span data-ttu-id="15860-116">`VSX64RemoteDebuggerPath`Hallo pad toohello map is waarin msvsmon.exe in Hallo externe hulpprogramma's voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15860-116">`VSX64RemoteDebuggerPath` is hello path toohello folder containing msvsmon.exe in hello Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="15860-117">`RemoteDebuggerConnectorVersion`hello Azure SDK-versie in uw cloudservice is.</span><span class="sxs-lookup"><span data-stu-id="15860-117">`RemoteDebuggerConnectorVersion` is hello Azure SDK version in your cloud service.</span></span> <span data-ttu-id="15860-118">Het moet ook overeenkomen met de Hallo-versie is geïnstalleerd met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15860-118">It should also match hello version installed with Visual Studio.</span></span>
5. <span data-ttu-id="15860-119">Hallo pakket- en cscfg-bestand dat wordt gegenereerd in de vorige stap Hallo met publiceren toohello target cloud-service.</span><span class="sxs-lookup"><span data-stu-id="15860-119">Publish toohello target cloud service by using hello package and .cscfg file generated in hello previous step.</span></span>
6. <span data-ttu-id="15860-120">Hallo-certificaat (.pfx-bestand) toohello machine met Visual Studio met Azure SDK voor .NET geïnstalleerd importeren.</span><span class="sxs-lookup"><span data-stu-id="15860-120">Import hello certificate (.pfx file) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="15860-121">Zorg ervoor dat tooimport toohello `CurrentUser\My` certificaatarchief, anders koppelen toohello foutopsporing in Visual Studio mislukt.</span><span class="sxs-lookup"><span data-stu-id="15860-121">Make sure tooimport toohello `CurrentUser\My` certificate store, otherwise attaching toohello debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="15860-122">Foutopsporing op afstand voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="15860-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="15860-123">Maak een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="15860-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="15860-124">Zie [maken van een virtuele Machine met WindowsServer](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [maken en beheren van virtuele Machines in Visual Studio in Azure](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="15860-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="15860-125">Op Hallo [Azure classic portal-pagina](http://go.microsoft.com/fwlink/p/?LinkID=269851), Hallo virtuele machine dashboard toosee Hallo van virtuele machine weergeven **RDP CERTIFICAATVINGERAFDRUK**.</span><span class="sxs-lookup"><span data-stu-id="15860-125">On hello [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view hello virtual machine's dashboard toosee hello virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="15860-126">Deze waarde wordt gebruikt voor Hallo `ServerThumbprint` waarde in de configuratie van Hallo-uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="15860-126">This value is used for hello `ServerThumbprint` value in hello extension configuration.</span></span>
3. <span data-ttu-id="15860-127">Maken van een clientcertificaat, zoals wordt beschreven in [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md) (Houd Hallo .pfx en certificaatvingerafdruk RDP).</span><span class="sxs-lookup"><span data-stu-id="15860-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep hello .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="15860-128">Azure Powershell installeren (versie 0.7.4 of hoger) zoals wordt beschreven in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="15860-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="15860-129">Hallo na scriptextensie tooenable hello RemoteDebug worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="15860-129">Run hello following script tooenable hello RemoteDebug extension.</span></span> <span data-ttu-id="15860-130">Hallo paden en persoonlijke gegevens vervangen door uw eigen, zoals de naam van abonnement, servicenaam en vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="15860-130">Replace hello paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="15860-131">Dit script is geconfigureerd voor Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="15860-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="15860-132">Als u Visual Studio 2013 of Visual Studio 2017, wijzigt u Hallo `$referenceName` en `$extensionName` onderstaande toewijzingen te`RemoteDebugVS2013` of `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="15860-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify hello `$referenceName` and `$extensionName` assignments below too`RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. <span data-ttu-id="15860-133">Hallo certificaat (.pfx) toohello machine importeren met Visual Studio met Azure SDK voor .NET is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="15860-133">Import hello certificate (.pfx) toohello machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

