# Systemy Czasu Rzeczywistego – Projekt

## Tytuł modelu
**System sterowania bramą wjazdową**

## Autor
Filip Bieńkowski
📧 fbienkowski@student.agh.edu.pl

---

## Opis modelowanego systemu

### Opis ogólny
Zamodelowany system to **inteligentny system sterowania bramą wjazdową**, przeznaczony dla domów jednorodzinnych, wspólnot mieszkaniowych lub obiektów przemysłowych.  
Głównym celem systemu jest bezpieczne i niezawodne otwieranie/zamykanie bramy wjazdowej na podstawie poleceń z różnych źródeł – pilota, aplikacji mobilnej – z uwzględnieniem logiki bezpieczeństwa oraz trybów automatycznych.

### Opis szczegółowy
System umożliwia sterowanie bramą z wielu źródeł:
- pilot zdalnego sterowania,
- aplikacja mobilna,
- harmonogram czasowy (automatyczne zamykanie).

Fizyczne otwieranie i zamykanie realizuje **siłownik** sterowany przez **centralę systemową**. Ruch bramy monitorowany jest przez **czujniki krańcowe**, które wykrywają stany bramy (otwarta, zamknięta, pośrednia).  
**Czujniki bezpieczeństwa** (np. fotokomórki) wykrywają przeszkody – w razie ich wykrycia system zatrzymuje ruch bramy, zapobiegając wypadkom.  

W razie awarii, np. braku zasilania, dostępny jest **mechanizm ręcznego odblokowania** i możliwość zasilania awaryjnego.  
Dodatkowo, możliwa jest konfiguracja automatycznego zamknięcia bramy po określonym czasie lub wg ustalonego harmonogramu.

---

## Komponenty systemu

| Komponent              | Opis                                                                 |
|------------------------|----------------------------------------------------------------------|
| `system GateControlSystem`   | Główny system sterujący logiką bramy                               |
| `device GateMotor`           | Siłownik elektryczny otwierający/zamykający bramę                   |
| `device LimitSwitch`         | Czujniki pozycji krańcowej bramy (otwarta/zamknięta)                |
| `device RemoteControlReceiver` | Odbiornik sygnału z pilota zdalnego sterowania                     |
| `device SafetySensor`        | Czujniki bezpieczeństwa (np. fotokomórki)                            |
| `device ManualOverride`      | Mechanizm ręcznego otwierania bramy                                 |
| `thread CommandProcessor`    | Wątek sterujący główną logiką bramy                                 |
| `thread SafetyMonitor`       | Wątek monitorujący stan bezpieczeństwa systemu                      |
| `thread AutoCloseScheduler`  | Wątek zarządzający automatycznym zamknięciem                        |
| `bus CommunicationBus`       | Magistrala komunikacyjna łącząca wszystkie komponenty systemu        |

---

## Możliwości systemu

- Wieloźródłowe sterowanie bramą (pilot, aplikacja)
- Reakcja na przeszkody i sytuacje awaryjne
- Harmonogram czasowy i tryb automatycznego zamykania
- Obsługa ręcznego trybu awaryjnego
- Integracja z siecią i innymi systemami (opcjonalnie)




