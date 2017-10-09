---
title: aaaCreate een Web-App in Azure App Service met behulp van hello Azure SDK voor Java
description: Meer informatie over hoe toocreate een Web-App in Azure App Service programmatisch met behulp van Azure SDK voor Java Hallo.
tags: azure-classic-portal
services: app-service-web
documentationcenter: Java
author: donntrenton
manager: erikre
editor: jimbe
ms.assetid: 8954c456-1275-4d57-aff4-ca7d6374b71e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/25/2016
ms.author: v-donntr
ms.openlocfilehash: 42ba86b7fbb5668b3675198d0c5bb454525f706b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a><span data-ttu-id="01fee-103">Een Web-App maken in Azure App Service met behulp van hello Azure SDK voor Java</span><span class="sxs-lookup"><span data-stu-id="01fee-103">Create a Web App in Azure App Service using hello Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a><span data-ttu-id="01fee-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="01fee-104">Overview</span></span>
<span data-ttu-id="01fee-105">Dit overzicht toont u hoe een Azure-SDK voor Java-toepassing maakt een Web-App in toocreate [Azure App Service][Azure App Service], implementeert u een toepassing tooit.</span><span class="sxs-lookup"><span data-stu-id="01fee-105">This walkthrough shows you how toocreate an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application tooit.</span></span> <span data-ttu-id="01fee-106">Deze bestaat uit twee delen:</span><span class="sxs-lookup"><span data-stu-id="01fee-106">It consists of two parts:</span></span>

* <span data-ttu-id="01fee-107">Deel 1 laat zien hoe toobuild een Java-toepassing die wordt gemaakt een web-app.</span><span class="sxs-lookup"><span data-stu-id="01fee-107">Part 1 demonstrates how toobuild a Java application that creates a web app.</span></span>
* <span data-ttu-id="01fee-108">Deel 2 laat zien hoe toocreate een eenvoudige 'Hallo wereld'-JSP-toepassing en gebruik een FTP-client toodeploy code tooApp Service.</span><span class="sxs-lookup"><span data-stu-id="01fee-108">Part 2 demonstrates how toocreate a simple JSP "Hello World" application, then use an FTP client toodeploy code tooApp Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01fee-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="01fee-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="01fee-110">Software-installaties</span><span class="sxs-lookup"><span data-stu-id="01fee-110">Software Installations</span></span>
<span data-ttu-id="01fee-111">Hallo AzureWebDemo toepassingscode in dit artikel is geschreven met behulp van Azure Java SDK 0.7.0, die u kunt installeren met behulp van Hallo [Web Platform Installer] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="01fee-111">hello AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using hello [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="01fee-112">Bovendien moet u ervoor dat toouse Hallo meest recente versie van Hallo [Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="01fee-112">In addition, make sure toouse hello latest version of hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="01fee-113">Na de installatie van SDK Hallo Hallo afhankelijkheden in uw Eclipse-project bijwerken door het uitvoeren van **Index bijwerken** in **Maven-opslagplaatsen**, voeg deze opnieuw Hallo meest recente versie van elk pakket in Hallo  **Afhankelijkheden** venster.</span><span class="sxs-lookup"><span data-stu-id="01fee-113">After you install hello SDK, update hello dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add hello latest version of each package in hello **Dependencies** window.</span></span> <span data-ttu-id="01fee-114">U kunt Hallo-versie van de geïnstalleerde software in Eclipse controleren door te klikken op **Help > Details van de installatie**; moet u ten minste hebben Hallo volgende versies:</span><span class="sxs-lookup"><span data-stu-id="01fee-114">You can verify hello version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least hello following versions:</span></span>

* <span data-ttu-id="01fee-115">Pakket voor Microsoft Azure-beheerbibliotheken voor Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="01fee-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="01fee-116">Eclipse IDE voor Java EE-ontwikkelaars 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="01fee-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="01fee-117">Maken en configureren van Cloud-bronnen in Azure</span><span class="sxs-lookup"><span data-stu-id="01fee-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="01fee-118">Voordat u deze procedure begint, moet u toohave een actief Azure-abonnement nodig en u een standaard Active Directory (AD) in Azure instellen.</span><span class="sxs-lookup"><span data-stu-id="01fee-118">Before you begin this procedure, you need toohave an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="01fee-119">Maken van een Active Directory (AD) in Azure</span><span class="sxs-lookup"><span data-stu-id="01fee-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="01fee-120">Als u nog geen een Active Directory (AD) voor uw Azure-abonnement, meld u aan bij Hallo [klassieke Azure-portal] [ Azure classic portal] met je Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="01fee-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into hello [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="01fee-121">Als u meerdere abonnementen hebt, klikt u op **abonnementen** en selecteer Hallo standaarddirectory voor Hallo abonnement gewenste toouse voor dit project.</span><span class="sxs-lookup"><span data-stu-id="01fee-121">If you have multiple subscriptions, click **Subscriptions** and select hello default directory for hello subscription you want toouse for this project.</span></span> <span data-ttu-id="01fee-122">Klik vervolgens op **toepassen** tooswitch toothat abonnementweergave.</span><span class="sxs-lookup"><span data-stu-id="01fee-122">Then click **Apply** tooswitch toothat subscription view.</span></span>

1. <span data-ttu-id="01fee-123">Selecteer **Active Directory** in het menu links op Hallo van.</span><span class="sxs-lookup"><span data-stu-id="01fee-123">Select **Active Directory** from hello menu at left.</span></span> <span data-ttu-id="01fee-124">**Klik op Nieuw > Directory > aangepast maken**.</span><span class="sxs-lookup"><span data-stu-id="01fee-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="01fee-125">In **map toevoegen**, selecteer **nieuwe map maken**.</span><span class="sxs-lookup"><span data-stu-id="01fee-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="01fee-126">In **naam**, een mapnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="01fee-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="01fee-127">In **domein**, voer een domeinnaam in.</span><span class="sxs-lookup"><span data-stu-id="01fee-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="01fee-128">Dit is een eenvoudige domeinnaam die is opgenomen in de standaardinstelling met uw directory; Hallo formulier heeft `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="01fee-128">This is a basic domain name that is included by default with your directory; it has hello form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="01fee-129">U kunt een naam op basis van de mapnaam hello of een andere domeinnaam die u bezit.</span><span class="sxs-lookup"><span data-stu-id="01fee-129">You can name it based on hello directory name or another domain name that you own.</span></span> <span data-ttu-id="01fee-130">Later kunt u toevoegen aan een andere domeinnaam die uw organisatie al gebruikt.</span><span class="sxs-lookup"><span data-stu-id="01fee-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="01fee-131">In **land of regio**, selecteer uw land.</span><span class="sxs-lookup"><span data-stu-id="01fee-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="01fee-132">Zie voor meer informatie over AD [wat is er een Azure AD-directory][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="01fee-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="01fee-133">Een Beheercertificaat voor Azure maken</span><span class="sxs-lookup"><span data-stu-id="01fee-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="01fee-134">beheer van certificaten tooauthenticate Hello Azure SDK voor Java gebruikt met Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="01fee-134">hello Azure SDK for Java uses management certificates tooauthenticate with Azure subscriptions.</span></span> <span data-ttu-id="01fee-135">Dit zijn de X.509 v3-certificaten gebruiken van tooauthenticate een clienttoepassing die gebruikmaakt van Hallo Service Management API tooact namens Hallo eigenaar toomanage abonnement abonnementresources.</span><span class="sxs-lookup"><span data-stu-id="01fee-135">These are X.509 v3 certificates you use tooauthenticate a client application that uses hello Service Management API tooact on behalf of hello subscription owner toomanage subscription resources.</span></span>

<span data-ttu-id="01fee-136">Hallo-code in deze procedure maakt gebruik van een zelfondertekend certificaat tooauthenticate met Azure.</span><span class="sxs-lookup"><span data-stu-id="01fee-136">hello code in this procedure uses a self-signed certificate tooauthenticate with Azure.</span></span> <span data-ttu-id="01fee-137">Voor deze procedure u moet toocreate een certificaat en upload het toohello [klassieke Azure-portal] [ Azure classic portal] tevoren.</span><span class="sxs-lookup"><span data-stu-id="01fee-137">For this procedure, you need toocreate a certificate and upload it toohello [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="01fee-138">Dit omvat het Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="01fee-138">This involves hello following steps:</span></span>

* <span data-ttu-id="01fee-139">Een PFX-bestand voor uw clientcertificaat genereren en lokaal opslaat.</span><span class="sxs-lookup"><span data-stu-id="01fee-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="01fee-140">Genereer een beheercertificaat (CER-bestand) van Hallo PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="01fee-140">Generate a management certificate (CER file) from hello PFX file.</span></span>
* <span data-ttu-id="01fee-141">Upload Hallo CER-bestand tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="01fee-141">Upload hello CER file tooyour Azure subscription.</span></span>
* <span data-ttu-id="01fee-142">Converteren naar JKS, Hallo PFX-bestand omdat deze indeling tooauthenticate met behulp van certificaten maakt gebruik van Java.</span><span class="sxs-lookup"><span data-stu-id="01fee-142">Convert hello PFX file into JKS, because Java uses that format tooauthenticate using certificates.</span></span>
* <span data-ttu-id="01fee-143">Schrijven van de toepassing hello verificatiecode, die toohello lokaal JKS-bestand verwijst.</span><span class="sxs-lookup"><span data-stu-id="01fee-143">Write hello application's authentication code, which refers toohello local JKS file.</span></span>

<span data-ttu-id="01fee-144">Wanneer u deze procedure hebt voltooid, Hallo CER certificaat wordt opgeslagen in uw Azure-abonnement en Hallo JKS certificaat wordt opgeslagen op uw lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="01fee-144">When you complete this procedure, hello CER certificate will reside in your Azure subscription and hello JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="01fee-145">Zie voor meer informatie over certificaten voor [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="01fee-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="01fee-146">Een certificaat maken</span><span class="sxs-lookup"><span data-stu-id="01fee-146">Create a certificate</span></span>
<span data-ttu-id="01fee-147">toocreate uw eigen zelf-ondertekend certificaat, open de opdrachtconsole van een op het besturingssysteem en Hallo volgende opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="01fee-147">toocreate your own self-signed certificate, open a command console on your operating system and run hello following commands.</span></span>

> <span data-ttu-id="01fee-148">**Opmerking:** Hallo-computer waarop u deze opdracht uitvoert moet Hallo JDK geïnstalleerd hebben.</span><span class="sxs-lookup"><span data-stu-id="01fee-148">**Note:**  hello computer on which you run this command must have hello JDK installed.</span></span> <span data-ttu-id="01fee-149">Hallo pad toohello keytool is ook afhankelijk van Hallo locatie waarin u Hallo JDK installeren.</span><span class="sxs-lookup"><span data-stu-id="01fee-149">Also, hello path toohello keytool depends on hello location in which you install hello JDK.</span></span> <span data-ttu-id="01fee-150">Zie voor meer informatie [sleutel en certificaat Management Tool (keytool)] [ Key and Certificate Management Tool (keytool)] in Hallo Java online documenten.</span><span class="sxs-lookup"><span data-stu-id="01fee-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in hello Java online docs.</span></span>
> 
> 

<span data-ttu-id="01fee-151">toocreate hello pfx-bestand:</span><span class="sxs-lookup"><span data-stu-id="01fee-151">toocreate hello .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="01fee-152">toocreate hello cer-bestand:</span><span class="sxs-lookup"><span data-stu-id="01fee-152">toocreate hello .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="01fee-153">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="01fee-153">where:</span></span>

* <span data-ttu-id="01fee-154">`<java-install-dir>`Hallo pad toohello directory waarin u Java geïnstalleerd is.</span><span class="sxs-lookup"><span data-stu-id="01fee-154">`<java-install-dir>` is hello path toohello directory in which you installed Java.</span></span>
* <span data-ttu-id="01fee-155">`<keystore-id>`Hallo keystore item-id is (bijvoorbeeld `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="01fee-155">`<keystore-id>` is hello keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="01fee-156">`<cert-store-dir>`Hallo pad toohello map waarin u certificaten toostore is (bijvoorbeeld `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="01fee-156">`<cert-store-dir>` is hello path toohello directory in which you want toostore certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="01fee-157">`<cert-file-name>`Hallo-naam van het Hallo-certificaatbestand (bijvoorbeeld `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="01fee-157">`<cert-file-name>` is hello name of hello certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="01fee-158">`<password>`Hallo wachtwoord u tooprotect Hallo certificaat kiezen Er moet ten minste 6 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="01fee-158">`<password>` is hello password you choose tooprotect hello certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="01fee-159">Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="01fee-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="01fee-160">`<dname>`Hallo X.500-DN-naam toobe alias gekoppeld is en wordt gebruikt als Hallo verlener en onderwerp velden in Hallo zelf-ondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="01fee-160">`<dname>` is hello X.500 Distinguished Name toobe associated with alias, and is used as hello issuer and subject fields in hello self-signed certificate.</span></span>

<span data-ttu-id="01fee-161">Zie voor meer informatie [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="01fee-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-hello-certificate"></a><span data-ttu-id="01fee-162">Hallo-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="01fee-162">Upload hello certificate</span></span>
<span data-ttu-id="01fee-163">tooupload een tooAzure zelf-ondertekend certificaat Ga toohello **instellingen** pagina in de klassieke portal hello, en klik vervolgens op Hallo **Beheercertificaten** tabblad. Klik op **uploaden** onderin Hallo Hallo pagina en navigeer toohello locatie van Hallo CER-bestand dat u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="01fee-163">tooupload a self-signed certificate tooAzure, go toohello **Settings** page in hello classic portal, then click hello **Management Certificates** tab. Click **Upload** at hello bottom of hello page and navigate toohello location of hello CER file you created.</span></span>

#### <a name="convert-hello-pfx-file-into-jks"></a><span data-ttu-id="01fee-164">Hallo PFX-bestand converteren naar JKS</span><span class="sxs-lookup"><span data-stu-id="01fee-164">Convert hello PFX file into JKS</span></span>
<span data-ttu-id="01fee-165">In Hallo Windows-opdrachtpromptvenster (uitgevoerd als beheerder), cd toohello directory met Hallo certificaten en Hallo volgende opdracht uitvoeren waarbij `<java-install-dir>` Hallo map waarin u Java op uw computer hebt geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="01fee-165">In hello Windows Command Prompt (running as admin), cd toohello directory containing hello certificates and run hello following command, where `<java-install-dir>` is hello directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="01fee-166">Voer desgevraagd Hallo bestemming keystore wachtwoord; Dit is Hallo wachtwoord voor Hallo JKS-bestand.</span><span class="sxs-lookup"><span data-stu-id="01fee-166">When prompted, enter hello destination keystore password; this will be hello password for hello JKS file.</span></span>
2. <span data-ttu-id="01fee-167">Voer desgevraagd Hallo bron keystore wachtwoord; Dit is Hallo wachtwoord die u hebt opgegeven voor Hallo PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="01fee-167">When prompted, enter hello source keystore password; this is hello password you specified for hello PFX file.</span></span>

<span data-ttu-id="01fee-168">Hallo twee wachtwoorden beschikt niet over dezelfde Hallo toobe.</span><span class="sxs-lookup"><span data-stu-id="01fee-168">hello two passwords do not have toobe hello same.</span></span> <span data-ttu-id="01fee-169">Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="01fee-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="01fee-170">Een Web-App maken toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="01fee-170">Build a Web App creation application</span></span>
### <a name="create-hello-eclipse-workspace-and-maven-project"></a><span data-ttu-id="01fee-171">Maak Hallo Eclipse werkruimte en Maven-Project</span><span class="sxs-lookup"><span data-stu-id="01fee-171">Create hello Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="01fee-172">In deze sectie maakt u een werkruimte en een Maven-project voor Hallo web-app maken toepassing, met de naam AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="01fee-172">In this section you create a workspace and a Maven project for hello web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="01fee-173">Maak een nieuw Maven-project.</span><span class="sxs-lookup"><span data-stu-id="01fee-173">Create a new Maven project.</span></span> <span data-ttu-id="01fee-174">Klik op **bestand > Nieuw > Maven-Project**.</span><span class="sxs-lookup"><span data-stu-id="01fee-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="01fee-175">In **nieuw Maven-Project**, selecteer **maken van een eenvoudig project** en **standaard werkruimte gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="01fee-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="01fee-176">Op de tweede pagina Hallo van **nieuw Maven-Project**, Hallo volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="01fee-176">On hello second page of **New Maven Project**, specify hello following:</span></span>
   
   * <span data-ttu-id="01fee-177">Groeps-ID:`com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="01fee-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="01fee-178">Artefact-ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="01fee-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="01fee-179">Versie: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="01fee-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="01fee-180">Verpakking: jar</span><span class="sxs-lookup"><span data-stu-id="01fee-180">Packaging: jar</span></span>
   * <span data-ttu-id="01fee-181">Naam: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="01fee-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="01fee-182">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="01fee-182">Click **Finish**.</span></span>
3. <span data-ttu-id="01fee-183">Hallo nieuw project pom.xml-bestand openen in Projectverkenner.</span><span class="sxs-lookup"><span data-stu-id="01fee-183">Open hello new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="01fee-184">Selecteer Hallo **afhankelijkheden** tabblad. Als dit een nieuw project is, worden er geen pakketten nog vermeld.</span><span class="sxs-lookup"><span data-stu-id="01fee-184">Select hello **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="01fee-185">Open Hallo Maven-opslagplaatsen weergeven.</span><span class="sxs-lookup"><span data-stu-id="01fee-185">Open hello Maven Repositories view.</span></span> <span data-ttu-id="01fee-186">**Klik op Venster > weergave tonen > andere > Maven > Maven-opslagplaatsen** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="01fee-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="01fee-187">Hallo **Maven-opslagplaatsen** weergave onderin Hallo Hallo IDE wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="01fee-187">hello **Maven Repositories** view will appear at hello bottom of hello IDE.</span></span>
5. <span data-ttu-id="01fee-188">Open **globale opslagplaatsen**, klik met de rechtermuisknop Hallo **centrale** opslagplaats en selecteer **Rebuild Index**.</span><span class="sxs-lookup"><span data-stu-id="01fee-188">Open **Global Repositories**, right-click hello **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="01fee-189">Deze stap kan enige tijd duren, afhankelijk van Hallo snelheid van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="01fee-189">This step can take several minutes depending on hello speed of your connection.</span></span> <span data-ttu-id="01fee-190">Wanneer het Hallo-index wordt opnieuw gemaakt, ziet u Hallo Microsoft Azure-pakketten in Hallo **centrale** Maven-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="01fee-190">When hello index rebuilds, you should see hello Microsoft Azure packages in hello **central** Maven repository.</span></span>
6. <span data-ttu-id="01fee-191">In **afhankelijkheden**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="01fee-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="01fee-192">In **groep-ID invoeren...**  Voer `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="01fee-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="01fee-193">Selecteer hello-pakketten voor base management en App Service Web Apps management:</span><span class="sxs-lookup"><span data-stu-id="01fee-193">Select hello packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="01fee-194">**Opmerking:** als u Hallo afhankelijkheden na de release van een nieuwe versie bijwerkt, moet u toore-elk Hallo afhankelijkheden in deze lijst toevoegen.</span><span class="sxs-lookup"><span data-stu-id="01fee-194">**Note:** If you are updating hello dependencies after a new version release, you need toore-add each of hello dependencies in this list.</span></span>
   > <span data-ttu-id="01fee-195">Nadat u op **toevoegen** en selecteer elke afhankelijkheid wordt dit weergegeven met het nieuwe versienummer in Hallo Hallo **afhankelijkheden** lijst.</span><span class="sxs-lookup"><span data-stu-id="01fee-195">After you click **Add** and select each dependency, it appears with hello new version number in hello **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="01fee-196">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="01fee-196">Click **OK**.</span></span> <span data-ttu-id="01fee-197">Hallo Azure pakketten wordt weergegeven in Hallo **afhankelijkheden** lijst.</span><span class="sxs-lookup"><span data-stu-id="01fee-197">hello Azure packages then appear in hello **Dependencies** list.</span></span>

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a><span data-ttu-id="01fee-198">Java-Code tooCreate schrijven van een Web-App door aanroepen hello Azure SDK</span><span class="sxs-lookup"><span data-stu-id="01fee-198">Writing Java Code tooCreate a Web App by Calling hello Azure SDK</span></span>
<span data-ttu-id="01fee-199">Schrijf nu Hallo-code die de API-in hello Azure SDK voor Java toocreate Hallo App Service-web-app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="01fee-199">Next, write hello code that calls APIs in hello Azure SDK for Java toocreate hello App Service web app.</span></span>

1. <span data-ttu-id="01fee-200">Maak een Java-klasse toocontain Hallo belangrijkste vermelding punt code.</span><span class="sxs-lookup"><span data-stu-id="01fee-200">Create a Java class toocontain hello main entry point code.</span></span> <span data-ttu-id="01fee-201">In Projectverkenner met de rechtermuisknop op Hallo projectknooppunt en selecteer **Nieuw > klasse**.</span><span class="sxs-lookup"><span data-stu-id="01fee-201">In Project Explorer, right-click on hello project node and select **New > Class**.</span></span>
2. <span data-ttu-id="01fee-202">In **nieuwe Java-klasse**, naam Hallo klasse `WebCreator` en controleer Hallo **openbare statische void main** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="01fee-202">In **New Java Class**, name hello class `WebCreator` and check hello **public static void main** checkbox.</span></span> <span data-ttu-id="01fee-203">Hallo selecties ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="01fee-203">hello selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="01fee-204">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="01fee-204">Click **Finish**.</span></span> <span data-ttu-id="01fee-205">Hallo WebCreator.java bestand weergegeven in de Projectverkenner.</span><span class="sxs-lookup"><span data-stu-id="01fee-205">hello WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a><span data-ttu-id="01fee-206">Hello Azure API tooCreate het aanroepen van een App Service-Web-App</span><span class="sxs-lookup"><span data-stu-id="01fee-206">Calling hello Azure API tooCreate an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="01fee-207">Vereiste imports toevoegen</span><span class="sxs-lookup"><span data-stu-id="01fee-207">Add necessary imports</span></span>
<span data-ttu-id="01fee-208">Voeg in WebCreator.java, Hallo na invoer; deze invoer bieden toegang tooclasses in Hallo management-bibliotheken voor het verbruik van Azure-API's:</span><span class="sxs-lookup"><span data-stu-id="01fee-208">In WebCreator.java, add hello following imports; these imports provide access tooclasses in hello management libraries for consuming Azure APIs:</span></span>

    // General imports
    import java.net.URI;
    import java.util.ArrayList;

    // Imports for Exceptions
    import java.io.IOException;
    import java.net.URISyntaxException;
    import javax.xml.parsers.ParserConfigurationException;
    import com.microsoft.windowsazure.exception.ServiceException;
    import org.xml.sax.SAXException;

    // Imports for Azure App Service management configuration
    import com.microsoft.windowsazure.Configuration;
    import com.microsoft.windowsazure.management.configuration.ManagementConfiguration;

    // Service management imports for App Service Web Apps creation
    import com.microsoft.windowsazure.management.websites.*;
    import com.microsoft.windowsazure.management.websites.models.*;

    // Imports for authentication
    import com.microsoft.windowsazure.core.utils.KeyStoreType;


#### <a name="define-hello-main-entry-point-class"></a><span data-ttu-id="01fee-209">Hallo belangrijkste vermelding punt klasse definiëren</span><span class="sxs-lookup"><span data-stu-id="01fee-209">Define hello main entry point class</span></span>
<span data-ttu-id="01fee-210">Hallo hoofdklasse omdat doel Hallo AzureWebDemo toepassing hello toocreate een App Service-Web-App, een naam voor deze toepassing `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="01fee-210">Because hello purpose of hello AzureWebDemo application is toocreate an App Service Web App, name hello main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="01fee-211">Deze klasse biedt Hallo belangrijkste vermelding punt code waarmee hello Azure Service Management API toocreate Hallo web-app wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="01fee-211">This class provides hello main entry point code that calls hello Azure Service Management API toocreate hello web app.</span></span>

<span data-ttu-id="01fee-212">Hallo volgende parameterdefinities voor Hallo web-app en webruimte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="01fee-212">Add hello following parameter definitions for hello web app and webspace.</span></span> <span data-ttu-id="01fee-213">U moet uw eigen Azure-abonnement-ID en certificaat informatie tooprovide.</span><span class="sxs-lookup"><span data-stu-id="01fee-213">You will need tooprovide your own Azure subscription ID and certificate information.</span></span>

    public class WebAppCreator {

        // Parameter definitions used for authentication.
        private static String uri = "https://management.core.windows.net/";
        private static String subscriptionId = "<subscription-id>";
        private static String keyStoreLocation = "<certificate-store-path>";
        private static String keyStorePassword = "<certificate-password>";

        // Define web app parameter values.
        private static String webAppName = "WebDemoWebApp";
        private static String domainName = ".azurewebsites.net";
        private static String webSpaceName = WebSpaceNames.WESTUSWEBSPACE;
        private static String appServicePlanName = "WebDemoAppServicePlan";

<span data-ttu-id="01fee-214">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="01fee-214">where:</span></span>

* <span data-ttu-id="01fee-215">`<subscription-id>`hello Azure-abonnement-ID die u toocreate Hallo resource wilt is.</span><span class="sxs-lookup"><span data-stu-id="01fee-215">`<subscription-id>` is hello Azure subscription ID in which you want toocreate hello resource.</span></span>
* <span data-ttu-id="01fee-216">`<certificate-store-path>`Hallo pad en bestandsnaam toohello JKS bestand in uw directory van de winkel lokale certificaatarchief is.</span><span class="sxs-lookup"><span data-stu-id="01fee-216">`<certificate-store-path>` is hello path and filename toohello JKS file in your local certificate store directory.</span></span> <span data-ttu-id="01fee-217">Bijvoorbeeld: `C:/Certificates/CertificateName.jks` voor Linux en `C:\Certificates\CertificateName.jks` voor Windows.</span><span class="sxs-lookup"><span data-stu-id="01fee-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="01fee-218">`<certificate-password>`u hebt opgegeven tijdens het maken van uw certificaat JKS Hallo-wachtwoord is.</span><span class="sxs-lookup"><span data-stu-id="01fee-218">`<certificate-password>` is hello password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="01fee-219">`webAppName`de naam die u kiezen; deze procedure gebruikt u de naam van de Hallo `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="01fee-219">`webAppName` can be any name you choose; this procedure uses hello name `WebDemoWebApp`.</span></span> <span data-ttu-id="01fee-220">de volledige domeinnaam Hallo is Hallo `webAppName` Hello `domainName` toegevoegd, dus in dit geval Hallo volledige domein is `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="01fee-220">hello full domain name is hello `webAppName` with hello `domainName` appended, so in this case hello full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="01fee-221">`domainName`moet worden opgegeven, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="01fee-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="01fee-222">`webSpaceName`moet een Hallo-waarden die zijn gedefinieerd in Hallo [WebSpaceNames] [ WebSpaceNames] klasse.</span><span class="sxs-lookup"><span data-stu-id="01fee-222">`webSpaceName` should be one of hello values defined in hello [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="01fee-223">`appServicePlanName`moet worden opgegeven, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="01fee-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="01fee-224">**Opmerking:** telkens wanneer u deze toepassing uitvoeren, moet u toochange Hallo-waarde van `webAppName` en `appServicePlanName` (of verwijderen van de web-app Hallo op Hallo Azure Portal) voordat u Hallo toepassing opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="01fee-224">**Note:** Each time you run this application, you need toochange hello value of `webAppName` and `appServicePlanName` (or delete hello web app on hello Azure Portal) before running hello application again.</span></span> <span data-ttu-id="01fee-225">Anders mislukt uitvoering omdat hello dezelfde resource al in Azure bestaat.</span><span class="sxs-lookup"><span data-stu-id="01fee-225">Otherwise, execution will fail because hello same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-hello-web-creation-method"></a><span data-ttu-id="01fee-226">Hallo-methode voor het maken van web definiëren</span><span class="sxs-lookup"><span data-stu-id="01fee-226">Define hello web creation method</span></span>
<span data-ttu-id="01fee-227">Definieer vervolgens een methode toocreate Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="01fee-227">Next, define a method toocreate hello web app.</span></span> <span data-ttu-id="01fee-228">Deze methode `createWebApp`, Hallo parameters van Hallo web-app en Hallo webruimte bevat.</span><span class="sxs-lookup"><span data-stu-id="01fee-228">This method, `createWebApp`, specifies hello parameters of hello web app and hello webspace.</span></span> <span data-ttu-id="01fee-229">Ook maakt en configureert deze Hallo App Service Web Apps management-client, die wordt gedefinieerd door Hallo [WebSiteManagementClient] [ WebSiteManagementClient] object.</span><span class="sxs-lookup"><span data-stu-id="01fee-229">It also creates and configures hello App Service Web Apps management client, which is defined by hello [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="01fee-230">Hallo-management-client is sleutel toocreating Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="01fee-230">hello management client is key toocreating Web Apps.</span></span> <span data-ttu-id="01fee-231">Het biedt de RESTful-web-services waarmee toepassingen toomanage web-apps (het uitvoeren van bewerkingen zoals maken, bijwerken en verwijderen) door het Hallo servicebeheer-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="01fee-231">It provides RESTful web services that allow applications toomanage web apps (performing operations such as create, update, and delete) by calling hello service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for hello App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path toohello JKS file
            keyStorePassword,  // Password for hello JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create hello App Service Web Apps management client toocall Azure APIs
        // and pass it hello App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for hello web app with hello specified parameters.
        WebHostingPlanCreateParameters appServicePlanParams = new WebHostingPlanCreateParameters();
        appServicePlanParams.setName(appServicePlanName);
        appServicePlanParams.setSKU(SkuOptions.Free);
        webAppManagementClient.getWebHostingPlansOperations().create(webSpaceName, appServicePlanParams);

        // Set webspace parameters.
        WebSiteCreateParameters.WebSpaceDetails webSpaceDetails = new WebSiteCreateParameters.WebSpaceDetails();
        webSpaceDetails.setGeoRegion(GeoRegionNames.WESTUS);
        webSpaceDetails.setPlan(WebSpacePlanNames.VIRTUALDEDICATEDPLAN);
        webSpaceDetails.setName(webSpaceName);

        // Set web app parameters.
        // Note that hello server farm name takes hello Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define hello web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create hello web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output hello HTTP status code of hello response; 200 indicates hello request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output hello name of hello web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="01fee-232">Hallo code Hallo HTTP-statuscode van antwoord Hallo die aangeeft of geslaagd of mislukt wordt uitgevoerd en als dit lukt, wordt de uitvoer Hallo-naam van de web-app gemaakt Hallo.</span><span class="sxs-lookup"><span data-stu-id="01fee-232">hello code will output hello HTTP status of hello response indicating success or failure, and if successful, will output hello name of hello created web app.</span></span>

#### <a name="define-hello-main-method"></a><span data-ttu-id="01fee-233">Hallo main() methode definiëren</span><span class="sxs-lookup"><span data-stu-id="01fee-233">Define hello main() method</span></span>
<span data-ttu-id="01fee-234">Geef Hallo main() methode code die aanroepen createWebApp() toocreate Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="01fee-234">Provide hello main() method code that calls createWebApp() toocreate hello web app.</span></span>

<span data-ttu-id="01fee-235">Tenslotte roept `createWebApp` van `main`:</span><span class="sxs-lookup"><span data-stu-id="01fee-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a><span data-ttu-id="01fee-236">Hallo-toepassing uitvoeren en controleer of web-apps maken</span><span class="sxs-lookup"><span data-stu-id="01fee-236">Run hello application and verify web app creation</span></span>
<span data-ttu-id="01fee-237">tooverify die uw toepassing wordt uitgevoerd, klikt u op **uitvoeren > Voer**.</span><span class="sxs-lookup"><span data-stu-id="01fee-237">tooverify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="01fee-238">Wanneer de toepassing hello is voltooid wordt uitgevoerd, ziet u Hallo uitvoer in Hallo Eclipse-console te volgen:</span><span class="sxs-lookup"><span data-stu-id="01fee-238">When hello application completes running, you should see hello following output in hello Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="01fee-239">Meld u aan bij de klassieke Azure-portal Hallo en klik op **Web-Apps**.</span><span class="sxs-lookup"><span data-stu-id="01fee-239">Log into hello Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="01fee-240">Hallo nieuwe web-app moet worden weergegeven in de lijst met de Hallo-Web-Apps binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="01fee-240">hello new web app should appear in hello Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-toohello-web-app"></a><span data-ttu-id="01fee-241">Een toepassing toohello Web-App implementeren</span><span class="sxs-lookup"><span data-stu-id="01fee-241">Deploying an Application toohello Web App</span></span>
<span data-ttu-id="01fee-242">Nadat u AzureWebDemo hebt uitgevoerd en gemaakte Hallo nieuwe web-app, meld u aan bij de klassieke portal hello, klikt u op **Web-Apps**, en selecteer **WebDemoWebApp** in Hallo **Web-Apps** lijst.</span><span class="sxs-lookup"><span data-stu-id="01fee-242">After you have run AzureWebDemo and created hello new web app, log into hello classic portal, click **Web Apps**, and select **WebDemoWebApp** in hello **Web Apps** list.</span></span> <span data-ttu-id="01fee-243">Klik in de dashboardpagina Hallo van web-app op **Bladeren** (of klik op Hallo-URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span><span class="sxs-lookup"><span data-stu-id="01fee-243">In hello web app's dashboard page, click **Browse** (or click hello URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit.</span></span> <span data-ttu-id="01fee-244">U ziet een pagina lege tijdelijke aanduiding omdat geen inhoud gepubliceerde toohello web-app nog is.</span><span class="sxs-lookup"><span data-stu-id="01fee-244">You will see a blank placeholder page, because no content has been published toohello web app yet.</span></span>

<span data-ttu-id="01fee-245">U wordt vervolgens een 'Hallo wereld'-toepassing maken en deze toohello web-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="01fee-245">Next you will create a "Hello World" application and deploy it toohello web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="01fee-246">Een JSP Hallo wereld-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="01fee-246">Create a JSP Hello World application</span></span>
#### <a name="create-hello-application"></a><span data-ttu-id="01fee-247">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="01fee-247">Create hello application</span></span>
<span data-ttu-id="01fee-248">In volgorde toodemonstrate hoe toodeploy een webpagina van de toohello toepassing hello na procedure ziet u hoe toocreate een eenvoudige "Hallo wereld" Java-toepassing en upload het toohello App Service Web-App die uw toepassing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="01fee-248">In order toodemonstrate how toodeploy an application toohello web, hello following procedure shows you how toocreate a simple "Hello World" Java application and upload it toohello App Service Web App that your application created.</span></span>

1. <span data-ttu-id="01fee-249">Klik op **bestand > Nieuw > Dynamic webproject**.</span><span class="sxs-lookup"><span data-stu-id="01fee-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="01fee-250">Noem deze `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="01fee-250">Name it `JSPHello`.</span></span> <span data-ttu-id="01fee-251">U hoeft geen andere instellingen in dit dialoogvenster niet toochange.</span><span class="sxs-lookup"><span data-stu-id="01fee-251">You do not need toochange any other settings in this dialog.</span></span> <span data-ttu-id="01fee-252">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="01fee-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="01fee-253">Vouw in Projectverkenner Hallo **JSPHello** project, met de rechtermuisknop op **WebContent**, klikt u vervolgens op **Nieuw > JSP-bestand**.</span><span class="sxs-lookup"><span data-stu-id="01fee-253">In Project Explorer, expand hello **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="01fee-254">Naam in het dialoogvenster Nieuw JSP-bestand Hallo Hallo nieuw bestand `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="01fee-254">In hello New JSP File dialog, name hello new file `index.jsp`.</span></span> <span data-ttu-id="01fee-255">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="01fee-255">Click **Next**.</span></span>
3. <span data-ttu-id="01fee-256">In Hallo **JSP-sjabloon selecteren** dialoogvenster **nieuw JSP-bestand (html)** en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="01fee-256">In hello **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="01fee-257">Voeg in index.jsp, na de code in Hallo Hallo `<head>` en `<body>` tag secties:</span><span class="sxs-lookup"><span data-stu-id="01fee-257">In index.jsp, add hello following code in hello `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a><span data-ttu-id="01fee-258">Hallo wereld Hallo toepassing uitvoert in localhost</span><span class="sxs-lookup"><span data-stu-id="01fee-258">Run hello Hello World application in localhost</span></span>
<span data-ttu-id="01fee-259">Voordat u deze toepassing uitvoert, moet u tooconfigure enkele eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="01fee-259">Before you run this application, you need tooconfigure a few properties.</span></span>

1. <span data-ttu-id="01fee-260">Klik met de rechtermuisknop Hallo **JSPHello** project en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="01fee-260">Right-click hello **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="01fee-261">In Hallo **eigenschappen** dialoogvenster: Selecteer **Javabuild-pad**, selecteer Hallo **rangschikken en exporteren** tabblad controle **JRE systeembibliotheek**, klikt u vervolgens op **Up** toomove het toohello boven aan Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="01fee-261">In hello **Properties** dialog: select **Java Build Path**, select hello **Order and Export** tab, check **JRE System Library**, then click **Up** toomove it toohello top of hello list.</span></span>
   
    ![][4]
3. <span data-ttu-id="01fee-262">Ook in Hallo **eigenschappen** dialoogvenster: Selecteer **Runtimes gericht** en klik op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="01fee-262">Also in hello **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="01fee-263">In Hallo **nieuwe Server Runtime-omgeving** dialoogvenster, selecteert u een server, zoals **Apache Tomcat v7.0** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="01fee-263">In hello **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="01fee-264">In Hallo **Tomcat-Server** dialoogvenster, set **naam** te`Apache Tomcat v7.0`, en stel **Tomcat-installatiedirectory** toohello directory waarin u de versie van Hallo geïnstalleerd Gewenste toouse Tomcat-server.</span><span class="sxs-lookup"><span data-stu-id="01fee-264">In hello **Tomcat Server** dialog, set **Name** too`Apache Tomcat v7.0`, and set **Tomcat Installation Directory** toohello directory in which you installed hello version of Tomcat server you want toouse.</span></span>
   
    ![][5]
   
    <span data-ttu-id="01fee-265">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="01fee-265">Click **Finish**.</span></span>
5. <span data-ttu-id="01fee-266">U terugkeren toohello **Runtimes gericht** pagina Hallo **eigenschappen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="01fee-266">You then return toohello **Targeted Runtimes** page of hello **Properties** dialog.</span></span> <span data-ttu-id="01fee-267">Selecteer **Apache Tomcat v7.0**, klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="01fee-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="01fee-268">In Eclipse hello **uitvoeren** menu, klikt u op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="01fee-268">In hello Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="01fee-269">In Hallo **uitvoeren als** dialoogvenster Selecteer **uitgevoerd op Server**.</span><span class="sxs-lookup"><span data-stu-id="01fee-269">In hello **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="01fee-270">In Hallo **uitgevoerd op Server** dialoogvenster Selecteer **Tomcat v7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="01fee-270">In hello **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="01fee-271">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="01fee-271">Click **Finish**.</span></span>
7. <span data-ttu-id="01fee-272">Wanneer Hallo toepassing wordt uitgevoerd, ziet u Hallo **JSPHello** pagina wordt weergegeven in een venster localhost in Eclipse (`http://localhost:8080/JSPHello/`), weer te geven Hallo volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="01fee-272">When hello application runs, you should see hello **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying hello following message:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a><span data-ttu-id="01fee-273">Hallo toepassing als een WAR exporteren</span><span class="sxs-lookup"><span data-stu-id="01fee-273">Export hello application as a WAR</span></span>
<span data-ttu-id="01fee-274">Hallo web project-bestanden exporteren als een web-archiefbestand (WAR), zodat u toohello web-app kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="01fee-274">Export hello web project files as a web archive (WAR) file so that you can deploy it toohello web app.</span></span> <span data-ttu-id="01fee-275">Hallo volgende web project-bestanden bevinden zich in Hallo WebContent map:</span><span class="sxs-lookup"><span data-stu-id="01fee-275">hello following web project files reside in hello WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="01fee-276">Hallo WebContent map met de rechtermuisknop en selecteer **exporteren**.</span><span class="sxs-lookup"><span data-stu-id="01fee-276">Right-click hello WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="01fee-277">In Hallo **exporteren Selecteer** dialoogvenster, klikt u op **Web > WAR** bestand en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="01fee-277">In hello **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="01fee-278">In Hallo **WAR exporteren** dialoogvenster Hallo src map te selecteren in het huidige project Hallo en Hallo-naam van Hallo WAR-bestand aan Hallo einde bevatten.</span><span class="sxs-lookup"><span data-stu-id="01fee-278">In hello **WAR Export** dialog, select hello src directory in hello current project, and include hello name of hello WAR file at hello end.</span></span> <span data-ttu-id="01fee-279">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="01fee-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="01fee-280">Zie voor meer informatie over het implementeren van WAR bestanden [toevoegen van een Java-toepassing tooAzure App Service Web Apps](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="01fee-280">For more information on deploying WAR files, see [Add a Java application tooAzure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-hello-hello-world-application-using-ftp"></a><span data-ttu-id="01fee-281">Hallo Hallo wereld-toepassing met behulp van FTP implementeren</span><span class="sxs-lookup"><span data-stu-id="01fee-281">Deploying hello Hello World Application Using FTP</span></span>
<span data-ttu-id="01fee-282">Selecteer een toepassing van derden FTP-client toopublish Hallo.</span><span class="sxs-lookup"><span data-stu-id="01fee-282">Select a third-party FTP client toopublish hello application.</span></span> <span data-ttu-id="01fee-283">Deze procedure wordt beschreven twee opties: Hallo Kudu-console is ingebouwd in Azure. en FileZilla, een populaire hulpmiddel met een handige, grafische gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="01fee-283">This procedure describes two options: hello Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="01fee-284">**Opmerking:** hello Azure Toolkit voor Eclipse implementatie toostorage accounts ondersteunt en cloud services, maar ondersteunt geen implementatie tooweb apps.</span><span class="sxs-lookup"><span data-stu-id="01fee-284">**Note:** hello Azure Toolkit for Eclipse supports deployment toostorage accounts and cloud services, but does not currently support deployment tooweb apps.</span></span> <span data-ttu-id="01fee-285">U kunt implementeren toostorage accounts en cloud services met behulp van een Azure-implementatieproject, zoals beschreven in [maken van een Hallo wereld-toepassing voor Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), maar niet tooweb apps.</span><span class="sxs-lookup"><span data-stu-id="01fee-285">You can deploy toostorage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not tooweb apps.</span></span> <span data-ttu-id="01fee-286">Andere methoden zoals FTP of GitHub tootransfer bestanden tooyour web-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="01fee-286">Use other methods such as FTP or GitHub tootransfer files tooyour web app.</span></span>
> 
> <span data-ttu-id="01fee-287">**Opmerking:** niet raadzaam met FTP van Hallo Windows-opdrachtpromptvenster (Hallo FTP.EXE opdrachtregelprogramma dat wordt geleverd met Windows).</span><span class="sxs-lookup"><span data-stu-id="01fee-287">**Note:** We do not recommend using FTP from hello Windows command prompt (hello command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="01fee-288">FTP-clients die gebruikmaken van actieve FTP, zoals FTP.EXE, vaak een failover toowork firewalls.</span><span class="sxs-lookup"><span data-stu-id="01fee-288">FTP clients that use active FTP, such as FTP.EXE, often fail toowork over firewalls.</span></span> <span data-ttu-id="01fee-289">Actieve FTP wordt een interne op basis van LAN-adres, toowhich een FTP-server, tooconnect waarschijnlijk niet.</span><span class="sxs-lookup"><span data-stu-id="01fee-289">Active FTP specifies an internal LAN-based address, toowhich an FTP server will likely fail tooconnect.</span></span>
> 
> 

<span data-ttu-id="01fee-290">Zie voor meer informatie over implementatie tooan App Service web-app met FTP Hallo volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="01fee-290">For more information on deployment tooan App Service web app using FTP, see hello following topics:</span></span>

* [<span data-ttu-id="01fee-291">Implementeren met behulp van een FTP-programma</span><span class="sxs-lookup"><span data-stu-id="01fee-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="01fee-292">Implementatiereferenties instellen</span><span class="sxs-lookup"><span data-stu-id="01fee-292">Set up deployment credentials</span></span>
<span data-ttu-id="01fee-293">Zorg ervoor dat u hebt uitgevoerd Hallo **AzureWebDemo** toepassing toocreate een web-app.</span><span class="sxs-lookup"><span data-stu-id="01fee-293">Make sure you have run hello **AzureWebDemo** application toocreate a web app.</span></span> <span data-ttu-id="01fee-294">U kunt bestanden toothis locatie worden overgebracht.</span><span class="sxs-lookup"><span data-stu-id="01fee-294">You will transfer files toothis location.</span></span>

1. <span data-ttu-id="01fee-295">Meld u aan bij de klassieke portal Hallo en klik op **Web-Apps**.</span><span class="sxs-lookup"><span data-stu-id="01fee-295">Log into hello classic portal and click **Web Apps**.</span></span> <span data-ttu-id="01fee-296">Zorg ervoor dat **WebDemoWebApp** wordt weergegeven in de lijst Hallo van web-apps en zorg ervoor dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="01fee-296">Make sure **WebDemoWebApp** appears in hello list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="01fee-297">Klik op **WebDemoWebApp** tooopen de **Dashboard** pagina.</span><span class="sxs-lookup"><span data-stu-id="01fee-297">Click **WebDemoWebApp** tooopen its **Dashboard** page.</span></span>
2. <span data-ttu-id="01fee-298">Op Hallo **Dashboard** pagina onder **snel in één oogopslag**, klikt u op **instellen van referenties voor uw implementatie** (als u de referenties voor implementatie al hebt, leest dit  **Opnieuw instellen van referenties voor uw implementatie**).</span><span class="sxs-lookup"><span data-stu-id="01fee-298">On hello **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="01fee-299">Referenties voor implementatie zijn gekoppeld aan een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="01fee-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="01fee-300">U moet toospecify een gebruikersnaam en wachtwoord waarmee u kunt met behulp van Git en FTP-toodeploy.</span><span class="sxs-lookup"><span data-stu-id="01fee-300">You need toospecify a username and password that you can use toodeploy using Git and FTP.</span></span> <span data-ttu-id="01fee-301">U kunt deze referenties toodeploy tooany web-app gebruiken in alle Azure-abonnementen die zijn gekoppeld aan je Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="01fee-301">You can use these credentials toodeploy tooany web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="01fee-302">Geef referenties op Git en FTP-implementatie in het dialoogvenster Hallo en record Hallo gebruikersnaam en wachtwoord voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="01fee-302">Provide Git and FTP deployment credentials in hello dialog, and record hello username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="01fee-303">Gegevens van de FTP-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="01fee-303">Get FTP connection information</span></span>
<span data-ttu-id="01fee-304">toouse FTP-toodeploy toepassing bestanden toohello nieuwe web-app, moet u de verbindingsgegevens tooobtain.</span><span class="sxs-lookup"><span data-stu-id="01fee-304">toouse FTP toodeploy application files toohello newly created web app, you need tooobtain connection information.</span></span> <span data-ttu-id="01fee-305">Er zijn twee manieren tooobtain verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="01fee-305">There are two ways tooobtain connection information.</span></span> <span data-ttu-id="01fee-306">Eenzijdige toovisit Hallo van web-app is **Dashboard** pagina; hello andere manier is publicatieprofiel toodownload Hallo van web-app.</span><span class="sxs-lookup"><span data-stu-id="01fee-306">One way is toovisit hello web app's **Dashboard** page; hello other way is toodownload hello web app's publish profile.</span></span> <span data-ttu-id="01fee-307">Hallo publicatieprofiel is een XML-bestand informatie zoals de FTP-host en het aanmeldingsaccount referenties voor uw web-apps in Azure App Service bevat.</span><span class="sxs-lookup"><span data-stu-id="01fee-307">hello publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="01fee-308">U kunt deze gebruikersnaam en wachtwoord toodeploy tooany web-app gebruiken in alle abonnementen die zijn gekoppeld aan hello Azure-account, niet alleen op deze aanbieding.</span><span class="sxs-lookup"><span data-stu-id="01fee-308">You can use this username and password toodeploy tooany web app in all subscriptions associated with hello Azure account, not only this one.</span></span>

<span data-ttu-id="01fee-309">tooobtain FTP verbindingsinformatie van de blade Hallo van web-app in Hallo [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="01fee-309">tooobtain FTP connection information from hello web app's blade in hello [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="01fee-310">Onder **Essentials**, vindt en kopieert Hallo **FTP-hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="01fee-310">Under **Essentials**, find and copy hello **FTP hostname**.</span></span> <span data-ttu-id="01fee-311">Dit is een soortgelijke URI te`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="01fee-311">This is a URI similar too`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="01fee-312">Onder **Essentials**, vindt en kopieert **FTP-/ Implementatiegebruiker gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="01fee-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="01fee-313">Dit heeft Hallo formulier *webappname\deployment-username*; bijvoorbeeld `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="01fee-313">This will have hello form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="01fee-314">publicatieprofiel tooobtain FTP-verbindingsinformatie van Hallo:</span><span class="sxs-lookup"><span data-stu-id="01fee-314">tooobtain FTP connection information from hello publish profile:</span></span>

1. <span data-ttu-id="01fee-315">Klik op Hallo van web-app blade **Get publicatieprofiel**.</span><span class="sxs-lookup"><span data-stu-id="01fee-315">In hello web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="01fee-316">Hiermee wordt een lokaal station voor .publishsettings-bestand tooyour gedownload.</span><span class="sxs-lookup"><span data-stu-id="01fee-316">This will download a .publishsettings file tooyour local drive.</span></span>
2. <span data-ttu-id="01fee-317">Hallo .publishsettings-bestand openen in een XML-editor of een teksteditor en zoek Hallo `<publishProfile>` element die `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="01fee-317">Open hello .publishsettings file in an XML editor or text editor and find hello `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="01fee-318">Het moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="01fee-318">It should look like hello following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="01fee-319">Houd er rekening mee dat Hallo web-app `publishProfile` instellingen toewijzen toohello FileZilla sitebeheerder instellingen als volgt:</span><span class="sxs-lookup"><span data-stu-id="01fee-319">Note that hello web app's `publishProfile` settings map toohello FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="01fee-320">`publishUrl`is gelijk aan Hallo **FTP-hostnaam**, Hallo waarde die u instelt in **Host**.</span><span class="sxs-lookup"><span data-stu-id="01fee-320">`publishUrl` is hello same as **FTP host name**, hello value you set in **Host**.</span></span>
* <span data-ttu-id="01fee-321">`publishMethod="FTP"`betekent dat u instelt **Protocol** te**FTP - File Transfer Protocol**, en **versleuteling** te**gewone FTP gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="01fee-321">`publishMethod="FTP"` means that you set **Protocol** too**FTP - File Transfer Protocol**, and **Encryption** too**Use plain FTP**.</span></span>
* <span data-ttu-id="01fee-322">`userName`en `userPWD` zijn de sleutels voor Hallo werkelijke gebruikersnaam en wachtwoord waarden die u hebt opgegeven dat wanneer u referenties voor Hallo implementatie opnieuw.</span><span class="sxs-lookup"><span data-stu-id="01fee-322">`userName` and `userPWD` are keys for hello actual username and password values you specified when you reset hello deployment credentials.</span></span> <span data-ttu-id="01fee-323">`userName`is gelijk aan Hallo **implementatie / FTP-gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="01fee-323">`userName` is hello same as **Deployment / FTP user**.</span></span> <span data-ttu-id="01fee-324">Ze wijzen te**gebruiker** en **wachtwoord** in FileZilla.</span><span class="sxs-lookup"><span data-stu-id="01fee-324">They map too**User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="01fee-325">`ftpPassiveMode="True"`betekent dat Hallo FTP-site gebruik maakt van Passief FTP-overdracht; Selecteer **passieve** op Hallo **Overdrachtinstellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="01fee-325">`ftpPassiveMode="True"` means that hello FTP site uses passive FTP transfer; select **Passive** on hello **Transfer Settings** tab.</span></span>

#### <a name="configure-hello-web-app-toohost-a-java-application"></a><span data-ttu-id="01fee-326">Hallo Web-App toohost een Java-toepassing configureren</span><span class="sxs-lookup"><span data-stu-id="01fee-326">Configure hello Web App toohost a Java application</span></span>
<span data-ttu-id="01fee-327">Voordat u de toepassing hello publiceert, moet u toochange enkele configuratie-instellingen zodat hello web-app een Java-toepassing hosten kan.</span><span class="sxs-lookup"><span data-stu-id="01fee-327">Before you publish hello application, you need toochange a few configuration settings so that hello web app can host a Java application.</span></span>

1. <span data-ttu-id="01fee-328">Ga in de klassieke portal Hallo toohello van web-app **Dashboard** pagina en klik op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="01fee-328">In hello classic portal, go toohello web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="01fee-329">Op Hallo **configureren** pagina, Hallo na instellingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="01fee-329">On hello **Configure** page, specify hello following settings.</span></span>
2. <span data-ttu-id="01fee-330">In **Java-versie** Hallo standaardwaarde is **uit**; Selecteer Hallo Java-versie de doelen van uw toepassing, bijvoorbeeld 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="01fee-330">In **Java version** hello default is **Off**; select hello Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="01fee-331">Nadat u dit doet, zorg er ook die **webcontainer** tooa versie van Tomcat-Server is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="01fee-331">After you do this, also make sure that **Web container** is set tooa version of Tomcat Server.</span></span>
3. <span data-ttu-id="01fee-332">In **standaarddocumenten**, het toevoegen van index.jsp en omhoog toohello boven aan Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="01fee-332">In **Default Documents**, add index.jsp and move it up toohello top of hello list.</span></span> <span data-ttu-id="01fee-333">(de standaardlocatie Hallo voor web-apps is hostingstart.html.)</span><span class="sxs-lookup"><span data-stu-id="01fee-333">(hello default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="01fee-334">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="01fee-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="01fee-335">Uw toepassing publiceren via Kudu</span><span class="sxs-lookup"><span data-stu-id="01fee-335">Publish your application using Kudu</span></span>
<span data-ttu-id="01fee-336">Eenzijdige toopublish Hallo toepassing is toouse hello die kudu debug console die is ingebouwd in Azure.</span><span class="sxs-lookup"><span data-stu-id="01fee-336">One way toopublish hello application is toouse hello Kudu debug console built into Azure.</span></span> <span data-ttu-id="01fee-337">Kudu bekend toobe stabiel en consistent zijn met App Service Web Apps en Tomcat-Server.</span><span class="sxs-lookup"><span data-stu-id="01fee-337">Kudu is known toobe stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="01fee-338">U openen Hallo-console voor Hallo web-app door te bladeren tooa URL Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="01fee-338">You access hello console for hello web app by browsing tooa URL of hello following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="01fee-339">Voor deze procedure bevindt Hallo Kudu-console zich op Hallo na URL; Blader toothis locatie:</span><span class="sxs-lookup"><span data-stu-id="01fee-339">For this procedure, hello Kudu console is located at hello following URL; browse toothis location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="01fee-340">Selecteer in het bovenste menu Hallo **Console fouten opsporen > CMD**.</span><span class="sxs-lookup"><span data-stu-id="01fee-340">From hello top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="01fee-341">Hallo-console vanaf de opdrachtregel, navigeert u in te`/site/wwwroot` (of klik op `site`, klikt u vervolgens `wwwroot` in Hallo directoryweergave bovenaan Hallo Hallo pagina):</span><span class="sxs-lookup"><span data-stu-id="01fee-341">In hello console command line, navigate too`/site/wwwroot` (or click `site`, then `wwwroot` in hello directory view at hello top of hello page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="01fee-342">Nadat u hebt opgegeven **Java-versie**, Tomcat-server moet een map webapps maken.</span><span class="sxs-lookup"><span data-stu-id="01fee-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="01fee-343">Navigeer in Hallo console vanaf de opdrachtregel, toohello map WebApps:</span><span class="sxs-lookup"><span data-stu-id="01fee-343">In hello console command line, navigate toohello webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="01fee-344">Sleep JSPHello.war van `<project-path>/JSPHello/src/` en zet het neer in Hallo Kudu directoryweergave onder `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="01fee-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into hello Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="01fee-345">Sleep niet het toohello 'Hier naartoe slepen tooupload en zip' gebied omdat Tomcat wordt behouden.</span><span class="sxs-lookup"><span data-stu-id="01fee-345">Do not drag it toohello "Drag here tooupload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="01fee-346">Op de eerste JSPHello.war wordt weergegeven in Hallo directory gebied zelfstandig:</span><span class="sxs-lookup"><span data-stu-id="01fee-346">At first JSPHello.war appears in hello directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="01fee-347">Tomcat-Server wordt Hallo WAR-bestand uitpakken naar een map met uitgepakte JSPHello in korte tijd (waarschijnlijk minder dan 5 minuten).</span><span class="sxs-lookup"><span data-stu-id="01fee-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip hello WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="01fee-348">Klik op Hallo ROOT directory toosee of index.jsp heeft uitgepakt en er wordt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="01fee-348">Click hello ROOT directory toosee whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="01fee-349">Als dit het geval is, gaat u terug toohello webapps directory toosee of Hallo uitgepakt JSPHello map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="01fee-349">If so, navigate back toohello webapps directory toosee whether hello unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="01fee-350">Als u deze items niet ziet, wacht en herhaalt.</span><span class="sxs-lookup"><span data-stu-id="01fee-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="01fee-351">Uw toepassing publiceren via FileZilla (optioneel)</span><span class="sxs-lookup"><span data-stu-id="01fee-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="01fee-352">Een ander hulpprogramma kunt u toopublish Hallo toepassing is FileZilla, een populaire van derden FTP-client met een handige, grafische gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="01fee-352">Another tool you can use toopublish hello application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="01fee-353">U kunt downloaden en installeren van FileZilla van [http://filezilla-project.org/](http://filezilla-project.org/) als u nog geen deze.</span><span class="sxs-lookup"><span data-stu-id="01fee-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="01fee-354">Zie voor meer informatie over het gebruik van de client Hallo Hallo [FileZilla documentatie](https://wiki.filezilla-project.org/Documentation) en dit blogbericht op [FTP-Clients - deel 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="01fee-354">For more information on using hello client, see hello [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="01fee-355">Klik in de FileZilla, **bestand > sitebeheerder**.</span><span class="sxs-lookup"><span data-stu-id="01fee-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="01fee-356">In Hallo **sitebeheerder** dialoogvenster, klikt u op **nieuwe Site**.</span><span class="sxs-lookup"><span data-stu-id="01fee-356">In hello **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="01fee-357">Een nieuwe lege FTP-site wordt weergegeven in **Selecteer vermelding** waarin u wordt gevraagd een naam tooprovide.</span><span class="sxs-lookup"><span data-stu-id="01fee-357">A new blank FTP site will appear in **Select Entry** prompting you tooprovide a name.</span></span> <span data-ttu-id="01fee-358">Naam voor deze procedure `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="01fee-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="01fee-359">Op Hallo **algemene** tabblad, geeft u Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="01fee-359">On hello **General** tab, specify hello following settings:</span></span>
   
   * <span data-ttu-id="01fee-360">**Host:** Enter Hallo **FTP-hostnaam** die u hebt gekopieerd uit Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="01fee-360">**Host:** Enter hello **FTP Host Name** that you copied from hello dashboard.</span></span>
   * <span data-ttu-id="01fee-361">**Poort:** (dit leeg laat, als dit een passief-overdracht is en Hallo server Hallo poort toouse bepaalt.)</span><span class="sxs-lookup"><span data-stu-id="01fee-361">**Port:** (Leave this blank, as this is a passive transfer and hello server will determine hello port toouse.)</span></span>
   * <span data-ttu-id="01fee-362">**Protocol:** FTP File Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="01fee-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="01fee-363">**Versleuteling:** gewone FTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="01fee-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="01fee-364">**Aanmeldingstype:** normaal</span><span class="sxs-lookup"><span data-stu-id="01fee-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="01fee-365">**Gebruiker:** Enter Hallo implementatie / FTP-gebruiker die u hebt gekopieerd uit Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="01fee-365">**User:** Enter hello Deployment / FTP user that you copied from hello dashboard.</span></span> <span data-ttu-id="01fee-366">Dit is Hallo volledige FTP-gebruikersnaam, waarvoor Hallo formulier *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="01fee-366">This is hello full FTP username, which has hello form *webappname\username*.</span></span>
   * <span data-ttu-id="01fee-367">**Wachtwoord:** Hallo-wachtwoord opgeven die u hebt opgegeven tijdens het Hallo-implementatiereferenties instellen.</span><span class="sxs-lookup"><span data-stu-id="01fee-367">**Password:** Enter hello password that you specified when you set hello deployment credentials.</span></span>
     
     <span data-ttu-id="01fee-368">Op Hallo **Overdrachtinstellingen** tabblad **passieve**.</span><span class="sxs-lookup"><span data-stu-id="01fee-368">On hello **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="01fee-369">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="01fee-369">Click **Connect**.</span></span> <span data-ttu-id="01fee-370">Als geslaagd, FileZilla van console wordt weergegeven een `Status: Connected` bericht en probleem een `LIST` toolist Hallo Mapinhoud opdracht.</span><span class="sxs-lookup"><span data-stu-id="01fee-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command toolist hello directory contents.</span></span>
4. <span data-ttu-id="01fee-371">In Hallo **lokale** deelvenster van de site, selecteer Hallo bronmap in welke Hallo JSPHello.war-bestand bevindt zich; Hallo-pad moet vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="01fee-371">In hello **Local** site panel, select hello source directory in which hello JSPHello.war file resides; hello path will be similar toohello following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="01fee-372">In Hallo **externe** deelvenster van de site, selecteer Hallo doelmap.</span><span class="sxs-lookup"><span data-stu-id="01fee-372">In hello **Remote** site panel, select hello destination folder.</span></span> <span data-ttu-id="01fee-373">U gaat implementeren Hallo WAR-bestand toohello `webapps` map onder basis-Hallo van web-app.</span><span class="sxs-lookup"><span data-stu-id="01fee-373">You will deploy hello WAR file toohello `webapps` directory under hello web app's root.</span></span> <span data-ttu-id="01fee-374">Navigeer te`/site/wwwroot`, met de rechtermuisknop op `wwwroot`, en selecteer **maken directory**.</span><span class="sxs-lookup"><span data-stu-id="01fee-374">Navigate too`/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="01fee-375">Gebruikersnaammap hello `webapps` en voert u deze map.</span><span class="sxs-lookup"><span data-stu-id="01fee-375">Name hello directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="01fee-376">JSPHello.war te dragen`/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="01fee-376">Transfer JSPHello.war too`/site/wwwroot/webapps`.</span></span> <span data-ttu-id="01fee-377">Selecteer JSPHello.war in Hallo **lokale** lijst bestand, met de rechtermuisknop op het en selecteert u **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="01fee-377">Select JSPHello.war in hello **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="01fee-378">U ziet het weergegeven in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="01fee-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="01fee-379">Na het kopiëren van JSPHello.war toohello map WebApps Tomcat-Server automatisch wordt uitgepakt (uitpakken)-bestanden in de WAR-bestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="01fee-379">After you copy JSPHello.war toohello webapps directory, Tomcat Server will automatically unpack (unzip) hello files in hello WAR file.</span></span> <span data-ttu-id="01fee-380">Hoewel Tomcat-Server bijna onmiddellijk uitpakken begint, kan het lang duren voordat tijd (mogelijk uren) voor Hallo bestanden tooappear in Hallo FTP-client.</span><span class="sxs-lookup"><span data-stu-id="01fee-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for hello files tooappear in hello FTP client.</span></span>

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a><span data-ttu-id="01fee-381">Hallo Hallo wereld-toepassing op Hallo Web-App uitvoeren</span><span class="sxs-lookup"><span data-stu-id="01fee-381">Run hello Hello World application on hello Web App</span></span>
1. <span data-ttu-id="01fee-382">Nadat u hebt geüpload Hallo WAR-bestand en geverifieerd dat Tomcat-server is gemaakt met een uitgepakte `JSPHello` map te bladeren`http://webdemowebapp.azurewebsites.net/JSPHello` toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="01fee-382">After you have uploaded hello WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse too`http://webdemowebapp.azurewebsites.net/JSPHello` toorun hello application.</span></span>
   
   > <span data-ttu-id="01fee-383">**Opmerking:** als u op **Bladeren** vanuit de klassieke portal hello, krijgt u mogelijk Hallo standaard webpagina, spreken "deze op basis van Java-webtoepassing is gemaakt."</span><span class="sxs-lookup"><span data-stu-id="01fee-383">**Note:** If you click **Browse** from hello classic portal, you might get hello default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="01fee-384">U hebt mogelijk toorefresh Hallo webpagina in volgorde tooview Hallo toepassing uitvoer in plaats van de webpagina die standaard Hallo.</span><span class="sxs-lookup"><span data-stu-id="01fee-384">You might have toorefresh hello webpage in order tooview hello application output instead of hello default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="01fee-385">Wanneer de toepassing hello wordt uitgevoerd, ziet u een webpagina Hello volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="01fee-385">When hello application runs, you should see a web page with hello following output:</span></span>
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="01fee-386">Azure-resources opschonen</span><span class="sxs-lookup"><span data-stu-id="01fee-386">Clean up Azure resources</span></span>
<span data-ttu-id="01fee-387">Deze procedure maakt u een App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="01fee-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="01fee-388">U wordt gefactureerd voor Hallo resource als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="01fee-388">You will be billed for hello resource as long as it exists.</span></span> <span data-ttu-id="01fee-389">Tenzij u van plan toocontinue Hallo web-app gebruiken voor testdoeleinden of ontwikkeling bent, moet u stoppen of te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="01fee-389">Unless you plan toocontinue using hello web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="01fee-390">Een web-app is gestopt, nog steeds een kleine vergoeding worden, maar u kunt deze opnieuw starten op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="01fee-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="01fee-391">Als u een web-app verwijdert, worden alle gegevens die u hebt geüpload tooit gewist.</span><span class="sxs-lookup"><span data-stu-id="01fee-391">Deleting a web app erases all data you have uploaded tooit.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

[1]: ./media/java-create-azure-website-using-java-sdk/eclipse-maven-repositories-rebuild-index.png
[2]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-java-class.png
[3]: ./media/java-create-azure-website-using-java-sdk/eclipse-new-dynamic-web-project.png
[4]: ./media/java-create-azure-website-using-java-sdk/eclipse-java-build-path.png
[5]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-tomcat-server.png
[6]: ./media/java-create-azure-website-using-java-sdk/eclipse-targeted-runtimes-properties-page.png
[7]: ./media/java-create-azure-website-using-java-sdk/eclipse-run-on-server.png
[8]: ./media/java-create-azure-website-using-java-sdk/kudu-console-drag-drop.png
[9]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-1.png
[10]: ./media/java-create-azure-website-using-java-sdk/kudu-console-jsphello-war-2.png


[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Platform Installer]: http://go.microsoft.com/fwlink/?LinkID=252838
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh690946.aspx
[Azure classic portal]: https://manage.windowsazure.com
[What is an Azure AD directory]: http://technet.microsoft.com/library/jj573650.aspx
[Create and Upload a Management Certificate for Azure]: ../cloud-services/cloud-services-certs-create.md
[Key and Certificate Management Tool (keytool)]: http://docs.oracle.com/javase/6/docs/technotes/tools/windows/keytool.html
[WebSiteManagementClient]: http://azure.github.io/azure-sdk-for-java/com/microsoft/azure/management/websites/WebSiteManagementClient.html
[WebSpaceNames]: http://dl.windowsazure.com/javadoc/com/microsoft/windowsazure/management/websites/models/WebSpaceNames.html
[Azure Portal]: https://portal.azure.com
