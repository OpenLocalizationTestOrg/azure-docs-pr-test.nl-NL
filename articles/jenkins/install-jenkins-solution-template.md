---
title: Een Jenkins-server maken in Azure
description: Op basis van de sjabloon voor de Jenkins-oplossing een virtuele Linux-machine van Azure installeren en een Java-voorbeeldtoepassing bouwen.
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 7bb74f297d52fb25171817175cce64187b397c38
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-the-azure-portal"></a><span data-ttu-id="f6f0a-103">Vanuit Azure Portal een Jenkins-server maken op een Azure-VM met Linux</span><span class="sxs-lookup"><span data-stu-id="f6f0a-103">Create a Jenkins server on an Azure Linux VM from the Azure portal</span></span>

<span data-ttu-id="f6f0a-104">Deze Quick Start laat zien hoe u [Jenkins](https://jenkins.io) installeert op een virtuele machine met Ubuntu Linux met behulp van de hulpprogramma's en invoegtoepassingen die zijn geconfigureerd om te werken met Azure.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-104">This quickstart shows how to install [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with the tools and plug-ins configured to work with Azure.</span></span> <span data-ttu-id="f6f0a-105">Wanneer u klaar bent, beschikt u over een Jenkins-server die wordt uitgevoerd in Azure voor het bouwen van een Java-voorbeeld-app uit [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="f6f0a-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6f0a-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f6f0a-106">Prerequisites</span></span>

* <span data-ttu-id="f6f0a-107">Een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="f6f0a-107">An Azure subscription</span></span>
* <span data-ttu-id="f6f0a-108">Toegang tot SSH vanaf de opdrachtregel van uw computer (zoals de Bash-shell of [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="f6f0a-108">Access to SSH on your computer's command line (such as the Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-the-jenkins-vm-from-the-solution-template"></a><span data-ttu-id="f6f0a-109">De virtuele machine met Jenkins maken van de oplossingssjabloon</span><span class="sxs-lookup"><span data-stu-id="f6f0a-109">Create the Jenkins VM from the solution template</span></span>

<span data-ttu-id="f6f0a-110">Open in uw webbrowser de [installatiekopie voor Jenkins in de Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) en selecteer **Nu downloaden** aan de linkerkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-110">Open the [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from the left-hand side of the page.</span></span> <span data-ttu-id="f6f0a-111">Controleer de prijsinformatie en selecteer **Doorgaan**. Selecteer vervolgens **Maken** om de Jenkins-server te configureren in Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-111">Review the pricing details and select **Continue**, then select **Create** to configure the Jenkins server in the Azure portal.</span></span> 
   
![Dialoogvenster Azure-portal](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="f6f0a-113">Vul de volgende velden in op het tabblad **Basisinstellingen configureren**:</span><span class="sxs-lookup"><span data-stu-id="f6f0a-113">In the **Configure basic settings** tab, fill in the following fields:</span></span>

![Basisinstellingen configureren](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="f6f0a-115">Geef **Jenkins** op bij **Naam**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="f6f0a-116">Voer een gebruikersnaam in bij **Gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-116">Enter a **User name**.</span></span> <span data-ttu-id="f6f0a-117">De gebruikersnaam moet voldoen aan [specifieke vereisten](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="f6f0a-117">The user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="f6f0a-118">Selecteer **Wachtwoord** bij **Verificatietype** en voer een wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-118">Select **Password** as the **Authentication type** and enter a password.</span></span> <span data-ttu-id="f6f0a-119">Het wachtwoord moet een hoofdletter, een cijfer en één speciaal teken bevatten.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-119">The password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="f6f0a-120">Geef **myJenkinsResourceGroup** op voor **Resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-120">Use **myJenkinsResourceGroup** for the **Resource Group**.</span></span>
* <span data-ttu-id="f6f0a-121">Kies de [Azure-regio](https://azure.microsoft.com/regions/) **VS-Oost** in de vervolgkeuzelijst **Locatie**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-121">Choose the **East US** [Azure region](https://azure.microsoft.com/regions/) from the **Location** drop-down.</span></span>

<span data-ttu-id="f6f0a-122">Selecteer **OK** om naar het tabblad **Extra opties configureren** te gaan. Geef een unieke domeinnaam op om de Jenkins-server te identificeren en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-122">Select **OK** to proceed to the **Configure additional options** tab. Enter a unique domain name to identify the Jenkins server and select **OK**.</span></span>

![selecteer aanvullende opties](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="f6f0a-124">Als de validatie is geslaagd, selecteert u **OK** op het tabblad **Samenvatting**. Selecteer ten slotte **Kopen** om de virtuele Jenkins-machine te maken.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-124">Once validation passes, select **OK** again from the **Summary** tab. Finally, select **Purchase** to create the Jenkins VM.</span></span> <span data-ttu-id="f6f0a-125">U ziet een melding in Azure Portal wanneer de server klaar is:</span><span class="sxs-lookup"><span data-stu-id="f6f0a-125">When your server is ready, you get a notification in the Azure portal:</span></span>   

![Melding dat de Jenkins-server klaar is](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-to-jenkins"></a><span data-ttu-id="f6f0a-127">Verbinding maken met Jenkins</span><span class="sxs-lookup"><span data-stu-id="f6f0a-127">Connect to Jenkins</span></span>

<span data-ttu-id="f6f0a-128">Navigeer in uw webbrowser naar de virtuele machine (bijvoorbeeld http://jenkins2517454.eastus.cloudapp.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f6f0a-128">Navigate to your virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="f6f0a-129">De Jenkins-console is niet toegankelijk via onbeveiligde HTTP. Om die reden bevat de pagina instructies om de console veilig vanaf uw computer te gebruiken via een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-129">The Jenkins console is inaccessible through unsecured HTTP so instructions are provided on the page to access the Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Jenkins ontgrendelen](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="f6f0a-131">Stel de tunnel op de pagina in met behulp van de opdracht `ssh` op de opdrachtregel. Vervang `username` hierbij door de naam van de gebruiker met beheerdersrechten van de virtuele machine die u eerder hebt gekozen bij het instellen van de virtuele machine op basis van de oplossingssjabloon.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-131">Set up the tunnel using the `ssh` command on the page from the command line, replacing `username` with the name of the virtual machine admin user chosen earlier when setting up the virtual machine from the solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="f6f0a-132">Nadat u de tunnel hebt gestart, gaat u naar http://localhost:8080/ op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-132">After you have started the tunnel, navigate to http://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="f6f0a-133">Vraag het initiële wachtwoord op door de volgende opdracht uit te voeren op de opdrachtregel terwijl u via SSH bent verbonden met de Jenkins-VM.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-133">Get the initial password by running the following command in the command line while connected through SSH to the Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="f6f0a-134">Gebruik dit initiële wachtwoord om het Jenkins-dashboard voor de eerste keer te ontgrendelen.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-134">Unlock the Jenkins dashboard for the first time using this initial password.</span></span>

![Jenkins ontgrendelen](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="f6f0a-136">Selecteer **Install suggested plugins** op de volgende pagina en maak vervolgens een Jenkins-gebruiker met beheerdersrechten om toegang te krijgen tot het Jenkins-dashboard.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-136">Select **Install suggested plugins** on the next page and then create a Jenkins admin user used to access the Jenkins dashboard.</span></span>

![Jenkins is klaar.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="f6f0a-138">De Jenkins-server is nu klaar voor het bouwen van code.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-138">The Jenkins server is now ready to build code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="f6f0a-139">Uw eerste taak maken</span><span class="sxs-lookup"><span data-stu-id="f6f0a-139">Create your first job</span></span>

<span data-ttu-id="f6f0a-140">Selecteer **Create new jobs** in de Jenkins-console, geef het project de naam **mySampleApp**, selecteer **Freestyle project** en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-140">Select **Create new jobs** from the Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Een nieuwe taak maken](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="f6f0a-142">Selecteer het tabblad **Source Code Management**, schakel het keuzerondje **Git** in en voer in het veld **Repository URL** de volgende URL in: `https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="f6f0a-142">Select the **Source Code Management** tab, enable **Git**, and enter the following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![De Git-opslagplaats definiëren](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="f6f0a-144">Selecteer het tabblad **Build** en selecteer vervolgens **Add build step**, **Invoke Gradle script**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-144">Select the **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="f6f0a-145">Selecteer **Use Gradle Wrapper** en voer vervolgens `complete` in bij **Wrapper location** en `build` bij **Tasks**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![De Gradle-wrapper gebruiken om de code te bouwen](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="f6f0a-147">Selecteer **Advanced..**</span><span class="sxs-lookup"><span data-stu-id="f6f0a-147">Select **Advanced..**</span></span> <span data-ttu-id="f6f0a-148">en voer vervolgens in het veld **Root Build script** de waarde `complete` in.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-148">and then enter `complete` in the **Root Build script** field.</span></span> <span data-ttu-id="f6f0a-149">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-149">Select **Save**.</span></span>

![Geavanceerde instellingen opgeven in de stap voor het bouwen van de Gradle-wrapper](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-the-code"></a><span data-ttu-id="f6f0a-151">De code bouwen</span><span class="sxs-lookup"><span data-stu-id="f6f0a-151">Build the code</span></span>

<span data-ttu-id="f6f0a-152">Selecteer **Build Now** om de code te compileren en een pakket te maken van de voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-152">Select **Build Now** to compile the code and package the sample app.</span></span> <span data-ttu-id="f6f0a-153">Als de build is voltooid, selecteert u de koppeling **Workspace** voor het project.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-153">When your build completes, select the **Workspace** link for the project.</span></span>

![Bladeren naar de werkruimte om het JAR-bestand van de build te zoeken](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="f6f0a-155">Navigeer naar `complete/build/libs` en controleer of u daar het bestand `gs-spring-boot-0.1.0.jar` ziet, zodat u weet dat de build is gelukt.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-155">Navigate to `complete/build/libs` and ensure the `gs-spring-boot-0.1.0.jar` is there to verify that your build was successful.</span></span> <span data-ttu-id="f6f0a-156">De Jenkins-server is nu gereed voor het bouwen van uw eigen projecten in Azure.</span><span class="sxs-lookup"><span data-stu-id="f6f0a-156">Your Jenkins server is now ready to build your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6f0a-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6f0a-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6f0a-158">Virtuele Azure-machines toevoegen als Jenkins-agents</span><span class="sxs-lookup"><span data-stu-id="f6f0a-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
