# Communication tussen server en flutter

## Algemeen

Deze file beschrijft hoe een model wordt opgesteld om data-transfers in json formaat mogelijk te maken. Het model bestaat eruit een "form" te maken in de vorm van een class die een bericht representeert. Hierbij wordt enkel de data beschreven en de rest wordt automatisch gegenereerd, deels met een aparte tool. Deze methode werkt alleen als de server dezelfde data verwacht/stuurt (key-value-pairs).

## stappenplan

- eenmalig
  1) Brengt dependencies in orde.
  
- telkens
  1) Maak een nieuwe class aan, liefst in een nieuwe file genoemd naar de class.
  2) Import de juiste files.
  3) Kopieer de setup-code en verander de naam van de file die gegenereert gaat worden naar die van de huidige _file_.
  4) Kopieer het skelet en verander elk voorkomen van de naam van de _class_ naar de nieuwe naam.
  5) Kies de gewenste data door deze ongeinitialiseerd te declaren op class level.
  6) Run het commando om de code te genereren.

## Dependencies

```yaml
dependencies:
  json_annotation: "3.1.0"

dev_dependencies:
  build_runner: "1.10.3"
  json_serializable: "3.5.0"
```

## Imports

```dart
import 'package:json_annotation/json_annotation.dart';
```

## Specifieke setup van de library

```dart
part 'user.g.dart'; // naam van gegenereerde file (aan te passen, filename)

@JsonSerializable()
```

## De form zelf met de data

```dart
class User {
  User(this.name, this.email);

  // Gewenste data
  String name;
  String email;
  int age;

  // json functies (aan te passen, classname)
  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
  Map<String, dynamic> toJson() => _$UserToJson(this);
}
```

## commando voor code-generatie

```bash
flutter pub run build_runner build
```
