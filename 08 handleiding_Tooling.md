# Tooling

Onderstaande tooling IfcGref en IFC Georeferencer werken volgens hetzelfde principe, maar verschillen in technische implementatie en gegevensverwerking. IfcGref verwerkt het BIM-model op een server, waardoor het model naar de server wordt geüpload. De IFC Georeferencer werkt daarentegen rechtstreeks in de browser, zodat het model lokaal kan worden verwerkt zonder het naar een externe server te uploaden. De onderliggende werkwijze kan in beide gevallen ook in andere software worden geïntegreerd.

## IfcGref
[IfcGref](https://ifcgref.bk.tudelft.nl/) is een webgebaseerde softwaretool die is ontwikkeld om de georeferentie van IFC (Industry Foundation Classes)-modellen vast te leggen, te verbeteren en te visualiseren. IFC-modellen bevatten vaak uiteenlopende niveaus van georeferentie en geo-informatie, variërend van een eenvoudig postadres (level 10) tot volledige projectie- en coördinatenstelselspecificaties (level 50). [[Hakim2024]] De eerste stap in de workflow van IfcGref is het detecteren van de bestaande geo-informatie in een IFC-bestand en het vaststellen welke gegevens reeds op het niveau level 50 zijn gegeorefereerd.

Ter verbetering van de nauwkeurigheid biedt IfcGref de mogelijkheid om ingemeten punten in te voeren. Dit zijn gemeenschappelijke punten die zowel in de lokale Cartesiaanse coördinaten van het BIM-model als in reële coördinaten binnen een gekozen CRS (Coordinate Reference System) bekend zijn. Door deze twee puntensets op elkaar af te stemmen, legt IfcGref een link tussen het (lokale) BIM-model en de omgeving vastgelegd in de aardoppervlakteprojectie. Vervolgens past de software een Helmert-transformatie toe, waarbij translaties, rotaties en schaalfactoren worden berekend om de twee coördinatenstelsels op elkaar af te stemmen. Deze transformatie wordt opgelost met behulp van de kleinste-kwadratenmethode (via de SciPy-bibliotheek), waardoor de fouten tot een minimum worden beperkt, vooral wanneer meerdere ingemeten punten beschikbaar zijn.

Afhankelijk van het initiële georeferentieniveau van het IFC-bestand kan IfcGref het model upgraden tot level 50. Twee ingemeten punten volstaan om bestanden die oorspronkelijk geen geo-informatie bevatten (level 10 of lager) te georefereren, terwijl slechts één aanvullend ingemeten punt nodig is voor modellen die reeds gedeeltelijke georeferentie-metagegevens bevatten (level 20–40). Voor de omzetting tussen verschillende geografische en geprojecteerde coördinatenstelsels maakt IfcGref gebruik van de pyproj-bibliotheek, wat het proces robuust maakt voor uiteenlopende regio’s en CRS-definities.

<figure id="IfcProjectedCRS-in-IfcGref" style="display: block; text-align: center; margin: 0 auto;">
    <img src="./media/Tooling/ifcProjCRS.png" alt="IfcProjectedCRS attributen en waarden" style="width: 100%; max-width: 600px; height: auto; display: block; margin: 0 auto;"/>
    <figcaption>
      IfcProjectedCRS-attributen en -waarden in IfcGref
    </figcaption>
</figure>

<figure id="IfcMapConversion-in-IfcGref" style="display: block; text-align: center; margin: 0 auto;">
    <img src="./media/Tooling/IfcMapconversion_attributen.png" alt="IfcMapConversion attributen en waarden" style="width: 100%; max-width: 600px; height: auto; display: block; margin: 0 auto;"/>
    <figcaption>
      IfcMapConversion-attributen en -waarden in IfcGref
    </figcaption>
</figure>

Aan het einde van het IfcGref georeferentie-proces wordt het IFC-bestand bijgewerkt met georeferentieattributen, waarna de gebruiker het bewerkte IFC-bestand kan downloaden en direct kan visualiseren op een kaart via de webinterface van IfcGref. Hierdoor kunnen gebruikers de ruimtelijke uitlijning onmiddellijk controleren.

<figure id="Visualisatie-in-IfcGref" style="display: block; text-align: center; margin: 0 auto;">
    <img src="./media/Tooling/ifcGref00.jpg" alt="Visualisatie van het gegeorefereerde model in IfcGref" style="width: 100%; max-width: 600px; height: auto; display: block; margin: 0 auto;"/>
    <figcaption>
      Visualisatie van het gegeorefereerde model in IfcGref
    </figcaption>
</figure>


## IFC Georeferencer 
[IFC Georeferencer](https://geo.buildingsmart.nl/) is een browsergebaseerde tool waarmee IFC-modellen kunnen worden georefereerd. De verwerking vindt volledig lokaal in de browser plaats, waardoor IFC-bestanden niet naar een server worden geüpload.

De tool kan bestaande georeferentie-informatie uitlezen, zoals IfcSite, TrueNorth, IfcMapConversion, IfcProjectedCRS, de IFC4.3-entiteit IfcRigidOperation en IFC2.3-propertyset-alternatieven (ePSet_MapConversion en ePSet_ProjectedCRS). Vervolgens kan de aangepaste georeferentie worden weggeschreven naar een nieuw IFC-bestand dat kan worden gedownload.

Gebruikers kunnen een doel-EPSG-coördinatenstelsel kiezen, een model positioneren op basis van IfcSite, een kaartpunt of ingemeten punten. Daarnaast kan een Helmert-transformatie worden berekend, kunnen restafwijkingen worden beoordeeld en kan het resultaat worden bekeken op een ondergrondkaart met optionele Nederlandse geodata-lagen.

De tool ondersteunt openBIM-workflows waarbij IFC-modellen moeten worden gekoppeld aan GIS, landmeetkundige data, gebiedsontwikkeling, digitale tweelingen of coördinatie van meerdere gebouwen. Hiermee kan georeferentie correct worden toegepast zonder afhankelijk te zijn van gesloten of specifieke authoringsoftware.


