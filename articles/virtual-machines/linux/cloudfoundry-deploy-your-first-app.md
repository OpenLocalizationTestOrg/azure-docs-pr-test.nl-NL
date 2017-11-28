---
title: aaaDeploy uw eerste app tooCloud Foundry op Microsoft Azure | Microsoft Docs
description: Een toepassing tooCloud Foundry in Azure implementeren
services: virtual-machines-linux
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 8fa04a58-56ad-4e6c-bef4-d02c80d4b60f
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/14/2017
ms.author: seanmck
ms.openlocfilehash: 878da38f6eabe32a339f02aa0ead811d6e5af9a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-first-app-toocloud-foundry-on-microsoft-azure"></a><span data-ttu-id="7730c-103">Implementeren van uw eerste app tooCloud Foundry op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7730c-103">Deploy your first app tooCloud Foundry on Microsoft Azure</span></span>

<span data-ttu-id="7730c-104">[Foundry cloud](http://cloudfoundry.org) is een platform voor populaire open-source beschikbaar op Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7730c-104">[Cloud Foundry](http://cloudfoundry.org) is a popular open-source application platform available on Microsoft Azure.</span></span> <span data-ttu-id="7730c-105">In dit artikel wordt gedemonstreerd hoe toodeploy en beheren van een toepassing in de Cloud Foundry in een Azure-omgeving.</span><span class="sxs-lookup"><span data-stu-id="7730c-105">In this article, we show how toodeploy and manage an application on Cloud Foundry in an Azure environment.</span></span>

## <a name="create-a-cloud-foundry-environment"></a><span data-ttu-id="7730c-106">Een Cloud Foundry-omgeving maken</span><span class="sxs-lookup"><span data-stu-id="7730c-106">Create a Cloud Foundry environment</span></span>

<span data-ttu-id="7730c-107">Er zijn verschillende opties voor het maken van een Cloud Foundry-omgeving op Azure:</span><span class="sxs-lookup"><span data-stu-id="7730c-107">There are several options for creating a Cloud Foundry environment on Azure:</span></span>

- <span data-ttu-id="7730c-108">Gebruik Hallo [belangrijke Cloud Foundry aanbieding] [ pcf-azuremarketplace] in hello Azure Marketplace toocreate een standaard omgeving die PCF Ops Manager en hello Azure Service Broker.</span><span class="sxs-lookup"><span data-stu-id="7730c-108">Use hello [Pivotal Cloud Foundry offer][pcf-azuremarketplace] in hello Azure Marketplace toocreate a standard environment that includes PCF Ops Manager and hello Azure Service Broker.</span></span> <span data-ttu-id="7730c-109">U vindt [volledige instructies] [ pcf-azuremarketplace-pivotaldocs] bieden voor het implementeren van Hallo marketplace in Hallo belangrijke documentatie.</span><span class="sxs-lookup"><span data-stu-id="7730c-109">You can find [complete instructions][pcf-azuremarketplace-pivotaldocs] for deploying hello marketplace offer in hello Pivotal documentation.</span></span>
- <span data-ttu-id="7730c-110">Maakt een aangepaste omgeving door [belangrijke Cloud Foundry handmatig implementeren][pcf-custom].</span><span class="sxs-lookup"><span data-stu-id="7730c-110">Create a customized environment by [deploying Pivotal Cloud Foundry manually][pcf-custom].</span></span>
- <span data-ttu-id="7730c-111">[Hallo open source Cloud Foundry pakketten rechtstreeks implementeren] [ oss-cf-bosh] door het instellen van een [BOSH](http://bosh.io) directeur, een virtuele machine die Hallo-implementatie van Hallo Cloud Foundry-omgeving coördineert.</span><span class="sxs-lookup"><span data-stu-id="7730c-111">[Deploy hello open-source Cloud Foundry packages directly][oss-cf-bosh] by setting up a [BOSH](http://bosh.io) director, a VM that coordinates hello deployment of hello Cloud Foundry environment.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="7730c-112">Als u PCF vanuit Azure Marketplace hello implementeert, noteer Hallo SYSTEMDOMAINURL en Hallo beheerdersreferenties vereist tooaccess Hallo belangrijke Apps Manager, die beide worden beschreven in de Implementatiehandleiding voor Hallo marketplace.</span><span class="sxs-lookup"><span data-stu-id="7730c-112">If you are deploying PCF from hello Azure Marketplace, make a note of hello SYSTEMDOMAINURL and hello admin credentials required tooaccess hello Pivotal Apps Manager, both of which are described in hello marketplace deployment guide.</span></span> <span data-ttu-id="7730c-113">Ze zijn benodigde toocomplete in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7730c-113">They are needed toocomplete this tutorial.</span></span> <span data-ttu-id="7730c-114">Voor implementaties van marketplace wordt Hallo SYSTEMDOMAINURL Hallo formulier https://system. *IP-adres*. cf.pcfazure.com.</span><span class="sxs-lookup"><span data-stu-id="7730c-114">For marketplace deployments, hello SYSTEMDOMAINURL is in hello form https://system.*ip-address*.cf.pcfazure.com.</span></span>

## <a name="connect-toohello-cloud-controller"></a><span data-ttu-id="7730c-115">Verbinding maken met toohello Cloud-Controller</span><span class="sxs-lookup"><span data-stu-id="7730c-115">Connect toohello Cloud Controller</span></span>

<span data-ttu-id="7730c-116">Hallo Cloud-Controller is Hallo primaire ingang punt tooa Cloud Foundry-omgeving voor het implementeren en beheren van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7730c-116">hello Cloud Controller is hello primary entry point tooa Cloud Foundry environment for deploying and managing applications.</span></span> <span data-ttu-id="7730c-117">Hallo core Cloud Controller API (CCAPI) is een REST-API, maar is toegankelijk via verschillende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="7730c-117">hello core Cloud Controller API (CCAPI) is a REST API, but it is accessible through various tools.</span></span> <span data-ttu-id="7730c-118">In dit geval er interactief mee werken via Hallo [Cloud Foundry CLI][cf-cli].</span><span class="sxs-lookup"><span data-stu-id="7730c-118">In this case, we interact with it through hello [Cloud Foundry CLI][cf-cli].</span></span> <span data-ttu-id="7730c-119">U kunt Hallo CLI installeren op Linux-, Mac OS- of Windows, maar als u liever niet tooinstall helemaal deze beschikbaar is geïnstalleerd in Hallo [Azure Cloud Shell][cloudshell-docs].</span><span class="sxs-lookup"><span data-stu-id="7730c-119">You can install hello CLI on Linux, MacOS, or Windows, but if you'd prefer not tooinstall it at all, it is available pre-installed in hello [Azure Cloud Shell][cloudshell-docs].</span></span>

<span data-ttu-id="7730c-120">toevoegen van toolog, `api` toohello SYSTEMDOMAINURL die u hebt verkregen via Hallo marketplace-implementatie.</span><span class="sxs-lookup"><span data-stu-id="7730c-120">toolog in, prepend `api` toohello SYSTEMDOMAINURL that you obtained from hello marketplace deployment.</span></span> <span data-ttu-id="7730c-121">Aangezien Hallo standaardimplementatie gebruikmaakt van een zelfondertekend certificaat, moet u ook opnemen Hallo `skip-ssl-validation` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="7730c-121">Since hello default deployment uses a self-signed certificate, you should also include hello `skip-ssl-validation` switch.</span></span>

```bash
cf login -a https://api.SYSTEMDOMAINURL --skip-ssl-validation
```

<span data-ttu-id="7730c-122">U bent na vragen aan gebruiker toolog in toohello Cloud-Controller.</span><span class="sxs-lookup"><span data-stu-id="7730c-122">You are prompted toolog in toohello Cloud Controller.</span></span> <span data-ttu-id="7730c-123">Hallo beheerder accountreferenties die u hebt aangeschaft van Hallo marketplace implementatiestappen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7730c-123">Use hello admin account credentials that you acquired from hello marketplace deployment steps.</span></span>

<span data-ttu-id="7730c-124">Cloud Foundry biedt *organisaties* en *spaties* als naamruimten tooisolate Hallo teams en omgevingen binnen een gedeelde implementatie.</span><span class="sxs-lookup"><span data-stu-id="7730c-124">Cloud Foundry provides *orgs* and *spaces* as namespaces tooisolate hello teams and environments within a shared deployment.</span></span> <span data-ttu-id="7730c-125">Hallo PCF marketplace implementatie bevat standaard Hallo *system* org en een set spaties gemaakt toocontain basisonderdelen Hallo zoals Hallo automatisch schalen service en hello Azure service broker.</span><span class="sxs-lookup"><span data-stu-id="7730c-125">hello PCF marketplace deployment includes hello default *system* org and a set of spaces created toocontain hello base components, like hello autoscaling service and hello Azure service broker.</span></span> <span data-ttu-id="7730c-126">Kies nu Hallo *system* ruimte.</span><span class="sxs-lookup"><span data-stu-id="7730c-126">For now, choose hello *system* space.</span></span>


## <a name="create-an-org-and-space"></a><span data-ttu-id="7730c-127">Een organisatie en de ruimte maken</span><span class="sxs-lookup"><span data-stu-id="7730c-127">Create an org and space</span></span>

<span data-ttu-id="7730c-128">Als u typt `cf apps`, ziet u een set systeemtoepassingen die zijn geïmplementeerd in de ruimte die op Hallo binnen Hallo system org.</span><span class="sxs-lookup"><span data-stu-id="7730c-128">If you type `cf apps`, you see a set of system applications that have been deployed in hello system space within hello system org.</span></span> 

<span data-ttu-id="7730c-129">U dient te houden met Hallo *system* org gereserveerd voor systeemtoepassingen, dus maak een organisatie en de ruimte toohouse onze voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="7730c-129">You should keep hello *system* org reserved for system applications, so create an org and space toohouse our sample application.</span></span>

```bash
cf create-org myorg
cf create-space dev -o myorg
```

<span data-ttu-id="7730c-130">Hallo doel opdracht tooswitch toohello nieuwe org en ruimte gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7730c-130">Use hello target command tooswitch toohello new org and space:</span></span>

```bash
cf target -o testorg -s dev
```

<span data-ttu-id="7730c-131">Nu, wanneer u een toepassing implementeert, deze automatisch is gemaakt in de nieuwe org Hallo en ruimte.</span><span class="sxs-lookup"><span data-stu-id="7730c-131">Now, when you deploy an application, it is automatically created in hello new org and space.</span></span> <span data-ttu-id="7730c-132">tooconfirm die er zijn momenteel geen apps in Hallo nieuwe org per ruimte, typ `cf apps` opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7730c-132">tooconfirm that there are currently no apps in hello new org/space, type `cf apps` again.</span></span>

> [!NOTE] 
> <span data-ttu-id="7730c-133">Zie voor meer informatie over organisaties en spaties en hoe ze kunnen worden gebruikt voor op rollen gebaseerde toegangsbeheer (RBAC) Hallo [Cloud Foundry documentatie][cf-orgs-spaces-docs].</span><span class="sxs-lookup"><span data-stu-id="7730c-133">For more information about orgs and spaces and how they can be used for role-based access control (RBAC), see hello [Cloud Foundry documentation][cf-orgs-spaces-docs].</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="7730c-134">Een app implementeren</span><span class="sxs-lookup"><span data-stu-id="7730c-134">Deploy an application</span></span>

<span data-ttu-id="7730c-135">We gebruiken een voorbeeldtoepassing Cloud Foundry Hallo Spring Cloud, die is geschreven in Java en op basis van Hallo aangeroepen [Spring Framework](http://spring.io) en [Spring Boot](http://projects.spring.io/spring-boot/).</span><span class="sxs-lookup"><span data-stu-id="7730c-135">Let's use a sample Cloud Foundry application called Hello Spring Cloud, which is written in Java and based on hello [Spring Framework](http://spring.io) and [Spring Boot](http://projects.spring.io/spring-boot/).</span></span>

### <a name="clone-hello-hello-spring-cloud-repository"></a><span data-ttu-id="7730c-136">Hallo Hallo Spring Cloud opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="7730c-136">Clone hello Hello Spring Cloud repository</span></span>

<span data-ttu-id="7730c-137">Hallo Hallo Spring Cloud voorbeeldtoepassing is beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="7730c-137">hello Hello Spring Cloud sample application is available on GitHub.</span></span> <span data-ttu-id="7730c-138">Kloon tooyour omgeving en naar de nieuwe map Hallo wijzigen:</span><span class="sxs-lookup"><span data-stu-id="7730c-138">Clone it tooyour environment and change into hello new directory:</span></span>

```bash
git clone https://github.com/cloudfoundry-samples/hello-spring-cloud
cd hello-spring-cloud
```

### <a name="build-hello-application"></a><span data-ttu-id="7730c-139">Hallo-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="7730c-139">Build hello application</span></span>

<span data-ttu-id="7730c-140">Build Hallo app met behulp [Apache Maven](http://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="7730c-140">Build hello app using [Apache Maven](http://maven.apache.org).</span></span>

```bash
mvn clean package
```

### <a name="deploy-hello-application-with-cf-push"></a><span data-ttu-id="7730c-141">Implementeer de toepassing hello met cf push</span><span class="sxs-lookup"><span data-stu-id="7730c-141">Deploy hello application with cf push</span></span>

<span data-ttu-id="7730c-142">U kunt de meeste toepassingen tooCloud Foundry implementeren met behulp van Hallo `push` opdracht:</span><span class="sxs-lookup"><span data-stu-id="7730c-142">You can deploy most applications tooCloud Foundry using hello `push` command:</span></span>

```bash
cf push
```

<span data-ttu-id="7730c-143">Wanneer u *push* een toepassing, Cloud Foundry detecteert Hallo type toepassing (in dit geval een Java-app) en de afhankelijkheden ervan (in dit geval Hallo Spring framework) identificeert.</span><span class="sxs-lookup"><span data-stu-id="7730c-143">When you *push* an application, Cloud Foundry detects hello type of application (in this case, a Java app) and identifies its dependencies (in this case, hello Spring framework).</span></span> <span data-ttu-id="7730c-144">Vervolgens pakketten alles toorun uw code vereist in de container installatiekopie van een zelfstandige, ook wel een *droplet*.</span><span class="sxs-lookup"><span data-stu-id="7730c-144">It then packages everything required toorun your code into a standalone container image, known as a *droplet*.</span></span> <span data-ttu-id="7730c-145">Ten slotte Cloud Foundry planningen Hallo van toepassing op een van de beschikbare machines Hallo in uw omgeving en maakt u een URL waarop u bereiken kan, die beschikbaar is in het Hallo-uitvoer van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="7730c-145">Finally, Cloud Foundry schedules hello application on one of hello available machines in your environment and creates a URL where you can reach it, which is available in hello output of hello command.</span></span>

![Uitvoer van cf push-opdracht][cf-push-output]

<span data-ttu-id="7730c-147">toosee Hallo Hallo-spring-cloud-toepassing open Hallo opgegeven URL in uw browser:</span><span class="sxs-lookup"><span data-stu-id="7730c-147">toosee hello hello-spring-cloud application, open hello provided URL in your browser:</span></span>

![Standaardgebruikersinterface voor Hallo Spring Cloud][hello-spring-cloud-basic]

> [!NOTE] 
> <span data-ttu-id="7730c-149">meer informatie over wat er tijdens gebeurt toolearn `cf push`, Zie [hoe toepassingen worden voorbereid] [ cf-push-docs] in Hallo Cloud Foundry-documentatie.</span><span class="sxs-lookup"><span data-stu-id="7730c-149">toolearn more about what happens during `cf push`, see [How Applications Are Staged][cf-push-docs] in hello Cloud Foundry documentation.</span></span>

## <a name="view-application-logs"></a><span data-ttu-id="7730c-150">Logboeken van de toepassing bekijken</span><span class="sxs-lookup"><span data-stu-id="7730c-150">View application logs</span></span>

<span data-ttu-id="7730c-151">U kunt Hallo Cloud Foundry CLI tooview Logboeken kunt gebruiken voor een toepassing met de naam:</span><span class="sxs-lookup"><span data-stu-id="7730c-151">You can use hello Cloud Foundry CLI tooview logs for an application by its name:</span></span>

```bash
cf logs hello-spring-cloud
```

<span data-ttu-id="7730c-152">Standaard Hallo opdracht gebruikt Logboeken *tail*, waarmee nieuwe logboeken wordt weergegeven als ze zijn geschreven.</span><span class="sxs-lookup"><span data-stu-id="7730c-152">By default, hello logs command uses *tail*, which shows new logs as they are written.</span></span> <span data-ttu-id="7730c-153">Hallo Hallo-spring-cloud-app in de browser Hallo toosee nieuwe logboeken worden weergegeven, worden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="7730c-153">toosee new logs appear, refresh hello hello-spring-cloud app in hello browser.</span></span>

<span data-ttu-id="7730c-154">tooview logboeken die al zijn geschreven, voeg Hallo `recent` switch:</span><span class="sxs-lookup"><span data-stu-id="7730c-154">tooview logs that have already been written, add hello `recent` switch:</span></span>

```bash
cf logs --recent hello-spring-cloud
```

## <a name="scale-hello-application"></a><span data-ttu-id="7730c-155">Hallo-toepassing schalen</span><span class="sxs-lookup"><span data-stu-id="7730c-155">Scale hello application</span></span>

<span data-ttu-id="7730c-156">Standaard `cf push` slechts één exemplaar van uw toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="7730c-156">By default, `cf push` only creates a single instance of your application.</span></span> <span data-ttu-id="7730c-157">tooensure hoge beschikbaarheid en inschakelen scale-out voor een hogere doorvoer, wilt u in het algemeen toorun meer dan één exemplaar van uw toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7730c-157">tooensure high availability and enable scale out for higher throughput, you generally want toorun more than one instance of your applications.</span></span> <span data-ttu-id="7730c-158">Kunt u eenvoudig uitschalen reeds geïmplementeerde toepassingen met behulp van Hallo `scale` opdracht:</span><span class="sxs-lookup"><span data-stu-id="7730c-158">You can easily scale out already deployed applications using hello `scale` command:</span></span>

```bash
cf scale -i 2 hello-spring-cloud
```

<span data-ttu-id="7730c-159">Actieve Hallo `cf app` opdracht bij de toepassing hello toont Cloud Foundry maken van een ander exemplaar van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="7730c-159">Running hello `cf app` command on hello application shows that Cloud Foundry is creating another instance of hello application.</span></span> <span data-ttu-id="7730c-160">Eenmaal Hallo toepassing is gestart, worden de taakverdeling verkeer tooit Cloud Foundry automatisch gestart.</span><span class="sxs-lookup"><span data-stu-id="7730c-160">Once hello application has started, Cloud Foundry automatically starts load balancing traffic tooit.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7730c-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7730c-161">Next steps</span></span>

- <span data-ttu-id="7730c-162">[Lees Hallo Cloud Foundry-documentatie][cloudfoundry-docs]</span><span class="sxs-lookup"><span data-stu-id="7730c-162">[Read hello Cloud Foundry documentation][cloudfoundry-docs]</span></span>
- <span data-ttu-id="7730c-163">[Hallo Visual Studio Team Services-invoegtoepassing voor Cloud Foundry instellen][vsts-plugin]</span><span class="sxs-lookup"><span data-stu-id="7730c-163">[Set up hello Visual Studio Team Services plugin for Cloud Foundry][vsts-plugin]</span></span>
- <span data-ttu-id="7730c-164">[Hallo Microsoft Log Analytics pijp configureren voor Cloud Foundry][loganalytics-nozzle]</span><span class="sxs-lookup"><span data-stu-id="7730c-164">[Configure hello Microsoft Log Analytics Nozzle for Cloud Foundry][loganalytics-nozzle]</span></span>

<!-- LINKS -->

[pcf-azuremarketplace]: https://azuremarketplace.microsoft.com/marketplace/apps/pivotal.pivotal-cloud-foundry
[pcf-custom]: https://docs.pivotal.io/pivotalcf/1-10/customizing/azure.html
[oss-cf-bosh]: https://github.com/cloudfoundry-incubator/bosh-azure-cpi-release/tree/master/docs
[pcf-azuremarketplace-pivotaldocs]: https://docs.pivotal.io/pivotalcf/customizing/pcf_azure.html
[cf-cli]: https://github.com/cloudfoundry/cli
[cloudshell-docs]: https://docs.microsoft.com/azure/cloud-shell/overview
[cf-orgs-spaces-docs]: https://docs.cloudfoundry.org/concepts/roles.html
[spring-boot]: https://projects.spring.io/spring-boot/
[spring-framework]: http://spring.io
[cf-push-docs]: https://docs.cloudfoundry.org/concepts/how-applications-are-staged.html
[cloudfoundry-docs]: https://docs.cloudfoundry.org
[vsts-plugin]: https://github.com/Microsoft/vsts-cloudfoundry
[loganalytics-nozzle]: https://github.com/Azure/oms-log-analytics-firehose-nozzle

<!-- IMAGES -->
[cf-push-output]: ./media/cloudfoundry-deploy-your-first-app/cf-push-output.png
[hello-spring-cloud-basic]: ./media/cloudfoundry-deploy-your-first-app/hello-spring-cloud-basic.png