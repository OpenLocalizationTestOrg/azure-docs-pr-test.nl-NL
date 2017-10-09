1. Navigeer tooand open Hallo blade voor uw virtuele netwerkgateway. Er zijn meerdere manieren toonavigate. In ons voorbeeld we toohello gateway 'VNet1GW' genavigeerd door te gaan**TestVNet1 -> overzicht -> verbonden apparaten -> VNet1GW**.
2. Klik op de blade Hallo voor VNet1GW **verbindingen**. Bovenaan Hallo Hallo verbindingen blade, klikt u op **+ toevoegen** tooopen hello **verbinding toevoegen** blade.

    ![Site-naar-Site-verbinding maken](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. Op Hallo **verbinding toevoegen** blade invullen Hallo waarden toocreate uw verbinding.

  - **Naam:** de naam van de verbinding. In het voorbeeld wordt gebruikgemaakt van de naam **VNet1toSite2**.
  - **Verbindingstype:** selecteer **Site-naar-site (IPsec)**.
  - **Virtuele netwerkgateway:** Hallo geldt een vaste waarde omdat u verbinding vanaf deze gateway maakt.
  - **Lokale netwerkgateway:** klikt u op **een lokale netwerkgateway kiezen** en selecteer Hallo lokale netwerkgateway die u toouse wilt. In het voorbeeld wordt gebruikgemaakt van **Site2**.
  - **Gedeelde sleutel:** hier Hallo-waarde moet overeenkomen met de Hallo-waarde die u voor uw lokale on-premises VPN-apparaat gebruikt. In Hallo voorbeeld hebben we 'abc123' gebruikt, maar u kunt (en moeten) gebruiken iets ingewikkelders. Hallo belangrijke dingen die u hier opgeeft, Hallo-waarde is moet Hallo die dezelfde waarde die u hebt opgegeven bij het configureren van uw VPN-apparaat.
  - Hallo resterende waarden voor **abonnement**, **resourcegroep**, en **locatie** worden opgelost.

4. Klik op **OK** toocreate uw verbinding. U ziet *verbinding maken* flash op het welkomstscherm.
5. U kunt Hallo verbinding weergeven in Hallo **verbindingen** blade van de virtuele netwerkgateway Hallo. Hallo Status gaat uit *onbekende* te*verbinding maakt met*, en vervolgens te*geslaagd*.
