# Handbook

## Список полезных ресурсов для изучения разработчику
- [Google SRE book](https://sre.google/sre-book/foreword/)
- [JVM anatomy quarks](https://shipilev.net/jvm/anatomy-quarks/)
- [Java Memory Model 2014](https://www.youtube.com/watch?v=iB2N8aqwtxc)
- [Как и зачем решать зазачи на leetcode](https://www.youtube.com/watch?v=ugGT4T5HcsI)
- [Data Structure Visualizations](https://www.cs.usfca.edu/~galles/visualization/Algorithms.html)
- [Теория по базам данных 2024](https://www.youtube.com/playlist?list=PLzWf2xLEjn8ZBtdz9sLbBBnNo1FtvQe30)
- [Подходы к реализации шардинга 2018](https://www.youtube.com/watch?v=DfaTNXCsYRg)
- [Распределенные системы 2021](https://www.youtube.com/playlist?list=PL4_hYwCyhAvaYKF6HkyCximCvlExxxnrC)
- [Теория параллельного программирования 2012](https://www.youtube.com/watch?v=D8DXW7wlGDE)
- [Concurrency 2022](https://www.youtube.com/playlist?list=PL4_hYwCyhAva37lNnoMuBcKRELso5nvBm)
- [Retry](https://habr.com/ru/companies/yandex/articles/762678/)
- [Idempotency](https://habr.com/ru/companies/yandex/articles/442762/)
- [Teamlead Roadmap](https://tlroadmap.io/guide.html)
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
- multitarget code
- p2p
- parallelism
- pipelining
- precalculation
- prefer sequential access to random
- prefetch
- prioritization
- rate limiting; circuit breaker; retry circuit breaker; retry budget; exponential backoff + jitter; deadline propagation
- reducing critical sections (Amdahl's law)
- replication and load balancing
- reserve
- reuse (buffers, object pool, GC free, etc.)
- reorder
- sampling
- sharding
- SIMD
- simplifying data (quantization, PCA, etc.)
- simplifying requirements (weaker consistency model, not fair scheduling, approximate algorithm, etc.)
- speculative execution
- temporal and spatial locality
- trade-off between CPU/disk/net/mem
- trade-off between latency/throughput (batching, empty queues, etc.)
- trade-off between read/write
- upgrade hardware
- using right algorithm and data structure
- warming up (JIT, cache) or compilation using execution statistics
- zero cost abstraction

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
