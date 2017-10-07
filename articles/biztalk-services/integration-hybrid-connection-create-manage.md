---
title: aaaCreate en beheren van hybride verbindingen | Microsoft Docs
description: Ontdek hoe u een hybride verbinding toocreate Hallo verbinding beheren en Hallo hybride Verbindingsbeheer installeren. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Hybride verbindingen maken en beheren

> [!IMPORTANT]
> Hybrid Connections van BizTalk is buiten gebruik gesteld en vervangen door App Service Hybrid Connections. Voor meer informatie, inclusief hoe toomanage uw bestaande BizTalk hybride verbindingen, Zie [Azure App Service hybride verbindingen](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Overzicht van stappen Hallo
1. Een hybride verbinding maken met het invoeren van Hallo **hostnaam** of **FQDN** van Hallo lokale resource in uw particuliere netwerk.
2. Koppel uw Azure-web-apps of apps van Azure mobile toohello hybride verbinding.
3. Hallo hybride Verbindingsbeheer installeren op uw lokale resource en toohello verbinding maken met specifieke hybride verbinding. Hello Azure-portal biedt een tooinstall éénkliks-ervaring en verbinding maken.
4. Hybride verbindingen en hun verbindingssleutels beheren.

In dit onderwerp vindt u deze stappen. 

> [!IMPORTANT]
> Het is mogelijk tooset een hybride verbinding eindpunt tooan IP-adres. Als u een IP-adres gebruikt, moet u mogelijk of Hallo lokale bron, kan niet worden bereikt, afhankelijk van de client. Hallo hybride verbinding is afhankelijk van Hallo client tijdens het doorzoeken van een DNS-zoekopdracht. In de meeste gevallen Hallo **client** is uw toepassingscode. Als hello client voert een DNS-lookup, (dit wordt niet geprobeerd tooresolve Hallo IP-adres alsof deze een domeinnaam (x.x.x.x)), en vervolgens verkeer via Hallo hybride verbinding niet verzonden.
> 
> Bijvoorbeeld (pseudocode), definieert u **10.4.5.6** als uw lokale host:
> 
> **Hallo volgende scenario werkt:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **Hallo volgen scenario werkt niet:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Een hybride verbinding maken
Een hybride verbinding kunnen worden gemaakt in hello Azure portal met behulp van Web-Apps **of** met behulp van BizTalk Services. 

**Hybride verbindingen met behulp van Web-Apps toocreate**, Zie [verbinding maken met Azure Web Apps tooan On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md). U kunt ook Hallo hybride Connection Manager (HCM) installeren uit uw web-app Hallo voorkeurs-methode is. 

**Hybride verbindingen in BizTalk Services toocreate**:

1. Meld u aan toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecteer in de Hallo navigatiedeelvenster links **BizTalk Services** en selecteer vervolgens uw BizTalk Service. 
   
    Als u een bestaande BizTalk Service hebt, kunt u [een BizTalk Service maakt](biztalk-provision-services.md).
3. Selecteer Hallo **hybride verbindingen** tabblad:  
   ![Tabblad hybride verbindingen][HybridConnectionTab]
4. Selecteer **maken van een hybride verbinding** of selecteer Hallo **toevoegen** knop in de taakbalk Hallo. Voer de volgende Hallo:
   
   | Eigenschap | Beschrijving |
   | --- | --- |
   | Naam |Hallo hybride verbinding naam moet uniek zijn en mag geen Hallo dezelfde naam als Hallo BizTalk Service. U kunt elke willekeurige naam invoeren, maar worden specifieke met het doel. Voorbeelden zijn:<br/><br/>Salarissen*SQLServer*<br/>SupplyList*SharepointServer*<br/>Klanten*OracleServer* |
   | Hostnaam |Hallo volledig gekwalificeerde hostnaam, alleen Hallo-hostnaam, invoeren of Hallo IPv4-adres van Hallo lokale resource. Voorbeelden zijn:<br/><br/>mySQLServer<br/>*mySQLServer*. *Domein*. corp.*uwbedrijf*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*. *uwbedrijf*.com<br/>10.100.10.10<br/><br/>Als u Hallo IPv4-adres gebruikt, houd er rekening mee dat uw code client of een toepassing hello IP-adres niet kan omzetten. Zie Hallo belangrijk Opmerking Hallo boven aan dit onderwerp. |
   | Poort |Voer het poortnummer Hallo Hallo lokale resource. Als u Web-Apps gebruikt, voert u bijvoorbeeld poort 80 of poort 443. Als u SQL Server gebruikt, voert u poort 1433. |
5. Selecteer Hallo vinkje toocomplete Hallo setup. 

#### <a name="additional"></a>Aanvullend
* Meerdere hybride verbindingen kunnen worden gemaakt. Zie Hallo [BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md) voor Hallo aantal toegestane verbindingen. 
* Elke hybride verbinding is gemaakt met een paar verbindingsreeksen: toepassing sleutels die verzenden en On-premises sleutels die LUISTEREN. Elk paar heeft een primaire en secundaire sleutel. 

## <a name="LinkWebSite"></a>Koppel uw Azure App Service-Web-App of mobiele App
Selecteer toolink een Web-App of mobiele apps in Azure App Service-tooan bestaande hybride verbinding **gebruik een bestaande hybride verbinding** Hallo hybride verbindingen blade. Zie [toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>Hallo hybride Verbindingsbeheer on-premises installeert
Nadat een hybride verbinding is gemaakt, installeert u Hallo hybride Verbindingsbeheer op Hallo lokale resource. Worden kan gedownload van uw Azure-web-apps of van uw BizTalk Service. Stappen voor BizTalk Services: 

1. Meld u aan toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecteer in de Hallo navigatiedeelvenster links **BizTalk Services** en selecteer vervolgens uw BizTalk Service. 
3. Selecteer Hallo **hybride verbindingen** tabblad:  
   ![Tabblad hybride verbindingen][HybridConnectionTab]
4. Selecteer in de taakbalk Hallo **On-Premises Setup**:  
   ![On-Premises Setup][HCOnPremSetup]
5. Selecteer **installeren en configureren van** toorun of downloaden Hallo hybride Verbindingsbeheer op Hallo on-premises systeem. 
6. Selecteer Hallo vinkje toostart Hallo installatie. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Aanvullend
* Hybride Verbindingsbeheer kan worden geïnstalleerd op Hallo volgende besturingssystemen:
  
  * Windows Server 2008 R2 (.NET Framework 4.5 + en Windows Management Framework 4.0 + vereist)
  * Windows Server 2012 (Windows Management Framework 4.0 + vereist)
  * Windows Server 2012 R2
* Nadat u Hallo hybride Verbindingsbeheer hebt geïnstalleerd, gebeurt Hallo volgende: 
  
  * Hallo hybride verbinding gehost op Azure is automatisch geconfigureerde toouse Hallo primaire verbindingsreeks van de toepassing. 
  * Hallo On-Premises resource is automatisch geconfigureerde toouse Hallo primaire verbindingsreeks voor On-Premises.
* Hallo hybride Verbindingsbeheer moet een geldige lokale verbindingsreeks gebruiken voor autorisatie. Hello Azure Web Apps of mobiele Apps moet een geldige aanvraag-verbindingsreeks gebruiken voor autorisatie.
* U kunt hybride verbindingen schalen door een ander exemplaar van Hallo hybride Verbindingsbeheer installeren op een andere server. Hallo lokale listener toouse Hallo hetzelfde adres als de eerste lokale listener Hallo configureren. In deze situatie is Hallo verkeer willekeurig gedistribueerde (round robin) tussen hello active lokale listeners. 

## <a name="ManageHybridConnection"></a>Hybride verbindingen beheren
toomanage uw hybride verbindingen, kunt u:

* Gebruik hello Azure-portal en gaat u tooyour BizTalk Service. 
* Gebruik [REST-API's](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Kopieer/opnieuw genereren Hallo hybride verbindingsreeksen
1. Meld u aan toohello [klassieke Azure-portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. Selecteer in de Hallo navigatiedeelvenster links **BizTalk Services** en selecteer vervolgens uw BizTalk Service. 
3. Selecteer Hallo **hybride verbindingen** tabblad:  
   ![Tabblad hybride verbindingen][HybridConnectionTab]
4. Selecteer Hallo hybride verbinding. Selecteer in de taakbalk Hallo **beheren verbinding**:  
   ![Opties beheren][HCManageConnection]
   
    **Verbinding beheren** lijsten Hallo toepassings- en On-Premises verbindingsreeksen. U kunt kopiëren Hallo verbindingsreeksen of opnieuw genereren van toegangssleutel in de verbindingsreeks Hallo gebruikt Hallo. 
   
    **Als u opnieuw genereren selecteert**, Hallo gedeelde toegangssleutel die wordt gebruikt binnen Hallo verbindingstekenreeks is gewijzigd. Hallo te volgen:
   
   * Selecteer in de klassieke Azure-portal hello, **sleutels synchroniseren** in hello Azure-toepassing.
   * Voer Hallo **On-Premises Setup**. Wanneer u opnieuw Hallo uitvoeren geconfigureerd On-Premises installatie Hallo lokale resource automatisch wordt toouse Hallo bijgewerkt primaire verbindingsreeks.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>Gebruik groep beleid toocontrol Hallo lokale bronnen worden gebruikt door een hybride verbinding
1. Hallo downloaden [beheersjablonen voor hybride Verbindingsbeheer](http://www.microsoft.com/download/details.aspx?id=42963).
2. Hallo-bestanden extraheren.
3. Op de computer Hallo die groepsbeleid wijzigt, Hallo te volgen:  
   
   * Hallo kopiëren. ADMX-bestanden toohello *%WINROOT%\PolicyDefinitions* map.
   * Hallo kopiëren. ADML bestanden toohello *%WINROOT%\PolicyDefinitions\en-us* map.

Eenmaal zijn gekopieerd, kunt u Groepsbeleidsobjecteditor toochange Hallo beleid kunt gebruiken.

## <a name="next"></a>Volgende
[Verbinding maken met Azure Web Apps tooan On-Premises Resource](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Verbinding maken met tooon lokale SQL Server vanuit Azure Web Apps](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Overzicht van hybride verbindingen](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>Zie ook
[REST-API voor het beheren van BizTalk Services op Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md)  
[Een BizTalk Service met behulp van de klassieke Azure portal maken](biztalk-provision-services.md)  
[BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
