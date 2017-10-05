---
title: Foutopsporing op afstand met continue levering inschakelen | Microsoft Docs
description: Meer informatie over het foutopsporing op afstand inschakelen wanneer u doorlopende levering implementeren naar Azure
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
ms.openlocfilehash: 7a8a853a93e3e9915f687a20c871444e6a0de50d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-to-publish-to-azure"></a><span data-ttu-id="ed527-103">Schakel foutopsporing op afstand in bij het gebruik van onafgebroken levering om te publiceren op Azure</span><span class="sxs-lookup"><span data-stu-id="ed527-103">Enable remote debugging when using continuous delivery to publish to Azure</span></span>
<span data-ttu-id="ed527-104">U kunt foutopsporing op afstand inschakelen in Azure, voor cloudservices of virtuele machines, wanneer u [continue levering](cloud-services-dotnet-continuous-delivery.md) publiceren naar Azure met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="ed527-104">You can enable remote debugging in Azure, for cloud services or virtual machines, when you use [continuous delivery](cloud-services-dotnet-continuous-delivery.md) to publish to Azure by following these steps.</span></span>

## <a name="enabling-remote-debugging-for-cloud-services"></a><span data-ttu-id="ed527-105">Foutopsporing op afstand voor cloudservices inschakelen</span><span class="sxs-lookup"><span data-stu-id="ed527-105">Enabling remote debugging for cloud services</span></span>
1. <span data-ttu-id="ed527-106">Op de agent build instellen van de eerste omgeving voor Azure zoals wordt beschreven in [Command-Line bouwen voor Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed527-106">On the build agent, set up the initial environment for Azure as outlined in [Command-Line Build for Azure](http://msdn.microsoft.com/library/hh535755.aspx).</span></span>
2. <span data-ttu-id="ed527-107">Omdat de foutopsporing op afstand-runtime (msvsmon.exe) vereist voor het pakket is, installeert de **externe hulpprogramma's voor Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="ed527-107">Because the remote debug runtime (msvsmon.exe) is required for the package, install the **Remote Tools for Visual Studio**.</span></span>

    * [<span data-ttu-id="ed527-108">Externe hulpprogramma's voor Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ed527-108">Remote Tools for Visual Studio 2017</span></span>](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [<span data-ttu-id="ed527-109">Externe hulpprogramma's voor Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="ed527-109">Remote Tools for Visual Studio 2015</span></span>](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [<span data-ttu-id="ed527-110">Externe hulpprogramma's voor Visual Studio 2013 Update 5</span><span class="sxs-lookup"><span data-stu-id="ed527-110">Remote Tools for Visual Studio 2013 Update 5</span></span>](https://www.microsoft.com/download/details.aspx?id=48156)
    
    <span data-ttu-id="ed527-111">Als alternatief kunt kunt u de binaire bestanden voor foutopsporing op afstand kopiëren van een systeem met Visual Studio is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ed527-111">As an alternative, you can copy the remote debug binaries from a system that has Visual Studio installed.</span></span>

3. <span data-ttu-id="ed527-112">Een certificaat te maken, zoals wordt beschreven in [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="ed527-112">Create a certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="ed527-113">Houd de pfx en het RDP-certificaatvingerafdruk en upload het certificaat naar de doel-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="ed527-113">Keep the .pfx and RDP certificate thumbprint and upload the certificate to the target cloud service.</span></span>
4. <span data-ttu-id="ed527-114">Gebruik de volgende opties op de opdrachtregel MSBuild te verpakken met foutopsporing op afstand is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ed527-114">Use the following options in the MSBuild command line to build and package with remote debug enabled.</span></span> <span data-ttu-id="ed527-115">(Vervangen door feitelijke paden naar uw systeem- en bestanden voor de hoek tussen items.)</span><span class="sxs-lookup"><span data-stu-id="ed527-115">(Substitute actual paths to your system and project files for the angle-bracketed items.)</span></span>
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of the certificate added to the cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path to your VS solution file>"
   
    <span data-ttu-id="ed527-116">`VSX64RemoteDebuggerPath`het pad naar de map is waarin msvsmon.exe in de externe hulpprogramma's voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed527-116">`VSX64RemoteDebuggerPath` is the path to the folder containing msvsmon.exe in the Remote Tools for Visual Studio.</span></span>
    <span data-ttu-id="ed527-117">`RemoteDebuggerConnectorVersion`is de Azure SDK-versie in uw cloudservice.</span><span class="sxs-lookup"><span data-stu-id="ed527-117">`RemoteDebuggerConnectorVersion` is the Azure SDK version in your cloud service.</span></span> <span data-ttu-id="ed527-118">Het moet ook overeenkomen met de versie met Visual Studio is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ed527-118">It should also match the version installed with Visual Studio.</span></span>
5. <span data-ttu-id="ed527-119">Publiceren naar de doel-cloudservice met behulp van de pakket- en .cscfg-bestand gegenereerd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="ed527-119">Publish to the target cloud service by using the package and .cscfg file generated in the previous step.</span></span>
6. <span data-ttu-id="ed527-120">Importeer het certificaat (.pfx-bestand) met de machine met Visual Studio met Azure SDK voor .NET is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ed527-120">Import the certificate (.pfx file) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span> <span data-ttu-id="ed527-121">Zorg ervoor dat voor het importeren naar de `CurrentUser\My` certificaatarchief, anders koppelen aan het foutopsporingsprogramma in Visual Studio zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="ed527-121">Make sure to import to the `CurrentUser\My` certificate store, otherwise attaching to the debugger in Visual Studio will fail.</span></span>

## <a name="enabling-remote-debugging-for-virtual-machines"></a><span data-ttu-id="ed527-122">Foutopsporing op afstand voor virtuele machines inschakelen</span><span class="sxs-lookup"><span data-stu-id="ed527-122">Enabling remote debugging for virtual machines</span></span>
1. <span data-ttu-id="ed527-123">Maak een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="ed527-123">Create an Azure virtual machine.</span></span> <span data-ttu-id="ed527-124">Zie [maken van een virtuele Machine met WindowsServer](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [maken en beheren van virtuele Machines in Visual Studio in Azure](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed527-124">See [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) or [Create and Manage Azure Virtual Machines in Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
2. <span data-ttu-id="ed527-125">Op de [Azure classic portal-pagina](http://go.microsoft.com/fwlink/p/?LinkID=269851), dashboard van de virtuele machine om te zien van de virtuele machine weergeven **RDP CERTIFICAATVINGERAFDRUK**.</span><span class="sxs-lookup"><span data-stu-id="ed527-125">On the [Azure classic portal page](http://go.microsoft.com/fwlink/p/?LinkID=269851), view the virtual machine's dashboard to see the virtual machine’s **RDP CERTIFICATE THUMBPRINT**.</span></span> <span data-ttu-id="ed527-126">Deze waarde wordt gebruikt voor de `ServerThumbprint` waarde in de configuratie voor de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="ed527-126">This value is used for the `ServerThumbprint` value in the extension configuration.</span></span>
3. <span data-ttu-id="ed527-127">Maken van een clientcertificaat, zoals wordt beschreven in [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md) (Houd de pfx en het RDP-certificaatvingerafdruk).</span><span class="sxs-lookup"><span data-stu-id="ed527-127">Create a client certificate as outlined in [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md) (keep the .pfx and RDP certificate thumbprint).</span></span>
4. <span data-ttu-id="ed527-128">Azure Powershell installeren (versie 0.7.4 of hoger) zoals wordt beschreven in [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ed527-128">Install Azure Powershell (version 0.7.4 or later) as outlined in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
5. <span data-ttu-id="ed527-129">Voer het volgende script de RemoteDebug-uitbreiding in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="ed527-129">Run the following script to enable the RemoteDebug extension.</span></span> <span data-ttu-id="ed527-130">Vervang de paden en persoonlijke gegevens door uw eigen, zoals de naam van abonnement, servicenaam en vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="ed527-130">Replace the paths and personal data with your own, such as your subscription name, service name, and thumbprint.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ed527-131">Dit script is geconfigureerd voor Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ed527-131">This script is configured for Visual Studio 2015.</span></span> <span data-ttu-id="ed527-132">Als u Visual Studio 2013 of Visual Studio 2017, wijzigt u de `$referenceName` en `$extensionName` toewijzingen hieronder aan `RemoteDebugVS2013` of `RemoteDebugVS2017`.</span><span class="sxs-lookup"><span data-stu-id="ed527-132">If you’re using Visual Studio 2013 or Visual Studio 2017, modify the `$referenceName` and `$extensionName` assignments below to `RemoteDebugVS2013` or `RemoteDebugVS2017`.</span></span>

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

6. <span data-ttu-id="ed527-133">Importeer het certificaat (.pfx) met de machine met Visual Studio met Azure SDK voor .NET is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ed527-133">Import the certificate (.pfx) to the machine that has Visual Studio with Azure SDK for .NET installed.</span></span>

