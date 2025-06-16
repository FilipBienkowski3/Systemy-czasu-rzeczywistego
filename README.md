# Systemy Czasu Rzeczywistego – Projekt

## 1.Tytuł modelu
**System sterowania bramą wjazdową**

## 2.Autor
Filip Bieńkowski
📧 fbienkowski@student.agh.edu.pl

---

## 3.Opis modelowanego systemu
System kontroli bramy automatycznej to zintegrowany system embedded odpowiedzialny za bezpieczne i automatyczne zarządzanie bramą wjazdową. System obsługuje sterowanie pilotem, wykrywanie przeszkód, automatyczne zamykanie oraz tryb ręczny. Model został zaprojektowany z uwzględnieniem wymagań czasu rzeczywistego i bezpieczeństwa funkcjonalnego.

## 4.Opis ogólny
Architektura systemu
System zbudowany jest w oparciu o architekturę warstwową składającą się z:

Warstwy aplikacyjnej - procesy sterujące (GateController)
Warstwy urządzeń - czujniki i aktuatory (GateMotor, SafetySensor, etc.)
Warstwy sprzętowej - procesor, pamięć, magistrala komunikacyjna

Główne funkcjonalności

Sterowanie zdalne - obsługa sygnałów z pilota zdalnego sterowania
Monitoring bezpieczeństwa - ciągły nadzór nad przeszkodami w torze ruchu bramy
Automatyczne zamykanie - zamykanie bramy po upływie określonego czasu
Tryb ręczny - możliwość przełączenia na sterowanie manualne
Kontrola pozycji - precyzyjne śledzenie położenia bramy

Wymagania czasowe
System pracuje w czasie rzeczywistym z najkrótszym cyklem 20ms (SafetySensor) i najdłuższym 1000ms (AutoCloseScheduler). Scheduler RMS zapewnia deterministyczne wykonanie zadań.

## 5.Opis dla użytkownika

Jak używać systemu

Zdalne sterowanie - naciśnij przycisk na pilocie aby otworzyć/zamknąć bramę
Automatyczne zamykanie - brama automatycznie zamknie się po określonym czasie od otwarcia
Wykrywanie przeszkód - system automatycznie zatrzyma bramę przy wykryciu przeszkody
Tryb ręczny - w przypadku awarii można przełączyć na sterowanie manualne

Stany bramy

Closed - brama zamknięta
Opening - brama w trakcie otwierania
Open - brama otwarta
Closing - brama w trakcie zamykania
Stopped - brama zatrzymana (np. z powodu przeszkody)

Komendy sterujące

Open - otwórz bramę
Close - zamknij bramę
Stop - zatrzymaj bramę

## 6.Komponenty systemu

# Typy danych
-- Definicja komend sterujących - bramą data GateCommand
-- Status pozycji bramy z pięcioma możliwymi stanami - data GatePosition
-- Sygnał wykrycia przeszkody (wartość boolean) - data ObstacleDetected

# System główny
-- Główny system integrujący wszystkie komponenty
system implementation GateControlSystem.impl
    subcomponents
        gateController: process GateController.impl;  -- Proces sterujący
        gateMotor: device GateMotor.impl;             -- Silnik bramy
        limitSwitch: device LimitSwitch.impl;         -- Wyłączniki krańcowe
        remoteReceiver: device RemoteControlReceiver.impl;  -- Odbiornik pilota
        safetySensor: device SafetySensor.impl;       -- Czujnik bezpieczeństwa
        manualOverride: device ManualOverride.impl;   -- Przełącznik trybu ręcznego
        cpu: processor CPU.impl;                      -- Procesor główny
        ram: memory RAM.impl;                         -- Pamięć RAM
        communicationBus: bus CommunicationBus.impl;  -- Magistrala komunikacyjna

# Procesy i wątki
-- Główny proces sterujący zawierający logikę systemu - process GateController
-- Wątek przetwarzający komendy z okresem 100ms - thread CommandProcessor
-- Wątek monitoringu bezpieczeństwa z najwyższym priorytetem (50ms) - thread SafetyMonitor
-- Wątek automatycznego zamykania z najdłuższym okresem (1s) - thread AutoCloseScheduler

# Urządzenia
-- Silnik bramy - główny aktuator systemu (15kg) - device GateMotor
-- Czujnik bezpieczeństwa - najczęściej sprawdzany (20ms) - device SafetySensor
-- Odbiornik zdalnego sterowania - tryb sporadyczny - device RemoteControlReceiver

#Sprzęt
-- Procesor z schedulingiem RMS i mocą 100 MIPS - processor CPU
-- Magistrala komunikacyjna z przepustowością 10 MB/s - bus CommunicationBus

## 7.Model - diagramy



## Analiza czasowa
System spełnia wymagania czasu rzeczywistego dzięki:

Algorytmowi szeregowania RMS
Odpowiednio dobranym okresom wykonania wątków
Budżetom mocy obliczeniowej nieprzekraczającym 50% dostępnej mocy procesora
Krótkim terminom wykonania zadań krytycznych dla bezpieczeństwa
