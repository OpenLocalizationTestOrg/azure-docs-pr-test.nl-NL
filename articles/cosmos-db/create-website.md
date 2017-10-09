---
title: een web-app met een sjabloon - Azure Cosmos DB aaaDeploy | Microsoft Docs
description: Meer informatie over hoe toodeploy een Cosmos-DB Azure-account, Azure App Service Web Apps en een voorbeeld van een webtoepassing met een Azure Resource Manager-sjabloon.
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>Azure Cosmos DB en Azure App Service Web Apps met een Azure Resource Manager-sjabloon implementeren
Deze zelfstudie leert u hoe een Azure Resource Manager-sjabloon toodeploy toouse en integreren [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), een [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) WebApp en een Voorbeeldwebtoepassing.

Met Azure Resource Manager-sjablonen, kunt u eenvoudig automatiseren Hallo-implementatie en configuratie van uw Azure-resources.  Deze zelfstudie laat zien hoe toodeploy een webtoepassing en Azure DB die Cosmos-accountgegevens verbinding automatisch worden geconfigureerd.

Na het voltooien van deze zelfstudie, kunt u zich kunt tooanswer Hallo vragen te volgen:  

* Hoe kan ik een Azure Resource Manager-sjabloon toodeploy en integreren van een Azure DB die Cosmos-account en een web-app in Azure App Service?
* Hoe kan ik een Azure Resource Manager-sjabloon toodeploy en integratie van een account voor Azure Cosmos DB, een web-app in App Service Web Apps en Web Deploy-toepassing?

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>Vereisten
> [!TIP]
> Tijdens deze zelfstudie wordt niet vanuit gegaan ervaring met Azure Resource Manager-sjablonen of JSON, indien u wenst toomodify Hallo waarnaar wordt verwezen sjablonen of implementatie-opties en klik vervolgens kennis van elk van deze gebieden zijn vereist.
> 
> 

Zorg ervoor dat u de volgende Hallo hebt voordat Hallo-instructies in deze zelfstudie:

* Een Azure-abonnement. Azure is een platform op basis van abonnement.  Zie voor meer informatie over het verkrijgen van een abonnement [koopopties](https://azure.microsoft.com/pricing/purchase-options/), [lid biedt](https://azure.microsoft.com/pricing/member-offers/), of [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).

## <a id="CreateDB"></a>Stap 1: Download de sjabloonbestanden Hallo
Downloaden van de sjabloonbestanden hello we in deze zelfstudie gebruiken begint.

1. Hallo downloaden [een account voor Azure Cosmos DB, Web-Apps maken en implementeren van een voorbeeld van een toepassing demo](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json) sjabloon tooa lokale map (bijvoorbeeld C:\Azure Cosmos DBTemplates). Deze sjabloon wordt een Azure DB die Cosmos-account, een App Service-web-app en een webtoepassing implementeren.  Deze configureert ook automatisch Hallo web application tooconnect toohello Azure Cosmos DB account.
2. Hallo downloaden [maken van een Azure DB die Cosmos-account en een voorbeeld van de Web-Apps](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json) sjabloon tooa lokale map (bijvoorbeeld C:\Azure Cosmos DBTemplates). Deze sjabloon implementeert u een account voor Azure Cosmos DB, een App Service web-app en Hallo-site-instellingen tooeasily water Azure Cosmos DB verbinding toepassingsinformatie wordt wijzigen, maar bevat geen een webtoepassing.  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>Stap 2: Implementeer hello Azure DB die Cosmos-account App Service web app en demo toepassing voorbeeld
Nu gaan we onze eerste sjabloon te implementeren.

> [!TIP]
> Hallo-sjabloon wordt niet gevalideerd Hallo web-appnaam en de naam van Azure DB die Cosmos ingevoerd onder een) geldig en b) beschikbaar zijn.  Het is raadzaam dat u controleert of Hallo beschikbaarheid van Hallo namen die u hebt toosupply voorafgaande toosubmitting Hallo-implementatie plannen.
> 
> 

1. Aanmelding toohello [Azure Portal](https://portal.azure.com), klikt u op Nieuw en zoek naar 'Sjabloonimplementatie'.
    ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment1.png)
2. Hallo sjabloon implementatie item te selecteren en klik op **maken** ![schermafbeelding van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment2.png)
3. Klik op **template bewerken**, plak de inhoud Hallo van Hallo DocDBWebsiteTodo.json sjabloonbestand en klikt u op **opslaan**.
   ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment3.png)
4. Klik op **parameters bewerken**waarden opgeven voor elk van de verplichte parameters Hallo en klikt u op **OK**.  Hallo-parameters zijn als volgt:
   
   1. SITENAAM: Hallo App Service web-appnaam geeft en gebruikte tooconstruct Hallo-URL die u tooaccess Hallo web-app gebruikt (bijvoorbeeld als u 'mydemodocdbwebapp' opgeeft, wordt de Hallo-URL waarmee u toegang hebben tot Hallo web-app mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Geeft de naam Hallo van App Service plan toocreate hosten.
   3. LOCATIE: Hiermee geeft u op Hallo van Azure-locatie in welke toocreate hello Azure Cosmos DB en web-app bronnen.
   4. DATABASEACCOUNTNAME: Geeft de naam Hallo van hello Azure Cosmos DB account toocreate.   
      
      ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment4.png)
5. Kies een bestaande resourcegroep of geef een naam toomake een nieuwe resourcegroep en kies een locatie voor resourcegroep Hallo.

    ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment5.png)
6. Klik op **juridische voorwaarden bekijken**, **aankoop**, en klik vervolgens op **maken** toobegin Hallo-implementatie.  Selecteer **pincode toodashboard** zodat de resulterende implementatie Hallo gemakkelijk zichtbaar zijn op uw startpagina van Azure portal.
   ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment6.png)
7. Wanneer het Hallo-implementatie is voltooid, wordt Hallo resourcegroepblade geopend.
   ![Schermopname van Hallo resourcegroepblade](./media/create-website/TemplateDeployment7.png)  
8. toouse toepassing hello, navigeert u gewoon toohello web-app-URL (Hallo bovenstaande voorbeeld Hallo URL zouden zijn http://mydemodocdbwebapp.azurewebsites.net).  Hier ziet u Hallo webtoepassing te volgen:
   
   ![Todo-voorbeeldtoepassing](./media/create-website/image2.png)
9. Opwekken en maken van een aantal taken in Hallo web-app en ga daarna terug toohello resourcegroepblade in hello Azure-portal. Klik op Hallo Azure Cosmos DB account resource in de lijst met Resources van Hallo en klik vervolgens op **Queryverkenner**.
    ![Schermopname van Hallo samenvatting lens met web-app Hallo gemarkeerd](./media/create-website/TemplateDeployment8.png)  
10. Hallo standaardquery uitvoert, ' Selecteer * van c ' en Hallo resultaten controleren.  U ziet dat deze query Hallo Hallo JSON-weergave van Hallo todo-items die u hebt gemaakt in stap 7 bovenstaande is opgehaald.  U kunt gratis tooexperiment met query's. Probeer bijvoorbeeld uitgevoerd Selecteer * in c WHERE c.isComplete = true tooreturn alle todo-items die zijn gemarkeerd als voltooid.
    
    ![Schermopname van Hallo Queryverkenner en resultaten blades met Hallo queryresultaten](./media/create-website/image5.png)
11. Gratis tooexplore hello Azure Cosmos DB portal ervaring van mening bent dat of de voorbeeldtoepassing Todo Hallo wijzigen.  Wanneer u klaar bent, gaan we een andere sjabloon te implementeren.

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>Stap 3: Hallo Document account en voorbeeld van web-app implementeren
Nu gaan we onze tweede sjabloon te implementeren.  Deze sjabloon is nuttig tooshow hoe u kunt invoeren Azure Cosmos DB-verbindingsgegevens zoals account eindpunt en de hoofdsleutel in een web-app als toepassingsinstellingen of als een aangepaste verbindingsreeks. Bijvoorbeeld, misschien hebt u uw eigen webtoepassing dat u wilt toodeploy met een Azure DB die Cosmos-account en Hallo verbindingsgegevens automatisch ingevuld tijdens de implementatie hebben.

> [!TIP]
> Hallo-sjabloon wordt niet gevalideerd Hallo web-appnaam en de naam van Azure DB die Cosmos ingevoerd onder een) geldig en b) beschikbaar zijn.  Het is raadzaam dat u controleert of Hallo beschikbaarheid van Hallo namen die u hebt toosupply voorafgaande toosubmitting Hallo-implementatie plannen.
> 
> 

1. In Hallo [Azure Portal](https://portal.azure.com), klikt u op Nieuw en zoek naar 'Sjabloonimplementatie'.
    ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment1.png)
2. Hallo sjabloon implementatie item te selecteren en klik op **maken** ![schermafbeelding van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment2.png)
3. Klik op **template bewerken**, plak de inhoud Hallo van Hallo DocDBWebSite.json sjabloonbestand en klikt u op **opslaan**.
   ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment3.png)
4. Klik op **parameters bewerken**waarden opgeven voor elk van de verplichte parameters Hallo en klikt u op **OK**.  Hallo-parameters zijn als volgt:
   
   1. SITENAAM: Hallo App Service web-appnaam geeft en gebruikte tooconstruct Hallo-URL die u tooaccess Hallo web-app gebruikt (bijvoorbeeld als u 'mydemodocdbwebapp' opgeeft, wordt de Hallo-URL waarmee u toegang hebben tot Hallo web-app mydemodocdbwebapp.azurewebsites.NET).
   2. HOSTINGPLANNAME: Geeft de naam Hallo van App Service plan toocreate hosten.
   3. LOCATIE: Hiermee geeft u op Hallo van Azure-locatie in welke toocreate hello Azure Cosmos DB en web-app bronnen.
   4. DATABASEACCOUNTNAME: Geeft de naam Hallo van hello Azure Cosmos DB account toocreate.   
      
      ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment4.png)
5. Kies een bestaande resourcegroep of geef een naam toomake een nieuwe resourcegroep en kies een locatie voor resourcegroep Hallo.

    ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment5.png)
6. Klik op **juridische voorwaarden bekijken**, **aankoop**, en klik vervolgens op **maken** toobegin Hallo-implementatie.  Selecteer **pincode toodashboard** zodat de resulterende implementatie Hallo gemakkelijk zichtbaar zijn op uw startpagina van Azure portal.
   ![Schermopname van sjabloonimplementatie Hallo gebruikersinterface](./media/create-website/TemplateDeployment6.png)
7. Wanneer het Hallo-implementatie is voltooid, wordt Hallo resourcegroepblade geopend.
   ![Schermopname van Hallo resourcegroepblade](./media/create-website/TemplateDeployment7.png)  
8. Klik op Hallo Web-App resource in de lijst met Resources van Hallo en klik vervolgens op **toepassingsinstellingen** ![schermafbeelding van de resourcegroep Hallo](./media/create-website/TemplateDeployment9.png)  
9. Houd er rekening mee hoe er toepassingsinstellingen voor hello Azure Cosmos DB eindpunt en elke hello Azure Cosmos DB hoofdsleutels aanwezig zijn.

    ![Schermopname van toepassingsinstellingen](./media/create-website/TemplateDeployment10.png)  
10. Kunt u gratis toocontinue verkennen hello Azure Portal of voert u een van onze Cosmos Azure DB [voorbeelden](http://go.microsoft.com/fwlink/?LinkID=402386) toocreate uw eigen Azure DB die Cosmos-toepassing.

<a name="NextSteps"></a>

## <a name="next-steps"></a>Volgende stappen
Gefeliciteerd. U kunt Azure Cosmos DB App Service-web-app en een Voorbeeldwebtoepassing met behulp van Azure Resource Manager-sjablonen hebt geïmplementeerd.

* toolearn meer informatie over Azure Cosmos DB, klikt u op [hier](http://azure.com/docdb).
* toolearn meer informatie over Azure App Service Web apps, klikt u op [hier](http://go.microsoft.com/fwlink/?LinkId=325362).
* toolearn meer informatie over Azure Resource Manager-sjablonen, klikt u op [hier](https://msdn.microsoft.com/library/azure/dn790549.aspx).

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)
* Zie voor een handleiding toohello wijziging van Hallo oude portal toohello nieuwe portal: [verwijzing voor het navigeren Hallo klassieke Azure-Portal](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](http://go.microsoft.com/fwlink/?LinkId=523751), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

