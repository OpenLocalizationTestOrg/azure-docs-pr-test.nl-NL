---
title: aaaGetting de slag met Azure Service Fabric XPlat CLI
description: Aan de slag met Azure Service Fabric XPlat CLI
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: c3ec8ff3-3b78-420c-a7ea-0c5e443fb10e
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: e4baa30536b4d8668d8efad301ed8210eb9c0335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a><span data-ttu-id="ec501-103">Hallo toointeract XPlat CLI gebruiken met een Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="ec501-103">Using hello XPlat CLI toointeract with a Service Fabric cluster</span></span>

<span data-ttu-id="ec501-104">U kunt werken met Service Fabric-cluster van Linux-machines Hallo XPlat CLI met op Linux.</span><span class="sxs-lookup"><span data-stu-id="ec501-104">You can interact with Service Fabric cluster from Linux machines using hello XPlat CLI on Linux.</span></span>

<span data-ttu-id="ec501-105">Hallo eerste stap is Hallo meest recente versie van Hallo CLI ophalen uit Hallo git rep en stel het in uw pad met Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="ec501-105">hello first step is get hello latest version of hello CLI from hello git rep and set it up in your path using hello following commands:</span></span>

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

<span data-ttu-id="ec501-106">Voor elke opdracht ondersteunt, kunt u de naam van de Hallo Hallo opdracht tooobtain Hallo Help voor de opdracht typen.</span><span class="sxs-lookup"><span data-stu-id="ec501-106">For each command, it supports, you can type hello name of hello command tooobtain hello help for that command.</span></span>
<span data-ttu-id="ec501-107">Automatisch aanvullen wordt ondersteund voor Hallo-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ec501-107">Auto-completion is supported for hello commands.</span></span> <span data-ttu-id="ec501-108">Bijvoorbeeld: hello opdracht geeft die u voor alle Hallo toepassing opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="ec501-108">For example, hello following command gives you help for all hello application commands.</span></span> 

```sh
 azure servicefabric application 
```

<span data-ttu-id="ec501-109">U kunt verder Hallo help tooa specifieke opdracht filteren als Hallo volgende voorbeeld wordt getoond:</span><span class="sxs-lookup"><span data-stu-id="ec501-109">You can further filter hello help tooa specific command, as hello following example shows:</span></span>

```sh
 azure servicefabric application  create
```

<span data-ttu-id="ec501-110">tooenable automatisch aanvullen in Hallo CLI Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ec501-110">tooenable auto-completion in hello CLI, run hello following commands:</span></span>

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

<span data-ttu-id="ec501-111">Hallo opdrachten na verbinding toohello cluster en Hallo van knooppunten in cluster Hallo weergeven:</span><span class="sxs-lookup"><span data-stu-id="ec501-111">hello following commands connect toohello cluster and show you hello nodes in hello cluster:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

<span data-ttu-id="ec501-112">toouse benoemde parameters uit te vinden wat ze zijn, kunt u typen--help na een opdracht.</span><span class="sxs-lookup"><span data-stu-id="ec501-112">toouse named parameters, and find what they are, you can type --help after a command.</span></span> <span data-ttu-id="ec501-113">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ec501-113">For example:</span></span>

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

<span data-ttu-id="ec501-114">Bij het cluster met meerdere machines tooa verbinden van een virtuele machine **die geen deel uit van de cluster Hallo**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec501-114">When connecting tooa multi-machine cluster from a machine **that is not part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

<span data-ttu-id="ec501-115">Vervangen door Hallo PublicIPorFQDN tag Hallo echte IP of FQDN naar gelang van toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec501-115">Replace hello PublicIPorFQDN tag with hello real IP or FQDN as appropriate.</span></span> <span data-ttu-id="ec501-116">Bij het cluster met meerdere machines tooa verbinden van een virtuele machine **die deel uitmaken van Hallo cluster**, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec501-116">When connecting tooa multi-machine cluster from a machine **that is part of hello cluster**, use hello following command:</span></span>

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

<span data-ttu-id="ec501-117">Kunt u PowerShell of CLI toointeract met uw Service Fabric-Cluster van Linux via hello Azure-portal is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ec501-117">You can use PowerShell or CLI toointeract with your Linux Service Fabric Cluster created through hello Azure portal.</span></span>

> [!WARNING]
> <span data-ttu-id="ec501-118">Deze clusters niet is beveiligd, dus u mogelijk worden openen van de 1-box door Hallo openbaar IP-adres toe te voegen in het clustermanifest Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec501-118">These clusters aren’t secure, thus, you may be opening up your one-box by adding hello public IP address in hello cluster manifest.</span></span>

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a><span data-ttu-id="ec501-119">Hallo XPlat CLI tooconnect tooa Service Fabric-cluster gebruiken</span><span class="sxs-lookup"><span data-stu-id="ec501-119">Using hello XPlat CLI tooconnect tooa Service Fabric cluster</span></span>

<span data-ttu-id="ec501-120">Hello Azure CLI-opdrachten na beschrijven hoe tooconnect tooa cluster beveiligen.</span><span class="sxs-lookup"><span data-stu-id="ec501-120">hello following Azure CLI commands describe how tooconnect tooa secure cluster.</span></span> <span data-ttu-id="ec501-121">details van Hallo certificaat moeten overeenkomen met een certificaat op de clusterknooppunten Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec501-121">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

<span data-ttu-id="ec501-122">Als uw certificaat heeft certificeringsinstanties (CA's), moet u tooadd Hallo--ca-certificaat-path-parameter zoals Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec501-122">If your certificate has Certificate Authorities (CAs), you need tooadd hello --ca-cert-path parameter like hello following example:</span></span> 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

<span data-ttu-id="ec501-123">Als u meerdere CA's hebt, gebruikt u een komma als scheidingsteken Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec501-123">If you have multiple CAs, use a comma as hello delimiter.</span></span>

<span data-ttu-id="ec501-124">Als de algemene naam in Hallo certificaat komt niet overeen met de Hallo verbindingseindpunt, kunt u gebruiken Hallo parameter `--strict-ssl-false` toobypass Hallo verificatie, zoals wordt weergegeven in de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ec501-124">If your Common Name in hello certificate does not match hello connection endpoint, you could use hello parameter `--strict-ssl-false` toobypass hello verification as shown in hello following command:</span></span>

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

<span data-ttu-id="ec501-125">Als u tooskip Hallo CA verificatie wilt, kunt u Hallo--afkeuren-niet-geautoriseerde ONWAAR parameter zoals weergegeven in de volgende opdracht Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ec501-125">If you would like tooskip hello CA verification, you could add hello --reject-unauthorized-false parameter as shown in hello following command:</span></span> 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

<span data-ttu-id="ec501-126">Nadat u verbinding maakt, moet u kunnen toorun andere toointeract CLI-opdrachten met Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ec501-126">After you connect, you should be able toorun other CLI commands toointeract with hello cluster.</span></span>

## <a name="deploying-your-service-fabric-application"></a><span data-ttu-id="ec501-127">Uw Service Fabric-toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="ec501-127">Deploying your Service Fabric application</span></span>

<span data-ttu-id="ec501-128">Hallo opdrachten toocopy, registreren en start de service fabric-toepassing hello volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ec501-128">Execute hello following commands toocopy, register, and start hello service fabric application:</span></span>

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a><span data-ttu-id="ec501-129">Bijwerken van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="ec501-129">Upgrading your application</span></span>

<span data-ttu-id="ec501-130">Hallo-proces is vergelijkbaar toohello [processen in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span><span class="sxs-lookup"><span data-stu-id="ec501-130">hello process is similar toohello [process in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).</span></span>

<span data-ttu-id="ec501-131">Bouwen, kopiëren, registreren en uw toepassing uit de hoofddirectory project maken.</span><span class="sxs-lookup"><span data-stu-id="ec501-131">Build, copy, register, and create your application from project root directory.</span></span> <span data-ttu-id="ec501-132">Als de naam van uw exemplaar van de `fabric:/MySFApp`, en Hallo type MySFApp, Hallo opdrachten worden als volgt:</span><span class="sxs-lookup"><span data-stu-id="ec501-132">If your application instance is named `fabric:/MySFApp`, and hello type is MySFApp, hello commands would be as follows:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

<span data-ttu-id="ec501-133">Controleer Hallo tooyour toepassing wijzigen en gewijzigd Hallo-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ec501-133">Make hello change tooyour application and rebuild hello modified service.</span></span>  <span data-ttu-id="ec501-134">Hallo update gewijzigd van service manifestbestand (ServiceManifest.xml) met Hallo bijgewerkt versies voor het Hallo-Service (en Code of configuratie of gegevens naar gelang van toepassing).</span><span class="sxs-lookup"><span data-stu-id="ec501-134">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello Service (and Code or Config or Data as appropriate).</span></span> <span data-ttu-id="ec501-135">Ook wijzigen van de toepassing hello-manifest (ApplicationManifest.xml) met versienummer Hallo bijgewerkt voor de toepassing hello en Hallo gewijzigde service.</span><span class="sxs-lookup"><span data-stu-id="ec501-135">Also modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application, and hello modified service.</span></span>  <span data-ttu-id="ec501-136">Nu, kopiëren en de bijgewerkte toepassing met behulp van de volgende opdrachten Hallo registreren:</span><span class="sxs-lookup"><span data-stu-id="ec501-136">Now, copy and register your updated application using hello following commands:</span></span>

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

<span data-ttu-id="ec501-137">U kunt nu de upgrade van de toepassing hello starten met Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ec501-137">Now, you can start hello application upgrade with hello following command:</span></span>

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

<span data-ttu-id="ec501-138">Nu kunt u de upgrade van de toepassing hello SFX met bewaken.</span><span class="sxs-lookup"><span data-stu-id="ec501-138">You can now monitor hello application upgrade using SFX.</span></span> <span data-ttu-id="ec501-139">In een paar minuten zou Hallo toepassing zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="ec501-139">In a few minutes, hello application would have been updated.</span></span> <span data-ttu-id="ec501-140">U kunt ook een app bijgewerkt met een fout te en Hallo automatische terugdraaifunctie in service fabric.</span><span class="sxs-lookup"><span data-stu-id="ec501-140">You can also try an updated app with an error and check hello auto rollback functionality in service fabric.</span></span>

## <a name="converting-from-pfx-toopem-and-vice-versa"></a><span data-ttu-id="ec501-141">Converteren van PFX-tooPEM en omgekeerd</span><span class="sxs-lookup"><span data-stu-id="ec501-141">Converting from PFX tooPEM and vice versa</span></span>

<span data-ttu-id="ec501-142">Mogelijk moet u een certificaat tooinstall in uw lokale computer (met Windows of Linux) tooaccess beveiligde clusters die mogelijk in een andere omgeving.</span><span class="sxs-lookup"><span data-stu-id="ec501-142">You might need tooinstall a certificate in your local machine (with Windows or Linux) tooaccess secure clusters that may be in a different environment.</span></span> <span data-ttu-id="ec501-143">Bijvoorbeeld bij het openen van een beveiligde Linux-cluster van een Windows-machine en omgekeerd moet u mogelijk tooconvert uw certificaat uit het PFX-tooPEM en vice versa.</span><span class="sxs-lookup"><span data-stu-id="ec501-143">For example, while accessing a secured Linux cluster from a Windows machine and vice versa you may need tooconvert your certificate from PFX tooPEM and vice versa.</span></span> 

<span data-ttu-id="ec501-144">tooconvert uit een PEM-bestand tooa PFX-bestand, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ec501-144">tooconvert from a PEM file tooa PFX file, use hello following command:</span></span>

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

<span data-ttu-id="ec501-145">tooconvert uit een PFX-bestand tooa PEM-bestand, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ec501-145">tooconvert from a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="ec501-146">Raadpleeg te[OpenSSL documentatie](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ec501-146">Refer too[OpenSSL documentation](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) for details.</span></span>

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a><span data-ttu-id="ec501-147">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ec501-147">Troubleshooting</span></span>


### <a name="copying-of-hello-application-package-does-not-succeed"></a><span data-ttu-id="ec501-148">Kopiëren van het toepassingspakket Hallo lukt niet</span><span class="sxs-lookup"><span data-stu-id="ec501-148">Copying of hello application package does not succeed</span></span>

<span data-ttu-id="ec501-149">Controleer of `openssh` is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ec501-149">Check if `openssh` is installed.</span></span> <span data-ttu-id="ec501-150">Standaard Ubuntu bureaublad geen geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ec501-150">By default, Ubuntu Desktop doesn't have it installed.</span></span> <span data-ttu-id="ec501-151">Installeren met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ec501-151">Install it using hello following command:</span></span>

```sh
sudo apt-get install openssh-server openssh-client**
```

<span data-ttu-id="ec501-152">Als Hallo probleem zich blijft voordoen, kunt u uitschakelen PAM voor ssh door het wijzigen van Hallo `sshd_config` -bestand met de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="ec501-152">If hello problem persists, try disabling PAM for ssh by changing hello `sshd_config` file using hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

<span data-ttu-id="ec501-153">Als Hallo probleem zich blijft voordoen, kunt u steeds Hallo meer ssh sessies door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="ec501-153">If hello problem still persists, try increasing hello number of ssh sessions by executing hello following commands:</span></span>

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

<span data-ttu-id="ec501-154">Sleutels voor ssh-verificatie (als tegengestelde toopasswords) niet wordt nog ondersteund (omdat het Hallo-platform gebruikt ssh toocopy pakketten), dus in plaats daarvan gebruikt wachtwoordverificatie.</span><span class="sxs-lookup"><span data-stu-id="ec501-154">Using keys for ssh authentication (as opposed toopasswords) isn't yet supported (since hello platform uses ssh toocopy packages), so use password authentication instead.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec501-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec501-155">Next steps</span></span>

[<span data-ttu-id="ec501-156">Hallo-ontwikkelomgeving instellen en implementeren van een Service Fabric-toepassing tooa Linux-cluster.</span><span class="sxs-lookup"><span data-stu-id="ec501-156">Set up hello development environment and deploy a Service Fabric application tooa Linux cluster.</span></span>](service-fabric-get-started-linux.md)

## <a name="related-articles"></a><span data-ttu-id="ec501-157">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="ec501-157">Related articles</span></span>

* [<span data-ttu-id="ec501-158">Aan de slag met Service Fabric en Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ec501-158">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
