---
title: aaaBack van VMware-servers met Azure Backup-Server | Microsoft Docs
description: Gebruik Azure Backup-Server tooback u een VMware vCenter/ESXi-servers tooAzure of de schijf. In dit artikel wordt stap voor-stap instructies voor back-ups maken (of beveiligen) = uw VMware-werkbelastingen.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a>Back-up van een VMware server tooAzure

Dit artikel wordt uitgelegd hoe tooconfigure Azure Backup-Server toohelp VMware server-werkbelasting beveiligen. In dit artikel wordt ervan uitgegaan dat u hebt al Azure Backup-Server is geïnstalleerd. Als u geen Azure Backup-Server is geïnstalleerd, raadpleegt u [tooback van de werkbelasting met behulp van Azure Backup-Server voorbereiden](backup-azure-microsoft-azure-backup.md).

Azure Backup-Server kunnen back-up maken of te beschermen, VMware vCenter-serverversie 6.5, 6.0 en 5.5.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Maken van een beveiligde verbinding toohello vCenter-Server

Standaard communiceert Azure Backup-Server met elk vCenter-Server via een HTTPS-kanaal. tooturn op Hallo veilige communicatie, wordt aangeraden dat u Hallo VMware certificeringsinstantie (CA)-certificaat op Azure Backup-Server installeren. Als u geen veilige communicatie vereist en toodisable Hallo HTTPS vereiste wilt gebruiken, Zie [uitschakelen beveiligde communicatieprotocol](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). een beveiligde verbinding tussen Azure Backup-Server en Hallo vCenter-Server, toocreate importeren Hallo vertrouwd certificaat op de Azure Backup-Server.

Normaal, gebruikt u een browser op Hallo back-upserver van Azure machine tooconnect toohello vCenter-Server via Hallo vSphere webclient. Hallo wanneer u eerst hello Azure Backup-Server browser tooconnect toohello vCenter Server, Hallo-verbinding niet veilig. Hallo volgende afbeelding geeft Hallo onbeveiligde verbinding.

![Voorbeeld van een niet-beveiligde verbinding tooVMware server](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix dit probleem en een beveiligde verbinding maken, downloaden Hallo vertrouwde basis-CA-certificaten.

1. Voer Hallo URL toohello vSphere webclient in Hallo-browser op Azure Backup-Server. Hallo vSphere webclient-aanmeldingspagina wordt weergegeven.

    ![vSphere webclient](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    Aan de onderkant van de Hallo van Hallo-informatie voor beheerders en ontwikkelaars, zoek Hallo **downloaden vertrouwde basis-CA-certificaten** koppeling.

    ![Koppeling toodownload Hallo vertrouwde basis-CA-certificaten](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Als u Hallo vSphere webclient-aanmeldingspagina niet ziet, controleert u de proxy-instellingen van uw browser.

2. Klik op **downloaden vertrouwde basis-CA-certificaten**.

    Hallo vCenter-Server downloadt een bestand tooyour lokale computer. Hallo bestandsnaam heet **downloaden**. Afhankelijk van uw browser die u ontvangt een bericht waarin wordt gevraagd of tooopen of Hallo bestand opslaan.

    ![bericht downloaden wanneer certificaten worden gedownload.](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Hallo tooa bestandslocatie op Azure Backup-Server opslaan. Wanneer u Hallo bestand opslaat, toevoegen Hallo .zip-extensie.

    Hallo-bestand is een ZIP-bestand dat Hallo informatie over Hallo certificaten bevat. U kunt met de extensie .zip hello, Hallo extractie-hulpprogramma's gebruiken.

4. Met de rechtermuisknop op **download.zip**, en selecteer vervolgens **Alles uitpakken** tooextract Hallo inhoud.

    Hallo ZIP-bestand uitgepakt haar inhoud tooa map met de naam **certificaten**. Twee typen bestanden worden weergegeven in Hallo certificaten map. Hallo basiscertificaatbestand heeft een extensie die met een genummerde volgorde zoals.0 en.1 begint.
    
    Hallo CRL-bestand heeft een extensie die met een reeks zoals .r0 of .r1 begint. Hallo CRL-bestand is gekoppeld aan een certificaat.

    ![Lokaal uitgepakt bestand downloaden ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. In Hallo **certificaten** map met de rechtermuisknop op Hallo basiscertificaatbestand en klik vervolgens op **naam**.

    ![Wijzig de naam van basiscertificaat ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Hallo-basiscertificaat van extensie too.crt wijzigen. Als u wordt gevraagd als u zeker dat u toochange Hallo extensie bent, klikt u op **Ja** of **OK**. Anders kunt u de juiste functie Hallo-bestand wijzigen. Hallo-pictogram voor Hallo bestand wijzigingen tooan pictogram van een basiscertificaat.

6. Met de rechtermuisknop op het Hallo-basiscertificaat en selecteer in het pop-upmenu hello, **certificaat installeren**.

    Hallo **Wizard Certificaat importeren** dialoogvenster wordt weergegeven.

7. In Hallo **Wizard Certificaat importeren** dialoogvenster, **lokale Machine** als bestemming voor Hallo-certificaat en klik vervolgens op Hallo **volgende** toocontinue.

    ![Certificaat bestemming opslagopties ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Als u wordt gevraagd als u wilt dat tooallow wijzigingen toohello computer, klikt u op **Ja** of **OK**, tooall Hallo wijzigingen.

8. Op Hallo **certificaatarchief** pagina **alle certificaten in Hallo volgende archief plaatsen**, en klik vervolgens op **Bladeren** toochoose Hallo-certificaatarchief.

    ![Certificaten in een bepaalde opslag-positie plaatsen](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Hallo **certificaatarchief selecteren** dialoogvenster wordt weergegeven.

    ![Map van de certificaathiërarchie opslag](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Selecteer **Trusted Root Certification Authorities** als de doelmap Hallo voor Hallo certificaten en klik vervolgens op **OK**.

    ![Certificaat-doelmap](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Hallo **Trusted Root Certification Authorities** map is bevestigd als Hallo-certificaatarchief. Klik op **Volgende**.

    ![Archiefmap certificaat](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. Op Hallo **voltooien Hallo Wizard Certificaat importeren** pagina en klik vervolgens op controleren of dat Hallo-certificaat in de gewenste map Hallo **voltooien**.

    ![Controleer of het certificaat bevindt zich in de juiste map Hallo](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Er verschijnt een dialoogvenster, wordt Hallo geslaagde certificaat importeren bevestigd.

11. Meld u aan toohello vCenter Server tooconfirm dat de verbinding beveiligd is.

  Hallo certificaat importeren niet met succes is voltooid en u geen beveiligde verbinding kan maken, de documentatie als Hallo VMware vSphere op [servercertificaten](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Als u beveiligde grenzen binnen uw organisatie hebben en tooturn op Hallo HTTPS-protocol niet wilt, gebruikt u hello te volgen procedure toodisable Hallo beveiligde communicatie.

### <a name="disable-secure-communication-protocol"></a>Beveiligde communicatieprotocol uitschakelen

Als uw organisatie niet Hallo HTTPS-protocol niet vereist, gebruik Hallo stappen toodisable HTTPS te volgen. toodisable standaardgedrag hello, maakt u een registersleutel die Hallo standaardgedrag negeert.

1. Kopieer en plak de volgende tekst in een txt-bestand Hallo.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Hallo bestand tooyour Azure Backup-Server computer opslaan. Gebruik voor Hallo bestandsnaam, DisableSecureAuthentication.reg.

3. Dubbelklik op Hallo bestand tooactivate Hallo register-item.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Een rol- en gebruikersaccount maakt op Hallo vCenter-Server

Hallo vcenter Server is een rol een vooraf gedefinieerde set met rechten. Een beheerder van de vCenter-Server maakt Hallo rollen. tooassign machtigingen, Hallo beheerder paren gebruikersaccounts met een rol. tooestablish hello nodig gebruiker referenties tooback van Hallo vCenter Server-computer een rol maken met specifieke rechten, en vervolgens Hallo-gebruikersaccount te koppelen aan Hallo-rol.

Azure Backup-Server gebruikt een gebruikersnaam en wachtwoord tooauthenticate met Hallo vCenter-Server. Azure Backup-Server gebruikt deze referenties als verificatie voor alle back-upbewerkingen.

tooadd een vCenter Server-rol en de rechten voor de beheerder van een back-up:

1. Meld u aan in toohello vCenter-Server en klik vervolgens in Hallo vCenter-Server **Navigator** -scherm, klikt u op **beheer**.

    ![Beheeroptie in vCenter Server Navigator Configuratiescherm](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. In **beheer** Selecteer **rollen**, en klik vervolgens in Hallo **rollen** Configuratiescherm klikt u op Hallo functiepictogram (symbool + Hallo) toevoegen.

    ![Functie toevoegen](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Hallo **rol maken** dialoogvenster wordt weergegeven.

    ![Rol maken](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. In Hallo **rol maken** dialoogvenster in Hallo **rolnaam** Voer *BackupAdminRole*. Hallo rolnaam is wat u maar wilt, maar moet herkenbare voor doel Hallo-rol.

4. Hallo bevoegdheden voor de juiste versie van vCenter Hallo selecteren en klik vervolgens op **OK**. Hallo volgende tabel identificeert Hallo vereiste bevoegdheden voor vCenter 6.0 en vCenter 5.5.

  Wanneer u Hallo bevoegdheden selecteert, klikt u op Hallo pictogram volgende toohello bovenliggende label tooexpand Hallo bovenliggende en bekijkt hello onderliggende bevoegdheden. tooselect hello VirtualMachine machtigingen beschikt, moet u toogo verschillende niveaus in Hallo bovenliggende/onderliggende hiërarchie. U hoeft niet tooselect alle onderliggende bevoegdheden binnen een bovenliggende-bevoegdheid.

  ![Bovenliggende/onderliggende hiërarchie bevoegdheden](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Nadat u op **OK**, Hallo nieuwe rol wordt weergegeven in de lijst Hallo op Hallo rollen Configuratiescherm.

|Bevoegdheden voor vCenter 6.0| Bevoegdheden voor vCenter 5.5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Maak een gebruikersaccount van de vCenter-Server en machtigingen

Nadat het Hallo-rol met bevoegdheden is ingesteld, moet u een gebruikersaccount maken. Hallo-gebruikersaccount heeft een naam en wachtwoord waarmee Hallo-referenties die worden gebruikt voor verificatie.

1. een gebruikersaccount in Hallo vCenter-Server toocreate **Navigator** -scherm, klikt u op **gebruikers en groepen**.

    ![Optie voor gebruikers en groepen](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Hallo **vCenter gebruikers en groepen** deelvenster wordt weergegeven.

    ![vCenter gebruikers en groepen Configuratiescherm](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. In Hallo **vCenter gebruikers en groepen** Configuratiescherm, selecteer Hallo **gebruikers** tabblad en klik vervolgens op Hallo gebruikers-pictogram (symbool + Hallo) toevoegen.

    Hallo **nieuwe gebruiker** dialoogvenster wordt weergegeven.

3. In Hallo **nieuwe gebruiker** dialoogvenster vak, Hallo gebruikersgegevens toevoegen en klik vervolgens op **OK**. In deze procedure is Hallo gebruikersnaam BackupAdmin.

    ![Dialoogvenster Nieuwe gebruiker](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    Hallo nieuwe gebruikersaccount wordt weergegeven in de lijst Hallo.

4. tooassociate Hallo-gebruikersaccount met Hallo-rol, in Hallo **Navigator** -scherm, klikt u op **algemene machtigingen**. In Hallo **algemene machtigingen** Configuratiescherm, selecteer Hallo **beheren** tabblad en klik vervolgens op Hallo pictogram (symbool + Hallo) toevoegen.

    ![Globale machtigingen Configuratiescherm](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Hallo **globale machtigingen Root - machtiging toevoegen** dialoogvenster wordt weergegeven.

5. In Hallo **globale machtiging Root - machtiging toevoegen** in het dialoogvenster, klikt u op **toevoegen** toochoose Hallo gebruiker of groep.

    ![Gebruiker of groep kiezen](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Hallo **gebruikers/groepen selecteren** dialoogvenster wordt weergegeven.

6. In Hallo **gebruikers/groepen selecteren** dialoogvenster Kies **BackupAdmin** en klik vervolgens op **toevoegen**.

    In **gebruikers**, Hallo *domein\gebruikersnaam* indeling wordt gebruikt voor het Hallo-gebruikersaccount. Als u een ander domein toouse wilt, kiezen uit Hallo **domein** lijst.

    ![BackupAdmin gebruiker toevoegen](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Klik op **OK** tooadd Hallo geselecteerd gebruikers toohello **machtiging toevoegen** in het dialoogvenster.

7. Nu dat u Hallo gebruiker hebt geïdentificeerd, toewijzen Hallo toohello gebruikersrol. In **toegewezen rol**, selecteer in de vervolgkeuzelijst hello, **BackupAdminRole**, en klik vervolgens op **OK**.

    ![Gebruiker toorole toewijzen](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  Op Hallo **beheren** tabblad in Hallo **algemene machtigingen** deelvenster, Hallo nieuwe gebruikersaccount en Hallo gekoppeld rol wordt weergegeven in Hallo lijst.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Referenties van de vCenter-Server op Azure Backup-Server tot stand brengen

Installeer voordat u Hallo VMware server tooAzure back-upserver toevoegt, [Update 1 voor Azure Backup-Server](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen Azure Backup-Server, dubbelklik op Hallo op Hallo Azure back-upserver bureaublad.

    ![Pictogram voor Azure Backup-Server](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Als u geen pictogram Hallo op Hallo bureaublad vinden, opent u Azure Backup-Server uit de lijst met geïnstalleerde apps Hallo. Hello Azure Backup-Server app-naam kan Microsoft Azure Backup wordt genoemd.

2. In de console hello Azure Backup-Server, klikt u op **Management**, klikt u op **productieservers**, en klik op het lint Hallo **beheren VMware**.

    ![Azure Backup-Server-console](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Hallo **referenties beheren** dialoogvenster wordt weergegeven.

    ![Het dialoogvenster Azure Backup-Server beheren referenties](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. In Hallo **referenties beheren** in het dialoogvenster, klikt u op **toevoegen** tooopen hello **referentie toevoegen** in het dialoogvenster.

4. In Hallo **referentie toevoegen** dialoogvenster Voer een naam en beschrijving voor de nieuwe referentie Hallo. Vervolgens Hallo gebruikersnaam en wachtwoord opgeven. Hallo-naam, *Contoso Vcenter referentie* wordt gebruikt tooidentify Hallo referentie in de volgende procedure Hallo. Gebruik Hallo dezelfde gebruikersnaam en het wachtwoord dat wordt gebruikt voor Hallo vCenter-Server. Als Hallo vCenter-Server en Azure Backup-Server zich niet in hetzelfde domein, Hallo **gebruikersnaam**, Hallo domein opgeven.

    ![In het dialoogvenster van Azure referentie van back-up-Server toevoegen](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Klik op **toevoegen** tooadd Hallo nieuwe referentie tooAzure back-upserver. Hallo nieuwe referentie wordt weergegeven in de lijst Hallo in Hallo **referenties beheren** in het dialoogvenster.
    
    ![Het dialoogvenster Azure Backup-Server beheren referenties](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. Hallo tooclose **referenties beheren** dialoogvenster vak, klikt u op Hallo **X** in de rechterbovenhoek Hallo.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Hallo vCenter Server tooAzure back-upserver toevoegen

Wizard voor toevoegen van productie-Server is gebruikt tooadd hello vCenter Server tooAzure back-upserver.

tooopen productie-Wizard voor het toevoegen van Server, volledige Hallo procedure te volgen:

1. Klik in hello Azure Backup-Server console **Management**, klikt u op **productieservers**, en klik vervolgens op **toevoegen**.

    ![De Wizard openen productie Server toevoegen](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Hallo **productie Server toevoeging Wizard** dialoogvenster wordt weergegeven.

    ![Wizard voor productie-Server toevoegen](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. Op Hallo **productieserver Selecteer type** pagina **VMware Servers**, en klik vervolgens op **volgende**.

3. In **Server naam of het IP-adres**, Hallo volledig gekwalificeerde domeinnaam (FQDN) of IP-adres van Hallo VMware-server opgeven. Als alle Hallo ESXi-servers worden beheerd door Hallo dezelfde vCenter, kunt u Hallo vCenter naam gebruiken.

    ![VMware server FQDN of IP-adres opgeven](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. In **SSL-poort**, Voer Hallo-poort die wordt gebruikt toocommunicate met Hallo VMware-server. Gebruik van poort 443, de standaardpoort hello, is tenzij u zeker weet dat een andere poort vereist is.

5. In **Geef referentie**, selecteer Hallo referentie die u eerder hebt gemaakt.

    ![Geef referenties](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Klik op **toevoegen** tooadd Hallo VMware toohello lijst met servers van **VMware-Servers toegevoegd**, en klik vervolgens op **volgende** toomove toohello volgende pagina in Hallo-wizard.

    ![VMWare-server en referentie toevoegen](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. In Hallo **samenvatting** pagina, klikt u op **toevoegen** tooadd Hallo opgegeven VMware server tooAzure back-upserver.

    ![VMware server tooAzure back-upserver toevoegen](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  Hallo VMware server back-up is een zonder agent back-up en de nieuwe server Hallo onmiddellijk wordt toegevoegd. Hallo **voltooien** pagina toont Hallo van resultaten.

  ![Voltooiingspagina](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd meerdere exemplaren van vCenter Server tooAzure back-upserver, herhaaldelijk Hallo vorige stappen in deze sectie.

Nadat u Hallo vCenter Server tooAzure back-upserver toevoegt, is de volgende stap Hallo toocreate een beveiligingsgroep. Hallo-beveiligingsgroep geeft Hallo verschillende details voor de korte of lange bewaarperiode en waar u definiëren en toepassen van de back-upbeleid Hallo is. back-upbeleid Hallo is Hallo planning voor wanneer de back-ups uitgevoerd en waarvan een back-is gemaakt.


## <a name="configure-a-protection-group"></a>Configureer een beveiligingsgroep

Als u System Center Data Protection Manager of Azure Backup-Server voordat u niet hebt gebruikt, raadpleegt u [plannen voor back-ups van schijf](https://technet.microsoft.com/library/hh758026.aspx) tooprepare uw hardware-omgeving. Nadat u hebt gecontroleerd dat u de juiste opslag hebt, gebruik Hallo nieuwe beveiligingsgroep maken wizard tooadd virtuele VMware-machines.

1. In de console hello Azure Backup-Server, klikt u op **beveiliging**, en klik in het lint Hallo op **nieuw** tooopen Hallo nieuwe beveiligingsgroep maken wizard.

    ![Wizard Open Hallo-nieuwe beveiligingsgroep maken](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Hallo **nieuwe beveiligingsgroep maken** in het dialoogvenster wizard wordt weergegeven.

    ![Dialoogvenster voor wizard nieuwe beveiligingsgroep maken](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Klik op **volgende** tooadvance toohello **type beveiligingsgroep selecteren** pagina.

2. Op Hallo **Selecteer type beveiligingsgroep** pagina **Servers** en klik vervolgens op **volgende**. Hallo **groepsleden selecteren** pagina wordt weergegeven.

3. Op Hallo **groepsleden selecteren** pagina, de beschikbare leden Hallo en Hallo geselecteerde leden worden weergegeven. Selecteer Hallo leden wilt tooprotect en klik vervolgens op **volgende**.

    ![Groepsleden selecteren](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Wanneer u een lid, selecteert als u een map met andere mappen of virtuele machines selecteert, worden de mappen en virtuele machines ook geselecteerd. Hallo insluiting Hallo mappen en virtuele machines in Hallo bovenliggende map heet mapniveau beveiliging. tooremove een map of virtuele machine, wissen Hallo selectievakje.

    Als een virtuele machine of een map met een VM al beveiligd tooAzure is, niet worden geselecteerd die virtuele machine opnieuw. Dat wil zeggen, nadat een virtuele machine beveiligd tooAzure is, worden niet beveiligd, waarmee wordt voorkomen dat dubbele herstelpunten worden gemaakt voor een virtuele machine. Als u wilt dat toosee beveiligt welk exemplaar van Azure Backup-Server al een lid, punt toohello toosee Hallo lidnaam Hallo server beveiligt.

4. Op Hallo **methode voor gegevensbeveiliging selecteren** pagina, voer een naam voor de beveiligingsgroep Hallo. Beveiliging op korte termijn (toodisk) en online beveiliging zijn geselecteerd. Als u wilt toouse online beveiliging (tooAzure), moet u kortdurende beveiliging toodisk gebruiken. Klik op **volgende** tooproceed toohello kortdurende beveiliging bereik.

    ![Methode voor gegevensbeveiliging selecteren](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. Op Hallo **Kortetermijndoelen opgeven** pagina voor **bewaartermijn**, geef het aantal dagen dat u wilt tooretain herstelpunten Hallo zijn *toodisk opgeslagen*. Als u wilt dat toochange Hallo tijd en de dagen waarop herstelpunten worden gemaakt, klikt u op **wijzigen**. Hallo op korte termijn herstelpunten zijn volledige back-ups. Ze zijn geen incrementele back-ups. Wanneer u tevreden met korte-termijndoelstellingen hello bent, klikt u op **volgende**.

    ![Korte-termijndoelstellingen opgeven](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. Op Hallo **Schijftoewijzing controleren** controleert en wijzig indien nodig Hallo schijfruimte beschikbaar voor Hallo virtuele machines. Hallo aanbevolen schijftoewijzingen zijn gebaseerd op Hallo bewaartermijn die is opgegeven in Hallo **Kortetermijndoelen opgeven** pagina Hallo type werkbelasting en de grootte Hallo Hallo van beveiligde gegevens (aangeduid in stap 3).  

  - **Gegevensgrootte:** grootte van de gegevens in de beveiligingsgroep Hallo Hallo.
  - **Schijfruimte:** Hallo aanbevolen hoeveelheid schijfruimte voor de beveiligingsgroep Hallo. Als u deze instelling toomodify wilt, moet u de totale ruimte die groter is dan Hallo bedrag in dat u een schatting maken van dat elke gegevensbron groeit toewijzen.
  - **Gegevens plaatsen:** als u collocatie inschakelt, op meerdere gegevensbronnen Hallo beveiliging tooa één replica en herstelpuntvolume kunnen toewijzen. Collocatie wordt niet ondersteund voor alle werkbelastingen.
  - **Automatisch vergroten:** als u voor deze instelling inschakelt als gegevens in de groep beveiligde Hallo groter worden dan de aanvankelijke toewijzing hello, System Center Data Protection Manager tooincrease Hallo schijfgrootte probeert met 25 procent.
  - **Opslaggroepdetails:** toont de status Hallo van Hallo opslaggroep aanwezig zijn, waaronder de totale en resterende schijfgrootte.

    ![Schijftoewijzing controleren](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Wanneer u tevreden met de ruimtetoewijzing hello bent, klikt u op **volgende**.

7. Op Hallo **methode voor maken van selecteren Replica** pagina, Geef op hoe u toogenerate Hallo eerste kopie of replica van Hallo beveiligde gegevens op Azure Backup-Server.

    Hallo standaardwaarde is **automatisch via netwerk Hallo** en **nu**. Als u Hallo standaard gebruikt, raden wij aan dat u een tijdstip buiten de piekuren opgeeft. Kies **Later** en geef een dag en tijd.

    Voor grote hoeveelheden gegevens of minder dan optimale netwerkomstandigheden, kunt u Hallo gegevens offline repliceren met behulp van verwijderbare media.

    Nadat u uw keuzes hebt aangebracht, klikt u op **volgende**.

    ![Methode voor het maken van replica selecteren](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. Op Hallo **opties voor consistentiecontrole** pagina hoe en wanneer tooautomate Hallo consistentiecontroles. Wanneer de gerepliceerde gegevens inconsistent, of volgens een vooropgezet schema, kunt u consistentiecontroles uitvoeren.

    Als u niet tooconfigure automatische consistentiecontroles wilt, kunt u een handmatige controle uitvoeren. Met de rechtermuisknop op de beveiligingsgroep Hallo in Hallo beveiliging gebied hello Azure Backup-Server-console, en selecteer vervolgens **consistentiecontrole uitvoeren**.

    Klik op **volgende** toomove toohello volgende pagina.

9. Op Hallo **gegevens voor Online beveiliging opgeven** pagina, selecteert u een of meer gegevensbronnen die u tooprotect wilt. Hallo leden afzonderlijk selecteren of klik op **Alles selecteren** toochoose alle leden. Nadat u ervoor Hallo leden kiest, klikt u op **volgende**.

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. Op Hallo **onlineback-upschema opgeven** pagina, Hallo planning toogenerate herstelpunten Hallo schijfback-up opgeven. Nadat het Hallo herstelpunt dat is gegenereerd, is het overgebrachte toohello Recovery Services-kluis in Azure. Wanneer u tevreden met online back-upschema hello bent, klikt u op **volgende**.

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. Op Hallo **Online bewaarbeleid opgeven** pagina, geeft u aan hoe lang u tooretain Hallo back-upgegevens in Azure. Nadat het Hallo-beleid is gedefinieerd, klikt u op **volgende**.

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Er is geen tijdslimiet voor hoe lang van gegevens in Azure bewaren. Wanneer u herstelpuntgegevens in Azure opslaat, hello alleen limiet is dat er geen meer dan 9999 herstelpunten per beveiligde exemplaar. In dit voorbeeld is het beveiligde exemplaar Hallo Hallo VMware-server.

12. Op Hallo **samenvatting** pagina, Hallo details bekijken voor de leden van de beveiligingsgroep en de instellingen en klik vervolgens op **groep maken**.

    ![Een lid van beveiligingsgroep en samenvatting van de instelling](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Volgende stappen
Als u Azure Backup-Server tooprotect VMware werkbelastingen gebruikt, hebt u mogelijk geïnteresseerd in met behulp van Azure Backup-Server beveiligen toohelp een [Microsoft Exchange-server](./backup-azure-exchange-mabs.md), een [Microsoft SharePoint-farm](./backup-azure-backup-sharepoint-mabs.md), of een [SQL Server-database](./backup-azure-sql-mabs.md).

Zie voor informatie over problemen met het Hallo-agent registreren, Hallo beveiligingsgroep configureert of back-ups van taken, [problemen met Azure Backup-Server](./backup-azure-mabs-troubleshoot.md).
