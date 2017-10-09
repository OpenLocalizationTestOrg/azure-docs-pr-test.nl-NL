---
title: aaaWhat is een Service in de Cloud-model en het pakket | Microsoft Docs
description: Beschrijft Hallo cloudservicemodel (csdef, cscfg-bestand) en -pakket (.cspkg) in Azure
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="572e1-103">Wat is Hallo Cloud Service-model en hoe ik dit pakket?</span><span class="sxs-lookup"><span data-stu-id="572e1-103">What is hello Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="572e1-104">Een cloudservice is gemaakt op basis van drie onderdelen, Hallo servicedefinitie *(.csdef)*, van de serviceconfiguratie Hallo *(.cscfg)*, en een servicepakket *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="572e1-104">A cloud service is created from three components, hello service definition *(.csdef)*, hello service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="572e1-105">Beide Hallo **ServiceDefinition.csdef** en **ServiceConfig.cscfg** bestanden zijn XML- en beschrijven Hallo-structuur van het Hallo-cloudservice en de manier waarop deze geconfigureerd; gezamenlijk Hallo-model genoemd.</span><span class="sxs-lookup"><span data-stu-id="572e1-105">Both hello **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe hello structure of hello cloud service and how it's configured; collectively called hello model.</span></span> <span data-ttu-id="572e1-106">Hallo **ServicePackage.cspkg** is een zipbestand dat is gegenereerd op basis van Hallo **ServiceDefinition.csdef** en bevat onder andere alle Hallo vereist op basis van een binair afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="572e1-106">hello **ServicePackage.cspkg** is a zip file that is generated from hello **ServiceDefinition.csdef** and among other things, contains all hello required binary-based dependencies.</span></span> <span data-ttu-id="572e1-107">Azure maakt een cloudservice van beide Hallo **ServicePackage.cspkg** en Hallo **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="572e1-107">Azure creates a cloud service from both hello **ServicePackage.cspkg** and hello **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="572e1-108">Zodra het Hallo-cloudservice wordt uitgevoerd in Azure, kunt u deze configureren via Hallo **ServiceConfig.cscfg** bestand, maar kan Hallo-definitie niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="572e1-108">Once hello cloud service is running in Azure, you can reconfigure it through hello **ServiceConfig.cscfg** file, but you cannot alter hello definition.</span></span>

## <a name="what-would-you-like-tooknow-more-about"></a><span data-ttu-id="572e1-109">Wat wilt u meer informatie over tooknow?</span><span class="sxs-lookup"><span data-stu-id="572e1-109">What would you like tooknow more about?</span></span>
* <span data-ttu-id="572e1-110">Ik wil meer informatie over Hallo tooknow [ServiceDefinition.csdef](#csdef) en [ServiceConfig.cscfg](#cscfg) bestanden.</span><span class="sxs-lookup"><span data-stu-id="572e1-110">I want tooknow more about hello [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="572e1-111">Ik heb al weet over die, geef me [enkele voorbeelden](#next-steps) op ik kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="572e1-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="572e1-112">Ik wil toocreate hello [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="572e1-112">I want toocreate hello [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="572e1-113">Ik gebruik Visual Studio en ik wil...</span><span class="sxs-lookup"><span data-stu-id="572e1-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="572e1-114">[Maak een cloudservice][vs_create]</span><span class="sxs-lookup"><span data-stu-id="572e1-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="572e1-115">[Configureren van een bestaande cloudservice][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="572e1-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="572e1-116">[Een Cloud Service-project implementeert][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="572e1-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="572e1-117">[Extern bureaublad in een cloud service-exemplaar][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="572e1-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="572e1-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="572e1-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="572e1-119">Hallo **ServiceDefinition.csdef** bestand geeft Hallo-instellingen die worden gebruikt door Azure tooconfigure een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="572e1-119">hello **ServiceDefinition.csdef** file specifies hello settings that are used by Azure tooconfigure a cloud service.</span></span> <span data-ttu-id="572e1-120">Hallo [Azure Service definitie Schema (.csdef-bestand)](https://msdn.microsoft.com/library/azure/ee758711.aspx) Hallo toegestane indeling biedt voor een servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="572e1-120">hello [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides hello allowable format for a service definition file.</span></span> <span data-ttu-id="572e1-121">Hallo toont volgende voorbeeld Hallo-instellingen die kunnen worden gedefinieerd voor hello Web- en werkrollen:</span><span class="sxs-lookup"><span data-stu-id="572e1-121">hello following example shows hello settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

<span data-ttu-id="572e1-122">U kunt verwijzen toohello [Service definitie Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) voor een beter begrip van XML-schema Hallo hier gebruikt, maar hier volgt een korte uitleg van een aantal Hallo elementen:</span><span class="sxs-lookup"><span data-stu-id="572e1-122">You can refer toohello [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of hello XML schema used here, however, here is a quick explanation of some of hello elements:</span></span>

<span data-ttu-id="572e1-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="572e1-123">**Sites**</span></span>  
<span data-ttu-id="572e1-124">Bevat de definities Hallo voor websites of web-toepassingen die worden gehost in IIS7.</span><span class="sxs-lookup"><span data-stu-id="572e1-124">Contains hello definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="572e1-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="572e1-125">**InputEndpoints**</span></span>  
<span data-ttu-id="572e1-126">Bevat definities voor eindpunten die zijn Hallo toocontact hello cloudservice gebruikt.</span><span class="sxs-lookup"><span data-stu-id="572e1-126">Contains hello definitions for endpoints that are used toocontact hello cloud service.</span></span>

<span data-ttu-id="572e1-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="572e1-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="572e1-128">Bevat de definities Hallo voor eindpunten die worden gebruikt door de functie instanties toocommunicate met elkaar.</span><span class="sxs-lookup"><span data-stu-id="572e1-128">Contains hello definitions for endpoints that are used by role instances toocommunicate with each other.</span></span>

<span data-ttu-id="572e1-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="572e1-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="572e1-130">Hallo instellingsdefinities voor de functies van een specifieke functie bevat.</span><span class="sxs-lookup"><span data-stu-id="572e1-130">Contains hello setting definitions for features of a specific role.</span></span>

<span data-ttu-id="572e1-131">**Certificaten**</span><span class="sxs-lookup"><span data-stu-id="572e1-131">**Certificates**</span></span>  
<span data-ttu-id="572e1-132">Bevat de definities Hallo voor certificaten die nodig zijn voor een rol.</span><span class="sxs-lookup"><span data-stu-id="572e1-132">Contains hello definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="572e1-133">Hallo vorige codevoorbeeld ziet u een certificaat dat wordt gebruikt voor het Hallo-configuratie van de Azure-verbinding.</span><span class="sxs-lookup"><span data-stu-id="572e1-133">hello previous code example shows a certificate that is used for hello configuration of Azure Connect.</span></span>

<span data-ttu-id="572e1-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="572e1-134">**LocalResources**</span></span>  
<span data-ttu-id="572e1-135">Bevat de definities Hallo voor resources voor lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="572e1-135">Contains hello definitions for local storage resources.</span></span> <span data-ttu-id="572e1-136">Een lokale opslagbron is een gereserveerde map op het bestandssysteem Hallo van Hallo virtuele machine waarop een exemplaar van een rol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="572e1-136">A local storage resource is a reserved directory on hello file system of hello virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="572e1-137">**Invoer**</span><span class="sxs-lookup"><span data-stu-id="572e1-137">**Imports**</span></span>  
<span data-ttu-id="572e1-138">Bevat de definities Hallo voor geïmporteerde modules.</span><span class="sxs-lookup"><span data-stu-id="572e1-138">Contains hello definitions for imported modules.</span></span> <span data-ttu-id="572e1-139">Hallo vorige codevoorbeeld toont Hallo-modules voor verbinding met extern bureaublad en Azure-verbinding.</span><span class="sxs-lookup"><span data-stu-id="572e1-139">hello previous code example shows hello modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="572e1-140">**Opstarten**</span><span class="sxs-lookup"><span data-stu-id="572e1-140">**Startup**</span></span>  
<span data-ttu-id="572e1-141">Bevat taken die worden uitgevoerd wanneer het Hallo-rol wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="572e1-141">Contains tasks that are run when hello role starts.</span></span> <span data-ttu-id="572e1-142">Hallo-taken zijn gedefinieerd in een .cmd of uitvoerbaar bestand.</span><span class="sxs-lookup"><span data-stu-id="572e1-142">hello tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="572e1-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="572e1-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="572e1-144">Hallo-configuratie van Hallo-instellingen voor uw cloudservice wordt bepaald door de waarden Hallo in Hallo **ServiceConfiguration.cscfg** bestand.</span><span class="sxs-lookup"><span data-stu-id="572e1-144">hello configuration of hello settings for your cloud service is determined by hello values in hello **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="572e1-145">U opgeven Hallo aantal instanties dat u toodeploy voor elke rol in dit bestand wilt.</span><span class="sxs-lookup"><span data-stu-id="572e1-145">You specify hello number of instances that you want toodeploy for each role in this file.</span></span> <span data-ttu-id="572e1-146">Hallo-waarden voor Hallo configuratie-instellingen die u hebt gedefinieerd in het servicedefinitiebestand hello, toohello serviceconfiguratiebestand worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="572e1-146">hello values for hello configuration settings that you defined in hello service definition file are added toohello service configuration file.</span></span> <span data-ttu-id="572e1-147">Hallo vingerafdrukken instellen voor van beheercertificaten die gekoppeld aan de cloudservice Hallo zijn ook toohello bestand toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="572e1-147">hello thumbprints for any management certificates that are associated with hello cloud service are also added toohello file.</span></span> <span data-ttu-id="572e1-148">Hallo [configuratieschema voor Azure-Service (.cscfg-bestand)](https://msdn.microsoft.com/library/azure/ee758710.aspx) Hallo toegestane indeling voorziet in een configuratiebestand voor de service.</span><span class="sxs-lookup"><span data-stu-id="572e1-148">hello [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides hello allowable format for a service configuration file.</span></span>

<span data-ttu-id="572e1-149">Hallo serviceconfiguratiebestand wordt niet geleverd met de toepassing hello, maar is geüploade tooAzure als een afzonderlijk bestand en wordt gebruikte tooconfigure hello cloudservice.</span><span class="sxs-lookup"><span data-stu-id="572e1-149">hello service configuration file is not packaged with hello application, but is uploaded tooAzure as a separate file and is used tooconfigure hello cloud service.</span></span> <span data-ttu-id="572e1-150">U kunt een nieuwe service-configuratiebestand zonder uw cloudservice opnieuw uploaden.</span><span class="sxs-lookup"><span data-stu-id="572e1-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="572e1-151">Hallo configuratiewaarden voor Hallo cloudservice kunnen worden gewijzigd terwijl Hallo cloudservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="572e1-151">hello configuration values for hello cloud service can be changed while hello cloud service is running.</span></span> <span data-ttu-id="572e1-152">Hallo toont volgende voorbeeld Hallo configuratie-instellingen die kunnen worden gedefinieerd voor hello Web- en werkrollen:</span><span class="sxs-lookup"><span data-stu-id="572e1-152">hello following example shows hello configuration settings that can be defined for hello Web and Worker roles:</span></span>

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

<span data-ttu-id="572e1-153">Raadpleegt u toohello [Service configuratieschema](https://msdn.microsoft.com/library/azure/ee758710.aspx) voor een beter begrip Hallo XML-schema hier gebruikt, hier is echter een korte uitleg van Hallo elementen:</span><span class="sxs-lookup"><span data-stu-id="572e1-153">You can refer toohello [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding hello XML schema used here, however, here is a quick explanation of hello elements:</span></span>

<span data-ttu-id="572e1-154">**Exemplaren**</span><span class="sxs-lookup"><span data-stu-id="572e1-154">**Instances**</span></span>  
<span data-ttu-id="572e1-155">Hiermee configureert u Hallo aantal actieve exemplaren voor Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="572e1-155">Configures hello number of running instances for hello role.</span></span> <span data-ttu-id="572e1-156">tooprevent uw cloud-service niet langer mogelijk niet beschikbaar tijdens upgrades, is het aanbevolen dat u meer dan één exemplaar van de functies van uw web gerichte implementeert.</span><span class="sxs-lookup"><span data-stu-id="572e1-156">tooprevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="572e1-157">Door het implementeren van meer dan één exemplaar u toohello richtlijnen in Hallo voldoet [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), die wordt gegarandeerd dat externe connectiviteit van 99,95% voor internetgerichte rollen wanneer twee of meer rol exemplaren worden geïmplementeerd voor een service.</span><span class="sxs-lookup"><span data-stu-id="572e1-157">By deploying more than one instance, you are adhering toohello guidelines in hello [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="572e1-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="572e1-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="572e1-159">Hallo-instellingen voor Hallo actieve exemplaren voor een functie configureert.</span><span class="sxs-lookup"><span data-stu-id="572e1-159">Configures hello settings for hello running instances for a role.</span></span> <span data-ttu-id="572e1-160">Hallo-naam van Hallo `<Setting>` elementen moeten overeenkomen met de definities in het servicedefinitiebestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-160">hello name of hello `<Setting>` elements must match hello setting definitions in hello service definition file.</span></span>

<span data-ttu-id="572e1-161">**Certificaten**</span><span class="sxs-lookup"><span data-stu-id="572e1-161">**Certificates**</span></span>  
<span data-ttu-id="572e1-162">Hallo-certificaten die worden gebruikt door Hallo service configureert.</span><span class="sxs-lookup"><span data-stu-id="572e1-162">Configures hello certificates that are used by hello service.</span></span> <span data-ttu-id="572e1-163">Hallo vorige codevoorbeeld ziet u hoe toodefine Hallo certificaat voor Hallo RemoteAccess-module.</span><span class="sxs-lookup"><span data-stu-id="572e1-163">hello previous code example shows how toodefine hello certificate for hello RemoteAccess module.</span></span> <span data-ttu-id="572e1-164">waarde van Hallo Hallo *vingerafdruk* kenmerk toohello vingerafdruk van Hallo certificaat toouse moet worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="572e1-164">hello value of hello *thumbprint* attribute must be set toohello thumbprint of hello certificate toouse.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="572e1-165">Hallo vingerafdruk voor Hallo certificaat kan configuratiebestand toohello worden toegevoegd met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="572e1-165">hello thumbprint for hello certificate can be added toohello configuration file by using a text editor.</span></span> <span data-ttu-id="572e1-166">Of het Hallo-waarde kan worden toegevoegd op Hallo **certificaten** tabblad Hallo **eigenschappen** pagina van de rol Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="572e1-166">Or, hello value can be added on hello **Certificates** tab of hello **Properties** page of hello role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="572e1-167">Poorten voor rolinstanties definiëren</span><span class="sxs-lookup"><span data-stu-id="572e1-167">Defining ports for role instances</span></span>
<span data-ttu-id="572e1-168">Azure kan slechts één vermelding punt tooa-Webrol.</span><span class="sxs-lookup"><span data-stu-id="572e1-168">Azure allows only one entry point tooa web role.</span></span> <span data-ttu-id="572e1-169">Dit betekent dat alle verkeer vindt plaats via één IP-adres.</span><span class="sxs-lookup"><span data-stu-id="572e1-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="572e1-170">U kunt uw websites tooshare een poort configureren door Hallo host-header toodirect Hallo aanvraag toohello juiste locatie te configureren.</span><span class="sxs-lookup"><span data-stu-id="572e1-170">You can configure your websites tooshare a port by configuring hello host header toodirect hello request toohello correct location.</span></span> <span data-ttu-id="572e1-171">U kunt ook uw toepassingen toolisten toowell bekende poorten op Hallo IP-adres configureren.</span><span class="sxs-lookup"><span data-stu-id="572e1-171">You can also configure your applications toolisten toowell-known ports on hello IP address.</span></span>

<span data-ttu-id="572e1-172">Hallo toont volgende voorbeeld Hallo-configuratie voor een Webrol aan een toepassing website en webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="572e1-172">hello following sample shows hello configuration for a web role with a website and web application.</span></span> <span data-ttu-id="572e1-173">Hallo-website is geconfigureerd als Hallo standaardlocatie vermelding op poort 80 en Hallo webtoepassingen zijn geconfigureerde tooreceive aanvragen van een andere host-header 'mail.mysite.cloudapp.net' wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="572e1-173">hello website is configured as hello default entry location on port 80, and hello web applications are configured tooreceive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a><span data-ttu-id="572e1-174">Hallo-configuratie van een rol wijzigen</span><span class="sxs-lookup"><span data-stu-id="572e1-174">Changing hello configuration of a role</span></span>
<span data-ttu-id="572e1-175">U kunt Hallo configuratie van uw cloudservice bijwerken terwijl deze wordt uitgevoerd in Azure, zonder Hallo service offline te halen.</span><span class="sxs-lookup"><span data-stu-id="572e1-175">You can update hello configuration of your cloud service while it is running in Azure, without taking hello service offline.</span></span> <span data-ttu-id="572e1-176">toochange configuratiegegevens, kunt u ofwel een nieuw configuratiebestand uploaden of het Hallo-configuratiebestand bewerken in plaatsen en dit toepassen tooyour waarop service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="572e1-176">toochange configuration information, you can either upload a new configuration file, or edit hello configuration file in place and apply it tooyour running service.</span></span> <span data-ttu-id="572e1-177">wijzigingen Hallo volgende kunnen worden aangebracht toohello configuratie van een service:</span><span class="sxs-lookup"><span data-stu-id="572e1-177">hello following changes can be made toohello configuration of a service:</span></span>

* <span data-ttu-id="572e1-178">**Hallo-waarden van configuratie-instellingen wijzigen**</span><span class="sxs-lookup"><span data-stu-id="572e1-178">**Changing hello values of configuration settings**</span></span>  
  <span data-ttu-id="572e1-179">Als er een configuratie kunt Instellingswijzigingen, een rolinstantie kiezen tooapply Hallo wijzigen tijdens het Hallo-exemplaar is online of toorecycle Hallo exemplaar probleemloos en Hallo wijziging toepassen tijdens het Hallo-exemplaar is offline.</span><span class="sxs-lookup"><span data-stu-id="572e1-179">When a configuration setting changes, a role instance can choose tooapply hello change while hello instance is online, or toorecycle hello instance gracefully and apply hello change while hello instance is offline.</span></span>
* <span data-ttu-id="572e1-180">**Hallo service topologie rolinstanties wijzigen**</span><span class="sxs-lookup"><span data-stu-id="572e1-180">**Changing hello service topology of role instances**</span></span>  
  <span data-ttu-id="572e1-181">Wijzigingen in de netwerktopologie hebben geen invloed op de exemplaren die worden uitgevoerd, behalve wanneer een exemplaar wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="572e1-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="572e1-182">Alle overige exemplaren moeten in het algemeen niet toobe gerecycled; u kunt echter toorecycle rolinstanties antwoord tooa topologiewijziging in.</span><span class="sxs-lookup"><span data-stu-id="572e1-182">All remaining instances generally do not need toobe recycled; however, you can choose toorecycle role instances in response tooa topology change.</span></span>
* <span data-ttu-id="572e1-183">**Hallo certificaatvingerafdruk wijzigen**</span><span class="sxs-lookup"><span data-stu-id="572e1-183">**Changing hello certificate thumbprint**</span></span>  
  <span data-ttu-id="572e1-184">U kunt een certificaat alleen bijwerken wanneer een rolinstantie offline is.</span><span class="sxs-lookup"><span data-stu-id="572e1-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="572e1-185">Als een certificaat is toegevoegd, verwijderd of gewijzigd terwijl een rolinstantie online is, wordt Azure probleemloos Hallo exemplaar offline tooupdate Hallo certificaat nodig en deze weer online brengen nadat Hallo wijziging is aangebracht.</span><span class="sxs-lookup"><span data-stu-id="572e1-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes hello instance offline tooupdate hello certificate and bring it back online after hello change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="572e1-186">Wijzigingen in de configuratie met gebeurtenissen van de Runtime-Service verwerken</span><span class="sxs-lookup"><span data-stu-id="572e1-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="572e1-187">Hallo [Azure-Runtime-bibliotheek](https://msdn.microsoft.com/library/azure/mt419365.aspx) Hallo omvat [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) naamruimte, waardoor de klassen voor interactie met hello Azure-omgeving van een rol.</span><span class="sxs-lookup"><span data-stu-id="572e1-187">hello [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with hello Azure environment from a role.</span></span> <span data-ttu-id="572e1-188">Hallo [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) klasse definieert Hallo gebeurtenissen die worden gegenereerd voor en na een wijziging in de configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="572e1-188">hello [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines hello following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="572e1-189">**[Het wijzigen van](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="572e1-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="572e1-190">Dit vindt plaats voordat de configuratiewijziging Hallo toegepaste tooa opgegeven exemplaar van een rol zodat u een kans tootake omlaag Hallo rolinstanties indien nodig.</span><span class="sxs-lookup"><span data-stu-id="572e1-190">This occurs before hello configuration change is applied tooa specified instance of a role giving you a chance tootake down hello role instances if necessary.</span></span>
* <span data-ttu-id="572e1-191">**[Gewijzigd](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="572e1-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="572e1-192">Deze gebeurtenis treedt op nadat Hallo configuratiewijziging toegepaste tooa opgegeven exemplaar van een rol is.</span><span class="sxs-lookup"><span data-stu-id="572e1-192">Occurs after hello configuration change is applied tooa specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="572e1-193">Omdat wijzigingen certificaat altijd Hallo exemplaren van een rol offline halen, beter ze Hallo RoleEnvironment.Changing of RoleEnvironment.Changed gebeurtenissen niet verhogen.</span><span class="sxs-lookup"><span data-stu-id="572e1-193">Because certificate changes always take hello instances of a role offline, they do not raise hello RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="572e1-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="572e1-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="572e1-195">toodeploy een toepassing als een cloudservice in Azure, moet u de eerste pakket Hallo-toepassing in de juiste notatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-195">toodeploy an application as a cloud service in Azure, you must first package hello application in hello appropriate format.</span></span> <span data-ttu-id="572e1-196">Kunt u Hallo **CSPack** opdrachtregelprogramma (geïnstalleerd met Hallo [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate Hallo pakketbestand als een alternatieve tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="572e1-196">You can use hello **CSPack** command-line tool (installed with hello [Azure SDK](https://azure.microsoft.com/downloads/)) toocreate hello package file as an alternative tooVisual Studio.</span></span>

<span data-ttu-id="572e1-197">**CSPack** gebruikt Hallo inhoud Hallo service definitie bestands- en configuratie toodefine Hallo bestandsinhoud van Hallo-pakket.</span><span class="sxs-lookup"><span data-stu-id="572e1-197">**CSPack** uses hello contents of hello service definition file and service configuration file toodefine hello contents of hello package.</span></span> <span data-ttu-id="572e1-198">**CSPack** genereert een toepassingspakketbestand (.cspkg) dat u tooAzure kunt uploaden via Hallo [Azure-portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="572e1-198">**CSPack** generates an application package file (.cspkg) that you can upload tooAzure by using hello [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="572e1-199">Standaard Hallo pakket heet `[ServiceDefinitionFileName].cspkg`, maar u kunt een andere naam opgeven met behulp van Hallo `/out` optie **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="572e1-199">By default, hello package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using hello `/out` option of **CSPack**.</span></span>

<span data-ttu-id="572e1-200">**CSPack** bevindt zich op</span><span class="sxs-lookup"><span data-stu-id="572e1-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="572e1-201">CSPack.exe (op windows) is beschikbaar door het uitvoeren van Hallo **Microsoft Azure-opdrachtprompt** snelkoppeling die is geïnstalleerd met Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="572e1-201">CSPack.exe (on windows) is available by running hello **Microsoft Azure Command Prompt** shortcut that is installed with hello SDK.</span></span>  
> 
> <span data-ttu-id="572e1-202">Hallo CSPack.exe programma zelfstandig toosee documentatie over alle mogelijke Hallo-switches en opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="572e1-202">Run hello CSPack.exe program by itself toosee documentation about all hello possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="572e1-203">Lokaal uitvoeren van de cloudservice in Hallo **Microsoft Azure Compute-Emulator**, gebruik Hallo **/copyonly** optie.</span><span class="sxs-lookup"><span data-stu-id="572e1-203">Run your cloud service locally in hello **Microsoft Azure Compute Emulator**, use hello **/copyonly** option.</span></span> <span data-ttu-id="572e1-204">Deze optie kopieert Hallo binaire bestanden voor Hallo tooa directory indeling van de toepassing waaruit ze kunnen worden uitgevoerd in Hallo rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="572e1-204">This option copies hello binary files for hello application tooa directory layout from which they can be run in hello compute emulator.</span></span>
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a><span data-ttu-id="572e1-205">Voorbeeld van de opdracht toopackage een cloudservice</span><span class="sxs-lookup"><span data-stu-id="572e1-205">Example command toopackage a cloud service</span></span>
<span data-ttu-id="572e1-206">Hallo wordt volgende voorbeeld een toepassingspakket met daarin Hallo-informatie voor een Webrol.</span><span class="sxs-lookup"><span data-stu-id="572e1-206">hello following example creates an application package that contains hello information for a web role.</span></span> <span data-ttu-id="572e1-207">Hallo-opdracht geeft Hallo service definitie bestand toouse, Hallo directory waar de binaire bestanden kunnen worden gevonden en de naam van het pakketbestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-207">hello command specifies hello service definition file toouse, hello directory where binary files can be found, and hello name of hello package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="572e1-208">Als de toepassing hello zowel een Webrol en een werkrol bevat, wordt hello volgende opdracht gebruikt:</span><span class="sxs-lookup"><span data-stu-id="572e1-208">If hello application contains both a web role and a worker role, hello following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="572e1-209">Waar Hallo variabelen worden als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="572e1-209">Where hello variables are defined as follows:</span></span>

| <span data-ttu-id="572e1-210">Variabele</span><span class="sxs-lookup"><span data-stu-id="572e1-210">Variable</span></span> | <span data-ttu-id="572e1-211">Waarde</span><span class="sxs-lookup"><span data-stu-id="572e1-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="572e1-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="572e1-212">\[DirectoryName\]</span></span> |<span data-ttu-id="572e1-213">Hallo submap onder Hallo project hoofdmap die Hallo csdef-bestand van hello Azure-project bevat.</span><span class="sxs-lookup"><span data-stu-id="572e1-213">hello subdirectory under hello root project directory that contains hello .csdef file of hello Azure project.</span></span> |
| <span data-ttu-id="572e1-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="572e1-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="572e1-215">Hallo-naam van het servicedefinitiebestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-215">hello name of hello service definition file.</span></span> <span data-ttu-id="572e1-216">Standaard is dit bestand ServiceDefinition.csdef naam.</span><span class="sxs-lookup"><span data-stu-id="572e1-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="572e1-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="572e1-217">\[OutputFileName\]</span></span> |<span data-ttu-id="572e1-218">Hallo-naam voor Hallo gegenereerd pakketbestand.</span><span class="sxs-lookup"><span data-stu-id="572e1-218">hello name for hello generated package file.</span></span> <span data-ttu-id="572e1-219">Dit is normaal gesproken toohello naam van de toepassing hello ingesteld.</span><span class="sxs-lookup"><span data-stu-id="572e1-219">Typically, this is set toohello name of hello application.</span></span> <span data-ttu-id="572e1-220">Als geen bestandsnaam is opgegeven, Hallo toepassingspakket is gemaakt als \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="572e1-220">If no file name is specified, hello application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="572e1-221">\[Rolnaam\]</span><span class="sxs-lookup"><span data-stu-id="572e1-221">\[RoleName\]</span></span> |<span data-ttu-id="572e1-222">Hallo-naam van Hallo rol zoals gedefinieerd in het servicedefinitiebestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-222">hello name of hello role as defined in hello service definition file.</span></span> |
| <span data-ttu-id="572e1-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="572e1-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="572e1-224">Hallo-locatie van de binaire bestanden voor de rol Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-224">hello location of hello binary files for hello role.</span></span> |
| <span data-ttu-id="572e1-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="572e1-225">\[VirtualPath\]</span></span> |<span data-ttu-id="572e1-226">Hallo fysieke mappen voor elke virtuele pad gedefinieerd in Hallo sectie Sites van Hallo servicedefinitie.</span><span class="sxs-lookup"><span data-stu-id="572e1-226">hello physical directories for each virtual path defined in hello Sites section of hello service definition.</span></span> |
| <span data-ttu-id="572e1-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="572e1-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="572e1-228">Hallo fysieke mappen van inhoud voor elke virtuele pad dat is gedefinieerd in Hallo siteknooppunt van de servicedefinitie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-228">hello physical directories of hello contents for each virtual path defined in hello site node of hello service definition.</span></span> |
| <span data-ttu-id="572e1-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="572e1-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="572e1-230">Hallo-naam van binair bestand voor de rol Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="572e1-230">hello name of hello binary file for hello role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="572e1-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="572e1-231">Next steps</span></span>
<span data-ttu-id="572e1-232">Ik ben een cloud service-pakket maken en ik wil...</span><span class="sxs-lookup"><span data-stu-id="572e1-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="572e1-233">[Extern bureaublad instellen voor een cloud service-exemplaar][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="572e1-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="572e1-234">[Een Cloud Service-project implementeert][deploy]</span><span class="sxs-lookup"><span data-stu-id="572e1-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="572e1-235">Ik gebruik Visual Studio en ik wil...</span><span class="sxs-lookup"><span data-stu-id="572e1-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="572e1-236">[Maak een nieuwe cloudservice][vs_create]</span><span class="sxs-lookup"><span data-stu-id="572e1-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="572e1-237">[Configureren van een bestaande cloudservice][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="572e1-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="572e1-238">[Een Cloud Service-project implementeert][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="572e1-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="572e1-239">[Extern bureaublad instellen voor een cloud service-exemplaar][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="572e1-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
