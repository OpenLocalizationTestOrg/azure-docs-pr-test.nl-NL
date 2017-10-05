---
title: Het beheren van certificaten in een Azure Service Fabric-cluster | Microsoft Docs
description: Beschrijft hoe nieuwe certificaten, rollovercertificaat, toevoegen en verwijderen van certificaat naar of van een Service Fabric-cluster.
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
ms.openlocfilehash: c433e8683755e454f9561f094269c3daccf78a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a><span data-ttu-id="06830-103">Toevoegen of verwijderen van certificaten voor een Service Fabric-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="06830-103">Add or remove certificates for a Service Fabric cluster in Azure</span></span>
<span data-ttu-id="06830-104">Het is raadzaam dat u raken met het Service Fabric X.509-certificaten gebruikt en vertrouwd met zijn de [security scenario's](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="06830-104">It is recommended that you familiarize yourself with how Service Fabric uses X.509 certificates and be familiar with the [Cluster security scenarios](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="06830-105">U moet begrijpen wat een certificaat in het cluster is en wat wordt gebruikt voor, voordat u verder.</span><span class="sxs-lookup"><span data-stu-id="06830-105">You must understand what a cluster certificate is and what is used for, before you proceed further.</span></span>

<span data-ttu-id="06830-106">Het service fabric kunt u twee clustercertificaten, een primaire en een secundaire opgeven bij het configureren van Certificaatbeveiliging tijdens het maken van het cluster naast clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="06830-106">Service fabric lets you specify two cluster certificates, a primary and a secondary, when you configure certificate security during cluster creation, in addition to client certificates.</span></span> <span data-ttu-id="06830-107">Raadpleeg [maken van een azure-cluster via de portal](service-fabric-cluster-creation-via-portal.md) of [maken van een azure-cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) voor meer informatie over het instellen op voor het maken.</span><span class="sxs-lookup"><span data-stu-id="06830-107">Refer to [creating an azure cluster via portal](service-fabric-cluster-creation-via-portal.md) or [creating an azure cluster via Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) for details on setting them up at create time.</span></span> <span data-ttu-id="06830-108">Als u slechts één cluster certificaat opgeeft op voor het maken, klikt u vervolgens die wordt gebruikt als het primaire certificaat.</span><span class="sxs-lookup"><span data-stu-id="06830-108">If you specify only one cluster certificate at create time, then that is used as the primary certificate.</span></span> <span data-ttu-id="06830-109">U kunt een nieuw certificaat na het maken van het cluster toevoegen als een secundaire database.</span><span class="sxs-lookup"><span data-stu-id="06830-109">After cluster creation, you can add a new certificate as a secondary.</span></span>

> [!NOTE]
> <span data-ttu-id="06830-110">Voor een beveiligde cluster moet altijd u ten minste één geldig (niet ingetrokken en niet verlopen)-cluster certificaat (primair of secundair) dat is geïmplementeerd (zo niet, de cluster stopt werkt).</span><span class="sxs-lookup"><span data-stu-id="06830-110">For a secure cluster, you will always need at least one valid (not revoked and not expired) cluster certificate (primary or secondary) deployed (if not, the cluster stops functioning).</span></span> <span data-ttu-id="06830-111">90 dagen voordat alle geldige certificaten verlopen, bereikt het systeem genereert een waarschuwing trace en ook een waarschuwingsgebeurtenis status op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="06830-111">90 days before all valid certificates reach expiration, the system generates a warning trace and also a warning health event on the node.</span></span> <span data-ttu-id="06830-112">Er is momenteel geen e-mail of andere berichten naar service fabric worden verzonden over dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="06830-112">There is currently no email or any other notification that service fabric sends out on this topic.</span></span> 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-the-portal"></a><span data-ttu-id="06830-113">Een secundaire cluster certificaat via de portal toevoegen</span><span class="sxs-lookup"><span data-stu-id="06830-113">Add a secondary cluster certificate using the portal</span></span>

<span data-ttu-id="06830-114">Secundaire cluster certificaat kan niet worden toegevoegd via de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="06830-114">Secondary cluster certificate cannot be added through the Azure portal.</span></span> <span data-ttu-id="06830-115">U moet Azure powershell gebruiken voor die.</span><span class="sxs-lookup"><span data-stu-id="06830-115">You have to use Azure powershell for that.</span></span> <span data-ttu-id="06830-116">Het proces wordt verderop in dit document beschreven.</span><span class="sxs-lookup"><span data-stu-id="06830-116">The process is outlined later in this document.</span></span>

## <a name="swap-the-cluster-certificates-using-the-portal"></a><span data-ttu-id="06830-117">Wisselen van de clustercertificaten met behulp van de portal</span><span class="sxs-lookup"><span data-stu-id="06830-117">Swap the cluster certificates using the portal</span></span>

<span data-ttu-id="06830-118">Nadat u hebt een certificaat secundaire cluster is geïmplementeerd als u wilt wisselen van de primaire en secundaire, Ga naar de blade beveiliging en selecteer de optie 'Wisseling met primaire' in het contextmenu wisselen van de secundaire cert met het primaire certificaat.</span><span class="sxs-lookup"><span data-stu-id="06830-118">After you have successfully deployed a secondary cluster certificate, if you want to swap the primary and secondary, then navigate to the Security blade, and select the 'Swap with primary' option from the context menu to swap the secondary cert with the primary cert.</span></span>

![Swap-certificaat][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-the-portal"></a><span data-ttu-id="06830-120">Het certificaat voor een cluster met behulp van de portal verwijderen</span><span class="sxs-lookup"><span data-stu-id="06830-120">Remove a cluster certificate using the portal</span></span>

<span data-ttu-id="06830-121">Voor een beveiligde cluster, moet u altijd ten minste één geldig (niet ingetrokken en niet verlopen)-certificaat (primair of secundair) geïmplementeerd zo niet, het cluster niet meer werkt.</span><span class="sxs-lookup"><span data-stu-id="06830-121">For a secure cluster, you will always need at least one valid (not revoked and not expired) certificate (primary or secondary) deployed if not, the cluster stops functioning.</span></span>

<span data-ttu-id="06830-122">Een secundair certificaat worden gebruikt voor een clusterbeveiliging navigeren naar de blade beveiliging verwijderen en selecteer de optie 'Verwijderen' in het contextmenu op de secundaire certificaat.</span><span class="sxs-lookup"><span data-stu-id="06830-122">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the secondary certificate.</span></span>

<span data-ttu-id="06830-123">Als uw bedoeling is om het certificaat dat is gemarkeerd als primaire verwijderen, wordt moet u eerst met de secundaire uitwisselen, en verwijder vervolgens de secundaire nadat de upgrade is voltooid.</span><span class="sxs-lookup"><span data-stu-id="06830-123">If your intent is to remove the certificate that is marked primary, then you will need to swap it with the secondary first, and then delete the secondary after the upgrade has completed.</span></span>

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a><span data-ttu-id="06830-124">Toevoegen van een secundair certificaat met behulp van Resource Manager Powershell</span><span class="sxs-lookup"><span data-stu-id="06830-124">Add a secondary certificate using Resource Manager Powershell</span></span>

<span data-ttu-id="06830-125">Deze stappen wordt ervan uitgegaan dat bekend bent met de werking van Resource Manager en moet ten minste één Service Fabric-cluster met een Resource Manager-sjabloon hebt geïmplementeerd en de sjabloon die u gebruikt voor het instellen van het cluster bij de hand hebt.</span><span class="sxs-lookup"><span data-stu-id="06830-125">These steps assume that you are familiar with how Resource Manager works and have deployed atleast one Service Fabric cluster using a Resource Manager template, and have the template that you used to set up the cluster handy.</span></span> <span data-ttu-id="06830-126">Ook wordt ervan uitgegaan dat u vertrouwd met een JSON bent.</span><span class="sxs-lookup"><span data-stu-id="06830-126">It is also assumed that you are comfortable using JSON.</span></span>

> [!NOTE]
> <span data-ttu-id="06830-127">Als u zoekt naar een voorbeeldsjabloon en parameters die u kunt volgen langs of als uitgangspunt, klikt u vervolgens het downloaden van deze [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="06830-127">If you are looking for a sample template and parameters that you can use to follow along or as a starting point, then download it from this [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span> 
> 
> 

### <a name="edit-your-resource-manager-template"></a><span data-ttu-id="06830-128">De Resource Manager-sjabloon bewerken</span><span class="sxs-lookup"><span data-stu-id="06830-128">Edit your Resource Manager template</span></span>

<span data-ttu-id="06830-129">Voorbeeld 5-VM-1-NodeTypes-Secure_Step2.JSON bevat voor een eenvoudige van volgende langs alle bewerkingen we brengen.</span><span class="sxs-lookup"><span data-stu-id="06830-129">For ease of following along, sample 5-VM-1-NodeTypes-Secure_Step2.JSON contains all the edits we will be making.</span></span> <span data-ttu-id="06830-130">het voorbeeld is beschikbaar op [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span><span class="sxs-lookup"><span data-stu-id="06830-130">the sample is available at [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).</span></span>

<span data-ttu-id="06830-131">**Zorg ervoor dat u alle stappen**</span><span class="sxs-lookup"><span data-stu-id="06830-131">**Make sure to follow all the steps**</span></span>

<span data-ttu-id="06830-132">**Stap 1:** Open de Resource Manager-sjabloon die u hebt gebruikt voor het implementeren van Cluster.</span><span class="sxs-lookup"><span data-stu-id="06830-132">**Step 1:** Open up the Resource Manager template you used to deploy you Cluster.</span></span> <span data-ttu-id="06830-133">(Als u het voorbeeld hebt gedownload uit de bovenstaande opslagplaats, 5-VM-1-NodeTypes-Secure_Step1.JSON vervolgens gebruiken voor het implementeren van een beveiligde cluster en vervolgens opent u dat de sjabloon).</span><span class="sxs-lookup"><span data-stu-id="06830-133">(If you have downloaded the sample from the above repo, then Use 5-VM-1-NodeTypes-Secure_Step1.JSON to deploy a secure cluster and then open up that template).</span></span>

<span data-ttu-id="06830-134">**Stap 2:** toevoegen **twee nieuwe parameters** 'secCertificateThumbprint' en 'secCertificateUrlValue' van type 'tekenreeks' aan de parametersectie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="06830-134">**Step 2:** Add **two new parameters** "secCertificateThumbprint" and "secCertificateUrlValue" of type "string" to the parameter section of your template.</span></span> <span data-ttu-id="06830-135">U kunt het volgende codefragment kopiëren en toevoegen aan de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="06830-135">You can copy the following code snippet and add it to the template.</span></span> <span data-ttu-id="06830-136">Afhankelijk van de bron van uw sjabloon mogelijk hebt u al deze gedefinieerd als dus verplaatsen naar de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="06830-136">Depending on the source of your template, you may already have these defined, if so move to the next step.</span></span> 
 
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
        "description": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

<span data-ttu-id="06830-137">**Stap 3:** wijzigingen aanbrengen in de **Microsoft.ServiceFabric/clusters** resource - de resourcedefinitie 'Microsoft.ServiceFabric/clusters' niet vinden in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="06830-137">**Step 3:** Make changes to the **Microsoft.ServiceFabric/clusters** resource - Locate the "Microsoft.ServiceFabric/clusters" resource definition in your template.</span></span> <span data-ttu-id="06830-138">Onder de eigenschappen van deze definitie van vindt u 'Certificaat' JSON tag, die u moet er ongeveer als de volgende JSON-fragment:</span><span class="sxs-lookup"><span data-stu-id="06830-138">Under properties of that definition, you will find "Certificate" JSON tag, which should look something like the following JSON snippet:</span></span>

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="06830-139">Voeg een nieuwe tag 'thumbprintSecondary' en hieraan een waarde '[parameters('secCertificateThumbprint')]'.</span><span class="sxs-lookup"><span data-stu-id="06830-139">Add a new tag "thumbprintSecondary" and give it a value "[parameters('secCertificateThumbprint')]".</span></span>  

<span data-ttu-id="06830-140">In dat geval nu de resourcedefinitie als in de volgende eruitzien moet (afhankelijk van de bron van de sjabloon niet mogelijk precies zoals het onderstaande codefragment).</span><span class="sxs-lookup"><span data-stu-id="06830-140">So now the resource definition should look like the following (depending on your source of the template, it may not be exactly like the snippet below).</span></span> 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

<span data-ttu-id="06830-141">Als u wilt **rollover van het certificaat**, geef het nieuwe certificaat als primaire en de huidige primaire als secundaire verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="06830-141">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="06830-142">Dit resulteert in de overschakeling van uw huidige primaire certificaat voor het nieuwe certificaat in één stap van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="06830-142">This results in the rollover of your current primary certificate to the new certificate in one deployment step.</span></span>

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


<span data-ttu-id="06830-143">**Stap 4:** wijzigingen aanbrengen in **alle** de **Microsoft.Compute/virtualMachineScaleSets** resourcedefinities - de bron Microsoft.Compute/virtualMachineScaleSets gevonden definitie.</span><span class="sxs-lookup"><span data-stu-id="06830-143">**Step 4:** Make changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="06830-144">Blader naar de 'publisher': 'Microsoft.Azure.ServiceFabric' onder 'virtualMachineProfile'.</span><span class="sxs-lookup"><span data-stu-id="06830-144">Scroll to the "publisher": "Microsoft.Azure.ServiceFabric", under "virtualMachineProfile".</span></span>

<span data-ttu-id="06830-145">In de instellingen voor service fabric publisher ziet u er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="06830-145">In the service fabric publisher settings, you should see something like this.</span></span>

![Json_Pub_Setting1][Json_Pub_Setting1]

<span data-ttu-id="06830-147">Voeg de nieuwe cert vermeldingen toe</span><span class="sxs-lookup"><span data-stu-id="06830-147">Add the new cert entries to it</span></span>

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

<span data-ttu-id="06830-148">De eigenschappen ziet er nu als volgt</span><span class="sxs-lookup"><span data-stu-id="06830-148">The properties should now look like this</span></span>

![Json_Pub_Setting2][Json_Pub_Setting2]

<span data-ttu-id="06830-150">Als u wilt **rollover van het certificaat**, geef het nieuwe certificaat als primaire en de huidige primaire als secundaire verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="06830-150">If you want to **rollover the cert**, then specify the new cert as primary and moving the current primary as secondary.</span></span> <span data-ttu-id="06830-151">Dit resulteert in de overschakeling van uw huidige certificaat naar het nieuwe certificaat in één stap van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="06830-151">This results in the rollover of your current certificate to the new certificate in one deployment step.</span></span> 


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
<span data-ttu-id="06830-152">De eigenschappen ziet er nu als volgt</span><span class="sxs-lookup"><span data-stu-id="06830-152">The properties should now look like this</span></span>

![Json_Pub_Setting3][Json_Pub_Setting3]


<span data-ttu-id="06830-154">**Stap 5:** wijzigingen aanbrengen in **alle** de **Microsoft.Compute/virtualMachineScaleSets** resourcedefinities - de bron Microsoft.Compute/virtualMachineScaleSets gevonden definitie.</span><span class="sxs-lookup"><span data-stu-id="06830-154">**Step 5:** Make Changes to **all** the **Microsoft.Compute/virtualMachineScaleSets** resource definitions - Locate the Microsoft.Compute/virtualMachineScaleSets resource definition.</span></span> <span data-ttu-id="06830-155">Blader naar de 'vaultCertificates':, onder 'OSProfile'.</span><span class="sxs-lookup"><span data-stu-id="06830-155">Scroll to the "vaultCertificates": , under "OSProfile".</span></span> <span data-ttu-id="06830-156">Dit ziet er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="06830-156">it should look something like this.</span></span>


![Json_Pub_Setting4][Json_Pub_Setting4]

<span data-ttu-id="06830-158">De secCertificateUrlValue aan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="06830-158">Add the secCertificateUrlValue to it.</span></span> <span data-ttu-id="06830-159">Gebruik het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="06830-159">use the following snippet:</span></span>

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
<span data-ttu-id="06830-160">Nu ziet de resulterende Json er ongeveer als volgt.</span><span class="sxs-lookup"><span data-stu-id="06830-160">Now the resulting Json should look something like this.</span></span>
<span data-ttu-id="06830-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span><span class="sxs-lookup"><span data-stu-id="06830-161">![Json_Pub_Setting5][Json_Pub_Setting5]</span></span>


> [!NOTE]
> <span data-ttu-id="06830-162">Zorg ervoor dat u stap 4 en 5 voor de definities voor de resource Nodetypes/Microsoft.Compute/virtualMachineScaleSets hebben herhaald in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="06830-162">Make sure that you have repeated steps 4 and 5 for all the Nodetypes/Microsoft.Compute/virtualMachineScaleSets resource definitions in your template.</span></span> <span data-ttu-id="06830-163">Als u een van beide mist, wordt het certificaat niet geïnstalleerd op dat VMSS u onvoorspelbare resultaten in het cluster hebt, met inbegrip van het cluster tijdelijk niet beschikbaar (als u uiteindelijk geen geldige certificaten die de cluster voor beveiliging gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="06830-163">If you miss one of them, the certificate will not get installed on that VMSS and you will have unpredictable results in your cluster, including the cluster going down (if you end up with no valid certificates that the cluster can use for security.</span></span> <span data-ttu-id="06830-164">Zo Controleer, voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="06830-164">So please double check, before proceeding further.</span></span>
> 
> 


### <a name="edit-your-template-file-to-reflect-the-new-parameters-you-added-above"></a><span data-ttu-id="06830-165">Bewerk het sjabloonbestand zodat de nieuwe parameters die u hebt toegevoegd</span><span class="sxs-lookup"><span data-stu-id="06830-165">Edit your template file to reflect the new parameters you added above</span></span>
<span data-ttu-id="06830-166">Als u het voorbeeld van de [git-opslagplaats](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) als u wilt volgen, kunt u beginnen met wijzigingen aanbrengen in het voorbeeld 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span><span class="sxs-lookup"><span data-stu-id="06830-166">If you are using the sample from the [git-repo](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) to follow along, you can start to make changes in The sample 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON</span></span> 

<span data-ttu-id="06830-167">De parameter-bestand voor uw Resource Manager-sjabloon bewerken, de twee nieuwe parameters voor secCertificateThumbprint en secCertificateUrlValue toevoegen.</span><span class="sxs-lookup"><span data-stu-id="06830-167">Edit your Resource Manager Template parameter File, add the two new parameters for secCertificateThumbprint and secCertificateUrlValue.</span></span> 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers to the location URL in your key vault where the certificate was uploaded, it is should be in the format of https://<name of the vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-the-template-to-azure"></a><span data-ttu-id="06830-168">De sjabloon te implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="06830-168">Deploy the template to Azure</span></span>

- <span data-ttu-id="06830-169">U bent nu klaar voor het implementeren van uw sjabloon naar Azure.</span><span class="sxs-lookup"><span data-stu-id="06830-169">You are now ready to deploy your template to Azure.</span></span> <span data-ttu-id="06830-170">Open een opdrachtprompt voor Azure PS-versie 1 +.</span><span class="sxs-lookup"><span data-stu-id="06830-170">Open an Azure PS version 1+ command prompt.</span></span>
- <span data-ttu-id="06830-171">Aanmelden bij uw Azure-Account en selecteer de specifieke azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="06830-171">Log in to your Azure Account and select the specific azure subscription.</span></span> <span data-ttu-id="06830-172">Dit is een belangrijke stap voor mensen die toegang tot meer dan één azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="06830-172">This is an important step for folks who have access to more than one azure subscription.</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

<span data-ttu-id="06830-173">Test de sjabloon voordat deze is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="06830-173">Test the template prior to deploying it.</span></span> <span data-ttu-id="06830-174">Gebruik dezelfde resourcegroep die uw cluster wordt momenteel geïmplementeerd op.</span><span class="sxs-lookup"><span data-stu-id="06830-174">Use the same Resource Group that your cluster is currently deployed to.</span></span>

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

<span data-ttu-id="06830-175">Implementeer de sjabloon in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="06830-175">Deploy the template to your resource group.</span></span> <span data-ttu-id="06830-176">Gebruik dezelfde resourcegroep die uw cluster wordt momenteel geïmplementeerd op.</span><span class="sxs-lookup"><span data-stu-id="06830-176">Use the same Resource Group that your cluster is currently deployed to.</span></span> <span data-ttu-id="06830-177">Voer de opdracht New-AzureRmResourceGroupDeployment.</span><span class="sxs-lookup"><span data-stu-id="06830-177">Run the New-AzureRmResourceGroupDeployment command.</span></span> <span data-ttu-id="06830-178">U hoeft niet te geven de modus, aangezien de standaardwaarde is **incrementele**.</span><span class="sxs-lookup"><span data-stu-id="06830-178">You do not need to specify the mode, since the default value is **incremental**.</span></span>

> [!NOTE]
> <span data-ttu-id="06830-179">Als u de modus op voltooid instellen, kunt u resources die zich niet in uw sjabloon per ongeluk verwijderen.</span><span class="sxs-lookup"><span data-stu-id="06830-179">If you set Mode to Complete, you can inadvertently delete resources that are not in your template.</span></span> <span data-ttu-id="06830-180">Dus gebruik deze niet in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="06830-180">So do not use it in this scenario.</span></span>
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

<span data-ttu-id="06830-181">Hier volgt een voorbeeld van een ingevuld van de dezelfde powershell.</span><span class="sxs-lookup"><span data-stu-id="06830-181">Here is a filled out example of the same powershell.</span></span>

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

<span data-ttu-id="06830-182">Zodra de implementatie voltooid is, verbinding maken met uw cluster met behulp van het nieuwe certificaat en enkele query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="06830-182">Once the deployment is complete, connect to your cluster using the new Certificate and perform some queries.</span></span> <span data-ttu-id="06830-183">Als u kunnen doen bent.</span><span class="sxs-lookup"><span data-stu-id="06830-183">If you are able to do.</span></span> <span data-ttu-id="06830-184">Vervolgens kunt u het oude certificaat verwijderen.</span><span class="sxs-lookup"><span data-stu-id="06830-184">Then you can delete the old certificate.</span></span> 

<span data-ttu-id="06830-185">Als u een zelfondertekend certificaat gebruikt, vergeet niet om te importeren in uw lokale TrustedPeople-certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="06830-185">If you are using a self-signed certificate, do not forget to import them into your local TrustedPeople cert store.</span></span>

```powershell
######## Set up the certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
<span data-ttu-id="06830-186">Voor snelle naslag hier is de opdracht verbinding maken met een beveiligde cluster</span><span class="sxs-lookup"><span data-stu-id="06830-186">For quick reference here is the command to connect to a secure cluster</span></span> 

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
<span data-ttu-id="06830-187">Voor snelle naslag hier is de opdracht cluster health ophalen</span><span class="sxs-lookup"><span data-stu-id="06830-187">For quick reference here is the command to get cluster health</span></span>

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-to-the-cluster"></a><span data-ttu-id="06830-188">Implementatie van certificaten van de toepassing aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="06830-188">Deploying Application certificates to the cluster.</span></span>

<span data-ttu-id="06830-189">U kunt dezelfde stappen gebruiken zoals wordt beschreven in stap 5 hierboven om de certificaten die aan de knooppunten van een keyvault is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="06830-189">You can use the same steps as outlined in Steps 5 above to have the certificates deployed from a keyvault to the Nodes.</span></span> <span data-ttu-id="06830-190">u moet alleen definiëren en andere parameters gebruikt.</span><span class="sxs-lookup"><span data-stu-id="06830-190">you just need define and use different parameters.</span></span>


## <a name="adding-or-removing-client-certificates"></a><span data-ttu-id="06830-191">Het toevoegen of verwijderen van clientcertificaten</span><span class="sxs-lookup"><span data-stu-id="06830-191">Adding or removing Client certificates</span></span>

<span data-ttu-id="06830-192">Naast de clustercertificaten, kunt u clientcertificaten voor het uitvoeren van beheerbewerkingen op een service fabric-cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="06830-192">In addition to the cluster certificates, you can add client certificates to perform management operations on a service fabric cluster.</span></span>

<span data-ttu-id="06830-193">U kunt twee soorten clientcertificaten - beheerder toevoegen of alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="06830-193">You can add two kinds of client certificates - Admin or Read-only.</span></span> <span data-ttu-id="06830-194">Deze kunnen vervolgens worden gebruikt om toegang aan de bewerkingen en zoekopdrachten op het cluster te beheren.</span><span class="sxs-lookup"><span data-stu-id="06830-194">These then can be used to control access to the admin operations and Query operations on the cluster.</span></span> <span data-ttu-id="06830-195">Standaard worden de clustercertificaten toegevoegd aan de lijst met toegestane Admin certificaten.</span><span class="sxs-lookup"><span data-stu-id="06830-195">By default, the cluster certificates are added to the allowed Admin certificates list.</span></span>

<span data-ttu-id="06830-196">u kunt een willekeurig aantal clientcertificaten opgeven.</span><span class="sxs-lookup"><span data-stu-id="06830-196">you can specify any number of client certificates.</span></span> <span data-ttu-id="06830-197">Elke toevoeging/verwijdering resulteert in een configuratie-update met de service fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="06830-197">Each addition/deletion results in a configuration update to the service fabric cluster</span></span>


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a><span data-ttu-id="06830-198">Clientcertificaten - beheerder toe te voegen of alleen-lezen via de portal</span><span class="sxs-lookup"><span data-stu-id="06830-198">Adding client certificates - Admin or Read-Only via portal</span></span>

1. <span data-ttu-id="06830-199">Navigeer naar de blade beveiliging en selecteer de '+ verificatie' knop boven op het tabblad Beveiliging.</span><span class="sxs-lookup"><span data-stu-id="06830-199">Navigate to the Security blade, and select the '+ Authentication' button on top of the security blade.</span></span>
2. <span data-ttu-id="06830-200">Kies op de blade 'Authentication toevoegen' het 'verificatietype' - 'Client alleen-lezen' of 'Admin client'</span><span class="sxs-lookup"><span data-stu-id="06830-200">On the 'Add Authentication' blade, choose the 'Authentication Type' - 'Read-only client' or 'Admin client'</span></span>
3. <span data-ttu-id="06830-201">Kies nu de autorisatie-methode.</span><span class="sxs-lookup"><span data-stu-id="06830-201">Now choose the Authorization method.</span></span> <span data-ttu-id="06830-202">Hiermee geeft u aan de Service Fabric of het opzoeken van dit certificaat met behulp van de onderwerpnaam of de vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="06830-202">This indicates to Service Fabric whether it should look up this certificate by using the subject name or the thumbprint.</span></span> <span data-ttu-id="06830-203">Het is in het algemeen niet verstandig uit veiligheidsoverwegingen met de autorisatiemethode van de onderwerpnaam.</span><span class="sxs-lookup"><span data-stu-id="06830-203">In general, it is not a good security practice to use the authorization method of subject name.</span></span> 

![Clientcertificaat toevoegen][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-the-portal"></a><span data-ttu-id="06830-205">Verwijderen van clientcertificaten - beheer of alleen-lezen met behulp van de portal</span><span class="sxs-lookup"><span data-stu-id="06830-205">Deletion of Client Certificates - Admin or Read-Only using the portal</span></span>

<span data-ttu-id="06830-206">Een secundair certificaat worden gebruikt voor een clusterbeveiliging navigeren naar de blade beveiliging verwijderen en selecteer de optie 'Verwijderen' in het contextmenu op de specifieke certificaat.</span><span class="sxs-lookup"><span data-stu-id="06830-206">To remove a secondary certificate from being used for cluster security, Navigate to the Security blade and select the 'Delete' option from the context menu on the specific certificate.</span></span>



## <a name="next-steps"></a><span data-ttu-id="06830-207">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="06830-207">Next steps</span></span>
<span data-ttu-id="06830-208">Lees deze artikelen voor meer informatie over het Clusterbeheer:</span><span class="sxs-lookup"><span data-stu-id="06830-208">Read these articles for more information on cluster management:</span></span>

* [<span data-ttu-id="06830-209">Het upgradeproces service Fabric-Cluster en de verwachtingen van u</span><span class="sxs-lookup"><span data-stu-id="06830-209">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="06830-210">Op rollen gebaseerde toegang instellen voor clients</span><span class="sxs-lookup"><span data-stu-id="06830-210">Setup role-based access for clients</span></span>](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


