Nadat het Hallo-records voor uw domeinnaam hebt doorgegeven, moet u kunnen toouse worden uw browser tooverify die uw aangepaste domeinnaam kan worden gebruikt tooaccess uw web-app in Azure App Service.

> [!NOTE]
> Het kan even duren voor uw toopropagate CNAME via Hallo DNS-systeem. U kunt een service zoals <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify die Hallo CNAME beschikbaar is.
> 
> 

Als u uw web-app nog niet als een Traffic Manager-eindpunt hebt toegevoegd, moet u dit doen voordat naamomzetting als Hallo aangepast domein naam routes tooTraffic Manager werkt. Traffic Manager stuurt vervolgens tooyour web-app. Hallo-informatie in [toevoegen of verwijderen eindpunten](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd uw web-app als een eindpunt in uw Traffic Manager-profiel.

> [!NOTE]
> Als uw web-app niet wordt weergegeven wanneer u een eindpunt toevoegt, controleert u of deze is geconfigureerd voor **standaard** modus van App Service-plan. U moet gebruiken **standaard** modus voor uw web-app in de volgorde toowork met Traffic Manager.
> 
> 

1. Open in uw browser Hallo [Azure Portal](https://portal.azure.com).
2. In Hallo **Web-Apps** en klik op Hallo-naam van uw web-app, selecteer **instellingen**, en selecteer vervolgens **aangepaste domeinen**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. In Hallo **aangepaste domeinen** blade, klikt u op **hostnaam toevoegen**.
4. Gebruik Hallo **hostnaam** tekst vakken tooenter Hallo Traffic Manager-domein naam tooassociate met deze web-app.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Klik op **valideren** configuratie toosave Hallo domain-name.
6. Wanneer u op klikt **valideren** Azure wordt ere van domeinverificatie werkstroom. Hiermee wordt gecontroleerd op domein eigendom, evenals de beschikbaarheid en rapport geslaagd hostnaam of gedetailleerde fout met prescriptieve guidence op hoe toofix fout Hallo.    
7. Na geslaagde validatie **hostnaam toevoegen** knop wordt actief en kunt u zich kunt toohello toewijzen hostnaam. Nu gaat u een aangepaste domeinnaam tooyour in een browser. U ziet nu uw app wordt uitgevoerd met behulp van uw aangepaste domeinnaam. 
   
   Zodra de configuratie is voltooid, de aangepaste domeinnaam hello wordt weergegeven in Hallo **domeinnamen** gedeelte van uw web-app.

U moet op dit moment worden kunnen tooenter Hallo Traffic Manager-domeinnaam in uw browser en ziet dat het met succes duurt u tooyour web-app voordat.

