### Sprint 1: Fundamenty Metodologiczne, Stabilizacja CI/CD i Eksperyment

Celem pierwszego sprintu jest zbudowanie stabilnego środowiska pomiarowego, zautomatyzowanie potoku wdrożeniowego oraz przeprowadzenie początkowego eksperymentu. Pozwoli to na uzyskanie wiarygodnego punktu odniesienia (Baseline) dla przyszłych modyfikacji generatora.

* **Zdefiniowanie ram eksperymentu badawczego (Projektowanie metryk)**
  * Wdrożenie zautomatyzowanych bramek jakości do pipeline'u (testy funkcjonalne, niefunkcjonalne oraz testy bezpieczeństwa, np. ZAP, Trivy).
* **Stabilizacja i higiena potoku CI/CD**
  * Wdrożenie uniwersalnego mechanizmu healthchecków w Jenkinsie, zapewniającego bezobsługową weryfikację stanu dla zróżnicowanych aplikacji.
  * Wprowadzenie polityki retencji (przechowywanie 3 ostatnich stabilnych wersji aplikacji) oraz automatyczne usuwanie osieroconych plików i starych obrazów (optymalizacja środowiska).
* **Wdrożenie wielopoziomowej strategii testowania oraz komunikacji zewnętrznej**
  * Implementacja testów na poziomie samego generatora (weryfikacja logiki tworzenia kodu) oraz na poziomie aplikacji (weryfikacja budowania obrazu).
  * Jeśli będzie to możliwe, otwarcie maszyny wirtualnej na ruch zewnętrzny w celu umożliwienia automatycznego wyzwalania potoków z zewnętrznych systemów kontroli wersji.
* **Wykonanie eksperymentu i dokumentacja**
  * Uruchomienie kolejnej wersji pipeline'u (POC) na zdefiniowanych kryteriach.
  * Udokumentowanie aktualnego stanu i porównanie do wersji bazowej

---

### Sprint 2: Skalowanie Code Generation (CG) i Zaawansowane Zastosowania Badawcze

Drugi sprint skupia się na rozbudowie kompetencji samego generatora, dołączeniu warstwy frontendowej oraz eksploracji innowacyjnych rozwiązań, takich jak włączenie AI do zautomatyzowanego potoku.

* **Ewolucja generatora (Od POC do dojrzałego narzędzia CG)**
  * Rozszerzenie obsługi typów danych oraz zaawansowana walidacja wejścia.
  * Wdrożenie zarządzania relacjami (np. walidacja integralności bazy/modeli) oraz inteligentna obsługa przypadków brzegowych (np. brak modelu w "usecases" blokujący generowanie pustych operacji).
* **Rozszerzenie stosu technologicznego o Frontend**
  * Próba włączenia generacji kodu frontendowego do istniejącego potoku, co pozwoli na testowanie kompleksowych aplikacji "Full-Stack".
* **Dynamiczna orkiestracja i izolacja środowisk (CD)**
  * Zarządzanie przydziałem portów i środowisk dla różnych aplikacji za pomocą centralnego słownika (np. "rejestr uruchomionych usług"), co pozwoli na równoległe wdrażanie wielu eksperymentów bez konfliktów.
* **Eksploracja AI w potoku i iteracja eksperymentalna**
  * Eksperymentalne włączenie sztucznej inteligencji bezpośrednio do pipeline'u CI/CD (np. jako asystenta rozwiązującego konflikty, optymalizującego wygenerowany kod lub analizującego wyniki testów ZAP/Trivy).
  * Przeprowadzenie zaktualizowanego eksperymentu na nowej architekturze i porównanie wyników skuteczności z eksperymentem bazowym (Baseline) ze Sprintu 1.