---
title: aaaGet de slag met Azure Service Fabric CLI (sfctl)
description: Meer informatie over hoe toouse hello Azure Service Fabric CLI. Meer informatie over hoe tooconnect tooa cluster, en hoe toomanage toepassingen.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 08/22/2017
ms.author: edwardsa
ms.openlocfilehash: f76e8ff65bb38dfb63791da0a23e19b93b337f6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-command-line"></a><span data-ttu-id="44607-104">Azure Service Fabric-opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="44607-104">Azure Service Fabric command line</span></span>

<span data-ttu-id="44607-105">Hello Azure Service Fabric CLI (sfctl) is een opdrachtregelprogramma voor interactie en beheren van Azure Service Fabric-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="44607-105">hello Azure Service Fabric CLI (sfctl) is a command-line utility for interacting and managing Azure Service Fabric entities.</span></span> <span data-ttu-id="44607-106">Sfctl kan worden gebruikt met Windows- of Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="44607-106">Sfctl can be used with either Windows or Linux clusters.</span></span> <span data-ttu-id="44607-107">Sfctl kan worden uitgevoerd op elk platform dat ondersteuning biedt voor python.</span><span class="sxs-lookup"><span data-stu-id="44607-107">Sfctl runs on any platform where python is supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44607-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="44607-108">Prerequisites</span></span>

<span data-ttu-id="44607-109">Eerdere tooinstallation Zorg ervoor dat uw omgeving heeft python en via pip geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="44607-109">Prior tooinstallation, make sure your environment has both python and pip installed.</span></span> <span data-ttu-id="44607-110">Voor meer informatie, bekijk Hallo [Quick Start-documentatie pip](https://pip.pypa.io/en/latest/quickstart/), en officiële [python installeren documentatie](https://wiki.python.org/moin/BeginnersGuide/Download).</span><span class="sxs-lookup"><span data-stu-id="44607-110">For more information, take a look at hello [pip quickstart documentation](https://pip.pypa.io/en/latest/quickstart/), and official [python install documentation](https://wiki.python.org/moin/BeginnersGuide/Download).</span></span>

<span data-ttu-id="44607-111">Beide python 2.7 en 3.6 worden wel ondersteund, is het raadzaam toouse python 3.6.</span><span class="sxs-lookup"><span data-stu-id="44607-111">While both python 2.7 and 3.6 are supported, it is recommended toouse python 3.6.</span></span>

## <a name="install"></a><span data-ttu-id="44607-112">Installeren</span><span class="sxs-lookup"><span data-stu-id="44607-112">Install</span></span>

<span data-ttu-id="44607-113">Hello Azure Service Fabric CLI (sfctl) wordt geleverd als een python-pakket.</span><span class="sxs-lookup"><span data-stu-id="44607-113">hello Azure Service Fabric CLI (sfctl) is packaged as a python package.</span></span> <span data-ttu-id="44607-114">tooinstall hello meest recente versie uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="44607-114">tooinstall hello latest version run:</span></span>

```bash
pip install sfctl
```

<span data-ttu-id="44607-115">Na de installatie voert `sfctl -h` tooget informatie over beschikbare opdrachten.</span><span class="sxs-lookup"><span data-stu-id="44607-115">After installation, run `sfctl -h` tooget information about available commands.</span></span>

## <a name="cli-syntax"></a><span data-ttu-id="44607-116">De syntaxis van de CLI</span><span class="sxs-lookup"><span data-stu-id="44607-116">CLI syntax</span></span>

<span data-ttu-id="44607-117">Opdrachten worden altijd voorafgegaan door `sfctl`.</span><span class="sxs-lookup"><span data-stu-id="44607-117">Commands are prefixed always with `sfctl`.</span></span> <span data-ttu-id="44607-118">Voor algemene informatie over alle opdrachten die u kunt gebruiken, gebruikt u `sfctl -h`.</span><span class="sxs-lookup"><span data-stu-id="44607-118">For general information about all commands you can use, use `sfctl -h`.</span></span> <span data-ttu-id="44607-119">Gebruik `sfctl <command> -h` voor hulp bij één opdracht.</span><span class="sxs-lookup"><span data-stu-id="44607-119">For help with a single command, use `sfctl <command> -h`.</span></span>

<span data-ttu-id="44607-120">Opdrachten Volg een herhaalbare-structuur met doel Hallo Hallo opdracht voorgaande Hallo-term of actie:</span><span class="sxs-lookup"><span data-stu-id="44607-120">Commands follow a repeatable structure, with hello target of hello command preceding hello verb or action:</span></span>

```azurecli
sfctl <object> <action>
```

<span data-ttu-id="44607-121">In dit voorbeeld `<object>` is Hallo doel voor `<action>`.</span><span class="sxs-lookup"><span data-stu-id="44607-121">In this example, `<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="44607-122">Een cluster selecteren</span><span class="sxs-lookup"><span data-stu-id="44607-122">Select a cluster</span></span>

<span data-ttu-id="44607-123">Voordat u bewerkingen uitvoert, moet u een cluster tooconnect te selecteren.</span><span class="sxs-lookup"><span data-stu-id="44607-123">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="44607-124">Bijvoorbeeld Hallo na tooselect uitvoeren en toohello cluster verbinding met de naam van de Hallo `testcluster.com`.</span><span class="sxs-lookup"><span data-stu-id="44607-124">For example, run hello following tooselect and connect toohello cluster with hello name `testcluster.com`.</span></span>

> [!WARNING]
> <span data-ttu-id="44607-125">Gebruik geen niet-beveiligde Service Fabric-clusters in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="44607-125">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
sfctl cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="44607-126">Hallo clustereindpunt moet worden voorafgegaan door `http` of `https`.</span><span class="sxs-lookup"><span data-stu-id="44607-126">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="44607-127">Hallo-poort voor Hallo http-gateway moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="44607-127">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="44607-128">Hallo-poort en adres zijn hetzelfde zijn als de URL van de Service Fabric Explorer Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44607-128">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="44607-129">Voor clusters die zijn beveiligd met een certificaat, kunt u een met PEM gecodeerd certificaat opgeven.</span><span class="sxs-lookup"><span data-stu-id="44607-129">For clusters that are secured with a certificate, you can specify a PEM encoded certificate.</span></span> <span data-ttu-id="44607-130">Hallo-certificaat kan worden opgegeven als een enkel bestand of het certificaat en de sleutelpaar.</span><span class="sxs-lookup"><span data-stu-id="44607-130">hello certificate can be specified as a single file or cert and key pair.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="44607-131">Zie voor meer informatie [Connect tooa beveiligde Azure Service Fabric-cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="44607-131">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="basic-operations"></a><span data-ttu-id="44607-132">Basisbewerkingen</span><span class="sxs-lookup"><span data-stu-id="44607-132">Basic operations</span></span>

<span data-ttu-id="44607-133">De gegevens van een clusterverbinding blijven behouden tussen meerdere sfctl-sessies.</span><span class="sxs-lookup"><span data-stu-id="44607-133">Cluster connection information persists across multiple sfctl sessions.</span></span> <span data-ttu-id="44607-134">Nadat u een Service Fabric-cluster selecteert, kunt u een Service Fabric-opdracht kunt uitvoeren op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="44607-134">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="44607-135">Bijvoorbeeld tooget Hallo status voor Service Fabric-cluster, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="44607-135">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
sfctl cluster health
```

<span data-ttu-id="44607-136">Hallo opdracht resulteert in Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="44607-136">hello command results in hello following output:</span></span>

```json
{
  "aggregatedHealthState": "Ok",
  "applicationHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "name": "fabric:/System"
    }
  ],
  "healthEvents": [],
  "nodeHealthStates": [
    {
      "aggregatedHealthState": "Ok",
      "id": {
        "id": "66aa824a642124089ee474b398d06a57"
      },
      "name": "_Test_0"
    }
  ],
  "unhealthyEvaluations": []
}
```

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="44607-137">Tips en probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="44607-137">Tips and troubleshooting</span></span>

<span data-ttu-id="44607-138">Enkele suggesties en tips voor het oplossen van veelvoorkomende problemen.</span><span class="sxs-lookup"><span data-stu-id="44607-138">Some suggestions and tips for solving common issues.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="44607-139">Een certificaat van PFX tooPEM-indeling converteren</span><span class="sxs-lookup"><span data-stu-id="44607-139">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="44607-140">Hallo Service Fabric CLI ondersteunt certificaten vanaf de client als PEM (.pem extensie)-bestanden.</span><span class="sxs-lookup"><span data-stu-id="44607-140">hello Service Fabric CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="44607-141">Als u PFX-bestanden van Windows gebruikt, moet u deze certificaten tooPEM-indeling converteren.</span><span class="sxs-lookup"><span data-stu-id="44607-141">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="44607-142">tooconvert een PFX-bestand tooa PEM-bestand de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="44607-142">tooconvert a PFX file tooa PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="44607-143">Zie voor meer informatie, Hallo [OpenSSL documentatie](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="44607-143">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="44607-144">Verbindingsproblemen</span><span class="sxs-lookup"><span data-stu-id="44607-144">Connection issues</span></span>

<span data-ttu-id="44607-145">Bepaalde bewerkingen mogelijk Hallo volgende bericht te genereren:</span><span class="sxs-lookup"><span data-stu-id="44607-145">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="44607-146">Controleer of dat deze Hallo opgegeven clustereindpunt is beschikbaar is en luistert.</span><span class="sxs-lookup"><span data-stu-id="44607-146">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="44607-147">Controleer ook of die Hallo Service Fabric Explorer UI is beschikbaar op die als host en poort.</span><span class="sxs-lookup"><span data-stu-id="44607-147">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="44607-148">tooupdate hello eindpunt, gebruik `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="44607-148">tooupdate hello endpoint, use `sfctl cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="44607-149">Gedetailleerde logboeken</span><span class="sxs-lookup"><span data-stu-id="44607-149">Detailed logs</span></span>

<span data-ttu-id="44607-150">Gedetailleerde logboeken zijn vaak nuttig zijn wanneer u fouten opspoort of een probleem meldt.</span><span class="sxs-lookup"><span data-stu-id="44607-150">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="44607-151">Er is een globale `--debug` vlag die wordt verhoogd Hallo uitgebreidheid van logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="44607-151">There is a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="44607-152">Syntaxis van Help-opdracht</span><span class="sxs-lookup"><span data-stu-id="44607-152">Command help and syntax</span></span>

<span data-ttu-id="44607-153">Gebruik voor hulp bij een bepaalde opdracht of een groep opdrachten, Hallo `-h` vlag:</span><span class="sxs-lookup"><span data-stu-id="44607-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
sfctl application -h
```

<span data-ttu-id="44607-154">Nog een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="44607-154">Another example:</span></span>

```azurecli
sfctl application create -h
```

## <a name="next-steps"></a><span data-ttu-id="44607-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44607-155">Next steps</span></span>

* [<span data-ttu-id="44607-156">Implementeer een toepassing met hello Azure Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="44607-156">Deploy an application with hello Azure Service Fabric CLI</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="44607-157">Aan de slag met Service Fabric in Linux</span><span class="sxs-lookup"><span data-stu-id="44607-157">Get started with Service Fabric on Linux</span></span>](service-fabric-get-started-linux.md)
