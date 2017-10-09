### <a name="gwipnoconnection"></a>toomodify hello lokale netwerk gateway IP-adres - er is geen gatewayverbinding

Hallo voorbeeld toomodify een lokale netwerkgateway die geen een gatewayverbinding gebruiken. Als u deze waarde wijzigt, kunt u ook Hallo adresvoorvoegsels op Hallo wijzigen hetzelfde moment.

1. Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.
2. In Hallo **IP-adres** Hallo IP-adres wijzigt.
3. Klik op **opslaan** toosave Hallo instellingen.

### <a name="gwipwithconnection"></a>toomodify hello lokale netwerk gateway gateway IP-adres - gatewayverbinding bestaande

toomodify een lokale netwerkgateway een verbinding heeft, moet u toofirst verwijderen Hallo verbinding. Nadat Hallo verbinding is verwijderd, kunt u Hallo gateway IP-adres wijzigen en maak een nieuwe verbinding. U kunt ook de adresvoorvoegsels Hallo op Hallo wijzigen hetzelfde moment. Dit veroorzaakt enige downtime in uw VPN-verbinding. Als u IP-adres van Hallo gateway wijzigt, hoeft u geen toodelete Hallo VPN-gateway. U hoeft alleen tooremove Hallo verbinding.
 
#### <a name="1-remove-hello-connection"></a>1. Hallo-verbinding verwijderen.

1. Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **verbindingen**.
2. Klik op Hallo **...**  op Hallo-regel voor Hallo verbinding en klik vervolgens op **verwijderen**.
3. Klik op **opslaan** toosave uw instellingen.

#### <a name="2-modify-hello-ip-address"></a>2. Hallo IP-adres wijzigen.

U kunt ook de adresvoorvoegsels Hallo op Hallo wijzigen hetzelfde moment.

1. In Hallo **IP-adres** Hallo IP-adres wijzigt.
2. Klik op **opslaan** toosave Hallo instellingen.

#### <a name="3-recreate-hello-connection"></a>3. Maak opnieuw verbinding Hallo.

1. Navigeer toohello virtuele netwerkgateway voor uw VNet. (Geen hello lokale netwerkgateway.)
2. Op de virtuele-netwerkgateway Hallo in Hallo **instellingen** sectie, klikt u op **verbindingen**.
3. Klik op Hallo **+ toevoegen** tooopen hello **verbinding toevoegen** blade.
4. Maak opnieuw een verbinding.
5. Klik op **OK** toocreate Hallo verbinding.
