>[!NOTE]
> U kunt opmerkingen laten op deze pagina voor feedback of via [Azure feedback](https://feedback.azure.com/forums/216843-virtual-machines) met #azerrormessage-tag.

## <a name="error-response-format"></a>Fout antwoord-indeling 
Virtuele machines in Azure gebruiken Hallo JSON-indeling voor het foutbericht te volgen:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Reactie op een fout bevat altijd een statuscode en een error-object. Elk foutobject bevat altijd een foutcode en een bericht. Als hello VM is gemaakt met een sjabloon, bevat Hallo foutobject ook een sectie voor informatie die een binnenste niveau van foutcodes en het bericht bevat. Normaal gesproken is hello meeste binnenste niveau van het foutbericht Hallo basis-fout.


## <a name="common-virtual-machine-management-errors"></a>Algemene fouten voor het beheer van virtuele machine

Deze sectie vindt u Hallo algemene foutberichten die optreden kunnen bij het beheren van virtuele machines:

|  Foutcode  |  Foutbericht  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  Tooacquire lease zijn mislukt bij het maken van schijf '{0}' met blob met URI {1}. BLOB wordt al gebruikt.  |  
|  AllocationFailed  |  Toewijzing is mislukt. Probeer het verminderen van Hallo VM-grootte of het aantal virtuele machines, probeer het later opnieuw, of tooa implementeren andere Beschikbaarheidsset of andere Azure-locatie.  |  
|  AllocationFailed  |  Hallo VM-toewijzing is mislukt vanwege een interne fout tooan. Probeer het later opnieuw of probeer te implementeren tooa andere locatie.  |
|  ArtifactNotFound  |  Hallo VM-extensie met uitgever {0} en het type '{1}' kan niet worden gevonden op locatie '{2}'.  |
|  ArtifactNotFound  |  Extensie met uitgever {0}, typ '{1}' en type handlerversie '{2}' kan niet worden gevonden in de extensieopslagplaats Hallo.  |
|  ArtifactVersionNotFound  |  Er is geen versie gevonden in de artefactopslagplaats Hallo die voldoet aan de Hallo aangevraagd versie {0}.  |
|  ArtifactVersionNotFound  |  Er is geen versie gevonden in de artefactopslagplaats Hallo die voldoet aan de Hallo aangevraagd versie {0} voor VM-extensie met uitgever '{1}' en het type '{2}'.  |
|  AttachDiskWhileBeingDetached  |  Geen gegevens schijf '{0}' tooVM '{1}' niet toevoegen omdat Hallo schijf is op dit moment wordt losgekoppeld. Wacht totdat het Hallo-schijf volledig is losgekoppeld en probeer het opnieuw.  |
|  BadRequest  |  Uitgelijnd ' Beschikbaarheidssets worden nog niet ondersteund in deze regio.  |
|  BadRequest  |  Toevoeging van een virtuele machine met beheerde schijven toonon beheerd Beschikbaarheidsset of toevoeging van een virtuele machine met blobs gebaseerde schijven toomanaged Beschikbaarheidsset wordt niet ondersteund. Maak een Beschikbaarheidsset met 'beheerde'-eigenschap is ingesteld in volgorde tooadd met beheerde schijven tooit een virtuele machine.  |
|  BadRequest  |  Beheerde schijven worden niet ondersteund in deze regio.  |
|  BadRequest  |  Meerdere VM-extensies per handler worden niet ondersteund voor OS Typ '{0}'. VMExtension '{1}' met de handler '{2}' is al toegevoegd of opgegeven in de invoer.  |
|  BadRequest  |  Bewerking '{0}' wordt niet ondersteund voor Resource '{1}' met beheerde-schijven.  |
|  CertificateImproperlyFormatted  |  Hallo van geheim opgehaald uit {0} JSON-weergave bevat een gegevensveld dat geen een onjuist geformatteerd PFX-bestand of Hallo wachtwoord opgegeven Hallo PFX-bestand niet correct decoderen.  |
|  CertificateImproperlyFormatted  |  Hallo-gegevens ophalen uit {0} is niet opnieuw worden geserialiseerd naar JSON.  |
|  Conflict  |  De schijfgrootte is toegestaan, alleen bij het maken van een virtuele machine of als Hallo VM toewijzing ongedaan is gemaakt.  |
|  ConflictingUserInput  |  Schijf '{0}' kan niet worden gekoppeld als Hallo schijf is al het eigendom van de virtuele machine '{1}'.  |
|  ConflictingUserInput  |  Bron-en doelresourcegroep zijn dezelfde Hallo.  |
|  ConflictingUserInput  |  Bron- en doelopslagaccounts voor schijf {0} verschillen.  |
|  ContainerAlreadyOnLease  |  Er is al een lease op Hallo storage-container houden Hallo blob met URI {0}.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  Hallo de aanvraag voor resources verplaatsen bevat KeyVault-resources waarnaar wordt verwezen door een of meer {0} s in Hallo-aanvraag. Dit wordt niet wordt momenteel ondersteund kruislingse verplaatsen. Controleer de foutdetails Hallo voor Hallo KeyVault-resource-id.  |
|  DiagnosticsOperationInternalError  |  Er is een interne fout opgetreden tijdens het verwerken van het diagnostische profiel van VM {0}.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  BLOB {0} is al in gebruik door een andere schijf die behoren tooVM '{1}'. U kunt nagaan Hallo blobmetagegevens voor Hallo schijf referentie-informatie.  |
|  DiskBlobNotFound  |  Kan geen toofind VHD blob met URI {0} voor schijf '{1}'.  |
|  DiskBlobNotFound  |  Kan geen toofind VHD blob met URI {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  {0} geheim beschikt niet over Hallo {1} labels. Hallo geheime versie bij te werken, Hallo vereist labels toevoegen en probeer het opnieuw.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  Uitpakken van de waarde van de geheime {0} met behulp van de belangrijkste {1} is mislukt.  |
|  DiskImageNotReady  |  Schijf installatiekopie {0} heeft {1} status. Probeer het opnieuw wanneer de installatiekopie is nu klaar.  |
|  DiskPreparationError  |  Een of meer fouten opgetreden tijdens het voorbereiden van VM-schijven. Zie schijf exemplaar weergeven voor meer informatie.  |
|  DiskProcessingError  |  Verwerking van de schijf is onderbroken omdat Hallo VM andere schijven in niet-werkende schijven heeft.  |
|  ImageBlobNotFound  |  Kan geen toofind VHD blob met URI {0} voor schijf '{1}'.  |
|  ImageBlobNotFound  |  Kan geen toofind VHD blob met URI {0}.  |
|  IncorrectDiskBlobType  |  Schijfblobs kunnen alleen worden van het type pagina-blob. BLOB {0} voor schijf '{1}' is van het type blok-blob.  |
|  IncorrectDiskBlobType  |  Schijfblobs kunnen alleen worden van het type pagina-blob. BLOB {0} is van het type '{1}'.  |
|  IncorrectImageBlobType  |  Schijfblobs kunnen alleen worden van het type pagina-blob. BLOB {0} voor schijf '{1}' is van het type blok-blob.  |
|  IncorrectImageBlobType  |  Schijfblobs kunnen alleen worden van het type pagina-blob. BLOB {0} is van het type '{1}'.  |
|  InternalOperationError  |  Kan het opslagaccount {0} niet omzetten. Zorg ervoor dat het is gemaakt via Hallo Storage Resource Provider Hallo dezelfde locatie als Hallo compute resource.  |
|  InternalOperationError  |  {0} taken voor Doelzoeken zijn mislukt.  |
|  InternalOperationError  |  Er is een fout opgetreden bij het valideren van Hallo netwerkprofiel van VM {0}.  |
|  InvalidAccountType  |  Hallo AccountType {0} is ongeldig.  |
|  InvalidParameter  |  Hallo-waarde van parameter {0} is ongeldig.  |
|  InvalidParameter  |  Hallo opgegeven beheerderswachtwoord is niet toegestaan.  |
|  InvalidParameter  |  ' Hallo opgegeven wachtwoord moet tussen {0}-\ {1\} tekens lang en moeten voldoen aan ten minste {2} van vereisten voor wachtwoordcomplexiteit van Hallo volgende: <ol><li> Bevat een hoofdletter</li><li>Bevat een kleine letter</li><li>Bevat een numerieke getal</li><li>Bevat een speciaal teken.</li></ol>  |
|  InvalidParameter  |  Hallo Beheerdersgebruikersnaam is opgegeven, is niet toegestaan.  |
|  InvalidParameter  |  Een bestaande OS-schijf kan niet worden gekoppeld als hello VM is gemaakt op basis van een installatiekopie van het platform of gebruiker.  |
|  InvalidParameter  |  Container naam {0} is ongeldig. Containernamen moeten 3-63 tekens lang zijn en mag alleen kleine alfanumerieke tekens en afbreekstreepjes bevatten. Afbreekstreepje moet worden voorafgegaan en gevolgd door een alfanumeriek teken.  |
|  InvalidParameter  |  Container naam {0} in de URL {1} is ongeldig. Containernamen moeten 3-63 tekens lang zijn en mag alleen kleine alfanumerieke tekens en afbreekstreepjes bevatten. Afbreekstreepje moet worden voorafgegaan en gevolgd door een alfanumeriek teken.  |
|  InvalidParameter  |  Hallo blob-naam in URL {0} bevat een slash. Dit wordt momenteel niet ondersteund voor schijven.  |
|  InvalidParameter  |  Hallo URI {0} lijkt niet de juiste blob-toobe URI.  |
|  InvalidParameter  |  Een schijf met de naam '{0}' al wordt gebruikt hetzelfde LUN Hallo: {1}.  |
|  InvalidParameter  |  Een schijf met de naam {0} al bestaat.  |
|  InvalidParameter  |  Kan niet opgeven voor een schijf die al is gedefinieerd in de opgegeven Hallo gebruikersafbeelding verwijzing afbeelding.  |
|  InvalidParameter  |  Een schijf met de naam '{0}' al wordt gebruikt dezelfde VHD URL {1} Hallo.  |
|  InvalidParameter  |  Hallo opgegeven foutdomein domein aantal {0} moet vallen in Hallo bereik {1} too\ {2\}.  |
|  InvalidParameter  |  Hallo licentie type {0} is ongeldig. Geldige licentietypen zijn: Windows_Client of Windows_Server, hoofdlettergevoelig.  |
|  InvalidParameter  |  Linux-hostnaam mag maximaal {0} tekens lang of Hallo volgende tekens bevatten: {1}.  |
|  InvalidParameter  |  Doelpad voor openbare Ssh-sleutels is momenteel beperkt tooits standaardwaarde {0} vanwege tooa bekend probleem in Linux-inrichtingsagent.  |
|  InvalidParameter  |  Een schijf voor LUN {0} bestaat al.  |
|  InvalidParameter  |  Abonnement {0} van Hallo-aanvraag moet overeenkomen met de Hallo abonnement {1} opgenomen in Hallo beheerde schijf-id.  |
|  InvalidParameter  |  Aangepaste gegevens in OSProfile moeten met Base64 zijn versleuteld en een maximum lengte hebben van {0} tekens.  |
|  InvalidParameter  |  BLOB-naam in URL {0} moet eindigen met '{1}'-extensie.  |
|  InvalidParameter  |  {0}' is niet een geldig voorvoegsel van het vastgelegde VHD-blob. Een geldig voorvoegsel komt overeen met reguliere expressie '{1}'.  |
|  InvalidParameter  |  Certificaten kunnen niet worden toegevoegd tooyour VM Hallo VM-agent niet is ingericht.  |
|  InvalidParameter  |  Een schijf voor LUN {0} bestaat al.  |
|  InvalidParameter  |  Kan geen toocreate Hallo VM is omdat Hallo grootte {0} aangevraagd niet beschikbaar in Hallo cluster waar Hallo beschikbaarheidsset momenteel is toegewezen. Hallo beschikbare grootten zijn: {1}. Lees meer over VM strategy op https://aka.ms/azure-resizevm vergroten of verkleinen.  |
|  InvalidParameter  |  Hallo aangevraagd {0} voor VM-grootte is niet beschikbaar in de huidige regio Hallo. Hallo grootten beschikbaar in de huidige regio Hallo zijn: {1}. Lees meer informatie over beschikbare VM-grootten Hallo in elke regio op https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Hallo aangevraagd {0} voor VM-grootte is niet beschikbaar in de huidige regio Hallo. Lees meer informatie over beschikbare VM-grootten Hallo in elke regio op https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Windows-beheerdersgebruikersnaam mag niet langer zijn dan {0} tekens lang, eindigen met een period(.) of Hallo volgende tekens bevatten: {1}.  |
|  InvalidParameter  |  Windows-computernaam mag niet langer zijn dan {0} tekens lang, uitsluitend uit cijfers bestaan of Hallo volgende tekens bevatten: {1}.  |
|  MissingMoveDependentResources  |  aanvraag Hallo verplaatsen van resources bevat niet alle Hallo afhankelijke resources. Controleer de foutdetails op ontbrekende resource-id.  |
|  MoveResourcesHaveInvalidState  |  Hallo-aanvraag voor Resources verplaatsen bevat virtuele machines die gekoppeld met ongeldige storage-accounts zijn. Controleer de details voor deze resource-id en de namen van opslagaccounts waarnaar wordt verwezen.  |
|  MoveResourcesHavePendingOperations  |  aanvraag Hallo verplaatsen van resources bevat resources waarvoor een bewerking in behandeling is. Controleer de details voor deze resource-id. Probeer de bewerking opnieuw nadat Hallo bewerkingen die in behandeling is voltooid.  |
|  MoveResourcesNotFound  |  Hallo verplaatsen van resources bevat resources die niet is gevonden. Controleer de details voor deze resource-id.  |
|  NetworkingInternalOperationError  |  Onbekende netwerktoewijzingsfout.  |
|  NetworkingInternalOperationError  |  Onbekende netwerktoewijzingsfout  |
|  NetworkingInternalOperationError  |  Een interne fout opgetreden bij het verwerken van het netwerkprofiel van Hallo VM.  |
|  notFound  |  Hallo Beschikbaarheidsset {0} kan niet worden gevonden.  |
|  notFound  |  Bron virtuele Machine '{0}' is opgegeven in de aanvraag Hallo bestaat niet in deze Azure-locatie.  |
|  notFound  |  Tenant met id {0} is niet gevonden.  |
|  notFound  |  Hallo-installatiekopie {0} kan niet worden gevonden.  |
|  NotSupported  |  Hallo licentietype is {0}, maar Hallo installatiekopie blob {1} is niet afkomstig van on-premises.  |
|  OperationNotAllowed  |  Beschikbaarheid Set {0} kan niet worden verwijderd. Voordat u verwijdert een Beschikbaarheidsset Zorg ervoor dat het heeft geen VM bevat.  |
|  OperationNotAllowed  |  SKU van 'Uitgelijnd' too'Classic wijzigingen beschikbaarheid instellen ' is niet toegestaan.  |
|  OperationNotAllowed  |  Kan geen extensies wijzigen in Hallo VM wanneer Hallo VM niet wordt uitgevoerd.  |
|  OperationNotAllowed  |  Hallo vastleggen actie wordt alleen ondersteund op een virtuele Machine met blobs gebaseerde schijven. Gebruik Hallo 'Image' resource-API's toocreate een installatiekopie van een beheerde virtuele Machine.  |
|  OperationNotAllowed  |  Hallo resource {0} kan niet worden gemaakt van de afbeelding {1} totdat de installatiekopie is gemaakt.  |
|  OperationNotAllowed  |  Updates tooencryptionSettings is niet toegestaan wanneer de VM is toegewezen, probeer het opnieuw nadat de toewijzing van VM ongedaan is gemaakt  |
|  OperationNotAllowed  |  Toevoeging van een beheerde schijf tooa VM met blobs gebaseerde schijven wordt niet ondersteund.  |
|  OperationNotAllowed  |  maximum aantal gegevensschijven Hallo toegestane toobe gekoppeld tooa VM van deze omvang is {0}.  |
|  OperationNotAllowed  |  Toevoeging van een blobs gebaseerde schijf tooVM met beheerde schijven wordt niet ondersteund.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op de installatiekopie '{1}' sinds Hallo die installatiekopie is gemarkeerd voor verwijdering. U kunt alleen Hallo Delete-bewerking opnieuw proberen (of wachten op een actieve één toocomplete).  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM '{1}' sinds Hallo die VM is gegeneraliseerd.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan als terugzetten punt verzameling '{1}' is gemarkeerd voor verwijdering.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM-extensie '{1}' omdat deze is gemarkeerd voor verwijdering. U kunt alleen Hallo Delete-bewerking opnieuw proberen (of wachten op een actieve één toocomplete).  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan omdat {1}' hello virtuele Machines' zijn ingericht met behulp van {2}' hello installatiekopie'.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan omdat Hallo ScaleSet van de virtuele Machine '{1}' Hallo '{2}' installatiekopie momenteel wordt gebruikt.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM '{1}' sinds Hallo die VM is gemarkeerd voor verwijdering. U kunt alleen Hallo Delete-bewerking opnieuw proberen (of wachten op een actieve één toocomplete).  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM '{1}' omdat Hallo VM toewijzing ongedaan is gemaakt of gemarkeerd toobe ongedaan.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM '{1}' sinds Hallo die VM wordt uitgevoerd. Neem uitschakelen expliciet als u afsluiten Hallo VM van in het gastbesturingssysteem Hallo.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM '{1}' sinds Hallo die VM wordt niet vrijgegeven.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM '{1}' omdat de VM heeft een extensie '{2}' status mislukt heeft.  |
|  OperationNotAllowed  |  Bewerking '{0}' is niet toegestaan op VM '{1}', omdat een andere bewerking uitgevoerd wordt.  |
|  OperationNotAllowed  |  Hallo-bewerking {0} moet Hallo virtuele Machine '{1}' toobe gegeneraliseerd.  |
|  OperationNotAllowed  |  Hallo-bewerking vereist Hallo VM toobe uitgevoerd (of toorun instellen).  |
|  OperationNotAllowed  |  Een schijf met de grootte van {0} GB, die is kleiner dan Hallo {1}GB van de bijbehorende schijf in afbeelding grootte, is niet toegestaan.  |
|  OperationNotAllowed  |  VM-Schaalset extensies van handler '{0}' kunnen alleen op Hallo moment VM-Schaalset gemaakt worden toegevoegd.  |
|  OperationNotAllowed  |  VM-Schaalset extensies van handler '{0}' kunnen alleen op Hallo tijdstip van verwijderen van een VM-Schaalset worden verwijderd.  |
|  OperationNotAllowed  |  Virtuele machine '{0}' wordt al gebruikt voor beheerde schijven.  |
|  OperationNotAllowed  |  Virtuele machine '{0}' behoort too'Classic' beschikbaarheidsset '{1}'. Beschikbaarheid van de Hallo Stel toouse 'Uitgelijnd' SKU in en probeer Hallo conversie.  |
|  OperationNotAllowed  |  VM gemaakt op basis van de installatiekopie kan geen BLOBs gebaseerde schijven hebben. Alle schijven hebben toobe beheerd schijven.  |
|  OperationNotAllowed  |  Vastleggen kan niet worden voltooid omdat hello VM niet is gegeneraliseerd.  |
|  OperationNotAllowed  |  Beheerbewerkingen op virtuele machine '{0}' zijn niet toegestaan omdat het VM-schijven worden geconverteerd toomanaged schijven.  |
|  OperationNotAllowed  |  Er een bewerking met het wijzigen van de voedingsstatus van de virtuele Machine {0} too\ {1\}. Voer de bewerking {2} na enige tijd.  |
|  OperationNotAllowed  |  Kan geen tooadd of update hello VM. Hallo aangevraagde VM-grootte {0} mogelijk niet beschikbaar in het bestaande cluster Hallo. Lees meer over VM strategy op https://aka.ms/azure-resizevm vergroten of verkleinen.  |
|  OperationNotAllowed  |  Kan geen tooresize Hallo VM is omdat Hallo grootte {0} aangevraagd niet beschikbaar in Hallo cluster waar Hallo beschikbaarheidsset momenteel is toegewezen. Hallo beschikbare grootten zijn: {1}. Lees meer over VM strategy op https://aka.ms/azure-resizevm vergroten of verkleinen.  |
|  OperationNotAllowed  |  Kan geen tooresize Hallo VM is omdat Hallo grootte {0} aangevraagd niet beschikbaar in Hallo cluster waar hello VM momenteel is toegewezen. uw VM too\ {1\} Neem ongedaan tooresize (dit is Stop-bewerking in hello Azure-portal) en probeer Hallo formaat opnieuw. Lees meer over VM strategy op https://aka.ms/azure-resizevm vergroten of verkleinen.  |
|  OSProvisioningClientError  |  Inrichting van het besturingssysteem is mislukt voor de virtuele machine '{0}' omdat Hallo gastbesturingssysteem momenteel wordt ingericht.  |
|  OSProvisioningClientError  |  Inrichting van het besturingssysteem voor de virtuele machine '{0}' is mislukt. Details van fout: {1} Zorg ervoor dat Hallo installatiekopie juist is voorbereid (gegeneraliseerd). <ul><li>Instructies voor Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  Sleutel genereren voor SSH-host is mislukt. Foutdetails: {0}. tooresolve dit probleem controleren als Linux-agent correct is ingesteld. <ul><li>U kunt controleren Hallo-instructies op: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Gebruikersnaam die is opgegeven voor Hallo dat VM is ongeldig voor deze Linux-distributie. Foutdetails: {0}.  |
|  OSProvisioningInternalError  |  Inrichting van het besturingssysteem is niet voor de virtuele machine '{0}' vanwege tooan interne fout.  |
|  OSProvisioningTimedOut  |  Inrichting van het besturingssysteem voor de virtuele machine '{0}' is niet voltooid binnen de toegewezen tijd Hallo. inrichting mogelijk alsnog voltooien door Hallo VM. Controleer de Inrichtingsstatus later.  |
|  OSProvisioningTimedOut  |  Inrichting van het besturingssysteem voor de virtuele machine '{0}' is niet voltooid binnen de toegewezen tijd Hallo. inrichting mogelijk alsnog voltooien door Hallo VM. Controleer de Inrichtingsstatus later. Controleer ook of de installatiekopie van het Hallo juist is voorbereid (gegeneraliseerd).   <ul><li>Instructies voor Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instructies voor Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  Inrichting van het besturingssysteem voor de virtuele machine '{0}' is niet voltooid binnen de toegewezen tijd Hallo. Hallo VM-gastagent is echter gedetecteerd uitgevoerd. Dit kan erop wijzen Hallo Gast OS is niet juist voorbereid toobe gebruikt als een VM-installatiekopie (CreateOption = FromImage). tooresolve dit probleem beide Hallo Gebruik VHD met CreateOption = koppelen of juist voorbereiden voor gebruik als een installatiekopie:   <ul><li>Instructies voor Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instructies voor Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Hallo vereist VM-grootte is momenteel niet beschikbaar op de locatie Hallo geselecteerd.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  Resource kan niet worden bijgewerkt op dit moment vanwege tooongoing platformupdate. Probeer het later opnieuw.  |
|  StorageAccountLimitation  |  Storage-account {0}' biedt geen ondersteuning voor pagina-blobs die vereist toocreate schijven zijn.  |
|  StorageAccountLimitation  |  Het toegewezen quotum is overschreden voor opslagaccount {0}.  |
|  StorageAccountLocationMismatch  |  Kan het opslagaccount {0} niet omzetten. Zorg ervoor dat het is gemaakt via Hallo Storage Resource Provider Hallo dezelfde locatie als Hallo compute resource.  |
|  StorageAccountNotFound  |  Storage-account {0} is niet gevonden. Zorg ervoor dat de storage-account is niet verwijderd en behoort toohello dezelfde Azure-locatie als Hallo VM.  |
|  StorageAccountNotRecognized  |  Gebruik een opslagaccount worden beheerd door Storage Resource Provider. Gebruik van {0} wordt niet ondersteund.  |
|  StorageAccountOperationInternalError  |  Er is een interne fout opgetreden bij het verkrijgen van toegang tot opslagaccount {0}.  |
|  StorageAccountSubscriptionMismatch  |  Storage-account {0} hoort niet toosubscription {1}.  |
|  StorageAccountTooBusy  |  Storage-account {0} is momenteel bezet. Overweeg het gebruik van een ander account.  |
|  StorageAccountTypeNotSupported  |  Schijf {0} {1} wat een Blob storage-account gebruikt. Probeer het opnieuw met een algemeen opslagaccount.  |
|  StorageAccountTypeNotSupported  |  Storage-account {0} is {1} type. Boot Diagnostics ondersteunt {2} opslagaccounttypen.  |
|  SubscriptionNotAuthorizedForImage  |  Hallo-abonnement is niet gemachtigd.  |
|  TargetDiskBlobAlreadyExists  |  BLOB {0} bestaat al. Geef een andere blob-URI toocreate een nieuwe lege data schijf '{1}'.  |
|  TargetDiskBlobAlreadyExists  |  Vastleggen bewerking kan niet doorgaan omdat de doel-installatiekopie blob {0} bestaat al en Hallo vlag toooverwrite VHD-blobs is niet ingesteld. Verwijderen van Hallo blob of stel Hallo vlag toooverwrite VHD-blobs en probeer opnieuw.  |
|  TargetDiskBlobAlreadyExists  |  De vastlegbewerking kan niet worden voortgezet omdat er een actieve reservering geldt voor de blob {0} voor installatiekopieën.   |
|  TargetDiskBlobAlreadyExists  |  BLOB {0} bestaat al. Geef een andere blob-URI als doel voor schijf '{1}'.  |
|  TooManyVMRedeploymentRequests  |  Te veel aanvragen voor opnieuw implementeren voor de virtuele machine '{0}' is ontvangen of Hallo virtuele machines in dezelfde beschikbaarheidsset als deze virtuele machine Hallo. Probeer het later opnieuw.  |
|  VHDSizeInvalid  |  Hallo opgegeven schijfgrootte van {0} voor schijf '{1}' met blob {2} is ongeldig. Schijfgrootte moet tussen {3} en {4}.  |
|  VMAgentStatusCommunicationError  |  Virtuele machine '{0}' heeft de status voor VM-agent of extensies niet gerapporteerd. Controleer Hallo VM heeft een actieve VM-agent en uitgaande verbindingen tooAzure opslag kunt maken.  |
|  VMArtifactRepositoryInternalError  |  Er is een fout opgetreden tijdens het communiceren met de Hallo artefact opslagplaats tooretrieve VM-artefactgegevens.  |
|  VMArtifactRepositoryInternalError  |  Een interne fout opgetreden bij het ophalen van de VM-artefactgegevens Hallo van Hallo artefactopslagplaats.  |
|  VMExtensionHandlerNonTransientError  |  Handler '{0}' heeft een fout gerapporteerd voor VM-extensie '{1}' met terminal fout code '{2}' en het volgende foutbericht: '{3}'  |
|  VMExtensionManagementInternalError  |  Er is een interne fout opgetreden bij het verwerken van VM-extensie {0}.  |
|  VMExtensionManagementInternalError  |  Meerdere fouten opgetreden tijdens het voorbereiden van Hallo VM-extensies. Zie de weergave van VM-extensie-exemplaar voor meer informatie.  |
|  VMExtensionProvisioningError  |  VM heeft een fout gerapporteerd bij het verwerken van de extensie {0}. Foutbericht weergegeven: '{1}'.  |
|  VMExtensionProvisioningError  |  Meerdere VM-extensies is ingericht op Hallo VM toobe mislukt. Zie de weergave van Hallo VM-extensie-exemplaar voor meer informatie.  |
|  VMExtensionProvisioningTimeout  |  Het inrichten van VM-extensie '{0}' is een time-out. Installatie van de extensie duurt mogelijk te lang of de status van extensie kan niet worden opgehaald.  |
|  VMMarketplaceInvalidInput  |  Maken van een virtuele machine van een niet-Marketplace-installatiekopie is niet nodig Plan informatie, verwijder Hallo plangegevens in Hallo-aanvraag. Naam Besturingssysteemschijf is {0}.  |
|  VMMarketplaceInvalidInput  |  Hallo aankoopgegevens komt niet overeen. Kan geen toodeploy vanuit Hallo Marketplace-installatiekopie. Naam Besturingssysteemschijf is {0}.  |
|  VMMarketplaceInvalidInput  |  Maken van een virtuele machine van de Marketplace-installatiekopie vereist plangegevens in Hallo aanvraag. Naam Besturingssysteemschijf is {0}.  |
|  VMNotFound  |  Hallo-virtuele machine '{0}' is niet gevonden.  |
|  VMRedeploymentFailed  |  VM {0} opnieuw implementeren is mislukt vanwege een interne fout tooan. Probeer het later opnieuw.  |
|  VMRedeploymentTimedOut  |  Opnieuw installeren van de virtuele machine '{0}' is niet op Hallo toegewezen tijd voltooid. Het kan worden voltooid enige tijd opnieuw. Anders kunt u Hallo aanvraag opnieuw proberen.  |
|  VMStartTimedOut  |  Virtuele machine '{0}' is niet gestart in Hallo tijd die is toegewezen. Hallo VM mogelijk alsnog worden gestart. Controleer de energiestatus hello later.  |


## <a name="next-steps"></a>Volgende stappen
Als u meer hulp nodig hebt, kunt u raadplegen hello Azure deskundigen op [MSDN Azure en Stack Overflow-forums Hallo](https://azure.microsoft.com/support/forums/). U kunt ook een incident voor ondersteuning van Azure indienen. Ga toohello [ondersteuning van Azure site](https://azure.microsoft.com/support/options/) en selecteer **ophalen ondersteunen**.
