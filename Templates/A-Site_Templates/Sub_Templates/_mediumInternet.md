	<%*
// Variablen anlegen, definieren
mediumTitle = title;
// Art der Notiz definieren
const articleTypeOptions = [
	"Webseite",
	"Blog Artikel",
	"Künstliche Intelligenz",
	"Dokument",
	"Whitepaper",
	"Bericht",
	"FAQ",
	"Anleitung",
	"Online Zeitschrift",
	"Nachrichten",
	"Video",
	"Audio",
	"eBook",
	"Sozial Media",
	"Anderes Internetmedium"
	];
artikelType = await tp.system.suggester(articleTypeOptions , articleTypeOptions);
// Artspezifische Informationen definieren
if (artikelType === "Anderes Internetmedium") {
	mediumOther = await tp.system.prompt("Bitte gib ein Medientyp ein");
	if (mediumOther === "" ){mediumOther = noInfo};
	artikelType = mediumOther;
};
// Informationen definieren
urlName = await tp.system.prompt("Name der URL Quelle eingeben \"Opensource Software\"");
urlSource = await tp.system.prompt("URL Quelle eingeben\"https://opensource.com\"");
lastCall = await tp.system.prompt("Datum des letzten Anfrage im Format DD.MM.MMMM. Enter um aktuelles Datum einzutragen");
if (lastCall === "" ){lastCall = tp.date.now("DD.MM.YYYY")};
mediaTopic = await tp.system.prompt("Beschreibe das Thema in ein bis drei Sätzen");
if (mediaTopic === "" ){mediaTopic = noInfo};
// Erhobene Informationen erstellen
tR += `## :RiInformation2Line: Informationen zum Online Medium
| | |
|:---|:---|
|**Artikeltyp:** |${artikelType}|
|**Medientitel:** |${mediumTitle}|
|**URL Quelle:** |[${urlName}]("${urlSource}")|
|**Datum des letzten Aufrufs:** |${lastCall}|
|**Thema:** |${mediaTopic}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Beschreibung des Online Mediums
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :LiBookOpenText: Inhaltsbeschreibung des Online Medium
**Zusammenfassung:**

**Wichtige Links:** 
 
**Wissenswertes und Notizen:**

**Bewertung :** 

### :BoBxInfoSquare: Essenzielle Informationen zum Online Medium:



***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
## :RiAdvertisementLine: Weitergehende Informationen zum Online Medium
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Informationen zum Online Medium: 
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%


### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken zum Online Medium:
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%


### :SiCrowdsource: Quellen: 
%% # Hier können weitere Quellen hinterlegt und gegebenenfalls verlinkt werden, die zum wiederauffinden oder das Verständnis der Notiz wichtig und nützlich sind. %%
<%* 
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[Medien]], [[${contentMark}${artikelType}]], [[${contentMark}${durability}]]`;
%>
