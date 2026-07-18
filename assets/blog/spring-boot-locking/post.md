---
title: Spring Boot Locking
slug: spring-boot-locking
date: 2026-07-18
author: Phat Le Tan
tags:
  - spring-boot
  - jpa
  - postgresql
---

# Spring Boot Locking

When multiple transactions touch the same row, you need a locking strategy to
keep data consistent. JPA gives you two options.

## Optimistic locking

Optimistic locking assumes conflicts are rare. Add a `@Version` column and JPA
checks it on update:

```java
@Version
private Long version;
```

If two transactions read the same version and both try to write, the second one
fails with an `OptimisticLockException`.

## Pessimistic locking

Pessimistic locking takes a database lock up front:

```java
entityManager.find(Account.class, id, LockModeType.PESSIMISTIC_WRITE);
```

Use it when contention is high and retrying would be expensive. Under the hood JPA
issues a locking `SELECT`:

```sql
SELECT id, balance, version
FROM account
WHERE id = 42
FOR UPDATE;
```

> **Note:** a pessimistic lock is held until the transaction commits, so keep those
> transactions short — long locks are how you turn a fast API into a queue.

## Configuration

Tune the lock timeout so a stuck transaction fails fast instead of hanging:

```yaml
spring:
  jpa:
    properties:
      jakarta:
        persistence:
          lock:
            timeout: 3000
```

## Which one?

| Strategy | Best for | Cost |
| --- | --- | --- |
| Optimistic | High read, low write contention | Retry on conflict |
| Pessimistic | High write contention, short transactions | Blocks other writers |

- **Optimistic** — high read, low write contention.
- **Pessimistic** — high write contention, short transactions.

Start optimistic; reach for pessimistic only when you measure a real problem.
