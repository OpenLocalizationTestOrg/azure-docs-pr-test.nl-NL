---
title: aaaManaging rollen in Azure cloud services met Visual Studio | Microsoft Docs
description: Meer informatie over hoe tooadd en verwijderen van rollen in Azure cloud services met Visual Studio.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5ec9ae2e-8579-4e5d-999e-8ae05b629bd1
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 131edc534d1110ba3d25cd00a3a24b643576875c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-roles-in-azure-cloud-services-with-visual-studio"></a>Het beheren van rollen in Azure cloudservices met Visual Studio
Nadat u uw Azure-cloud-service hebt gemaakt, kunt u nieuwe functies tooit toevoegen of verwijderen van bestaande rollen uit. U kunt ook een bestaand project importeren en converteert u deze rol tooa. U kunt bijvoorbeeld een ASP.NET-webtoepassing importeren en opgeven dat het een Webrol.

## <a name="adding-a-role-tooan-azure-cloud-service"></a>Toevoegen van een rol tooan Azure-cloudservice
Hallo stappen volgen helpt u bij het toevoegen van een web- of worker-rol tooan Azure cloud service-project in Visual Studio.

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, Hallo projectknooppunt uitvouwen

1. Klik met de rechtermuisknop Hallo **rollen** knooppunt toodisplay Hallo contextmenu. Selecteer in het contextmenu hello, **toevoegen**, selecteer vervolgens een bestaande Webrol of functie worker uit de huidige oplossing hello of een web- of worker-rol-project maken. Ook kunt u een juiste project, zoals een ASP.NET-toepassing-webproject selecteren en deze koppelen aan een rolproject.

    ![Menu Opties tooadd een rol tooan Azure cloud service-project](media/vs-azure-tools-cloud-service-project-managing-roles/add-role.png)

## <a name="removing-a-role-from-an-azure-cloud-service"></a>Een rol verwijderen uit een Azure cloudservice
Hallo volgende stappen begeleiden u bij een web- of worker-rol verwijderen uit een Azure-cloud service-project in Visual Studio.

1. Maak of open een Azure-cloud service-project in Visual Studio.

1. In **Solution Explorer**, Hallo projectknooppunt uitvouwen

1. Vouw Hallo **rollen** knooppunt.

1. Klik met de rechtermuisknop Hallo knooppunt u wilt tooremove en, in het contextmenu hello, selecteer **verwijderen**. 

    ![Menu Opties tooadd een rol tooan Azure-cloudservice](media/vs-azure-tools-cloud-service-project-managing-roles/remove-role.png)

## <a name="readding-a-role-tooan-azure-cloud-service-project"></a>Een rol tooan Azure cloud service-project readding
Als u een rol verwijderen uit uw cloudserviceproject maar later besluit tooadd Hallo-functie weer toohello project alleen Hallo rol declaratie- en basic kenmerken, zoals eindpunten en diagnostische gegevens, worden toegevoegd. Er is geen aanvullende resources of de verwijzingen worden toegevoegd toohello `ServiceDefinition.csdef` bestand of toohello `ServiceConfiguration.cscfg` bestand. Als u deze informatie tooadd wilt, moet u toomanually terug naar deze bestanden toe te voegen.

Bijvoorbeeld, u mogelijk een Webrol service verwijdert en later besluit van deze rol back tooadd in uw oplossing. Als u dit doet, treedt er een fout op. tooprevent deze fout, hebt u tooadd hello `<LocalResources>` element wordt weergegeven in volgende Hallo XML weer naar Hallo `ServiceDefinition.csdef` bestand. Gebruik de naam van de Hallo van Hallo-webservicerol die u hebt toegevoegd Hallo project als onderdeel van het naamkenmerk Hallo voor Hallo  **<LocalStorage>**  element. In dit voorbeeld is de naam van de Hallo van Hallo-webservicerol **WCFServiceWebRole1**.

    <WebRole name="WCFServiceWebRole1">
        <Sites>
          <Site name="Web">
            <Bindings>
              <Binding name="Endpoint1" endpointName="Endpoint1" />
            </Bindings>
          </Site>
        </Sites>
        <Endpoints>
          <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
          <Import moduleName="Diagnostics" />
        </Imports>
       <LocalResources>
          <LocalStorage name="WCFServiceWebRole1.svclog" sizeInMB="1000" cleanOnRoleRecycle="false" />
       </LocalResources>
    </WebRole>

## <a name="next-steps"></a>Volgende stappen
- [Hallo rollen configureert voor een Azure-cloudservice met Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md)
