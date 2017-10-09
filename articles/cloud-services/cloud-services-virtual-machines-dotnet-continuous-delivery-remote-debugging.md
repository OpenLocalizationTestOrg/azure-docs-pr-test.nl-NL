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
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>Foutopsporing op afstand inschakelen wanneer u doorlopende levering toopublish tooAzure
U kunt foutopsporing op afstand inschakelen in Azure, voor cloudservices of virtuele machines, wanneer u [continue levering](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure met de volgende stappen.

## <a name="enabling-remote-debugging-for-cloud-services"></a>Foutopsporing op afstand voor cloudservices inschakelen
1. Op Hallo build-agent, Hallo initiële omgeving instellen voor Azure zoals wordt beschreven in [Command-Line bouwen voor Azure](http://msdn.microsoft.com/library/hh535755.aspx).
2. Omdat Hallo foutopsporing op afstand runtime (msvsmon.exe) vereist voor Hallo pakket is, installeert u Hallo **externe hulpprogramma's voor Visual Studio**.

    * [Externe hulpprogramma's voor Visual Studio 2017](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Externe hulpprogramma's voor Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Externe hulpprogramma's voor Visual Studio 2013 Update 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    U kunt als alternatief kunt Hallo foutopsporing op afstand binaire bestanden kopiëren van een systeem met Visual Studio is geïnstalleerd.

3. Een certificaat te maken, zoals wordt beschreven in [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md). Hallo pfx en RDP-certificaatvingerafdruk houden en upload Hallo certificaat toohello target cloud-service.
4. Gebruik Hallo volgend op opties in Hallo MSBuild opdrachtregel toobuild en het pakket met foutopsporing op afstand is ingeschakeld. (Vervangen door feitelijke paden tooyour systeem- en bestanden voor Hallo hoek tussen items.)
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`Hallo pad toohello map is waarin msvsmon.exe in Hallo externe hulpprogramma's voor Visual Studio.
    `RemoteDebuggerConnectorVersion`hello Azure SDK-versie in uw cloudservice is. Het moet ook overeenkomen met de Hallo-versie is geïnstalleerd met Visual Studio.
5. Hallo pakket- en cscfg-bestand dat wordt gegenereerd in de vorige stap Hallo met publiceren toohello target cloud-service.
6. Hallo-certificaat (.pfx-bestand) toohello machine met Visual Studio met Azure SDK voor .NET geïnstalleerd importeren. Zorg ervoor dat tooimport toohello `CurrentUser\My` certificaatarchief, anders koppelen toohello foutopsporing in Visual Studio mislukt.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>Foutopsporing op afstand voor virtuele machines inschakelen
1. Maak een virtuele machine van Azure. Zie [maken van een virtuele Machine met WindowsServer](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) of [maken en beheren van virtuele Machines in Visual Studio in Azure](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
2. Op Hallo [Azure classic portal-pagina](http://go.microsoft.com/fwlink/p/?LinkID=269851), Hallo virtuele machine dashboard toosee Hallo van virtuele machine weergeven **RDP CERTIFICAATVINGERAFDRUK**. Deze waarde wordt gebruikt voor Hallo `ServerThumbprint` waarde in de configuratie van Hallo-uitbreiding.
3. Maken van een clientcertificaat, zoals wordt beschreven in [certificaten voor Azure Cloud Services-overzicht](cloud-services-certs-create.md) (Houd Hallo .pfx en certificaatvingerafdruk RDP).
4. Azure Powershell installeren (versie 0.7.4 of hoger) zoals wordt beschreven in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
5. Hallo na scriptextensie tooenable hello RemoteDebug worden uitgevoerd. Hallo paden en persoonlijke gegevens vervangen door uw eigen, zoals de naam van abonnement, servicenaam en vingerafdruk.
   
   > [!NOTE]
   > Dit script is geconfigureerd voor Visual Studio 2015. Als u Visual Studio 2013 of Visual Studio 2017, wijzigt u Hallo `$referenceName` en `$extensionName` onderstaande toewijzingen te`RemoteDebugVS2013` of `RemoteDebugVS2017`.

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

6. Hallo certificaat (.pfx) toohello machine importeren met Visual Studio met Azure SDK voor .NET is geïnstalleerd.

