---
title: aaaLocal Git-implementatie tooAzure App Service
description: Meer informatie over hoe tooenable lokale Git-implementatie tooAzure App Service.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a>Lokale Git-implementatie tooAzure App Service
Deze zelfstudie leert u hoe toodeploy uw app te[Azure App Service] van een Git-opslagplaats op uw lokale computer. App Service biedt ondersteuning voor deze benadering Hello **lokale Git** Implementatieoptie in Hallo [Azure Portal].  
Veel van Hallo Git-opdrachten die worden beschreven in dit artikel worden automatisch uitgevoerd tijdens het maken van een App Service-app met behulp van Hallo [Azure-opdrachtregelinterface] zoals beschreven [hier](app-service-web-get-started.md).

## <a name="prerequisites"></a>Vereisten
toocomplete deze zelfstudie hebt u nodig:

* GIT. U kunt downloaden Hallo installatie binaire [hier](http://www.git-scm.com/downloads).  
* Basiskennis van Git.
* Een Microsoft Azure-account. Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.  
> 
> 

## <a name="Step1"></a>Stap 1: Maak een lokale opslagplaats
Voer Hallo taken toocreate nieuwe Git-opslagplaats te volgen.

1. Start een opdrachtregelprogramma, zoals **GitBash** (Windows) of **Bash** (Unix-Shell). U kunt op OS X-systemen Hallo opdrachtregelprogramma benaderen via Hallo **Terminal** toepassing.
2. Navigeer toohello directory waar de inhoud toodeploy Hallo geplaatst worden.
3. Gebruik Hallo opdracht tooinitialize nieuwe Git-opslagplaats te volgen:

```bash  
git init
```

## <a name="Step2"></a>Stap 2: Uw inhoud doorvoeren
App Service biedt ondersteuning voor toepassingen die zijn gemaakt in diverse programmeertalen. 

1. Als uw opslagplaats al inhoud overslaan dit punt bevat en toopoint 2 hieronder verplaatsen wordt weergegeven. Als uw opslagplaats geen inhoud gewoon bevat nog te vullen met een statische HTML-bestand als volgt: 
   
   * Start een teksteditor en maak een nieuw bestand met de naam **index.html** in de hoofdmap Hallo van Hallo Git-opslagplaats
   * Hallo na tekst hello inhoud voor Hallo index.html bestand en slaat u deze toevoegen: *Hallo Git!*
2. Vanaf de opdrachtregel hello, controleert u of u onder Hallo hoofdmap van de Git-opslagplaats. Gebruik vervolgens de volgende opdracht tooadd bestanden tooyour opslagplaats Hallo:

```bash  
git add -A
```
3. Vervolgens doorvoeren Hallo wijzigingen toohello opslagplaats met behulp van de volgende opdracht Hallo:

```bash  
git commit -m "Hello Azure App Service"
```  

## <a name="Step3"></a>Stap 3: Schakel Hallo App Service-app-opslagplaats
Hallo te volgen stappen tooenable een Git-opslagplaats voor uw App Service-app uitvoeren.

1. Meld u bij toohello [Azure Portal].
2. Klik op de blade van uw App Service-app **instellingen > implementatiebron**. Klik op **bron kiezen**, klikt u vervolgens op **lokale Git-opslagplaats**, en klik vervolgens op **OK**.  
   
    ![Lokale Git-opslagplaats](./media/app-service-deploy-local-git/local_git_selection.png)
3. Als dit de eerste keer instellen van een opslagplaats in Azure, moet u de aanmeldingsreferenties toocreate voor deze. U gebruikt deze toolog in hello Azure-opslagplaats en wijzigingen van uw lokale Git-opslagplaats. Op de blade van uw app, klikt u op **instellingen > implementatiereferenties**, configureert u uw implementatie gebruikersnaam en wachtwoord. Wanneer u bent klaar, klikt u op **opslaan**.
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <a name="Step4"></a>Stap 4: Implementeer uw project
Hallo toopublish stappen na de tooApp van uw app Service met lokale Git gebruiken.

1. Klik in de blade van uw app in Azure Portal Hallo op **instellingen > eigenschappen** voor Hallo **Git-URL**.
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    **GIT-URL** Hallo externe verwijzing toodeploy toofrom is uw lokale opslagplaats. U gebruikt deze URL in Hallo stappen te volgen.
2. Hallo opdrachtregelprogramma gebruikt, controleert u of u in de hoofdmap Hallo van uw lokale Git-opslagplaats.
3. Gebruik `git remote` tooadd Hallo externe verwijzing die worden vermeld in **Git-URL** uit stap 1. De opdracht ziet er vergelijkbare toohello volgende:
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > Hallo **externe** opdracht voegt een benoemde verwijzing tooa externe opslagplaats. In dit voorbeeld wordt een verwijzing met de naam 'azure' voor uw web-app-opslagplaats gemaakt.
   > 
   > 
4. Uw inhoud tooApp Service push met Hallo nieuwe **azure** externe u zojuist hebt gemaakt.

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. Ga terug in Azure Portal Hallo tooyour app. Een logboekvermelding van de meest recente push moet worden weergegeven in Hallo **implementaties** blade. 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. Klik op Hallo **Bladeren** knop Hallo boven aan het Hallo-app blade tooverify Hallo inhoud is geïmplementeerd. 

## <a name="Step5"></a>Problemen oplossen
Hallo volgen fouten of problemen meestal opgetreden bij het gebruik van Git toopublish tooan App Service-app in Azure:

- - -
**Symptoom**: kan geen tooaccess [siteURL]: tooconnect te is mislukt [scmAddress]

**Oorzaak**: deze fout kan optreden als het Hallo-app niet actief is.

**Resolutie**: begin Hallo-app in hello Azure-Portal. GIT-implementatie werkt niet, tenzij het Hallo-app wordt uitgevoerd. 

- - -
**Symptoom**: host 'naam' niet oplossen

**Oorzaak**: deze fout kan optreden als de adresgegevens Hallo ingevoerd bij het maken van Hallo 'azure' externe is onjuist.

**Resolutie**: gebruik Hallo `git remote -v` opdracht toolist alle afstandsbedieningen, samen met de URL van de Hallo die zijn gekoppeld. Controleer of Hallo-URL voor Hallo 'azure' externe klopt. Indien nodig, verwijderen en maak dit externe met behulp van de juiste URL Hallo.

- - -
**Symptoom**: Er is geen refs in algemene en er is geen opgegeven; niets te doen. Mogelijk moet u een vertakking zoals 'master' opgeven.

**Oorzaak**: deze fout kan optreden als u geen een vertakking opgeven wanneer u een git push-bewerking uitvoert, en er geen set Hallo push.default waarde die wordt gebruikt door Git.

**Resolutie**: Hallo push-bewerking opnieuw uitvoeren Hallo hoofdvertakking opgeven. Bijvoorbeeld:

```bash  
git push azure master
```
- - -
**Symptoom**: src refspec [branchname] komt niet overeen.

**Oorzaak**: deze fout kan optreden als u toopush tooa vertakking dan master op Hallo 'azure' externe probeert.

**Resolutie**: Hallo push-bewerking opnieuw uitvoeren Hallo hoofdvertakking opgeven. Bijvoorbeeld:

```bash  
git push azure master
```
- - -
**Symptoom**: RPC is mislukt; resulteren = 22, HTTP-code = 502.

**Oorzaak**: deze fout kan optreden als u een groot git-opslagplaats toopush via HTTPS probeert.

**Resolutie**: Hallo git-configuratie wijzigen op Hallo lokale machine toomake Hallo postBuffer groter

```bash  
git config --global http.postBuffer 524288000
```
- - -
**Symptoom**: fout - wijzigingen doorgevoerd tooremote opslagplaats maar uw web-app niet bijgewerkt.

**Oorzaak**: deze fout kan optreden als u een Node.js-app met een package.json-bestand waarin aanvullende vereiste modules implementeert.

**Resolutie**: aanvullende berichten met 'npm ERR!' moet aangemelde voorafgaande toothis fout en aanvullende context kan bieden bij Hallo-fout. Hallo Hieronder volgen bekende oorzaken van deze fout en bijbehorende 'npm ERR!' Hallo Bericht:

* **Ongeldige package.json-bestand**: npm ERR! Afhankelijkheden kan niet worden gelezen.
* **Systeemeigen module die geen heeft een binaire distributiepunt voor Windows**:
  
  * npm ERR! \`cmd '/ c"'knooppunt gyp rebuild'\` is mislukt: 1
    
      OF
  * npm ERR! [modulename@version] vooraf: \`zorg || gmake\`

## <a name="additional-resources"></a>Aanvullende resources
* [Git-documentatie](http://git-scm.com/documentation)
* [Project Kudu documentatie](https://github.com/projectkudu/kudu/wiki)
* [Continue implementatie tooAzure App Service](app-service-continuous-deployment.md)
* [Hoe toouse PowerShell voor Azure](/powershell/azure/overview)
* [Hoe toouse hello Azure-opdrachtregelinterface](../cli-install-nodejs.md)

[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Azure Portal]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Azure-opdrachtregelinterface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
