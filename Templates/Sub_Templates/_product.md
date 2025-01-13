<%*
// Variablen anlegen, definieren

// Art der Notiz definieren
const productTypeOptions = [
	"Hardware",
	"Software",
	"Alltagsprodukt",
	"Industrieprodukt",
	"Immaterielle Güter",
	"Dienstleistung",
	"Andere Produkte"
	];
productType = await tp.system.suggester(productTypeOptions , productTypeOptions);
// Artspezifische Informationen definieren
if (productType === "Andere Produkte") {
	productOther = await tp.system.prompt("Bitte gib einen entsprechenden Produkttyp ein");
	if (productOther === "" ){productOther = noInfo};
	productType = productOther;
};
// Informationen definieren
manufacturName = await tp.system.prompt("Trage den Hersteller des Produkts ein");
if (manufacturName === "" ){manufacturName = noInfo};
productName = await tp.system.prompt("Trage den Produktnamen ein");
if (productName === "" ){productName = noInfo};
manufacturNr = await tp.system.prompt("Trage die Herstellernummer des Produkts ein");
if (manufacturNr === "" ){manufacturNr = noInfo};
source = await tp.system.prompt("Trage die Quelle Ein. Als interner [Link] oder externer [Linkbeschreibung](URL) ein");
if (source === "" ){source = noInfo};
productTopic = await tp.system.prompt("Beschreibe das Produkt in ein bis drei Sätzen");
if (productTopic === "" ){productTopic = noInfo};
// Erhobene Informationen erstellen
tR +=  `## :RiInformation2Line: Wichtige Informationen zum Produkt
| | |
|:---|:---|
|**Produkttyp:** |${productType}|
|**Hersteller:** |${manufacturName}|
|**Produkt Name:** |${productName}|
|**Hersteller Nummer** |${manufacturNr}|
|**Quelle:** |${source}|
|**Wichtiges über das Produkt:** |${productTopic}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Produktbeschreibung
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

###  :LiBookOpenText: Produktbeschreibung:
**Zusammenfassung:** 

**Wichtige Links:** 

**Wissenswertes und Notizen:**

**Erweiterungsmöglichkeiten:**

**bekannte Probleme :** 


### :BoBxInfoSquare: Essenzielle Produktinformationen:


***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
## :RiAdvertisementLine: Weitergehende Produktinformationen
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Produktinformationen: 
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%


### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken zum Produkt:
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%


### :SiCrowdsource: Quellen: 
%% # Hier können weitere Quellen hinterlegt und gegebenenfalls verlinkt werden, die zum wiederauffinden oder das Verständnis der Notiz wichtig und nützlich sind. %%
<%*
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[${contentMark}${productType}]], [[${contentMark}${durability}]]`;
%>
