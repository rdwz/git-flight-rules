# Flugregeln für Git

🌍
*[English](README.md) ∙ [Español](README_es.md) ∙ [Русский](README_ru.md) ∙ [繁體中文](README_zh-TW.md) ∙ [简体中文](README_zh-CN.md) ∙ [한국어](README_kr.md) ∙ [Tiếng Việt](README_vi.md) ∙ [Français](README_fr.md) ∙ [日本語](README_ja.md)*

#### Was sind "Flugregeln"?

Ein Leitfaden für Astronauten (jetzt Programmierer, die Git verwenden), was zu tun ist, wenn etwas schief läuft.

> Flugregeln sind das hart erarbeitete Wissen, das in Handbüchern festgehalten wird, die Schritt für Schritt auflisten, was zu tun ist, wenn X auftritt, und warum. Im Wesentlichen handelt es sich um extrem detaillierte, szenariospezifische Standardarbeitsanweisungen. [...]

> Die NASA hat unsere Fehltritte, Katastrophen und Lösungen seit den frühen 1960er Jahren festgehalten, als die Bodenteams der Mercury-Ära begannen, "Lessons Learned" in einem Kompendium zu sammeln, in dem heute Tausende von problematischen Situationen - von Triebwerksausfällen über kaputte Lukengriffe bis hin zu Computerpannen - und deren Lösungen aufgeführt sind.

Chris Hadfield, *An Astronaut's Guide to Life on Earth*.

#### Konventionen für dieses Dokument

Aus Gründen der Übersichtlichkeit wird in allen Beispielen in diesem Dokument ein angepasster Bash-Prompt verwendet, um den aktuellen Zweig anzuzeigen und zu verdeutlichen, ob es sich um abgestufte Änderungen handelt oder nicht. Die Verzweigung ist in Klammern eingeschlossen, und ein "*" neben dem Namen der Verzweigung weist auf abgestufte Änderungen hin.

Alle Befehle sollten mindestens mit der Git-Version 2.13.0 funktionieren. Siehe die [git-Website](https://www.git-scm.com/), um Ihre lokale git-Version zu aktualisieren.

[![Treten Sie dem Chat bei https://gitter.im/k88hudson/git-flight-rules](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/k88hudson/git-flight-rules?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- BEARBEITEN SIE DIESEN ABSCHNITT NICHT, sondern führen Sie doctoc ZUR AKTUALISIERUNG erneut aus -->
**Inhaltsverzeichnis** *generiert mit [DocToc](https://github.com/thlorenz/doctoc)*

- [Repositories](#repositories)
  - [Ich möchte ein lokales Repository starten](#i-want-to-start-a-local-repository)
  - [Ich möchte ein entferntes Repository klonen](#i-want-to-clone-a-remote-repository)
  - [Ich habe das falsche entfernte Repository eingestellt](#i-set-the-wrong-remote-repository)
  - [Ich möchte Code zum Repository von jemand anderem hinzufügen](#i-want-to-add-code-to-someone-elses-repository)
    - [Code über Pull-Requests vorschlagen](#suggesting-code-via-pull-requests)
    - [Code über Patches vorschlagen](#suggesting-code-via-patches)
    - [Ich muss meinen Fork mit den neuesten Updates aus dem Original-Repository aktualisieren](#i-need-to-update-my-fork-with-latest-updates-from-the-original-repository)
- [Commits bearbeiten](#editing-commits)
  - [Was habe ich gerade übertragen?](#what-did-i-just-commit)
  - [Ich habe das Falsche in eine Commit-Nachricht geschrieben](#i-wrote-the-wrong-thing-in-a-commit-message)
  - [Ich habe einen Commit mit dem falschen Namen und der falschen E-Mail Adresse gemacht](#i-committed-with-the-wrong-name-and-email-configured)
  - [Ich möchte eine Datei aus dem vorherigen Commit entfernen](#i-want-to-remove-a-file-from-the-previous-commit)
  - [Ich möchte eine Änderung von einem Commit zu einem anderen verschieben](#i-want-to-move-a-change-from-one-commit-to-another)
  - [Ich möchte meine letzte Übertragung löschen oder entfernen](#i-want-to-delete-or-remove-my-last-commit)
  - [Beliebigen Commit löschen/entfernen](#deleteremove-arbitrary-commit)
  - [Ich habe versucht, meinen geänderten Commit an einen entfernten Server zu übertragen, aber ich bekam eine Fehlermeldung](#i-tried-to-push-my-amended-commit-to-a-remote-but-i-got-an-error-message)
  - [Ich habe versehentlich einen Hard-Reset gemacht und möchte meine Änderungen zurück](#i-accidentally-did-a-hard-reset-and-i-want-my-changes-back)
  - [Ich habe versehentlich einen Commit gemacht und einen Merge veröffentlicht](#i-accidentally-committed-and-pushed-a-merge)
  - [Ich habe versehentlich Dateien mit sensiblen Daten übertragen und verschoben](#i-accidentally-committed-and-pushed-files-containing-sensitive-data)
  - [Ich möchte eine große Datei aus der Repo-Historie entfernen](#i-want-to-remove-a-large-file-from-ever-existing-in-repo-history)
    - [Empfohlene Technik: Verwenden Sie bfg von Drittanbietern](#recommended-technique-use-third-party-bfg)
    - [Eingebaute Technik: git-filter-branch verwenden](#built-in-technique-use-git-filter-branch)
    - [Letzter Schritt: Übertragen der geänderten Repository-Historie](#final-step-pushing-your-changed-repo-history)
  - [Ich muss den Inhalt eines Commits ändern, das nicht mein letztes ist](#i-need-to-change-the-content-of-a-commit-which-is-not-my-last)
- [Staging](#staging)
  - [Ich möchte alle verfolgten Dateien bereitstellen und nicht verfolgte Dateien zurücklassen](#i-want-to-stage-all-tracked-files-and-leave-untracked-files)
    - [Einen Teil der getrackten Dateien bereitstellen](#to-stage-part-of-tracked-files)
  - [Ich muss bereitgestellte Änderungen zum vorherigen Commit hinzufügen](#i-need-to-add-staged-changes-to-the-previous-commit)
  - [Ich möchte einen Teil einer neuen Datei bereitstellen, aber nicht die ganze Datei](#i-want-to-stage-part-of-a-new-file-but-not-the-whole-file)
  - [Ich möchte Änderungen in einer Datei zu zwei verschiedenen Commits hinzufügen](#i-want-to-add-changes-in-one-file-to-two-different-commits)
  - [Ich habe zu viele Bearbeitungen inszeniert und möchte sie in einen separaten Commit auslagern](#i-inszeniert-zu-viele-Bearbeitungen-und-ich-will-sie-in-einen-separaten-Commit-auslagern)
  - [Ich möchte meine unstaged Edits inszenieren, und meine staged Edits inszenieren](#i-want-to-stage-my-unstaged-edits-and-unstage-my-staged-edits)
- [Uninszenierte Bearbeitungen](#uninszenierte-bearbeitungen)
  - [Ich möchte meine unbearbeiteten Bearbeitungen in einen neuen Zweig verschieben](#i-want-to-move-my-unstaged-edits-to-a-new-branch)
  - [Ich möchte meine unbearbeiteten Bearbeitungen in einen anderen, bestehenden Zweig verschieben](#i-want-to-move-my-unstaged-edits-to-a-different-existing-branch)
  - [Ich möchte meine lokalen unbestätigten Änderungen (staged und unstaged) verwerfen](#i-want-to-discard-my-local-uncommitted-changes-staged-and-unstaged)
  - [Ich möchte bestimmte nicht übertragene Änderungen verwerfen](#i-want-to-discard-specific-unstaged-changes)
  - [Ich möchte bestimmte unveröffentlichte Dateien verwerfen](#i-want-to-discard-specific-unstaged-files)
  - [Ich möchte nur meine unbearbeiteten lokalen Änderungen verwerfen](#i-want-to-discard-only-my-unstaged-local-changes)
  - [Ich möchte alle meine nicht verfolgten Dateien verwerfen](#i-want-to-discard-all-of-my-untracked-files)
  - [Ich möchte eine bestimmte Stagedatei unstaggen](#i-want-to-unstage-a-specific-staged-file)
- [Verzweigungen](#branches)
  - [Ich möchte alle Zweige auflisten](#i-want-to-list-all-branches)
  - [Einen Zweig aus einem Commit erstellen](#create-a-branch-from-a-commit)
  - [Ich habe von/auf den falschen Zweig gezogen](#i-pulled-frominto-the-wrong-branch)
  - [Ich möchte lokale Commits verwerfen, damit mein Branch derselbe ist wie der auf dem Server](#i-want-to-discard-local-commits-so-my-branch-is-the-same-as-one-on-the-server)
  - [Ich habe in den Hauptzweig statt in einen neuen Zweig übertragen](#i-committed-to-main-instead-of-a-new-branch)
  - [Ich möchte die ganze Datei von einem anderen ref-ish behalten](#i-want-to-keep-the-whole-file-from-another-ref-ish)
  - [Ich habe mehrere Übertragungen auf einem einzigen Zweig gemacht, die auf verschiedenen Zweigen sein sollten](#i-machte-mehrere-übertragungen-auf-einem-einzigen-zweig-die-auf-verschiedenen-zweigen-sein-sollten)
  - [Ich möchte lokale Zweige löschen, die upstream gelöscht wurden](#i-want-to-delete-local-branches-that-were-deleted-upstream)
  - [Ich habe versehentlich meinen Zweig gelöscht](#i-accidentally-deleted-my-branch)
  - [Ich möchte einen Zweig löschen](#i-want-to-delete-a-branch)
  - [Ich möchte mehrere Zweige löschen](#i-want-to-delete-multiple-branches)
  - [Ich möchte einen Zweig umbenennen](#i-want-to-rename-a-branch)
  - [Ich möchte in einen entfernten Zweig auschecken, an dem jemand anderes arbeitet](#i-want-to-checkout-to-a-remote-branch-that-someone-else-is-working-on)
  - [Ich möchte einen neuen entfernten Zweig aus dem aktuellen lokalen Zweig erstellen](#i-want-to-create-a-new-remote-branch-from-current-local-one)
  - [Ich möchte einen entfernten Zweig als Upstream für einen lokalen Zweig setzen](#i-want-to-set-a-remote-branch-as-the-upstream-for-a-local-branch)
  - [Ich möchte meinen HEAD so einstellen, dass er den Standard-Fernzweig verfolgt](#i-want-to-set-my-head-to-track-the-default-remote-branch)
  - [Ich habe Änderungen am falschen Zweig vorgenommen](#i-machte-änderungen-am-falschen-zweig)
  - [Ich möchte einen Zweig in zwei Zweige aufteilen](#i-want-to-split-a-branch-into-two)
- [Umbasieren und Zusammenführen](#rebasing-and-merging)
  - [Ich möchte Rebase/Merge rückgängig machen](#i-want-to-undo-rebasemerge)
  - [Ich habe rebased, aber ich will keinen Push erzwingen](#i-rebased-but-i-dont-want-to-force-push)
  - [Ich muss Commits kombinieren](#i-need-to-combine-commits)
    - [Sichere Zusammenführungsstrategie](#safe-merging-strategy)
    - [Ich muss einen Zweig zu einem einzigen Commit zusammenführen](#i-need-to-merge-a-branch-into-a-single-commit)
    - [Ich möchte nur nicht gepushte Commits zusammenführen](#i-want-to-combine-only-unpushed-commits)
    - [Ich muss die Zusammenführung abbrechen](#i-need-to-abort-the-merge)
  - [Ich muss den übergeordneten Commit meines Zweigs aktualisieren](#i-need-to-update-the-parent-commit-of-my-branch)
  - [Prüfen, ob alle Commits eines Zweiges zusammengeführt sind](#check-if-all-commits-on-a-branch-are-merged)
  - [Mögliche Probleme mit interaktiven Rebases](#possible-issues-with-interactive-rebases)
    - [Der Rebase-Bearbeitungsbildschirm sagt 'noop'](#the-rebase-editing-screen-says-noop)
    - [Es gab Konflikte](#there-were-conflicts)
- [Stash](#stash)
  - [Alle Bearbeitungen auslagern](#stash-all-edits)
  - [Bestimmte Dateien auslagern](#stash-specific-files)
  - [Auslagern mit Nachricht](#stash-with-message)
  - [Einen bestimmten Stash aus einer Liste anwenden](#apply-a-specific-stash-from-list)
  - [Auslagern unter Beibehaltung nicht verteilter Bearbeitungen](#stash-while-keeping-unstaged-edits)
- [Suchen](#finding)
  - [Ich möchte eine Zeichenfolge in einem beliebigen Commit finden](#i-want-to-find-a-string-in-any-commit)
  - [Ich möchte nach Autor/Committer suchen](#i-want-to-find-by-author-committer)
  - [Ich möchte Commits auflisten, die bestimmte Dateien enthalten](#i-want-to-list-commits-containing-specific-files)
  - [Ich möchte die Commit-Historie für eine bestimmte Funktion einsehen](#i-want-to-view-the-commit-history-for-a-specific-function)
  - [Einen Tag finden, auf den ein Commit verwiesen wird](#find-a-tag-where-a-commit-is-referenced)
- [Untermodule](#submodules)
  - [Alle Submodule klonen](#clone-all-submodules)
  - [Ein Submodul entfernen](#remove-a-submodule)
- [Verschiedene Objekte](#miscellaneous-objects)
  - [Einen Ordner oder eine Datei von einem Zweig in einen anderen kopieren](#copy-a-folder-or-file-from-one-branch-to-another)
  - [Wiederherstellen einer gelöschten Datei](#restore-a-deleted-file)
  - [Tag löschen](#delete-tag)
  - [Gelöschten Tag wiederherstellen](#recover-a-deleted-tag)
  - [Gelöschter Patch](#deleted-patch)
  - [Ein Repository als Zip-Datei exportieren](#exporting-a-repository-as-a-zip-file)
  - [Einen Zweig und einen Tag mit demselben Namen pushen](#push-a-branch-and-a-tag-that-have-the-same-name)
- [Dateien verfolgen](#tracking-files)
  - [Ich möchte die Großschreibung eines Dateinamens ändern, ohne den Inhalt der Datei zu verändern](#i-want-to-change-a-file-names-capitalization-without-changing-the-contents-of-the-file)
  - [Ich möchte lokale Dateien überschreiben, wenn ich einen Git-Pull durchführe](#i-want-to-overwrite-local-files-when-doing-a-git-pull)
  - [Ich möchte eine Datei aus Git entfernen, aber die Datei behalten](#i-want-to-remove-a-file-from-git-but-keep-the-file)
  - [Ich möchte eine Datei auf eine bestimmte Revision zurücksetzen](#i-want-to-revert-a-file-to-a-specific-revision)
  - [Ich möchte Änderungen an einer bestimmten Datei zwischen Commits oder Branches auflisten](#i-want-to-list-changes-of-a-specific-file-between-commits-or-branches)
  - [Ich möchte, dass Git Änderungen an einer bestimmten Datei ignoriert](#i-want-git-to-ignore-changes-to-a-specific-file)
- [Fehlersuche mit Git](#debugging-with-git)
- [Konfiguration](#configuration)
  - [Ich möchte Aliase für einige Git-Befehle hinzufügen](#i-want-to-add-aliases-for-some-git-commands)
  - [Ich möchte ein leeres Verzeichnis zu meinem Repository hinzufügen](#i-want-to-add-an-empty-directory-to-my-repository)
  - [Ich möchte einen Benutzernamen und ein Passwort für ein Repository zwischenspeichern](#i-want-to-cache-a-username-and-password-for-a-repository)
  - [Ich möchte, dass Git Änderungen an Berechtigungen und Dateimodus ignoriert](#i-want-to-make-git-ignore-permissions-and-filemode-changes)
  - [Ich möchte einen globalen Benutzer festlegen](#i-want-to-set-a-global-user)
- [Ich habe keine Ahnung, was ich falsch gemacht habe](#ive-no-idea-what-i-did-wrong)
- [Git Shortcuts](#git-shortcuts)
  - [Git Bash](#git-bash)
  - [PowerShell unter Windows](#powershell-on-windows)
- [Andere Ressourcen](#other-resources)
  - [Bücher](#books)
  - [Tutorials](#tutorials)
  - [Scripts and Tools](#scripts-and-tools)
  - [GUI Clients](#gui-clients)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Repositories

### Ich möchte ein lokales Repository starten

So initialisieren Sie ein vorhandenes Verzeichnis als Git-Repository:

```sh
(mein-ordner) $ git init
```

### Ich möchte ein entferntes Repository klonen

Um ein entferntes Repository zu klonen (zu kopieren), kopieren Sie die URL des Repositorys und führen Sie aus:

```sh
git clone [url]
```

Dadurch wird es in einem Ordner gespeichert, der den gleichen Namen wie das entfernte Repository hat. Stellen Sie sicher, dass Sie eine Verbindung zu dem entfernten Server haben, von dem Sie klonen (für die meisten Zwecke bedeutet dies, dass Sie mit dem Internet verbunden sind).

Klonen in einen Ordner mit einem anderen Namen als dem Standardnamen des Repositorys:

```sh
git clone [url] name-des-neuen-ordners
```

### Ich habe das falsche entfernte Repository eingestellt

Hier gibt es einige mögliche Probleme:

Wenn Sie das falsche Repository geklont haben, löschen Sie einfach das Verzeichnis, das nach dem Ausführen von `git clone` erstellt wurde, und klonen Sie das richtige Repository.

Wenn Sie das falsche Repository als Ursprung eines bestehenden lokalen Repositorys festgelegt haben, ändern Sie die URL Ihres Ursprungs, indem Sie `git clone` ausführen:

```sh
git remote set-url origin [URL des aktuellen Projektarchivs]
```

Weitere Informationen finden Sie in [diesem StackOverflow-Thema] (<https://stackoverflow.com/questions/2432764/how-to-change-the-uri-url-for-a-remote-git-repository#2432799>).

### Ich möchte Code zum Repository eines anderen hinzufügen

Git erlaubt es Ihnen nicht, Code ohne Zugriffsrechte zum Repository eines anderen hinzuzufügen. Das gilt auch für GitHub, das nicht mit Git identisch ist, sondern ein gehosteter Dienst für Git-Repositorys ist. Sie können jedoch Code vorschlagen, indem Sie Patches oder, auf GitHub, Forks und Pull Requests verwenden.

Zunächst ein paar Worte zum Forken. Ein Fork ist eine Kopie eines Repositorys. Es handelt sich dabei nicht um eine Git-Operation, sondern um eine übliche Aktion auf GitHub, Bitbucket, GitLab - oder überall dort, wo Git-Repositorys gehostet werden. Sie können ein Repository über die gehostete Benutzeroberfläche forken.

#### Vorschlagen von Code über Pull Requests

Nachdem Sie ein Repository geforkt haben, müssen Sie das Repository normalerweise auf Ihren Rechner klonen. Sie können einige kleine Änderungen auf GitHub vornehmen, ohne zu klonen, aber dies ist keine Github-Flugregeln-Liste, also lassen Sie uns damit fortfahren, wie Sie dies lokal tun.

```sh
# wenn du ssh verwendest
$ git clone git@github.com:k88hudson/git-flight-rules.git

# wenn Sie https verwenden
$ git clone https://github.com/k88hudson/git-flight-rules.git
```

Wenn Sie `cd` in das resultierende Verzeichnis gehen und `git remote` eingeben, sehen Sie eine Liste der Remotes. Normalerweise wird es eine Fernbedienung geben - `origin` - die auf `k88hudson/git-flight-rules` zeigt. In diesem Fall wollen wir auch eine Fernbedienung, die auf Ihren Fork verweist.

Um einer Git-Konvention zu folgen, verwenden wir normalerweise den Remote-Namen `origin` für Ihr eigenes Repository und `upstream` für das, was Sie geforkt haben. Benennen Sie also das `origin`-Repository in `upstream` um

``sh
git remote rename origin upstream

```

Sie können dies auch mit `git remote set-url` machen, aber es dauert länger und umfasst mehr Schritte.

Richten Sie dann ein neues Remote ein, das auf Ihr Projekt verweist.

``sh
git remote add origin git@github.com:YourName/git-flight-rules.git
```

Beachten Sie, dass Sie nun zwei Fernzugänge haben.

- `origin` verweist auf Ihr eigenes Repository.
- Upstream" verweist auf das ursprüngliche Repository.

Vom Ursprung aus können Sie lesen und schreiben. Von upstream aus können Sie nur lesen.

Wenn Sie mit den Änderungen fertig sind, pushen Sie Ihre Änderungen (normalerweise in einem Zweig) auf die entfernte Seite namens `origin`. Wenn Sie sich auf einem Zweig befinden, können Sie `--set-upstream` verwenden, um zu vermeiden, dass der entfernte Tracking-Zweig bei jedem zukünftigen Push mit diesem Zweig angegeben wird. Zum Beispiel:

``sh
(feature/my-feature) git push --set-upstream origin feature/my-feature

```

Es gibt keine Möglichkeit, einen Pull Request über die CLI mit Git vorzuschlagen (obwohl es Tools wie [hub](http://github.com/github/hub) gibt, die dies für Sie erledigen). Wenn Sie also bereit sind, eine Pull-Anfrage zu stellen, gehen Sie zu Ihrem GitHub (oder einem anderen Git-Host) und erstellen Sie eine neue Pull-Anfrage. Beachten Sie, dass Ihr Host automatisch die ursprünglichen und die geforkten Repositories verlinkt.

Vergessen Sie danach nicht, auf das Feedback der Code-Reviews zu reagieren.

#### Code über Patches vorschlagen

Eine andere Möglichkeit, Codeänderungen vorzuschlagen, die nicht auf Websites von Drittanbietern wie Github angewiesen ist, ist die Verwendung von `git format-patch`.

format-patch" erstellt eine .patch-Datei für einen oder mehrere Commits. Diese Datei ist im Wesentlichen eine Liste von Änderungen, die ähnlich aussieht wie die Commit-Diffs, die Sie auf Github sehen können.

Ein Patch kann vom Empfänger eingesehen und sogar bearbeitet und mit `git am` angewendet werden.

Um zum Beispiel einen Patch zu erstellen, der auf dem vorherigen Commit basiert, würden Sie `git format-patch HEAD^` ausführen, was eine .patch-Datei mit dem Namen 0001-My-Commit-Message.patch erstellen würde.

Um diese Patch-Datei auf Ihr Repository anzuwenden, würden Sie `git am ./0001-My-Commit-Message.patch` ausführen.

Patches können auch mit dem Befehl `git send-email` per E-Mail verschickt werden. Für Informationen zur Verwendung und Konfiguration siehe: <https://git-send-email.io>.

#### Ich muss meinen Fork mit den neuesten Updates aus dem ursprünglichen Repository aktualisieren

Nach einer Weile kann es sein, dass das `upstream` Repository aktualisiert wurde und diese Aktualisierungen in Ihr `origin` Repository gezogen werden müssen. Denken Sie daran, dass auch andere Leute einen Beitrag leisten, genau wie Sie. Nehmen wir an, Sie befinden sich in Ihrem eigenen Funktionszweig und müssen diesen mit den Aktualisierungen aus dem ursprünglichen Repository aktualisieren.

Wahrscheinlich haben Sie einen Remote-Zweig eingerichtet, der auf das ursprüngliche Projekt verweist. Wenn nicht, tun Sie dies jetzt. Im Allgemeinen verwenden wir `upstream` als Remote-Namen:

```sh
$ (main) git remote add upstream <Link-zum-Original-Repository>
# $ (main) git remote add upstream git@github.com:k88hudson/git-flight-rules.git
```

Jetzt können Sie die neuesten Updates von Upstream abrufen.

```sh
$ (main) git fetch upstream
$ (main) git merge upstream/main

# oder mit einem einzigen Befehl
$ (main) git pull upstream main
```

## Bearbeiten von Commits

<a name="diff-last"></a>

### Was habe ich gerade übertragen?

Nehmen wir an, Sie haben gerade blind Änderungen mit `git commit -a` übertragen und sind sich nicht sicher, was der tatsächliche Inhalt der Übertragung war, die Sie gerade vorgenommen haben. Sie können den letzten Commit auf Ihrem aktuellen HEAD mit anzeigen:

```sh
(main)$ git show
```

Oder

```sh
git log -n1 -p
```

Wenn Sie eine Datei bei einem bestimmten Commit sehen wollen, können Sie auch dies tun (wobei `<commitid>` der Commit ist, an dem Sie interessiert sind):

```sh
git show <commitid>:filename
```

### Ich habe das Falsche in eine Commit-Nachricht geschrieben

Wenn Sie etwas Falsches geschrieben haben und der Commit noch nicht gepusht wurde, können Sie wie folgt vorgehen, um die Commit-Nachricht zu ändern, ohne die Änderungen im Commit zu verändern:

```sh
git commit --amend --only
```

Dadurch wird Ihr Standard-Texteditor geöffnet, in dem Sie die Nachricht bearbeiten können. Andererseits können Sie dies auch mit einem einzigen Befehl tun:

```sh
git commit --amend --only -m 'xxxxxxx'
```

Wenn Sie die Nachricht bereits gepusht haben, können Sie den Commit ändern und den Push erzwingen, aber das wird nicht empfohlen.

<a name="commit-falscher-autor"></a>

### Ich habe einen Commit mit dem falschen Namen und der falschen E-Mail Adresse durchgeführt

Wenn es sich um einen einzelnen Commit handelt, ändern Sie ihn

```sh
git commit --amend --no-edit --author "Neuer Authorname <authoremail@mydomain.com>"
```

Eine Alternative ist die korrekte Konfiguration der Autoreneinstellungen in `git config --global author.(name|email)` und dann die Verwendung von

``sh
git commit --amend --reset-author --no-edit

```

Wenn Sie die gesamte Historie ändern müssen, lesen Sie die Manpage für `git filter-branch`.

### Ich möchte eine Datei aus dem vorherigen Commit entfernen

Um Änderungen an einer Datei aus dem vorherigen Commit zu entfernen, gehen Sie wie folgt vor:

```sh
git checkout HEAD^ myfile
git add myfile
git commit --amend --no-edit
```

Falls die Datei neu zum Commit hinzugefügt wurde und Sie sie entfernen wollen (nur von Git aus), tun Sie dies:

```sh
git rm --cached myfile
git commit --amend --no-edit
```

Dies ist besonders nützlich, wenn Sie einen offenen Patch haben und eine unnötige Datei übertragen haben und einen Push erzwingen müssen, um den Patch auf einem entfernten Rechner zu aktualisieren. Die Option "--no-edit" wird verwendet, um die bestehende Commit-Nachricht beizubehalten.

<a name="move-change-to-new-commit"></a>

### Ich möchte eine Änderung von einem Commit zu einem anderen verschieben

Wenn Sie einen Commit gemacht haben, der Änderungen enthält, die besser in einen anderen Commit passen würden, können Sie die Änderungen mit einem interaktiven Rebase in den anderen Commit verschieben. Dies stammt von [stackoverflow](https://stackoverflow.com/a/54985304/2491502).

Ein Beispiel: Sie haben drei Commits (a, b, c). In b haben Sie Änderungen an file1 und file2 vorgenommen und möchten die Änderung an file1 von Commit b nach Commit a verschieben.

Führen Sie zunächst ein interaktives Rebase durch:

```sh
git rebase -i HEAD~3
```

Dadurch wird ein Editor mit folgendem Inhalt geöffnet:

```sh
pick a
pick b
c auswählen
```

Ändern Sie die Zeilen mit a und b zu bearbeiten:

```sh
a bearbeiten
b bearbeiten
c auswählen
```

Speichern Sie und schließen Sie den Editor. Dies bringt Sie zu commit b. Setzen Sie nun die Änderungen von file1 zurück:

```sh
git reset HEAD~1 file1
```

Damit werden die Änderungen in Datei1 zurückgesetzt. Verstecken Sie diese Änderungen und fahren Sie mit dem rebase fort:

```sh
git stash
git rebase --continue
```

Nun werden Sie Commit a bearbeiten. Entstashen Sie die Änderungen, fügen Sie sie dem aktuellen Commit hinzu und setzen Sie das Rebase fort:

```sh
git stash pop
git add file1
git commit --amend --no-edit
git rebase --continue
```

Wenn Sie die Änderungen von b nach c verschieben wollten, müssten Sie zwei Rebases durchführen, da c vor b kommt: einen, um die Änderungen aus b zu holen, dann einen weiteren, um c zu bearbeiten und die versteckten Änderungen hinzuzufügen.

<a name="delete-pushed-commit"></a>

### Ich möchte meinen letzten Commit löschen oder entfernen

Wenn Sie gepushte Commits löschen müssen, können Sie folgendes verwenden. Allerdings wird dies Ihre Historie unwiderruflich ändern und die Historie aller anderen, die bereits aus dem Repository gezogen haben, durcheinander bringen. Kurz gesagt, wenn Sie sich nicht sicher sind, sollten Sie dies niemals tun.

```sh
git reset HEAD^ --hard
git push --force-with-lease [remote] [branch]
```

Wenn Sie noch nicht gepusht haben, setzen Sie Git auf den Zustand zurück, in dem es sich vor Ihrem letzten Commit befand (und behalten dabei Ihre Staged Changes):

```
(mein-zweig)$ git reset --soft HEAD^
```

Dies funktioniert nur, wenn Sie noch nicht gepusht haben. Wenn Sie gepusht haben, ist das einzig wirklich sichere, was Sie tun können, `git revert SHAofBadCommit`. Das wird einen neuen Commit erzeugen, der alle Änderungen des vorherigen Commits rückgängig macht. Oder, wenn der Zweig, in den Sie gepusht haben, rebase-safe ist (d.h. andere Entwickler sollen nicht von ihm ziehen), können Sie einfach `git push --force-with-lease` benutzen. Weitere Informationen finden Sie in [dem obigen Abschnitt](#deleteremove-last-pushed-commit).

<a name="delete-any-commit"></a>

### Beliebigen Commit löschen/entfernen

Es gilt die gleiche Warnung wie oben. Tun Sie dies niemals, wenn möglich.

```sh
git rebase --onto SHA1_OF_BAD_COMMIT^ SHA1_OF_BAD_COMMIT
git push --force-with-lease [remote] [branch]
```

Oder führen Sie ein [interaktives rebase](#interactive-rebase) durch und entfernen Sie die Zeile(n), die dem/den Commit(s) entsprechen, den/die Sie entfernt sehen wollen.

<a name="#force-push"></a>

### Ich habe versucht, meinen geänderten Commit auf einen entfernten Server zu pushen, aber ich bekam eine Fehlermeldung

```sh
An https://github.com/yourusername/repo.git.
! [rejected] mybranch -> mybranch (non-fast-forward)
Fehler: Einige Refs konnten nicht nach 'https://github.com/tanay1337/webmaker.org.git' verschoben werden.
Hinweis: Aktualisierungen wurden abgelehnt, weil die Spitze des aktuellen Zweigs hinter
hint: seinem entfernten Gegenstück liegt. Integrieren Sie die entfernten Änderungen (z.B.
hint: 'git pull ...'), bevor Sie erneut pushen.
hint: Siehe die 'Note about fast-forwards' in 'git push --help' für Details.
```

Beachten Sie, dass, wie beim Rebasing (siehe unten), das Ändern **den alten Commit durch einen neuen ersetzt**, so dass Sie Ihre Änderungen erzwingen müssen (`--force-with-lease`), wenn Sie den zuvor geänderten Commit bereits auf Ihren Remote-Server übertragen haben. Seien Sie vorsichtig, wenn Sie dies tun &ndash; *immer* stellen Sie sicher, dass Sie einen Zweig angeben!

```sh
(mein-zweig)$ git push origin mein-zweig --force-with-lease
```

Generell sollten Sie **Force-Push** vermeiden. Es ist besser, einen neuen Commit zu erstellen und zu pushen, als den geänderten Commit zu erzwingen, da dies zu Konflikten in der Quellcode-Historie für alle anderen Entwickler führt, die mit dem betreffenden Zweig oder den untergeordneten Zweigen interagiert haben. `--force-with-lease` wird immer noch fehlschlagen, wenn jemand anderes auch an demselben Zweig wie Sie gearbeitet hat und Ihr Push diese Änderungen überschreiben würde.

Wenn Sie *absolut* sicher sind, dass niemand an demselben Zweig arbeitet oder Sie die Spitze des Zweiges *unbedingt* aktualisieren wollen, können Sie `--force` (`-f`) verwenden, aber dies sollte im Allgemeinen vermieden werden.

<a href="undo-git-reset-hard"></a>

### Ich habe versehentlich einen Hard Reset durchgeführt und möchte meine Änderungen wiederherstellen

Wenn Sie versehentlich `git reset --hard` gemacht haben, können Sie normalerweise immer noch Ihren Commit zurückbekommen, da Git ein paar Tage lang ein Protokoll von allem aufbewahrt.

Hinweis: Dies gilt nur, wenn Ihre Arbeit gesichert ist, d.h. entweder committed oder gebunkert. Die Option `git reset --hard` *entfernt* nicht übertragene Änderungen, daher ist sie mit Vorsicht zu verwenden. (Eine sicherere Option ist `git reset --keep`.)

```sh
(main)$ git reflog
```

Sie sehen eine Liste Ihrer früheren Commits und einen Commit für das Zurücksetzen. Wählen Sie die SHA der Übertragung, zu der Sie zurückkehren möchten, und setzen Sie sie erneut zurück:

```sh
(main)$ git reset --hard SHA1234
```

Und schon sollten Sie loslegen können.

<a href="undo-a-commit-merge"></a>

### Ich habe versehentlich einen Commit gemacht und einen Merge verschoben

Wenn Sie versehentlich einen Funktionszweig in den Hauptentwicklungszweig überführt haben, bevor er für die Zusammenführung bereit war, können Sie die Zusammenführung noch rückgängig machen. Aber es gibt einen Haken: Ein Merge Commit hat mehr als einen Parent (normalerweise zwei).

Der zu verwendende Befehl

```sh
(feature-branch)$ git revert -m 1 <commit>
```

wobei die Option -m 1 besagt, dass der übergeordnete Zweig Nummer 1 (der Zweig, in dem die Zusammenführung vorgenommen wurde) als übergeordneter Zweig für die Rückgängigmachung ausgewählt werden soll.

Hinweis: Die übergeordnete Nummer ist kein Commit-Bezeichner. Vielmehr hat eine Zusammenführungsübergabe die Zeile `Merge: 8e2ce2d 86ac2e7`. Die übergeordnete Nummer ist der 1-basierte Index der gewünschten übergeordneten Stelle in dieser Zeile, der erste Bezeichner ist die Nummer 1, der zweite die Nummer 2, usw.

<a href="undo-sensitive-commit-push"></a>

### Ich habe versehentlich Dateien mit sensiblen Daten übertragen und gepusht

Wenn Sie versehentlich Dateien mit sensiblen oder privaten Daten (Passwörter, Schlüssel usw.) übertragen haben, können Sie den vorherigen Commit ändern. Denken Sie daran, dass Sie nach dem Veröffentlichen eines Commits alle darin enthaltenen Daten als kompromittiert betrachten sollten. Diese Schritte können die sensiblen Daten aus Ihrem öffentlichen Projektarchiv oder Ihrer lokalen Kopie entfernen, aber Sie **können** die sensiblen Daten nicht aus den gezogenen Kopien anderer Leute entfernen. Wenn Sie ein Passwort übergeben haben, **ändern Sie es sofort**. Wenn Sie einen Schlüssel übertragen haben, **erzeugen Sie ihn sofort**. Es reicht nicht aus, den gepushten Commit zu ändern, da jeder in der Zwischenzeit den ursprünglichen Commit mit Ihren sensiblen Daten gezogen haben könnte.

Wenn Sie die Datei bearbeiten und die sensiblen Daten entfernen, dann führen Sie

```sh
(funktions-zweig)$ git add edited_file
(feature-branch)$ git commit --amend --no-edit
(feature-branch)$ git push --force-with-lease origin [branch]
```

Wenn Sie eine ganze Datei entfernen (aber lokal behalten) möchten, führen Sie Folgendes aus

```sh
(feature-branch)$ git rm --cached sensitive_file
echo sensitive_file >> .gitignore
(funktions-zweig)$ git add .gitignore
(feature-branch)$ git commit --amend --no-edit
(feature-branch)$ git push --force-with-lease origin [branch]
```

Alternativ können Sie Ihre sensiblen Daten auch in lokalen Umgebungsvariablen speichern.

Wenn Sie eine ganze Datei vollständig entfernen (und nicht lokal speichern) wollen, dann führen Sie

```sh
(funktions-zweig)$ git rm sensitive_file
(funktions-zweig)$ git commit --amend --no-edit
(feature-branch)$ git push --force-with-lease origin [branch]
```

Wenn Sie in der Zwischenzeit andere Commits gemacht haben (d.h. die sensiblen Daten befinden sich in einem Commit vor dem vorherigen Commit), müssen Sie ein rebase durchführen.

<a href="#i-want-to-remove-a-large-file-from-ever-existing-in-repo-history"></a>

### Ich möchte eine große Datei aus der Repo-Historie entfernen

Wenn die Datei, die Sie löschen wollen, geheim oder sensibel ist, lesen Sie stattdessen [wie man sensible Dateien entfernt](#i-accidentally-committed-and-pushed-files-containing-sensitive-data).

Selbst wenn Sie eine große oder unerwünschte Datei in einem aktuellen Commit löschen, existiert sie immer noch in der Git-Historie, im `.git`-Ordner Ihrer Projektgruppe, und wird `git clone` dazu bringen, nicht benötigte Dateien herunterzuladen.

Die Aktionen in diesem Teil des Leitfadens erfordern einen Force-Push und überschreiben große Teile des Projektarchivs. Wenn Sie also mit entfernten Mitarbeitern zusammenarbeiten, überprüfen Sie zuerst, ob deren lokale Arbeit gepusht wurde.

Es gibt zwei Optionen für das Umschreiben der Geschichte, den eingebauten `git-filter-branch` oder [`bfg-repo-cleaner`](https://rtyley.github.io/bfg-repo-cleaner/). `bfg` ist wesentlich sauberer und leistungsfähiger, aber es ist ein Drittanbieter und benötigt Java. Wir werden beide Alternativen beschreiben. Der letzte Schritt ist das Forcieren Ihrer Änderungen, was zusätzlich zu einem normalen Forcieren besondere Überlegungen erfordert, da ein großer Teil der Repo-Historie dauerhaft verändert wurde.

#### Empfohlene Technik: Drittanbieter bfg verwenden

Die Verwendung von bfg-repo-cleaner erfordert Java. Laden Sie das bfg jar von dem Link [hier](https://rtyley.github.io/bfg-repo-cleaner/) herunter. Unsere Beispiele verwenden `bfg.jar`, aber Ihr Download kann eine Versionsnummer haben, z.B. `bfg-1.13.0.jar`.

Um eine bestimmte Datei zu löschen.

```sh
(main)$ git rm path/to/filetoremove
(main)$ git commit -m "Commit Entfernen von filetoremove"
(main)$ java -jar ~/Downloads/bfg.jar --delete-files filetoremove
```

Beachten Sie, dass Sie in bfg den reinen Dateinamen verwenden müssen, auch wenn er in einem Unterverzeichnis liegt.

Sie können eine Datei auch nach einem Muster löschen, z.B.:

```sh
(main)$ git rm *.jpg
(main)$ git commit -m "Commit entfernt *.jpg"
(main)$ java -jar ~/Downloads/bfg.jar --delete-files *.jpg
```

Mit bfg werden die Dateien, die beim letzten Commit vorhanden sind, nicht beeinflusst. Wenn Sie zum Beispiel mehrere große .tga-Dateien in Ihrem Projektarchiv hatten und in einem früheren Commit eine Teilmenge davon gelöscht haben, berührt dieser Aufruf nicht die Dateien, die im letzten Commit vorhanden sind

Beachten Sie, wenn Sie eine Datei als Teil eines Commits umbenannt haben, z.B. wenn sie als `LargeFileFirstName.mp4` begann und durch einen Commit in `LargeFileSecondName.mp4` geändert wurde, wird der Befehl `java -jar ~/Downloads/bfg.jar --delete-files LargeFileSecondName.mp4` sie nicht aus dem Git-Verlauf entfernen. Führen Sie entweder den Befehl `--delete-files` mit beiden Dateinamen oder mit einem passenden Muster aus.

#### Eingebaute Technik: git-filter-branch verwenden

`git-filter-branch` ist umständlicher und hat weniger Funktionen, aber Sie können es verwenden, wenn Sie `bfg` nicht installieren oder ausführen können.

Im Folgenden kann `filepattern` ein bestimmter Name oder ein Muster sein, z.B. `*.jpg`. Dies wird Dateien, die dem Muster entsprechen, aus allen Historien und Zweigen entfernen.

```sh
(main)$ git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch filepattern' --prune-empty --tag-name-filter cat -- --all
```

Erklärung hinter den Kulissen:

`--tag-name-filter cat` ist ein umständlicher, aber einfachster Weg, die ursprünglichen Tags auf die neuen Commits anzuwenden, indem man den Befehl cat verwendet.

`--prune-empty` entfernt alle nun leeren Commits.

#### Letzter Schritt: Pushen der geänderten Repo-Historie

Sobald Sie die gewünschten Dateien entfernt haben, prüfen Sie sorgfältig, dass Sie nichts in Ihrem Projektarchiv kaputt gemacht haben - falls doch, ist es am einfachsten, Ihr Projektarchiv neu zu klonen und neu zu beginnen.
Verwenden Sie zum Abschluss optional die Git Garbage Collection, um die Größe Ihres lokalen Git-Ordners zu minimieren, und erzwingen Sie dann den Push.

```sh
(main)$ git reflog expire --expire=now --all && git gc --prune=now --aggressive
(main)$ git push origin --force --tags
```

Da Sie gerade die gesamte Git-Repository-Historie neu geschrieben haben, könnte der Vorgang "git push" zu groß sein und den Fehler "The remote end hung up unexpectedly" zurückgeben. Wenn das passiert, können Sie versuchen, den Git-Post-Puffer zu erhöhen:

```sh
(main)$ git config http.postBuffer 524288000
(main)$ git push --force
```

Wenn dies nicht funktioniert, müssen Sie die Repo-Historie manuell in Stücken von Übertragungen pushen. Versuchen Sie im folgenden Befehl, `<Anzahl>` zu erhöhen, bis der Push-Vorgang erfolgreich ist.

```sh
(main)$ git push -u origin HEAD~<Nummer>:refs/head/main --force
```

Sobald die Push-Operation beim ersten Mal erfolgreich war, verringern Sie `<Anzahl>` schrittweise, bis ein herkömmliches `git push` erfolgreich ist.

<a href="ich-muss-den-Inhalt-eines-Befehls-ändern-der-nicht-mein-letzter-ist"></a>

### Ich muss den Inhalt einer Übertragung ändern, die nicht meine letzte ist

Stellen Sie sich vor, Sie haben einige (z.B. drei) Commits erstellt und stellen später fest, dass Sie etwas verpasst haben, das kontextuell in den ersten dieser Commits gehört. Das stört Sie, denn wenn Sie einen neuen Commit mit diesen Änderungen erstellen würden, hätten Sie eine saubere Codebasis, aber Ihre Commits wären nicht atomar (d.h. Änderungen, die zueinander gehören, wären nicht im selben Commit). In einer solchen Situation möchten Sie vielleicht den Commit ändern, zu dem diese Änderungen gehören, sie einfügen und die folgenden Commits unverändert lassen. In einem solchen Fall kann `git rebase` Sie retten.

Betrachten Sie eine Situation, in der Sie den drittletzten Commit, den Sie gemacht haben, ändern wollen.

```sh
(dein-zweig)$ git rebase -i HEAD~4
```

bringt Sie in den interaktiven Rebase-Modus, der es Ihnen erlaubt, jeden Ihrer letzten drei Commits zu bearbeiten. Ein Texteditor öffnet sich und zeigt Ihnen etwas wie

```sh
pick 9e1d264 Der drittletzte Commit
pick 4b6e19a Der vorletzte Commit
pick f4037ec Die letzte Übertragung
```

den Sie ändern in

``sch
edit 9e1d264 Die drittletzte Übergabe
pick 4b6e19a Die vorletzte Übergabe
pick f4037ec Die letzte Übertragung

```

Damit teilen Sie rebase mit, dass Sie Ihren drittletzten Commit bearbeiten und die anderen beiden unverändert lassen wollen. Dann speichern (und schließen) Sie den Editor. Git beginnt dann mit rebase. Es hält bei dem Commit an, den Sie ändern wollen, und gibt Ihnen die Möglichkeit, diesen Commit zu bearbeiten. Jetzt können Sie die Änderungen übernehmen, die Sie beim ersten Commit nicht übernommen haben. Dazu bearbeiten Sie sie und stellen sie bereit. Danach führen Sie

```sh
(dein-zweig)$ git commit --amend
```

was Git anweist, den Commit neu zu erstellen, aber die Commit-Nachricht unbearbeitet zu lassen. Wenn Sie das getan haben, ist der schwierige Teil gelöst.

```sh
(dein-zweig)$ git rebase --continue
```

wird den Rest der Arbeit für Sie erledigen.

## Staging

<a href="#i-want-to-stage-all-tracked-files-and-leave-untracked-files"></a>

### Ich möchte alle verfolgten Dateien bereitstellen und nicht verfolgte Dateien zurücklassen

```sh
git add -u
```

#### Zur Bereitstellung eines Teils der verfolgten Dateien

```sh
# um Dateien mit der Endung .txt bereitzustellen
$ git add -u *.txt

# um alle Dateien im Verzeichnis src bereitzustellen
$ git add -u src/
```

<a href="#i-need-to-add-staged-changes-to-the-previous-commit"></a>

### Ich muss gestufte Änderungen zum vorherigen Commit hinzufügen

```sh
(mein-zweig*)$ git commit --amend
```

Wenn Sie bereits wissen, dass Sie die Commit-Nachricht nicht ändern wollen, können Sie git anweisen, die Commit-Nachricht wieder zu verwenden:

```sh
(mein-zweig*)$ git commit --amend -C HEAD
```

<a name="commit-partial-new-file"></a>

### Ich möchte einen Teil einer neuen Datei übertragen, aber nicht die ganze Datei

Normalerweise, wenn Sie einen Teil einer Datei bereitstellen wollen, führen Sie dies aus:

```sh
git add --patch dateiname.x
```

p" funktioniert als Abkürzung. Damit wird der interaktive Modus geöffnet. Sie könnten die Option `s` verwenden, um den Commit zu teilen - wenn die Datei jedoch neu ist, haben Sie diese Option nicht. Um eine neue Datei hinzuzufügen, gehen Sie wie folgt vor:

```sh
git add -N filename.x
```

Dann müssen Sie die Option `e` verwenden, um manuell auszuwählen, welche Zeilen hinzugefügt werden sollen. Wenn Sie `git diff --cached` oder
`git diff --staged` zeigt Ihnen, welche Zeilen Sie zwischengespeichert haben und welche noch lokal gespeichert sind.

<a href="stage-in-zwei-commits"></a>

### Ich möchte Änderungen in einer Datei zu zwei verschiedenen Commits hinzufügen

Mit `git add` wird die gesamte Datei zu einem Commit hinzugefügt. Mit `git add -p` können Sie interaktiv auswählen, welche Änderungen Sie hinzufügen wollen.

<a href="selective-unstage-edits"></a>

### Ich habe zu viele Änderungen vorgenommen und möchte sie in einen separaten Commit auslagern

Mit `git reset -p` wird ein Dialog zum Zurücksetzen des Patch-Modus geöffnet.  Dies ist ähnlich wie `git add -p`, mit dem Unterschied, dass die Auswahl von "yes" die Änderung aus der Übertragung herausnimmt und sie aus der kommenden Übertragung entfernt.

<a href="unstaging-edits-and-staging-the-unstaged"></a>

### Ich möchte meine unstaged Edits und meine staged Edits unstaged

In den meisten Fällen sollten Sie alle bereitgestellten Dateien freischalten und dann die gewünschte Datei auswählen und sie übertragen. Wenn Sie jedoch die bereitgestellten und die nicht bereitgestellten Bearbeitungen vertauschen möchten, können Sie eine temporäre Übergabe erstellen, um die bereitgestellten Dateien zu speichern, die nicht bereitgestellten Dateien bereitzustellen und sie dann zu verstecken. Setzen Sie dann die temporäre Übergabe zurück und löschen Sie Ihren Stash.

```sh
git commit -m "WIP"
git add . # Dies fügt auch nicht verfolgte Dateien hinzu.
git stash
git reset HEAD^
git stash pop --index 0
```

ANMERKUNG 1: Der Grund für die Verwendung von `pop` hier ist, dass Sie so viel wie möglich idempotent halten wollen.
ANMERKUNG 2: Ihre staged Dateien werden als unstaged markiert, wenn Sie nicht das `--index` Flag verwenden. ([Dieser Link](https://stackoverflow.com/questions/31595873/git-stash-with-staged-files-does-stash-convert-staged-files-to-unstaged?answertab=active#tab-top) erklärt, warum.)

## Unstaged Edits

<a href="move-unstaged-edits-to-new-branch"></a>

### Ich möchte meine unbearbeiteten Bearbeitungen in einen neuen Zweig verschieben

```sh
git checkout -b my-branch
```

<a href="move-unstaged-edits-to-old-branch"></a>

### Ich möchte meine unstaged Edits in einen anderen, bestehenden Branch verschieben

```sh
git stash
git checkout my-branch
git stash pop
```

<a href="ich-will-meine-lokalen-unübertragenen-Änderungen-verwerfen"></a>

### Ich möchte meine lokalen unbestätigten Änderungen verwerfen (staged und unstaged)

Wenn Sie alle Ihre lokalen Staged- und Unstaged-Änderungen verwerfen wollen, können Sie dies tun:

```sh
(mein-zweig)$ git reset --hard
# oder
(main)$ git checkout -f
```

Dies hebt alle Dateien auf, die Sie möglicherweise mit "git add" bereitgestellt haben:

```sh
git reset
```

Dies macht alle lokalen, nicht übertragenen Änderungen rückgängig (sollte im Stammverzeichnis des Projektarchivs ausgeführt werden):

```sh
git checkout .
```

Sie können auch nicht übertragene Änderungen an einer bestimmten Datei oder einem bestimmten Verzeichnis rückgängig machen:

```sh
git checkout [some_dir|file.txt]
```

Eine weitere Möglichkeit, alle nicht übertragenen Änderungen rückgängig zu machen (länger zu tippen, funktioniert aber von jedem Unterverzeichnis aus):

```sh
git reset --hard HEAD
```

Dadurch werden alle lokalen, nicht verfolgten Dateien entfernt, so dass nur die von Git verfolgten Dateien übrig bleiben:

```sh
git clean -fd
```

-x" wird auch alle ignorierten Dateien entfernen.

### Ich möchte bestimmte unstaged Änderungen verwerfen

Wenn Sie einige, aber nicht alle Änderungen in Ihrer Arbeitskopie loswerden wollen.

Unerwünschte Änderungen auschecken, gute Änderungen behalten.

```sh
$ git checkout -p
# Beantworten Sie alle Snippets, die Sie löschen wollen, mit "y".
```

Eine andere Strategie ist die Verwendung von `stash`. Verstecken Sie alle guten Änderungen, setzen Sie die Arbeitskopie zurück und wenden Sie die guten Änderungen erneut an.

```sh
$ git stash -p
# Wählen Sie alle Schnipsel aus, die Sie speichern wollen.
$ git reset --hard
$ git stash pop
```

Alternativ können Sie die unerwünschten Änderungen zwischenlagern und dann stash löschen.

```sh
$ git stash -p
# Markiere alle Snippets, die du nicht speichern willst
$ git stash drop
```

### Ich möchte bestimmte nicht gespeicherte Dateien verwerfen

Wenn Sie eine bestimmte Datei in Ihrer Arbeitskopie loswerden wollen.

```sh
git checkout myFile
```

Um mehrere Dateien in Ihrer Arbeitskopie zu verwerfen, können Sie sie auch alle auflisten.

```sh
git checkout myFirstFile mySecondFile
```

### Ich möchte nur meine lokalen Änderungen verwerfen, die noch nicht veröffentlicht wurden

Wenn Sie alle Ihre lokalen, noch nicht übertragenen Änderungen loswerden wollen

```sh
git checkout .
```

<a href="ich-will-alle-meine-unverfolgten-dateien-zuruecklegen"></a>

### Ich möchte alle meine nicht getrackten Dateien verwerfen

Wenn Sie alle Ihre nicht verfolgten Dateien loswerden wollen

``sh
git clean -f

```

<a href="Ich-will-eine-stufenspezifische-staged-Datei-entfernen"></a>

### Ich möchte eine bestimmte Stagedatei entstagen

Manchmal gibt es eine oder mehrere Dateien, die versehentlich in das Staged-Verzeichnis aufgenommen wurden, und diese Dateien wurden noch nicht übertragen. Um sie freizugeben:

```sh
git reset -- <Dateiname>
```

Dies führt dazu, dass die Datei unstaged wird und es so aussieht, als ob sie untracked ist.

## Verzweigungen

### Ich möchte alle Zweige auflisten

Lokale Zweigstellen auflisten

```sh
Git-Zweig
```

Entfernte Zweige auflisten

```sh
git branch -r
```

Alle Zweige auflisten (sowohl lokale als auch entfernte)

```sh
git branch -a
```

<a name="create-branch-from-commit"></a>

### Einen Zweig aus einem Commit erstellen

```sh
git checkout -b <branch> <SHA1_OF_COMMIT>
```

<a name="pull-wrong-branch"></a>

### Ich habe von/auf den falschen Zweig gezogen

Dies ist eine weitere Möglichkeit, `git reflog` zu benutzen, um zu sehen, wohin Ihr HEAD vor dem falschen Pull zeigte.

``sh
(main)$ git reflog
ab7555f HEAD@{0}: pull origin wrong-branch: Schnellvorlauf
c5bc55a HEAD@{1}: checkout: checkout Nachricht geht hier hin

```

Setzen Sie Ihren Zweig einfach wieder auf den gewünschten Commit zurück:

```sh
git reset --hard c5bc55a
```

Erledigt.

<a href="discard-local-commits"></a>

### Ich möchte lokale Übertragungen verwerfen, damit mein Zweig derselbe ist wie der auf dem Server

Bestätigen Sie, dass Sie Ihre Änderungen nicht auf den Server übertragen haben.

`git status` sollte anzeigen, wie viele Commits Sie dem Ursprung voraus sind:

```sh
(mein-zweig)$ git status
# On branch my-branch
# Ihr Zweig ist dem 'origin/my-branch' um 2 Commits voraus.
# (benutze "git push" um deine lokalen Commits zu veröffentlichen)
#
```

Eine Möglichkeit, den Zweig `my-branch` auf `origin/my-branch` zurückzusetzen (um das Gleiche zu haben, wie auf der Remote-Seite), ist dies zu tun:

```sh
(mein-zweig)$ git reset --hard origin/mein-zweig
```

<a name="commit-falscher-zweig"></a>

### Ich habe in den Hauptzweig statt in einen neuen Zweig übertragen

Erzeugen Sie den neuen Zweig, während Sie auf main bleiben:

```sh
(main)$ git branch my-branch
```

Setzt den Zweig main auf den vorherigen Commit zurück:

```sh
(main)$ git reset --hard HEAD^
```

`HEAD^` ist die Abkürzung für `HEAD^1`. Dies steht für den ersten Elternteil von `HEAD`, ebenso steht `HEAD^2` für den zweiten Elternteil des Commits (Merges können 2 Elternteile haben).

Beachten Sie, dass `HEAD^2` **nicht** dasselbe ist wie `HEAD~2` (siehe [dieser Link](http://www.paulboxley.com/blog/2011/06/git-caret-and-tilde) für weitere Informationen).

Alternativ, wenn Sie `HEAD^` nicht verwenden wollen, finden Sie den Commit-Hash heraus, auf den Sie Ihren Hauptzweig setzen wollen (`git log` sollte den Trick machen). Setzen Sie dann auf diesen Hash zurück. Mit `git push` stellen Sie sicher, dass diese Änderung auch auf Ihrem Remote-Zweig sichtbar wird.

Wenn der Hash des Commits, bei dem Ihr Hauptzweig sein soll, zum Beispiel `a13b85e` ist:

```sh
(main)$ git reset --hard a13b85e
HEAD ist jetzt bei a13b85e
```

Checken Sie den neuen Zweig aus, um weiterzuarbeiten:

```sh
(main)$ git checkout my-branch
```

<a name="keep-whole-file"></a>

### Ich möchte die gesamte Datei von einem anderen ref-ish behalten

Angenommen, Sie haben einen funktionierenden Spike (siehe Hinweis) mit Hunderten von Änderungen. Alles funktioniert. Jetzt übertragen Sie in einen anderen Zweig, um die Arbeit zu sichern:

```sh
(Lösung)$ git add -A && git commit -m "Alle Änderungen aus diesem Spike werden in einem großen Commit zusammengefasst."
```

Wenn du sie in einen Zweig (vielleicht Feature, vielleicht `develop`) einfügen willst, bist du daran interessiert, ganze Dateien zu behalten. Sie wollen Ihren großen Commit in kleinere aufteilen.

Sagen wir, Sie haben:

- branch `solution`, mit der Lösung für deinen Spike. Einer vor `develop`.
- Zweig `Entwicklung`, wo Sie Ihre Änderungen hinzufügen wollen.

Du kannst es lösen, indem du den Inhalt in deinen Zweig bringst:

``sh
(develop)$ git checkout solution -- file1.txt

```

Dies wird den Inhalt der Datei im Zweig `solution` in den Zweig `develop` übertragen:

```sh
# Im Zweig develop
# Ihr Zweig ist auf dem neuesten Stand mit 'origin/develop'.
# Änderungen, die übertragen werden sollen:
# (benutze "git reset HEAD <Datei>..." um unstage zu machen)
#
# geändert: file1.txt
```

Übertragen Sie dann wie gewohnt.

Hinweis: Spike-Lösungen werden erstellt, um das Problem zu analysieren oder zu lösen. Diese Lösungen werden zur Abschätzung verwendet und verworfen, sobald jeder eine klare Vorstellung von dem Problem hat. ~ [Wikipedia](https://en.wikipedia.org/wiki/Extreme_programming_practices).

<a name="cherry-pick"></a>

### Ich habe mehrere Commits auf einem einzigen Zweig gemacht, die auf verschiedenen Zweigen sein sollten

Angenommen, Sie befinden sich auf Ihrem Hauptzweig. Wenn Sie `git log` aufrufen, sehen Sie, dass Sie zwei Commits gemacht haben:

```sh
(main)$ git log

commit e3851e817c451cc36f2e6f3049db528415e3c114
Author: Alex Lee <alexlee@example.com>
Date:   Tue Jul 22 15:39:27 2014 -0400

    Bug #21 - CSRF-Schutz hinzugefügt

commit 5ea51731d150f7ddc4a365437931cd8be3bf3131
Author: Alex Lee <alexlee@example.com>
Date:   Tue Jul 22 15:39:12 2014 -0400

    Fehler #14 - Abstand im Titel korrigiert

commit a13b85e984171c6e2a1729bb061994525f626d14
Author: Aki Rose <akirose@example.com>
Date:   Tue Jul 21 01:12:48 2014 -0400

    Erste Übergabe
```

Notieren wir uns unsere Commit-Hashes für jeden Bug (`e3851e8` für #21, `5ea5173` für #14).

Zuerst setzen wir unseren Hauptzweig auf den richtigen Commit zurück (`a13b85e`):

```sh
(main)$ git reset --hard a13b85e
HEAD ist jetzt bei a13b85e
```

Jetzt können wir einen neuen Zweig für unseren Fehler #21 erstellen:

```sh
(main)$ git checkout -b 21
(21)$
```

Nun *wählen* wir den Commit für den Fehler #21 auf unseren Zweig. Das bedeutet, dass wir diesen Commit, und nur diesen Commit, direkt auf unseren Kopf anwenden werden.

```sh
(21)$ git cherry-pick e3851e8
```

Zu diesem Zeitpunkt besteht die Möglichkeit, dass es Konflikte gibt. Siehe den Abschnitt [**Es gab Konflikte**](#merge-conflict) im Abschnitt [interaktives rebasing oben](#interactive-rebase), um zu erfahren, wie man Konflikte auflöst.

Lassen Sie uns nun einen neuen Zweig für Fehler #14 erstellen, der ebenfalls auf main basiert

```sh
(21)$ git checkout main
(main)$ git checkout -b 14
(14)$
```

Und schließlich wählen wir den Commit für Fehler #14 aus:

```sh
(14)$ git cherry-pick 5ea5173
```

<a name="delete-stale-local-branches"></a>

### Ich möchte lokale Zweige löschen, die upstream gelöscht wurden

Sobald Sie einen Pull Request auf GitHub zusammenführen, haben Sie die Möglichkeit, den zusammengeführten Zweig in Ihrem Fork zu löschen. Wenn Sie nicht vorhaben, weiter an der Verzweigung zu arbeiten, ist es sauberer, die lokalen Kopien der Verzweigung zu löschen, damit Sie Ihr Arbeits-Checkout nicht mit einer Menge veralteter Verzweigungen verstopfen.

```sh
git fetch -p upstream
```

wobei `upstream` die entfernte Stelle ist, von der Sie etwas holen wollen.

<a name='restore-a-deleted-branch'></a>

### Ich habe versehentlich meinen Zweig gelöscht

Wenn Sie regelmäßig remote pushen, sollten Sie die meiste Zeit sicher sein. Trotzdem kann es manchmal vorkommen, dass Sie Ihre Zweige löschen. Nehmen wir an, wir erstellen einen Zweig und erstellen eine neue Datei:

```sh
(main)$ git checkout -b my-branch
(mein-zweig)$ git branch
(mein-zweig)$ touch foo.txt
(mein-zweig)$ ls
README.md foo.txt
```

Fügen wir sie hinzu und übertragen sie.

```sh
(mein-zweig)$ git add .
(mein-zweig)$ git commit -m 'foo.txt hinzugefügt'
(mein-zweig)$ foo.txt hinzugefügt
 1 Dateien geändert, 1 Einfügungen(+)
 Modus erstellen 100644 foo.txt
(mein-zweig)$ git log

commit 4e3cd85a670ced7cc17a2b5d8d3d809ac88d5012
Autor: siemiatj <siemiatj@example.com>
Date:   Wed Jul 30 00:34:10 2014 +0200

    foo.txt hinzugefügt

commit 69204cdf0acbab201619d95ad8295928e7f411d5
Author: Kate Hudson <katehudson@example.com>
Date:   Tue Jul 29 13:14:46 2014 -0400

    Fixes #6: Pushing nach Änderung von Commits erzwingen
```

Jetzt wechseln wir zurück zu main und entfernen "versehentlich" unseren Branch.

```sh
(mein-zweig)$ git checkout main
Zum Zweig 'main' gewechselt
Ihr Zweig ist mit 'origin/main' auf dem neuesten Stand.
(main)$ git branch -D my-branch
Der Zweig my-branch wurde gelöscht (war 4e3cd85).
(main)$ echo oh nein, mein Zweig wurde gelöscht!
Oh nein, mein Zweig wurde gelöscht!
```

An dieser Stelle sollten Sie sich mit 'reflog', einem erweiterten Logger, vertraut machen. Er speichert den Verlauf aller Aktionen im Repo.

```
(main)$ git reflog
69204cd HEAD@{0}: checkout: Umzug von my-branch nach main
4e3cd85 HEAD@{1}: commit: foo.txt hinzugefügt
69204cd HEAD@{2}: checkout: Umzug von main nach my-branch
```

Wie Sie sehen können, haben wir einen Commit-Hash von unserem gelöschten Zweig. Lassen Sie uns sehen, ob wir unseren gelöschten Zweig wiederherstellen können.

```sh
(main)$ git checkout -b my-branch-help
Zu einem neuen Zweig 'my-branch-help' gewechselt
(mein-zweig-hilfe)$ git reset --hard 4e3cd85
HEAD ist jetzt bei 4e3cd85 foo.txt hinzugefügt
(mein-zweig-hilfe)$ ls
README.md foo.txt
```

Voila! Wir haben unsere entfernte Datei zurück. `git reflog` ist auch nützlich, wenn das Rebasing furchtbar schief geht.

### Ich möchte einen Zweig löschen

Um einen entfernten Zweig zu löschen:

```sh
(main)$ git push origin --delete my-branch
```

Sie können das auch tun:

```sh
(main)$ git push origin :my-branch
```

Um einen lokalen Zweig zu löschen:

```sh
(main)$ git branch -d my-branch
```

Um einen lokalen Zweig zu löschen, der *nicht* mit dem aktuellen Zweig oder einem Upstream zusammengeführt wurde:

```sh
(main)$ git branch -D my-branch
```

### Ich möchte mehrere Zweige löschen

Angenommen, Sie möchten alle Zweige löschen, die mit "fix/" beginnen:

```sh
(main)$ git branch | grep 'fix/' | xargs git branch -d
```

### Ich möchte einen Zweig umbenennen

Um den aktuellen (lokalen) Zweig umzubenennen:

```sh
(main)$ git branch -m new-name
```

Um einen anderen (lokalen) Zweig umzubenennen:

```sh
(main)$ git branch -m alter-name neuer-name
```

Um den entfernten Zweig `alter-name` zu löschen und den lokalen Zweig `neuer-name` zu pushen:

```sh
(main)$ git push origin :alter_name neuer_name
```

<a name="ich-will-einen-entfernten-zweig-auschecken-an-dem-jemand-anderes-arbeitet"></a>

### Ich möchte in einen entfernten Zweig auschecken, an dem jemand anderes arbeitet

Holen Sie zunächst alle Zweige aus der Ferne:

```sh
(main)$ git fetch --all
```

Angenommen, Sie wollen `daves` aus der Ferne auschecken.

```sh
(main)$ git checkout --track origin/daves
Der Zweig daves wurde so eingerichtet, dass er den entfernten Zweig daves vom Ursprung aus verfolgt.
Zu einem neuen Zweig 'daves' gewechselt
```

(`--track` ist eine Abkürzung für `git checkout -b [branch] [remotename]/[branch]`)

Dadurch erhalten Sie eine lokale Kopie der Verzweigung `daves`, und alle Aktualisierungen, die gepusht wurden, werden auch in der Ferne angezeigt.

### Ich möchte einen neuen entfernten Zweig vom aktuellen lokalen Zweig erstellen

``sh
git push <remote> HEAD

```

Wenn Sie diesen entfernten Zweig auch als Upstream für den aktuellen Zweig festlegen möchten, verwenden Sie stattdessen Folgendes:

```sh
git push -u <remote> HEAD
```

Mit dem `upstream` Modus und dem `simple` (Standard in Git 2.0) Modus der `push.default` Konfiguration, wird der folgende Befehl den aktuellen Zweig in Bezug auf den entfernten Zweig pushen, der zuvor mit `-u` registriert wurde:

``sh
git push

```

Das Verhalten der anderen Modi von `git push` ist in der [doc von `push.default`](https://git-scm.com/docs/git-config#git-config-pushdefault) beschrieben.

### Ich möchte einen entfernten Zweig als Upstream für einen lokalen Zweig festlegen

Sie können einen entfernten Zweig als Upstream für den aktuellen lokalen Zweig festlegen:

```sh
$ git branch --set-upstream-to [remotename]/[branch]
# oder, unter Verwendung der Abkürzung
$ git branch -u [remotename]/[branch]
```

Um den entfernten Upstream-Zweig für einen anderen lokalen Zweig zu setzen:

```sh
git branch -u [remotename]/[branch] [local-branch]
```

<a name="i-want-to-set-my-HEAD-to-track-the-default-remote-branch"></a>

### Ich möchte meinen HEAD so einstellen, dass er den Standard-Remote-Branch verfolgt

Wenn Sie Ihre entfernten Zweige überprüfen, können Sie sehen, welchen entfernten Zweig Ihr HEAD verfolgt. In manchen Fällen ist dies nicht der gewünschte Zweig.

```sh
$ git branch -r
  origin/HEAD -> origin/gh-pages
  ursprung/haupt
```

Um `origin/HEAD` auf `origin/main` umzustellen, können Sie diesen Befehl ausführen:

```sh
$ git remote set-head origin --auto
origin/HEAD auf main setzen
```

### Ich habe Änderungen am falschen Zweig vorgenommen

Sie haben unbestätigte Änderungen vorgenommen und stellen fest, dass Sie sich auf dem falschen Zweig befinden. Verstecken Sie die Änderungen und wenden Sie sie auf den gewünschten Zweig an:

```sh
(falscher_Zweig)$ git stash
(falsche_Verzweigung)$ git checkout <richtige_Verzweigung>
(richtiger_Zweig)$ git stash apply
```

<a name="ich-will-einen-zweig-auf-zwei-teilen"></a>

### Ich möchte einen Zweig in zwei teilen

Sie haben viele Übertragungen an einem Zweig vorgenommen und möchten ihn nun in zwei Zweige aufteilen, so dass ein Zweig bis zu einer früheren Übertragung und ein anderer mit allen Änderungen entsteht.

Verwenden Sie `git log`, um den Commit zu finden, den Sie aufteilen wollen. Gehen Sie dann wie folgt vor:

```sh
(ursprünglicher_Zweig)$ git checkout -b neuer_Zweig
(new_branch)$ git checkout original_branch
(original_branch)$ git reset --hard <sha1 split here>
```

Wenn Sie den `original_branch` zuvor auf remote gepusht hatten, müssen Sie einen force push durchführen. Weitere Informationen finden Sie unter [Stack Overflow](https://stackoverflow.com/questions/28983458/how-to-split-a-branch-in-two-with-git/28983843#28983843)

## Rebasing und Merging

<a name="undo-rebase"></a>

### Ich möchte das Zurücksetzen/Zusammenführen rückgängig machen

Vielleicht haben Sie Ihren aktuellen Zweig mit einem falschen Zweig zusammengeführt, oder Sie können es nicht herausfinden oder den rebase/merge-Prozess beenden. Git speichert den ursprünglichen HEAD-Zeiger in einer Variablen namens ORIG_HEAD, bevor es gefährliche Operationen durchführt, so dass es einfach ist, Ihren Zweig auf den Stand vor dem rebase/merge zurückzubringen.

```sh
(mein-zweig)$ git reset --hard ORIG_HEAD
```

<a name="force-push-rebase"></a>

### Ich habe rebased, aber ich möchte keinen Force-Push durchführen

Leider müssen Sie Push erzwingen, wenn Sie wollen, dass die Änderungen im entfernten Zweig übernommen werden. Der Grund dafür ist, dass Sie die Historie geändert haben. Der entfernte Zweig wird die Änderungen nicht annehmen, wenn Sie keinen Push erzwingen. Dies ist einer der Hauptgründe, warum viele Leute einen Merge-Workflow statt eines Rebasing-Workflows verwenden - große Teams können in Schwierigkeiten geraten, wenn Entwickler das Pushen erzwingen. Verwenden Sie dies mit Vorsicht. Eine sicherere Art Rebase zu benutzen ist, Ihre Änderungen überhaupt nicht in den entfernten Zweig zu übernehmen, und stattdessen folgendes zu tun:

```sh
(main)$ git checkout my-branch
(mein-zweig)$ git rebase -i main
(mein-zweig)$ git checkout haupt
(main)$ git merge --ff-only mein-zweig
```

Weitere Informationen finden Sie in [diesem SO-Thread] (<https://stackoverflow.com/questions/11058312/how-can-i-use-git-rebase-without-requiring-a-forced-push>).

<a name="interactive-rebase"></a>

### I need to combine commits

Nehmen wir an, Sie arbeiten an einem Zweig, der ein Pull-Request gegen `main` ist/werden wird. Im einfachsten Fall, wenn Sie nur *alle* Commits zu einem einzigen zusammenfassen wollen und Sie sich nicht um die Zeitstempel der Commits kümmern, können Sie zurücksetzen und rekommitieren. Stellen Sie sicher, dass der Hauptzweig auf dem neuesten Stand ist und alle Ihre Änderungen übertragen wurden:

```sh
(mein-zweig)$ git reset --soft main
(mein-zweig)$ git commit -am "Neue fantastische Funktion"
```

Wenn Sie mehr Kontrolle haben wollen und auch die Zeitstempel beibehalten wollen, müssen Sie eine so genannte interaktive Umbasierung durchführen:

```sh
(mein-zweig)$ git rebase -i main
```

Wenn du nicht gegen einen anderen Zweig arbeitest, musst du relativ zu deinem `HEAD` rebase machen. Wenn du zum Beispiel die letzten 2 Commits löschen willst, musst du gegen `HEAD~2` rebasen. Für die letzten 3, `HEAD~3`, usw.

```sh
(main)$ git rebase -i HEAD~2
```

Nachdem Sie den interaktiven rebase-Befehl ausgeführt haben, sehen Sie in Ihrem Texteditor etwas wie dieses:

```vim
pick a9c8a1d Einige Überarbeitungen
pick 01b2fd8 Neue großartige Funktion
pick b729ad5 Überarbeitung
pick e3851e8 weitere Korrektur

# Rebase 8074d12..b729ad5 auf 8074d12
#
# Befehle:
# p, pick = commit verwenden
# r, reword = Commit verwenden, aber die Commit-Nachricht bearbeiten
# e, edit = commit verwenden, aber zum Ändern anhalten
# s, squash = Commit verwenden, aber mit vorherigem Commit verschmelzen
# f, fixup = wie "squash", aber die Logmeldung dieses Commits verwerfen
# x, exec = Kommando (den Rest der Zeile) in der Shell ausführen
#
# Diese Zeilen können neu sortiert werden; sie werden von oben nach unten ausgeführt.
#
# Wenn Sie hier eine Zeile entfernen, geht DIESER COMMIT VERLOREN.
#
# Wenn Sie jedoch alles entfernen, wird der rebase abgebrochen.
#
# Beachten Sie, dass leere Commits auskommentiert werden
```

Alle Zeilen, die mit einem `#` beginnen, sind Kommentare, sie haben keinen Einfluss auf Ihr Rebase.

Dann ersetzen Sie "pick"-Befehle durch beliebige aus der obigen Liste, und Sie können auch Commits entfernen, indem Sie die entsprechenden Zeilen entfernen.

Wenn Sie zum Beispiel **den ältesten (ersten) Commit alleine lassen und alle folgenden Commits mit dem zweitältesten kombinieren** wollen, sollten Sie den Buchstaben neben jedem Commit außer dem ersten und zweiten so ändern, dass er `f` sagt:

```vim
pick a9c8a1d Einige Überarbeitungen
pick 01b2fd8 Neue großartige Funktion
f b729ad5 Überarbeitung
f e3851e8 weitere Korrektur
```

Wenn Sie diese Commits kombinieren **und den Commit umbenennen** wollen, sollten Sie zusätzlich ein `r` neben dem zweiten Commit hinzufügen oder einfach `s` anstelle von `f` verwenden:

``vim
pick a9c8a1d Einige Überarbeitungen
pick 01b2fd8 Neue großartige Funktion
s b729ad5 Überarbeitung
s e3851e8 weitere Korrektur

```

In der nächsten Texteingabeaufforderung können Sie den Commit dann umbenennen.

```vim
Neuere, tollere Funktionen

# Bitte geben Sie die Commit-Nachricht für Ihre Änderungen ein. Zeilen, die
# mit '#' beginnen, werden ignoriert, und eine leere Nachricht bricht die Übergabe ab.
# rebase in progress; onto 8074d12
# Sie bearbeiten gerade einen Commit, während Sie den Zweig 'main' auf '8074d12' umbasen.
#
# Änderungen, die übertragen werden sollen:
# geändert:   README.md
#

```

Wenn alles erfolgreich war, sollten Sie etwas wie dieses sehen:

```sh
(main)$ Erfolgreich rebased und refs/heads/main aktualisiert.
```

#### Sichere Zusammenführungsstrategie

`--no-commit` führt die Zusammenführung durch, tut aber so, als ob die Zusammenführung fehlgeschlagen wäre und führt keine automatische Übergabe durch, so dass der Benutzer die Möglichkeit hat, das Ergebnis der Zusammenführung vor der Übergabe zu überprüfen und weiter zu verbessern. `no-ff` bewahrt den Beweis, dass ein Funktionszweig einmal existierte, und hält die Projektgeschichte konsistent.

```sh
(main)$ git merge --no-ff --no-commit my-branch
```

#### Ich muss einen Zweig in einer einzigen Übergabe zusammenführen

```sh
(main)$ git merge --squash my-branch
```

<a name="rebase-unpushed-commits"></a>

#### Ich möchte nur nicht gepushte Commits zusammenführen

Manchmal hat man mehrere in Arbeit befindliche Commits, die man kombinieren möchte, bevor man sie upstream schiebt. Sie wollen nicht versehentlich Commits kombinieren, die bereits upstream gepusht wurden, weil jemand anderes bereits Commits gemacht haben könnte, die auf sie verweisen.

```sh
(main)$ git rebase -i @{u}
```

Dies führt ein interaktives Rebase durch, das nur die Commits auflistet, die Sie noch nicht gepusht haben, so dass es sicher ist, alles in der Liste neu anzuordnen/zu korrigieren/zu löschen.

#### Ich muss die Zusammenführung abbrechen

In solchen Fällen können wir die Option `abort` verwenden, um den aktuellen Konfliktlösungsprozess abzubrechen und zu versuchen, den Zustand vor der Zusammenführung wiederherzustellen.

``sh
(mein-zweig)$ git merge --abort

```

Dieser Befehl ist seit Git Version >= 1.7.4 verfügbar

### Ich muss die übergeordnete Übergabe meines Zweigs aktualisieren

Angenommen, ich habe einen Hauptzweig, einen Feature-1-Zweig, der vom Hauptzweig abgezweigt ist, und einen Feature-2-Zweig, der von Feature-1 abgezweigt ist. Wenn ich einen Commit zu Feature-1 mache, dann ist der Eltern-Commit von Feature-2 nicht mehr korrekt (es sollte der Kopf von Feature-1 sein, da wir von ihm abgezweigt haben). Wir können dies mit `git rebase --onto` beheben.

```sh
(feature-2)$ git rebase --onto feature-1 <der erste Commit in Ihrem feature-2 Zweig, den Sie nicht mitnehmen wollen> feature-2
```

Dies ist in schwierigen Fällen hilfreich, in denen ein Feature auf einem anderen Feature aufbaut, das noch nicht zusammengeführt wurde, und ein Bugfix im Feature-1-Zweig in Ihrem Feature-2-Zweig berücksichtigt werden muss.

### Prüfen, ob alle Commits eines Zweiges zusammengeführt sind

Um zu überprüfen, ob alle Commits eines Zweiges in einen anderen Zweig zusammengeführt wurden, sollten Sie einen Diff zwischen den Köpfen (oder allen Commits) dieser Zweige durchführen:

```sh
(main)$ git log --graph --left-right --cherry-pick --oneline HEAD...feature/120-on-scroll
```

Dies zeigt Ihnen an, ob sich Commits in einem der beiden Zweige befinden, aber nicht im anderen, und gibt Ihnen eine Liste aller nicht gemeinsam genutzten Zweige. Eine andere Möglichkeit ist dies:

```sh
(main)$ git log main ^feature/120-on-scroll --no-merges
```

### Mögliche Probleme mit interaktiven Rebases

<a name="noop"></a>

#### Der Rebase-Bearbeitungsbildschirm sagt 'noop'

Wenn Sie dies sehen:

```
noop
```

Das bedeutet, dass Sie versuchen, gegen einen Zweig zu rebasen, der sich an einem identischen Commit befindet oder *vor* Ihrem aktuellen Zweig liegt. Sie können es versuchen:

- Stellen Sie sicher, dass Ihr Hauptzweig dort ist, wo er sein sollte
- rebase gegen `HEAD~2` oder früher stattdessen

<a name="merge-conflict"></a>

#### Es gab Konflikte

Wenn Sie das Rebase nicht erfolgreich abschließen können, müssen Sie möglicherweise Konflikte auflösen.

Führen Sie zunächst `git status` aus, um zu sehen, welche Dateien Konflikte enthalten:

```sh
(mein-zweig)$ git status
Auf Zweig my-branch
Änderungen, die nicht für die Übergabe bereitgestellt wurden:
  (verwenden Sie "git add <Datei>...", um zu aktualisieren, was übertragen werden soll)
  (verwenden Sie "git checkout -- <Datei>...", um Änderungen im Arbeitsverzeichnis zu verwerfen)

  beide geändert:   README.md
```

In diesem Beispiel hat die Datei `README.md` Konflikte. Öffnen Sie diese Datei und suchen Sie nach dem Folgenden:

```vim
   <<<<<<< HEAD
   etwas Code
   =========
   etwas Code
   >>>>>>> new-commit
```

Sie müssen die Unterschiede zwischen dem Code, der in Ihrem neuen Commit hinzugefügt wurde (im Beispiel alles von der mittleren Zeile bis `new-commit`) und Ihrem `HEAD` auflösen.

Wenn Sie die Version eines Zweiges des Codes behalten wollen, können Sie `--deiner` oder `--deren` verwenden:

``sh
(main*)$ git checkout --ours README.md

```

- Beim *Mergen* verwenden Sie `--deiner`, um Änderungen aus dem lokalen Zweig zu behalten, oder `--deiner`, um Änderungen aus dem anderen Zweig zu behalten.
- Beim *rebasing*, verwenden Sie `--theirs`, um Änderungen aus dem lokalen Zweig zu behalten, oder `--ours`, um Änderungen aus dem anderen Zweig zu behalten. Für eine Erklärung dieses Tausches, siehe [diese Notiz in der Git Dokumentation](https://git-scm.com/docs/git-rebase#git-rebase---merge).

Wenn die Zusammenführungen komplizierter sind, können Sie einen visuellen Diff-Editor verwenden:

```sh
(main*)$ git mergetool -t opendiff
```

Nachdem Sie alle Konflikte beseitigt und Ihren Code getestet haben, fügen Sie die geänderten Dateien mit `git add` hinzu, und setzen Sie dann die Umbasierung mit `git rebase --continue` fort

``sh
(mein-zweig)$ git add README.md
(mein-zweig)$ git rebase --continue

```

Wenn Sie nach dem Auflösen aller Konflikte einen identischen Baum wie vor der Übergabe haben, müssen Sie stattdessen `git rebase --skip` verwenden.

Wenn Sie zu irgendeinem Zeitpunkt den gesamten Rebase-Vorgang abbrechen und zum ursprünglichen Zustand Ihres Zweigs zurückkehren möchten, können Sie dies tun:

```sh
(mein-zweig)$ git rebase --abort
```

<a name="stashing"></a>

## Stash

### Alle Bearbeitungen zwischenspeichern

Um alle Bearbeitungen in Ihrem Arbeitsverzeichnis zwischenzuspeichern

```sh
git stash
```

Wenn Sie auch ungetrackte Dateien auslagern wollen, verwenden Sie die Option `-u`.

```sh
git stash -u
```

### Bestimmte Dateien stashen

Um nur eine Datei aus Ihrem Arbeitsverzeichnis zu verstecken

```sh
git stash push arbeitsverzeichnis-pfad/dateiname.ext
```

Um mehrere Dateien aus dem Arbeitsverzeichnis auszulagern

```sh
git stash push Arbeitsverzeichnis-Pfad/Dateiname1.ext Arbeitsverzeichnis-Pfad/Dateiname2.ext
```

<a name="stash-msg"></a>

### Stash mit Nachricht

```sh
git stash save <Nachricht>
```

oder

```sh
git stash push -m <Nachricht>
```

<a name="stash-apply-spezifisch"></a>

### Einen bestimmten Stash aus der Liste anwenden

Überprüfen Sie zunächst die Liste der Verstecke mit der Nachricht mit

```sh
git stash list
```

Wenden Sie dann einen bestimmten Stash aus der Liste an, indem Sie

```sh
git stash apply "stash@{n}"
```

Hier gibt 'n' die Position des Stashs im Stack an. Der oberste Stash ist die Position 0.

Darüber hinaus ist auch die Verwendung einer zeitbasierten Stash-Referenz möglich.

```sh
git stash apply "stash@{2.hours.ago}"
```

<a name="stage-and-keep-unstaged"></a>

### Stash unter Beibehaltung der unstaged Edits

Sie können manuell einen "stash commit" erstellen und dann "git stash store" verwenden.

``sh
git stash create
git stash store -m <Nachricht> CREATED_SHA1

```

## Finding

### Ich möchte eine Zeichenkette in einem beliebigen Commit finden.

Um eine bestimmte Zeichenkette zu finden, die in einem beliebigen Commit eingeführt wurde, können Sie die folgende Struktur verwenden:

```sh
git log -S "string to find"
```

Gemeinsame Parameter:

- `--source` bedeutet, dass der in der Kommandozeile angegebene Name angezeigt werden soll, über den jede Übergabe erreicht wurde.

- `--all` bedeutet, dass von jedem Zweig ausgegangen wird.

- `--reverse` druckt in umgekehrter Reihenfolge, d.h. es wird der erste Commit angezeigt, der die Änderung vorgenommen hat.

<a name="i-want-to-find-by-author-committer"></a>

### Ich möchte nach Autor/Committer suchen

Um alle Commits nach Autor/Committer zu finden, können Sie verwenden:

```sh
git log --author=<Name oder E-Mail>
git log --committer=<Name oder E-Mail>
```

Beachten Sie, dass Autor und Committer nicht dasselbe sind. Der "--author" ist die Person, die den Code ursprünglich geschrieben hat; der "--committer" hingegen ist die Person, die den Code im Namen des ursprünglichen Autors übertragen hat.

### Ich möchte Commits auflisten, die bestimmte Dateien enthalten

Um alle Commits zu finden, die eine bestimmte Datei enthalten, können Sie verwenden:

```sh
git log -- <Pfad zur Datei>
```

Normalerweise geben Sie einen exakten Pfad an, aber Sie können auch Platzhalter für den Pfad und den Dateinamen verwenden:

```sh
git log -- **/*.js
```

Bei der Verwendung von Platzhaltern ist es nützlich, `--name-status` anzugeben, um die Liste der übergebenen Dateien zu sehen:

```sh
git log --name-status -- **/*.js
```

<a name="#i-want-to-view-the-commit-history-for-a-special-function"></a>

### Ich möchte die Commit-Historie für eine bestimmte Funktion anzeigen

Um die Entwicklung einer einzelnen Funktion zu verfolgen, können Sie verwenden:

```sh
git log -L :Funktionsname:Dateipfad
```

Beachten Sie, dass Sie dies mit weiteren "git log"-Optionen kombinieren können, wie z.B. [revision ranges] (<https://git-scm.com/docs/gitrevisions>) und [commit limits] (<https://git-scm.com/docs/git-log/#_commit_limiting>).

### Finde ein Tag, in dem eine Übergabe referenziert wird

Um alle Tags zu finden, die einen bestimmten Commit enthalten:

```sh
git tag --enthält <commitid>
```

## Submodule

<a name="clone-submodules"></a>

### Klone alle Submodule

```sh
git clone --recursive git://github.com/foo/bar.git
```

Falls bereits geklont:

```sh
git submodule update --init --recursive
```

<a name="delete-submodule"></a>

### Entfernen eines Submoduls

Das Erstellen eines Submoduls ist ziemlich einfach, das Löschen dagegen weniger. Die Befehle, die Sie benötigen, sind:

```sh
git submodule deinit submodulename
git rm submodulename
git rm --cached submodulename
rm -rf .git/modules/submodulename
```

## Verschiedene Objekte

### Kopieren eines Ordners oder einer Datei von einem Zweig in einen anderen

```sh
git checkout <Branch-du-willst-das-Verzeichnis-von> -- <Ordner-Name oder Datei-Name>
```

### Wiederherstellen einer gelöschten Datei

Suchen Sie zunächst den Commit, an dem die Datei zuletzt existierte:

```sh
git rev-list -n 1 HEAD -- Dateiname
```

Dann checken Sie diese Datei aus:

```
git checkout deletingcommitid^ -- filename
```

### Tag löschen

```sh
git tag -d <tag_name>
git push <remote> :refs/tags/<tag_name>
```

<a name="recover-tag"></a>

### Wiederherstellen eines gelöschten Tags

Wenn Sie einen bereits gelöschten Tag wiederherstellen möchten, können Sie dies mit den folgenden Schritten tun: Zunächst müssen Sie den nicht mehr erreichbaren Tag finden:

```sh
git fsck --unreachable | grep tag
```

Notieren Sie sich den Hash des Tags. Stellen Sie dann das gelöschte Tag mit folgendem wieder her, indem Sie [`git update-ref`](https://git-scm.com/docs/git-update-ref) verwenden:

```sh
git update-ref refs/tags/<tag_name> <hash>
```

Ihr Tag sollte nun wiederhergestellt worden sein.

### Gelöschter Patch

Wenn Ihnen jemand einen Pull Request auf GitHub geschickt hat, dann aber den ursprünglichen Fork gelöscht hat, können Sie das Repository nicht klonen oder `git am` verwenden, da die [.diff, .patch](https://github.com/blog/967-github-secrets) URLs nicht mehr verfügbar sind. Aber Sie können den PR selbst mit [GitHub's special refs](https://gist.github.com/piscisaureus/3342247) auschecken. Um den Inhalt von PR#1 in einen neuen Zweig namens pr_1 zu holen:

```sh
$ git fetch origin refs/pull/1/head:pr_1
Von github.com:foo/bar
 * [new ref] refs/pull/1/head -> pr_1
```

### Exportieren eines Repositorys als Zip-Datei

```sh
git archive --format zip --output /full/path/to/zipfile.zip main
```

### Einen Zweig und einen Tag mit demselben Namen pushen

Wenn ein Tag in einem entfernten Repository den gleichen Namen wie ein Zweig hat, erhalten Sie folgende Fehlermeldung, wenn Sie versuchen, diesen Zweig mit dem Standardbefehl `$ git push <remote> <branch>` zu pushen.

``sh
$ git push origin <branch>
error: dst refspec same stimmt mit mehr als einem überein.
error: push some refs to '<git server>' fehlgeschlagen

```

Beheben Sie dieses Problem, indem Sie angeben, dass Sie die Head-Referenz pushen wollen.

```sh
git push origin refs/heads/<Zweig-name>
```

Wenn Sie ein Tag in ein entferntes Repository schieben wollen, das den gleichen Namen wie ein Zweig hat, können Sie einen ähnlichen Befehl verwenden.

```sh
git push origin refs/tags/<tag-name>
```

## Dateien nachverfolgen

<a href="ich-will-einen-dateinamen-ändern-kapitalisieren-ohne-den-inhalt-der-datei-zu-ändern"></a>

### Ich möchte die Großschreibung eines Dateinamens ändern, ohne den Inhalt der Datei zu verändern

```sh
(main)$ git mv --force myfile MeineDatei
```

### Ich möchte lokale Dateien überschreiben, wenn ich einen Git Pull durchführe

```sh
(main)$ git fetch --all
(main)$ git reset --hard origin/main
```

<a href="remove-from-git"></a>

### Ich möchte eine Datei aus Git entfernen, aber die Datei behalten

```sh
(main)$ git rm --cached log.txt
```

### Ich möchte eine Datei auf eine bestimmte Revision zurücksetzen

Angenommen, der Hash des gewünschten Commits ist c5f567:

```sh
(main)$ git checkout c5f567 -- file1/to/restore file2/to/restore
```

Wenn Sie auf Änderungen zurückgreifen wollen, die nur 1 Commit vor c5f567 gemacht wurden, übergeben Sie den Commit-Hash als c5f567~1:

```sh
(main)$ git checkout c5f567~1 -- file1/to/restore file2/to/restore
```

### Ich möchte die Änderungen einer bestimmten Datei zwischen Commits oder Zweigen auflisten

Angenommen, Sie wollen den letzten Commit mit der Datei von Commit c5f567 vergleichen:

```sh
$ git diff HEAD:path_to_file/file c5f567:path_to_file/file
# oder
$ git diff HEAD c5f567 -- path_to_file/file
```

Wenn Sie Änderungen zwischen den Spitzen des `main` und des `staging` Zweiges vergleichen wollen:

```sh
$ git diff main:path_to_file/file staging:path_to_file/file
# oder
$ git diff main staging -- path_to_file/file
```

### Ich möchte, dass Git Änderungen an einer bestimmten Datei ignoriert

Dies eignet sich hervorragend für Konfigurationsvorlagen oder andere Dateien, bei denen lokal Anmeldeinformationen hinzugefügt werden müssen, die nicht übertragen werden sollen.

```sh
git update-index --assume-unchanged file-to-ignore
```

Beachten Sie, dass dies die Datei *nicht* aus der Versionskontrolle entfernt - sie wird nur lokal ignoriert. Um dies rückgängig zu machen und Git wieder zu veranlassen, Änderungen zu beachten, wird das Ignore-Flag gelöscht:

```sh
git update-index --no-assume-unchanged file-to-stop-ignoring
```

## Fehlersuche mit Git

Der Befehl [git-bisect](https://git-scm.com/docs/git-bisect) verwendet eine binäre Suche, um herauszufinden, welcher Commit in Ihrer Git-Historie einen Fehler eingeführt hat.

Nehmen wir an, Sie befinden sich auf dem `main`-Zweig und wollen den Commit finden, der eine Funktion zerstört hat. Sie starten bisect:

```sh
git bisect start
```

Dann sollten Sie angeben, welcher Commit schlecht ist und welcher als gut bekannt ist. Angenommen, Ihre *aktuelle* Version ist schlecht, und `v1.1.1` ist gut:

```sh
git bisect schlecht
git bisect good v1.1.1
```

Jetzt wählt `git-bisect` einen Commit in der Mitte des von Ihnen angegebenen Bereichs aus, überprüft ihn und fragt Sie, ob er gut oder schlecht ist. Sie sollten etwas sehen wie:

```sh
Bisecting: 5 Revisionen zum Testen übrig (ungefähr 5 Schritte)
[c44abbbee29cb93d8499283101fe7c8d9d97f0fe] Commit Nachricht
(c44abbb)$
```

Sie werden nun überprüfen, ob dieser Commit gut oder schlecht ist. Wenn er gut ist:

```sh
(c44abbb)$ git bisect good
```

und `git-bisect` wählt einen anderen Commit aus dem Bereich für Sie aus. Dieser Prozess (Auswahl von ``gut`` oder ``schlecht``) wiederholt sich, bis keine Revisionen mehr übrig sind, die man untersuchen kann, und der Befehl gibt schließlich eine Beschreibung der **ersten** schlechten Übertragung aus.

## Konfiguration

### Ich möchte Aliase für einige Git-Befehle hinzufügen

Unter OS X und Linux wird Ihre Git-Konfigurationsdatei in ```~/.gitconfig`` gespeichert.  Ich habe einige Beispiel-Aliase, die ich als Abkürzungen benutze (und einige meiner häufigen Tippfehler), in den```[alias]``-Abschnitt eingefügt, wie unten gezeigt:

```vim
[alias]
    a = hinzufügen
    amend = commit --amend
    c = festschreiben
    ca = Übertragen --Ändern
    ci = Übertragen -a
    co = auschecken
    d = diff
    dc = diff --geändert
    ds = diff --staged
    extend = commit --amend -C HEAD
    f = fetch
    loll = log --graph --decorate --pretty=oneline --abbrev-commit
    m = zusammenführen
    eins = protokollieren --pretty=oneline
    outstanding = rebase -i @{u}
    reword = commit --amend --only
    s = Status
    unpushed = protokollieren @{u}
    wc = whatchanged
    wip = rebase -i @{u}
    zap = fetch -p
    day = log --reverse --no-merges --branches=* --date=local --since=midnight --author=\"$(git config --get user.name)\"
    delete-merged-branches = "!f() { git checkout --quiet main && git branch --merged | grep --invert-match '\\*' | xargs -n 1 git branch --delete; git checkout --quiet @{-1}; }; f"
```

### Ich möchte ein leeres Verzeichnis zu meinem Repository hinzufügen

Das geht nicht! Git unterstützt dies nicht, aber es gibt einen Hack. Sie können in dem Verzeichnis eine .gitignore-Datei mit folgendem Inhalt erstellen:

```
 # Ignoriere alles in diesem Verzeichnis
 *
 # Außer dieser Datei
 !.gitignore
```

Eine weitere gängige Konvention ist die Erstellung einer leeren Datei im Ordner mit dem Namen .gitkeep.

```sh
mkdir mydir
touch mydir/.gitkeep
```

Sie k?nnen die Datei auch einfach .keep nennen, in diesem Fall w?re die zweite Zeile oben ```touch mydir/.keep```

### Ich möchte einen Benutzernamen und ein Passwort für ein Repository zwischenspeichern

Sie haben vielleicht ein Repository, das eine Authentifizierung erfordert.  In diesem Fall können Sie einen Benutzernamen und ein Passwort zwischenspeichern, damit Sie sie nicht bei jedem Push und Pull eingeben müssen. Credential Helper kann dies für Sie tun.

```sh
$ git config --global credential.helper cache
# Git so einstellen, dass es den Credential-Speicher-Cache benutzt
```

```sh
$ git config --global credential.helper 'cache --timeout=3600'
# Den Cache so einstellen, dass nach 1 Stunde ein Timeout erfolgt (die Einstellung erfolgt in Sekunden)
```

Um einen Credential Helper zu finden:

```sh
$ git help -a | grep credential
# Zeigt Ihnen mögliche Credential-Helfer
```

Für OS-spezifisches Caching von Anmeldeinformationen:

```sh
$ git config --global credential.helper osxkeychain
# Für OSX
```

```sh
$ git config --global credential.helper manager
# Git für Windows 2.7.3+
```

```sh
$ git config --global credential.helper gnome-keyring
# Ubuntu und andere GNOME-basierte Distributionen
```

Weitere Credential-Helfer können für verschiedene Distributionen und Betriebssysteme gefunden werden.

### Ich möchte, dass Git Berechtigungen und Dateimodusänderungen ignoriert

```sh
git config core.fileMode false
```

Wenn Sie dies zum Standardverhalten für angemeldete Benutzer machen wollen, dann verwenden Sie:

```sh
git config --global core.fileMode false
```

### Ich möchte einen globalen Benutzer festlegen

Um Benutzerinformationen zu konfigurieren, die in allen lokalen Repositories verwendet werden, und um einen Namen festzulegen, der bei der Überprüfung des Versionsverlaufs identifizierbar ist:

```sh
git config --global user.name "[vorname nachname]"
```

So legen Sie eine E-Mail-Adresse fest, die mit jeder Verlaufsmarkierung verknüpft wird:

```sh
git config --global user.email "[valid-email]"
```

## Ich habe keine Ahnung, was ich falsch gemacht habe

Du bist also aufgeschmissen - du hast irgendetwas "zurückgesetzt", oder du hast den falschen Zweig zusammengeführt, oder du hast einen Push erzwungen und jetzt kannst du deine Commits nicht mehr finden. Sie wissen, dass es Ihnen irgendwann einmal gut ging, und Sie wollen zu einem Zustand zurückkehren, in dem Sie sich befanden.

Dafür ist `git reflog` da. reflog" verfolgt alle Änderungen an der Spitze eines Zweiges, auch wenn diese Spitze nicht durch einen Zweig oder ein Tag referenziert wird. Im Grunde genommen wird jedes Mal, wenn sich HEAD ändert, ein neuer Eintrag zum reflog hinzugefügt. Dies funktioniert leider nur für lokale Repositories, und es verfolgt nur Bewegungen (nicht Änderungen an einer Datei, die zum Beispiel nirgendwo aufgezeichnet wurden).

```sh
(main)$ git reflog
0a2e358 HEAD@{0}: zurückgesetzt: Umzug nach HEAD~2
0254ea7 HEAD@{1}: checkout: Umzug von 2.2 nach main
c10f740 HEAD@{2}: checkout: Umzug von main nach 2.2
```

Das obige Reflog zeigt einen Checkout von main zum 2.2-Zweig und zurück. Von dort aus gibt es einen Hard Reset zu einem älteren Commit. Die letzte Aktivität ist oben mit `HEAD@{0}` gekennzeichnet.

Wenn es sich herausstellt, dass Sie versehentlich zurück gewechselt haben, wird das Reflog den Commit enthalten, auf den main zeigte (0254ea7), bevor Sie versehentlich 2 Commits gelöscht haben.

```sh
git reset --hard 0254ea7
```

Mit `git reset` ist es dann möglich, main wieder auf den vorherigen Commit zurückzusetzen. Dies bietet ein Sicherheitsnetz für den Fall, dass die Historie versehentlich geändert wurde.

(kopiert und bearbeitet von [Source](https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog)).

<a name="git-shortcuts"></a>

## Git Shortcuts

## Git Bash

Wenn Sie mit den oben genannten Befehlen vertraut sind, sollten Sie einige Shortcuts für Git Bash erstellen. Auf diese Weise können Sie viel schneller arbeiten, indem Sie komplexe Aufgaben mit wirklich kurzen Befehlen erledigen.

```sh
alias sq=squash

function squash() {
    git rebase -i HEAD~$1
}
```

Kopieren Sie diese Befehle in Ihre .bashrc oder Ihr .bash_profile.

### PowerShell unter Windows

Wenn Sie PowerShell unter Windows verwenden, können Sie auch Aliase und Funktionen einrichten. Fügen Sie diese Befehle zu Ihrem Profil hinzu, dessen Pfad in der Variablen `$profile` definiert ist. Weitere Informationen finden Sie auf der Seite [About Profiles](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles) auf der Microsoft-Dokumentationsseite.

``Powershell
Set-Alias sq Squash-Commits

Funktion Squash-Commits {
  git rebase -i HEAD~$1
}

```

# Andere Ressourcen

## Bücher

- [Learn Enough Git to Be Dangerous](https://www.learnenough.com/git-tutorial) - Ein Buch von Michael Hartl, das Git von den Grundlagen an behandelt
- [Pro Git](https://git-scm.com/book/en/v2) - Scott Chacons und Ben Straubs ausgezeichnetes Buch über Git
- [Git Internals](https://github.com/pluralsight/git-internals-pdf) - Scott Chacons anderes ausgezeichnetes Buch über Git
- [Nasa-Handbuch](https://www.nasa.gov/sites/default/files/atoms/files/nasa_systems_engineering_handbook.pdf)

## Tutorials

- [19 Git Tips For Everyday Use](https://www.alexkras.com/19-git-tips-for-everyday-use) - Eine Liste nützlicher Git One-Liner
- [Atlassian's Git tutorial](https://www.atlassian.com/git/tutorials) Git richtig einsetzen mit Tutorials für Anfänger und Fortgeschrittene.
- Git Branching lernen](https://learngitbranching.js.org/) Ein interaktives webbasiertes Branching/Merging/Rebasing-Tutorial
- [Git rebase vs. merge](https://medium.com/@porteneuve/getting-solid-at-git-rebase-vs-merge-4fa1a48c53aa)
- [Git Commands and Best Practices Cheat Sheet](https://zeroturnaround.com/rebellabs/git-commands-and-best-practices-cheat-sheet) - Ein Git-Spickzettel in einem Blogpost mit weiteren Erklärungen
- [Git from the inside out](https://codewords.recurse.com/issues/two/git-from-the-inside-out) - Ein Tutorium, das sich mit den Interna von Git befasst
- [git-workflow](https://github.com/asmeurer/git-workflow) - [Aaron Meurer](https://github.com/asmeurer)'s Anleitung zur Verwendung von Git für Beiträge zu Open Source Repositories
- [GitHub als Arbeitsablauf](https://hugogiraudel.com/2015/08/13/github-as-a-workflow/) - Ein interessanter Blick auf die Verwendung von GitHub als Arbeitsablauf, insbesondere mit leeren PRs
- [Githug](https://github.com/Gazler/githug) - Ein Spiel zum Erlernen gängiger Git-Workflows
- [learnGitBranching](https://github.com/pcottle/learnGitBranching) - Eine interaktive Git-Visualisierung, die herausfordert und weiterbildet!

## Skripte und Tools

- [firstaidgit.io](http://firstaidgit.io/) Eine durchsuchbare Auswahl der am häufigsten gestellten Git-Fragen
- [git-extra-commands](https://github.com/unixorn/git-extra-commands) - eine Sammlung nützlicher zusätzlicher Git-Skripte
- [git-extras](https://github.com/tj/git-extras) - GIT-Hilfsprogramme - Repo-Zusammenfassung, Repl, Changelog-Population, Prozentsatz der Autoren-Commits und mehr
- [git-fire](https://github.com/qw3rtman/git-fire) - git-fire ist ein Git-Plugin, das im Notfall hilft, indem es alle aktuellen Dateien hinzufügt, überträgt und in einen neuen Zweig schiebt (um Merge-Konflikte zu vermeiden).
- [git-tips](https://github.com/git-tips/tips) - Kleine Git-Tipps
- [git-town](https://github.com/Originate/git-town) - Allgemeine Git-Workflow-Unterstützung auf hohem Niveau! <http://www.git-town.com>

## GUI-Clients

* [GitKraken](https://www.gitkraken.com/) - Der geradezu luxuriöse Git-Client, für Windows, Mac & Linux
- [git-cola](https://git-cola.github.io/) - ein weiterer Git-Client für Windows und OS X
- [GitUp](https://github.com/git-up/GitUp) - Eine neuere GUI, die einige sehr eigenwillige Möglichkeiten bietet, mit den Komplikationen von Git umzugehen
- [gitx-dev](https://rowanj.github.io/gitx/) - ein weiterer grafischer Git-Client für OS X
- [Sourcetree](https://www.sourcetreeapp.com/) - Einfachheit trifft auf Leistung in einer schönen und kostenlosen Git-GUI. Für Windows und Mac.
- [Tower](https://www.git-tower.com/) - grafischer Git-Client für OS X (kostenpflichtig)
- [tig](https://jonas.github.io/tig/) - Terminal-Textmodus-Schnittstelle für Git
- [Magit](https://magit.vc/) - Schnittstelle zu Git, implementiert als Emacs-Paket.
- [GitExtensions](https://github.com/gitextensions/gitextensions) - eine Shell-Erweiterung, ein Visual Studio 2010-2015 Plugin und ein eigenständiges Git-Repository-Tool.
- Fork](https://git-fork.com/) - ein schneller und freundlicher Git-Client für Mac (beta)
- [gmaster](https://gmaster.io/) - ein Git-Client für Windows mit 3-Wege-Zusammenführung, Refactor-Analyse, semantischem Diff und Merge (Beta)
- [gitk](https://git-scm.com/docs/gitk) - ein Git-Client für Linux, der einen einfachen Blick auf den Status der Projektgruppe ermöglicht.
- [SublimeMerge](https://www.sublimemerge.com/) - Rasend schneller, erweiterbarer Client, der 3-Wege-Merge, leistungsstarke Suche und Syntaxhervorhebung bietet, in aktiver Entwicklung.
