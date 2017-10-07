---
title: aaaSync inhoud van een map tooAzure voor cloud-App Service
description: Meer informatie over hoe toodeploy uw app tooAzure App Service via inhoud synchroniseren vanuit een map van de cloud.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 88d3a670-303a-4fa2-9de9-715cc904acec
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: e1c6d53a427c36126d9cdb33cc21b4126b9d9c2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="sync-content-from-a-cloud-folder-tooazure-app-service"></a>Synchronisatie-inhoud van een map tooAzure voor cloud-App Service
Deze zelfstudie leert u hoe toodeploy te[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) door het synchroniseren van uw inhoud van de opslagservices populaire cloudtoepassingen zoals Dropbox en OneDrive. 

## <a name="overview"></a>Overzicht van de implementatie van inhoud synchroniseren
Hallo inhoud op aanvraag-sync-implementatie wordt aangedreven door Hallo [implementatie-engine Kudu](https://github.com/projectkudu/kudu/wiki) geïntegreerd met App Service. In Hallo [Azure Portal](https://portal.azure.com), kunt u een map in de cloudopslag, werken met uw app-code en de inhoud in de map en sync tooApp Service Hello op een knop. Inhoud synchronisatie maakt gebruik van Hallo Kudu proces voor het bouwen en uitvoeren. 

## <a name="contentsync"></a>Hoe tooenable inhoud implementatie synchroniseren
tooenable inhoud synchroniseren vanuit Hallo [Azure Portal](https://portal.azure.com), als volgt te werk:

1. Klik in de blade van uw app in Azure Portal Hallo op **instellingen** > **Implementatiebron**. Klik op **bron kiezen**, selecteer daarna **OneDrive** of **Dropbox** als Hallo bron voor de implementatie. 
   
    ![Inhoud synchroniseren](./media/app-service-deploy-content-sync/deployment_source.png)
   
   > [!NOTE]
   > Vanwege onderliggende verschillen in Hallo-API's, **OneDrive voor bedrijven** wordt niet ondersteund op dit moment. 
   > 
   > 
2. Volledige Hallo autorisatie werkstroom tooenable tooaccess App Service een specifieke vooraf gedefinieerde opgegeven pad voor OneDrive of Dropbox waarin alle inhoud van de App Service wordt opgeslagen.  
    Hallo optie toocreate een map met inhoud onder Hallo aangewezen na autorisatie Hallo App Service-platform u krijgt, het pad naar inhoud of een bestaande map met inhoud onder deze aangewezen Inhoudspad toochoose. paden naar inhoud in uw cloud-opslag-accounts die worden gebruikt voor synchronisatie van App Service Hallo aangewezen zijn Hallo volgende:  
   
   * **OneDrive**:`Apps\Azure Web Apps` 
   * **Dropbox**:`Dropbox\Apps\Azure`
3. Na Hallo kan de initiële synchronisatie van de inhoud Hallo inhoud synchronisatie worden gestart op verzoek via hello Azure-portal. Geschiedenis van implementatie is beschikbaar met Hallo **implementaties** blade.
   
    ![Implementatiegeschiedenis](./media/app-service-deploy-content-sync/onedrive_sync.png)

Meer informatie voor de implementatie van Dropbox vindt onder [implementeren van Dropbox](http://blogs.msdn.com/b/windowsazure/archive/2013/03/19/new-deploy-to-windows-azure-web-sites-from-dropbox.aspx). 

