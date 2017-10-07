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
# <a name="configure-security-policies-for-your-application"></a><span data-ttu-id="812e2-103">Beveiligingsbeleid configureren voor uw toepassing</span><span class="sxs-lookup"><span data-stu-id="812e2-103">Configure security policies for your application</span></span>
<span data-ttu-id="812e2-104">U kunt toepassingen die worden uitgevoerd in de cluster Hallo onder verschillende gebruikersaccounts beveiligen met behulp van Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="812e2-104">By using Azure Service Fabric, you can secure applications that are running in hello cluster under different user accounts.</span></span> <span data-ttu-id="812e2-105">Service Fabric kunt u ook beveiligde Hallo resources die worden gebruikt door toepassingen op moment van implementatie onder Hallo gebruikersaccounts--Hallo bijvoorbeeld, bestanden, mappen en certificaten.</span><span class="sxs-lookup"><span data-stu-id="812e2-105">Service Fabric also helps secure hello resources that are used by applications at hello time of deployment under hello user accounts--for example, files, directories, and certificates.</span></span> <span data-ttu-id="812e2-106">Hierdoor waarop toepassingen worden uitgevoerd, zelfs in een gedeelde gehoste omgeving veiliger van elkaar.</span><span class="sxs-lookup"><span data-stu-id="812e2-106">This makes running applications, even in a shared hosted environment, more secure from one another.</span></span>

<span data-ttu-id="812e2-107">Service Fabric-toepassingen worden standaard uitgevoerd onder Hallo-account dat Hallo Fabric.exe-proces wordt uitgevoerd onder.</span><span class="sxs-lookup"><span data-stu-id="812e2-107">By default, Service Fabric applications run under hello account that hello Fabric.exe process runs under.</span></span> <span data-ttu-id="812e2-108">Service Fabric biedt tevens de mogelijkheid Hallo toorun toepassingen met een lokale gebruikersaccount of het lokale systeemaccount gebruikt, is opgegeven in het manifest toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="812e2-108">Service Fabric also provides hello capability toorun applications under a local user account or local system account, which is specified within hello application manifest.</span></span> <span data-ttu-id="812e2-109">Ondersteunde lokaal systeem accounttypen zijn **LocalUser**, **NetworkService**, **LocalService**, en **LocalSystem**.</span><span class="sxs-lookup"><span data-stu-id="812e2-109">Supported local system account types are **LocalUser**, **NetworkService**, **LocalService**, and **LocalSystem**.</span></span>

 <span data-ttu-id="812e2-110">Als u Service Fabric op Windows Server in uw datacenter met behulp van Hallo zelfstandig installatieprogramma, kunt u Active Directory-domeinaccounts, met inbegrip van beheerde serviceaccounts voor groepen.</span><span class="sxs-lookup"><span data-stu-id="812e2-110">When you're running Service Fabric on Windows Server in your datacenter by using hello standalone installer, you can use Active Directory domain accounts, including group managed service accounts.</span></span>

<span data-ttu-id="812e2-111">U kunt definiëren en gebruikersgroepen maken zodat tooeach groep toobe samen beheerd door een of meer gebruikers kunnen worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="812e2-111">You can define and create user groups so that one or more users can be added tooeach group toobe managed together.</span></span> <span data-ttu-id="812e2-112">Dit is handig wanneer er meerdere gebruikers voor verschillende toegangspunten en ze toohave bepaalde algemene rechten die beschikbaar op Hallo groepeerniveau zijn nodig.</span><span class="sxs-lookup"><span data-stu-id="812e2-112">This is useful when there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span>

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a><span data-ttu-id="812e2-113">Hallo-beleid voor een toegangspunt voor service-instellingen configureren</span><span class="sxs-lookup"><span data-stu-id="812e2-113">Configure hello policy for a service setup entry point</span></span>
<span data-ttu-id="812e2-114">Zoals beschreven in Hallo [toepassingsmodel](service-fabric-application-model.md), setup ingangspunt Hallo **entrypoint**, is een bevoorrechte toegangspunt dat wordt uitgevoerd met dezelfde referenties als Service Fabric hello (meestal Hallo *NetworkService* account) voordat andere toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="812e2-114">As described in hello [application model](service-fabric-application-model.md), hello setup entry point, **SetupEntryPoint**, is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *NetworkService* account) before any other entry point.</span></span> <span data-ttu-id="812e2-115">Hallo uitvoerbaar bestand dat is opgegeven door **EntryPoint** is doorgaans Hallo langlopende ServiceHost.</span><span class="sxs-lookup"><span data-stu-id="812e2-115">hello executable that is specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="812e2-116">Dus met een afzonderlijke installatie ingangspunt zo voorkomt u dat toorun Hallo-ServiceHost uitvoerbare met hoge bevoegdheden voor langere tijd.</span><span class="sxs-lookup"><span data-stu-id="812e2-116">So having a separate setup entry point avoids having toorun hello service host executable with high privileges for extended periods of time.</span></span> <span data-ttu-id="812e2-117">Hallo uitvoerbare die **EntryPoint** geeft wordt uitgevoerd na **entrypoint** is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="812e2-117">hello executable that **EntryPoint** specifies is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="812e2-118">Hallo resulterende proces wordt bewaakt en opnieuw opgestart, en opnieuw begint met **entrypoint** ooit wordt beëindigd als of als deze is vastgelopen.</span><span class="sxs-lookup"><span data-stu-id="812e2-118">hello resulting process is monitored and restarted, and begins again with **SetupEntryPoint** if it ever terminates or crashes.</span></span>

<span data-ttu-id="812e2-119">Hallo volgende is een eenvoudige service manifest-voorbeeld dat toont Hallo entrypoint en Hallo belangrijkste EntryPoint voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="812e2-119">hello following is a simple service manifest example that shows hello SetupEntryPoint and hello main EntryPoint for hello service.</span></span>

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

### <a name="configure-hello-policy-by-using-a-local-account"></a><span data-ttu-id="812e2-120">Hallo-beleid configureren met behulp van een lokaal account</span><span class="sxs-lookup"><span data-stu-id="812e2-120">Configure hello policy by using a local account</span></span>
<span data-ttu-id="812e2-121">Nadat u Hallo service toohave een toegangspunt setup configureert, kunt u Hallo beveiligingsmachtigingen die wordt uitgevoerd onder in het toepassingsmanifest Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="812e2-121">After you configure hello service toohave a setup entry point, you can change hello security permissions that it runs under in hello application manifest.</span></span> <span data-ttu-id="812e2-122">Hallo volgende voorbeeld ziet u hoe tooconfigure Hallo service toorun onder gebruikersbevoegdheden administrator-account.</span><span class="sxs-lookup"><span data-stu-id="812e2-122">hello following example shows how tooconfigure hello service toorun under user administrator account privileges.</span></span>

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

<span data-ttu-id="812e2-123">Maak eerst een **Principals** sectie met een gebruikersnaam, zoals SetupAdminUser.</span><span class="sxs-lookup"><span data-stu-id="812e2-123">First, create a **Principals** section with a user name, such as SetupAdminUser.</span></span> <span data-ttu-id="812e2-124">Dit betekent dat Hallo-gebruiker is lid van de beheerdersgroep system Hallo.</span><span class="sxs-lookup"><span data-stu-id="812e2-124">This indicates that hello user is a member of hello Administrators system group.</span></span>

<span data-ttu-id="812e2-125">Vervolgens onder Hallo **ServiceManifestImport** sectie, configureer een beleid tooapply deze principal te**entrypoint**.</span><span class="sxs-lookup"><span data-stu-id="812e2-125">Next, under hello **ServiceManifestImport** section, configure a policy tooapply this principal too**SetupEntryPoint**.</span></span> <span data-ttu-id="812e2-126">Dit vertelt Service Fabric die wanneer hello **MySetup.bat** -bestand wordt uitgevoerd, dit moet `RunAs` met administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="812e2-126">This tells Service Fabric that when hello **MySetup.bat** file is run, it should be `RunAs` with administrator privileges.</span></span> <span data-ttu-id="812e2-127">Gezien het feit dat u hebt *niet* toegepast een beleid toohello Hoofdingangspunt, Hallo-code in **MyServiceHost.exe** wordt uitgevoerd onder Hallo systeem **NetworkService** account.</span><span class="sxs-lookup"><span data-stu-id="812e2-127">Given that you have *not* applied a policy toohello main entry point, hello code in **MyServiceHost.exe** runs under hello system **NetworkService** account.</span></span> <span data-ttu-id="812e2-128">Dit is Hallo standaardaccount op dat alle toegangspunten van de service worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="812e2-128">This is hello default account that all service entry points are run as.</span></span>

<span data-ttu-id="812e2-129">Laten we nu toevoegen Hallo bestand MySetup.bat toohello Visual Studio-project tootest Hallo administrator-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="812e2-129">Let's now add hello file MySetup.bat toohello Visual Studio project tootest hello administrator privileges.</span></span> <span data-ttu-id="812e2-130">In Visual Studio met de rechtermuisknop op het Hallo-service-project en voeg een nieuw bestand met de naam MySetup.bat.</span><span class="sxs-lookup"><span data-stu-id="812e2-130">In Visual Studio, right-click hello service project and add a new file called MySetup.bat.</span></span>

<span data-ttu-id="812e2-131">Controleer vervolgens dat Hallo MySetup.bat-bestand is opgenomen in het servicepakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="812e2-131">Next, ensure that hello MySetup.bat file is included in hello service package.</span></span> <span data-ttu-id="812e2-132">Standaard is dit niet.</span><span class="sxs-lookup"><span data-stu-id="812e2-132">By default, it is not.</span></span> <span data-ttu-id="812e2-133">Selecteer Hallo-bestand, met de rechtermuisknop op tooget Hallo contextmenu en kiest u **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="812e2-133">Select hello file, right-click tooget hello context menu, and choose **Properties**.</span></span> <span data-ttu-id="812e2-134">Zorg ervoor dat in het dialoogvenster Eigenschappen hello, **tooOutput Directory kopiëren** te is ingesteld,**kopiëren indien nieuwer**.</span><span class="sxs-lookup"><span data-stu-id="812e2-134">In hello Properties dialog box, ensure that **Copy tooOutput Directory** is set too**Copy if newer**.</span></span> <span data-ttu-id="812e2-135">Zie Hallo volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="812e2-135">See hello following screenshot.</span></span>

![Visual Studio CopyToOutput voor batchbestand entrypoint][image1]

<span data-ttu-id="812e2-137">Nu Hallo MySetup.bat bestand openen en voeg toe Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="812e2-137">Now open hello MySetup.bat file and add hello following commands:</span></span>

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

<span data-ttu-id="812e2-138">Vervolgens bouwen en implementeren van Hallo oplossing tooa lokaal ontwikkelcluster.</span><span class="sxs-lookup"><span data-stu-id="812e2-138">Next, build and deploy hello solution tooa local development cluster.</span></span> <span data-ttu-id="812e2-139">Nadat het Hallo-service is gestart, zoals wordt weergegeven in Service Fabric Explorer, kunt u zien dat Hallo MySetup.bat-bestand in een op twee manieren geslaagd.</span><span class="sxs-lookup"><span data-stu-id="812e2-139">After hello service has started, as shown in Service Fabric Explorer, you can see that hello MySetup.bat file was successful in a two ways.</span></span> <span data-ttu-id="812e2-140">Open een PowerShell-opdrachtprompt en typ:</span><span class="sxs-lookup"><span data-stu-id="812e2-140">Open a PowerShell command prompt and type:</span></span>

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

<span data-ttu-id="812e2-141">Noteer Hallo-naam van Hallo knooppunt waarbij Hallo-service is geïmplementeerd en 2 is gestart in Service Fabric Explorer--bijvoorbeeld knooppunt.</span><span class="sxs-lookup"><span data-stu-id="812e2-141">Then, note hello name of hello node where hello service was deployed and started in Service Fabric Explorer--for example, Node 2.</span></span> <span data-ttu-id="812e2-142">Vervolgens gaat u toohello toepassing exemplaar map toofind hello out.txt werkbestand waarin Hallo-waarde voor **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="812e2-142">Next, navigate toohello application instance work folder toofind hello out.txt file that shows hello value of **TestVariable**.</span></span> <span data-ttu-id="812e2-143">Bijvoorbeeld, als deze service geïmplementeerd tooNode 2 is, vervolgens kunt u gaan toothis pad voor Hallo **MyApplicationType**:</span><span class="sxs-lookup"><span data-stu-id="812e2-143">For example, if this service was deployed tooNode 2, then you can go toothis path for hello **MyApplicationType**:</span></span>

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a><span data-ttu-id="812e2-144">Hallo-beleid configureren met behulp van lokaal systeemaccounts</span><span class="sxs-lookup"><span data-stu-id="812e2-144">Configure hello policy by using local system accounts</span></span>
<span data-ttu-id="812e2-145">Het is vaak beter toorun Hallo opstartscript met behulp van een lokale systeemaccount in plaats van een administrator-account.</span><span class="sxs-lookup"><span data-stu-id="812e2-145">Often, it's preferable toorun hello startup script by using a local system account rather than an administrator account.</span></span> <span data-ttu-id="812e2-146">Hallo RunAs beleid uitgevoerd als een lid van Hallo beheerdersgroep doorgaans werkt niet goed omdat machines gebruikers toegang Gebruikersaccountbeheer (UAC) is standaard ingeschakeld hebben.</span><span class="sxs-lookup"><span data-stu-id="812e2-146">Running hello RunAs policy as a member of hello Administrators group typically doesn’t work well because machines have User Access Control (UAC) enabled by default.</span></span> <span data-ttu-id="812e2-147">In dergelijke gevallen **Hallo aanbeveling is toorun Hallo entrypoint als LocalSystem, in plaats van als een lokale gebruikersgroep met toegevoegde tooAdministrators**.</span><span class="sxs-lookup"><span data-stu-id="812e2-147">In such cases, **hello recommendation is toorun hello SetupEntryPoint as LocalSystem, instead of as a local user added tooAdministrators group**.</span></span> <span data-ttu-id="812e2-148">Hallo volgende voorbeeld toont instelling Hallo entrypoint toorun als LocalSystem:</span><span class="sxs-lookup"><span data-stu-id="812e2-148">hello following example shows setting hello SetupEntryPoint toorun as LocalSystem:</span></span>

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

## <a name="start-powershell-commands-from-a-setup-entry-point"></a><span data-ttu-id="812e2-149">PowerShell-opdrachten starten vanuit een toegangspunt setup.</span><span class="sxs-lookup"><span data-stu-id="812e2-149">Start PowerShell commands from a setup entry point</span></span>
<span data-ttu-id="812e2-150">toorun PowerShell van Hallo **entrypoint** punt, u kunt uitvoeren **PowerShell.exe** bestand in een batchbestand dat tooa PowerShell verwijst.</span><span class="sxs-lookup"><span data-stu-id="812e2-150">toorun PowerShell from hello **SetupEntryPoint** point, you can run **PowerShell.exe** in a batch file that points tooa PowerShell file.</span></span> <span data-ttu-id="812e2-151">Voeg eerst een PowerShell-bestand toohello serviceproject--bijvoorbeeld **MySetup.ps1**.</span><span class="sxs-lookup"><span data-stu-id="812e2-151">First, add a PowerShell file toohello service project--for example, **MySetup.ps1**.</span></span> <span data-ttu-id="812e2-152">Houd er rekening mee tooset hello *kopiëren indien nieuwer* , zodat de dat bestand Hallo is ook opgenomen in het servicepakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="812e2-152">Remember tooset hello *Copy if newer* property so that hello file is also included in hello service package.</span></span> <span data-ttu-id="812e2-153">Hallo volgende voorbeeld ziet u een batch voorbeeldbestand die een PowerShell-bestand aangeroepen MySetup.ps1 die Hiermee stelt u een systeemomgevingsvariabele aangeroepen begint **TestVariable**.</span><span class="sxs-lookup"><span data-stu-id="812e2-153">hello following example shows a sample batch file that starts a PowerShell file called MySetup.ps1, which sets a system environment variable called **TestVariable**.</span></span>

<span data-ttu-id="812e2-154">MySetup.bat toostart een PowerShell-bestand:</span><span class="sxs-lookup"><span data-stu-id="812e2-154">MySetup.bat toostart a PowerShell file:</span></span>

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

<span data-ttu-id="812e2-155">In Hallo PowerShell-bestand toevoegen Hallo tooset een systeemomgevingsvariabele te volgen:</span><span class="sxs-lookup"><span data-stu-id="812e2-155">In hello PowerShell file, add hello following tooset a system environment variable:</span></span>

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> <span data-ttu-id="812e2-156">Standaard wanneer Hallo batchbestand wordt uitgevoerd, wordt er gezocht op Hallo toepassingsmap met de naam **werken** voor bestanden.</span><span class="sxs-lookup"><span data-stu-id="812e2-156">By default, when hello batch file runs, it looks at hello application folder called **work** for files.</span></span> <span data-ttu-id="812e2-157">In dit geval wanneer MySetup.bat wordt uitgevoerd, willen we deze toofind hello MySetup.ps1 bestand Hallo dezelfde map Hallo Application **codepakket** map.</span><span class="sxs-lookup"><span data-stu-id="812e2-157">In this case, when MySetup.bat runs, we want this toofind hello MySetup.ps1 file in hello same folder, which is hello application **code package** folder.</span></span> <span data-ttu-id="812e2-158">toochange set Hallo-werkmap, deze map:</span><span class="sxs-lookup"><span data-stu-id="812e2-158">toochange this folder, set hello working folder:</span></span>
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

## <a name="use-console-redirection-for-local-debugging"></a><span data-ttu-id="812e2-159">Console-omleiding gebruiken voor lokale foutopsporing</span><span class="sxs-lookup"><span data-stu-id="812e2-159">Use console redirection for local debugging</span></span>
<span data-ttu-id="812e2-160">Soms is het nuttig toosee Hallo console-uitvoer van het uitvoeren van een script voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="812e2-160">Occasionally, it's useful toosee hello console output from running a script for debugging purposes.</span></span> <span data-ttu-id="812e2-161">toodo, kunt u een console Omleidingsbeleid, schrijft Hallo tooa uitvoerbestand instellen.</span><span class="sxs-lookup"><span data-stu-id="812e2-161">toodo this, you can set a console redirection policy, which writes hello output tooa file.</span></span> <span data-ttu-id="812e2-162">Hallo bestand uitvoer geschreven toohello toepassingsmap heet **logboek** op Hallo knooppunt waar de toepassing hello wordt geïmplementeerd en uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="812e2-162">hello file output is written toohello application folder called **log** on hello node where hello application is deployed and run.</span></span> <span data-ttu-id="812e2-163">(Zie toofind dit in het voorgaande voorbeeld Hallo.)</span><span class="sxs-lookup"><span data-stu-id="812e2-163">(See where toofind this in hello preceding example.)</span></span>

> [!WARNING]
> <span data-ttu-id="812e2-164">Gebruik nooit Omleidingsbeleid Hallo-console in een toepassing die is geïmplementeerd in productie, omdat dit Hallo toepassing failover kan beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="812e2-164">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="812e2-165">*Alleen* Gebruik deze optie voor lokale ontwikkeling en foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="812e2-165">*Only* use this for local development and debugging purposes.</span></span>  
> 
> 

<span data-ttu-id="812e2-166">Hallo toont volgende voorbeeld instelling Hallo console-omleiding met een waarde FileRetentionCount:</span><span class="sxs-lookup"><span data-stu-id="812e2-166">hello following example shows setting hello console redirection with a FileRetentionCount value:</span></span>

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

<span data-ttu-id="812e2-167">Als u nu Hallo MySetup.ps1 bestand toowrite wijzigt een **Echo** uitvoert, en dit toohello uitvoerbestand voor foutopsporing worden geschreven:</span><span class="sxs-lookup"><span data-stu-id="812e2-167">If you now change hello MySetup.ps1 file toowrite an **Echo** command, this will write toohello output file for debugging purposes:</span></span>

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

<span data-ttu-id="812e2-168">**Nadat u fouten opsporen in uw script, onmiddellijk verwijderen van deze console Omleidingsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="812e2-168">**After you debug your script, immediately remove this console redirection policy**.</span></span>

## <a name="configure-a-policy-for-service-code-packages"></a><span data-ttu-id="812e2-169">Configureer een beleid voor servicepakketten code</span><span class="sxs-lookup"><span data-stu-id="812e2-169">Configure a policy for service code packages</span></span>
<span data-ttu-id="812e2-170">In de Hallo vorige stappen, hebt u gezien hoe tooapply een tooSetupEntryPoint RunAs-beleid.</span><span class="sxs-lookup"><span data-stu-id="812e2-170">In hello preceding steps, you saw how tooapply a RunAs policy tooSetupEntryPoint.</span></span> <span data-ttu-id="812e2-171">We bekijken een beetje dieper in hoe toocreate verschillende principals die kunnen worden toegepast als service voor beleid.</span><span class="sxs-lookup"><span data-stu-id="812e2-171">Let's look a little deeper into how toocreate different principals that can be applied as service policies.</span></span>

### <a name="create-local-user-groups"></a><span data-ttu-id="812e2-172">Lokale gebruikersgroepen maken</span><span class="sxs-lookup"><span data-stu-id="812e2-172">Create local user groups</span></span>
<span data-ttu-id="812e2-173">U kunt definiëren en maak gebruikersgroepen waarmee een of meer gebruikers toobe tooa groep toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="812e2-173">You can define and create user groups that allow one or more users toobe added tooa group.</span></span> <span data-ttu-id="812e2-174">Dit is handig als er meerdere gebruikers voor verschillende toegangspunten en ze toohave bepaalde algemene rechten die beschikbaar op Hallo groepeerniveau zijn nodig.</span><span class="sxs-lookup"><span data-stu-id="812e2-174">This is useful if there are multiple users for different service entry points and they need toohave certain common privileges that are available at hello group level.</span></span> <span data-ttu-id="812e2-175">Hallo volgende voorbeeld ziet u een lokale groep genaamd **LocalAdminGroup** die administrator-bevoegdheden heeft.</span><span class="sxs-lookup"><span data-stu-id="812e2-175">hello following example shows a local group called **LocalAdminGroup** that has administrator privileges.</span></span> <span data-ttu-id="812e2-176">Twee gebruikers, Customer1 en Customer2, worden leden van deze lokale groep gemaakt.</span><span class="sxs-lookup"><span data-stu-id="812e2-176">Two users, Customer1 and Customer2, are made members of this local group.</span></span>

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

### <a name="create-local-users"></a><span data-ttu-id="812e2-177">Lokale gebruikers maken</span><span class="sxs-lookup"><span data-stu-id="812e2-177">Create local users</span></span>
<span data-ttu-id="812e2-178">U kunt een lokale gebruiker die gebruikt toohelp veilig worden kan een service in de toepassing hello maken.</span><span class="sxs-lookup"><span data-stu-id="812e2-178">You can create a local user that can be used toohelp secure a service within hello application.</span></span> <span data-ttu-id="812e2-179">Wanneer een **LocalUser** accounttype is opgegeven in Hallo principals sectie van het toepassingsmanifest hello, Service Fabric lokale gebruikersaccounts maakt op computers waarop de toepassing hello wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="812e2-179">When a **LocalUser** account type is specified in hello principals section of hello application manifest, Service Fabric creates local user accounts on machines where hello application is deployed.</span></span> <span data-ttu-id="812e2-180">Deze accounts hoeft standaard geen Hallo dezelfde naam als die zijn opgegeven in de toepassing hello manifest (bijvoorbeeld Customer3 in Hallo volgende voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="812e2-180">By default, these accounts do not have hello same names as those specified in hello application manifest (for example, Customer3 in hello following sample).</span></span> <span data-ttu-id="812e2-181">In plaats daarvan dynamisch worden gegenereerd en willekeurige wachtwoorden hebben.</span><span class="sxs-lookup"><span data-stu-id="812e2-181">Instead, they are dynamically generated and have random passwords.</span></span>

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

<span data-ttu-id="812e2-182">Als een toepassing vereist dat Hallo-gebruikersaccount en wachtwoord niet hetzelfde zijn op alle machines (bijvoorbeeld tooenable NTLM-verificatie), moet het clustermanifest hello NTLMAuthenticationEnabled tootrue ingesteld.</span><span class="sxs-lookup"><span data-stu-id="812e2-182">If an application requires that hello user account and password be same on all machines (for example, tooenable NTLM authentication), hello cluster manifest must set NTLMAuthenticationEnabled tootrue.</span></span> <span data-ttu-id="812e2-183">Hallo clustermanifest moet ook opgeven voor een NTLMAuthenticationPasswordSecret die wordt gebruikt toogenerate Hallo hetzelfde wachtwoord alle machines.</span><span class="sxs-lookup"><span data-stu-id="812e2-183">hello cluster manifest must also specify an NTLMAuthenticationPasswordSecret that is used toogenerate hello same password across all machines.</span></span>

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a><span data-ttu-id="812e2-184">Beleid toohello code servicepakketten toewijzen</span><span class="sxs-lookup"><span data-stu-id="812e2-184">Assign policies toohello service code packages</span></span>
<span data-ttu-id="812e2-185">Hallo **RunAsPolicy** sectie voor een **ServiceManifestImport** Hiermee geeft u de account Hallo van Hallo principals sectie gebruikte toorun een codepakket moet.</span><span class="sxs-lookup"><span data-stu-id="812e2-185">hello **RunAsPolicy** section for a **ServiceManifestImport** specifies hello account from hello principals section that should be used toorun a code package.</span></span> <span data-ttu-id="812e2-186">Pakketten van Hallo service manifest code wordt gekoppeld met een gebruikersaccount in Hallo principals sectie.</span><span class="sxs-lookup"><span data-stu-id="812e2-186">It also associates code packages from hello service manifest with user accounts in hello principals section.</span></span> <span data-ttu-id="812e2-187">U kunt dit opgeven voor het Hallo-setup of belangrijkste toegangspunten, of u kunt opgeven `All` tooapply het tooboth.</span><span class="sxs-lookup"><span data-stu-id="812e2-187">You can specify this for hello setup or main entry points, or you can specify `All` tooapply it tooboth.</span></span> <span data-ttu-id="812e2-188">Hallo volgende voorbeeld ziet u verschillende soorten beleid wordt toegepast:</span><span class="sxs-lookup"><span data-stu-id="812e2-188">hello following example shows different policies being applied:</span></span>

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

<span data-ttu-id="812e2-189">Als **EntryPointType** niet is opgegeven, Hallo standaard is ingesteld tooEntryPointType = 'Main'.</span><span class="sxs-lookup"><span data-stu-id="812e2-189">If **EntryPointType** is not specified, hello default is set tooEntryPointType=”Main”.</span></span> <span data-ttu-id="812e2-190">Geven **entrypoint** is vooral nuttig wanneer u toorun wilt dat bepaalde installatiebewerkingen hoge privileges met een systeemaccount.</span><span class="sxs-lookup"><span data-stu-id="812e2-190">Specifying **SetupEntryPoint** is especially useful when you want toorun certain high-privilege setup operations under a system account.</span></span> <span data-ttu-id="812e2-191">Hallo werkelijke service programmacode kan worden uitgevoerd onder een account met kleine-bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="812e2-191">hello actual service code can run under a lower-privilege account.</span></span>

### <a name="apply-a-default-policy-tooall-service-code-packages"></a><span data-ttu-id="812e2-192">Een standaard beleid tooall service code pakketten toepassen</span><span class="sxs-lookup"><span data-stu-id="812e2-192">Apply a default policy tooall service code packages</span></span>
<span data-ttu-id="812e2-193">Gebruik van Hallo **DefaultRunAsPolicy** sectie toospecify een standaardgebruikersaccount voor alle pakketten van code die een specifieke geen **RunAsPolicy** gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="812e2-193">You use hello **DefaultRunAsPolicy** section toospecify a default user account for all code packages that don’t have a specific **RunAsPolicy** defined.</span></span> <span data-ttu-id="812e2-194">Als de meeste Hallo code pakketten die zijn opgegeven in het Hallo-servicemanifest gebruikt door een toepassing moet toorun onder Hallo dezelfde gebruiker hello toepassing kunt alleen een standaardbeleid RunAs met dat gebruikersaccount definiëren.</span><span class="sxs-lookup"><span data-stu-id="812e2-194">If most of hello code packages that are specified in hello service manifest used by an application need toorun under hello same user, hello application can just define a default RunAs policy with that user account.</span></span> <span data-ttu-id="812e2-195">Hallo volgende voorbeeld wordt opgegeven dat als een codepakket geen heeft een **RunAsPolicy** opgegeven, Hallo codepakket moet worden uitgevoerd onder Hallo **MyDefaultAccount** in Hallo principals sectie hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="812e2-195">hello following example specifies that if a code package does not have a **RunAsPolicy** specified, hello code package should run under hello **MyDefaultAccount** specified in hello principals section.</span></span>

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a><span data-ttu-id="812e2-196">Gebruik van een gebruiker of groep voor Active Directory-domein</span><span class="sxs-lookup"><span data-stu-id="812e2-196">Use an Active Directory domain group or user</span></span>
<span data-ttu-id="812e2-197">U kunt voor een exemplaar van de Service-infrastructuur die is geïnstalleerd op Windows Server met behulp van Hallo zelfstandig installatieprogramma Hallo service onder Hallo referenties voor een Active Directory-gebruiker of groep account uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="812e2-197">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service under hello credentials for an Active Directory user or group account.</span></span> <span data-ttu-id="812e2-198">Dit is van Active Directory on-premises binnen uw domein en is niet met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="812e2-198">This is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="812e2-199">U kunt andere bronnen in Hallo-domein (bijvoorbeeld bestandsshares) die machtigingen hebben gekregen benaderen via een domeingebruiker of -groep.</span><span class="sxs-lookup"><span data-stu-id="812e2-199">By using a domain user or group, you can then access other resources in hello domain (for example, file shares) that have been granted permissions.</span></span>

<span data-ttu-id="812e2-200">Hallo volgende voorbeeld ziet u een Active Directory-gebruiker aangeroepen *testgebruiker* met hun domein wachtwoord dat wordt versleuteld met behulp van een certificaat genoemd *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="812e2-200">hello following example shows an Active Directory user called *TestUser* with their domain password encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="812e2-201">U kunt Hallo `Invoke-ServiceFabricEncryptText` PowerShell-opdracht toocreate Hallo geheime gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="812e2-201">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text.</span></span> <span data-ttu-id="812e2-202">Zie [geheimen in Service Fabric-toepassingen beheren](service-fabric-application-secret-management.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="812e2-202">See [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md) for details.</span></span>

<span data-ttu-id="812e2-203">Moet u de persoonlijke sleutel Hallo van Hallo certificaat toodecrypt Hallo wachtwoord toohello lokale machine implementeren met behulp van een out-of-band-methode (dit is in Azure, via Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="812e2-203">You must deploy hello private key of hello certificate toodecrypt hello password toohello local machine by using an out-of-band method (in Azure, this is via Azure Resource Manager).</span></span> <span data-ttu-id="812e2-204">Vervolgens wanneer Service Fabric Hallo service pakket toohello machine implementeert, kunnen toodecrypt Hallo geheim en verifiëren met Active Directory-toorun onder deze referenties (samen met de naam van de gebruiker Hallo).</span><span class="sxs-lookup"><span data-stu-id="812e2-204">Then, when Service Fabric deploys hello service package toohello machine, it is able toodecrypt hello secret and (along with hello user name) authenticate with Active Directory toorun under those credentials.</span></span>

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
### <a name="use-a-group-managed-service-account"></a><span data-ttu-id="812e2-205">Gebruik een groep beheerd serviceaccount.</span><span class="sxs-lookup"><span data-stu-id="812e2-205">Use a Group Managed Service Account.</span></span>
<span data-ttu-id="812e2-206">U kunt voor een exemplaar van de Service-infrastructuur die is geïnstalleerd op Windows Server met behulp van Hallo zelfstandig installatieprogramma Hallo service uitvoeren als een groep beheerde serviceaccounts (gMSA).</span><span class="sxs-lookup"><span data-stu-id="812e2-206">For an instance of Service Fabric that was installed on Windows Server by using hello standalone installer, you can run hello service as a group Managed Service Account (gMSA).</span></span> <span data-ttu-id="812e2-207">Active Directory wordt on-premises binnen uw domein en is niet met Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="812e2-207">Note that this is Active Directory on-premises within your domain and is not with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="812e2-208">Met behulp van een gMSA er is geen wachtwoord of het versleutelde wachtwoord opgeslagen in Hallo `Application Manifest`.</span><span class="sxs-lookup"><span data-stu-id="812e2-208">By using a gMSA there is no password or encrypted password stored in hello `Application Manifest`.</span></span>

<span data-ttu-id="812e2-209">Hallo volgende voorbeeld laat zien hoe toocreate een gMSA-account genoemd *svc-Test$*; hoe toodeploy die worden beheerd clusterknooppunten voor service-account toohello; en hoe tooconfigure Hallo UPN.</span><span class="sxs-lookup"><span data-stu-id="812e2-209">hello following example shows how toocreate a gMSA account called *svc-Test$*; how toodeploy that managed service account toohello cluster nodes; and how tooconfigure hello user principal.</span></span>

##### <a name="prerequisites"></a><span data-ttu-id="812e2-210">Vereisten.</span><span class="sxs-lookup"><span data-stu-id="812e2-210">Prerequisites.</span></span>
- <span data-ttu-id="812e2-211">Hallo-domein moet een KDS-hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="812e2-211">hello domain needs a KDS root key.</span></span>
- <span data-ttu-id="812e2-212">Hallo-domein moet toobe op een Windows Server 2012 of hoger functionaliteitsniveau.</span><span class="sxs-lookup"><span data-stu-id="812e2-212">hello domain needs toobe at a Windows Server 2012 or later functional level.</span></span>

##### <a name="example"></a><span data-ttu-id="812e2-213">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="812e2-213">Example</span></span>
1. <span data-ttu-id="812e2-214">De beheerder van een active directory-domein maken van een groep beheerd serviceaccount met Hallo hebben `New-ADServiceAccount` commandlet en zorg ervoor dat Hallo `PrincipalsAllowedToRetrieveManagedPassword` bevat alle clusterknooppunten van Hallo service fabric.</span><span class="sxs-lookup"><span data-stu-id="812e2-214">Have an active directory domain administrator create a group managed service account using hello `New-ADServiceAccount` commandlet and ensure that hello `PrincipalsAllowedToRetrieveManagedPassword` includes all of hello service fabric cluster nodes.</span></span> <span data-ttu-id="812e2-215">Houd er rekening mee dat `AccountName`, `DnsHostName`, en `ServicePrincipalName` moeten uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="812e2-215">Note that `AccountName`, `DnsHostName`, and `ServicePrincipalName` must be unique.</span></span>
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. <span data-ttu-id="812e2-216">Op elk knooppunt Hallo service fabric-cluster (bijvoorbeeld `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), installeren en te testen Hallo gMSA.</span><span class="sxs-lookup"><span data-stu-id="812e2-216">On each of hello service fabric cluster nodes (for example, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), install and test hello gMSA.</span></span>
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. <span data-ttu-id="812e2-217">Configureer Hallo User principal en Hallo RunAsPolicy tooreference Hallo gebruiker configureren.</span><span class="sxs-lookup"><span data-stu-id="812e2-217">Configure hello User principal, and configure hello RunAsPolicy tooreference hello user.</span></span>
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

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a><span data-ttu-id="812e2-218">Toewijzen van een beveiligingsbeleid voor toegang voor HTTP en HTTPS-eindpunten</span><span class="sxs-lookup"><span data-stu-id="812e2-218">Assign a security access policy for HTTP and HTTPS endpoints</span></span>
<span data-ttu-id="812e2-219">Als u een RunAs-service voor beleid tooa toepassen en Hallo servicemanifest eindpunt resources met Hallo HTTP-protocol declareert, moet u een **SecurityAccessPolicy** tooensure dat poorten toothese eindpunten toegewezen correct zijn Access control vermeld voor Hallo RunAs-gebruikersaccount dat Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="812e2-219">If you apply a RunAs policy tooa service and hello service manifest declares endpoint resources with hello HTTP protocol, you must specify a **SecurityAccessPolicy** tooensure that ports allocated toothese endpoints are correctly access-control listed for hello RunAs user account that hello service runs under.</span></span> <span data-ttu-id="812e2-220">Anders **http.sys** geen toegang toohello service en voor het ophalen van de fouten met aanroepen van Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="812e2-220">Otherwise, **http.sys** does not have access toohello service, and you get failures with calls from hello client.</span></span> <span data-ttu-id="812e2-221">Hallo volgende voorbeeld wordt Hallo Customer1 account tooan eindpunt aangeroepen **EndpointName**, waardoor het volledige toegangsrechten.</span><span class="sxs-lookup"><span data-stu-id="812e2-221">hello following example applies hello Customer1 account tooan endpoint called **EndpointName**, which gives it full access rights.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

<span data-ttu-id="812e2-222">Voor de HTTPS-eindpunt hello hebt u ook tooindicate Hallo-naam van Hallo certificaat tooreturn toohello client.</span><span class="sxs-lookup"><span data-stu-id="812e2-222">For hello HTTPS endpoint, you also have tooindicate hello name of hello certificate tooreturn toohello client.</span></span> <span data-ttu-id="812e2-223">U kunt dit doen met behulp van **EndpointBindingPolicy**, met gedefinieerd in een sectie certificaten in het toepassingsmanifest Hallo Hallo-certificaat.</span><span class="sxs-lookup"><span data-stu-id="812e2-223">You can do this by using **EndpointBindingPolicy**, with hello certificate defined in a certificates section in hello application manifest.</span></span>

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a><span data-ttu-id="812e2-224">Bijwerken van meerdere toepassingen met https-eindpunten</span><span class="sxs-lookup"><span data-stu-id="812e2-224">Upgrading multiple applications with https endpoints</span></span>
<span data-ttu-id="812e2-225">U moet toobe zorgvuldige niet toouse hello **dezelfde poort** voor verschillende exemplaren van Hallo dezelfde toepassing als u http gebruikt**s**.</span><span class="sxs-lookup"><span data-stu-id="812e2-225">You need toobe careful not toouse hello **same port** for different instances of hello same application when using http**s**.</span></span> <span data-ttu-id="812e2-226">Hallo reden is dat het Service Fabric kunnen tooupgrade HALLO cert voor een van de exemplaren van een toepassing hello niet kan worden.</span><span class="sxs-lookup"><span data-stu-id="812e2-226">hello reason is that Service Fabric won't be able tooupgrade hello cert for one of hello application instances.</span></span> <span data-ttu-id="812e2-227">Bijvoorbeeld als toepassing 1 of een toepassing 2 beide wilt tooupgrade hun certificaat 1 toocert 2.</span><span class="sxs-lookup"><span data-stu-id="812e2-227">For example, if application 1 or application 2 both want tooupgrade their cert 1 toocert 2.</span></span> <span data-ttu-id="812e2-228">Wanneer Hallo upgrade gebeurt, Service Fabric mogelijk zijn opgeschoond Hallo certificaat 1 registratie bij http.sys Hoewel hello andere toepassing wordt nog steeds gebruikt.</span><span class="sxs-lookup"><span data-stu-id="812e2-228">When hello upgrade happens, Service Fabric might have cleaned up hello cert 1 registration with http.sys even though hello other application is still using it.</span></span> <span data-ttu-id="812e2-229">tooprevent dit Service Fabric detecteert dat er al een ander exemplaar op Hallo poort met Hallo certificaat geregistreerd (vanwege toohttp.sys) en mislukt de bewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="812e2-229">tooprevent this, Service Fabric detects that there is already another application instance registered on hello port with hello certificate (due toohttp.sys) and fails hello operation.</span></span>

<span data-ttu-id="812e2-230">Daarom Service Fabric biedt geen ondersteuning voor twee verschillende services met behulp van een upgrade **Hallo dezelfde poort** in exemplaren van een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="812e2-230">Hence Service Fabric does not support upgrading two different services using **hello same port** in different application instances.</span></span> <span data-ttu-id="812e2-231">Met andere woorden, u Hallo dezelfde van het certificaat niet gebruiken voor andere services op Hallo dezelfde poort.</span><span class="sxs-lookup"><span data-stu-id="812e2-231">In other words, you cannot use hello same certificate on different services on hello same port.</span></span> <span data-ttu-id="812e2-232">Als u toohave moet een gedeelde certificaten op Hallo dezelfde poort u tooensure dat services worden geplaatst op verschillende computers met plaatsingsbeperkingen Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="812e2-232">If you need toohave a shared certificate on hello same port, you need tooensure that hello services are placed on different machines with placement constraints.</span></span> <span data-ttu-id="812e2-233">Of Overweeg het gebruik van dynamische poorten Service Fabric indien mogelijk voor elke service in elk toepassingsexemplaar.</span><span class="sxs-lookup"><span data-stu-id="812e2-233">Or consider using Service Fabric dynamic ports if possible for each service in each application instance.</span></span> 

<span data-ttu-id="812e2-234">Als u een upgrade is mislukt met https, een fout waarschuwing wordt weergegeven met de tekst "Hallo Windows HTTP-Server API ondersteunt geen meerdere certificaten voor toepassingen die een poort delen."</span><span class="sxs-lookup"><span data-stu-id="812e2-234">If you see an upgrade fail with https, an error warning saying "hello Windows HTTP Server API does not support multiple certificates for applications that share a port.”</span></span>

## <a name="a-complete-application-manifest-example"></a><span data-ttu-id="812e2-235">Een voorbeeld van een volledige toepassing manifest</span><span class="sxs-lookup"><span data-stu-id="812e2-235">A complete application manifest example</span></span>
<span data-ttu-id="812e2-236">Hallo na het toepassingsmanifest bevat veel Hallo verschillende instellingen:</span><span class="sxs-lookup"><span data-stu-id="812e2-236">hello following application manifest shows many of hello different settings:</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="812e2-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="812e2-237">Next steps</span></span>
* [<span data-ttu-id="812e2-238">Hallo toepassingsmodel begrijpen</span><span class="sxs-lookup"><span data-stu-id="812e2-238">Understand hello application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="812e2-239">Bronnen opgeven in een servicemanifest</span><span class="sxs-lookup"><span data-stu-id="812e2-239">Specify resources in a service manifest</span></span>](service-fabric-service-manifest-resources.md)
* [<span data-ttu-id="812e2-240">Een toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="812e2-240">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
