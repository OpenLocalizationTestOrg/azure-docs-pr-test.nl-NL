



Afhankelijk van uw omgeving en keuzes kunt Hallo script alle Hallo cluster-infrastructuur, met inbegrip van Hallo virtuele Azure-netwerk, opslagaccounts, cloudservices, domeincontroller, lokale of externe SQL-databases, hoofdknooppunt en extra cluster maken knooppunten. Hallo-script kunt ook vooraf bestaande Azure-infrastructuur gebruiken en maken alleen Hallo HPC clusterknooppunten.

Zie voor achtergrondinformatie over het plannen van een cluster HPC Pack Hallo [productevaluatie en Planning](https://technet.microsoft.com/library/jj899596.aspx) en [aan de slag](https://technet.microsoft.com/library/jj899590.aspx) inhoud in Hallo HPC Pack 2012 R2 TechNet-bibliotheek.

## <a name="prerequisites"></a>Vereisten
* **Azure-abonnement**: U kunt een abonnement in beide hello Azure globale of Azure China-service gebruiken. Uw abonnement limieten van invloed op Hallo aantal en type van clusterknooppunten die u kunt implementeren. Zie voor informatie [Azure-abonnement en Servicelimieten, quota's en beperkingen](../articles/azure-subscription-service-limits.md).
* **Windows-clientcomputer met Azure PowerShell 0.8.10 of hoger geïnstalleerd en geconfigureerd**: Zie [aan de slag met Azure PowerShell](/powershell/azureps-cmdlets-docs) voor installatie-instructies en stappen tooconnect tooyour Azure-abonnement.
* **HPC Pack IaaS-implementatiescript**: downloaden en uitpakken Hallo meest recente versie van script Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Hallo-versie van script Hallo controleren door te voeren `New-HPCIaaSCluster.ps1 –Version`. In dit artikel is gebaseerd op versie 4.5.2 van Hallo-script.
* **Script-configuratiebestand**: Maak een XML-bestand dat Hallo script tooconfigure Hallo HPC-cluster gebruikt. Zie de secties verderop in dit artikel en bestand Manual.rtf die wordt meegestuurd met implementatiescript Hallo Hallo voor informatie over en voorbeelden.

## <a name="syntax"></a>Syntaxis
```PowerShell
New-HPCIaaSCluster.ps1 [-ConfigFile] <String> [-AdminUserName]<String> [[-AdminPassword] <String>] [[-HPCImageName] <String>] [[-LogFile] <String>] [-Force] [-NoCleanOnFailure] [-PSSessionSkipCACheck] [<CommonParameters>]
```
> [!NOTE]
> Hallo-script uitvoeren als beheerder.
> 
> 

### <a name="parameters"></a>Parameters
* **ConfigFile**: Hiermee geeft u het bestandspad Hallo van Hallo configuration file toodescribe Hallo HPC-cluster. Zie voor meer informatie over het Hallo-configuratiebestand in dit onderwerp of in Hallo bestand Manual.rtf in Hallo-map met de Hallo-script.
* **AdminUserName**: Hiermee geeft u de gebruikersnaam Hallo. Als Hallo domein-forest is gemaakt door Hallo script, wordt dit Hallo lokale beheerder zijn gebruikersnaam op voor alle VM's en Hallo beheerder domeinnaam. Als Hallo domein-forest al bestaat, geeft dit Hallo domeingebruiker als lokale beheerder gebruiker naam tooinstall HPC Pack Hallo.
* **AdminPassword**: Hiermee geeft u het wachtwoord van Hallo beheerder. Als het niet is opgegeven in de opdrachtregel hello, vraagt u Hallo script tooinput Hallo wachtwoord.
* **HPCImageName** (optioneel): Hiermee geeft u Hallo HPC Pack VM procesnaam toodeploy Hallo HPC-cluster gebruikt. Het moet de installatiekopie van een opgegeven Microsoft HPC Pack van hello Azure Marketplace. Als niet wordt opgegeven (aanbevolen meestal), Hallo script kiest Hallo laatste gepubliceerd [HPC Pack 2012 R2-afbeelding](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/). meest recente Hallo-installatiekopie is gebaseerd op Windows Server 2012 R2 Datacenter met HPC Pack 2012 R2 Update 3 is geïnstalleerd.
  
  > [!NOTE]
  > Implementatie mislukt als u een geldige afbeelding zijn HPC Pack niet opgeeft.
  > 
  > 
* **LogFile** (optioneel): Hallo implementatie logboekbestandspad bevat. Als niet wordt opgegeven, wordt een logboekbestand gemaakt in de tijdelijke map Hallo van Hallo computer uitvoeren van script Hallo van Hallo-script.
* **Force** (optioneel): alle Hallo bevestiging vragen onderdrukt.
* **NoCleanOnFailure** (optioneel): Hiermee geeft u op dat hello Azure VM's die niet correct is geïmplementeerd, worden niet verwijderd. Deze virtuele machines handmatig te verwijderen voordat u Hallo script toocontinue Hallo-implementatie of Hallo implementatie mislukken.
* **PSSessionSkipCACheck** (optioneel): voor elke cloudservice met virtuele machines die door dit script wordt geïmplementeerd, wordt automatisch een zelfondertekend certificaat gegenereerd door Azure en alle Hallo virtuele machines in de cloudservice Hallo dit certificaat gebruiken als standaard Windows hello Certificaat voor extern beheer (WinRM). toodeploy HPC-functies in deze virtuele Azure-machines, Hallo script standaard, wordt tijdelijk geïnstalleerd deze certificaten in de lokale Computer Hallo\\archief van vertrouwde basiscertificeringsinstanties van Hallo client computer toosuppress Hallo 'geen vertrouwde CA' beveiliging Fout tijdens uitvoering van het script. Hallo-certificaten worden verwijderd wanneer het Hallo-script is voltooid. Als deze parameter wordt opgegeven, Hallo certificaten zijn niet geïnstalleerd op de clientcomputer Hallo en Hallo beveiligingswaarschuwing wordt onderdrukt.
  
  > [!IMPORTANT]
  > Deze parameter wordt niet aanbevolen voor productie-implementaties.
  > 
  > 

### <a name="example"></a>Voorbeeld
Hallo volgende voorbeeld wordt een HPC Pack cluster met behulp van het configuratiebestand *MyConfigFile.xml*, en Hiermee geeft u de beheerdersreferenties voor het installeren van Hallo-cluster.

```PowerShell
.\New-HPCIaaSCluster.ps1 –ConfigFile MyConfigFile.xml -AdminUserName <username> –AdminPassword <password>
```

### <a name="additional-considerations"></a>Aanvullende overwegingen
* Hallo-script kunt optioneel in staat taak verzending via Hallo HPC Pack webportal of Hallo HPC Pack REST-API.
* Hallo-script kunt eventueel aangepaste scripts voor vóór en na configuratie hoofdknooppunt Hallo van uitvoeren als u aanvullende software tooinstall of andere instellingen te configureren.

## <a name="configuration-file"></a>Configuratiebestand
Hallo-configuratiebestand voor het implementatiescript Hallo is een XML-bestand. Hallo-schemabestand HPCIaaSClusterConfig.xsd wordt Hallo HPC Pack IaaS-Implementatiemap script. **IaaSClusterConfig** Hallo-hoofdelement van Hallo-configuratiebestand, waarin Hallo onderliggende elementen in Hallo bestand Manual.rtf in de implementatiemap script Hallo in detail beschreven.

