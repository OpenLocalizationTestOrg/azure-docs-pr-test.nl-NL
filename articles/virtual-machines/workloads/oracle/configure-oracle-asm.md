---
title: aaaSet van Oracle ASM op een virtuele machine van Azure Linux | Microsoft Docs
description: Snel gebruiksklaar Oracle ASM omhoog in uw Azure-omgeving.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a>Oracle ASM instellen op een virtuele machine van Azure Linux  

Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving. Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie in combinatie met het Hallo-installatie en configuratie van Oracle geautomatiseerde Storage Management (ASM).  Procedures voor:

> [!div class="checklist"]
> * Maken en koppelen tooan VM voor Oracle-Database
> * Installeren en configureren van Oracle automatische opslagbeheer
> * Installeren en configureren van Oracle raster infrastructuur
> * De installatie van een Oracle-ASM initialiseren
> * Een beheerd door ASM Oracle-database maken


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="prepare-hello-environment"></a>Hallo-omgeving voorbereiden

### <a name="create-a-resource-group"></a>Een resourcegroep maken

een resourcegroep toocreate gebruiken Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container in welke Azure resources worden geïmplementeerd en beheerd. In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* regio.

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a>Een virtuele machine maken

toocreate een virtuele machine op basis van de installatiekopie van de Oracle-Database Hallo en toouse Oracle ASM configureert, voert u Hallo [az vm maken](/cli/azure/vm#create) opdracht. 

Hallo wordt volgende voorbeeld een virtuele machine met de naam myVM een groot Standard_DS2_v2 met vier bijgesloten gegevensschijven van 50 GB. Als deze niet al bestaan op Hallo van sleutel standaardlocatie, maakt het ook SSH-sleutels.  toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

Nadat u Hallo VM maakt, geeft Azure CLI informatie vergelijkbare toohello voorbeeld te volgen. Houd er rekening mee Hallo-waarde voor `publicIpAddress`. U gebruikt dit adres tooaccess Hallo VM.

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a>Verbinding maken met toohello VM

toocreate een SSH-sessie met Hallo VM en extra instellingen configureren, gebruikt u Hallo opdracht te volgen. Hallo IP-adres vervangen door Hallo `publicIpAddress` waarde voor uw virtuele machine.

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a>Oracle ASM installeren

tooinstall Oracle ASM, volledige Hallo stappen te volgen. 

Zie voor meer informatie over het installeren van Oracle ASM [Oracle ASMLib Downloads voor Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).  

1. U moet toologin als hoofdgebruiker in volgorde toocontinue ASM-installatie:

   ```bash
   sudo su -
   ```
   
2. Deze aanvullende opdrachten tooinstall Oracle ASM onderdelen uitvoeren:

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. Controleer of de Oracle-ASM is geïnstalleerd:

   ```bash
   rpm -qa |grep oracleasm
   ```

    Hallo-uitvoer van deze opdracht moet lijst Hallo volgende onderdelen:

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. ASM vereist specifieke gebruikers en rollen in volgorde toofunction correct. Hallo opdrachten na maken Hallo vereiste gebruikersaccounts en groepen: 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. Controleer of de gebruikers en groepen correct zijn gemaakt:

   ```bash
   id grid
   ```

    Hallo uitvoer van deze opdracht moet lijst Hallo volgende gebruikers en groepen:

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. Maak een map voor de gebruiker *raster* en Hallo eigenaar wijzigen:

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a>Oracle ASM instellen

Voor deze zelfstudie Hallo standaardgebruiker is *raster* en Hallo standaardgroep is *asmadmin*. Zorg ervoor dat Hallo *oracle* gebruiker maakt deel uit van Hallo asmadmin groep. tooset van uw Oracle ASM-installatie voltooid Hallo stappen te volgen:

1. Het instellen van Hallo Oracle ASM bibliotheek stuurprogramma Hallo standaardgebruiker (raster) en de standaardgroep (asmadmin) definiëren evenals Hallo station toostart configureren bij het opstarten is (Kies y) en tooscan voor schijven bij het opstarten (Kies y). U moet tooanswer Hallo prompts van Hallo volgende opdracht:

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   Hallo-uitvoer van deze opdracht moet eruitzien vergelijkbare toohello te volgen, te stoppen met prompts toobe beantwoord.

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. Weergaveconfiguratie Hallo schijf:
   ```bash
   cat /proc/partitions
   ```

   Hallo-uitvoer van deze opdracht ziet er vergelijkbare toohello volgen in de lijst met beschikbare schijven

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. Schijf formatteren */dev/sdc* Hallo door de volgende opdracht en het beantwoorden van Hallo prompts met:
   - *n*voor nieuwe partitie
   - *p* voor primaire partitie
   - *1* tooselect Hallo eerste partitie
   - Druk op `enter` voor Hallo standaard eerste cilinder
   - Druk op `enter` voor Hallo standaard laatste cilinder
   - Druk op *w* toowrite Hallo wijzigingen toohello-partitietabel  

   ```bash
   fdisk /dev/sdc
   ```
   
   Met de bovenstaande Hallo-antwoorden, moet Hallo uitvoer voor Hallo fdisk opdracht eruitzien als Hallo volgende:

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. Herhalingen Hallo voorafgaand aan de opdracht fdisk voor `/dev/sdd`, `/dev/sde`, en `/dev/sdf`.

5. Controleer de schijfconfiguratie Hallo:

   ```bash
   cat /proc/partitions
   ```

   Hallo-uitvoer van Hallo-opdracht moet eruitzien als Hallo volgende:

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. Controleer de servicestatus voor Oracle ASM Hallo Hallo Oracle ASM-service en starten:

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   Hallo-uitvoer van Hallo-opdracht moet eruitzien als Hallo volgende:
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. Oracle ASM schijven maken:

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   Hallo-uitvoer van Hallo-opdracht moet eruitzien als Hallo volgende:

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. Lijst met Oracle ASM schijven:

   ```bash
   service oracleasm listdisks
   ```   

   Hallo-uitvoer van Hallo-opdracht moet lijst uitschakelen Hallo Oracle ASM schijven te volgen:

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. Hallo wachtwoorden wijzigen voor de basis-, oracle en raster gebruikers Hallo. **Noteer deze nieuwe wachtwoorden** als u deze later tijdens het Hallo-installatie gebruikt.

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. Hallo map machtiging wijzigen:

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a>Download en Oracle raster infrastructuur voorbereiden

toodownload en bereid Hallo Oracle raster software voor de infrastructuur voltooid Hallo stappen te volgen:

1. Oracle raster infrastructuur downloaden van Hallo [Oracle ASM-downloadpagina](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html). 

   Klik onder Hallo-download met de titel **Oracle-Database 12c versie 1 raster infrastructuur (12.1.0.2.0) voor Linux x86-64**, Hallo twee ZIP-bestanden downloaden.

2. Nadat u Hallo ZIP-bestanden tooyour-clientcomputer hebt gedownload, kunt u beveiligde kopie Protocol (SCP) toocopy Hallo bestanden tooyour VM:

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. SSH in uw Oracle-virtuele machine in Azure in volgorde toomove Hallo ZIP-bestanden in Hallo back-map te kiezen. Wijzig Hallo-eigenaar van het Hallo-bestanden:

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. Hallo bestanden uitpakken. (Installatie Hallo Linux pak hulpprogramma als deze nog niet is geïnstalleerd.)
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. De machtiging wijzigen:
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. Update geconfigureerd wisselruimte. Oracle raster onderdelen moeten ten minste 6,8 GB wisselen ruimte tooinstall raster. Hallo standaard wisselbestand voor Oracle Linux afbeeldingen in Azure is alleen 2048MB. U moet tooincrease `ResourceDisk.SwapSizeMB` in Hallo `/etc/waagent.conf` bestands- en Hallo WALinuxAgent service opnieuw starten om Hallo bijgewerkt instellingen tootake effect. Omdat het een alleen-lezen bestand, moet u tooenable schrijftoegang voor toochange bestand machtigingen.

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   Zoeken naar `ResourceDisk.SwapSizeMB` en Hallo waarde te wijzigen**8192**. U moet toopress `insert` tooenter invoegmodus, typt u de waarde Hallo van **8192** en druk vervolgens op `esc` tooreturn toocommand modus. toowrite hello wijzigingen en afsluiten Hallo-bestand, typ `:wq` en druk op `enter`.
   
   > [!NOTE]
   > We raden dat u altijd gebruiken `WALinuxAgent` tooconfigure wisselruimte zodat deze altijd op Hallo lokale kortstondige schijf (tijdelijke schijf) voor de beste prestaties gemaakt. Zie voor meer informatie over [hoe tooadd een wisseling in Linux Azure virtuele machines bestand](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a>Voorbereiden van uw lokale client en de VM toorun x11
Oracle ASM configureert, dient een grafische interface toocomplete Hallo installatie en configuratie. We gebruiken Hallo x11 protocol toofacilitate deze installatie. Als u een clientsysteem (Mac of Linux) dat al X11 is mogelijkheden ingeschakeld en geconfigureerd - kunt u deze configuratie overslaan en exclusieve tooWindows machines in te stellen. 

1. [Download PuTTY](http://www.putty.org/) en [downloaden Xming](https://xming.en.softonic.com/) tooyour Windows-computer. U moet toocomplete Hallo installatie van beide toepassingen met de Hallo standaardwaarden voordat u doorgaat.

2. Nadat u PuTTY hebt geïnstalleerd, open een opdrachtprompt, wijzigen in Hallo PuTTY map (bijvoorbeeld C:\Program Files\PuTTY) en voer `puttygen.exe` in volgorde toogenerate een sleutel.

3. In de PuTTY codegenerator:
   
   1. Een sleutel te genereren door het selecteren van Hallo `Generate` knop.
   2. Kopieer de inhoud Hallo van Hallo-sleutel (Ctrl + C).
   3. Selecteer Hallo `Save private key` knop.
   4. Hallo-waarschuwing over het beveiligen van sleutel met een wachtwoordzin Hallo negeren en selecteer vervolgens `OK`.

   ![Schermopname van PuTTY codegenerator](./media/oracle-asm/puttykeygen.png)

4. In de virtuele machine, moet u deze opdrachten uitvoeren:

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. Maak een bestand met de naam `authorized_keys`. Hallo-inhoud van Hallo key plakken in dit bestand en sla Hallo-bestand.

   > [!NOTE]
   > Hallo-sleutel moet Hallo tekenreeks bevatten `ssh-rsa`. Hallo-inhoud van Hallo-sleutel moet ook een enkele regel tekst.
   >  

6. Start op uw clientsysteem PuTTY. In Hallo **categorie** deelvenster te gaan**verbinding** > **SSH** > **Auth**. In Hallo **persoonlijke sleutelbestand voor verificatie** vak, blader toohello-sleutel die u eerder hebt gegenereerd.

   ![Schermafbeelding van de opties voor Hallo SSH-verificatie](./media/oracle-asm/setprivatekey.png)

7. In Hallo **categorie** deelvenster te gaan**verbinding** > **SSH** > **X11**. Selecteer Hallo **inschakelen X11 doorsturen** selectievakje.

   ![Schermopname van Hallo SSH X11 opties doorsturen](./media/oracle-asm/enablex11.png)

8. In Hallo **categorie** deelvenster te gaan**sessie**. Voer uw Oracle ASM VM `<publicIPaddress>` in Hallo host naam in het dialoogvenster vult u een nieuwe `Saved Session` name op en klik vervolgens op `Save`.  Wanneer opgeslagen, klik op `open` tooconnect tooyour Oracle ASM virtuele machine.  Hallo eerste keer dat u verbinding maakt u een waarschuwing Hallo externe systeem is niet in de cache opgeslagen in het register. Klik op `yes` tooadd deze en door te gaan.

   ![Schermopname van Hallo PuTTY-sessie-opties](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a>Oracle raster infrastructuur installeren

tooinstall Oracle raster infrastructuur, volledige Hallo stappen te volgen:

1. Meld u aan als **raster**. (U moet kunnen toosign in zonder te worden gevraagd om een wachtwoord.) 

   > [!NOTE]
   > Als u Windows uitvoert, zorg er dan voor dat u hebt Xming voordat u begint met Hallo installatie gestart.

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   Oracle raster infrastructuur 12c versie 1 installatieprogramma wordt geopend. (Het kan enkele minuten duren voordat Hallo installer toostart.)

2. Op Hallo **installatieoptie selecteren** pagina **installeren en configureren van Oracle raster infrastructuur voor een zelfstandige Server**.

   ![Schermafbeelding van pagina met Hallo-installatieprogramma installatieoptie selecteren](./media/oracle-asm/install01.png)

3. Op Hallo **Product talen selecteren** pagina, controleert u **Engels** of Hallo taal die u wilt dat is geselecteerd.  Klik op `next`.

4. Op Hallo **ASM schijfgroep maken** pagina:
   - Voer een naam voor de schijfgroep Hallo.
   - Onder **redundantie**, selecteer **externe**.
   - Onder **clustergrootte**, selecteer **4**.
   - Onder **schijven toevoegen**, selecteer **ORCLASMSP**.
   - Klik op `next`.

5. Op Hallo **ASM wachtwoord opgeven** pagina, selecteer Hallo **dezelfde wachtwoorden gebruiken voor deze accounts** optie en voer een wachtwoord.

   ![Schermafbeelding van pagina met Hallo-installatieprogramma ASM wachtwoord opgeven](./media/oracle-asm/install04.png)

6. Op Hallo **beheeropties opgeven** pagina, hebt u Hallo optie tooconfigure EM Cloud-besturingselement. Deze optie wordt overgeslagen: klik `next` toocontinue. 

7. Op Hallo **bevoorrechte besturingssysteem** pagina, Hallo standaardinstellingen gebruiken. Klik op `next` toocontinue.

8. Op Hallo **installatielocatie opgeven** pagina, Hallo standaardinstellingen gebruiken. Klik op `next` toocontinue.

9. Op Hallo **inventaris maken** pagina, Hallo inventaris Directory ook wijzigen`/u01/app/grid/oraInventory`. Klik op `next` toocontinue.

   ![Schermafbeelding van pagina met Hallo-installatieprogramma inventaris maken](./media/oracle-asm/install08.png)

10. Op Hallo **hoofdmap script uitvoering configuratie** pagina, selecteer Hallo **automatisch uitgevoerd configuratiescripts** selectievakje. Selecteer Hallo **'root' gebruikersreferenties gebruiken** optie en geef Hallo hoofdmap gebruikerswachtwoord.

    ![Schermafbeelding van pagina met Hallo-installatieprogramma hoofdmap script uitvoering configuratie](./media/oracle-asm/install09.png)

11. Op Hallo **vereiste controles uitvoeren** pagina Hallo huidige mislukt de installatie met fouten. Dit is verwacht gedrag. Selecteer `Fix & Check Again`.

12. In Hallo **reparatie Script** in het dialoogvenster, klikt u op `OK`.

13. Op Hallo **samenvatting** pagina, Controleer de geselecteerde instellingen en klik vervolgens op `Install`.

    ![Schermafbeelding van overzichtspagina Hallo-installatieprogramma](./media/oracle-asm/install12.png)

14. Een waarschuwingsdialoogvenster verschijnt de melding u configuratiescripts moet toobe uitgevoerd als een bevoegde gebruiker. Klik op `Yes` toocontinue.

15. Op Hallo **voltooien** pagina, klikt u op `Close` toofinish Hallo-installatie.

## <a name="set-up-your-oracle-asm-installation"></a>Instellen van de Oracle-ASM-installatie

tooset van uw Oracle ASM-installatie voltooid Hallo stappen te volgen:

1. Zorg ervoor dat u nog steeds bent aangemeld als **raster**, van uw X11 sessie. Mogelijk moet u toohit `enter` toorevive Hallo terminal. Start vervolgens Hallo Oracle geautomatiseerde Storage Management Configuration-assistent:

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   Oracle ASM configuratie-assistent wordt geopend.

2. In Hallo **ASM configureren: schijfgroepen** dialoogvenster vak, klikt u op Hallo `Create` knop en klik vervolgens op `Show Advanced Options`.

3. In Hallo **schijfgroep maken** in het dialoogvenster:

   - Voer Hallo schijf groepsnaam **gegevens**.
   - Onder **lidschijven selecteren**, selecteer **ORCL_DATA** en **ORCL_DATA1**.
   - Onder **clustergrootte**, selecteer **4**.
   - Klik op `ok` toocreate Hallo schijfgroep.
   - Klik op `ok` tooclose Hallo bevestigingsvenster.

   ![Schermopname van dialoogvenster Hallo-schijfgroep maken](./media/oracle-asm/asm02.png)

4. In Hallo **ASM configureren: schijfgroepen** dialoogvenster vak, klikt u op Hallo `Create` knop en klik vervolgens op `Show Advanced Options`.

5. In Hallo **schijfgroep maken** in het dialoogvenster:

   - Voer Hallo schijf groepsnaam **FRA**.
   - Onder **redundantie**, selecteer **External (geen)**.
   - Onder **lidschijven selecteren**, selecteer **ORCL_FRA**.
   - Onder **clustergrootte**, selecteer **4**.
   - Klik op `ok` toocreate Hallo schijfgroep.
   - Klik op `ok` tooclose Hallo bevestigingsvenster.

   ![Schermopname van dialoogvenster Hallo-schijfgroep maken](./media/oracle-asm/asm04.png)

6. Selecteer **afsluiten** tooclose configuratie-assistent ASM.

   ![Schermopname van Hallo ASM configureren: schijfgroepen-dialoogvenster met de knop Afsluiten](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a>Hallo-database maken

Hallo software voor Oracle-database is al geïnstalleerd op de hello Azure Marketplace-installatiekopie. toocreate een database, volledige Hallo stappen te volgen:

1. Schakelen gebruikers toohello Oracle supergebruiker en vervolgens initialiseren Hallo-listener voor logboekregistratie:

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   Configuratie-assistent database wordt geopend.

2. Op Hallo **databasebewerking** pagina, klikt u op `Create Database`.

3. Op Hallo **aanmaakmodus** pagina:

   - Voer een naam voor de Hallo-database.
   - Voor **opslagtype**, zorg ervoor dat **automatische Storage Management (ASM)** is geselecteerd.
   - Voor **bestanden databaselocatie**, standaard-Hallo ASM voorgestelde locatie.
   - Voor **snel herstel gebied**, standaard-Hallo ASM voorgestelde locatie.
   - Typ in een **beheerderswachtwoord** en **wachtwoord bevestigen**.
   - Zorg ervoor dat `create as container database` is geselecteerd.
   - Typ in een `pluggable database name` waarde.

4. Op Hallo **samenvatting** pagina, Controleer de geselecteerde instellingen en klik vervolgens op `Finish` toocreate Hallo-database.

   ![Schermafbeelding van overzichtspagina Hallo](./media/oracle-asm/createdb03.png)

5. Hallo Database is gemaakt. Op Hallo **voltooien** pagina, hebt u Hallo optie toounlock extra accounts toouse deze database en Hallo wachtwoorden wijzigen. Als u toodo doet wenst, selecteer **wachtwoordbeheer** -anders klikt u op `close`.

## <a name="delete-hello-vm"></a>Hallo VM verwijderen

U hebt Oracle automatisch beheer van opslag geconfigureerd op de installatiekopie van Oracle DB Hallo van hello Azure Marketplace.  Wanneer u deze virtuele machine niet meer nodig hebt, kunt u na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources hello gebruiken:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

[Zelfstudie: Oracle DataGuard configureren](configure-oracle-dataguard.md)

[Zelfstudie: Oracle GoldenGate configureren](Configure-oracle-golden-gate.md)

Bekijk [bouwen van een Oracle DB](oracle-design.md)
