1. Meld u aan toohello [klassieke Azure-portal](http://manage.windowsazure.com).  
2. Klik op de opdrachtbalk Hallo HALLO hallo venster onderaan in **nieuw**.
3. Onder **Compute**, klikt u op **virtuele Machine**, en klik vervolgens op **uit galerie**.
   
    ![Maak een nieuwe virtuele Machine][Image1]
4. Onder Hallo **SUSE** groep, selecteert u een installatiekopie van de virtuele machine OpenSUSE en klik vervolgens op Hallo pijl toocontinue.
5. Op Hallo eerste **Virtuele-machineconfiguratie** pagina:
   
   * Typ een **virtuele-machinenaam**, zoals 'testlinuxvm'. Hallo naam moet tussen 3 en 15 tekens bevatten, kunnen alleen letters, cijfers en afbreekstreepjes bevatten en moet beginnen met een letter en eindigen met een letter of een cijfer.
   * Controleer of Hallo **laag** en kies een **grootte**. Hallo laag bepaalt Hallo grootten die kunt u kiezen uit. Hallo grootte is van invloed op Hallo kosten voor het gebruik ervan, alsmede configuratie-opties, zoals een gegevensschijven met hoeveel u kunt koppelen. Zie voor meer informatie [grootten voor virtuele machines](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
   * Typ een **nieuwe gebruikersnaam**, of accepteer de standaardnaam hello, **azureuser**. Deze naam wordt toohello Sudoers bestand toegevoegd.
   * Bepaal welk type **verificatie** toouse. Zie voor richtlijnen voor algemene wachtwoord [sterke wachtwoorden](http://msdn.microsoft.com/library/ms161962.aspx).
6. Op Hallo volgende **Virtuele-machineconfiguratie** pagina:
   
   * Standaard-Hallo **Maak een nieuwe cloudservice**.
   * In Hallo **DNS-naam** typt u een unieke DNS-naam toouse als onderdeel van het Hallo-adres, zoals 'testlinuxvm'.
   * In Hallo **regio/affiniteit groep/virtueel netwerk** Selecteer een regio waar deze virtuele-installatiekopie wordt gehost.
   * Onder **eindpunten**, houden Hallo SSH-eindpunt. U kunt nu toevoegen of toevoegen, wijzigen of verwijderen nadat Hallo virtuele machine is gemaakt.
     
     > [!NOTE]
     > Als u een virtuele machine toouse een virtueel netwerk, wilt u **moet** Hallo virtueel netwerk opgeven wanneer u Hallo virtuele machine maken. U kunt een virtuele machine tooa virtueel netwerk niet toevoegen nadat u Hallo virtuele machine hebt gemaakt. Zie voor meer informatie [Virtual Network-overzicht](../articles/virtual-network/virtual-networks-overview.md).
     > 
     > 
7. Op Hallo laatste **Virtuele-machineconfiguratie** pagina, Hallo standaardinstellingen behouden en klik vervolgens op Hallo vinkje toofinish.

Hallo portal geeft een lijst van nieuwe virtuele machine onder Hallo **virtuele Machines**. Tijdens het Hallo-status wordt vermeld als **(Provisioning genoemd)**, Hallo virtuele machine wordt ingesteld. Wanneer Hallo status wordt gerapporteerd als **met**, kunt u op de volgende stap toohello.

## <a name="connect-toohello-virtual-machine"></a>Verbinding maken met virtuele Machine toohello
U SSH of PuTTY tooconnect toohello virtuele machine, afhankelijk van het besturingssysteem Hallo op Hallo-computer maakt u verbinding met:

* Vanaf een computer waarop Linux wordt uitgevoerd, SSH te gebruiken. Typ het volgende achter de opdrachtprompt Hallo:
  
    `$ ssh newuser@testlinuxvm.cloudapp.net -o ServerAliveInterval=180`
  
    Typ het wachtwoord van gebruiker Hallo.
* Vanaf een computer waarop Windows wordt uitgevoerd, moet u PuTTY gebruiken. Als u niet geïnstalleerd hebt, downloadt u dit uit Hallo [PuTTY-downloadpagina][PuTTYDownload].
  
    Sla **putty.exe** tooa map op uw computer. Open een opdrachtprompt, gaat u toothat map en voer **putty.exe**.
  
    Typ Hallo host-naam, bijvoorbeeld 'testlinuxvm.cloudapp.net' en '22' voor Hallo **poort**.
  
    ![PuTTY scherm][Image6]  

## <a name="update-hello-virtual-machine-optional"></a>Update Hallo virtuele Machine (optioneel)
1. Nadat u verbonden toohello virtuele machine bent, kunt u eventueel systeemupdates en -patches installeren. toorun hello update, type:
   
    `$ sudo zypper update`
2. Selecteer **Software**, klikt u vervolgens **Online-Update** toolist beschikbare updates. Selecteer **accepteren** toostart Hallo installatie en toepassen van alle nieuwe beschikbaar patches (behalve Hallo optionele waarden).
3. Nadat de installatie wordt uitgevoerd, selecteert u **voltooien**.  Uw systeem is nu maximaal toodate.

[PuTTYDownload]: http://www.puttyssh.org/download.html

[Image1]: ./media/create-and-configure-opensuse-vm-in-portal/CreateVM.png

[Image6]: ./media/create-and-configure-opensuse-vm-in-portal/putty.png
