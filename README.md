# Inhaltsverzeichnis
- [Setup](#setup)
    - [1 XAMPP Installieren](#1-xampp-installieren)
    - [2 MySQL Workbench Installieren](#2-mysql-workbench-installieren)
    - [3 Visual Studio Code Installieren](#3-visual-studio-code-installieren)
- [Datenbanken](#datenbanken)
    - [1. Connection zur Datenbank herstellen](#1-connection-zur-datenbank-herstellen)
    - [2. ER Modell Erstellen](#2-er-modell-erstellen)
    - [3. SQL Script Erstellen](#3-sql-script-erstellen)
- [PHP](#php)
    - [1. VS Code Extensions](#1-vs-code-extensions)
    - [2. Projekt Setup](#2-projekt-setup)
    - [3. Projekt Basis Erstellen](#3-projekt-basis-erstellen)
    - [4. Daten mit PDO aus der Datenbank abrufen und in einer Tabelle anzeigen](#4-daten-mit-pdo-aus-der-datenbank-abrufen-und-in-einer-tabelle-anzeigen)

# Setup
## 1 XAMPP Installieren
1. XAMPP von [https://www.apachefriends.org/de/index.html](https://www.apachefriends.org/de/index.html) herunterladen und installieren.
2. XAMPP starten und Apache und MySQL starten.

## 2 MySQL Workbench Installieren
1. MySQL Workbench von [https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/) herunterladen und installieren. (Workbench Community)

## 3 Visual Studio Code Installieren
1. Visual Studio Code von [https://code.visualstudio.com/](https://code.visualstudio.com/) herunterladen und installieren.

# Datenbanken

## 1. Connection zur Datenbank herstellen
1. In XAMPP den MySQL Server starten
2. In MySQL Workbench auf das "+" klicken und eine neue Verbindung erstellen.
3. Hostname: localhost, Port: 3306, Username: root, Password: leer lassen.
4. Auf Test Connection klicken und wenn die Verbindung erfolgreich ist auf OK klicken.

## 2. ER Modell Erstellen
1. In MySQL Workbench auf File -> New Model klicken.
2. Auf "New Diagram" klicken und ein neues Diagramm erstellen.
3. In der linken Sidebar auf "mydb" rechtsklicken und auf "Edit Schema" klicken, gib der Datenbank einen passenden Namen.
Jetzt kannst du Tabellen erstellen und Beziehungen zwischen den Tabellen erstellen.

## 3. SQL Script Erstellen
1. In MySQL Workbench auf Database -> Forward Engineer klicken.
2. Drücke so lange "Next" bis du beim Script bist.
3. Achte jetzt auf den Schema Namne ob alles passt, und entferne alle "VISIBLE" texte von dem Script, mit einem externen Tool wie z.B. Visual Studio Code.
4. Füge jetzt das Script ohne "VISIBLE" in MySQL Workbench ein und führe es aus.

# PHP

## 1. VS Code Extensions
- [All In one PHP Support Extension Package](https://marketplace.visualstudio.com/items?itemName=DEVSENSE.phptools-vscode)
- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)

Diese Extensions können über den Extensions Tab in Visual Studio Code installiert werden, einfach den Namen eingeben und auf Installieren klicken.

## 2. Projekt Setup
In Visual Studio Code auf File -> Open Folder -> <C:\xampp\htdocs> navigieren und den Ordner "htdocs" auswählen.

Du kannst alle Dateien die da drin sind löschen, damit wir einen leeren HTDOCS Ordner haben.

## 3. Projekt Basis Erstellen
1. In Visual Studio Code erstellst du jetzt via Rechtsklick im leeren HTDOCS Ordner eine neue Datei mit dem Namen "config.php".

2. In dieser Datei fügst du folgenden Code ein:
```
<?php
$host = 'localhost';
$db = 'dbname';
$user = 'root';
$password = '';
$dsn = "mysql:host=$host;dbname=$db";
try {
    $pdo = new PDO($dsn, $user, $password);
} catch (PDOException $e) {
    echo 'Connection failed: ' . $e->getMessage();
}

?>
```

Dieser Code verbindet dich mit der Datenbank. Du musst die Variablen $db, $user und $password anpassen. $db ist der Name der Datenbank, $user ist der Benutzername und $password ist das Passwort.

3. Jetzt erstellst du eine neue Datei mit dem Namen "index.php". Das wird unsere Startseite.

Du kannst in VSCode wenn du ein "!" + Tab drückst, automatisch eine HTML Struktur erstellen lassen.

Du kannst jetzt je nach Usecase diese Datei mit HTMl Füllen, und z.B. Buttons oder Links einfügen. Hier ein Beispiel:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Willkommen auf der Startseite</h1>
</body>
</html>
```

4. Jetzt kannst du die Datei speichern und im Browser öffnen. Dazu musst du in der URL "localhost/index.php" eingeben.

5. Wenn du die Startseite siehst, hast du alles richtig gemacht.

## 4. Daten mit PDO aus der Datenbank abrufen und in einer Tabelle anzeigen
1. Erstelle eine neue Datei mit dem Namen "show.php".

2. Füge folgenden Code ein:
```
<?php
require_once 'config.php';

$sql = "SELECT * FROM users";
$stmt = $pdo->prepare($sql);
$users = $stmt->fetchAll();

?>

... HTML Code ...

<table>
    <thead>
        <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Email</th>
        </tr>
    </thead>
    <tbody>
        <?php foreach($users as $user): ?>
            <tr>
                <td><?php echo $user['id']; ?></td>
                <td><?php echo $user['name']; ?></td>
            </tr>
        <?php endforeach; ?>
    </tbody>
</table>
```

In dieser Datei verbinden wir uns mit der Datenbank und holen uns alle User aus der Tabelle "users". Diese Daten werden dann in einer Tabelle angezeigt.

$sql