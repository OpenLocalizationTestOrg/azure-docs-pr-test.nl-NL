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
# <a name="using-hello-xplat-cli-toointeract-with-a-service-fabric-cluster"></a>Hallo toointeract XPlat CLI gebruiken met een Service Fabric-cluster

U kunt werken met Service Fabric-cluster van Linux-machines Hallo XPlat CLI met op Linux.

Hallo eerste stap is Hallo meest recente versie van Hallo CLI ophalen uit Hallo git rep en stel het in uw pad met Hallo volgende opdrachten:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Voor elke opdracht ondersteunt, kunt u de naam van de Hallo Hallo opdracht tooobtain Hallo Help voor de opdracht typen.
Automatisch aanvullen wordt ondersteund voor Hallo-opdrachten. Bijvoorbeeld: hello opdracht geeft die u voor alle Hallo toepassing opdrachten te volgen. 

```sh
 azure servicefabric application 
```

U kunt verder Hallo help tooa specifieke opdracht filteren als Hallo volgende voorbeeld wordt getoond:

```sh
 azure servicefabric application  create
```

tooenable automatisch aanvullen in Hallo CLI Hallo volgende opdrachten uitvoeren:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

Hallo opdrachten na verbinding toohello cluster en Hallo van knooppunten in cluster Hallo weergeven:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

toouse benoemde parameters uit te vinden wat ze zijn, kunt u typen--help na een opdracht. Bijvoorbeeld:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Bij het cluster met meerdere machines tooa verbinden van een virtuele machine **die geen deel uit van de cluster Hallo**, Hallo volgende opdracht gebruiken:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

Vervangen door Hallo PublicIPorFQDN tag Hallo echte IP of FQDN naar gelang van toepassing. Bij het cluster met meerdere machines tooa verbinden van een virtuele machine **die deel uitmaken van Hallo cluster**, Hallo volgende opdracht gebruiken:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Kunt u PowerShell of CLI toointeract met uw Service Fabric-Cluster van Linux via hello Azure-portal is gemaakt.

> [!WARNING]
> Deze clusters niet is beveiligd, dus u mogelijk worden openen van de 1-box door Hallo openbaar IP-adres toe te voegen in het clustermanifest Hallo.

## <a name="using-hello-xplat-cli-tooconnect-tooa-service-fabric-cluster"></a>Hallo XPlat CLI tooconnect tooa Service Fabric-cluster gebruiken

Hello Azure CLI-opdrachten na beschrijven hoe tooconnect tooa cluster beveiligen. details van Hallo certificaat moeten overeenkomen met een certificaat op de clusterknooppunten Hallo.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Als uw certificaat heeft certificeringsinstanties (CA's), moet u tooadd Hallo--ca-certificaat-path-parameter zoals Hallo voorbeeld te volgen: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Als u meerdere CA's hebt, gebruikt u een komma als scheidingsteken Hallo.

Als de algemene naam in Hallo certificaat komt niet overeen met de Hallo verbindingseindpunt, kunt u gebruiken Hallo parameter `--strict-ssl-false` toobypass Hallo verificatie, zoals wordt weergegeven in de volgende opdracht Hallo:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Als u tooskip Hallo CA verificatie wilt, kunt u Hallo--afkeuren-niet-geautoriseerde ONWAAR parameter zoals weergegeven in de volgende opdracht Hallo toevoegen: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Nadat u verbinding maakt, moet u kunnen toorun andere toointeract CLI-opdrachten met Hallo-cluster.

## <a name="deploying-your-service-fabric-application"></a>Uw Service Fabric-toepassing implementeren

Hallo opdrachten toocopy, registreren en start de service fabric-toepassing hello volgende uitvoeren:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Bijwerken van uw toepassing

Hallo-proces is vergelijkbaar toohello [processen in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Bouwen, kopiëren, registreren en uw toepassing uit de hoofddirectory project maken. Als de naam van uw exemplaar van de `fabric:/MySFApp`, en Hallo type MySFApp, Hallo opdrachten worden als volgt:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Controleer Hallo tooyour toepassing wijzigen en gewijzigd Hallo-service opnieuw.  Hallo update gewijzigd van service manifestbestand (ServiceManifest.xml) met Hallo bijgewerkt versies voor het Hallo-Service (en Code of configuratie of gegevens naar gelang van toepassing). Ook wijzigen van de toepassing hello-manifest (ApplicationManifest.xml) met versienummer Hallo bijgewerkt voor de toepassing hello en Hallo gewijzigde service.  Nu, kopiëren en de bijgewerkte toepassing met behulp van de volgende opdrachten Hallo registreren:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

U kunt nu de upgrade van de toepassing hello starten met Hallo volgende opdracht:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Nu kunt u de upgrade van de toepassing hello SFX met bewaken. In een paar minuten zou Hallo toepassing zijn bijgewerkt. U kunt ook een app bijgewerkt met een fout te en Hallo automatische terugdraaifunctie in service fabric.

## <a name="converting-from-pfx-toopem-and-vice-versa"></a>Converteren van PFX-tooPEM en omgekeerd

Mogelijk moet u een certificaat tooinstall in uw lokale computer (met Windows of Linux) tooaccess beveiligde clusters die mogelijk in een andere omgeving. Bijvoorbeeld bij het openen van een beveiligde Linux-cluster van een Windows-machine en omgekeerd moet u mogelijk tooconvert uw certificaat uit het PFX-tooPEM en vice versa. 

tooconvert uit een PEM-bestand tooa PFX-bestand, gebruik Hallo volgende opdracht:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

tooconvert uit een PFX-bestand tooa PEM-bestand, gebruik Hallo volgende opdracht:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Raadpleeg te[OpenSSL documentatie](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) voor meer informatie.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Problemen oplossen


### <a name="copying-of-hello-application-package-does-not-succeed"></a>Kopiëren van het toepassingspakket Hallo lukt niet

Controleer of `openssh` is geïnstalleerd. Standaard Ubuntu bureaublad geen geïnstalleerd. Installeren met behulp van de volgende opdracht Hallo:

```sh
sudo apt-get install openssh-server openssh-client**
```

Als Hallo probleem zich blijft voordoen, kunt u uitschakelen PAM voor ssh door het wijzigen van Hallo `sshd_config` -bestand met de volgende opdrachten Hallo:

```sh
sudo vi /etc/ssh/sshd_config
#Change hello line with UsePAM toohello following: UsePAM no
sudo service sshd reload
```

Als Hallo probleem zich blijft voordoen, kunt u steeds Hallo meer ssh sessies door het uitvoeren van de volgende opdrachten Hallo:

```sh
sudo vi /etc/ssh/sshd\_config
# Add hello following toolines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Sleutels voor ssh-verificatie (als tegengestelde toopasswords) niet wordt nog ondersteund (omdat het Hallo-platform gebruikt ssh toocopy pakketten), dus in plaats daarvan gebruikt wachtwoordverificatie.

## <a name="next-steps"></a>Volgende stappen

[Hallo-ontwikkelomgeving instellen en implementeren van een Service Fabric-toepassing tooa Linux-cluster.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Verwante artikelen:

* [Aan de slag met Service Fabric en Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
