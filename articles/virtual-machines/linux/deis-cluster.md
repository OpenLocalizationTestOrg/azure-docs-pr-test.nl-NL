---
title: Implementeren van een 3-node cluster Deis | Microsoft Docs
description: In dit artikel wordt beschreven hoe u een 3-node cluster in Azure met een Azure Resource Manager-sjabloon Deis
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a0c3dd7562dfb5ce54c2ebfd4665109f59cd8fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Implementeren en configureren van een 3-node cluster in Azure Deis
Dit artikel begeleidt u bij het inrichten van een [Deis](http://deis.io/) cluster in Azure. Dit omvat alle stappen van het maken van de benodigde certificaten te implementeren en schalen van een steekproef **gaat** toepassing op het nieuw ingerichte cluster.

Het volgende diagram toont de architectuur van het geïmplementeerde systeem. Een systeembeheerder beheert het cluster met behulp van hulpprogramma's zoals Deis **deis** en **deisctl**. Verbindingen worden tot stand gebracht via een Azure load balancer, die de verbindingen naar een van de lid-knooppunten op het cluster doorstuurt. De toegang van clients geïmplementeerde toepassingen via de load balancer. In dit geval wordt de load balancer stuurt het verkeer naar een Deis router mesh, die verdere routs verkeer naar de bijbehorende Docker-containers die worden gehost op het cluster.

  ![Architectuurdiagram van geïmplementeerde Desis cluster](./media/deis-cluster/architecture-overview.png)

De volgende stappen uitvoeren, hebt u nodig:

* Een actief Azure-abonnement. Als u niet hebt, kunt u een gratis spoor krijgen op [azure.com](https://azure.microsoft.com/).
* Een werk- of schoolaccount-id te gebruiken van Azure-resourcegroepen. Als u een persoonlijk account en meld u aan met een Microsoft-id hebt, moet u [maken van een werk-id van uw persoonlijke](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Een--afhankelijk van uw clientbesturingssysteem--de [Azure PowerShell](/powershell/azureps-cmdlets-docs) of de [Azure CLI voor Mac, Linux en Windows](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL wordt gebruikt voor het genereren van de benodigde certificaten.
* Een client Git zoals [Git Bash](https://git-scm.com/).
* Als u wilt testen van de voorbeeldtoepassing, hebt u ook een DNS-server nodig. U kunt alle DNS-servers of services die ondersteuning bieden voor de A-records jokertekens gebruiken.
* Een computer om uit te voeren Deis clienthulpprogramma's. U kunt een lokale computer of een virtuele machine. U kunt deze hulpprogramma's uitvoeren op bijna elke Linux-distributie, maar de volgende instructies Ubuntu gebruiken.

## <a name="provision-the-cluster"></a>Het cluster inrichten
In deze sectie maakt u een [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) sjabloon uit de opslagplaats voor open-source [azure-snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates). U moet eerst kopiëren omlaag in de sjabloon. Vervolgens maakt u een nieuwe SSH-sleutelpaar voor verificatie. En vervolgens configureert u een nieuwe id voor u cluster. En ten slotte wordt vervolgens gebruikt u de Shell-script of het PowerShell-script voor het inrichten van het cluster.

1. Kloon de opslagplaats: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Ga naar de sjabloonmap:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Maak een nieuwe SSH-sleutelpaar ssh-keygen gebruiken:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Een certificaat met de bovenstaande persoonlijke sleutel genereren:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file to be generated]
5. Ga naar [https://discovery.etcd.io/new](https://discovery.etcd.io/new) voor het genereren van een nieuw cluster token ziet eruit als:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Elke virtuele CoreOS-cluster moet een unieke token van deze gratis service hebben. Zie [virtuele CoreOS documentatie](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) voor meer informatie.
6. Wijzig de **cloud config.yaml** bestand vervangt de bestaande **detectie** token met het nieuwe token:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment the following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Wijzig de **azuredeploy-parameters.json** bestand: het certificaat dat u hebt gemaakt in stap 4 in een teksteditor openen. Kopieer alle tekst tussen `----BEGIN CERTIFICATE-----` en `-----END CERTIFICATE-----` in de **sshKeyData** parameter (moet u alle newline-tekens te verwijderen).
8. Wijzig de **newStorageAccountName** parameter. Dit is het opslagaccount voor VM-OS-schijven. De accountnaam moet globaal uniek zijn.
9. Wijzig de **publicDomainName** parameter. Dit wordt een onderdeel van de DNS-naam die is gekoppeld aan de load balancer openbare IP-adres. De laatste FQDN hebben de indeling van *[waarde van deze parameter]*. *[regio]* . cloudapp.azure.com. Bijvoorbeeld, als u de naam als deishbai32 opgeven en de resourcegroep wordt geïmplementeerd voor de regio VS-West, klikt u vervolgens de uiteindelijke FQDN-naam voor de load balancer worden deishbai32.westus.cloudapp.azure.com.
10. Sla het parameterbestand. En vervolgens inrichten van het cluster met Azure PowerShell:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    of Azure CLI:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Zodra de resourcegroep is geconfigureerd, ziet u alle resources in de groep naar de klassieke Azure-portal. Zoals u in de volgende schermafbeelding ziet, bevat de resourcegroep een virtueel netwerk met drie virtuele machines die zijn gekoppeld aan dezelfde beschikbaarheidsset. De groep bevat ook een load balancer met een bijbehorende openbare IP-adres.
    
    ![De ingerichte resourcegroep in de klassieke Azure-portal](./media/deis-cluster/resource-group.png)

## <a name="install-the-client"></a>De client installeren
U moet **deisctl** om te bepalen uw cluster Deis. Hoewel deisctl automatisch op alle clusterknooppunten is geïnstalleerd, is het raadzaam deisctl gebruiken op een afzonderlijke administratieve machine. Bovendien, omdat alle knooppunten zijn geconfigureerd met alleen persoonlijke IP-adressen, moet u SSH-tunneling via de load balancer met een openbare IP-adres om verbinding met de knooppunt-machines te gebruiken. Hier volgen de stappen voor het instellen van deisctl op een afzonderlijke Ubuntu fysieke of virtuele machine.

1. Installatie deisctl:mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Uw persoonlijke sleutel voor ssh-agent toevoegen:
   
        eval `ssh-agent -s`
        ssh-add [path to the private key file, see step 1 in the previous section]
3. Deisctl configureren:
   
        export DEISCTL_TUNNEL=[public ip of the load balancer]:2223

De sjabloon definieert inkomende NAT-regels die zijn toegewezen 2223 waarvan u een exemplaar van 1, 2224 met exemplaar 2 en 2225 met 3-exemplaar. Dit biedt redundantie voor het gebruik van het hulpprogramma deisctl. U kunt deze regels in de klassieke Azure-portal bekijken:

![NAT-regels op de load balancer](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> De sjabloon ondersteunt momenteel alleen clusters 3-knooppunten. Dit is vanwege een beperking in Azure Resource Manager-sjabloon NAT regeldefinitie, die de syntaxis van de lus niet ondersteunt.
> 
> 

## <a name="install-and-start-the-deis-platform"></a>Installeer en start de Deis platform
Nu kunt u deisctl installeren en start de Deis platform:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path to the private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Starten van het platform even duurt voordat (zo veel 10 minuten). Met name, kan starten van de opbouwfunctie voor service erg lang duren. En soms duurt een paar probeert te slagen: als de bewerking lijkt vastlopen, kunt u `ctrl+c` opsplitsen uitvoeren van de opdracht en probeer het opnieuw.
> 
> 

U kunt `deisctl list` om te controleren of alle services worden uitgevoerd:

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

Gefeliciteerd. Nu u een actieve hebt Deis clsuter op Azure! Vervolgens laten we implementeert u een toepassing Ga om te zien van het cluster in te grijpen.

## <a name="deploy-and-scale-a-hello-world-application"></a>Implementeren en schalen van een toepassing Hello World
De volgende stappen ziet u het implementeren van een 'Hallo wereld' gaat de toepassing aan het cluster. De stappen zijn gebaseerd op [Deis documentatie](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Voor de routering mesh goed te laten werken, moet u een jokerteken A-record voor uw domein die verwijst naar het openbare IP-adres van de load balancer hebben. De volgende schermafbeelding ziet u de A-record voor een voorbeeld-domeinregistratie op GoDaddy:
   
    ![Godaddy-A-record](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Installatie deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Maak een nieuwe SSH-sleutel en voeg vervolgens de openbare sleutel met GitHub (natuurlijk kunt u ook hergebruiken uw bestaande sleutels). Voor het maken van een nieuw sleutelpaar van de SSH-sleutel gebruikt:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s to use default file names and empty passcode)
4. Id_rsa.pub of de openbare sleutel van uw keuze toevoegen met GitHub. U kunt dit doen met behulp van de sleutel toevoegen SSH-knop in het scherm van de SSH-sleutels configuratie:
   
   ![GitHub-sleutel](./media/deis-cluster/github-key.png)
   
   <p />
5. Een nieuwe gebruiker registreren:
   
        deis register http://deis.[your domain]
   <p />
6. De SSH-sleutel toevoegen:
   
        deis keys:add [path to your SSH public key]
   <p />      
7. Een toepassing maken.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.De git push activeren Docker-installatiekopieën worden gemaakt en geïmplementeerd, duurt enkele minuten duren. Mijn ervaring van soms vastlopen stap 10 (Pushing installatiekopie naar de opslagplaats voor persoonlijke). Als dit gebeurt, kunt u het proces beëindigen, verwijdert u de toepassing met behulp van ' deis apps: vernietigen – a <application name> ` to remove the application and try again. You can use `deis apps:list' om erachter te komen met de naam van uw toepassing. Als alles werkt, moet er ongeveer als volgt aan het einde van de uitvoer van de opdracht:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed to Deis
               http://lambda-underdog.artitrack.com
               To learn more, use `deis help` or visit http://deis.io
        To ssh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Controleer of de toepassing werkt:
   
        curl -S http://[your application name].[your domain]
   U ziet het volgende:
   
        Welcome to Deis!
        See the documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list to get the name of your application).
   <p />
10. Schaal de toepassing naar 3 exemplaren:
    
        deis scale cmd=3
    <p />
11. Desgewenst kunt u deis info om te controleren van de details van uw toepassing. De volgende uitvoer zijn van de implementatie van mijn toepassingen:
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Volgende stappen
In dit artikel gelopen u stapsgewijs door de procedure voor het inrichten van een nieuw cluster in Azure met een Azure Resource Manager-sjabloon Deis. De sjabloon ondersteunt redundantie in tooling verbindingen, evenals taakverdeling voor geïmplementeerde toepassingen. De sjabloon ook voorkomt met behulp van openbare IP-adressen op lid-knooppunten, bespaart kostbare openbare IP-netwerkbronnen en biedt een beter beveiligde omgeving host voor toepassingen. Zie voor meer informatie de volgende artikelen:

[Overzicht van Azure Resource Manager][resource-group-overview]  
[Het gebruik van de Azure CLI][azure-command-line-tools]  
[Azure PowerShell gebruiken met Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
