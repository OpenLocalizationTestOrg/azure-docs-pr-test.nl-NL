---
title: aaaInstall On-premises gegevensgateway | Microsoft Docs
description: Meer informatie over hoe tooinstall en configureer een On-premises data gateway.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Installeren en configureren van een lokale gegevensgateway
Een lokale gegevensgateway is vereist wanneer een of meer Azure Analysis Services-servers in Hallo dezelfde regio verbinding tooon-premises gegevensbronnen. toolearn meer informatie over het Hallo-gateway, Zie [On-premises gegevensgateway](analysis-services-gateway.md).

## <a name="prerequisites"></a>Vereisten
**Minimale vereisten:**

* .NET 4.5 framework
* 64-bits versie van Windows 7 / Windows Server 2008 R2 (of hoger)

**Aanbevolen:**

* 8-core CPU
* 8 GB geheugen
* 64-bits versie van Windows 2012 R2 (of hoger)

**Belangrijke overwegingen:**

* Tijdens de installatie bij het registreren van uw gateway met Azure, is Hallo standaard regio voor uw abonnement geselecteerd. U kunt een andere regio. Als u servers in meer dan één regio hebt, moet u een gateway voor elke regio. 
* Hallo-gateway kan niet worden geïnstalleerd op een domeincontroller.
* Slechts één gateway kan worden geïnstalleerd op een enkele computer.
* Hallo-gateway installeren op een computer die op blijft en toosleep niet verder.
* Installeer geen Hallo-gateway op een computer tooyour draadloos verbonden netwerk. Prestaties kan afnemen.


## <a name="download"></a>Downloaden
 [Hallo gateway downloaden](https://aka.ms/azureasgateway)

## <a name="install"></a>Installeren

1. Voer de installatie.

2. Selecteer een locatie en klik vervolgens op Hallo voorwaarden accepteren **installeren**.

   ![Installeren van de locatie en de licentievoorwaarden](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Selecteer **On-premises gegevensgateway (aanbevolen)**. Azure Analysis Services biedt geen ondersteuning voor persoonlijke modus.

   ![Kies het type gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Geef een account toosign in tooAzure. Hallo-account moet zich in uw tenant Azure Active Directory. Dit account wordt gebruikt voor het Hallo-gatewaybeheerder. 

   ![Geef een account toosign in tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Als u zich met een domeinaccount aanmeldt, moeten worden toegewezen tooyour organisatieaccount in Azure AD. Account van uw organisatie wordt gebruikt als Hallo Hallo gatewaybeheerder.

## <a name="register"></a>Registreren
In de volgorde toocreate een bron van de gateway in Azure, moet u Hallo lokaal exemplaar die u geïnstalleerd met Hallo Gateway Cloud Service registreren. 

1.  Selecteer **registreren van een nieuwe gateway op deze computer**.

    ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Typ een naam en herstel de sleutel voor uw gateway. Hallo-gateway gebruikt standaard standaardwaarde regio van uw abonnement. Als u een andere regio tooselect nodig hebt, selecteert u **wijziging regio**.

   ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Een Azure-gateway-resource maken
Nadat u hebt geïnstalleerd en uw gateway is geregistreerd, moet u een gateway-resource toocreate in uw Azure-abonnement. Meld u aan tooAzure Hello dezelfde account die u hebt gebruikt bij het registreren van Hallo-gateway.

1. Klik in de Azure-portal op **een nieuwe service maken** > **Enterprise Integration** > **On-premises gegevensgateway** > **maken**.

   ![Een gateway-resource maken](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. In **verbinding-gateway maken**, voer de volgende instellingen:

    * **Naam**: Voer een naam voor uw gateway-resource. 

    * **Abonnement**: Selecteer Hallo tooassociate Azure-abonnement met uw gateway-resource. 
    Dit abonnement moet hetzelfde abonnement uw servers bevinden zich in Hallo.
   
      Hallo standaardabonnement is gebaseerd op Hallo Azure-account waarmee u toosign in.

    * **Resourcegroep**: maak een resourcegroep of selecteer een bestaande resourcegroep.

    * **Locatie**: Selecteer Hallo regio geregistreerd van uw gateway in.

    * **De naam van de installatie**: als uw gateway-installatie niet is geselecteerd, selecteer Hallo gateway is geregistreerd. 

    Wanneer u bent klaar, klikt u op **maken**.

## <a name="connect-servers"></a>Verbinding maken met servers toohello gateway resource

1. Klik in het overzicht Azure Analysis Services-server op **On-Premises Data Gateway**.

   ![Verbinding maken met server toogateway](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. In **kiezen van een On-Premises Data Gateway tooconnect**, selecteer uw gateway-resource en klik vervolgens op **verbinding maken met geselecteerde gatewayapparaat**.

   ![Verbinding maken met server toogateway-bron](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Als uw gateway niet wordt weergegeven in de lijst hello, uw server is waarschijnlijk niet in dezelfde regio bevinden als het Hallo-regio die u hebt opgegeven bij het registreren van de gateway Hallo Hallo. 

Dat is alles. Als tooopen poorten of u problemen oplost, moet u ervoor toocheck uit [On-premises gegevensgateway](analysis-services-gateway.md).

## <a name="next-steps"></a>Volgende stappen
* [Analyseservices beheren](analysis-services-manage.md)   
* [Gegevens ophalen uit Azure Analysis Services](analysis-services-connect.md)
