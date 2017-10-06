---
title: een aangepaste Java-web-app tooAzure aaaUpload
description: Deze zelfstudie leert u hoe tooupload een aangepaste Java web-app tooAzure App Service Web Apps.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a>Een aangepaste Java-web-app tooAzure uploaden
Dit onderwerp wordt uitgelegd hoe tooupload een aangepaste Java web-app te[Azure App Service] Web-Apps. Bevat informatie die van toepassing tooany Java-website of web-app en ook enkele voorbeelden voor specifieke toepassingen is.

Houd er rekening mee dat Azure een manier biedt voor het maken van Java web-apps met behulp van de gebruikersinterface voor configuratie hello Azure Portal en Azure Marketplace Hallo zoals beschreven op [een Java-web-app maken in Azure App Service](web-sites-java-get-started.md). Deze zelfstudie is bedoeld voor scenario's waarin u niet wilt dat toouse hello Azure Portal de gebruikersinterface voor configuratie of hello Azure Marketplace.  

## <a name="configuration-guidelines"></a>Configuratie-instructies
Hallo volgende beschrijft Hallo-instellingen voor aangepaste Java-web-apps in Azure wordt verwacht.

* Hallo HTTP-poort die wordt gebruikt door Hallo proces Java dynamisch toegewezen.  Hallo-proces moet Hallo-poort van de omgevingsvariabele hello gebruiken `HTTP_PLATFORM_PORT`.
* Alle luisteren poorten andere dan Hallo één HTTP-listener moet worden uitgeschakeld.  In Tomcat, die Hallo afsluiten, HTTPS en AJP bevat poorten.
* Hallo-container moet toobe geconfigureerd voor IPv4-verkeer.
* Hallo **opstarten** opdracht voor het Hallo-toepassing moet toobe in Hallo configuratie instellen.
* Toepassingen waarvoor de mappen met schrijftoegang nodig toobe zich in de inhoud map hello Azure-WebApp, dat zich **D:\home**.  Hallo-omgevingsvariabele `HOME` tooD:\home verwijst.  

Omgevingsvariabelen kunt zo nodig u instellen in Hallo web.config-bestand.

## <a name="webconfig-httpplatform-configuration"></a>Web.config httpPlatform configuratie
Hallo volgende informatie beschrijft Hallo **httpPlatform** indeling in web.config.

**argumenten** (standaard = ""). Argumenten toohello uitvoerbaar bestand of script dat is opgegeven in Hallo **processPath** instelling.

Voorbeelden (weergegeven met **processPath** opgenomen):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -pad toohello uitvoerbaar bestand of script dat een proces luistert naar HTTP-aanvragen wordt gestart.

Voorbeelden:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (standaard = 10.) Aantal keren opgegeven in Hallo-proces **processPath** toocrash per minuut is toegestaan. Als deze limiet wordt overschreden, **HttpPlatformHandler** start een proces voor de rest Hallo Hallo minuut hello wordt gestopt.

**requestTimeout** (standaard = "00: 02:00 '.) Duur waarvoor **HttpPlatformHandler** wordt gewacht op een reactie van Hallo proces luistert op `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (standaard = 10.) Aantal keren **HttpPlatformHandler** probeert toolaunch Hallo proces is opgegeven in **processPath**. Zie **startupTimeLimit** voor meer informatie.

**startupTimeLimit** (standaard = 10 seconden.) Duur waarvoor **HttpPlatformHandler** wordt gewacht op Hallo executable/script toostart een proces op Hallo-poort luistert.  Als deze tijd limiet wordt overschreden, **HttpPlatformHandler** wordt Hallo proces beëindigen en toolaunch probeer deze opnieuw **startupRetryCount** tijden.

**stdoutLogEnabled** (standaard = "true".) Indien waar, **stdout** en **stderr** voor Hallo proces opgegeven in Hallo **processPath** instelling worden omgeleid toohello dat is opgegeven in  **stdoutLogFile** (Zie **stdoutLogFile** sectie).

**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log'.) Absoluut bestandspad waarvoor **stdout** en **stderr** uit Hallo-proces is opgegeven in **processPath** worden geregistreerd.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`is een speciale tijdelijke aanduiding die moet toospecified bij **argumenten** of als onderdeel van Hallo **httpPlatform** **omgevingsvariabelen** lijst. Dit wordt vervangen door een intern gegenereerde poort door **HttpPlatformHandler** zodat Hallo proces opgegeven door **processPath** kunt luisteren op deze poort.
> 
> 

## <a name="deployment"></a>Implementatie
Op basis van Java-web-apps kunnen eenvoudig worden geïmplementeerd via Hallo dezelfde betekent dat de meeste die worden gebruikt met Hallo Internet Information Services (IIS) op basis van webtoepassingen.  FTP, Git en Kudu worden alle ondersteund als mechanismen voor implementatie, zoals is Hallo geïntegreerde SCM-functionaliteit voor web-apps. Web Deploy werkt als een protocol, zoals Java niet is ontwikkeld in Visual Studio, Web Deploy komt niet overeen met gebruiksvoorbeelden voor Java web-app-implementatie.

## <a name="application-configuration-examples"></a>Toepassingsconfiguratie voorbeelden
Hallo toepassingen, een web.config-bestand en het Hallo na de configuratie van toepassing is opgegeven voor als voorbeelden tooshow hoe tooenable uw Java-toepassing op App Service Web Apps.

### <a name="tomcat"></a>Tomcat
Er zijn twee variaties op Tomcat die worden geleverd met App Service Web Apps, is maar nog steeds behoorlijk mogelijke tooupload klant specifieke exemplaren. Hieronder volgt een voorbeeld van een installatie van Tomcat met een andere Java Virtual Machine (JVM).

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

Op Hallo Tomcat aan clientzijde zijn er enkele configuratiewijzigingen die toobe aangebracht moeten. Hallo server.xml moet tooset toobe bewerkt:

* Afsluiten, poort = -1
* HTTP-connector poort = ${port.http}
* HTTP-connector adres = "127.0.0.1"
* HTTPS- en AJP connectors uitcommentariëren
* Hallo IPv4-instelling kan ook worden ingesteld in Hallo catalina.properties bestand waarin u kunt toevoegen`java.net.preferIPv4Stack=true`

Direct3d aanroepen worden niet ondersteund op App Service Web Apps. toodisable, Hallo volgende Java-optie moet u uw toepassing dergelijke aanroepen toevoegen:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Zoals Hallo geval voor Tomcat, kunnen klanten hun eigen exemplaren voor Jetty uploaden. In geval van actieve Hallo volledige installatie van Jetty Hallo eruit Hallo configuratie als volgt:

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

Hallo Jetty-configuratie moet toobe gewijzigd in Hallo start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
In volgorde tooget een Springboot toepassing waarop uitgevoerd. u moet tooupload uw JAR of WAR-bestand en voeg Hallo web.config-bestand te volgen. Hallo web.config-bestand is verplaatst naar de map wwwroot Hallo. Pas in web.config Hallo Hallo argumenten toopoint tooyour JAR-bestand, in Hallo na voorbeeld Hallo JAR-bestand bevindt zich in Hallo wwwroot-map ook.  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a>Hudson
Onze test die wordt gebruikt Hudson 3.1.2 war Hallo en Tomcat 7.0.50 standaardexemplaar Hallo maar zonder te Hallo UI tooset dingen gebruiken.  Omdat Hudson een hulpprogramma voor het bouwen van software is, is het aanbevolen tooinstall op specifieke exemplaren waar hello **AlwaysOn** vlag kan worden ingesteld op Hallo web-app.

1. In uw web-app de hoofdmap, dat wil zeggen, **d:\home\site\wwwroot**, maak een **webapps** directory (indien niet aanwezig), en plaats Hudson.war in **d:\home\site\wwwroot\webapps**.
2. Apache maven 3.0.5 (compatibel met Hudson) downloaden en plaats deze in **d:\home\site\wwwroot**.
3. Maken van web.config in **d:\home\site\wwwroot** en plakken Hallo inhoud in het volgende:
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    Hallo-web-app kan op dit moment opnieuw gestart tootake Hallo wijzigingen zijn.  Verbinding maken met toohttp://yourwebapp/hudson toostart Hudson.
4. Nadat Hudson zichzelf configureert, ziet u Hallo scherm te volgen:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Toegang Hallo Hudson configuratiepagina: klik op **beheren Hudson**, en klik vervolgens op **System configureren**.
6. Configureer Hallo JDK zoals hieronder wordt weergegeven:
   
    ![Hudson configuratie](./media/web-sites-java-custom-upload/hudson2.png)
7. Maven configureren zoals hieronder wordt weergegeven:
   
    ![Maven-configuratie](./media/web-sites-java-custom-upload/maven.png)
8. Hallo-instellingen opslaan. Hudson worden nu geconfigureerd en klaar voor gebruik.

Zie voor meer informatie over Hudson [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay wordt ondersteund op App Service Web Apps. Omdat het Liferay kan aanzienlijke geheugen vereist, moet Hallo web-app toorun op een grote of middelgrote toegewezen werknemer, die voldoende geheugen kan bieden. Liferay neemt ook toostart van enkele minuten in beslag. Daarom wordt aanbevolen dat u de web-app hello te ingesteld**altijd op**.  

Voor informatie over het gebruik van Liferay 6.1.2 die community Edition GA3 gebundeld met Tomcat zijn hello volgende bestanden bewerkt na het downloaden van Liferay:

**Server.XML**

* Wijzig afsluiten poort te-1.
* HTTP-connector te wijzigen`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Hallo AJP connector uitcommentariëren.

In Hallo **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** map, maakt u een bestand met de naam **portal ext.properties**. Dit bestand moet toocontain één regel, zoals hier wordt weergegeven:

    liferay.home=%HOME%/site/wwwroot/liferay

Op Hallo maken dezelfde mapniveau Hallo tomcat 7.0.40 map als een bestand met de naam **web.config** Hello volgende inhoud:

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

Onder Hallo **httpPlatform** blokkeert, hello **requestTimeout** te is ingesteld ' 00: 10:00 '.  Kan worden verkleind, maar u hebt waarschijnlijk toosee sommige time-outfouten tijdens het uitvoeren van de Liferay is bootstrap.  Als deze waarde is gewijzigd, Hallo **connectionTimeout** in Hallo tomcat server.xml moet ook worden gewijzigd.  

Hierbij moet worden opgemerkt dat varariable hello JRE_HOME omgeving is opgegeven in Hallo hierboven web.config toopoint toohello JDK 64-bits. Hallo standaard 32-bits, maar omdat Liferay kan een hoge mate van geheugen is vereist, is het aanbevolen toouse Hallo 64-bits JDK.

Zodra u deze wijzigingen aanbrengt, opnieuw opstarten van uw web-app uitgevoerd Liferay, open vervolgens http://yourwebapp. Hallo Liferay portal is beschikbaar via Hallo web-app-hoofdmap. 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Liferay [http://www.liferay.com](http://www.liferay.com).

Voor meer informatie over Java, gaat u naar [Azure voor Java-ontwikkelaars](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
