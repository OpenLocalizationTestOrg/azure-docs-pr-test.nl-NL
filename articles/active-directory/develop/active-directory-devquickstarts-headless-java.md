---
title: Azure AD-Java-opdrachtregel aan de slag | Microsoft Docs
description: Het bouwen van een Java-opdrachtregel-app die gebruikers zich aanmeldt voor toegang tot een API.
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
ms.openlocfilehash: 91e4a7b2ac454465d5cce4948a4d5f0b542d2b55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-java-command-line-app-to-access-an-api-with-azure-ad"></a><span data-ttu-id="d8843-103">Gebruik van Java-opdrachtregel-App voor toegang tot een API met Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8843-103">Using Java Command Line App To Access An API with Azure AD</span></span>
[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="d8843-104">Azure AD kunt u eenvoudig en snel te uitbesteden identiteitsbeheer van uw web-app, bieden één aanmelden en afmelden met slechts een paar regels code.</span><span class="sxs-lookup"><span data-stu-id="d8843-104">Azure AD makes it simple and straightforward to outsource your web app's identity management, providing single sign-in and sign-out with only a few lines of code.</span></span>  <span data-ttu-id="d8843-105">In Java-web-apps, kunt u dit doen met behulp van Microsoft implementatie van de community aangestuurde ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="d8843-105">In Java web apps, you can accomplish this using Microsoft's implementation of the community-driven ADAL4J.</span></span>

  <span data-ttu-id="d8843-106">We gebruiken hier ADAL4J naar:</span><span class="sxs-lookup"><span data-stu-id="d8843-106">Here we'll use ADAL4J to:</span></span>

* <span data-ttu-id="d8843-107">Meld u aan de gebruiker in de app gebruikmaken van Azure AD als de id-provider.</span><span class="sxs-lookup"><span data-stu-id="d8843-107">Sign the user into the app using Azure AD as the identity provider.</span></span>
* <span data-ttu-id="d8843-108">Sommige informatie over de gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d8843-108">Display some information about the user.</span></span>
* <span data-ttu-id="d8843-109">Meld u aan de gebruiker buiten de app.</span><span class="sxs-lookup"><span data-stu-id="d8843-109">Sign the user out of the app.</span></span>

<span data-ttu-id="d8843-110">Om dit te doen, moet u het:</span><span class="sxs-lookup"><span data-stu-id="d8843-110">In order to do this, you'll need to:</span></span>

1. <span data-ttu-id="d8843-111">Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8843-111">Register an application with Azure AD</span></span>
2. <span data-ttu-id="d8843-112">Uw app instellen voor gebruik van de bibliotheek ADAL4J.</span><span class="sxs-lookup"><span data-stu-id="d8843-112">Set up your app to use the ADAL4J library.</span></span>
3. <span data-ttu-id="d8843-113">De bibliotheek ADAL4J gebruiken om aan- en afmeldingsaanvragen te verzenden naar Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8843-113">Use the ADAL4J library to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="d8843-114">Gegevens over de gebruiker te drukken.</span><span class="sxs-lookup"><span data-stu-id="d8843-114">Print out data about the user.</span></span>

<span data-ttu-id="d8843-115">Aan de slag [de basis van de app downloaden](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) of [het voltooide voorbeeld downloaden](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="d8843-115">To get started, [download the app skeleton](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/skeleton.zip) or [download the completed sample](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect\\/archive/complete.zip).</span></span>  <span data-ttu-id="d8843-116">U moet ook een Azure AD-tenant waarin u uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="d8843-116">You'll also need an Azure AD tenant in which to register your application.</span></span>  <span data-ttu-id="d8843-117">Als u niet hebt, [Lees hoe u een](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="d8843-117">If you don't have one already, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1--register-an-application-with-azure-ad"></a><span data-ttu-id="d8843-118">1.  Een toepassing registreren met Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8843-118">1.  Register an Application with Azure AD</span></span>
<span data-ttu-id="d8843-119">Om uw app om gebruikers te verifiëren, moet u eerst een nieuwe toepassing registreren in uw tenant.</span><span class="sxs-lookup"><span data-stu-id="d8843-119">To enable your app to authenticate users, you'll first need to register a new application in your tenant.</span></span>

1. <span data-ttu-id="d8843-120">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8843-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d8843-121">Klik op de bovenste balk op je account en klikt u onder de **Directory** kiest u de Active Directory-tenant waar u wilt uw toepassing registreren.</span><span class="sxs-lookup"><span data-stu-id="d8843-121">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="d8843-122">Klik op **meer Services** in de nav linkerkant en kies **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8843-122">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="d8843-123">Klik op **App registraties** en kies **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="d8843-123">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="d8843-124">Volg de aanwijzingen en maak een nieuwe **webtoepassing en/of WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="d8843-124">Follow the prompts and create a new **Web Application and/or WebAPI**.</span></span>
  * <span data-ttu-id="d8843-125">De **naam** van de toepassing bevat een beschrijving van uw toepassing aan eindgebruikers</span><span class="sxs-lookup"><span data-stu-id="d8843-125">The **name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="d8843-126">De **aanmeldings-URL** is de basis-URL van uw app.</span><span class="sxs-lookup"><span data-stu-id="d8843-126">The **Sign-On URL** is the base URL of your app.</span></span>  <span data-ttu-id="d8843-127">Het basisproject standaardwaarde is `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="d8843-127">The skeleton's default is `http://localhost:8080/adal4jsample/`.</span></span>
6. <span data-ttu-id="d8843-128">Zodra u inschrijving hebt voltooid, toewijst AAD uw app een unieke id</span><span class="sxs-lookup"><span data-stu-id="d8843-128">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="d8843-129">U moet deze waarde in de volgende secties, dus kopiëren vanaf het toepassingstabblad.</span><span class="sxs-lookup"><span data-stu-id="d8843-129">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="d8843-130">Van de **instellingen** -> **eigenschappen** pagina voor uw toepassing, het bijwerken van de App ID URI.</span><span class="sxs-lookup"><span data-stu-id="d8843-130">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="d8843-131">De **App ID URI** is de unieke id voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d8843-131">The **App ID URI** is a unique identifier for your application.</span></span>  <span data-ttu-id="d8843-132">De overeenkomst is met `https://<tenant-domain>/<app-name>`, bijvoorbeeld `http://localhost:8080/adal4jsample/`.</span><span class="sxs-lookup"><span data-stu-id="d8843-132">The convention is to use `https://<tenant-domain>/<app-name>`, e.g. `http://localhost:8080/adal4jsample/`.</span></span>

<span data-ttu-id="d8843-133">Eenmaal in de portal voor uw app maakt een **sleutel** van de **instellingen** pagina voor uw toepassing en kopieer het naar beneden.</span><span class="sxs-lookup"><span data-stu-id="d8843-133">Once in the portal for your app create a **Key** from the **Settings** page for your application and copy it down.</span></span>  <span data-ttu-id="d8843-134">U hebt dit zo direct nodig.</span><span class="sxs-lookup"><span data-stu-id="d8843-134">You will need it shortly.</span></span>

## <a name="2-set-up-your-app-to-use-adal4j-library-and-prerequisites-using-maven"></a><span data-ttu-id="d8843-135">2. Uw app instellen voor gebruik van de bibliotheek ADAL4J en vereisten met behulp van Maven</span><span class="sxs-lookup"><span data-stu-id="d8843-135">2. Set up your app to use ADAL4J library and prerequisites using Maven</span></span>
<span data-ttu-id="d8843-136">Hier geconfigureerd ADAL4J voor het gebruik van het OpenID Connect-verificatieprotocol.</span><span class="sxs-lookup"><span data-stu-id="d8843-136">Here, we'll configure ADAL4J to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="d8843-137">ADAL4J wordt gebruikt op aan- en afmeldingsaanvragen te verzenden en informatie ophalen over de gebruiker, onder andere de gebruikerssessie te beheren.</span><span class="sxs-lookup"><span data-stu-id="d8843-137">ADAL4J will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="d8843-138">In de hoofdmap van uw project openen/maken `pom.xml` en zoek de `// TODO: provide dependencies for Maven` en vervangen door het volgende:</span><span class="sxs-lookup"><span data-stu-id="d8843-138">In the root directory of your project, open/create `pom.xml` and locate the `// TODO: provide dependencies for Maven` and replace with the following:</span></span>

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



## <a name="3-create-the-java-publicclient-file"></a><span data-ttu-id="d8843-139">3. Het bestand Java PublicClient maken</span><span class="sxs-lookup"><span data-stu-id="d8843-139">3. Create the Java PublicClient file</span></span>
<span data-ttu-id="d8843-140">Zoals hierboven vermeld we gebruiken de Graph API om gegevens over de aangemelde gebruiker te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="d8843-140">As indicated above, we will be using the Graph API to get data about the logged in user.</span></span> <span data-ttu-id="d8843-141">Voor dit eenvoudig ons moet maken we beide een bestand vertegenwoordigt een **mapobject** en een afzonderlijk bestand vertegenwoordigt de **gebruiker** zodat het patroon OO van Java kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d8843-141">For this to be easy for us we should create both a file to represent a **Directory Object** and an individual file to represent the **User** so that the OO pattern of Java can be used.</span></span>

* <span data-ttu-id="d8843-142">Maken van een bestand met de naam `DirectoryObject.java` die zullen worden gebruikt voor het opslaan van elementaire gegevens over een DirectoryObject (u kunt gerust dit later gebruiken voor andere grafiek query's kunt u doen).</span><span class="sxs-lookup"><span data-stu-id="d8843-142">Create a file called `DirectoryObject.java` which we will use to store basic data about any DirectoryObject (you can feel free to use this later for any other Graph Queries you may do).</span></span> <span data-ttu-id="d8843-143">U kunt knippen en plakken dit uit het volgende:</span><span class="sxs-lookup"><span data-stu-id="d8843-143">You can cut/paste this from below:</span></span>

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


## <a name="compile-and-run-the-sample"></a><span data-ttu-id="d8843-144">Compileren en uitvoeren van de steekproef</span><span class="sxs-lookup"><span data-stu-id="d8843-144">Compile and run the sample</span></span>
<span data-ttu-id="d8843-145">Wijzig weer uit in de hoofdmap en voer de volgende opdracht voor het bouwen van de steekproef u plaatsen samen met `maven`.</span><span class="sxs-lookup"><span data-stu-id="d8843-145">Change back out to your root directory and run the following command to build the sample you just put together using `maven`.</span></span> <span data-ttu-id="d8843-146">Hiermee worden gebruikt. de `pom.xml` bestand dat u voor afhankelijkheden hebt geschreven.</span><span class="sxs-lookup"><span data-stu-id="d8843-146">This will use the `pom.xml` file you wrote for dependencies.</span></span>

`$ mvn package`

<span data-ttu-id="d8843-147">U hebt nu een `adal4jsample.war` bestand uw `/targets` directory.</span><span class="sxs-lookup"><span data-stu-id="d8843-147">You should now have a `adal4jsample.war` file in your `/targets` directory.</span></span> <span data-ttu-id="d8843-148">U kunt implementeren die in uw Tomcat-container en Ga naar de URL</span><span class="sxs-lookup"><span data-stu-id="d8843-148">You may deploy that in your Tomcat container and visit the URL</span></span> 

`http://localhost:8080/adal4jsample/`

> [!NOTE]
> <span data-ttu-id="d8843-149">Het is heel eenvoudig een WAR met de meest recente Tomcat-servers implementeren.</span><span class="sxs-lookup"><span data-stu-id="d8843-149">It is very easy to deploy a WAR with the latest Tomcat servers.</span></span> <span data-ttu-id="d8843-150">Gewoon gaat u naar `http://localhost:8080/manager/` en volg de instructies over het uploaden van uw '' adal4jsample.war' bestand.</span><span class="sxs-lookup"><span data-stu-id="d8843-150">Simply navigate to `http://localhost:8080/manager/` and follow the instructions on uploading your ``adal4jsample.war\` file.</span></span> <span data-ttu-id="d8843-151">Deze autodeploy wordt voor u met het juiste eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d8843-151">It will autodeploy for you with the correct endpoint.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d8843-152">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d8843-152">Next Steps</span></span>
<span data-ttu-id="d8843-153">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="d8843-153">Congratulations!</span></span> <span data-ttu-id="d8843-154">U hebt nu een werkende Java-toepassing heeft de mogelijkheid om gebruikers te verifiëren, veilig aanroepen van Web-API's met behulp van OAuth 2.0 en algemene informatie over de gebruiker ophalen.</span><span class="sxs-lookup"><span data-stu-id="d8843-154">You now have a working Java application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="d8843-155">Als u nog niet gedaan hebt, is nu de tijd voor het vullen van uw tenant waarbij sommige gebruikers.</span><span class="sxs-lookup"><span data-stu-id="d8843-155">If you haven't already, now is the time to populate your tenant with some users.</span></span>

<span data-ttu-id="d8843-156">Voor een verwijzing naar het voltooide voorbeeld (zonder uw configuratiewaarden) [is opgegeven als een ZIP hier](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), of u kunt dit ook klonen vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="d8843-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/Azure-Samples/active-directory-java-webapp-openidconnect.git```

