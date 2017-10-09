

Wanneer u een toepassing webproject voor Azure maakt, kunt u een virtuele machine in Azure inrichten. U kunt vervolgens Hallo virtuele machine configureren met extra software of Hallo virtuele machine worden gebruikt voor diagnostische of foutopsporing doeleinden.

toocreate een virtuele machine wanneer u een webtoepassing maakt als volgt te werk:

1. Klik in Visual Studio **bestand** > **nieuw** > **Project** > **Web**, en kies vervolgens **ASP.NET-webtoepassing** (onder Hallo **Visual C#** of **Visual Basic** knooppunten).
2. In Hallo **nieuw ASP.NET-Project** in het dialoogvenster, selecteer Hallo type webtoepassing die u wilt en in hello Azure gedeelte van het dialoogvenster hello (in de rechterbenedenhoek Hallo), zorg ervoor dat Hallo **Host in de cloud Hallo**selectievakje is ingeschakeld (deze selectievakje **maken van externe bronnen** in sommige installaties).
   
    ![][0]
3. Kies voor dit voorbeeld in Hallo vervolgkeuzelijst onder Microsoft Azure **virtuele Machine (v1)**, en klik vervolgens op Hallo **OK** knop.
4. Meld u tooAzure als u wordt gevraagd. Hallo **virtuele Machine maken** dialoogvenster wordt weergegeven.
   
    ![][2]
5. In Hallo **DNS-naam** Voer een naam voor Hallo virtuele machine. Hallo DNS-naam moet uniek zijn in Azure. Als Hallo die u hebt ingevoerd is niet beschikbaar, verschijnt er een rood uitroepteken.
6. In Hallo **installatiekopie** Kies Hallo afbeelding op het gewenste toobase Hallo virtuele machine. U kunt een van de installatiekopieën van de virtuele machine van de standaard Azure Hallo of uw installatiekopie die u tooAzure hebt geüpload.
7. Hallo laat **IIS inschakelen en Web Deploy** selectievakje geselecteerd tenzij u van plan een andere webserver tooinstall bent. U kunt toopublish vanuit Visual Studio niet als u Web Deploy uitschakelt. U kunt IIS en Web Deploy tooany van installatiekopieën van Windows Server voor Hallo verpakt, met inbegrip van uw eigen aangepaste installatiekopieën toevoegen.
8. In Hallo **grootte** Kies Hallo grootte van Hallo virtuele machine.
9. Geef Hallo aanmeldingsreferenties voor deze virtuele machine. Noteer deze, omdat u moet ze tooaccess Hallo machine via Extern bureaublad.
10. In Hallo **locatie** Kies Hallo regio toohost Hallo virtuele machine.
11. Klik op Hallo **OK** knop toostart Hallo virtuele machine wordt gemaakt. Kunt u Hallo voortgang van Hallo-bewerking in Hallo **uitvoer** venster.
    
    ![][3]
12. Wanneer Hallo virtuele machine is ingericht, gepubliceerde scripts worden gemaakt in een **PublishScripts** knooppunt in uw oplossing. Hallo gepubliceerd script wordt uitgevoerd en voorziet in een virtuele machine in Azure. Hallo **uitvoer** venster Hallo status bevat. Hallo script voert Hallo acties tooset Hallo virtuele machine te volgen:
    
    * Als deze nog niet bestaat, maakt Hallo virtuele machine.
    * Een opslagaccount maakt met een naam die met begint `devtest`, maar alleen als er al een opslagaccount in Hallo opgegeven regio.
    * Maakt een cloudservice als een container voor Hallo virtuele machine en een Webrol voor Hallo-webtoepassing maakt.
    * Hiermee configureert u Web Deploy op Hallo virtuele machine.
    * Hiermee configureert u IIS en ASP.NET op Hallo virtuele machine.
    
    ![][4]
13. (Optioneel) U kunt de nieuwe virtuele machine toohello verbinden. In **Server Explorer**, vouw Hallo **virtuele Machines** knooppunt Hallo knooppunt voor Hallo virtuele machine die u hebt gemaakt, en in het snelmenu kiezen, kiest u **verbinding maken met extern bureaublad**. U kunt ook in **Cloud Explorer** kunt u **openen in de Portal** snelmenu Hallo en worden er toohello virtuele machine verbinding maken.
    
    ![][5]

## <a name="next-steps"></a>Volgende stappen
Meer gedetailleerde informatie op als u wilt dat toocustomize Hallo gepubliceerde scripts die u hebt gemaakt, gelezen [tooPublish tooDev van Windows PowerShell-Scripts en testomgevingen](http://msdn.microsoft.com/library/dn642480.aspx).

[0]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_NewProject.PNG
[1]: ./media/dotnet-visual-studio-create-virtual-machine/CreateVM_SignIn.PNG
[2]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_CreateVM.PNG
[3]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_Provisioning.png
[4]: ./media/virtual-machines-common-classic-web-app-visual-studio/CreateVM_SolutionExplorer.png
[5]: ./media/virtual-machines-common-classic-web-app-visual-studio/VS_Create_VM_Connect.png
