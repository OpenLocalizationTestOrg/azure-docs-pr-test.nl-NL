---
title: voor continue integratie met Jenkins aaaUse Azure VM-agents.
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
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a><span data-ttu-id="e8ff2-103">Azure VM-agents gebruiken voor continue integratie met Jenkins</span><span class="sxs-lookup"><span data-stu-id="e8ff2-103">Use Azure VM agents for continuous integration with Jenkins.</span></span>

<span data-ttu-id="e8ff2-104">Deze snelstartgids ziet u hoe toouse Hallo Jenkins Azure VM Agents invoegtoepassing toocreate een agent op aanvraag Linux (Ubuntu) in Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-104">This quickstart shows how toouse hello Jenkins Azure VM Agents plugin toocreate an on-demand Linux (Ubuntu) agent in Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8ff2-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e8ff2-105">Prerequisites</span></span>

<span data-ttu-id="e8ff2-106">toocomplete deze snelstartgids:</span><span class="sxs-lookup"><span data-stu-id="e8ff2-106">toocomplete this quickstart:</span></span>

* <span data-ttu-id="e8ff2-107">Als u nog geen een model Jenkins, kunt u beginnen met Hallo [oplossingssjabloon](install-jenkins-solution-template.md)</span><span class="sxs-lookup"><span data-stu-id="e8ff2-107">If you do not already have a Jenkins master, you can start with hello [Solution Template](install-jenkins-solution-template.md)</span></span> 
* <span data-ttu-id="e8ff2-108">Raadpleeg te[een Azure-Service-principal maken met Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) als u nog geen een Azure-service-principal.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-108">Refer too[Create an Azure Service principal with Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) if you do not already have an Azure service principal.</span></span>

## <a name="install-azure-vm-agents-plugin"></a><span data-ttu-id="e8ff2-109">Azure VM Agents-invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="e8ff2-109">Install Azure VM Agents plugin</span></span>

<span data-ttu-id="e8ff2-110">Als u vanaf Hallo [oplossingssjabloon](install-jenkins-solution-template.md), hello Azure VM-Agent-invoegtoepassing is geïnstalleerd in de Hallo Jenkins master.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-110">If you start from hello [Solution Template](install-jenkins-solution-template.md), hello Azure VM Agent plugin is installed in hello Jenkins master.</span></span>

<span data-ttu-id="e8ff2-111">Anders installeert Hallo **Azure VM Agents** invoegtoepassing uit binnen Hallo Jenkins dashboard.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-111">Otherwise, install hello **Azure VM Agents** plugin from within hello Jenkins dashboard.</span></span>

## <a name="configure-hello-plugin"></a><span data-ttu-id="e8ff2-112">Hallo-invoegtoepassing configureren</span><span class="sxs-lookup"><span data-stu-id="e8ff2-112">Configure hello plugin</span></span>

* <span data-ttu-id="e8ff2-113">Klik in het Hallo Jenkins dashboard op **Jenkins beheren -> systeem configureren ->**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-113">Within hello Jenkins dashboard, click **Manage Jenkins -> Configure System ->**.</span></span> <span data-ttu-id="e8ff2-114">Schuif toohello onder aan de pagina Hallo en Hallo sectie met Hallo dropdown zoeken **toevoegen van nieuwe cloud**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-114">Scroll toohello bottom of hello page and find hello section with hello dropdown **Add new cloud**.</span></span> <span data-ttu-id="e8ff2-115">Hallo-menu en selecteer **Microsoft Azure VM-Agents**</span><span class="sxs-lookup"><span data-stu-id="e8ff2-115">From hello menu, select **Microsoft Azure VM Agents**</span></span>
* <span data-ttu-id="e8ff2-116">Selecteer een bestaand account in hello Azure-referenties vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-116">Select an existing account from hello Azure Credentials dropdown.</span></span>  <span data-ttu-id="e8ff2-117">tooadd een nieuwe **Microsoft Azure Service-Principal** Hallo waarden volgende invoeren: abonnements-ID, Client-ID, Client Secret en OAuth 2.0-Tokeneindpunt.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-117">tooadd a new **Microsoft Azure Service Principal,** enter hello following values: Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span>

![Azure-referenties](./media/jenkins-azure-vm-agents/service-principal.png)

* <span data-ttu-id="e8ff2-119">Klik op **controleren configuratie** toomake of die Hallo profielconfiguratie juist is.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-119">Click **Verify configuration** toomake sure that hello profile configuration is correct.</span></span>
* <span data-ttu-id="e8ff2-120">Hallo-configuratie op te slaan en verder toohello volgende stap.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-120">Save hello configuration, and continue toohello next step.</span></span>

## <a name="template-configuration"></a><span data-ttu-id="e8ff2-121">Sjabloonconfiguratie</span><span class="sxs-lookup"><span data-stu-id="e8ff2-121">Template configuration</span></span>

### <a name="general-configuration"></a><span data-ttu-id="e8ff2-122">Algemene configuratie</span><span class="sxs-lookup"><span data-stu-id="e8ff2-122">General configuration</span></span>
<span data-ttu-id="e8ff2-123">Configureer vervolgens een sjabloon voor gebruik toodefine een Azure VM-agent.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-123">Next, configure a template for use toodefine an Azure VM agent.</span></span> 

* <span data-ttu-id="e8ff2-124">Klik op **toevoegen** tooadd een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-124">Click **Add** tooadd a template.</span></span> 
* <span data-ttu-id="e8ff2-125">Geef een naam op voor de nieuwe sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-125">Provide a name for your new template.</span></span> 
* <span data-ttu-id="e8ff2-126">Voer voor Hallo-label "ubuntu."</span><span class="sxs-lookup"><span data-stu-id="e8ff2-126">For hello label, enter  "ubuntu."</span></span> <span data-ttu-id="e8ff2-127">Dit label wordt gebruikt tijdens het Hallo taak configureren.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-127">This label is used during hello job configuration.</span></span>
* <span data-ttu-id="e8ff2-128">Selecteer de gewenste regio Hallo in Hallo keuzelijst met invoervak.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-128">Select hello desired region from hello combo box.</span></span>
* <span data-ttu-id="e8ff2-129">Selecteer Hallo gewenste VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-129">Select hello desired VM size.</span></span>
* <span data-ttu-id="e8ff2-130">Geef hello Azure Storage-accountnaam of laat dit leeg toouse Hallo standaardnaam 'jenkinsarmst'.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-130">Specify hello Azure Storage account name or leave it blank toouse hello default name "jenkinsarmst."</span></span>
* <span data-ttu-id="e8ff2-131">Geef de bewaartijd Hallo in minuten.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-131">Specify hello retention time in minutes.</span></span> <span data-ttu-id="e8ff2-132">Deze instelling bepaalt Hallo aantal minuten die jenkins wachten kunt voordat u een niet-actieve agent automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-132">This setting defines hello number of minutes Jenkins can wait before automatically deleting an idle agent.</span></span> <span data-ttu-id="e8ff2-133">Geef 0 als u niet dat niet-actieve agents toobe automatisch verwijderd wilt.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-133">Specify 0 if you do not want idle agents toobe deleted automatically.</span></span>

![Algemene configuratie](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a><span data-ttu-id="e8ff2-135">Configuratie van installatiekopie</span><span class="sxs-lookup"><span data-stu-id="e8ff2-135">Image configuration</span></span>

<span data-ttu-id="e8ff2-136">Selecteer toocreate (Ubuntu) Linux-agent **verwijzing afbeelding** en gebruik Hallo configuratie als een voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-136">toocreate a Linux (Ubuntu) agent, select **Image reference** and use hello following configuration as an example.</span></span> <span data-ttu-id="e8ff2-137">Raadpleeg te[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) voor Hallo meest recente Azure installatiekopieën ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-137">Refer too[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) for hello latest Azure supported images.</span></span>

* <span data-ttu-id="e8ff2-138">Image Publisher: Canonical</span><span class="sxs-lookup"><span data-stu-id="e8ff2-138">Image Publisher: Canonical</span></span>
* <span data-ttu-id="e8ff2-139">Image Offer: UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e8ff2-139">Image Offer: UbuntuServer</span></span>
* <span data-ttu-id="e8ff2-140">Image Sku: 14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="e8ff2-140">Image Sku: 14.04.5-LTS</span></span>
* <span data-ttu-id="e8ff2-141">Image Version: latest</span><span class="sxs-lookup"><span data-stu-id="e8ff2-141">Image version: latest</span></span>
* <span data-ttu-id="e8ff2-142">OS Type: Linux</span><span class="sxs-lookup"><span data-stu-id="e8ff2-142">OS Type: Linux</span></span>
* <span data-ttu-id="e8ff2-143">Launch Method: SSH</span><span class="sxs-lookup"><span data-stu-id="e8ff2-143">Launch method: SSH</span></span>
* <span data-ttu-id="e8ff2-144">Voer referenties van een beheerder in</span><span class="sxs-lookup"><span data-stu-id="e8ff2-144">Provide an admin credentials</span></span>
* <span data-ttu-id="e8ff2-145">Voer het volgende in voor het script voor de initialisatie van virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="e8ff2-145">For VM initialization script, enter:</span></span>
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuratie van installatiekopie](./media/jenkins-azure-vm-agents/image-config.png)

* <span data-ttu-id="e8ff2-147">Klik op **sjabloon controleren** tooverify Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-147">Click **Verify Template** tooverify hello configuration.</span></span>
* <span data-ttu-id="e8ff2-148">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-148">Click **Save**.</span></span>

## <a name="create-a-job-in-jenkins"></a><span data-ttu-id="e8ff2-149">Een taak maken in Jenkins</span><span class="sxs-lookup"><span data-stu-id="e8ff2-149">Create a job in Jenkins</span></span>

* <span data-ttu-id="e8ff2-150">Klik in het Hallo Jenkins dashboard op **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-150">Within hello Jenkins dashboard, click **New Item**.</span></span> 
* <span data-ttu-id="e8ff2-151">Voer een naam in, selecteer **Freestyle project** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-151">Enter a name and select **Freestyle project** and click **OK**.</span></span>
* <span data-ttu-id="e8ff2-152">In Hallo **algemene** tabblad, selecteer 'Beperken waar project kan worden uitgevoerd' en het type 'ubuntu' in de Label-expressie.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-152">In hello **General** tab, select "Restrict where project can be run" and type "ubuntu" in Label Expression.</span></span> <span data-ttu-id="e8ff2-153">U ziet nu 'ubuntu' hello vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-153">You now see "ubuntu" in hello dropdown.</span></span>
* <span data-ttu-id="e8ff2-154">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-154">Click **Save**.</span></span>

![Een taak instellen](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a><span data-ttu-id="e8ff2-156">Het nieuwe project bouwen</span><span class="sxs-lookup"><span data-stu-id="e8ff2-156">Build your new project</span></span>

* <span data-ttu-id="e8ff2-157">Ga terug toohello Jenkins dashboard.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-157">Go back toohello Jenkins dashboard.</span></span>
* <span data-ttu-id="e8ff2-158">Klik met de rechtermuisknop Hallo nieuwe taak die u hebt gemaakt, klikt u op **nu samenstellen**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-158">Right-click hello new job you created, then click **Build now**.</span></span> <span data-ttu-id="e8ff2-159">De bewerking wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-159">A build is kicked off.</span></span> 
* <span data-ttu-id="e8ff2-160">Zodra de Hallo build is voltooid, gaat u te**Console uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-160">Once hello build is complete, go too**Console output**.</span></span> <span data-ttu-id="e8ff2-161">U ziet Hallo build op afstand is uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ff2-161">You see that hello build was performed remotely on Azure.</span></span>

![Console-uitvoer](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a><span data-ttu-id="e8ff2-163">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="e8ff2-163">Reference</span></span>

* <span data-ttu-id="e8ff2-164">Video van Azure Friday: [Continuous Integration with Jenkins Using Azure VM Agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Continue integratie met Jenkins met behulp van Azure VM-agents)</span><span class="sxs-lookup"><span data-stu-id="e8ff2-164">Azure Friday video: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents)</span></span>
* <span data-ttu-id="e8ff2-165">Ondersteuningsinformatie en configuratie-opties: de Engelstalige wiki van Jenkins [Azure VM Agents plugin](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span><span class="sxs-lookup"><span data-stu-id="e8ff2-165">Support information and configuration options:  [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin)</span></span> 

