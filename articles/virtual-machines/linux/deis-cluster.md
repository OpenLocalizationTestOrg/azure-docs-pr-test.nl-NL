---
title: aaaDeploy Deis een 3-node cluster | Microsoft Docs
description: Dit artikel wordt beschreven hoe toocreate een 3-knooppunt Deis cluster in Azure met een Azure Resource Manager-sjabloon
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
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Implementeren en configureren van een 3-node cluster in Azure Deis
Dit artikel begeleidt u bij het inrichten van een [Deis](http://deis.io/) cluster in Azure. Dit omvat alle Hallo stappen van Hallo benodigde certificaten toodeploying maken en schalen van een steekproef **gaat** toepassing op nieuw ingerichte Hallo-cluster.

Hallo toont volgende diagram de architectuur Hallo van systeem Hallo geïmplementeerd. Een systeembeheerder beheert Hallo cluster met behulp van hulpprogramma's zoals Deis **deis** en **deisctl**. Verbindingen worden tot stand gebracht via een Azure load balancer, die Hallo verbindingen tooone van Hallo lid knooppunten op Hallo-cluster doorstuurt. Hallo clients toegang geïmplementeerde toepassingen via ook Hallo load balancer. In dit geval Hallo load balancer Hallo verkeer tooa stuurt Deis router mesh, die verdere routs verkeer toocorresponding Docker containers die worden gehost op Hallo-cluster.

  ![Architectuurdiagram van geïmplementeerde Desis cluster](./media/deis-cluster/architecture-overview.png)

In de volgorde toorun via Hallo stappen te volgen, hebt u het volgende nodig:

* Een actief Azure-abonnement. Als u niet hebt, kunt u een gratis spoor krijgen op [azure.com](https://azure.microsoft.com/).
* Een werk of school id toouse Azure-resourcegroepen. Als u een persoonlijk account en meld u aan met een Microsoft-id hebt, moet u deze te[maken van een werk-id van uw persoonlijke](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Een--, afhankelijk van uw client-besturingssysteem--Hallo [Azure PowerShell](/powershell/azureps-cmdlets-docs) of Hallo [Azure CLI voor Mac, Linux en Windows](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL is gebruikte toogenerate Hallo benodigde certificaten.
* Een client Git zoals [Git Bash](https://git-scm.com/).
* voorbeeldtoepassing tootest hello, hebt u ook een DNS-server nodig. U kunt alle DNS-servers of services die ondersteuning bieden voor de A-records jokertekens gebruiken.
* Een computer toorun Deis clienthulpprogramma's. U kunt een lokale computer of een virtuele machine. U kunt deze hulpprogramma's uitvoeren op bijna elke Linux-distributie, maar hello volgende instructies gebruiken Ubuntu.

## <a name="provision-hello-cluster"></a>Hallo-cluster inrichten
In deze sectie maakt u een [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) sjabloon van Hallo open-source opslagplaats [azure-snelstartsjablonen](https://github.com/Azure/azure-quickstart-templates). U moet eerst omlaag Hallo sjabloon kopiëren. Vervolgens maakt u een nieuwe SSH-sleutelpaar voor verificatie. En vervolgens configureert u een nieuwe id voor u cluster. En ten slotte kunt u Hallo Shell-script of Hallo PowerShell script tooprovision Hallo cluster.

1. Kloon Hallo opslagplaats: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Ga toohello sjabloonmap:
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Maak een nieuwe SSH-sleutelpaar ssh-keygen gebruiken:
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Een certificaat met de Hallo boven de persoonlijke sleutel genereren:
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Ga te[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate een nieuw cluster-token ziet eruit als:
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Elke virtuele CoreOS-cluster moet een unieke token van deze gratis service toohave. Zie [virtuele CoreOS documentatie](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) voor meer informatie.
6. Hallo wijzigen **cloud config.yaml** bestand tooreplace Hallo bestaande **detectie** token met het nieuwe token Hallo:
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Hallo wijzigen **azuredeploy-parameters.json** bestand: u hebt gemaakt in stap 4 in een teksteditor openen Hallo-certificaat. Kopieer alle tekst tussen `----BEGIN CERTIFICATE-----` en `-----END CERTIFICATE-----` in Hallo **sshKeyData** parameter (u moet tooremove alle newline-tekens).
8. Hallo wijzigen **newStorageAccountName** parameter. Dit is de opslagaccount Hallo voor VM-OS-schijven. De accountnaam heeft toobe globaal uniek zijn.
9. Hallo wijzigen **publicDomainName** parameter. Hiermee wordt een onderdeel van Hallo DNS-naam die is gekoppeld aan Hallo load balancer openbare IP-adres. Hallo laatste FQDN hebben Hallo indeling van *[waarde van deze parameter]*. *[regio]* . cloudapp.azure.com. Bijvoorbeeld, als u Hallo naam als deishbai32 opgeven en Hallo resourcegroep bevindt zich de regio VS-West geïmplementeerde toohello en vervolgens laatste Hallo FQDN tooyour load balancer worden deishbai32.westus.cloudapp.azure.com.
10. Hallo parameterbestand opslaan. En vervolgens kunt u met Azure PowerShell Hallo-cluster inrichten:
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    of Azure CLI:
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Zodra de resourcegroep Hallo is geconfigureerd, ziet u alle Hallo bronnen in Hallo-groep op de klassieke Azure-portal. Zoals u in de volgende schermafbeelding Hallo Hallo resourcegroep bevat een virtueel netwerk met drie virtuele machines, die lid zijn van toohello dezelfde beschikbaarheidsset. Hallo-groep bevat ook een load balancer met een bijbehorende openbare IP-adres.
    
    ![Hallo ingericht resourcegroep in de klassieke Azure-portal](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Hallo-client installeren
U moet **deisctl** toocontrol uw cluster Deis. Hoewel deisctl wordt automatisch geïnstalleerd op alle clusterknooppunten van hello, is een goede gewoonte toouse deisctl op een afzonderlijke administratieve machine. Bovendien, omdat alle knooppunten zijn geconfigureerd met alleen persoonlijke IP-adressen, moet u toouse SSH-tunneling via Hallo load balancer met een openbare IP-adres, tooconnect toohello knooppunt machines. Hallo volgen Hallo stappen voor het instellen van deisctl op een afzonderlijke Ubuntu fysieke of virtuele machine.

1. Installatie deisctl:mkdir deis
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. De agent van uw persoonlijke sleutel toossh toevoegen:
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Deisctl configureren:
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

Hallo sjabloon definieert inkomende NAT-regels die zijn toegewezen 2223 tooinstance 1, 2224 tooinstance 2 en 2225 tooinstance 3. Dit biedt redundantie voor het gebruik Hallo deisctl hulpprogramma. U kunt deze regels in de klassieke Azure-portal bekijken:

![NAT-regels op Hallo load balancer](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Hallo sjabloon ondersteunt momenteel alleen clusters 3-knooppunten. Dit is vanwege een beperking in Azure Resource Manager-sjabloon NAT regeldefinitie, die de syntaxis van de lus niet ondersteunt.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Installeren en starten Hallo Deis platform
Nu u kunt deisctl tooinstall gebruiken en Hallo start Deis platform:

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Begin Hallo platform even duurt voordat (zo veel 10 minuten). Met name, kan Hallo builder-service wordt gestart lang duren. En soms duurt een paar pogingen toosucceed: als Hallo bewerking toohang lijkt, kunt u `ctrl+c` toobreak uitvoering van het Hallo-opdracht en probeer het opnieuw.
> 
> 

U kunt `deisctl list` tooverify als alle services worden uitgevoerd:

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

Gefeliciteerd. Nu u een actieve hebt Deis clsuter op Azure! Vervolgens laten we u een voorbeeld Ga toepassing toosee Hallo cluster in actie implementeert.

## <a name="deploy-and-scale-a-hello-world-application"></a>Implementeren en schalen van een toepassing Hello World
Hallo volgende stappen laten zien hoe toodeploy "Hallo wereld" Ga toepassing toohello cluster. Hallo stappen zijn gebaseerd op [Deis documentatie](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Voor Hallo routering mesh toowork goed is, moet u toohave een jokerteken A-record voor uw domein toohello openbare IP-adres van Hallo load balancer aan te wijzen. Hallo volgende schermafbeelding ziet Hallo A-record voor een voorbeeld-domeinregistratie op GoDaddy:
   
    ![Godaddy-A-record](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Installatie deis:
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Maak een nieuwe SSH-sleutel en voeg vervolgens de openbare sleutel tooGitHub hello (natuurlijk kunt u ook hergebruiken uw bestaande sleutels). een nieuw SSH-sleutelpaar, toocreate gebruiken:
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Id_rsa.pub of openbare sleutel van uw keuze, tooGitHub Hallo toevoegen. U kunt dit doen via Hallo toevoegen SSH sleutel knop in het scherm van de SSH-sleutels configuratie:
   
   ![GitHub-sleutel](./media/deis-cluster/github-key.png)
   
   <p />
5. Een nieuwe gebruiker registreren:
   
        deis register http://deis.[your domain]
   <p />
6. Hallo SSH-sleutel toevoegen:
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Een toepassing maken.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.Hallo git push activeren Docker installatiekopieën toobe gemaakt en geïmplementeerd, duurt enkele minuten duren. Mijn ervaring van soms vastlopen stap 10 (Pushing tooprivate-opslagplaats voor installatiekopieën). Als dit gebeurt, kunt u Hallo-proces stoppen verwijderen Hallo toepassing gebruikt ' deis apps: vernietigen – a <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind Hallo-naam van uw toepassing. Als alles werkt, ziet u dat lijkt op de volgende Hallo aan Hallo einde van de uitvoer van de opdracht:
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Controleer of de toepassing hello werkt:
   
        curl -S http://[your application name].[your domain]
   U ziet het volgende:
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Hallo too3 toepassingsexemplaren schalen:
    
        deis scale cmd=3
    <p />
11. Desgewenst kunt u deis info tooexamine details van uw toepassing. Hallo zijn volgende uitgangen van de implementatie van mijn toepassingen:
    
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
In dit artikel doorlopen u alle Hallo stappen tooprovision Deis van een nieuw cluster in Azure met een Azure Resource Manager-sjabloon. Hallo sjabloon ondersteunt redundantie in tooling verbindingen, evenals taakverdeling voor geïmplementeerde toepassingen. Hallo sjabloon voorkomt ook met behulp van openbare IP-adressen op lid-knooppunten, bespaart kostbare openbare IP-netwerkbronnen en biedt een beter beveiligde omgeving toohost toepassingen. toolearn Zie meer Hallo artikelen te volgen:

[Overzicht van Azure Resource Manager][resource-group-overview]  
[Hoe toouse hello Azure CLI][azure-command-line-tools]  
[Azure PowerShell gebruiken met Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
