### <a name="noconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - er is geen gatewayverbinding

#### <a name="tooadd-additional-address-prefixes"></a>tooadd aanvullende adresvoorvoegsels:

1. Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.
2. Hallo IP-adresruimte toevoegen in Hallo *aanvullend adresbereik toevoegen* vak.
3. Klik op **opslaan** toosave uw instellingen.

#### <a name="tooremove-address-prefixes"></a>tooremove adresvoorvoegsels:

1. Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.
2. Klik op Hallo **'...'** op Hallo regel Hallo voorvoegsel met de gewenste tooremove.
3. Klik op **verwijderen**.
4. Klik op **opslaan** toosave uw instellingen.

### <a name="withconnection"></a>toomodify lokale netwerk gateway IP-adresvoorvoegsels - gatewayverbinding bestaande

Als u een gatewayverbinding hebt en tooadd wilt of Hallo IP-adresvoorvoegsels is opgenomen in uw lokale netwerkgateway verwijdert, moet u toodo Hallo stappen hebt uitgevoerd, in volgorde. Dit veroorzaakt enige downtime in uw VPN-verbinding. Als u IP-adresvoorvoegsels wijzigt, hoeft u geen toodelete Hallo VPN-gateway. U hoeft alleen tooremove Hallo verbinding.

#### <a name="1-remove-hello-connection"></a>1. Hallo-verbinding verwijderen.

1. Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **verbindingen**.
2. Klik op Hallo **...**  op Hallo-regel voor elke verbinding en klik vervolgens op **verwijderen**.
3. Klik op **opslaan** toosave uw instellingen.

#### <a name="2-modify-hello-address-prefixes"></a>2. Hallo-adresvoorvoegsels wijzigen.

tooadd aanvullende adresvoorvoegsels:

1. Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.
2. Hallo IP-adresruimte toevoegen.
3. Klik op **opslaan** toosave uw instellingen.

tooremove adresvoorvoegsels:

1. Op de lokale netwerkgateway bron, in Hallo Hallo **instellingen** sectie, klikt u op **configuratie**.
2. Klik op Hallo **...**  op Hallo regel Hallo voorvoegsel met de gewenste tooremove.
3. Klik op **verwijderen**.
4. Klik op **opslaan** toosave uw instellingen.

#### <a name="3-recreate-hello-connection"></a>3. Maak opnieuw verbinding Hallo.

1. Navigeer toohello virtuele netwerkgateway voor uw VNet. (Geen hello lokale netwerkgateway.)
2. Op de virtuele-netwerkgateway Hallo in Hallo **instellingen** sectie, klikt u op **verbindingen**.
3. Klik op Hallo **+ toevoegen** tooopen hello **verbinding toevoegen** blade.
4. Maak opnieuw een verbinding.
5. Klik op **OK** toocreate Hallo verbinding.
