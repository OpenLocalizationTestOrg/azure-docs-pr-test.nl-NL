---
title: aaaManaging geheimen in Service Fabric-toepassingen | Microsoft Docs
description: Dit artikel wordt beschreven hoe toosecure geheim waarden in een Service Fabric-toepassing.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="62d24-103">Het beheren van geheimen in Service Fabric-toepassingen</span><span class="sxs-lookup"><span data-stu-id="62d24-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="62d24-104">Deze handleiding leert u Hallo van het beheer van geheimen in een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="62d24-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="62d24-105">Geheimen mag gevoelige informatie, zoals de storage-verbindingsreeksen, wachtwoorden of andere waarden die niet moeten worden behandeld als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="62d24-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="62d24-106">Deze handleiding maakt gebruik van Azure Sleutelkluis toomanage sleutels en geheimen.</span><span class="sxs-lookup"><span data-stu-id="62d24-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="62d24-107">Echter, *met* geheimen in een toepassing is cloud platform networkdirect tooallow toepassingen toobe geïmplementeerde tooa cluster gehost elke locatie.</span><span class="sxs-lookup"><span data-stu-id="62d24-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="62d24-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="62d24-108">Overview</span></span>
<span data-ttu-id="62d24-109">Hallo configuratie-instellingen voor de service aanbevolen manier toomanage is via [service configuratiepakketten][config-package].</span><span class="sxs-lookup"><span data-stu-id="62d24-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="62d24-110">Configuratiepakketten zijn samengestelde en bij te werken via beheerde rollende upgrades met health-validatie en voor automatisch terugdraaien.</span><span class="sxs-lookup"><span data-stu-id="62d24-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="62d24-111">Dit is voorkeur tooglobal configuratie vermindert Hallo kans op een globale Services uitvallen.</span><span class="sxs-lookup"><span data-stu-id="62d24-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="62d24-112">Versleutelde geheimen zijn geen uitzondering.</span><span class="sxs-lookup"><span data-stu-id="62d24-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="62d24-113">Service Fabric bevat ingebouwde functies voor het versleutelen en ontsleutelen van waarden in een pakket Settings.xml configuratiebestand met behulp van certificaatversleuteling.</span><span class="sxs-lookup"><span data-stu-id="62d24-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="62d24-114">Hallo illustreert volgende diagram Hallo-basisprincipes voor het beheer van de geheime in een Service Fabric-toepassing:</span><span class="sxs-lookup"><span data-stu-id="62d24-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![overzicht van geheime management][overview]

<span data-ttu-id="62d24-116">Er zijn vier hoofdstappen in deze overdracht:</span><span class="sxs-lookup"><span data-stu-id="62d24-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="62d24-117">Verkrijgen van een certificaat voor het uitwisselen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="62d24-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="62d24-118">Hallo-certificaat installeren in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="62d24-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="62d24-119">Versleutelen geheime waarden bij het implementeren van een toepassing met Hallo-certificaat en injecteren van een service Settings.xml-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="62d24-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="62d24-120">Alleen versleutelde waarden buiten Settings.xml door te ontsleutelen met Hallo hetzelfde uitwisselen certificaat.</span><span class="sxs-lookup"><span data-stu-id="62d24-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="62d24-121">[Azure Sleutelkluis] [ key-vault-get-started] wordt hier gebruikt als een locatie voor de veilige opslag voor certificaten en als een manier tooget certificaten zijn geïnstalleerd op de Service Fabric-clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="62d24-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="62d24-122">Als u geen tooAzure implementeert, hoeft u geen toouse Sleutelkluis toomanage geheimen in Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="62d24-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="62d24-123">Gegevens uitwisselen certificaat</span><span class="sxs-lookup"><span data-stu-id="62d24-123">Data encipherment certificate</span></span>
<span data-ttu-id="62d24-124">Een certificaat voor het uitwisselen van gegevens wordt uitsluitend gebruikt voor versleuteling en ontsleuteling van de configuratie van de waarden in een service Settings.xml en wordt niet gebruikt voor de verificatie of het ondertekenen van de gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="62d24-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="62d24-125">Hallo-certificaat moet voldoen aan Hallo volgens de vereisten:</span><span class="sxs-lookup"><span data-stu-id="62d24-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="62d24-126">Hallo-certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="62d24-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="62d24-127">Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling, exporteerbaar tooa Personal Information Exchange (.pfx)-bestand.</span><span class="sxs-lookup"><span data-stu-id="62d24-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="62d24-128">Hallo certificaat sleutelgebruik gegevenscodering (10) moet bevatten en mag geen serververificatie of clientverificatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="62d24-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="62d24-129">Bijvoorbeeld bij het maken van een zelfondertekend certificaat met behulp van PowerShell Hallo `KeyUsage` moet de vlag te instellen`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="62d24-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="62d24-130">Hallo-certificaat installeren in het cluster</span><span class="sxs-lookup"><span data-stu-id="62d24-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="62d24-131">Dit certificaat moet worden geïnstalleerd op elk knooppunt in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="62d24-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="62d24-132">Deze wordt gebruikt tijdens runtime toodecrypt waarden in een service Settings.xml zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="62d24-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="62d24-133">Zie [hoe toocreate een cluster met Azure Resource Manager] [ service-fabric-cluster-creation-via-arm] voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="62d24-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="62d24-134">Toepassing geheimen versleutelen</span><span class="sxs-lookup"><span data-stu-id="62d24-134">Encrypt application secrets</span></span>
<span data-ttu-id="62d24-135">Hallo Service Fabric SDK bevat ingebouwde geheime versleuteling en ontsleuteling functies.</span><span class="sxs-lookup"><span data-stu-id="62d24-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="62d24-136">Geheime waarden kunnen worden versleuteld op het moment van gebouwd ontsleuteld en gelezen via een programma in de servicecode.</span><span class="sxs-lookup"><span data-stu-id="62d24-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="62d24-137">Hallo volgende PowerShell-opdracht is gebruikte tooencrypt een geheim.</span><span class="sxs-lookup"><span data-stu-id="62d24-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="62d24-138">Met deze opdracht versleutelt alleen Hallo value; Dit gebeurt **niet** ondertekenen Hallo gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="62d24-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="62d24-139">Hallo moet u hetzelfde certificaat voor uitwisselen die is geïnstalleerd in uw cluster tooproduce gecodeerde tekst voor geheime waarden:</span><span class="sxs-lookup"><span data-stu-id="62d24-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="62d24-140">Hallo resulterende base 64-tekenreeks bevat zowel geheime gecodeerde tekst hello, evenals informatie over het Hallo-certificaat dat gebruikt tooencrypt is deze.</span><span class="sxs-lookup"><span data-stu-id="62d24-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="62d24-141">Hallo Base64-gecodeerde tekenreeks kan worden ingevoegd in een parameter in het configuratiebestand van uw service Settings.xml Hello `IsEncrypted` kenmerkset te`true`:</span><span class="sxs-lookup"><span data-stu-id="62d24-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="62d24-142">Toepassing geheimen invoeren in toepassingsexemplaren</span><span class="sxs-lookup"><span data-stu-id="62d24-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="62d24-143">Implementatie toodifferent omgevingen moeten in het ideale geval als geautomatiseerde mogelijk.</span><span class="sxs-lookup"><span data-stu-id="62d24-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="62d24-144">Dit kan worden bereikt door geheime versleuteling uitvoeren in een build-omgeving en het leveren van geheimen Hallo versleuteld als parameters bij het maken van exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="62d24-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="62d24-145">Onderdrukbare parameters in Settings.xml gebruiken</span><span class="sxs-lookup"><span data-stu-id="62d24-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="62d24-146">Hallo Settings.xml configuratiebestand kunt overschrijfbare parameters die tijdens de aanmaak van de toepassing kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="62d24-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="62d24-147">Gebruik Hallo `MustOverride` kenmerk in plaats van een waarde voor een parameter op te geven:</span><span class="sxs-lookup"><span data-stu-id="62d24-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="62d24-148">toooverride waarden in Settings.xml, declareren een overrideparameter voor Hallo-service in ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="62d24-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

<span data-ttu-id="62d24-149">Nu het Hallo-waarde kan worden opgegeven als een *toepassing parameter* bij het maken van een exemplaar van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="62d24-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="62d24-150">Maken van een toepassingsexemplaar kan scripts worden gebruikt met behulp van PowerShell, of geschreven in C#, voor eenvoudige integratie in een buildproces.</span><span class="sxs-lookup"><span data-stu-id="62d24-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="62d24-151">Met behulp van PowerShell, Hallo parameter wordt opgegeven toohello `New-ServiceFabricApplication` opdracht als een [hash-tabel](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="62d24-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="62d24-152">Met C#, parameters voor de toepassing zijn opgegeven in een `ApplicationDescription` als een `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="62d24-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="62d24-153">Ontsleutelen van geheimen van servicecode</span><span class="sxs-lookup"><span data-stu-id="62d24-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="62d24-154">Services in Service Fabric onder netwerkservice standaard uitgevoerd in Windows en geen toegang toocertificates op hebt geïnstalleerd Hallo-knooppunt zonder extra instellingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="62d24-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="62d24-155">Wanneer u een certificaat voor het uitwisselen van gegevens, moet u ervoor dat netwerkservice of de gebruiker account Hallo-service wordt uitgevoerd onder de persoonlijke sleutel toegang toohello certificaat toomake.</span><span class="sxs-lookup"><span data-stu-id="62d24-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="62d24-156">Service Fabric, het verlenen van toegang voor uw service automatisch als u deze toodo dus configureren verwerkt.</span><span class="sxs-lookup"><span data-stu-id="62d24-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="62d24-157">Deze configuratie kan worden gedaan in ApplicationManifest.xml door gebruikers- en beveiligingsbeleid voor certificaten te definiëren.</span><span class="sxs-lookup"><span data-stu-id="62d24-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="62d24-158">Hallo Netwerkservice-account in Hallo voorbeeld te volgen, krijgt leestoegang tooa certificaat gedefinieerd door de vingerafdruk:</span><span class="sxs-lookup"><span data-stu-id="62d24-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> <span data-ttu-id="62d24-159">Bij het kopiëren van een certificaatvingerafdruk opslaan van Hallo-certificaat-module voor Windows, een onzichtbare teken aan begin Hallo van Hallo vingerafdruk tekenreeks geplaatst.</span><span class="sxs-lookup"><span data-stu-id="62d24-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="62d24-160">Dit onzichtbaar teken kan leiden tot een fout opgetreden bij het toolocate een certificaat met vingerafdruk, dus worden toodelete ervoor dat deze extra tekens.</span><span class="sxs-lookup"><span data-stu-id="62d24-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="62d24-161">Gebruik application geheimen in servicecode</span><span class="sxs-lookup"><span data-stu-id="62d24-161">Use application secrets in service code</span></span>
<span data-ttu-id="62d24-162">Hallo API voor het openen van configuratiewaarden uit Settings.xml in een configuratiepakket kunt u eenvoudig ontsleutelen van waarden die Hallo hebben `IsEncrypted` kenmerkset te`true`.</span><span class="sxs-lookup"><span data-stu-id="62d24-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="62d24-163">Omdat Hallo versleuteld tekst informatie over Hallo certificaat gebruikt voor versleuteling bevat, hoeft u geen toomanually zoeken Hallo certificaat.</span><span class="sxs-lookup"><span data-stu-id="62d24-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="62d24-164">Hallo-certificaat moet net toobe op Hallo-knooppunt dat Hallo-service wordt uitgevoerd op is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="62d24-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="62d24-165">Hallo te roepen `DecryptValue()` methode tooretrieve Hallo oorspronkelijke geheime waarde:</span><span class="sxs-lookup"><span data-stu-id="62d24-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="62d24-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62d24-166">Next Steps</span></span>
<span data-ttu-id="62d24-167">Meer informatie over [met toepassingen met andere machtigingen](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="62d24-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
