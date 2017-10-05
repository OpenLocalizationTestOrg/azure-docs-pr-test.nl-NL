---
title: Externe toegang inschakelen voor Azure-implementaties in Eclipse
description: Informatie over het inschakelen van externe toegang voor Azure met de Azure-Toolkit voor Eclipse-implementaties.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: b6150006-9a7f-4d83-be18-d35ec780c7c5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 654d511bd5a62341f87569317e97360c94a6f26c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="9d244-103">Externe toegang inschakelen voor Azure-implementaties in Eclipse</span><span class="sxs-lookup"><span data-stu-id="9d244-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="9d244-104">U kunt voor het oplossen van uw implementaties, inschakelen en gebruiken van externe toegang verbinding maken met de virtuele machine die als host fungeert voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="9d244-104">To help troubleshoot your deployments, you may enable and use Remote Access to connect to the virtual machine hosting your deployment.</span></span> <span data-ttu-id="9d244-105">De functionaliteit voor externe toegang is afhankelijk van de Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="9d244-105">The Remote Access functionality relies on the Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="9d244-106">Nadat u deze hebt gepubliceerd naar Azure, of als u Eclipse met een Windows-besturingssysteem gebruikt, u externe toegang configureren kunt voordat u naar Azure publiceert, kunt u externe toegang configureert voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="9d244-106">You can configure Remote Access for your deployment after you have published it to Azure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish to Azure.</span></span> <span data-ttu-id="9d244-107">Houd er rekening mee dat u een extern-bureaubladclient die compatibel is met het besturingssysteem moet om verbinding met uw implementatie virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="9d244-107">Note that you will need a remote desktop client that is compatible with your operating system in order to connect to your deployment's virtual machine in Azure.</span></span>

## <a name="how-to-enable-remote-access-before-you-deploy-to-azure"></a><span data-ttu-id="9d244-108">Het inschakelen van externe toegang, voordat u naar Azure implementeert</span><span class="sxs-lookup"><span data-stu-id="9d244-108">How to enable Remote Access before you deploy to Azure</span></span>
> [!NOTE]
> <span data-ttu-id="9d244-109">Om externe toegang inschakelen voordat u uw toepassing in Azure implementeert, moet u Eclipse worden uitgevoerd op Windows.</span><span class="sxs-lookup"><span data-stu-id="9d244-109">To enable Remote Access before you deploy your application to Azure, you need to be running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="9d244-110">De volgende afbeelding toont de **RAS** eigenschappenvenster gebruikt om externe toegang.</span><span class="sxs-lookup"><span data-stu-id="9d244-110">The following image shows the **Remote Access** properties dialog used to enable remote access.</span></span>

![][ic719494]

<span data-ttu-id="9d244-111">Er zijn twee manieren om weer te geven de **RAS** dialoogvenster met eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="9d244-111">There are two ways to display the **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="9d244-112">Klik op de **Geavanceerd** koppelen de **RAS** sectie van de **publiceren naar Azure** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d244-112">Click the **Advanced** link in the **Remote Access** section of the **Publish to Azure** dialog.</span></span>

* <span data-ttu-id="9d244-113">Open de **eigenschappen** dialoogvenster van uw Azure-project.</span><span class="sxs-lookup"><span data-stu-id="9d244-113">Open the **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="9d244-114">Wanneer u een nieuw project in de Azure-implementatie maakt, is het project heeft geen externe toegang is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d244-114">When you create a new Azure deployment project, the project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="9d244-115">Echter, kunt u eenvoudig externe toegang inschakelen door te geven van de gebruikersnaam en wachtwoord in de **publiceren naar Azure** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d244-115">However, you can easily enable remote access by specifying the user name and password in the **Publish to Azure** dialog.</span></span> <span data-ttu-id="9d244-116">De RAS-wachtwoord is versleuteld met behulp van x.509-certificaten.</span><span class="sxs-lookup"><span data-stu-id="9d244-116">The Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="9d244-117">Als u geen gebruik geeft u uw eigen certificaat de versleuteling is afhankelijk van een zelfondertekend certificaat met de Azure-invoegtoepassing voor Eclipse verzonden.</span><span class="sxs-lookup"><span data-stu-id="9d244-117">If you do not use provide your own certificate, the encryption relies on a self-signed certificate shipped with the Azure Plugin for Eclipse.</span></span> <span data-ttu-id="9d244-118">Dit zelfondertekende certificaat bevindt zich in de **cert** map van uw Azure-project opgeslagen als een openbaar certificaat-bestand (SampleRemoteAccessPublic.cer) en als een certificaatbestand Personal Information Exchange (PFX) (SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="9d244-118">This self-signed certificate is in the **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="9d244-119">De laatste bevat de persoonlijke sleutel voor het certificaat en heeft deze een standaardwachtwoord **Wachtwoord1**.</span><span class="sxs-lookup"><span data-stu-id="9d244-119">The latter contains the private key for the certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="9d244-120">Echter, omdat dit wachtwoord algemeen bekend is, kan de standaardcertificaat moet worden gebruikt alleen voor het leren van de toepassing wordt niet voor een productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="9d244-120">However, since this password is public knowledge, the default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="9d244-121">Dus anders dan voor het leren van toepassing wanneer u wilt ingeschakeld externe sessies voor uw implementaties, klikt u de **Geavanceerd** koppelen de **publiceren naar Azure** dialoogvenster om uw eigen certificaat te geven.</span><span class="sxs-lookup"><span data-stu-id="9d244-121">So other than for learning purposes, when you want to enabled remote sessions for your deployments, you should click the **Advanced** link in the **Publish to Azure** dialog to specify your own certificate.</span></span> <span data-ttu-id="9d244-122">Houd er rekening mee dat u uploaden van het PFX-versie van het certificaat naar de gehoste service in de Azure-beheerportal wilt, zodat die Azure om het wachtwoord van de gebruiker te ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="9d244-122">Note that you'll need to upload the PFX version of the certificate to your hosted service within the Azure Management Portal, so that Azure can decrypt the user password.</span></span>

<span data-ttu-id="9d244-123">De rest van de zelfstudie laat zien hoe u externe toegang inschakelt voor een Azure-implementatie-project die aanvankelijk is gemaakt met externe toegang uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d244-123">The remainder of the tutorial shows you how to enable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="9d244-124">Voor deze zelfstudie maken we een nieuw zelfondertekend certificaat en het pfx-bestand heeft een wachtwoord van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="9d244-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="9d244-125">U hebt ook de optie van het gebruik van een certificaat zijn uitgegeven door een certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="9d244-125">You also have the option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-to-enable-remote-access-after-you-have-deployed-to-azure"></a><span data-ttu-id="9d244-126">Het inschakelen van externe toegang nadat u hebt geïmplementeerd naar Azure</span><span class="sxs-lookup"><span data-stu-id="9d244-126">How to enable Remote Access after you have deployed to Azure</span></span>
<span data-ttu-id="9d244-127">Voor externe toegang nadat u hebt geïmplementeerd naar Azure, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="9d244-127">To enable remote access after you have deployed to Azure, use the following steps:</span></span>

1. <span data-ttu-id="9d244-128">Meld u aan bij de Azure-beheerportal met behulp van uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="9d244-128">Log into the Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="9d244-129">In de lijst met **Cloudservices**, selecteer uw geïmplementeerde cloudservice</span><span class="sxs-lookup"><span data-stu-id="9d244-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="9d244-130">Klik in de cloud service-webpagina op de **configureren** koppeling</span><span class="sxs-lookup"><span data-stu-id="9d244-130">In the cloud service web page, click the **Configure** link</span></span>

4. <span data-ttu-id="9d244-131">Klik op de onderkant van de pagina op de **externe** koppeling</span><span class="sxs-lookup"><span data-stu-id="9d244-131">On the bottom of the configuration page, click the **Remote** link</span></span>

5. <span data-ttu-id="9d244-132">Wanneer het pop-updialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="9d244-132">When the pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="9d244-133">Geef de rol waarvoor u wilt externe toegang inschakelen</span><span class="sxs-lookup"><span data-stu-id="9d244-133">Specify the Role you for which you want to enable remote access</span></span>

   * <span data-ttu-id="9d244-134">Selecteer de **extern bureaublad inschakelen** selectievakje</span><span class="sxs-lookup"><span data-stu-id="9d244-134">Click to select the **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="9d244-135">Geef een gebruikersnaam en wachtwoord die u wilt gebruiken voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="9d244-135">Specify a user name and password you want to use for remote access</span></span>
   
   * <span data-ttu-id="9d244-136">Selecteer het certificaat te gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d244-136">Select the certificate to use</span></span>

6. <span data-ttu-id="9d244-137">Klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="9d244-137">Click **OK**</span></span> 

<span data-ttu-id="9d244-138">U ziet een bericht weergegeven dat de wijziging in de configuratie is gemaakt, maar dit kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="9d244-138">You will see a message stating that your configuration change is in progress, which may take a few minutes to complete.</span></span> <span data-ttu-id="9d244-139">Nadat de wijziging in de configuratie is voltooid, volg de stappen in de **extern aanmelden** verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="9d244-139">After the configuration change has completed, follow the steps in the **To log in remotely** section later in this article.</span></span>

## <a name="how-to-enable-remote-access-in-your-package"></a><span data-ttu-id="9d244-140">Het inschakelen van externe toegang in het pakket</span><span class="sxs-lookup"><span data-stu-id="9d244-140">How to enable Remote Access in your package</span></span>
1. <span data-ttu-id="9d244-141">Binnen de Eclipse-Project Explorer deelvenster met de rechtermuisknop op uw Azure-project en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="9d244-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="9d244-142">In de **eigenschappen** dialoogvenster Vouw **Azure** in het linkerdeelvenster op **RAS**.</span><span class="sxs-lookup"><span data-stu-id="9d244-142">In the **Properties** dialog, expand **Azure** in the left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="9d244-143">In de **RAS** dialoogvenster, zorg ervoor dat **alle rollen te accepteren van extern bureaublad-verbindingen met deze aanmeldingsreferenties inschakelen** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9d244-143">In the **Remote Access** dialog, ensure **Enable all roles to accept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="9d244-144">Geef een naam op voor de extern bureaublad-verbinding.</span><span class="sxs-lookup"><span data-stu-id="9d244-144">Specify a user name for the Remote Desktop connection.</span></span>

5. <span data-ttu-id="9d244-145">Geef en Bevestig het wachtwoord voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="9d244-145">Specify and confirm the password for the user.</span></span> <span data-ttu-id="9d244-146">De waarden gebruikersnaam en het wachtwoord instellen in dit dialoogvenster wordt gebruikt wanneer u een extern bureaublad-verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="9d244-146">The user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="9d244-147">(Houd er rekening mee dat dit een afzonderlijk wachtwoord van het PFX-wachtwoord is.)</span><span class="sxs-lookup"><span data-stu-id="9d244-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="9d244-148">De verloopdatum voor het gebruikersaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="9d244-148">Specify the expiration date for the user account.</span></span>

7. <span data-ttu-id="9d244-149">Klik op **nieuw** een nieuw zelfondertekend certificaat maken.</span><span class="sxs-lookup"><span data-stu-id="9d244-149">Click **New** to create a new self-signed certificate.</span></span> <span data-ttu-id="9d244-150">(U kunt ook een certificaat selecteren van uw systeem werkruimte of het bestand via de **werkruimte** of **bestandssysteem** knoppen, respectievelijk, maar voor de doeleinden van deze zelfstudie maken we een nieuw certificaat.)</span><span class="sxs-lookup"><span data-stu-id="9d244-150">(Alternatively, you could select a certificate from your workspace or file system through the **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="9d244-151">In de **nieuw certificaat** dialoogvenster Geef en Bevestig het wachtwoord dat u voor het PFX-bestand gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d244-151">In the **New Certificate** dialog, specify and confirm the password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="9d244-152">De opgegeven waarde voor accepteren **naam (CN)**, of gebruik een aangepaste naam.</span><span class="sxs-lookup"><span data-stu-id="9d244-152">Accept the value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="9d244-153">Geef het pad en de naam waarin het nieuwe certificaat, in cer-vorm moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9d244-153">Specify the path and file name where the new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="9d244-154">Voor deze stap en de volgende stap, u kunt de **cert** map van uw Azure-project, maar u bent een andere locatie kiezen.</span><span class="sxs-lookup"><span data-stu-id="9d244-154">For this step and the next step, you could use the **cert** folder of your Azure project, but you're free to choose another location.</span></span> <span data-ttu-id="9d244-155">Voor deze zelfstudie gebruiken we **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="9d244-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="9d244-156">(Maken de **c:\mycert** map voordat u doorgaat, of gebruik een bestaande map, indien gewenst.)</span><span class="sxs-lookup"><span data-stu-id="9d244-156">(Create the **c:\mycert** folder prior to proceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="9d244-157">Geef de naam van het pad en bestand waarin het nieuwe certificaat en de persoonlijke sleutel, PFX-indeling moeten worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9d244-157">Specify the path and file name where the new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="9d244-158">Voor deze zelfstudie gebruiken we **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="9d244-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="9d244-159">Uw **nieuw certificaat** dialoogvenster ziet er ongeveer als volgt (bijwerken van de paden voor mappen als u niet gebruikt **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="9d244-159">Your **New Certificate** dialog should look similar to the following (update the folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="9d244-160">Klik op **OK** sluiten de **nieuw certificaat** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d244-160">Click **OK** to close the **New Certificate** dialog.</span></span>

8. <span data-ttu-id="9d244-161">Uw **RAS** dialoogvenster ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="9d244-161">Your **Remote Access** dialog should look similar to the following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="9d244-162">Klik op **OK** sluiten de **RAS** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="9d244-162">Click **OK** to close the **Remote Access** dialog.</span></span>

<span data-ttu-id="9d244-163">Bouw uw toepassing opnieuw met de build instellen voor implementatie naar cloud.</span><span class="sxs-lookup"><span data-stu-id="9d244-163">Rebuild your application, with the build set for deployment to cloud.</span></span>

## <a name="to-log-in-remotely"></a><span data-ttu-id="9d244-164">Om aan te melden op afstand</span><span class="sxs-lookup"><span data-stu-id="9d244-164">To log in remotely</span></span>
<span data-ttu-id="9d244-165">Zodra uw rolinstantie gereed is, kunt u extern aanmelden bij de virtuele machine die als host voor uw toepassing fungeert.</span><span class="sxs-lookup"><span data-stu-id="9d244-165">Once your role instance is ready, you can remotely log in to the virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="9d244-166">Als Eclipse op Windows en u hebt geselecteerd de **Start extern bureaublad op implementeren** optie tijdens de implementatie naar Azure, u krijgt een verbinding met extern bureaublad-aanmeldingsscherm wanneer uw implementatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="9d244-166">If are using Eclipse on Windows and you selected the **Start remote desktop on deploy** option during your deployment to Azure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="9d244-167">Wanneer u wordt gevraagd om de gebruikersnaam en wachtwoord, voer de waarden die u hebt opgegeven voor de externe gebruiker en zich aan te melden.</span><span class="sxs-lookup"><span data-stu-id="9d244-167">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

* <span data-ttu-id="9d244-168">Een andere manier om aan te melden op afstand is via de <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span><span class="sxs-lookup"><span data-stu-id="9d244-168">Another way to log in remotely is through the <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="9d244-169">Binnen de **Cloudservices** weergeven van de Azure Management portal, klik op de cloudservice, **exemplaren**, klikt u op een specifiek exemplaar en klik op de **Connect** knop.</span><span class="sxs-lookup"><span data-stu-id="9d244-169">Within the **Cloud Services** view of the Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click the **Connect** button.</span></span> <span data-ttu-id="9d244-170">De **Connect** knop wordt weergegeven als het volgende in de opdrachtbalk:</span><span class="sxs-lookup"><span data-stu-id="9d244-170">The **Connect** button appears as the following in the command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="9d244-171">Wanneer u op de **Connect** knop, wordt u gevraagd om een RDP-bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="9d244-171">After clicking the **Connect** button, you will be prompted to open an RDP file.</span></span> <span data-ttu-id="9d244-172">Open het bestand en volg de aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="9d244-172">Open the file and follow the prompts.</span></span> <span data-ttu-id="9d244-173">(U kan dit bestand ook opslaan op uw lokale computer en voer vervolgens het bestand door erop te dubbelklikken op extern aanmelden met uw virtuele machine zonder eerst de beheerportal gaat.)</span><span class="sxs-lookup"><span data-stu-id="9d244-173">(You could also save this file to your local computer, and then run the file by double-clicking it to remote log in to your virtual machine without needing to first go the management portal.)</span></span>

  * <span data-ttu-id="9d244-174">Wanneer u wordt gevraagd om de gebruikersnaam en wachtwoord, voer de waarden die u hebt opgegeven voor de externe gebruiker en zich aan te melden.</span><span class="sxs-lookup"><span data-stu-id="9d244-174">When you are prompted for the user name and password, enter the values that you specified for the remote user and will be able to log in.</span></span>

> [!NOTE]
> <span data-ttu-id="9d244-175">Als u op een niet-Windows-besturingssysteem, moet u een extern bureaublad-client die compatibel is met het besturingssysteem gebruiken en volg de stappen voor het configureren van de client met de instellingen in het RDP-bestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="9d244-175">If you are on a non-Windows operating system, you need to use a Remote Desktop client that is compatible with your operating system and follow the steps to configure that client with the settings in the RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="9d244-176">Zie ook</span><span class="sxs-lookup"><span data-stu-id="9d244-176">See Also</span></span>
<span data-ttu-id="9d244-177">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9d244-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="9d244-178">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9d244-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="9d244-179">[De installatie van de Azure Toolkit voor Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="9d244-179">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="9d244-180">Zie voor meer informatie over het gebruik van Azure met Java de [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="9d244-180">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
