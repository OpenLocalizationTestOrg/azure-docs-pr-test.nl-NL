---
title: aaaConnect HDInsight tooyour on-premises netwerk - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate een HDInsight-cluster in een Azure-netwerk en sluit vervolgens tooyour on-premises netwerk. Meer informatie over hoe tooconfigure naamomzetting tussen HDInsight en uw on-premises netwerk via een aangepaste DNS-server.
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a3adf0e3df7726d8e6566d723700506baaf89a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-hdinsight-tooyour-on-premise-network"></a>HDInsight tooyour on-premises netwerk verbinden

Meer informatie over hoe tooconnect HDInsight tooyour on-premises netwerk door met behulp van Azure Virtual Networks en een VPN-gateway. Dit document bevat de planningsinformatie over:

* Gebruik HDInsight in een Azure-netwerk die verbinding tooyour maakt on-premises netwerk.

* Configureren van DNS-naamomzetting tussen Hallo virtuele netwerk en uw on-premises netwerk.

* Network security groepen toorestrict internet toegang tooHDInsight configureren.

* Poorten die zijn geleverd door HDInsight op Hallo virtueel netwerk.

## <a name="create-hello-virtual-network-configuration"></a>Hallo-configuratie voor virtuele netwerken maken

> [!IMPORTANT]
> Als u op zoek bent voor stapsgewijze instructies voor het verbinden van HDInsight tooyour lokaal netwerk met een virtueel netwerk van Azure, Zie Hallo [verbinding maken met HDInsight tooyour on-premises netwerk](connect-on-premises-network.md) document.

Gebruik Hallo volgende documenten toolearn hoe een Azure-netwerk dat is verbonden tooyour toocreate lokale netwerk:
    
* [Met behulp van hello Azure-portal](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)

* [Azure PowerShell gebruiken](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)

* [Azure CLI gebruiken](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli.md)

## <a name="configure-name-resolution"></a>Naamomzetting configureren

tooallow HDInsight en resources die lid zijn van Hallo netwerk toocommunicate met de naam, moet u de volgende activiteiten Hallo uitvoeren:

* Maak een aangepaste DNS-server in hello Azure Virtual Network.

* Hallo virtueel netwerk toouse Hallo aangepaste DNS-server in plaats van Hallo standaard Azure recursieve naamomzetting configureren.

* Configureren van forwarding tussen Hallo aangepaste DNS-server en de lokale DNS-server.

Deze configuratie kunt Hallo volgende gedrag:

* Aanvragen voor de volledig gekwalificeerde domeinnamen met Hallo DNS-achtervoegsel __voor het virtuele netwerk Hallo__ toohello aangepaste DNS-server worden doorgestuurd. Hallo aangepaste DNS-server stuurt vervolgens deze aanvragen toohello Azure recursieve Resolver, die als resultaat Hallo IP-adres.

* Alle andere aanvragen worden doorgestuurd toohello lokale DNS-server. Zelfs aanvragen voor het openbare internet-bronnen zoals microsoft.com doorgestuurd toohello lokale DNS-server voor naamomzetting.

Groen regels zijn in Hallo diagram te volgen, aanvragen voor bronnen die op Hallo DNS-achtervoegsel van het virtuele netwerk Hallo eindigen. Blauwe lijnen zijn aanvragen voor bronnen in Hallo on-premises netwerk of op Hallo openbare internet.

![Diagram van hoe de DNS-aanvragen worden verwerkt in Hallo-configuratie gebruikt in dit document](./media/connect-on-premises-network/on-premises-to-cloud-dns.png)

### <a name="create-a-custom-dns-server"></a>Maken van een aangepaste DNS-server

> [!IMPORTANT]
> U moet maken en configureren van Hallo DNS-server voordat u HDInsight in Hallo virtueel netwerk installeert.

een Linux-VM die gebruikmaakt van Hallo toocreate [binden](https://www.isc.org/downloads/bind/) DNS-software, gebruik Hallo stappen te volgen:

> [!NOTE]
> Hallo volgende stappen gebruikt Hallo [Azure-portal](https://portal.azure.com) toocreate een virtuele Machine van Azure. Zie voor andere toocreate manieren een virtuele machine Hallo [VM maken, Azure CLI](../virtual-machines/linux/quick-create-cli.md) en [VM maken, Azure PowerShell](../virtual-machines/linux/quick-create-portal.md) documenten.

1. Van Hallo [Azure-portal](https://portal.azure.com), selecteer  __+__ , __Compute__, en __Ubuntu Server 16.04 LTS__.

    ![Een virtuele Ubuntu-machine maken](./media/connect-on-premises-network/create-ubuntu-vm.png)

2. Van Hallo __basisbeginselen__ sectie, voert u Hallo volgende informatie:

    * __Naam__: een beschrijvende naam die deze virtuele machine wordt aangeduid. Bijvoorbeeld: __DNSProxy__.
    * __Gebruikersnaam__: naam Hallo Hallo SSH-account.
    * __Openbare SSH-sleutel__ of __wachtwoord__: Hallo verificatiemethode voor Hallo SSH-account. Wordt aangeraden met openbare sleutels, omdat ze beter te beveiligen. Zie voor meer informatie, Hallo [maken en gebruiken SSH-sleutels voor virtuele Linux-machines](../virtual-machines/linux/mac-create-ssh-keys.md) document.
    * __Resourcegroep__: Selecteer __gebruik bestaande__, en selecteer vervolgens de resourcegroep Hallo met Hallo virtueel netwerk eerder hebt gemaakt.
    * __Locatie__: Selecteer dezelfde locatie als het virtuele netwerk Hallo Hallo.

    ![Basisconfiguratie van de virtuele machine](./media/connect-on-premises-network/vm-basics.png)

    Laat de andere vermeldingen op Hallo standaardwaarden en selecteer vervolgens __OK__.

3. Van Hallo __een grootte kiezen__ sectie, selecteer Hallo VM-grootte. Voor deze zelfstudie Hallo kleinste selecteren en de laagste kosten optie. toocontinue, gebruik Hallo __Selecteer__ knop.

4. Van Hallo __instellingen__ sectie, voert u Hallo volgende informatie:

    * __Virtueel netwerk__: Selecteer Hallo virtueel netwerk dat u eerder hebt gemaakt.

    * __Subnet__: Hallo standaard subnet voor het virtuele netwerk Hallo selecteert. Voer __niet__ Selecteer Hallo subnet dat wordt gebruikt door Hallo VPN-gateway.

    * __Opslagaccount voor diagnostische gegevens__: Selecteer een bestaand opslagaccount of maak een nieuwe.

    ![Virtuele-netwerkinstellingen](./media/connect-on-premises-network/virtual-network-settings.png)

    Hallo andere vermeldingen laten op het Hallo-standaardwaarde, selecteert u vervolgens __OK__ toocontinue.

5. Van Hallo __aankoop__ sectie, selecteer Hallo __aankoop__ knop toocreate Hallo virtuele machine.

6. Zodra Hallo virtuele machine is gemaakt, de __overzicht__ sectie wordt weergegeven. Selecteer in lijst aan de linkerkant Hallo Hallo __eigenschappen__. Hallo opslaan __openbaar IP-adres__ en __particuliere IP-adres__ waarden. Deze wordt gebruikt in de volgende sectie Hallo.

    ![Openbare en particuliere IP-adressen](./media/connect-on-premises-network/vm-ip-addresses.png)

### <a name="install-and-configure-bind-dns-software"></a>Installeren en configureren van de binding (DNS-software)

1. Gebruik van SSH tooconnect toohello __openbaar IP-adres__ van Hallo virtuele machine. Hallo volgende voorbeeld maakt tooa virtuele machine op 40.68.254.142 verbinding:

    ```bash
    ssh sshuser@40.68.254.142
    ```

    Vervang `sshuser` Hello SSH gebruikersaccount die u hebt opgegeven bij het maken van Hallo-cluster.

    > [!NOTE]
    > Er zijn tal van manieren tooobtain hello `ssh` hulpprogramma. Op Linux, Unix- en Mac OS, wordt dit geleverd als onderdeel van het Hallo-besturingssysteem. Als u van Windows gebruikmaakt, overweeg dan een Hallo volgende opties:
    >
    > * [Azure-Cloud-Shell](../cloud-shell/quickstart.md)
    > * [Bash op Ubuntu op Windows 10](https://msdn.microsoft.com/commandline/wsl/about)
    > * [GIT (https://git-scm.com/)](https://git-scm.com/)
    > * [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)

2. tooinstall binding, gebruik Hallo volgende opdrachten uit Hallo SSH-sessie:

    ```bash
    sudo apt-get update -y
    sudo apt-get install bind9 -y
    ```

3. tooconfigure Bind tooforward aanvragen tooyour on-premises DNS-server voor naamomzetting, gebruiken na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.options` bestand:

        acl goodclients {
            10.0.0.0/16; # Replace with hello IP address range of hello virtual network
            10.1.0.0/16; # Replace with hello IP address range of hello on-premises network
            localhost;
            localnets;
        };

        options {
                directory "/var/cache/bind";

                recursion yes;

                allow-query { goodclients; };

                forwarders {
                192.168.0.1; # Replace with hello IP address of hello on-premises DNS server
                };

                dnssec-validation auto;

                auth-nxdomain no;    # conform tooRFC1035
                listen-on { any; };
        };

    > [!IMPORTANT]
    > Vervang de waarden Hallo in Hallo `goodclients` sectie met Hallo IP-adresbereik van Hallo virtueel netwerk en on-premises netwerk. Deze sectie definieert hello-mailadressen die deze DNS-server aanvragen van accepteert.
    >
    > Vervang Hallo `192.168.0.1` vermelding in Hallo `forwarders` sectie met Hallo IP-adres van uw lokale DNS-server. Deze vermelding routes DNS-aanvragen tooyour lokale DNS-server voor naamomzetting.

    tooedit dit bestand, gebruik Hallo volgende opdracht:

    ```bash
    sudo nano /etc/bind/named.conf.options
    ```

    Gebruik-bestand Hallo toosave __Ctrl + X__, __Y__, en vervolgens __Enter__.

4. Gebruik van Hallo SSH-sessie, Hallo volgende opdracht:

    ```bash
    hostname -f
    ```

    Met deze opdracht retourneert een waarde van een vergelijkbare toohello volgende tekst:

        dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net

    Hallo `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` tekst hello is __DNS-achtervoegsel__ voor dit virtuele netwerk. Deze waarde niet opslaan omdat het wordt later gebruikt.

5. tooconfigure Bind tooresolve DNS-namen voor resources binnen het virtuele netwerk hello, gebruiken na de tekst hello inhoud Hallo Hallo `/etc/bind/named.conf.local` bestand:

        // Replace hello following with hello DNS suffix for your virtual network
        zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
            type forward;
            forwarders {168.63.129.16;}; # hello Azure recursive resolver
        };

    > [!IMPORTANT]
    > Vervang Hallo `icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net` met Hallo DNS-achtervoegsel die u eerder hebt opgehaald.

    tooedit dit bestand, gebruik Hallo volgende opdracht:

    ```bash
    sudo nano /etc/bind/named.conf.local
    ```

    Gebruik-bestand Hallo toosave __Ctrl + X__, __Y__, en vervolgens __Enter__.

6. toostart binding, Hallo volgende opdracht gebruiken:

    ```bash
    sudo service bind9 restart
    ```

7. tooverify die binden kunt oplossen Hallo namen van resources in uw on-premises netwerk, gebruik Hallo volgende opdrachten:

    ```bash
    sudo apt install dnsutils
    nslookup dns.mynetwork.net 10.0.0.4
    ```

    > [!IMPORTANT]
    > Vervang `dns.mynetwork.net` met Hallo volledig gekwalificeerde domeinnaam (FQDN) van een bron in uw on-premises netwerk.
    >
    > Vervang `10.0.0.4` Hello __interne IP-adres__ van uw aangepaste DNS-server in het virtuele netwerk Hallo.

    antwoord Hallo verschijnt vergelijkbare toohello volgende tekst:

        Server:         10.0.0.4
        Address:        10.0.0.4#53

        Non-authoritative answer:
        Name:   dns.mynetwork.net
        Address: 192.168.0.4

### <a name="configure-hello-virtual-network-toouse-hello-custom-dns-server"></a>Hallo virtueel netwerk toouse Hallo aangepaste DNS-server configureren

tooconfigure hello virtueel netwerk toouse Hallo aangepaste DNS-server in plaats van hello Azure recursieve resolver, gebruik Hallo stappen te volgen:

1. In Hallo [Azure-portal](https://portal.azure.com)Hallo virtueel netwerk selecteert en selecteer vervolgens __DNS-Servers__.

2. Selecteer __aangepaste__, en Voer Hallo __interne IP-adres__ van Hallo aangepaste DNS-server. Tot slot selecteert __opslaan__.

    ![Hallo aangepaste DNS-server voor Hallo netwerk instellen](./media/connect-on-premises-network/configure-custom-dns.png)

### <a name="configure-hello-on-premises-dns-server"></a>Hallo lokale DNS-server configureren

In de vorige sectie hello, moet u Hallo aangepaste DNS-server tooforward aanvragen toohello lokale DNS-server geconfigureerd. Vervolgens configureert u Hallo lokale DNS-server tooforward aanvragen toohello aangepaste DNS-server.

Voor specifieke stappen over het tooconfigure uw DNS-server, Raadpleeg de documentatie van de Hallo voor uw DNS-server-software. Zoek naar Hallo Stapsgewijze instructies voor het tooconfigure een __voorwaardelijke doorstuurserver__.

Een voorwaardelijke voorwaartse verzendt alleen aanvragen voor een specifieke DNS-achtervoegsel. In dit geval moet u een doorstuurserver voor Hallo DNS-achtervoegsel van het virtuele netwerk Hallo configureren. Aanvragen voor dit achtervoegsel moeten toohello IP-adres van Hallo aangepaste DNS-server worden doorgestuurd. 

Hallo volgende tekst is een voorbeeld van een voorwaardelijke doorstuurserver-configuratie voor Hallo **binden** DNS-software:

    zone "icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello custom DNS server's internal IP address
    };

Voor informatie over het gebruik van DNS op **Windows Server 2016**, Zie Hallo [toevoegen DnsServerConditionalForwarderZone](https://technet.microsoft.com/itpro/powershell/windows/dnsserver/add-dnsserverconditionalforwarderzone) documentatie...

Wanneer u Hallo lokale DNS-server hebt geconfigureerd, kunt u `nslookup` van Hallo lokale netwerk tooverify in Hallo virtueel netwerk dat u het kunt oplossen namen. Hallo voorbeeld te volgen 

```bash
nslookup dnsproxy.icb0d0thtw0ebifqt0g1jycdxd.ex.internal.cloudapp.net 196.168.0.4
```

In dit voorbeeld maakt gebruik van de lokale DNS-server op 196.168.0.4 Hallo tooresolve Hallo-naam van Hallo aangepaste DNS-server. Hallo IP-adres vervangen door Hallo voor Hallo lokale DNS-server. Vervang Hallo `dnsproxy` adres met de volledig gekwalificeerde domeinnaam Hallo van Hallo aangepaste DNS-server.

## <a name="optional-control-network-traffic"></a>Optioneel: Besturingselement netwerkverkeer

U kunt de netwerkbeveiligingsgroepen (NSG) of de gebruiker gedefinieerde routes (UDR) toocontrol-netwerkverkeer. Nsg's kunnen u toofilter binnenkomend en uitgaand verkeer, en verkeer toestaan of weigeren Hallo. Udr's kunnen u toocontrol hoe tussen resources in het virtuele netwerk Hallo verkeersstromen Hallo van internet en Hallo on-premises netwerk.

> [!WARNING]
> HDInsight vereist binnenkomende toegang van specifieke IP-adressen in hello Azure-cloud en onbeperkte uitgaande toegang. Wanneer u nsg's of udr's toocontrol-verkeer gebruikt, moet u Hallo stappen uitvoeren:
>
> 1. Hallo IP-adressen voor Hallo locatie waarin het virtuele netwerk zoeken. Zie voor een lijst met vereiste IP-adressen per locatie, [vereiste IP-adressen](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-ip).
>
> 2. Binnenkomend verkeer van Hallo IP-adressen toestaan.
>
>    * __NSG__: toestaan __inkomende__ verkeer op poort __443__ van Hallo __Internet__.
>    * __UDR__: Set Hallo __volgende Hop__ Hallo route too__Internet__ type.

Zie voor een voorbeeld van het gebruik van Azure PowerShell of hello Azure CLI toocreate nsg's Hallo [HDInsight uitbreiden met Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md#hdinsight-nsg) document.

## <a name="create-hello-hdinsight-cluster"></a>Hallo HDInsight-cluster maken

> [!WARNING]
> Hallo aangepaste DNS-server moet u configureren voordat u HDInsight in het virtuele netwerk Hallo installeert.

Gebruik Hallo stappen voor het Hallo [maken van een HDInsight-cluster met behulp van Azure-portal Hallo](./hdinsight-hadoop-create-linux-clusters-portal.md) document toocreate een HDInsight-cluster.

> [!WARNING]
> * Tijdens het maken, moet u Hallo locatie waarin het virtuele netwerk.
>
> * In Hallo __geavanceerde instellingen__ deel van de configuratie, moet u Hallo virtueel netwerk en subnet dat u eerder hebt gemaakt.

## <a name="connecting-toohdinsight"></a>Verbinding maken met tooHDInsight

De meeste documentatie op HDInsight wordt ervan uitgegaan dat u toegang toohello cluster via Hallo internet. Bijvoorbeeld, kunt u de cluster toohello op https://CLUSTERNAME.azurehdinsight.net koppelen. Dit adres Hallo openbare-gateway niet beschikbaar is als u nsg's hebt gebruikt of udr's toorestrict toegang vanaf internet Hallo gebruikt.

toodirectly tooHDInsight via Hallo virtueel netwerk verbinding maken, gebruikt u Hallo stappen te volgen:

1. toodiscover hello interne FQDN-namen van de clusterknooppunten Hallo HDInsight, een van de volgende methoden hello gebruiken:

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

2. toodetermine hello poort die een service is beschikbaar op, Zie Hallo [poorten die worden gebruikt door de services van Hadoop op HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.

    > [!IMPORTANT]
    > Sommige services die worden gehost op Hallo hoofdknooppunten zijn alleen actief is op één knooppunt tegelijk. Als u probeert toegang tot een service op één hoofdknooppunt en dit mislukt, overschakelen toohello andere hoofdknooppunt.
    >
    > Bijvoorbeeld, is Ambari alleen actief op één hoofdknooppunt tegelijk. Als u probeert toegang tot Ambari op één hoofdknooppunt en een 404-fout, retourneert en vervolgens deze wordt uitgevoerd op Hallo andere hoofdknooppunt.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over het gebruik van HDInsight in een virtueel netwerk [HDInsight uitbreiden met behulp van Azure Virtual Networks](./hdinsight-extend-hadoop-virtual-network.md).

* Zie voor meer informatie over virtuele netwerken van Azure Hallo [Azure Virtual Network-overzicht](../virtual-network/virtual-networks-overview.md).

* Zie voor meer informatie over netwerkbeveiligingsgroepen [Netwerkbeveiligingsgroepen](../virtual-network/virtual-networks-nsg.md).

* Zie voor meer informatie over de gebruiker gedefinieerde routes, [gebruiker gedefinieerde routes en doorsturen via IP](../virtual-network/virtual-networks-udr-overview.md).
