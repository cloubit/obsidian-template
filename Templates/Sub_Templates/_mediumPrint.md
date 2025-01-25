<%* 
// Variablen anlegen, definieren
mediumTitle = title;
// Art der Notiz definieren
const articleTypeOptions = [
	"Buch",
	"Zeitschrift",
	"Tageszeitung",
	"Artikel",
	"Bericht",
	"Dokument",
	"Gesetz",
	"Anderes Printmedium"
	];
artikelType = await tp.system.suggester(articleTypeOptions , articleTypeOptions);
// Artspezifische Informationen definieren
if (artikelType === "Anderes Printmedium") {
	mediumOther = await tp.system.prompt("Bitte gib ein Medientyp ein");
	if (mediumOther === "" ){mediumOther = noInfo};
	artikelType = mediumOther;
};
// Informationen definieren
autor = await tp.system.prompt("Mehrere Autoren sind kommasepariert einzutragen");
if (autor === "" ){autor = noInfo};
erscheinungsJahr = await tp.system.prompt("Erscheinungsjahr 4 stellig eingeben");
if (erscheinungsJahr === "" ){erscheinungsJahr = noInfo};
mediaTopic = await tp.system.prompt("Beschreibe das Thema in ein bis drei Sätzen");
if (mediaTopic === "" ){mediaTopic = noInfo};
// Erhobene Informationen erstellen
tR += `## :RiInformation2Line: Wichtige Kurzinformationen
| | |
|:---|:---|
|**Artikeltyp:** |${artikelType}|
|**Medientitel:** |${mediumTitle}|
|**Autor/en:** |${autor}|
|**Erscheinungsjahr:** |${erscheinungsJahr}|
|**Thema des Artikels:** |${mediaTopic}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Informationen
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :LiBookOpenText: Inhaltsbeschreibung
**Zusammenfassung :**

**Wichtige Lesezeichen:** 

**Wissenswertes und Notizen:**

**Bewertung :** 

### :BoBxInfoSquare: Essenzielle Informationen
- **Die Welt retten:** Wenn es auch noch weit weg erscheint, die Zeit rennt!


***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
## :RiAdvertisementLine: Weitergehende Informationen
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Informationen
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%


### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%


### :SiCrowdsource: Quellen
%% # Hier können weitere Quellen hinterlegt und gegebenenfalls verlinkt werden, die zum wiederauffinden oder das Verständnis der Notiz wichtig und nützlich sind. %%
<%* 
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[Medien]], [[${contentMark}${artikelType}]], [[${contentMark}${durability}]]`;
%>
