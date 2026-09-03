# Створення Virtual Private Cloud

## Огляд і цілі практичної роботи

Традиційні мережі складні. Вони потребують обладнання, кабелів, складних конфігурацій і спеціалізованих навичок. Amazon Virtual Private Cloud (Amazon VPC) приховує цю складність і спрощує розгортання захищених приватних мереж.

У цій практичній роботі ви створите власну virtual private cloud (VPC) і розгорнете в ній resources.

Можливості доступу до цієї практичної роботи за допомогою screen reader обмежені. Якщо ви використовуєте screen reader, зверніться до **Simulation Instructions**, щоб дізнатися, як виконувати дії.

### Цілі

Після завершення цієї практичної роботи ви зможете:

- пояснювати основні компоненти VPC;
- розгортати базову VPC із public subnets;
- розгортати Amazon Elastic Compute Cloud (Amazon EC2) instance у VPC.

Наприкінці практичної роботи ваша архітектура складатиметься з EC2 instance, розгорнутого у VPC.

### Тривалість

Для завершення цієї практичної роботи потрібно приблизно 45 хвилин.

## Завдання 1. Дослідження конфігурації Example VPC

У цій практичній роботі ви почнете з дослідження Example VPC. Example VPC створено за зразком default VPC, яка автоматично доступна в кожному Region у межах Amazon Web Services (AWS) account.

VPC - це віртуальна мережа, виділена для вашого AWS account. Вона логічно ізольована від інших віртуальних мереж в AWS Cloud. У VPC можна запускати AWS resources, зокрема EC2 instances.

Example VPC розгорнуто в AWS Region.

1. В **AWS Management Console** у меню **Services** введіть `VPC` і натисніть **Enter** на клавіатурі.
2. У результатах пошуку виберіть **VPC**.
3. На лівій навігаційній панелі виберіть **Your VPCs**.

Ви маєте побачити дві VPC: default VPC та Example VPC. Зверніть увагу, що Example VPC налаштовано з Classless Inter-Domain Routing (CIDR) range `172.31.0.0/16`. Цей CIDR range охоплює всі addresses від `172.31.0.0` до `172.31.255.255` - загалом 65 536 addresses.

4. Запишіть **VPC ID** для Example VPC, який закінчується на `882de`. Цей VPC ID знадобиться пізніше під час практичної роботи.
5. Виберіть **Continue**.

## Завдання 2. Дослідження subnet

У цьому завданні ви дослідите public subnet.

Subnet - це піддіапазон IP addresses у VPC. AWS resources можна запускати у визначеній subnet. Використовуйте public subnet для resources, які мають бути доступними з інтернету, а private subnet - для resources, які не повинні бути доступними з інтернету.

Example VPC містить чотири subnets.

6. На лівій навігаційній панелі виберіть **Subnets**.

Зверніть увагу, що всі subnets, імена яких починаються з `PublicSubnet`, пов'язані з однією VPC - Example VPC. Також кожна subnet має IPv4 CIDR range. Кожен subnet CIDR range є окремою підмножиною addresses, доступних у VPC. Під час проєктування subnets необхідно переконатися, що CIDR ranges у межах однієї VPC не перекриваються з address ranges, які використовують інші subnets.

7. У списку subnets установіть прапорець біля **PublicSubnet1**.

Ця subnet використовує IPv4 CIDR range `172.31.0.0/20`.

VPC має CIDR block `172.31.0.0/16`, що охоплює всі IP addresses виду `172.31.x.x`. Ця subnet має CIDR block `172.31.0.0/20`, що охоплює addresses від `172.31.0.0` до `172.31.15.255`. Ці CIDR ranges можуть здаватися схожими, але subnet менша за VPC через `/20` у CIDR range. Ця subnet використовує перші 4096 addresses, доступні у VPC. Консоль показує, що для використання доступна лише 4091 address, оскільки AWS завжди резервує п'ять addresses у кожній subnet для потреб IP networking.

Зверніть увагу, що параметр **Auto-assign public IPv4 address** має значення **Yes**, тобто його ввімкнено. Це означає, що subnet автоматично призначає public IP address усім instances, які в ній запускаються.

8. Виберіть **Continue**.

## Завдання 3. Дослідження internet gateway

У цьому завданні ви дослідите internet gateway VPC.

Internet gateway забезпечує зв'язок між resources у VPC та інтернетом. Це horizontally scaled, redundant і highly available компонент VPC. Він не створює availability risks або bandwidth constraints для network traffic.

Internet gateway надає доступ до інтернету двом subnets, розташованим у VPC.

Internet gateway виконує дві функції:

- надає target у route tables для підключення до інтернету;
- виконує network address translation (NAT) для instances, яким призначено public IPv4 addresses.

9. На лівій навігаційній панелі виберіть **Internet gateways**.

Перегляньте рядок з internet gateway під назвою **Example Internet Gateway**. Зверніть увагу, що **State** цього internet gateway має значення **Attached**. У стовпці **VPC ID** також указано, що internet gateway підключено до VPC ID для Example VPC.

10. Виберіть **Continue**.

## Завдання 4. Дослідження route table

У цьому завданні ви дослідите route table, яку використовує Example VPC.

Ви переконалися, що internet gateway існує та підключений до Example VPC. Перш ніж subnets зможуть використовувати internet gateway, пов'язану з ними route table потрібно налаштувати для використання internet gateway.

Route table містить набір rules, які називаються routes і визначають, куди спрямовується network traffic. Кожна subnet у VPC має бути пов'язана з route table, оскільки ця table керує routing для subnet. Subnet може бути пов'язана лише з однією route table одночасно, але з однією route table можна пов'язати кілька subnets.

Щоб використовувати internet gateway, route table subnet має містити route, який спрямовує internet-bound traffic до internet gateway. Якщо subnet пов'язана з route table, яка має route до internet gateway, така subnet називається public subnet.

Route table спрямовує traffic локально всередині VPC, а public traffic - до internet gateway.

11. На лівій навігаційній панелі виберіть **Route tables**.
12. Знайдіть і виберіть рядок із route table під назвою **Public Route Table**.

Ця route table пов'язана з Example VPC.

Вкладку **Routes** вибрано за замовчуванням. Перегляньте routes.

Route table містить дві routes: local route і public route.

Коли routes перекриваються, route tables використовують longest prefix match. Routes перекриваються, якщо дві routes у route table відповідають певній destination IP. У цьому випадку route `172.31.0.0/16` перекривається з route `0.0.0.0/0` для всіх destination IP у межах IP range `172.31.0.0/16`.

Оскільки prefix `172.31.0.0/16` має більше значення - 16 - порівняно з prefix `0.0.0.0/0`, значення якого дорівнює 0, route `172.31.0.0/16` використовуватиметься першою для всіх destination IP, що відповідають обом routes.

Отже, весь traffic, призначений для `172.31.0.0/16`, тобто range Example VPC, спрямовується локально. Ця route дає змогу всім subnets у VPC взаємодіяти між собою. Увесь інший traffic (`0.0.0.0/0`) спрямовується до internet gateway.

13. Виберіть вкладку **Subnet associations**.

У розділі **Explicit subnet associations** зверніть увагу, що до списку входить subnet з IPv4 CIDR block `172.31.0.0/20`. Це та сама subnet, яку ви переглядали раніше.

14. Виберіть **Continue**.

Усі subnets у цьому списку є public subnets, оскільки вони мають запис у route table, який спрямовує traffic до інтернету через internet gateway.

## Завдання 5. Дослідження security group

У цьому завданні ви дослідите й оновите security group, яку використовують subnets в Example VPC.

Security group працює як віртуальний firewall для instances і контролює inbound та outbound traffic. Security groups працюють на рівні elastic network interface instance, а не на рівні subnet. Тому кожен instance може мати власний firewall, який контролює traffic. Якщо під час запуску не вказати конкретну security group, instance автоматично призначається default security group для VPC.

Rules security group дозволяють доступ до всіх ports для traffic, що надходить із цієї security group. Rules також дозволяють outbound access до інтернету для internal і external traffic (`0.0.0.0/0`).

У цьому завданні ви переглянете default security group, пов'язану з Example VPC. Потім ви оновите custom security group, щоб користувачі могли отримувати доступ до resources через HTTP.

15. На лівій навігаційній панелі виберіть **Security groups**.
16. Знайдіть і виберіть рядок із default VPC security group для Example VPC, VPC ID якої закінчується на `882de`.
17. У нижній частині сторінки виберіть вкладку **Outbound rules**.

Ви побачите одне rule. Воно дозволяє **All protocols** і **All port ranges** надсилати traffic до будь-якої IP address (`0.0.0.0/0`).

18. Виберіть вкладку **Inbound rules**.

Ви побачите одне rule для incoming traffic. Воно дозволяє incoming traffic для **All protocols** і **All port ranges** від resources, які використовують default security group.

На наступному етапі ви протестуєте EC2 instance, який було розгорнуто в Example VPC на початку практичної роботи. Щоб incoming traffic із джерел поза межами VPC міг отримати доступ до цього вебсайту, потрібно додати нове security group rule. Оскільки default security group змінювати не варто, ви використаєте іншу security group. Потім додасте до неї rule, яке дозволяє HTTP traffic через port 80 з будь-якого джерела в інтернеті (`0.0.0.0/0`).

19. Зніміть вибір із default security group.
20. Знайдіть і виберіть рядок із security group **Web-Server-SG** для Example VPC.
21. У нижній частині сторінки виберіть вкладку **Inbound rules**.
22. Виберіть **Edit inbound rules**.
23. Виберіть **Add rule**.
24. Налаштуйте такі параметри:

    - у полі **Type** виберіть **HTTP**;
    - у розкривному списку **Source** виберіть **Anywhere-IPv4**;
    - у полі **Description** введіть `Allow web access` і натисніть **Enter**.

25. Виберіть **Save rules**.

## Завдання 6. Визначення VPC і subnet для EC2 instance та створення VPC

У цьому завданні ви знайдете VPC і subnet для EC2 instance. Ви також перевірите конфігурацію security group **Web-Server-SG**, переконавшись, що EC2 instance доступний з інтернету.

EC2 instance розгорнуто в public subnet у default VPC, а з EC2 instance пов'язано security group.

26. У полі пошуку введіть `EC2` і натисніть **Enter** на клавіатурі.
27. У меню **Services** виберіть **EC2**.
28. У розділі **Resources** виберіть **Instances (running)**.
29. Виберіть **Web-Server**.
30. У нижній частині екрана знайдіть значення **VPC ID** та **Subnet ID**.

Цей EC2 instance було розгорнуто в Example VPC, яку ви досліджували.

31. Перегляньте наведену нижче інформацію, а потім у вікні програвача виберіть **Continue**.

Цей EC2 instance було розгорнуто в Public Subnet 1, яка є частиною Example VPC.

Під час запуску EC2 instance для нього визначаються VPC і subnet. Ці конфігурації неможливо змінити. У наступному завданні ви ознайомитеся з кроками створення нового EC2 instance.

У live environment можна було б перевірити роботу вебсайту, запущеного на EC2 instance. Для цього потрібно скопіювати public IPv4 address і вставити її у веббраузер.

Default VPC дуже зручно використовувати на початку вивчення AWS Cloud. Однак у реальних проєктах часто потрібно створювати custom VPCs відповідно до вимог замовника. Наприклад, замовник міг уже використати CIDR range default VPC у конфігурації своєї on-premises network. Також замовнику може знадобитися інша кількість addresses у кожній subnet. Оскільки змінити CIDR ranges, призначені VPC або її subnets, неможливо, для замовника потрібно створити нову VPC.

У цьому сценарії ви створите нову VPC. Замовник надав такі мережеві вимоги до CIDR ranges VPC:

**Top-level VPC:**

- **VPC IPv4 CIDR block:** `10.0.0.0/16`.

**Availability Zones:**

- resources потрібно розгорнути у двох Availability Zones.

**Дві public subnets:**

- **Public Subnet 1:** `10.0.0.0/24`;
- **Public Subnet 2:** `10.0.1.0/24`.

**Дві private subnets:**

- **Private Subnet 1:** `10.0.2.0/24`;
- **Private Subnet 2:** `10.0.3.0/24`.

Example VPC, яку ви досліджували раніше, не мала private subnets. Пам'ятайте, що відмінність між public subnet і private subnet полягає в тому, чи доступна вона безпосередньо з інтернету. Route table, пов'язана з public subnet, містить route до internet gateway, а route table для private subnet такої route не має.

## Завдання 7. Створення custom VPC

VPC можна налаштувати, визначивши її IP address range і створивши subnets. Також можна налаштувати route tables, network gateways і параметри security.

VPC console містить wizard, який може автоматично створювати кілька архітектур VPC. За допомогою цього wizard ви створите нову VPC.

Якщо в кроках не згадано конфігурацію певного параметра, залиште його значення за замовчуванням.

32. В **AWS Management Console** у меню **Services** введіть `VPC` і натисніть **Enter** на клавіатурі.
33. У результатах пошуку виберіть **VPC**.
34. На лівій навігаційній панелі виберіть **Your VPCs**.
35. Виберіть **Create VPC**.
36. На сторінці **Create VPC** налаштуйте такі параметри:

    - у полі **Resources to create** виберіть **VPC and more**;
    - у полі **Name tag auto-generation** введіть `Lab` і натисніть **Enter** на клавіатурі;
    - переконайтеся, що **IPv4 CIDR block** має значення `10.0.0.0/16`;
    - у полі **Availability Zones (AZs)** виберіть `2`;
    - у полі **Number of public subnets** виберіть `2`;
    - у полі **Number of private subnets** виберіть `2`;
    - розгорніть **Customize subnets CIDR blocks**;
    - оновіть subnet CIDR block values наведеними нижче ranges. Після введення кожного значення натискайте **Enter**.

    **Дві public subnets:**

    - **Public Subnet 1a:** `10.0.0.0/24`;
    - **Public Subnet 2b:** `10.0.1.0/24`.

    **Дві private subnets:**

    - **Private Subnet 1a:** `10.0.2.0/24`;
    - **Private Subnet 2b:** `10.0.3.0/24`.

Перегляньте **Preview** diagram у wizard.

37. Виберіть **Continue**.
38. Виберіть **Create VPC**.

Wizard одразу почне створювати VPC. Після завершення ви матимете VPC з усіма компонентами, які досліджували раніше: subnets, route tables, internet gateway і default security group. VPC wizard також автоматично налаштує routes у route tables для public та private subnets.

Як і default security group, яку ви досліджували раніше, default security group, створена wizard, блокує incoming traffic з інтернету. Щоб отримати доступ до вебсервера в новій VPC, потрібно додати rule до окремої security group.

39. Виберіть **View VPC**.

Пам'ятайте, що default security group VPC не дозволяє traffic ззовні VPC. Оскільки default security group змінювати не варто, додайте нову security group до custom VPC.

40. На лівій навігаційній панелі виберіть **Security groups**.
41. Виберіть **Create security group**.
42. У полі **Security group name** введіть `Web-Server2-SG` і натисніть **Enter** на клавіатурі.
43. У полі **Description** введіть `Allows HTTP access` і натисніть **Enter** на клавіатурі.
44. У полі **VPC** виберіть **Lab-vpc**.
45. У розділі **Inbound rules** виберіть **Add rule**, а потім налаштуйте такі параметри:

    - у полі **Type** виберіть **HTTP**;
    - у розкривному списку **Source** виберіть **Anywhere-IPv4**;
    - у полі **Description** введіть `Allow web access` і натисніть **Enter** на клавіатурі.

46. Виберіть **Create security group**.

## Завдання 8. Дослідження параметрів запуску EC2 instance у custom VPC

У цьому завданні ви дослідите сторінку **Launch an instance** і введете параметри, необхідні для запуску нового EC2 instance у custom VPC.

47. У розділі **Launch instance** натисніть кнопку **Launch instance**.
48. На сторінці **Launch an instance** налаштуйте такі параметри:

    - на панелі **Name and tags** у полі **Name** введіть `Web-Server2` і натисніть **Enter** на клавіатурі;
    - у розділі **Application and OS Images (Amazon Machine Image)** за замовчуванням вибрано **Amazon Linux**. У списку **Amazon Machine Image (AMI)** виберіть **Amazon Linux 2 AMI**;

      > **Примітка.** Не вибирайте **Amazon Linux 2023 AMI**.

    - instance type за замовчуванням - `t2.micro`. Залиште це значення;
    - у розділі **Key pair (login)** у розкривному списку **Key pair name - required** виберіть **Proceed without a key pair (Not recommended)**;
    - у розділі **Network settings** виберіть **Edit** і налаштуйте такі параметри:
      - у полі **VPC - required** виберіть **Lab-vpc**;
      - у полі **Subnet** виберіть subnet, ім'я якої містить `public1`;
      - у полі **Auto-assign public IP** виберіть **Enable**;
      - у розділі **Firewall (security groups)** виберіть **Select an existing security group**;
      - у розкривному списку **Common security groups** виберіть security group **Web-Server2-SG**.

49. Виберіть **Launch instance**.

Чудова робота! Тепер ви знаєте, як створити custom VPC і розгорнути в ній новий EC2 instance.

## Практичну роботу завершено

Вітаємо! Ви завершили практичну роботу.

Ми будемо вдячні за ваш відгук.

Якщо ви хочете поділитися пропозиціями або виправленнями, надайте докладну інформацію через AWS Training and Certification Contact Form.

© 2022 Amazon Web Services, Inc. або її афілійовані компанії. Усі права захищено. Цю роботу заборонено відтворювати або розповсюджувати повністю чи частково без попереднього письмового дозволу Amazon Web Services, Inc. Комерційне копіювання, надання в користування або продаж заборонені.
