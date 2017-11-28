---
title: aaaCreate een Jenkins-server op Azure
description: Jenkins installeren op een virtuele machine van Azure Linux van Hallo Jenkins oplossingssjabloon en een voorbeeld van een Java-toepassing bouwen.
author: mlearned
manager: douge
ms.service: multiple
ms.workload: web
ms.devlang: java
ms.topic: hero-article
ms.date: 08/21/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 82ab2ac52594acba131414b449b608978591d4b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-jenkins-server-on-an-azure-linux-vm-from-hello-azure-portal"></a><span data-ttu-id="2a3eb-103">Een server Jenkins maken op een Azure Linux VM van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="2a3eb-103">Create a Jenkins server on an Azure Linux VM from hello Azure portal</span></span>

<span data-ttu-id="2a3eb-104">Deze snelstartgids toont hoe tooinstall [Jenkins](https://jenkins.io) op een virtuele Ubuntu Linux-machine met Hallo-hulpprogramma's en invoegtoepassingen geconfigureerd toowork met Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-104">This quickstart shows how tooinstall [Jenkins](https://jenkins.io) on an Ubuntu Linux VM with hello tools and plug-ins configured toowork with Azure.</span></span> <span data-ttu-id="2a3eb-105">Wanneer u klaar bent, beschikt u over een Jenkins-server die wordt uitgevoerd in Azure voor het bouwen van een Java-voorbeeld-app uit [GitHub](https://github.com).</span><span class="sxs-lookup"><span data-stu-id="2a3eb-105">When you're finished, you have a Jenkins server running in Azure building a sample Java app from [GitHub](https://github.com).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a3eb-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2a3eb-106">Prerequisites</span></span>

* <span data-ttu-id="2a3eb-107">Een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="2a3eb-107">An Azure subscription</span></span>
* <span data-ttu-id="2a3eb-108">Toegang tooSSH op de opdrachtregel van de computer (zoals Hallo Bash shell of [PuTTY](http://www.putty.org/))</span><span class="sxs-lookup"><span data-stu-id="2a3eb-108">Access tooSSH on your computer's command line (such as hello Bash shell or [PuTTY](http://www.putty.org/))</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-jenkins-vm-from-hello-solution-template"></a><span data-ttu-id="2a3eb-109">Hallo Jenkins VM van Hallo oplossingssjabloon maken</span><span class="sxs-lookup"><span data-stu-id="2a3eb-109">Create hello Jenkins VM from hello solution template</span></span>

<span data-ttu-id="2a3eb-110">Open Hallo [marketplace-installatiekopie voor Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in uw webbrowser en selecteer **IT ophalen nu** vanaf de linkerkant van de pagina Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-110">Open hello [marketplace image for Jenkins](https://azuremarketplace.microsoft.com/marketplace/apps/azure-oss.jenkins?tab=Overview) in your web browser and select  **GET IT NOW** from hello left-hand side of hello page.</span></span> <span data-ttu-id="2a3eb-111">Bekijk Hallo pricing details en selecteer **doorgaan**, selecteer daarna **maken** tooconfigure hello Jenkins server in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-111">Review hello pricing details and select **Continue**, then select **Create** tooconfigure hello Jenkins server in hello Azure portal.</span></span> 
   
![Dialoogvenster Azure-portal](./media/install-jenkins-solution-template/ap-create.png)

<span data-ttu-id="2a3eb-113">In Hallo **basisinstellingen configureren** tabblad, vul Hallo velden te volgen:</span><span class="sxs-lookup"><span data-stu-id="2a3eb-113">In hello **Configure basic settings** tab, fill in hello following fields:</span></span>

![Basisinstellingen configureren](./media/install-jenkins-solution-template/ap-basic.png)

* <span data-ttu-id="2a3eb-115">Geef **Jenkins** op bij **Naam**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-115">Use **Jenkins** for **Name**.</span></span>
* <span data-ttu-id="2a3eb-116">Voer een gebruikersnaam in bij **Gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-116">Enter a **User name**.</span></span> <span data-ttu-id="2a3eb-117">Hallo-gebruikersnaam moet voldoen aan [specifieke vereisten](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="2a3eb-117">hello user name must meet [specific requirements](/azure/virtual-machines/linux/faq#what-are-the-username-requirements-when-creating-a-vm).</span></span>
* <span data-ttu-id="2a3eb-118">Selecteer **wachtwoord** als Hallo **verificatietype** en voer een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-118">Select **Password** as hello **Authentication type** and enter a password.</span></span> <span data-ttu-id="2a3eb-119">Hallo-wachtwoord moet een hoofdletter, cijfer en één speciaal teken.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-119">hello password must have an upper case character, a number, and one special character.</span></span>
* <span data-ttu-id="2a3eb-120">Gebruik **myJenkinsResourceGroup** voor Hallo **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-120">Use **myJenkinsResourceGroup** for hello **Resource Group**.</span></span>
* <span data-ttu-id="2a3eb-121">Kies Hallo **VS-Oost** [Azure-regio](https://azure.microsoft.com/regions/) van Hallo **locatie** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-121">Choose hello **East US** [Azure region](https://azure.microsoft.com/regions/) from hello **Location** drop-down.</span></span>

<span data-ttu-id="2a3eb-122">Selecteer **OK** tooproceed toohello **extra opties configureren** tabblad. Voer een unieke naam tooidentify hello Jenkins domeinserver en selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-122">Select **OK** tooproceed toohello **Configure additional options** tab. Enter a unique domain name tooidentify hello Jenkins server and select **OK**.</span></span>

![selecteer aanvullende opties](./media/install-jenkins-solution-template/ap-addtional.png)  

 <span data-ttu-id="2a3eb-124">Als de validatie is geslaagd, selecteert u **OK** opnieuw uit Hallo **samenvatting** tabblad. Tot slot selecteert **aankoop** toocreate Hallo Jenkins VM.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-124">Once validation passes, select **OK** again from hello **Summary** tab. Finally, select **Purchase** toocreate hello Jenkins VM.</span></span> <span data-ttu-id="2a3eb-125">Wanneer de server klaar is, kunt u een melding krijgen in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="2a3eb-125">When your server is ready, you get a notification in hello Azure portal:</span></span>   

![Melding dat de Jenkins-server klaar is](./media/install-jenkins-solution-template/jenkins-deploy-notification-ready.png)

## <a name="connect-toojenkins"></a><span data-ttu-id="2a3eb-127">Verbinding maken met tooJenkins</span><span class="sxs-lookup"><span data-stu-id="2a3eb-127">Connect tooJenkins</span></span>

<span data-ttu-id="2a3eb-128">Navigeer tooyour virtuele machine (bijvoorbeeld http://jenkins2517454.eastus.cloudapp.azure.com/) in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-128">Navigate tooyour virtual machine (for example, http://jenkins2517454.eastus.cloudapp.azure.com/) in  your web browser.</span></span> <span data-ttu-id="2a3eb-129">Hallo Jenkins console is niet toegankelijk via niet-beveiligde HTTP, zodat de instructies vindt u op Hallo pagina tooaccess hello Jenkins console veilig vanaf uw computer met behulp van een SSH-tunnel.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-129">hello Jenkins console is inaccessible through unsecured HTTP so instructions are provided on hello page tooaccess hello Jenkins console securely from your computer using an SSH tunnel.</span></span>

![Jenkins ontgrendelen](./media/install-jenkins-solution-template/jenkins-ssh-instructions.png)

<span data-ttu-id="2a3eb-131">Hallo-tunnel met Hallo instellen `ssh` opdracht op de pagina Hallo vanaf de opdrachtregel Hallo vervangen `username` met Hallo-naam van Hallo virtuele machine admin gebruiker eerder gekozen bij het instellen van Hallo virtuele machine uit Hallo oplossingssjabloon.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-131">Set up hello tunnel using hello `ssh` command on hello page from hello command line, replacing `username` with hello name of hello virtual machine admin user chosen earlier when setting up hello virtual machine from hello solution template.</span></span>

```bash
ssh -L 127.0.0.1:8080:localhost:8080 jenkinsadmin@jenkins2517454.eastus.cloudapp.azure.com
```

<span data-ttu-id="2a3eb-132">Nadat u de tunnel Hallo hebt gestart, gaat u toohttp://localhost:8080 / op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-132">After you have started hello tunnel, navigate toohttp://localhost:8080/ on your local machine.</span></span> 

<span data-ttu-id="2a3eb-133">Hallo eerste wachtwoord door het uitvoeren van de volgende opdracht in de opdrachtregel Hallo terwijl u bent verbonden via SSH toohello Jenkins VM Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-133">Get hello initial password by running hello following command in hello command line while connected through SSH toohello Jenkins VM.</span></span>

```bash
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
```

<span data-ttu-id="2a3eb-134">Hallo Jenkins dashboard voor Hallo eerst met behulp van deze eerste wachtwoord ontgrendelen.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-134">Unlock hello Jenkins dashboard for hello first time using this initial password.</span></span>

![Jenkins ontgrendelen](./media/install-jenkins-solution-template/jenkins-unlock.png)

<span data-ttu-id="2a3eb-136">Selecteer **voorgestelde invoegtoepassingen installeren** op Hallo voor volgende pagina en maak vervolgens een Jenkins admin gebruikt tooaccess hello Jenkins gebruikersdashboard.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-136">Select **Install suggested plugins** on hello next page and then create a Jenkins admin user used tooaccess hello Jenkins dashboard.</span></span>

![Jenkins is klaar.](./media/install-jenkins-solution-template/jenkins-welcome.png)

<span data-ttu-id="2a3eb-138">Hallo Jenkins server is nu gereed toobuild code.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-138">hello Jenkins server is now ready toobuild code.</span></span>

## <a name="create-your-first-job"></a><span data-ttu-id="2a3eb-139">Uw eerste taak maken</span><span class="sxs-lookup"><span data-stu-id="2a3eb-139">Create your first job</span></span>

<span data-ttu-id="2a3eb-140">Selecteer **nieuwe taken maken** Hallo Jenkins console noem deze **mySampleApp** en selecteer **Freestyle project**, selecteer daarna **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-140">Select **Create new jobs** from hello Jenkins console, then name it **mySampleApp** and select **Freestyle project**, then select **OK**.</span></span>

![Een nieuwe taak maken](./media/install-jenkins-solution-template/jenkins-new-job.png) 

<span data-ttu-id="2a3eb-142">Selecteer Hallo **Source Code Management** tabblad, schakelt u **Git**, en voer de volgende URL in Hallo **URL opslagplaats** veld:`https://github.com/spring-guides/gs-spring-boot.git`</span><span class="sxs-lookup"><span data-stu-id="2a3eb-142">Select hello **Source Code Management** tab, enable **Git**, and enter hello following URL in **Repository URL**  field: `https://github.com/spring-guides/gs-spring-boot.git`</span></span>

![Hallo Git-opslagplaats definiëren](./media/install-jenkins-solution-template/jenkins-job-git-configuration.png) 

<span data-ttu-id="2a3eb-144">Selecteer Hallo **bouwen** tabblad en selecteer vervolgens **toevoegen build stap**, **Gradle aanroepen script**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-144">Select hello **Build** tab, then select **Add build step**, **Invoke Gradle script**.</span></span> <span data-ttu-id="2a3eb-145">Selecteer **Use Gradle Wrapper** en voer vervolgens `complete` in bij **Wrapper location** en `build` bij **Tasks**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-145">Select **Use Gradle Wrapper**, then enter `complete` in **Wrapper location** and `build` for **Tasks**.</span></span>

![Hallo Gradle wrapper toobuild gebruiken](./media/install-jenkins-solution-template/jenkins-job-gradle-config.png) 

<span data-ttu-id="2a3eb-147">Selecteer **Advanced..**</span><span class="sxs-lookup"><span data-stu-id="2a3eb-147">Select **Advanced..**</span></span> <span data-ttu-id="2a3eb-148">en voer vervolgens `complete` in Hallo **hoofdmap Build script** veld.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-148">and then enter `complete` in hello **Root Build script** field.</span></span> <span data-ttu-id="2a3eb-149">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-149">Select **Save**.</span></span>

![Geavanceerde instellingen opgeven in Hallo Gradle wrapper build stap](./media/install-jenkins-solution-template/jenkins-job-gradle-advances.png) 

## <a name="build-hello-code"></a><span data-ttu-id="2a3eb-151">Hallo code bouwen</span><span class="sxs-lookup"><span data-stu-id="2a3eb-151">Build hello code</span></span>

<span data-ttu-id="2a3eb-152">Selecteer **nu bouwen** toocompile Hallo code en pakket Hallo voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-152">Select **Build Now** toocompile hello code and package hello sample app.</span></span> <span data-ttu-id="2a3eb-153">Als uw build is voltooid, selecteert u Hallo **werkruimte** koppeling voor Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-153">When your build completes, select hello **Workspace** link for hello project.</span></span>

![Blader toohello werkruimte tooget Hallo JAR-bestand van Hallo-versie](./media/install-jenkins-solution-template/jenkins-access-workspace.png) 

<span data-ttu-id="2a3eb-155">Navigeer te`complete/build/libs` en zorg ervoor dat Hallo `gs-spring-boot-0.1.0.jar` is er tooverify build is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-155">Navigate too`complete/build/libs` and ensure hello `gs-spring-boot-0.1.0.jar` is there tooverify that your build was successful.</span></span> <span data-ttu-id="2a3eb-156">Uw Jenkins server nu is klaar toobuild projecten in Azure.</span><span class="sxs-lookup"><span data-stu-id="2a3eb-156">Your Jenkins server is now ready toobuild your own projects in Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a3eb-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a3eb-157">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2a3eb-158">Virtuele Azure-machines toevoegen als Jenkins-agents</span><span class="sxs-lookup"><span data-stu-id="2a3eb-158">Add Azure VMs as Jenkins agents</span></span>](jenkins-azure-vm-agents.md)
