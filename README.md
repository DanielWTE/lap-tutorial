## 1. Setup
### 1.1 XAMPP Installieren
1. XAMPP von [https://www.apachefriends.org/de/index.html](https://www.apachefriends.org/de/index.html) herunterladen und installieren.
2. XAMPP starten und Apache und MySQL starten.

### 1.2 MySQL Workbench Installieren
1. MySQL Workbench von [https://dev.mysql.com/downloads/workbench/](https://dev.mysql.com/downloads/workbench/) herunterladen und installieren. (Workbench Community)

### 1.3 Visual Studio Code Installieren
1. Visual Studio Code von [https://code.visualstudio.com/](https://code.visualstudio.com/) herunterladen und installieren.

## 2. VS Code Extensions
- [All In one PHP Support Extension Package](https://marketplace.visualstudio.com/items?itemName=DEVSENSE.phptools-vscode)
- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)

Diese Extensions können über den Extensions Tab in Visual Studio Code installiert werden, einfach den Namen eingeben und auf Installieren klicken.

## 3. Projekt Setup
In Visual Studio Code auf File -> Open Folder -> <C:\xampp\htdocs> navigieren und den Ordner "htdocs" auswählen.

Du kannst alle Dateien die da drin sind löschen, damit wir einen leeren HTDOCS Ordner haben.

## 4. Projekt Basis Erstellen
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