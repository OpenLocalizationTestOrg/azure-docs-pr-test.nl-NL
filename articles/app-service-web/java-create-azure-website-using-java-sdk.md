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
# <a name="create-a-web-app-in-azure-app-service-using-hello-azure-sdk-for-java"></a>Een Web-App maken in Azure App Service met behulp van hello Azure SDK voor Java
<!-- Azure Active Directory workflow is not yet available on hello Azure Portal -->

## <a name="overview"></a>Overzicht
Dit overzicht toont u hoe een Azure-SDK voor Java-toepassing maakt een Web-App in toocreate [Azure App Service][Azure App Service], implementeert u een toepassing tooit. Deze bestaat uit twee delen:

* Deel 1 laat zien hoe toobuild een Java-toepassing die wordt gemaakt een web-app.
* Deel 2 laat zien hoe toocreate een eenvoudige 'Hallo wereld'-JSP-toepassing en gebruik een FTP-client toodeploy code tooApp Service.

## <a name="prerequisites"></a>Vereisten
### <a name="software-installations"></a>Software-installaties
Hallo AzureWebDemo toepassingscode in dit artikel is geschreven met behulp van Azure Java SDK 0.7.0, die u kunt installeren met behulp van Hallo [Web Platform Installer] [ Web Platform Installer] (WebPI). Bovendien moet u ervoor dat toouse Hallo meest recente versie van Hallo [Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]. Na de installatie van SDK Hallo Hallo afhankelijkheden in uw Eclipse-project bijwerken door het uitvoeren van **Index bijwerken** in **Maven-opslagplaatsen**, voeg deze opnieuw Hallo meest recente versie van elk pakket in Hallo  **Afhankelijkheden** venster. U kunt Hallo-versie van de geïnstalleerde software in Eclipse controleren door te klikken op **Help > Details van de installatie**; moet u ten minste hebben Hallo volgende versies:

* Pakket voor Microsoft Azure-beheerbibliotheken voor Java 0.7.0.20150309
* Eclipse IDE voor Java EE-ontwikkelaars 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Maken en configureren van Cloud-bronnen in Azure
Voordat u deze procedure begint, moet u toohave een actief Azure-abonnement nodig en u een standaard Active Directory (AD) in Azure instellen.

### <a name="create-an-active-directory-ad-in-azure"></a>Maken van een Active Directory (AD) in Azure
Als u nog geen een Active Directory (AD) voor uw Azure-abonnement, meld u aan bij Hallo [klassieke Azure-portal] [ Azure classic portal] met je Microsoft-account. Als u meerdere abonnementen hebt, klikt u op **abonnementen** en selecteer Hallo standaarddirectory voor Hallo abonnement gewenste toouse voor dit project. Klik vervolgens op **toepassen** tooswitch toothat abonnementweergave.

1. Selecteer **Active Directory** in het menu links op Hallo van. **Klik op Nieuw > Directory > aangepast maken**.
2. In **map toevoegen**, selecteer **nieuwe map maken**.
3. In **naam**, een mapnaam opgeven.
4. In **domein**, voer een domeinnaam in. Dit is een eenvoudige domeinnaam die is opgenomen in de standaardinstelling met uw directory; Hallo formulier heeft `<domain_name>.onmicrosoft.com`. U kunt een naam op basis van de mapnaam hello of een andere domeinnaam die u bezit. Later kunt u toevoegen aan een andere domeinnaam die uw organisatie al gebruikt.
5. In **land of regio**, selecteer uw land.

Zie voor meer informatie over AD [wat is er een Azure AD-directory][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Een Beheercertificaat voor Azure maken
beheer van certificaten tooauthenticate Hello Azure SDK voor Java gebruikt met Azure-abonnementen. Dit zijn de X.509 v3-certificaten gebruiken van tooauthenticate een clienttoepassing die gebruikmaakt van Hallo Service Management API tooact namens Hallo eigenaar toomanage abonnement abonnementresources.

Hallo-code in deze procedure maakt gebruik van een zelfondertekend certificaat tooauthenticate met Azure. Voor deze procedure u moet toocreate een certificaat en upload het toohello [klassieke Azure-portal] [ Azure classic portal] tevoren. Dit omvat het Hallo stappen te volgen:

* Een PFX-bestand voor uw clientcertificaat genereren en lokaal opslaat.
* Genereer een beheercertificaat (CER-bestand) van Hallo PFX-bestand.
* Upload Hallo CER-bestand tooyour Azure-abonnement.
* Converteren naar JKS, Hallo PFX-bestand omdat deze indeling tooauthenticate met behulp van certificaten maakt gebruik van Java.
* Schrijven van de toepassing hello verificatiecode, die toohello lokaal JKS-bestand verwijst.

Wanneer u deze procedure hebt voltooid, Hallo CER certificaat wordt opgeslagen in uw Azure-abonnement en Hallo JKS certificaat wordt opgeslagen op uw lokale schijf. Zie voor meer informatie over certificaten voor [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Een certificaat maken
toocreate uw eigen zelf-ondertekend certificaat, open de opdrachtconsole van een op het besturingssysteem en Hallo volgende opdrachten uitvoeren.

> **Opmerking:** Hallo-computer waarop u deze opdracht uitvoert moet Hallo JDK geïnstalleerd hebben. Hallo pad toohello keytool is ook afhankelijk van Hallo locatie waarin u Hallo JDK installeren. Zie voor meer informatie [sleutel en certificaat Management Tool (keytool)] [ Key and Certificate Management Tool (keytool)] in Hallo Java online documenten.
> 
> 

toocreate hello pfx-bestand:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

toocreate hello cer-bestand:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

Waarbij:

* `<java-install-dir>`Hallo pad toohello directory waarin u Java geïnstalleerd is.
* `<keystore-id>`Hallo keystore item-id is (bijvoorbeeld `AzureRemoteAccess`).
* `<cert-store-dir>`Hallo pad toohello map waarin u certificaten toostore is (bijvoorbeeld `C:/Certificates`).
* `<cert-file-name>`Hallo-naam van het Hallo-certificaatbestand (bijvoorbeeld `AzureWebDemoCert`).
* `<password>`Hallo wachtwoord u tooprotect Hallo certificaat kiezen Er moet ten minste 6 tekens lang zijn. Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.
* `<dname>`Hallo X.500-DN-naam toobe alias gekoppeld is en wordt gebruikt als Hallo verlener en onderwerp velden in Hallo zelf-ondertekend certificaat.

Zie voor meer informatie [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-hello-certificate"></a>Hallo-certificaat uploaden
tooupload een tooAzure zelf-ondertekend certificaat Ga toohello **instellingen** pagina in de klassieke portal hello, en klik vervolgens op Hallo **Beheercertificaten** tabblad. Klik op **uploaden** onderin Hallo Hallo pagina en navigeer toohello locatie van Hallo CER-bestand dat u gemaakt.

#### <a name="convert-hello-pfx-file-into-jks"></a>Hallo PFX-bestand converteren naar JKS
In Hallo Windows-opdrachtpromptvenster (uitgevoerd als beheerder), cd toohello directory met Hallo certificaten en Hallo volgende opdracht uitvoeren waarbij `<java-install-dir>` Hallo map waarin u Java op uw computer hebt geïnstalleerd:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Voer desgevraagd Hallo bestemming keystore wachtwoord; Dit is Hallo wachtwoord voor Hallo JKS-bestand.
2. Voer desgevraagd Hallo bron keystore wachtwoord; Dit is Hallo wachtwoord die u hebt opgegeven voor Hallo PFX-bestand.

Hallo twee wachtwoorden beschikt niet over dezelfde Hallo toobe. Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.

## <a name="build-a-web-app-creation-application"></a>Een Web-App maken toepassing bouwen
### <a name="create-hello-eclipse-workspace-and-maven-project"></a>Maak Hallo Eclipse werkruimte en Maven-Project
In deze sectie maakt u een werkruimte en een Maven-project voor Hallo web-app maken toepassing, met de naam AzureWebDemo.

1. Maak een nieuw Maven-project. Klik op **bestand > Nieuw > Maven-Project**. In **nieuw Maven-Project**, selecteer **maken van een eenvoudig project** en **standaard werkruimte gebruiken**.
2. Op de tweede pagina Hallo van **nieuw Maven-Project**, Hallo volgende opgeven:
   
   * Groeps-ID:`com.<username>.azure.webdemo`
   * Artefact-ID: AzureWebDemo
   * Versie: 0.0.1-SNAPSHOT
   * Verpakking: jar
   * Naam: AzureWebDemo
     
     Klik op **Voltooien**.
3. Hallo nieuw project pom.xml-bestand openen in Projectverkenner. Selecteer Hallo **afhankelijkheden** tabblad. Als dit een nieuw project is, worden er geen pakketten nog vermeld.
4. Open Hallo Maven-opslagplaatsen weergeven. **Klik op Venster > weergave tonen > andere > Maven > Maven-opslagplaatsen** en klik op **OK**. Hallo **Maven-opslagplaatsen** weergave onderin Hallo Hallo IDE wordt weergegeven.
5. Open **globale opslagplaatsen**, klik met de rechtermuisknop Hallo **centrale** opslagplaats en selecteer **Rebuild Index**.
   
    ![][1]
   
    Deze stap kan enige tijd duren, afhankelijk van Hallo snelheid van de verbinding. Wanneer het Hallo-index wordt opnieuw gemaakt, ziet u Hallo Microsoft Azure-pakketten in Hallo **centrale** Maven-opslagplaats.
6. In **afhankelijkheden**, klikt u op **toevoegen**. In **groep-ID invoeren...**  Voer `azure-management`. Selecteer hello-pakketten voor base management en App Service Web Apps management:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Opmerking:** als u Hallo afhankelijkheden na de release van een nieuwe versie bijwerkt, moet u toore-elk Hallo afhankelijkheden in deze lijst toevoegen.
   > Nadat u op **toevoegen** en selecteer elke afhankelijkheid wordt dit weergegeven met het nieuwe versienummer in Hallo Hallo **afhankelijkheden** lijst.
   > 
   > 

Klik op **OK**. Hallo Azure pakketten wordt weergegeven in Hallo **afhankelijkheden** lijst.

### <a name="writing-java-code-toocreate-a-web-app-by-calling-hello-azure-sdk"></a>Java-Code tooCreate schrijven van een Web-App door aanroepen hello Azure SDK
Schrijf nu Hallo-code die de API-in hello Azure SDK voor Java toocreate Hallo App Service-web-app aanroepen.

1. Maak een Java-klasse toocontain Hallo belangrijkste vermelding punt code. In Projectverkenner met de rechtermuisknop op Hallo projectknooppunt en selecteer **Nieuw > klasse**.
2. In **nieuwe Java-klasse**, naam Hallo klasse `WebCreator` en controleer Hallo **openbare statische void main** selectievakje. Hallo selecties ziet er als volgt:
   
    ![][2]
3. Klik op **Voltooien**. Hallo WebCreator.java bestand weergegeven in de Projectverkenner.

### <a name="calling-hello-azure-api-toocreate-an-app-service-web-app"></a>Hello Azure API tooCreate het aanroepen van een App Service-Web-App
#### <a name="add-necessary-imports"></a>Vereiste imports toevoegen
Voeg in WebCreator.java, Hallo na invoer; deze invoer bieden toegang tooclasses in Hallo management-bibliotheken voor het verbruik van Azure-API's:

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


#### <a name="define-hello-main-entry-point-class"></a>Hallo belangrijkste vermelding punt klasse definiëren
Hallo hoofdklasse omdat doel Hallo AzureWebDemo toepassing hello toocreate een App Service-Web-App, een naam voor deze toepassing `WebAppCreator`. Deze klasse biedt Hallo belangrijkste vermelding punt code waarmee hello Azure Service Management API toocreate Hallo web-app wordt aangeroepen.

Hallo volgende parameterdefinities voor Hallo web-app en webruimte toevoegen. U moet uw eigen Azure-abonnement-ID en certificaat informatie tooprovide.

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

Waarbij:

* `<subscription-id>`hello Azure-abonnement-ID die u toocreate Hallo resource wilt is.
* `<certificate-store-path>`Hallo pad en bestandsnaam toohello JKS bestand in uw directory van de winkel lokale certificaatarchief is. Bijvoorbeeld: `C:/Certificates/CertificateName.jks` voor Linux en `C:\Certificates\CertificateName.jks` voor Windows.
* `<certificate-password>`u hebt opgegeven tijdens het maken van uw certificaat JKS Hallo-wachtwoord is.
* `webAppName`de naam die u kiezen; deze procedure gebruikt u de naam van de Hallo `WebDemoWebApp`. de volledige domeinnaam Hallo is Hallo `webAppName` Hello `domainName` toegevoegd, dus in dit geval Hallo volledige domein is `webdemowebapp.azurewebsites.net`.
* `domainName`moet worden opgegeven, zoals hierboven.
* `webSpaceName`moet een Hallo-waarden die zijn gedefinieerd in Hallo [WebSpaceNames] [ WebSpaceNames] klasse.
* `appServicePlanName`moet worden opgegeven, zoals hierboven.

> **Opmerking:** telkens wanneer u deze toepassing uitvoeren, moet u toochange Hallo-waarde van `webAppName` en `appServicePlanName` (of verwijderen van de web-app Hallo op Hallo Azure Portal) voordat u Hallo toepassing opnieuw uitvoert. Anders mislukt uitvoering omdat hello dezelfde resource al in Azure bestaat.
> 
> 

#### <a name="define-hello-web-creation-method"></a>Hallo-methode voor het maken van web definiëren
Definieer vervolgens een methode toocreate Hallo web-app. Deze methode `createWebApp`, Hallo parameters van Hallo web-app en Hallo webruimte bevat. Ook maakt en configureert deze Hallo App Service Web Apps management-client, die wordt gedefinieerd door Hallo [WebSiteManagementClient] [ WebSiteManagementClient] object. Hallo-management-client is sleutel toocreating Web-Apps. Het biedt de RESTful-web-services waarmee toepassingen toomanage web-apps (het uitvoeren van bewerkingen zoals maken, bijwerken en verwijderen) door het Hallo servicebeheer-API aanroepen.

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

Hallo code Hallo HTTP-statuscode van antwoord Hallo die aangeeft of geslaagd of mislukt wordt uitgevoerd en als dit lukt, wordt de uitvoer Hallo-naam van de web-app gemaakt Hallo.

#### <a name="define-hello-main-method"></a>Hallo main() methode definiëren
Geef Hallo main() methode code die aanroepen createWebApp() toocreate Hallo web-app.

Tenslotte roept `createWebApp` van `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-hello-application-and-verify-web-app-creation"></a>Hallo-toepassing uitvoeren en controleer of web-apps maken
tooverify die uw toepassing wordt uitgevoerd, klikt u op **uitvoeren > Voer**. Wanneer de toepassing hello is voltooid wordt uitgevoerd, ziet u Hallo uitvoer in Hallo Eclipse-console te volgen:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Meld u aan bij de klassieke Azure-portal Hallo en klik op **Web-Apps**. Hallo nieuwe web-app moet worden weergegeven in de lijst met de Hallo-Web-Apps binnen een paar minuten.

## <a name="deploying-an-application-toohello-web-app"></a>Een toepassing toohello Web-App implementeren
Nadat u AzureWebDemo hebt uitgevoerd en gemaakte Hallo nieuwe web-app, meld u aan bij de klassieke portal hello, klikt u op **Web-Apps**, en selecteer **WebDemoWebApp** in Hallo **Web-Apps** lijst. Klik in de dashboardpagina Hallo van web-app op **Bladeren** (of klik op Hallo-URL, `webdemowebapp.azurewebsites.net`) toonavigate tooit. U ziet een pagina lege tijdelijke aanduiding omdat geen inhoud gepubliceerde toohello web-app nog is.

U wordt vervolgens een 'Hallo wereld'-toepassing maken en deze toohello web-app implementeren.

### <a name="create-a-jsp-hello-world-application"></a>Een JSP Hallo wereld-toepassing maken
#### <a name="create-hello-application"></a>Hallo-toepassing maken
In volgorde toodemonstrate hoe toodeploy een webpagina van de toohello toepassing hello na procedure ziet u hoe toocreate een eenvoudige "Hallo wereld" Java-toepassing en upload het toohello App Service Web-App die uw toepassing gemaakt.

1. Klik op **bestand > Nieuw > Dynamic webproject**. Noem deze `JSPHello`. U hoeft geen andere instellingen in dit dialoogvenster niet toochange. Klik op **Voltooien**.
   
    ![][3]
2. Vouw in Projectverkenner Hallo **JSPHello** project, met de rechtermuisknop op **WebContent**, klikt u vervolgens op **Nieuw > JSP-bestand**. Naam in het dialoogvenster Nieuw JSP-bestand Hallo Hallo nieuw bestand `index.jsp`. Klik op **Volgende**.
3. In Hallo **JSP-sjabloon selecteren** dialoogvenster **nieuw JSP-bestand (html)** en klik op **voltooien**.
4. Voeg in index.jsp, na de code in Hallo Hallo `<head>` en `<body>` tag secties:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, hello time is <%= date %> 
        </body>

#### <a name="run-hello-hello-world-application-in-localhost"></a>Hallo wereld Hallo toepassing uitvoert in localhost
Voordat u deze toepassing uitvoert, moet u tooconfigure enkele eigenschappen.

1. Klik met de rechtermuisknop Hallo **JSPHello** project en selecteer **eigenschappen**.
2. In Hallo **eigenschappen** dialoogvenster: Selecteer **Javabuild-pad**, selecteer Hallo **rangschikken en exporteren** tabblad controle **JRE systeembibliotheek**, klikt u vervolgens op **Up** toomove het toohello boven aan Hallo-lijst.
   
    ![][4]
3. Ook in Hallo **eigenschappen** dialoogvenster: Selecteer **Runtimes gericht** en klik op **nieuw**.
4. In Hallo **nieuwe Server Runtime-omgeving** dialoogvenster, selecteert u een server, zoals **Apache Tomcat v7.0** en klik op **volgende**. In Hallo **Tomcat-Server** dialoogvenster, set **naam** te`Apache Tomcat v7.0`, en stel **Tomcat-installatiedirectory** toohello directory waarin u de versie van Hallo geïnstalleerd Gewenste toouse Tomcat-server.
   
    ![][5]
   
    Klik op **Voltooien**.
5. U terugkeren toohello **Runtimes gericht** pagina Hallo **eigenschappen** dialoogvenster. Selecteer **Apache Tomcat v7.0**, klikt u vervolgens op **OK**.
   
    ![][6]
6. In Eclipse hello **uitvoeren** menu, klikt u op **uitvoeren**. In Hallo **uitvoeren als** dialoogvenster Selecteer **uitgevoerd op Server**. In Hallo **uitgevoerd op Server** dialoogvenster Selecteer **Tomcat v7.0 Server**:
   
    ![][7]
   
    Klik op **Voltooien**.
7. Wanneer Hallo toepassing wordt uitgevoerd, ziet u Hallo **JSPHello** pagina wordt weergegeven in een venster localhost in Eclipse (`http://localhost:8080/JSPHello/`), weer te geven Hallo volgende weergegeven:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-hello-application-as-a-war"></a>Hallo toepassing als een WAR exporteren
Hallo web project-bestanden exporteren als een web-archiefbestand (WAR), zodat u toohello web-app kunt implementeren. Hallo volgende web project-bestanden bevinden zich in Hallo WebContent map:

    META-INF
    WEB-INF
    index.jsp

1. Hallo WebContent map met de rechtermuisknop en selecteer **exporteren**.
2. In Hallo **exporteren Selecteer** dialoogvenster, klikt u op **Web > WAR** bestand en klik vervolgens op **volgende**.
3. In Hallo **WAR exporteren** dialoogvenster Hallo src map te selecteren in het huidige project Hallo en Hallo-naam van Hallo WAR-bestand aan Hallo einde bevatten. Bijvoorbeeld:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Zie voor meer informatie over het implementeren van WAR bestanden [toevoegen van een Java-toepassing tooAzure App Service Web Apps](web-sites-java-add-app.md).

### <a name="deploying-hello-hello-world-application-using-ftp"></a>Hallo Hallo wereld-toepassing met behulp van FTP implementeren
Selecteer een toepassing van derden FTP-client toopublish Hallo. Deze procedure wordt beschreven twee opties: Hallo Kudu-console is ingebouwd in Azure. en FileZilla, een populaire hulpmiddel met een handige, grafische gebruikersinterface.

> **Opmerking:** hello Azure Toolkit voor Eclipse implementatie toostorage accounts ondersteunt en cloud services, maar ondersteunt geen implementatie tooweb apps. U kunt implementeren toostorage accounts en cloud services met behulp van een Azure-implementatieproject, zoals beschreven in [maken van een Hallo wereld-toepassing voor Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), maar niet tooweb apps. Andere methoden zoals FTP of GitHub tootransfer bestanden tooyour web-app gebruiken.
> 
> **Opmerking:** niet raadzaam met FTP van Hallo Windows-opdrachtpromptvenster (Hallo FTP.EXE opdrachtregelprogramma dat wordt geleverd met Windows). FTP-clients die gebruikmaken van actieve FTP, zoals FTP.EXE, vaak een failover toowork firewalls. Actieve FTP wordt een interne op basis van LAN-adres, toowhich een FTP-server, tooconnect waarschijnlijk niet.
> 
> 

Zie voor meer informatie over implementatie tooan App Service web-app met FTP Hallo volgende onderwerpen:

* [Implementeren met behulp van een FTP-programma](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Implementatiereferenties instellen
Zorg ervoor dat u hebt uitgevoerd Hallo **AzureWebDemo** toepassing toocreate een web-app. U kunt bestanden toothis locatie worden overgebracht.

1. Meld u aan bij de klassieke portal Hallo en klik op **Web-Apps**. Zorg ervoor dat **WebDemoWebApp** wordt weergegeven in de lijst Hallo van web-apps en zorg ervoor dat deze wordt uitgevoerd. Klik op **WebDemoWebApp** tooopen de **Dashboard** pagina.
2. Op Hallo **Dashboard** pagina onder **snel in één oogopslag**, klikt u op **instellen van referenties voor uw implementatie** (als u de referenties voor implementatie al hebt, leest dit  **Opnieuw instellen van referenties voor uw implementatie**).
   
    Referenties voor implementatie zijn gekoppeld aan een Microsoft-account. U moet toospecify een gebruikersnaam en wachtwoord waarmee u kunt met behulp van Git en FTP-toodeploy. U kunt deze referenties toodeploy tooany web-app gebruiken in alle Azure-abonnementen die zijn gekoppeld aan je Microsoft-account. Geef referenties op Git en FTP-implementatie in het dialoogvenster Hallo en record Hallo gebruikersnaam en wachtwoord voor toekomstig gebruik.

#### <a name="get-ftp-connection-information"></a>Gegevens van de FTP-verbinding ophalen
toouse FTP-toodeploy toepassing bestanden toohello nieuwe web-app, moet u de verbindingsgegevens tooobtain. Er zijn twee manieren tooobtain verbindingsgegevens. Eenzijdige toovisit Hallo van web-app is **Dashboard** pagina; hello andere manier is publicatieprofiel toodownload Hallo van web-app. Hallo publicatieprofiel is een XML-bestand informatie zoals de FTP-host en het aanmeldingsaccount referenties voor uw web-apps in Azure App Service bevat. U kunt deze gebruikersnaam en wachtwoord toodeploy tooany web-app gebruiken in alle abonnementen die zijn gekoppeld aan hello Azure-account, niet alleen op deze aanbieding.

tooobtain FTP verbindingsinformatie van de blade Hallo van web-app in Hallo [Azure Portal][Azure Portal]:

1. Onder **Essentials**, vindt en kopieert Hallo **FTP-hostnaam**. Dit is een soortgelijke URI te`ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. Onder **Essentials**, vindt en kopieert **FTP-/ Implementatiegebruiker gebruikersnaam**. Dit heeft Hallo formulier *webappname\deployment-username*; bijvoorbeeld `WebDemoWebApp\deployer77`.

publicatieprofiel tooobtain FTP-verbindingsinformatie van Hallo:

1. Klik op Hallo van web-app blade **Get publicatieprofiel**. Hiermee wordt een lokaal station voor .publishsettings-bestand tooyour gedownload.
2. Hallo .publishsettings-bestand openen in een XML-editor of een teksteditor en zoek Hallo `<publishProfile>` element die `publishMethod="FTP"`. Het moet eruitzien als Hallo volgende:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Houd er rekening mee dat Hallo web-app `publishProfile` instellingen toewijzen toohello FileZilla sitebeheerder instellingen als volgt:

* `publishUrl`is gelijk aan Hallo **FTP-hostnaam**, Hallo waarde die u instelt in **Host**.
* `publishMethod="FTP"`betekent dat u instelt **Protocol** te**FTP - File Transfer Protocol**, en **versleuteling** te**gewone FTP gebruiken**.
* `userName`en `userPWD` zijn de sleutels voor Hallo werkelijke gebruikersnaam en wachtwoord waarden die u hebt opgegeven dat wanneer u referenties voor Hallo implementatie opnieuw. `userName`is gelijk aan Hallo **implementatie / FTP-gebruiker**. Ze wijzen te**gebruiker** en **wachtwoord** in FileZilla.
* `ftpPassiveMode="True"`betekent dat Hallo FTP-site gebruik maakt van Passief FTP-overdracht; Selecteer **passieve** op Hallo **Overdrachtinstellingen** tabblad.

#### <a name="configure-hello-web-app-toohost-a-java-application"></a>Hallo Web-App toohost een Java-toepassing configureren
Voordat u de toepassing hello publiceert, moet u toochange enkele configuratie-instellingen zodat hello web-app een Java-toepassing hosten kan.

1. Ga in de klassieke portal Hallo toohello van web-app **Dashboard** pagina en klik op **configureren**. Op Hallo **configureren** pagina, Hallo na instellingen opgeven.
2. In **Java-versie** Hallo standaardwaarde is **uit**; Selecteer Hallo Java-versie de doelen van uw toepassing, bijvoorbeeld 1.7.0_51. Nadat u dit doet, zorg er ook die **webcontainer** tooa versie van Tomcat-Server is ingesteld.
3. In **standaarddocumenten**, het toevoegen van index.jsp en omhoog toohello boven aan Hallo-lijst. (de standaardlocatie Hallo voor web-apps is hostingstart.html.)
4. Klik op **Opslaan**.

#### <a name="publish-your-application-using-kudu"></a>Uw toepassing publiceren via Kudu
Eenzijdige toopublish Hallo toepassing is toouse hello die kudu debug console die is ingebouwd in Azure. Kudu bekend toobe stabiel en consistent zijn met App Service Web Apps en Tomcat-Server. U openen Hallo-console voor Hallo web-app door te bladeren tooa URL Hallo formulier te volgen:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Voor deze procedure bevindt Hallo Kudu-console zich op Hallo na URL; Blader toothis locatie:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Selecteer in het bovenste menu Hallo **Console fouten opsporen > CMD**.
3. Hallo-console vanaf de opdrachtregel, navigeert u in te`/site/wwwroot` (of klik op `site`, klikt u vervolgens `wwwroot` in Hallo directoryweergave bovenaan Hallo Hallo pagina):
   
    `cd /site/wwwroot`
4. Nadat u hebt opgegeven **Java-versie**, Tomcat-server moet een map webapps maken. Navigeer in Hallo console vanaf de opdrachtregel, toohello map WebApps:
   
    `mkdir webapps`
   
    `cd webapps`
5. Sleep JSPHello.war van `<project-path>/JSPHello/src/` en zet het neer in Hallo Kudu directoryweergave onder `/site/wwwroot/webapps`. Sleep niet het toohello 'Hier naartoe slepen tooupload en zip' gebied omdat Tomcat wordt behouden.
   
   ![][8]

Op de eerste JSPHello.war wordt weergegeven in Hallo directory gebied zelfstandig:

  ![][9]

Tomcat-Server wordt Hallo WAR-bestand uitpakken naar een map met uitgepakte JSPHello in korte tijd (waarschijnlijk minder dan 5 minuten). Klik op Hallo ROOT directory toosee of index.jsp heeft uitgepakt en er wordt gekopieerd. Als dit het geval is, gaat u terug toohello webapps directory toosee of Hallo uitgepakt JSPHello map is gemaakt. Als u deze items niet ziet, wacht en herhaalt.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Uw toepassing publiceren via FileZilla (optioneel)
Een ander hulpprogramma kunt u toopublish Hallo toepassing is FileZilla, een populaire van derden FTP-client met een handige, grafische gebruikersinterface. U kunt downloaden en installeren van FileZilla van [http://filezilla-project.org/](http://filezilla-project.org/) als u nog geen deze. Zie voor meer informatie over het gebruik van de client Hallo Hallo [FileZilla documentatie](https://wiki.filezilla-project.org/Documentation) en dit blogbericht op [FTP-Clients - deel 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. Klik in de FileZilla, **bestand > sitebeheerder**.
2. In Hallo **sitebeheerder** dialoogvenster, klikt u op **nieuwe Site**. Een nieuwe lege FTP-site wordt weergegeven in **Selecteer vermelding** waarin u wordt gevraagd een naam tooprovide. Naam voor deze procedure `AzureWebDemo-FTP`.
   
    Op Hallo **algemene** tabblad, geeft u Hallo volgende instellingen:
   
   * **Host:** Enter Hallo **FTP-hostnaam** die u hebt gekopieerd uit Hallo-dashboard.
   * **Poort:** (dit leeg laat, als dit een passief-overdracht is en Hallo server Hallo poort toouse bepaalt.)
   * **Protocol:** FTP File Transfer Protocol
   * **Versleuteling:** gewone FTP gebruiken
   * **Aanmeldingstype:** normaal
   * **Gebruiker:** Enter Hallo implementatie / FTP-gebruiker die u hebt gekopieerd uit Hallo-dashboard. Dit is Hallo volledige FTP-gebruikersnaam, waarvoor Hallo formulier *webappname\username*.
   * **Wachtwoord:** Hallo-wachtwoord opgeven die u hebt opgegeven tijdens het Hallo-implementatiereferenties instellen.
     
     Op Hallo **Overdrachtinstellingen** tabblad **passieve**.
3. Klik op **Verbinden**. Als geslaagd, FileZilla van console wordt weergegeven een `Status: Connected` bericht en probleem een `LIST` toolist Hallo Mapinhoud opdracht.
4. In Hallo **lokale** deelvenster van de site, selecteer Hallo bronmap in welke Hallo JSPHello.war-bestand bevindt zich; Hallo-pad moet vergelijkbaar toohello volgende:
   
    `<project-path>/JSPHello/src/`
5. In Hallo **externe** deelvenster van de site, selecteer Hallo doelmap. U gaat implementeren Hallo WAR-bestand toohello `webapps` map onder basis-Hallo van web-app. Navigeer te`/site/wwwroot`, met de rechtermuisknop op `wwwroot`, en selecteer **maken directory**. Gebruikersnaammap hello `webapps` en voert u deze map.
6. JSPHello.war te dragen`/site/wwwroot/webapps`. Selecteer JSPHello.war in Hallo **lokale** lijst bestand, met de rechtermuisknop op het en selecteert u **uploaden**. U ziet het weergegeven in `/site/wwwroot/webapps`.
7. Na het kopiëren van JSPHello.war toohello map WebApps Tomcat-Server automatisch wordt uitgepakt (uitpakken)-bestanden in de WAR-bestand Hallo Hallo. Hoewel Tomcat-Server bijna onmiddellijk uitpakken begint, kan het lang duren voordat tijd (mogelijk uren) voor Hallo bestanden tooappear in Hallo FTP-client.

#### <a name="run-hello-hello-world-application-on-hello-web-app"></a>Hallo Hallo wereld-toepassing op Hallo Web-App uitvoeren
1. Nadat u hebt geüpload Hallo WAR-bestand en geverifieerd dat Tomcat-server is gemaakt met een uitgepakte `JSPHello` map te bladeren`http://webdemowebapp.azurewebsites.net/JSPHello` toorun Hallo-toepassing.
   
   > **Opmerking:** als u op **Bladeren** vanuit de klassieke portal hello, krijgt u mogelijk Hallo standaard webpagina, spreken "deze op basis van Java-webtoepassing is gemaakt." U hebt mogelijk toorefresh Hallo webpagina in volgorde tooview Hallo toepassing uitvoer in plaats van de webpagina die standaard Hallo.
   > 
   > 
2. Wanneer de toepassing hello wordt uitgevoerd, ziet u een webpagina Hello volgende uitvoer:
   
    `Hello World, hello time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Azure-resources opschonen
Deze procedure maakt u een App Service-web-app. U wordt gefactureerd voor Hallo resource als deze bestaat. Tenzij u van plan toocontinue Hallo web-app gebruiken voor testdoeleinden of ontwikkeling bent, moet u stoppen of te verwijderen. Een web-app is gestopt, nog steeds een kleine vergoeding worden, maar u kunt deze opnieuw starten op elk gewenst moment. Als u een web-app verwijdert, worden alle gegevens die u hebt geüpload tooit gewist.

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
