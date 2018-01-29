---
title: Instellingen voor beheer van Azure Machine Learning-Model en configuratie | Microsoft Docs
description: Dit document beschrijft de stappen en -concepten betrokken bij het instellen en configureren van Model Management in Azure Machine Learning.
services: machine-learning
author: raymondlaghaeian
ms.author: raymondl
manager: neerajkh
ms.reviewer: garyericson, jasonwhowell, mldocs
ms.service: machine-learning
ms.workload: data-services
ms.topic: article
ms.date: 08/29/2017
ms.openlocfilehash: 151e7c2dc808a8fa117a0d7a1950185abe9e3152
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/08/2017
---
# <a name="model-management-setup"></a>Instellingen voor het beheer van model

## <a name="overview"></a>Overzicht
Dit document helpt u op weg met het gebruik van Azure ML-model management implementeren en beheren van uw machine learning-modellen als webservices. 

Met behulp van Azure ML-model management, kunt u efficiënt implementeren en beheren van Machine Learning-modellen die zijn gebouwd met een aantal frameworks, met inbegrip van SparkML, Keras, TensorFlow, de Microsoft cognitieve Toolkit of Python. 

Aan het einde van dit document moet u het volgende kunnen uw model beheeromgeving ingesteld en klaar voor het implementeren van uw machine learning-modellen.

## <a name="what-you-need-to-get-started"></a>Wat u moet aan de slag
Als u optimaal gebruik van deze handleiding, moet u eigenaar toegang hebt tot een Azure-abonnement dat u uw modellen kunt implementeren.
De CLI is voorgeïnstalleerd op de Workbench van Azure Machine Learning en klik op [Azure DSVMs](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).

## <a name="using-the-cli"></a>Met behulp van de CLI
Met de opdrachtregelinterfaces (CLIs) van de Workbench, klikt u op **bestand** -] **Open CommandLine Interface**. 

Op een gegevens wetenschappelijke virtuele Machine, verbinding maken en open de opdrachtprompt. Type `az ml -h` om de opties te bekijken. Voor meer informatie over de opdrachten gebruiken de--help-vlag.

U moet de CLIs installeren op andere systemen.

### <a name="installing-or-updating-on-windows"></a>Installeren (of bijwerken) in Windows

Python van https://www.python.org/ installeren. Zorg ervoor dat u hebt geselecteerd voor het installeren van pip.

Open een opdrachtprompt met als Administrator uitvoeren en voer de volgende opdrachten:

```cmd
pip install azure-cli
pip install azure-cli-ml
```
 
>[!NOTE]
>Als u een eerdere versie hebt, verwijdert u eerst met behulp van de volgende opdracht:
>

```cmd
pip uninstall azure-cli-ml
```

### <a name="installing-or-updating-on-linux"></a>Installeren (of bijwerken) op Linux
Voer de volgende opdracht vanaf de opdrachtregel en volg de aanwijzingen:

```bash
sudo -i
pip install azure-cli
pip install azure-cli-ml
```

Nadat installatieassembly voltooid is, kunt u de volgende opdracht uitvoeren:

```bash
sudo /opt/microsoft/azureml/initial_setup.sh
```

>[!NOTE]
>Meld u af en weer aanmelden op uw SSH-sessie om de wijzigingen van kracht te laten worden.
>De vorige opdrachten kunt u een eerdere versie van de CLIs op de DSVM bijwerken.
>

## <a name="deploying-your-model"></a>Implementeren van uw model
Gebruik de CLIs modellen als webservices implementeren. De webservices kunnen worden geïmplementeerd, lokaal of naar een cluster.

Beginnen met een lokale implementatie, te valideren dat uw model en code werkt, klikt u vervolgens implementeert op een cluster voor gebruik in productieomgevingen schaal.

Als u wilt starten, moet u uw implementatieomgeving instellen. De instelling van de omgeving is een taak. Zodra de installatie voltooid is, kunt u de omgeving voor toekomstige implementaties opnieuw gebruiken. Zie de volgende sectie voor meer informatie.

Wanneer de omgeving-installatie te voltooien:
- U wordt gevraagd aan te melden bij Azure. Als u wilt aanmelden, moet u een webbrowser gebruiken op de pagina https://aka.ms/devicelogin opent en voert u de opgegeven code om te verifiëren.
- U wordt gevraagd tijdens het verificatieproces voor een account te verifiëren met. Belangrijk: Selecteer een account met een geldige Azure-abonnement en voldoende machtigingen voor het maken van resources in het account. - Als het aanmelden voltooid is, uw abonnementsgegevens wordt weergegeven en u wordt gevraagd of u doorgaan wilt met de geselecteerde account.

### <a name="environment-setup"></a>Instellen van de omgeving
Om het installatieproces start, moet u de omgeving-provider geregistreerd met de volgende opdracht:

```azurecli
az provider register -n Microsoft.MachineLearningCompute
```

#### <a name="local-deployment"></a>Lokale implementatie
Als u wilt implementeren en testen van uw web-service op de lokale computer, stelt u een lokale omgeving met de volgende opdracht:

```azurecli
az ml env setup -l [location of Azure Region, e.g. eastus2] -n [your environment name] [-g [existing resource group]]
```
>[!NOTE] 
>Lokale web service wilt implementeren, moet uw Docker installeren op de lokale computer. 
>

De lokale omgeving setup-opdracht maakt u de volgende bronnen in uw abonnement:
- Een resourcegroep (als niet is opgegeven)
- een opslagaccount
- Een Azure Container Registry (ACR)
- Application insights

Nadat setup voltooid is, stelt u de omgeving moet worden gebruikt met de volgende opdracht:

```azurecli
az ml env set -n [environment name] -g [resource group]
```

#### <a name="cluster-deployment"></a>Implementatie van het cluster
Implementatie van het Cluster voor hoge schaalbaarheid productiescenario's gebruiken. Deze stelt een ACS-cluster met Kubernetes als de orchestrator. De ACS-cluster kan worden uitgebreid voor het afhandelen van grotere doorvoer voor uw web-serviceaanroepen.

Als u wilt uw webservice implementeren in een productieomgeving, Stel eerst de omgeving met de volgende opdracht:

```azurecli
az ml env setup -c --name [your environment name] --location [Azure region e.g. eastus2] [-g [resource group]]
```

De installatieopdracht van de cluster-omgeving maakt de volgende bronnen in uw abonnement:
- Een resourcegroep (als niet is opgegeven)
- een opslagaccount
- Een Azure Container Registry (ACR)
- Een Kubernetes-implementatie in een Azure Container Service (ACS)-cluster
- Application insights

De resourcegroep, een opslagaccount en een ACR worden snel gemaakt. De ACS-implementatie kan maximaal 20 minuten duren. 

Nadat setup voltooid is, moet u de omgeving moet worden gebruikt voor deze implementatie in te stellen. Gebruik de volgende opdracht:

```azurecli
az ml env set -n [environment name] -g [resource group]
```

>[!NOTE] 
> Nadat de omgeving is gemaakt voor de volgende implementaties, moet u alleen gebruik van de bovenstaande set-opdracht te gebruiken.
>

>[!NOTE] 
>Geef een SSL-certificaat voor het maken van een HTTPS-eindpunt bij het maken van een cluster met behulp van de--opties cert-naam en--cert pem in az ml env setup. Hiermee stelt u het cluster voor aanvragen op https, beveiligd met het opgegeven certificaat. Nadat setup voltooid is, maakt u een DNS CNAME-record die naar de FQDN van het cluster verwijst.

### <a name="create-an-account"></a>Een Account maken
Er is een account vereist voor het implementeren van modellen. U moet hiervoor eenmaal per account, en dezelfde account in meerdere implementaties kunnen gebruiken.

Gebruik de volgende opdracht voor het maken van een nieuw account:

```azurecli
az ml account modelmanagement create -l [Azure region, e.g. eastus2] -n [your account name] -g [resource group name] --sku-instances [number of instances, e.g. 1] --sku-name [Pricing tier for example S1]
```

Voor het gebruik van een bestaand account, moet u de volgende opdracht gebruiken:
```azurecli
az ml account modelmanagement set -n [your account name] -g [resource group it was created in]
```

### <a name="deploy-your-model"></a>Implementeer uw model
U bent nu klaar voor het implementeren van het model van uw opgeslagen als een webservice. 

```azurecli
az ml service create realtime --model-file [model file/folder path] -f [scoring file e.g. score.py] -n [your service name] -s [schema file e.g. service_schema.json] -r [runtime for the Docker container e.g. spark-py or python] -c [conda dependencies file for additional python packages]
```

### <a name="next-steps"></a>Volgende stappen
Probeer een aantal voorbeelden in de galerie.
