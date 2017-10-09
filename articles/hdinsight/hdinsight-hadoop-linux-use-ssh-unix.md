---
title: aaaUse SSH met Hadoop - Azure HDInsight | Microsoft Docs
description: U kunt HDInsight openen met Secure Shell (SSH). Dit document bevat informatie over verbinding maken met tooHDInsight met Hallo ssh en scp opdrachten van Windows, Linux, Unix- of Mac OS-clients.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: hadoop-opdrachten in linux,hadoop linux-opdrachten,hadoop-macro's,ssh hadoop,ssh hadoop-cluster
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>TooHDInsight (Hadoop) via SSH verbinding

Meer informatie over hoe toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely tooHadoop in Azure HDInsight verbinden. 

HDInsight kunt Linux (Ubuntu) gebruiken als besturingssysteem Hallo voor knooppunten binnen Hallo Hadoop-cluster. Hallo bevat volgende tabel Hallo-adres en poort informatie die nodig zijn om verbinding te maken op basis van tooLinux HDInsight met behulp van een SSH-client:

| Adres | Poort | Maakt verbinding met... |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Edge-knooppunt (R Server op HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Edge-knooppunt (ieder ander clustertype, als er een Edge-knooppunt bestaat) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Primaire hoofdknooppunt |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Secundaire hoofdknooppunt |

> [!NOTE]
> Vervang `<edgenodename>` met de naam Hallo van Hallo edge-knooppunt.
>
> Vervang `<clustername>` met Hallo-naam van het cluster.
>
> Als uw cluster een edge-knooppunt bevat, raden we u __altijd verbinding maken met het edge-knooppunt toohello__ via SSH. de hoofdknooppunten Hallo hosten services die de status kritiek toohello van Hadoop. Hallo edge-knooppunt kan worden uitgevoerd alleen wat put erop.
>
> Zie [Edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node) voor meer informatie over het gebruik van Edge-knooppunten.

## <a name="ssh-clients"></a>SSH-clients

Linux-, Unix-en Mac OS bieden Hallo `ssh` en `scp` opdrachten. Hallo `ssh` -client is vaak gebruikte toocreate een externe opdrachtregelprogramma sessie met een Linux of Unix-systeem. Hallo `scp` client bestanden van de gebruikte toosecurely kopiëren tussen de client en Hallo externe systeem is.

Microsoft Windows beschikt standaard niet over een SSH-client. Hallo `ssh` en `scp` clients zijn beschikbaar voor Windows via hello-pakketten te volgen:

* [Azure Cloud-Shell](../cloud-shell/quickstart.md): Hallo Cloud Shell biedt een Bash-omgeving in uw browser en biedt Hallo `ssh`, `scp`, en andere algemene Linux-opdrachten.

* [Bash op Ubuntu op Windows 10](https://msdn.microsoft.com/commandline/wsl/about): Hallo `ssh` en `scp` opdrachten zijn beschikbaar via Hallo Bash op Windows-opdrachtregel.

* [GIT (https://git-scm.com/)](https://git-scm.com/): Hallo `ssh` en `scp` opdrachten zijn beschikbaar via Hallo GitBash vanaf de opdrachtregel.

* [GitHub bureaublad (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` en `scp` opdrachten zijn beschikbaar via Hallo GitHub Shell-opdrachtregel. GitHub bureaublad kan geconfigureerde toouse Bash, Hallo Windows-opdrachtprompt of PowerShell zijn als de opdrachtregel Hallo voor Hallo Git-Shell.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): Hallo PowerShell team is overdragen OpenSSH tooWindows en biedt test releases.

    > [!WARNING]
    > Hallo OpenSSH-pakket bevat Hallo SSH-serveronderdeel `sshd`. Dit onderdeel wordt gestart van een SSH-server op uw systeem, zodat anderen tooconnect tooit. Dit onderdeel configureren of open poort 22, tenzij u een SSH-server toohost op uw systeem wilt geen. Het is niet vereist toocommunicate met HDInsight.

Er zijn ook verschillende grafische SSH-clients, zoals [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) en [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Deze clients kunnen gebruikte tooconnect tooHDInsight zijn, Hallo proces van het verbinden van is anders dan met behulp van Hallo `ssh` hulpprogramma. Zie de documentatie van de Hallo van Hallo grafische client die u gebruikt voor meer informatie.

## <a id="sshkey"></a>Verificatie: SSH-sleutels

SSH sleutels gebruiken [cryptografie met openbare sleutels](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate SSH-sessies. SSH-sleutels zijn veiliger dan wachtwoorden, en bieden een eenvoudige manier toosecure toegang tooyour Hadoop-cluster.

Als uw SSH-account is beveiligd met een sleutel, moet Hallo client Hallo overeenkomende persoonlijke sleutel wanneer u verbinding maakt opgeven:

* De meeste clients kunnen worden geconfigureerd toouse een __standaardsleutel__. Bijvoorbeeld, Hallo `ssh` client zoekt naar een persoonlijke sleutel op `~/.ssh/id_rsa` op Linux en Unix-omgevingen.

* U kunt opgeven dat Hallo __pad tooa persoonlijke sleutel__. Hello `ssh` client, Hallo `-i` parameter gebruikte toospecify Hallo pad tooprivate sleutel is. Bijvoorbeeld `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Als u __meerdere privésleutels__ gebruikt voor verschillende servers, kunt u overwegen om een hulpprogramma zoals [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent) te gebruiken. Hallo `ssh-agent` hulpprogramma gebruikte tooautomatically Selecteer Hallo sleutel toouse kan zijn bij het maken van een SSH-sessie.

> [!IMPORTANT]
>
> Als u uw persoonlijke sleutel met een wachtwoordzin beveiligt, moet u Hallo wachtwoordzin opgeven als u Hallo-sleutel. Hulpprogramma's zoals `ssh-agent` Hallo wachtwoord voor uw gemak in cache.

### <a name="create-an-ssh-key-pair"></a>Een SSH-sleutelpaar maken

Gebruik Hallo `ssh-keygen` toocreate openbare en persoonlijke sleutelbestanden opdracht. Hallo volgende opdracht genereert een 2048-bits RSA-sleutelpaar die kan worden gebruikt met HDInsight:

    ssh-keygen -t rsa -b 2048

U wordt gevraagd naar informatie tijdens het Hallo sleutel maken. Bijvoorbeeld, waarbij Hallo sleutels worden opgeslagen of toouse een wachtwoordzin. Nadat het Hallo-proces is voltooid, worden twee bestanden gemaakt. een openbare sleutel en een persoonlijke sleutel.

* Hallo __openbare sleutel__ gebruikte toocreate is een HDInsight-cluster. Hallo openbare sleutel heeft een extensie van `.pub`.

* Hallo __privésleutel__ gebruikte tooauthenticate uw client toohello HDInsight-cluster is.

> [!IMPORTANT]
> U kunt uw sleutels beveiligen met een wachtwoordzin. Dit is in feite een wachtwoord voor uw privésleutel. Zelfs als iemand anders uw persoonlijke sleutel krijgt, moeten ze Hallo wachtwoordzin toouse Hallo sleutel hebben.

### <a name="create-hdinsight-using-hello-public-key"></a>HDInsight met behulp van de openbare sleutel Hallo maken

| Methode voor het maken | Hoe toouse Hallo openbare sleutel |
| ------- | ------- |
| **Azure Portal** | Schakel het selectievakje __gebruik hetzelfde wachtwoord als cluster aanmelding__, en selecteer vervolgens __openbare sleutel__ zoals Hallo type van de SSH-verificatie. Ten slotte Hallo-bestand met openbare sleutel selecteren of de tekstinhoud Hallo van Hallo bestand plak in Hallo __openbare SSH-sleutel__ veld.</br>![Dialoogvenster voor de openbare SSH-sleutel tijdens het maken van een HDInsight-cluster](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Gebruik Hallo `-SshPublicKey` parameter Hallo `New-AzureRmHdinsightCluster` cmdlet en pass Hallo-inhoud van de openbare sleutel als tekenreeks Hallo.|
| **Azure CLI 1.0** | Gebruik Hallo `--sshPublicKey` parameter Hallo `azure hdinsight cluster create` opdracht en de inhoud van de openbare sleutel Hallo Hallo doorgeven als een tekenreeks. |
| **Resource Manager-sjabloon** | Zie [HDInsight op Linux implementeren met een SSH-sleutel](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/) voor een voorbeeld van het gebruik van SSH-sleutels met een sjabloon. Hallo `publicKeys` -element in Hallo [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) bestand gebruikte toopass Hallo sleutels tooAzure is bij het maken van Hallo-cluster. |

## <a id="sshpassword"></a>Verificatie: wachtwoord

SSH-accounts kunnen worden beveiligd met een wachtwoord. Wanneer u verbinding met behulp van SSH tooHDInsight maakt, bent u vraag tooenter Hallo wachtwoord.

> [!WARNING]
> Het wordt niet aangeraden om wachtwoordverificatie te gebruiken voor SSH. Wachtwoorden kunnen worden geraden en zijn kwetsbaar toobrute force-aanvallen. In plaats daarvan wordt aangeraden om [SSH-sleutels te gebruiken voor verificatie](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>HDInsight maken met een wachtwoord

| Methode voor het maken | Hoe toospecify Hallo wachtwoord |
| --------------- | ---------------- |
| **Azure Portal** | Hallo SSH gebruikersaccount heeft standaard Hallo hetzelfde wachtwoord als aanmeldingsaccount Hallo-cluster. Schakel het selectievakje toouse een ander wachtwoord __gebruik hetzelfde wachtwoord als cluster aanmelding__, en Voer Hallo wachtwoord in Hallo __SSH-wachtwoord__ veld.</br>![Dialoogvenster voor het SSH-wachtwoord tijdens het maken van een HDInsight-cluster](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Gebruik Hallo `--SshCredential` parameter Hallo `New-AzureRmHdinsightCluster` cmdlet en geef een `PSCredential` object met Hallo SSH-gebruikersnaam voor account en wachtwoord. |
| **Azure CLI 1.0** | Gebruik Hallo `--sshPassword` parameter Hallo `azure hdinsight cluster create` opdracht in en geef Hallo wachtwoordwaarde. |
| **Resource Manager-sjabloon** | Zie [HDInsight op Linux implementeren met een SSH-wachtwoord](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/) voor een voorbeeld van het gebruik met een wachtwoord met een sjabloon. Hallo `linuxOperatingSystemProfile` -element in Hallo [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) bestand gebruikte toopass Hallo SSH-account en wachtwoord tooAzure is bij het maken van Hallo-cluster.|

### <a name="change-hello-ssh-password"></a>Hallo SSH-wachtwoord wijzigen

Zie voor informatie over het wijzigen van wachtwoord voor gebruikersaccount Hallo SSH Hallo __wachtwoorden wijzigen__ sectie Hallo [HDInsight beheren](hdinsight-administer-use-portal-linux.md#change-passwords) document.

## <a id="domainjoined"></a>Verificatie: HDInsight, gekoppeld aan een domein

Als u een __HDInsight-cluster domein__, moet u Hallo `kinit` opdracht nadat u verbinding met SSH hebt. Deze opdracht wordt u gevraagd een domeingebruiker en het wachtwoord en verifieert de sessie met hello Azure Active Directory-domein is gekoppeld aan het Hallo-cluster.

Zie [Aan een domein gekoppelde HDInsight-clusters configureren](hdinsight-domain-joined-configure.md) voor meer informatie.

## <a name="connect-toonodes"></a>Verbinding maken met toonodes

Hallo hoofdknooppunten en edge-knooppunt (indien aanwezig) toegankelijk is via Hallo internet op poort 22 en 23.

* Wanneer u verbinding maakt toohello __hoofdknooppunten__, gebruik van poort __22__ tooconnect toohello primaire head knooppunt en poort __23__ tooconnect toohello secundair hoofdknooppunt. Hallo FQDN-naam toouse is `clustername-ssh.azurehdinsight.net`, waarbij `clustername` Hallo-naam van uw cluster.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Wanneer connectiung toohello __edge-knooppunt__, poort 22 gebruikt. Hallo volledig gekwalificeerde domeinnaam is `edgenodename.clustername-ssh.azurehdinsight.net`, waarbij `edgenodename` maakt een naam die u hebt opgegeven als Hallo edge-knooppunt. `clustername`Hallo-naam van Hallo-cluster is.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> Hallo eerdere voorbeelden wordt ervan uitgegaan dat u wachtwoordverificatie gebruikt of dat certificaatverificatie automatisch die zich kunnen voordoen wordt. Als u een SSH-sleutelpaar voor verificatie gebruiken en Hallo certificaat niet automatisch gebruikt, gebruikt u Hallo `-i` parameter toospecify Hallo persoonlijke sleutel. Bijvoorbeeld `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Eenmaal zijn verbonden, verandert Hallo prompt tooindicate Hallo SSH gebruiker naam Hallo knooppunt en die u met verbonden bent. Bijvoorbeeld, wanneer verbonden toohello primaire hoofdknooppunt als `sshuser`, Hallo prompt is `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Verbinding maken met tooworker en Zookeeper-knooppunten

Hallo worker-knooppunten en Zookeeper-knooppunten zijn niet rechtstreeks toegankelijk zijn vanaf internet Hallo. Ze toegankelijk zijn vanuit head clusterknooppunten Hallo of edge-knooppunten. Hallo volgen Hallo algemene stappen tooconnect tooother knooppunten:

1. Gebruik SSH tooconnect tooa head of edge-knooppunt:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Gebruik van SSH-verbinding toohello head Hallo of edge-knooppunt, Hallo `ssh` opdracht tooconnect tooa werkrolknooppunt in Hallo-cluster:

        ssh sshuser@wn0-myhdi

    een lijst van domeinnamen op Hallo van Hallo-knooppunten in cluster Hallo tooretrieve Zie Hallo [HDInsight beheren met behulp van de Ambari REST-API Hallo](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) document.

Als Hallo SSH-account is beveiligd met een __wachtwoord__, Hallo wachtwoord invoeren om verbinding te maken.

Als Hallo SSH-account is beveiligd met __SSH-sleutels__, zorg ervoor dat de SSH-doorsturen is ingeschakeld op Hallo-client.

> [!NOTE]
> Een andere manier toodirectly toegang tot alle knooppunten in cluster Hallo is tooinstall HDInsight in een virtueel netwerk van Azure. Vervolgens kunt u deelnemen aan de externe computer toohello hetzelfde virtuele netwerk en rechtstreeks toegang tot alle knooppunten in cluster Hallo.
>
> Zie [Een virtueel netwerk gebruiken met HDInsight](hdinsight-extend-hadoop-virtual-network.md) voor meer informatie.

### <a name="configure-ssh-agent-forwarding"></a>Het doorsturen van SSH-agents configureren

> [!IMPORTANT]
> Hallo volgende stappen wordt ervan uitgegaan dat een Linux- of UNIX-systeem en werken met Bash op Windows 10. Als u deze stappen voor uw systeem niet werkt, moet u mogelijk tooconsult Hallo-documentatie voor de SSH-client.

1. Start een teksteditor en open `~/.ssh/config`. Als dit bestand niet bestaat, kunt u dit maken door `touch ~/.ssh/config` in te voeren op een opdrachtregel.

2. Hallo na tekst toohello toevoegen `config` bestand.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Vervang Hallo __Host__ informatie met Hallo-adres van Hallo knooppunt u toousing SSH verbinding maken. het vorige voorbeeld Hallo gebruikt Hallo edge-knooppunt. Deze vermelding configureert voor het opgegeven knooppunt Hallo doorsturen van SSH-agent.

3. Test doorsturen met behulp van de volgende opdracht uit Hallo terminal Hallo SSH-agent:

        echo "$SSH_AUTH_SOCK"

    Met deze opdracht retourneert informatie vergelijkbare toohello volgende tekst:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Als er niets wordt geretourneerd, wordt `ssh-agent` niet uitgevoerd. Zie voor meer informatie, Hallo agent scripts opstartgegevens op [met behulp van ssh-agent met ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) of Raadpleeg de documentatie bij de SSH-client.

4. Zodra u hebt gecontroleerd of **ssh-agent** is uitgevoerd, gebruik Hallo tooadd na uw persoonlijke sleutel toohello de SSH-agent:

        ssh-add ~/.ssh/id_rsa

    Als uw persoonlijke sleutel wordt opgeslagen in een ander bestand, vervangt `~/.ssh/id_rsa` met Hallo pad toohello bestand.

5. Verbinding maken met toohello cluster edge-knooppunt of hoofdknooppunten via SSH. Gebruik vervolgens Hallo SSH-opdracht tooconnect tooa worker of zookeeper-knooppunt. Hallo-verbinding is gemaakt met behulp van de sleutel Hallo doorgestuurd.

## <a name="copy-files"></a>Bestanden kopiëren

Hallo `scp` hulpprogramma kan worden gebruikt toocopy bestanden tooand uit afzonderlijke knooppunten in het Hallo-cluster. Bijvoorbeeld, Hallo opdracht kopieën Hallo na `test.txt` map uit Hallo lokaal systeem toohello primaire hoofdknooppunt:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Omdat u geen pad wordt opgegeven na Hallo `:`, Hallo-bestand wordt geplaatst in Hallo `sshuser` basismap.

Hallo na voorbeeld kopieën Hallo `test.txt` bestand van Hallo `sshuser` basismap op Hallo primaire hoofdknooppunt toohello lokaal systeem:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`alleen toegang tot bestandssysteem Hallo van afzonderlijke knooppunten binnen Hallo-cluster. Deze kan niet worden gebruikt tooaccess in Hallo HDFS-compatibele opslag voor Hallo-cluster.
>
> Gebruik `scp` wanneer u een resource tooupload moet voor gebruik van een SSH-sessie. Bijvoorbeeld, een pythonscript uploaden en vervolgens Hallo-script uitvoeren van een SSH-sessie.
>
> Zie voor informatie over de gegevens rechtstreeks in Hallo HDFS-compatibele opslag laden, Hallo documenten te volgen:
>
> * [HDInsight op basis van Azure Storage](hdinsight-hadoop-use-blob-storage.md).
>
> * [HDInsight op basis van Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).

## <a name="next-steps"></a>Volgende stappen

* [SSH-tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)
* [Een virtueel netwerk gebruiken met HDInsight](hdinsight-extend-hadoop-virtual-network.md)
* [Edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node)