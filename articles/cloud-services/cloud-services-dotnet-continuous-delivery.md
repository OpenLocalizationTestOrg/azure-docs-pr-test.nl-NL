---
title: aaaContinuous leveringsmethode voor cloud services met TFS in Azure | Microsoft Docs
description: Meer informatie over hoe tooset up continue leveringsmethode voor Azure cloud-apps. Codevoorbeelden voor opdrachtregelprogramma MSBuild-instructies en PowerShell-scripts.
services: cloud-services
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4f3c93c6-5c82-4779-9d19-7404a01e82ca
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/12/2017
ms.author: kraigb
ms.openlocfilehash: c0e5e72ffbd3c05b84ce1733068e92c528bcc4b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-for-cloud-services-in-azure"></a>Continue leveringsmethode voor Cloudservices in Azure
Hallo proces dat wordt beschreven in dit artikel leest u hoe tooset up continue leveringsmethode voor Azure cloud-apps. Dit proces kunt u automatisch pakketten maken en implementeren van Hallo pakket tooAzure na elke code incheckt. Hallo pakket buildproces beschreven in dit artikel is gelijkwaardig toohello **pakket** opdracht in Visual Studio en de publicatie stappen zijn equivalent toohello **publiceren** opdracht in Visual Studio.
Hallo artikel behandelt Hallo methoden die u zou ook toocreate een installatieserver met opdrachtregelprogramma MSBuild-instructies en Windows PowerShell-scripts gebruiken laat zien hoe toooptionally Visual Studio Team Foundation Server - Team bouwen definities configureren toouse hello MSBuild-opdrachten en PowerShell-scripts. Hallo-proces kan worden aangepast voor uw build-omgeving en de doel-Azure-omgevingen.

U kunt ook Visual Studio Team Services, een versie van TFS die wordt gehost in Azure, toodo dit eenvoudiger. 

Voordat u begint, moet u uw toepassing vanuit Visual Studio publiceren.
Dit zorgt ervoor dat alle Hallo resources beschikbaar en geïnitialiseerd zijn wanneer u probeert tooautomate Hallo publicatieproces.

## <a name="1-configure-hello-build-server"></a>1: Hallo bouwen Server configureren
Voordat u een Azure-pakket maken kunt met behulp van MSBuild, moet u Hallo vereiste software en hulpprogramma's installeren op Hallo build-server.

Visual Studio is niet vereist toobe op Hallo build-server geïnstalleerd. Als u uw buildserver toouse Team Foundation bouwen Service toomanage wilt, volgt u de instructies Hallo in Hallo [Team Foundation bouwen Service] [ Team Foundation Build Service] documentatie.

1. Installeer op Hallo buildserver Hallo [.NET Framework 4.5.2][.NET Framework 4.5.2], waaronder MSBuild.
2. Meest recente Hallo installeren [Authoring hulpprogramma's van Azure voor .NET](https://azure.microsoft.com/develop/net/).
3. Hallo installeren [Azure-bibliotheken voor .NET](http://go.microsoft.com/fwlink/?LinkId=623519).
4. Hallo Microsoft.WebApplication.targets bestandskopie van een installatie van Visual Studio toohello bouwen server.

   Op een computer met Visual Studio is geïnstalleerd, dit bestand bevindt zich in de directory Hallo C:\\Program Files(x86)\\MSBuild\\Microsoft\\VisualStudio\\v14.0\\WebApplications. Kopieer deze toohello dezelfde directory op Hallo build-server.
5. Hallo installeren [Azure-Tools voor Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx).

## <a name="2-build-a-package-using-msbuild-commands"></a>2: een pakket met MSBuild-opdrachten maken
Deze sectie wordt beschreven hoe een MSBuild tooconstruct opdracht die wordt gemaakt van een Azure-pakket. Deze stap uitvoeren op Hallo build server tooverify dat alles juist is geconfigureerd en dat Hallo MSBuild-opdracht is wat u wilt deze toodo. U kunt deze opdrachtregel tooexisting bouwscripts op Hallo build-server of Hallo vanaf de opdrachtregel in een definitie TFS bouwen, kunt u ofwel toevoegen zoals beschreven in de volgende sectie Hallo. Zie voor meer informatie over opdrachtregelparameters en MSBuild [MSBuild opdrachtregel verwijzing](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).

1. Als Visual Studio op Hallo build-server is geïnstalleerd, zoekt en kies **Visual Studio-opdrachtprompt** in Hallo **Visual Studio Tools** map in Windows.

   Als Visual Studio op Hallo build-server niet is geïnstalleerd, open een opdrachtprompt en zorg ervoor dat MSBuild.exe toegankelijk is op het pad. MSBuild is geïnstalleerd met hello .NET Framework in Hallo pad % WINDIR %\\Microsoft.NET\\Framework\\*versie*. Bijvoorbeeld om toe te voegen MSBuild.exe toohello pad omgevingsvariabele wanneer u .NET Framework 4 geïnstalleerd hebt, typt u de volgende opdracht achter de opdrachtprompt Hallo Hallo:

       set PATH=%PATH%;"C:\Windows\Microsoft.NET\Framework\v4.0.30319"
2. Ga bij de opdrachtprompt Hallo toohello map met het Azure-project-bestand dat u wilt dat toobuild.
3. MSBuild uitvoeren met Hallo/target: optie zoals in het volgende voorbeeld Hallo publiceren:

       MSBuild /target:Publish

   Deze optie kan worden afgekort tot /t: publiceren. Hallo /t:Publish optie in MSBuild moet niet verwarren met Hallo publiceren opdrachten die beschikbaar zijn in Visual Studio wanneer u hello die Azure SDK geïnstalleerd hebt. Hallo /t: publicatieoptie alleen bij builds hello Azure pakketten. Deze implementeert geen hello-pakketten zoals Hallo publiceren opdrachten in Visual Studio doet.

   U kunt eventueel Hallo projectnaam opgeven als een MSBuild-parameter. Als niet wordt opgegeven, wordt de huidige map Hallo gebruikt. Zie voor meer informatie over de opdrachtregelopties MSBuild [MSBuild opdrachtregel verwijzing](https://msdn.microsoft.com/library/ms164311%28v=vs.140%29.aspx).
4. Zoek Hallo uitvoer. Met deze opdracht maakt standaard een map in de relatie toohello-hoofdmap voor Hallo-project, zoals *ProjectDir*\\bin\\*configuratie* \\ App.publish\\. Wanneer u een Azure-project maakt, u twee bestanden: Hallo pakketbestand zelf en bijbehorende configuratiebestand Hallo genereren:

   * Project.cspkg
   * Serviceconfiguration zijn. *TargetProfile*.cscfg

   Standaard elke Azure-project bevat één serviceconfiguratiebestand (.cscfg-bestand) voor de lokale (foutopsporing) builds en een andere voor builds cloud (fasering of productie), maar u kunt toevoegen of verwijderen van service configuratiebestanden zo nodig. Wanneer u een pakket vanuit Visual Studio maakt, wordt u gevraagd welke service configuration file tooinclude naast Hallo-pakket.
5. Hallo serviceconfiguratiebestand opgeven. Als u een pakket met behulp van MSBuild bouwen, is Hallo lokale service-configuratiebestand standaard. tooinclude een andere service-configuratiebestand, stel de eigenschap TargetProfile van Hallo MSBuild-opdracht, zoals in het volgende voorbeeld Hallo:

       MSBuild /t:Publish /p:TargetProfile=Cloud
6. Geef de locatie Hallo voor Hallo uitvoer. Hallo pad instellen met behulp van de /p:PublishDir =*Directory* \\ optie, met inbegrip van Hallo afsluitende backslash scheidingsteken, zoals in het volgende voorbeeld Hallo:

       MSBuild /target:Publish /p:PublishDir=\\myserver\drops\

   Nadat u hebt gemaakt en getest een juiste MSBuild command line toobuild projecten en ze combineren in een Azure-pakket, kunt u deze opdrachtregel tooyour build scripts toevoegen. Als uw buildserver gebruikmaakt van aangepaste scripts, wordt dit proces afhankelijk van de details van uw aangepaste buildproces. Als u TFS gebruikt als een build-omgeving, kunt u Hallo-instructies in Hallo volgende stap tooadd hello Azure-pakket build tooyour buildproces volgen.

## <a name="3-build-a-package-using-tfs-team-build"></a>3: bouwen van een pakket met TFS-Team maken
Als u hebt Team Foundation Server (TFS) instellen terwijl een controller bouwen en Hallo server maakt die zijn ingesteld als een TFS-build-machine en u kunt desgewenst een geautomatiseerde build instellen voor uw Azure-pakket op. Voor informatie over hoe tooset up en Team Foundation server gebruiken als een build-systeem zien [Scale-out uw build-systeem][Scale out your build system]. Met name de volgende procedure wordt ervan uitgegaan dat u uw buildserver hebt geconfigureerd zoals beschreven in [implementeren en configureren van een buildserver][Deploy and configure a build server], en dat u hebt gemaakt dat een teamproject gemaakt een cloud Service-project in Hallo teamproject.

tooconfigure TFS toobuild Azure-pakketten voeren Hallo stappen te volgen:

1. Kies in Visual Studio op uw ontwikkelcomputer in menu Beeld Hallo **Team Explorer**, of kies Ctrl +\\, Ctrl + M. Vouw in het venster Team Explorer Hallo **Builds** knooppunt of kies Hallo **Builds** pagina en kies **nieuwe bouwen definitie**.

   ![Nieuwe bouwen definitie-optie][0]
2. Kies Hallo **Trigger** tabblad en geef Hallo gewenst voorwaarden voor als u wilt dat Hallo pakket toobe gebouwd. Geef bijvoorbeeld **continue integratie** toobuild Hallo pakket wanneer een bron beheren inchecken optreedt.
3. Kies Hallo **broninstellingen** tabblad en zorg ervoor dat de projectmap wordt vermeld in Hallo **bronmap van het besturingselement** kolom en Hallo status **Active**.
4. Kies Hallo **bouwen standaard** tabblad en controleer onder Build-controller Hallo-naam van Hallo build-server.  Hallo ook optie **kopie build uitvoer toohello volgende doelmap** Hallo gewenst neerzetten locatie op te geven.
5. Kies Hallo **proces** tabblad. Kies op Hallo proces tabblad Hallo standaardsjabloon onder **bouwen**, Hallo project kiezen als deze nog niet is geselecteerd, en vouw Hallo **Geavanceerd** sectie in Hallo **bouwen**sectie Hallo raster.
6. Kies **MSBuild-argumenten**, en Hallo juiste MSBuild opdrachtregelargumenten ingesteld zoals beschreven in stap 2 hierboven. Voer bijvoorbeeld **/t: publiceren /p:PublishDir =\\\\MijnServer\\zakt\\**  toobuild een pakket en kopieer Hallo pakket bestanden toohello locatie \\ \\MijnServer\\zakt\\:

   ![MSBuild-argumenten][2]

   > [!NOTE]
   > Openbare share kopiëren Hallo bestanden tooa maakt het eenvoudiger toomanually implementeren hello-pakketten uit uw ontwikkelcomputer.
7. Hallo succes van uw build-stap door te controleren in een wijziging tooyour project testen of een nieuwe build in de wachtrij. tooqueue van een nieuwe build, in de Explorer-Team met de rechtermuisknop op **alle bouwen definities** en kies vervolgens **wachtrij nieuwe bouwen**.

## <a name="4-publish-a-package-using-a-powershell-script"></a>4: een pakket met een PowerShell-Script publiceren
Deze sectie wordt beschreven hoe Windows PowerShell-script die Hallo Cloud-app-pakket publiceert tooconstruct tooAzure met optionele parameters uitvoer. Dit script kan worden aangeroepen na Hallo build stap in uw aangepaste build automation. Het kan ook worden aangeroepen vanuit de werkstroomactiviteiten processjabloon in Visual Studio TFS Team bouwen.

1. Hallo installeren [Azure PowerShell-cmdlets] [ Azure PowerShell cmdlets] (v0.6.1 of hoger).
   Tijdens de installatiefase Hallo-cmdlet, kiest u tooinstall als een module. Houd er rekening mee dat deze officieel ondersteunde versie Hallo oudere versie die worden aangeboden via CodePlex, vervangt Hoewel Hallo eerdere versies werden 2.x.x genummerd.
2. Azure PowerShell Hallo startmenu of startpagina starten. Als u op deze manier wordt gestart, worden hello Azure PowerShell-cmdlets geladen.
3. Controleren of Hallo PowerShell-cmdlets zijn geladen met Hallo gedeeltelijke opdracht bij de PowerShell-prompt Hallo `Get-Azure` en drukt u vervolgens op Tab-toets voor voltooiing van instructie Hallo.

   Als u herhaaldelijk op Hallo Tab-toets drukt, ziet u diverse Azure PowerShell-opdrachten.
4. Controleer of u verbinding tooyour Azure-abonnement maken kunt via uw abonnementsgegevens van Hallo .publishsettings-bestand importeren.

   `Import-AzurePublishSettingsFile c:\scripts\WindowsAzure\default.publishsettings`

   Voer de opdracht Hallo

   `Get-AzureSubscription`

   Dit toont informatie over uw abonnement. Controleer of alles juist is.
5. Hallo script sjabloon tijdens het Hallo-einde van dit artikel naar uw scriptmap als c: opgegeven opslaan\\scripts\\WindowsAzure\\**PublishCloudService.ps1**.
6. Raadpleeg Hallo parameters sectie Hallo-script. Toevoegen of wijzigen van de standaardwaarden. Deze waarden kunnen altijd worden genegeerd door door te geven in expliciete parameters.
7. Zorg ervoor dat er geldige cloudservice en storage-accounts die zijn gemaakt in uw abonnement die kan worden geselecteerd door de Hallo script publiceren. Het opslagaccount (blobopslag) wordt gebruikt tooupload en tijdelijk Hallo-implementatie van pakket en config-bestand op te slaan tijdens de implementatie wordt gemaakt.

   * een nieuwe cloudservice toocreate, kunt u dit script of gebruik Hallo aanroepen [Azure-portal](https://portal.azure.com). Hallo cloudservicenaam wordt gebruikt als een voorvoegsel in een volledig gekwalificeerde domeinnaam en daarom moet uniek zijn.

         New-AzureService -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
   * een nieuw opslagaccount toocreate, kunt u dit script of gebruik Hallo aanroepen [Azure-portal](https://portal.azure.com). Hallo opslagaccountnaam wordt gebruikt als een voorvoegsel in een volledig gekwalificeerde domeinnaam en daarom moet uniek zijn. U kunt proberen Hallo dezelfde naam als de cloudservice.

         New-AzureStorageAccount -ServiceName "mytestcloudservice" -Location "North Central US" -Label "mytestcloudservice"
8. Hallo script aanroepen rechtstreeks vanuit Azure PowerShell, of op wire om dit script tooyour host build automation toooccur na Hallo pakket build.

   > [!IMPORTANT]
   > Hallo-script wordt altijd verwijderen of uw bestaande implementaties vervangen standaard als ze worden gedetecteerd. Dit is nodig om in te schakelen continue van automatisering geen gebruiker wordt gevraagd wanneer mogelijk is.
   >
   >

   **Voorbeeldscenario 1:** continue implementatie toohello staging-omgeving van een service:

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Staging -serviceName mycloudservice -storageAccountName mystoragesaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   Dit is doorgaans opgevolgd door testuitvoering verificatie en geen VIP's wisselen. Hallo VIP wisselen kan worden uitgevoerd via Hallo [Azure-portal](https://portal.azure.com) of met behulp van de cmdlet Hallo Move-implementatie.

   **Voorbeeldscenario 2:** continue implementatie toohello productie-omgeving van een speciale test-service

       PowerShell c:\scripts\windowsazure\PublishCloudService.ps1 -environment Production -enableDeploymentUpgrade 1 -serviceName mycloudservice -storageAccountName mystorageaccount -packageLocation c:\drops\app.publish\ContactManager.Azure.cspkg -cloudConfigLocation c:\drops\app.publish\ServiceConfiguration.Cloud.cscfg -subscriptionDataFile c:\scripts\default.publishsettings

   **Extern bureaublad:**

   U moet tooperform extra eenmalige stappen tooensure Hallo die juiste Cloud Service-certificaat is geüpload tooall cloudservices gericht door dit script als extern bureaublad is ingeschakeld in uw Azure-project.

   Zoek Hallo certificaat vingerafdruk waarden door uw rollen wordt verwacht. De vingerafdruk-waarden zijn niet zichtbaar in Hallo certificaten sectie van het configuratiebestand van de cloud (dat wil zeggen ServiceConfiguration.Cloud.cscfg). Het is ook zichtbaar in de configuratie voor extern bureaublad-dialoogvenster Hallo in Visual Studio wanneer u opties weergeven en bekijkt hello certificaat geselecteerd.

       <Certificates>
             <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="C33B6C432C25581601B84C80F86EC2809DC224E8" thumbprintAlgorithm="sha1" />
       </Certificates>

   Extern bureaublad-certificaten als een eenmalige instellingsstap met behulp van de volgende cmdlet script Hallo uploaden:

       Add-AzureCertificate -serviceName <CLOUDSERVICENAME> -certToDeploy (get-item cert:\CurrentUser\MY\<THUMBPRINT>)

   Bijvoorbeeld:

       Add-AzureCertificate -serviceName 'mytestcloudservice' -certToDeploy (get-item cert:\CurrentUser\MY\C33B6C432C25581601B84C80F86EC2809DC224E8

   Ook kunt u Hallo bestand PFX-certificaat met persoonlijke sleutel en het uploaden van certificaten tooeach doel cloud service exporteren de [Azure-portal](https://portal.azure.com).

   <!---
   Fixing broken links for Azure content migration from ACOM tooDOCS. I'm unable toofind a replacement links, so I'm commenting out this reference for now. hello author can investigate in hello future. "Read hello following article toolearn more: http://msdn.microsoft.com/library/windowsazure/gg443832.aspx.
   -->
   **Upgraden versus van de implementatie. Verwijderen van implementatie -\> nieuwe implementatie**

   Hallo-script wordt standaard uitvoeren een Upgrade-implementatie ($enableDeploymentUpgrade = 1) als er is geen parameter is doorgegeven, of de waarde 1 expliciet wordt doorgegeven. Dit heeft het voordeel van het minder tijd nodig dan een volledige implementatie voor enkele exemplaren. Voor exemplaren waarvoor hoge beschikbaarheid die dit ook Hallo profiteren heeft van het verlaten van sommige gevallen terwijl anderen kunnen worden bijgewerkt (roulatie van uw updatedomein), plus de VIP wordt niet verwijderd.

   Upgrade-implementatie kan worden uitgeschakeld in het Hallo-script ($enableDeploymentUpgrade = 0) of door het doorgeven van *- enableDeploymentUpgrade 0* als een parameter die wordt gewijzigd van het script gedrag toofirst verwijderen alle bestaande implementatie en maak vervolgens een nieuwe implementatie.

   > [!IMPORTANT]
   > Hallo-script wordt altijd verwijderen of uw bestaande implementaties vervangen standaard als ze worden gedetecteerd. Dit is nodig om in te schakelen continue van automatisering wanneer er geen gebruiker/operator vragen mogelijk is.
   >
   >

## <a name="5-publish-a-package-using-tfs-team-build"></a>5: een pakket met behulp van TFS-Team bouwen publiceren
Deze optionele stap maakt u verbinding maken van TFS-Team toohello script gemaakt in stap 4, die worden gepubliceerd Hallo pakket build tooAzure verwerkt. Dit houdt in dat wijzigen Hallo processjabloon gebruikt door de definitie van de build zodat deze wordt uitgevoerd een activiteit publiceren achter Hallo Hallo-werkstroom. Hallo publiceren activiteit kan uw PowerShell-opdracht wordt doorgegeven in parameters van Hallo-versie wordt uitgevoerd. Uitvoer van Hallo MSBuild-doelen en publiceren van script zal worden doorgesluisd naar Hallo standaard builduitvoer.

1. Hallo definitie bouwen die verantwoordelijk is voor bewerken continue implementeren.
2. Selecteer Hallo **proces** tabblad.
3. Ga als volgt [deze instructies](http://msdn.microsoft.com/library/dd647551.aspx) tooadd een activiteit-project voor Hallo processjabloon bouwen, Hallo standaardsjabloon downloaden, toe te voegen aan het Hallo-project en incheckt. Hallo build processjabloon een nieuwe naam, zoals AzureBuildProcessTemplate opgeven.
4. Retourneren van toohello **proces** tabblad en gebruik **Details weergeven** tooshow een lijst met beschikbare build processjablonen. Kies Hallo **nieuw...**  knop en navigeer toohello project u zojuist hebt toegevoegd en ingecheckt. Zoek Hallo-sjabloon die u zojuist hebt gemaakt en kies **OK**.
5. Open Hallo geselecteerd processjabloon voor bewerking. U kunt rechtstreeks in de werkstroomontwerper Hallo of in Hallo XML-editor toowork Hello XAML openen.
6. Lijst met nieuwe argumenten volgen als afzonderlijke regels op Hallo argumenten tabblad van de werkstroomontwerper Hallo Hallo toevoegen. Alle argumenten moet richting = In en typ = tekenreeks. Deze worden gebruikt tooflow parameters van Hallo build definitie in de werkstroom hello, welke vervolgens get gebruikte toocall Hallo script publiceren.

       SubscriptionName
       StorageAccountName
       CloudConfigLocation
       PackageLocation
       Environment
       SubscriptionDataFileLocation
       PublishScriptLocation
       ServiceName

   ![Lijst met argumenten][3]

   Hallo die bijbehorende XAML uitziet:

       <Activity  _ />
         <x:Members>
           <x:Property Name="BuildSettings" Type="InArgument(mtbwa:BuildSettings)" />
           <x:Property Name="TestSpecs" Type="InArgument(mtbwa:TestSpecList)" />
           <x:Property Name="BuildNumberFormat" Type="InArgument(x:String)" />
           <x:Property Name="CleanWorkspace" Type="InArgument(mtbwa:CleanWorkspaceOption)" />
           <x:Property Name="RunCodeAnalysis" Type="InArgument(mtbwa:CodeAnalysisOption)" />
           <x:Property Name="SourceAndSymbolServerSettings" Type="InArgument(mtbwa:SourceAndSymbolServerSettings)" />
           <x:Property Name="AgentSettings" Type="InArgument(mtbwa:AgentSettings)" />
           <x:Property Name="AssociateChangesetsAndWorkItems" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateWorkItem" Type="InArgument(x:Boolean)" />
           <x:Property Name="DropBuild" Type="InArgument(x:Boolean)" />
           <x:Property Name="MSBuildArguments" Type="InArgument(x:String)" />
           <x:Property Name="MSBuildPlatform" Type="InArgument(mtbwa:ToolPlatform)" />
           <x:Property Name="PerformTestImpactAnalysis" Type="InArgument(x:Boolean)" />
           <x:Property Name="CreateLabel" Type="InArgument(x:Boolean)" />
           <x:Property Name="DisableTests" Type="InArgument(x:Boolean)" />
           <x:Property Name="GetVersion" Type="InArgument(x:String)" />
           <x:Property Name="PrivateDropLocation" Type="InArgument(x:String)" />
           <x:Property Name="Verbosity" Type="InArgument(mtbw:BuildVerbosity)" />
           <x:Property Name="Metadata" Type="mtbw:ProcessParameterMetadataCollection" />
           <x:Property Name="SupportedReasons" Type="mtbc:BuildReason" />
           <x:Property Name="SubscriptionName" Type="InArgument(x:String)" />
           <x:Property Name="StorageAccountName" Type="InArgument(x:String)" />
           <x:Property Name="CloudConfigLocation" Type="InArgument(x:String)" />
           <x:Property Name="PackageLocation" Type="InArgument(x:String)" />
           <x:Property Name="Environment" Type="InArgument(x:String)" />
           <x:Property Name="SubscriptionDataFileLocation" Type="InArgument(x:String)" />
           <x:Property Name="PublishScriptLocation" Type="InArgument(x:String)" />
           <x:Property Name="ServiceName" Type="InArgument(x:String)" />
         </x:Members>

         <this:Process.MSBuildArguments>
7. Een nieuwe reeks toevoegen aan Hallo einde van de Agent worden uitgevoerd op:

   1. Gestart door een If-instructie activiteit toocheck voor een geldige scriptbestand toe te voegen. Hallo voorwaarde toothis waarde instellen:

          Not String.IsNullOrEmpty(PublishScriptLocation)
   2. Hallo vervolgens geval Hallo If-instructie, Voeg een nieuwe Sequence-activiteit. Set Hallo weergegeven naam too'Start publiceren '
   3. De volgende lijst met nieuwe variabelen Hallo Start publiceren reeks nog steeds is geselecteerd, toevoegen als afzonderlijke regels in het tabblad variabelen van Hallo workflow designer. Alle variabelen moet type variabele = tekenreeks en bereik = Start publiceren. Deze worden gebruikt tooflow parameters van Hallo build definitie in de werkstroom, welke vervolgens get gebruikte toocall Hallo script publiceren.

      * SubscriptionDataFilePath van het type tekenreeks
      * PublishScriptFilePath van het type tekenreeks

        ![Nieuwe variabelen][4]
   4. Als u met behulp van TFS 2012 of eerder een ConvertWorkspaceItem-activiteit aan begin van Hallo toevoegen Hallo nieuwe tekenreeks. Als u TFS 2013 of later gebruikt, voegt u een activiteit GetLocalPath aan begin van de nieuwe tekenreeks Hallo Hallo. Voor een ConvertWorkspaceItem Hallo eigenschappen als volgt instellen: richting = ServerToLocal, DisplayName = 'Converteren publiceren script filename', invoer PublishScriptLocation, resultaat = = PublishScriptFilePath, werkruimte = 'Werkruimte'. Voor een activiteit GetLocalPath ingesteld Hallo eigenschap IncomingPath too'PublishScriptLocation', en het resultaat too'PublishScriptFilePath Hallo ". Deze activiteit kunnen worden geconverteerd Hallo pad toohello publiceren script vanaf locaties voor TFS-server (indien van toepassing) tooa schijfpad met lokale.
   5. Als u met behulp van TFS 2012 of ouder, een andere ConvertWorkspaceItem activiteit aan Hallo einde van toevoegen Hallo nieuwe tekenreeks. Richting = ServerToLocal, DisplayName = 'Converteren abonnement filename', invoer = SubscriptionDataFileLocation, resultaat = SubscriptionDataFilePath, werkruimte = 'Werkruimte'. Als u TFS 2013 of later gebruikt, voegt u een andere GetLocalPath. IncomingPath = 'SubscriptionDataFileLocation' en resultaat = 'SubscriptionDataFilePath'.
   6. Een activiteit InvokeProcess toevoegen aan einde Hallo Hallo nieuwe tekenreeks.
      Deze activiteit oproepen PowerShell.exe met Hallo argumenten doorgegeven door Hallo definitie bouwen.

      + Argumenten String.Format = ('-'' {0}' ' - serviceName {1} - storageAccountName {2} - packageLocation '' {3}' ' - cloudConfigLocation '' {4}' ' - subscriptionDataFile '' {5}' ' - selectedSubscription {6} bestand-omgeving '' {7}' ' ",  PublishScriptFilePath, ServiceName, StorageAccountName, PackageLocation, CloudConfigLocation, SubscriptionDataFilePath, SubscriptionName, omgeving)
      + DisplayName = Execute script publiceren
      + FileName = 'PowerShell' (inclusief Hallo aanhalingstekens)
      + OutputEncoding System.Text.Encoding.GetEncoding(System.Globalization.CultureInfo.InstalledUICulture.TextInfo.OEMCodePage) =
   7. In Hallo **standaarduitvoer verwerken** sectie textbox van de InvokeProcess, stelt u Hallo textbox waarde too'data'. Dit is een variabele toostore Hallo standaarduitvoer.
   8. Toevoegen van een activiteit WriteBuildMessage onder Hallo **standaarduitvoer verwerken** sectie. Hallo belang ingesteld = 'Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High' en het Hallo-bericht = 'data'. Dit zorgt ervoor Hallo standaarduitvoer van het script ophalen toohello builduitvoer wordt geschreven.
   9. In Hallo **foutuitvoer verwerken** sectie textbox van de InvokeProcess, stelt u Hallo textbox waarde too'data'. Dit is een variabele toostore Hallo standaardfout gegevens.
   10. Toevoegen van een activiteit WriteBuildError onder Hallo **foutuitvoer verwerken** sectie. Hallo-bericht instellen = 'data'. Dit zorgt ervoor Hallo standaardfouten van Hallo script toohello fout builduitvoer ophalen geschreven.
   11. Corrigeer eventuele fouten, aangegeven door blauw uitroepteken aanhalingstekens. Beweeg de muisaanwijzer over de tooget uitroepteken markeert een aanwijzing over Hallo-fout. Hallo workflow om te wissen fouten niet opslaan.

   eindresultaat Hallo Hallo publiceren workflow-activiteiten in de ontwerpfunctie Hallo er als volgt:

   ![Workflow-activiteiten][5]

   eindresultaat Hallo Hallo publiceren workflow-activiteiten in XAML er als volgt:

       <If Condition="[Not String.IsNullOrEmpty(PublishScriptLocation)]" sap2010:WorkflowViewState.IdRef="If_1">
           <If.Then>
             <Sequence DisplayName="Start Publish" sap2010:WorkflowViewState.IdRef="Sequence_4">
               <Sequence.Variables>
                 <Variable x:TypeArguments="x:String" Name="SubscriptionDataFilePath" />
                 <Variable x:TypeArguments="x:String" Name="PublishScriptFilePath" />
               </Sequence.Variables>
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert publish script filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_1" Input="[PublishScriptLocation]" Result="[PublishScriptFilePath]" Workspace="[Workspace]" />
               <mtbwa:ConvertWorkspaceItem DisplayName="Convert subscription filename" sap2010:WorkflowViewState.IdRef="ConvertWorkspaceItem_2" Input="[SubscriptionDataFileLocation]" Result="[SubscriptionDataFilePath]" Workspace="[Workspace]" />
               <mtbwa:InvokeProcess Arguments="[String.Format(&quot; -File &quot;&quot;{0}&quot;&quot; -serviceName {1}&#xD;&#xA;            -storageAccountName {2} -packageLocation &quot;&quot;{3}&quot;&quot;&#xD;&#xA;            -cloudConfigLocation &quot;&quot;{4}&quot;&quot; -subscriptionDataFile &quot;&quot;{5}&quot;&quot;&#xD;&#xA;            -selectedSubscription {6} -environment &quot;&quot;{7}&quot;&quot;&quot;,&#xD;&#xA;            PublishScriptFilePath, ServiceName, StorageAccountName,&#xD;&#xA;            PackageLocation, CloudConfigLocation,&#xD;&#xA;            SubscriptionDataFilePath, SubscriptionName, Environment)]" DisplayName="'Execute Publish Script'" FileName="[PowerShell]" sap2010:WorkflowViewState.IdRef="InvokeProcess_1">
                 <mtbwa:InvokeProcess.ErrorDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildError Message="{x:Null}" sap2010:WorkflowViewState.IdRef="WriteBuildError_1" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.ErrorDataReceived>
                 <mtbwa:InvokeProcess.OutputDataReceived>
                   <ActivityAction x:TypeArguments="x:String">
                     <ActivityAction.Argument>
                       <DelegateInArgument x:TypeArguments="x:String" Name="data" />
                     </ActivityAction.Argument>
                     <mtbwa:WriteBuildMessage sap2010:WorkflowViewState.IdRef="WriteBuildMessage_2" Importance="[Microsoft.TeamFoundation.Build.Client.BuildMessageImportance.High]" Message="[data]" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" />
                   </ActivityAction>
                 </mtbwa:InvokeProcess.OutputDataReceived>
               </mtbwa:InvokeProcess>
             </Sequence>
           </If.Then>
         </If>
       </Sequence>
8. Hallo build proces sjabloon werkstroom en controleer In dit bestand opslaan.
9. Bewerk Hallo build-definitie (sluit als het al geopend is), en selecteer Hallo **nieuw** knop als u nog niet Hallo nieuwe sjabloon in de lijst Hallo van processjablonen ziet.
10. Hallo eigenschap parameterwaarden in Hallo div sectie als volgt instellen:

    1. CloudConfigLocation ='c:\\zakt\\app.publish\\ServiceConfiguration.Cloud.cscfg' *deze waarde is afgeleid van: ($PublishDir)ServiceConfiguration.Cloud.cscfg*
    2. PackageLocation = ' c:\\zakt\\app.publish\\ContactManager.Azure.cspkg' *deze waarde is afgeleid van: ($PublishDir)($ProjectName) .cspkg*
    3. PublishScriptLocation = ' c:\\scripts\\WindowsAzure\\PublishCloudService.ps1'
    4. ServiceName = 'mycloudservicename' *gebruik Hallo juiste cloudservicenaam hier*
    5. Omgeving = 'Fasering'
    6. StorageAccountName = 'mystorageaccountname' *gebruik Hallo juiste opslagaccountnaam hier*
    7. SubscriptionDataFileLocation = ' c:\\scripts\\WindowsAzure\\Subscription.xml'
    8. SubscriptionName = 'default'

    ![Eigenschap parameterwaarden][6]
11. Hallo wijzigingen toohello bouwen definitie opslaan.
12. Een Build tooexecute beide Hallo pakket build en publiceren van de verzendwachtrij. Als u een trigger tooContinuous integratie ingesteld, kunt u dit gedrag wordt uitgevoerd bij elke controle.

### <a name="publishcloudserviceps1-script-template"></a>PublishCloudService.ps1 script sjabloon
```
Param(  $serviceName = "",
        $storageAccountName = "",
        $packageLocation = "",
        $cloudConfigLocation = "",
        $environment = "Staging",
        $deploymentLabel = "ContinuousDeploy too$servicename",
        $timeStampFormat = "g",
        $alwaysDeleteExistingDeployments = 1,
        $enableDeploymentUpgrade = 1,
        $selectedsubscription = "default",
        $subscriptionDataFile = ""
     )


function Publish()
{
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot -ErrorVariable a -ErrorAction silentlycontinue
    if ($a[0] -ne $null)
    {
        Write-Output "$(Get-Date -f $timeStampFormat) - No deployment is detected. Creating a new deployment. "
    }
    #check for existing deployment and then either upgrade, delete + deploy, or cancel according too$alwaysDeleteExistingDeployments and $enableDeploymentUpgrade boolean variables
    if ($deployment.Name -ne $null)
    {
        switch ($alwaysDeleteExistingDeployments)
        {
            1
            {
                switch ($enableDeploymentUpgrade)
                {
                    1  #Update deployment inplace (usually faster, cheaper, won't destroy VIP)
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Upgrading deployment."
                        UpgradeDeployment
                    }
                    0  #Delete then create new deployment
                    {
                        Write-Output "$(Get-Date -f $timeStampFormat) - Deployment exists in $servicename.  Deleting deployment."
                        DeleteDeployment
                        CreateNewDeployment

                    }
                } # switch ($enableDeploymentUpgrade)
            }
            0
            {
                Write-Output "$(Get-Date -f $timeStampFormat) - ERROR: Deployment exists in $servicename.  Script execution cancelled."
                exit
            }
        } #switch ($alwaysDeleteExistingDeployments)
    } else {
            CreateNewDeployment
    }
}

function CreateNewDeployment()
{
    write-progress -id 3 -activity "Creating New Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: In progress"

    $opstat = New-AzureDeployment -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Creating New Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Creating New Deployment: Complete, Deployment ID: $completeDeploymentID"

    StartInstances
}

function UpgradeDeployment()
{
    write-progress -id 3 -activity "Upgrading Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: In progress"

    # perform Update-Deployment
    $setdeployment = Set-AzureDeployment -Upgrade -Slot $slot -Package $packageLocation -Configuration $cloudConfigLocation -label $deploymentLabel -ServiceName $serviceName -Force

    $completeDeployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $completeDeploymentID = $completeDeployment.deploymentid

    write-progress -id 3 -activity "Upgrading Deployment" -completed -Status "Complete"
    Write-Output "$(Get-Date -f $timeStampFormat) - Upgrading Deployment: Complete, Deployment ID: $completeDeploymentID"
}

function DeleteDeployment()
{

    write-progress -id 2 -activity "Deleting Deployment" -Status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: In progress"

    #WARNING - always deletes with force
    $removeDeployment = Remove-AzureDeployment -Slot $slot -ServiceName $serviceName -Force

    write-progress -id 2 -activity "Deleting Deployment: Complete" -completed -Status $removeDeployment
    Write-Output "$(Get-Date -f $timeStampFormat) - Deleting Deployment: Complete"

}

function StartInstances()
{
    write-progress -id 4 -activity "Starting Instances" -status "In progress"
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: In progress"

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $runstatus = $deployment.Status

    if ($runstatus -ne 'Running')
    {
        $run = Set-AzureDeployment -Slot $slot -ServiceName $serviceName -Status Running
    }
    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $oldStatusStr = @("") * $deployment.RoleInstanceList.Count

    while (-not(AllInstancesRunning($deployment.RoleInstanceList)))
    {
        $i = 1
        foreach ($roleInstance in $deployment.RoleInstanceList)
        {
            $instanceName = $roleInstance.InstanceName
            $instanceStatus = $roleInstance.InstanceStatus

            if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
            {
                $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
                Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
            }

            write-progress -id (4 + $i) -activity "Starting Instance '$instanceName'" -status "$instanceStatus"
            $i = $i + 1
        }

        sleep -Seconds 1

        $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    }

    $i = 1
    foreach ($roleInstance in $deployment.RoleInstanceList)
    {
        $instanceName = $roleInstance.InstanceName
        $instanceStatus = $roleInstance.InstanceStatus

        if ($oldStatusStr[$i - 1] -ne $roleInstance.InstanceStatus)
        {
            $oldStatusStr[$i - 1] = $roleInstance.InstanceStatus
            Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instance '$instanceName': $instanceStatus"
        }

        $i = $i + 1
    }

    $deployment = Get-AzureDeployment -ServiceName $serviceName -Slot $slot
    $opstat = $deployment.Status

    write-progress -id 4 -activity "Starting Instances" -completed -status $opstat
    Write-Output "$(Get-Date -f $timeStampFormat) - Starting Instances: $opstat"
}

function AllInstancesRunning($roleInstanceList)
{
    foreach ($roleInstance in $roleInstanceList)
    {
        if ($roleInstance.InstanceStatus -ne "ReadyRole")
        {
            return $false
        }
    }

    return $true
}

#configure powershell with Azure 1.7 modules
Import-Module Azure

#configure powershell with publishsettings for your subscription
$pubsettings = $subscriptionDataFile
Import-AzurePublishSettingsFile $pubsettings
Set-AzureSubscription -CurrentStorageAccountName $storageAccountName -SubscriptionName $selectedsubscription
Select-AzureSubscription $selectedsubscription

#set remaining environment variables for Azure cmdlets
$subscription = Get-AzureSubscription $selectedsubscription
$subscriptionname = $subscription.subscriptionname
$subscriptionid = $subscription.subscriptionid
$slot = $environment

#main driver - publish & write progress tooactivity log
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script started."
Write-Output "$(Get-Date -f $timeStampFormat) - Preparing deployment of $deploymentLabel for $subscriptionname with Subscription ID $subscriptionid."

Publish

$deployment = Get-AzureDeployment -slot $slot -serviceName $servicename
$deploymentUrl = $deployment.Url

Write-Output "$(Get-Date -f $timeStampFormat) - Created Cloud Service with URL $deploymentUrl."
Write-Output "$(Get-Date -f $timeStampFormat) - Azure Cloud Service deploy script finished."
```

## <a name="next-steps"></a>Volgende stappen
Zie tooenable foutopsporing op afstand bij gebruik van doorlopende levering [foutopsporing op afstand inschakelen wanneer u doorlopende levering toopublish tooAzure](cloud-services-virtual-machines-dotnet-continuous-delivery-remote-debugging.md).

[Team Foundation Build Service]: https://msdn.microsoft.com/library/ee259687.aspx
[.NET Framework 4]: https://www.microsoft.com/download/details.aspx?id=17851
[.NET Framework 4.5]: https://www.microsoft.com/download/details.aspx?id=30653
[.NET Framework 4.5.2]: https://www.microsoft.com/download/details.aspx?id=42643
[Scale out your build system]: https://msdn.microsoft.com/library/dd793166.aspx
[Deploy and configure a build server]: https://msdn.microsoft.com/library/ms181712.aspx
[Azure PowerShell cmdlets]: /powershell/azureps-cmdlets-docs
[hello .publishsettings file]: https://manage.windowsazure.com/download/publishprofile.aspx?wa=wsignin1.0
[0]: ./media/cloud-services-dotnet-continuous-delivery/tfs-01bc.png
[2]: ./media/cloud-services-dotnet-continuous-delivery/tfs-02.png
[3]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-03.png
[4]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-04.png
[5]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-05.png
[6]: ./media/cloud-services-dotnet-continuous-delivery/common-task-tfs-06.png
