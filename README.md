[![Swift](https://img.shields.io/badge/Swift-5.3-orange.svg)](https://swift.org)
[![Xcode](https://img.shields.io/badge/Xcode-12.4-blue.svg)](https://developer.apple.com/xcode)

# Трекер Задач.

Реализован абстрактный трекер задач в разных исполнениях:
1. `GCDJobTracker<Key, Output, Faulure>` с поддержкой протокола `CallbackBlockTracking`.
    - Использован GCD и примитивы синхронизации из него.
2. `ConcurrentJobTracker<Key, Output>` с поддержкой протокола `AsyncJobTracking`.
    - Использован structured/unstructured concurrency из swift
3. `CombineJobTracker<Key, Output, Failure>  с поддержкой протокола `PublishingJobTracking`.
    - По-максимуму использован Combine в связке с очередями из GCD.
    
Имплементации доступны извне пакета (public).

Реализован модификатор паблишера `.process(on: DispatchQueue)` (по аналогии с `.receive(on: Scheduler)`), 
который безопасно и корректно работает с параллельными (concurrent) очередями. 

Реализован с его помощью паблишер всех задач для трекера из п.3. 
Сам трекер построен с максимальным использованием инструментов Combine.
