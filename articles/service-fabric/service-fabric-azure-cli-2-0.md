---
title: Aan de slag met Azure Service Fabric en Azure CLI 2.0
description: Informatie over het gebruik van de Azure Service Fabric-opdrachtenmodule in Azure CLI versie 2.0. Informatie over verbinding maken met een cluster en het beheren van toepassingen.
services: service-fabric
author: samedder
manager: timlt
ms.service: service-fabric
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: edwardsa
ms.openlocfilehash: ee3302b984ca2f5509755dc17b0a5fd06ace0afe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-service-fabric-and-azure-cli-20"></a><span data-ttu-id="12586-104">Azure Service Fabric en Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="12586-104">Azure Service Fabric and Azure CLI 2.0</span></span>

<span data-ttu-id="12586-105">Het Azure-opdrachtregelprogramma (Azure CLI) versie 2.0 bevat opdrachten voor het beheren van Azure Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="12586-105">The Azure command-line tool (Azure CLI) version 2.0 includes commands to help you manage Azure Service Fabric clusters.</span></span> <span data-ttu-id="12586-106">Lees hoe u aan de slag kunt gaan met Azure Service Fabric en Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="12586-106">Learn how to get started with Azure CLI and Service Fabric.</span></span>

## <a name="install-azure-cli-20"></a><span data-ttu-id="12586-107">Azure CLI 2.0 installeren</span><span class="sxs-lookup"><span data-stu-id="12586-107">Install Azure CLI 2.0</span></span>

<span data-ttu-id="12586-108">U kunt Azure CLI 2.0-opdrachten gebruiken voor het beheren en manipuleren van Service Fabric-clusters.</span><span class="sxs-lookup"><span data-stu-id="12586-108">You can use Azure CLI 2.0 commands to interact with and manage Service Fabric clusters.</span></span> <span data-ttu-id="12586-109">Volg voor de nieuwste versie van Azure CLI het [standaardinstallatieproces van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="12586-109">To get the latest version of Azure CLI, follow the [Azure CLI 2.0 standard installation process](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="12586-110">Zie [Overzicht van Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/overview) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="12586-110">For more information, see the [Azure CLI 2.0 overview](https://docs.microsoft.com/en-us/cli/azure/overview).</span></span>

## <a name="azure-cli-syntax"></a><span data-ttu-id="12586-111">De syntaxis van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="12586-111">Azure CLI syntax</span></span>

<span data-ttu-id="12586-112">Alle Service Fabric-opdrachten worden voorafgegaan door `az sf` in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="12586-112">In Azure CLI, all Service Fabric commands are prefixed with `az sf`.</span></span> <span data-ttu-id="12586-113">Voor algemene informatie over de opdrachten die u kunt gebruiken, gebruikt u `az sf -h`.</span><span class="sxs-lookup"><span data-stu-id="12586-113">For general information about the commands you can use, use `az sf -h`.</span></span> <span data-ttu-id="12586-114">Gebruik `az sf <command> -h` voor hulp bij één opdracht.</span><span class="sxs-lookup"><span data-stu-id="12586-114">For help with a single command, use `az sf <command> -h`.</span></span>

<span data-ttu-id="12586-115">Service Fabric-opdrachten in de Azure CLI volgen dit naamgevingspatroon:</span><span class="sxs-lookup"><span data-stu-id="12586-115">Service Fabric commands in Azure CLI follow this naming pattern:</span></span>

```azurecli
az sf <object> <action>
```

<span data-ttu-id="12586-116">`<object>` is het doel voor `<action>`.</span><span class="sxs-lookup"><span data-stu-id="12586-116">`<object>` is the target for `<action>`.</span></span>

## <a name="select-a-cluster"></a><span data-ttu-id="12586-117">Een cluster selecteren</span><span class="sxs-lookup"><span data-stu-id="12586-117">Select a cluster</span></span>

<span data-ttu-id="12586-118">U kunt pas bewerkingen uitvoeren nadat u een cluster hebt geselecteerd waarmee u verbinding wilt maken.</span><span class="sxs-lookup"><span data-stu-id="12586-118">Before you perform any operations, you must select a cluster to connect to.</span></span> <span data-ttu-id="12586-119">Zie de volgende code voor een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="12586-119">For an example, see the following code.</span></span> <span data-ttu-id="12586-120">De code maakt verbinding met een niet-beveiligd cluster.</span><span class="sxs-lookup"><span data-stu-id="12586-120">The code connects to an unsecured cluster.</span></span>

> [!WARNING]
> <span data-ttu-id="12586-121">Gebruik geen niet-beveiligde Service Fabric-clusters in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="12586-121">Do not use unsecured Service Fabric clusters in a production environment.</span></span>

```azurecli
az sf cluster select --endpoint http://testcluster.com:19080
```

<span data-ttu-id="12586-122">Het clustereindpunt moet worden voorafgegaan door `http` of `https`.</span><span class="sxs-lookup"><span data-stu-id="12586-122">The cluster endpoint must be prefixed by `http` or `https`.</span></span> <span data-ttu-id="12586-123">Het moet de poort voor de HTTP-gateway bevatten.</span><span class="sxs-lookup"><span data-stu-id="12586-123">It must include the port for the HTTP gateway.</span></span> <span data-ttu-id="12586-124">De poort en het adres komen overeen met de Service Fabric Explorer-URL.</span><span class="sxs-lookup"><span data-stu-id="12586-124">The port and address are the same as the Service Fabric Explorer URL.</span></span>

<span data-ttu-id="12586-125">Voor clusters die zijn beveiligd met een certificaat, kunt u niet-versleutelde .pem-bestanden of .crt- en .key-bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="12586-125">For clusters that are secured with a certificate, you can use either unencrypted .pem files, or .crt and .key files.</span></span> <span data-ttu-id="12586-126">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="12586-126">For example:</span></span>

```azurecli
az sf cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="12586-127">Zie [Verbinding maken met een beveiligd Azure Service Fabric-cluster](service-fabric-connect-to-secure-cluster.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="12586-127">For more information, see [Connect to a secure Azure Service Fabric cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

> [!NOTE]
> <span data-ttu-id="12586-128">De `select`-opdracht reageert niet op aanvragen voordat deze wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="12586-128">The `select` command doesn't act on any requests before it returns.</span></span> <span data-ttu-id="12586-129">Gebruik een opdracht als `az sf cluster health` om te controleren of u een cluster correct hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12586-129">To verify that you've specified a cluster correctly, use a command like `az sf cluster health`.</span></span> <span data-ttu-id="12586-130">Controleer of de opdracht niet eventuele fouten retourneert.</span><span class="sxs-lookup"><span data-stu-id="12586-130">Verify that the command doesn't return any errors.</span></span>

## <a name="basic-operations"></a><span data-ttu-id="12586-131">Basisbewerkingen</span><span class="sxs-lookup"><span data-stu-id="12586-131">Basic operations</span></span>

<span data-ttu-id="12586-132">De gegevens van een clusterverbinding blijven behouden tussen meerdere Azure CLI-sessies.</span><span class="sxs-lookup"><span data-stu-id="12586-132">Cluster connection information persists across multiple Azure CLI sessions.</span></span> <span data-ttu-id="12586-133">Nadat u een Service Fabric-cluster hebt geselecteerd, kunt u elke Service Fabric-opdracht in het cluster uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="12586-133">After you select a Service Fabric cluster, you can run any Service Fabric command on the cluster.</span></span>

<span data-ttu-id="12586-134">Als u bijvoorbeeld de status van het Service Fabric-cluster wilt weten, voert u de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="12586-134">For example, to get the Service Fabric cluster health state, use the following command:</span></span>

```azurecli
az sf cluster health
```

<span data-ttu-id="12586-135">De opdracht levert de volgende uitvoer op (ervan uitgaande dat JSON-uitvoer is opgegeven in de configuratie van de Azure CLI):</span><span class="sxs-lookup"><span data-stu-id="12586-135">The command results in the following output (assuming that JSON output is specified in the Azure CLI configuration):</span></span>

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

## <a name="tips-and-troubleshooting"></a><span data-ttu-id="12586-136">Tips en probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="12586-136">Tips and troubleshooting</span></span>

<span data-ttu-id="12586-137">U kunt de volgende informatie handig vinden als u problemen ondervindt tijdens het gebruik van Service Fabric-opdrachten in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="12586-137">You might find the following information helpful if you run into issues while using Service Fabric commands in Azure CLI.</span></span>

### <a name="convert-a-certificate-from-pfx-to-pem-format"></a><span data-ttu-id="12586-138">Een certificaat converteren van PFX- naar PEM-indeling</span><span class="sxs-lookup"><span data-stu-id="12586-138">Convert a certificate from PFX to PEM format</span></span>

<span data-ttu-id="12586-139">De Azure CLI ondersteunt clientcertificaten als PEM-bestanden (extensie .pem).</span><span class="sxs-lookup"><span data-stu-id="12586-139">Azure CLI supports client-side certificates as PEM (.pem extension) files.</span></span> <span data-ttu-id="12586-140">Als u PFX-bestanden van Windows gebruikt, moet u deze certificaten converteren naar PEM-indeling.</span><span class="sxs-lookup"><span data-stu-id="12586-140">If you use PFX files from Windows, you must convert those certificates to PEM format.</span></span> <span data-ttu-id="12586-141">Gebruik de volgende opdracht om een PFX-bestand te converteren naar een PEM-bestand:</span><span class="sxs-lookup"><span data-stu-id="12586-141">To convert a PFX file to a PEM file, use the following command:</span></span>

```bash
openssl pkcs12 -in certificate.pfx -out mycert.pem -nodes
```

<span data-ttu-id="12586-142">Voor meer informatie raadpleegt u de [OpenSSL-documentatie](https://www.openssl.org/docs/).</span><span class="sxs-lookup"><span data-stu-id="12586-142">For more information, see the [OpenSSL documentation](https://www.openssl.org/docs/).</span></span>

### <a name="connection-issues"></a><span data-ttu-id="12586-143">Verbindingsproblemen</span><span class="sxs-lookup"><span data-stu-id="12586-143">Connection issues</span></span>

<span data-ttu-id="12586-144">Bepaalde bewerkingen genereren mogelijk het volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="12586-144">Some operations might generate the following message:</span></span>

`Failed to establish a new connection: [Errno 8] nodename nor servname provided, or not known`

<span data-ttu-id="12586-145">Controleer of het opgegeven clustereindpunt beschikbaar is en luistert.</span><span class="sxs-lookup"><span data-stu-id="12586-145">Verify that the specified cluster endpoint is available and listening.</span></span> <span data-ttu-id="12586-146">Controleer ook of de gebruikersinterface van Service Fabric Explorer beschikbaar is op die host en poort.</span><span class="sxs-lookup"><span data-stu-id="12586-146">Also, verify that the Service Fabric Explorer UI is available at that host and port.</span></span> <span data-ttu-id="12586-147">Gebruik `az sf cluster select` om het eindpunt bij te werken.</span><span class="sxs-lookup"><span data-stu-id="12586-147">To update the endpoint, use `az sf cluster select`.</span></span>

### <a name="detailed-logs"></a><span data-ttu-id="12586-148">Gedetailleerde logboeken</span><span class="sxs-lookup"><span data-stu-id="12586-148">Detailed logs</span></span>

<span data-ttu-id="12586-149">Gedetailleerde logboeken zijn vaak nuttig zijn wanneer u fouten opspoort of een probleem meldt.</span><span class="sxs-lookup"><span data-stu-id="12586-149">Detailed logs often are helpful when you debug or report an issue.</span></span> <span data-ttu-id="12586-150">De Azure CLI bevat een algemene `--debug`-vlag waarmee het detailniveau van logboeken wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="12586-150">Azure CLI offers a global `--debug` flag that increases the verbosity of log files.</span></span>

### <a name="command-help-and-syntax"></a><span data-ttu-id="12586-151">Syntaxis van Help-opdracht</span><span class="sxs-lookup"><span data-stu-id="12586-151">Command help and syntax</span></span>

<span data-ttu-id="12586-152">De Service Fabric-opdrachten volgen dezelfde conventie als de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="12586-152">Service Fabric commands follow the same conventions as Azure CLI.</span></span> <span data-ttu-id="12586-153">Als u hulp nodig hebt met een specifieke opdracht of een groep opdrachten, gebruikt u de `-h`-vlag:</span><span class="sxs-lookup"><span data-stu-id="12586-153">For help with a specific command or a group of commands, use the `-h` flag:</span></span>

```azurecli
az sf application -h
```

<span data-ttu-id="12586-154">Hier volgt nog een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="12586-154">Here's another example:</span></span>

```azurecli
az sf application create -h
```
