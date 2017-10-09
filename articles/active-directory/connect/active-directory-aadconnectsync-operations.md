---
title: 'Azure AD Connect-synchronisatie: operationele taken en overwegingen | Microsoft Docs'
description: Dit onderwerp beschrijft operationele taken voor Azure AD Connect-synchronisatie en hoe tooprepare voor de werking van dit onderdeel.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a>Azure AD Connect-synchronisatie: operationele taken en afweging
Hallo-doel van dit onderwerp is toodescribe operationele taken voor Azure AD Connect-synchronisatie.

## <a name="staging-mode"></a>Faseringsmodus
De faseringsmodus kan worden gebruikt voor verschillende scenario's, waaronder:

* Hoge beschikbaarheid.
* Testen en implementeren van nieuwe wijzigingen in de configuratie.
* Introduceert een nieuwe server en uit bedrijf nemen Hallo oude.

Met een server in de faseringsmodus kunt u wijzigingen toohello configuratie en preview Hallo wijzigingen voordat u Hallo-server actief maken. U kunt er ook toorun volledige import en een volledige synchronisatie tooverify dat alle wijzigingen worden verwacht, voordat u deze wijzigingen naar uw productieomgeving.

Tijdens de installatie, selecteert u Hallo server toobe in **faseringsmodus**. Deze actie wordt Hallo-server actief is voor de import en synchronisatie, maar eventuele uitvoer kan niet worden uitgevoerd. Een server in de faseringsmodus is Wachtwoordsynchronisatie of wachtwoord terugschrijven niet actief, zelfs als u deze functies ingeschakeld tijdens de installatie. Wanneer u de faseringsmodus uitschakelt, Hallo-server is, wordt het exporteren wordt gestart, schakelt Wachtwoordsynchronisatie en wachtwoord terugschrijven maakt.

U kunt nog steeds exporteren van een afdwingen met behulp van Hallo synchronisatie servicemanager.

Een server in de faseringsmodus blijft tooreceive wijzigingen van Active Directory en Azure AD. Heeft altijd een kopie van de meest recente wijzigingen Hallo en kunnen zeer snel nemen via Hallo verantwoordelijkheden van een andere server. Als u wijzigingen tooyour primaire configuratieserver maakt, is uw verantwoordelijkheid toomake Hallo dezelfde wijzigingen toohello server in de faseringsmodus.

Voor mensen met kennis van de oudere synchronisatie-technologieën verschilt Hallo faseringsmodus omdat Hallo server een eigen SQL-database heeft. Deze architectuur kunnen Hallo staging-modus server toobe zich in een ander datacenter.

### <a name="verify-hello-configuration-of-a-server"></a>Hallo-configuratie van een server controleren
tooapply deze methode als volgt te werk:

1. [Voorbereiden](#prepare)
2. [Configuratie](#configuration)
3. [Importeren en synchroniseren](#import-and-synchronize)
4. [Controleer of](#verify)
5. [Actieve switchserver](#switch-active-server)

#### <a name="prepare"></a>Voorbereiden
1. Azure AD Connect installeert, selecteert u **faseringsmodus**, en deselecteren **synchronisatie starten** op Hallo laatste pagina van de installatiewizard Hallo. Deze modus kunt u toorun Hallo synchronisatie-engine handmatig.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)
2. Meld u af/aanmeldingsnaam en op Hallo start menu selecteren **synchronisatieservice**.

#### <a name="configuration"></a>Configuratie
Als u aangebrachte wijzigingen toohello primaire server en gewenste toocompare Hallo configuratie Hello staging-server, gebruikt u [documentatie voor Azure AD Connect-configuratie](https://github.com/Microsoft/AADConnectConfigDocumenter).

#### <a name="import-and-synchronize"></a>Importeren en synchroniseren
1. Selecteer **Connectors**, en selecteer eerste Connector is met type Hallo Hallo **Active Directory Domain Services**. Klik op **uitvoeren**, selecteer **volledige import**, en **OK**. Voer deze stappen uit voor alle Connectors van dit type.
2. Selecteer Hallo Connector met het type **Azure Active Directory (Microsoft)**. Klik op **uitvoeren**, selecteer **volledige import**, en **OK**.
3. Zorg ervoor dat Hallo tabblad Connectors nog steeds is geselecteerd. Voor elke Connector met het type **Active Directory Domain Services**, klikt u op **uitvoeren**, selecteer **Deltasynchronisatie**, en **OK**.
4. Selecteer Hallo Connector met het type **Azure Active Directory (Microsoft)**. Klik op **uitvoeren**, selecteer **Deltasynchronisatie**, en **OK**.

U hebt nu gefaseerde export tooAzure AD wijzigingen en on-premises AD (als u hybride implementatie voor Exchange). de volgende stappen Hallo kunnen u tooinspect wat over toochange is voordat u daadwerkelijk Hallo toohello exportmappen.

#### <a name="verify"></a>Verifiëren
1. Start een opdrachtprompt en te gaan`%ProgramFiles%\Microsoft Azure AD Sync\bin`
2. Voer: `csexport "Name of Connector" %temp%\export.xml /f:x` Hallo-naam van Connector Hallo vindt u in de synchronisatieservice. Heeft een naam vergelijkbare too"contoso.com – AAD' voor Azure AD.
3. Hallo PowerShell-script kopiëren van Hallo sectie [CSAnalyzer](#appendix-csanalyzer) tooa-bestand met de naam `csanalyzer.ps1`.
4. Open een PowerShell-venster en blader toohello map waar u de PowerShell-script Hallo hebt gemaakt.
5. Voer: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.
6. U hebt nu een bestand met de naam **processedusers1.csv** die kan worden onderzocht in Microsoft Excel. Alle wijzigingen gefaseerde toobe geëxporteerd tooAzure AD vindt u in dit bestand.
7. Breng wijzigingen toohello gegevens of configuratie en voer deze stappen opnieuw (importeren en synchroniseren en controleer of) pas Hallo wijzigingen die over toobe geëxporteerd zijn worden verwacht.

#### <a name="switch-active-server"></a>Actieve switchserver
1. Op de huidige actieve server Hallo Hallo-server (FIM-DirSync/Azure AD Sync) uitschakelen zodat deze niet tooAzure AD exporteert of stel deze in de faseringsmodus (Azure AD Connect).
2. Hallo-installatiewizard uitgevoerd op Hallo-server in **faseringsmodus** en uitschakelen **faseringsmodus**.
   ![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)

## <a name="disaster-recovery"></a>Herstel na noodgevallen
Deel van Hallo implementatieontwerp is tooplan voor welke toodo als er een ramp optreedt waarbij u Hallo synchronisatieserver verliezen. Er zijn verschillende modellen toouse en welke één toouse is afhankelijk van verschillende factoren, waaronder:

* Wat is de tolerantie voor tooobjects niet wordt kunnen Zorg in Azure AD tijdens Hallo uitvaltijd wijzigt?
* Als u synchronisatie van wachtwoorden, Hallo gebruikers accepteert dat ze toouse Hallo oud wachtwoord in Azure AD hebben als ze deze lokale wijzigen?
* Hebt u een afhankelijkheid op realtime bewerkingen, zoals wachtwoord terugschrijven?

Afhankelijk van Hallo antwoorden toothese vragen en beleid van uw organisatie, kan een van de volgende strategieën Hallo worden geïmplementeerd:

* Opnieuw opbouwen wanneer deze nodig is.
* Een ongebruikte stand-by-server, ook wel **faseringsmodus**.
* Gebruik virtuele machines.

Als u geen Hallo ingebouwde SQL Express-database gebruikt, wordt ook rekening met het Hallo [SQL maximale beschikbaarheid](#sql-high-availability) sectie.

### <a name="rebuild-when-needed"></a>Opnieuw opbouwen wanneer deze nodig is
Een strategie voor een praktische is tooplan voor de server opnieuw opbouwen wanneer deze nodig. Normaal gesproken installeren Hallo synchronisatie-engine en importeren in eerste instantie Hallo en synchronisatie kan worden uitgevoerd binnen een paar uur. Als er niet een vervangende server beschikbaar is, is het mogelijk tootemporarily gebruik een domain controller toohost Hallo synchronisatie-engine.

Hallo synchronisatie-engine-server slaat geen geen status over Hallo objecten zodat Hallo-database kan worden gemaakt van Hallo-gegevens in Active Directory en Azure AD. Hallo **sourceAnchor** kenmerk is gebruikte toojoin Hallo objecten van on-premises en Hallo cloud. Als u opnieuw opbouwen Hallo van server met bestaande objecten on-premises en Hallo cloud, en vervolgens Hallo synchronisatie-engine overeenkomt met deze objecten samen nogmaals op opnieuw installeren. Hallo zaken die u nodig hebt toodocument en opslaan zijn Hallo wijzigingen in configuratie toohello-server, zoals filteren en synchronisatieregels. Deze aangepaste configuraties moeten opnieuw worden toegepast voordat u begint te synchroniseren.

### <a name="have-a-spare-standby-server---staging-mode"></a>Een ongebruikte stand-by-server - faseringsmodus
Als u een meer complexe omgeving hebt, wordt klikt u vervolgens met een of meer stand-by-servers aanbevolen. Tijdens de installatie, kunt u een server toobe in **faseringsmodus**.

Zie voor meer informatie [faseringsmodus](#staging-mode).

### <a name="use-virtual-machines"></a>Gebruik virtuele machines
Een veelvoorkomende en ondersteunde methode is toorun Hallo synchronisatie-engine in een virtuele machine. Als Hallo host een probleem heeft, kan Hallo installatiekopie met de synchronisatieserver engine Hallo gemigreerde tooanother server zijn.

### <a name="sql-high-availability"></a>Hoge beschikbaarheid van SQL
Als u SQL Server Express die wordt geleverd met Azure AD Connect Hallo niet gebruikt, moet vervolgens hoge beschikbaarheid voor SQL Server ook worden overwogen. Hallo hoge beschikbaarheidsoplossingen ondersteund omvatten SQL-clustering en AOA (AlwaysOn-beschikbaarheidsgroepen). Niet-ondersteunde oplossingen bevatten mirroring.

Ondersteuning voor SQL AOA is toegevoegd tooAzure AD verbinden in versie 1.1.524.0. Voordat u Azure AD Connect installeert, moet u SQL AOA inschakelen. Tijdens de installatie van detecteert Azure AD Connect of Hallo opgegeven SQL-exemplaar is ingeschakeld voor SQL AOA. Als SQL AOA is ingeschakeld, wordt Azure AD Connect meer cijfers uit als SQL AOA geconfigureerde toouse synchrone replicatie of asynchrone replicatie is. Bij het instellen van Hallo beschikbaarheidsgroep-Listener, verdient het aanbeveling Hallo RegisterAllProvidersIP eigenschap too0 in te stellen. Dit is omdat Azure AD Connect momenteel SQL Native Client tooconnect tooSQL gebruikt en SQL Native Client biedt geen ondersteuning voor Hallo gebruik van de MultiSubNetFailover-eigenschap.

## <a name="appendix-csanalyzer"></a>Bijlage CSAnalyzer
Zie de sectie Hallo [controleren](#verify) over het toouse dit script.

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have hello basics, go get hello details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a>Volgende stappen
**Overzichtsonderwerpen**  

* [Azure AD Connect-synchronisatie: inzicht en synchronisatie aanpassen](active-directory-aadconnectsync-whatis.md)  
* [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md)  
