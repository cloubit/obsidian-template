<%* 
// Variablen anlegen, definieren
mediumTitle = title;
// Art der Notiz definieren
const articleTypeOptions = [
	"Radio Sendung",
	"Radio Interview",
	"Radio Dokumentation",
	"Radio Nachrichten",
	"TV Sendung",
	"TV Interview",
	"TV Dokumentation",
	"TV Nachrichten",
	"Anderes Radio-TV-Medium"
	];
artikelType = await tp.system.suggester(articleTypeOptions , articleTypeOptions);
// Artspezifische Informationen definieren
if (artikelType === "Anderes Radio-TV-Medium") {
	mediumOther = await tp.system.prompt("Bitte gib ein Medientyp ein");
	if (mediumOther === "" ){mediumOther = noInfo};
	artikelType = mediumOther;
};
// Informationen definieren
transmitter = await tp.system.prompt("Radio TV Sender eingeben");
if (transmitter === "" ){transmitter = noInfo};
overAirDate = await tp.system.prompt("Ausstrahlungsdatum eingeben \"31.12.2022\"");
if (overAirDate === "" ){overAirDate = noInfo};
mediaTopic = await tp.system.prompt("Beschreibe das Thema in ein bis drei Sätzen");
if (mediaTopic === "" ){mediaTopic = noInfo};
// Erhobene Informationen erstellen
tR +=  `## :RiInformation2Line: Wichtige Kurzinformationen
| | |
|:---|:---|
|**Artikeltyp:** |${artikelType}|
|**Medientitel:** |${mediumTitle}|
|**Sender:** |${transmitter}|
|**Erscheinungsjahr:** |${overAirDate}|
|**Thema der Sendung:** |${mediaTopic}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Beschreibung
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :LiBookOpenText: Inhaltsbeschreibung
**Zusammenfassung der Sendung:** 

**Wichtige Zeitangaben und Kurzbeschreibungen zur Auffindbarkeit wichtiger Aussagen :** 

**Wissenswertes und Notizen:**

**Bewertung:** 

### :BoBxInfoSquare: Essenzielle Informationen


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
