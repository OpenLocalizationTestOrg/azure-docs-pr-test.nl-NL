---
title: aaaConnect Operations Manager tooLog Analytics | Microsoft Docs
description: toomaintain uw bestaande investeringen in System Center Operations Manager en gebruik uitgebreide mogelijkheden met Log Analytics, kunt u Operations Manager integreren met de OMS-werkruimte.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Verbinding maken met Operations Manager tooLog Analytics
toomaintain uw bestaande investeringen in System Center Operations Manager en gebruik uitgebreide mogelijkheden met Log Analytics, kunt u Operations Manager integreren met de OMS-werkruimte.  Hiermee kunt u gebruikmaken van Hallo-mogelijkheden van OMS terwijl u toouse Operations Manager op:

* Doorgaan met het Hallo-status van uw IT-services met Operations Manager bewaken
* Integratie met uw ITSM oplossingen die incidenten en oplossen van problemen management ondersteunen onderhouden
* Hallo levenscyclus van agents geïmplementeerd tooon-premises en openbare cloud IaaS virtuele machines die u met Operations Manager bewaken beheren

Integratie met System Center Operations Manager voegt waarde tooyour service operations strategie met Hallo sneller en efficiënter OMS in verzamelen, opslaan en analyseren van gegevens uit Operations Manager.  OMS helpt correleer en werk naar Hallo-fouten van problemen te identificeren en op te halen terugkeerpatronen ter ondersteuning van uw bestaande beheerproces van het probleem.   Hallo flexibiliteit van Hallo-engine tooexamine prestaties, gebeurtenis en waarschuwing zoekgegevens, met uitgebreide dashboards en mogelijkheden tooexpose reporting wordt deze gegevens op allerlei zinvolle manieren getoond Hallo sterkte OMS brengt complimenting Operations Manager.

Hallo-agents toohello Operations Manager-beheergroep reporting verzamelt gegevens van uw servers op basis van Hallo Log Analytics-gegevensbronnen en oplossingen die u hebt ingeschakeld in uw abonnement OMS.  Gegevens van deze oplossingen zijn afhankelijk van het Hallo-oplossing die u hebt ingeschakeld, dat hetzij rechtstreeks vanuit een Operations Manager-beheerserver verzonden toohello OMS-webservice, of vanwege Hallo hoeveelheid gegevens die worden verzameld op Hallo agent beheerde computer rechtstreeks worden verzonden van Hallo agent tooOMS-webservice. Hallo-beheerserver stuurt Hallo OMS gegevens rechtstreeks toohello OMS webservice; Deze wordt nooit toohello OperationsManager of OperationsManagerDW-database geschreven.  Wanneer een beheerserver connectiviteit met Hallo OMS-webservice verliest, slaat het Hallo gegevens lokaal tot communicatie opnieuw tot stand gebracht met OMS is.  Als Hallo-beheerserver offline vanwege tooplanned onderhoud of een niet-geplande storing is, hervat een andere beheerserver in beheergroep Hallo connectiviteit met OMS.  

Hallo illustreert volgende diagram Hallo verbinding tussen het Hallo-beheerservers en agents in een System Center Operations Manager-beheergroep en OMS, met inbegrip van Hallo richting en poorten.   

![OMS-operations-manager-integratie-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Als de beleidsregels van uw IT-beveiliging niet toestaan computers op uw netwerk tooconnect toohello Internet dat, kunnen beheerservers geconfigureerde tooconnect toohello OMS Gateway tooreceive configuratie-informatie en verzend de verzamelde gegevens afhankelijk van het Hallo-oplossing u hebt ingeschakeld.  Voor meer informatie en stapsgewijze instructies voor hoe tooconfigure uw Operations Manager management groep toocommunicate via een OMS-Gateway toohello OMS-service, bekijken [verbinding maken met computers tooOMS Hallo OMS-Gateway met](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Systeemvereisten
Controleer voordat u begint, Hallo details tooverify u voldoen aan de vereisten te volgen.

* OMS biedt alleen ondersteuning voor Operations Manager 2016, UR6 van Operations Manager 2012 SP1 en hoger, en UR2 van Operations Manager 2012 R2 en hoger.  Proxyondersteuning is toegevoegd aan Operations Manager 2012 SP1 UR7 en Operations Manager 2012 R2 UR3.
* Alle Operations Manager-agents moeten voldoen aan de vereisten voor minimale ondersteuning. Zorg ervoor dat agents op Hallo minimale update zijn, anders verkeer voor Windows-agent mislukken en veel fouten Hallo Operations Manager-gebeurtenislogboek vullen mogelijk.
* Een OMS-abonnement.  Bekijk voor meer informatie [aan de slag met logboekanalyse](log-analytics-get-started.md).

### <a name="network"></a>Netwerk
Hallo informatie hieronder lijst Hallo proxy- en firewallservers configuratie-informatie voor Operations Manager-agent hello, beheerservers en Operations-console toocommunicate met OMS vereist.  Verkeer van elk onderdeel is uitgaande van uw netwerk toohello OMS-service.     

|Resource | Poortnummer| HTTP-controle overslaan|  
|---------|------|-----------------------|  
|**Agent**|||  
|\*.ods.opinsights.azure.com| 443 |Ja|  
|\*.oms.opinsights.azure.com| 443|Ja|  
|\*.blob.core.windows.net| 443|Ja|  
|\*.azure-automation.net| 443|Ja|  
|**Beheerserver**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Ja|  
|\*.ods.opinsights.azure.com| 443| Ja|  
|*.azure-automation.net | 443| Ja|  
|**Operations Manager-console tooOMS**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 en 443||  
|\*.microsoft.com| 80 en 443||  
|\*.microsoftonline.com| 80 en 443||  
|\*.mms.microsoft.com| 80 en 443||  
|login.windows.net| 80 en 443||  


## <a name="connecting-operations-manager-toooms"></a>Verbinding maken met Operations Manager tooOMS
Hallo reeks stappen tooconfigure na uw Operations Manager management groep tooconnect tooone van uw werkruimten OMS uitvoeren.

1. Selecteer in de Operations Manager-console Hallo Hallo **beheer** werkruimte.
2. Hallo Operations Management Suite knooppunt uitvouwen en klikt u op **verbinding**.
3. Klik op Hallo **tooOperations Management Suite registreren** koppeling.
4. Op Hallo **Wizard Operations Management Suite voorbereiden: verificatie** pagina, Voer Hallo e-mailadres of telefoonnummer en het wachtwoord van Hallo administrator-account dat is gekoppeld aan uw abonnement OMS en op **Meld u aan**.
5. Wanneer u bent geverifieerd, op Hallo **Wizard Operations Management Suite voorbereiden: werkruimte selecteren** pagina worden gevraagd tooselect OMS-werkruimte.  Als u meer dan één werkruimte hebt, selecteer werkruimte die u wilt tooregister met Hallo Operations Manager-beheergroep van Hallo vervolgkeuzelijst en klik vervolgens op Hallo **volgende**.
   
   > [!NOTE]
   > Operations Manager ondersteunt slechts één OMS-werkruimte tegelijk. Hallo-verbinding en Hallo-computers die geregistreerd tooOMS met Hallo vorige werkruimte zijn worden verwijderd van OMS.
   > 
   > 
6. Op Hallo **Wizard Operations Management Suite voorbereiden: Samenvatting** pagina, bevestig de instellingen en als ze juist zijn, klikt u op **maken**.
7. Op Hallo **Wizard Operations Management Suite voorbereiden: voltooien** pagina, klikt u op **sluiten**.

### <a name="add-agent-managed-computers"></a>Door agents beheerde computers toevoegen
Na het configureren van integratie met de OMS-werkruimte, dit alleen verbinding maakt met een OMS, geen gegevens verzameld van Hallo agents reporting tooyour-beheergroep. Dit zal niet worden uitgevoerd totdat nadat u hebt geconfigureerd welke specifieke door agents beheerde computers worden gegevens verzameld voor logboekanalyse. U kunt de computerobjecten Hallo afzonderlijk selecteren of u een groep met objecten voor Windows-computer kunt selecteren. U kunt een groep met exemplaren van een andere klasse, zoals logische schijven of SQL-databases niet selecteren.

1. Open Hallo Operations Manager-console en selecteer Hallo **beheer** werkruimte.
2. Hallo Operations Management Suite knooppunt uitvouwen en klikt u op **verbinding**.
3. Klik op Hallo **een computergroep toevoegen** koppeling onder Hallo acties kop op Hallo aan de rechterkant van Hallo deelvenster.
4. In Hallo **Computer zoeken** in het dialoogvenster dat u kunt zoeken naar computers of groepen die worden bewaakt door Operations Manager. Selecteer computers of groepen tooonboard tooOMS, klik op **toevoegen**, en klik vervolgens op **OK**.

U kunt computers weergeven en groepen toocollect gegevens vanuit het knooppunt van de Hallo beheerde Computers onder Operations Management Suite geconfigureerd in Hallo **beheer** werkruimte van Hallo Operations-console.  Hier kunt u toevoegen of verwijderen van computers en groepen indien nodig.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>OMS proxy-instellingen configureren in de Operations-console Hallo
Volgende stappen uit als een interne proxyserver tussen de beheergroep Hallo en OMS-webservice is Hallo uitvoeren.  Deze instellingen worden centraal beheerd vanuit het Hallo-beheergroep en gedistribueerde tooagent beheerde systemen die zijn opgenomen in Hallo bereik toocollect gegevens voor OMS.  Dit is nuttig voor wanneer bepaalde oplossingen overslaan Hallo management server- en verzenden gegevens rechtstreeks tooOMS-webservice.

1. Open Hallo Operations Manager-console en selecteer Hallo **beheer** werkruimte.
2. Vouw Operations Management Suite en klik vervolgens op **verbindingen**.
3. In Hallo OMS verbinding weergeven, klikt u op **proxyserver configureren**.
4. Op **Wizard Operations Management Suite: proxyserver** pagina **gebruik van een proxy server tooaccess Hallo Operations Management Suite**, en typ vervolgens de URL Hallo met Hallo poortnummer, bijvoorbeeld http:// corpproxy:80 en klik vervolgens op **voltooien**.

Als de proxyserver verificatie vereist, voert u Hallo volgende stappen uit tooconfigure referenties en instellingen die u moet toopropagate toomanaged computers die tooOMS in de beheergroep Hallo rapporteert.

1. Open Hallo Operations Manager-console en selecteer Hallo **beheer** werkruimte.
2. Selecteer onder **RunAs-configuratie** de optie **Profielen**.
3. Open Hallo **Proxy System Center Advisor uitvoeren als-profiel** profiel.
4. In de Wizard Run As-profiel hello, klikt u op toevoegen toouse uitvoeren als-account. Kunt u een [Run As-account](https://technet.microsoft.com/library/hh321655.aspx) of een bestaand account gebruiken. Dit account moet voldoende machtigingen toopass toohave via Hallo proxyserver.
5. tooset account toomanage hello, kiest u **een geselecteerde klasse, groep of object**, klikt u op **selecteren...** en klik vervolgens op **groep...** Hallo tooopen **groep zoeken** vak.
6. Zoek en selecteer vervolgens **Microsoft System Center Advisor Monitoring Server-groep**.  Klik op **OK** na het selecteren van Hallo groep tooclose hello **groep zoeken** vak.
7. Klik op **OK** tooclose hello **een Run As-account toevoegen** vak.
8. Klik op **opslaan** toocomplete wizard Hallo en sla de wijzigingen.

Nadat het Hallo-verbinding is gemaakt en u configureren welke agents verzamelt en rapporteert gegevens tooOMS, is hello volgende configuratie toegepast in de beheergroep hello, niet per se in volgorde:

* Hallo Run As-Account **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** wordt gemaakt.  Het is gekoppeld aan Hallo Run As-profiel **Microsoft System Center Advisor uitvoeren als-profiel Blob** en is gemaakt voor twee klassen - **Verzamelingserver** en **Operations Manager-beheergroep** .
* Twee connectors worden gemaakt.  Hallo eerst heet **Microsoft.SystemCenter.Advisor.DataConnector** en wordt automatisch geconfigureerd met een abonnement dat u alle waarschuwingen gegenereerd op basis van exemplaren van alle klassen in Hallo management groep tooOMS logboek verzendt Analytics. de tweede connector Hallo is **Advisor Connector**, die verantwoordelijk is voor communicatie met OMS-webservice en delen van gegevens.
* Agents en groepen die u toocollect gegevens hebt geselecteerd in de beheergroep Hallo toegevoegd toohello **Microsoft System Center Advisor Monitoring Server-groep**.

## <a name="management-pack-updates"></a>Management pack-updates
Nadat de configuratie is voltooid, maakt Hallo Operations Manager-beheergroep verbinding met een Hallo OMS-service.  Hallo beheerserver synchroniseert met de webservice Hallo en informatie over de bijgewerkte configuratie ontvangen in de vorm Hallo van management packs voor u hebt ingeschakeld Hallo-oplossingen die zijn geïntegreerd met Operations Manager.   Operations Manager wordt gecontroleerd op updates van deze management packs en automatisch downloaden en importeert wanneer ze beschikbaar.  Er zijn twee regels in het bijzonder die dit gedrag beheren:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -Updates Hallo base OMS management packs. Standaard wordt elke 12 uur uitgevoerd.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** -oplossing management packs is ingeschakeld in uw werkruimte-Updates. Wordt standaard uitgevoerd om minuten vijf (5).

U kunt deze twee regels tooeither automatisch downloaden voorkomen door het uitschakelen van deze overschrijven of wijzigen Hallo frequentie voor hoe vaak hello beheerserver met OMS toodetermine synchroniseert als een nieuw management pack beschikbaar is en moet worden gedownload.  Volg de stappen Hallo [hoe tooOverride een regel of Monitor](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **frequentie** parameter met een waarde in seconden toochange Hallo Synchronisatieplanning of Hallo wijzigen **ingeschakeld**  parameter toodisable Hallo regels.  Doel Hallo overschrijft tooall objecten van klasse Operations Manager-beheergroep.

Als u toocontinue gevolgd door uw bestaande wijziging besturingselement proces wilt voor het beheren van management Packs in uw productiebeheergroep, kunt u regels voor Hallo uitschakelen en inschakelen ze specifieke tijdstippen waarop updates zijn toegestaan. Als u een ontwikkelings- of QA-beheergroep in uw omgeving hebt en deze connectiviteit toohello Internet heeft, kunt u die beheergroep configureren met een OMS-werkruimte toosupport dit scenario.  Hiermee kunt u tooreview en Hallo iteratieve releases van Hallo OMS management packs evalueren voordat ze in uw productiebeheergroep zijn vrijgegeven.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Overschakelen van een groep Operations Manager tooa nieuwe OMS-werkruimte
1. Meld u bij tooyour OMS-abonnement en maak een werkruimte in [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Open Hallo Operations Manager-console met een account dat lid is van Hallo Administrators in Operations Manager-functie en selecteer Hallo **beheer** werkruimte.
3. Vouw Operations Management Suite en selecteer **verbindingen**.
4. Selecteer Hallo **bewerking Management Suite opnieuw configureren** koppeling Hallo midden-zijde van Hallo deelvenster.
5. Ga als volgt Hallo **Wizard Operations Management Suite voorbereiden** en Voer Hallo e-mailadres of telefoonnummer getal en het wachtwoord van Hallo administrator-account dat is gekoppeld aan uw nieuwe OMS-werkruimte.
   
   > [!NOTE]
   > Hallo **Wizard Operations Management Suite voorbereiden: werkruimte selecteren** pagina geeft Hallo bestaande werkruimte die wordt gebruikt.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Integratie van Operations Manager met OMS valideren
Er zijn een aantal verschillende manieren kunt u controleren of uw OMS tooOperations Manager integratie is geslaagd.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>tooconfirm integratie van Hallo OMS-portal
1. Klik in het Hallo-OMS-portal op Hallo **instellingen** tegel
2. Selecteer **verbonden gegevensbronnen**.
3. U ziet in de tabel Hallo onder Hallo System Center Operations Manager sectie, Hallo-naam van beheergroep Hallo vermeld met Hallo aantal agents en status wanneer deze gegevens voor het laatst is ontvangen.
   
   ![OMS-instellingen-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Opmerking Hallo **werkruimte-ID** waarde onder Hallo aan de linkerkant van de pagina instellingen Hallo.  U te valideren op basis van uw beheergroep Operations Manager.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>integratie van Operations-console Hallo tooconfirm
1. Open Hallo Operations Manager-console en selecteer Hallo **beheer** werkruimte.
2. Selecteer **Management Packs** en in Hallo **zoekt u naar:** vak teksttype **Advisor** of **Intelligence**.
3. Afhankelijk van het Hallo-oplossingen die u hebt ingeschakeld, ziet u een overeenkomstige management pack weergegeven in zoekresultaten Hallo.  Bijvoorbeeld, als u Hallo waarschuwing beheeroplossing hebt ingeschakeld, is Hallo management pack voor Microsoft System Center Advisor waarschuwing Management in Hallo-lijst.
4. Van Hallo **bewaking** bekijken, navigeert u toohello **Operations Management Suite\Health status** weergeven.  Selecteer een beheerserver onder Hallo **status van beheerservers** deelvenster en in Hallo **detailweergave** deelvenster Hallo-waarde voor eigenschap controleren **URI verificatieservice** komt overeen met de Hallo OMS-werkruimte-ID.
   
   ![OMS-opsmgr-mg-authsvcuri-Property-MS](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Integratie met OMS verwijderen
Wanneer u integratie tussen uw Operations Manager-beheergroep en de OMS-werkruimte niet meer nodig hebt, zijn er meerdere stappen die nodig zijn tooproperly verwijderen Hallo verbinding en -configuratie in Hallo-beheergroep. Hallo moet volgende procedure u de OMS-werkruimte bijwerken door Hallo verwijzing van uw beheergroep te verwijderen, verwijder Hallo OMS-connectors en verwijder vervolgens beheerpakketten ondersteunende OMS.   

Management packs voor u hebt ingeschakeld Hallo-oplossingen die zijn geïntegreerd met Operations Manager en Hallo management packs vereist toosupport integratie met Hallo OMS-service kan niet eenvoudig worden verwijderd uit de beheergroep Hallo.  Dit komt omdat sommige van Hallo OMS management packs afhankelijk van andere gerelateerde management packs zijn.  toodelete management packs met een afhankelijkheid van andere management packs downloaden Hallo script [verwijderen van een management pack met afhankelijkheden](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) van TechNet Script Center.  

1. Open Operations Manager-opdrachtshell Hallo met een account dat lid is van de rol van Operations Manager-beheerders Hallo.
   
    > [!WARNING]
    > Controleer of u hebt geen aangepaste management packs die Hallo woord Advisor of IntelligencePack in Hallo naam voordat u doorgaat, anders Hallo stappen te volgen verwijderen uit de beheergroep Hallo.
    > 

2. Hallo opdrachtprompt, typ`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Volgende type`Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. tooremove management packs resterende die een afhankelijkheid hebben van andere System Center Advisor-management packs, gebruikt u Hallo script *RecursiveRemove.ps1* u hebt gedownload van TechNet Script Center Hallo eerder.  
 
    > [!NOTE]
    > Hallo Microsoft System Center Advisor of Microsoft System Center Advisor interne management packs niet verwijderen.  
    >  

5. Open Hallo Operations Manager, Operations-console met een account dat lid is van de rol van Operations Manager-beheerders Hallo.
6. Onder **beheer**, selecteer Hallo **Management Packs** knooppunt en in Hallo **zoekt u naar:** in het vak **Advisor** en controleer of Hallo volgende management packs zijn nog steeds in de beheergroep geïmporteerd:
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor interne
7. Klik in het Hallo-OMS-portal op Hallo **instellingen** tegel.
8. Selecteer **verbonden gegevensbronnen**.
9. In de tabel Hallo onder Hallo System Center Operations Manager sectie, ziet u Hallo naam van beheergroep Hallo gewenste tooremove uit Hallo-werkruimte.  Onder de kolom Hallo **laatste gegevens**, klikt u op **verwijderen**.  
   
    > [!NOTE]
    > Hallo **verwijderen** koppeling wordt pas beschikbaar nadat het is 14 dagen als er geen activiteit gedetecteerd op basis van de verbonden beheergroep Hallo.  
    > 

10. Een venster weergegeven waarin u wordt gevraagd tooconfirm dat u wilt dat tooproceed Hallo verwijdering.  Klik op **Ja** tooproceed. 

toodelete Hallo twee connectors - Microsoft.SystemCenter.Advisor.DataConnector en Advisor Connector, PowerShell-script Hallo hieronder tooyour computer opslaan en uitvoeren met behulp van Hallo volgen voorbeelden:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> Hallo computer u dit script uit als dit niet een beheerserver hebt Hallo Operations Manager-opdrachtshell, afhankelijk van Hallo-versie van uw beheergroep zijn geïnstalleerd.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

In toekomstige Hallo als u van plan bent opnieuw verbinding te maken van uw management groep tooan OMS-werkruimte, moet u toore importeren Hallo `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` management pack-bestand van de meest recente updatepakket Hallo tooyour beheergroep toegepast.  U kunt dit bestand vinden in Hallo `%ProgramFiles%\Microsoft System Center 2012` of Hallo `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` map.

## <a name="next-steps"></a>Volgende stappen
tooadd functionaliteit en verzamelen gegevens, Zie [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).


