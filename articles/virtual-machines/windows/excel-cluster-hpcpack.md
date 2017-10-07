---
title: aaaHPC Pack voor Excel en SOA-cluster | Microsoft Docs
description: Aan de slag grootschalige workloads voor Excel- en SOA-uitgevoerd op een HPC Pack-cluster in Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a>Excel- en SOA-belastingen uitgevoerd op een HPC Pack-cluster in Azure aan de slag
Dit artikel laat zien hoe toodeploy een Microsoft HPC Pack 2012 R2-cluster op virtuele machines in Azure met behulp van een Azure quickstart-sjabloon of desgewenst een Azure PowerShell-script voor implementatie. Hallo-cluster maakt gebruik van virtuele machine in Azure Marketplace-installatiekopieën ontworpen toorun Microsoft Excel of service oriented architecture (SOA) werkbelastingen met HPC Pack. U kunt Hallo cluster toorun Excel HPC en SOA-services van een on-premises clientcomputer gebruiken. Hallo Excel HPC-services bevatten Excel-werkmap offloading en de gebruiker gedefinieerde functies van Excel of de UDF's.

> [!IMPORTANT] 
> In dit artikel is gebaseerd op de functies, sjablonen en scripts voor HPC Pack 2012 R2. Dit scenario is momenteel niet ondersteund in HPC Pack 2016.
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Op een hoog niveau hello volgende diagram toont Hallo HPC Pack cluster dat u maakt.

![HPC-cluster met knooppunten waarop Excel werkbelastingen worden uitgevoerd][scenario]

## <a name="prerequisites"></a>Vereisten
* **Clientcomputer** -moet u een Windows-clientapparaten computer toosubmit voorbeeld Excel- en SOA-taken toohello cluster. U moet ook een Windows computer toorun Hallo script voor implementatie van Azure PowerShell-cluster (als u deze implementatiemethode kiest).
* **Azure-abonnement** -als u geen Azure-abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/pricing/free-trial/) binnen een paar minuten.
* **Quotum voor kernen** -moet u mogelijk tooincrease Hallo quotum van kernen, vooral als u verschillende clusterknooppunten met multicore VM-grootten implementeert. Als u een Azure quickstart-sjabloon gebruikt, is het Hallo kernen quotum in Resource Manager per Azure-regio. In dat geval moet u mogelijk tooincrease Hallo quotum in een specifieke regio. Zie [Azure-abonnement limieten, quota's en beperkingen](../../azure-subscription-service-limits.md). een quotum tooincrease [opent u een ondersteuningsaanvraag online klant](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) zonder kosten.
* **Microsoft Office-licentie** - als het implementeren van compute knooppunten met de installatiekopie van een virtuele machine Marketplace HPC Pack 2012 R2 met Microsoft Excel, een 30-daagse evaluatieversie van Microsoft Excel Professional Plus 2013 is geïnstalleerd. Nadat de evaluatieperiode hello moet u tooprovide een geldige Microsoft Office-licentie tooactivate Excel toocontinue toorun werkbelastingen. Zie [Excel-activering](#excel-activation) verderop in dit artikel. 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a>Step 1. Een HPC Pack cluster in Azure instellen
Laten we zien twee opties tooset Hallo HPC Pack 2012 R2-cluster: eerste, met behulp van een sjabloon van de Azure quickstart en hello Azure-portal; en de tweede pagina, met behulp van een Azure PowerShell-script voor implementatie.

### <a name="option-1-use-a-quickstart-template"></a>Optie 1. Een Quick Start-sjabloon gebruiken
Gebruik een sjabloon Azure quickstart tooquickly een cluster HPC Pack in hello Azure-portal implementeren. Als u Hallo-sjabloon in Hallo-portal opent, krijgt u een eenvoudige gebruikersinterface waar u Hallo-instellingen voor uw cluster opgeven. Hier volgen de stappen Hallo. 

> [!TIP]
> Als u wilt, gebruikt u een [Azure Marketplace sjabloon](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) die wordt een soortgelijke cluster specifiek voor werkbelastingen van Excel. Hallo stappen verschillen enigszins van de volgende Hallo.
> 
> 

1. Ga naar Hallo [sjabloonpagina HPC-Cluster maken op GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster). Als u wilt, kunt u informatie over het Hallo-sjabloon en Hallo broncode controleren.
2. Klik op **implementeren tooAzure** toostart een implementatie met Hallo-sjabloon in hello Azure-portal.
   
   ![Sjabloon tooAzure implementeren][github]
3. Volg deze stappen tooenter Hallo parameters voor Hallo HPC cluster sjabloon in Hallo-portal.
   
   a. Op Hallo **Parameters** pagina Typ of wijzig de waarden voor de sjabloonparameters Hallo. (Klik op Hallo pictogram volgende tooeach-instelling voor help-informatie). Voorbeeldwaarden weergegeven in het volgende scherm Hallo. In dit voorbeeld wordt een cluster met de naam *hpc01* in Hallo *hpc.local* domein die bestaan uit een hoofdknooppunt en 2 rekenknooppunten. Hallo rekenknooppunten worden gemaakt van een installatiekopie van een HPC Pack VM met Microsoft Excel.
   
   ![Geef parameters][parameters-new-portal]
   
   > [!NOTE]
   > virtuele machine automatisch wordt gemaakt van Hallo Hallo-hoofdknooppunt [nieuwste Marketplace-installatiekopie](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) van HPC Pack 2012 R2 op Windows Server 2012 R2. Momenteel is Hallo-installatiekopie gebaseerd op HPC Pack 2012 R2 Update 3.
   > 
   > COMPUTE knooppunt virtuele machines worden gemaakt van de meest recente image Hallo van Hallo geselecteerd compute-knooppunt producten. Selecteer Hallo **ComputeNodeWithExcel** optie voor Hallo nieuwste HPC Pack compute knooppunt afbeelding met een evaluatieversie van Microsoft Excel Professional Plus 2013. toodeploy een cluster voor algemene SOA-sessies of Excel UDF-offloading, kies Hallo **ComputeNode** optie (zonder Excel geïnstalleerd).
   > 
   > 
   
   b. Kies Hallo-abonnement.
   
   c. Maak een resourcegroep voor Hallo-cluster, zoals *hpc01RG*.
   
   d. Kies een locatie voor de resourcegroep hello, zoals VS-midden.
   
   e. Op Hallo **juridische voorwaarden** pagina, bekijkt hello voorwaarden. Als u akkoord gaat, klikt u op **aankoop**. Vervolgens, wanneer u klaar bent met waarden voor de sjabloon Hallo Hallo instellen, klikt u op **maken**.
4. Wanneer Hallo-implementatie is voltooid (het duurt meestal ongeveer 30 minuten), Hallo cluster certificaatbestand exporteren van hoofdknooppunt Hallo-cluster. In een latere stap, moet u deze openbaar certificaat op Hallo computer tooprovide Hallo serverzijde clientverificatie voor beveiligde HTTP-binding importeren.
   
   a. Ga in hello Azure-portal, toohello dashboard, selecteer Hallo hoofdknooppunt, en klik op **Connect** bovenaan Hallo Hallo pagina tooconnect met extern bureaublad.
   
    <!-- ![Connect toohello head node][connect] -->
   
   b. Standaardprocedures in Certificate Manager tooexport Hallo hoofdknooppunt certificaat (te vinden onder Cert: \LocalMachine\My) zonder Hallo persoonlijke sleutel gebruiken. In dit voorbeeld exporteren *CN = hpc01.eastus.cloudapp.azure.com*.
   
   ![Hallo-certificaat exporteren][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a>Optie 2. Hallo HPC Pack IaaS implementatiescript gebruiken
Hallo HPC Pack IaaS-implementatiescript biedt een andere manier veelzijdige toodeploy een HPC Pack-cluster. Wordt gemaakt van een cluster in het klassieke implementatiemodel hello, terwijl het Hallo-sjabloon gebruikt hello Azure Resource Manager-implementatiemodel. Hallo-script is ook compatibel met een abonnement in Azure globale Hallo of service van Azure voor China.

**Aanvullende vereisten**

* **Azure PowerShell** - [installeren en configureren van Azure PowerShell](/powershell/azure/overview) (versie 0.8.10 of hoger) op de clientcomputer.
* **HPC Pack IaaS-implementatiescript** - downloaden en uitpakken Hallo meest recente versie van script Hallo van Hallo [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949). Hallo-versie van script Hallo controleren door te voeren `New-HPCIaaSCluster.ps1 –Version`. In dit artikel is gebaseerd op versie 4.5.0 of hoger van Hallo-script.

**Hallo-configuratiebestand maken**

 Hallo HPC Pack IaaS-implementatiescript maakt gebruik van een XML-configuratiebestand als invoer die Hallo-infrastructuur van Hallo HPC-cluster beschrijft. een cluster die bestaan uit een hoofdknooppunt en 18 rekenknooppunten gemaakt op basis van Hallo compute knooppunt installatiekopie, zoals Microsoft Excel toodeploy vervangen door waarden voor uw omgeving in Hallo voorbeeldconfiguratiebestand te volgen. Zie voor meer informatie over het Hallo-configuratiebestand Hallo Manual.rtf bestand in map voor Hallo-script en [een HPC-cluster maken met Hallo HPC Pack IaaS-implementatiescript](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

**Opmerkingen over Hallo-configuratiebestand**

* Hallo **VMName** van hoofdknooppunt Hallo **moet** zijn dezelfde als Hallo Hallo **ServiceName**, of de SOA-taken mislukken toorun.
* Zorg ervoor dat u opgeeft **EnableWebPortal** zodat hello hoofdknooppunt certificaat wordt gegenereerd en geëxporteerd.
* Hallo-bestand geeft een PowerShell-script na configuratie PostConfig.ps1 die wordt uitgevoerd op Hallo hoofdknooppunt. Hallo volgende voorbeeldscript hello Azure storage-verbindingsreeks configureert, Hallo knooppunt berekeningsfunctie verwijdert uit het hoofdknooppunt Hallo en alle knooppunten online brengt wanneer ze zijn geïmplementeerd. 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

**Hallo-script uitvoeren**

1. Open PowerShell-console op de clientcomputer Hallo Hallo als beheerder.
2. Wijzig de directory toohello script-map (E:\IaaSClusterScript in dit voorbeeld).
   
   ```
   cd E:\IaaSClusterScript
   ```
3. toodeploy hello HPC Pack cluster, Hallo volgende opdracht worden uitgevoerd. In dit voorbeeld wordt ervan uitgegaan dat configuratiebestand Hallo bevindt zich in E:\HPCDemoConfig.xml.
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

Hallo HPC Pack implementatiescript kan enige tijd worden uitgevoerd. Een ding Hallo script doet tooexport en Hallo cluster certificaat downloaden en opslaan in de map documenten Hallo van de huidige gebruiker op Hallo-clientcomputer. Hallo script genereert een bericht vergelijkbaar toohello volgende. In de volgende stap moet u Hallo-certificaat in de juiste certificaatarchief Hallo importeren.    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a>Stap 2. Offload Excel-werkmappen en UDF's uitvoert vanuit een on-premises client
### <a name="excel-activation"></a>Excel-activering
Wanneer u Hallo ComputeNodeWithExcel VM-installatiekopie voor productieworkloads, moet u een geldige Microsoft Office license key tooactivate Excel op rekenknooppunten hello tooprovide. Anders Hallo evaluatie-versie van Excel verloopt na 30 dagen en uitvoeren van Excel-werkmappen mislukt met de Hallo COMException (0x800AC472). 

U kunt Excel opnieuw 30 dagen van evaluatietijd rearm: Meld u aan het hoofdknooppunt toohello en clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` op alle Excel rekenknooppunten via HPC Cluster Manager. U kunt maximaal twee keer rearm. Daarna moet u een geldige sleutel van de Office-licentie opgeven.

Hallo Office Professional Plus 2013 is geïnstalleerd op Hallo VM-installatiekopie is een volume-editie met een Generic Volume License Key (GVLK). Kan worden geactiveerd via Key Management Service (KMS) / Active Directory gebaseerde activering (AD BA) of Multiple Activation Key (MAK). 

    * toouse AD-KMS-BA, een bestaande KMS-server gebruiken of een nieuwe met behulp van Microsoft Office 2013 Volume License Pack Hallo instellen. (Als u wilt instellen Hallo-server op Hallo hoofdknooppunt.) Vervolgens activeren Hallo KMS-hostsleutel via Hallo Internet of telefonisch. Vervolgens clusrun `ospp.vbs` tooset Hallo KMS-server en de poort en het activeren van Office op alle rekenknooppunten voor Hallo Excel. 

    * toouse MAK, eerste clusrun `ospp.vbs` tooinput Hallo sleutel en vervolgens alle Hallo Excel rekenknooppunten via Hallo Internet of telefonisch te activeren. 

> [!NOTE]
> Retail-productcodes voor Office Professional Plus 2013 kunnen niet worden gebruikt met deze VM-installatiekopie. Als u geldige sleutels en installatiemedia voor Office of Microsoft Excel-versies dan deze versie van de volume Office Professional Plus 2013 hebt, kunt u ze in plaats daarvan. Eerst verwijderen van dit volume-editie en Hallo-editie die u hebt installeren. Hallo opnieuw geïnstalleerd Excel rekenknooppunt worden vastgelegd als een aangepaste VM-installatiekopie toouse in een implementatie op grote schaal.
> 
> 

### <a name="offload-excel-workbooks"></a>Offload Excel-werkmappen
Volg deze stappen toooffload een Excel-werkmap in zodat deze wordt uitgevoerd op Hallo HPC Pack cluster in Azure. toodo, moet u Excel 2010 of 2013 is al geïnstalleerd op de clientcomputer Hallo hebben.

1. Gebruik een van de opties Hallo in stap 1 toodeploy een cluster HPC Pack Hello Excel compute installatiekopie van het knooppunt. Hallo cluster-certificaatbestand (.cer) en cluster-gebruikersnaam en wachtwoord ophalen.
2. Klik op de clientcomputer Hallo Hallo cluster certificaat onder Cert: \CurrentUser\Root te importeren.
3. Zorg ervoor dat Excel is geïnstalleerd. Maak een Excel.exe.config-bestand met de volgende inhoud in Hallo Hallo dezelfde map als Excel.exe op Hallo-clientcomputer. Deze stap zorgt ervoor dat Hallo HPC Pack 2012 R2 Excel COM-invoegtoepassing is geladen.
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. Hallo client toosubmit taken toohello HPC Pack cluster ingesteld. Een mogelijkheid is toodownload Hallo volledige [HPC Pack 2012 R2 Update 3 installatie](http://www.microsoft.com/download/details.aspx?id=49922) en Hallo HPC Pack client installeren. U kunt ook downloaden en installeren van Hallo [HPC Pack 2012 R2 Update 3 client-hulpprogramma's](https://www.microsoft.com/download/details.aspx?id=49923) en Hallo juiste Visual C++ 2010 redistributable voor uw computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).
5. In dit voorbeeld gebruiken we een voorbeeld-Excel-werkmap met de naam ConvertiblePricing_Complete.xlsb. U kunt dit downloaden [hier](https://www.microsoft.com/en-us/download/details.aspx?id=2939).
6. Hallo Excel-werkmap tooa werkmap zoals D:\Excel\Run kopiëren.
7. Hallo Excel-werkmap opent. Op Hallo **ontwikkelen** lint, klikt u op **COM-invoegtoepassingen** en Bevestig dat Hallo HPC Pack Excel COM-invoegtoepassing is geladen.
   
   ![Excel-invoegtoepassing voor HPC Pack][addin]
8. Bewerken Hallo VBA-macro HPCControlMacros in Excel door het wijzigen van Hallo toegelicht regels, zoals weergegeven in het volgende script Hallo. Vervang de juiste waarden voor uw omgeving.
   
   ![Excel-macro voor HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. Hallo Excel-werkmap tooan uploaden directory zoals D:\Excel\Upload kopiëren. Deze map is opgegeven in Hallo HPC_DependsFiles constante in Hallo VBA-macro.
10. toorun hello werkmap op Hallo-cluster in Azure, klikt u op Hallo **Cluster** knop op Hallo werkblad.

### <a name="run-excel-udfs"></a>Excel UDF's uitvoeren
toorun Excel UDF's, volg Hallo vorige stappen 1-3 tooset van Hallo-clientcomputer. Voor Excel UDF's hoeft u geen toohave Hallo Excel toepassing is geïnstalleerd op de rekenknooppunten. Dus bij het maken van uw cluster rekenknooppunten, kunt u berekenen de installatiekopie van een normale compute-knooppunt in plaats van Hallo knooppunt van de installatiekopie met Excel.

> [!NOTE]
> Er is een 34 tekenlimiet in Hallo Excel 2010 en 2013 cluster connector dialoogvenster. U dit dialoogvenster vak toospecify Hallo cluster die Hallo UDF's uitvoert. Als de volledige clusternaam Hallo langer (bijvoorbeeld hpcexcelhn01.southeastasia.cloudapp.azure.com), past niet in het dialoogvenster Hallo. Hallo tijdelijke oplossing is tooset een variabele van alle computers, zoals *CCP_IAASHN* met Hallo Hallo lang clusternaam waarde. Voer de *% CCP_IAASHN %* in het dialoogvenster Hallo als Hallo hoofdknooppunt clusternaam. 
> 
> 

Hallo-cluster is geïmplementeerd, Ga verder met nadat Hallo toorun stappen te volgen een ingebouwde voorbeeld Excel UDF. Zie voor aangepaste Excel UDF's, deze [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Hallo XLL's en deze implementeren op Hallo IaaS-cluster.

1. Open een nieuwe Excel-werkmap. Op Hallo **ontwikkelen** lint, klikt u op **-invoegtoepassingen**. Klik vervolgens in het dialoogvenster Hallo op **Bladeren**, toohello %CCP_HOME%Bin\XLL32 map te navigeren en selecteert u Hallo voorbeeld ClusterUDF32.xll. Als hello ClusterUDF32 niet op de clientcomputer hello bestaat, kunt u deze vanuit Hallo %CCP_HOME%Bin\XLL32 map op het hoofdknooppunt Hallo kopiëren.
   
   ![Hallo UDF selecteren][udf]
2. Klik op **bestand** > **opties** > **geavanceerde**. Onder **formules**, Controleer **toestaan gebruiker gedefinieerde XLL functies toorun een rekencluster**. Klik vervolgens op **opties** en voer de volledige clusternaam Hallo in **hoofdknooppunt clusternaam**. (Als zijn aangegeven eerder deze invoervak is beperkt too34 tekens, zodat een lange clusternaam niet past. U kunt hier een variabele voor alle computers voor een lange clusternaam.)
   
   ![Hallo UDF configureren][options]
3. toorun hello UDF berekening op Hallo-cluster, klik op Hallo cel met de waarde =XllGetComputerNameC() en druk op Enter. Hallo-functie haalt gewoon Hallo-naam van het Hallo-rekenknooppunt op welke Hallo UDF wordt uitgevoerd. Voor Hallo voor het eerst uitvoert, wordt een dialoogvenster referenties gevraagd voor Hallo gebruikersnaam en wachtwoord tooconnect toohello IaaS-cluster.
   
   ![UDF uitvoeren][run]
   
   Wanneer er veel cellen toocalculate, druk op Alt-Shift-Ctrl + F9 toorun Hallo berekening op alle cellen.

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a>Stap 3. Een SOA-werkbelasting uitvoeren vanuit een on-premises client
toorun algemene SOA-toepassingen op Hallo HPC Pack IaaS cluster gebruik een van de methoden Hallo eerst in stap 1 toodeploy Hallo-cluster. Geef de installatiekopie van een algemene compute-knooppunt in dit geval omdat u geen Excel nodig op Hallo rekenknooppunten. Volg deze stappen.

1. Bij het ophalen van Hallo cluster certificaat, moet u het importeren op de clientcomputer Hallo onder Cert: \CurrentUser\Root.
2. Hallo installeren [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) en [HPC Pack 2012 R2 Update 3 client-hulpprogramma's](https://www.microsoft.com/download/details.aspx?id=49923). Deze hulpprogramma's kunnen u toodevelop en SOA-clienttoepassingen uitvoeren.
3. Hallo HelloWorldR2 downloaden [voorbeeldcode](https://www.microsoft.com/download/details.aspx?id=41633). Open Hallo HelloWorldR2.sln in Visual Studio 2010 of 2012. (Dit voorbeeld is niet compatibel met latere versies van Visual Studio).
4. Hallo EchoService project eerst bouwen. Vervolgens implementeert Hallo service toohello IaaS-cluster in Hallo dezelfde manier als tooan lokale cluster. Zie voor gedetailleerde stappen Hallo Readme.doc in HelloWordR2. Wijzig en Hallo HellWorldR2 en andere projecten bouwen, zoals beschreven in de volgende sectie toogenerate Hallo SOA-clienttoepassingen die worden uitgevoerd op een cluster Azure IaaS Hallo.

### <a name="use-http-binding-with-azure-storage-queue"></a>Http-binding gebruiken met Azure storage-wachtrij
toouse Http-binding met een Azure storage-wachtrij worden enkele wijzigingen aanbrengen toohello voorbeeldcode.

* De clusternaam Hallo bijwerken.
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* Eventueel Hallo standaard TransportScheme in SessionStartInfo gebruiken of stel expliciet tooHttp.

```
    info.TransportScheme = TransportScheme.Http;
```

* Standaard-binding voor Hallo BrokerClient gebruiken.
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    Of expliciet met Hallo basicHttpBinding ingesteld.
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* Eventueel Hallo UseAzureQueue vlag tootrue in SessionStartInfo instellen. Als dat niet is ingesteld, wordt deze ingesteld tootrue standaard wanneer clusternaam hello Azure domeinachtervoegsels en Hallo TransportScheme Http is.
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a>Gebruik Http-binding zonder Azure storage-wachtrij
zonder een Azure storage-wachtrij, expliciet set Hallo UseAzureQueue vlag toofalse in Hallo SessionStartInfo toouse Http-binding.

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a>Gebruik NetTcp-binding
toouse NetTcp binding, Hallo-configuratie is vergelijkbaar tooconnecting tooan on-premises-cluster. U moet enkele eindpunten op Hallo hoofdknooppunt VM tooopen. Als u Hallo HPC Pack IaaS implementatie script toocreate Hallo cluster gebruikt, bijvoorbeeld hello set Hallo eindpunten in Azure-portal als volgt.

1. Hallo VM stoppen.
2. Voeg Hallo TCP-poorten 9090, 9087, 9091, 9094 voor Hallo-sessie Broker, respectievelijk worker en Data services Broker
   
    ![Eindpunten configureren][endpoint-new-portal]
3. Hallo VM start.

Hallo SOA-clienttoepassing vereist geen wijzigingen behalve Hallo head toohello IaaS cluster volledige naam te wijzigen.

## <a name="next-steps"></a>Volgende stappen
* Zie [deze resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) voor meer informatie over het uitvoeren van Excel-werkbelastingen met HPC Pack.
* Zie [SOA-Services beheren in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) voor meer informatie over het implementeren en beheren van SOA-services met HPC Pack.

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
