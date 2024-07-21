# RAGtime! Wie man KI-Assistenten und andere Ratgeber zum Tanzen bringt

Session auf der Netzwerk-Recherche-Jahreskonferenz 2024 - alle Folien [als PDF hier.](https://github.com/JanEggers-hr/NR24/raw/main/RAG/NR24%20RAGtime.pdf)

## Use Case 1: BBK-Ratgeber

* [Link zum Ratgeber-PDF](https://www.bbk.bund.de/SharedDocs/Downloads/DE/Mediathek/Publikationen/Buergerinformationen/Ratgeber/ratgeber-notfallvorsorge.pdf?__blob=publicationFile&v=15) - liegt aber auch hier im Github
* Blogartikel mit [Anleitung, wie man den Agenten auf dem "Playground" einrichtet](https://www.janeggers.tech/eeblog/2024/wie-funktionieren-die-gpts-die-neuen-ki-assistenten/)

Kostenlose Alternative im Netz (thx [Oskar Vitlif](https://oskar.tools/)): https://chatpdf.com

### Prompt für den BBK-Ratgeber
```
Du bist ein Berater für die Vorbereitung auf Not- und Krisensituationen. Beantworte Fragen, wie man sich in Notlagen verhält, und wie man sich darauf vorbereiten sollte. 

Vorgehensweise: Lies über Retrieval in der Datei ratgeber-notfallvorsorge.pdf nach. Antworte mit den jeweiligen Textauszügen. Nenne und zitiere Quellen. 

Einschränkungen: Verweigere die Antwort, wenn das Thema der Anfrage nicht in der Datei ratgeber-notfallvorsorge.pdf erwähnt ist. Spekuliere nicht.
```
## Use Case 2: ("fRAG den Staat")

Bei diesem Anwendungsfall ist das richtige Format für Dokument-Bibliothek entscheidend: Die PDFs der ursprünglichen Protokolle kann die KI nicht richtig lesen. Ich habe dafür Python-Code benutzt, der auch im Repository liegt - vielleicht gibt es auch ein Online-Tool. 

Der Python-Code findet sich in einem JuPyter-Notebook, das man beispielsweise auf [Colab](https://colab.google.com) hochladen und ausführen kann. 

* [Blogpost](https://www.janeggers.tech/eeblog/2024/anwendungsfall-fuer-gpts-die-rki-protokolle-mit-ki-hilfe-durchsuchbar-machen/) erklärt den Weg zum Assistenten - und liefert aufbereitete Varianten der (geschwärzten) Protokolle
* [Die RKI-Krisenstab-Protokolle ungeschwärzt als PDF vom RKI](https://www.rki.de/DE/Content/InfAZ/C/COVID-19-Pandemie/COVID-19-Krisenstabsprotokolle_Download.pdf?__blob=publicationFile)
* Für ChatGPT-Plus-Kunden: [Der RKI-Protokolle-GPTs](https://chat.openai.com/g/g-oTgJQDcEG-rki-krisenstab-protokolle) (allerdings noch mit den geschwärzten Protokollen)
* Der Code zum Umformatieren der PDFs in einem Notebook: https://github.com/JanEggers-hr/NR24/blob/main/RAG/NR24/pdf_skripte.ipynb

## Use Case 3: Verurteilt-Podcast-Quizbot

* [Blogpost](https://www.janeggers.tech/eeblog/2024/die-quiz-ki-die-weiss-was-in-110-folgen-verurteilt-passierte/): Wie der Quizbot entstand - und seine Stärken und Schwächen
* Sich den ganzen Installationskram sparen und statt dessen Docker-Container ausführen:
	* [Docker Desktop](https://www.docker.com/) ist der OG für Container. Die Software ist leicht zu installieren, leicht zu verstehen und funktioniert super - leider ist das ehemalige Open-Source-Projekt inzwischen für Menschen in größeren Unternehmen kostenpflichtig. 
	* [Rancher Desktop](https://rancherdesktop.io/) ist eine Docker-Desktop-Alternative des Open-Source-Herstellers SuSE und funktioniert genauso gut, ist aber nicht ganz so komfortabel. Es darf ohne Einschränkung von jedermensch genutzt werden. 
* Verba (das RAG für den eigenen Rechner): https://github.com/weaviate/Verba - Version 2.0 kommt in etwa vier Wochen!
* Ollama: https://www.ollama.com
* Werkstattpost zum Einrichten von Verba mit Ollama folgt!
* Code zum Download und zur Verschriftlichung der Podcast-Folgen mit whisper.cpp folgt!

## Use Case 3a: Eigene Recherche-Notizen, geleakte Dokumente

...funktioniert ganz genau so wie bei den Podcast-Folgen. Ein paar Dinge, die man im Blick behalten sollte - Das hier kann ein RAG-Assistent wie Verba – oder ein GPTs von OpenAI – derzeit nicht:

* **Zählen.** Mit der Frage: “Wie oft wurde im Podcast gemordet?” kann man die KI regelmäßig blamieren. Zählen ist etwas, das Sprachmodelle ohnehin nicht so gut können – und dann beachtet die KI nie alle Schnipsel, die einen Bezug zum Thema haben. Vollständigkeit sollte man von einem RAG-Assistenten nicht erwarten. Und da die KI-Ergebnisse auch hier stark zufallsabhängig sind – wir sprachen darüber – fehlen immer wieder Stellen, an denen das Thema behandelt wurde.
* **Den Kontext des jeweiligen Dokuments erfassen**. Wenn die KI Schnipsel gesucht hat, in denen es um Charly, die Heldentaube geht, “weiß” sie nicht, worum es in der zugehörigen Podcast-Folge ging – um einen Produkterpresser – wenn das nicht zufällig in einem der gefundenen Schnipsel erwähnt wird. Deshalb sollen die Text-Schnipsel in einer zukünftigen Verba-Variante Metadaten mitbekommen; das könnte in unserem Beispiel die Inhaltsangabe der jeweiligen Podcast-Folge sein. Edward hat versprochen, dass er das umsetzen wird, wie viele andere gute Ideen, mit denen man die Leistung des KI-Assistenten weiter verbessern kann.
* **Immer richtig zitieren und zusammenfassen**. Manchmal fasst die KI Textblöcke falsch zusammen, insbesondere, wenn sie den Kontext nicht kennt.
* **Die Quelle korrekt nennen**. Gerade die GPTs von OpenAI tun sich schwer damit, die ursprüngliche Fundstelle korrekt zu zitieren. Seitenzahlen? Schwierig. (Die Alternative chatgpt.com schafft das wesentlich besser!)
* **Größere Strukturen erkennen**. Man kann die KI nicht nutzen, um sich beispielsweise das dreiteilige Special rund um das Schicksal eines Verbrechensopfers zusammenfassen zu lassen. Oder der KI Tolstois Romanschwarte “Krieg und Frieden” zu geben und zu sagen: lies es für mich und schreib mir dann den Aufsatz darüber.

