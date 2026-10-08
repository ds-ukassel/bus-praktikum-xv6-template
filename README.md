# Nutzung von xv6 für die Bearbeitung der Praktikumsaufgaben
Um das Betriebssystem xv6 zu nutzen, müssen einige Vorbereitungen getroffen werden.
Diese sind unterschiedlich je nach Betriebssystem.

## Setup für Windows 10/11
1. Installieren Sie WSL (Windows Subsystem for Linux).
   1. Öffnen Sie die Konsole (geben Sie `cmd` in die Suchleiste ein).
   2. Geben Sie `wsl --install` ein.
   3. Lassen Sie die Installation abschließen.

2. Geben Sie `wsl ~` in einem Terminal ein, um das Linux-Subsystem zu starten.
   Falls aus irgendeinem Grund keine Distribution vorhanden ist, installieren Sie Ubuntu durch die Eingabe von `wsl --install -d ubuntu` in der Konsole und geben Sie dann `wsl ~` ein.
   Sie sollten nun das Linux-Subsystem in Ihrer Konsole geöffnet haben.

3. Sie haben nun ein Linux-System!
   Folgen Sie den Schritten im Abschnitt „Setup für Linux“, um das System für die Nutzung von xv6 einzurichten.

### Troubleshooting für das Windows Setup
Falls bei Ihrer Installation von WSL ein „Schwerwiegender Fehler“ auftritt, kann dies verschiedene Ursachen haben.
Stellen Sie sicher, dass Sie die Konsole als Administrator ausgeführt haben bzw. Ihr Nutzer über Adminrechte verfügt.

Wenn es immer noch nicht geht, konsultieren Sie bitte diesen Thread:
https://stackoverflow.com/questions/76405462/error-while-installing-the-wsl-in-window-10-by-running-wsl-install-in-powershe

Es kann sein, dass das „Windows Subsystem for Linux“ erst auf Ihrem System eingeschaltet werden muss, bevor Sie das Installationskommando ausführen.

## Setup für Linux

Geben Sie die folgenden Kommandos ein, um das System für die Nutzung von xv6 einzurichten:

    sudo apt-get update
    sudo apt-get install -y build-essential gcc-riscv64-linux-gnu qemu-system-riscv64 git make gdb-multiarch

Falls Sie eine Arch-basierte Distribution verwenden:

    sudo pacman -Sy
    sudo pacman -S base-devel qemu-system-riscv riscv64-linux-gnu-gcc riscv64-linux-gnu-gdb git 

## Setup für Mac M1

Installieren Sie die folgenden Tools mit [Homebrew](https://brew.sh/):

    brew tap riscv/riscv
    brew install riscv-tools riscv64-elf-gcc qemu

Zum Ausführen von xv6 müssen Sie eine zusätzliche Option verwenden:

    TOOLPREFIX=riscv64-elf- make qemu

## xv6-Quellcode von GitHub beziehen und Änderungen vornehmen

### Windows 10/11 und Mac: GitHub Desktop
Für das Klonen des Quellcodes und das Pushen von Änderungen empfehlen wir für Windows- und Mac-Systeme die Verwendung von GitHub Desktop (https://desktop.github.com/download/).

Eine Anleitung zur Verwendung dieses Tools finden Sie hier:
https://docs.github.com/en/desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop

Das Tool ist in der Lage, auf das Subsystem zuzugreifen.
Klonen Sie den Quellcode am besten in das Home-Verzeichnis unter:

    \\wsl.localhost\Ubuntu\home\<IhrWSLNutzername>

oder alternativ, falls dieses Verzeichnis nicht erreichbar ist:

    %LOCALAPPDATA%\Packages\CanonicalGroupLimited.Ubuntu_79rhkp1fndgsc\LocalState\rootfs\home

### Linux: git

Falls Ihr Hostsystem bereits Linux ist, können Sie problemlos Git nutzen.
Klonen Sie hierfür das xv6-Betriebssystem aus dem von GitHub Classroom erstellten Repository.
Die URL dafür finden Sie auf der Seite des Repositories unter der grünen „Code“-Schaltfläche.

    git clone <IhreRepoURLausGithub>

Wenn Sie Änderungen vornehmen, müssen Sie diese in einem Commit im Repository speichern und den Commit anschließend mit `git push` an den GitHub-Server senden.

    git add .
    git commit -m "Beschreibung der Änderungen hier"
    git push

Hinweis: Für die Bewertung klonen wir Ihr Repository von GitHub.
Ihre Abgabe besteht darin, einen Commit vor Ablauf der Abgabefrist zu pushen.
Vergessen Sie daher nicht zu pushen!
