---
title: aaaBuild een Java- en MySQL web-app in Azure
description: Meer informatie over hoe tooget een Java-app die is verbonden toohello Azure MySQL database-service in Azure App service werkt.
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Een Java- en MySQL web-app in Azure bouwen

Deze zelfstudie leert u hoe toocreate een Java web-app in Azure en verbindt u deze tooa MySQL-database. Wanneer u klaar bent, hebt u een [Spring Boot](https://projects.spring.io/spring-boot/) toepassing opslaan van gegevens in [Azure Database voor MySQL](https://docs.microsoft.com/azure/mysql/overview) uitgevoerd op [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![Java-app uitgevoerd in Azure App service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een MySQL-database maken in Azure
> * Verbinding maken met een voorbeeld-app toohello database
> * Hallo app tooAzure implementeren
> * Bijwerken en het Hallo-app implementeren
> * Diagnostische logboeken van de stroom van Azure
> * Hallo app controleren in hello Azure-portal


## <a name="prerequisites"></a>Vereisten

1. [Download en installeer Git](https://git-scm.com/)
1. [Download en installeer Hallo JDK van Java-7 of hoger](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [Downloaden, installeren en starten van MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Lokale MySQL voorbereiden 

In deze stap maakt u een database in een lokale MySQL-server voor gebruik in testen Hallo app lokaal op uw computer.

### <a name="connect-toomysql-server"></a>TooMySQL server verbinden

In een terminalvenster verbinding tooyour lokale MySQL-server. U kunt deze toorun terminalvenster alle Hallo-opdrachten gebruiken in deze zelfstudie.

```bash
mysql -u root -p
```

Als u wordt gevraagd om een wachtwoord, hello wachtwoord invoeren voor Hallo `root` account. Als je het wachtwoord van je root-account, Zie [MySQL: hoe tooReset hoofdwachtwoord Hallo](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Als uw opdracht is uitgevoerd, wordt al uw MySQL-server uitgevoerd. Als dit niet het geval is, zorg ervoor dat de lokale MySQL-server is gestart met de volgende Hallo [MySQL na de installatie stappen](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Een database maken 

In Hallo `mysql` vragen, maakt u een database en een tabel voor Hallo taakitems.

```sql
CREATE DATABASE tododb;
```

Uw serververbinding sluiten door te typen `quit`.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Maken en Hallo voorbeeld-app uitvoeren 

In deze stap voorbeeldapp Spring opstarten klonen, toouse Hallo lokale MySQL-database configureren en uitvoeren op uw computer. 

### <a name="clone-hello-sample"></a>Kloon Hallo-voorbeeld

Navigeer in terminalvenster hello, tooa directory- en kloon Hallo voorbeeld opslagplaats werkt. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Hallo app toouse Hallo MySQL-database configureren

Update Hallo `spring.datasource.password` en de waarde *spring-boot-mysql-todo/src/main/resources/application.properties* Hello dezelfde hoofdwachtwoord tooopen Hallo MySQL prompt gebruikt:

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Bouwen en uitvoeren van Hallo-voorbeeld

Bouwen en uitvoeren met Hallo Maven wrapper die is opgenomen in de opslagplaats Hallo Hallo-voorbeeld:

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Open uw browser toohttp://localhost:8080 toosee in de steekproef Hallo in te grijpen. Als u een lijst met taken toohello toevoegt, gebruik Hallo volgende SQL-in Hallo MySQL vragen tooview Hallo opgeslagen gegevens in MySQL opdrachten.

```SQL
use testdb;
select * from todo_item;
```

Hallo toepassing stoppen roept `Ctrl` + `C` in Hallo terminal. 

## <a name="create-an-azure-mysql-database"></a>Een Azure-MySQL-database maken

In deze stap maakt u een [Azure Database voor MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) exemplaar met gebruikmaking van Hallo [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli). U Hallo voorbeeld toepassing toouse deze database later op in de zelfstudie Hallo.

Gebruik hello Azure CLI 2.0 in een terminalvenster toocreate Hallo bronnen nodig toohost uw Java-toepassing in Azure App service. Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) Hello [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waar verwante resources, zoals web-apps, databases en storage-accounts worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld wordt een resourcegroep in Hallo Noord-Europa regio:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

toosee hello mogelijke waarden kunt u gebruiken voor `--location`, gebruik Hallo [az appservice lijst-locaties](/cli/azure/appservice#list-locations) opdracht.

### <a name="create-a-mysql-server"></a>Een MySQL-server maken

Maken van een server in Azure-Database voor MySQL (Preview) Hello [az mysql-server maken](/cli/azure/mysql/server#create) opdracht.    
Vervangen door uw eigen unieke MySQL servernaam op waar u Hallo zien `<mysql_server_name>` tijdelijke aanduiding. Deze naam maakt deel uit van de hostnaam van uw MySQL-server, `<mysql_server_name>.mysql.database.azure.com`, dus moet toobe globaal uniek zijn. Ook vervangen `<admin_user>` en `<admin_password>` met uw eigen waarden.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Wanneer Hallo MySQL-server is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>Een firewall configureren

Een firewallregel maken voor uw MySQL server tooallow client verbindingen via Hallo [az mysql server-firewallregel maken](/cli/azure/mysql/server/firewall-rule#create) opdracht. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Azure-Database voor MySQL (Preview) kunnen niet automatisch momenteel verbindingen van Azure-services. Zoals IP-adressen in Azure dynamisch toegewezen worden, is het beter tooenable alle IP-adressen voor nu. Wanneer Hallo service de preview blijft, kunt u betere methoden voor het beveiligen van uw database wordt ingeschakeld.

## <a name="configure-hello-azure-mysql-database"></a>Hello Azure MySQL-database configureren

In terminalvenster Hallo op uw computer verbinding met toohello MySQL-server in Azure. Hallo-waarde die u eerder hebt opgegeven voor `<admin_user>` en `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Een database maken 

In Hallo `mysql` vragen, maakt u een database en een tabel voor Hallo taakitems.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>Een gebruiker met machtigingen maken

Een databasegebruiker maken en hieraan alle bevoegdheden in Hallo `tododb` database. Vervang de tijdelijke aanduidingen Hallo `<Javaapp_user>` en `<Javaapp_password>` met uw eigen unieke app-naam.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Uw serververbinding sluiten door te typen `quit`.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Hallo voorbeeld tooAzure App Service implementeren

Maken van een Azure App Service-abonnement met Hallo **vrije** prijscategorie Hallo met [az appservice-abonnement maken](/cli/azure/appservice/plan#create) CLI-opdracht. Hallo appservice-abonnement definieert Hallo fysieke resources gebruikt toohost uw apps. Alle toepassingen die toegewezen tooan appservice-abonnement kunt u deze resources, zodat u toosave kosten bij het hosten van meerdere apps delen. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Wanneer Hallo plan klaar is, uitvoer hello die Azure CLI ongeveer dezelfde wordt toohello voorbeeld te volgen:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Een Azure-Web-app maken

 Gebruik Hallo [az webapp maken](/cli/azure/appservice/web#create) CLI opdracht toocreate de definitie van een web-app in Hallo `myAppServicePlan` App Service-abonnement. Hallo web app definitie voorziet in uw toepassing met een URL-tooaccess en verschillende opties toodeploy uw code tooAzure configureert. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

Vervang Hallo `<app_name>` aanduiding voor items met uw eigen unieke app-naam. Deze unieke naam is onderdeel van de standaarddomeinnaam Hallo voor Hallo-web-app Hallo naam moet toobe uniek zijn in alle apps in Azure. U kunt een aangepast domein de naam van vermelding toohello web-app kunt toewijzen, voordat u deze tooyour gebruikers weergeven.

Wanneer de definitie van Hallo web apps klaar is, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Java configureren 

Hallo Java runtime-configuratie die uw app Hello moet instellen [az appservice web config update](/cli/azure/appservice/web/config#update) opdracht.

Hallo volgende opdracht configureert u Hallo web app toorun op een recente Java 8 JDK en [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Hallo app toouse hello Azure SQL database configureren

Voordat u de voorbeeld-app hello, stelt u toepassingsinstellingen op Hallo web app toouse hello Azure MySQL-database die in Azure worden gemaakt. Deze eigenschappen zijn blootgestelde toohello webtoepassing als omgevingsvariabelen en Hallo onderdrukkingswaarden in Hallo application.properties binnen Hallo verpakte web-app ingesteld. 

Toepassingsinstellingen met [az webapp config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) in Hallo CLI:

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>FTP-implementatiereferenties ophalen 
U kunt uw toepassing tooAzure appservice op verschillende manieren, met inbegrip van de FTP-, lokale Git, GitHub, Visual Studio Team Services en BitBucket implementeren. FTP-toodeploy Hallo voor dit voorbeeld. WAR-bestand is gebouwd eerder op uw lokale machine tooAzure App Service.

toodetermine wat toopass langs in een FTP-opdracht toohello Web-App gebruikt de referenties [implementatie in az appservice web-lijst-publicatie-profielen](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) opdracht: 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>Met FTP Hallo-app uploaden

Gebruik uw favoriete toodeploy Hallo voor FTP-hulpprogramma. WAR-bestand toohello */site/wwwroot/webapps* map op het Hallo-serveradres die afkomstig zijn uit Hallo `URL` veld in de vorige opdracht Hallo. Hallo bestaande (ROOT) standaardmap toepassingen verwijderen en vervang bestaande ROOT.war Hello Hallo. Ingebouwd in Hallo eerder in de zelfstudie Hallo WAR-bestand.

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>Test Hallo web-app

Te bladeren`http://<app_name>.azurewebsites.net/` en enkele taken toohello lijst toevoegen. 

![Java-app uitgevoerd in Azure App service](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**Gefeliciteerd!** U uitvoert een Java-gegevensgestuurde app in Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Update Hallo app en de implementatie opnieuw uit

Werk Hallo toepassing tooinclude een extra kolom in de takenlijst Hallo voor welke dag Hallo-item is gemaakt. Spring opstarten verwerkt bijwerken Hallo-databaseschema voor u als wijzigingen in het gegevensmodel Hallo zonder uw bestaande databaserecords zelf te wijzigen.

1. Open op uw lokale systeem *src/main/java/com/example/fabrikam/TodoItem.java* en voeg de volgende Hallo importeert toohello klasse:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Voeg een `String` eigenschap `timeCreated` te*src/main/java/com/example/fabrikam/TodoItem.java*, deze met een tijdstempel bij het maken van een object te initialiseren. Toevoegen van getters/setters voor nieuwe Hallo `timeCreated` eigenschap tijdens het bewerken van dit bestand.

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. Update *src/main/java/com/example/fabrikam/TodoDemoController.java* met een regel in Hallo `updateTodo` methode tooset Hallo tijdstempel:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Ondersteuning voor het nieuwe veld Hallo in Hallo Thymeleaf sjabloon toevoegen. Update *src/main/resources/templates/index.html* met een nieuwe tabel-header voor Hallo tijdstempel, en een nieuwe toodisplay Hallo veldwaarde van Hallo tijdstempel in elke tabel gegevensrij.

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. Hallo-toepassing bouwen:

    ```bash
    mvnw clean package 
    ```

6. FTP-hello bijgewerkt. WAR als voorheen kunt verwijderen van bestaande Hallo *site/wwwroot/webapps/ROOT* directory en *ROOT.war*, en vervolgens uploaden Hallo bijgewerkt. WAR-bestand als ROOT.war. 

Wanneer u Hallo-app vernieuwen een **Aanmaaktijd** kolom nu zichtbaar is. Wanneer u een nieuwe taak toevoegt, wordt app Hallo Hallo tijdstempel automatisch gevuld. Uw bestaande taken blijven ongewijzigd en werken met Hallo app Hoewel Hallo onderliggende gegevensmodel is gewijzigd. 

![Java-app bijgewerkt met een nieuwe kolom](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Diagnostische logboeken 

Als uw Java-toepassing in Azure App Service wordt uitgevoerd, kunt u de console Hallo opvragen logboeken doorgesluisd rechtstreeks tooyour terminal. Op die manier kunt u Hallo dezelfde diagnostische ontvangt toohelp foutopsporing van toepassingsfouten.

toostart logboek streaming gebruik Hallo [az webapp logboek tail](/cli/azure/appservice/web/log#tail) opdracht.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Uw Azure-web-app beheren

Ga toohello Azure portal toosee Hallo web-app die u hebt gemaakt.

toodo dit te melden[https://portal.azure.com](https://portal.azure.com).

In het linkermenu hello, klikt u op **App Service**, klikt u op Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-java-mysql/access-portal.png)

Standaard ziet u uw web-app-blade Hallo **overzicht** pagina. Deze pagina geeft u een overzicht van hoe uw app presteert. U kunt hier ook beheertaken zoals stoppen, starten, opnieuw opstarten en verwijderen uitvoeren. Hallo tabbladen aan de linkerkant Hallo van Hallo blade bevatten Hallo verschillende configuratiepagina's die u kunt openen.

![App Service-blade in Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Deze tabbladen Hallo blade bevatten Hallo vele handige functies u tooyour web-app kunt toevoegen. Hallo na lijst hebt u slechts een paar van Hallo mogelijkheden:
* Een aangepaste DNS-naam toewijzen
* Een aangepast SSL-certificaat binden
* Continue implementatie inschakelen
* Omhoog en omlaag schalen
* Gebruikersverificatie toevoegen

## <a name="clean-up-resources"></a>Resources opschonen

Als u deze resources niet voor een andere zelfstudie hoeft (Zie [Vervolgstappen](#next)), kunt u ze verwijderen door het uitvoeren van de volgende opdracht Hallo: 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Volgende stappen

> [!div class="checklist"]
> * Een MySQL-database maken in Azure
> * Verbinding maken met een steekproef Java app toohello MySQL
> * Hallo app tooAzure implementeren
> * Bijwerken en het Hallo-app implementeren
> * Diagnostische logboeken van de stroom van Azure
> * Hallo-app in hello Azure-portal beheren

De volgende zelfstudie toolearn toohello gaan hoe een aangepaste DNS-server toomap toohello app name.

> [!div class="nextstepaction"] 
> [Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md)
