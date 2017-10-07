---
title: aaaLearn over Azure microservices beveiligingsbeleid | Microsoft Docs
description: Een overzicht van hoe toorun een Service Fabric-toepassing onder systeem en voor lokale beveiligingsaccounts, met inbegrip van Hallo SetupEntry punt waarin een toepassing tooperform sommige moet actie beschermde voordat deze wordt gestart
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a>Beveiligingsbeleid configureren voor uw toepassing
U kunt toepassingen die worden uitgevoerd in de cluster Hallo onder verschillende gebruikersaccounts beveiligen met behulp van Azure Service Fabric. Service Fabric kunt u ook beveiligde Hallo resources die worden gebruikt door toepassingen op moment van implementatie onder Hallo gebruikersaccounts--Hallo bijvoorbeeld, bestanden, mappen en certificaten. Hierdoor waarop toepassingen worden uitgevoerd, zelfs in een gedeelde gehoste omgeving veiliger van elkaar.

Service Fabric-toepassingen worden standaard uitgevoerd onder Hallo-account dat Hallo Fabric.exe-proces wordt uitgevoerd onder. Service Fabric biedt tevens de mogelijkheid Hallo toorun toepassingen met een lokale gebruikersaccount of het lokale systeemaccount gebruikt, is opgegeven in het manifest toepassing hello. Ondersteunde lokaal systeem accounttypen zijn **LocalUser**, **NetworkService**, **LocalService**, en **LocalSystem**.

 Als u Service Fabric op Windows Server in uw datacenter met behulp van Hallo zelfstandig installatieprogramma, kunt u Active Directory-domeinaccounts, met inbegrip van beheerde serviceaccounts voor groepen.

U kunt definiëren en gebruikersgroepen maken zodat tooeach groep toobe samen beheerd door een of meer gebruikers kunnen worden toegevoegd. Dit is handig wanneer er meerdere gebruikers voor verschillende toegangspunten en ze toohave bepaalde algemene rechten die beschikbaar op Hallo groepeerniveau zijn nodig.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Hallo-beleid voor een toegangspunt voor service-instellingen configureren
Zoals beschreven in Hallo [toepassingsmodel](service-fabric-application-model.md), setup ingangspunt Hallo **entrypoint**, is een bevoorrechte toegangspunt dat wordt uitgevoerd met dezelfde referenties als Service Fabric hello (meestal Hallo *NetworkService* account) voordat andere toegangspunt. Hallo uitvoerbaar bestand dat is opgegeven door **EntryPoint** is doorgaans Hallo langlopende ServiceHost. Dus met een afzonderlijke installatie ingangspunt zo voorkomt u dat toorun Hallo-ServiceHost uitvoerbare met hoge bevoegdheden voor langere tijd. Hallo uitvoerbare die **EntryPoint** geeft wordt uitgevoerd na **entrypoint** is afgesloten. Hallo resulterende proces wordt bewaakt en opnieuw opgestart, en opnieuw begint met **entrypoint** ooit wordt beëindigd als of als deze is vastgelopen.

Hallo volgende is een eenvoudige service manifest-voorbeeld dat toont Hallo entrypoint en Hallo belangrijkste EntryPoint voor Hallo-service.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a>Hallo-beleid configureren met behulp van een lokaal account
Nadat u Hallo service toohave een toegangspunt setup configureert, kunt u Hallo beveiligingsmachtigingen die wordt uitgevoerd onder in het toepassingsmanifest Hallo wijzigen. Hallo volgende voorbeeld ziet u hoe tooconfigure Hallo service toorun onder gebruikersbevoegdheden administrator-account.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

Maak eerst een **Principals** sectie met een gebruikersnaam, zoals SetupAdminUser. Dit betekent dat Hallo-gebruiker is lid van de beheerdersgroep system Hallo.

Vervolgens onder Hallo **ServiceManifestImport** sectie, configureer een beleid tooapply deze principal te**entrypoint**. Dit vertelt Service Fabric die wanneer hello **MySetup.bat** -bestand wordt uitgevoerd, dit moet `RunAs` met administrator-bevoegdheden. Gezien het feit dat u hebt *niet* toegepast een beleid toohello Hoofdingangspunt, Hallo-code in **MyServiceHost.exe** wordt uitgevoerd onder Hallo systeem **NetworkService** account. Dit is Hallo standaardaccount op dat alle toegangspunten van de service worden uitgevoerd.

Laten we nu toevoegen Hallo bestand MySetup.bat toohello Visual Studio-project tootest Hallo administrator-bevoegdheden. In Visual Studio met de rechtermuisknop op het Hallo-service-project en voeg een nieuw bestand met de naam MySetup.bat.

Controleer vervolgens dat Hallo MySetup.bat-bestand is opgenomen in het servicepakket Hallo. Standaard is dit niet. Selecteer Hallo-bestand, met de rechtermuisknop op tooget Hallo contextmenu en kiest u **eigenschappen**. Zorg ervoor dat in het dialoogvenster Eigenschappen hello, **tooOutput Directory kopiëren** te is ingesteld,**kopiëren indien nieuwer**. Zie Hallo volgende schermopname.

![Visual Studio CopyToOutput voor batchbestand entrypoint][image1]

Nu Hallo MySetup.bat bestand openen en voeg toe Hallo volgende opdrachten:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

Vervolgens bouwen en implementeren van Hallo oplossing tooa lokaal ontwikkelcluster. Nadat het Hallo-service is gestart, zoals wordt weergegeven in Service Fabric Explorer, kunt u zien dat Hallo MySetup.bat-bestand in een op twee manieren geslaagd. Open een PowerShell-opdrachtprompt en typ:

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Noteer Hallo-naam van Hallo knooppunt waarbij Hallo-service is geïmplementeerd en 2 is gestart in Service Fabric Explorer--bijvoorbeeld knooppunt. Vervolgens gaat u toohello toepassing exemplaar map toofind hello out.txt werkbestand waarin Hallo-waarde voor **TestVariable**. Bijvoorbeeld, als deze service geïmplementeerd tooNode 2 is, vervolgens kunt u gaan toothis pad voor Hallo **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Hallo-beleid configureren met behulp van lokaal systeemaccounts
Het is vaak beter toorun Hallo opstartscript met behulp van een lokale systeemaccount in plaats van een administrator-account. Hallo RunAs beleid uitgevoerd als een lid van Hallo beheerdersgroep doorgaans werkt niet goed omdat machines gebruikers toegang Gebruikersaccountbeheer (UAC) is standaard ingeschakeld hebben. In dergelijke gevallen **Hallo aanbeveling is toorun Hallo entrypoint als LocalSystem, in plaats van als een lokale gebruikersgroep met toegevoegde tooAdministrators**. Hallo volgende voorbeeld toont instelling Hallo entrypoint toorun als LocalSystem:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>PowerShell-opdrachten starten vanuit een toegangspunt setup.
toorun PowerShell van Hallo **entrypoint** punt, u kunt uitvoeren **PowerShell.exe** bestand in een batchbestand dat tooa PowerShell verwijst. Voeg eerst een PowerShell-bestand toohello serviceproject--bijvoorbeeld **MySetup.ps1**. Houd er rekening mee tooset hello *kopiëren indien nieuwer* , zodat de dat bestand Hallo is ook opgenomen in het servicepakket Hallo. Hallo volgende voorbeeld ziet u een batch voorbeeldbestand die een PowerShell-bestand aangeroepen MySetup.ps1 die Hiermee stelt u een systeemomgevingsvariabele aangeroepen begint **TestVariable**.

MySetup.bat toostart een PowerShell-bestand:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

In Hallo PowerShell-bestand toevoegen Hallo tooset een systeemomgevingsvariabele te volgen:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> Standaard wanneer Hallo batchbestand wordt uitgevoerd, wordt er gezocht op Hallo toepassingsmap met de naam **werken** voor bestanden. In dit geval wanneer MySetup.bat wordt uitgevoerd, willen we deze toofind hello MySetup.ps1 bestand Hallo dezelfde map Hallo Application **codepakket** map. toochange set Hallo-werkmap, deze map:
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a>Console-omleiding gebruiken voor lokale foutopsporing
Soms is het nuttig toosee Hallo console-uitvoer van het uitvoeren van een script voor foutopsporing. toodo, kunt u een console Omleidingsbeleid, schrijft Hallo tooa uitvoerbestand instellen. Hallo bestand uitvoer geschreven toohello toepassingsmap heet **logboek** op Hallo knooppunt waar de toepassing hello wordt geïmplementeerd en uitgevoerd. (Zie toofind dit in het voorgaande voorbeeld Hallo.)

> [!WARNING]
> Gebruik nooit Omleidingsbeleid Hallo-console in een toepassing die is geïmplementeerd in productie, omdat dit Hallo toepassing failover kan beïnvloeden. *Alleen* Gebruik deze optie voor lokale ontwikkeling en foutopsporing.  
> 
> 

Hallo toont volgende voorbeeld instelling Hallo console-omleiding met een waarde FileRetentionCount:

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Als u nu Hallo MySetup.ps1 bestand toowrite wijzigt een **Echo** uitvoert, en dit toohello uitvoerbestand voor foutopsporing worden geschreven:

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Nadat u fouten opsporen in uw script, onmiddellijk verwijderen van deze console Omleidingsbeleid**.

## <a name="configure-a-policy-for-service-code-packages"></a>Configureer een beleid voor servicepakketten code
In de Hallo vorige stappen, hebt u gezien hoe tooapply een tooSetupEntryPoint RunAs-beleid. We bekijken een beetje dieper in hoe toocreate verschillende principals die kunnen worden toegepast als service voor beleid.

### <a name="create-local-user-groups"></a>Lokale gebruikersgroepen maken
U kunt definiëren en maak gebruikersgroepen waarmee een of meer gebruikers toobe tooa groep toegevoegd. Dit is handig als er meerdere gebruikers voor verschillende toegangspunten en ze toohave bepaalde algemene rechten die beschikbaar op Hallo groepeerniveau zijn nodig. Hallo volgende voorbeeld ziet u een lokale groep genaamd **LocalAdminGroup** die administrator-bevoegdheden heeft. Twee gebruikers, Customer1 en Customer2, worden leden van deze lokale groep gemaakt.

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a>Lokale gebruikers maken
U kunt een lokale gebruiker die gebruikt toohelp veilig worden kan een service in de toepassing hello maken. Wanneer een **LocalUser** accounttype is opgegeven in Hallo principals sectie van het toepassingsmanifest hello, Service Fabric lokale gebruikersaccounts maakt op computers waarop de toepassing hello wordt geïmplementeerd. Deze accounts hoeft standaard geen Hallo dezelfde naam als die zijn opgegeven in de toepassing hello manifest (bijvoorbeeld Customer3 in Hallo volgende voorbeeld). In plaats daarvan dynamisch worden gegenereerd en willekeurige wachtwoorden hebben.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Als een toepassing vereist dat Hallo-gebruikersaccount en wachtwoord niet hetzelfde zijn op alle machines (bijvoorbeeld tooenable NTLM-verificatie), moet het clustermanifest hello NTLMAuthenticationEnabled tootrue ingesteld. Hallo clustermanifest moet ook opgeven voor een NTLMAuthenticationPasswordSecret die wordt gebruikt toogenerate Hallo hetzelfde wachtwoord alle machines.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Beleid toohello code servicepakketten toewijzen
Hallo **RunAsPolicy** sectie voor een **ServiceManifestImport** Hiermee geeft u de account Hallo van Hallo principals sectie gebruikte toorun een codepakket moet. Pakketten van Hallo service manifest code wordt gekoppeld met een gebruikersaccount in Hallo principals sectie. U kunt dit opgeven voor het Hallo-setup of belangrijkste toegangspunten, of u kunt opgeven `All` tooapply het tooboth. Hallo volgende voorbeeld ziet u verschillende soorten beleid wordt toegepast:

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Als **EntryPointType** niet is opgegeven, Hallo standaard is ingesteld tooEntryPointType = 'Main'. Geven **entrypoint** is vooral nuttig wanneer u toorun wilt dat bepaalde installatiebewerkingen hoge privileges met een systeemaccount. Hallo werkelijke service programmacode kan worden uitgevoerd onder een account met kleine-bevoegdheden.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Een standaard beleid tooall service code pakketten toepassen
Gebruik van Hallo **DefaultRunAsPolicy** sectie toospecify een standaardgebruikersaccount voor alle pakketten van code die een specifieke geen **RunAsPolicy** gedefinieerd. Als de meeste Hallo code pakketten die zijn opgegeven in het Hallo-servicemanifest gebruikt door een toepassing moet toorun onder Hallo dezelfde gebruiker hello toepassing kunt alleen een standaardbeleid RunAs met dat gebruikersaccount definiëren. Hallo volgende voorbeeld wordt opgegeven dat als een codepakket geen heeft een **RunAsPolicy** opgegeven, Hallo codepakket moet worden uitgevoerd onder Hallo **MyDefaultAccount** in Hallo principals sectie hebt opgegeven.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Gebruik van een gebruiker of groep voor Active Directory-domein
U kunt voor een exemplaar van de Service-infrastructuur die is geïnstalleerd op Windows Server met behulp van Hallo zelfstandig installatieprogramma Hallo service onder Hallo referenties voor een Active Directory-gebruiker of groep account uitvoeren. Dit is van Active Directory on-premises binnen uw domein en is niet met Azure Active Directory (Azure AD). U kunt andere bronnen in Hallo-domein (bijvoorbeeld bestandsshares) die machtigingen hebben gekregen benaderen via een domeingebruiker of -groep.

Hallo volgende voorbeeld ziet u een Active Directory-gebruiker aangeroepen *testgebruiker* met hun domein wachtwoord dat wordt versleuteld met behulp van een certificaat genoemd *MyCert*. U kunt Hallo `Invoke-ServiceFabricEncryptText` PowerShell-opdracht toocreate Hallo geheime gecodeerde tekst. Zie [geheimen in Service Fabric-toepassingen beheren](service-fabric-application-secret-management.md) voor meer informatie.

Moet u de persoonlijke sleutel Hallo van Hallo certificaat toodecrypt Hallo wachtwoord toohello lokale machine implementeren met behulp van een out-of-band-methode (dit is in Azure, via Azure Resource Manager). Vervolgens wanneer Service Fabric Hallo service pakket toohello machine implementeert, kunnen toodecrypt Hallo geheim en verifiëren met Active Directory-toorun onder deze referenties (samen met de naam van de gebruiker Hallo).

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a>Gebruik een groep beheerd serviceaccount.
U kunt voor een exemplaar van de Service-infrastructuur die is geïnstalleerd op Windows Server met behulp van Hallo zelfstandig installatieprogramma Hallo service uitvoeren als een groep beheerde serviceaccounts (gMSA). Active Directory wordt on-premises binnen uw domein en is niet met Azure Active Directory (Azure AD). Met behulp van een gMSA er is geen wachtwoord of het versleutelde wachtwoord opgeslagen in Hallo `Application Manifest`.

Hallo volgende voorbeeld laat zien hoe toocreate een gMSA-account genoemd *svc-Test$*; hoe toodeploy die worden beheerd clusterknooppunten voor service-account toohello; en hoe tooconfigure Hallo UPN.

##### <a name="prerequisites"></a>Vereisten.
- Hallo-domein moet een KDS-hoofdsleutel.
- Hallo-domein moet toobe op een Windows Server 2012 of hoger functionaliteitsniveau.

##### <a name="example"></a>Voorbeeld
1. De beheerder van een active directory-domein maken van een groep beheerd serviceaccount met Hallo hebben `New-ADServiceAccount` commandlet en zorg ervoor dat Hallo `PrincipalsAllowedToRetrieveManagedPassword` bevat alle clusterknooppunten van Hallo service fabric. Houd er rekening mee dat `AccountName`, `DnsHostName`, en `ServicePrincipalName` moeten uniek zijn.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. Op elk knooppunt Hallo service fabric-cluster (bijvoorbeeld `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), installeren en te testen Hallo gMSA.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Configureer Hallo User principal en Hallo RunAsPolicy tooreference Hallo gebruiker configureren.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Toewijzen van een beveiligingsbeleid voor toegang voor HTTP en HTTPS-eindpunten
Als u een RunAs-service voor beleid tooa toepassen en Hallo servicemanifest eindpunt resources met Hallo HTTP-protocol declareert, moet u een **SecurityAccessPolicy** tooensure dat poorten toothese eindpunten toegewezen correct zijn Access control vermeld voor Hallo RunAs-gebruikersaccount dat Hallo-service wordt uitgevoerd. Anders **http.sys** geen toegang toohello service en voor het ophalen van de fouten met aanroepen van Hallo-client. Hallo volgende voorbeeld wordt Hallo Customer1 account tooan eindpunt aangeroepen **EndpointName**, waardoor het volledige toegangsrechten.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Voor de HTTPS-eindpunt hello hebt u ook tooindicate Hallo-naam van Hallo certificaat tooreturn toohello client. U kunt dit doen met behulp van **EndpointBindingPolicy**, met gedefinieerd in een sectie certificaten in het toepassingsmanifest Hallo Hallo-certificaat.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Bijwerken van meerdere toepassingen met https-eindpunten
U moet toobe zorgvuldige niet toouse hello **dezelfde poort** voor verschillende exemplaren van Hallo dezelfde toepassing als u http gebruikt**s**. Hallo reden is dat het Service Fabric kunnen tooupgrade HALLO cert voor een van de exemplaren van een toepassing hello niet kan worden. Bijvoorbeeld als toepassing 1 of een toepassing 2 beide wilt tooupgrade hun certificaat 1 toocert 2. Wanneer Hallo upgrade gebeurt, Service Fabric mogelijk zijn opgeschoond Hallo certificaat 1 registratie bij http.sys Hoewel hello andere toepassing wordt nog steeds gebruikt. tooprevent dit Service Fabric detecteert dat er al een ander exemplaar op Hallo poort met Hallo certificaat geregistreerd (vanwege toohttp.sys) en mislukt de bewerking Hallo.

Daarom Service Fabric biedt geen ondersteuning voor twee verschillende services met behulp van een upgrade **Hallo dezelfde poort** in exemplaren van een andere toepassing. Met andere woorden, u Hallo dezelfde van het certificaat niet gebruiken voor andere services op Hallo dezelfde poort. Als u toohave moet een gedeelde certificaten op Hallo dezelfde poort u tooensure dat services worden geplaatst op verschillende computers met plaatsingsbeperkingen Hallo nodig. Of Overweeg het gebruik van dynamische poorten Service Fabric indien mogelijk voor elke service in elk toepassingsexemplaar. 

Als u een upgrade is mislukt met https, een fout waarschuwing wordt weergegeven met de tekst "Hallo Windows HTTP-Server API ondersteunt geen meerdere certificaten voor toepassingen die een poort delen."

## <a name="a-complete-application-manifest-example"></a>Een voorbeeld van een volledige toepassing manifest
Hallo na het toepassingsmanifest bevat veel Hallo verschillende instellingen:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Volgende stappen
* [Hallo toepassingsmodel begrijpen](service-fabric-application-model.md)
* [Bronnen opgeven in een servicemanifest](service-fabric-service-manifest-resources.md)
* [Een toepassing implementeren](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
