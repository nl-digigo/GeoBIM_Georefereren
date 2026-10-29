# Georeferentie in de domeinen Burgerlijke en Utiliteitsbouw (B&U) en Infra

## Georeferentie in de B&U
B&U staat voor Burgerlijke en Utiliteitsbouw. Burgerlijke bouw betreft vooral woningbouw en utiliteitsbouw betreft allerlei gebouwen voor het openbare en zakelijke leven. B&U-projecten kenmerken zich doorgaans door een beperkte ruimtelijke omvang. Modellen worden 
daarom vaak in een lokaal assenstelsel opgezet. Dit verhoogt de numerieke stabiliteit van 
berekeningen en voorkomt afrondingsfouten in ontwerpsoftware. Daarnaast vereenvoudigt het 
de samenwerking tussen disciplines binnen één modelomgeving. Wanneer integratie met 
informatiesystemen, infrastructuurmodellen of stadsmodellen nodig is, wordt het model 
gekoppeld aan een bekend nationaal coördinatenstelsel.

**Voorbeelden van B&U-projecten**

- Woningen (beperkte omvang)
- Vliegvelden en ziekenhuizen (relatief langgerekte objecten)  

Woningen, flats en ziekenhuizen beslaan meestal enkele tientallen tot honderden meters. Over dergelijke afstanden zijn de effecten van aardkromming en kaartprojectievervorming verwaarloosbaar. Het gebruik van vlakke coördinaten leidt daardoor in de praktijk tot meetbare, maar toelaatbare geometrische afwijkingen (zie [methodes voor  georeferentie](#Methodes-voor-Georeferentie)). 

## Georeferentie in de Infra

Infraprojecten zijn vaak langgerekt en sterk afhankelijk van hun omgeving. De ligging van objecten wordt bepaald door bestaande infrastructuur, terreincondities en wettelijke liggingseisen. Hierdoor bestaan veel raakvlakken met de omgeving. Om deze raakvlakken goed te beheersen is een nauwkeurige positionering van zowel het ontwerp als de omgeving essentieel. Over de langere afstanden van infrastructuurprojecten zijn de effecten van aardkromming en kaartprojectievervorming vaak niet verwaarloosbaar. Het gebruik van vlakke coördinaten leidt daardoor in de praktijk tot meetbare en vaak ontoelaatbare meetbare geometrische afwijkingen (zie [methode voor georeferentie](#Methodes-voor-Georeferentie)). In Nederland voorkomt men de afwijkingen doorgaans door te modelleren in RD-coördinaten in combinatie met NAP-hoogten.

**Voorbeelden van infraprojecten**

- (Snel)wegen, tunnels en dijkversterkingen (langgerekt)  
- Bruggen, viaducten en sluizen (locatiegebonden)

Binnen infraprojecten wordt gewerkt met RD-coördinaten en NAP-hoogten. Dit maakt directe aansluiting op bestaande infrastructuur en geodata mogelijk. Bestaande objecten en terreinpunten worden door landmeters ingemeten met GNSS- of tachymetrische metingen. GNSS-metingen worden daarbij eerst bepaald in een geodetisch CRS (zoals ETRS89) en vervolgens met de officiële transformatie RDNAPTRANS omgerekend naar RD- en NAP-coördinaten. Op basis van deze gegevens wordt het ontwerp opgesteld.

Ook andere geometrische projectinformatie, zoals utiliteits netwerken (KLIC) en systeemgrenzen, wordt doorgaans in RD aangeleverd. Het RD-stelsel vormt daardoor de logische standaard voor gegevensuitwisseling en ontwerp binnen infraprojecten.

Het ontwerp wordt uitgewerkt in een geprojecteerd CRS (RD), waarbij op tekeningen RD-coördinaten en NAP-hoogten worden vermeld om objectlocaties eenduidig vast te leggen. Op de bouwplaats worden ontwerpen uitgezet met meetapparatuur die is georiënteerd op bekende RD-grondslagpunten. Hierdoor kunnen ontwerpcoördinaten rechtstreeks in het veld worden gerealiseerd met de vereiste nauwkeurigheid.

### Toepassing van 3D-software
Tijdens het ontwerp wordt software ingesteld op het werken met RD-coördinaten, zodat de modelruimte overeenkomt met de projectrealiteit. Afhankelijk van het softwarepakket wordt intern nog met een lokaal stelsel gerekend, maar dit heeft geen inhoudelijke betekenis voor het projectteam. In sommige toepassingen wordt bijvoorbeeld een intern referentiepunt gebruikt waarvan de positie projectmatig wordt gekozen, vaak als afgeronde RD-coördinaat. Andere pakketten ondersteunen directe modellering op nationale coördinaten, waarbij ver van de interne oorsprong wordt gewerkt.

Gegevensuitwisseling tussen softwarepakketten vindt eveneens plaats op basis van RD-coördinaten. Dit verloopt niet altijd probleemloos, omdat niet alle software het gebruikte referentiestelsel automatisch herkent. Wanneer CRS-informatie ontbreekt of verkeerd wordt geïnterpreteerd, kunnen bestanden worden ingelezen alsof zij een lokaal stelsel met grote coördinaatwaarden bevatten. Dit kan leiden tot foutieve positionering.

### Gevolgen van projectievervorming
Ontwerpen worden opgesteld in een geprojecteerd CRS. Kaartprojecties hebben een schaalfactor die licht afwijkt (zie [Geprojecteerd CRS](#geprojecteerd-crs)). Hierdoor kan de afstand tussen twee punten in het ontwerp iets verschillen van de werkelijke afstand in het terrein. Voor geprefabriceerde elementen, zoals prefab liggers die in een fabriek worden geproduceerd, blijft dit effect zeer beperkt, omdat de elementlengtes meestal ruim onder de 100 meter liggen. De afwijking blijft daardoor doorgaans beperkt tot millimeters en valt binnen constructietoleranties.

Voor objecten die over grote afstanden worden gerealiseerd, zoals wegen van meerdere kilometers lang, worden langs het tracé meerdere uitzetpunten gebruikt. Hierdoor wordt het effect van de projectieschaal verdeeld over de totale lengte. De afwijking bedraagt afhankelijk van de ligging binnen het projectiestelsel, tot ca. 10 cm per kilometer. Dit vormt in de praktijk geen probleem omdat aansluitende infrastructuur in hetzelfde referentiestelsel is ingemeten. Bij het combineren van geodata en BIM-data kan dit wel problemen veroorzaken met niet aansluitende geometrieën. Het opnemen van bestaande terreinpunten en geodetische referentiepunten in het BIM-model kan dit oplossen (Level60).
