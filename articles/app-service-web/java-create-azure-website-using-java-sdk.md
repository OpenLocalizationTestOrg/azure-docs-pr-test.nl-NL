---
title: Een Web-App maken in Azure App Service met de Azure SDK voor Java
description: Informatie over het maken van een Web-App in Azure App Service programmatisch met behulp van de Azure SDK voor Java.
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
ms.openlocfilehash: 08bb53de8cf437a5a2b1c3b38bce9f81b8349493
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a><span data-ttu-id="b7328-103">Een Web-App maken in Azure App Service met de Azure SDK voor Java</span><span class="sxs-lookup"><span data-stu-id="b7328-103">Create a Web App in Azure App Service using the Azure SDK for Java</span></span>
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a><span data-ttu-id="b7328-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b7328-104">Overview</span></span>
<span data-ttu-id="b7328-105">Dit overzicht toont u het maken van een Azure-SDK voor Java-toepassing maakt een Web-App in [Azure App Service][Azure App Service], vervolgens een toepassing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="b7328-105">This walkthrough shows you how to create an Azure SDK for Java application that creates a Web App in [Azure App Service][Azure App Service], then deploy an application to it.</span></span> <span data-ttu-id="b7328-106">Deze bestaat uit twee delen:</span><span class="sxs-lookup"><span data-stu-id="b7328-106">It consists of two parts:</span></span>

* <span data-ttu-id="b7328-107">Deel 1 laat zien hoe een Java-toepassing bouwt die een web-app maakt.</span><span class="sxs-lookup"><span data-stu-id="b7328-107">Part 1 demonstrates how to build a Java application that creates a web app.</span></span>
* <span data-ttu-id="b7328-108">Deel 2 laat zien hoe u voor het maken van een eenvoudige 'Hallo wereld'-JSP-toepassing en gebruik een FTP-client om code te implementeren in App Service.</span><span class="sxs-lookup"><span data-stu-id="b7328-108">Part 2 demonstrates how to create a simple JSP "Hello World" application, then use an FTP client to deploy code to App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7328-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b7328-109">Prerequisites</span></span>
### <a name="software-installations"></a><span data-ttu-id="b7328-110">Software-installaties</span><span class="sxs-lookup"><span data-stu-id="b7328-110">Software Installations</span></span>
<span data-ttu-id="b7328-111">De code van de toepassing AzureWebDemo in dit artikel is geschreven met behulp van Azure Java SDK 0.7.0, die u kunt installeren met behulp van de [Web Platform Installer] [ Web Platform Installer] (WebPI).</span><span class="sxs-lookup"><span data-stu-id="b7328-111">The AzureWebDemo application code in this article was written using Azure Java SDK 0.7.0, which you can install using the [Web Platform Installer][Web Platform Installer] (WebPI).</span></span> <span data-ttu-id="b7328-112">Bovendien moet u de nieuwste versie van de [Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse].</span><span class="sxs-lookup"><span data-stu-id="b7328-112">In addition, make sure to use the latest version of the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse].</span></span> <span data-ttu-id="b7328-113">Nadat u de SDK hebt geïnstalleerd, de afhankelijkheden in uw Eclipse-project bijwerken door het uitvoeren van **Index bijwerken** in **Maven-opslagplaatsen**, voeg deze opnieuw de meest recente versie van elk pakket in de **afhankelijkheden** venster.</span><span class="sxs-lookup"><span data-stu-id="b7328-113">After you install the SDK, update the dependencies in your Eclipse project by running **Update Index** in **Maven Repositories**, then re-add the latest version of each package in the **Dependencies** window.</span></span> <span data-ttu-id="b7328-114">U kunt de versie van de geïnstalleerde software in Eclipse controleren door te klikken op **Help > Details van de installatie**; u moet ten minste beschikken over de volgende versies:</span><span class="sxs-lookup"><span data-stu-id="b7328-114">You can verify the version of your installed software in Eclipse by clicking **Help > Installation Details**; you should have at least the following versions:</span></span>

* <span data-ttu-id="b7328-115">Pakket voor Microsoft Azure-beheerbibliotheken voor Java 0.7.0.20150309</span><span class="sxs-lookup"><span data-stu-id="b7328-115">Package for Microsoft Azure Libraries for Java 0.7.0.20150309</span></span>
* <span data-ttu-id="b7328-116">Eclipse IDE voor Java EE-ontwikkelaars 4.4.2.20150219</span><span class="sxs-lookup"><span data-stu-id="b7328-116">Eclipse IDE for Java EE Developers 4.4.2.20150219</span></span>

### <a name="create-and-configure-cloud-resources-in-azure"></a><span data-ttu-id="b7328-117">Maken en configureren van Cloud-bronnen in Azure</span><span class="sxs-lookup"><span data-stu-id="b7328-117">Create and Configure Cloud Resources in Azure</span></span>
<span data-ttu-id="b7328-118">Voordat u deze procedure begint, moet u een actief Azure-abonnement hebt en u een standaard Active Directory (AD) in Azure instellen.</span><span class="sxs-lookup"><span data-stu-id="b7328-118">Before you begin this procedure, you need to have an active Azure subscription and set up a default Active Directory (AD) on Azure.</span></span>

### <a name="create-an-active-directory-ad-in-azure"></a><span data-ttu-id="b7328-119">Maken van een Active Directory (AD) in Azure</span><span class="sxs-lookup"><span data-stu-id="b7328-119">Create an Active Directory (AD) in Azure</span></span>
<span data-ttu-id="b7328-120">Als u nog geen een Active Directory (AD) voor uw Azure-abonnement, meld u aan bij de [klassieke Azure-portal] [ Azure classic portal] met je Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="b7328-120">If you do not already have an Active Directory (AD) on your Azure subscription, log into the [Azure classic portal][Azure classic portal] with your Microsoft account.</span></span> <span data-ttu-id="b7328-121">Als u meerdere abonnementen hebt, klikt u op **abonnementen** en selecteer de standaardmap voor het abonnement dat u wilt gebruiken voor dit project.</span><span class="sxs-lookup"><span data-stu-id="b7328-121">If you have multiple subscriptions, click **Subscriptions** and select the default directory for the subscription you want to use for this project.</span></span> <span data-ttu-id="b7328-122">Klik vervolgens op **toepassen** overschakelen naar de abonnementweergave van dit.</span><span class="sxs-lookup"><span data-stu-id="b7328-122">Then click **Apply** to switch to that subscription view.</span></span>

1. <span data-ttu-id="b7328-123">Selecteer **Active Directory** in het menu links.</span><span class="sxs-lookup"><span data-stu-id="b7328-123">Select **Active Directory** from the menu at left.</span></span> <span data-ttu-id="b7328-124">**Klik op Nieuw > Directory > aangepast maken**.</span><span class="sxs-lookup"><span data-stu-id="b7328-124">**Click New > Directory > Custom Create**.</span></span>
2. <span data-ttu-id="b7328-125">In **map toevoegen**, selecteer **nieuwe map maken**.</span><span class="sxs-lookup"><span data-stu-id="b7328-125">In **Add Directory**, select **Create New Directory**.</span></span>
3. <span data-ttu-id="b7328-126">In **naam**, een mapnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="b7328-126">In **Name**, enter a directory name.</span></span>
4. <span data-ttu-id="b7328-127">In **domein**, voer een domeinnaam in.</span><span class="sxs-lookup"><span data-stu-id="b7328-127">In **Domain**, enter a domain name.</span></span> <span data-ttu-id="b7328-128">Dit is een eenvoudige domeinnaam die is opgenomen in de standaardinstelling met uw directory; het formulier heeft `<domain_name>.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="b7328-128">This is a basic domain name that is included by default with your directory; it has the form `<domain_name>.onmicrosoft.com`.</span></span> <span data-ttu-id="b7328-129">U kunt een naam op basis van de mapnaam of een andere domeinnaam die u bezit.</span><span class="sxs-lookup"><span data-stu-id="b7328-129">You can name it based on the directory name or another domain name that you own.</span></span> <span data-ttu-id="b7328-130">Later kunt u toevoegen aan een andere domeinnaam die uw organisatie al gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b7328-130">Later, you can add another domain name that your organization already uses.</span></span>
5. <span data-ttu-id="b7328-131">In **land of regio**, selecteer uw land.</span><span class="sxs-lookup"><span data-stu-id="b7328-131">In **Country or region**, select your locale.</span></span>

<span data-ttu-id="b7328-132">Zie voor meer informatie over AD [wat is er een Azure AD-directory][What is an Azure AD directory]?</span><span class="sxs-lookup"><span data-stu-id="b7328-132">For more information on AD, see [What is an Azure AD directory][What is an Azure AD directory]?</span></span>

### <a name="create-a-management-certificate-for-azure"></a><span data-ttu-id="b7328-133">Een Beheercertificaat voor Azure maken</span><span class="sxs-lookup"><span data-stu-id="b7328-133">Create a Management Certificate for Azure</span></span>
<span data-ttu-id="b7328-134">De Azure SDK voor Java maakt gebruik van certificaten voor verificatie met Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="b7328-134">The Azure SDK for Java uses management certificates to authenticate with Azure subscriptions.</span></span> <span data-ttu-id="b7328-135">Dit zijn de X.509 v3-certificaten met u een clienttoepassing die gebruikmaakt van de Service Management API te handelen namens de eigenaar van het abonnement voor het beheren van abonnementresources verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b7328-135">These are X.509 v3 certificates you use to authenticate a client application that uses the Service Management API to act on behalf of the subscription owner to manage subscription resources.</span></span>

<span data-ttu-id="b7328-136">De code in deze procedure gebruikt een zelfondertekend certificaat te verifiëren bij Azure.</span><span class="sxs-lookup"><span data-stu-id="b7328-136">The code in this procedure uses a self-signed certificate to authenticate with Azure.</span></span> <span data-ttu-id="b7328-137">Voor deze procedure moet u een certificaat maken en uploaden naar de [klassieke Azure-portal] [ Azure classic portal] tevoren.</span><span class="sxs-lookup"><span data-stu-id="b7328-137">For this procedure, you need to create a certificate and upload it to the [Azure classic portal][Azure classic portal] beforehand.</span></span> <span data-ttu-id="b7328-138">Dit omvat de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="b7328-138">This involves the following steps:</span></span>

* <span data-ttu-id="b7328-139">Een PFX-bestand voor uw clientcertificaat genereren en lokaal opslaat.</span><span class="sxs-lookup"><span data-stu-id="b7328-139">Generate a PFX file representing your client certificate and save it locally.</span></span>
* <span data-ttu-id="b7328-140">Genereer een beheercertificaat (CER-bestand) van het PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="b7328-140">Generate a management certificate (CER file) from the PFX file.</span></span>
* <span data-ttu-id="b7328-141">Het CER-bestand uploaden naar uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b7328-141">Upload the CER file to your Azure subscription.</span></span>
* <span data-ttu-id="b7328-142">Converteren naar JKS, het PFX-bestand omdat Java die indeling gebruikt om te verifiëren met behulp van certificaten.</span><span class="sxs-lookup"><span data-stu-id="b7328-142">Convert the PFX file into JKS, because Java uses that format to authenticate using certificates.</span></span>
* <span data-ttu-id="b7328-143">Schrijven van de toepassing authenticatie code, die naar het lokale JKS-bestand verwijst.</span><span class="sxs-lookup"><span data-stu-id="b7328-143">Write the application's authentication code, which refers to the local JKS file.</span></span>

<span data-ttu-id="b7328-144">Wanneer u deze procedure hebt voltooid, het CER-certificaat wordt opgeslagen in uw Azure-abonnement en het certificaat JKS wordt opgeslagen op uw lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="b7328-144">When you complete this procedure, the CER certificate will reside in your Azure subscription and the JKS certificate will reside on your local drive.</span></span> <span data-ttu-id="b7328-145">Zie voor meer informatie over certificaten voor [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="b7328-145">For more information on management certificates, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="create-a-certificate"></a><span data-ttu-id="b7328-146">Een certificaat maken</span><span class="sxs-lookup"><span data-stu-id="b7328-146">Create a certificate</span></span>
<span data-ttu-id="b7328-147">Open de opdrachtconsole van een op het besturingssysteem en voer de volgende opdrachten voor het maken van uw eigen zelf-ondertekend certificaat.</span><span class="sxs-lookup"><span data-stu-id="b7328-147">To create your own self-signed certificate, open a command console on your operating system and run the following commands.</span></span>

> <span data-ttu-id="b7328-148">**Opmerking:** de computer waarop u deze opdracht uitvoert de JDK die geïnstalleerd moet hebben.</span><span class="sxs-lookup"><span data-stu-id="b7328-148">**Note:**  The computer on which you run this command must have the JDK installed.</span></span> <span data-ttu-id="b7328-149">Het pad naar de keytool is ook afhankelijk van de locatie waarin u de JDK installeren.</span><span class="sxs-lookup"><span data-stu-id="b7328-149">Also, the path to the keytool depends on the location in which you install the JDK.</span></span> <span data-ttu-id="b7328-150">Zie voor meer informatie [sleutel en certificaat Management Tool (keytool)] [ Key and Certificate Management Tool (keytool)] in de online documentatie voor Java.</span><span class="sxs-lookup"><span data-stu-id="b7328-150">For more information, see [Key and Certificate Management Tool (keytool)][Key and Certificate Management Tool (keytool)] in the Java online docs.</span></span>
> 
> 

<span data-ttu-id="b7328-151">Het pfx-bestand maken:</span><span class="sxs-lookup"><span data-stu-id="b7328-151">To create the .pfx file:</span></span>

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

<span data-ttu-id="b7328-152">Het cer-bestand maken:</span><span class="sxs-lookup"><span data-stu-id="b7328-152">To create the .cer file:</span></span>

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

<span data-ttu-id="b7328-153">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="b7328-153">where:</span></span>

* <span data-ttu-id="b7328-154">`<java-install-dir>`het pad naar de map waarin u Java geïnstalleerd is.</span><span class="sxs-lookup"><span data-stu-id="b7328-154">`<java-install-dir>` is the path to the directory in which you installed Java.</span></span>
* <span data-ttu-id="b7328-155">`<keystore-id>`de id van de vermelding keystore (bijvoorbeeld `AzureRemoteAccess`).</span><span class="sxs-lookup"><span data-stu-id="b7328-155">`<keystore-id>` is the keystore entry identifier (for example, `AzureRemoteAccess`).</span></span>
* <span data-ttu-id="b7328-156">`<cert-store-dir>`het pad naar de map waarin u wilt opslaan van certificaten (bijvoorbeeld `C:/Certificates`).</span><span class="sxs-lookup"><span data-stu-id="b7328-156">`<cert-store-dir>` is the path to the directory in which you want to store certificates (for example `C:/Certificates`).</span></span>
* <span data-ttu-id="b7328-157">`<cert-file-name>`de naam van het certificaatbestand (bijvoorbeeld `AzureWebDemoCert`).</span><span class="sxs-lookup"><span data-stu-id="b7328-157">`<cert-file-name>` is the name of the certificate file (for example `AzureWebDemoCert`).</span></span>
* <span data-ttu-id="b7328-158">`<password>`is het wachtwoord dat u wilt beveiligen van het certificaat; Er moet ten minste 6 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="b7328-158">`<password>` is the password you choose to protect the certificate; it must be at least 6 characters long.</span></span> <span data-ttu-id="b7328-159">Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="b7328-159">You can enter no password, although this is not recommended.</span></span>
* <span data-ttu-id="b7328-160">`<dname>`de X.500-DN-naam moet worden gekoppeld met de alias is en als de verlener en onderwerp velden in het zelfondertekende certificaat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b7328-160">`<dname>` is the X.500 Distinguished Name to be associated with alias, and is used as the issuer and subject fields in the self-signed certificate.</span></span>

<span data-ttu-id="b7328-161">Zie voor meer informatie [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].</span><span class="sxs-lookup"><span data-stu-id="b7328-161">For more information, see [Create and Upload a Management Certificate for Azure][Create and Upload a Management Certificate for Azure].</span></span>

#### <a name="upload-the-certificate"></a><span data-ttu-id="b7328-162">Het certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="b7328-162">Upload the certificate</span></span>
<span data-ttu-id="b7328-163">Als u wilt een zelfondertekend certificaat uploaden naar Azure, gaat u naar de **instellingen** pagina in de klassieke portal en klik vervolgens op de **Beheercertificaten** tabblad. Klik op **uploaden** aan de onderkant van de pagina en navigeer naar de locatie van het CER-bestand dat u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7328-163">To upload a self-signed certificate to Azure, go to the **Settings** page in the classic portal, then click the **Management Certificates** tab. Click **Upload** at the bottom of the page and navigate to the location of the CER file you created.</span></span>

#### <a name="convert-the-pfx-file-into-jks"></a><span data-ttu-id="b7328-164">Het PFX-bestand converteren naar JKS</span><span class="sxs-lookup"><span data-stu-id="b7328-164">Convert the PFX file into JKS</span></span>
<span data-ttu-id="b7328-165">In de opdrachtprompt van Windows (uitgevoerd als beheerder), cd naar de map met de certificaten en voer de volgende opdracht, waarbij `<java-install-dir>` is de directory waarin u Java op uw computer hebt geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="b7328-165">In the Windows Command Prompt (running as admin), cd to the directory containing the certificates and run the following command, where `<java-install-dir>` is the directory in which you installed Java on your computer:</span></span>

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. <span data-ttu-id="b7328-166">Voer desgevraagd het wachtwoord van de bestemming keystore; Dit is het wachtwoord voor het bestand JKS.</span><span class="sxs-lookup"><span data-stu-id="b7328-166">When prompted, enter the destination keystore password; this will be the password for the JKS file.</span></span>
2. <span data-ttu-id="b7328-167">Voer desgevraagd het wachtwoord voor de gegevensbron keystore; Dit is het wachtwoord die u hebt opgegeven voor het PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="b7328-167">When prompted, enter the source keystore password; this is the password you specified for the PFX file.</span></span>

<span data-ttu-id="b7328-168">De twee wachtwoorden hebt niet dezelfde zijn.</span><span class="sxs-lookup"><span data-stu-id="b7328-168">The two passwords do not have to be the same.</span></span> <span data-ttu-id="b7328-169">Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="b7328-169">You can enter no password, although this is not recommended.</span></span>

## <a name="build-a-web-app-creation-application"></a><span data-ttu-id="b7328-170">Een Web-App maken toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="b7328-170">Build a Web App creation application</span></span>
### <a name="create-the-eclipse-workspace-and-maven-project"></a><span data-ttu-id="b7328-171">De Eclipse-werkruimte en Maven-Project maken</span><span class="sxs-lookup"><span data-stu-id="b7328-171">Create the Eclipse Workspace and Maven Project</span></span>
<span data-ttu-id="b7328-172">In deze sectie maakt u een werkruimte en een Maven-project voor de web-app maken toepassing, met de naam AzureWebDemo.</span><span class="sxs-lookup"><span data-stu-id="b7328-172">In this section you create a workspace and a Maven project for the web app creation application, named AzureWebDemo.</span></span>

1. <span data-ttu-id="b7328-173">Maak een nieuw Maven-project.</span><span class="sxs-lookup"><span data-stu-id="b7328-173">Create a new Maven project.</span></span> <span data-ttu-id="b7328-174">Klik op **bestand > Nieuw > Maven-Project**.</span><span class="sxs-lookup"><span data-stu-id="b7328-174">Click **File > New > Maven Project**.</span></span> <span data-ttu-id="b7328-175">In **nieuw Maven-Project**, selecteer **maken van een eenvoudig project** en **standaard werkruimte gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="b7328-175">In **New Maven Project**, select **Create a simple project** and **Use default workspace location**.</span></span>
2. <span data-ttu-id="b7328-176">Op de tweede pagina van **nieuw Maven-Project**, het volgende opgeven:</span><span class="sxs-lookup"><span data-stu-id="b7328-176">On the second page of **New Maven Project**, specify the following:</span></span>
   
   * <span data-ttu-id="b7328-177">Groeps-ID:`com.<username>.azure.webdemo`</span><span class="sxs-lookup"><span data-stu-id="b7328-177">Group ID: `com.<username>.azure.webdemo`</span></span>
   * <span data-ttu-id="b7328-178">Artefact-ID: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="b7328-178">Artifact ID: AzureWebDemo</span></span>
   * <span data-ttu-id="b7328-179">Versie: 0.0.1-SNAPSHOT</span><span class="sxs-lookup"><span data-stu-id="b7328-179">Version: 0.0.1-SNAPSHOT</span></span>
   * <span data-ttu-id="b7328-180">Verpakking: jar</span><span class="sxs-lookup"><span data-stu-id="b7328-180">Packaging: jar</span></span>
   * <span data-ttu-id="b7328-181">Naam: AzureWebDemo</span><span class="sxs-lookup"><span data-stu-id="b7328-181">Name: AzureWebDemo</span></span>
     
     <span data-ttu-id="b7328-182">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b7328-182">Click **Finish**.</span></span>
3. <span data-ttu-id="b7328-183">Het nieuwe project pom.xml-bestand openen in Projectverkenner.</span><span class="sxs-lookup"><span data-stu-id="b7328-183">Open the new project's pom.xml file in Project Explorer.</span></span> <span data-ttu-id="b7328-184">Selecteer de **afhankelijkheden** tabblad. Als dit een nieuw project is, worden er geen pakketten nog vermeld.</span><span class="sxs-lookup"><span data-stu-id="b7328-184">Select the **Dependencies** tab. As this is a new project, no packages are listed yet.</span></span>
4. <span data-ttu-id="b7328-185">Open de Maven-opslagplaatsen.</span><span class="sxs-lookup"><span data-stu-id="b7328-185">Open the Maven Repositories view.</span></span> <span data-ttu-id="b7328-186">**Klik op Venster > weergave tonen > andere > Maven > Maven-opslagplaatsen** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7328-186">**Click Window > Show View > Other > Maven > Maven Repositories** and click **OK**.</span></span> <span data-ttu-id="b7328-187">De **Maven-opslagplaatsen** weergave wordt weergegeven onder aan de IDE.</span><span class="sxs-lookup"><span data-stu-id="b7328-187">The **Maven Repositories** view will appear at the bottom of the IDE.</span></span>
5. <span data-ttu-id="b7328-188">Open **globale opslagplaatsen**, met de rechtermuisknop op de **centrale** opslagplaats en selecteer **Rebuild Index**.</span><span class="sxs-lookup"><span data-stu-id="b7328-188">Open **Global Repositories**, right-click the **central** repository, and select **Rebuild Index**.</span></span>
   
    ![][1]
   
    <span data-ttu-id="b7328-189">Deze stap kan enige tijd duren, afhankelijk van de snelheid van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="b7328-189">This step can take several minutes depending on the speed of your connection.</span></span> <span data-ttu-id="b7328-190">Wanneer de index wordt opnieuw gemaakt, ziet u de Microsoft Azure-pakketten in de **centrale** Maven-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b7328-190">When the index rebuilds, you should see the Microsoft Azure packages in the **central** Maven repository.</span></span>
6. <span data-ttu-id="b7328-191">In **afhankelijkheden**, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="b7328-191">In **Dependencies**, click **Add**.</span></span> <span data-ttu-id="b7328-192">In **groep-ID invoeren...**  Voer `azure-management`.</span><span class="sxs-lookup"><span data-stu-id="b7328-192">In **Enter Group ID...** enter `azure-management`.</span></span> <span data-ttu-id="b7328-193">Selecteer de pakketten voor base management en App Service Web Apps management:</span><span class="sxs-lookup"><span data-stu-id="b7328-193">Select the packages for base management and App Service Web Apps management:</span></span>
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > <span data-ttu-id="b7328-194">**Opmerking:** als u de afhankelijkheden na de release van een nieuwe versie bijwerkt, moet u elk van de afhankelijkheden in deze lijst opnieuw toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b7328-194">**Note:** If you are updating the dependencies after a new version release, you need to re-add each of the dependencies in this list.</span></span>
   > <span data-ttu-id="b7328-195">Nadat u op **toevoegen** en selecteer elke afhankelijkheid wordt dit weergegeven met het nieuwe versienummer in de **afhankelijkheden** lijst.</span><span class="sxs-lookup"><span data-stu-id="b7328-195">After you click **Add** and select each dependency, it appears with the new version number in the **Dependencies** list.</span></span>
   > 
   > 

<span data-ttu-id="b7328-196">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7328-196">Click **OK**.</span></span> <span data-ttu-id="b7328-197">De Azure-pakketten worden weergegeven de **afhankelijkheden** lijst.</span><span class="sxs-lookup"><span data-stu-id="b7328-197">The Azure packages then appear in the **Dependencies** list.</span></span>

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a><span data-ttu-id="b7328-198">Schrijven van Java-Code voor het maken van een Web-App door het aanroepen van de Azure SDK</span><span class="sxs-lookup"><span data-stu-id="b7328-198">Writing Java Code to Create a Web App by Calling the Azure SDK</span></span>
<span data-ttu-id="b7328-199">Vervolgens wordt de code schrijven waarmee roept de API's in de Azure SDK voor Java voor het maken van de App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="b7328-199">Next, write the code that calls APIs in the Azure SDK for Java to create the App Service web app.</span></span>

1. <span data-ttu-id="b7328-200">Maak een Java-klasse om de belangrijkste vermelding punt code bevatten.</span><span class="sxs-lookup"><span data-stu-id="b7328-200">Create a Java class to contain the main entry point code.</span></span> <span data-ttu-id="b7328-201">Klik in Projectverkenner met de rechtermuisknop op het projectknooppunt en selecteer **Nieuw > klasse**.</span><span class="sxs-lookup"><span data-stu-id="b7328-201">In Project Explorer, right-click on the project node and select **New > Class**.</span></span>
2. <span data-ttu-id="b7328-202">In **nieuwe Java-klasse**, naam van de klasse `WebCreator` en controleer de **openbare statische void main** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="b7328-202">In **New Java Class**, name the class `WebCreator` and check the **public static void main** checkbox.</span></span> <span data-ttu-id="b7328-203">De selecties ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b7328-203">The selections should appear as follows:</span></span>
   
    ![][2]
3. <span data-ttu-id="b7328-204">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b7328-204">Click **Finish**.</span></span> <span data-ttu-id="b7328-205">Het bestand WebCreator.java weergegeven in Projectverkenner.</span><span class="sxs-lookup"><span data-stu-id="b7328-205">The WebCreator.java file appears in Project Explorer.</span></span>

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a><span data-ttu-id="b7328-206">Aanroepen van de Azure-API voor het maken van een App Service-Web-App</span><span class="sxs-lookup"><span data-stu-id="b7328-206">Calling the Azure API to Create an App Service Web App</span></span>
#### <a name="add-necessary-imports"></a><span data-ttu-id="b7328-207">Vereiste imports toevoegen</span><span class="sxs-lookup"><span data-stu-id="b7328-207">Add necessary imports</span></span>
<span data-ttu-id="b7328-208">In WebCreator.java, voegt u de volgende import; deze invoer bieden toegang tot de klassen in de management-bibliotheken voor het verbruik van Azure-API's:</span><span class="sxs-lookup"><span data-stu-id="b7328-208">In WebCreator.java, add the following imports; these imports provide access to classes in the management libraries for consuming Azure APIs:</span></span>

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


#### <a name="define-the-main-entry-point-class"></a><span data-ttu-id="b7328-209">De klasse van de belangrijkste vermelding point definiëren</span><span class="sxs-lookup"><span data-stu-id="b7328-209">Define the main entry point class</span></span>
<span data-ttu-id="b7328-210">De hoofdklasse omdat het doel van de toepassing AzureWebDemo is voor het maken van een App Service-Web-App, een naam voor deze toepassing `WebAppCreator`.</span><span class="sxs-lookup"><span data-stu-id="b7328-210">Because the purpose of the AzureWebDemo application is to create an App Service Web App, name the main class for this application `WebAppCreator`.</span></span> <span data-ttu-id="b7328-211">Deze klasse biedt de belangrijkste vermelding punt code die de Azure Service Management API voor het maken van de web-app aanroept.</span><span class="sxs-lookup"><span data-stu-id="b7328-211">This class provides the main entry point code that calls the Azure Service Management API to create the web app.</span></span>

<span data-ttu-id="b7328-212">De volgende parameterdefinities voor de web-app en webruimte toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b7328-212">Add the following parameter definitions for the web app and webspace.</span></span> <span data-ttu-id="b7328-213">U moet uw eigen Azure-abonnement-ID en certificaat-informatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="b7328-213">You will need to provide your own Azure subscription ID and certificate information.</span></span>

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

<span data-ttu-id="b7328-214">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="b7328-214">where:</span></span>

* <span data-ttu-id="b7328-215">`<subscription-id>`is de Azure-abonnement-ID in die u wilt maken van de resource.</span><span class="sxs-lookup"><span data-stu-id="b7328-215">`<subscription-id>` is the Azure subscription ID in which you want to create the resource.</span></span>
* <span data-ttu-id="b7328-216">`<certificate-store-path>`is het pad en bestandsnaam in het bestand JKS in uw directory van de winkel lokale certificaatarchief.</span><span class="sxs-lookup"><span data-stu-id="b7328-216">`<certificate-store-path>` is the path and filename to the JKS file in your local certificate store directory.</span></span> <span data-ttu-id="b7328-217">Bijvoorbeeld: `C:/Certificates/CertificateName.jks` voor Linux en `C:\Certificates\CertificateName.jks` voor Windows.</span><span class="sxs-lookup"><span data-stu-id="b7328-217">For example, `C:/Certificates/CertificateName.jks` for Linux and `C:\Certificates\CertificateName.jks` for Windows.</span></span>
* <span data-ttu-id="b7328-218">`<certificate-password>`is het wachtwoord die u hebt opgegeven toen u uw certificaat JKS hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7328-218">`<certificate-password>` is the password you specified when you created your JKS certificate.</span></span>
* <span data-ttu-id="b7328-219">`webAppName`de naam die u kiezen; deze procedure gebruikt u de naam van de `WebDemoWebApp`.</span><span class="sxs-lookup"><span data-stu-id="b7328-219">`webAppName` can be any name you choose; this procedure uses the name `WebDemoWebApp`.</span></span> <span data-ttu-id="b7328-220">De volledige domeinnaam is de `webAppName` met de `domainName` toegevoegd, dus in dit geval het volledige domein is `webdemowebapp.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="b7328-220">The full domain name is the `webAppName` with the `domainName` appended, so in this case the full domain is `webdemowebapp.azurewebsites.net`.</span></span>
* <span data-ttu-id="b7328-221">`domainName`moet worden opgegeven, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="b7328-221">`domainName` should be specified as shown above.</span></span>
* <span data-ttu-id="b7328-222">`webSpaceName`moet een van de waarden die zijn gedefinieerd in de [WebSpaceNames] [ WebSpaceNames] klasse.</span><span class="sxs-lookup"><span data-stu-id="b7328-222">`webSpaceName` should be one of the values defined in the [WebSpaceNames][WebSpaceNames] class.</span></span>
* <span data-ttu-id="b7328-223">`appServicePlanName`moet worden opgegeven, zoals hierboven.</span><span class="sxs-lookup"><span data-stu-id="b7328-223">`appServicePlanName` should be specified as shown above.</span></span>

> <span data-ttu-id="b7328-224">**Opmerking:** elke keer dat u deze toepassing uitvoeren, moet u de waarde van wijzigen `webAppName` en `appServicePlanName` (of verwijderen van de web-app in de Azure Portal) voordat u de toepassing opnieuw uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b7328-224">**Note:** Each time you run this application, you need to change the value of `webAppName` and `appServicePlanName` (or delete the web app on the Azure Portal) before running the application again.</span></span> <span data-ttu-id="b7328-225">Anders mislukt uitvoering omdat de dezelfde resource al in Azure bestaat.</span><span class="sxs-lookup"><span data-stu-id="b7328-225">Otherwise, execution will fail because the same resource already exists on Azure.</span></span>
> 
> 

#### <a name="define-the-web-creation-method"></a><span data-ttu-id="b7328-226">De methode voor het maken van web definiëren</span><span class="sxs-lookup"><span data-stu-id="b7328-226">Define the web creation method</span></span>
<span data-ttu-id="b7328-227">Definieer vervolgens een methode voor het maken van de web-app.</span><span class="sxs-lookup"><span data-stu-id="b7328-227">Next, define a method to create the web app.</span></span> <span data-ttu-id="b7328-228">Deze methode `createWebApp`, geeft de parameters van de web-app en de webruimte.</span><span class="sxs-lookup"><span data-stu-id="b7328-228">This method, `createWebApp`, specifies the parameters of the web app and the webspace.</span></span> <span data-ttu-id="b7328-229">Daarnaast maakt en configureert u de App Service Web Apps management-client, die wordt gedefinieerd door de [WebSiteManagementClient] [ WebSiteManagementClient] object.</span><span class="sxs-lookup"><span data-stu-id="b7328-229">It also creates and configures the App Service Web Apps management client, which is defined by the [WebSiteManagementClient][WebSiteManagementClient] object.</span></span> <span data-ttu-id="b7328-230">De management-client is de sleutel voor het maken van Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="b7328-230">The management client is key to creating Web Apps.</span></span> <span data-ttu-id="b7328-231">Het biedt de RESTful-web-services waarmee toepassingen voor het beheren van web-apps (het uitvoeren van bewerkingen zoals maken, bijwerken en verwijderen) door het aanroepen van de servicebeheer-API.</span><span class="sxs-lookup"><span data-stu-id="b7328-231">It provides RESTful web services that allow applications to manage web apps (performing operations such as create, update, and delete) by calling the service management API.</span></span>

    private static void createWebApp() throws Exception {

        // Specify configuration settings for the App Service management client.
        Configuration config = ManagementConfiguration.configure(
            new URI(uri),
            subscriptionId,
            keyStoreLocation,  // Path to the JKS file
            keyStorePassword,  // Password for the JKS file
            KeyStoreType.jks   // Flag that you are using a JKS keystore
        );

        // Create the App Service Web Apps management client to call Azure APIs
        // and pass it the App Service management configuration object.
        WebSiteManagementClient webAppManagementClient = WebSiteManagementService.create(config);

        // Create an App Service plan for the web app with the specified parameters.
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
        // Note that the server farm name takes the Azure App Service plan name.
        WebSiteCreateParameters webAppCreateParameters = new WebSiteCreateParameters();
        webAppCreateParameters.setName(webAppName);
        webAppCreateParameters.setServerFarm(appServicePlanName);
        webAppCreateParameters.setWebSpace(webSpaceDetails);

        // Set usage metrics attributes.
        WebSiteGetUsageMetricsResponse.UsageMetric usageMetric = new WebSiteGetUsageMetricsResponse.UsageMetric();
        usageMetric.setSiteMode(WebSiteMode.Basic);
        usageMetric.setComputeMode(WebSiteComputeMode.Shared);

        // Define the web app object.
        ArrayList<String> fullWebAppName = new ArrayList<String>();
        fullWebAppName.add(webAppName + domainName);
        WebSite webApp = new WebSite();
        webApp.setHostNames(fullWebAppName);

        // Create the web app.
        WebSiteCreateResponse webAppCreateResponse = webAppManagementClient.getWebSitesOperations().create(webSpaceName, webAppCreateParameters);

        // Output the HTTP status code of the response; 200 indicates the request succeeded; 4xx indicates failure.
        System.out.println("----------");
        System.out.println("Web app created - HTTP response " + webAppCreateResponse.getStatusCode() + "\n");

        // Output the name of the web app that this application created.
        String shinyNewWebAppName = webAppCreateResponse.getWebSite().getName();
        System.out.println("----------\n");
        System.out.println("Name of web app created: " + shinyNewWebAppName + "\n");
        System.out.println("----------\n");
    }

<span data-ttu-id="b7328-232">De code de HTTP-status van de reactie waarmee wordt aangegeven of geslaagd of mislukt wordt uitgevoerd en als dit lukt, wordt de naam van de gemaakte web-app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b7328-232">The code will output the HTTP status of the response indicating success or failure, and if successful, will output the name of the created web app.</span></span>

#### <a name="define-the-main-method"></a><span data-ttu-id="b7328-233">De methode main() definiëren</span><span class="sxs-lookup"><span data-stu-id="b7328-233">Define the main() method</span></span>
<span data-ttu-id="b7328-234">Geef de code van main() methode waarmee createWebApp() voor het maken van de web-app wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b7328-234">Provide the main() method code that calls createWebApp() to create the web app.</span></span>

<span data-ttu-id="b7328-235">Tenslotte roept `createWebApp` van `main`:</span><span class="sxs-lookup"><span data-stu-id="b7328-235">Finally, call `createWebApp` from `main`:</span></span>

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a><span data-ttu-id="b7328-236">Voer de toepassing en controleer of de web-apps maken</span><span class="sxs-lookup"><span data-stu-id="b7328-236">Run the application and verify web app creation</span></span>
<span data-ttu-id="b7328-237">Om te controleren of uw toepassing wordt uitgevoerd, klikt u op **uitvoeren > Voer**.</span><span class="sxs-lookup"><span data-stu-id="b7328-237">To verify that your application runs, click **Run > Run**.</span></span> <span data-ttu-id="b7328-238">Wanneer de toepassing is voltooid wordt uitgevoerd, ziet u de volgende uitvoer in de Eclipse-console:</span><span class="sxs-lookup"><span data-stu-id="b7328-238">When the application completes running, you should see the following output in the Eclipse console:</span></span>

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

<span data-ttu-id="b7328-239">Meld u aan bij de klassieke Azure portal en klikt u op **Web-Apps**.</span><span class="sxs-lookup"><span data-stu-id="b7328-239">Log into the Azure classic portal and click **Web Apps**.</span></span> <span data-ttu-id="b7328-240">De nieuwe web-app moet worden weergegeven in de lijst met Web-Apps binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="b7328-240">The new web app should appear in the Web Apps list within a few minutes.</span></span>

## <a name="deploying-an-application-to-the-web-app"></a><span data-ttu-id="b7328-241">Een toepassing implementeren in de Web-App</span><span class="sxs-lookup"><span data-stu-id="b7328-241">Deploying an Application to the Web App</span></span>
<span data-ttu-id="b7328-242">Nadat u AzureWebDemo hebt uitgevoerd en klik op de nieuwe web-app, meld u aan bij de klassieke portal gemaakt **Web-Apps**, en selecteer **WebDemoWebApp** in de **Web-Apps** lijst.</span><span class="sxs-lookup"><span data-stu-id="b7328-242">After you have run AzureWebDemo and created the new web app, log into the classic portal, click **Web Apps**, and select **WebDemoWebApp** in the **Web Apps** list.</span></span> <span data-ttu-id="b7328-243">Klik in de web-app dashboardpagina op **Bladeren** (of klik op de URL `webdemowebapp.azurewebsites.net`) om hiernaar te navigeren.</span><span class="sxs-lookup"><span data-stu-id="b7328-243">In the web app's dashboard page, click **Browse** (or click the URL, `webdemowebapp.azurewebsites.net`) to navigate to it.</span></span> <span data-ttu-id="b7328-244">U ziet een lege tijdelijke aanduiding-pagina, omdat het geen inhoud is gepubliceerd naar de web-app nog.</span><span class="sxs-lookup"><span data-stu-id="b7328-244">You will see a blank placeholder page, because no content has been published to the web app yet.</span></span>

<span data-ttu-id="b7328-245">U wordt vervolgens een 'Hallo wereld'-toepassing maken en implementeren op de web-app.</span><span class="sxs-lookup"><span data-stu-id="b7328-245">Next you will create a "Hello World" application and deploy it to the web app.</span></span>

### <a name="create-a-jsp-hello-world-application"></a><span data-ttu-id="b7328-246">Een JSP Hallo wereld-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="b7328-246">Create a JSP Hello World application</span></span>
#### <a name="create-the-application"></a><span data-ttu-id="b7328-247">De toepassing maken</span><span class="sxs-lookup"><span data-stu-id="b7328-247">Create the application</span></span>
<span data-ttu-id="b7328-248">Als u wilt laten zien hoe een toepassing implementeert op het web, ziet de volgende procedure u hoe een eenvoudige 'Hallo wereld' Java-toepassing maken en uploaden naar de App Service Web-App die uw toepassing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7328-248">In order to demonstrate how to deploy an application to the web, the following procedure shows you how to create a simple "Hello World" Java application and upload it to the App Service Web App that your application created.</span></span>

1. <span data-ttu-id="b7328-249">Klik op **bestand > Nieuw > Dynamic webproject**.</span><span class="sxs-lookup"><span data-stu-id="b7328-249">Click **File > New > Dynamic Web Project**.</span></span> <span data-ttu-id="b7328-250">Noem deze `JSPHello`.</span><span class="sxs-lookup"><span data-stu-id="b7328-250">Name it `JSPHello`.</span></span> <span data-ttu-id="b7328-251">U hoeft niet te wijzigen van de andere instellingen in dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7328-251">You do not need to change any other settings in this dialog.</span></span> <span data-ttu-id="b7328-252">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b7328-252">Click **Finish**.</span></span>
   
    ![][3]
2. <span data-ttu-id="b7328-253">Vouw in Projectverkenner de **JSPHello** project, met de rechtermuisknop op **WebContent**, klikt u vervolgens op **Nieuw > JSP-bestand**.</span><span class="sxs-lookup"><span data-stu-id="b7328-253">In Project Explorer, expand the **JSPHello** project, right-click **WebContent**, then click **New > JSP File**.</span></span> <span data-ttu-id="b7328-254">In het dialoogvenster Nieuw JSP-bestand een naam op het nieuwe bestand `index.jsp`.</span><span class="sxs-lookup"><span data-stu-id="b7328-254">In the New JSP File dialog, name the new file `index.jsp`.</span></span> <span data-ttu-id="b7328-255">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="b7328-255">Click **Next**.</span></span>
3. <span data-ttu-id="b7328-256">In de **JSP-sjabloon selecteren** dialoogvenster **nieuw JSP-bestand (html)** en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b7328-256">In the **Select JSP Template** dialog, select **New JSP File (html)** and click **Finish**.</span></span>
4. <span data-ttu-id="b7328-257">In index.jsp, voeg de volgende code in de `<head>` en `<body>` tag secties:</span><span class="sxs-lookup"><span data-stu-id="b7328-257">In index.jsp, add the following code in the `<head>` and `<body>` tag sections:</span></span>
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a><span data-ttu-id="b7328-258">Uitvoeren van de toepassing Hello World in localhost</span><span class="sxs-lookup"><span data-stu-id="b7328-258">Run the Hello World application in localhost</span></span>
<span data-ttu-id="b7328-259">Voordat u deze toepassing uitvoert, moet u enkele eigenschappen configureren.</span><span class="sxs-lookup"><span data-stu-id="b7328-259">Before you run this application, you need to configure a few properties.</span></span>

1. <span data-ttu-id="b7328-260">Met de rechtermuisknop op de **JSPHello** project en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="b7328-260">Right-click the **JSPHello** project and select **Properties**.</span></span>
2. <span data-ttu-id="b7328-261">In de **eigenschappen** dialoogvenster: Selecteer **Javabuild-pad**, selecteer de **rangschikken en exporteren** tabblad controle **JRE systeembibliotheek**, klikt u vervolgens op **Up** te verplaatsen naar de bovenkant van de lijst.</span><span class="sxs-lookup"><span data-stu-id="b7328-261">In the **Properties** dialog: select **Java Build Path**, select the **Order and Export** tab, check **JRE System Library**, then click **Up** to move it to the top of the list.</span></span>
   
    ![][4]
3. <span data-ttu-id="b7328-262">Ook in de **eigenschappen** dialoogvenster: Selecteer **Runtimes gericht** en klik op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="b7328-262">Also in the **Properties** dialog: select **Targeted Runtimes** and click **New**.</span></span>
4. <span data-ttu-id="b7328-263">In de **nieuwe Server Runtime-omgeving** dialoogvenster, selecteert u een server, zoals **Apache Tomcat v7.0** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b7328-263">In the **New Server Runtime Environment** dialog, select a server such as **Apache Tomcat v7.0** and click **Next**.</span></span> <span data-ttu-id="b7328-264">In de **Tomcat-Server** dialoogvenster, set **naam** naar `Apache Tomcat v7.0`, en stel **Tomcat-installatiedirectory** naar de map waarin u de versie van Tomcat-server die u wilt gebruiken, hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b7328-264">In the **Tomcat Server** dialog, set **Name** to `Apache Tomcat v7.0`, and set **Tomcat Installation Directory** to the directory in which you installed the version of Tomcat server you want to use.</span></span>
   
    ![][5]
   
    <span data-ttu-id="b7328-265">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b7328-265">Click **Finish**.</span></span>
5. <span data-ttu-id="b7328-266">U keer vervolgens terug naar de **Runtimes gericht** pagina van de **eigenschappen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="b7328-266">You then return to the **Targeted Runtimes** page of the **Properties** dialog.</span></span> <span data-ttu-id="b7328-267">Selecteer **Apache Tomcat v7.0**, klikt u vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="b7328-267">Select **Apache Tomcat v7.0**, then click **OK**.</span></span>
   
    ![][6]
6. <span data-ttu-id="b7328-268">In de Eclipse **uitvoeren** menu, klikt u op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="b7328-268">In the Eclipse **Run** menu, click **Run**.</span></span> <span data-ttu-id="b7328-269">In de **uitvoeren als** dialoogvenster Selecteer **uitgevoerd op Server**.</span><span class="sxs-lookup"><span data-stu-id="b7328-269">In the **Run As** dialog, select **Run on Server**.</span></span> <span data-ttu-id="b7328-270">In de **uitgevoerd op Server** dialoogvenster Selecteer **Tomcat v7.0 Server**:</span><span class="sxs-lookup"><span data-stu-id="b7328-270">In the **Run on Server** dialog, select **Tomcat v7.0 Server**:</span></span>
   
    ![][7]
   
    <span data-ttu-id="b7328-271">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="b7328-271">Click **Finish**.</span></span>
7. <span data-ttu-id="b7328-272">Wanneer de toepassing wordt uitgevoerd, ziet u de **JSPHello** pagina wordt weergegeven in een venster localhost in Eclipse (`http://localhost:8080/JSPHello/`), het volgende bericht wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="b7328-272">When the application runs, you should see the **JSPHello** page appear in a localhost window in Eclipse (`http://localhost:8080/JSPHello/`), displaying the following message:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a><span data-ttu-id="b7328-273">De toepassing als een WAR exporteren</span><span class="sxs-lookup"><span data-stu-id="b7328-273">Export the application as a WAR</span></span>
<span data-ttu-id="b7328-274">De web-projectbestanden exporteren als een web-archiefbestand (WAR) zodat u deze op de web-app implementeren kunt.</span><span class="sxs-lookup"><span data-stu-id="b7328-274">Export the web project files as a web archive (WAR) file so that you can deploy it to the web app.</span></span> <span data-ttu-id="b7328-275">De volgende web project-bestanden bevinden zich in de map WebContent:</span><span class="sxs-lookup"><span data-stu-id="b7328-275">The following web project files reside in the WebContent folder:</span></span>

    META-INF
    WEB-INF
    index.jsp

1. <span data-ttu-id="b7328-276">Met de rechtermuisknop op de map WebContent en selecteer **exporteren**.</span><span class="sxs-lookup"><span data-stu-id="b7328-276">Right-click the WebContent folder and select **Export**.</span></span>
2. <span data-ttu-id="b7328-277">In de **exporteren Selecteer** dialoogvenster, klikt u op **Web > WAR** bestand en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="b7328-277">In the **Export Select** dialog, click **Web > WAR** file, then click **Next**.</span></span>
3. <span data-ttu-id="b7328-278">In de **WAR exporteren** dialoogvenster, selecteer de src-map in het huidige project en de naam van het WAR-bestand aan het einde bevatten.</span><span class="sxs-lookup"><span data-stu-id="b7328-278">In the **WAR Export** dialog, select the src directory in the current project, and include the name of the WAR file at the end.</span></span> <span data-ttu-id="b7328-279">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b7328-279">For example:</span></span>
   
    `<project-path>/JSPHello/src/JSPHello.war`

<span data-ttu-id="b7328-280">Zie voor meer informatie over het implementeren van WAR bestanden [toevoegen van een Java-toepassing naar Azure App Service Web Apps](web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="b7328-280">For more information on deploying WAR files, see [Add a Java application to Azure App Service Web Apps](web-sites-java-add-app.md).</span></span>

### <a name="deploying-the-hello-world-application-using-ftp"></a><span data-ttu-id="b7328-281">De Hallo wereld-toepassing met FTP implementeert</span><span class="sxs-lookup"><span data-stu-id="b7328-281">Deploying the Hello World Application Using FTP</span></span>
<span data-ttu-id="b7328-282">Selecteer een FTP-client van derden voor het publiceren van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b7328-282">Select a third-party FTP client to publish the application.</span></span> <span data-ttu-id="b7328-283">Deze procedure wordt beschreven twee opties: de Kudu-console die is ingebouwd in Azure. en FileZilla, een populaire hulpmiddel met een handige, grafische gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="b7328-283">This procedure describes two options: the Kudu console built into Azure; and FileZilla, a popular tool with a convenient, graphical UI.</span></span>

> <span data-ttu-id="b7328-284">**Opmerking:** de Azure-werkset voor Eclipse ondersteunt de implementatie naar storage-accounts en cloud services, maar ondersteunt geen implementatie voor web-apps.</span><span class="sxs-lookup"><span data-stu-id="b7328-284">**Note:** The Azure Toolkit for Eclipse supports deployment to storage accounts and cloud services, but does not currently support deployment to web apps.</span></span> <span data-ttu-id="b7328-285">U kunt implementeren voor storage-accounts en cloud services met behulp van een Azure-implementatieproject, zoals beschreven in [maken van een Hallo wereld-toepassing voor Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), maar niet naar de web-apps.</span><span class="sxs-lookup"><span data-stu-id="b7328-285">You can deploy to storage accounts and cloud services using an Azure Deployment Project as described in [Creating a Hello World Application for Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), but not to web apps.</span></span> <span data-ttu-id="b7328-286">Andere methoden zoals FTP- of GitHub bestanden overbrengen naar uw web-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b7328-286">Use other methods such as FTP or GitHub to transfer files to your web app.</span></span>
> 
> <span data-ttu-id="b7328-287">**Opmerking:** niet raadzaam met FTP vanaf de opdrachtprompt van Windows (het FTP.EXE opdrachtregelprogramma dat wordt geleverd bij Windows).</span><span class="sxs-lookup"><span data-stu-id="b7328-287">**Note:** We do not recommend using FTP from the Windows command prompt (the command-line FTP.EXE utility that ships with Windows).</span></span> <span data-ttu-id="b7328-288">FTP-clients die gebruikmaken van actieve FTP, zoals FTP.EXE, niet vaak werken via firewalls.</span><span class="sxs-lookup"><span data-stu-id="b7328-288">FTP clients that use active FTP, such as FTP.EXE, often fail to work over firewalls.</span></span> <span data-ttu-id="b7328-289">Actieve FTP geeft een interne, op basis van LAN adres waarnaar een FTP-server waarschijnlijk geen verbinding maken.</span><span class="sxs-lookup"><span data-stu-id="b7328-289">Active FTP specifies an internal LAN-based address, to which an FTP server will likely fail to connect.</span></span>
> 
> 

<span data-ttu-id="b7328-290">Zie de volgende onderwerpen voor meer informatie over de implementatie van een App Service-web-app met FTP:</span><span class="sxs-lookup"><span data-stu-id="b7328-290">For more information on deployment to an App Service web app using FTP, see the following topics:</span></span>

* [<span data-ttu-id="b7328-291">Implementeren met behulp van een FTP-programma</span><span class="sxs-lookup"><span data-stu-id="b7328-291">Deploy using an FTP utility</span></span>](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a><span data-ttu-id="b7328-292">Implementatiereferenties instellen</span><span class="sxs-lookup"><span data-stu-id="b7328-292">Set up deployment credentials</span></span>
<span data-ttu-id="b7328-293">Zorg ervoor dat u hebt uitgevoerd, de **AzureWebDemo** toepassing maken van een web-app.</span><span class="sxs-lookup"><span data-stu-id="b7328-293">Make sure you have run the **AzureWebDemo** application to create a web app.</span></span> <span data-ttu-id="b7328-294">U kunt bestanden worden overgebracht naar deze locatie.</span><span class="sxs-lookup"><span data-stu-id="b7328-294">You will transfer files to this location.</span></span>

1. <span data-ttu-id="b7328-295">Meld u aan bij de klassieke portal en klikt u op **Web-Apps**.</span><span class="sxs-lookup"><span data-stu-id="b7328-295">Log into the classic portal and click **Web Apps**.</span></span> <span data-ttu-id="b7328-296">Zorg ervoor dat **WebDemoWebApp** wordt weergegeven in de lijst met web-apps en zorg ervoor dat deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b7328-296">Make sure **WebDemoWebApp** appears in the list of web apps, and make sure that it is running.</span></span> <span data-ttu-id="b7328-297">Klik op **WebDemoWebApp** openen de **Dashboard** pagina.</span><span class="sxs-lookup"><span data-stu-id="b7328-297">Click **WebDemoWebApp** to open its **Dashboard** page.</span></span>
2. <span data-ttu-id="b7328-298">Op de **Dashboard** pagina onder **snel in één oogopslag**, klikt u op **instellen van referenties voor uw implementatie** (als u de referenties voor implementatie al hebt, leest dit **opnieuw instellen van referenties voor uw implementatie**).</span><span class="sxs-lookup"><span data-stu-id="b7328-298">On the **Dashboard** page, under **Quick Glance**, click **Set up your deployment credentials** (if you already have deployment credentials, this reads **Reset your deployment credentials**).</span></span>
   
    <span data-ttu-id="b7328-299">Referenties voor implementatie zijn gekoppeld aan een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="b7328-299">Deployment credentials are associated with a Microsoft account.</span></span> <span data-ttu-id="b7328-300">U moet een gebruikersnaam en wachtwoord waarmee u kunt implementeren met behulp van Git en FTP opgeven.</span><span class="sxs-lookup"><span data-stu-id="b7328-300">You need to specify a username and password that you can use to deploy using Git and FTP.</span></span> <span data-ttu-id="b7328-301">U kunt deze referenties gebruiken om te implementeren voor een web-app in alle Azure-abonnementen die zijn gekoppeld aan je Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="b7328-301">You can use these credentials to deploy to any web app in all Azure subscriptions associated with your Microsoft account.</span></span> <span data-ttu-id="b7328-302">Geef referenties op Git en FTP-implementatie in het dialoogvenster en noteert u de gebruikersnaam en het wachtwoord voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="b7328-302">Provide Git and FTP deployment credentials in the dialog, and record the username and password for future use.</span></span>

#### <a name="get-ftp-connection-information"></a><span data-ttu-id="b7328-303">Gegevens van de FTP-verbinding ophalen</span><span class="sxs-lookup"><span data-stu-id="b7328-303">Get FTP connection information</span></span>
<span data-ttu-id="b7328-304">Gebruik van FTP toepassingsbestanden naar de nieuwe web-app implementeren, moet u de verbindingsgegevens verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="b7328-304">To use FTP to deploy application files to the newly created web app, you need to obtain connection information.</span></span> <span data-ttu-id="b7328-305">Er zijn twee manieren verkrijgen verbindingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="b7328-305">There are two ways to obtain connection information.</span></span> <span data-ttu-id="b7328-306">Te gaat u naar de web-app **Dashboard** pagina; de andere manier is om te downloaden van het web van app publicatieprofiel.</span><span class="sxs-lookup"><span data-stu-id="b7328-306">One way is to visit the web app's **Dashboard** page; the other way is to download the web app's publish profile.</span></span> <span data-ttu-id="b7328-307">Het publicatieprofiel is een XML-bestand informatie zoals de FTP-host en het aanmeldingsaccount referenties voor uw web-apps in Azure App Service bevat.</span><span class="sxs-lookup"><span data-stu-id="b7328-307">The publish profile is an XML file that provides information such as FTP host name and logon credentials for your web apps in Azure App Service.</span></span> <span data-ttu-id="b7328-308">U kunt deze gebruikersnaam en wachtwoord gebruiken om te implementeren voor een web-app in alle abonnementen die zijn gekoppeld aan het Azure-account, niet alleen dit exemplaar.</span><span class="sxs-lookup"><span data-stu-id="b7328-308">You can use this username and password to deploy to any web app in all subscriptions associated with the Azure account, not only this one.</span></span>

<span data-ttu-id="b7328-309">FTP-verbinding om informatie te verkrijgen uit de blade web-app in de [Azure Portal][Azure Portal]:</span><span class="sxs-lookup"><span data-stu-id="b7328-309">To obtain FTP connection information from the web app's blade in the [Azure Portal][Azure Portal]:</span></span>

1. <span data-ttu-id="b7328-310">Onder **Essentials**, vindt en kopieert de **FTP-hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="b7328-310">Under **Essentials**, find and copy the **FTP hostname**.</span></span> <span data-ttu-id="b7328-311">Dit is een URI die vergelijkbaar is met `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="b7328-311">This is a URI similar to `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.</span></span>
2. <span data-ttu-id="b7328-312">Onder **Essentials**, vindt en kopieert **FTP-/ Implementatiegebruiker gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="b7328-312">Under **Essentials**, find and copy **FTP/Deployment username**.</span></span> <span data-ttu-id="b7328-313">Dit heeft de vorm *webappname\deployment-username*; bijvoorbeeld `WebDemoWebApp\deployer77`.</span><span class="sxs-lookup"><span data-stu-id="b7328-313">This will have the form *webappname\deployment-username*; for example `WebDemoWebApp\deployer77`.</span></span>

<span data-ttu-id="b7328-314">FTP-verbinding om informatie te verkrijgen uit het publicatieprofiel:</span><span class="sxs-lookup"><span data-stu-id="b7328-314">To obtain FTP connection information from the publish profile:</span></span>

1. <span data-ttu-id="b7328-315">Klik op de web-app blade **Get publicatieprofiel**.</span><span class="sxs-lookup"><span data-stu-id="b7328-315">In the web app's blade, click **Get publish profile**.</span></span> <span data-ttu-id="b7328-316">Hiermee wordt een .publishsettings-bestand downloaden naar uw lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="b7328-316">This will download a .publishsettings file to your local drive.</span></span>
2. <span data-ttu-id="b7328-317">Open het .publishsettings-bestand in een XML-editor of een teksteditor en zoek de `<publishProfile>` element die `publishMethod="FTP"`.</span><span class="sxs-lookup"><span data-stu-id="b7328-317">Open the .publishsettings file in an XML editor or text editor and find the `<publishProfile>` element containing `publishMethod="FTP"`.</span></span> <span data-ttu-id="b7328-318">Het moet eruitzien als in het volgende:</span><span class="sxs-lookup"><span data-stu-id="b7328-318">It should look like the following:</span></span>
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. <span data-ttu-id="b7328-319">Houd er rekening mee dat de web-app `publishProfile` instellingen zijn toegewezen aan de instellingen FileZilla sitebeheerder als volgt:</span><span class="sxs-lookup"><span data-stu-id="b7328-319">Note that the web app's `publishProfile` settings map to the FileZilla Site Manager settings as follows:</span></span>

* <span data-ttu-id="b7328-320">`publishUrl`is hetzelfde als **FTP-hostnaam**, de waarde die u instelt in **Host**.</span><span class="sxs-lookup"><span data-stu-id="b7328-320">`publishUrl` is the same as **FTP host name**, the value you set in **Host**.</span></span>
* <span data-ttu-id="b7328-321">`publishMethod="FTP"`betekent dat u instelt **Protocol** naar **FTP - File Transfer Protocol**, en **versleuteling** naar **gewone FTP gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="b7328-321">`publishMethod="FTP"` means that you set **Protocol** to **FTP - File Transfer Protocol**, and **Encryption** to **Use plain FTP**.</span></span>
* <span data-ttu-id="b7328-322">`userName`en `userPWD` zijn de sleutels voor de werkelijke gebruikersnaam en wachtwoord waarden die u hebt opgegeven dat wanneer u de referenties voor de implementatie opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b7328-322">`userName` and `userPWD` are keys for the actual username and password values you specified when you reset the deployment credentials.</span></span> <span data-ttu-id="b7328-323">`userName`is hetzelfde als **implementatie / FTP-gebruiker**.</span><span class="sxs-lookup"><span data-stu-id="b7328-323">`userName` is the same as **Deployment / FTP user**.</span></span> <span data-ttu-id="b7328-324">Deze worden toegewezen aan **gebruiker** en **wachtwoord** in FileZilla.</span><span class="sxs-lookup"><span data-stu-id="b7328-324">They map to **User** and **Password** in FileZilla.</span></span>
* <span data-ttu-id="b7328-325">`ftpPassiveMode="True"`betekent dat de FTP-site maakt gebruik van Passief FTP-overdracht; Selecteer **passieve** op de **Overdrachtinstellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b7328-325">`ftpPassiveMode="True"` means that the FTP site uses passive FTP transfer; select **Passive** on the **Transfer Settings** tab.</span></span>

#### <a name="configure-the-web-app-to-host-a-java-application"></a><span data-ttu-id="b7328-326">De Web-App voor het hosten van een Java-toepassing configureren</span><span class="sxs-lookup"><span data-stu-id="b7328-326">Configure the Web App to host a Java application</span></span>
<span data-ttu-id="b7328-327">Voordat u de toepassing publiceert, moet u enkele configuratie-instellingen wijzigen zodat de web-app kan een Java-toepassing hosten.</span><span class="sxs-lookup"><span data-stu-id="b7328-327">Before you publish the application, you need to change a few configuration settings so that the web app can host a Java application.</span></span>

1. <span data-ttu-id="b7328-328">In de klassieke portal, gaat u naar de web-app **Dashboard** pagina en klik op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="b7328-328">In the classic portal, go to the web app's **Dashboard** page and click **Configure**.</span></span> <span data-ttu-id="b7328-329">Op de **configureren** pagina, geeft u de volgende instellingen.</span><span class="sxs-lookup"><span data-stu-id="b7328-329">On the **Configure** page, specify the following settings.</span></span>
2. <span data-ttu-id="b7328-330">In **Java-versie** de standaardwaarde is **uit**; de Java-versie selecteren die uw toepassing doelen; bijvoorbeeld 1.7.0_51.</span><span class="sxs-lookup"><span data-stu-id="b7328-330">In **Java version** the default is **Off**; select the Java version your application targets; for example 1.7.0_51.</span></span> <span data-ttu-id="b7328-331">Nadat u dit doet, zorg er ook die **webcontainer** is ingesteld op een versie van Tomcat-Server.</span><span class="sxs-lookup"><span data-stu-id="b7328-331">After you do this, also make sure that **Web container** is set to a version of Tomcat Server.</span></span>
3. <span data-ttu-id="b7328-332">In **standaarddocumenten**, index.jsp toevoegen en verplaatsen naar het begin van de lijst.</span><span class="sxs-lookup"><span data-stu-id="b7328-332">In **Default Documents**, add index.jsp and move it up to the top of the list.</span></span> <span data-ttu-id="b7328-333">(Het standaardbestand voor web-apps is hostingstart.html.)</span><span class="sxs-lookup"><span data-stu-id="b7328-333">(The default file for web apps is hostingstart.html.)</span></span>
4. <span data-ttu-id="b7328-334">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="b7328-334">Click **Save**.</span></span>

#### <a name="publish-your-application-using-kudu"></a><span data-ttu-id="b7328-335">Uw toepassing publiceren via Kudu</span><span class="sxs-lookup"><span data-stu-id="b7328-335">Publish your application using Kudu</span></span>
<span data-ttu-id="b7328-336">Er is een manier om de toepassing publiceren met de Kudu debug-console die is ingebouwd in Azure.</span><span class="sxs-lookup"><span data-stu-id="b7328-336">One way to publish the application is to use the Kudu debug console built into Azure.</span></span> <span data-ttu-id="b7328-337">Kudu bekend is dat deze stabiel en consistent zijn met App Service Web Apps en Tomcat-Server.</span><span class="sxs-lookup"><span data-stu-id="b7328-337">Kudu is known to be stable and consistent with App Service Web Apps and Tomcat Server.</span></span> <span data-ttu-id="b7328-338">U kunt de console voor de web-app openen door te bladeren naar een URL van de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="b7328-338">You access the console for the web app by browsing to a URL of the following form:</span></span>

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. <span data-ttu-id="b7328-339">Voor deze procedure bevindt de Kudu-console zich in de volgende URL; Blader naar deze locatie:</span><span class="sxs-lookup"><span data-stu-id="b7328-339">For this procedure, the Kudu console is located at the following URL; browse to this location:</span></span>
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. <span data-ttu-id="b7328-340">Selecteer in het bovenste menu **Console fouten opsporen > CMD**.</span><span class="sxs-lookup"><span data-stu-id="b7328-340">From the top menu, select **Debug Console > CMD**.</span></span>
3. <span data-ttu-id="b7328-341">In de console vanaf de opdrachtregel, gaat u naar `/site/wwwroot` (of klik op `site`, klikt u vervolgens `wwwroot` in de directoryweergave aan de bovenkant van de pagina):</span><span class="sxs-lookup"><span data-stu-id="b7328-341">In the console command line, navigate to `/site/wwwroot` (or click `site`, then `wwwroot` in the directory view at the top of the page):</span></span>
   
    `cd /site/wwwroot`
4. <span data-ttu-id="b7328-342">Nadat u hebt opgegeven **Java-versie**, Tomcat-server moet een map webapps maken.</span><span class="sxs-lookup"><span data-stu-id="b7328-342">After you specify **Java version**, Tomcat server should create a webapps directory.</span></span> <span data-ttu-id="b7328-343">Navigeer naar de map WebApps op de opdrachtregel van de console:</span><span class="sxs-lookup"><span data-stu-id="b7328-343">In the console command line, navigate to the webapps directory:</span></span>
   
    `mkdir webapps`
   
    `cd webapps`
5. <span data-ttu-id="b7328-344">Sleep JSPHello.war van `<project-path>/JSPHello/src/` en zet het neer in de weergave van de directory Kudu onder `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="b7328-344">Drag JSPHello.war from `<project-path>/JSPHello/src/` and drop it into the Kudu directory view under `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="b7328-345">Sleep niet het aan het gebied 'Hier naartoe slepen om te uploaden en zip-', omdat Tomcat wordt behouden.</span><span class="sxs-lookup"><span data-stu-id="b7328-345">Do not drag it to the "Drag here to upload and zip" area, because Tomcat will unzip it.</span></span>
   
   ![][8]

<span data-ttu-id="b7328-346">Op de eerste JSPHello.war wordt weergegeven in het gebied van directory zelfstandig:</span><span class="sxs-lookup"><span data-stu-id="b7328-346">At first JSPHello.war appears in the directory area by itself:</span></span>

  ![][9]

<span data-ttu-id="b7328-347">Tomcat-Server wordt het WAR-bestand uitpakken naar een map met uitgepakte JSPHello in korte tijd (waarschijnlijk minder dan 5 minuten).</span><span class="sxs-lookup"><span data-stu-id="b7328-347">In a short time (probably less than 5 minutes) Tomcat Server will unzip the WAR file into an unpacked JSPHello directory.</span></span> <span data-ttu-id="b7328-348">Klik op de hoofdmap of index.jsp is uitgepakt en er wordt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="b7328-348">Click the ROOT directory to see whether index.jsp has been unzipped and copied there.</span></span> <span data-ttu-id="b7328-349">Zo ja, ga dan terug naar de map WebApps om te zien of de uitgepakte JSPHello-map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7328-349">If so, navigate back to the webapps directory to see whether the unpacked JSPHello directory has been created.</span></span> <span data-ttu-id="b7328-350">Als u deze items niet ziet, wacht en herhaalt.</span><span class="sxs-lookup"><span data-stu-id="b7328-350">If you do not see these items, wait and repeat.</span></span>

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a><span data-ttu-id="b7328-351">Uw toepassing publiceren via FileZilla (optioneel)</span><span class="sxs-lookup"><span data-stu-id="b7328-351">Publish your application using FileZilla (optional)</span></span>
<span data-ttu-id="b7328-352">Een ander hulpprogramma die kunt u de toepassing publiceren is FileZilla, een populaire van derden FTP-client met een handige, grafische gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="b7328-352">Another tool you can use to publish the application is FileZilla, a popular third-party FTP client with a convenient, graphical UI.</span></span> <span data-ttu-id="b7328-353">U kunt downloaden en installeren van FileZilla van [http://filezilla-project.org/](http://filezilla-project.org/) als u nog geen deze.</span><span class="sxs-lookup"><span data-stu-id="b7328-353">You can download and install FileZilla from [http://filezilla-project.org/](http://filezilla-project.org/) if you do not already have it.</span></span> <span data-ttu-id="b7328-354">Zie voor meer informatie over het gebruik van de client de [FileZilla documentatie](https://wiki.filezilla-project.org/Documentation) en dit blogbericht op [FTP-Clients - deel 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span><span class="sxs-lookup"><span data-stu-id="b7328-354">For more information on using the client, see the [FileZilla documentation](https://wiki.filezilla-project.org/Documentation) and this blog entry on [FTP Clients - Part 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).</span></span>

1. <span data-ttu-id="b7328-355">Klik in de FileZilla, **bestand > sitebeheerder**.</span><span class="sxs-lookup"><span data-stu-id="b7328-355">In FileZilla, click **File > Site Manager**.</span></span>
2. <span data-ttu-id="b7328-356">In de **sitebeheerder** dialoogvenster, klikt u op **nieuwe Site**.</span><span class="sxs-lookup"><span data-stu-id="b7328-356">In the **Site Manager** dialog, click **New Site**.</span></span> <span data-ttu-id="b7328-357">Een nieuwe lege FTP-site wordt weergegeven in **Selecteer vermelding** waarin u een naam te geven.</span><span class="sxs-lookup"><span data-stu-id="b7328-357">A new blank FTP site will appear in **Select Entry** prompting you to provide a name.</span></span> <span data-ttu-id="b7328-358">Naam voor deze procedure `AzureWebDemo-FTP`.</span><span class="sxs-lookup"><span data-stu-id="b7328-358">For this procedure, name it `AzureWebDemo-FTP`.</span></span>
   
    <span data-ttu-id="b7328-359">Op de **algemene** tabblad, geeft u de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="b7328-359">On the **General** tab, specify the following settings:</span></span>
   
   * <span data-ttu-id="b7328-360">**Host:** Enter de **FTP-hostnaam** die u hebt gekopieerd vanuit het dashboard.</span><span class="sxs-lookup"><span data-stu-id="b7328-360">**Host:** Enter the **FTP Host Name** that you copied from the dashboard.</span></span>
   * <span data-ttu-id="b7328-361">**Poort:** (dit leeg laat, als dit een passief-overdracht is en de poort wordt bepaald door de server.)</span><span class="sxs-lookup"><span data-stu-id="b7328-361">**Port:** (Leave this blank, as this is a passive transfer and the server will determine the port to use.)</span></span>
   * <span data-ttu-id="b7328-362">**Protocol:** FTP File Transfer Protocol</span><span class="sxs-lookup"><span data-stu-id="b7328-362">**Protocol:** FTP File Transfer Protocol</span></span>
   * <span data-ttu-id="b7328-363">**Versleuteling:** gewone FTP gebruiken</span><span class="sxs-lookup"><span data-stu-id="b7328-363">**Encryption:** Use plain FTP</span></span>
   * <span data-ttu-id="b7328-364">**Aanmeldingstype:** normaal</span><span class="sxs-lookup"><span data-stu-id="b7328-364">**Logon Type:** Normal</span></span>
   * <span data-ttu-id="b7328-365">**Gebruiker:** invoeren van de implementatie / FTP-gebruiker die u hebt gekopieerd vanuit het dashboard.</span><span class="sxs-lookup"><span data-stu-id="b7328-365">**User:** Enter the Deployment / FTP user that you copied from the dashboard.</span></span> <span data-ttu-id="b7328-366">Dit is de volledige gebruikersnaam van het FTP-, die het formulier heeft *webappname\username*.</span><span class="sxs-lookup"><span data-stu-id="b7328-366">This is the full FTP username, which has the form *webappname\username*.</span></span>
   * <span data-ttu-id="b7328-367">**Wachtwoord:** Voer het wachtwoord die u hebt opgegeven als u instelt dat de referenties voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="b7328-367">**Password:** Enter the password that you specified when you set the deployment credentials.</span></span>
     
     <span data-ttu-id="b7328-368">Op de **Overdrachtinstellingen** tabblad **passieve**.</span><span class="sxs-lookup"><span data-stu-id="b7328-368">On the **Transfer Settings** tab, select **Passive**.</span></span>
3. <span data-ttu-id="b7328-369">Klik op **Verbinden**.</span><span class="sxs-lookup"><span data-stu-id="b7328-369">Click **Connect**.</span></span> <span data-ttu-id="b7328-370">Als geslaagd, FileZilla van console wordt weergegeven een `Status: Connected` bericht en probleem een `LIST` opdracht om een lijst van de mapinhoud.</span><span class="sxs-lookup"><span data-stu-id="b7328-370">If successful, FileZilla's console will display a `Status: Connected` message and issue a `LIST` command to list the directory contents.</span></span>
4. <span data-ttu-id="b7328-371">In de **lokale** deelvenster site, selecteer de bron directory waarin het bestand JSPHello.war zich bevindt; het pad moet de volgende strekking:</span><span class="sxs-lookup"><span data-stu-id="b7328-371">In the **Local** site panel, select the source directory in which the JSPHello.war file resides; the path will be similar to the following:</span></span>
   
    `<project-path>/JSPHello/src/`
5. <span data-ttu-id="b7328-372">In de **externe** deelvenster site, selecteer de doelmap.</span><span class="sxs-lookup"><span data-stu-id="b7328-372">In the **Remote** site panel, select the destination folder.</span></span> <span data-ttu-id="b7328-373">Implementeert u het WAR-bestand naar de `webapps` map onder de hoofdmap van de web-app.</span><span class="sxs-lookup"><span data-stu-id="b7328-373">You will deploy the WAR file to the `webapps` directory under the web app's root.</span></span> <span data-ttu-id="b7328-374">Navigeer naar `/site/wwwroot`, met de rechtermuisknop op `wwwroot`, en selecteer **maken directory**.</span><span class="sxs-lookup"><span data-stu-id="b7328-374">Navigate to `/site/wwwroot`, right-click on `wwwroot`, and select **Create directory**.</span></span> <span data-ttu-id="b7328-375">Naam van de map `webapps` en voert u deze map.</span><span class="sxs-lookup"><span data-stu-id="b7328-375">Name the directory `webapps` and enter that directory.</span></span>
6. <span data-ttu-id="b7328-376">Transfer JSPHello.war naar `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="b7328-376">Transfer JSPHello.war to `/site/wwwroot/webapps`.</span></span> <span data-ttu-id="b7328-377">Selecteer JSPHello.war in de **lokale** lijst bestand, met de rechtermuisknop op het en selecteert u **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="b7328-377">Select JSPHello.war in the **Local** file list, right-click on it and select **Upload**.</span></span> <span data-ttu-id="b7328-378">U ziet het weergegeven in `/site/wwwroot/webapps`.</span><span class="sxs-lookup"><span data-stu-id="b7328-378">You should see it appear in `/site/wwwroot/webapps`.</span></span>
7. <span data-ttu-id="b7328-379">Nadat u JSPHello.war gekopieerd naar de map WebApps, Tomcat-Server automatisch wordt uitgepakt (uitpakken van) de bestanden in het WAR-bestand.</span><span class="sxs-lookup"><span data-stu-id="b7328-379">After you copy JSPHello.war to the webapps directory, Tomcat Server will automatically unpack (unzip) the files in the WAR file.</span></span> <span data-ttu-id="b7328-380">Hoewel Tomcat-Server bijna onmiddellijk uitpakken begint, kan het lang duren voordat tijd (mogelijk uren) voor de bestanden in de FTP-client wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b7328-380">Although Tomcat Server begins unpacking almost immediately, it might take a long time (possibly hours) for the files to appear in the FTP client.</span></span>

#### <a name="run-the-hello-world-application-on-the-web-app"></a><span data-ttu-id="b7328-381">De toepassing Hello World uitvoeren op de Web-App</span><span class="sxs-lookup"><span data-stu-id="b7328-381">Run the Hello World application on the Web App</span></span>
1. <span data-ttu-id="b7328-382">Nadat u hebt het WAR-bestand wordt geüpload en geverifieerd dat Tomcat-server is gemaakt met een uitgepakte `JSPHello` directory, blader naar `http://webdemowebapp.azurewebsites.net/JSPHello` de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b7328-382">After you have uploaded the WAR file and verified that Tomcat server has created an unpacked `JSPHello` directory, browse to `http://webdemowebapp.azurewebsites.net/JSPHello` to run the application.</span></span>
   
   > <span data-ttu-id="b7328-383">**Opmerking:** als u op **Bladeren** vanuit de klassieke portal krijgt u mogelijk de standaard-webpagina weergegeven met de tekst "dit op basis van Java-webtoepassing is gemaakt."</span><span class="sxs-lookup"><span data-stu-id="b7328-383">**Note:** If you click **Browse** from the classic portal, you might get the default webpage, saying "This Java based web application has been successfully created."</span></span> <span data-ttu-id="b7328-384">Mogelijk moet de webpagina vernieuwen om de uitvoer van de toepassing in plaats van de webpagina die standaard weergeven.</span><span class="sxs-lookup"><span data-stu-id="b7328-384">You might have to refresh the webpage in order to view the application output instead of the default webpage.</span></span>
   > 
   > 
2. <span data-ttu-id="b7328-385">Wanneer de toepassing wordt uitgevoerd, ziet u een webpagina met de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="b7328-385">When the application runs, you should see a web page with the following output:</span></span>
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a><span data-ttu-id="b7328-386">Azure-resources opschonen</span><span class="sxs-lookup"><span data-stu-id="b7328-386">Clean up Azure resources</span></span>
<span data-ttu-id="b7328-387">Deze procedure maakt u een App Service-web-app.</span><span class="sxs-lookup"><span data-stu-id="b7328-387">This procedure creates an App Service web app.</span></span> <span data-ttu-id="b7328-388">U wordt gefactureerd voor de resource als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="b7328-388">You will be billed for the resource as long as it exists.</span></span> <span data-ttu-id="b7328-389">Tenzij u van plan bent om door te gaan met de web-app voor testdoeleinden of ontwikkeling, moet u stoppen of te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b7328-389">Unless you plan to continue using the web app for testing or development, you should consider stopping or deleting it.</span></span> <span data-ttu-id="b7328-390">Een web-app is gestopt, nog steeds een kleine vergoeding worden, maar u kunt deze opnieuw starten op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="b7328-390">A web app that has been stopped will still incur a small charge, but you can restart it at any time.</span></span> <span data-ttu-id="b7328-391">Als u een web-app verwijdert, worden alle gegevens die u hebt geüpload naar het gewist.</span><span class="sxs-lookup"><span data-stu-id="b7328-391">Deleting a web app erases all data you have uploaded to it.</span></span>

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
