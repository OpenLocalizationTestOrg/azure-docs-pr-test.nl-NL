---
title: aaaCreate Hadoop-clusters met Azure REST API - Azure | Microsoft Docs
description: Meer informatie over hoe toocreate HDInsight-clusters door het indienen van Azure Resource Manager-sjablonen toohello REST API van Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="6f809-103">Hadoop-clusters met hello Azure REST-API maken</span><span class="sxs-lookup"><span data-stu-id="6f809-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="6f809-104">Ontdek hoe toocreate een HDInsight-cluster met een Azure Resource Manager-sjabloon en Hallo REST API van Azure.</span><span class="sxs-lookup"><span data-stu-id="6f809-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="6f809-105">Hallo REST API van Azure kunt u tooperform beheerbewerkingen op services die worden gehost in hello Azure-platform, inclusief Hallo maken van nieuwe resources, zoals de HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6f809-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f809-106">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6f809-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6f809-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6f809-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="6f809-108">Hallo stappen in dit document gebruik Hallo [curl (https://curl.haxx.se/)](https://curl.haxx.se/) hulpprogramma toocommunicate Hello Azure REST-API.</span><span class="sxs-lookup"><span data-stu-id="6f809-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="6f809-109">Een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="6f809-109">Create a template</span></span>

<span data-ttu-id="6f809-110">Azure Resource Manager-sjablonen zijn JSON-documenten die worden beschreven een **resourcegroep** en alle resources daarin (zoals HDInsight.) Deze aanpak op basis van een sjabloon kunt u toodefine Hallo bronnen die u nodig hebt voor HDInsight in één sjabloon.</span><span class="sxs-lookup"><span data-stu-id="6f809-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="6f809-111">Hallo volgende JSON-document is een fusie Hallo sjabloon en de parameters-bestanden van [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), waarbij automatisch een op Linux gebaseerde cluster met behulp van een wachtwoord toosecure Hallo SSH gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="6f809-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used tooremotely access hello cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

<span data-ttu-id="6f809-112">In dit voorbeeld wordt gebruikt in Hallo stappen in dit document.</span><span class="sxs-lookup"><span data-stu-id="6f809-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="6f809-113">Vervang Hallo voorbeeld *waarden* in Hallo **Parameters** sectie met Hallo waarden voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6f809-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f809-114">Hallo-sjabloon gebruikt Hallo standaardaantal worker-knooppunten (4) voor een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6f809-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="6f809-115">Als u van plan meer dan 32 worker-knooppunten bent, selecteert u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="6f809-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="6f809-116">Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="6f809-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="6f809-117">Meld u bij tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="6f809-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="6f809-118">Hallo stappen beschreven in [aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) en maak verbinding met Hallo tooyour-abonnement `az login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6f809-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="6f809-119">Een service-principal maken</span><span class="sxs-lookup"><span data-stu-id="6f809-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="6f809-120">Deze stappen zijn een verkorte versie Hallo *service-principal maken met een wachtwoord* sectie Hallo [gebruik Azure CLI toocreate een service-principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span><span class="sxs-lookup"><span data-stu-id="6f809-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="6f809-121">Deze procedure maakt u een service-principal die is gebruikt tooauthenticate toohello REST API van Azure.</span><span class="sxs-lookup"><span data-stu-id="6f809-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="6f809-122">Gebruik vanaf een opdrachtregel Hallo opdracht toolist na uw Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="6f809-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="6f809-123">Selecteer in Hallo lijst Hallo-abonnement dat u toouse wilt en houd er rekening mee Hallo **Subscription_ID** en __Tenant_ID__ kolommen.</span><span class="sxs-lookup"><span data-stu-id="6f809-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="6f809-124">Sla deze waarden.</span><span class="sxs-lookup"><span data-stu-id="6f809-124">Save these values.</span></span>

2. <span data-ttu-id="6f809-125">Gebruik Hallo opdracht toocreate een toepassing in Azure Active Directory te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f809-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="6f809-126">Vervang de waarden Hallo voor Hallo `--display-name`, `--homepage`, en `--identifier-uris` met uw eigen waarden.</span><span class="sxs-lookup"><span data-stu-id="6f809-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="6f809-127">Een wachtwoord opgeven voor hello nieuwe Active Directory-vermelding.</span><span class="sxs-lookup"><span data-stu-id="6f809-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6f809-128">Hallo `--home-page` en `--identifier-uris` tooreference een webpagina die worden gehost op Hallo niet moeten de waarden op internet.</span><span class="sxs-lookup"><span data-stu-id="6f809-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="6f809-129">Ze moeten unieke URI's zijn.</span><span class="sxs-lookup"><span data-stu-id="6f809-129">They must be unique URIs.</span></span>

   <span data-ttu-id="6f809-130">Hallo geretourneerde waarde van deze opdracht is Hallo __App-ID__ voor de nieuwe toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="6f809-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="6f809-131">Sla deze waarde.</span><span class="sxs-lookup"><span data-stu-id="6f809-131">Save this value.</span></span>

3. <span data-ttu-id="6f809-132">Gebruik Hallo volgende opdracht toocreate een service-principal met behulp van Hallo **App-ID**.</span><span class="sxs-lookup"><span data-stu-id="6f809-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="6f809-133">Hallo geretourneerde waarde van deze opdracht is Hallo __Object-ID__.</span><span class="sxs-lookup"><span data-stu-id="6f809-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="6f809-134">Sla deze waarde.</span><span class="sxs-lookup"><span data-stu-id="6f809-134">Save this value.</span></span>

4. <span data-ttu-id="6f809-135">Hallo toewijzen **eigenaar** rol toohello service-principal met behulp van Hallo **Object-ID** waarde.</span><span class="sxs-lookup"><span data-stu-id="6f809-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="6f809-136">Gebruik Hallo **abonnements-ID** u eerder hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="6f809-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="6f809-137">Geen verificatietoken ophalen</span><span class="sxs-lookup"><span data-stu-id="6f809-137">Get an authentication token</span></span>

<span data-ttu-id="6f809-138">Gebruik Hallo opdracht tooretrieve geen verificatietoken te volgen:</span><span class="sxs-lookup"><span data-stu-id="6f809-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="6f809-139">Stel `$TENANTID`, `$APPID`, en `$PASSWORD` toohello waarden verkregen of eerder gebruikte.</span><span class="sxs-lookup"><span data-stu-id="6f809-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="6f809-140">Als deze aanvraag gelukt is, u 200 reeks beantwoord en antwoordtekst Hallo bevat een JSON-document.</span><span class="sxs-lookup"><span data-stu-id="6f809-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="6f809-141">Hallo JSON-document geretourneerd door deze aanvraag bevat een element met de naam **access_token**.</span><span class="sxs-lookup"><span data-stu-id="6f809-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="6f809-142">waarde van Hallo **access_token** gebruikte tooauthentication aanvragen toohello REST-API is.</span><span class="sxs-lookup"><span data-stu-id="6f809-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="6f809-143">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="6f809-143">Create a resource group</span></span>

<span data-ttu-id="6f809-144">Gebruik Hallo toocreate een resourcegroep te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f809-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="6f809-145">Stel `$SUBSCRIPTIONID` toohello abonnements-ID ontvangen tijdens het Hallo-service-principal maken.</span><span class="sxs-lookup"><span data-stu-id="6f809-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="6f809-146">Stel `$ACCESSTOKEN` toohello toegangstoken ontvangen in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f809-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="6f809-147">Vervang `DATACENTERLOCATION` met Hallo Datacenter gewenst toocreate Hallo-resourcegroep en bronnen.</span><span class="sxs-lookup"><span data-stu-id="6f809-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="6f809-148">Bijvoorbeeld 'Zuid-centraal VS'.</span><span class="sxs-lookup"><span data-stu-id="6f809-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="6f809-149">Stel `$RESOURCEGROUPNAME` toohello-naam die u wenst dat toouse voor deze groep:</span><span class="sxs-lookup"><span data-stu-id="6f809-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="6f809-150">Als deze aanvraag gelukt is, u 200 reeks beantwoord en antwoordtekst Hallo bevat een JSON-document dat informatie bevat over Hallo-groep.</span><span class="sxs-lookup"><span data-stu-id="6f809-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="6f809-151">Hallo `"provisioningState"` element bevat een waarde van `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="6f809-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="6f809-152">Een implementatie maken</span><span class="sxs-lookup"><span data-stu-id="6f809-152">Create a deployment</span></span>

<span data-ttu-id="6f809-153">Gebruik hello opdracht toodeploy Hallo sjabloon toohello resourcegroep te volgen.</span><span class="sxs-lookup"><span data-stu-id="6f809-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="6f809-154">Stel `$DEPLOYMENTNAME` toohello-naam die u wenst dat toouse voor deze implementatie.</span><span class="sxs-lookup"><span data-stu-id="6f809-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="6f809-155">Als u Hallo tooa sjabloonbestand hebt opgeslagen, kunt u na de opdracht in plaats van Hallo `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="6f809-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="6f809-156">Als deze aanvraag gelukt is, u 200 reeks beantwoord en antwoordtekst Hallo bevat een JSON-document dat informatie bevat over de implementatiebewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="6f809-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6f809-157">Hallo-implementatie is verzonden, maar is niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="6f809-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="6f809-158">Het kan enkele minuten duren voordat, meestal ongeveer 15 Hallo implementatie toocomplete.</span><span class="sxs-lookup"><span data-stu-id="6f809-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="6f809-159">Hallo-status van een implementatie controleren</span><span class="sxs-lookup"><span data-stu-id="6f809-159">Check hello status of a deployment</span></span>

<span data-ttu-id="6f809-160">status van de toocheck Hallo van Hallo-implementatie, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6f809-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="6f809-161">Deze opdracht retourneert een JSON-document dat informatie bevat over Hallo implementatie opnieuw.</span><span class="sxs-lookup"><span data-stu-id="6f809-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="6f809-162">Hallo `"provisioningState"` element bevat Hallo status van Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="6f809-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="6f809-163">Als dit element een waarde van bevat `"Succeeded"`, en vervolgens het Hallo-implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6f809-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="6f809-164">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6f809-164">Troubleshoot</span></span>

<span data-ttu-id="6f809-165">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6f809-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f809-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6f809-166">Next steps</span></span>

<span data-ttu-id="6f809-167">Nu u een HDInsight-cluster hebt gemaakt, gebruiken Hallo toolearn hoe na toowork met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6f809-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="6f809-168">Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="6f809-168">Hadoop clusters</span></span>

* [<span data-ttu-id="6f809-169">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f809-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6f809-170">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f809-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="6f809-171">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f809-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="6f809-172">HBase-clusters</span><span class="sxs-lookup"><span data-stu-id="6f809-172">HBase clusters</span></span>

* [<span data-ttu-id="6f809-173">Aan de slag met HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f809-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="6f809-174">Ontwikkelen van Java-toepassingen voor HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f809-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="6f809-175">Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="6f809-175">Storm clusters</span></span>

* [<span data-ttu-id="6f809-176">Java-topologieën ontwikkelen voor Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f809-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="6f809-177">Python-onderdelen in Storm op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="6f809-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="6f809-178">Implementeren en bewaken topologieën met Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="6f809-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
