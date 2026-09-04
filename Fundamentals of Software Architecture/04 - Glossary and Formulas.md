---
title: "FOSA Chapters 1-3 - Glossary and Formulas"
aliases:
  - "Software Architecture Glossary"
tags:
  - software-architecture
  - glossary
  - formulas
---

# Glossary and Formulas

← [[03 - Modularity|← Chapter 3]] | [[00 - Index|Index]]

## Основні терміни

| English term | Коротке пояснення |
|---|---|
| **Architecture characteristic** | Системна якість і критерій успіху: scalability, availability тощо |
| **Architecture decision** | Правило або constraint, що спрямовує implementation |
| **Architecture style** | Іменована базова topology системи |
| **Architecture vitality** | Актуальність архітектури в поточному business/technology context |
| **Architectural thinking** | Системне бачення впливу та trade-offs рішень |
| **Technical breadth** | Обізнаність у багатьох technologies та підходах |
| **Trade-off** | Виграш однієї властивості ціною іншої |
| **Modularity** | Логічний поділ системи на пов'язані частини |
| **Granularity** | Розмір цих частин |
| **Cohesion** | Наскільки elements усередині module належать разом |
| **Coupling** | Ступінь залежності між artifacts або modules |
| **Connascence** | Необхідність змінити один component разом з іншим |
| **Structural decay** | Поступова втрата задуманих architecture characteristics |
| **Fitness function** | Автоматизована перевірка архітектурної властивості або правила |

## Формули Chapter 3

### Abstractness

$$
A = \frac{m_a}{m_c + m_a}
$$

- $m_a$ - abstract artifacts;
- $m_c$ - concrete artifacts;
- діапазон переважно від `0` до `1`.

### Instability

$$
I = \frac{C_e}{C_e + C_a}
$$

- $C_e$ - efferent/outgoing coupling;
- $C_a$ - afferent/incoming coupling;
- `0` - stable, `1` - unstable.

### Distance from the Main Sequence

$$
D = |A + I - 1|
$$

- `D = 0` - точка лежить на Main Sequence;
- що більше `D`, то сильніший дисбаланс;
- high `A` + high `I` -> **Zone of Uselessness**;
- low `A` + low `I` -> **Zone of Pain**.

## Connascence cheat sheet

![[Assets/FOSA/connascence-strength.svg]]

Ліворуч - слабші й зазвичай бажаніші форми; праворуч - сильніші та дорожчі для зміни.

## Decision checklist

- Який **business driver** стоїть за рішенням?
- Які architecture characteristics справді критичні?
- Які є alternatives?
- Які benefits, costs і risks кожної?
- Які assumptions можуть змінитися?
- Чи не надто дрібна granularity?
- Чи висока cohesion усередині module?
- Який coupling перетинає boundaries?
- Чи можна замінити сильну connascence слабшою?
- Чи записано **why**, а не лише **how**?
- Як автоматично перевіряти compliance?

## Пов'язані нотатки

- [[01 - Introduction]]
- [[02 - Architectural Thinking]]
- [[03 - Modularity]]
