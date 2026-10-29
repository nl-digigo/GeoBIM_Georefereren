# Methodes voor georeferentie

## Routes voor georeferentie

Wanneer men een BIM-model daadwerkelijk gaat realiseren op de bouwplaats, worden de coördinaten uit het model uitgezet in de werkelijkheid. Dit betekent dat het digitale coördinatensysteem van het BIM-model wordt gekoppeld aan vaste referentiepunten op de bouwplaats. Vanuit deze koppeling worden assen, stramienen (hulplijnen), hoogtes en punten vanuit het BIM-model uitgezet met meetapparatuur zoals een total station. De posities daarvan markeert men fysiek in het veld, bijvoorbeeld met piketten of andere markeringen. Voor omvangrijke projecten kan dit proces ook worden ondersteund door machinebesturing. Een BIM-model vormt zo de basis voor de maatvoering in constructie in de werkelijkheid. Met bijvoorbeeld een rolmaat, of laserafstandsmeter doet men snelle metingen en detailcontrole op de bouwplaats. 

Om de gecreëerde fysieke werkelijkheid vast te leggen in een coördinatensysteem meet men objecten weer in, met meetapparatuur zoals een total station en RTK-GNSS. Hiervoor meet men o.a. de hoekpunten en dakranden van gebouwen in. Alle gemeten punten worden omgerekend naar RD (x,y) met de hoogte in NAP. Vervolgens worden de punten in GIS/CAD-software verbonden tot polygonen, classificeert men de objecten en voegt men attributen toe.  

<figure id="Routes-voor-georefereren" style="display: block; text-align: center; margin: 0 auto;">
  <img src="media/Georeferentie Informatie Levels/Routes_voor_Georefereren.png" alt="Routes voor georefereren" style="width: 100%; max-width: 500px; height: auto; display: block; margin: 0 auto;">
  <figcaption><a class="self-link" href="#fig-Routes-voor-georefereren"></a><span class="fig-title">Routes voor georefereren</span></figcaption>
</figure>

Wanneer men een BIM-model, dat gemodelleerd is in een lokaal cartesisch CRS (engineering CRS), in <a>geo-software</a> wil importeren, zonder de route uit te zetten en in te meten, moet men een transformatie doen. Afhankelijk van de situatie zijn er verschillende methodes beschikbaar om BIM-modellen en geodata samen te voegen in één omgeving. Een in RD ingemeten (as-built) gebouwgeometrie kan men bijvoorbeeld vergelijken met een XYZ (as-designed) BIM-gebouwgeometrie, na een 2D-gelijkvormigheidstransformatie en hoogtecorrectie, waarin translaties, rotatie en schaal aangegeven dienen te worden. 

## 1D, 2D en 3D Geo- en BIM-modellen
Zowel BIM-modellen als geodata kunnen een 2D, 3D of samengesteld coördinatenstelsel gebruiken. Om een juiste transformatie te verkrijgen kunnen verschillende transformatiemethoden worden toegepast. 

Onderstaande figuur geeft schematisch weer hoe een bronmodel (Source) in een ander model (Target) geplaatst kan worden. Wanneer bron en doel hetzelfde zijn, is de combinatie gemakkelijk. Wanneer er verschillen in dimensie of CRS zijn tussen bron en doel, zijn verschillende methodieken nodig. 

<div style="display: flex; gap: 10px;">
  <figure id="2D-en-3D-Geo-of-BIM-combineren-deel-1">
      <img src="./media/Georeferentie Informatie Levels/2d_en_3d_GeoBIM_1.png" alt="2D en 3D Geo of BIM combineren (1)" width="400"/>
    <figcaption><a class="self-link" href="#fig-2D-en-3D-Geo-of-BIM-combineren-deel-1"></a><span class="fig-title">2D en 3D BIM-model en geodata combineren (1)</span></figcaption>
</figure>
  <figure id="2D-en-3D-Geo-of-BIM-combineren-deel-2">
      <img src="./media/Georeferentie Informatie Levels/2d_en_3d_GeoBIM_2.png" alt="2D en 3D Geo of BIM combineren (2)" width="700"/>
    <figcaption><a class="self-link" href="#fig-2D-en-3D-Geo-of-BIM-combineren-deel-2"></a><span class="fig-title">2D en 3D BIM-model en geodata combineren (2)</span></figcaption>
</figure>
</div>

Onderstaande tabel geeft een aanbeveling voor transformatie bij een bepaalde bron en een bepaald doel. 

<table style="width:100%; table-layout:fixed; font-size:80%;">
<caption>Transformatie tussen 2D, 3D en samengestelde coördinatenstelsels van BIM-modellen en/of geodata</caption>
  <thead>
    <tr>
    <th>Bron (Source) <br>&#8725;<br>Doel (Target)</th>
      <th>2D RD</th>
      <th>2D XY lokaal</th>
      <th>2D ETRS89</th>
      <th>2D+1D RDNAP</th>
      <th>3D XYZ lokaal</th>
      <th>3D ETRS89</th>
      </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>2D RD</strong></td>
      <td>Nultransformatie</td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a></td>
      <td>RDNAPTRANS zonder hoogte</td>
      <td>Nultransformatie en interpolatie naar NAP-hoogte van het doel</td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a> en interpolatie naar Z-waarde van het doel</td>
      <td>RDNAPTRANS</td>
    </tr>
    <tr>
      <td><strong>2D XY lokaal</strong></td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a></td>
      <td>Nultransformatie</td>
      <td><a href="#x3d-gelijkvormigheidstransformatie-voor-geografisch-crs">3D-Helmerttransformatie</a> met Z=0 (zonder gebruik ellipsoïdische hoogte)</td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a> en interpolatie naar NAP-hoogte van het doel</td>
      <td>Nultransformatie en interpolatie naar Z-waarde van het doel</td>
      <td><a href="#x3d-gelijkvormigheidstransformatie-voor-geografisch-crs">3D-Helmerttransformatie</a> met Z=0 en interpolatie naar ellipsoïdische hoogte van het doel</td>
    </tr>
    <tr>
      <td><strong>2D ETRS89</strong></td>
      <td>RDNAPTRANS zonder hoogte</td>
      <td><a href="#x3d-gelijkvormigheidstransformatie-voor-geografisch-crs">3D-Helmerttransformatie</a> met h=43 m (zonder gebruik Z-waarde)</td>
      <td>Nultransformatie</td>
      <td>RDNAPTRANS zonder hoogte en interpolatie naar NAP-hoogte van het doel</td>
      <td><a href="#x3d-gelijkvormigheidstransformatie-voor-geografisch-crs">3D-Helmerttransformatie</a> met h=43 m en interpolatie naar Z-waarde van het doel</td>
      <td>Nultransformatie en interpolatie naar ellipsoïdische hoogte van het doel</td>
    </tr>
    <tr>
      <td><strong>2D+1D RDNAP</strong></td>
      <td>Nultransformatie (zonder gebruik NAP-hoogte)</td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a> (zonder gebruik NAP-hoogte)</td>
      <td>RDNAPTRANS zonder hoogte</td>
      <td>Nultransformatie</td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a> en 1D-Helmerttransformatie van hoogte</td>
      <td>RDNAPTRANS</td>
    </tr>
    <tr>
      <td><strong>3D XYZ lokaal</strong></td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a></td>
      <td>Nultransformatie (zonder gebruik Z-waarde)</td>
      <td><a href="#x3d-gelijkvormigheidstransformatie-voor-geografisch-crs">3D-Helmerttransformatie</a> (zonder gebruik ellipsoïdische hoogte)</td>
      <td><a href="#2D-gelijkvormigheidstransformatie">2D-Helmerttransformatie</a> en 1D-Helmerttransformatie van hoogte</td>
      <td>Nultransformatie</td>
      <td><a href="#x3d-gelijkvormigheidstransformatie-voor-geografisch-crs">3D-Helmerttransformatie</a></td>
    </tr>
    <tr>
      <td><strong>3D ETRS89</strong></td>
      <td>RDNAPTRANS zonder hoogte</td>
      <td><a href="#x3d-gelijkvormigheidstransformatie-voor-geografisch-crs">3D-Helmerttransformatie</a> (zonder gebruik Z-waarde)</td>
      <td>Nultransformatie (zonder gebruik ellipsoïdische hoogte)</td>
      <td>RDNAPTRANS</td>
      <td>3D-gelijkvormigheidstransformatie</td>
      <td>Nultransformatie</td>
    </tr>
  </tbody>
</table>

## Methodes voor georeferentie 

### RD-gemodelleerd BIM naar RDNAP 
Het is mogelijk om "RD bewust" te modelleren in BIM. Wanneer men dit doet moet men rekening houden met de [schaalcorrectie voor RD](#schaalfout-door-projectie). Een project in de stad Amersfoort moet vanwege projectie in RD ca. 9 mm per 100 meter kleiner getekend worden dan hoe het in werkelijkheid moet worden. Een lijn van 400 meter zal dan als een lijn van +/- 396,4 meter gemodelleerd moeten worden. De vergroting of reductie geldt niet voor verticale lijnen en NAP-hoogtes in het model. Dit vereist grote zorgvuldigheid van de modelleur. Een alternatief is de afwijking accepteren. 
De transformatie van lokaal XYZ-BIM als RDNAP in BIM naar RDNAP is een "nultransformatie". 

### XYZ gemodelleerd BIM als RD naar RDNAP 
Het is mogelijk dat de transformatie van lokaal XYZ in BIM naar RDNAP-coördinaten door BIM-software wordt ondersteund. In dit geval zal de software bij een commando om een lijn van 400 meter te maken in BIM in Amersfoort eigenlijk een lijn van 396,4 meter in RD maken die overeenkomt met een lijn van 400 m in werkelijkheid. Deze methode komt overeen met de methode hierboven beschreven. Het verschil in de methode zit in het feit dat niet de modelleur, maar de software de schaalcorrectie doet om het model in RD te tekenen. 
De transformatie van RDNAP in BIM naar RDNAP is een "nultransformatie". 

### XYZ gemodelleerd BIM via een 2D-gelijkvormigheidstransformatie naar RDNAP 
Een andere methode is om een in lokaal cartesisch XYZ gemodelleerd BIM-model met een 2D-gelijkvormigheidstransformatie naar RD met NAP-hoogte te transformeren. Een schaalparameter is, afhankelijk van de locatie in Nederland, vaak nodig. Belangrijk hierbij is dat de hoogtewaarde geen schaalcorrectie dient te krijgen. 

Zonder schaalcorrectie kunnen afwijkingen optreden zoals beschreven in [Afwijkingen](#afwijkingen). Zonder correctie ontstaat een afwijking van 1 cm bij 100 meter wanneer bron en doel gecombineerd worden. Bij toepassing van een RD-schaalcorrectie voor XY en dezelfde schaalcorrectie voor Z, is de afwijking 1 cm bij een model van 500 meter en maximaal 100 meter hoogteverschil (&Delta;H), of 10 cm bij een model van 5 km. Bij toepassing van de RD-schaalcorrectie op XY en niet voor Z, dan is de afwijking vergelijkbaar door vervorming door het RD-correctiegrid en de aardkromming. Voordeel van deze laatste methode is dat deze ook voor modellen met een kleinere lengte (L) en een groter hoogteverschil (&Delta;H) en op zee te gebruiken is, bijvoorbeeld L=200 m en &Delta;H=320 m.

### XYZ gemodelleerd BIM via een 3D-gelijkvormigheidstransformatie naar ETRS89 
Een volgende methode is om een in lokaal cartesisch XYZ gemodelleerd BIM-model met een 3D-gelijkvormigheidstransformatie te transformeren naar cartesisch XYZ in het geocentrische ETRS89-coördinatenstelsel. Dit getransformeerde model kan men vervolgens converteren naar breedte, lengte en hoogte in geografisch 3D ETRS89 en transformeren naar RDNAP. 

Doordat het model niet met de aardkromming meebuigt onstaat er een hoogtefout bij deze methode zoals eerder beschreven. Daarnaast staan objecten uit het model niet loodrecht op het gekromde aardoppervlak. Dit effect is verwaarloosbaar. Er treedt geen vervorming op van het model. 

### XYZ gemodelleerd BIM via 3D een 3D-gelijkvormigheidstransformatie naar ETRS89 en hoogte naar NAP 
Deze methode waarbij men BIM via een 3D-gelijkvormigheidstransformatie naar ETRS89 brengt en de hoogte naar NAP lijkt op de hiervoor beschreven methode. Het verschil is dat men in deze methode de hoogte apart, als 1D-transformatie, naar NAP transformeert. Deze methode transformeert allereerst XYZ-data met een 3D-gelijkvormigheidstransformatie naar ETRS89. De hoogte transformeert men daarna apart als 1D-transformatie naar NAP. De breedte en lengte in ETRS89 kan men vervolgens transformeren naar RD en er de NAP-hoogte aan toevoegen voor RDNAP-coördinaten.

Deze optie geeft een oplossing voor de hoogteafwijking zoals in de hiervoor beschreven methode optreedt. Wel genereert deze methode vervorming van het orginele model. Deze vervorming is 1 cm bij een model dat zich maximaal 2 km strekt en een maximale hoogte heeft van 32m. De vervorming is ook 1 cm bij een model dat zich 200m uitstrekt met een hoogte van maximaal 320 meter.

### Conclusie 
Om bovenstaande methodes uit te voeren is een bepaald level aan georeferentie-informatie nodig. Met het hieronder beschreven level 50 georeferentie-informatie zijn de nultransformaties, en 2D+1D-Helmerttransformaties te voorzien van informatie. Voor een 3D-Helmerttransformatie en de 3D+1D-Helmerttransformatie zijn 7 transformatieparameters nodig. Die kunnen alleen worden voorzien met een uitbreiding van level 50 of op basis van impliciete aannames. Bij gebruik van level 60 is geen uitbreiding nodig, mits de software de 7 parameters zelf kan berekenen uit de referentiepunten.


## Levels van georeferentie-informatie
Voor gegeorefereerde data zijn verschillende referentiegegevens of transformatieparameters nodig. Deze gegevens beschrijven bijvoorbeeld het gebruikte coördinatenstelsel, transformatieparameters of referentiepunten. Deze informatie is nodig om de brondata (source) correct te koppelen aan een geografische locatie (target).

Deze gegevens kunnen op verschillende manieren beschikbaar zijn. Soms zijn deze aanwezig in de brondata waarin informatie voor georeferentie reeds opgenomen is, in metadata of in gekoppelde bestanden zoals een prj-bestand (proj). Hierdoor kan de positionering grotendeels automatisch plaatsvinden. Wanneer parameters voor een bepaalde methode ontbreken, kan men dit aanvullen. De gegevens daarvoor kan men verzamelen uit externe bronnen of door handmatige interpretatie van referentiekaarten of bekende referentiepunten. Dit proces vergt extra validatie om de nauwkeurigheid en betrouwbaarheid van de georeferentie te waarborgen.

De kwaliteit van deze parameters heeft directe invloed op het georeferentieproces en de uiteindelijke bruikbaarheid van de ruimtelijke data. In een onderzoek van Clemen en Görne [[Clemen2019]] worden verschillende levels van georeferentie-informatie beschreven. De verschillende levels faciliteren verschillende methodes van georeferentie en verschillen in de te behalen nauwkeurigheid en mogelijkheid voor het samenvoegen van modellen. 

### Level 10 

Een locatienaam opgeven:

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <div>
<img src="./media/Georeferentie Informatie Levels/georefereren_Level_10.png" alt="Georeferentie level 10" title="Georeferentie level 10" style="float: left; width: min(300px, 35vw); height: auto; margin: 0 20px 10px 0;">
  </div>
  <div>
    <p>
      Met dit informatielevel wordt alleen de locatie waar een model moet komen benoemd. Bijvoorbeeld door een adres als "Barchman Wuytierslaan 10, Amersfoort" in een model op te nemen. Men weet hierdoor op welk adres het model moet komen, maar exacte plaatsing, rotatie en schaling zijn hier niet uit te bepalen.
    </p>
  </div>
</div>

### Level 20 

 Voor één punt coördinaten opgeven:

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <div>
<img src="./media/Georeferentie Informatie Levels/georefereren_Level_20.png" alt="Georeferentie level 20" title="Georeferentie level 20" width="300">
  </div>
  <div>
    <p>
      Met dit informatielevel duidt men één enkel punt (breedte- en lengtegraad) waar het model geplaatst moet worden. Bijvoorbeeld met de coördinaten "52.15249407, 5.37205549". Plaatsing van het model op de juiste plek, zowel in 2D als in 3D wordt hiermee mogelijk. Rotatie en schalen van het model blijft niet mogelijk.
    </p>
  </div>
</div>

### Level 30

De positie en richting van het grondvlak specificeren:

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <div>
      <img src="./media/Georeferentie Informatie Levels/georefereren_Level_30.png" alt="Georeferentie level 30" title="Georeferentie level 30" width="300">
  </div>
  <div>
    <p>
      Met dit informatielevel wordt aan het grondvlak van een model een verplaatsing ten opzichte van het model nulpunt toegekend die overeenkomt met het beoogd coördinaatrefentiesysteem. Objectplaatsing wordt gebruikt als georeferentie. Doordat elementen een ruimtelijke relatie hebben met het grondvlak worden deze elementen ook juist geplaatst en kunnen coördinaten van deze elementen klein gehouden worden. Ook is het mogelijk om de rotatie ten opzichte van het Noorden te duiden. Het schalen van het model is niet mogelijk. Ook is het niet mogelijk om het CRS waarvoor de coördinaat gelden te duiden.
    </p>
  </div>
</div>

### Level 40

De positie en richting van het model duiden:

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <div>
      <img src="./media/Georeferentie Informatie Levels/georefereren_Level_40.png" alt="Georeferentie level 40" title="Georeferentie level 40" width="300">
  </div>
  <div>
    <p>
      Met dit informatielevel wordt aan het <strong>totaalmodel</strong> een coordinaat toegekend, en ook de rotatie ten opzichte van Noorden kan men duiden. De georeferentie is een aparte entiteit, en is daarmee expliciet geduid. De methode komt verder overeen met level 30. Het schalen van het model is niet mogelijk. Ook is het niet mogelijk om het CRS waarvoor het coordinaat geldt te duiden.
    </p>
  </div>
</div>


### Level 50

Het bron-CRS, het doel-CRS en de transformatie specificeren:: 

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <div>
  <img src="./media/Georeferentie Informatie Levels/georefereren_Level_50.png" alt="Georeferentie level 50" title="Georeferentie level 50" width="600">
  </div>
  <div>
    <p>
      Met dit informatielevel geeft men aan wat het oorspronkelijk coördinatenstelsel is waarin het model is gemodelleerd. Daarnaast geeft men in het model aan naar welk coördinatenstelsel een coversie gedaan wordt. Heeft men bijvoorbeeld gemodelleerd vanuit een lokaal assenstelsel (0,0,0) dan kan men beschrijven welke translatie, rotatie en verschaling men moet toepassen om te kunnen combineren met data in RD-coördinaten
    </p>
  </div>
</div>


### Level 60

Coördinaten van referentiepunten in het BIM-model en een CRS: 

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <div>
      <img src="./media/Georeferentie Informatie Levels/georefereren_Level_60.png" alt="Georeferentie level 60" title="Georeferentie level 60" width="600">
  </div>
  <div>
    <p>
      Met dit informatielevel koppelt men punten in het model aan ingemeten punten tijdens constructie aan coördinaten in een specifiek coördinatenstelsel
    </p>
  </div>
</div>

### Mogelijkheden en toepassingen
De beschikbaarheid van informatie voor het berekenen van georeferentie-parameters voor de verschillende methoden is onderzocht door de TU Delft [[Hakim2024]]. Een hoger level van georeferentie geeft een model explicietere, completere en beter gestructureerde georeferentie-informatie. Dit geeft meer mogelijkheden in gebruik. Een hoger level van georeferentie stelt ook hogere eisen aan datakwaliteit en expertise. Georeferentie kan men gedurende een ontwerpproces stapsgewijs opbouwen, parallel aan de toenemende detaillering van een ontwerp. In de initiatieffase (INI) en haalbaarheidsfase (HBH) kan een globale geografische positionering volstaan. Vanaf de projectdefinitie (PD) worden de ruimtelijke uitgangspunten verder vastgelegd. In het structuurontwerp (SO) en voorontwerp (VO) wordt de situering bepaald en afgestemd op de omgeving. In de daaropvolgende fasen (DO–UO) worden de positionering en coördinaten nauwkeuriger uitgewerkt en consistent toegepast. Tijdens uitvoering, oplevering en beheer (UV–GB) wordt de georeferentie waar nodig geverifieerd en bijgewerkt op basis van de gerealiseerde situatie, zodat ontwerp- en beheergegevens onderling uitwisselbaar blijven. Men kan in sommige situaties besluiten een lager level van georeferentie aan te houden. De hierboven beschreven methodes van georeferentie bieden onderstaande mogelijkheden en kunnen worden toegepast in de beschreven situaties. Bij een hoger level van georefentie van een model blijven de toepassingsvoorbeelden van lager niveaus ook werken. 

<table>
  <tr>
    <th width ="50"> Level </th>
    <th> Georeferentie-informatie </th>
    <th> Translatie XY </th>
    <th> Translatie Z </th>
    <th> Rotatie </th>
    <th> Schaal XY </th>
    <th> Schaal Z </th>
    <th> Toepassingsvoorbeeld </th>
  </tr>
  <tr>
    <td> 10 </td>
    <td> Het benoemen van een adres </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> Voor administratieve analyses of voor navigatie naar de locatie van het BIM-model</td>
  </tr>
  <tr>
    <td> 20 </td>
    <td> Het specificeren van één punt </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> Voor het weergeven van een model als punt op de kaart en analyses zonder geometrische context </td>
  </tr>
  <tr>
    <td> 30 </td>
    <td> Het specificeren van één punt en verdraaiing van het grondvlak </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> 🔶 </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> Voor niet-geometrische analyses of controle van rotatie </td>
  </tr>
  <tr>
    <td> 40 </td>
    <td> Het specificeren van punt en verdraaiing van het totaalmodel </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> 🔶 </td>
    <td> ❌ </td>
    <td> ❌ </td>
    <td> Voor niet-geometrische analyse of controle van rotatie </td>
  </tr>
  <tr>
    <td> 50 </td>
    <td> Het aangeven van een bron-CRS en de 2D+1D-Helmerttransformatie naar een doel-CRS </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> ✅  </td>
    <td> ✅  </td>
    <td> 🔶  </td>
    <td> Voor het combineren van geodata en BIM-modellen in applicaties t.b.v. visualisatie en analyse, coördinatie of integratie </td>
  </tr>
  <tr>
    <td> 60 </td>
    <td> Koppeling van punten in BIM, Geo en op een fysiek terrein </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> ✅ </td>
    <td> Als het BIM-model gebruikt moet worden voor constructie of andere toepassingen waarbij de positie van het model in het terrein landmeetkundig aanwijsbaar moet zijn. </td>
  </tr>
</table>

✅ = Mogelijk
🔶 = Optioneel
❌ = Niet mogelijk

<aside class="note" title="Te gebruiken level van georeferentie">
  <p><strong>AANBEVELING:</strong> Gebruik voor integratie van BIM-modellen en geodata level 50 georeferentie en voor constructiedoeleinden level 60 van georeferentie.  </p>
</aside>
<aside class="note" title="Gebruik tooling om modellen te verrijken">
<p><strong>AANBEVELING:</strong> Gebruik tooling om modellen die nog niet voldoen aan georeferentie level 50, wanneer nodig, te verrijken met georeferentie-informatie conform level 50. </p>
</aside>

## Schaal en correctie op basis van gebruikte eenheden
Geodata of een BIM-model kan in een andere eenheid zijn opgesteld dan het coördinatenstelsel waarnaar het moet worden getransformeerd. Het is daarom essentieel om de gebruikte eenheden expliciet te specificeren in het model. Wanneer de bron bijvoorbeeld in millimeters is gemodelleerd en het doel meters gebruikt, moet er een eenheidsconversie worden toegepast. 

Leg daarom altijd twee dingen vast. Ten eerste specificeert men de gebruikte eenheden expliciet in het model. Ten tweede geeft men in de georeferentie-informatie de schaal aan die bij dat verschil in eenheden hoort, bijvoorbeeld 0,001 voor millimeter naar meter of 0,0254 voor inch naar meter. De eenheden en de schaal moeten met elkaar in overeenstemming zijn. Software kan dan aan de eenheden controleren of de schaal klopt. Het risico van deze aanpak is dat software die de eenheden correct interpreteert, de schaalcorrectie opnieuw toepast, wat leidt tot een dubbele conversie en dus foutieve geometrie.

<figure id="Schaalprobleem_bij_georefereren" style="display: block; text-align: center; margin: 0 auto;">
  <img src="media/Georeferentie Informatie Levels/Schaalfout_bij_Georeferentie.jpg" alt="Schaal en/of eenheden probleem bij georefereren" style="width: 100%; max-width: 500px; height: auto; display: block; margin: 0 auto;">
  <figcaption><a class="self-link" href="#fig-Schaalprobleem_bij_georefereren"></a><span class="fig-title">Schaal- en/of eenhedenprobleem bij georefereren</span></figcaption>
</figure>

<aside class="note" title="Gebruik van schaal voor eenheidconversie"> <p><strong>AANBEVELING:</strong> Gebruik één schaalparameter binnen georeferentie uitsluitend voor eenheidsconversies. Dit kan men bijvoorbeeld doen met het scale attribuut in <a href="https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcMapConversion.htm">IfcMapConversion</a>. Definieer aanvullend daarop eenheden expliciet via de daarvoor bestemde attributen, zoals <a href="https://ifc43-docs.standards.buildingsmart.org/IFC/RELEASE/IFC4x3/HTML/lexical/IfcUnitAssignment.htm">IfcUnitAssignment</a>.</p> </aside>

<aside class="note" title="Gebruik van schaal voor geometrische transformaties"> <p><strong>AANBEVELING:</strong> Gebruik drie schaalparameters binnen georeferentie uitsluitend voor geometrische transformaties binnen het coördinatensysteem (bijvoorbeeld CRS-transformaties). Hiervoor gebruikt men bijvoorbeeld <a href="https://standards.buildingsmart.org/IFC/RELEASE/IFC4_3/HTML/lexical/IfcMapConversionScaled.htm">IfcMapConversionScaled</a>, waarmee men met de aparte schaalfactoren, (FactorX, FactorY en FactorZ) kan definieren. Dit maakt een nauwkeurigere combinatie met data mogelijk die een verschillende x,y en z schaal kunnen hebben zoals RDNAP. </p> </aside>


## Prototypische modellen en catalogusmodellen
Prototypische modellen en catalogusmodellen zijn herbruikbare modellen die als basis dienen voor meerdere instanties, zoals een boomtype dat op verschillende locaties wordt geplaatst of een lichtmast die meerdere keren in een gebied voorkomt. Binnen geo-uitwisseling ([CityGML](https://www.ogc.org/standards/citygml/)) zijn voorzieningen beschikbaar om dergelijke geometrie ([ImplicitGeometry](https://docs.ogc.org/is/20-010/20-010.html#ImplicitGeometry-section)) herbruikbaar uit te wisselen en op verschillende locaties toe te passen. IFC biedt hiervoor geen vergelijkbare, eenduidige werkwijze. In de ontwerpfase daarom volstaan met het vastleggen van het lokale coördinatenstelsel. De daadwerkelijke georeferentie en positionering van de modelinstanties kan vervolgens bij de realisatie in projecten worden uitgewerkt, wanneer de definitieve locatie en oriëntatie bekend zijn.


