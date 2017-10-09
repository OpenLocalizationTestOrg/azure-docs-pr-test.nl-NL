---
title: aaaRun OpenFOAM HPC Pack op de virtuele Linux-machines | Microsoft Docs
description: Een Microsoft HPC Pack cluster in Azure implementeren en uitvoeren van een taak OpenFOAM op meerdere rekenknooppunten van Linux via een netwerk RDMA.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a>OpenFoam uitvoeren met Microsoft HPC Pack op een Linux RDMA-cluster in Azure
Dit artikel ziet u een eenrichtingssessie toorun OpenFoam in virtuele machines in Azure. Hier kunt u een cluster met Microsoft HPC Pack met Linux-rekenknooppunten in Azure en voer implementeert een [OpenFoam](http://openfoam.com/) taak met de Intel MPI. Kunt u RDMA-compatibele Azure Virtual machines Hallo rekenknooppunten, zodat Hallo rekenknooppunten hello Azure RDMA netwerk communiceert. Andere opties toorun OpenFoam in Azure omvatten volledig geconfigureerd commerciële installatiekopieën beschikbaar zijn in Hallo Marketplace, zoals de UberCloud [OpenFoam 2.3 op CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), en door te voeren op [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/). 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

OpenFOAM (voor veld bewerking openen en bewerken) is een open source computational fluid dynamics (CFD)-softwarepakket dat algemeen wordt gebruikt in de technische en wetenschappelijke in commerciële en academic organisaties. Dit omvat de hulpprogramma's voor meshing, met name snappyHexMesh, een parallelized mesher voor complexe CAD-geometrie en voor vóór en na verwerking. Bijna alle processen parallel uitgevoerd, waardoor gebruikers tootake volledig gebruikmaken van de hardware van de computer beschikken.  

Microsoft HPC Pack functies toorun biedt grootschalige HPC en parallelle toepassingen, waaronder MPI-toepassingen op clusters van Microsoft Azure virtuele machines. HPC Pack ondersteunt ook actief Linux HPC-toepassingen op Linux VM's geïmplementeerd in een cluster HPC Pack rekenknooppunt. Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor een inleiding toousing Linux rekenknooppunten HPC Pack.

> [!NOTE]
> Dit artikel wordt beschreven hoe een Linux MPI-werkbelasting met HPC Pack toorun. Wordt ervan uitgegaan dat u enigszins bekend bent met Linux Systeembeheer en MPI belastingen uitgevoerd op Linux-clusters hebben. Als u versies van MPI en OpenFOAM verschilt Hallo voorbeelden in dit artikel gebruikt, wellicht u toomodify een aantal stappen installatie en configuratie. 
> 
> 

## <a name="prerequisites"></a>Vereisten
* **HPC Pack cluster met RDMA-compatibele Linux-rekenknooppunten** : een cluster HPC Pack met een grootte A8, A9, H16r, implementeren of H16rm Linux-rekenknooppunten met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) of een [Azure PowerShell-script](hpcpack-cluster-powershell-script.md). Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor Hallo vereisten en stappen voor beide opties. Als u ervoor Hallo Implementatieoptie PowerShell-script kiest, ziet u Hallo voorbeeldconfiguratiebestand in Hallo voorbeeldbestanden aan Hallo einde van dit artikel. Gebruik deze configuratie een op Azure gebaseerde toodeploy HPC Pack cluster die bestaan uit een grootte A8 Windows Server 2012 R2-hoofdknooppunt en 2 grootte A8 SUSE Linux Enterprise Server 12 rekenknooppunten. Vervang de juiste waarden voor uw abonnement en de service namen. 
  
  **Extra zaken tooknow**
  
  * Zie voor Linux RDMA netwerken vereisten in Azure, [hoge prestaties compute-VM-grootten](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  * Als u Hallo Implementatieoptie Powershell-script gebruikt, moet u alle Hallo Linux-rekenknooppunten in een cloud service toouse hello RDMA-netwerkverbinding implementeren.
  * Na implementatie Hallo Linux-knooppunten, verbinding maken via SSH tooperform eventuele extra beheertaken. Hallo SSH Verbindingsdetails voor elke Linux-VM niet vinden in hello Azure-portal.  
* **Intel MPI** -toorun OpenFOAM op SLES 12 HPC rekenknooppunten in Azure, moet u tooinstall Hallo Intel MPI-bibliotheek 5 runtime vanuit Hallo [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/). (Intel MPI 5 is voorgeïnstalleerd op op basis van CentOS HPC-installatiekopieën.)  Installeer Intel MPI op uw Linux-rekenknooppunten in een latere stap, indien nodig. tooprepare voor deze stap nadat u hebt geregistreerd met Intel, volg Hallo koppeling op Hallo bevestiging e toohello gerelateerde webpagina. Vervolgens kopiëren Hallo downloadkoppeling voor Hallo .tgz bestand voor de juiste versie van Intel MPI Hallo. In dit artikel is gebaseerd op Intel MPI versie 5.0.3.048.
* **OpenFOAM bron Pack** -Hallo OpenFOAM bron Pack software voor Linux downloaden van Hallo [OpenFOAM Foundation-site](http://openfoam.org/download/2-3-1-source/). In dit artikel is gebaseerd op de bron-packversie 2.3.1-specificaties gedownload als OpenFOAM 2.3.1.tgz. Volg de instructies Hallo verderop in dit artikel toounpack en OpenFOAM compileren op Hallo Linux-rekenknooppunten.
* **EnSight** (optioneel) - toosee Hallo resultaten van uw simulatie OpenFOAM downloaden en installeren van Hallo [EnSight](https://www.ceisoftware.com/download/) visualisatie en analyse-programma. Licentie-en downloaden op Hallo EnSight site zijn.

## <a name="set-up-mutual-trust-between-compute-nodes"></a>Wederzijdse vertrouwensrelatie tussen de rekenknooppunten instellen
Een taak cross-knooppunt wordt uitgevoerd op meerdere Linux-knooppunten vereist Hallo knooppunten tootrust elkaar (door **rsh** of **ssh**). Wanneer u Hallo HPC Pack cluster met Microsoft HPC Pack IaaS-implementatiescript hello maakt, Hallo script permanente wederzijds vertrouwen voor Hallo beheerdersaccount dat u opgeeft automatisch ingesteld. Voor gebruikers die geen beheerder u in Hallo clusterdomein maakt, hebt u tooset een tijdelijke wederzijdse vertrouwensrelatie tussen knooppunten Hallo wanneer een taak toothem is toegewezen en Hallo relatie vernietigen wanneer Hallo is voltooid. tooestablish vertrouwen voor elke gebruiker een RSA-sleutelpaar toohello cluster HPC Pack gebruikt voor de vertrouwensrelatie Hallo bieden.

### <a name="generate-an-rsa-key-pair"></a>Een RSA-sleutelpaar niet genereren
Is het eenvoudig toogenerate een RSA-sleutelpaar, die een openbare sleutel en een persoonlijke sleutel bevat, door te voeren Hallo Linux **ssh-keygen** opdracht.

1. Meld u aan tooa Linux-computer.
2. Hallo volgende opdracht uitvoeren:
   
   ```
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
1. Maken van een extern bureaublad verbinding tooyour hoofdknooppunt met uw beheerdersaccount HPC Pack (Hallo administrator-account u instellen wanneer u het implementatiescript Hallo uitgevoerd).
2. Gebruik standaard Windows Server procedures toocreate een domeingebruikersaccount in Active Directory-domein Hallo-cluster. Bijvoorbeeld Hallo Active Directory-gebruikers en Computers hulpprogramma gebruiken op Hallo hoofdknooppunt. Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u een domeingebruiker die met de naam hpclab\hpcuser maken.
3. Maak een bestand met de naam C:\cred.xml en kopieer Hallo RSA belangrijke gegevens in de App. Er is een voorbeeldbestand cred.xml op Hallo einde van dit artikel.
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. Open een opdrachtprompt en Voer Hallo opdracht tooset Hallo-gegevens voor Hallo hpclab\hpcuser account referenties te volgen. Gebruik van Hallo **extendeddata** parameter toopass Hallo naam van C:\cred.xml u hebt gemaakt voor Hallo belangrijke gegevens.
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   Deze opdracht is voltooid zonder uitvoer. Na het instellen van referenties voor gebruikersaccounts Hallo moet u taken toorun Hallo Hallo cred.xml bestand opslaan op een veilige locatie of verwijder deze.
5. Als u Hallo RSA-sleutelpaar gegenereerd op een van uw Linux-knooppunten, moet u toodelete Hallo sleutels als u klaar bent met het gebruik ervan. HPC Pack vindt een bestaande id_rsa bestand of id_rsa.pub-bestand, dan wordt deze wederzijds vertrouwen niet ingesteld.

> [!IMPORTANT]
> Wordt niet aanbevolen als de Clusterbeheerder van een een Linux-taak wordt uitgevoerd op een gedeelde cluster, omdat een taak die is verzonden door een beheerder wordt uitgevoerd onder het hoofdaccount Hallo op Hallo Linux-knooppunten. Een taak die is verzonden door een gebruiker die geen beheerder wordt echter uitgevoerd onder een lokale Linux-gebruikersaccount met dezelfde naam als Hallo taak gebruiker Hallo. In dit geval stelt HPC Pack wederzijds vertrouwen voor deze gebruiker Linux op Hallo knooppunten toohello taak toegewezen. U kunt Hallo Linux gebruiker handmatig op de Linux-knooppunten Hallo instellen voordat u Hallo batchverwerking of HPC Pack Hallo gebruiker automatisch gemaakt wanneer Hallo job wordt verzonden. Als HPC Pack Hallo gebruiker maakt, verwijderd HPC Pack nadat het Hallo-taak is voltooid. Hallo sleutels tooreduce beveiligingsrisico's, HPC Pack verwijdert na Taakvoltooiing van de.
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a>Instellen van een bestandsshare voor Linux-knooppunten
Nu een standaard SMB-share op een map op het hoofdknooppunt Hallo ingesteld. tooallow hello Linux knooppunten tooaccess toepassingsbestanden met een algemeen pad, koppelpunt Hallo gedeelde map op Hallo Linux-knooppunten. Als u wilt, kunt u een andere optie, zoals een Azure-bestanden share - aanbevolen voor veel scenario's- of een NFS-share voor bestandsdeling. Zie Hallo-bestand delen van informatie en gedetailleerde stappen in [aan de slag met Linux-rekenknooppunten in een HPC Pack-Cluster in Azure](hpcpack-cluster.md).

1. Maak een map op het hoofdknooppunt Hallo en tooEveryone delen door het instellen van machtigingen voor lezen/schrijven. Bijvoorbeeld C:\OpenFOAM delen op Hallo hoofdknooppunt als \\ \\SUSE12RDMA HN\OpenFOAM. Hier *SUSE12RDMA HN* Hallo-hostnaam van Hallo hoofdknooppunt.
2. Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten uit:
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

de eerste opdracht Hallo maakt een map met de naam /openfoam op alle knooppunten in Hallo LinuxNodes groep. de tweede opdracht Hallo koppelt Hallo gedeelde map //SUSE12RDMA-HN/OpenFOAM op Hallo Linux-knooppunten met dir_mode en file_mode bits set too777. Hallo *gebruikersnaam* en *wachtwoord* Hallo opdracht moet Hallo referenties van een gebruiker op Hallo hoofdknooppunt.

> [!NOTE]
> Hallo '\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell. "\`, 'betekent Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.
> 
> 

## <a name="install-mpi-and-openfoam"></a>MPI en OpenFOAM installeren
toorun OpenFOAM als een MPI-taak op Hallo RDMA netwerk, moet u toocompile OpenFOAM met Hallo Intel MPI-bibliotheken. 

Voer eerst enkele **clusrun** tooinstall Intel MPI-bibliotheken (indien nog niet is geïnstalleerd) en OpenFOAM opdrachten op uw Linux-knooppunten. Gebruik Hallo hoofdknooppunt share geconfigureerde eerder tooshare Hallo installatiebestanden tussen Hallo Linux-knooppunten.

> [!IMPORTANT]
> Deze installatie en gecompileerd stappen zijn voorbeelden. Moet u enige kennis van Linux-systeem beheer tooensure afhankelijke compilers en bibliotheken correct zijn geïnstalleerd. Mogelijk moet u toomodify bepaalde omgevingsvariabelen of andere instellingen voor uw versie van Intel MPI en OpenFOAM. Zie voor meer informatie [Intel MPI-bibliotheek voor Linux-installatiehandleiding](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) en [OpenFOAM bron Pack installatie](http://openfoam.org/download/2-3-1-source/) voor uw omgeving.
> 
> 

### <a name="install-intel-mpi"></a>Intel MPI installeren
Hallo gedownloade installatiepakket voor Intel MPI (l_mpi_p_5.0.3.048.tgz in dit voorbeeld) in C:\OpenFoam opslaan op Hallo hoofdknooppunt zodat Hallo Linux-knooppunten toegang dit bestand uit /openfoam tot. Voer **clusrun** tooinstall Intel MPI-bibliotheek op alle Hallo Linux-knooppunten.

1. Hallo hieronder kopiëren Hallo installatiepakket voor de opdrachten en pakt te/opt/intel op elk knooppunt.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. tooinstall Intel MPI-bibliotheek achtergrond, een silent.cfg-bestand gebruiken. U kunt een voorbeeld vinden in Hallo voorbeeldbestanden aan Hallo einde van dit artikel. Plaats dit bestand in Hallo gedeelde map /openfoam. Zie voor meer informatie over Hallo silent.cfg bestand [Intel MPI-bibliotheek voor de installatiehandleiding voor Linux - installatie op de achtergrond](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).
   
   > [!TIP]
   > Zorg ervoor dat u uw silent.cfg bestand opslaan als een tekstbestand met Linux regeleinden heb (alleen LF, niet CR LF). Deze stap zorgt ervoor dat deze goed op Hallo Linux-knooppunten.
   > 
   > 
3. Intel MPI-bibliotheek in stille modus installeren.
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a>MPI configureren
Voor het testen, moet u de volgende regels toohello /etc/security/limits.conf op elke Linux-knooppunten Hallo Hallo toevoegen:

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


Hallo Linux-knooppunten starten nadat u Hallo limits.conf bestand bijwerken. Bijvoorbeeld, gebruikt u Hallo volgende **clusrun** opdracht:

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

Start opnieuw op en zorg ervoor dat die gedeelde map Hallo als /openfoam is gekoppeld.

### <a name="compile-and-install-openfoam"></a>Compileren en OpenFOAM installeren
Opslaan op het hoofdknooppunt Hallo Hallo gedownloade installatiepakket voor Hallo tooC:\OpenFoam OpenFOAM bron Pack (OpenFOAM-2.3.1.tgz in dit voorbeeld) zodat Hallo Linux-knooppunten toegang dit bestand uit /openfoam tot. Voer **clusrun** opdrachten toocompile OpenFOAM op alle Hallo Linux-knooppunten.

1. Maak een map /opt/OpenFOAM op elk knooppunt Linux, kopie Hallo pakket toothis bronmap, en pak deze.
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. toocompile OpenFOAM Hello Intel MPI-bibliotheek, Stel eerst enkele omgevingsvariabelen voor Intel MPI- en OpenFOAM. Een bash-script aangeroepen settings.sh tooset Hallo variabelen gebruiken. U kunt een voorbeeld vinden in Hallo voorbeeldbestanden aan Hallo einde van dit artikel. Plaats dit bestand (opgeslagen met regeleinden Linux) in Hallo gedeelde map /openfoam. Dit bestand bevat ook de instellingen voor Hallo MPI en OpenFOAM runtimes hoger toorun een taak OpenFOAM te gebruiken.
3. Afhankelijke pakketten nodig toocompile OpenFOAM installeren. Afhankelijk van uw Linux-distributie moet u mogelijk eerst tooadd een opslagplaats. Voer **clusrun** vergelijkbare toohello volgende opdrachten:
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    Indien nodig, opdrachten SSH tooeach Linux knooppunt toorun hello tooconfirm die ze naar behoren uitgevoerd.
4. Hallo na de opdracht toocompile OpenFOAM worden uitgevoerd. Hallo compilatie proces neemt enige tijd toocomplete en genereert een grote hoeveelheid logboekuitvoer informatie toostandard, gebruikt u dus Hallo **/ interleaved** toodisplay Hallo uitvoer interleaved optie.
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > Hallo '\`' symbool in Hallo-opdracht is een escapeteken voor PowerShell. "\`&" betekent Hallo "&" deel uitmaakt van het Hallo-opdracht.
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a>Een taak OpenFOAM voor toorun voorbereiden
Nu get gereed toorun een MPI-taak aangeroepen sloshingTank3D, namelijk een Hallo OpenFoam steekproeven van op twee Linux-knooppunten. 

### <a name="set-up-hello-runtime-environment"></a>Hallo-runtime-omgeving instellen
tooset hello runtime-omgevingen voor MPI en OpenFOAM op Hallo Linux-knooppunten, uitvoeren van de volgende opdracht in een Windows PowerShell-venster op het hoofdknooppunt Hallo Hallo. (Deze opdracht is alleen geldig voor SUSE Linux.)

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a>Voorbeeldgegevens voorbereiden
Gebruik Hallo hoofdknooppunt share u eerder hebt geconfigureerd tooshare bestanden tussen Hallo Linux-knooppunten (gekoppeld als /openfoam).

1. SSH-tooone van uw Linux-rekenknooppunten.
2. Hallo na de opdracht tooset hello OpenFOAM runtime-omgeving worden uitgevoerd als u dit nog niet hebt gedaan.
   
   ```
   $ source /openfoam/settings.sh
   ```
3. Hallo sloshingTank3D voorbeeld toohello gedeelde mappen kopiëren en navigeer tooit.
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. Wanneer u de standaardparameters Hallo van dit voorbeeld gebruikt, kan duren tien minuten toorun, zodat u toomodify kunt sommige parameters toomake het sneller worden uitgevoerd. Een eenvoudige keuze is toomodify Hallo tijd stap variabelen deltaT en writeInterval in Hallo system/controlDict-bestand. Dit bestand wordt alle ingevoerde gegevens betreffende toohello besturingselement van het tijd- en lezen en schrijven van oplossingsgegevens. U kan bijvoorbeeld Hallo-waarde van deltaT van 0,05 too0.5 en Hallo-waarde van writeInterval van 0,05 too0.5 wijzigen.
   
   ![Wijzig de variabelen in stap][step_variables]
5. Gewenste waarden voor Hallo variabelen in Hallo system/decomposeParDict bestand opgeven. In dit voorbeeld worden twee Linux knooppunten, elk met 8 kernen, dus Stel numberOfSubdomains too16 en n van hierarchicalCoeffs too(1 1 16), wat betekent dat OpenFOAM parallel met 16 processen worden uitgevoerd. Zie voor meer informatie [OpenFOAM User Guide: 3,4 uitgevoerd toepassingen parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).
   
   ![Processen afbreken][decompose]
6. Hallo volgende opdrachten uit Hallo sloshingTank3D directory tooprepare Hallo voorbeeldgegevens worden uitgevoerd.
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. Op het hoofdknooppunt hello ziet u bestanden met voorbeeldgegevens Hallo worden gekopieerd naar C:\OpenFoam\sloshingTank3D. (C:\OpenFoam is Hallo gedeelde map op het hoofdknooppunt Hallo.)
   
   ![Gegevensbestanden op Hallo hoofdknooppunt][data_files]

### <a name="host-file-for-mpirun"></a>Hostbestand voor mpirun
In deze stap maakt u een hostbestand (een lijst van rekenknooppunten) welke Hallo **mpirun** opdracht gebruikt.

1. Op een van de Linux-knooppunten hello, door een bestand met de naam hostfile onder /openfoam, zodat dit bestand kan worden bereikt op /openfoam/hostfile op alle knooppunten van Linux te maken.
2. Schrijf uw Linux-knooppuntnamen in dit bestand. In dit voorbeeld bevat Hallo bestand Hallo namen te volgen:
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > U kunt ook dit bestand maken op C:\OpenFoam\hostfile op Hallo hoofdknooppunt. Als u deze optie kiest, opslaan als een tekstbestand met Linux regeleinden (alleen LF, niet CR LF). Dit zorgt ervoor dat deze wordt uitgevoerd naar behoren op Hallo Linux-knooppunten.
   > 
   > 
   
   **Wrapper voor Bash-scripts**
   
   Als u veel Linux-knooppunten hebt en u wilt dat uw taak toorun op slechts een deel ervan, kan niet een goed idee toouse-bestand een vaste host, omdat u niet weet welke knooppunten tooyour taak worden toegewezen. In dit geval een bash script wrapper voor schrijven **mpirun** toocreate Hallo hostbestand automatisch. U kunt een voorbeeld bash script wrapper aangeroepen hpcimpirun.sh aan Hallo einde van dit artikel vinden en opslaan als /openfoam/hpcimpirun.sh. Dit voorbeeldscript Hallo te volgen:
   
   1. Stelt de omgevingsvariabelen Hallo voor **mpirun**, en sommige toevoeging opdracht parameters toorun Hallo MPI-taak via Hallo RDMA-netwerk. In dit geval stelt het Hallo variabelen te volgen:
      
      * I_MPI_FABRICS shm:dapl =
      * I_MPI_DAPL_PROVIDER weergeeft van een-v2-ib0 =
      * I_MPI_DYNAMIC_CONNECTION = 0
   2. Maakt een hostbestand toohello op basis van de variabele $ omgeving CCP_NODES_CORES die is ingesteld door Hallo HPC-hoofdknooppunt wanneer Hallo-taak wordt geactiveerd.
      
      Hallo-indeling van $CCP_NODES_CORES volgt dit patroon:
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      waar
      
      * `<Number of nodes>`-het aantal knooppunten Hallo toothis taak toegewezen.  
      * `<Name of node_n_...>`-Hallo-naam van elk knooppunt toegewezen toothis taak.
      * `<Cores of node_n_...>`-het aantal kernen op Hallo knooppunt toegewezen toothis taak Hallo.
      
      Bijvoorbeeld, als Hallo-taak twee knooppunten toorun moet, is $CCP_NODES_CORES vergelijkbaar met
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. Aanroepen Hallo **mpirun** opdracht en voegt u twee parameters toohello vanaf de opdrachtregel.
      
      * `--hostfile <hostfilepath>: <hostfilepath>`-Hallo pad van Hallo host bestand Hallo script wordt gemaakt
      * `-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-een omgevingsvariabele ingesteld door Hallo HPC Pack hoofdknooppunt, die het aantal totale kernen Hallo opslaat toothis taak toegewezen. In dit geval geeft Hallo processen voor het aantal **mpirun**.

## <a name="submit-an-openfoam-job"></a>Verzenden van een taak OpenFOAM
U kunt nu een taak in HPC Cluster Manager verzenden. U moet toopass Hallo script hpcimpirun.sh in Hallo opdrachtregels voor een aantal taken Hallo.

1. Verbinding maken met hoofdknooppunt tooyour-cluster en start HPC Cluster Manager.
2. **In de Resource Management**, moet u ervoor zorgen dat Hallo Linux-rekenknooppunten hello **Online** status. Als dat niet het geval is, selecteert u deze en klikt u op **Online brengen**.
3. In **Jobbeheer**, klikt u op **nieuwe taak**.
4. Voer een naam voor de taak zoals *sloshingTank3D*.
   
   ![Taakdetails][job_details]
5. In **taak resources**, kies het type resource als 'Knooppunt' Hallo en Hallo Minimum too2 ingesteld. Deze configuratie Hallo-taak op twee Linux-knooppunten, elk met acht kernen in dit voorbeeld heeft wordt uitgevoerd.
   
   ![Taak resources][job_resources]
6. Klik op **taken bewerken** in Hallo navigatiebalk aan de linkerkant en klik vervolgens op **toevoegen** tooadd een taak toohello taak. Vier taken toohello taak met de Hallo toevoegen na de opdracht regels en instellingen.
   
   > [!NOTE]
   > Met `source /openfoam/settings.sh` stelt Hallo OpenFOAM en MPI-runtime-omgevingen, zodat elk van de taken te volgen Hallo voordat Hallo OpenFOAM opdracht aangeroepen.
   > 
   > 
   
   * **Taak 1**. Voer **decomposePar** toogenerate gegevensbestanden worden opgeslagen voor het werken met **interDyMFoam** parallel.
     
     * Een knooppunt toohello taak toewijzen
     * **Vanaf de opdrachtregel** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`
     * **Werkmap** -/ openfoam/sloshingTank3D
     
     Zie Hallo volgende afbeelding. U configureren de resterende taken Hallo op dezelfde manier.
     
     ![Taak 1-details][task_details1]
   * **Taak 2**. Voer **interDyMFoam** in parallelle toocompute Hallo voorbeeld.
     
     * Twee knooppunten toohello taak toewijzen
     * **Vanaf de opdrachtregel** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`
     * **Werkmap** -/ openfoam/sloshingTank3D
   * **Taak 3**. Voer **reconstructPar** toomerge Hallo wordt ingesteld met mappen van de tijd van elke map processor_N_ in één verzameling.
     
     * Een knooppunt toohello taak toewijzen
     * **Vanaf de opdrachtregel** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`
     * **Werkmap** -/ openfoam/sloshingTank3D
   * **Taak 4**. Voer **foamToEnsight** in parallelle tooconvert hello OpenFOAM resultaat bestanden naar EnSight formatteren en Hallo EnSight bestanden in een map met de naam Ensight in case directory Hallo plaatsen.
     
     * Twee knooppunten toohello taak toewijzen
     * **Vanaf de opdrachtregel** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`
     * **Werkmap** -/ openfoam/sloshingTank3D
7. Afhankelijkheden toothese taken in oplopende taakvolgorde toevoegen.
   
   ![Taakafhankelijkheden][task_dependencies]
8. Klik op **indienen** toorun deze taak.
   
   Standaard verzendt HPC Pack Hallo taak als uw huidige aangemelde gebruikersaccount. Nadat u op **indienen**, ziet u mogelijk een dialoogvenster waarin u tooenter Hallo-gebruikersnaam en wachtwoord wordt gevraagd.
   
   ![Taak referenties][creds]
   
   Onder bepaalde omstandigheden onthoudt HPC Pack Hallo gebruikersgegevens u invoer voordat en dit dialoogvenster niet weergeven. toomake HPC Pack opnieuw weergeven, voer de volgende opdracht achter de opdrachtprompt Hallo en vervolgens dient Hallo-taak.
   
   ```
   hpccred delcreds
   ```
9. Hallo taak neemt van tien minuten tooseveral uur volgens toohello parameters die u hebt ingesteld voor het Hallo-voorbeeld. U ziet in heatmap hello, Hallo-taak uitgevoerd op Hallo Linux-knooppunten. 
   
   ![Heatmap][heat_map]
   
   Op elk knooppunt worden acht processen gestart.
   
   ![Linux-processen][linux_processes]
10. Wanneer het Hallo-taak is voltooid, kunt u de Hallo taak resultaten vinden in mappen onder C:\OpenFoam\sloshingTank3D en Hallo-logboekbestanden op C:\OpenFoam.

## <a name="view-results-in-ensight"></a>De resultaten weergeven in EnSight
Optioneel gebruik [EnSight](https://www.ceisoftware.com/) toovisualize en analyseer de resultaten Hallo van Hallo OpenFOAM taak. Zie voor meer informatie over visualisatie en animatie in EnSight, [video handleiding](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).

1. Nadat u op het hoofdknooppunt Hallo EnSight hebt geïnstalleerd, start u deze.
2. Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.
   
   U ziet een vervangen in Hallo-viewer.
   
   ![Vervangen in EnSight][tank]
3. Maak een **Isosurface** van **internalMesh**, en kies vervolgens Hallo variabele **alpha_water**.
   
   ![Een isosurface maken][isosurface]
4. Hallo voor kleur instellen **Isosurface_part** in de vorige stap Hallo gemaakt. Zo ingesteld dat deze toowater blauw.
   
   ![Isosurface kleur bewerken][isosurface_color]
5. Maak een **Iso-volume** van **wanden** door te selecteren **wanden** in Hallo **delen** paneel en klik op Hallo **Isosurfaces**  knop op Hallo-werkbalk.
6. Selecteer in het dialoogvenster Hallo **Type** als **Isovolume** en stel Hallo Min van **Isovolume bereik** too0.5. toocreate isovolume hello, klikt u op **maken met de geselecteerde onderdelen**.
7. Hallo voor kleur instellen **Iso_volume_part** in de vorige stap Hallo gemaakt. Zo ingesteld dat deze toodeep water blauw.
8. Hallo voor kleur instellen **wanden**. Zo ingesteld dat deze tootransparent wit.
9. Klik nu op **afspelen** toosee Hallo resultaten van Hallo simulatie.
   
    ![Resultaat van de vervangen][tank_result]

## <a name="sample-files"></a>Voorbeeldbestanden
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a>Voorbeeld XML-configuratiebestand voor implementatie van het cluster door PowerShell-script
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a>Voorbeeld silent.cfg bestand tooinstall MPI
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a>Voorbeeldscript settings.sh
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a>Voorbeeldscript hpcimpirun.sh
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
