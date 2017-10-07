---
title: aaaDeploy OpenShift oorsprong tooAzure | Microsoft Docs
description: Meer informatie over toodeploy OpenShift oorsprong tooAzure virtuele machines.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>OpenShift oorsprong tooAzure virtuele Machines implementeren 

[OpenShift oorsprong](https://www.openshift.org/) is een open-source container-platform gebouwd op [Kubernetes](https://kubernetes.io/). Het vereenvoudigt Hallo implementeren, schaal en werken met multitenant-toepassingen. 

Deze handleiding wordt beschreven hoe toodeploy OpenShift oorsprong over het gebruik van Azure Virtual Machines hello Azure CLI en Azure Resource Manager-sjablonen. In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een toomanage KeyVault SSH-sleutels voor Hallo OpenShift cluster maken.
> * Een cluster OpenShift op Azure VM's implementeren. 
> * Installeer en configureer Hallo [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage Hallo-cluster.
> * Hallo OpenShift implementatie aanpassen.

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

Deze snel starten vereist hello Azure CLI versie 2.0.8 of hoger. toofind hello versie, voer `az --version`. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>Meld u bij tooAzure 
Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht en volg Hallo op het scherm instructies of klik op **Try it** toouse Cloud Shell.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>Een sleutelkluis maken
Maken van een KeyVault toostore Hallo SSH-sleutels voor Hallo cluster Hello [az keyvault maken](/cli/azure/keyvault#create) opdracht.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>Een SSH-sleutel maken 
Een SSH-sleutel is vereist toosecure toegang toohello OpenShift oorsprong cluster. Maken van een SSH-sleutelpaar met Hallo `ssh-keygen` opdracht. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> Hallo SSH-sleutelpaar, hebt u geen een wachtwoordzin.

Voor meer informatie over de SSH-sleutels op Windows, [hoe toocreate SSH-sleutels op Windows](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Opslaan van persoonlijke SSH-sleutel in de Sleutelkluis
Hallo OpenShift implementatie maakt gebruik van SSH-sleutel Hallo u toosecure toegang toohello OpenShift master gemaakt. tooenable hello implementatie toosecurely Hallo SSH-sleutel ophalen, Hallo sleutel opslaan in de Sleutelkluis met behulp van de volgende opdracht Hallo.

# <a name="enabled-for-template-deployment"></a>Ingeschakeld voor de sjabloonimplementatie van
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Een service-principal maken 
OpenShift communiceert met Azure met behulp van een gebruikersnaam en wachtwoord of een service-principal. Een Azure-service-principal is een beveiligings-id die u met apps, services en automatiseringsprogramma's zoals OpenShift gebruiken kunt. U bepaalt de en definieer Hallo machtigingen als toowhat operations Hallo service-principal in Azure uitvoeren kunt. tooimprove beveiliging via gewoon een gebruikersnaam en wachtwoord voor het bieden, in dit voorbeeld wordt een basic service principal.

Maken van een service principal met [az ad sp maken-voor-rbac](/cli/azure/ad/sp#create-for-rbac) en uitvoer Hallo de referenties die OpenShift moet:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Let op de eigenschap appId Hallo van Hallo-opdracht geretourneerd.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > Maak geen onbeveiligd wachtwoord.  Volg de richtlijnen in [Azure AD password rules and restrictions](/azure/active-directory/active-directory-passwords-policy) (Regels en beperkingen voor wachtwoorden in Azure AD).

Zie voor meer informatie over service-principals [een Azure-service-principal maken met Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>Hallo OpenShift oorsprong sjabloon implementeren
Naast OpenShift oorsprong met een Azure Resource Manager-sjabloon implementeren. 

> [!NOTE] 
> Hallo volgende opdracht vereist az CLI 2.0.8 of hoger. U kunt controleren of Hallo az CLI versie Hello `az --version` opdracht. tooupdate hello CLI versie, Zie [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).

Gebruik Hallo `appId` waarde van de service-principal Hallo u eerder hebt gemaakt voor Hallo `aadClientId` parameter.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
Hallo-implementatie kan toocomplete van too20 minuten duren. Hallo Hallo OpenShift console-URL en DNS-naam van Hallo OpenShift-master is afgedrukt toohello terminal wanneer Hallo-implementatie is voltooid.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Verbinding maken met toohello OpenShift cluster
Wanneer het Hallo-implementatie is voltooid, verbinding maken met toohello OpenShift console met behulp van Hallo browser met Hallo `OpenShift Console Uri`. U kunt ook toohello OpenShift master met behulp van de volgende opdracht Hallo verbinden.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Resources opschonen
Wanneer deze niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, OpenShift cluster en alle gerelateerde resources.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie, geleerde procedure:
> [!div class="checklist"]
> * Een toomanage KeyVault SSH-sleutels voor Hallo OpenShift cluster maken.
> * Een cluster OpenShift op Azure VM's implementeren. 
> * Installeer en configureer Hallo [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) toomanage Hallo-cluster.

Nu wordt dat OpenShift oorsprong-cluster geïmplementeerd. U kunt OpenShift zelfstudies toolearn hoe volgen toodeploy uw eerste toepassing en gebruik Hallo OpenShift hulpprogramma's. Zie [aan de slag met OpenShift oorsprong](https://docs.openshift.org/latest/getting_started/index.html) tooget gestart. 
