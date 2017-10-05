---
title: Het beheren van geheimen in Service Fabric-toepassingen | Microsoft Docs
description: In dit artikel wordt beschreven hoe secure geheime waarden in een Service Fabric-toepassing.
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
ms.openlocfilehash: d71924cda8bb3bffbe221946d80dba150359e38e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="55787-103">Het beheren van geheimen in Service Fabric-toepassingen</span><span class="sxs-lookup"><span data-stu-id="55787-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="55787-104">Deze handleiding leert u de stappen voor het beheren van geheimen in een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="55787-104">This guide walks you through the steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="55787-105">Geheimen mag gevoelige informatie, zoals de storage-verbindingsreeksen, wachtwoorden of andere waarden die niet moeten worden behandeld als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="55787-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="55787-106">Deze handleiding maakt gebruik van Azure Sleutelkluis sleutels en geheimen beheren.</span><span class="sxs-lookup"><span data-stu-id="55787-106">This guide uses Azure Key Vault to manage keys and secrets.</span></span> <span data-ttu-id="55787-107">Echter, *met* geheimen in een toepassing is cloud platform-networkdirect naar toepassingen kunnen worden geïmplementeerd naar een cluster overal worden gehost.</span><span class="sxs-lookup"><span data-stu-id="55787-107">However, *using* secrets in an application is cloud platform-agnostic to allow applications to be deployed to a cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="55787-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="55787-108">Overview</span></span>
<span data-ttu-id="55787-109">De aanbevolen manier voor het beheren van configuratie-instellingen is via [service configuratiepakketten][config-package].</span><span class="sxs-lookup"><span data-stu-id="55787-109">The recommended way to manage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="55787-110">Configuratiepakketten zijn samengestelde en bij te werken via beheerde rollende upgrades met health-validatie en voor automatisch terugdraaien.</span><span class="sxs-lookup"><span data-stu-id="55787-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="55787-111">Dit is voorkeur naar globale configuratie vermindert de kans op een globale Services uitvallen.</span><span class="sxs-lookup"><span data-stu-id="55787-111">This is preferred to global configuration as it reduces the chances of a global service outage.</span></span> <span data-ttu-id="55787-112">Versleutelde geheimen zijn geen uitzondering.</span><span class="sxs-lookup"><span data-stu-id="55787-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="55787-113">Service Fabric bevat ingebouwde functies voor het versleutelen en ontsleutelen van waarden in een pakket Settings.xml configuratiebestand met behulp van certificaatversleuteling.</span><span class="sxs-lookup"><span data-stu-id="55787-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="55787-114">Het volgende diagram illustreert de basisprincipes voor beheer van de geheime in een Service Fabric-toepassing:</span><span class="sxs-lookup"><span data-stu-id="55787-114">The following diagram illustrates the basic flow for secret management in a Service Fabric application:</span></span>

![overzicht van geheime management][overview]

<span data-ttu-id="55787-116">Er zijn vier hoofdstappen in deze overdracht:</span><span class="sxs-lookup"><span data-stu-id="55787-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="55787-117">Verkrijgen van een certificaat voor het uitwisselen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="55787-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="55787-118">Installeer het certificaat in het cluster.</span><span class="sxs-lookup"><span data-stu-id="55787-118">Install the certificate in your cluster.</span></span>
3. <span data-ttu-id="55787-119">Versleutelen geheime waarden bij het implementeren van een toepassing met het certificaat en een service Settings.xml configuratiebestand injecteren.</span><span class="sxs-lookup"><span data-stu-id="55787-119">Encrypt secret values when deploying an application with the certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="55787-120">Versleutelde waarden buiten Settings.xml lezen door te ontsleutelen met hetzelfde certificaat uitwisselen.</span><span class="sxs-lookup"><span data-stu-id="55787-120">Read encrypted values out of Settings.xml by decrypting with the same encipherment certificate.</span></span> 

<span data-ttu-id="55787-121">[Azure Sleutelkluis] [ key-vault-get-started] wordt hier gebruikt als een locatie voor de veilige opslag voor certificaten en als een manier om certificaten zijn geïnstalleerd op de Service Fabric-clusters in Azure.</span><span class="sxs-lookup"><span data-stu-id="55787-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way to get certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="55787-122">Als u niet in Azure implementeert, hoeft u geen Sleutelkluis gebruiken voor het beheren van geheimen in Service Fabric-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="55787-122">If you are not deploying to Azure, you do not need to use Key Vault to manage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="55787-123">Gegevens uitwisselen certificaat</span><span class="sxs-lookup"><span data-stu-id="55787-123">Data encipherment certificate</span></span>
<span data-ttu-id="55787-124">Een certificaat voor het uitwisselen van gegevens wordt uitsluitend gebruikt voor versleuteling en ontsleuteling van de configuratie van de waarden in een service Settings.xml en wordt niet gebruikt voor de verificatie of het ondertekenen van de gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="55787-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="55787-125">Het certificaat moet voldoen aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="55787-125">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="55787-126">Het certificaat moet een persoonlijke sleutel bevatten.</span><span class="sxs-lookup"><span data-stu-id="55787-126">The certificate must contain a private key.</span></span>
* <span data-ttu-id="55787-127">Het certificaat moet worden gemaakt voor sleuteluitwisseling, geëxporteerd naar een bestand Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="55787-127">The certificate must be created for key exchange, exportable to a Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="55787-128">Het certificaat sleutelgebruik gegevenscodering (10) moet bevatten en mag geen serververificatie of clientverificatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="55787-128">The certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="55787-129">Bij het maken van een zelfondertekend certificaat met behulp van PowerShell, bijvoorbeeld de `KeyUsage` vlag moet worden ingesteld op `DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="55787-129">For example, when creating a self-signed certificate using PowerShell, the `KeyUsage` flag must be set to `DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-the-certificate-in-your-cluster"></a><span data-ttu-id="55787-130">Installeer het certificaat in het cluster</span><span class="sxs-lookup"><span data-stu-id="55787-130">Install the certificate in your cluster</span></span>
<span data-ttu-id="55787-131">Dit certificaat moet worden geïnstalleerd op elk knooppunt in het cluster.</span><span class="sxs-lookup"><span data-stu-id="55787-131">This certificate must be installed on each node in the cluster.</span></span> <span data-ttu-id="55787-132">Deze wordt gebruikt tijdens runtime voor het ontsleutelen van waarden in een service Settings.xml zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="55787-132">It will be used at runtime to decrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="55787-133">Zie [het maken van een cluster met Azure Resource Manager] [ service-fabric-cluster-creation-via-arm] voor installatie-instructies.</span><span class="sxs-lookup"><span data-stu-id="55787-133">See [how to create a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="55787-134">Toepassing geheimen versleutelen</span><span class="sxs-lookup"><span data-stu-id="55787-134">Encrypt application secrets</span></span>
<span data-ttu-id="55787-135">De Service Fabric SDK bevat ingebouwde geheime versleuteling en ontsleuteling functies.</span><span class="sxs-lookup"><span data-stu-id="55787-135">The Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="55787-136">Geheime waarden kunnen worden versleuteld op het moment van gebouwd ontsleuteld en gelezen via een programma in de servicecode.</span><span class="sxs-lookup"><span data-stu-id="55787-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="55787-137">De volgende PowerShell-opdracht wordt gebruikt voor het versleutelen van een geheim.</span><span class="sxs-lookup"><span data-stu-id="55787-137">The following PowerShell command is used to encrypt a secret.</span></span> <span data-ttu-id="55787-138">Met deze opdracht versleutelt alleen de waarde; Dit gebeurt **niet** Meld u aan de gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="55787-138">This command only encrypts the value; it does **not** sign the cipher text.</span></span> <span data-ttu-id="55787-139">U moet hetzelfde certificaat uitwisselen die is geïnstalleerd in uw cluster voor het produceren van gecodeerde tekst voor geheime waarden gebruiken:</span><span class="sxs-lookup"><span data-stu-id="55787-139">You must use the same encipherment certificate that is installed in your cluster to produce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="55787-140">De resulterende base 64-tekenreeks bevat zowel de geheime gecodeerde tekst, evenals informatie over het certificaat dat is gebruikt om ze te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="55787-140">The resulting base-64 string contains both the secret ciphertext as well as information about the certificate that was used to encrypt it.</span></span>  <span data-ttu-id="55787-141">De base-64 gecodeerde tekenreeks kan worden ingevoegd in een parameter in Settings.xml-configuratiebestand voor uw service met de `IsEncrypted` -kenmerk ingesteld op `true`:</span><span class="sxs-lookup"><span data-stu-id="55787-141">The base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with the `IsEncrypted` attribute set to `true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="55787-142">Toepassing geheimen invoeren in toepassingsexemplaren</span><span class="sxs-lookup"><span data-stu-id="55787-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="55787-143">In het ideale geval implementatie in verschillende omgevingen worden als geautomatiseerde mogelijk.</span><span class="sxs-lookup"><span data-stu-id="55787-143">Ideally, deployment to different environments should be as automated as possible.</span></span> <span data-ttu-id="55787-144">Dit kan worden bereikt door geheime versleuteling uitvoeren in een build-omgeving en het geven van de versleutelde geheimen als parameters bij het maken van exemplaren van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="55787-144">This can be accomplished by performing secret encryption in a build environment and providing the encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="55787-145">Onderdrukbare parameters in Settings.xml gebruiken</span><span class="sxs-lookup"><span data-stu-id="55787-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="55787-146">Het configuratiebestand Settings.xml kunt overschrijfbare parameters die tijdens de aanmaak van de toepassing kunnen worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="55787-146">The Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="55787-147">Gebruik de `MustOverride` kenmerk in plaats van een waarde voor een parameter op te geven:</span><span class="sxs-lookup"><span data-stu-id="55787-147">Use the `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="55787-148">U kunt met het overschrijven van waarden in Settings.xml, declareren een onderdrukking-parameter voor de service in ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="55787-148">To override values in Settings.xml, declare an override parameter for the service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="55787-149">Nu de waarde kan worden opgegeven als een *toepassing parameter* bij het maken van een exemplaar van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="55787-149">Now the value can be specified as an *application parameter* when creating an instance of the application.</span></span> <span data-ttu-id="55787-150">Maken van een toepassingsexemplaar kan scripts worden gebruikt met behulp van PowerShell, of geschreven in C#, voor eenvoudige integratie in een buildproces.</span><span class="sxs-lookup"><span data-stu-id="55787-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="55787-151">Met behulp van PowerShell, wordt de parameter doorgegeven aan de `New-ServiceFabricApplication` opdracht als een [hash-tabel](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="55787-151">Using PowerShell, the parameter is supplied to the `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="55787-152">Met C#, parameters voor de toepassing zijn opgegeven in een `ApplicationDescription` als een `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="55787-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="55787-153">Ontsleutelen van geheimen van servicecode</span><span class="sxs-lookup"><span data-stu-id="55787-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="55787-154">Services in Service Fabric onder netwerkservice standaard op Windows worden uitgevoerd en geen toegang hebt tot de certificaten zijn geïnstalleerd op het knooppunt zonder extra instellingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="55787-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access to certificates installed on the node without some extra setup.</span></span>

<span data-ttu-id="55787-155">Wanneer met behulp van een certificaat voor het uitwisselen van gegevens, moet u ervoor dat netwerkservice of de gebruikersaccount van de service wordt uitgevoerd toegang heeft tot de persoonlijke sleutel van het certificaat.</span><span class="sxs-lookup"><span data-stu-id="55787-155">When using a data encipherment certificate, you need to make sure NETWORK SERVICE or whatever user account the service is running under has access to the certificate's private key.</span></span> <span data-ttu-id="55787-156">Service Fabric verwerkt door de toegang voor uw service automatisch te verlenen als u configureert om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="55787-156">Service Fabric will handle granting access for your service automatically if you configure it to do so.</span></span> <span data-ttu-id="55787-157">Deze configuratie kan worden gedaan in ApplicationManifest.xml door gebruikers- en beveiligingsbeleid voor certificaten te definiëren.</span><span class="sxs-lookup"><span data-stu-id="55787-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="55787-158">In het volgende voorbeeld is de Netwerkservice-account lezen toegang krijgen tot een gedefinieerd door de vingerafdruk van certificaat:</span><span class="sxs-lookup"><span data-stu-id="55787-158">In the following example, the NETWORK SERVICE account is given read access to a certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="55787-159">Bij het kopiëren van de vingerafdruk van een certificaat uit de store-module certificate in Windows, wordt een onzichtbare teken aan het begin van de vingerafdruk tekenreeks geplaatst.</span><span class="sxs-lookup"><span data-stu-id="55787-159">When copying a certificate thumbprint from the certificate store snap-in on Windows, an invisible character is placed at the beginning of the thumbprint string.</span></span> <span data-ttu-id="55787-160">Dit onzichtbaar teken kan een fout ontstaan bij het vinden van een certificaat met vingerafdruk, dus deze extra teken verwijderen.</span><span class="sxs-lookup"><span data-stu-id="55787-160">This invisible character can cause an error when trying to locate a certificate by thumbprint, so be sure to delete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="55787-161">Gebruik application geheimen in servicecode</span><span class="sxs-lookup"><span data-stu-id="55787-161">Use application secrets in service code</span></span>
<span data-ttu-id="55787-162">De API voor het openen van configuratiewaarden uit Settings.xml in een configuratiepakket kunt u gemakkelijk te ontsleutelen van waarden die u hebt de `IsEncrypted` -kenmerk ingesteld op `true`.</span><span class="sxs-lookup"><span data-stu-id="55787-162">The API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have the `IsEncrypted` attribute set to `true`.</span></span> <span data-ttu-id="55787-163">Aangezien de gecodeerde tekst informatie over het certificaat dat wordt gebruikt voor versleuteling bevat, hoeft u niet handmatig het certificaat niet vinden.</span><span class="sxs-lookup"><span data-stu-id="55787-163">Since the encrypted text contains information about the certificate used for encryption, you do not need to manually find the certificate.</span></span> <span data-ttu-id="55787-164">Het certificaat moet alleen worden geïnstalleerd op het knooppunt dat de service wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="55787-164">The certificate just needs to be installed on the node that the service is running on.</span></span> <span data-ttu-id="55787-165">Te roepen de `DecryptValue()` methode voor het ophalen van de oorspronkelijke geheime waarde:</span><span class="sxs-lookup"><span data-stu-id="55787-165">Simply call the `DecryptValue()` method to retrieve the original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="55787-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55787-166">Next Steps</span></span>
<span data-ttu-id="55787-167">Meer informatie over [met toepassingen met andere machtigingen](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="55787-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
