---
title: "aaaOpen bron technologieën Veelgestelde vragen over Azure web-apps | Microsoft Docs"
description: "Toofrequently van antwoorden op veelgestelde vragen over open source-technologieën in functie van Hallo-Web-Apps van Azure App Service worden opgehaald."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Open source-technologieën Veelgestelde vragen voor Web-Apps in Azure

Dit artikel bevat antwoorden toofrequently Veelgestelde vragen (FAQ's) over problemen met open source-technologieën voor Hallo [functie van Azure App Service Web Apps](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>Mijn ClearDB-database is niet beschikbaar. Hoe kan ik dit oplossen?

Problemen met database contact op met [ClearDB ondersteuning](https://www.cleardb.com/developers/help/support). 

Bekijk voor antwoorden toocommon vragen over ClearDB [ClearDB Veelgestelde vragen over](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>Waarom wordt mijn ClearDB-database niet vermeld in Hallo-portal

Als u een ClearDB-database in Hallo maken [Azure-portal](http://portal.azure.com/), Hallo-database wordt niet weergegeven in Hallo [klassieke Azure-portal](http://manage.windowsazure.com/). toowork voorkomen, kunt u handmatig uw database toohello web-app koppelen.

Op dezelfde manier als u een ClearDB-database in Hallo maken [klassieke Azure-portal](http://manage.windowsazure.com/), ziet u niet de database in Hallo [Azure-portal](http://portal.azure.com/). In dit geval is geen oplossing beschikbaar. 

Zie voor meer informatie [Veelgestelde vragen over ClearDB MySQL-databases met Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>Waarom worden mijn ClearDB-database, is niet gemigreerd tijdens de abonnementmigratie van mijn?

Wanneer u Resourcemigratie voor abonnementen uitvoert, zijn enkele beperkingen van toepassing. Een ClearDB MySQL-database is een service van derden en wordt tijdens de migratie van een Azure-abonnement niet gemigreerd.

Als u geen Hallo migratie van uw MySQL-database beheren voordat u uw Azure-resources migreert, is het mogelijk dat uw ClearDB MySQL-database niet beschikbaar. tooavoid dit eerst handmatig migreren uw ClearDB-database en vervolgens migreren hello Azure-abonnement voor uw web-app.

Zie voor meer informatie [Veelgestelde vragen over ClearDB MySQL-databases met Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>Hoe kan ik PHP tootroubleshoot PHP problemen logboekregistratie inschakelen?

tooturn PHP logboekregistratie:

1. Meld u aan tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selecteer in het bovenste menu Hallo **Console voor foutopsporing** > **CMD**.
3. Selecteer Hallo **Site** map.
4. Selecteer Hallo **wwwroot** map.
5. Selecteer Hallo  **+**  pictogram en selecteer vervolgens **nieuw bestand**.
6. Hallo-bestandsnaam te ingesteld**. user.ini**.
7. Selecteer Hallo potloodpictogram naast te**. user.ini**.
8. Voeg deze code in Hallo-bestand:`log_errors=on`
9. Selecteer **Opslaan**.
10. Selecteer Hallo potloodpictogram naast te**wp-config.php**.
11. Hallo tekst toohello na code wijzigen:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Start opnieuw op uw web-app in hello Azure-portal in Hallo web app-menu.

Zie voor meer informatie [inschakelen WordPress foutenlogboeken](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>Hoe meld ik toepassingsfouten in Python in apps die worden gehost in App Service

toepassingsfouten in Python toocapture:

1. Selecteer in de Azure-portal in uw web-app Hallo **instellingen**.
2. Op Hallo **instellingen** tabblad **toepassingsinstellingen**.
3. Onder **appinstellingen**, Voer Hallo sleutel-waardepaar te volgen:
    * Sleutel: WSGI_LOG
    * Waarde: D:\home\site\wwwroot\logs.txt (uw keuze van bestandsnaam invoeren)

U ziet nu de fouten in Hallo logs.txt bestand in de map wwwroot Hallo.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Hoe wijzig ik Hallo-versie van Hallo Node.js-toepassing die wordt gehost in App Service?

toochange Hallo-versie van Node.js-toepassing hello, kunt u een Hallo volgende opties:

*   Gebruik in hello Azure-portal, **appinstellingen**.
    1. Ga in de Azure-portal hello, tooyour web-app.
    2. Op Hallo **instellingen** blade Selecteer **toepassingsinstellingen**.
    3. In **appinstellingen**, kunt u WEBSITE_NODE_DEFAULT_VERSION als Hallo sleutel opnemen en hello versie van Node.js u wilt gebruiken als Hallo-waarde.
    4. Ga tooyour [Kudu-console](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck Hallo Node.js-versie, Voer Hallo volgende opdracht:  
   ```
   node -v
   ```
*   Hallo iisnode.yml bestand te wijzigen. Veranderende Hallo Node.js-versie in Hallo iisnode.yml bestand alleen ingesteld Hallo runtime-omgeving waarnaar iisnode gebruikt. Uw cmd Kudu en anderen die nog steeds gebruiken Hallo Node.js-versie die is ingesteld in **appinstellingen** in hello Azure-portal.

    een bestand iisnode.yml tooset hello iisnode.yml handmatig maken in de hoofdmap van uw app. In het bestand hello, zijn onder andere Hallo volgt regel:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Hallo iisnode.yml bestand worden ingesteld met behulp van package.json tijdens de implementatie van de bron-besturingselement.
    Hello Azure bron besturingselement implementatieproces omvat Hallo stappen te volgen:
    1. Hiermee verplaatst u inhoud toohello Azure-web-app.
    2. Als er niet (deploy.cmd, .deployment-bestanden) in de hoofdmap van Hallo web app is, maakt een standaard implementatiescript.
    3. Wordt uitgevoerd een implementatiescript waarin deze een iisnode.yml bestand maakt als u vermeld Hallo Node.js-versie in Hallo package.json-bestand > engine`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. Hallo iisnode.yml bestand heeft de volgende coderegel Hallo:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>Ik zie Hallo-bericht 'Fout bij het maken van een databaseverbinding ' in mijn WordPress-app die wordt gehost in App Service. Hoe kan ik dit oplossen?

Als u deze fout in uw Azure WordPress-app, tooenable php_errors.log en debug.log ziet, volledige Hallo stappen uiteengezet in [inschakelen WordPress foutenlogboeken](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

Wanneer Hallo logboeken zijn ingeschakeld, Hallo-fout optreedt en controleer vervolgens Hallo logboeken toosee als u werkt met buiten-verbindingen:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

Als deze fout wordt weergegeven in uw debug.log of php_errors.log bestanden, wordt uw app Hallo aantal verbindingen overschrijdt. Als u op ClearDB host, controleert u of Hallo aantal verbindingen die beschikbaar zijn in uw [serviceplan](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>Hoe ik fouten opsporen in een Node.js-app die wordt gehost in App Service?

1.  Ga tooyour [Kudu-console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Ga tooyour logboeken toepassingsmap (D:\home\LogFiles\Application).
3.  Controleer in Hallo logging_errors.txt bestand, voor inhoud.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>Hoe kan ik systeemeigen Python-modules in een App Service-web-app of API-app installeren?

Sommige pakketten mogelijk niet installeren met behulp van pip in Azure. Hallo-pakket mogelijk niet beschikbaar op Hallo Python Package Index of het is mogelijk dat een compiler vereist (een compiler is niet beschikbaar is op Hallo-computer met Hallo web-app in App Service). Zie voor meer informatie over het installeren van systeemeigen modules in App Service-web-apps en API apps [installeren Python-modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Hoe implementeer ik het tooApp in een Django-app Service met behulp van Git en Hallo nieuwe versie van Python

Zie voor meer informatie over het installeren van Django [implementeren van een Django-app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>Waar zijn Hallo Tomcat-logboekbestanden bevinden?

Voor Azure Marketplace en aangepaste implementaties:

* Locatie van de map: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* Bestanden die van belang:
    * catalina. *jjjj-mm-dd*.log
    * host-manager. *jjjj-mm-dd*.log
    * localhost. *jjjj-mm-dd*.log
    * Manager. *jjjj-mm-dd*.log
    * site_access_log. *jjjj-mm-dd*.log


Voor portal **appinstellingen** implementaties:

* Locatie van de map: D:\home\LogFiles
* Bestanden die van belang:
    * catalina. *jjjj-mm-dd*.log
    * host-manager. *jjjj-mm-dd*.log
    * localhost. *jjjj-mm-dd*.log
    * Manager. *jjjj-mm-dd*.log
    * site_access_log. *jjjj-mm-dd*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>Hoe kan ik JDBC-stuurprogramma verbindingsfouten oplossen?

U ziet Hallo-bericht in uw Tomcat-logboeken te volgen:

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

tooresolve Hallo-fout:

1. Hallo sqljdbc*.jar bestand uit de map van uw app/lib verwijderen.
2. Als u van Hallo aangepaste Tomcat of Azure Marketplace Tomcat webserver gebruikmaakt, moet u deze JAR-bestand toohello Tomcat lib map kopiëren.
3. Als u Java van inschakelt hello Azure-portal (Selecteer **Java 1.8** > **Tomcat-server**), Hallo sqljdbc.* jar-bestand in map Hallo die parallel tooyour app kopiëren. Vervolgens voegt u Hallo classpath instelling toohello web.config-bestand te volgen:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Waarom zie ik fouten wanneer ik de live logboekbestanden toocopy proberen?

Als u probeert toocopy live logboekbestanden voor een Java-app (bijvoorbeeld Tomcat), ziet u mogelijk deze FTP-fout:

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

Fout bij het Hallo-bericht kan variëren, afhankelijk van Hallo FTP-client.

Alle Java-apps hebben dit probleem vergrendelen. Alleen Kudu biedt ondersteuning voor het downloaden van dit bestand tijdens het Hallo-app wordt uitgevoerd.

Stoppen Hallo app toestaat toothese bestanden FTP-toegang.

Er is een fout opgetreden in een andere oplossing toowrite een webtaak die volgens een planning wordt uitgevoerd en deze bestanden tooa andere map kopieert. Zie voor een voorbeeldproject Hallo [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Waar vind ik Hallo-logboekbestanden voor Jetty

Voor Marketplace- en aangepaste implementaties is het logboekbestand Hallo Hallo D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs map. Houd er rekening mee dat Hallo maplocatie afhankelijk is van Hallo-versie van de Jetty die u gebruikt. Hallo-pad opgegeven bijvoorbeeld hier is voor Jetty 9.1.2. Zoek naar jetty_*YYYY_MM_DD*. stderrout.log.

Voor implementaties van de portal App-instelling is Hallo logboekbestand in D:\home\LogFiles. Zoek naar jetty_*YYYY_MM_DD*. stderrout.log

## <a name="can-i-send-email-from-my-azure-web-app"></a>Kan ik e-mail verzenden vanuit Mijn Azure-web-app

App Service beschikt niet over een ingebouwde e-functie. Voor sommige goede alternatieven voor het verzenden van e-mail van uw app, raadpleegt u dit [bespreking van de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>Waarom mijn WordPress-site Omleidings-URL tooanother?

Als u onlangs tooAzure hebt gemigreerd, mogelijk WordPress toohello oude domein-URL omleiden. Dit wordt veroorzaakt door een instelling in Hallo MySQL-database.

WordPress contactpersoon + is een Azure Site-uitbreiding die u rechtstreeks in de database Hallo tooupdate Hallo Omleidings-URL kunt gebruiken. Zie voor meer informatie over het gebruik van WordPress contactpersoon + [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

U kunt ook als u liever toomanually update Hallo Omleidings-URL met behulp van SQL-query's of PHPMyAdmin, Zie [WordPress: toowrong URL omleiden](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>Hoe kan ik mijn WordPress aanmelden wachtwoord wijzigen?

Als u uw WordPress aanmelden wachtwoord vergeten bent, kunt u WordPress contactpersoon + tooupdate deze. uw wachtwoord, installatie Hallo WordPress contactpersoon + Azure Site-uitbreiding en vervolgens voltooit Hallo stappen wordt beschreven in tooreset [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>Ik kan niet tooWordPress aanmelden. Hoe kan ik dit oplossen?

Als u WordPress vergrendeld merkt na de installatie van een invoegtoepassing onlangs, hebt u mogelijk een defecte invoegtoepassing. WordPress contactpersoon + is een Azure-Site-uitbreiding die u kunnen helpen uitschakelen invoegtoepassingen in WordPress. Zie voor meer informatie [WordPress hulpprogramma's en MySQL migratie met WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="how-do-i-migrate-my-wordpress-database"></a>Hoe Migreer ik mijn WordPress-database

U hebt meerdere mogelijkheden voor migratie Hallo MySQL-database die is verbonden tooyour WordPress-website:

* Ontwikkelaars: Gebruik Hallo [opdrachtprompt of PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* Niet-Ontwikkelaars: [WordPress contactpersoon +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)

## <a name="how-do-i-help-make-wordpress-more-secure"></a>Hoe u helpen WordPress veiliger maken?

toolearn over aanbevolen beveiligingsprocedures voor WordPress, Zie [Best practices voor beveiliging van WordPress in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Ik probeer toouse PHPMyAdmin en Zie Hallo-bericht 'Toegang geweigerd'. Hoe kan ik dit oplossen?

U kunt dit probleem kan optreden als Hallo MySQL in-app-functie nog niet wordt uitgevoerd in dit App Service-exemplaar. tooresolve Hallo probleem, probeer tooaccess uw website. Hallo vereist processen, inclusief Hallo MySQL in-app-proces wordt gestart. MySQL-app wordt uitgevoerd, klikt u in proces Explorer ervoor te zorgen dat mysqld.exe tooverify wordt vermeld in het Hallo-processen.

Nadat u ervoor te zorgen dat MySQL in-app wordt uitgevoerd, probeert u toouse PHPMyAdmin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Er verschijnt een HTTP 403-fout als ik probeer tooimport of mijn MySQL-database in-app met behulp van PHPMyadmin exporteren. Hoe kan ik dit oplossen?

Als u een oudere versie van Chrome gebruikt, u mogelijk ondervindt een bekend probleem. tooresolve hello probleem upgrade tooa nieuwere versie van Chrome. Ook kunt u proberen met een andere browser, zoals Internet Explorer of Edge, waarbij Hallo niet gebeurt.
