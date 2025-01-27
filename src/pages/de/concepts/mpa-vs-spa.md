---
layout: ~/layouts/MainLayout.astro
title: MPA vs. SPA
description: "Das Verständnis der Architektur-Kompromisse zwischen einer Multi-Page-Anwendung (MPA) und einer Single-Page-Anwendung (SPA) ist der Schlüssel zum Verständnis, was Astro von anderen Web-Frameworks unterscheidet."
i18nReady: true
---

Um zu verstehen, was Astro von anderen Web-Frameworks wie Next.js und Remix unterscheidet, muss man die Kompromisse zwischen der Architektur von Multi-Page-Anwendungen (MPAs) und Single-Page-Anwendungen (SPAs) verstehen.

## Terminologie

Eine **Multi-Page-Anwendung (MPA)** ist eine Website, die aus mehreren HTML-Seiten besteht, die meist auf einem Server gerendert werden. Wenn du zu einer neuen Seite navigierst, fordert dein Browser eine neue HTML-Seite vom Server an. **Astro ist ein MPA-Framework.** Zu den traditionellen MPA-Frameworks gehören auch Ruby on Rails, Python Django, PHP Laravel, WordPress und statische Website-Baukästen wie Eleventy oder Hugo.

**Eine Single-Page-Anwendung (SPA)** ist eine Website, die aus einer einzigen JavaScript-Anwendung besteht, welche im Browser geladen wird und dann lokal HTML erzeugt. SPAs können *auch* HTML auf dem Server erzeugen, aber SPAs haben die besondere Fähigkeit, deine Website als JavaScript-Anwendung im Browser auszuführen, um neue HTML-Inhalte zu erzeugen, wenn du zwischen Seiten navigierst. Next.js, Nuxt, SvelteKit, Remix, Gatsby und Create-React-App sind alles Beispiele für SPA-Frameworks.

## Astro vs. andere MPAs

Astro ist ein MPA-Framework. Astro unterscheidet sich jedoch auch von anderen MPA-Frameworks. Der Hauptunterschied besteht darin, dass es JavaScript als Server- und Laufzeitsprache verwendet. Bei herkömmlichen MPA-Frameworks müsstest du eine andere Sprache auf dem Server (Ruby, PHP usw.) und JavaScript im Browser verwenden. In Astro scheibst du immer nur JavaScript, HTML und CSS. Auf diese Weise kannst du deine UI-Komponenten (wie React und Svelte) sowohl auf dem Server als auch auf dem Client rendern.

Das Ergebnis ist eine Entwicklererfahrung, die Next.js und anderen modernen Web-Frameworks sehr ähnlich ist, aber die Leistungsmerkmale einer traditionelleren MPA-Seiten-Architektur aufweist.

## MPAs vs. SPAs

Beim Vergleich von MPAs und SPAs gibt es drei Hauptunterschiede, die zu beachten sind:

#### Server-Rendering (MPA) vs. Client-Rendering (SPA)

Bei MPAs wird der größte Teil des HTML-Codes deiner Seite auf dem Server gerendert. Bei SPAs wird das meiste HTML lokal gerendert, indem JavaScript im Browser ausgeführt wird. Dies hat erhebliche Auswirkungen auf das Verhalten der Website, die Leistung und die Suchmaschinenoptimierung.

Das Rendern von HTML im Browser scheint die schnellere Option zu sein, als es von einem entfernten Server anzufordern. Das Gegenteil ist jedoch der Fall. Eine SPA wird beim ersten Laden der Seite durchweg langsamer sein als eine MPA, es sei denn, es wird Server-Rendering verwendet. Das liegt daran, dass eine SPA eine ganze JavaScript-Anwendung herunterladen, analysieren und im Browser ausführen muss, nur um HTML auf der Seite zu rendern. Dann muss deine SPA wahrscheinlich ohnehin Remote-Daten abrufen, was zu noch mehr Wartezeit führt, bevor deine Seite fertig geladen ist.

Die meisten SPA-Frameworks versuchen, dieses Leistungsproblem durch Hinzufügen eines grundlegenden Server-Renderings beim ersten Laden der Seite zu entschärfen. Dies ist zwar eine Verbesserung, führt aber zu neuer Komplexität, da deine Website nun auf mehrere Arten und in mehreren Umgebungen (Server, Browser) gerendert werden kann. Dies führt auch zu einem neuen "uncanny valley"-Problem, bei dem deine Website geladen erscheint (HTML), aber nicht reagiert, da die JavaScript-Logik der Anwendung noch im Hintergrund geladen wird.

MPAs rendern das gesamte HTML auf einem entfernten Server und benötigen oft nur wenig JavaScript (wenn überhaupt) zur Ausführung. Dies führt dazu, dass MPAs viel schneller geladen werden als SPAs, was für inhaltsorientierte Websites wichtig ist. Dies bringt jedoch einen Nachteil mit sich: Die zukünftige Seitennavigation kann nicht vom lokalen Rendering profitieren, so dass langlebige Benutzererfahrungen nach dem ersten Laden der Seite nicht mehr so stark profitieren.

#### Server-Routing (MPA) vs. Client-Routing (SPA)

Wo befindet sich der Router deiner Website? Bei einer MPA wird bei jeder Anfrage an den Server entschieden, mit welchem HTML-Code geantwortet werden soll; die Routing-Logik befindet sich also auf dem Server. Bei einer SPA wird der Router lokal im Browser ausgeführt und übernimmt jede Navigation, um die neue Seite zu rendern, ohne dass der Server jemals kontaktiert wird.

Dies ist ein ähnlicher Kompromiss wie der oben beschriebene: MPAs bieten einen schnelleren ersten Ladevorgang, während SPAs möglicherweise einen schnelleren zweiten oder dritten Seitenladevorgang bieten, sobald die JavaScript-Anwendung vollständig im Browser geladen ist.

SPAs können auch leistungsfähigere Übergänge bei der Seitennavigation bieten, weil sie so viel über das Rendering der Seite steuern. Um dieser Unterstützung gerecht zu werden, nutzen MPAs Tools wie das von Hotwire [Turbo](https://turbo.hotwired.dev), die das Client-Routing nachahmen, indem sie auch die Navigation im Browser steuern. Das HTML wird immer noch auf dem Server gerendert, aber Turbo kann nun einen nahtlosen Übergang zwischen den Seiten anzeigen, ähnlich dem Client-Routing in einer SPA.

#### Server-Status-Verwaltung (MPA) vs. Client-Status-Verwaltung (SPA)

SPAs sind die überlegene Architektur für Websites, die mit komplexer, mehrseitiger Statusverwaltung zu tun haben (z. B. Gmail). Der Grund dafür ist, dass eine SPA die gesamte Website als eine einzige JavaScript-Anwendung ausführt, wodurch die Anwendung den Status und den Speicher über mehrere Seiten hinweg beibehalten kann. Interaktive, datengesteuerte Erlebnisse wie Posteingänge und Verwaltungs-Dashboards eignen sich gut für SPAs, da die Website selbst von Natur aus "app-ähnlich" ist.

## Sind MPAs besser als SPAs?

Beim Vergleich zwischen MPAs und SPAs gibt es keine "bessere" oder "schlechtere" Wahl. Es geht immer um Kompromisse.

**Astro bevorzugt die Leistung und Einfachheit von MPAs, da dies für unseren Anwendungsfall der inhaltsorientierten Websites am sinnvollsten ist.** Zustandsbezogenere, interaktionslastige Websites profitieren möglicherweise mehr von der App-ähnlichen Architektur, die SPAs auf Kosten der Leistung beim ersten Laden bieten.

:::note[Barrierefreiheit]
MPAs verwenden das Standardelement `<a>` für die Navigation. Dies bietet wichtige Funktionen für die Barrierefreiheit wie die Verwaltung von Fokuszuständen und die standardmäßige Ankündigung von Routenänderungen.
:::

## Fallstudien

Nachfolgend findest du alle öffentlichen Astro-Vergleiche, die uns bekannt sind:

- [Astro vs. SPA (Next.js)](https://twitter.com/t3dotgg/status/1437195415439360003) - 94% weniger JavaScript
- [Astro vs. SPA (Next.js)](https://twitter.com/jlengstorf/status/1442707241627385860?lang=en) - 34% schnelleres Laden
- [Astro vs. SPA (Remix, SvelteKit)](https://www.youtube.com/watch?v=2ZEMb_H-LYE&t=8163s) - "Das [Lighthouse-Ergebnis] ist unglaublich."
- [Astro vs. Qwik](https://www.youtube.com/watch?v=2ZEMb_H-LYE&t=8504s) - 43% schnellerer TTI

Wenn du eine öffentliche Migration oder einen Benchmark kennst, der hier nicht aufgeführt ist, erstelle bitte einen PR, um ihn hinzuzufügen.

## Weitere Ressourcen

Wenn du mehr erfahren möchtest, haben Surma (Google) und Jake Archibald (Google) eine großartige Diskussion [zu genau diesem Thema](https://www.youtube.com/watch?v=ivLhf3hq7eM) aufgezeichnet.
