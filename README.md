# Handbook

## Список полезных ресурсов для изучения разработчику
- [Google SRE book](https://sre.google/sre-book/foreword/)
- [JVM anatomy quarks](https://shipilev.net/jvm/anatomy-quarks/)
- [Визуальный paxos](https://isaacwr.github.io/thesecretlivesofdata/paxos/)
- [Визуальный raft](http://thesecretlivesofdata.com/raft/)
- [Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)
- [Доклад: JMM 2014](https://www.youtube.com/watch?v=iB2N8aqwtxc)
- [Доклад: S3 в OK 2022](https://www.youtube.com/watch?v=N3mbocqCtsk)
- [Доклад: soft skills на собесах 2022](https://www.youtube.com/watch?v=S-jQIYp38tc)
- [Доклад: бинарныое хранилище в ОК 2017](https://www.youtube.com/watch?v=Hs2txKgnpAk)
- [Доклад: платформа 4К-стриминга на миллион онлайнов в ОК 2018](https://www.youtube.com/watch?v=pqz_qld6jVA)
- [Доклад: подходы к реализации шардинга 2018](https://www.youtube.com/watch?v=DfaTNXCsYRg)
- [Доклад: теория параллельного программирования 2012](https://www.youtube.com/watch?v=D8DXW7wlGDE)
- [Лекции: concurrency 2022](https://www.youtube.com/playlist?list=PL4_hYwCyhAva37lNnoMuBcKRELso5nvBm)
- [Лекции: git 2021](https://www.youtube.com/playlist?list=PLDyvV36pndZFHXjXuwA_NywNrVQO0aQqb)
- [Лекции: hardware 2023](https://www.youtube.com/watch?v=czl3NwGNuHg&list=PLcXpxQEvs8cPCuSy7hliyFXI1l829u7RZ)
- [Лекции: java 2022](https://www.youtube.com/playlist?list=PLlb7e2G7aSpTCB2OxGlezpgOXwq4xer7Z)
- [Лекции: kubernetes 2021](https://www.youtube.com/playlist?list=PL8D2P0ruohOBSA_CDqJLflJ8FLJNe26K-)
- [Лекции: распределенные системы 2021](https://www.youtube.com/playlist?list=PL4_hYwCyhAvaYKF6HkyCximCvlExxxnrC)
- [Лекции: системное программирование 2019](https://www.youtube.com/playlist?list=PLrCZzMib1e9pOdLmE2qtMgL3QMEIrxyu7)
- [Лекции: управление IT-проектами и продуктом 2019](https://www.youtube.com/playlist?list=PLrCZzMib1e9oUFO9saNfPAqBjpQW8v9I-)
- [Список: GOF паттерны](https://refactoring.guru/ru/design-patterns)
- [Список: АиСД](https://www.geeksforgeeks.org/learn-data-structures-and-algorithms-dsa-tutorial/)
- [Статья: обзор ML](https://vas3k.ru/blog/machine_learning/)
- Clean Code. Robert Martin
- Computer Networks. Andrew Tanenbaum
- Database Internals. Alex Petrov
- Designing Data-Intensive Applications. Martin Kleppmann
- Introduction to Algorithms. Thomas Cormen
- Java Concurrency in Practice. Brian Goetz, Tim Peierls, Joshua Bloch, Joseph Bowbeer, David Holmes, Doug Lea
- Mastering Regular Expressions. Jeffrey Friedl
- Microservices Patterns. Chris Richardson
- Modern Operating Systems. Andrew Tanenbaum
- Structured Computer Organization. Andrew Tanenbaum, Todd Austin
- System Design Interview. Alex Xu
- The Staff Engineer's Path. Tanya Reilly

## Performance

### Troubleshooting
- stress and load testing
- monitoring and alerting
- tracing
- profiling
- logging

### Fix
- buffering and merge/deduplication
- caching and memoization
- cleanup
- concurrency
- copy reduction
- data compression
- hot and cold data storage (mem/SSD/HDD/streamer, etc.)
- improvement of higher quantiles at the cost of degradation of lower quantiles
- independent scaling
- indexing and CQRS
- load prediction
- manual memory and resource management
- more efficient transport and data format
- multicast
- multiplexing
- p2p
- parallelism, SIMD, sharding
- pipelining
- prefer sequential access to random
- prefetch
- prioritization
- rate limiting; circuit breaker; retry circuit breaker; retry budget; exponential backoff + jitter; deadline propagation
- reducing critical sections (Amdahl's law)
- replication and load balancing
- reserve
- reuse (buffers, object pool, GC free, etc.)
- simplifying data (quantization, PCA, etc.)
- simplifying requirements (weaker consistency model, not fair scheduling, approximate algorithm, etc.)
- speculative execution
- temporal and spatial locality
- trade-off between CPU/disk/net/mem
- trade-off between latency/throughput (batching, empty queues, etc.)
- trade-off between read/write
- upgrade hardware
- using right algorithm and data structure
- warming up (compilation using execution statistics)
- zero cost abstraction

## Вариантность

PECS (Producer Extends Consumer Super)

|                    |                                               | Java    | Kotlin | Scala |
|--------------------|-----------------------------------------------|---------|--------|-------|
| Ковариантность     | сам тип + наследники                          | extends | out    | +     |
| Контравариантность | сам тип + родители                            | super   | in     | -     |
| Инвариантность     | сам тип (Ковариантность + Контравариантность) |         |        |       |

## Concurrency
- with shared state
    + locking
    + wait-free algorithm
    + hardware transactional memory
- without shared state
    + actor model
    + functional programming

## Архитектура

### Возможные нефункциональные требования (атрибуты качества или архитектурные характеристики)
- Прозрачность
- Тестируемость
- Доступность
- Отказоустойчивость
- Масштабируемость
- Эластичность
- Удобство эксплуатации
- Поддерживаемость
- Безопасность
- Конфигурируемость
- Расширяемость
- Производительность
    + Пропускная способность
    + Задержка
    + Эффективное использование ресурсов
- Переносимость
- Удобство использования
- Модульность (cohesion и coupling)

### pg_stat_statements
```sql
SELECT   Substring(query, 1, 50)       AS short_query,
         Round(total_time::numeric, 2) AS total_time,
         calls,
         Round(mean_time::numeric, 2)                                             AS mean,
         Round((100 * total_time / Sum(total_time::numeric) OVER ())::numeric, 2) AS percentage_cpu
FROM     pg_stat_statements
ORDER BY total_time DESC LIMIT 20; 
```
