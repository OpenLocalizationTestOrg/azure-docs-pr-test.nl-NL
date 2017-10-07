---
title: aaaUse SSH-sleutels met Windows voor virtuele Linux-machines | Microsoft Docs
description: Meer informatie over hoe toogenerate en het gebruik van SSH-sleutels op een Windows computer tooconnect tooa Linux virtuele machine in Azure.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Hoe tooUse SSH-sleutels met Windows in Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Als u verbinding tooLinux virtuele machines (VM's) in Azure, moet u [cryptografie met openbare sleutels](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide een veiliger manier toolog in tooyour Linux VM. Dit proces omvat een openbare en persoonlijke sleuteluitwisseling Hallo secure shell (SSH) opdracht tooauthenticate zelf gebruikt in plaats van een gebruikersnaam en wachtwoord. Wachtwoorden zijn kwetsbaar toobrute-force-aanvallen, vooral op Internet gerichte VMs zoals webservers. Dit artikel bevat een overzicht van SSH-sleutels en hoe toogenerate Hallo juiste sleutels op een Windows-computer.

## <a name="overview-of-ssh-and-keys"></a>Overzicht van SSH en sleutels
U kunt veilig tooyour Linux VM aanmelden met behulp van openbare en persoonlijke sleutels:

* Hallo **openbare sleutel** uw Linux-VM of een andere service die u wenst dat toouse met cryptografie met openbare sleutels is geplaatst.
* Hallo **persoonlijke sleutel** is wat u aanwezig tooyour Linux VM wanneer u zich aanmeldt, tooverify uw identiteit. Houd deze privésleutel geheim. Deel deze niet.

Deze openbare en persoonlijke sleutels kunnen worden gebruikt voor meerdere virtuele machines en services. U hoeft niet een sleutelpaar voor elke virtuele machine of service die u wenst dat tooaccess. Zie voor een gedetailleerd overzicht [cryptografie met openbare sleutels](https://wikipedia.org/wiki/Public-key_cryptography).

SSH is een versleutelde verbindingsprotocol waarmee beveiligde aanmeldingen via niet-beveiligde verbindingen. Is het Hallo standaardverbindingsprotocol voor virtuele Linux-machines gehost in Azure. Maar SSH zelf een versleutelde verbinding biedt, verlaat met wachtwoorden met SSH-verbindingen nog steeds Hallo VM kwetsbaar toobrute-force-aanvallen of te raden van wachtwoorden. Een veiliger en aanbevolen methode voor het maken van verbinding tooa VM via SSH is met behulp van deze openbare en persoonlijke sleutels, ook wel bekend als SSH-sleutels.

Als u niet dat toouse SSH-sleutels wenst, kunt u nog steeds aanmelden tooyour virtuele Linux-machines met een wachtwoord. Als uw virtuele machine niet blootgestelde toohello Internet, volstaan met wachtwoorden. Echter nog steeds toomanage uw wachtwoorden nodig voor elke Linux-VM en onderhouden in orde wachtwoordbeleid en -procedures, zoals minimale wachtwoordlengte en deze regelmatig bij te werken. Hallo-gebruik van SSH-sleutels vermindert Hallo complexiteit van het beheren van afzonderlijke referenties in meerdere virtuele machines.

## <a name="windows-packages-and-ssh-clients"></a>Windows-pakketten en SSH-clients
Verbinding van tooand Linux VM's beheren in Azure worden verkregen met een **SSH client**. Windows-computers hebben doorgaans geen een SSH-client is geïnstalleerd. Hallo Windows 10 Verjaardag Update toegevoegd Bash voor Windows en hello nieuwste Update van Windows 10 gebruikers biedt aanvullende updates. Deze Windows-subsysteem voor Linux kunt u toorun en toegang tot hulpprogramma's zoals een SSH-client systeemeigen binnen een Bash-shell. Voer vervolgens een van de Hallo Linux documenten, zoals [hoe toogenerate SSH-sleutel voor Linux-paren](mac-create-ssh-keys.md). Bash voor Windows, nog in ontwikkeling is en wordt beschouwd als een bètaversie. Zie voor meer informatie over Windows Bash [Bash op Ubuntu op Windows](https://msdn.microsoft.com/commandline/wsl/about).

Als u toouse iets anders dan voor Windows Bash wenst, algemene Windows SSH clients die kunt u installeren zijn opgenomen in hello-pakketten te volgen:

* [GIT voor Windows](https://git-for-windows.github.io/)
* [puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>Die belangrijke bestanden moet u toocreate?
Azure vereist ten minste 2048 bits **ssh-rsa** geformatteerd openbare en persoonlijke sleutels. Als u Azure-resources met Hallo klassieke implementatiemodel beheert, moet u ook een PEM toogenerate (`.pem` bestand).

Hier volgen Hallo implementatiescenario's en bestanden die u in elk gebruikt Hallo typen:

1. **SSH-rsa** sleutels zijn vereist voor de implementatie met behulp van Hallo [Azure-portal](https://portal.azure.com), en implementaties van Resource Manager met behulp van Hallo [Azure CLI](../../cli-install-nodejs.md).
   * Deze sleutels worden doorgaans alle de meeste mensen hebben.
2. Een `.pem` bestand is vereist toocreate virtuele machines met Hallo klassieke implementatie. Deze sleutels worden ondersteund in de klassieke implementaties wanneer Hallo [Azure-portal](https://portal.azure.com) of [Azure CLI](../../cli-install-nodejs.md).
   * U hoeft alleen toocreate deze aanvullende sleutels en certificaten als u de resources die zijn gemaakt met behulp van de klassieke implementatiemodel Hallo beheert.

## <a name="install-git-for-windows"></a>Installeer Git voor Windows
Hallo voorgaande sectie vermeld verschillende pakketten met Hallo `openssl` hulpprogramma voor Windows. Dit hulpprogramma is benodigde toocreate openbare en persoonlijke sleutels. Hallo volgen voorbeelden detail hoe tooinstall en gebruik **Git voor Windows**, maar u kunt kiezen welke u liever pakket. **GIT voor Windows** hebt u toegang toosome extra open source software ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) hulpprogramma's en hulpmiddelen die nuttig zijn kunnen bij het werken met virtuele Linux-machines.

1. Download en installeer **Git voor Windows** van Hallo volgende locatie: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Accepteer de standaardopties Hallo tijdens Hallo proces installeren tenzij u moet in het bijzonder toochange ze.
3. Voer **Git Bash** van Hallo **startmenu** > **Git** > **Git Bash**. Hallo-console lijkt vergelijkbare toohello voorbeeld te volgen:

    ![GIT voor Windows Bash-shell](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Een persoonlijke sleutel maken
1. In uw **Git Bash** venster gebruik `openssl.exe` toocreate een persoonlijke sleutel. Hallo volgende voorbeeld wordt een sleutel met de naam `myPrivateKey` en het certificaat met de naam `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    Hallo-uitvoer ziet er vergelijkbare toohello voorbeeld te volgen:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Als bash is een fout rapporteert, probeert te openen van een nieuwe **Git Bash** venster met verhoogde bevoegdheden. Voer Hallo `openssl` opdracht.

2. Antwoord Hallo vraagt om de landnaam, locatie, de organisatienaam van de, enzovoort.
3. Uw nieuwe persoonlijke sleutel en het certificaat worden in de huidige werkmap gemaakt. Uit veiligheidsoogpunt, moet u Hallo machtigingen instellen voor uw persoonlijke sleutel zodat alleen u toegang hebt tot het:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Hallo [volgende sectie](#create-a-private-key-for-putty) PuTTYgen tooboth met details bekijken en Hallo openbare sleutel wordt gebruikt en een persoonlijke sleutel maken dat specifiek is voor het gebruik van PuTTY tooSSH tooLinux virtuele machines. Hallo volgende opdracht genereert u een openbare sleutel bestand met de naam `myPublicKey.key` die u meteen kunt gebruiken:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Als u ook toomanage klassieke resources moet, converteren Hallo `myCert.pem` te`myCert.cer` (DER encoded X509 certificaat). Deze optionele stap alleen uitvoeren als u toospecifically moet oudere klassieke resources beheren.

    Hallo-certificaat met behulp van de volgende opdracht Hallo converteren:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Maken van een persoonlijke sleutel voor PuTTY
PuTTY is een algemene SSH-client voor Windows. U gratis toouse zijn een SSH-client die u wenst. toouse PuTTY, moet u een extra type sleutel - een PuTTY persoonlijke sleutel (PPK) toocreate. Als u niet dat toouse PuTTY wenst, moet u deze sectie overslaan.

Hallo volgende voorbeeld maakt u deze extra persoonlijke sleutel specifiek voor PuTTY toouse:

1. Gebruik **Git Bash** tooconvert uw persoonlijke sleutel in een persoonlijke sleutel RSA dat PuTTYgen kan begrijpen. Hallo volgende voorbeeld wordt een sleutel met de naam `myPrivateKey_rsa` van Hallo bestaande sleutel met de naam `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Uit veiligheidsoogpunt, moet u Hallo machtigingen instellen voor uw persoonlijke sleutel zodat alleen u toegang hebt tot het:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Downloaden en uitvoeren van PuTTYgen van Hallo volgende locatie: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Klik op Hallo menu: **bestand** > **Load persoonlijke sleutel**
4. Zoek uw persoonlijke sleutel (`myPrivateKey_rsa` in het vorige voorbeeld Hallo). Hallo standaarddirectory bij het starten van **Git Bash** is `C:\Users\%username%`. Hallo bestand filter tooshow wijzigen **alle bestanden (\*.\*)** :

    ![Hallo bestaande persoonlijke sleutel in PuTTYgen laden](./media/ssh-from-windows/load-private-key.png)
5. Klik op **Open**. Een prompt geeft aan dat deze sleutel Hallo zijn geïmporteerd:

    ![Sleutel tooPuTTYgen zijn geïmporteerd](./media/ssh-from-windows/successfully-imported-key.png)
6. Klik op **OK** tooclose Hallo prompt.
7. Hallo openbare sleutel wordt weergegeven boven Hallo Hallo **PuTTYgen** venster. U kopieert en plakt u deze openbare sleutel in hello Azure-portal of de Azure Resource Manager-sjabloon bij het maken van een Linux-VM. U kunt ook klikken op **openbare sleutel opslaan** toosave een kopie tooyour computer:

    ![PuTTY bestand voor de openbare sleutel opslaan](./media/ssh-from-windows/save-public-key.png)

    Hallo volgende voorbeeld ziet u hoe u wilt kopiëren en plak deze openbare sleutel in hello Azure-portal als u een Linux-VM maakt. Hallo openbare sleutel vervolgens doorgaans wordt opgeslagen in `~/.ssh/authorized_keys` op de nieuwe virtuele machine.

    ![Openbare sleutel wordt gebruikt bij het maken van een virtuele machine in hello Azure-portal](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. Terug in de **PuTTYgen**, klikt u op **persoonlijke sleutel opslaan**:

    ![PuTTY persoonlijke sleutel opslaan](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Gevraagd als u wenst dat toocontinue zonder uw sleutel een wachtwoordzin invoeren. Een wachtwoordzin is vergelijkbaar met een wachtwoord tooyour gekoppelde persoonlijke sleutel. Zelfs als iemand tooobtain uw persoonlijke sleutel ze nog steeds niet zou kunnen tooauthenticate met NET Hallo-sleutel. Ze moet tevens Hallo wachtwoordzin. Zonder een wachtwoordzin als iemand krijgt van uw persoonlijke sleutel ze zich in tooany VM of service die wordt gebruikt die sleutel. U wordt aangeraden maken van een wachtwoordzin. Als u Hallo wachtwoordzin vergeet, is er echter geen manier toorecover deze.
   >
   >

    Als u wenst dat tooenter een wachtwoordzin, klikt u op **Nee**, voer een wachtwoordzin in Hallo hoofdvenster PuTTYgen en klik vervolgens op **persoonlijke sleutel opslaan** opnieuw. Klik anders op **Ja** toocontinue zonder Hallo optionele wachtwoordzin.
9. Voer een naam en locatie toosave het PPK-bestand.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Putty tooSSH tooa Linux-Machine gebruiken
PuTTY is opnieuw een algemene SSH-client voor Windows. U gratis toouse zijn een SSH-client die u wenst. volgende stappen, details hoe Hallo toouse uw persoonlijke sleutel tooauthenticate met uw Azure-virtuele machine via SSH. Hallo stappen zijn vergelijkbaar in andere SSH-sleutel-clients in termen van tooload dat uw persoonlijke sleutel tooauthenticate Hallo SSH-verbinding.

1. Downloaden en uitvoeren putty van Hallo volgende locatie: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Vul in het Hallo-hostnaam of IP-adres van uw virtuele machine uit hello Azure-portal:

    ![Nieuwe PuTTY verbinding openen](./media/ssh-from-windows/putty-new-connection.png)
3. Voordat u selecteert **Open**, klikt u op **verbinding** > **SSH** > **Auth** tabblad. Bladeren tooand uw persoonlijke sleutel selecteren:

    ![Selecteer uw PuTTY persoonlijke sleutel voor verificatie](./media/ssh-from-windows/putty-auth-dialog.png)
4. Klik op **Open** tooconnect tooyour virtuele machine

## <a name="next-steps"></a>Volgende stappen
U kunt ook Hallo openbare en persoonlijke sleutels genereren [met OS X- en Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Zie voor meer informatie over Bash voor Windows en voordelen van OSS-hulpprogramma's direct beschikbaar op uw computer Windows hello [Bash op Ubuntu op Windows](https://msdn.microsoft.com/commandline/wsl/about).

Als u problemen ondervindt bij het gebruik van SSH tooconnect tooyour virtuele Linux-machines, Zie [oplossen SSH-verbindingen tooan Azure Linux VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
