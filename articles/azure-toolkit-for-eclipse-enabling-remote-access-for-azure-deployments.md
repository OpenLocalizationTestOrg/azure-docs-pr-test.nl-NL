---
title: Externe toegang voor Azure-implementaties in Eclipse aaaEnabling
description: Meer informatie over hoe tooenable van RAS voor Azure met hello Azure Toolkit voor Eclipse-implementaties.
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
ms.openlocfilehash: 00c2bf22c1f3ec792098f154f771c87506e87881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enabling-remote-access-for-azure-deployments-in-eclipse"></a><span data-ttu-id="4ead3-103">Externe toegang inschakelen voor Azure-implementaties in Eclipse</span><span class="sxs-lookup"><span data-stu-id="4ead3-103">Enabling Remote Access for Azure Deployments in Eclipse</span></span>
<span data-ttu-id="4ead3-104">toohelp oplossen van uw implementaties, mag u inschakelen en gebruiken van externe toegang tooconnect toohello virtuele machine die als host fungeert voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="4ead3-104">toohelp troubleshoot your deployments, you may enable and use Remote Access tooconnect toohello virtual machine hosting your deployment.</span></span> <span data-ttu-id="4ead3-105">Hallo functionaliteit voor externe toegang is afhankelijk van Hallo Remote Desktop Protocol (RDP).</span><span class="sxs-lookup"><span data-stu-id="4ead3-105">hello Remote Access functionality relies on hello Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="4ead3-106">Nadat u tooAzure hebt gepubliceerd, of als u Eclipse met een Windows-besturingssysteem gebruikt, u externe toegang configureren kunt voordat u tooAzure publiceert, kunt u externe toegang configureert voor uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="4ead3-106">You can configure Remote Access for your deployment after you have published it tooAzure, or if you are using Eclipse with a Windows operating system, you can configure Remote Access before you publish tooAzure.</span></span> <span data-ttu-id="4ead3-107">Houd er rekening mee dat u moet een extern-bureaubladclient die compatibel is met het besturingssysteem in volgorde tooconnect tooyour implementatie van virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="4ead3-107">Note that you will need a remote desktop client that is compatible with your operating system in order tooconnect tooyour deployment's virtual machine in Azure.</span></span>

## <a name="how-tooenable-remote-access-before-you-deploy-tooazure"></a><span data-ttu-id="4ead3-108">Hoe tooenable RAS voordat u tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="4ead3-108">How tooenable Remote Access before you deploy tooAzure</span></span>
> [!NOTE]
> <span data-ttu-id="4ead3-109">tooenable RAS voordat u uw toepassing tooAzure implementeert, moet u toobe Eclipse met Windows.</span><span class="sxs-lookup"><span data-stu-id="4ead3-109">tooenable Remote Access before you deploy your application tooAzure, you need toobe running Eclipse on Windows.</span></span>
> 
> 

<span data-ttu-id="4ead3-110">Hallo volgende afbeelding toont Hallo **RAS** eigenschappenvenster tooenable externe toegang gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ead3-110">hello following image shows hello **Remote Access** properties dialog used tooenable remote access.</span></span>

![][ic719494]

<span data-ttu-id="4ead3-111">Er zijn twee manieren toodisplay hello **RAS** dialoogvenster met eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4ead3-111">There are two ways toodisplay hello **Remote Access** properties dialog:</span></span>

* <span data-ttu-id="4ead3-112">Klik op Hallo **Geavanceerd** koppeling in Hallo **RAS** sectie Hallo **tooAzure publiceren** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ead3-112">Click hello **Advanced** link in hello **Remote Access** section of hello **Publish tooAzure** dialog.</span></span>

* <span data-ttu-id="4ead3-113">Open Hallo **eigenschappen** dialoogvenster van uw Azure-project.</span><span class="sxs-lookup"><span data-stu-id="4ead3-113">Open hello **Properties** dialog of your Azure project.</span></span>

<span data-ttu-id="4ead3-114">Wanneer u een nieuw project in de Azure-implementatie maakt, project Hallo geen externe toegang is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4ead3-114">When you create a new Azure deployment project, hello project will not have Remote Access enabled by default.</span></span> <span data-ttu-id="4ead3-115">Echter, u eenvoudig externe toegang kunt inschakelen door het Hallo-gebruikersnaam en wachtwoord opgeven in Hallo **tooAzure publiceren** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ead3-115">However, you can easily enable remote access by specifying hello user name and password in hello **Publish tooAzure** dialog.</span></span> <span data-ttu-id="4ead3-116">Hallo RAS-wachtwoord is versleuteld met behulp van x.509-certificaten.</span><span class="sxs-lookup"><span data-stu-id="4ead3-116">hello Remote Access password is encrypted using X.509 certificates.</span></span> <span data-ttu-id="4ead3-117">Als u geen gebruik geeft u uw eigen certificaat Hallo versleuteling is afhankelijk van een zelfondertekend certificaat met hello Azure Eclipse-invoegtoepassing verzonden.</span><span class="sxs-lookup"><span data-stu-id="4ead3-117">If you do not use provide your own certificate, hello encryption relies on a self-signed certificate shipped with hello Azure Plugin for Eclipse.</span></span> <span data-ttu-id="4ead3-118">Dit zelfondertekende certificaat is in Hallo **cert** map van uw Azure-project opgeslagen beide als een openbaar certificaat-bestand (SampleRemoteAccessPublic.cer) en als een persoonlijke informatie Exchange (PFX)-certificaat (bestand SampleRemoteAccessPrivate.pfx).</span><span class="sxs-lookup"><span data-stu-id="4ead3-118">This self-signed certificate is in hello **cert** folder of your Azure project, stored both as a public certificate file (SampleRemoteAccessPublic.cer) and as a Personal Information Exchange (PFX) certificate file (SampleRemoteAccessPrivate.pfx).</span></span> <span data-ttu-id="4ead3-119">laatste Hallo Hallo persoonlijke sleutel voor Hallo certificaat bevat en heeft deze een standaardwachtwoord **Wachtwoord1**.</span><span class="sxs-lookup"><span data-stu-id="4ead3-119">hello latter contains hello private key for hello certificate, and it has a default password, **Password1**.</span></span> <span data-ttu-id="4ead3-120">Echter, omdat dit wachtwoord algemeen bekend is, kan Hallo standaardcertificaat moet worden gebruikt alleen voor het leren van de toepassing wordt niet voor een productie-implementatie.</span><span class="sxs-lookup"><span data-stu-id="4ead3-120">However, since this password is public knowledge, hello default certificate should be used only for learning purposes, not for a production deployment.</span></span> <span data-ttu-id="4ead3-121">Dus anders dan voor het leren van toepassing als u wilt dat externe sessies tooenabled voor uw implementaties, klikt u Hallo **Geavanceerd** koppeling in Hallo **tooAzure publiceren** dialoogvenster toospecify uw eigen certificaat.</span><span class="sxs-lookup"><span data-stu-id="4ead3-121">So other than for learning purposes, when you want tooenabled remote sessions for your deployments, you should click hello **Advanced** link in hello **Publish tooAzure** dialog toospecify your own certificate.</span></span> <span data-ttu-id="4ead3-122">Houd er rekening mee dat u tooupload Hallo PFX-versie van Hallo certificaat tooyour gehoste service binnen hello Azure Management Portal moet zodanig dat Azure Hallo gebruikerswachtwoord kan ontsleutelen.</span><span class="sxs-lookup"><span data-stu-id="4ead3-122">Note that you'll need tooupload hello PFX version of hello certificate tooyour hosted service within hello Azure Management Portal, so that Azure can decrypt hello user password.</span></span>

<span data-ttu-id="4ead3-123">Hallo overige Hallo zelfstudie ziet u hoe tooenable van RAS voor een Azure-implementatie-project die aanvankelijk is gemaakt met externe toegang uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4ead3-123">hello remainder of hello tutorial shows you how tooenable remote access for an Azure deployment project that was initially created with remote access disabled.</span></span> <span data-ttu-id="4ead3-124">Voor deze zelfstudie maken we een nieuw zelfondertekend certificaat en het pfx-bestand heeft een wachtwoord van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="4ead3-124">For purposes of this tutorial, we'll create a new self-signed certificate, and its .pfx file will have a password of your choice.</span></span> <span data-ttu-id="4ead3-125">U hebt bovendien de optie Hallo van het gebruik van een certificaat zijn uitgegeven door een certificeringsinstantie.</span><span class="sxs-lookup"><span data-stu-id="4ead3-125">You also have hello option of using a certificate issued by a certificate authority.</span></span>

## <a name="how-tooenable-remote-access-after-you-have-deployed-tooazure"></a><span data-ttu-id="4ead3-126">Hoe tooenable RAS nadat u tooAzure hebt geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="4ead3-126">How tooenable Remote Access after you have deployed tooAzure</span></span>
<span data-ttu-id="4ead3-127">tooenable externe toegang nadat u hebt geïmplementeerd tooAzure, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4ead3-127">tooenable remote access after you have deployed tooAzure, use hello following steps:</span></span>

1. <span data-ttu-id="4ead3-128">Meld u aan bij hello Azure management portal met behulp van uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="4ead3-128">Log into hello Azure management portal using your Azure account</span></span>

2. <span data-ttu-id="4ead3-129">In de lijst met **Cloudservices**, selecteer uw geïmplementeerde cloudservice</span><span class="sxs-lookup"><span data-stu-id="4ead3-129">In your list of **Cloud Services**, select your deployed cloud service</span></span>

3. <span data-ttu-id="4ead3-130">Klik in de Hallo cloud service webpagina op Hallo **configureren** koppeling</span><span class="sxs-lookup"><span data-stu-id="4ead3-130">In hello cloud service web page, click hello **Configure** link</span></span>

4. <span data-ttu-id="4ead3-131">Klik op Hallo onderaan configuratiepagina Hallo Hallo **externe** koppeling</span><span class="sxs-lookup"><span data-stu-id="4ead3-131">On hello bottom of hello configuration page, click hello **Remote** link</span></span>

5. <span data-ttu-id="4ead3-132">Wanneer de pop-updialoogvenster hello wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4ead3-132">When hello pop-up dialog box appears:</span></span>
   
   * <span data-ttu-id="4ead3-133">Geef Hallo rol u waarvoor u wilt dat externe toegang tooenable</span><span class="sxs-lookup"><span data-stu-id="4ead3-133">Specify hello Role you for which you want tooenable remote access</span></span>

   * <span data-ttu-id="4ead3-134">Klik op tooselect hello **extern bureaublad inschakelen** selectievakje</span><span class="sxs-lookup"><span data-stu-id="4ead3-134">Click tooselect hello **Enable Remote Desktop** checkbox</span></span>
   
   * <span data-ttu-id="4ead3-135">Geef een gebruikersnaam en wachtwoord die u wilt dat toouse voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="4ead3-135">Specify a user name and password you want toouse for remote access</span></span>
   
   * <span data-ttu-id="4ead3-136">Hallo certificaat toouse selecteren</span><span class="sxs-lookup"><span data-stu-id="4ead3-136">Select hello certificate toouse</span></span>

6. <span data-ttu-id="4ead3-137">Klik op **OK**</span><span class="sxs-lookup"><span data-stu-id="4ead3-137">Click **OK**</span></span> 

<span data-ttu-id="4ead3-138">U ziet een bericht weergegeven dat de wijziging in de configuratie is gemaakt, maar dit kan enkele minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="4ead3-138">You will see a message stating that your configuration change is in progress, which may take a few minutes toocomplete.</span></span> <span data-ttu-id="4ead3-139">Nadat de configuratiewijziging Hallo is voltooid, volgt u de stappen Hallo in Hallo **toolog in op afstand** verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4ead3-139">After hello configuration change has completed, follow hello steps in hello **toolog in remotely** section later in this article.</span></span>

## <a name="how-tooenable-remote-access-in-your-package"></a><span data-ttu-id="4ead3-140">Hoe tooenable externe toegang in het pakket</span><span class="sxs-lookup"><span data-stu-id="4ead3-140">How tooenable Remote Access in your package</span></span>
1. <span data-ttu-id="4ead3-141">Binnen de Eclipse-Project Explorer deelvenster met de rechtermuisknop op uw Azure-project en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="4ead3-141">Within Eclipse's Project Explorer pane, right-click your Azure project and click **Properties**.</span></span>

2. <span data-ttu-id="4ead3-142">In Hallo **eigenschappen** dialoogvenster Vouw **Azure** in het linkerdeelvenster Hallo en klik op **RAS**.</span><span class="sxs-lookup"><span data-stu-id="4ead3-142">In hello **Properties** dialog, expand **Azure** in hello left-hand pane and click **Remote Access**.</span></span>

3. <span data-ttu-id="4ead3-143">In Hallo **RAS** dialoogvenster, zorg ervoor dat **inschakelen van alle rollen tooaccept extern bureaublad-verbindingen met deze aanmeldingsreferenties** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4ead3-143">In hello **Remote Access** dialog, ensure **Enable all roles tooaccept Remote Desktop Connections with these login credentials** is checked.</span></span>

4. <span data-ttu-id="4ead3-144">Geef een gebruikersnaam voor verbinding met extern bureaublad Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ead3-144">Specify a user name for hello Remote Desktop connection.</span></span>

5. <span data-ttu-id="4ead3-145">Geef en Bevestig het wachtwoord voor gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ead3-145">Specify and confirm hello password for hello user.</span></span> <span data-ttu-id="4ead3-146">Hallo waarden gebruikersnaam en het wachtwoord instellen in dit dialoogvenster wordt gebruikt wanneer u een extern bureaublad-verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="4ead3-146">hello user name and password values set in this dialog will be used when you make a Remote Desktop connection.</span></span> <span data-ttu-id="4ead3-147">(Houd er rekening mee dat dit een afzonderlijk wachtwoord van het PFX-wachtwoord is.)</span><span class="sxs-lookup"><span data-stu-id="4ead3-147">(Note that this is a separate password from your PFX password.)</span></span>

6. <span data-ttu-id="4ead3-148">Hallo verloopdatum voor Hallo gebruikersaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="4ead3-148">Specify hello expiration date for hello user account.</span></span>

7. <span data-ttu-id="4ead3-149">Klik op **nieuw** toocreate een nieuw zelfondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="4ead3-149">Click **New** toocreate a new self-signed certificate.</span></span> <span data-ttu-id="4ead3-150">(U kunt ook kunt u een certificaat selecteren van uw systeem werkruimte of het bestand via Hallo **werkruimte** of **bestandssysteem** respectievelijk, maar voor deze zelfstudie we een nieuwe maken knoppen certificaat.)</span><span class="sxs-lookup"><span data-stu-id="4ead3-150">(Alternatively, you could select a certificate from your workspace or file system through hello **Workspace** or **FileSystem** buttons, respectively, but for purposes of this tutorial we'll create a new certificate.)</span></span>

   * <span data-ttu-id="4ead3-151">In Hallo **nieuw certificaat** dialoogvenster Geef en Bevestig Hallo wachtwoord dat u hebt gebruikt voor het PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="4ead3-151">In hello **New Certificate** dialog, specify and confirm hello password you'll use for your PFX file.</span></span>

   * <span data-ttu-id="4ead3-152">Hallo-waarde opgegeven voor het accepteren **naam (CN)**, of gebruik een aangepaste naam.</span><span class="sxs-lookup"><span data-stu-id="4ead3-152">Accept hello value provided for **Name (CN)**, or use a custom name.</span></span>

   * <span data-ttu-id="4ead3-153">Hallo pad en de naam aangegeven waarin Hallo nieuw certificaat in cer-vorm moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4ead3-153">Specify hello path and file name where hello new certificate, in .cer form, will be saved.</span></span> <span data-ttu-id="4ead3-154">Voor deze stap en de volgende stap hello, kunt u Hallo **cert** map van uw Azure-project, maar u bent gratis toochoose een andere locatie.</span><span class="sxs-lookup"><span data-stu-id="4ead3-154">For this step and hello next step, you could use hello **cert** folder of your Azure project, but you're free toochoose another location.</span></span> <span data-ttu-id="4ead3-155">Voor deze zelfstudie gebruiken we **c:\mycert\mycert.cer**.</span><span class="sxs-lookup"><span data-stu-id="4ead3-155">For purposes of this tutorial, we'll use **c:\mycert\mycert.cer**.</span></span> <span data-ttu-id="4ead3-156">(Hallo maken **c:\mycert** map voorafgaande tooproceeding of gebruik een bestaande map, indien gewenst.)</span><span class="sxs-lookup"><span data-stu-id="4ead3-156">(Create hello **c:\mycert** folder prior tooproceeding, or use an existing folder if desired.)</span></span>

   * <span data-ttu-id="4ead3-157">Hallo pad en de naam aangegeven waarin Hallo nieuw certificaat en de persoonlijke sleutel, PFX-indeling moeten worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4ead3-157">Specify hello path and file name where hello new certificate and its private key, in .pfx form, will be saved.</span></span> <span data-ttu-id="4ead3-158">Voor deze zelfstudie gebruiken we **c:\mycert\mycert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="4ead3-158">For purposes of this tutorial, we'll use **c:\mycert\mycert.pfx**.</span></span> <span data-ttu-id="4ead3-159">Uw **nieuw certificaat** dialoogvenster ziet er vergelijkbare toohello volgende (Hallo mappaden bijwerken als u niet gebruikt **c:\mycert**):</span><span class="sxs-lookup"><span data-stu-id="4ead3-159">Your **New Certificate** dialog should look similar toohello following (update hello folder paths if you did not use **c:\mycert**):</span></span>
     
      ![][ic712275]

   * <span data-ttu-id="4ead3-160">Klik op **OK** tooclose hello **nieuw certificaat** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ead3-160">Click **OK** tooclose hello **New Certificate** dialog.</span></span>

8. <span data-ttu-id="4ead3-161">Uw **RAS** dialoogvenster ziet er vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="4ead3-161">Your **Remote Access** dialog should look similar toohello following:</span></span></p>
   
   ![][ic719495]

9. <span data-ttu-id="4ead3-162">Klik op **OK** tooclose hello **RAS** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="4ead3-162">Click **OK** tooclose hello **Remote Access** dialog.</span></span>

<span data-ttu-id="4ead3-163">Uw toepassing opnieuw bouwt, hello set voor implementatie toocloud samenstellen.</span><span class="sxs-lookup"><span data-stu-id="4ead3-163">Rebuild your application, with hello build set for deployment toocloud.</span></span>

## <a name="toolog-in-remotely"></a><span data-ttu-id="4ead3-164">toolog in op afstand</span><span class="sxs-lookup"><span data-stu-id="4ead3-164">toolog in remotely</span></span>
<span data-ttu-id="4ead3-165">Zodra uw rolinstantie gereed is, kunt u extern aanmelden toohello virtuele machine die als host voor uw toepassing fungeert.</span><span class="sxs-lookup"><span data-stu-id="4ead3-165">Once your role instance is ready, you can remotely log in toohello virtual machine that is hosting your application.</span></span>

* <span data-ttu-id="4ead3-166">Als Eclipse op Windows en geselecteerde Hallo **Start extern bureaublad op implementeren** optie tijdens uw tooAzure implementatie u krijgt een verbinding met extern bureaublad-aanmeldingsscherm wanneer uw implementatie wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="4ead3-166">If are using Eclipse on Windows and you selected hello **Start remote desktop on deploy** option during your deployment tooAzure, you will be presented with a Remote Desktop Connection logon screen when your deployment starts.</span></span> <span data-ttu-id="4ead3-167">Wanneer u wordt gevraagd om het Hallo-gebruikersnaam en wachtwoord, Voer Hallo-waarden die u hebt opgegeven voor de externe gebruiker Hallo en kunnen toolog in.</span><span class="sxs-lookup"><span data-stu-id="4ead3-167">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

* <span data-ttu-id="4ead3-168">Een andere manier toolog in op afstand is via Hallo <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span><span class="sxs-lookup"><span data-stu-id="4ead3-168">Another way toolog in remotely is through hello <a href="http://go.microsoft.com/fwlink/?LinkID=512959">Azure Management Portal</a>:</span></span>
  
  * <span data-ttu-id="4ead3-169">Binnen Hallo **Cloudservices** weergave van hello Azure Management portal op uw cloudservice, klik op **exemplaren**, klikt u op een specifiek exemplaar en klik vervolgens op Hallo **Connect**knop.</span><span class="sxs-lookup"><span data-stu-id="4ead3-169">Within hello **Cloud Services** view of hello Azure Management portal, click your cloud service, click **Instances**, click a specific instance, and then click hello **Connect** button.</span></span> <span data-ttu-id="4ead3-170">Hallo **Connect** knop wordt weergegeven als in de opdrachtbalk Hallo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4ead3-170">hello **Connect** button appears as hello following in hello command bar:</span></span>
    
      ![][ic659273]

  * <span data-ttu-id="4ead3-171">Wanneer u op Hallo **Connect** knop, kunt u zich na vragen aan gebruiker tooopen een RDP-bestand.</span><span class="sxs-lookup"><span data-stu-id="4ead3-171">After clicking hello **Connect** button, you will be prompted tooopen an RDP file.</span></span> <span data-ttu-id="4ead3-172">Hallo-bestand openen en volg de aanwijzingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="4ead3-172">Open hello file and follow hello prompts.</span></span> <span data-ttu-id="4ead3-173">(U kan ook Sla dit bestand tooyour lokale computer, en Voer Hallo-bestand door erop te dubbelklikken tooremote log in tooyour virtuele machine zonder toofirst Hallo-beheerportal gaat.)</span><span class="sxs-lookup"><span data-stu-id="4ead3-173">(You could also save this file tooyour local computer, and then run hello file by double-clicking it tooremote log in tooyour virtual machine without needing toofirst go hello management portal.)</span></span>

  * <span data-ttu-id="4ead3-174">Wanneer u wordt gevraagd om het Hallo-gebruikersnaam en wachtwoord, Voer Hallo-waarden die u hebt opgegeven voor de externe gebruiker Hallo en kunnen toolog in.</span><span class="sxs-lookup"><span data-stu-id="4ead3-174">When you are prompted for hello user name and password, enter hello values that you specified for hello remote user and will be able toolog in.</span></span>

> [!NOTE]
> <span data-ttu-id="4ead3-175">Als u op een niet-Windows-besturingssysteem, u moet een extern bureaublad-client die compatibel is met uw besturingssysteem toouse en volg Hallo stappen tooconfigure dat de client met Hallo-instellingen in Hallo RDP-bestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="4ead3-175">If you are on a non-Windows operating system, you need toouse a Remote Desktop client that is compatible with your operating system and follow hello steps tooconfigure that client with hello settings in hello RDP file that you downloaded.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="4ead3-176">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4ead3-176">See Also</span></span>
<span data-ttu-id="4ead3-177">[Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4ead3-177">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="4ead3-178">[Maken van een Hallo wereld-toepassing voor Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4ead3-178">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="4ead3-179">[Hello Azure Toolkit voor Eclipse installeren][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4ead3-179">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="4ead3-180">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="4ead3-180">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic712275]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic712275.png
[ic719495]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719495.png
[ic719494]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic719494.png
[ic659273]: ./media/azure-toolkit-for-eclipse-enabling-remote-access-for-azure-deployments/ic659273.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690951.aspx -->
