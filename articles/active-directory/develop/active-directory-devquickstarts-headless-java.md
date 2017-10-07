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
# <a name="using-java-command-line-app-tooaccess-an-api-with-azure-ad"></a><span data-ttu-id="adf0d-103">Met behulp van Java-opdrachtregel-App tooAccess een API met Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf0d-103">Using Java Command Line App tooAccess An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="adf0d-104">Azure AD maakt het eenvoudig en snel toooutsource identiteitsbeheer van uw web-app, biedt eenmalige aanmelden en afmelden met slechts een paar regels code.</span><span class="sxs-lookup"><span data-stu-id="adf0d-104">Azure AD makes it simple and straightforward toooutsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="adf0d-105">In Java-web-apps, kunt u dit doen met behulp van Microsoft implementatie van Hallo community aangestuurde ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="adf0d-105">In Java web apps, you can accomplish this using Microsoft's implementation of hello community-driven ADAL4J.</span></span>

  <span data-ttu-id="adf0d-106">We gebruiken hier ADAL4J naar:</span><span class="sxs-lookup"><span data-stu-id="adf0d-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="adf0d-107">Meld u Hallo gebruiker in met behulp van Azure AD als id-provider Hallo Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="adf0d-107">Sign hello user into hello app using Azure AD as hello identity provider.</span></span>
* <span data-ttu-id="adf0d-108">Sommige informatie over Hallo gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="adf0d-108">Display some information about hello user.</span></span>
* <span data-ttu-id="adf0d-109">Meld u Hallo gebruiker buiten het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="adf0d-109">Sign hello user out of hello app.</span></span>

<span data-ttu-id="adf0d-110">Toodo dit order, moet u in:</span><span class="sxs-lookup"><span data-stu-id="adf0d-110">In order toodo this, you'll need to:</span></span>

1. <span data-ttu-id="adf0d-111">Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf0d-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="adf0d-112">Instellen van uw app toouse hello ADAL4J-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="adf0d-112">Set up your app toouse hello ADAL4J library.</span></span>
3. <span data-ttu-id="adf0d-113">Hallo ADAL4J bibliotheek tooissue aanmelden en afmelden aanvragen tooAzure AD gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adf0d-113">Use hello ADAL4J library tooissue sign-in and sign-out requests tooAzure AD.</span></span>
4. <span data-ttu-id="adf0d-114">Gegevens over Hallo gebruiker afdrukken.</span><span class="sxs-lookup"><span data-stu-id="adf0d-114">Print out data about hello user.</span></span>

<span data-ttu-id="adf0d-115">tooget gestart, [Hallo app basisproject downloaden](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) of [Hallo voltooid voorbeeld downloaden](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="adf0d-115">tooget started, [download hello app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download hello completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="adf0d-116">Ook moet u een Azure AD-tenant in welke tooregister uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="adf0d-116">You'll also need an Azure AD tenant in which tooregister your application.</span></span>  <span data-ttu-id="adf0d-117">Als u niet hebt, [meer informatie over hoe tooget een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="adf0d-117">If you don't have one already, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="adf0d-118">1.  Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="adf0d-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="adf0d-119">tooenable uw app tooauthenticate gebruikers, moet u eerst een nieuwe toepassing tooregister in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="adf0d-119">tooenable your app tooauthenticate users, you'll first need tooregister a new application in your tenant.</span></span>

1. <span data-ttu-id="adf0d-120">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="adf0d-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="adf0d-121">Op de bovenste balk hello, klikt u op voor uw account en Hallo **Directory** Kies Hallo Active Directory-tenant waar u wenst dat tooregister uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="adf0d-121">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="adf0d-122">Klik op **meer Services** in linkerkant nav Hallo en kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="adf0d-122">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="adf0d-123">Klik op **App registraties** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="adf0d-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="adf0d-124">Volg de aanwijzingen Hallo en maak een nieuwe **webtoepassing en/of WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="adf0d-124">Follow hello prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="adf0d-125">Hallo **naam** Hallo bevat toepassing een beschrijving van uw toepassing tooend-gebruikers</span><span class="sxs-lookup"><span data-stu-id="adf0d-125">hello **name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="adf0d-126">Hallo **aanmeldings-URL** Hallo basis-URL van uw app is.</span><span class="sxs-lookup"><span data-stu-id="adf0d-126">hello **Sign-On URL** is hello base URL of your app.</span></span>  <span data-ttu-id="adf0d-127">Hallo basisproject de standaardwaarde is `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="adf0d-127">hello skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="adf0d-128">Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id</span><span class="sxs-lookup"><span data-stu-id="adf0d-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="adf0d-129">U moet deze waarde in de volgende secties hello, dus kopieer het van Hallo toepassingstabblad.</span><span class="sxs-lookup"><span data-stu-id="adf0d-129">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="adf0d-130">Van Hallo **instellingen** -> **eigenschappen** pagina voor uw toepassing, Hallo App ID URI bijwerken.</span><span class="sxs-lookup"><span data-stu-id="adf0d-130">From hello **Settings** -> **Properties** page for your application, update hello App ID URI.</span></span> <span data-ttu-id="adf0d-131">Hallo **App ID URI** is de unieke id voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="adf0d-131">hello **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="adf0d-132">Hallo-conventie is toouse `https://<tenant-domain>/<app-name>`, bijvoorbeeld `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="adf0d-132">hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="adf0d-133">Eenmaal in Hallo-portal voor uw app maakt een **sleutel** van Hallo **instellingen** pagina voor uw toepassing en kopieer het naar beneden.</span><span class="sxs-lookup"><span data-stu-id="adf0d-133">Once in hello portal for your app create a **Key** from hello **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="adf0d-134">U hebt dit zo direct nodig.</span><span class="sxs-lookup"><span data-stu-id="adf0d-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-toouse-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="adf0d-135">2. Uw app toouse ADAL4J-bibliotheek en de vereisten met behulp van Maven instellen</span><span class="sxs-lookup"><span data-stu-id="adf0d-135">2. Set up your app toouse ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="adf0d-136">Hier geconfigureerd ADAL4J toouse hello OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="adf0d-136">Here, we'll configure ADAL4J toouse hello OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="adf0d-137">ADAL4J gaat gebruikte tooissue aanmelden en afmeldingsaanvragen te verzenden, Hallo gebruikerssessie beheren en informatie ophalen over de gebruiker hello, onder andere.</span><span class="sxs-lookup"><span data-stu-id="adf0d-137">ADAL4J will be used tooissue sign-in and sign-out requests, manage hello user's session, and get information about hello user, amongst other things.</span></span>

* <span data-ttu-id="adf0d-138">In de hoofdmap van uw project Hallo openen/maken `pom.xml` en zoek Hallo `// TODO: provide dependencies for Maven` en vervang door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="adf0d-138">In hello root directory of your project, open/create `pom.xml` and locate hello `// TODO: provide dependencies for Maven` and replace with hello following:</span></span>

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



## <a name="3-create-hello-java-publicclient-file"></a><span data-ttu-id="adf0d-139">3. Hallo Java PublicClient bestand maken</span><span class="sxs-lookup"><span data-stu-id="adf0d-139">3. Create hello Java PublicClient file</span></span>
<span data-ttu-id="adf0d-140">Zoals hierboven vermeld, zullen we gebruikmaken van Hallo Graph API tooget gegevens over Hallo aangemelde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="adf0d-140">As indicated above, we will be using hello Graph API tooget data about hello logged in user.</span></span> <span data-ttu-id="adf0d-141">Voor deze gemakkelijk voor ons toobe moet maken we beide een bestand toorepresent een **mapobject** en een afzonderlijk bestand toorepresent hello **gebruiker** zodat hello OO patroon van Java kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="adf0d-141">For this toobe easy for us we should create both a file toorepresent a **Directory Object** and an individual file toorepresent hello **User** so that hello OO pattern of Java can be used.</span></span>

* <span data-ttu-id="adf0d-142">Maken van een bestand met de naam `DirectoryObject.java` die we toostore basisgegevens over eventuele DirectoryObject (kunt u erop gratis toouse dit later voor andere grafiek query's kunt u doen) worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="adf0d-142">Create a file called `DirectoryObject.java` which we will use toostore basic data about any DirectoryObject (you can feel free toouse this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="adf0d-143">U kunt knippen en plakken dit uit het volgende:</span><span class="sxs-lookup"><span data-stu-id="adf0d-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-hello-sample"></a><span data-ttu-id="adf0d-144">Compileren en Hallo-voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="adf0d-144">Compile and run hello sample</span></span>
<span data-ttu-id="adf0d-145">Wijzig weer uit tooyour-hoofdmap en Voer Hallo na de opdracht toobuild Hallo voorbeeld u plaatsen samen met `maven`.</span><span class="sxs-lookup"><span data-stu-id="adf0d-145">Change back out tooyour root directory and run hello following command toobuild hello sample you just put together using `maven`.</span></span> <span data-ttu-id="adf0d-146">Hiermee worden gebruikt. Hallo `pom.xml` bestand dat u voor afhankelijkheden hebt geschreven.</span><span class="sxs-lookup"><span data-stu-id="adf0d-146">This will use hello `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="adf0d-147">U hebt nu een `adal4jsample.war` bestand uw `/targets` directory.</span><span class="sxs-lookup"><span data-stu-id="adf0d-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="adf0d-148">U kunt implementeren die in uw Tomcat-container en Ga naar Hallo-URL</span><span class="sxs-lookup"><span data-stu-id="adf0d-148">You may deploy that in your Tomcat container and visit hello URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="adf0d-149">Het is heel eenvoudig toodeploy een WAR met Hallo meest recente Tomcat-servers.</span><span class="sxs-lookup"><span data-stu-id="adf0d-149">It is very easy toodeploy a WAR with hello latest Tomcat servers.</span></span> <span data-ttu-id="adf0d-150">Eenvoudig te navigeren`http://localhost:8080/manager/` Hallo instructies over het uploaden van uw '' adal4jsample.war' bestand.</span><span class="sxs-lookup"><span data-stu-id="adf0d-150">Simply navigate too`http://localhost:8080/manager/` and follow hello instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="adf0d-151">Deze autodeploy wordt voor u met het juiste Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="adf0d-151">It will autodeploy for you with hello correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="adf0d-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="adf0d-152">Next Steps</span></span>
<span data-ttu-id="adf0d-153">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="adf0d-153">Congratulations!</span></span> <span data-ttu-id="adf0d-154">U nu beschikken over een werkende Java-toepassing hello mogelijkheid tooauthenticate gebruikers heeft, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en basisinformatie over Hallo gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="adf0d-154">You now have a working Java application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="adf0d-155">Als u nog niet gedaan hebt, is nu Hallo tijd toopopulate uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="adf0d-155">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>

<span data-ttu-id="adf0d-156">Ter referentie: voltooid Hallo voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="adf0d-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

