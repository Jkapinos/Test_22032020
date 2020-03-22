<main class="DocPage__content">

# <span>Создание сайта на WordPress</span>

<div class="DocPage__content-mini-toc yfm">

*   [Подготовьте облако к работе](https://cloud.yandex.ru/docs/solutions/web/wordpress#before-you-begin)
    *   [Необходимые платные ресурсы](https://cloud.yandex.ru/docs/solutions/web/wordpress#paid-resources)
*   [Создание виртуальной машины для WordPress](https://cloud.yandex.ru/docs/solutions/web/wordpress#create-vm)
*   [Настройка WordPress](https://cloud.yandex.ru/docs/solutions/web/wordpress#wordpress-setup)
*   [Настройка DNS](https://cloud.yandex.ru/docs/solutions/web/wordpress#configure-dns)
*   [Как удалить созданные ресурсы](https://cloud.yandex.ru/docs/solutions/web/wordpress#clear-out)

</div>

<div class="DocPage__body yfm">

Сценарий описывает создание и настройку веб-сайта на базе CMS WordPress с помощью специального образа ВМ.

Чтобы настроить веб-сайт на WordPress:

1.  [Создайте виртуальную машину для WordPress](https://cloud.yandex.ru/docs/solutions/web/wordpress#create-vm).
2.  [Настройте WordPress](https://cloud.yandex.ru/docs/solutions/web/wordpress#wordpress-setup).
3.  [Настройте DNS](https://cloud.yandex.ru/docs/solutions/web/wordpress#configure-dns).

Если сайт вам больше не нужен, [удалите ВМ с ним](https://cloud.yandex.ru/docs/solutions/web/wordpress#clear-out).

## [](https://cloud.yandex.ru/docs/solutions/web/wordpress#before-you-begin)Подготовьте облако к работе

Перед тем, как разворачивать сервер, нужно зарегистрироваться в Облаке и создать платежный аккаунт:

1.  Перейдите в [консоль управления](https://console.cloud.yandex.ru/), затем войдите в Яндекс.Облако или зарегистрируйтесь, если вы еще не зарегистрированы.
2.  [На странице биллинга](https://console.cloud.yandex.ru/billing) убедитесь, что у вас подключен [платежный аккаунт](https://cloud.yandex.ru/docs/billing/concepts/billing-account), и он находится в статусе `ACTIVE` или `TRIAL_ACTIVE`. Если платежного аккаунта нет, [создайте его](https://cloud.yandex.ru/docs/billing/quickstart/#create_billing_account).

Если у вас есть активный платежный аккаунт, вы можете создать или выбрать каталог, в котором будет работать ваша виртуальная машина, на [странице облака](https://console.cloud.yandex.ru/cloud).

[Подробнее об облаках и каталогах](https://cloud.yandex.ru/docs/resource-manager/concepts/resources-hierarchy).

Убедитесь, что в выбранном каталоге есть облачная сеть с подсетью хотя бы в одной зоне доступности. Для этого на странице каталога выберите сервис **Virtual Private Cloud**. Если в списке есть сеть — нажмите на нее, чтобы увидеть список подсетей. Если нужных подсетей или сети нет, [создайте их](https://cloud.yandex.ru/docs/vpc/quickstart).

### [](https://cloud.yandex.ru/docs/solutions/web/wordpress#paid-resources)Необходимые платные ресурсы

В стоимость поддержки веб-сайта на WordPress входит:

*   плата за постоянно запущенную виртуальную машину (см. [тарифы Yandex Compute Cloud](https://cloud.yandex.ru/docs/compute/pricing));
*   плата за использование динамического или статического внешнего IP-адреса (см. [тарифы Yandex Virtual Private Cloud](https://cloud.yandex.ru/docs/vpc/pricing)).

## [](https://cloud.yandex.ru/docs/solutions/web/wordpress#create-vm)Создание виртуальной машины для WordPress

Чтобы создать виртуальную машину:

1.  На странице каталога в [консоли управления](https://console.cloud.yandex.ru/) нажмите кнопку **Создать ресурс** и выберите **Виртуальная машина**.

    ![create-vm](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/vm-create-1.png)

2.  В поле **Имя** введите имя виртуальной машины: `wordpress`.

    *   Длина — от 3 до 63 символов.
    *   Может содержать строчные буквы латинского алфавита, цифры и дефисы.
    *   Первый символ — буква. Последний символ — не дефис.

    ![add-vm-name](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/vm-create-2.png)

3.  Выберите [зону доступности](https://cloud.yandex.ru/docs/overview/concepts/geo-scope), в которой будет находиться виртуальная машина.

4.  В блоке **Публичные образы** нажмите кнопку **Выбрать**. Выберите публичный образ **WordPress**.

    ![choose-image](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/vm-create-3.png)

5.  В блоке **Вычислительные ресурсы**:

    *   Выберите [платформу](https://cloud.yandex.ru/docs/compute/concepts/vm-platforms).
    *   Укажите необходимое количество vCPU и объем RAM.

    Для тестирования хватит минимальной конфигурации:

    *   **Платформа** — Intel Cascade Lake.
    *   **vCPU** — 2.
    *   **Гарантированная доля vCPU** — 5%.
    *   **RAM** — 1 ГБ.
6.  В блоке **Сетевые настройки** выберите, к какой подсети необходимо подключить виртуальную машину при создании.

7.  В пункте **Публичный адрес** выберите **Автоматически**.

    ![choose-network](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/vm-create-4.png)

8.  Укажите данные для доступа на виртуальную машину:

    *   В поле **Логин** введите имя пользователя.
    *   В поле **SSH ключ** вставьте содержимое файла открытого ключа. Пару ключей для подключения по SSH необходимо создать самостоятельно. Подробнее см. [Подключиться к виртуальной машине Linux по SSH](https://cloud.yandex.ru/docs/compute/operations/vm-connect/ssh).
9.  Нажмите кнопку **Создать ВМ**.

Создание виртуальной машины может занять несколько минут. Когда виртуальная машина перейдет в статус `RUNNING`, вы можете начать настраивать сайт.

При создании виртуальной машине назначается публичный IP-адрес и имя хоста (FQDN). Эти данные можно использовать для доступа по SSH.

## [](https://cloud.yandex.ru/docs/solutions/web/wordpress#wordpress-setup)Настройка WordPress

После того как виртуальная машина `wordpress` перейдет в статус `RUNNING`, выполните:

1.  В блоке **Сеть** на странице виртуальной машины в [консоли управления](https://console.cloud.yandex.ru/) найдите публичный IP-адрес виртуальной машины.

    ![add-ssh](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/vm-create-5.png)

2.  Перейдите по адресу виртуальной машины в браузере.

3.  Выберите язык и нажмите кнопку **Продолжить**.

    ![choose-language](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/wordpress-1.png)

4.  Заполните информацию для доступа к сайту:

    1.  Укажите любое название сайта, например, `yc-wordpress`.
    2.  Укажите имя пользователя, которое будет использоваться для входа в административную панель, например, `yc-user`.
    3.  Укажите пароль, который будет использоваться для входа в административную панель.
    4.  Укажите вашу электронную почту.

    ![credentials](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/wordpress-2.png)

5.  Нажмите кнопку **Установить WordPress**.

6.  Если установка прошла успешно, нажмите кнопку **Войти**.

    ![login](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/wordpress-3.png)

7.  Войдите на сайт, используя указанные на прошлых шагах имя пользователя и пароль. После этого откроется административная панель, в которой можно приступать к работе с вашим сайтом.

8.  Убедитесь, что сайт доступен, открыв публичный IP-адрес виртуальной машины в браузере.

## [](https://cloud.yandex.ru/docs/solutions/web/wordpress#configure-dns)Настройка DNS

Чтобы привязать сайт к домену, настройте DNS у вашего регистратора следующим образом:

*   A-запись: поддомен `@`, в качестве адреса используйте публичный IP-адрес виртуальной машины.
*   CNAME-запись: поддомен `www`, в качестве канонического имени используйте домен с точкой на конце, например: `example.com.`

## [](https://cloud.yandex.ru/docs/solutions/web/wordpress#clear-out)Как удалить созданные ресурсы

Чтобы перестать платить за развернутый сервер, достаточно [удалить](https://cloud.yandex.ru/docs/compute/operations/vm-control/vm-delete) виртуальную машину `wordpress`.

Если вы зарезервировали статический публичный IP-адрес специально для этой ВМ:

1.  Откройте сервис **Virtual Private Cloud** в вашем каталоге.
2.  Перейдите на вкладку **IP-адреса**.
3.  Найдите нужный адрес, нажмите значок ![ellipsis](./Создание сайта на WordPress _ Яндекс.Облако - Документация_files/options.svg) и выберите пункт **Удалить**.

</div>

</main>