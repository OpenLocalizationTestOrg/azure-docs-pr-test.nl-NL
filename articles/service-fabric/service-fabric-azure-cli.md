---
title: Aan de slag met Azure Service Fabric XPlat CLI
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
ms.openlocfilehash: ddf881f6c202a82a3f64773639aa29b660057f8d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-xplat-cli-to-interact-with-a-service-fabric-cluster"></a>Met behulp van de XPlat CLI om te communiceren met een Service Fabric-cluster

U kunt werken met Service Fabric-cluster van Linux-machines met behulp van de XPlat CLI op Linux.

De eerste stap is Download de nieuwste versie van de CLI van de git-rep en instellen in het pad met de volgende opdrachten:

```sh
 git clone https://github.com/Azure/azure-xplat-cli.git
 cd azure-xplat-cli
 npm install
 sudo ln -s \$(pwd)/bin/azure /usr/bin/azure
 azure servicefabric
```

Voor elke opdracht ondersteunt, kunt u de naam van de opdracht voor het verkrijgen van de help voor de opdracht typen.
Automatisch aanvullen wordt ondersteund voor de opdrachten. De volgende opdracht geeft bijvoorbeeld u Help-informatie voor alle opdrachten voor de toepassing. 

```sh
 azure servicefabric application 
```

U kunt de help voor een specifieke opdracht verder filteren als het volgende voorbeeld wordt getoond:

```sh
 azure servicefabric application  create
```

Als u automatisch aanvullen in de CLI, voert u de volgende opdrachten:

```sh
azure --completion >> ~/azure.completion.sh
echo 'source ~/azure.completion.sh' >> ~/.sh\_profile
source ~/azure.completion.sh
```

De volgende opdrachten verbinding met het cluster en de knooppunten in het cluster weergegeven:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric node show
```

Voor benoemde parameters gebruiken en vinden wat ze zijn, kunt u typen--help na een opdracht. Bijvoorbeeld:

```sh
 azure servicefabric node show --help
 azure servicefabric application create --help
```

Bij het verbinden met een cluster met meerdere machines vanaf een machine **die geen deel uit van het cluster**, gebruik de volgende opdracht:

```sh
 azure servicefabric cluster connect http://PublicIPorFQDN:19080
```

De tag PublicIPorFQDN vervangen door de echte IP of FQDN naar gelang van toepassing. Bij het verbinden met een cluster met meerdere machines vanaf een machine **dat onderdeel is van het cluster**, gebruik de volgende opdracht:

```sh
 azure servicefabric cluster connect --connection-endpoint http://localhost:19080 --client-connection-endpoint PublicIPorFQDN:19000
```

Kunt u PowerShell of CLI om te communiceren met uw Linux Service Fabric-Cluster gemaakt via de Azure portal.

> [!WARNING]
> Deze clusters niet is beveiligd, dus u mogelijk worden openen van de 1-box door het openbare IP-adres toe te voegen in het clustermanifest.

## <a name="using-the-xplat-cli-to-connect-to-a-service-fabric-cluster"></a>Verbinding maken met een Service Fabric-cluster met behulp van de XPlat CLI

De volgende Azure CLI-opdrachten wordt beschreven hoe u verbinding maken met een beveiligde cluster. De details van het certificaat moeten overeenkomen met een certificaat op de clusterknooppunten.

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert
```

Als uw certificaat heeft certificeringsinstanties (CA's), moet u de parameter--ca-certificaat-path op het volgende voorbeeld toevoegen: 

```sh
 azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --ca-cert-path /tmp/ca1,/tmp/ca2 
```

Als u meerdere CA's hebt, gebruikt u een komma als scheidingsteken.

Als de algemene naam in het certificaat komt niet overeen met het verbindingseindpunt, kunt u gebruiken de parameter `--strict-ssl-false` voor het overslaan van de verificatie, zoals wordt weergegeven in de volgende opdracht:

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --strict-ssl-false 
```

Als u de CA-verificatie overslaat wilt, zou u de--parameter afkeuren-niet-geautoriseerde ONWAAR zoals weergegeven in de volgende opdracht: 

```sh
azure servicefabric cluster connect --connection-endpoint http://ip:19080 --client-key-path /tmp/key --client-cert-path /tmp/cert --reject-unauthorized-false 
```

Nadat u verbinding maakt, moet u mogelijk zijn andere CLI-opdrachten om te communiceren met het cluster uit te voeren.

## <a name="deploying-your-service-fabric-application"></a>Uw Service Fabric-toepassing implementeren

Voer de volgende opdrachten om te kopiëren, registreren en start de service fabric-toepassing:

```sh
azure servicefabric application package copy [applicationPackagePath] [imageStoreConnectionString] [applicationPathInImageStore]
azure servicefabric application type register [applicationPathinImageStore]
azure servicefabric application create [applicationName] [applicationTypeName] [applicationTypeVersion]
```

## <a name="upgrading-your-application"></a>Bijwerken van uw toepassing

Het proces is vergelijkbaar met de [processen in Windows](service-fabric-application-upgrade-tutorial-powershell.md)).

Bouwen, kopiëren, registreren en uw toepassing uit de hoofddirectory project maken. Als de naam van uw exemplaar van de `fabric:/MySFApp`, en het type MySFApp is, de opdrachten worden als volgt:

```sh
 azure servicefabric cluster connect http://localhost:19080
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
 azure servicefabric application create fabric:/MySFApp MySFApp 1.0
```

Breng de wijziging aan in uw toepassing en bouw de gewijzigde service opnieuw op.  Bijwerken van de gewijzigde service manifestbestand (ServiceManifest.xml) met de bijgewerkte versies voor de Service (en Code of configuratie of gegevens naar gelang van toepassing). Het toepassingsmanifest (ApplicationManifest.xml) ook wijzigen met het bijgewerkte versienummer voor de toepassing en de gewijzigde service.  Nu, kopiëren en registreren van uw bijgewerkte toepassing met de volgende opdrachten:

```sh
 azure servicefabric cluster connect http://localhost:19080>
 azure servicefabric application package copy MySFApp fabric:ImageStore
 azure servicefabric application type register MySFApp
```

U kunt de upgrade van de toepassing nu starten met de volgende opdracht:

```sh
 azure servicefabric application upgrade start -–application-name fabric:/MySFApp -–target-application-type-version 2.0 --rolling-upgrade-mode UnmonitoredAuto
```

Nu kunt u de upgrade van de toepassing met behulp van SFX bewaken. De upgrade van de toepassing is binnen enkele minuten voltooid. U kunt ook een app bijgewerkt met een fout te en de automatische terugdraaifunctie in service fabric.

## <a name="converting-from-pfx-to-pem-and-vice-versa"></a>Converteren van PFX naar PEM en omgekeerd

Mogelijk moet u een certificaat installeren in uw lokale computer (met Windows of Linux) voor toegang tot beveiligde clusters die mogelijk in een andere omgeving. Bijvoorbeeld bij het openen van een beveiligde Linux-cluster van een Windows-machine en omgekeerd wellicht moet u uw certificaat voor converteren van PFX naar PEM en vice versa. 

Als u wilt converteren van een PEM-bestand naar een PFX-bestand, moet u de volgende opdracht gebruiken:

```bash
openssl pkcs12 -export -out certificate.pfx -inkey mycert.pem -in mycert.pem -certfile mycert.pem
```

Gebruik de volgende opdracht om een PFX-bestand te converteren naar een PEM-bestand:

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

Raadpleeg de [OpenSSL-documentatie](https://www.openssl.org/docs/man1.0.1/apps/pkcs12.html) voor meer informatie.

<a id="troubleshooting"></a>

## <a name="troubleshooting"></a>Problemen oplossen


### <a name="copying-of-the-application-package-does-not-succeed"></a>Kopiëren van het toepassingspakket lukt niet

Controleer of `openssh` is geïnstalleerd. Standaard Ubuntu bureaublad geen geïnstalleerd. Installeren met behulp van de volgende opdracht:

```sh
sudo apt-get install openssh-server openssh-client**
```

Als het probleem zich blijft voordoen, kunt u uitschakelen PAM voor ssh door het wijzigen van de `sshd_config` bestand met de volgende opdrachten:

```sh
sudo vi /etc/ssh/sshd_config
#Change the line with UsePAM to the following: UsePAM no
sudo service sshd reload
```

Als het probleem zich blijft voordoen, kunt u proberen om het aantal ssh sessies door het uitvoeren van de volgende opdrachten:

```sh
sudo vi /etc/ssh/sshd\_config
# Add the following to lines:
# MaxSessions 500
# MaxStartups 300:30:500
sudo service sshd reload
```

Gebruik van sleutels voor ssh-verificatie (in plaats van wachtwoorden) niet wordt nog ondersteund (omdat het platform worden gebruikt voor ssh pakketten kopiëren), dus in plaats daarvan gebruiken wachtwoordverificatie.

## <a name="next-steps"></a>Volgende stappen

[De ontwikkelomgeving instellen en implementeren van een Service Fabric-toepassing naar een Linux-cluster.](service-fabric-get-started-linux.md)

## <a name="related-articles"></a>Verwante artikelen:

* [Aan de slag met Service Fabric en Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
