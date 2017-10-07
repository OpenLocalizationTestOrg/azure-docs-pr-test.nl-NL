---
title: aaaConnect Windows-computers tooAzure Log Analytics | Microsoft Docs
description: Dit artikel ziet Hallo stappen tooconnect Hallo Windows-computers in uw lokale infrastructuur toohello Log Analytics-service met behulp van een aangepaste versie van Microsoft Monitoring Agent (MMA) Hallo.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Verbinding maken met Windows-computers toohello Log Analytics-service in Azure

In dit artikel bevat de stappen Hallo tooconnect Windows-computers in uw lokale infrastructuur tooOMS werkruimten met behulp van een aangepaste versie van Microsoft Monitoring Agent (MMA) Hallo. U moet tooinstall en verbinding maken met agents voor alle Hallo computers die u wilt tooonboard zodat ze toosend data toohello Log Analytics-service en tooview en act van die gegevens. Elke agent kan toomultiple werkruimten rapporteren.

U kunt met behulp van de installatie vanaf de opdrachtregel, agents installeren of met Desired State Configuration (DSC) in Azure Automation.  

>[!NOTE]
Voor virtuele machines in Azure wordt uitgevoerd, kunt u de installatie vereenvoudigen met behulp van Hallo [extensie van virtuele machine](log-analytics-azure-vm-extension.md).

Hallo-agent gebruikt op computers met een internetverbinding, Hallo verbinding toohello Internet toosend gegevens tooOMS. Voor computers die u geen verbinding met Internet hebt, kunt u een proxy of Hallo [OMS Gateway](log-analytics-oms-gateway.md).

Verbinding maken met uw Windows-computers tooOMS is eenvoudig met behulp van de drie eenvoudige stappen:

1. Hallo agent setup-bestand downloaden van Hallo OMS-portal
2. Hallo agent installeren met Hallo methode die u kiest
3. Hallo-agent configureren of het toevoegen van extra werkruimten, indien nodig

Hallo volgende diagram toont Hallo relatie tussen uw Windows-computers en OMS nadat u hebt geïnstalleerd en geconfigureerd agents.

![OMS-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Als de beleidsregels van uw IT-beveiliging niet toestaan computers op uw netwerk tooconnect toohello Internet dat, kunt u uw computers tooconnect toohello OMS-Gateway configureren. Voor meer informatie en stapsgewijze instructies voor hoe tooconfigure uw toocommunicate servers via een OMS-Gateway toohello OMS-service, bekijken [verbinding maken met computers tooOMS Hallo OMS-Gateway met](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Systeemvereisten en de vereiste configuratie
Voordat u installeert of agents te implementeren, controleert u Hallo details tooensure u voldoet aan de vereisten hello te volgen.

- U kunt alleen Hallo OMS MMA installeren op computers met Windows Server 2008 SP 1 of hoger of Windows 7 SP1 of hoger.
- U moet een Azure-abonnement.  Zie voor meer informatie [aan de slag met logboekanalyse](log-analytics-get-started.md).
- Elke computer met Windows moet kunnen tooconnect toohello Internet met behulp van HTTPS- of toohello OMS-Gateway. Deze verbinding kan worden direct, via een proxy of via Hallo OMS-Gateway.
- U kunt Hallo OMS MMA installeren op zelfstandige computers, servers en virtuele machines. Als u tooconnect Azure gehoste virtuele machines tooOMS wilt, Zie [verbinding maken met Azure virtuele machines tooLog Analytics](log-analytics-azure-vm-extension.md).
- Hallo-agent moet toouse TCP-poort 443 voor verschillende bronnen.

### <a name="network"></a>Netwerk

Voor Windows-agents tooconnect tooand registreren met Hallo OMS-service, moeten ze toegang toonetwork bronnen, met inbegrip van poortnummers Hallo en domein-URL's hebben.

- Proxy-servers moet u tooensure die Hallo juiste proxyserver resources zijn geconfigureerd in instellingen voor de agent.
- Voor firewalls die toegang toohello Internet beperken, moeten u of uw netwerken engineers tooconfigure uw firewall toopermit toegang tooOMS. De agent-instellingen hoeven niet te worden aangepast.

Hallo volgende tabel ziet u bronnen die nodig zijn voor communicatie.

>[!NOTE]
>Aantal Hallo na bronnen vermeld operationeel inzicht, waarop een vorige naam op voor logboekanalyse is.

| Agentresource | Poorten | HTTPS-controle overslaan |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Ja |
| *.oms.opinsights.azure.com | 443 | Ja |
| *.blob.core.windows.net | 443 | Ja |
| *.azure-automation.net | 443 | Ja |



## <a name="download-hello-agent-setup-file-from-oms"></a>Hallo agent setup-bestand downloaden van OMS
1. In Hallo OMS-portal op Hallo **overzicht** pagina, klikt u op Hallo **instellingen** tegel.  Klik op Hallo **verbonden bronnen** Hallo boven op tabblad.  
    ![Tabblad verbonden bronnen](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Klik op **Windows-Servers** en klik vervolgens op **Windows-Agent downloaden** toepasselijke tooyour computer processor type toodownload Hallo setup-bestand.
3. Op Hallo van **werkruimte-ID**en klik op de pictogram kopiëren Hallo Hallo-ID in Kladblok plakken.
4. Op Hallo van **primaire sleutel**, klik op de pictogram kopiëren Hallo en Hallo-sleutel in Kladblok plakken.     

## <a name="install-hello-agent-using-setup"></a>Hallo agent installeren met setup
1. Setup tooinstall Hallo agent uitvoeren op een computer die u toomanage wilt.
2. Klik op de welkomstpagina Hallo **volgende**.
3. Lees de licentiebepalingen Hallo op de pagina licentievoorwaarden hello, en klik vervolgens op **ik ga akkoord**.
4. Op Hallo doelmap pagina wijzigen of de standaardinstallatiemap Hallo houden en klik vervolgens op **volgende**.
5. Op Hallo installatieopties voor Agent pagina tooconnect Hallo agent tooAzure logboekanalyse (OMS), Operations Manager, kunt u of u kunt Hallo keuzes leeg laten als u wilt dat tooconfigure Hallo agent later. Klik op **Volgende**.   
    - Als u kiest tooconnect tooAzure logboekanalyse (OMS), plak Hallo **werkruimte-ID** en **Werkruimtesleutel (primaire sleutel)** die u in de vorige procedure Hallo in Kladblok hebt gekopieerd en klik vervolgens op  **Volgende**.  
        ![Werkruimte-ID en Primary Key plakken](./media/log-analytics-windows-agents/connect-workspace.png)
    - Als u tooconnect tooOperations Manager hebt gekozen, typt u Hallo **Beheergroepsnaam**, **beheerserver** naam, en **Beheerserverpoort**, en klik vervolgens op **Volgende**. Kies op Hallo Agentactieacount pagina Hallo lokale systeemaccount of een lokale account en klik vervolgens op **volgende**.  
        ![beheergroepconfiguratie](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![actie-account van agent](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Controleer uw selecties op Hallo gereed tooInstall pagina en klik vervolgens op **installeren**.
7. Pagina op Hallo configuratie is voltooid, klikt u op **voltooien**.
8. Als u klaar Hallo **Microsoft Monitoring Agent** wordt weergegeven in **Configuratiescherm**. U kunt uw configuratie er bekijken en controleren dat die Hallo-agent is verbonden tooOperational Insights (OMS). Wanneer verbonden tooOMS Hallo agent wordt een bericht weergegeven: **Hallo Microsoft Monitoring Agent verbonden is toohello Microsoft Operations Management Suite-service.**

## <a name="configure-proxy-settings"></a>Proxy-instellingen configureren

U kunt volgen procedure tooconfigure proxy-instellingen voor Microsoft Monitoring Agent via het Configuratiescherm Hallo Hallo gebruiken. U moet deze procedure toouse voor elke server. Als u een groot aantal servers dat u tooconfigure nodig hebt, vindt u het misschien gemakkelijker toouse een script tooautomate dit proces. Als dit het geval is, raadpleegt u de volgende procedure Hallo [tooconfigure proxy-instellingen voor Microsoft Monitoring Agent met een script Hallo](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>tooconfigure proxy-instellingen voor Hallo Microsoft Monitoring Agent via het Configuratiescherm
1. Open het **Configuratiescherm**.
2. Open **Microsoft Monitoring Agent**.
3. Klik op Hallo **Proxy-instellingen** tabblad.  
    ![tabblad proxyinstellingen](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Selecteer **een proxyserver gebruiken** en typ Hallo-URL en het poortnummer, indien nodig, vergelijkbaar toohello voorbeeld. Als de proxyserver verificatie vereist, typt u Hallo gebruikersnaam en wachtwoord tooaccess Hallo proxyserver.


### <a name="verify-agent-connectivity-toooms"></a>Controleer of de agent-connectiviteit tooOMS

U kunt eenvoudig controleren of uw agents communiceert Hallo procedure te volgen met OMS:

1.  Open het Configuratiescherm op Hallo-computer met Windows-agent Hallo.
2.  Open Microsoft Monitoring Agent.
3.  Klik op tabblad van hello Azure logboekanalyse (OMS).
4.  U ziet in de kolom Status Hallo dat die Hallo-agent is verbonden met succes toohello Operations Management Suite-service.

![Agent verbonden](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>tooconfigure proxy-instellingen voor Hallo Microsoft Monitoring Agent met een script
Kopieer Hallo volgende steekproef, bijwerken met specifieke tooyour omgeving, sla het bestand met extensie PS1 en vervolgens Hallo-script uitvoeren op elke computer die verbinding rechtstreeks toohello OMS-service maakt.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Hallo agent installeren met Hallo vanaf de opdrachtregel
- Wijzigen en gebruik vervolgens Hallo voorbeeld tooinstall Hallo agent via de opdrachtregel hello te volgen. Hallo-voorbeeld wordt een volledig stille installatie uitgevoerd.

    >[!NOTE]
    Als u een agent tooupgrade wilt, moet u toouse Hallo logboekanalyse scripting API. Zie Hallo volgende sectie tooupgrade een agent.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

Hallo agent IExpress gebruikt als de zelfstandig uitpakken met Hallo `/c` opdracht. U kunt opdrachtregelopties op Hallo zien [opdrachtregelopties voor IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) en vervolgens update Hallo voorbeeld toosuit uw behoeften.

|MMA-specifieke opties                   |Opmerkingen         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = configureren Hallo agent tooreport tooa werkruimte                |
|OPINSIGHTS_WORKSPACE_ID                | Werkruimte-Id (guid) voor Hallo werkruimte tooadd                    |
|OPINSIGHTS_WORKSPACE_KEY               | Werkruimte sleutel gebruikte tooinitially verifiëren met Hallo-werkruimte |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Geef Hallo cloud-omgeving waar Hallo werkruimte zich bevindt <br> 0 = azure commerciële cloudservice (standaard) <br> 1 = azure Government |
|OPINSIGHTS_PROXY_URL               | URI voor Hallo proxy toouse |
|OPINSIGHTS_PROXY_USERNAME               | Gebruikersnaam tooaccess een geverifieerde proxyserver |
|OPINSIGHTS_PROXY_PASSWORD               | Wachtwoord tooaccess een geverifieerde proxyserver |

>[!NOTE]
tooavoid roept Hallo opdrachtregelprogramma lengtelimiet van IExpress, Hallo-agent installeren met geen werkruimte geconfigureerd en gebruik vervolgens de configuratie van een script tooset voor Hallo-werkruimte.

>[!NOTE]
Als u krijgt een `Command line option syntax error.` bij gebruik van Hallo `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, kunt u Hallo volgende tijdelijke oplossing:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Een werkruimte met een script toevoegen
Toevoegen van een werkruimte Hallo logboekanalyse agent scripting API gebruiken met Hallo voorbeeld te volgen:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd een werkruimte in Azure voor US Government, gebruik Hallo voorbeeldscript te volgen:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Als u hebt gebruikt Hallo vanaf de opdrachtregel of eerder tooinstall script of Hallo-agent configureren `EnableAzureOperationalInsights` is vervangen door `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Hallo agent installeren met DSC in Azure Automation

U kunt Hallo script voorbeeld tooinstall Hallo agent met behulp van DSC in Azure Automation te volgen. Hallo-voorbeeld installeert de 64-bits agent, geïdentificeerd door Hallo Hallo `URI` waarde. U kunt ook Hallo 32-bits versie door te vervangen Hallo URI-waarde. Hallo URI's voor beide versies zijn:

- Windows 64-bits agent - https://go.microsoft.com/fwlink/?LinkId=828603
- Windows 32-bits agent - https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
In dit voorbeeld procedure en het script wordt een bestaand agent niet bijgewerkt.

1. Hallo xPSDesiredStateConfiguration DSC-Module importeren uit [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) in Azure Automation.  
2.  Maken van Azure Automation-variabele assets voor *OPSINSIGHTS_WS_ID* en *OPSINSIGHTS_WS_KEY*. Stel *OPSINSIGHTS_WS_ID* tooyour logboekanalyse OMS-werkruimte-ID en stel *OPSINSIGHTS_WS_KEY* toohello primaire sleutel van uw werkruimte.
3.  Hallo volgende script en sla deze op als MMAgent.ps1 gebruiken
4.  Wijzigen en gebruik vervolgens Hallo voorbeeld tooinstall Hallo agent met behulp van DSC in Azure Automation te volgen. MMAgent.ps1 in Azure Automation importeren met behulp van hello Azure Automation-interface of de cmdlet.
5.  De configuratie van een knooppunt toohello toewijzen. Hallo knooppunt controleert de configuratie en Hallo MMA wordt doorgeschoven, toohello knooppunt binnen 15 minuten.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Hallo laatste ProductId waarde ophalen

Hallo `ProductId value` in Hallo MMAgent.ps1 script unieke tooeach agent-versie is. Wanneer een bijgewerkte versie van elke agent wordt gepubliceerd, verandert de Hallo-product-id-waarde. Wanneer Hallo ProductId wordt gewijzigd in toekomstige hello, kunt u dus Hallo agent-versie met een eenvoudige script vinden. Nadat u Hallo nieuwste agentversie is geïnstalleerd op een testserver hebt, kunt u Hallo Scriptwaarde tooget hello geïnstalleerd ProductId te volgen. Hallo laatste ProductId waarde kunt u Hallo-waarde in Hallo MMAgent.ps1 script bijwerken.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Een agent handmatig configureren of extra werkruimten toevoegen
Als u agents hebt geïnstalleerd, maar kon niet configureren of als u wilt dat Hallo agent tooreport toomultiple werkruimten, kunt u deze kunt gebruiken Hallo informatie tooenable een agent te volgen of configureer het opnieuw. Nadat u de agent Hallo hebt geconfigureerd, worden geregistreerd bij Hallo agent-service en krijgen de vereiste configuratiegegevens en management packs die oplossingsgegevens bevatten.

1. Nadat u Hallo Microsoft Monitoring Agent hebt geïnstalleerd, opent u **Configuratiescherm**.
2. Open **Microsoft Monitoring Agent** en klik vervolgens op Hallo **Azure logboekanalyse (OMS)** tabblad.   
3. Klik op **toevoegen** tooopen hello **Log Analytics-werkruimte toevoegen** vak.
4. Plakken Hallo **werkruimte-ID** en **Werkruimtesleutel (primaire sleutel)** dat u hebt gekopieerd in Kladblok in een eerdere procedure voor Hallo werkruimte wilt tooadd uit te voeren en klik vervolgens op **OK**.  
    ![Configureer operationeel inzicht](./media/log-analytics-windows-agents/add-workspace.png)

Nadat gegevens worden verzameld van computers die worden bewaakt door Hallo-agent, het aantal computers worden bewaakt door OMS Hallo verschijnen in Hallo OMS-portal op Hallo **verbonden bronnen** tabblad **instellingen** als  **Servers die zijn verbonden**.


## <a name="toodisable-an-agent"></a>toodisable een agent
1. Open na de installatie van agent Hallo **Configuratiescherm**.
2. Microsoft Monitoring Agent te openen en klik vervolgens op Hallo **Azure logboekanalyse (OMS)** tabblad.
3. Selecteer een werkruimte en klik vervolgens op **verwijderen**. Herhaal deze stap voor alle andere werkruimten.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>Configureer desgewenst agents tooreport tooan Operations Manager-beheergroep

Als u Operations Manager in uw IT-infrastructuur, kunt u ook Hallo MMA agent gebruiken als een Operations Manager-agent.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>tooconfigure MMA agents tooreport tooan Operations Manager-beheergroep
1.  Open op Hallo-computer waarop Hallo-agent is geïnstalleerd, **Configuratiescherm**.  
2.  Open **Microsoft Monitoring Agent** en klik vervolgens op Hallo **Operations Manager** tabblad.  
    ![Microsoft Monitoring Agent Operations Manager-tabblad](./media/log-analytics-windows-agents/om-mg01.png)
3.  Als uw Operations Manager-servers integratie met Active Directory hebt, klikt u op **automatisch bijwerken van beheergroeptoewijzingen van AD DS**.
4.  Klik op **toevoegen** tooopen hello **toevoegen van een beheergroep** in het dialoogvenster.  
    ![Microsoft Monitoring Agent een beheergroep toevoegen](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  In **beheergroepsnaam** vak, type Hallo-naam van uw beheergroep.
6.  In Hallo **primaire beheerserver** vak, typ de computernaam van de primaire beheerserver Hallo Hallo.
7.  In Hallo **beheerserverpoort** vak type Hallo TCP-poortnummer.
8.  Onder **Agentactieacount**, kies Hallo lokale systeemaccount of een lokale account.
9.  Klik op **OK** tooclose hello **toevoegen van een beheergroep** in het dialoogvenster en klik vervolgens op **OK** tooclose hello **Microsoft Monitoring Agenteigenschappen**in het dialoogvenster.


## <a name="next-steps"></a>Volgende stappen

- [Log Analytics-oplossingen van Hallo oplossingen galerie toevoegen](log-analytics-add-solutions.md) tooadd functionaliteit en verzamelen gegevens.
