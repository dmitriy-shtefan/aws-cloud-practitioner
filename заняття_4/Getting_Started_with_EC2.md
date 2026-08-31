# Початок роботи з Amazon EC2

## Огляд і цілі

Ця практична робота надає базовий огляд запуску, зміни розміру, керування та моніторингу Amazon Elastic Compute Cloud (Amazon EC2) instance.

Amazon EC2 - це вебсервіс, який надає масштабовані обчислювальні ресурси в хмарі. Він розроблений так, щоб зробити хмарні обчислення вебмасштабу інтуїтивно зрозумілими та простими у використанні. Amazon EC2 забезпечує швидкий доступ до нових server instances і дає змогу оперативно збільшувати або зменшувати capacity відповідно до змін ваших обчислювальних потреб.

Можливості доступу до цієї практичної роботи за допомогою screen reader обмежені. Якщо ви використовуєте screen reader, зверніться до **Simulation Instructions** у вікні програвача, щоб дізнатися, як виконувати дії.

### Цілі

Після завершення цієї практичної роботи ви знатимете, як виконувати такі дії:

- запускати EC2 instance з увімкненим termination protection;
- здійснювати моніторинг EC2 instance;
- змінювати security group, яку використовує вебсервер, щоб дозволити HTTP access;
- підключатися до EC2 instance за допомогою AWS Systems Manager Fleet Manager;
- керувати станом EC2 instance;
- змінювати EC2 instance type;
- перевіряти роботу termination protection;
- досліджувати Amazon EC2 limits.

### Тривалість

Для завершення цієї практичної роботи потрібно приблизно 60 хвилин. Загалом на виконання завдання вам буде надано 180 хвилин.

## Завдання 1. Запуск EC2 instance

У цьому завданні ви запустите EC2 instance з termination protection. Termination protection запобігає випадковому припиненню роботи EC2 instance. Ви також розгорнете instance із user data script, який розгортає простий вебсервер.

1. В **AWS Management Console** у полі **Search** введіть `EC2` і натисніть **Enter**.
2. У результатах пошуку виберіть **EC2**.
3. У розділі **Launch instance** виберіть **Launch instance**.

### Крок 1. Надайте ім'я EC2 instance

За допомогою tags можна класифікувати AWS resources різними способами, наприклад за призначенням, власником або середовищем. Така класифікація корисна, коли у вас є багато resources одного типу. Ви можете швидко знайти конкретний resource за призначеними йому tags. Кожен tag складається з key і value, які ви визначаєте самостійно.

Коли ви надаєте instance ім'я, AWS створює пару key-value. Key цієї пари - `Name`, а value - ім'я, яке ви вводите для свого EC2 instance.

4. На панелі **Name and tags** у текстовому полі **Name** введіть `Web-Server`, а потім натисніть **Enter**.
5. Виберіть посилання **Add additional tags**.
6. У розкривному списку **Resource types** за замовчуванням вибрано **Instances**. Залиште **Instances** вибраним і додатково виберіть **Volumes**.

### Крок 2. Виберіть AMI

Amazon Machine Image (AMI) містить інформацію, необхідну для запуску instance, тобто віртуального сервера в хмарі. AMI містить:

- launch permissions, які визначають, які AWS accounts можуть використовувати AMI для запуску instances;
- шаблон root volume для instance, наприклад операційну систему з чистою інсталяцією або попередньо налаштовану операційну систему;
- block device mapping, що визначає volumes, які потрібно підключити до instance під час його запуску.

Список **Quick Start** містить найчастіше використовувані AMIs. Ви також можете створити власний AMI або вибрати AMI в AWS Marketplace - онлайн-магазині, де можна продавати або купувати програмне забезпечення, що працює в AWS.

7. Знайдіть розділ **Application and OS Images (Amazon Machine Image)**. Він розташований під розділом **Name and tags**. У полі пошуку введіть `Windows Server 2019 Base` і натисніть **Enter**.
8. Поруч із **Microsoft Windows Server 2019 Base** виберіть **Select**.

### Крок 3. Виберіть instance type

Amazon EC2 пропонує широкий вибір instance types, оптимізованих для різних сценаріїв використання. Instance types містять різні комбінації CPU, пам'яті, сховища та мережевої capacity, що дає змогу вибрати відповідний набір resources для ваших застосунків. Кожен instance type має один або кілька instance sizes, тому ви можете масштабувати resources відповідно до вимог цільового workload.

На цьому кроці ви виберете `t2.micro` instance. Цей instance type має один virtual CPU і 1 GiB пам'яті.

9. У розділі **Instance type** залиште instance type за замовчуванням - `t2.micro`.

   > **Примітка.** Створюючи власний instance, завжди перевіряйте, який instance type найкраще відповідає вашим потребам.

### Крок 4. Налаштуйте key pair

Amazon EC2 використовує public key cryptography для шифрування й розшифрування даних для входу. Щоб увійти в цей instance, створіть key pair, укажіть ім'я key pair під час запуску instance та надайте private key під час підключення до instance.

У цій практичній роботі ви не підключатиметеся до instance за допомогою SSH key, тому налаштовувати key pair не потрібно.

10. У розділі **Key pair (login)** у розкривному списку **Key pair name - required** виберіть **Proceed without a key pair (not recommended)**.

### Крок 5. Налаштуйте network settings

Ця панель використовується для налаштування параметрів мережі.

Virtual private cloud (VPC) визначає, у якому VPC потрібно запустити instance. Ви можете мати кілька VPC, зокрема окремі VPC для розробки, тестування та production.

11. У розділі **Network settings** виберіть **Edit**.
12. У розкривному списку **VPC - required** виберіть **Lab VPC**.

    Lab VPC було створено за допомогою AWS CloudFormation template під час налаштування практичної роботи. Цей VPC містить дві public subnets у двох різних Availability Zones.

13. У розділі **Firewall (security groups)** виберіть **Select existing security group**.
14. У списку **Common security groups** виберіть **Web Server security group**.

Security group працює як віртуальний firewall, що контролює traffic для одного або кількох instances. Під час запуску instance ви пов'язуєте з ним одну або кілька security groups. До кожної security group додаються rules, які дозволяють traffic до або від пов'язаних із нею instances. Rules security group можна змінити будь-коли; нові rules автоматично застосовуються до всіх instances, пов'язаних із цією security group.

### Крок 6. Додайте storage

Amazon EC2 зберігає дані на підключеному через мережу віртуальному диску Amazon Elastic Block Store (Amazon EBS). EC2 instance запускається з disk volume за замовчуванням обсягом 30 GiB. Це ваш root volume, також відомий як boot volume.

### Крок 7. Налаштуйте advanced details

15. Розгорніть розділ **Advanced details**.
16. У полі **IAM instance profile** виберіть role, ім'я якої починається з `LabStack`.

Коли EC2 instance більше не потрібен, його можна terminate. Це означає, що instance зупиняється, а Amazon EC2 вивільняє resources цього instance. Перезапустити terminated instance неможливо. Щоб запобігти випадковому припиненню роботи instance користувачами, для нього можна ввімкнути termination protection, яке не дає користувачам terminate instances.

17. У розкривному списку **Termination protection** виберіть **Enable**.

Під час запуску instance в Amazon EC2 ви можете передати йому user data. Ці команди можна використовувати для виконання типових автоматизованих завдань налаштування та запуску scripts після старту instance.

18. Скопіюйте наведені нижче команди, виберіть текстове поле **User data**, а потім виберіть **Paste**.

```powershell
<powershell>
# Installing web server
Install-WindowsFeature -name Web-Server -IncludeManagementTools
# Getting website code
wget https://us-east-1-tcprod.s3.amazonaws.com/courses/CUR-TF-100-EDCOMP/v1.0.4.prod-ef70397c/01-Lab-ec2/scripts/code.zip -outfile "C:\Users\Administrator\Downloads\code.zip"
# Unzipping website code
Add-Type -AssemblyName System.IO.Compression.FileSystem
function Unzip
{
    param([string]$zipfile, [string]$outpath)
    [System.IO.Compression.ZipFile]::ExtractToDirectory($zipfile, $outpath)
}
Unzip "C:\Users\Administrator\Downloads\code.zip" "C:\inetpub\"
# Setting Administrator password
$Secure_String_Pwd = ConvertTo-SecureString "P@ssW0rD!" -AsPlainText -Force
$UserAccount = Get-LocalUser -Name "Administrator"
$UserAccount | Set-LocalUser -Password $Secure_String_Pwd
</powershell>
```

Script виконує такі дії:

- установлює вебсервер Microsoft Internet Information Services (IIS);
- створює простий вебсайт;
- установлює пароль для користувача Administrator.

### Крок 8. Запустіть EC2 instance

Тепер, коли ви налаштували параметри EC2 instance, настав час запустити instance.

19. У розділі **Summary** виберіть **Launch instance**.

    З'явиться повідомлення про успішний початок запуску instance.

20. Виберіть **View all instances**.

Instance відображається у стані **Pending**, що означає, що він запускається. Потім стан змінюється на **Running**, що означає початок завантаження instance. Перш ніж instance стане доступним, мине трохи часу. У цій практичній роботі період очікування скорочено.

Instance отримує public DNS name, яке можна використовувати для підключення до нього через інтернет.

21. Поруч із вашим **Web-Server** установіть прапорець. Після цього відобразиться вкладка **Details**. Перегляньте вкладку **Details**, на якій наведено інформацію про instance.
22. Виберіть вкладку **Security** і перегляньте доступну інформацію.
23. Виберіть вкладку **Networking** і перегляньте доступну інформацію. Потім виберіть **Continue**.

Для instance мають відображатися такі дані:

- **Instance State:** `Running`;
- **Status Checks:** `2/2 checks passed`.

## Завдання 2. Моніторинг instance

Моніторинг є важливою складовою підтримання надійності, availability і performance ваших EC2 instances та AWS solutions.

24. Виберіть вкладку **Status and alarms**. Перегляньте доступну інформацію.

За допомогою instance status monitoring можна швидко визначити, чи виявив Amazon EC2 проблеми, які можуть перешкоджати запуску applications на instances. Amazon EC2 автоматично перевіряє кожен запущений EC2 instance, щоб виявити проблеми з hardware і software.

Зверніть увагу, що перевірки **System reachability** і **Instance reachability** успішно пройдено.

25. Виберіть вкладку **Monitoring**.

На цій вкладці відображаються Amazon CloudWatch metrics для вашого instance. Наразі metrics небагато, оскільки instance було запущено нещодавно.

Ви можете вибрати графік, щоб відкрити його розширене представлення.

Amazon EC2 надсилає metrics ваших EC2 instances до Amazon CloudWatch. Basic monitoring з інтервалом 5 хвилин увімкнено за замовчуванням і надається безкоштовно. Ви можете ввімкнути detailed monitoring з інтервалом 1 хвилина. У разі використання detailed monitoring плата стягується за кожну metric, яку ви надсилаєте до CloudWatch.

26. Угорі сторінки відкрийте розкривний список **Actions**, а потім виберіть **Monitor and troubleshoot** > **Get system log**.

System log відображає console output instance і є цінним засобом для діагностики проблем. Він особливо корисний для усунення проблем із налаштуванням сервісів, через які instance може terminate або стати недоступним. Якщо system log не відображається, зачекайте кілька хвилин і повторіть спробу.

27. У **System log** перегляньте повідомлення в output.
28. Щоб повернутися до Amazon EC2 dashboard, виберіть **Cancel**.
29. Переконайтеся, що ваш **Web-Server** вибрано, відкрийте розкривний список **Actions**, а потім виберіть **Monitor and troubleshoot** > **Get instance screenshot**.

Ця функція показує, який вигляд мала б консоль EC2 instance, якби до нього було підключено екран. Оскільки це Windows instance, на screenshot відображається заблокований екран входу.

Якщо вам не вдається підключитися до instance через SSH або RDP, ви можете зробити screenshot instance і переглянути його як зображення. Ця функція дає змогу побачити стан instance і швидше усунути проблему.

30. Унизу сторінки виберіть **Cancel**.

## Завдання 3. Оновлення security group і доступ до вебсервера

Під час запуску EC2 instance ви надали script, який установив вебсервер і створив просту вебсторінку. У цьому завданні ви отримаєте доступ до вмісту вебсервера.

Наразі отримати доступ до вебсервера неможливо, оскільки security group не дозволяє inbound traffic на port 80, який використовується для HTTP web requests. Наступний крок демонструє, як використовувати security group як firewall, щоб обмежувати network traffic, дозволений для входу та виходу з instance.

Щоб виправити це, оновіть security group і дозвольте web traffic на port 80.

31. На лівій навігаційній панелі виберіть **Security Groups**.
32. Поруч із **Web Server security group** установіть прапорець.
33. Виберіть вкладку **Inbound rules**.

    Наразі security group не містить rules.

34. Виберіть **Edit inbound rules**, потім **Add rule** і налаштуйте такі параметри:

    - **Type:** виберіть **HTTP**;
    - **Source:** виберіть **Anywhere-IPv4**.

    > **Примітка.** Зверніть увагу на повідомлення: «Rules із source `0.0.0.0/0` дозволяють усім IP addresses отримувати доступ до inbound port 80. Рекомендуємо налаштовувати security group rules так, щоб дозволяти доступ лише з відомих IP addresses». Це справді є поширеною best practice, однак у цій практичній роботі доступ дозволено з будь-якої IP address, щоб спростити налаштування security group і тестування вебсайту, який працює на вашому EC2 instance.

У цій практичній роботі можна лише додати нове ingress rule. Змінити rule після створення неможливо. Ретельно перевірте налаштування, перш ніж вибрати **Save rules**.

35. Виберіть **Save rules**.

У live environment ви могли б скопіювати public IPv4 address, вставити її в браузер і переконатися, що SG та user data script успішно розгорнуто.

## Завдання 4. Підключення до instance за допомогою AWS Systems Manager Fleet Manager

За допомогою Fleet Manager в AWS Systems Manager можна віддалено керувати managed nodes та налаштовувати їх. Managed node - це будь-який комп'ютер, налаштований для Systems Manager.

На початку практичної роботи ваш AWS user автоматично отримав permissions для використання Systems Manager. Крім того, AWS Identity and Access Management (IAM) policy, яку ви вибрали під час налаштування EC2 instance, увімкнула Systems Manager для instance **Web-Server**.

Однією зі зручних функцій Fleet Manager є можливість підключатися до EC2 instance за допомогою браузера. У цьому завданні ви підключитеся до Windows desktop за допомогою Fleet Manager.

36. У полі пошуку введіть `Systems Manager` і натисніть **Enter**.
37. Виберіть **Systems Manager**.
38. На лівій навігаційній панелі виберіть **Fleet Manager**.
39. У розділі **Managed nodes** виберіть свій **Web-Server** EC2 instance.
40. У розкривному списку **Node actions** виберіть **Connect**, а потім **Connect with Remote Desktop**.
41. Введіть **Username:** `Administrator`.
42. Введіть **Password:** `P@ssW0rD!`.
43. Виберіть **Connect**.

Через кілька секунд на панелі відобразиться Windows desktop. Ви можете працювати з ним так само, як із локальним комп'ютером. Як ви дізналися раніше, Amazon EC2 забезпечує швидкий доступ до compute resources. Замість придбання фізичного hardware та налаштування операційної системи достатньо запустити EC2 instance, і всю цю роботу буде автоматично виконано за вас протягом кількох хвилин.

44. Щоб відключитися від instance **Web-Server**, виберіть **Action**, а потім **End session**.
45. У спливному вікні ще раз виберіть **End session**.

## Завдання 5. Зміна розміру instance

Коли ваші потреби змінюються, instance може виявитися overutilized, тобто замалим, або underutilized, тобто завеликим. У такому разі можна змінити instance type.

### Зупиніть instance

Перш ніж змінювати розмір instance, його потрібно зупинити.

Коли ви зупиняєте instance, його роботу завершують. За зупинений EC2 instance плата не стягується, але плата за storage підключених EBS volumes зберігається.

46. В **AWS Management Console** знайдіть `EC2` і натисніть **Enter**. Потім виберіть **EC2**.
47. В **EC2 Management Console** на лівій навігаційній панелі виберіть **Instances**.
48. Установіть прапорець поруч із instance **Web-Server**. Угорі сторінки відкрийте розкривний список **Instance state** і виберіть **Stop instance**.
49. У спливному вікні **Stop instance?** виберіть **Stop**.

Instance виконає звичайне завершення роботи, а потім зупиниться.

50. Зачекайте, доки для **Instance state** не відобразиться значення **Stopped**.

### Змініть instance type

51. Установіть прапорець поруч із **Web-Server**. У розкривному списку **Actions** виберіть **Instance settings** > **Change instance type**, а потім налаштуйте такий параметр:

    - **Instance type:** виберіть `t2.nano`.

52. Виберіть **Apply**.

    > **Примітка.** У цій практичній роботі використання інших instance types заборонено.

### Запустіть instance зі зміненим розміром

Після повторного запуску instance матиме instance type `t2.nano`. Тепер ви знову запустите instance, який має менше пам'яті, але більше дискового простору.

53. Поруч із **Web-Server** установіть прапорець.
54. У розкривному списку **Instance state** виберіть **Start instance**.

Після повторного запуску instance для **Instance state** відобразиться значення **Running**. Виберіть **Continue**.

## Завдання 6. Перевірка termination protection

Коли instance більше не потрібен, його можна видалити. Ця операція називається termination. Після termination instance до нього неможливо підключитися або повторно запустити його.

У цьому завданні ви дізнаєтеся, як використовувати termination protection.

55. Установіть прапорець поруч із instance **Web-Server**. У розкривному списку **Instance state** виберіть **Terminate instance**.

    Зверніть увагу, що **Termination protection** увімкнено. Це захист від випадкового termination instance.

56. Виберіть **Terminate**, щоб побачити, що станеться під час спроби terminate instance.

    Якщо ви справді хочете terminate instance, необхідно вимкнути termination protection.

57. У розкривному списку **Actions** виберіть **Instance settings**, а потім **Change termination protection**.
58. Прапорець **Enable** буде встановлено. Зніміть його, щоб вимкнути termination protection.
59. Виберіть **Save**.
60. Тепер знову спробуйте terminate instance. У розкривному списку **Instance state** виберіть **Terminate instance**.
61. Тепер instance можна успішно terminate. Виберіть **Terminate**.

## Підсумок

У цій практичній роботі ви створили EC2 instance і навчилися керувати його властивостями, зокрема instance type. Ви змінили налаштування security group, щоб вебсайт став доступним, і навчилися використовувати termination protection для запобігання видаленню instance. Ви також навчилися зупиняти, запускати й terminate EC2 instance. Насамкінець ви дізналися, як знаходити EC2 limits для свого AWS account. Чудова робота!

Докладніше про AWS Training and Certification див. на сторінці [AWS Training and Certification](https://aws.amazon.com/training/).

Ми будемо вдячні за ваш відгук.

Якщо ви хочете поділитися відгуком, пропозиціями або виправленнями, надайте докладну інформацію через AWS Training and Certification Contact Form.

© 2024 Amazon Web Services, Inc. або її афілійовані компанії. Усі права захищено. Цю роботу заборонено відтворювати або розповсюджувати повністю чи частково без попереднього письмового дозволу Amazon Web Services, Inc. Комерційне копіювання, надання в користування або продаж заборонені.
