---
title: aaaService principal voor Azure Kubernetes cluster | Microsoft Docs
description: Een service-principal voor Azure Active Directory voor een Kubernetes-cluster in Azure Container Service maken en beheren
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Een service-principal voor Azure AD voor een Kubernetes-cluster in Container Service instellen


In Azure Container Service een cluster Kubernetes vereist een [Azure Active Directory-service-principal](../../active-directory/develop/active-directory-application-objects.md) toointeract met Azure-API's. Hallo service-principal is nodig toodynamically beheren van resources, zoals [gebruiker gedefinieerde routes](../../virtual-network/virtual-networks-udr-overview.md) en Hallo [laag 4 Azure Load Balancer](../../load-balancer/load-balancer-overview.md). 


In dit artikel bevat verschillende opties tooset van een service principal voor uw cluster Kubernetes. Bijvoorbeeld, als u geïnstalleerd en geconfigureerd Hallo [Azure CLI 2.0](/cli/azure/install-az-cli2), kunt u Hallo uitvoeren [ `az acs create` ](/cli/azure/acs#create) opdracht toocreate hello Kubernetes cluster en Hallo service-principal op Hallo hetzelfde moment.


## <a name="requirements-for-hello-service-principal"></a>Vereisten voor service-principal Hallo

U kunt een bestaande Azure AD-service-principal Hallo volgens de vereisten voldoet aan of een nieuwe maken.

* **Bereik**: Hallo resourcegroep in Hallo abonnement toodeploy hello Kubernetes cluster gebruikt of (minder restrictief) Hallo abonnement toodeploy Hallo-cluster.

* **Rol**: **inzender**

* **Clientgeheim**: moet een wachtwoord zijn. U kunt momenteel geen service-principal gebruiken om verificatie via een certificaat in te stellen.

> [!IMPORTANT] 
> een service-principal toocreate, u moet machtigingen tooregister een toepassing hebt met uw Azure AD-tenant en tooassign Hallo toepassingsrol tooa in uw abonnement. toosee als u Hallo vereist machtigingen hebt, [inchecken Hallo Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Optie 1: een service-principal maken in Azure AD

Als u een Azure AD-service-principal toocreate wilt voordat u uw cluster Kubernetes implementeert, biedt Azure verschillende methoden. 

Hallo volgende voorbeeldopdrachten laten zien hoe u toodo dit Hello [Azure CLI 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). U kunt ook een maken service principal met [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), Hallo [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), of andere methoden.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

Uitvoer is vergelijkbaar toohello volgende (hier weergegeven geredigeerde):

![Een service-principal maken](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Hallo gemarkeerd zijn **client-ID** (`appId`) en Hallo **clientgeheim** (`password`) die u gebruikt als parameters van de service-principal voor implementatie van het cluster.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Service-principal bij het maken van Hallo Kubernetes cluster opgeven

Hallo bieden **client-ID** (ook wel Hallo `appId`, voor toepassings-ID) en **clientgeheim** (`password`) van een bestaande service-principal als parameters bij het maken van Hallo Kubernetes cluster. Zorg ervoor dat service-principal Hallo Hallo voldoet op Hallo vanaf dit artikel.

U kunt deze parameters opgeven bij het implementeren van Hallo Kubernetes cluster met behulp van Hallo [Azure opdrachtregelinterface (CLI) 2.0](container-service-kubernetes-walkthrough.md), [Azure-portal](../dcos-swarm/container-service-deployment.md), of andere methoden.

>[!TIP] 
>Bij het opgeven van Hallo **client-ID**, worden ervoor toouse hello `appId`, niet Hallo `ObjectId`, van de service-principal Hallo.
>

Hallo volgende voorbeeld ziet eenrichtingssessie toopass Hallo parameters Hello Azure CLI 2.0. In dit voorbeeld wordt Hallo [Kubernetes snelstartsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Download](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) Hallo parameters sjabloonbestand `azuredeploy.parameters.json` vanuit GitHub.

2. toospecify hello service-principal, voer waarden in voor `servicePrincipalClientId` en `servicePrincipalClientSecret` in Hallo-bestand. (U moet ook tooprovide uw eigen waarden voor `dnsNamePrefix` en `sshRSAPublicKey`. Hallo laatstgenoemde is Hallo SSH openbare sleutel tooaccess Hallo cluster.) Hallo-bestand opslaan.

    ![Parameters voor de service-principal doorgeven](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Voer Hallo de volgende opdracht, met behulp van `--parameters` tooset Hallo pad toohello azuredeploy.parameters.json bestand. Met deze opdracht implementeert Hallo-cluster in een resourcegroep die u aangeroepen maakt `myResourceGroup` in de regio VS-West Hallo.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Optie 2: Een service-principal genereren bij het maken van Hallo-cluster met`az acs create`

Als u Hallo uitvoert [ `az acs create` ](/cli/azure/acs#create) opdracht toocreate Hallo Kubernetes cluster, hebt u Hallo optie toogenerate een service-principal automatisch.

Net zoals bij andere opties voor het maken van Kubernetes-clusters kunt u parameters voor een bestaande service-principal opgeven tijdens het uitvoeren van `az acs create`. Echter, wanneer u deze parameters weglaat, hello Azure CLI maakt een automatisch voor gebruik met Container Service. Dit vindt plaats transparant tijdens het Hallo-implementatie. 

Hallo volgende opdracht maakt u een cluster Kubernetes en genereert zowel SSH-sleutels en service-principal referenties:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Als uw account geen hello Azure AD- en abonnement machtigingen toocreate een service-principal, Hallo-opdracht wordt een fout gegenereerd vergelijkbaar te`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Aanvullende overwegingen

* Als u geen machtigingen toocreate een service-principal in uw abonnement, moet u mogelijk tooask uw Azure AD of abonnement beheerder tooassign Hallo vereiste machtigingen of vraag om een service-principal toouse met Azure Container Service. 

* Hallo service-principal voor Kubernetes is een onderdeel van de clusterconfiguratie Hallo. Echter niet gebruiken Hallo identiteit toodeploy Hallo cluster.

* Elke service-principal is gekoppeld aan een Azure AD-toepassing. Hallo service-principal voor een cluster Kubernetes kan worden gekoppeld aan een geldig Azure AD-toepassingsnaam (bijvoorbeeld: `https://www.contoso.org/example`). Hallo-URL voor de toepassing hello beschikt niet over toobe een echte-eindpunt.

* Opgeven wanneer Hallo service-principal **Client-ID**, kunt u Hallo-waarde van Hallo `appId` (zoals weergegeven in dit artikel) of de bijbehorende service-principal Hallo `name` (bijvoorbeeld`https://www.contoso.org/example`).

* Hallo-service-principal referenties worden op Hallo hoofd- en agent Hallo Kubernetes cluster virtuele machines opgeslagen in Hallo bestand /etc/kubernetes/azure.json.

* Wanneer u Hallo gebruikt `az acs create` toogenerate Hallo service-principal met de opdracht automatisch, principal Servicereferenties Hallo toohello bestand ~/.azure/acsServicePrincipal.json op Hallo machine toorun Hallo opdracht gebruikt worden geschreven. 

* Bij het gebruik van Hallo `az acs create` toogenerate Hallo service-principal met de opdracht automatisch, service-principal Hallo kan ook worden geverifieerd met een [Azure container register](../../container-registry/container-registry-intro.md) gemaakt in Hallo hetzelfde abonnement.




## <a name="next-steps"></a>Volgende stappen

* [Aan de slag met Kubernetes](container-service-kubernetes-walkthrough.md) in de Cluster Container Service-cluster.

* tootroubleshoot hello service-principal voor Kubernetes, Zie Hallo [ACS-Engine documentatie](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


