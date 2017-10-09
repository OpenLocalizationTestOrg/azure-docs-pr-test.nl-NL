---
title: aaaManage certificaten in een Azure Service Fabric-cluster | Microsoft Docs
description: Beschrijft hoe nieuwe certificaten tooadd, rollovercertificaat en verwijderen van het certificaat tooor van een Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="a0f7a-103">Toevoegen of verwijderen van certificaten voor een Service Fabric-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="a0f7a-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="a0f7a-104">Het is raadzaam dat u raken met het Service Fabric X.509-certificaten gebruikt en vertrouwd met de Hallo zijn [security scenario's](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="a0f7a-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with hello [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="a0f7a-105">U moet begrijpen wat een certificaat in het cluster is en wat wordt gebruikt voor, voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="a0f7a-106">Service fabric kunt die u opgeven dat twee certificaten, een primaire en een secundaire cluster bij het configureren van beveiliging certificate tijdens het maken van het cluster in toevoeging tooclient certificaten.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition tooclient certificates.</span></span> <span data-ttu-id="a0f7a-107">Raadpleeg te[maken van een azure-cluster via de portal](service-fabric-cluster-creation-via-portal.md) of [maken van een azure-cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) voor meer informatie over het instellen op voor het maken.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-107">Refer too[creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="a0f7a-108">Als u slechts één cluster certificaat opgeeft op voor het maken, klikt u vervolgens die wordt gebruikt als het primaire certificaat voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-108">If you specify only one cluster certificate at create time, then that is used as hello primary certificate.</span></span> <span data-ttu-id="a0f7a-109">U kunt een nieuw certificaat na het maken van het cluster toevoegen als een secundaire database.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="a0f7a-110">Voor een beveiligde cluster, moet u altijd ten minste één geldig (niet ingetrokken en niet verlopen)-cluster-certificaat (primair of secundair) geïmplementeerd (zo niet, Hallo cluster niet meer werkt).</span><span class="sxs-lookup"><span data-stu-id="a0f7a-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, hello cluster stops functioning).</span></span> <span data-ttu-id="a0f7a-111">90 dagen voordat alle geldige certificaten verlopen, bereiken Hallo system genereert een waarschuwing trace en ook een waarschuwingsgebeurtenis health op Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-111">90 days before all valid certificates reach expiration, hello system generates a warning trace and also a warning health event on hello node.</span></span> <span data-ttu-id="a0f7a-112">Er is momenteel geen e-mail of andere berichten naar service fabric worden verzonden over dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a><span data-ttu-id="a0f7a-113">Een secundaire cluster-certificaat met behulp van de portal Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="a0f7a-113">Add a secondary cluster certificate using hello portal</span></span>

<span data-ttu-id="a0f7a-114">Secundaire cluster certificaat kan niet worden toegevoegd via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-114">Secondary cluster certificate cannot be added through hello Azure portal.</span></span> <span data-ttu-id="a0f7a-115">U hebt toouse Azure powershell voor die.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-115">You have toouse Azure powershell for that.</span></span> <span data-ttu-id="a0f7a-116">Hallo proces wordt verderop in dit document beschreven.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-116">hello process is outlined later in this document.</span></span>

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a><span data-ttu-id="a0f7a-117">Hallo clustercertificaten met behulp van de portal Hallo uitwisselen</span><span class="sxs-lookup"><span data-stu-id="a0f7a-117">Swap hello cluster certificates using hello portal</span></span>

<span data-ttu-id="a0f7a-118">Nadat u hebt een certificaat secundaire cluster is geïmplementeerd als u wilt dat tooswap Hallo primaire en secundaire, vervolgens toohello beveiliging blade navigeren, en selecteer Hallo 'Wisseling met primaire' optie van Hallo context menu tooswap Hallo secundaire cert met Hallo primaire cert.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-118">After you have successfully deployed a secondary cluster certificate, if you want tooswap hello primary and secondary, then navigate toohello Security blade, and select hello 'Swap with primary' option from hello context menu tooswap hello secondary cert with hello primary cert.</span></span>

![Swap-certificaat][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a><span data-ttu-id="a0f7a-120">Het certificaat voor een cluster met Hallo portal verwijderen</span><span class="sxs-lookup"><span data-stu-id="a0f7a-120">Remove a cluster certificate using hello portal</span></span>

<span data-ttu-id="a0f7a-121">Voor een beveiligde cluster, moet u altijd ten minste één geldig (niet ingetrokken en niet verlopen)-certificaat (primair of secundair) geïmplementeerd zo niet, Hallo cluster niet meer werkt.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, hello cluster stops functioning.</span></span>

<span data-ttu-id="a0f7a-122">tooremove een secundair certificaat worden gebruikt voor clusterbeveiliging, navigeren toohello beveiliging blade en selecteer Hallo 'Delete' optie in het contextmenu Hallo op Hallo secundair certificaat.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-122">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello secondary certificate.</span></span>

<span data-ttu-id="a0f7a-123">Als uw bedoeling is tooremove Hallo certificaat dat is gemarkeerd als primaire, moet u tooswap met eerst secundaire Hallo en verwijder vervolgens de Hallo secundaire nadat het Hallo-upgrade is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-123">If your intent is tooremove hello certificate that is marked primary, then you will need tooswap it with hello secondary first, and then delete hello secondary after hello upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="a0f7a-124">Toevoegen van een secundair certificaat met behulp van Resource Manager Powershell</span><span class="sxs-lookup"><span data-stu-id="a0f7a-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="a0f7a-125">Deze stappen wordt ervan uitgegaan dat u bekend bent met de werking van Resource Manager en ten minste één Service Fabric-cluster met een Resource Manager-sjabloon hebt geïmplementeerd en Hallo-sjabloon die u hebt gebruikt tooset Hallo cluster handige hebt.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have hello template that you used tooset up hello cluster handy.</span></span> <span data-ttu-id="a0f7a-126">Ook wordt ervan uitgegaan dat u vertrouwd met een JSON bent.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="a0f7a-127">Als u zoekt naar een voorbeeldsjabloon en parameters waarmee u toofollow langs of als uitgangspunt kunt, klikt u vervolgens het downloaden van deze [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="a0f7a-127">If you are looking for a sample template and parameters that you can use toofollow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="a0f7a-128">De Resource Manager-sjabloon bewerken</span><span class="sxs-lookup"><span data-stu-id="a0f7a-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="a0f7a-129">Voorbeeld 5-VM-1-NodeTypes-Secure_Step2.JSON bevat voor een eenvoudige van volgende langs alle Hallo bewerkingen we brengen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all hello edits we will be making.</span></span> <span data-ttu-id="a0f7a-130">Hallo-voorbeeld is beschikbaar op [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="a0f7a-130">hello sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="a0f7a-131">**Zorg ervoor dat toofollow alle Hallo stappen**</span><span class="sxs-lookup"><span data-stu-id="a0f7a-131">**Make sure toofollow all hello steps**</span></span>

<span data-ttu-id="a0f7a-132">**Stap 1:** Open Hallo Resource Manager-sjabloon gebruikt van toodeploy die u in de Cluster.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-132">**Step 1:** Open up hello Resource Manager template you used toodeploy you Cluster.</span></span> <span data-ttu-id="a0f7a-133">(Als u Hallo voorbeeld van Hallo hierboven opslagplaats hebt gedownload, gebruikt u 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy een beveiligde cluster en opent u dat de sjabloon).</span><span class="sxs-lookup"><span data-stu-id="a0f7a-133">(If you have downloaded hello sample from hello above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="a0f7a-134">**Stap 2:** toevoegen **twee nieuwe parameters** 'secCertificateThumbprint' en 'secCertificateUrlValue' van het type 'string' toohello parameter gedeelte van uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" toohello parameter section of your template.</span></span> <span data-ttu-id="a0f7a-135">U kunt Hallo volgende codefragment kopiëren en deze toohello sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-135">You can copy hello following code snippet and add it toohello template.</span></span> <span data-ttu-id="a0f7a-136">Afhankelijk van het Hallo-bron van de sjabloon, kunnen u al deze gedefinieerd, als dit het geval de volgende stap toohello verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-136">Depending on hello source of your template, you may already have these defined, if so move toohello next step.</span></span> 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="a0f7a-137">**Stap 3:** wijzigingen aanbrengen toohello **Microsoft.ServiceFabric/clusters** resource - Hallo 'Microsoft.ServiceFabric/clusters' resourcedefinitie niet vinden in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-137">**Step 3:** Make changes toohello **Microsoft.ServiceFabric/clusters** resource - Locate hello "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="a0f7a-138">Onder de eigenschappen van deze definitie van vindt u 'Certificaat' JSON tag, die u moet er ongeveer als Hallo volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="a0f7a-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like hello following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="a0f7a-139">Voeg een nieuwe tag 'thumbprintSecondary' en hieraan een waarde '[parameters('secCertificateThumbprint')]'.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="a0f7a-140">In dat geval nu resourcedefinitie Hallo als in de volgende hello eruitzien moet (afhankelijk van de bron van de sjabloon hello, deze mogelijk niet precies zoals Hallo codefragment hieronder).</span><span class="sxs-lookup"><span data-stu-id="a0f7a-140">So now hello resource definition should look like hello following (depending on your source of hello template, it may not be exactly like hello snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="a0f7a-141">Als u wilt dat te**rollover HALLO cert**, geef vervolgens het nieuwe certificaat Hallo als primaire en verplaatsen Hallo huidige primaire als secundaire.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-141">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="a0f7a-142">Dit resulteert in Hallo overschakeling van uw huidige primaire toohello nieuwe certificaat in één stap van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-142">This results in hello rollover of your current primary certificate toohello new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="a0f7a-143">**Stap 4:** te wijzigingen aanbrengen**alle** hello **Microsoft.Compute/virtualMachineScaleSets** resourcedefinities - Hallo Microsoft.Compute/virtualMachineScaleSets bron vinden definitie.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-143">**Step 4:** Make changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="a0f7a-144">Schuif toohello 'publisher': 'Microsoft.Azure.ServiceFabric' onder 'virtualMachineProfile'.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-144">Scroll toohello "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="a0f7a-145">In de instellingen voor Hallo service fabric publisher ziet u er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-145">In hello service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="a0f7a-147">Hallo nieuwe cert vermeldingen tooit toevoegen</span><span class="sxs-lookup"><span data-stu-id="a0f7a-147">Add hello new cert entries tooit</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="a0f7a-148">Hallo eigenschappen ziet er nu als volgt</span><span class="sxs-lookup"><span data-stu-id="a0f7a-148">hello properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="a0f7a-150">Als u wilt dat te**rollover HALLO cert**, geef vervolgens het nieuwe certificaat Hallo als primaire en verplaatsen Hallo huidige primaire als secundaire.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-150">If you want too**rollover hello cert**, then specify hello new cert as primary and moving hello current primary as secondary.</span></span> <span data-ttu-id="a0f7a-151">Dit resulteert in Hallo overschakeling van uw huidige toohello nieuwe certificaat in één stap van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-151">This results in hello rollover of your current certificate toohello new certificate in one deployment step.</span></span> 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
<span data-ttu-id="a0f7a-152">Hallo eigenschappen ziet er nu als volgt</span><span class="sxs-lookup"><span data-stu-id="a0f7a-152">hello properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="a0f7a-154">**Stap 5:** aanbrengen te**alle** hello **Microsoft.Compute/virtualMachineScaleSets** resourcedefinities - Hallo Microsoft.Compute/virtualMachineScaleSets bron vinden definitie.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-154">**Step 5:** Make Changes too**all** hello **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate hello Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="a0f7a-155">Schuif toohello 'vaultCertificates':, onder 'OSProfile'.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-155">Scroll toohello "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="a0f7a-156">Dit ziet er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="a0f7a-158">Hallo secCertificateUrlValue tooit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-158">Add hello secCertificateUrlValue tooit.</span></span> <span data-ttu-id="a0f7a-159">Hallo codefragment volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a0f7a-159">use hello following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="a0f7a-160">Nu Hallo resulterende Json moet als volgt uitzien.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-160">Now hello resulting Json should look something like this.</span></span>
<span data-ttu-id="a0f7a-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="a0f7a-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="a0f7a-162">Zorg ervoor dat u stap 4 en 5 hebt herhaald voor alle Hallo Nodetypes/Microsoft.Compute/virtualMachineScaleSets resourcedefinities in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-162">Make sure that you have repeated steps 4 and 5 for all hello Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="a0f7a-163">Als u een van beide mist, Hallo certificaat wordt niet geïnstalleerd op deze VMSS en moet u onvoorspelbare resultaten in het cluster, met inbegrip van Hallo cluster tijdelijk niet beschikbaar (als u uiteindelijk geen geldige certificaten dat cluster Hallo kunt gebruiken voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-163">If you miss one of them, hello certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including hello cluster going down (if you end up with no valid certificates that hello cluster can use for security.</span></span> <span data-ttu-id="a0f7a-164">Zo Controleer, voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a><span data-ttu-id="a0f7a-165">Uw bestand tooreflect Hallo nieuwe Sjabloonparameters u die hierboven staan vermeld bewerken</span><span class="sxs-lookup"><span data-stu-id="a0f7a-165">Edit your template file tooreflect hello new parameters you added above</span></span>
<span data-ttu-id="a0f7a-166">Als u van Hallo voorbeeld Hallo gebruikmaakt [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow samen, kunt u wijzigingen toomake starten in 5 in voorbeeld van Hallo-bestanden-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="a0f7a-166">If you are using hello sample from hello [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow along, you can start toomake changes in hello sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="a0f7a-167">De parameter-bestand voor uw Resource Manager-sjabloon bewerken, Hallo twee nieuwe parameters voor secCertificateThumbprint en secCertificateUrlValue toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-167">Edit your Resource Manager Template parameter File, add hello two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a><span data-ttu-id="a0f7a-168">Hallo sjabloon tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="a0f7a-168">Deploy hello template tooAzure</span></span>

- <span data-ttu-id="a0f7a-169">U zijn nu gereed toodeploy uw tooAzure sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-169">You are now ready toodeploy your template tooAzure.</span></span> <span data-ttu-id="a0f7a-170">Open een opdrachtprompt voor Azure PS-versie 1 +.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="a0f7a-171">Log in tooyour Azure-Account en selecteer Hallo specifieke azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-171">Log in tooyour Azure Account and select hello specific azure subscription.</span></span> <span data-ttu-id="a0f7a-172">Dit is een belangrijke stap voor mensen die toegang toomore dan één azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-172">This is an important step for folks who have access toomore than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="a0f7a-173">Hallo sjabloon voorafgaande toodeploying test deze.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-173">Test hello template prior toodeploying it.</span></span> <span data-ttu-id="a0f7a-174">Gebruik dezelfde resourcegroep die uw cluster wordt momenteel geïmplementeerd op Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-174">Use hello same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="a0f7a-175">Hallo sjabloon tooyour resourcegroep implementeren.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-175">Deploy hello template tooyour resource group.</span></span> <span data-ttu-id="a0f7a-176">Gebruik dezelfde resourcegroep die uw cluster wordt momenteel geïmplementeerd op Hallo.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-176">Use hello same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="a0f7a-177">Hallo New-AzureRmResourceGroupDeployment opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-177">Run hello New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="a0f7a-178">U hoeft niet toospecify Hallo-modus, aangezien Hallo standaardwaarde **incrementele**.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-178">You do not need toospecify hello mode, since hello default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="a0f7a-179">Als u de modus tooComplete instelt, kunt u de resources die zich niet in uw sjabloon per ongeluk verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-179">If you set Mode tooComplete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="a0f7a-180">Dus gebruik deze niet in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="a0f7a-181">Hier volgt een gevulde uit voorbeeld Hallo dezelfde powershell.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-181">Here is a filled out example of hello same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="a0f7a-182">Zodra het Hallo-implementatie is voltooid, verbinding maken met behulp van tooyour-cluster Hallo nieuw certificaat en enkele query's uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-182">Once hello deployment is complete, connect tooyour cluster using hello new Certificate and perform some queries.</span></span> <span data-ttu-id="a0f7a-183">Als u kunnen toodo.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-183">If you are able toodo.</span></span> <span data-ttu-id="a0f7a-184">Vervolgens kunt u het oude certificaat Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-184">Then you can delete hello old certificate.</span></span> 

<span data-ttu-id="a0f7a-185">Als u een zelfondertekend certificaat gebruikt, vergeet niet tooimport bij uw lokale TrustedPeople-certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-185">If you are using a self-signed certificate, do not forget tooimport them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="a0f7a-186">Voor naslag is hier Hallo opdracht tooconnect tooa beveiligde cluster</span><span class="sxs-lookup"><span data-stu-id="a0f7a-186">For quick reference here is hello command tooconnect tooa secure cluster</span></span> 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
<span data-ttu-id="a0f7a-187">Voor naslag is hier Hallo opdracht tooget cluster status</span><span class="sxs-lookup"><span data-stu-id="a0f7a-187">For quick reference here is hello command tooget cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a><span data-ttu-id="a0f7a-188">Toepassing certificaten toohello-cluster implementeren.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-188">Deploying Application certificates toohello cluster.</span></span>

<span data-ttu-id="a0f7a-189">U kunt dezelfde stappen zoals wordt beschreven in stap 5 hierboven toohave Hallo certificaten op basis van een keyvault toohello knooppunten geïmplementeerd hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-189">You can use hello same steps as outlined in Steps 5 above toohave hello certificates deployed from a keyvault toohello Nodes.</span></span> <span data-ttu-id="a0f7a-190">u moet alleen definiëren en andere parameters gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="a0f7a-191">Het toevoegen of verwijderen van clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="a0f7a-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="a0f7a-192">U kunt in toevoeging toohello clustercertificaten, client certificaten tooperform beheerbewerkingen op een service fabric-cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-192">In addition toohello cluster certificates, you can add client certificates tooperform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="a0f7a-193">U kunt twee soorten clientcertificaten - beheerder toevoegen of alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="a0f7a-194">Deze kunnen vervolgens worden gebruikt toocontrol toegang toohello bewerkingen en zoekopdrachten op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-194">These then can be used toocontrol access toohello admin operations and Query operations on hello cluster.</span></span> <span data-ttu-id="a0f7a-195">Standaard worden clustercertificaten hello toohello Admin certificaten lijst met toegestane toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-195">By default, hello cluster certificates are added toohello allowed Admin certificates list.</span></span>

<span data-ttu-id="a0f7a-196">u kunt een willekeurig aantal clientcertificaten opgeven.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="a0f7a-197">Elke toevoeging/verwijdering resulteert in een configuratie update toohello service fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="a0f7a-197">Each addition/deletion results in a configuration update toohello service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="a0f7a-198">Clientcertificaten - beheerder toe te voegen of alleen-lezen via de portal</span><span class="sxs-lookup"><span data-stu-id="a0f7a-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="a0f7a-199">Navigeer toohello beveiliging blade en selecteer Hallo '+ verificatie' knop boven op Hallo beveiliging blade.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-199">Navigate toohello Security blade, and select hello '+ Authentication' button on top of hello security blade.</span></span>
2. <span data-ttu-id="a0f7a-200">Kies op de blade 'Authentication toevoegen' Hallo Hallo 'Verificatietype' - 'Client alleen-lezen' of 'Admin client'</span><span class="sxs-lookup"><span data-stu-id="a0f7a-200">On hello 'Add Authentication' blade, choose hello 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="a0f7a-201">Hallo-autorisatiemethode nu kiezen.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-201">Now choose hello Authorization method.</span></span> <span data-ttu-id="a0f7a-202">Dit tooService Fabric geeft aan of het opzoeken van dit certificaat met behulp van de onderwerpnaam Hallo of Hallo vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-202">This indicates tooService Fabric whether it should look up this certificate by using hello subject name or hello thumbprint.</span></span> <span data-ttu-id="a0f7a-203">Het is in het algemeen geen goed beveiligd practice toouse Hallo autorisatiemethode van de onderwerpnaam.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-203">In general, it is not a good security practice toouse hello authorization method of subject name.</span></span> 

![Clientcertificaat toevoegen][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a><span data-ttu-id="a0f7a-205">Verwijderen van clientcertificaten - beheer of met behulp van alleen-lezen Hallo portal</span><span class="sxs-lookup"><span data-stu-id="a0f7a-205">Deletion of Client Certificates - Admin or Read-Only using hello portal</span></span>

<span data-ttu-id="a0f7a-206">tooremove een secundair certificaat voor clusterbeveiliging, navigeren toohello beveiliging blade en selecteer Hallo 'Delete' optie in het contextmenu Hallo op Hallo specifiek certificaat kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a0f7a-206">tooremove a secondary certificate from being used for cluster security, Navigate toohello Security blade and select hello 'Delete' option from hello context menu on hello specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a0f7a-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0f7a-207">Next steps</span></span>
<span data-ttu-id="a0f7a-208">Lees deze artikelen voor meer informatie over het Clusterbeheer:</span><span class="sxs-lookup"><span data-stu-id="a0f7a-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="a0f7a-209">Het upgradeproces service Fabric-Cluster en de verwachtingen van u</span><span class="sxs-lookup"><span data-stu-id="a0f7a-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="a0f7a-210">Op rollen gebaseerde toegang instellen voor clients</span><span class="sxs-lookup"><span data-stu-id="a0f7a-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


