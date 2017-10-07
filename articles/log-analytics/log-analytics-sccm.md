---
title: aaaConnect Configuration Manager tooLog Analytics | Microsoft Docs
description: Dit artikel ziet Hallo stappen tooconnect Configuration Manager tooLog Analytics en analyseren van gegevens is gestart.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f2298bd7-18d7-4371-b24a-7f9f15f06d66
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: banders
ms.openlocfilehash: dc50ebc46020a806d99d1a3e3d0e91fd09ad2c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-configuration-manager-toolog-analytics"></a>Verbinding maken met Configuration Manager tooLog Analytics
U kunt System Center Configuration Manager tooLog Analytics in OMS toosync apparaatgegevens verzameling verbinden. Dit zijn de gegevens van uw Configuration Manager-hiërarchie beschikbaar in OMS.

## <a name="prerequisites"></a>Vereisten

Log Analytics biedt ondersteuning voor System Center Configuration Manager current branch versie 1606 of hoger.  

## <a name="configuration-overview"></a>Configuratie-overzicht
Hallo stappen te volgen bevat een overzicht van Hallo proces tooconnect Configuration Manager tooLog Analytics.  

1. Configuration Manager registreert als een webtoepassing en/of Web-API-app in Azure Management Portal Hallo, en zorg ervoor dat er Hallo client-ID en client geheime sleutel van de registratie Hallo van Azure Active Directory. Zie [portal toocreate Active Directory-toepassing en service-principal die toegang bronnen tot gebruiken](../azure-resource-manager/resource-group-create-service-principal-portal.md) uitvoeren voor gedetailleerde informatie over hoe u deze stap.
2. In Azure Management Portal Hallo [Configuration Manager (Hallo geregistreerde web-app) voorzien van machtiging tooaccess OMS](#provide-configuration-manager-with-permissions-to-oms).
3. In Configuration Manager [toevoegen van een verbinding met de Wizard OMS-verbinding toevoegen Hallo](#add-an-oms-connection-to-configuration-manager).
4. In Configuration Manager [Hallo verbindingseigenschappen bijwerken](#update-oms-connection-properties) als Hallo wachtwoord of de client de geheime sleutel ooit is verlopen of verloren gegaan is.
5. Met informatie uit Hallo OMS-portal, [downloaden en installeren van Microsoft Monitoring Agent Hallo](#download-and-install-the-agent) wijst op Hallo computer Hallo Configuration Manager-serviceverbinding met de sitesysteemrol. Hallo-agent verzendt gegevens tooOMS van Configuration Manager.
6. In Log Analytics [verzamelingen importeren uit Configuration Manager](#import-collections) als computergroepen.
7. Weergeven in Log Analytics gegevens uit Configuration Manager als [computergroepen](log-analytics-computer-groups.md).

Meer informatie over het aansluiten van Configuration Manager tooOMS op [synchroniseren van gegevens van Configuration Manager toohello Microsoft Operations Management Suite](https://technet.microsoft.com/library/mt757374.aspx).

## <a name="provide-configuration-manager-with-permissions-toooms"></a>Geef de Configuration Manager met machtigingen tooOMS
Hallo bevat volgende procedure hello Azure Management Portal met machtigingen tooaccess OMS. In het bijzonder moet u Hallo verlenen *rol van Inzender* toousers in de resourcegroep Hallo in volgorde tooallow hello Azure Management Portal tooconnect tooOMS Configuration Manager.

> [!NOTE]
> U moet machtigingen opgeven in OMS voor Configuration Manager. Anders, ontvangt u een foutbericht weergegeven wanneer u de configuratiewizard hello in Configuration Manager gebruiken.
>
>

1. Open Hallo [Azure-portal](https://portal.azure.com/) en klik op **Bladeren** > **logboekanalyse (OMS)** tooopen Hallo logboekanalyse (OMS) blade.  
2. Op Hallo **logboekanalyse (OMS)** blade, klikt u op **toevoegen** tooopen hello **OMS-werkruimte** blade.  
   ![OMS-blade](./media/log-analytics-sccm/sccm-azure01.png)
3. Op Hallo **OMS-werkruimte** blade Hallo volgende informatie en klik vervolgens op **OK**.

   * **OMS-werkruimte**
   * **Abonnement**
   * **Resourcegroep**
   * **Locatie**
   * **Prijscategorie**  
     ![OMS-blade](./media/log-analytics-sccm/sccm-azure02.png)  

     > [!NOTE]
     > Hallo in bovenstaand voorbeeld maakt een nieuwe resourcegroep. Hallo-resourcegroep is alleen gebruikte tooprovide Configuration Manager met machtigingen toohello OMS-werkruimte in dit voorbeeld.
     >
     >
4. Klik op **Bladeren** > **resourcegroepen** tooopen hello **resourcegroepen** blade.
5. In Hallo **resourcegroepen** blade, klikt u op Hallo resourcegroep die u hebt gemaakt hierboven tooopen hello &lt;Resourcegroepnaam&gt; instellingenblade.  
   ![instellingen van de resourcegroepblade](./media/log-analytics-sccm/sccm-azure03.png)
6. In Hallo &lt;Resourcegroepnaam&gt; instellingenblade, klikt u op de Access control (IAM) tooopen hello &lt;Resourcegroepnaam&gt; blade gebruikers.  
   ![Gebruikers van de resourcegroepblade](./media/log-analytics-sccm/sccm-azure04.png)  
7. In Hallo &lt;Resourcegroepnaam&gt; blade gebruikers, klikt u op **toevoegen** tooopen hello **toegang toevoegen** blade.
8. In Hallo **toegang toevoegen** blade, klikt u op **Selecteer een rol**, en selecteer vervolgens Hallo **Inzender** rol.  
   ![Selecteer een rol](./media/log-analytics-sccm/sccm-azure05.png)  
9. Klik op **gebruikers toevoegen**Hallo Configuration Manager-gebruiker, klik op **Selecteer**, en klik vervolgens op **OK**.  
   ![gebruikers toevoegen](./media/log-analytics-sccm/sccm-azure06.png)  

## <a name="add-an-oms-connection-tooconfiguration-manager"></a>Een OMS verbinding tooConfiguration Manager toevoegen
Volgorde tooadd een OMS-verbinding, uw Configuration Manager-omgeving moet beschikken over een [serviceaansluitpunt](https://technet.microsoft.com/library/mt627781.aspx) geconfigureerd voor de onlinemodus bevindt.

1. In Hallo **beheer** werkruimte van Configuration Manager, selecteer **OMS Connector**. Hiermee opent u Hallo **OMS verbinding Wizard toevoegen**. Selecteer **volgende**.
2. Op Hallo **algemene** scherm, bevestig dat u de volgende activiteiten Hallo hebt gedaan en dat u hebt de details voor elk item, en selecteer **volgende**.

   1. Hallo in Azure Management Portal, hebt u Configuration Manager geregistreerd als een webtoepassing en/of Web-API-app en die u hebt Hallo [client-ID van de registratie van Hallo](../active-directory/active-directory-integrating-applications.md).
   2. In Azure Management Portal Hallo, hebt u een geheime sleutel van de app voor geregistreerde Hallo-app in Azure Active Directory gemaakt.  
   3. In Azure Management Portal hello, die u hebt opgegeven Hallo geregistreerde web-app met de machtiging tooaccess OMS.  
      ![Verbinding tooOMS Wizard algemene pagina](./media/log-analytics-sccm/sccm-console-general01.png)
3. Op Hallo **Azure Active Directory** scherm, uw tooOMS verbinding-instellingen configureren door te geven uw **Tenant** , **Client-ID** , en **Client geheime sleutel**  , selecteer daarna **volgende**.  
   ![Verbinding tooOMS Wizard Azure Active Directory-pagina](./media/log-analytics-sccm/sccm-wizard-tenant-filled03.png)
4. Als u gerealiseerd alle Hallo andere procedures is, klikt u vervolgens informatie over Hallo Hallo **OMS verbindingsconfiguratie** scherm automatisch wordt weergegeven op deze pagina. Informatie voor de verbindingsinstellingen Hallo moet worden weergegeven voor uw **Azure-abonnement** , **Azure-resourcegroep** , en **Operations Management Suite-werkruimte**.  
   ![Pagina van Wizard OMS verbinding tooOMS verbinding](./media/log-analytics-sccm/sccm-wizard-configure04.png)
5. Hallo wizard verbindt toohello OMS-service met behulp van Hallo-informatie die u hebt ingevoerd. Selecteer Hallo apparaatverzamelingen dat u wilt dat toosync met OMS en klik vervolgens op **toevoegen**.  
   ![Selecteer verzamelingen](./media/log-analytics-sccm/sccm-wizard-add-collections05.png)
6. Controleer de verbindingsinstellingen op Hallo **samenvatting** scherm en selecteer vervolgens **volgende**. Hallo **voortgang** scherm ziet u de verbindingsstatus Hallo en vervolgens moet **Complete**.

> [!NOTE]
> U moet de verbinding van OMS toohello bovenste site in uw hiërarchie te maken. Als u verbinding maken met OMS tooa zelfstandige primaire site en voegt u een centrale beheersite site tooyour omgeving, u hebt toodelete en maak Hallo OMS-verbinding in de nieuwe hiërarchie Hallo opnieuw.
>
>

Nadat u de Configuration Manager tooOMS hebt gekoppeld, kunt u toevoegen of verwijderen van verzamelingen en eigenschappen Hallo Hallo OMS verbinding weergeven.

## <a name="update-oms-connection-properties"></a>De eigenschappen van de OMS-verbinding bijwerken
Als een geheime sleutel met het wachtwoord of de client nooit verloopt of verloren, moet u de verbindingseigenschappen van toomanually update Hallo OMS.

1. In Configuration Manager te navigeren**Cloudservices** , selecteer daarna **OMS Connector** tooopen hello **OMS verbindingseigenschappen** pagina.
2. Op deze pagina, klikt u op Hallo **Azure Active Directory** tooview tabblad uw **Tenant**, **Client-ID**, **Client geheime sleutelverloop**. **Controleer of** uw **geheime sleutel van de Client** als deze is verlopen.

## <a name="download-and-install-hello-agent"></a>Download en installeer Hallo-agent
1. In de OMS-portal Hallo [downloaden Hallo agent-installatiebestand van OMS](log-analytics-windows-agents.md#download-the-agent-setup-file-from-oms).
2. Gebruik een van de methoden tooinstall na Hallo en Hallo agent configureren op Hallo-computers Hallo Configuration Manager-service verbinding sitesysteemrol:
   * [Hallo agent installeren met setup](log-analytics-windows-agents.md#install-the-agent-using-setup)
   * [Hallo agent installeren met Hallo vanaf de opdrachtregel](log-analytics-windows-agents.md#install-the-agent-using-the-command-line)
   * [Hallo agent installeren met DSC in Azure Automation](log-analytics-windows-agents.md#install-the-agent-using-dsc-in-azure-automation)

## <a name="import-collections"></a>Verzamelingen importeren
Nadat u hebt een OMS verbinding tooConfiguration Manager toegevoegd en Hallo agent geïnstalleerd op Hallo computer Hallo Configuration Manager-serviceverbinding met sitesysteemrol, wordt de volgende stap Hallo tooimport verzamelingen van Configuration Manager in OMS Als computergroepen.

Nadat de invoer is ingeschakeld, Hallo verzameling lidmaatschapsgegevens zijn opgehaald elke drie uur tookeep hello verzamelingslidmaatschappen huidige. U kunt toodisable invoer op elk gewenst moment.

1. Klik in de OMS-portal Hallo **instellingen**.
2. Klik op Hallo **computergroepen** tabblad en klik vervolgens op Hallo **SCCM** tabblad.
3. Selecteer **Import Configuration Manager-verzamelinglidmaatschappen** en klik vervolgens op **opslaan**.  
   ![Computergroepen - SCCM-tabblad](./media/log-analytics-sccm/sccm-computer-groups01.png)

## <a name="view-data-from-configuration-manager"></a>Gegevens weergeven van Configuration Manager
Nadat u hebt een OMS verbinding tooConfiguration Manager toegevoegd en Hallo agent geïnstalleerd op Hallo computer uitgevoerd Hallo Configuration Manager-service verbinding sitesysteemrol, gegevens van de agent Hallo tooOMS verzonden. In de OMS, uw Configuration Manager-verzamelingen worden weergegeven als [computergroepen](log-analytics-computer-groups.md). U kunt groepen van Hallo Hallo weergeven **Configuration Manager** pagina onder **computergroepen** in **instellingen**.

Na het Hallo verzamelingen worden geïmporteerd, kunt u zien hoeveel computers met verzamelinglidmaatschappen zijn gedetecteerd. U ziet ook Hallo aantal verzamelingen die zijn geïmporteerd.

![Computergroepen - SCCM-tabblad](./media/log-analytics-sccm/sccm-computer-groups02.png)

Als u een, zoeken geopend, klikt u op weergeven van alle Hallo geïmporteerd groepen of alle computers die deel uitmaken van de groep tooeach. Met behulp van [logboek zoeken](log-analytics-log-searches.md), kunt u beginnen met gedetailleerde analyse van Configuration Manager-gegevens.

## <a name="next-steps"></a>Volgende stappen
* Gebruik [logboek zoeken](log-analytics-log-searches.md) tooview gedetailleerde informatie over uw Configuration Manager-gegevens.
