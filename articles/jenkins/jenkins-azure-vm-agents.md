---
title: Azure VM-agents gebruiken voor continue integratie met Jenkins
description: Azure VM-agents als Jenkins-slaves.
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 0b22a559fbc03158a6d4398603d1a7d2874d7b67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="b60db-103">Azure VM-agents gebruiken voor continue integratie met Jenkins</span><span class="sxs-lookup"><span data-stu-id="b60db-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="b60db-104">In deze Quickstart ziet u hoe u met de invoegtoepassing Jenkins Azure VM Agents een on-demand Linux-agent (Ubuntu) maakt in Azure.</span><span class="sxs-lookup"><span data-stu-id="b60db-104">This quickstart shows how to use the Jenkins Azure VM Agents plugin to create an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b60db-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b60db-105">Prerequisites</span></span>

<span data-ttu-id="b60db-106">Dit zijn de vereisten voor het voltooien van deze Quickstart:</span><span class="sxs-lookup"><span data-stu-id="b60db-106">To complete this quickstart:</span></span>

* <span data-ttu-id="b60db-107">Als u nog geen Jenkins-master hebt, kunt u beginnen met de [oplossingssjabloon](install-jenkins-solution-template.md).</span><span class="sxs-lookup"><span data-stu-id="b60db-107">If you do not already have a Jenkins master, you can start with the [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="b60db-108">Raadpleeg [Een Azure-service-principal maken met de Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) als u nog geen Azure-service-principal hebt.</span><span class="sxs-lookup"><span data-stu-id="b60db-108">Refer to [Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="b60db-109">Azure VM Agents-invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="b60db-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="b60db-110">Als u begint vanuit de [oplossingssjabloon](install-jenkins-solution-template.md), wordt de invoegtoepassing Azure VM Agents geïnstalleerd in de Jenkins-master.</span><span class="sxs-lookup"><span data-stu-id="b60db-110">If you start from the [Solution Template](install-jenkins-solution-template.md), the Azure VM Agent plugin is installed in the Jenkins master.</span></span>

<span data-ttu-id="b60db-111">Anders installeert u de**invoegtoepassing** vanuit het dashboard van Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b60db-111">Otherwise, install the **Azure VM Agents** plugin from within the Jenkins dashboard.</span></span>

## <a name="configure-the-plugin"></a><span data-ttu-id="b60db-112">De invoegtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="b60db-112">Configure the plugin</span></span>

* <span data-ttu-id="b60db-113">Klik in het dashboard van Jenkins op **Manage Jenkins -> Configure System ->**.</span><span class="sxs-lookup"><span data-stu-id="b60db-113">Within the Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="b60db-114">Ga naar de onderkant van de pagina en zoek de sectie met de vervolgkeuzelijst **Add new cloud**.</span><span class="sxs-lookup"><span data-stu-id="b60db-114">Scroll to the bottom of the page and find the section with the dropdown **Add new cloud**.</span></span> <span data-ttu-id="b60db-115">Selecteer **Microsoft Azure VM Agents** in de lijst.</span><span class="sxs-lookup"><span data-stu-id="b60db-115">From the menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="b60db-116">Selecteer een bestaand account in de vervolgkeuzelijst Azure Credentials.</span><span class="sxs-lookup"><span data-stu-id="b60db-116">Select an existing account from the Azure Credentials dropdown.</span></span>  <span data-ttu-id="b60db-117">Als u een nieuwe **Microsoft Azure-service-principal** wilt toevoegen, geeft u waarden op voor: Subscription ID, Client ID, Client Secret en OAuth 2.0 Token Endpoint.</span><span class="sxs-lookup"><span data-stu-id="b60db-117">To add a new **Microsoft Azure Service Principal,** enter the following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Azure-referenties](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="b60db-119">Klik op **Verify configuration** om er zeker van te zijn dat de configuratie juist is.</span><span class="sxs-lookup"><span data-stu-id="b60db-119">Click **Verify configuration** to make sure that the profile configuration is correct.</span></span>
* <span data-ttu-id="b60db-120">Sla de configuratie op en ga verder met de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="b60db-120">Save the configuration, and continue to the next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="b60db-121">Sjabloonconfiguratie</span><span class="sxs-lookup"><span data-stu-id="b60db-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="b60db-122">Algemene configuratie</span><span class="sxs-lookup"><span data-stu-id="b60db-122">General configuration</span></span>
<span data-ttu-id="b60db-123">Configureer vervolgens een sjabloon die u wilt gebruiken voor het definiëren van een Azure VM-agent.</span><span class="sxs-lookup"><span data-stu-id="b60db-123">Next, configure a template for use to define an Azure VM agent.</span></span> 

* <span data-ttu-id="b60db-124">Klik op **Add** om een sjabloon toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b60db-124">Click **Add** to add a template.</span></span> 
* <span data-ttu-id="b60db-125">Geef een naam op voor de nieuwe sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b60db-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="b60db-126">Voer voor het label 'ubuntu' in.</span><span class="sxs-lookup"><span data-stu-id="b60db-126">For the label, enter  "ubuntu."</span></span> <span data-ttu-id="b60db-127">Dit label wordt gebruikt tijdens de taakconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="b60db-127">This label is used during the job configuration.</span></span>
* <span data-ttu-id="b60db-128">Selecteer de gewenste regio in de keuzelijst met invoervak.</span><span class="sxs-lookup"><span data-stu-id="b60db-128">Select the desired region from the combo box.</span></span>
* <span data-ttu-id="b60db-129">Selecteer de gewenste grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b60db-129">Select the desired VM size.</span></span>
* <span data-ttu-id="b60db-130">Geef de naam van het Azure Storage-account op of laat het veld leeg als u de standaardnaam 'jenkinsarmst' wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b60db-130">Specify the Azure Storage account name or leave it blank to use the default name "jenkinsarmst."</span></span>
* <span data-ttu-id="b60db-131">Geef de bewaartijd in minuten op.</span><span class="sxs-lookup"><span data-stu-id="b60db-131">Specify the retention time in minutes.</span></span> <span data-ttu-id="b60db-132">Deze instelling bepaalt het aantal minuten dat Jenkins moet wachten voordat een niet-actieve agent automatisch wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b60db-132">This setting defines the number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="b60db-133">Geef 0 op om niet-actieve agents nooit te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b60db-133">Specify 0 if you do not want idle agents to be deleted automatically.</span></span>

![Algemene configuratie](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="b60db-135">Configuratie van installatiekopie</span><span class="sxs-lookup"><span data-stu-id="b60db-135">Image configuration</span></span>

<span data-ttu-id="b60db-136">Als u een Linux-agent (Ubuntu) wilt maken, selecteert u **Image reference** en gebruikt u de volgende configuratie als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b60db-136">To create a Linux (Ubuntu) agent, select **Image reference** and use the following configuration as an example.</span></span> <span data-ttu-id="b60db-137">Raadpleeg [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) voor de nieuwste ondersteunde Azure-installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="b60db-137">Refer to [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for the latest Azure supported images.</span></span>

* <span data-ttu-id="b60db-138">Image Publisher: Canonical</span><span class="sxs-lookup"><span data-stu-id="b60db-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="b60db-139">Image Offer: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="b60db-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="b60db-140">Image Sku: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="b60db-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="b60db-141">Image Version: latest</span><span class="sxs-lookup"><span data-stu-id="b60db-141">Image version: latest</span></span>
* <span data-ttu-id="b60db-142">OS Type: Linux</span><span class="sxs-lookup"><span data-stu-id="b60db-142">OS Type: Linux</span></span>
* <span data-ttu-id="b60db-143">Launch Method: SSH</span><span class="sxs-lookup"><span data-stu-id="b60db-143">Launch method: SSH</span></span>
* <span data-ttu-id="b60db-144">Voer referenties van een beheerder in</span><span class="sxs-lookup"><span data-stu-id="b60db-144">Provide an admin credentials</span></span>
* <span data-ttu-id="b60db-145">Voer het volgende in voor het script voor de initialisatie van virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="b60db-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuratie van installatiekopie](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="b60db-147">Klik op **Verify Template** om de configuratie te controleren.</span><span class="sxs-lookup"><span data-stu-id="b60db-147">Click **Verify Template** to verify the configuration.</span></span>
* <span data-ttu-id="b60db-148">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b60db-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="b60db-149">Een taak maken in Jenkins</span><span class="sxs-lookup"><span data-stu-id="b60db-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="b60db-150">Klik in het dashboard van Jenkins op **New Item**.</span><span class="sxs-lookup"><span data-stu-id="b60db-150">Within the Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="b60db-151">Voer een naam in, selecteer **Freestyle project** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b60db-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="b60db-152">Schakel op het tabblad **General** het selectievakje Restrict where this project can be run in en typ 'ubuntu' in het vak Label Expression.</span><span class="sxs-lookup"><span data-stu-id="b60db-152">In the **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="b60db-153">U ziet nu 'ubuntu' in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b60db-153">You now see "ubuntu" in the dropdown.</span></span>
* <span data-ttu-id="b60db-154">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b60db-154">Click **Save**.</span></span>

![Een taak instellen](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="b60db-156">Het nieuwe project bouwen</span><span class="sxs-lookup"><span data-stu-id="b60db-156">Build your new project</span></span>

* <span data-ttu-id="b60db-157">Ga terug naar het dashboard van Jenkins.</span><span class="sxs-lookup"><span data-stu-id="b60db-157">Go back to the Jenkins dashboard.</span></span>
* <span data-ttu-id="b60db-158">Klik met de rechtermuisknop op de nieuwe taak die u hebt gemaakt en klik vervolgens op **Build now**.</span><span class="sxs-lookup"><span data-stu-id="b60db-158">Right-click the new job you created, then click **Build now**.</span></span> <span data-ttu-id="b60db-159">De bewerking wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b60db-159">A build is kicked off.</span></span> 
* <span data-ttu-id="b60db-160">Zodra de bewerking is voltooid, gaat u naar **Console Output**.</span><span class="sxs-lookup"><span data-stu-id="b60db-160">Once the build is complete, go to **Console output**.</span></span> <span data-ttu-id="b60db-161">U ziet dat de bewerking op afstand is uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="b60db-161">You see that the build was performed remotely on Azure.</span></span>

![Console-uitvoer](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="b60db-163">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="b60db-163">Reference</span></span>

* <span data-ttu-id="b60db-164">Video van Azure Friday: [Continuous Integration with Jenkins Using Azure VM Agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Continue integratie met Jenkins met behulp van Azure VM-agents)</span><span class="sxs-lookup"><span data-stu-id="b60db-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="b60db-165">Ondersteuningsinformatie en configuratie-opties: de Engelstalige wiki van Jenkins [Azure VM Agents plugin](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="b60db-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

