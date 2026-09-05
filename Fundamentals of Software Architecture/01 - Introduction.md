---
title: "Chapter 1 - Introduction"
tags:
  - software-architecture
  - architecture-decisions
  - chapter-1
source: "Fundamentals of Software Architecture: An Engineering Approach"
---

# Chapter 1 - Introduction

← [[00 - Index|Index]] | Далі: [[02 - Architectural Thinking|Chapter 2 →]]

> [!summary] Суть
> Software architecture - це структура системи, її системні якості, логічна поведінка та правила побудови. Рішення завжди залежать від контексту і мають trade-offs.

Джерело: [[dokumen_pub_fundamentals_of_software_architecture_a_modern_engineering.pdf]], сторінки книги 1-13.

## Чотири виміри software architecture

![[Assets/FOSA/architecture-dimensions.svg]]

*Перемальовано за Figure 1-1: чотири виміри утримують структуру системи як єдине ціле.*

| Вимір | Практичне значення | Приклад |
|---|---|---|
| **Architecture characteristics** | Критерії успіху, або *-ilities* | availability, performance, scalability |
| **Logical components** | Domains, entities і workflows | `Orders`, `Payments` |
| **Architecture style** | Базова topology системи | layered, microservices |
| **Architecture decisions** | Guardrails для реалізації | UI не має direct database access |

Архітектура є продуктом свого часу: на рішення впливають вартість infrastructure, доступні tools, business constraints, культура компанії та компетенції команди.

### Приклад: сервіс продажу квитків

*Навчальний приклад для пояснення чотирьох вимірів, не цитата з книги.*

Бізнес хоче продавати квитки на популярні концерти. «Купити квиток» - функціональна вимога. «Витримати одночасний наплив покупців» - вимога до **scalability**. Це різні питання, і виконання першої вимоги не гарантує другої.

| Вимір | Як він проявляється у прикладі |
|---|---|
| Characteristics | Витримувати пікове навантаження; зберігати коректність бронювання |
| Logical components | `Catalog`, `Reservations`, `Payments`, `Notifications` |
| Style | Для невеликої команди розглядаємо modular monolith як початкову структуру |
| Decisions | Лише `Reservations` змінює стан місця; решта звертається через його API |

Модулі тут можуть працювати в одному процесі. Якщо згодом одному з них знадобиться незалежне масштабування, переглянемо спосіб розгортання. Назви компонентів самі по собі ще не означають microservices.

## Три закони архітектури

### 1. Усе має trade-off

> "Everything in software architecture is a trade-off."  
> - *First Law of Software Architecture*, p. 6

Кожне рішення щось покращує і водночас створює cost або risk. Аналіз потрібно повторювати, бо контекст змінюється.

Наприклад, cache каталогу зменшує час відповіді та навантаження на database, але може показувати застарілі дані. Для опису концерту затримка оновлення може бути прийнятною; для підтвердження останнього вільного місця потрібна перевірка актуального стану. Вибір залежить навіть від конкретних даних усередині однієї системи.

### 2. Why важливіше за how

> "Why is more important than how."  
> - *Second Law of Software Architecture*, p. 7

Структура показує, **як** працює система, але не пояснює, **чому** обрано саме її. Документувати потрібно decision context, alternatives і consequences.

> [!example] Як виглядає корисне пояснення рішення
> **Рішення:** надсилати email після покупки через queue.
>
> **Чому:** недоступність email-провайдера не повинна блокувати оформлення квитка.
>
> **Ціна:** лист може прийти пізніше; потрібні повторні спроби та захист від дублювання.
>
> Запис «використовуємо queue» без цих причин майже не допоможе майбутній команді.

### 3. Рішення лежать на спектрі

> "Most architecture decisions aren't binary but rather exist on a spectrum between extremes."  
> - *Third Law of Software Architecture*, p. 7

Рішення рідко є простим `A` або `B`. Частіше це вибір прийнятної точки між consistency та availability, simplicity та flexibility, abstraction та implementation.

## Вісім очікувань від software architect

| Очікування | Що робити |
|---|---|
| **Make architecture decisions** | Задавати напрям і guardrails, не мікрокерувати всі technology choices |
| **Continually analyze architecture** | Підтримувати *architecture vitality*, виявляти *structural decay* |
| **Keep current with trends** | Розуміти нові можливості та ризики |
| **Ensure compliance** | Перевіряти виконання decisions і design principles |
| **Understand diverse technologies** | Розвивати technical breadth |
| **Know the business domain** | Говорити мовою problem domain і stakeholders |
| **Possess interpersonal skills** | Лідерство, mentoring, facilitation, communication |
| **Navigate organizational politics** | Обґрунтовувати рішення та узгоджувати інтереси |

> [!tip] Guide, не dictate
> "Use a reactive-based frontend framework" - architecture guidance. "Use React" - переважно technology decision. Конкретну технологію варто фіксувати лише тоді, коли вона захищає критичну architecture characteristic.

## Ключові поняття

- **Architecture vitality** - актуальність архітектури після змін у бізнесі й технологіях.
- **Structural decay** - поступове руйнування потрібних характеристик через непогоджені code/design changes.
- **Compliance** - відповідність реалізації прийнятим architectural decisions.
- **Business domain** - проблема, цілі, правила та мова бізнесу, для якого створюється система.

Наприклад, команда погодила, що лише `Reservations` керує бронюванням. Через дедлайн інший модуль почав напряму оновлювати його таблиці. Спочатку це працює, але зміна схеми вже вимагає координації двох модулів: так накопичується **structural decay**. Архітектор допомагає усунути обхід і перевіряти межі залежностей, а також з'ясовує, чому погоджений API виявився незручним.

## Самоперевірка

1. Які чотири виміри визначають software architecture?
2. Чому список технологій не є повним описом архітектури?
3. Який із трьох законів змушує записувати rationale рішення?
4. Чим guidance відрізняється від жорсткого technology choice?
5. Як structural decay може зруйнувати availability або scalability?

← [[00 - Index|Index]] | Далі: [[02 - Architectural Thinking|Chapter 2 →]]
