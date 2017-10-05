---
title: Wat is er een Service in de Cloud-model en het pakket | Microsoft Docs
description: Hierin worden de cloud-servicemodel (csdef, cscfg-bestand) en het pakket (.cspkg) in Azure
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
ms.openlocfilehash: 21fbdbc4c24440c6fbbd7487cfbb2e0a3140aa96
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-the-cloud-service-model-and-how-do-i-package-it"></a><span data-ttu-id="c6778-103">Wat is het Cloudservice-model en hoe ik dit pakket?</span><span class="sxs-lookup"><span data-stu-id="c6778-103">What is the Cloud Service model and how do I package it?</span></span>
<span data-ttu-id="c6778-104">Een cloudservice is gemaakt op basis van drie onderdelen, de servicedefinitie *(.csdef)*, de serviceconfiguratie *(.cscfg)*, en een servicepakket *(.cspkg)*.</span><span class="sxs-lookup"><span data-stu-id="c6778-104">A cloud service is created from three components, the service definition *(.csdef)*, the service config *(.cscfg)*, and a service package *(.cspkg)*.</span></span> <span data-ttu-id="c6778-105">Zowel de **ServiceDefinition.csdef** en **ServiceConfig.cscfg** bestanden zijn XML- en beschrijven de structuur van de cloudservice en de manier waarop deze geconfigureerd; genoemd op het model.</span><span class="sxs-lookup"><span data-stu-id="c6778-105">Both the **ServiceDefinition.csdef** and **ServiceConfig.cscfg** files are XML-based and describe the structure of the cloud service and how it's configured; collectively called the model.</span></span> <span data-ttu-id="c6778-106">De **ServicePackage.cspkg** is een zipbestand dat is gegenereerd op basis van de **ServiceDefinition.csdef** en onder andere bevat alle vereiste binaire gebaseerde afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="c6778-106">The **ServicePackage.cspkg** is a zip file that is generated from the **ServiceDefinition.csdef** and among other things, contains all the required binary-based dependencies.</span></span> <span data-ttu-id="c6778-107">Azure maakt een cloudservice van zowel de **ServicePackage.cspkg** en de **ServiceConfig.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="c6778-107">Azure creates a cloud service from both the **ServicePackage.cspkg** and the **ServiceConfig.cscfg**.</span></span>

<span data-ttu-id="c6778-108">Zodra de cloudservice in Azure wordt uitgevoerd, kunt u het configureren via de **ServiceConfig.cscfg** bestand, maar kan de definitie niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c6778-108">Once the cloud service is running in Azure, you can reconfigure it through the **ServiceConfig.cscfg** file, but you cannot alter the definition.</span></span>

## <a name="what-would-you-like-to-know-more-about"></a><span data-ttu-id="c6778-109">Wat wilt u meer weten?</span><span class="sxs-lookup"><span data-stu-id="c6778-109">What would you like to know more about?</span></span>
* <span data-ttu-id="c6778-110">Ik wil meer informatie over de [ServiceDefinition.csdef](#csdef) en [ServiceConfig.cscfg](#cscfg) bestanden.</span><span class="sxs-lookup"><span data-stu-id="c6778-110">I want to know more about the [ServiceDefinition.csdef](#csdef) and [ServiceConfig.cscfg](#cscfg) files.</span></span>
* <span data-ttu-id="c6778-111">Ik heb al weet over die, geef me [enkele voorbeelden](#next-steps) op ik kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="c6778-111">I already know about that, give me [some examples](#next-steps) on what I can configure.</span></span>
* <span data-ttu-id="c6778-112">Ik wil maken de [ServicePackage.cspkg](#cspkg).</span><span class="sxs-lookup"><span data-stu-id="c6778-112">I want to create the [ServicePackage.cspkg](#cspkg).</span></span>
* <span data-ttu-id="c6778-113">Ik gebruik Visual Studio en ik wil...</span><span class="sxs-lookup"><span data-stu-id="c6778-113">I am using Visual Studio and I want to...</span></span>
  * <span data-ttu-id="c6778-114">[Maak een cloudservice][vs_create]</span><span class="sxs-lookup"><span data-stu-id="c6778-114">[Create a cloud service][vs_create]</span></span>
  * <span data-ttu-id="c6778-115">[Configureren van een bestaande cloudservice][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="c6778-115">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
  * <span data-ttu-id="c6778-116">[Een Cloud Service-project implementeert][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="c6778-116">[Deploy a Cloud Service project][vs_deploy]</span></span>
  * <span data-ttu-id="c6778-117">[Extern bureaublad in een cloud service-exemplaar][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="c6778-117">[Remote desktop into a cloud service instance][remotedesktop]</span></span>

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a><span data-ttu-id="c6778-118">ServiceDefinition.csdef</span><span class="sxs-lookup"><span data-stu-id="c6778-118">ServiceDefinition.csdef</span></span>
<span data-ttu-id="c6778-119">De **ServiceDefinition.csdef** bestand geeft de instellingen die door Azure worden gebruikt om een cloudservice te configureren.</span><span class="sxs-lookup"><span data-stu-id="c6778-119">The **ServiceDefinition.csdef** file specifies the settings that are used by Azure to configure a cloud service.</span></span> <span data-ttu-id="c6778-120">De [Azure Service definitie Schema (.csdef-bestand)](https://msdn.microsoft.com/library/azure/ee758711.aspx) biedt de toegestane notatie voor een servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-120">The [Azure Service Definition Schema (.csdef File)](https://msdn.microsoft.com/library/azure/ee758711.aspx) provides the allowable format for a service definition file.</span></span> <span data-ttu-id="c6778-121">Het volgende voorbeeld ziet u de instellingen die kunnen worden gedefinieerd voor de Web- en werkrollen rollen:</span><span class="sxs-lookup"><span data-stu-id="c6778-121">The following example shows the settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="c6778-122">U kunt verwijzen naar de [Service definitie Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) voor een beter inzicht in het XML-schema hier gebruikt, maar hier volgt een korte uitleg van enkele van de elementen:</span><span class="sxs-lookup"><span data-stu-id="c6778-122">You can refer to the [Service Definition Schema](https://msdn.microsoft.com/library/azure/ee758711.aspx) for a better understanding of the XML schema used here, however, here is a quick explanation of some of the elements:</span></span>

<span data-ttu-id="c6778-123">**Sites**</span><span class="sxs-lookup"><span data-stu-id="c6778-123">**Sites**</span></span>  
<span data-ttu-id="c6778-124">Bevat de definities voor websites of web-toepassingen die worden gehost in IIS7.</span><span class="sxs-lookup"><span data-stu-id="c6778-124">Contains the definitions for websites or web applications that are hosted in IIS7.</span></span>

<span data-ttu-id="c6778-125">**InputEndpoints**</span><span class="sxs-lookup"><span data-stu-id="c6778-125">**InputEndpoints**</span></span>  
<span data-ttu-id="c6778-126">Bevat de definities voor eindpunten die worden gebruikt voor het contact op met de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="c6778-126">Contains the definitions for endpoints that are used to contact the cloud service.</span></span>

<span data-ttu-id="c6778-127">**InternalEndpoints**</span><span class="sxs-lookup"><span data-stu-id="c6778-127">**InternalEndpoints**</span></span>  
<span data-ttu-id="c6778-128">Bevat de definities voor eindpunten die worden gebruikt door de rolinstanties met elkaar communiceren.</span><span class="sxs-lookup"><span data-stu-id="c6778-128">Contains the definitions for endpoints that are used by role instances to communicate with each other.</span></span>

<span data-ttu-id="c6778-129">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="c6778-129">**ConfigurationSettings**</span></span>  
<span data-ttu-id="c6778-130">Bevat de instellingsdefinities voor onderdelen van een specifieke rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-130">Contains the setting definitions for features of a specific role.</span></span>

<span data-ttu-id="c6778-131">**Certificaten**</span><span class="sxs-lookup"><span data-stu-id="c6778-131">**Certificates**</span></span>  
<span data-ttu-id="c6778-132">Bevat de definities voor certificaten die nodig zijn voor een rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-132">Contains the definitions for certificates that are needed for a role.</span></span> <span data-ttu-id="c6778-133">Het vorige codevoorbeeld ziet u een certificaat dat wordt gebruikt voor de configuratie van de Azure-verbinding.</span><span class="sxs-lookup"><span data-stu-id="c6778-133">The previous code example shows a certificate that is used for the configuration of Azure Connect.</span></span>

<span data-ttu-id="c6778-134">**LocalResources**</span><span class="sxs-lookup"><span data-stu-id="c6778-134">**LocalResources**</span></span>  
<span data-ttu-id="c6778-135">Bevat de definities voor resources voor lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="c6778-135">Contains the definitions for local storage resources.</span></span> <span data-ttu-id="c6778-136">Een lokale opslagbron is een gereserveerde map op het bestandssysteem van de virtuele machine waarop een exemplaar van een rol wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6778-136">A local storage resource is a reserved directory on the file system of the virtual machine in which an instance of a role is running.</span></span>

<span data-ttu-id="c6778-137">**Invoer**</span><span class="sxs-lookup"><span data-stu-id="c6778-137">**Imports**</span></span>  
<span data-ttu-id="c6778-138">Bevat de definities voor geïmporteerde modules.</span><span class="sxs-lookup"><span data-stu-id="c6778-138">Contains the definitions for imported modules.</span></span> <span data-ttu-id="c6778-139">Het vorige codevoorbeeld toont de modules voor verbinding met extern bureaublad en Azure-verbinding.</span><span class="sxs-lookup"><span data-stu-id="c6778-139">The previous code example shows the modules for Remote Desktop Connection and Azure Connect.</span></span>

<span data-ttu-id="c6778-140">**Opstarten**</span><span class="sxs-lookup"><span data-stu-id="c6778-140">**Startup**</span></span>  
<span data-ttu-id="c6778-141">Bevat taken die worden uitgevoerd wanneer de functie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="c6778-141">Contains tasks that are run when the role starts.</span></span> <span data-ttu-id="c6778-142">De taken zijn gedefinieerd in een .cmd of uitvoerbaar bestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-142">The tasks are defined in a .cmd or executable file.</span></span>

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a><span data-ttu-id="c6778-143">ServiceConfiguration.cscfg</span><span class="sxs-lookup"><span data-stu-id="c6778-143">ServiceConfiguration.cscfg</span></span>
<span data-ttu-id="c6778-144">De configuratie van de instellingen voor uw cloudservice wordt bepaald door de waarden in de **ServiceConfiguration.cscfg** bestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-144">The configuration of the settings for your cloud service is determined by the values in the **ServiceConfiguration.cscfg** file.</span></span> <span data-ttu-id="c6778-145">U opgeven het aantal exemplaren die u wilt implementeren voor elke rol in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-145">You specify the number of instances that you want to deploy for each role in this file.</span></span> <span data-ttu-id="c6778-146">De waarden voor de configuratie-instellingen die u hebt gedefinieerd in het servicedefinitiebestand worden toegevoegd aan het configuratiebestand van de service.</span><span class="sxs-lookup"><span data-stu-id="c6778-146">The values for the configuration settings that you defined in the service definition file are added to the service configuration file.</span></span> <span data-ttu-id="c6778-147">De vingerafdrukken instellen voor van beheercertificaten die gekoppeld aan de cloudservice zijn worden ook toegevoegd aan het bestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-147">The thumbprints for any management certificates that are associated with the cloud service are also added to the file.</span></span> <span data-ttu-id="c6778-148">De [configuratieschema voor Azure-Service (.cscfg-bestand)](https://msdn.microsoft.com/library/azure/ee758710.aspx) biedt de toegestane notatie voor een service-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-148">The [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx) provides the allowable format for a service configuration file.</span></span>

<span data-ttu-id="c6778-149">Het configuratiebestand van de service niet wordt verpakt met de toepassing, maar is geüpload naar Azure als een afzonderlijk bestand en wordt gebruikt om de cloudservice te configureren.</span><span class="sxs-lookup"><span data-stu-id="c6778-149">The service configuration file is not packaged with the application, but is uploaded to Azure as a separate file and is used to configure the cloud service.</span></span> <span data-ttu-id="c6778-150">U kunt een nieuwe service-configuratiebestand zonder uw cloudservice opnieuw uploaden.</span><span class="sxs-lookup"><span data-stu-id="c6778-150">You can upload a new service configuration file without redeploying your cloud service.</span></span> <span data-ttu-id="c6778-151">De configuratiewaarden voor de cloudservice kunnen worden gewijzigd terwijl de cloudservice wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c6778-151">The configuration values for the cloud service can be changed while the cloud service is running.</span></span> <span data-ttu-id="c6778-152">Het volgende voorbeeld ziet u de configuratie-instellingen die kunnen worden gedefinieerd voor de Web- en werkrollen rollen:</span><span class="sxs-lookup"><span data-stu-id="c6778-152">The following example shows the configuration settings that can be defined for the Web and Worker roles:</span></span>

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

<span data-ttu-id="c6778-153">U kunt verwijzen naar de [Service configuratieschema](https://msdn.microsoft.com/library/azure/ee758710.aspx) voor een beter inzicht in het XML-schema hier gebruikt, maar hier volgt een korte uitleg van de elementen:</span><span class="sxs-lookup"><span data-stu-id="c6778-153">You can refer to the [Service Configuration Schema](https://msdn.microsoft.com/library/azure/ee758710.aspx) for better understanding the XML schema used here, however, here is a quick explanation of the elements:</span></span>

<span data-ttu-id="c6778-154">**Exemplaren**</span><span class="sxs-lookup"><span data-stu-id="c6778-154">**Instances**</span></span>  
<span data-ttu-id="c6778-155">Hiermee configureert u het aantal actieve exemplaren voor de rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-155">Configures the number of running instances for the role.</span></span> <span data-ttu-id="c6778-156">Als u wilt voorkomen dat uw cloudservice mogelijk niet beschikbaar tijdens upgrades, wordt het aanbevolen dat u meer dan één exemplaar van de functies van uw web gerichte implementeert.</span><span class="sxs-lookup"><span data-stu-id="c6778-156">To prevent your cloud service from potentially becoming unavailable during upgrades, it is recommended that you deploy more than one instance of your web-facing roles.</span></span> <span data-ttu-id="c6778-157">Door het implementeren van meer dan één exemplaar u voldoet aan de richtlijnen in de [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), die wordt gegarandeerd dat externe connectiviteit van 99,95% voor internetgerichte rollen wanneer twee of meer rolinstanties zijn geïmplementeerd voor een service.</span><span class="sxs-lookup"><span data-stu-id="c6778-157">By deploying more than one instance, you are adhering to the guidelines in the [Azure Compute Service Level Agreement (SLA)](http://azure.microsoft.com/support/legal/sla/), which guarantees 99.95% external connectivity for Internet-facing roles when two or more role instances are deployed for a service.</span></span>

<span data-ttu-id="c6778-158">**ConfigurationSettings**</span><span class="sxs-lookup"><span data-stu-id="c6778-158">**ConfigurationSettings**</span></span>  
<span data-ttu-id="c6778-159">Hiermee configureert u de instellingen voor de exemplaren die worden uitgevoerd voor een rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-159">Configures the settings for the running instances for a role.</span></span> <span data-ttu-id="c6778-160">De naam van de `<Setting>` elementen moeten overeenkomen met de instellingsdefinities in het servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-160">The name of the `<Setting>` elements must match the setting definitions in the service definition file.</span></span>

<span data-ttu-id="c6778-161">**Certificaten**</span><span class="sxs-lookup"><span data-stu-id="c6778-161">**Certificates**</span></span>  
<span data-ttu-id="c6778-162">Hiermee configureert u de certificaten die worden gebruikt door de service.</span><span class="sxs-lookup"><span data-stu-id="c6778-162">Configures the certificates that are used by the service.</span></span> <span data-ttu-id="c6778-163">Het vorige codevoorbeeld toont het definiëren van het certificaat voor de Remote Access-module.</span><span class="sxs-lookup"><span data-stu-id="c6778-163">The previous code example shows how to define the certificate for the RemoteAccess module.</span></span> <span data-ttu-id="c6778-164">De waarde van de *vingerafdruk* kenmerk moet worden ingesteld op de vingerafdruk van het certificaat te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c6778-164">The value of the *thumbprint* attribute must be set to the thumbprint of the certificate to use.</span></span>

<p/>

> [!NOTE]
> <span data-ttu-id="c6778-165">De vingerafdruk van het certificaat kan worden toegevoegd aan het configuratiebestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="c6778-165">The thumbprint for the certificate can be added to the configuration file by using a text editor.</span></span> <span data-ttu-id="c6778-166">Of de waarde mag worden toegevoegd aan de **certificaten** tabblad van de **eigenschappen** pagina van de rol in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6778-166">Or, the value can be added on the **Certificates** tab of the **Properties** page of the role in Visual Studio.</span></span>
> 
> 

## <a name="defining-ports-for-role-instances"></a><span data-ttu-id="c6778-167">Poorten voor rolinstanties definiëren</span><span class="sxs-lookup"><span data-stu-id="c6778-167">Defining ports for role instances</span></span>
<span data-ttu-id="c6778-168">Azure kan slechts één toegangspunt aan een Webrol.</span><span class="sxs-lookup"><span data-stu-id="c6778-168">Azure allows only one entry point to a web role.</span></span> <span data-ttu-id="c6778-169">Dit betekent dat alle verkeer vindt plaats via één IP-adres.</span><span class="sxs-lookup"><span data-stu-id="c6778-169">Meaning that all traffic occurs through one IP address.</span></span> <span data-ttu-id="c6778-170">U kunt uw websites als u wilt een poort delen door het configureren van de host-header voor de aanvraag naar de juiste locatie configureren.</span><span class="sxs-lookup"><span data-stu-id="c6778-170">You can configure your websites to share a port by configuring the host header to direct the request to the correct location.</span></span> <span data-ttu-id="c6778-171">U kunt ook uw toepassingen om te luisteren naar bekende poorten van het IP-adres configureren.</span><span class="sxs-lookup"><span data-stu-id="c6778-171">You can also configure your applications to listen to well-known ports on the IP address.</span></span>

<span data-ttu-id="c6778-172">Het volgende voorbeeld ziet u de configuratie voor een Webrol aan een toepassing website en webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="c6778-172">The following sample shows the configuration for a web role with a website and web application.</span></span> <span data-ttu-id="c6778-173">De website is geconfigureerd als de standaardlocatie voor de vermelding op poort 80 en de webtoepassingen zijn geconfigureerd voor het ontvangen van aanvragen van een andere host-header 'mail.mysite.cloudapp.net' wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="c6778-173">The website is configured as the default entry location on port 80, and the web applications are configured to receive requests from an alternate host header that is called “mail.mysite.cloudapp.net”.</span></span>

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


## <a name="changing-the-configuration-of-a-role"></a><span data-ttu-id="c6778-174">Wijzigen van de configuratie van een rol</span><span class="sxs-lookup"><span data-stu-id="c6778-174">Changing the configuration of a role</span></span>
<span data-ttu-id="c6778-175">U kunt de configuratie van uw cloudservice bijwerken terwijl deze wordt uitgevoerd in Azure, zonder de service offline te halen.</span><span class="sxs-lookup"><span data-stu-id="c6778-175">You can update the configuration of your cloud service while it is running in Azure, without taking the service offline.</span></span> <span data-ttu-id="c6778-176">Om te wijzigen van configuratie-informatie, kunt u uploaden van een nieuw configuratiebestand of de configuratiebestand in-place bewerken en toepassen op uw actieve service.</span><span class="sxs-lookup"><span data-stu-id="c6778-176">To change configuration information, you can either upload a new configuration file, or edit the configuration file in place and apply it to your running service.</span></span> <span data-ttu-id="c6778-177">De volgende wijzigingen kunnen worden aangebracht in de configuratie van een service:</span><span class="sxs-lookup"><span data-stu-id="c6778-177">The following changes can be made to the configuration of a service:</span></span>

* <span data-ttu-id="c6778-178">**De waarden van configuratie-instellingen wijzigen**</span><span class="sxs-lookup"><span data-stu-id="c6778-178">**Changing the values of configuration settings**</span></span>  
  <span data-ttu-id="c6778-179">Wanneer een configuratie-instelling wijzigingen een rolinstantie kunt de wijziging toepassen terwijl het exemplaar online is of het exemplaar probleemloos recyclen en toepassen van de wijziging tijdens het exemplaar offline is.</span><span class="sxs-lookup"><span data-stu-id="c6778-179">When a configuration setting changes, a role instance can choose to apply the change while the instance is online, or to recycle the instance gracefully and apply the change while the instance is offline.</span></span>
* <span data-ttu-id="c6778-180">**Het wijzigen van de service-topologie van de rolinstanties**</span><span class="sxs-lookup"><span data-stu-id="c6778-180">**Changing the service topology of role instances**</span></span>  
  <span data-ttu-id="c6778-181">Wijzigingen in de netwerktopologie hebben geen invloed op de exemplaren die worden uitgevoerd, behalve wanneer een exemplaar wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="c6778-181">Topology changes do not affect running instances, except where an instance is being removed.</span></span> <span data-ttu-id="c6778-182">Alle resterende exemplaren in het algemeen hoeft niet te worden gerecycled; u kunt echter recyclen rolinstanties in reactie op een topologiewijziging in de.</span><span class="sxs-lookup"><span data-stu-id="c6778-182">All remaining instances generally do not need to be recycled; however, you can choose to recycle role instances in response to a topology change.</span></span>
* <span data-ttu-id="c6778-183">**Vingerafdruk van het certificaat wijzigen**</span><span class="sxs-lookup"><span data-stu-id="c6778-183">**Changing the certificate thumbprint**</span></span>  
  <span data-ttu-id="c6778-184">U kunt een certificaat alleen bijwerken wanneer een rolinstantie offline is.</span><span class="sxs-lookup"><span data-stu-id="c6778-184">You can only update a certificate when a role instance is offline.</span></span> <span data-ttu-id="c6778-185">Als een certificaat is toegevoegd, verwijderd of gewijzigd terwijl een rolinstantie online is, wordt Azure probleemloos het exemplaar offline voor het bijwerken van het certificaat en weer online brengen nadat de wijziging aangebracht is.</span><span class="sxs-lookup"><span data-stu-id="c6778-185">If a certificate is added, deleted, or changed while a role instance is online, Azure gracefully takes the instance offline to update the certificate and bring it back online after the change is complete.</span></span>

### <a name="handling-configuration-changes-with-service-runtime-events"></a><span data-ttu-id="c6778-186">Wijzigingen in de configuratie met gebeurtenissen van de Runtime-Service verwerken</span><span class="sxs-lookup"><span data-stu-id="c6778-186">Handling configuration changes with Service Runtime Events</span></span>
<span data-ttu-id="c6778-187">De [Azure-Runtime-bibliotheek](https://msdn.microsoft.com/library/azure/mt419365.aspx) bevat de [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) naamruimte, waardoor de klassen voor interactie met de Azure-omgeving van een rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-187">The [Azure Runtime Library](https://msdn.microsoft.com/library/azure/mt419365.aspx) includes the [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) namespace, which provides classes for interacting with the Azure environment from a role.</span></span> <span data-ttu-id="c6778-188">De [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) klasse definieert de volgende gebeurtenissen die worden gegenereerd voor en na een wijziging in de configuratie:</span><span class="sxs-lookup"><span data-stu-id="c6778-188">The [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) class defines the following events that are raised before and after a configuration change:</span></span>

* <span data-ttu-id="c6778-189">**[Het wijzigen van](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="c6778-189">**[Changing](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) event**</span></span>  
  <span data-ttu-id="c6778-190">Dit gebeurt voordat de wijziging in de configuratie wordt toegepast op een opgegeven exemplaar van een rol zodat u de kans te nemen de exemplaren van de rol, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="c6778-190">This occurs before the configuration change is applied to a specified instance of a role giving you a chance to take down the role instances if necessary.</span></span>
* <span data-ttu-id="c6778-191">**[Gewijzigd](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) gebeurtenis**</span><span class="sxs-lookup"><span data-stu-id="c6778-191">**[Changed](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) event**</span></span>  
  <span data-ttu-id="c6778-192">Deze gebeurtenis treedt op nadat de wijziging in de configuratie is toegepast op een opgegeven exemplaar van een rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-192">Occurs after the configuration change is applied to a specified instance of a role.</span></span>

> [!NOTE]
> <span data-ttu-id="c6778-193">Omdat wijzigingen certificaat altijd de exemplaren van een functie offline halen, komen ze niet de gebeurtenissen RoleEnvironment.Changing of RoleEnvironment.Changed verhogen.</span><span class="sxs-lookup"><span data-stu-id="c6778-193">Because certificate changes always take the instances of a role offline, they do not raise the RoleEnvironment.Changing or RoleEnvironment.Changed events.</span></span>
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a><span data-ttu-id="c6778-194">ServicePackage.cspkg</span><span class="sxs-lookup"><span data-stu-id="c6778-194">ServicePackage.cspkg</span></span>
<span data-ttu-id="c6778-195">Als u wilt een toepassing als een cloudservice in Azure implementeert, moet u eerst inpakken van de toepassing in de juiste indeling.</span><span class="sxs-lookup"><span data-stu-id="c6778-195">To deploy an application as a cloud service in Azure, you must first package the application in the appropriate format.</span></span> <span data-ttu-id="c6778-196">U kunt de **CSPack** opdrachtregelprogramma (geïnstalleerd met de [Azure SDK](https://azure.microsoft.com/downloads/)) voor het maken van het pakketbestand als alternatief voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c6778-196">You can use the **CSPack** command-line tool (installed with the [Azure SDK](https://azure.microsoft.com/downloads/)) to create the package file as an alternative to Visual Studio.</span></span>

<span data-ttu-id="c6778-197">**CSPack** de inhoud van het servicedefinitiebestand en serviceconfiguratiebestand gebruikt voor het definiëren van de inhoud van het pakket.</span><span class="sxs-lookup"><span data-stu-id="c6778-197">**CSPack** uses the contents of the service definition file and service configuration file to define the contents of the package.</span></span> <span data-ttu-id="c6778-198">**CSPack** genereert een toepassingspakketbestand (.cspkg) die u uploaden naar Azure met behulp van kunt de [Azure-portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span><span class="sxs-lookup"><span data-stu-id="c6778-198">**CSPack** generates an application package file (.cspkg) that you can upload to Azure by using the [Azure portal](cloud-services-how-to-create-deploy-portal.md#create-and-deploy).</span></span> <span data-ttu-id="c6778-199">Standaard het pakket met de naam `[ServiceDefinitionFileName].cspkg`, maar u kunt een andere naam opgeven met behulp van de `/out` optie **CSPack**.</span><span class="sxs-lookup"><span data-stu-id="c6778-199">By default, the package is named `[ServiceDefinitionFileName].cspkg`, but you can specify a different name by using the `/out` option of **CSPack**.</span></span>

<span data-ttu-id="c6778-200">**CSPack** bevindt zich op</span><span class="sxs-lookup"><span data-stu-id="c6778-200">**CSPack** is located at</span></span>  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> <span data-ttu-id="c6778-201">CSPack.exe (op windows) is beschikbaar door het uitvoeren van de **Microsoft Azure-opdrachtprompt** snelkoppeling die is geïnstalleerd met de SDK.</span><span class="sxs-lookup"><span data-stu-id="c6778-201">CSPack.exe (on windows) is available by running the **Microsoft Azure Command Prompt** shortcut that is installed with the SDK.</span></span>  
> 
> <span data-ttu-id="c6778-202">Voer het programma CSPack.exe zelfstandig Zie documentatie over de mogelijke switches en opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c6778-202">Run the CSPack.exe program by itself to see documentation about all the possible switches and commands.</span></span>
> 
> 

<p />

> [!TIP]
> <span data-ttu-id="c6778-203">Uitvoeren van uw cloudservice lokaal in de **Microsoft Azure Compute-Emulator**, gebruiken de **/copyonly** optie.</span><span class="sxs-lookup"><span data-stu-id="c6778-203">Run your cloud service locally in the **Microsoft Azure Compute Emulator**, use the **/copyonly** option.</span></span> <span data-ttu-id="c6778-204">Deze optie kopieert de binaire bestanden voor de toepassing aan de indeling van een directory waaruit ze kunnen worden uitgevoerd in de rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="c6778-204">This option copies the binary files for the application to a directory layout from which they can be run in the compute emulator.</span></span>
> 
> 

### <a name="example-command-to-package-a-cloud-service"></a><span data-ttu-id="c6778-205">Van de voorbeeldopdracht aan het pakket een cloudservice</span><span class="sxs-lookup"><span data-stu-id="c6778-205">Example command to package a cloud service</span></span>
<span data-ttu-id="c6778-206">Het volgende voorbeeld wordt een toepassingspakket met de informatie voor een Webrol.</span><span class="sxs-lookup"><span data-stu-id="c6778-206">The following example creates an application package that contains the information for a web role.</span></span> <span data-ttu-id="c6778-207">De opdracht geeft u het servicedefinitiebestand moet worden gebruikt, de map waar de binaire bestanden kunnen worden gevonden, en de naam van het pakket.</span><span class="sxs-lookup"><span data-stu-id="c6778-207">The command specifies the service definition file to use, the directory where binary files can be found, and the name of the package file.</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

<span data-ttu-id="c6778-208">Als de toepassing zowel een Webrol en een werkrol bevat, worden de volgende opdracht wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="c6778-208">If the application contains both a web role and a worker role, the following command is used:</span></span>

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

<span data-ttu-id="c6778-209">Waar worden de variabelen als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="c6778-209">Where the variables are defined as follows:</span></span>

| <span data-ttu-id="c6778-210">Variabele</span><span class="sxs-lookup"><span data-stu-id="c6778-210">Variable</span></span> | <span data-ttu-id="c6778-211">Waarde</span><span class="sxs-lookup"><span data-stu-id="c6778-211">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c6778-212">\[DirectoryName\]</span><span class="sxs-lookup"><span data-stu-id="c6778-212">\[DirectoryName\]</span></span> |<span data-ttu-id="c6778-213">De submap onder de hoofdmap van het project die het csdef-bestand van de Azure-project bevat.</span><span class="sxs-lookup"><span data-stu-id="c6778-213">The subdirectory under the root project directory that contains the .csdef file of the Azure project.</span></span> |
| <span data-ttu-id="c6778-214">\[ServiceDefinition\]</span><span class="sxs-lookup"><span data-stu-id="c6778-214">\[ServiceDefinition\]</span></span> |<span data-ttu-id="c6778-215">De naam van het servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-215">The name of the service definition file.</span></span> <span data-ttu-id="c6778-216">Standaard is dit bestand ServiceDefinition.csdef naam.</span><span class="sxs-lookup"><span data-stu-id="c6778-216">By default, this file is named ServiceDefinition.csdef.</span></span> |
| <span data-ttu-id="c6778-217">\[OutputFileName\]</span><span class="sxs-lookup"><span data-stu-id="c6778-217">\[OutputFileName\]</span></span> |<span data-ttu-id="c6778-218">De naam van het gegenereerde pakketbestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-218">The name for the generated package file.</span></span> <span data-ttu-id="c6778-219">Dit is normaal gesproken ingesteld op de naam van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="c6778-219">Typically, this is set to the name of the application.</span></span> <span data-ttu-id="c6778-220">Als er geen bestandsnaam is opgegeven, wordt het toepassingspakket gemaakt als \[ApplicationName\].cspkg.</span><span class="sxs-lookup"><span data-stu-id="c6778-220">If no file name is specified, the application package is created as \[ApplicationName\].cspkg.</span></span> |
| <span data-ttu-id="c6778-221">\[Rolnaam\]</span><span class="sxs-lookup"><span data-stu-id="c6778-221">\[RoleName\]</span></span> |<span data-ttu-id="c6778-222">De naam van de rol, zoals gedefinieerd in het servicedefinitiebestand.</span><span class="sxs-lookup"><span data-stu-id="c6778-222">The name of the role as defined in the service definition file.</span></span> |
| <span data-ttu-id="c6778-223">\[RoleBinariesDirectory]</span><span class="sxs-lookup"><span data-stu-id="c6778-223">\[RoleBinariesDirectory]</span></span> |<span data-ttu-id="c6778-224">De locatie van de binaire bestanden voor de rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-224">The location of the binary files for the role.</span></span> |
| <span data-ttu-id="c6778-225">\[VirtualPath\]</span><span class="sxs-lookup"><span data-stu-id="c6778-225">\[VirtualPath\]</span></span> |<span data-ttu-id="c6778-226">De fysieke mappen voor elke virtuele pad dat is gedefinieerd in de sectie Sites van de definitie van de service.</span><span class="sxs-lookup"><span data-stu-id="c6778-226">The physical directories for each virtual path defined in the Sites section of the service definition.</span></span> |
| <span data-ttu-id="c6778-227">\[PhysicalPath\]</span><span class="sxs-lookup"><span data-stu-id="c6778-227">\[PhysicalPath\]</span></span> |<span data-ttu-id="c6778-228">De fysieke mappen van de inhoud voor elke virtuele pad dat is gedefinieerd in het siteknooppunt van de definitie van de service.</span><span class="sxs-lookup"><span data-stu-id="c6778-228">The physical directories of the contents for each virtual path defined in the site node of the service definition.</span></span> |
| <span data-ttu-id="c6778-229">\[RoleAssemblyName\]</span><span class="sxs-lookup"><span data-stu-id="c6778-229">\[RoleAssemblyName\]</span></span> |<span data-ttu-id="c6778-230">De naam van het binaire bestand voor de rol.</span><span class="sxs-lookup"><span data-stu-id="c6778-230">The name of the binary file for the role.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c6778-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c6778-231">Next steps</span></span>
<span data-ttu-id="c6778-232">Ik ben een cloud service-pakket maken en ik wil...</span><span class="sxs-lookup"><span data-stu-id="c6778-232">I'm creating a cloud service package and I want to...</span></span>

* <span data-ttu-id="c6778-233">[Extern bureaublad instellen voor een cloud service-exemplaar][remotedesktop]</span><span class="sxs-lookup"><span data-stu-id="c6778-233">[Setup remote desktop for a cloud service instance][remotedesktop]</span></span>
* <span data-ttu-id="c6778-234">[Een Cloud Service-project implementeert][deploy]</span><span class="sxs-lookup"><span data-stu-id="c6778-234">[Deploy a Cloud Service project][deploy]</span></span>

<span data-ttu-id="c6778-235">Ik gebruik Visual Studio en ik wil...</span><span class="sxs-lookup"><span data-stu-id="c6778-235">I am using Visual Studio and I want to...</span></span>

* <span data-ttu-id="c6778-236">[Maak een nieuwe cloudservice][vs_create]</span><span class="sxs-lookup"><span data-stu-id="c6778-236">[Create a new cloud service][vs_create]</span></span>
* <span data-ttu-id="c6778-237">[Configureren van een bestaande cloudservice][vs_reconfigure]</span><span class="sxs-lookup"><span data-stu-id="c6778-237">[Reconfigure an existing cloud service][vs_reconfigure]</span></span>
* <span data-ttu-id="c6778-238">[Een Cloud Service-project implementeert][vs_deploy]</span><span class="sxs-lookup"><span data-stu-id="c6778-238">[Deploy a Cloud Service project][vs_deploy]</span></span>
* <span data-ttu-id="c6778-239">[Extern bureaublad instellen voor een cloud service-exemplaar][vs_remote]</span><span class="sxs-lookup"><span data-stu-id="c6778-239">[Setup remote desktop for a cloud service instance][vs_remote]</span></span>

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
