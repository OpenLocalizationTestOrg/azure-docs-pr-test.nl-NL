---
title: aaaNAMD met Microsoft HPC Pack op de virtuele Linux-machines | Microsoft Docs
description: Een Microsoft HPC Pack cluster in Azure implementeren en uitvoeren van een simulatie NAMD met charmrun op meerdere rekenknooppunten voor Linux
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a>NAMD uitvoeren met Microsoft HPC Pack op Linux-rekenknooppunten in Azure
Dit artikel ziet u enkele toorun een werkbelasting Linux high performance computing (HPC) op virtuele machines in Azure. Hier kunt u instellen van een [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure met Linux-rekenknooppunten en voer een [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulatie toocalculate en visualiseren Hallo-structuur van een grote biomoleculaire-systeem.  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* **NAMD** (Nanoscale moleculaire Dynamics programma) is een parallelle moleculaire dynamics-pakket ontworpen voor high-performance simulatie van grote biomoleculaire systemen die up toomillions van atomen. Voorbeelden van deze systemen zijn virussen, cel structuren en grote eiwitten. NAMD schaalt toohundreds van kernen voor het typische simulaties en toomore dan 500.000 kernen voor het grootste simulaties Hallo.
* **Microsoft HPC Pack** functies toorun biedt grootschalige HPC en parallelle toepassingen in clusters van lokale computers of virtuele machines in Azure. Oorspronkelijk is ontwikkeld als een oplossing voor Windows HPC-workloads, HPC Pack nu ondersteunt Linux HPC-toepassingen uitvoert op Linux compute knooppunt virtuele machines in een cluster HPC Pack geïmplementeerd. Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor een inleiding.

Voor andere opties toorun Linux HPC werkbelastingen in Azure, Zie [technische bronnen voor batchverwerking en high performance computing](../../../batch/batch-hpc-solutions.md).

## <a name="prerequisites"></a>Vereisten
* **HPC Pack cluster met Linux-rekenknooppunten** -implementeren van een cluster met HPC Pack met Linux-rekenknooppunten in Azure met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) of een [Azure PowerShell-script](hpcpack-cluster-powershell-script.md). Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor Hallo vereisten en stappen voor beide opties. Als u ervoor Hallo Implementatieoptie PowerShell-script kiest, ziet u Hallo voorbeeldconfiguratiebestand in Hallo voorbeeldbestanden aan Hallo einde van dit artikel. Dit bestand configureert een HPC Pack op basis van een Azure-cluster die bestaan uit een Windows Server 2012 R2-hoofdknooppunt en vier grootte grote CentOS 6.6-rekenknooppunten. Dit bestand aanpassen nodig zijn voor uw omgeving.
* **De software en zelfstudie bestanden NAMD** -NAMD downloaden van software voor Linux van Hallo [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registratie vereist). In dit artikel is gebaseerd op NAMD versie 2.10 en maakt gebruik van Hallo [Linux-x86_64 (64-bits Intel/AMD met Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archief. Ook downloaden Hallo [NAMD zelfstudie bestanden](http://www.ks.uiuc.edu/Training/Tutorials/#namd). Hallo downloads tar-bestanden zijn en moet u een Windows-hulpprogramma tooextract Hallo bestanden op Hallo cluster hoofdknooppunt. tooextract hello bestanden, volg de instructies Hallo verderop in dit artikel. 
* **VMD** (optioneel) - toosee Hallo resultaten van de taak NAMD downloaden en installeren van Hallo moleculaire visualisatie programma [VMD](http://www.ks.uiuc.edu/Research/vmd/) op een computer van uw keuze. Er is een fout opgetreden in de huidige versie Hallo 1.9.2. Zie Hallo VMD downloaden site tooget gestart.  

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Wederzijdse vertrouwensrelatie tussen de rekenknooppunten instellen
Een taak cross-knooppunt wordt uitgevoerd op meerdere Linux-knooppunten vereist Hallo knooppunten tootrust elkaar (door **rsh** of **ssh**). Wanneer u Hallo HPC Pack cluster met Microsoft HPC Pack IaaS-implementatiescript hello maakt, Hallo script permanente wederzijds vertrouwen voor Hallo beheerdersaccount dat u opgeeft automatisch ingesteld. Voor gebruikers die geen beheerder u in Hallo clusterdomein maakt, hebt u tooset een tijdelijke wederzijdse vertrouwensrelatie tussen knooppunten Hallo wanneer een taak toothem is toegewezen. Vernietig vervolgens Hallo relatie wanneer Hallo voltooid is. toodo voor elke gebruiker zodoende een RSA-sleutelpaar toohello cluster welke HPC Pack tooestablish Hallo vertrouwensrelatie gebruikt. Instructies volgen.

### <a name="generate-an-rsa-key-pair"></a>Een RSA-sleutelpaar niet genereren
Is het eenvoudig toogenerate een RSA-sleutelpaar, die een openbare sleutel en een persoonlijke sleutel bevat, door te voeren Hallo Linux **ssh-keygen** opdracht.

1. Meld u aan tooa Linux-computer.
2. Hallo volgende opdracht uitvoeren:
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > Druk op **Enter** toouse Hallo standaardinstellingen totdat Hallo-opdracht is voltooid. Voer een wachtwoordzin hier; niet Wanneer u daarom wordt gevraagd om een wachtwoord op te geven, drukt u op **Enter**.
   > 
   > 
   
   ![Een RSA-sleutelpaar niet genereren][keygen]
3. Wijzig de directory toohello ~/.ssh directory. Hallo persoonlijke sleutel wordt opgeslagen in id_rsa en Hallo openbare sleutel in id_rsa.pub.
   
   ![Persoonlijke en openbare sleutel][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a>Hallo sleutelpaar toohello HPC Pack cluster toevoegen
1. [Verbinding maken met extern bureaublad](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello hoofdknooppunt VM gebruik Hallo domeinreferenties die u hebt opgegeven tijdens de implementatie Hallo-cluster (bijvoorbeeld hpc\clusteradmin). U beheren Hallo cluster vanaf het hoofdknooppunt Hallo.
2. Gebruik standaard Windows Server procedures toocreate een domeingebruikersaccount in Active Directory-domein Hallo-cluster. Bijvoorbeeld Hallo Active Directory-gebruikers en Computers hulpprogramma gebruiken op Hallo hoofdknooppunt. Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u een domeingebruiker die met de naam hpcuser in Hallo hpclab domein (hpclab\hpcuser) maken.
3. Hallo domein gebruiker toohello HPC Pack cluster toevoegen als een gebruiker van het cluster. Zie voor instructies [toevoegen of verwijderen cluster gebruikers](https://technet.microsoft.com/library/ff919330.aspx).
4. Maak een bestand met de naam C:\cred.xml en kopieer Hallo RSA belangrijke gegevens in de App. U kunt een voorbeeld vinden in Hallo voorbeeldbestanden aan Hallo einde van dit artikel.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. Open een opdrachtprompt en Voer Hallo opdracht tooset Hallo-gegevens voor Hallo hpclab\hpcuser account referenties te volgen. Gebruik van Hallo **extendeddata** parameter toopass Hallo naam van Hallo C:\cred.xml u hebt gemaakt voor Hallo belangrijke gegevens.
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Deze opdracht is voltooid zonder uitvoer. Na het instellen van referenties voor gebruikersaccounts Hallo moet u taken toorun Hallo Hallo cred.xml bestand opslaan op een veilige locatie of verwijder deze.
6. Als u Hallo RSA-sleutelpaar gegenereerd op een van uw Linux-knooppunten, moet u toodelete Hallo sleutels als u klaar bent met het gebruik ervan. HPC Pack stelt geen wederzijdse vertrouwensrelatie Als het een bestaand id_rsa bestand of id_rsa.pub bestand gevonden.

> [!IMPORTANT]
> Wordt niet aanbevolen als de Clusterbeheerder van een een Linux-taak wordt uitgevoerd op een gedeelde cluster, omdat een taak die is verzonden door een beheerder wordt uitgevoerd onder het hoofdaccount Hallo op Hallo Linux-knooppunten. Een taak die is verzonden door een gebruiker die geen beheerder wordt uitgevoerd onder een lokale Linux-gebruikersaccount met dezelfde naam als Hallo taak gebruiker Hallo. In dit geval stelt HPC Pack wederzijds vertrouwen voor deze gebruiker Linux op alle Hallo knooppunten toohello taak toegewezen. U kunt Hallo Linux gebruiker handmatig op de Linux-knooppunten Hallo instellen voordat u Hallo batchverwerking of HPC Pack Hallo gebruiker automatisch gemaakt wanneer Hallo job wordt verzonden. Als HPC Pack Hallo gebruiker maakt, verwijderd HPC Pack nadat het Hallo-taak is voltooid. tooreduce beveiligingsrisico, Hallo-codes worden verwijderd nadat het Hallo-taak is voltooid op Hallo knooppunten.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Instellen van een bestandsshare voor Linux-knooppunten
Nu instellen van een SMB-bestandsshare en Hallo gedeelde map op alle Linux-knooppunten tooallow Hallo Linux knooppunten tooaccess NAMD bestanden met een algemeen pad koppelen. Hieronder vindt u stappen toomount een gedeelde map op Hallo hoofdknooppunt. Een share wordt aanbevolen voor distributies zoals CentOS 6.6 die hello Azure File service momenteel niet ondersteund. Als uw Linux-knooppunten een Azure-bestandsshare ondersteunt, Zie [hoe toouse Azure File storage met Linux](../../../storage/files/storage-how-to-use-files-linux.md). Zie voor extra opties met HPC Pack delen van bestanden, [aan de slag met Linux-rekenknooppunten in een HPC Pack-Cluster in Azure](hpcpack-cluster.md).

1. Maak een map op het hoofdknooppunt Hallo en tooEveryone delen door het instellen van machtigingen voor lezen/schrijven. In dit voorbeeld \\ \\CentOS66HN\Namd heet Hallo Hallo map, waarbij CentOS66HN Hallo-hostnaam van Hallo hoofdknooppunt.
2. Maak een submap met de naam namd2 in Hallo gedeelde map. In namd2, maakt u een nieuwe submap met de naam namdsample.
3. Hallo NAMD bestanden in de map Hallo uitpakken met behulp van een Windows-versie van **tar** of een ander Windows-hulpprogramma dat met TAR-archieven werkt. 
   
   * Hallo NAMD tar-archief te extraheren\\\\CentOS66HN\Namd\namd2.
   * Pak de zelfstudie bestanden Hallo onder \\ \\CentOS66HN\Namd\namd2\namdsample.
4. Open een Windows PowerShell-venster en Voer Hallo opdrachten toomount Hallo gedeelde map op Hallo Linux-knooppunten te volgen.
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

de eerste opdracht Hallo maakt een map met de naam /namd2 op alle knooppunten in Hallo LinuxNodes groep. de tweede opdracht Hallo koppelt Hallo gedeelde map //CentOS66HN/Namd/namd2 op Hallo-map met dir_mode en file_mode bits set too777. Hallo *gebruikersnaam* en *wachtwoord* Hallo opdracht moet Hallo referenties van een gebruiker op Hallo hoofdknooppunt.

> [!NOTE]
> Hallo '\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell. "\`, 'betekent Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a>Een script Bash toorun NAMD taak maken
De taak NAMD moet een *nodelist* bestand voor **charmrun** toodetermine Hallo aantal knooppunten toouse bij het starten van NAMD processen. U gebruikt een Bash-script die wordt uitgevoerd en genereert Hallo knooppuntenbestand **charmrun** met deze knooppuntenbestand. Vervolgens dient u een taak NAMD in HPC Cluster Manager waarmee dit script wordt aangeroepen.

Met een teksteditor van uw keuze, een Bash-script maken in Hallo /namd2 map met de Hallo NAMD-programmabestanden en noem deze hpccharmrun.sh. Voor een snel testen van het concept kopiëren Hallo hpccharmrun.sh voorbeeldscript gegeven aan het einde van dit artikel Hallo en ga te[verzenden van een taak NAMD](#submit-a-namd-job).

> [!TIP]
> Sla het script als een tekstbestand met Linux regeleinden (alleen LF, niet CR LF). Dit zorgt ervoor dat deze wordt uitgevoerd naar behoren op Hallo Linux-knooppunten.
> 
> 

Hieronder vindt u meer informatie over de werking van dit bash-script. 

1. Sommige variabelen definiëren.
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. Knooppunt-informatie ophalen uit het Hallo-omgevingsvariabelen. $NODESCORES slaat een lijst met woorden van $CCP_NODES_CORES splitsen. $COUNT is Hallo grootte van $NODESCORES.
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   Hallo-indeling voor Hallo $CCP_NODES_CORES variabele is als volgt:
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   Deze variabele bevat Hallo totaal aantal knooppunten, knooppuntnamen en het aantal kernen op elk knooppunt dat toohello taak is toegewezen. Bijvoorbeeld als Hallo-taak 10 kernen toorun moet, lijkt Hallo-waarde van $CCP_NODES_CORES op:
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. Als Hallo $CCP_NODES_CORES variabele niet is ingesteld, start u **charmrun** rechtstreeks. (Dit moet alleen worden uitgevoerd als u dit script rechtstreeks op uw Linux-knooppunten uitvoert.)
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. Of maak een knooppuntenbestand voor **charmrun**.
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. Voer **charmrun** met knooppuntenbestand Hallo, krijgen de status van het resultaat, en verwijder knooppuntenbestand Hallo Hallo achter.
   
   ${CCP_NUMCPUS} is een andere omgevingsvariabele instellen door Hallo HPC Pack hoofdknooppunt. Hallo-nummer van de totale kernen toothis taak toegewezen worden opgeslagen. We gebruiken deze toospecify Hallo aantal processen voor charmrun.
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. Exit Hello **charmrun** status retourneren.
   
   ```
   exit ${RTNSTS}
   ```

Hieronder vindt u Hallo-informatie in de knooppuntenbestand hello, welke Hallo script genereert:

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

Bijvoorbeeld:

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a>Verzenden van een taak NAMD
U bent nu klaar toosubmit een taak NAMD in HPC Cluster Manager.

1. Verbinding maken met hoofdknooppunt tooyour-cluster en start HPC Cluster Manager.
2. In **bronbeheer**, moet u ervoor zorgen dat Hallo Linux-rekenknooppunten hello **Online** status. Als dat niet het geval is, selecteert u deze en klikt u op **Online brengen**.
3. In **Jobbeheer**, klikt u op **nieuwe taak**.
4. Voer een naam voor de taak zoals *hpccharmrun*.
   
   ![Nieuwe HPC-taak][namd_job]
5. Op Hallo **taakdetails** pagina onder **taak Resources**, selecteer Hallo type resource als **knooppunt** en set Hallo **Minimum** too3. , we Hallo taak uitvoeren op drie Linux-knooppunten en elk knooppunt vier kernen heeft.
   
   ![Taak resources][job_resources]
6. Klik op **taken bewerken** in Hallo navigatiebalk aan de linkerkant en klik vervolgens op **toevoegen** tooadd een taak toohello taak.    
7. Op Hallo **taakdetails en i/o-omleiding** pagina set Hallo volgende waarden:
   
   * **Opdrachtregel**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`
     
     > [!TIP]
     > Hallo is voorgaande opdrachtregel één opdracht zonder regeleinden. Loopt deze tooappear op meerdere regels onder **opdrachtregel**.
     > 
     > 
   * **Werkmap** -/namd2
   * **Minimale** - 3
     
     ![Taakdetails][task_details]
     
     > [!NOTE]
     > Hallo-werkmap hier ingestelde omdat **charmrun** toonavigate toohello probeert dezelfde werkmap op elk knooppunt. Als het Hallo-werkmap niet is ingesteld, begint HPC Pack Hallo-opdracht in een willekeurige naam map gemaakt op een Hallo Linux-knooppunten. Dit zorgt ervoor dat Hallo volgende fout op Hallo andere knooppunten: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid dit probleem op door een mappad die kan worden geopend door alle knooppunten als werkmap Hallo opgeven.
     > 
     > 
8. Klik op **OK** en klik vervolgens op **indienen** toorun deze taak.
   
   Standaard verzendt HPC Pack Hallo taak als uw huidige aangemelde gebruikersaccount. Een dialoogvenster vragen u tooenter Hallo-gebruikersnaam en wachtwoord nadat u op **indienen**.
   
   ![Taak referenties][creds]
   
   Onder bepaalde omstandigheden onthoudt HPC Pack Hallo gebruikersgegevens u invoer voordat en dit dialoogvenster niet weergeven. toomake HPC Pack opnieuw weergeven, voer de volgende opdracht achter de opdrachtprompt Hallo en vervolgens dient Hallo-taak.
   
   ```command
   hpccred delcreds
   ```
9. Hallo taak duurt enkele minuten toofinish.
10. Hallo taaklogboek op vinden \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log en Hallo uitvoerbestanden in \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.
11. Start VMD tooview eventueel de taak van de resultaten. Hallo-stappen voor het visualiseren van Hallo NAMD uitvoerbestanden (in dit geval een ubiquitin eiwit molecuul in een bol water) zijn buiten bereik Hallo van dit artikel. Zie [NAMD zelfstudie](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) voor meer informatie.
    
    ![Resultaten van de taak][vmd_view]

## <a name="sample-files"></a>Voorbeeldbestanden
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Voorbeeld XML-configuratiebestand voor implementatie van het cluster door PowerShell-script
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a>Voorbeeldbestand cred.xml
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```

### <a name="sample-hpccharmrunsh-script"></a>Voorbeeldscript hpccharmrun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
