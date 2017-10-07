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
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a>Hadoop-clusters met hello Azure REST-API maken

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Ontdek hoe toocreate een HDInsight-cluster met een Azure Resource Manager-sjabloon en Hallo REST API van Azure.

Hallo REST API van Azure kunt u tooperform beheerbewerkingen op services die worden gehost in hello Azure-platform, inclusief Hallo maken van nieuwe resources, zoals de HDInsight-clusters.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

> [!NOTE]
> Hallo stappen in dit document gebruik Hallo [curl (https://curl.haxx.se/)](https://curl.haxx.se/) hulpprogramma toocommunicate Hello Azure REST-API.

## <a name="create-a-template"></a>Een sjabloon maken

Azure Resource Manager-sjablonen zijn JSON-documenten die worden beschreven een **resourcegroep** en alle resources daarin (zoals HDInsight.) Deze aanpak op basis van een sjabloon kunt u toodefine Hallo bronnen die u nodig hebt voor HDInsight in één sjabloon.

Hallo volgende JSON-document is een fusie Hallo sjabloon en de parameters-bestanden van [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), waarbij automatisch een op Linux gebaseerde cluster met behulp van een wachtwoord toosecure Hallo SSH gebruikersaccount.

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

In dit voorbeeld wordt gebruikt in Hallo stappen in dit document. Vervang Hallo voorbeeld *waarden* in Hallo **Parameters** sectie met Hallo waarden voor uw cluster.

> [!IMPORTANT]
> Hallo-sjabloon gebruikt Hallo standaardaantal worker-knooppunten (4) voor een HDInsight-cluster. Als u van plan meer dan 32 worker-knooppunten bent, selecteert u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.
>
> Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="log-in-tooyour-azure-subscription"></a>Meld u bij tooyour Azure-abonnement

Hallo stappen beschreven in [aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) en maak verbinding met Hallo tooyour-abonnement `az login` opdracht.

## <a name="create-a-service-principal"></a>Een service-principal maken

> [!NOTE]
> Deze stappen zijn een verkorte versie Hallo *service-principal maken met een wachtwoord* sectie Hallo [gebruik Azure CLI toocreate een service-principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document. Deze procedure maakt u een service-principal die is gebruikt tooauthenticate toohello REST API van Azure.

1. Gebruik vanaf een opdrachtregel Hallo opdracht toolist na uw Azure-abonnementen.

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    Selecteer in Hallo lijst Hallo-abonnement dat u toouse wilt en houd er rekening mee Hallo **Subscription_ID** en __Tenant_ID__ kolommen. Sla deze waarden.

2. Gebruik Hallo opdracht toocreate een toepassing in Azure Active Directory te volgen.

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    Vervang de waarden Hallo voor Hallo `--display-name`, `--homepage`, en `--identifier-uris` met uw eigen waarden. Een wachtwoord opgeven voor hello nieuwe Active Directory-vermelding.

   > [!NOTE]
   > Hallo `--home-page` en `--identifier-uris` tooreference een webpagina die worden gehost op Hallo niet moeten de waarden op internet. Ze moeten unieke URI's zijn.

   Hallo geretourneerde waarde van deze opdracht is Hallo __App-ID__ voor de nieuwe toepassing hello. Sla deze waarde.

3. Gebruik Hallo volgende opdracht toocreate een service-principal met behulp van Hallo **App-ID**.

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     Hallo geretourneerde waarde van deze opdracht is Hallo __Object-ID__. Sla deze waarde.

4. Hallo toewijzen **eigenaar** rol toohello service-principal met behulp van Hallo **Object-ID** waarde. Gebruik Hallo **abonnements-ID** u eerder hebt verkregen.

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a>Geen verificatietoken ophalen

Gebruik Hallo opdracht tooretrieve geen verificatietoken te volgen:

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

Stel `$TENANTID`, `$APPID`, en `$PASSWORD` toohello waarden verkregen of eerder gebruikte.

Als deze aanvraag gelukt is, u 200 reeks beantwoord en antwoordtekst Hallo bevat een JSON-document.

Hallo JSON-document geretourneerd door deze aanvraag bevat een element met de naam **access_token**. waarde van Hallo **access_token** gebruikte tooauthentication aanvragen toohello REST-API is.

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Gebruik Hallo toocreate een resourcegroep te volgen.

* Stel `$SUBSCRIPTIONID` toohello abonnements-ID ontvangen tijdens het Hallo-service-principal maken.
* Stel `$ACCESSTOKEN` toohello toegangstoken ontvangen in de vorige stap Hallo.
* Vervang `DATACENTERLOCATION` met Hallo Datacenter gewenst toocreate Hallo-resourcegroep en bronnen. Bijvoorbeeld 'Zuid-centraal VS'.
* Stel `$RESOURCEGROUPNAME` toohello-naam die u wenst dat toouse voor deze groep:

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

Als deze aanvraag gelukt is, u 200 reeks beantwoord en antwoordtekst Hallo bevat een JSON-document dat informatie bevat over Hallo-groep. Hallo `"provisioningState"` element bevat een waarde van `"Succeeded"`.

## <a name="create-a-deployment"></a>Een implementatie maken

Gebruik hello opdracht toodeploy Hallo sjabloon toohello resourcegroep te volgen.

* Stel `$DEPLOYMENTNAME` toohello-naam die u wenst dat toouse voor deze implementatie.

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> Als u Hallo tooa sjabloonbestand hebt opgeslagen, kunt u na de opdracht in plaats van Hallo `-d "{ template and parameters}"`:
>
> `--data-binary "@/path/to/file.json"`

Als deze aanvraag gelukt is, u 200 reeks beantwoord en antwoordtekst Hallo bevat een JSON-document dat informatie bevat over de implementatiebewerking Hallo.

> [!IMPORTANT]
> Hallo-implementatie is verzonden, maar is niet voltooid. Het kan enkele minuten duren voordat, meestal ongeveer 15 Hallo implementatie toocomplete.

## <a name="check-hello-status-of-a-deployment"></a>Hallo-status van een implementatie controleren

status van de toocheck Hallo van Hallo-implementatie, gebruik Hallo volgende opdracht:

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

Deze opdracht retourneert een JSON-document dat informatie bevat over Hallo implementatie opnieuw. Hallo `"provisioningState"` element bevat Hallo status van Hallo-implementatie. Als dit element een waarde van bevat `"Succeeded"`, en vervolgens het Hallo-implementatie is voltooid.

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen

Nu u een HDInsight-cluster hebt gemaakt, gebruiken Hallo toolearn hoe na toowork met uw cluster.

### <a name="hadoop-clusters"></a>Hadoop-clusters

* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase-clusters

* [Aan de slag met HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Ontwikkelen van Java-toepassingen voor HBase in HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm-clusters

* [Java-topologieën ontwikkelen voor Storm op HDInsight](hdinsight-storm-develop-java-topology.md)
* [Python-onderdelen in Storm op HDInsight gebruiken](hdinsight-storm-develop-python-topology.md)
* [Implementeren en bewaken topologieën met Storm op HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
