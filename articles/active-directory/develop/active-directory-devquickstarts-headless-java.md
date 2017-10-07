---
title: aaaAzure AD Java-opdrachtregel die aan de slag | Microsoft Docs
description: Hoe toobuild een Java command line Application die gebruikers in een API tooaccess ondertekent.
services: active-directory
documentationcenter: java
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 51e1a8f9-6ff0-4643-a350-0ba794e26fd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 01/23/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 9ba1d1e794928a39ca1f091bd0e6eba57ce3d6aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a>Met behulp van Java-opdrachtregel-App tooAccess een API met Azure AD
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

Azure AD maakt het eenvoudig en snel toooutsource identiteitsbeheer van uw web-app, biedt eenmalige aanmelden en afmelden met slechts een paar regels code.  In Java-web-apps, kunt u dit doen met behulp van Microsoft implementatie van Hallo community aangestuurde ADAL4J.

  We gebruiken hier ADAL4J naar:

* Meld u Hallo gebruiker in met behulp van Azure AD als id-provider Hallo Hallo-app.
* Sommige informatie over Hallo gebruiker weergegeven.
* Meld u Hallo gebruiker buiten het Hallo-app.

Toodo dit order, moet u in:

1. Een toepassing registreren met Azure AD
2. Instellen van uw app toouse hello ADAL4J-bibliotheek.
3. Hallo ADAL4J bibliotheek tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken.
4. Gegevens over Hallo gebruiker afdrukken.

tooget gestart, [Hallo app basisproject downloaden](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).  Ook moet u een Azure AD-tenant in welke tooregister uw toepassing.  Als u niet hebt, [meer informatie over hoe tooget een](active-directory-howto-tenant.md).

## <a name="1--register-an-application-with-azure-ad"></a>1.  Een toepassing registreren met Azure AD
tooenable uw app tooauthenticate gebruikers, moet u eerst een nieuwe toepassing tooregister in uw tenant.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.
3. Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.
4. Klik op **App registraties** en kies **toevoegen**.
5. Volg de aanwijzingen Hallo en maak een nieuwe **webtoepassing en/of WebAPI**.
  * Hallo **naam** Hallo bevat toepassing een beschrijving van uw toepassing tooend-gebruikers
  * Hallo **aanmeldings-URL** Hallo basis-URL van uw app is.  Hallo basisproject de standaardwaarde is `http://localhost:8080/adal4jsample/`.
6. Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id  U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.
7. Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken. Hallo **App ID URI** is de unieke id voor uw toepassing.  Hallo-conventie is toouse `https://<tenant-domain>/<app-name>`, bijvoorbeeld `http://localhost:8080/adal4jsample/`.

Eenmaal in Hallo-portal voor uw app maakt een **sleutel** van Hallo **instellingen** pagina voor uw toepassing en kopieer het naar beneden.  U hebt dit zo direct nodig.

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a>2. Uw app toouse ADAL4J-bibliotheek en de vereisten met behulp van Maven instellen
Hier geconfigureerd ADAL4J toouse hello OpenID Connect-verificatieprotocol.  ADAL4J gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.

* In de hoofdmap van uw project Hallo openen/maken `pom.xml` en zoek Hallo `// TODO: provide dependencies for Maven` en vervang door Hallo volgende:

```Java
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>public-client-adal4j-sample</artifactId>
    <packaging>jar</packaging>
    <version>0.0.1-SNAPSHOT</version>
    <name>public-client-adal4j-sample</name>
    <url>http://maven.apache.org</url>
    <properties>
        <spring.version>3.0.5.RELEASE</spring.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>adal4j</artifactId>
            <version>1.1.2</version>
        </dependency>
        <dependency>
            <groupId>com.nimbusds</groupId>
            <artifactId>oauth2-oidc-sdk</artifactId>
            <version>4.5</version>
        </dependency>
        <dependency>
            <groupId>org.json</groupId>
            <artifactId>json</artifactId>
            <version>20090211</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.0.1</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.5</version>
        </dependency>
</dependencies>
    <build>
        <finalName>public-client-adal4j-sample</finalName>
        <plugins>
                <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <version>1.2.1</version>
            <configuration>
                <mainClass>PublicClient</mainClass>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>1.7</source>
                    <target>1.7</target>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-dependency-plugin</artifactId>
                <executions>
                    <execution>
                        <id>install</id>
                        <phase>install</phase>
                        <goals>
                            <goal>sources</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-resources-plugin</artifactId>
                <version>2.5</version>
                <configuration>
                    <encoding>UTF-8</encoding>
                </configuration>
            </plugin>
            <plugin>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
          </execution>
        </executions>
        <configuration>
          <descriptorRefs>
            <descriptorRef>jar-with-dependencies</descriptorRef>
          </descriptorRefs>
        </configuration>
      </plugin>
      <plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-assembly-plugin</artifactId>
  <configuration>
    <archive>
      <manifest>
        <mainClass>PublicClient</mainClass>
      </manifest>
    </archive>
  </configuration>
</plugin>
        </plugins>
    </build>

</project>


```



## <a name="3-create-hello-java-publicclient-file"></a>3. Hallo Java PublicClient bestand maken
Zoals hierboven vermeld, zullen we gebruikmaken van Hallo Graph API tooget gegevens over Hallo aangemelde gebruiker. Voor deze gemakkelijk voor ons toobe moet maken we beide een bestand toorepresent een **mapobject** en een afzonderlijk bestand toorepresent hello **gebruiker** zodat hello OO patroon van Java kan worden gebruikt.

* Maken van een bestand met de naam `DirectoryObject.java` die we toostore basisgegevens over eventuele DirectoryObject (kunt u erop gratis toouse dit later voor andere grafiek query's kunt u doen) worden gebruikt. U kunt knippen en plakken dit uit het volgende:

```Java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;

import javax.naming.ServiceUnavailableException;

import com.microsoft.aad.adal4j.AuthenticationContext;
import com.microsoft.aad.adal4j.AuthenticationResult;

public class PublicClient {

    private final static String AUTHORITY = "https://login.microsoftonline.com/common/";
    private final static String CLIENT_ID = "2a4da06c-ff07-410d-af8a-542a512f5092";

    public static void main(String args[]) throws Exception {

        try (BufferedReader br = new BufferedReader(new InputStreamReader(
                System.in))) {
            System.out.print("Enter username: ");
            String username = br.readLine();
            System.out.print("Enter password: ");
            String password = br.readLine();

            AuthenticationResult result = getAccessTokenFromUserCredentials(
                    username, password);
            System.out.println("Access Token - " + result.getAccessToken());
            System.out.println("Refresh Token - " + result.getRefreshToken());
            System.out.println("ID Token - " + result.getIdToken());
        }
    }

    private static AuthenticationResult getAccessTokenFromUserCredentials(
            String username, String password) throws Exception {
        AuthenticationContext context = null;
        AuthenticationResult result = null;
        ExecutorService service = null;
        try {
            service = Executors.newFixedThreadPool(1);
            context = new AuthenticationContext(AUTHORITY, false, service);
            Future<AuthenticationResult> future = context.acquireToken(
                    "https://graph.windows.net", CLIENT_ID, username, password,
                    null);
            result = future.get();
        } finally {
            service.shutdown();
        }

        if (result == null) {
            throw new ServiceUnavailableException(
                    "authentication result was null");
        }
        return result;
    }
}


```


## <a name="compile-and-run-hello-sample"></a>Compileren en Hallo-voorbeeld uitvoeren
Wijzig weer uit tooyour-hoofdmap en Voer Hallo na de opdracht toobuild Hallo voorbeeld u plaatsen samen met `maven`. Hiermee worden gebruikt. Hallo `pom.xml` bestand dat u voor afhankelijkheden hebt geschreven.

`$ mvn package`

U hebt nu een `adal4jsample.war` bestand uw `/targets` directory. U kunt implementeren die in uw Tomcat-container en Ga naar Hallo-URL 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> Het is heel eenvoudig toodeploy een WAR met Hallo meest recente Tomcat-servers. Eenvoudig te navigeren`http://localhost:8080/manager/` Hallo instructies over het uploaden van uw '' adal4jsample.war' bestand. Deze autodeploy wordt voor u met het juiste Hallo-eindpunt.
> 
> 

## <a name="next-steps"></a>Volgende stappen
Gefeliciteerd. U nu beschikken over een werkende Java-toepassing hello mogelijkheid tooauthenticate gebruikers heeft, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.  Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.

Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

