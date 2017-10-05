---
title: On-premises gegevensgateway installeren | Microsoft Docs
description: Informatie over het installeren en configureren van een On-premises data gateway.
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
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a>Installeren en configureren van een lokale gegevensgateway
Een lokale gegevensgateway is vereist wanneer een of meer Azure Analysis Services-servers in dezelfde regio verbinding met on-premises gegevensbronnen maken. Zie voor meer informatie over de gateway, [On-premises gegevensgateway](analysis-services-gateway.md).

## <a name="prerequisites"></a>Vereisten
**Minimale vereisten:**

* .NET 4.5 framework
* 64-bits versie van Windows 7 / Windows Server 2008 R2 (of hoger)

**Aanbevolen:**

* 8-core CPU
* 8 GB geheugen
* 64-bits versie van Windows 2012 R2 (of hoger)

**Belangrijke overwegingen:**

* Tijdens de installatie bij het registreren van uw gateway met Azure, is de standaardregio voor uw abonnement geselecteerd. U kunt een andere regio. Als u servers in meer dan één regio hebt, moet u een gateway voor elke regio. 
* De gateway kan niet worden geïnstalleerd op een domeincontroller.
* Slechts één gateway kan worden geïnstalleerd op een enkele computer.
* De gateway installeren op een computer waarop blijft op en gaat niet naar de slaapstand.
* Installeer de gateway niet op een computer draadloos verbonden met uw netwerk. Prestaties kan afnemen.


## <a name="download"></a>Downloaden
 [De gateway downloaden](https://aka.ms/azureasgateway)

## <a name="install"></a>Installeren

1. Voer de installatie.

2. Selecteer een locatie en klik vervolgens op de voorwaarden accepteren **installeren**.

   ![Installeren van de locatie en de licentievoorwaarden](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. Selecteer **On-premises gegevensgateway (aanbevolen)**. Azure Analysis Services biedt geen ondersteuning voor persoonlijke modus.

   ![Kies het type gateway](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. Geef een account aan te melden bij Azure. De account moet zich in uw tenant Azure Active Directory. Dit account wordt gebruikt voor de gatewaybeheerder. 

   ![Geef een account aan te melden bij Azure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > Als u zich met een domeinaccount aanmeldt, worden deze toegewezen aan uw organisatieaccount in Azure AD. Account van uw organisatie worden gebruikt als de beheerder van de gateway.

## <a name="register"></a>Registreren
Om een gateway-resource maken in Azure, moet u het lokale exemplaar dat u hebt geïnstalleerd met de Gateway-Cloudservice registreren. 

1.  Selecteer **registreren van een nieuwe gateway op deze computer**.

    ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. Typ een naam en herstel de sleutel voor uw gateway. De gateway gebruikt standaard standaardwaarde regio van uw abonnement. Als u een andere regio selecteren moet, selecteert u **wijziging regio**.

   ![Registreren](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <a name="create-resource"></a>Een Azure-gateway-resource maken
Nadat u hebt geïnstalleerd en uw gateway is geregistreerd, moet u een gateway-resource maken in uw Azure-abonnement. Aanmelden bij Azure met dezelfde account die u hebt gebruikt bij het registreren van de gateway.

1. Klik in de Azure-portal op **een nieuwe service maken** > **Enterprise Integration** > **On-premises gegevensgateway** > **maken**.

   ![Een gateway-resource maken](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. In **verbinding-gateway maken**, voer de volgende instellingen:

    * **Naam**: Voer een naam voor uw gateway-resource. 

    * **Abonnement**: Selecteer de Azure-abonnement wilt koppelen aan uw gateway-resource. 
    Dit abonnement moet uw servers bevinden zich in hetzelfde abonnement.
   
      Het standaardabonnement is gebaseerd op het Azure-account dat u gebruikt voor aanmelden.

    * **Resourcegroep**: maak een resourcegroep of selecteer een bestaande resourcegroep.

    * **Locatie**: Selecteer de regio die u uw gateway in geregistreerd.

    * **De naam van de installatie**: als uw gateway-installatie niet is geselecteerd, selecteert u de gateway is geregistreerd. 

    Wanneer u bent klaar, klikt u op **maken**.

## <a name="connect-servers"></a>Verbinding maken met servers van de gateway-resource

1. Klik in het overzicht Azure Analysis Services-server op **On-Premises Data Gateway**.

   ![Server-gateway verbinding maken](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. In **een On-Premises Data Gateway om verbinding te kiezen**, selecteer uw gateway-resource en klik vervolgens op **verbinding maken met geselecteerde gatewayapparaat**.

   ![Verbinding maken met server gateway-resource](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > Als uw gateway niet wordt weergegeven in de lijst, wordt de server is waarschijnlijk dat niet bij dezelfde regio bevinden als de regio u hebt opgegeven bij het registreren van de gateway. 

Dat is alles. Als u wilt openen van poorten of problemen oplost, moet u uitchecken [On-premises gegevensgateway](analysis-services-gateway.md).

## <a name="next-steps"></a>Volgende stappen
* [Analyseservices beheren](analysis-services-manage.md)   
* [Gegevens ophalen uit Azure Analysis Services](analysis-services-connect.md)
