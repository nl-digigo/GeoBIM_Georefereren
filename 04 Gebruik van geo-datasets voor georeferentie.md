# Gebruik van geodata voor georeferentie

## Georeferentie van BIM-modellen met behulp van geodata
De aanbevolen methode voor georeferentie (level 50) is voor infrastructuurprojecten vaak niet toereikend; in de praktijk is daar een hogere nauwkeurigheid nodig (level 60). Om een model met level 60 te georefereren, is geodata nodig. Er zijn o.a. drie mogelijkheden om dit toe te passen: (1) Gebruik van referentiepunten (<a>survey point</a>s), (2) <a>Geografische uitlijning</a> en (3) <a>scan-to-BIM</a> gebaseerd op technieken getoond door [BuildingSMART et al. (2020)](https://www.buildingsmart.org/wp-content/uploads/2025/04/The-buildingSMART-Awards-Yearbook-2020.pdf). Voor iedere methode van georeferentie wordt in de theorie nader toegelicht hoe deze kan worden toegepast. Bij de derde mogelijkheid is het model vaak reeds gegeorefereerd en zijn er in de meeste gevallen transformatieparameters beschikbaar die het model vertalen van een BIM-softwareomgeving naar het coördinatenstelsel waarin de puntenwolk is ingewonnen.

Daarom wordt geadviseerd om uitsluitend bij optie 1 en 2 een beoordelingstoets uit te voeren, om te verifiëren of het model zich daadwerkelijk op de correcte locatie bevindt.

### Het gebruik van referentiepunten
Voor kleine netwerken worden vaste meetpunten op plekken gezet waarvan met een bepaalde zekerheid aangenomen kan worden dat deze niet verstoord worden of verdwijnen. De meetpunten worden in RDNAP bepaald, en kunnen beschouwd worden als stabiel in het terrein. De bepaling in RD wordt door middel van RTK-<a>GNSS</a> uitgevoerd met een nauwkeurigheid van 2 à 3 cm. Wanneer het niet mogelijk is meetpunten direct via RTK-GNSS te bepalen, bijvoorbeeld als de meetpunten in een muur zitten, worden er tijdelijke punten gemaakt en via tachymetrie de RD-coördinaten ingemeten. Door middel van waterpassing wordt de hoogte (H) met mm-nauwkeurigheid bepaald.

Bij het verwerken van langgerekte netwerken kan er gekozen worden voor referentievelden. Deze worden op dezelfde manier bepaald, maar alleen via GNSS gekoppeld aan RD-coördinaten. Voor de NAP-hoogte kan een waterpassing uitgevoerd worden per veld. Het geodetisch netwerk wordt gebruikt om een puntenwolk te georefereren; van die puntenwolk wordt vervolgens een BIM-model gemaakt. Er kan een controle uitgevoerd worden door de coördinaten en het BIM-model te vergelijken.

### Geografische uitlijning
Geografische uitlijning (in de Engelstalige literatuur aangeduid als footprint alignment) vereist dat zowel de planimetrische (XY) als de altimetrische (Z) component expliciet worden meegenomen. Om een niet-geogerefereerd model te transformeren naar een gegeorefereerde ruimtelijke omgeving, is het noodzakelijk gebruik te maken van bestaande, stabiele objecten waarvan de verplaatsing in de tijd verwaarloosbaar is. Hierbij wordt een iteratief uitlijningsproces toegepast. Dit proces start met een initiële, grove schatting van de planimetrische component, waarna de altimetrische component verder wordt verfijnd op basis van patroonherkenning. Voor toepassing binnen infrastructuur- en B&U-projecten kunnen twee typen objecten als referentie worden ingezet: (1) noklijnen en (2) straatmeubilair.

*Noklijnen*  
Als de planimetrische componenten van de dataset op de juiste plek liggen, is het nog steeds van belang om de hoogtecomponent op de juiste manier te georefereren. Vanuit het Integraal Hoogtevoorziening Nederland (IHN)-project is gebleken dat er in Nederland methoden beschikbaar zijn om data die niet zijn gegeorefereerd of die geen 3D-informatie bevatten, te koppelen aan bestaande referentiesystemen. Hiervoor kan bijvoorbeeld gebruik worden gemaakt van noklijnen die zijn geëxtraheerd uit het [Actueel Hoogtebestand Nederland (AHN)](https://www.ahn.nl/integrale-hoogtevoorziening-nederland).
De noklijnen zijn vrij beschikbaar via de dataroom van het AHN. Hiermee kan men de beschikbare noklijnen binnen het projectgebied te gebruiken als referentie voor het positioneren van het model ten opzichte van de GIS-laag. Een aandachtspunt is echter dat deze datasets beschikbaar zijn in GeoPackage-formaat (GPKG), waardoor de gebruiker de data  moet converteren naar een DWG-bestand om deze binnen gangbare BIM-software te kunnen gebruiken.

*Straatmeubilair*  
Bij infrastructuurprojecten zijn in veel gevallen geen gebouwen aanwezig, waardoor het gebruik van noklijnen beperkt is voor de hoogteregistratie binnen infrastructurele BIM-modellen buiten stedelijke gebieden. In dergelijke situaties kan gebruik worden gemaakt van straatmeubilair en andere infrastructuurobjecten met een duidelijke geometrische of semantische herkenbaarheid, zoals wegmarkeringen, kantverharding en overige vaste objecten.

Voor deze toepassing zijn verschillende landelijke datasets van belang die, naast het Actueel Hoogtebestand Nederland (AHN), kunnen worden ingezet. Voorbeelden hiervan zijn het Digitaal Topografisch Bestand (1GiS) en het Nationaal Wegenbestand (NWB). Het is hierbij van belang te onderkennen dat deze datasets niet volledig driedimensionaal zijn. Zo is het DTB/1GiS een 2.5D-dataset, waarbij per xy-coördinaat slechts één hoogtewaarde beschikbaar is, terwijl het huidige NWB uitsluitend tweedimensionale geometrie bevat.

Door wisselende prioriteiten binnen grootschalige infrastructuurprojecten kunnen er verschillen optreden in betrouwbaarheid en in de toegepaste inwin- en meetmethoden per objecttype. Daarom is het raadzaam om vooraf het 1GIS-handboek te raadplegen, voordat een object wordt geselecteerd voor toepassing binnen de geografische uitlijningsmethode. Afhankelijk van de objectcategorie kan dit resulteren in verschillende afwijkingen.

De onderstaande figuur toont de combinatie van een BIM-model met het DTB/1GiS van de Drechttunnel. Het volledige overzicht boven (links) en onder (rechts) maaiveld illustreert hoe een geo-gereferereerd BIM-model is gepositioneerd binnen zijn geografische context.
<figure id="Geo_overzicht_BIM_DTB">

  <div style="display: flex; justify-content: center; gap: 20px; flex-wrap: wrap;">
    <img src="./media/Geografische uitlijning/geo_overzicht.png" alt="geo_overzicht" height="250"/>
    <img src="./media/Geografische uitlijning/geo_overzicht_2.png" alt="geo_overzicht_2" height="250"/>
  </div>

  <figcaption>
    <em>
      Overzicht van de Drechttunnel met het DTB en de 3DBAG. Links geeft de data boven de grond weer, en rechts de data onder de grond.  
      Dit overzicht is gemaakt vanuit de RWS Digital Twin Basisvoorziening.
    </em>
  </figcaption>

</figure>

Naast vectordatasets zoals het DTB/1GiS en het NWB kan ook het AHN, of een andere beschikbare puntenwolk in de omgeving, worden ingezet. Wegmarkeringen en andere infrastructurele objecten zijn hierin vaak goed herkenbaar doordat de intensiteitswaarden van deze punten doorgaans significant hoger zijn dan die van het omliggende wegdek. Hierdoor kunnen deze objecten relatief eenvoudig worden geïdentificeerd en geëxtraheerd uit de puntenwolk, wat ze geschikt maakt als referentie voor hoogteregistratie.

## Geodatasets voor het georefereren van BIM-modellen
Voor georefereren zijn een aantal datasets en RD- en NAP-referentiepunten beschikbaar om op aan te sluiten. Deze zijn (niet limitatief) weergegeven in onderstaande [tabel](#tabel-overzicht-nationale-datasets) In de tabel is de volgende informatie weergegeven: de naam, dimensie, het domein en de gespecificeerde nauwkeurigheid. Hierbij is het ook van belang om te kijken welke dataset er gebruikt kan worden die geschikt is voor het doel van het BIM-model. Het georefereren van een BIM-model met gebruik van geodata, wordt nooit beter dan de nauwkeurigheid van de gebruikte geodataset. Hierbij heeft de absolute nauwkeurigeid van een dataset vooral invloed op de ligging van het BIM-model als geheel en heeft de relatieve nauwkeurigeid van een dataset vooral invloed op de consistentie met maten in het BIM-model. Het wel of niet onderscheid maken tussen absolutie en relatieve nauwkeurigeid en de manier waarop deze gespecificeerd worden, kan per dataset verschillen. Een optimistische waarde voor de nauwkeurigheid leidt tot onhaalbare verwachtingen en onbegrepen fouten bij het georefereren. 

<table id="tabel-overzicht-nationale-datasets">
   <caption>Overzicht van nationale datasets en referentiepunten beschikbaar voor georeferentie</caption>
  <thead>
    <tr>
      <th>Naam</th>
      <th>Dimensie</th>
      <th>Domein</th>
      <th>Gespecificeerde nauwkeurigheid*</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://www.pdok.nl/introductie/-/article/digitaal-topografisch-bestand-dtb-"><strong>1GiS</strong></a></td>
      <td>2.5D</td>
      <td>Landelijk beheerde water/wegen-infrastructuur</td>
      <td> Eis verschilt per soort topografie (<i>middel</i> (absoluut 10 cm xy, 12 cm z)(relatief 5 cm xy, 6 cm z), <i>zacht</i> (absoluut 15 cm xy, 15 cm z)(relatief 13 cm xy, 9 cm z), <i>kabel/leiding</i> (absoluut 20 cm xy, 10 cm z), <i>riolering</i> (absoluut 10 cm xy, 1,5 cm z), <i>functioneel gebied </i> (niet gedefinieerd)) (bron: <a href="https://standaarden.rws.nl"> Standaarden RWS - Data-eisen 1GIS (Geografisch Informatie Systeem) - Standaard 6058 </a>)</td>
    </tr>
    <tr>
      <td><a href="https://www.pdok.nl/introductie/-/article/basisregistratie-grootschalige-topografie-bgt-"><strong>BGT</strong></a></td>
      <td>2D</td>
      <td>Landelijk</td>
      <td>30 tot 60 cm positionele nauwkeurigheid <br> (bron: <a href="https://docs.geostandaarden.nl/imgeo/catalogus/bgt/#positionele-nauwkeurigheid">nauwkeurigheidsbeschrijving catalogus BGT</a>)</td>
    </tr>
    <tr>
      <td><a href="https://www.pdok.nl/introductie/-/article/basisregistratie-adressen-en-gebouwen-ba-1"><strong>BAG</strong></a></td>
      <td>2D/2.5D</td>
      <td>Landelijk</td>
      <td>De ingemeten geometrie van een Pand heeft een positionele nauwkeurigheid van 20 cm × √2. Afgerond is dit 30 cm. (bron: <a href="https://www.geobasisregistraties.nl/documenten/2018/03/12/catalogus-2018">BAG catalogus 2018</a>)</td>
    </tr>
    <tr>
      <td><a href="https://www.ahn.nl/dataroom"><strong>AHN</strong></a></td>
      <td>3D</td>
      <td>Landelijk</td>
      <td>De hoogtenauwkeurigheid van AHN 2,3 en 4 is 15 cm (95,4%). Het bestand bezit een zodanige dichtheid, een zodanige verdeling en een zodanige planimetrische nauwkeurigheid dat topografische objecten met een grootte van 2 x 2 m eenduidig en met een positieafwijking van maximaal 50 centimeter kunnen worden geïdentificeerd. (bron: <a href="https://www.ahn.nl/kwaliteitsbeschrijving">kwaliteitsbeschrijving AHN</a>)</td>
    </tr>
    <tr>
      <td><a href="https://www.nationaalwegenbestand.nl/nwb-downloaden"><strong>NWB</strong></a></td>
      <td>2D</td>
      <td>Landelijk, wegennet</td>
      <td> De doelstelling is een maximale afwijking van 10 centimeter ten opzichte van het midden van de weg. Weggeometrie wordt vereenvoudigd met een tolerantie van 5 centimeter. (bron: <a href="https://docs.ndw.nu/en/handleidingen/nwb/kwaliteit/kwaliteitsmetingen/">kwaliteitsmeting NWB</a> en <a href="https://docs.ndw.nu/handleidingen/nwb/kwaliteit/"> kwaliteit NWB</a>)</td>
    </tr>
    <tr>
      <td><a href="https://spoorinbeeld.nl/"><strong>SpoorInBeeld - Helicopter vluchten</strong></a></td>
      <td>3D</td>
      <td>Spoortracés</td>
      <td>onbekend bij de opstellers van deze praktijkrichtlijn</td>
    </tr>
    <tr>
      <td><a href="https://www.beeldmateriaal.nl/dataroom"><strong>Beeldmateriaal</strong></a></td>
      <td>2.5D</td>
      <td>Landelijk</td>
      <td>onbekend bij de opstellers van deze praktijkrichtlijn</td>
    </tr>
    <tr>
      <td><a href="https://www.nsgi.nl/referentiepunten-en-gnss-data/informatie-referentiepunten/rdinfo"><strong>RD-referentiepunten</strong></a></td>      
      <td>3D</td>
      <td>Landelijk netwerk (GNSS-kernnetpunten)</td>
      <td>1 cm (horizontaal), 3 cm (ellipsoïdische hoogte)</td>
    </tr>
    <tr>
      <td><a href="https://geoweb.rijkswaterstaat.nl/ModuleViewer/?app=9b07e48705b54e6aa39af7eb36e9544c"><strong>NAP-referentiepunten</strong></a></td>
      <td>1D</td>
      <td>Landelijk netwerk (NAP-peilmerken)</td>
      <td>1 cm (verticaal)</td>
    </tr>
    <tr>
      <td><a href="https://docs.3dbag.nl/nl/"><strong>3DBAG</strong></a></td>
      <td>3D</td>
      <td>Landelijk</td>
      <td>Gebaseerd op de AHN3 en AHN4 in combinatie met de BAG/BGT (zie nauwkeurigheid BAG/BGT en AHN) (bron:<a href="https://docs.3dbag.nl/nl/overview/sources/"> 3D BAG documentatie </a>)</td>
    </tr>
    <tr>
      <td><a href="https://www.pdok.nl/introductie/-/article/basisregistratie-adressen-en-gebouwen-ba-1"><strong>3D Basisvoorziening</strong></a></td>
      <td>3D</td>
      <td>Landelijk</td>
      <td>Gebaseerd op de AHN5 en AHN6, hoogtes uit luchtfotobeelden in combinatie met de BAG/BGT (zie nauwkeurigheid BAG/BGT en AHN) (bron:<a href="https://3d.kadaster.nl/productbeschrijving/"> 3D Basisvoorziening productbeschrijving) </a></td>
    </tr>
  </tbody>
</table>

*) In de specificaties worden nauwkeurigheidseisen vermeld die minimaal gehaald dienen te worden om te voldoen aan de eisen voor de dataset. Bij de interpretatie van deze nauwkeurigheden moet er rekening mee gehouden worden dat de gemiddelde nauwkeurigheid van de dataset hoger kan zijn, maar dat data incidenteel ook slechter kan zijn dan de specificaties. Met name bij specificatie van standaardafwijkingen is het belangrijk te weten dat in 32% van de data in een dataset fouten groter dan 1 standaardafwijking (sigma) voor kunnen komen, 4,6% fouten groter dan 2 maal de standaardafwijking en 0,3% groter dan 3 maal de standaardafwijking. 

Naast primaire geodatasets, kunnen gemeentes, provicies en centrale overheden andere datasets beschikbaar hebben, die een kleiner gebied beslaan. Ook zijn er datasets die zijn afgeleid uit de bovengenoemde datasets. Een voorbeeld is de 3DBAG, waar de BAG en het <a>AHN</a> de basis zijn voor het maken van deze dataset. Het <a>DTB</a> is opgebouwd met verschillende meettechnieken en verschillende standaarden. Vanuit het onderzoek van Rijkswaterstaat, TU Delft, Het Waterschapshuis en EuroSDR is er een analyse uitgevoerd voor alle LiDAR-datasets in Europa. De resultaten hiervan zijn in te zien in de portal die in dit onderzoek is ontwikkeld: <a href="https://3d.bk.tudelft.nl/eupc/"> <strong>European Pointclouds (EUPC)</strong></a>

### Kwaliteitskenmerken voor geodata in BIM-modellen
De verschillende datasets die voor dit doel kunnen worden gebruikt, zijn duidelijk van elkaar te onderscheiden. Zoals in de vorige paragraaf is benadrukt, vormen zowel het planimetrische (xy) als het altimetrische (H) component een fundamenteel onderdeel van geodata. Afwijkingen in deze componenten, of verschillen die ontstaan door uiteenlopende momenten van inwinning of ontwerp, kunnen een aanzienlijke impact hebben op de onderlinge uitlijning van datasets. Het correct georefereren van een bestand ten opzichte van een CRS is daarom essentieel om betrouwbare vervolgstappen in het uitlijnings- en integratieproces te kunnen uitvoeren.

Het doel van het georefereren van een BIM-model in geo-software is het positioneren ervan in de echte wereld. Deze echte wereld is vastgelegd via nationale, regionale en internationale coördinatenstelsels. Zoals eerder beschreven, wordt voor BIM-modellen in de gebruikte softwarepakketten vaak een lokaal coördinatenstelsel gebruikt. Coördinaten in geodetische coördinatenstelsels hebben vaak aanzienlijk grotere waarden. In sommige applicaties tot afrondingsfouten of vastlopers kan leiden. De documentatie van het gebruikte coördinatenstelsel is eveneens van cruciaal belang. Wanneer dit niet correct is vastgelegd, kunnen er problemen ontstaan tijdens transformatie.

### Primaire kwaliteitskenmerken voor geodata in BIM-modellen
Voor het gebruik van een dataset uit het GIS-domein zijn verschillende kenmerken van belang voor de toepassing binnen een BIM-systeem. Niet alle data is even geschikt om gebruikt te worden, naast het gebruik van het juiste coördinatenstelsel, spelen er kwaliteitskenmerken mee die van invloed zijn op zowel de ingewonnen als de gebruikte referentiedata. Op basis van o.a. de onderzoeken en initiatieven van het <a href="https://www.ahn.nl/integrale-hoogtevoorziening-nederland"> <em>Integrale Hoogtevoorziening Nederland</em></a> (Het Waterschapshuis, Rijkswaterstaat, TU Delft & het Kadaster), de  <a href="https://www.digigo.nu/ilsen-en-richtlijnen/basis-ils-puntenwolk/"> <em>Basis ILS puntenwolken</em></a> (DigiGo) en <a href="https://docs.geostandaarden.nl/3d/3d-tiling/"> <em>Handreiking 3D Tiling</em></a> (Geonovum) kunnen de volgende componenten worden meegenomen. Let wel, er zijn meer componenten die van invloed zijn op de kwaliteit en bruikbaarheid van de data. 

***1. Geografische distributie van de meetpunten***

Afhankelijk van de inwinmethode, is de geografische distributie van de meetpunten van belang. Dit heeft namelijk een direct effect op het onderscheiden van objecten in het terrein, maar ondersteunt ook bij het correct vinden van georeferentiepunten. De distributie wordt omschreven door de hoeveelheid punten per vierkante meter of door de minimale afstand tussen de punten. De praktijk leert dat een hoge puntdichtheid vaak gepaard gaat met een hoger detailniveau van het 3D-model.

***2. De absolute en relatieve nauwkeurigheid van geodata***

In de literatuur en uitvraag­specificaties wordt onderscheid gemaakt tussen de **absolute** en **relatieve** nauwkeurigheid van geodata. De **absolute nauwkeurigheid** beschrijft de afwijking tussen de inwinning of het model en de werkelijkheid, terwijl de **relatieve nauwkeurigheid** vaak wordt gebruikt om de afwijking tussen meetpunten binnen de dataset te omschrijven. Een voorbeeld hiervan is een dwarsprofiel over een ingewonnen stuk snelweg. Beide typen nauwkeurigheden worden uitgedrukt in een planimetrische (xy) en een altimetrische (H) component. De verschillende uitvraag­specificaties laten zien dat de relatieve nauwkeurigheid doorgaans beter is dan de absolute nauwkeurigheid.

***3. De classificatieparameters in een geodataset***

De wijze waarop objecten binnen een geodataset worden geclassificeerd, is essentieel voor de bruikbaarheid binnen de context van BIM-modellen. De toegepaste classificatiemethode vormt een belangrijke kwaliteitsparameter, bijvoorbeeld of de classificatie is uitgevoerd door kunstmatige intelligentie (AI) of door menselijke experts. Daarnaast zijn de gebruikte definities cruciaal. Zo kan de classificatie van vegetatie in een referentiedataset een andere definitie hebben dan in de ingewonnen dataset, wat kan leiden tot interpretatieverschillen of inconsistenties in het uiteindelijke model.

***4. De inwindatum van de geodataset***

Het moment van inwinning bepaalt de bruikbaarheid van de dataset, aangezien iedere geodataset die wordt weergegeven in een GIS-omgeving een momentopname is. Een geodataset vertegenwoordigt nooit de volledige werkelijkheid, maar vormt slechts een benadering van de omgeving. Hierdoor kan de omgeving, afhankelijk van de mate van verandering, in de loop van de tijd sterk of minder sterk afwijken van de oorspronkelijke weergave. Dit wordt geïllustreerd in onderstaande figuur aan de hand van de stationsregio van Delft, zoals weergegeven in het Actueel Hoogtebestand Nederland en de 3D Basisvoorziening, waarbij de bouw van de stationsregio een ingrijpende verandering in het terrein laat zien.

<figure id="Leeftijd-van-verschillende-puntenwolken-van-de-stations-regio-in-Delft">
    <img src="./media/Geografische uitlijning/Regio_delft_verandering.png" alt="Leefttijd van verschillende puntenwolken van de stationsregio in Delft" height="500"/>
    <figcaption><a class="self-link" href="#fig-Leeftijd-van-verschillende-puntenwolken-van-de-stations-regio-in-Delft"></a><span class="fig-title">Leeftijd van verschillende puntenwolken van de stationsregio in Delft (figuur is uit wp1 van het <a href="https://www.ahn.nl/integrale-hoogtevoorziening-nederland"> <em>Integrale Hoogtevoorziening Nederland</em></a> overgenomen.) 
</figure>





De kwaliteitseisen van een BIM-model bepalen welke geodata toe te passen is t.b.v. georeferentie. De geodata voor een BIM-model dient een hogere nauwkeurigheid te hebben dan de kwaliteitseis aan een BIM-model. Door de geolocatie op een vastgelegde en standaard manier vast te leggen is duidelijk wat de bedoelde locatie van een object is. Dit helpt miscommunicatie gedurende het gehele proces te voorkomen, maar is uiteraard geen vervanging voor controleprocessen die worden doorlopen op de bouwplaats. Deze zullen nog steeds doorlopen moeten worden. Het doel is wel ontwerpafwijkingen op de bouwplaats te verminderen door miscommunicaties eerder in het proces te verminderen.

