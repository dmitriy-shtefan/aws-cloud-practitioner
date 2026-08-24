# Cloud Architecture

## 1. AWS Cloud Adoption Framework (AWS CAF)

**AWS CAF** — фреймворк для планування переходу організації до cloud і керування цифровою трансформацією. Він охоплює не лише технології, а й бізнес-процеси, людей, управління, безпеку та операційну діяльність. AWS CAF містить рекомендації для оцінювання й підвищення готовності організації до cloud. ([AWS Документація][2])

> **Для іспиту:** AWS CAF = **організація + перехід до cloud + цифрова трансформація**.

### Бізнес-результати

AWS CAF допомагає організації: ([AWS Документація][1])

- **зменшувати бізнес- та операційні ризики**;
- **збільшувати дохід** завдяки новим продуктам і можливостям;
- **підвищувати операційну ефективність** через оптимізацію й автоматизацію;
- **покращувати показники ESG** — екологічні, соціальні та управлінські результати.

Коротко: **ризик ↓ / дохід ↑ / ефективність ↑ / ESG ↑**.

## 2. Шість перспектив AWS CAF

| Перспектива | Фокус | Типові ознаки в запитанні |
| --- | --- | --- |
| **Business** | Бізнес-цінність cloud | стратегія, дохід, витрати, продукти, бізнес-результати |
| **People** | Люди, навички й культура | навчання, лідерство, персонал, організаційні зміни |
| **Governance** | Контроль і нагляд | ризики, фінанси, політики, портфель, програми й проєкти |
| **Platform** | Побудова cloud-середовища | архітектура, інфраструктура, застосунки, дані, CI/CD |
| **Security** | Захист даних і навантажень | IAM, вразливості, загрози, відповідність, інциденти |
| **Operations** | Експлуатація навантажень | моніторинг, зміни, інциденти, доступність, підтримка |

Мнемоніка: **B P G P S O** — Business, People, Governance, Platform, Security, Operations.

### Business Perspective

Забезпечує відповідність cloud-інвестицій стратегії та очікуваним бізнес-результатам. Типові зацікавлені сторони: **CEO, CFO, COO, CIO, CTO**. ([AWS Документація][3])

> Cloud має збільшити дохід, зменшити витрати або допомогти створити новий продукт → **Business**.

### People Perspective

Охоплює культуру, організаційну структуру, лідерство, навички й персонал. Допомагає розвивати культуру безперервного навчання. Типові зацікавлені сторони: **CIO, COO, CTO, HR і керівники організації**. ([AWS Документація][4])

> Працівникам бракує cloud-навичок або потрібні організаційні зміни → **People**.

### Governance Perspective

Координує cloud-ініціативи, допомагає максимізувати користь і зменшувати ризики. Охоплює управління ризиками, фінансами, політиками, портфелем, програмами й проєктами. Типові зацікавлені сторони: **CIO, CTO, CFO та керівник із ризиків**. ([AWS Документація][5])

> Потрібні процеси контролю cloud-витрат і ризиків → **Governance**.

### Platform Perspective

Охоплює побудову масштабованої cloud-платформи, модернізацію наявних навантажень і створення cloud-рішень. Типові зацікавлені сторони: **CTO, архітектори, інженери та технологічні керівники**. ([AWS Документація][6])

> Потрібно спроєктувати AWS-інфраструктуру для перенесення застосунків → **Platform**.

### Security Perspective

Забезпечує **конфіденційність, цілісність і доступність (CIA)** даних і навантажень. Охоплює IAM, захист даних та інфраструктури, керування вразливостями, виявлення загроз, відповідність вимогам і реагування на інциденти. Типові зацікавлені сторони: **CISO, фахівці з безпеки й відповідності, аудитори**. ([AWS Документація][7])

> Потрібна стратегія керування ідентичностями та захисту даних → **Security**.

### Operations Perspective

Визначає, як запускати, відстежувати та підтримувати cloud-навантаження відповідно до потреб бізнесу. Охоплює моніторинг, інциденти, зміни, оновлення, доступність, потужність і керування застосунками. Типові зацікавлені сторони: **операційні команди, менеджери ІТ-послуг і SRE**. ([AWS Документація][2])

> Потрібно покращити моніторинг і реагування на інциденти → **Operations**.

### Швидке повторення AWS CAF

| Business | People | Governance | Platform | Security | Operations |
| --- | --- | --- | --- | --- | --- |
| Навіщо? | Хто? | Як контролювати? | Як побудувати? | Як захистити? | Як підтримувати? |

---

## 3. AWS Well-Architected Framework

**AWS Well-Architected Framework** — набір найкращих практик і запитань для проєктування, оцінювання та покращення cloud-навантажень. Він допомагає створювати надійні, безпечні, продуктивні, економічно ефективні та сталі рішення в AWS. ([AWS Документація][8])

> **Для іспиту:** AWS Well-Architected = **архітектура + робоче навантаження + найкращі практики**.

## 4. Шість основ AWS Well-Architected

1. **Operational Excellence**
2. **Security**
3. **Reliability**
4. **Performance Efficiency**
5. **Cost Optimization**
6. **Sustainability**

Мнемоніка: **O S R P C S**. ([AWS Документація][9])

| Основа | Головна ідея | Типові ознаки в запитанні |
| --- | --- | --- |
| **Operational Excellence** | Експлуатувати й удосконалювати | автоматизація, IaC, моніторинг, часті зворотні зміни |
| **Security** | Захищати | IAM, шифрування, найменші привілеї, загрози, інциденти |
| **Reliability** | Працювати й відновлюватися після збоїв | доступність, резервні копії, масштабування, disaster recovery |
| **Performance Efficiency** | Ефективно використовувати належні ресурси | типи EC2, serverless, вибір БД, продуктивність |
| **Cost Optimization** | Усувати зайві витрати | невикористані ресурси, right-sizing, моделі ціноутворення |
| **Sustainability** | Зменшувати вплив на довкілля | енергія, викиди, ефективне використання ресурсів |

### Operational Excellence

Здатність ефективно підтримувати розробку й експлуатацію навантажень, спостерігати за їхньою роботою та постійно вдосконалювати процеси. Ключові практики: **Infrastructure as Code, автоматизація, моніторинг, невеликі часті зворотні зміни та навчання на операційних подіях**.

> Автоматизація розгортання інфраструктури замість ручних змін → **Operational Excellence**.

### Security

Захист даних, систем і активів за допомогою IAM, найменших привілеїв, шифрування, виявлення загроз, захисту інфраструктури та реагування на інциденти. Дані слід захищати **під час передавання і зберігання**. ([AWS Документація][8])

> Застосування принципу найменших привілеїв → **Security**.

### Reliability

Здатність навантаження правильно й стабільно працювати та відновлюватися після збоїв. Ключові практики: **автоматичне відновлення, розподілена архітектура, масштабування, резервне копіювання й аварійне відновлення**. ([AWS Документація][8])

> Застосунок автоматично відновлюється після відмови EC2 → **Reliability**.

### Performance Efficiency

Ефективне використання ресурсів відповідно до вимог системи та адаптація до змін технологій і попиту. Охоплює вибір типів EC2, serverless-рішень і баз даних, моніторинг продуктивності, масштабування та експерименти з новими технологіями.

> Потрібно вибрати найвідповідніший тип EC2 для навантаження → **Performance Efficiency**.

### Cost Optimization

Отримання максимальної бізнес-цінності без зайвих витрат. Ключові практики: **видалення невикористаних ресурсів, right-sizing, аналіз структури витрат, вибір моделей ціноутворення та узгодження пропозиції з попитом**.

> Компанія виявляє й зупиняє неактивні EC2 → **Cost Optimization**.

### Sustainability

Мінімізація впливу cloud-навантажень на довкілля: вимірювання впливу, скорочення зайвих ресурсів, підвищення їх використання та вибір ефективних технологій. AWS рекомендує визначати цілі сталого розвитку й порівнювати спожиті ресурси та викиди з корисним результатом. ([AWS Документація][10])

> Компанія хоче зменшити вплив AWS-навантажень на довкілля → **Sustainability**.

### Швидке повторення Well-Architected

| Основа | Контрольне питання |
| --- | --- |
| **Operational Excellence** | Як ми цим керуємо й удосконалюємо? |
| **Security** | Як ми це захищаємо? |
| **Reliability** | Чи продовжить система працювати після збою? |
| **Performance Efficiency** | Чи використовує система належні ресурси? |
| **Cost Optimization** | Чи не платимо ми забагато? |
| **Sustainability** | Як зменшити вплив на довкілля? |

---

## 5. AWS CAF і AWS Well-Architected: різниця

| | AWS CAF | AWS Well-Architected |
| --- | --- | --- |
| **Фокус** | Організація | Робоче навантаження й архітектура |
| **Мета** | Перехід до cloud і трансформація | Якісна cloud-архітектура |
| **Структура** | 6 перспектив | 6 основ |
| **Головне питання** | Як організації перейти до AWS? | Як правильно спроєктувати й експлуатувати навантаження? |

Приклади:

- працівникам бракує навичок AWS → **AWS CAF, People**;
- застосунок має автоматично відновлюватися після збоїв → **Well-Architected, Reliability**.

## 6. Що обов’язково знати для CLF-C02

### AWS CAF

- призначення: **перехід до cloud і цифрова трансформація організації**;
- 6 перспектив: **Business, People, Governance, Platform, Security, Operations**;
- бізнес-результати: **ризик ↓, дохід ↑, ефективність ↑, ESG ↑**;
- визначення перспективи за сценарієм.

### AWS Well-Architected Framework

- призначення: **найкращі практики cloud-архітектури**;
- 6 основ: **Operational Excellence, Security, Reliability, Performance Efficiency, Cost Optimization, Sustainability**;
- відмінності між основами та їх визначення за сценарієм.

Ці знання відповідають вимогам посібника CLF-C02 щодо основ Well-Architected і компонентів AWS CAF. ([AWS Документація][1])

Додатково: [AWS Cloud Adoption Framework](https://docs.aws.amazon.com/whitepapers/latest/overview-aws-cloud-adoption-framework/foundational-capabilities.html) і [AWS Well-Architected Framework](https://docs.aws.amazon.com/wellarchitected/latest/framework/the-pillars-of-the-framework.html).

[1]: https://docs.aws.amazon.com/pdfs/aws-certification/latest/cloud-practitioner-02/cloud-practitioner-02.pdf "AWS Certified Cloud Practitioner — Exam Guide (CLF-C02)"
[2]: https://docs.aws.amazon.com/whitepapers/latest/overview-aws-cloud-adoption-framework/foundational-capabilities.html "Foundational capabilities — AWS CAF"
[3]: https://docs.aws.amazon.com/whitepapers/latest/overview-aws-cloud-adoption-framework/business-perspective.html "Business perspective — AWS CAF"
[4]: https://docs.aws.amazon.com/whitepapers/latest/overview-aws-cloud-adoption-framework/people-perspective.html "People perspective — AWS CAF"
[5]: https://docs.aws.amazon.com/whitepapers/latest/overview-aws-cloud-adoption-framework/governance-perspective.html "Governance perspective — AWS CAF"
[6]: https://docs.aws.amazon.com/whitepapers/latest/overview-aws-cloud-adoption-framework/platform-perspective.html "Platform perspective — AWS CAF"
[7]: https://docs.aws.amazon.com/whitepapers/latest/overview-aws-cloud-adoption-framework/security-perspective.html "Security perspective — AWS CAF"
[8]: https://docs.aws.amazon.com/wellarchitected/latest/framework/definitions.html "Definitions — AWS Well-Architected Framework"
[9]: https://docs.aws.amazon.com/wellarchitected/latest/framework/the-pillars-of-the-framework.html "The pillars of the framework — AWS Well-Architected Framework"
[10]: https://docs.aws.amazon.com/wellarchitected/latest/framework/sus-design-principles.html "Sustainability design principles — AWS Well-Architected Framework"
