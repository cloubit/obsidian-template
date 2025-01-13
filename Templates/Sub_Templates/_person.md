<%*
// Variablen anlegen, definieren

// Art der Notiz definieren
const personTypeOptions = [
	"Künstler:in",
	"Sänger:in",
	"Musiker:in",
	"Kabarettist:in",
	"Comedian",
	"Schauspieler:in",
	"Autor:in",
	"Journalist:in",
	"Politiker:in",
	"Unternehmer:in",
	"Forscher:in",
	"Andere Person"
	];
personType = await tp.system.suggester(personTypeOptions , personTypeOptions);
// Artspezifische Informationen definieren
if (personType === "Andere Person") {
	personOther = await tp.system.prompt("Bitte gib einen Personentyp ein");
	if (personOther === "" ){personOther = noInfo};
	personType = personOther;
};
// Informationen definieren
personName = await tp.system.prompt("Trage die Namen ein");
if (personName === "" ){personName = noInfo};
artistName = await tp.system.prompt("Trage den Künstlernamen ein");
if (artistName === "" ){artistName = noInfo};
birthDay = await tp.system.prompt("Trage das Geburtsdatum ein");
if (birthDay === "" ){birthDay = noInfo};
death  = await tp.system.prompt("Trage das Todesdatum ein");
if (death === "" ){death = noInfo};
source = await tp.system.prompt("Trage die Quellen als interner [Link] oder externe [Linkbeschreibung](URL) ein");
if (source === "" ){source = noInfo};
personTopic = await tp.system.prompt("Beschreibe die Person in ein bis drei Sätzen");
if (personTopic === "" ){personTopic = noInfo};
relevant = await tp.system.prompt("Trage die Relevanten Werke Kommagetrennt ein. Als interner [Link] oder externer [Linkbeschreibung](URL) ein");
if (personTopic === "" ){personTopic = noInfo};
// Erhobene Informationen erstellen
tR +=  `## :RiInformation2Line: Informationen zur Person
| | |
|:---|:---|
|**Name:** |${personName}|
|**Künstlername** |${artistName}|
|**Geboren:** |${birthDay}|
|**Gestorben:** |${death}|
|**URL Quelle:** |${source}|
|**Wichtiges zur Person:** |${personTopic}|
|**Relevante Werke:** |${relevant}|`;
%>

***
## :FasArrowDownShortWide: Ausführliche Beschreibung der Person
%% # Ab hier bis zu den *** kann der Inhalt individuell und frei gestaltet werden. %%

### :LiBookOpenText: Personenbeschreibung
**Zusammenfassung:** 

**Wichtige Links:** 
 
**Wissenswertes und Notizen:**

**Bewertung :** 


***
%% # Die Struktur des folgenden Abschnitts sollte nur mit bedacht geändert werden. %%
## :RiAdvertisementLine: Weitergehende Informationen zur Person
%% Informationstexte wie diesen dürfen gelöscht werden %%

### :LiNotepadText: Sekundäre Informationen zur Person: 
%% # Hier können Informationen abgelegt werden, die nur indirekt mit der Notiz in Verbindung stehen, für die Notiz aber wichtig und Nützlich sind. %%


### :BoBxMessageSquareDetail: Eigene Erkenntnisse und Gedanken zur Person:
%% # Hier können eigene Erkenntnisse, Erfahrungen, Gedanken usw. der Notiz hinzugefügt werden. %%


### :SiCrowdsource: Quellen: 
%% # Hier können weitere Quellen hinterlegt und gegebenenfalls verlinkt werden, die zum wiederauffinden oder das Verständnis der Notiz wichtig und nützlich sind. %%
<%*
// Interne Links zu erhobenen Informationen werden zur besseren Wiederauffindbarkeit erstellt
tR += `### :CoLink: Weitere interne Links:
[[${contentMark}${noteType}]], [[${contentMark}${personType}]], [[${contentMark}${durability}]]`;
%>
