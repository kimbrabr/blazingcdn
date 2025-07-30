# BlazingCDN

Высокопроизводительный распределённый CDN-кеш на C++23 с HTTP/3, lock-free RAM-кешем, LSM-деревом и репликацией через gossip.

---

## Основные возможности

- HTTP/3 + HTTPS/TLS 1.3 с высокопроизводительным роутером (`/v1/bucket/<hash>/w<width>h<height>.webp`)
- L1 кеш — lock-free in-RAM shared_ptr стек для горячих объектов
- L2 кеш — LSM-дерево на NVMe с mmap и madvise для холодных данных
- Репликация между нодами через gossip-протокол
- Реальное время: трассировки и метрики через side-car metricsd
- Кроссплатформенная плагин-архитектура для кодеков (WebP, AVIF, JPEG-XL)
- Современные C++23 возможности: constexpr regex, concepts, modules, variadic templates, CRTP
- CI/CD с Conan, CMake, sanitizers, clang-tidy, matrix билдом, Docker-образами
- Высокая параллельность: lock-free MPSC очереди, condition_variable, atomics, futex
- Полный контроль ABI/ODR/visibility для надёжности плагинов
- Полиморфные интерфейсы StorageBackend, CachePolicy, MetricsCollector и др.
- 1000+ unit и интеграционных тестов, включая Docker-compose кластерные тесты

---

## Технологии и инструменты

- Язык: C++23 (RAII, move-семантика, smart pointers, std::variant, std::optional, std::span)
- Сети: io_uring, Boost.Asio, epoll/kqueue, QUIC (HTTP/3)
- Многопоточность: std::thread, async, future, lock-free структуры
- Файловый ввод-вывод: mmap, aio, madvise
- Профилирование: perf, valgrind, Tracy, VTune
- CI: GitHub Actions / GitLab CI с matrix билдом и pre-commit hooks

---

## Архитектура

- Lock-free L1 кеш (shared_ptr стек)
- LSM-дерево на NVMe с mmap
- Gossip репликация и распределённые метрики
- Плагин-архитектура кодеков с ABI-контролем
- Полиморфные policy-based классы (EvictionPolicy, StorageBackend и др.)

---

## Сборка и запуск

```bash
git clone https://github.com/youruser/blazingcdn.git
cd blazingcdn
conan install . --build=missing
cmake -B build -S .
cmake --build build -- -j
./build/blazingcdn
