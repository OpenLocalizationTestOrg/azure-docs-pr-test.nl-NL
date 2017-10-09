---
title: de slag met Azure Service Fabric en Azure CLI 2.0 aaaGet
description: Meer informatie over hoe toouse hello Azure Service Fabric-module in versie 2.0 van Azure CLI-opdrachten. Meer informatie over hoe tooconnect tooa cluster, en hoe toomanage toepassingen.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ddbd0ef503dd3fff61494cc2cfa7c9a2e8d0a9a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="65468-104">Azure Service Fabric en Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="65468-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="65468-105">Hello Azure-opdrachtregelprogramma (Azure CLI) versie 2.0 bevat opdrachten toohelp beheren van Azure Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="65468-105">hello Azure command-line tool (Azure CLI) version 2.0 includes commands toohelp you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="65468-106">Meer informatie over hoe tooget de slag met Azure CLI en Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="65468-106">Learn how tooget started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="65468-107">Azure CLI 2.0 installeren</span><span class="sxs-lookup"><span data-stu-id="65468-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="65468-108">U kunt Azure CLI 2.0 opdrachten toointeract met gebruiken en beheren van Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="65468-108">You can use Azure CLI 2.0 commands toointeract with and manage Service Fabric clusters.</span></span> <span data-ttu-id="65468-109">tooget hello meest recente versie van Azure CLI, volg Hallo [standaard Azure CLI 2.0-installatieproces](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="65468-109">tooget hello latest version of Azure CLI, follow hello [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="65468-110">Zie voor meer informatie, Hallo [overzicht van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65468-110">For more information, see hello [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="65468-111">De syntaxis van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="65468-111">Azure CLI syntax</span></span>

<span data-ttu-id="65468-112">Alle Service Fabric-opdrachten worden voorafgegaan door `az sf` in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="65468-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="65468-113">Gebruik voor algemene informatie over Hallo opdrachten kunt u `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="65468-113">For general information about hello commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="65468-114">Gebruik `az sf <command> -h` voor hulp bij één opdracht.</span><span class="sxs-lookup"><span data-stu-id="65468-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="65468-115">Service Fabric-opdrachten in de Azure CLI volgen dit naamgevingspatroon:</span><span class="sxs-lookup"><span data-stu-id="65468-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="65468-116">`<object>`Hallo-doel voor `<action>`.</span><span class="sxs-lookup"><span data-stu-id="65468-116">`<object>` is hello target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="65468-117">Een cluster selecteren</span><span class="sxs-lookup"><span data-stu-id="65468-117">Select a cluster</span></span>

<span data-ttu-id="65468-118">Voordat u bewerkingen uitvoert, moet u een cluster tooconnect te selecteren.</span><span class="sxs-lookup"><span data-stu-id="65468-118">Before you perform any operations, you must select a cluster tooconnect to.</span></span> <span data-ttu-id="65468-119">Zie voor een voorbeeld Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="65468-119">For an example, see hello following code.</span></span> <span data-ttu-id="65468-120">Hallo code verbindt tooan onbeveiligde cluster.</span><span class="sxs-lookup"><span data-stu-id="65468-120">hello code connects tooan unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="65468-121">Gebruik geen niet-beveiligde Service Fabric-clusters in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="65468-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="65468-122">Hallo clustereindpunt moet worden voorafgegaan door `http` of `https`.</span><span class="sxs-lookup"><span data-stu-id="65468-122">hello cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="65468-123">Hallo-poort voor Hallo http-gateway moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="65468-123">It must include hello port for hello HTTP gateway.</span></span> <span data-ttu-id="65468-124">Hallo-poort en adres zijn hetzelfde zijn als de URL van de Service Fabric Explorer Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="65468-124">hello port and address are hello same as hello Service Fabric Explorer URL.</span></span>

<span data-ttu-id="65468-125">Voor clusters die zijn beveiligd met een certificaat, kunt u niet-versleutelde .pem-bestanden of .crt- en .key-bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65468-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="65468-126">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="65468-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="65468-127">Zie voor meer informatie [Connect tooa beveiligde Azure Service Fabric-cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="65468-127">For more information, see [Connect tooa secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="65468-128">Hallo `select` opdracht niet reageren op alle aanvragen voordat deze wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="65468-128">hello `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="65468-129">tooverify u een cluster correct hebt opgegeven een opdracht zoals gebruiken `az sf cluster health`.</span><span class="sxs-lookup"><span data-stu-id="65468-129">tooverify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="65468-130">Controleer of Hallo opdracht retourneert niet eventuele fouten.</span><span class="sxs-lookup"><span data-stu-id="65468-130">Verify that hello command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="65468-131">Basisbewerkingen</span><span class="sxs-lookup"><span data-stu-id="65468-131">Basic operations</span></span>

<span data-ttu-id="65468-132">De gegevens van een clusterverbinding blijven behouden tussen meerdere Azure CLI-sessies.</span><span class="sxs-lookup"><span data-stu-id="65468-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="65468-133">Nadat u een Service Fabric-cluster selecteert, kunt u een Service Fabric-opdracht kunt uitvoeren op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="65468-133">After you select a Service Fabric cluster, you can run any Service Fabric command on hello cluster.</span></span>

<span data-ttu-id="65468-134">Bijvoorbeeld tooget Hallo status voor Service Fabric-cluster, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="65468-134">For example, tooget hello Service Fabric cluster health state, use hello following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="65468-135">Hallo opdracht resulteert in Hallo volgende uitvoer (ervan uitgaande dat JSON-uitvoer is opgegeven in de configuratie van hello Azure CLI):</span><span class="sxs-lookup"><span data-stu-id="65468-135">hello command results in hello following output (assuming that JSON output is specified in hello Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="65468-136">Tips en probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="65468-136">Tips and troubleshooting</span></span>

<span data-ttu-id="65468-137">Mogelijk vindt u nuttige informatie te volgen als u problemen ondervindt tijdens het gebruik van Service Fabric-opdrachten in de Azure CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="65468-137">You might find hello following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-toopem-format"></a><span data-ttu-id="65468-138">Een certificaat van PFX tooPEM-indeling converteren</span><span class="sxs-lookup"><span data-stu-id="65468-138">Convert a certificate from PFX tooPEM format</span></span>

<span data-ttu-id="65468-139">De Azure CLI ondersteunt clientcertificaten als PEM-bestanden (extensie .pem).</span><span class="sxs-lookup"><span data-stu-id="65468-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="65468-140">Als u PFX-bestanden van Windows gebruikt, moet u deze certificaten tooPEM-indeling converteren.</span><span class="sxs-lookup"><span data-stu-id="65468-140">If you use PFX files from Windows, you must convert those certificates tooPEM format.</span></span> <span data-ttu-id="65468-141">tooconvert een PFX-bestand tooa PEM-bestand Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="65468-141">tooconvert a PFX file tooa PEM file, use hello following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="65468-142">Zie voor meer informatie, Hallo [OpenSSL documentatie](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="65468-142">For more information, see hello [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="65468-143">Verbindingsproblemen</span><span class="sxs-lookup"><span data-stu-id="65468-143">Connection issues</span></span>

<span data-ttu-id="65468-144">Bepaalde bewerkingen mogelijk Hallo volgende bericht te genereren:</span><span class="sxs-lookup"><span data-stu-id="65468-144">Some operations might generate hello following message:</span></span>

`Failed tooestablish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="65468-145">Controleer of dat deze Hallo opgegeven clustereindpunt is beschikbaar is en luistert.</span><span class="sxs-lookup"><span data-stu-id="65468-145">Verify that hello specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="65468-146">Controleer ook of die Hallo Service Fabric Explorer UI is beschikbaar op die als host en poort.</span><span class="sxs-lookup"><span data-stu-id="65468-146">Also, verify that hello Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="65468-147">tooupdate hello eindpunt, gebruik `az sf cluster select`.</span><span class="sxs-lookup"><span data-stu-id="65468-147">tooupdate hello endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="65468-148">Gedetailleerde logboeken</span><span class="sxs-lookup"><span data-stu-id="65468-148">Detailed logs</span></span>

<span data-ttu-id="65468-149">Gedetailleerde logboeken zijn vaak nuttig zijn wanneer u fouten opspoort of een probleem meldt.</span><span class="sxs-lookup"><span data-stu-id="65468-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="65468-150">Azure CLI biedt een algemene `--debug` vlag die wordt verhoogd Hallo uitgebreidheid van logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="65468-150">Azure CLI offers a global `--debug` flag that increases hello verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="65468-151">Syntaxis van Help-opdracht</span><span class="sxs-lookup"><span data-stu-id="65468-151">Command help and syntax</span></span>

<span data-ttu-id="65468-152">Service Fabric-opdrachten Volg Hallo dezelfde conventies als Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="65468-152">Service Fabric commands follow hello same conventions as Azure CLI.</span></span> <span data-ttu-id="65468-153">Gebruik voor hulp bij een bepaalde opdracht of een groep opdrachten, Hallo `-h` vlag:</span><span class="sxs-lookup"><span data-stu-id="65468-153">For help with a specific command or a group of commands, use hello `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="65468-154">Hier volgt nog een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="65468-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
