# Nutzung von xv6 für die Bearbeitung der Praktikumsaufgaben
Um das Betriebssystem xv6 zu Nutzen müssen einige Vorbereitungen getroffen werden.
Diese sind unterschiedlich je nach Betriebssystem.

## Setup für Windows 10/11
1. Installieren Sie das WSL (Windows Subsystem for Linux)
   1. Öffnen Sie die Konsole (cmd in Suchleiste)
   2. Geben Sie `wsl --install` ein
   3. Installieren lassen

2. Geben Sie `wsl ~` in einem Terminal ein um das Linux Subsystem zu starten.
   Falls aus irgendeinem Grund keine Distribution vorhanden ist, installieren Sie Ubuntu durch die Eingabe von `wsl --install -d ubuntu` in der Konsole und geben Sie dann `wsl ~` ein.
   Sie sollten nun das Linux Subsystem in ihrer Konsole offen haben.

3. Sie haben nun ein Linux System!
   Folgen Sie den Schritten in dem "Setup für Linux" um das System für die Nutzung von xv6 einzurichten.

### Troubleshooting für das Windows Setup
Falls Sie einen "Schwerwiegenden Fehler" bei ihrer Installation von WSL haben, kann dies eine Reihe an Ursachen haben.
Stellen Sie sicher, dass sie die Konsole als Administrator ausgeführt haben bzw. Ihr Nutzer Admin Rechte hat.

Wenn es immer noch nicht geht, konsultieren Sie bitte diesen Thread:
https://stackoverflow.com/questions/76405462/error-while-installing-the-wsl-in-window-10-by-running-wsl-install-in-powershe

Es kann sein, dass das "Windows Subsystem for Linux" erst auf ihrem System eingeschaltet werden muss, bevor sie das Installationskommando ausführen.

## Setup für Linux

Geben Sie die folgenden Kommandos ein um das System für die Nutzung von xv6 einzurichten:

    sudo apt-get update
    sudo apt-get install -y build-essential gcc-riscv64-linux-gnu qemu-system-riscv64 git make gdb-multiarch

Falls Sie eine Arch basierte Distribution verwenden:

    sudo pacman -Sy
    sudo pacman -S base-devel qemu-system-riscv riscv64-linux-gnu-gcc riscv64-linux-gnu-gdb git 

## Setup für Mac M1

Installieren Sie folgende Tools mit [Homebrew](https://brew.sh/):

    brew tap riscv/riscv
    brew install riscv-tools riscv64-elf-gcc qemu

Zum Ausführen von Xv6 müssen Sie eine zusätzliche Option benutzen:

    TOOLPREFIX=riscv64-elf- make qemu

## xv6 Quellcode von Github beziehen & Änderungen vornehmen

### Windows 10/11 & Mac : GitHub Desktop
Für das Clonen des Quellcodes und dem Pushen von Änderungen empfehlen wir für Windows und Mac Systeme das Verwenden von GitHub Desktop (https://desktop.github.com/download/).

Eine Anleitung, wie dieses Tool zu verwenden ist finden Sie hier:
https://docs.github.com/en/desktop/adding-and-cloning-repositories/cloning-and-forking-repositories-from-github-desktop

Das Tool ist in der Lage auf das Subsystem zuzugreifen.
Clonen Sie den Quellcode am besten in den home folder unter:

    \\wsl.localhost\Ubuntu\home\<IhrWSLNutzername>

oder alternativ, falls darunter nicht zu erreichen:

    %LOCALAPPDATA%\Packages\CanonicalGroupLimited.Ubuntu_79rhkp1fndgsc\LocalState\rootfs\home

### Linux: git

Falls ihr Hostsystem schon Linux ist, können Sie unbeschwerlich git nutzen.
Clonen Sie hierfür das xv6 Betriebsystem von dem von Github-Classroom erzeugten Repository.
Die URL dafür finden unter der grünen "Code" Fläche auf der Seite des Repositories.

    git clone <IhreRepoURLausGithub>

Wenn Sie Änderungen vornehmen, müssen Sie diese via einem Commit in das Repository einstellen und diesen Commit dann mittels git push an den GitHub Server senden.

    git add .
    git commit -m "Beschreibung der Änderungen hier"
    git push

Hinweis: Für die Bewertung clonen wir Ihr Repository von GitHub.
Ihre Abgabe erfolgt dadurch durch das Pushen von commit vor der Deadline.
Vergessen Sie daher nicht zu pushen!
