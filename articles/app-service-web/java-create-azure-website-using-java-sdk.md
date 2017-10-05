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
# <a name="create-a-web-app-in-azure-app-service-using-the-azure-sdk-for-java"></a>Een Web-App maken in Azure App Service met de Azure SDK voor Java
<!-- Azure Active Directory workflow is not yet available on the Azure Portal -->

## <a name="overview"></a>Overzicht
Dit overzicht toont u het maken van een Azure-SDK voor Java-toepassing maakt een Web-App in [Azure App Service][Azure App Service], vervolgens een toepassing te implementeren. Deze bestaat uit twee delen:

* Deel 1 laat zien hoe een Java-toepassing bouwt die een web-app maakt.
* Deel 2 laat zien hoe u voor het maken van een eenvoudige 'Hallo wereld'-JSP-toepassing en gebruik een FTP-client om code te implementeren in App Service.

## <a name="prerequisites"></a>Vereisten
### <a name="software-installations"></a>Software-installaties
De code van de toepassing AzureWebDemo in dit artikel is geschreven met behulp van Azure Java SDK 0.7.0, die u kunt installeren met behulp van de [Web Platform Installer] [ Web Platform Installer] (WebPI). Bovendien moet u de nieuwste versie van de [Azure Toolkit voor Eclipse][Azure Toolkit for Eclipse]. Nadat u de SDK hebt geïnstalleerd, de afhankelijkheden in uw Eclipse-project bijwerken door het uitvoeren van **Index bijwerken** in **Maven-opslagplaatsen**, voeg deze opnieuw de meest recente versie van elk pakket in de **afhankelijkheden** venster. U kunt de versie van de geïnstalleerde software in Eclipse controleren door te klikken op **Help > Details van de installatie**; u moet ten minste beschikken over de volgende versies:

* Pakket voor Microsoft Azure-beheerbibliotheken voor Java 0.7.0.20150309
* Eclipse IDE voor Java EE-ontwikkelaars 4.4.2.20150219

### <a name="create-and-configure-cloud-resources-in-azure"></a>Maken en configureren van Cloud-bronnen in Azure
Voordat u deze procedure begint, moet u een actief Azure-abonnement hebt en u een standaard Active Directory (AD) in Azure instellen.

### <a name="create-an-active-directory-ad-in-azure"></a>Maken van een Active Directory (AD) in Azure
Als u nog geen een Active Directory (AD) voor uw Azure-abonnement, meld u aan bij de [klassieke Azure-portal] [ Azure classic portal] met je Microsoft-account. Als u meerdere abonnementen hebt, klikt u op **abonnementen** en selecteer de standaardmap voor het abonnement dat u wilt gebruiken voor dit project. Klik vervolgens op **toepassen** overschakelen naar de abonnementweergave van dit.

1. Selecteer **Active Directory** in het menu links. **Klik op Nieuw > Directory > aangepast maken**.
2. In **map toevoegen**, selecteer **nieuwe map maken**.
3. In **naam**, een mapnaam opgeven.
4. In **domein**, voer een domeinnaam in. Dit is een eenvoudige domeinnaam die is opgenomen in de standaardinstelling met uw directory; het formulier heeft `<domain_name>.onmicrosoft.com`. U kunt een naam op basis van de mapnaam of een andere domeinnaam die u bezit. Later kunt u toevoegen aan een andere domeinnaam die uw organisatie al gebruikt.
5. In **land of regio**, selecteer uw land.

Zie voor meer informatie over AD [wat is er een Azure AD-directory][What is an Azure AD directory]?

### <a name="create-a-management-certificate-for-azure"></a>Een Beheercertificaat voor Azure maken
De Azure SDK voor Java maakt gebruik van certificaten voor verificatie met Azure-abonnementen. Dit zijn de X.509 v3-certificaten met u een clienttoepassing die gebruikmaakt van de Service Management API te handelen namens de eigenaar van het abonnement voor het beheren van abonnementresources verifiëren.

De code in deze procedure gebruikt een zelfondertekend certificaat te verifiëren bij Azure. Voor deze procedure moet u een certificaat maken en uploaden naar de [klassieke Azure-portal] [ Azure classic portal] tevoren. Dit omvat de volgende stappen:

* Een PFX-bestand voor uw clientcertificaat genereren en lokaal opslaat.
* Genereer een beheercertificaat (CER-bestand) van het PFX-bestand.
* Het CER-bestand uploaden naar uw Azure-abonnement.
* Converteren naar JKS, het PFX-bestand omdat Java die indeling gebruikt om te verifiëren met behulp van certificaten.
* Schrijven van de toepassing authenticatie code, die naar het lokale JKS-bestand verwijst.

Wanneer u deze procedure hebt voltooid, het CER-certificaat wordt opgeslagen in uw Azure-abonnement en het certificaat JKS wordt opgeslagen op uw lokale schijf. Zie voor meer informatie over certificaten voor [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].

#### <a name="create-a-certificate"></a>Een certificaat maken
Open de opdrachtconsole van een op het besturingssysteem en voer de volgende opdrachten voor het maken van uw eigen zelf-ondertekend certificaat.

> **Opmerking:** de computer waarop u deze opdracht uitvoert de JDK die geïnstalleerd moet hebben. Het pad naar de keytool is ook afhankelijk van de locatie waarin u de JDK installeren. Zie voor meer informatie [sleutel en certificaat Management Tool (keytool)] [ Key and Certificate Management Tool (keytool)] in de online documentatie voor Java.
> 
> 

Het pfx-bestand maken:

    <java-install-dir>/bin/keytool -genkey -alias <keystore-id>
     -keystore <cert-store-dir>/<cert-file-name>.pfx -storepass <password>
     -validity 3650 -keyalg RSA -keysize 2048 -storetype pkcs12
     -dname "CN=Self Signed Certificate 20141118170652"

Het cer-bestand maken:

    <java-install-dir>/bin/keytool -export -alias <keystore-id>
     -storetype pkcs12 -keystore <cert-store-dir>/<cert-file-name>.pfx
     -storepass <password> -rfc -file <cert-store-dir>/<cert-file-name>.cer

Waarbij:

* `<java-install-dir>`het pad naar de map waarin u Java geïnstalleerd is.
* `<keystore-id>`de id van de vermelding keystore (bijvoorbeeld `AzureRemoteAccess`).
* `<cert-store-dir>`het pad naar de map waarin u wilt opslaan van certificaten (bijvoorbeeld `C:/Certificates`).
* `<cert-file-name>`de naam van het certificaatbestand (bijvoorbeeld `AzureWebDemoCert`).
* `<password>`is het wachtwoord dat u wilt beveiligen van het certificaat; Er moet ten minste 6 tekens lang zijn. Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.
* `<dname>`de X.500-DN-naam moet worden gekoppeld met de alias is en als de verlener en onderwerp velden in het zelfondertekende certificaat wordt gebruikt.

Zie voor meer informatie [maken en uploaden van een Beheercertificaat voor Azure][Create and Upload a Management Certificate for Azure].

#### <a name="upload-the-certificate"></a>Het certificaat uploaden
Als u wilt een zelfondertekend certificaat uploaden naar Azure, gaat u naar de **instellingen** pagina in de klassieke portal en klik vervolgens op de **Beheercertificaten** tabblad. Klik op **uploaden** aan de onderkant van de pagina en navigeer naar de locatie van het CER-bestand dat u hebt gemaakt.

#### <a name="convert-the-pfx-file-into-jks"></a>Het PFX-bestand converteren naar JKS
In de opdrachtprompt van Windows (uitgevoerd als beheerder), cd naar de map met de certificaten en voer de volgende opdracht, waarbij `<java-install-dir>` is de directory waarin u Java op uw computer hebt geïnstalleerd:

    <java-install-dir>/bin/keytool.exe -importkeystore
     -srckeystore <cert-store-dir>/<cert-file-name>.pfx
     -destkeystore <cert-store-dir>/<cert-file-name>.jks
     -srcstoretype pkcs12 -deststoretype JKS

1. Voer desgevraagd het wachtwoord van de bestemming keystore; Dit is het wachtwoord voor het bestand JKS.
2. Voer desgevraagd het wachtwoord voor de gegevensbron keystore; Dit is het wachtwoord die u hebt opgegeven voor het PFX-bestand.

De twee wachtwoorden hebt niet dezelfde zijn. Hoewel dit niet wordt aangeraden, kunt u geen wachtwoord invoeren.

## <a name="build-a-web-app-creation-application"></a>Een Web-App maken toepassing bouwen
### <a name="create-the-eclipse-workspace-and-maven-project"></a>De Eclipse-werkruimte en Maven-Project maken
In deze sectie maakt u een werkruimte en een Maven-project voor de web-app maken toepassing, met de naam AzureWebDemo.

1. Maak een nieuw Maven-project. Klik op **bestand > Nieuw > Maven-Project**. In **nieuw Maven-Project**, selecteer **maken van een eenvoudig project** en **standaard werkruimte gebruiken**.
2. Op de tweede pagina van **nieuw Maven-Project**, het volgende opgeven:
   
   * Groeps-ID:`com.<username>.azure.webdemo`
   * Artefact-ID: AzureWebDemo
   * Versie: 0.0.1-SNAPSHOT
   * Verpakking: jar
   * Naam: AzureWebDemo
     
     Klik op **Voltooien**.
3. Het nieuwe project pom.xml-bestand openen in Projectverkenner. Selecteer de **afhankelijkheden** tabblad. Als dit een nieuw project is, worden er geen pakketten nog vermeld.
4. Open de Maven-opslagplaatsen. **Klik op Venster > weergave tonen > andere > Maven > Maven-opslagplaatsen** en klik op **OK**. De **Maven-opslagplaatsen** weergave wordt weergegeven onder aan de IDE.
5. Open **globale opslagplaatsen**, met de rechtermuisknop op de **centrale** opslagplaats en selecteer **Rebuild Index**.
   
    ![][1]
   
    Deze stap kan enige tijd duren, afhankelijk van de snelheid van de verbinding. Wanneer de index wordt opnieuw gemaakt, ziet u de Microsoft Azure-pakketten in de **centrale** Maven-opslagplaats.
6. In **afhankelijkheden**, klikt u op **toevoegen**. In **groep-ID invoeren...**  Voer `azure-management`. Selecteer de pakketten voor base management en App Service Web Apps management:
   
        com.microsoft.azure  azure-management
        com.microsoft.azure  azure-management-websites
   
   > **Opmerking:** als u de afhankelijkheden na de release van een nieuwe versie bijwerkt, moet u elk van de afhankelijkheden in deze lijst opnieuw toevoegen.
   > Nadat u op **toevoegen** en selecteer elke afhankelijkheid wordt dit weergegeven met het nieuwe versienummer in de **afhankelijkheden** lijst.
   > 
   > 

Klik op **OK**. De Azure-pakketten worden weergegeven de **afhankelijkheden** lijst.

### <a name="writing-java-code-to-create-a-web-app-by-calling-the-azure-sdk"></a>Schrijven van Java-Code voor het maken van een Web-App door het aanroepen van de Azure SDK
Vervolgens wordt de code schrijven waarmee roept de API's in de Azure SDK voor Java voor het maken van de App Service-web-app.

1. Maak een Java-klasse om de belangrijkste vermelding punt code bevatten. Klik in Projectverkenner met de rechtermuisknop op het projectknooppunt en selecteer **Nieuw > klasse**.
2. In **nieuwe Java-klasse**, naam van de klasse `WebCreator` en controleer de **openbare statische void main** selectievakje. De selecties ziet er als volgt:
   
    ![][2]
3. Klik op **Voltooien**. Het bestand WebCreator.java weergegeven in Projectverkenner.

### <a name="calling-the-azure-api-to-create-an-app-service-web-app"></a>Aanroepen van de Azure-API voor het maken van een App Service-Web-App
#### <a name="add-necessary-imports"></a>Vereiste imports toevoegen
In WebCreator.java, voegt u de volgende import; deze invoer bieden toegang tot de klassen in de management-bibliotheken voor het verbruik van Azure-API's:

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


#### <a name="define-the-main-entry-point-class"></a>De klasse van de belangrijkste vermelding point definiëren
De hoofdklasse omdat het doel van de toepassing AzureWebDemo is voor het maken van een App Service-Web-App, een naam voor deze toepassing `WebAppCreator`. Deze klasse biedt de belangrijkste vermelding punt code die de Azure Service Management API voor het maken van de web-app aanroept.

De volgende parameterdefinities voor de web-app en webruimte toevoegen. U moet uw eigen Azure-abonnement-ID en certificaat-informatie opgeven.

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

* `<subscription-id>`is de Azure-abonnement-ID in die u wilt maken van de resource.
* `<certificate-store-path>`is het pad en bestandsnaam in het bestand JKS in uw directory van de winkel lokale certificaatarchief. Bijvoorbeeld: `C:/Certificates/CertificateName.jks` voor Linux en `C:\Certificates\CertificateName.jks` voor Windows.
* `<certificate-password>`is het wachtwoord die u hebt opgegeven toen u uw certificaat JKS hebt gemaakt.
* `webAppName`de naam die u kiezen; deze procedure gebruikt u de naam van de `WebDemoWebApp`. De volledige domeinnaam is de `webAppName` met de `domainName` toegevoegd, dus in dit geval het volledige domein is `webdemowebapp.azurewebsites.net`.
* `domainName`moet worden opgegeven, zoals hierboven.
* `webSpaceName`moet een van de waarden die zijn gedefinieerd in de [WebSpaceNames] [ WebSpaceNames] klasse.
* `appServicePlanName`moet worden opgegeven, zoals hierboven.

> **Opmerking:** elke keer dat u deze toepassing uitvoeren, moet u de waarde van wijzigen `webAppName` en `appServicePlanName` (of verwijderen van de web-app in de Azure Portal) voordat u de toepassing opnieuw uitvoert. Anders mislukt uitvoering omdat de dezelfde resource al in Azure bestaat.
> 
> 

#### <a name="define-the-web-creation-method"></a>De methode voor het maken van web definiëren
Definieer vervolgens een methode voor het maken van de web-app. Deze methode `createWebApp`, geeft de parameters van de web-app en de webruimte. Daarnaast maakt en configureert u de App Service Web Apps management-client, die wordt gedefinieerd door de [WebSiteManagementClient] [ WebSiteManagementClient] object. De management-client is de sleutel voor het maken van Web-Apps. Het biedt de RESTful-web-services waarmee toepassingen voor het beheren van web-apps (het uitvoeren van bewerkingen zoals maken, bijwerken en verwijderen) door het aanroepen van de servicebeheer-API.

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

De code de HTTP-status van de reactie waarmee wordt aangegeven of geslaagd of mislukt wordt uitgevoerd en als dit lukt, wordt de naam van de gemaakte web-app uitvoeren.

#### <a name="define-the-main-method"></a>De methode main() definiëren
Geef de code van main() methode waarmee createWebApp() voor het maken van de web-app wordt aangeroepen.

Tenslotte roept `createWebApp` van `main`:

        public static void main(String[] args)
            throws IOException, URISyntaxException, ServiceException,
            ParserConfigurationException, SAXException, Exception {

            // Create web app
            createWebApp();

        }  // end of main()

    }  // end of WebAppCreator class


#### <a name="run-the-application-and-verify-web-app-creation"></a>Voer de toepassing en controleer of de web-apps maken
Om te controleren of uw toepassing wordt uitgevoerd, klikt u op **uitvoeren > Voer**. Wanneer de toepassing is voltooid wordt uitgevoerd, ziet u de volgende uitvoer in de Eclipse-console:

    ----------
    Web app created - HTTP response 200

    ----------

    Name of web app created: WebDemoWebApp

    ----------

Meld u aan bij de klassieke Azure portal en klikt u op **Web-Apps**. De nieuwe web-app moet worden weergegeven in de lijst met Web-Apps binnen een paar minuten.

## <a name="deploying-an-application-to-the-web-app"></a>Een toepassing implementeren in de Web-App
Nadat u AzureWebDemo hebt uitgevoerd en klik op de nieuwe web-app, meld u aan bij de klassieke portal gemaakt **Web-Apps**, en selecteer **WebDemoWebApp** in de **Web-Apps** lijst. Klik in de web-app dashboardpagina op **Bladeren** (of klik op de URL `webdemowebapp.azurewebsites.net`) om hiernaar te navigeren. U ziet een lege tijdelijke aanduiding-pagina, omdat het geen inhoud is gepubliceerd naar de web-app nog.

U wordt vervolgens een 'Hallo wereld'-toepassing maken en implementeren op de web-app.

### <a name="create-a-jsp-hello-world-application"></a>Een JSP Hallo wereld-toepassing maken
#### <a name="create-the-application"></a>De toepassing maken
Als u wilt laten zien hoe een toepassing implementeert op het web, ziet de volgende procedure u hoe een eenvoudige 'Hallo wereld' Java-toepassing maken en uploaden naar de App Service Web-App die uw toepassing gemaakt.

1. Klik op **bestand > Nieuw > Dynamic webproject**. Noem deze `JSPHello`. U hoeft niet te wijzigen van de andere instellingen in dit dialoogvenster. Klik op **Voltooien**.
   
    ![][3]
2. Vouw in Projectverkenner de **JSPHello** project, met de rechtermuisknop op **WebContent**, klikt u vervolgens op **Nieuw > JSP-bestand**. In het dialoogvenster Nieuw JSP-bestand een naam op het nieuwe bestand `index.jsp`. Klik op **Volgende**.
3. In de **JSP-sjabloon selecteren** dialoogvenster **nieuw JSP-bestand (html)** en klik op **voltooien**.
4. In index.jsp, voeg de volgende code in de `<head>` en `<body>` tag secties:
   
        <head>
          ...
          java.util.Date date = new java.util.Date();
        </head>
   
        <body>
          Hello, the time is <%= date %> 
        </body>

#### <a name="run-the-hello-world-application-in-localhost"></a>Uitvoeren van de toepassing Hello World in localhost
Voordat u deze toepassing uitvoert, moet u enkele eigenschappen configureren.

1. Met de rechtermuisknop op de **JSPHello** project en selecteer **eigenschappen**.
2. In de **eigenschappen** dialoogvenster: Selecteer **Javabuild-pad**, selecteer de **rangschikken en exporteren** tabblad controle **JRE systeembibliotheek**, klikt u vervolgens op **Up** te verplaatsen naar de bovenkant van de lijst.
   
    ![][4]
3. Ook in de **eigenschappen** dialoogvenster: Selecteer **Runtimes gericht** en klik op **nieuw**.
4. In de **nieuwe Server Runtime-omgeving** dialoogvenster, selecteert u een server, zoals **Apache Tomcat v7.0** en klik op **volgende**. In de **Tomcat-Server** dialoogvenster, set **naam** naar `Apache Tomcat v7.0`, en stel **Tomcat-installatiedirectory** naar de map waarin u de versie van Tomcat-server die u wilt gebruiken, hebt geïnstalleerd.
   
    ![][5]
   
    Klik op **Voltooien**.
5. U keer vervolgens terug naar de **Runtimes gericht** pagina van de **eigenschappen** dialoogvenster. Selecteer **Apache Tomcat v7.0**, klikt u vervolgens op **OK**.
   
    ![][6]
6. In de Eclipse **uitvoeren** menu, klikt u op **uitvoeren**. In de **uitvoeren als** dialoogvenster Selecteer **uitgevoerd op Server**. In de **uitgevoerd op Server** dialoogvenster Selecteer **Tomcat v7.0 Server**:
   
    ![][7]
   
    Klik op **Voltooien**.
7. Wanneer de toepassing wordt uitgevoerd, ziet u de **JSPHello** pagina wordt weergegeven in een venster localhost in Eclipse (`http://localhost:8080/JSPHello/`), het volgende bericht wordt weergegeven:
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="export-the-application-as-a-war"></a>De toepassing als een WAR exporteren
De web-projectbestanden exporteren als een web-archiefbestand (WAR) zodat u deze op de web-app implementeren kunt. De volgende web project-bestanden bevinden zich in de map WebContent:

    META-INF
    WEB-INF
    index.jsp

1. Met de rechtermuisknop op de map WebContent en selecteer **exporteren**.
2. In de **exporteren Selecteer** dialoogvenster, klikt u op **Web > WAR** bestand en klik vervolgens op **volgende**.
3. In de **WAR exporteren** dialoogvenster, selecteer de src-map in het huidige project en de naam van het WAR-bestand aan het einde bevatten. Bijvoorbeeld:
   
    `<project-path>/JSPHello/src/JSPHello.war`

Zie voor meer informatie over het implementeren van WAR bestanden [toevoegen van een Java-toepassing naar Azure App Service Web Apps](web-sites-java-add-app.md).

### <a name="deploying-the-hello-world-application-using-ftp"></a>De Hallo wereld-toepassing met FTP implementeert
Selecteer een FTP-client van derden voor het publiceren van de toepassing. Deze procedure wordt beschreven twee opties: de Kudu-console die is ingebouwd in Azure. en FileZilla, een populaire hulpmiddel met een handige, grafische gebruikersinterface.

> **Opmerking:** de Azure-werkset voor Eclipse ondersteunt de implementatie naar storage-accounts en cloud services, maar ondersteunt geen implementatie voor web-apps. U kunt implementeren voor storage-accounts en cloud services met behulp van een Azure-implementatieproject, zoals beschreven in [maken van een Hallo wereld-toepassing voor Azure in Eclipse](http://msdn.microsoft.com/library/azure/hh690944.aspx), maar niet naar de web-apps. Andere methoden zoals FTP- of GitHub bestanden overbrengen naar uw web-app gebruiken.
> 
> **Opmerking:** niet raadzaam met FTP vanaf de opdrachtprompt van Windows (het FTP.EXE opdrachtregelprogramma dat wordt geleverd bij Windows). FTP-clients die gebruikmaken van actieve FTP, zoals FTP.EXE, niet vaak werken via firewalls. Actieve FTP geeft een interne, op basis van LAN adres waarnaar een FTP-server waarschijnlijk geen verbinding maken.
> 
> 

Zie de volgende onderwerpen voor meer informatie over de implementatie van een App Service-web-app met FTP:

* [Implementeren met behulp van een FTP-programma](web-sites-deploy.md)

#### <a name="set-up-deployment-credentials"></a>Implementatiereferenties instellen
Zorg ervoor dat u hebt uitgevoerd, de **AzureWebDemo** toepassing maken van een web-app. U kunt bestanden worden overgebracht naar deze locatie.

1. Meld u aan bij de klassieke portal en klikt u op **Web-Apps**. Zorg ervoor dat **WebDemoWebApp** wordt weergegeven in de lijst met web-apps en zorg ervoor dat deze wordt uitgevoerd. Klik op **WebDemoWebApp** openen de **Dashboard** pagina.
2. Op de **Dashboard** pagina onder **snel in één oogopslag**, klikt u op **instellen van referenties voor uw implementatie** (als u de referenties voor implementatie al hebt, leest dit **opnieuw instellen van referenties voor uw implementatie**).
   
    Referenties voor implementatie zijn gekoppeld aan een Microsoft-account. U moet een gebruikersnaam en wachtwoord waarmee u kunt implementeren met behulp van Git en FTP opgeven. U kunt deze referenties gebruiken om te implementeren voor een web-app in alle Azure-abonnementen die zijn gekoppeld aan je Microsoft-account. Geef referenties op Git en FTP-implementatie in het dialoogvenster en noteert u de gebruikersnaam en het wachtwoord voor toekomstig gebruik.

#### <a name="get-ftp-connection-information"></a>Gegevens van de FTP-verbinding ophalen
Gebruik van FTP toepassingsbestanden naar de nieuwe web-app implementeren, moet u de verbindingsgegevens verkrijgen. Er zijn twee manieren verkrijgen verbindingsgegevens. Te gaat u naar de web-app **Dashboard** pagina; de andere manier is om te downloaden van het web van app publicatieprofiel. Het publicatieprofiel is een XML-bestand informatie zoals de FTP-host en het aanmeldingsaccount referenties voor uw web-apps in Azure App Service bevat. U kunt deze gebruikersnaam en wachtwoord gebruiken om te implementeren voor een web-app in alle abonnementen die zijn gekoppeld aan het Azure-account, niet alleen dit exemplaar.

FTP-verbinding om informatie te verkrijgen uit de blade web-app in de [Azure Portal][Azure Portal]:

1. Onder **Essentials**, vindt en kopieert de **FTP-hostnaam**. Dit is een URI die vergelijkbaar is met `ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net`.
2. Onder **Essentials**, vindt en kopieert **FTP-/ Implementatiegebruiker gebruikersnaam**. Dit heeft de vorm *webappname\deployment-username*; bijvoorbeeld `WebDemoWebApp\deployer77`.

FTP-verbinding om informatie te verkrijgen uit het publicatieprofiel:

1. Klik op de web-app blade **Get publicatieprofiel**. Hiermee wordt een .publishsettings-bestand downloaden naar uw lokale schijf.
2. Open het .publishsettings-bestand in een XML-editor of een teksteditor en zoek de `<publishProfile>` element die `publishMethod="FTP"`. Het moet eruitzien als in het volgende:
   
        <publishProfile
            profileName="WebDemoWebApp - FTP"
            publishMethod="FTP"
            publishUrl="ftp://waws-prod-bay-NNN.ftp.azurewebsites.windows.net/site/wwwroot"
            ftpPassiveMode="True"
            userName="WebDemoWebApp\$WebDemoWebApp"
            userPWD="<deployment-password>"
            ...
        </publishProfile>
3. Houd er rekening mee dat de web-app `publishProfile` instellingen zijn toegewezen aan de instellingen FileZilla sitebeheerder als volgt:

* `publishUrl`is hetzelfde als **FTP-hostnaam**, de waarde die u instelt in **Host**.
* `publishMethod="FTP"`betekent dat u instelt **Protocol** naar **FTP - File Transfer Protocol**, en **versleuteling** naar **gewone FTP gebruiken**.
* `userName`en `userPWD` zijn de sleutels voor de werkelijke gebruikersnaam en wachtwoord waarden die u hebt opgegeven dat wanneer u de referenties voor de implementatie opnieuw. `userName`is hetzelfde als **implementatie / FTP-gebruiker**. Deze worden toegewezen aan **gebruiker** en **wachtwoord** in FileZilla.
* `ftpPassiveMode="True"`betekent dat de FTP-site maakt gebruik van Passief FTP-overdracht; Selecteer **passieve** op de **Overdrachtinstellingen** tabblad.

#### <a name="configure-the-web-app-to-host-a-java-application"></a>De Web-App voor het hosten van een Java-toepassing configureren
Voordat u de toepassing publiceert, moet u enkele configuratie-instellingen wijzigen zodat de web-app kan een Java-toepassing hosten.

1. In de klassieke portal, gaat u naar de web-app **Dashboard** pagina en klik op **configureren**. Op de **configureren** pagina, geeft u de volgende instellingen.
2. In **Java-versie** de standaardwaarde is **uit**; de Java-versie selecteren die uw toepassing doelen; bijvoorbeeld 1.7.0_51. Nadat u dit doet, zorg er ook die **webcontainer** is ingesteld op een versie van Tomcat-Server.
3. In **standaarddocumenten**, index.jsp toevoegen en verplaatsen naar het begin van de lijst. (Het standaardbestand voor web-apps is hostingstart.html.)
4. Klik op **Opslaan**.

#### <a name="publish-your-application-using-kudu"></a>Uw toepassing publiceren via Kudu
Er is een manier om de toepassing publiceren met de Kudu debug-console die is ingebouwd in Azure. Kudu bekend is dat deze stabiel en consistent zijn met App Service Web Apps en Tomcat-Server. U kunt de console voor de web-app openen door te bladeren naar een URL van de volgende notatie:

`https://<webappname>.scm.azurewebsites.net/DebugConsole`

1. Voor deze procedure bevindt de Kudu-console zich in de volgende URL; Blader naar deze locatie:
   
    `https://webdemowebapp.scm.azurewebsites.net/DebugConsole`
2. Selecteer in het bovenste menu **Console fouten opsporen > CMD**.
3. In de console vanaf de opdrachtregel, gaat u naar `/site/wwwroot` (of klik op `site`, klikt u vervolgens `wwwroot` in de directoryweergave aan de bovenkant van de pagina):
   
    `cd /site/wwwroot`
4. Nadat u hebt opgegeven **Java-versie**, Tomcat-server moet een map webapps maken. Navigeer naar de map WebApps op de opdrachtregel van de console:
   
    `mkdir webapps`
   
    `cd webapps`
5. Sleep JSPHello.war van `<project-path>/JSPHello/src/` en zet het neer in de weergave van de directory Kudu onder `/site/wwwroot/webapps`. Sleep niet het aan het gebied 'Hier naartoe slepen om te uploaden en zip-', omdat Tomcat wordt behouden.
   
   ![][8]

Op de eerste JSPHello.war wordt weergegeven in het gebied van directory zelfstandig:

  ![][9]

Tomcat-Server wordt het WAR-bestand uitpakken naar een map met uitgepakte JSPHello in korte tijd (waarschijnlijk minder dan 5 minuten). Klik op de hoofdmap of index.jsp is uitgepakt en er wordt gekopieerd. Zo ja, ga dan terug naar de map WebApps om te zien of de uitgepakte JSPHello-map is gemaakt. Als u deze items niet ziet, wacht en herhaalt.

  ![][10]

#### <a name="publish-your-application-using-filezilla-optional"></a>Uw toepassing publiceren via FileZilla (optioneel)
Een ander hulpprogramma die kunt u de toepassing publiceren is FileZilla, een populaire van derden FTP-client met een handige, grafische gebruikersinterface. U kunt downloaden en installeren van FileZilla van [http://filezilla-project.org/](http://filezilla-project.org/) als u nog geen deze. Zie voor meer informatie over het gebruik van de client de [FileZilla documentatie](https://wiki.filezilla-project.org/Documentation) en dit blogbericht op [FTP-Clients - deel 4: FileZilla](http://blogs.msdn.com/b/robert_mcmurray/archive/2008/12/17/ftp-clients-part-4-filezilla.aspx).

1. Klik in de FileZilla, **bestand > sitebeheerder**.
2. In de **sitebeheerder** dialoogvenster, klikt u op **nieuwe Site**. Een nieuwe lege FTP-site wordt weergegeven in **Selecteer vermelding** waarin u een naam te geven. Naam voor deze procedure `AzureWebDemo-FTP`.
   
    Op de **algemene** tabblad, geeft u de volgende instellingen:
   
   * **Host:** Enter de **FTP-hostnaam** die u hebt gekopieerd vanuit het dashboard.
   * **Poort:** (dit leeg laat, als dit een passief-overdracht is en de poort wordt bepaald door de server.)
   * **Protocol:** FTP File Transfer Protocol
   * **Versleuteling:** gewone FTP gebruiken
   * **Aanmeldingstype:** normaal
   * **Gebruiker:** invoeren van de implementatie / FTP-gebruiker die u hebt gekopieerd vanuit het dashboard. Dit is de volledige gebruikersnaam van het FTP-, die het formulier heeft *webappname\username*.
   * **Wachtwoord:** Voer het wachtwoord die u hebt opgegeven als u instelt dat de referenties voor implementatie.
     
     Op de **Overdrachtinstellingen** tabblad **passieve**.
3. Klik op **Verbinden**. Als geslaagd, FileZilla van console wordt weergegeven een `Status: Connected` bericht en probleem een `LIST` opdracht om een lijst van de mapinhoud.
4. In de **lokale** deelvenster site, selecteer de bron directory waarin het bestand JSPHello.war zich bevindt; het pad moet de volgende strekking:
   
    `<project-path>/JSPHello/src/`
5. In de **externe** deelvenster site, selecteer de doelmap. Implementeert u het WAR-bestand naar de `webapps` map onder de hoofdmap van de web-app. Navigeer naar `/site/wwwroot`, met de rechtermuisknop op `wwwroot`, en selecteer **maken directory**. Naam van de map `webapps` en voert u deze map.
6. Transfer JSPHello.war naar `/site/wwwroot/webapps`. Selecteer JSPHello.war in de **lokale** lijst bestand, met de rechtermuisknop op het en selecteert u **uploaden**. U ziet het weergegeven in `/site/wwwroot/webapps`.
7. Nadat u JSPHello.war gekopieerd naar de map WebApps, Tomcat-Server automatisch wordt uitgepakt (uitpakken van) de bestanden in het WAR-bestand. Hoewel Tomcat-Server bijna onmiddellijk uitpakken begint, kan het lang duren voordat tijd (mogelijk uren) voor de bestanden in de FTP-client wordt weergegeven.

#### <a name="run-the-hello-world-application-on-the-web-app"></a>De toepassing Hello World uitvoeren op de Web-App
1. Nadat u hebt het WAR-bestand wordt geüpload en geverifieerd dat Tomcat-server is gemaakt met een uitgepakte `JSPHello` directory, blader naar `http://webdemowebapp.azurewebsites.net/JSPHello` de toepassing uit te voeren.
   
   > **Opmerking:** als u op **Bladeren** vanuit de klassieke portal krijgt u mogelijk de standaard-webpagina weergegeven met de tekst "dit op basis van Java-webtoepassing is gemaakt." Mogelijk moet de webpagina vernieuwen om de uitvoer van de toepassing in plaats van de webpagina die standaard weergeven.
   > 
   > 
2. Wanneer de toepassing wordt uitgevoerd, ziet u een webpagina met de volgende uitvoer:
   
    `Hello World, the time is Tue Mar 24 23:21:10 GMT 2015`

#### <a name="clean-up-azure-resources"></a>Azure-resources opschonen
Deze procedure maakt u een App Service-web-app. U wordt gefactureerd voor de resource als deze bestaat. Tenzij u van plan bent om door te gaan met de web-app voor testdoeleinden of ontwikkeling, moet u stoppen of te verwijderen. Een web-app is gestopt, nog steeds een kleine vergoeding worden, maar u kunt deze opnieuw starten op elk gewenst moment. Als u een web-app verwijdert, worden alle gegevens die u hebt geüpload naar het gewist.

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
