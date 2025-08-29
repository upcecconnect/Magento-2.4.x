# UPC e-Commerce Connect для Magento 2

## Рекомендовані вимоги

- **Magento:** >= 2.4.0 (рекомендовано Magento 2.4.6 або 2.4.8)
- **PHP:** >= 8.1 (підтримуються також 7.4 та 8.2, залежно від вашого хостингу)
- **MySQL:** >= 5.7 або MariaDB >= 10.3
- Підтримка `openssl` для PHP (для підпису та перевірки)

---

## Як встановити модуль

Якщо у вас немає git, ви можете завантажити цей репозиторій у вигляді ZIP-архіву та вручну розмістити файли у вашій установці Magento.

1. Натисніть кнопку **`Code` → `Download ZIP`** на сторінці GitHub цього репозиторію.
2. Розпакуйте архів.
3. Скопіюйте вміст папки:

    ```
    magento-pgp/app/code/Upc
    ```

   у відповідну директорію вашого магазину Magento:

    ```
    ваш_проєкт_magento/app/code/Upc
    ```

4. Після цього виконайте стандартні команди для оновлення Magento:

    ```bash
    php bin/magento setup:upgrade
    php bin/magento setup:di:compile
    php bin/magento cache:flush
    ```

---

## Налаштування модуля

1. Перейдіть в **Адмін панель → Stores → Configuration → Sales → Payment Methods → UPC e-Commerce Connect**.
2. Введіть:
   - **Merchant ID** (отриманий від UPC)
   - **Terminal ID**
   - **Payment Gateway Action URL** (наприклад: `https://ecg.test.upc.ua` для тестового середовища)
3. Налаштуйте **Test Mode** якщо працюєте в тестовому середовищі.
4. За потреби активуйте **Pre-authorization**, тоді кошти спершу будуть заморожені (Hold).
5. Задайте **Sort Order** для порядку відображення на checkout.
6. Введіть у відповідні поля ваші **приватні ключі** (private key) та **сертифікати** (public certificate), отримані від UPC:
   - ключі вводяться у вигляді PEM з усіма рядками включно з `-----BEGIN PRIVATE KEY-----` та `-----END PRIVATE KEY-----`
   - сертифікати також з `-----BEGIN CERTIFICATE-----` ... `-----END CERTIFICATE-----`
7. Для тестового середовища введіть відповідні тестові ключі у окремі поля або залиште пустими, якщо не використовуються.
8. Надайте URL-адресу зворотного виклику до Українського процесингового центру, щоб увімкнути сповіщення про онлайн-платежі (вкажіть свій домен) `https://example.com/ecommconnect/webhook/index`

---

## Списання коштів (Capture) при Pre-authorization

- Якщо в адмінці в налаштуваннях методу ввімкнено **Pre-authorization**, замовлення спершу отримує статус `Awaiting Capture`.
- Для списання коштів адміністратор переходить на сторінку замовлення (**Sales → Orders → Order View**) та бачить форму **Capture via UPC**.
- Заповніть/перевірте суму, натисніть **Capture**, Magento надішле запит до UPC та після підтвердження переведе замовлення в `Processing`.

---

## Офіційна документація UPC
![UPC Logo](https://ecconnect.upc.ua/public/images/newLogo.svg)
- [API Checkout (українська)](https://docsecom.atlassian.net/wiki/spaces/DOCUK/pages/49644046/API+Checkout)

---

---

# UPC e-Commerce Connect for Magento 2

## Recommended requirements

- **Magento:** >= 2.4.0 (recommended 2.4.6 or 2.4.8)
- **PHP:** >= 8.1 (7.4 and 8.2 also supported)
- **MySQL:** >= 5.7 or MariaDB >= 10.3
- PHP with `openssl` support for signing/verification.

---

## How to install

```bash
cd <your Magento root>
git clone https://github.com/upcecconnect/magento-pgp.git
cp -R magento-pgp/app/code/Upc/EcommConnect app/code/Upc/
```

Then run Magento commands:

```bash
php bin/magento module:enable Upc_EcommConnect
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento cache:clean
```

---

## Alternative installation (without git)

If you don’t have git, you can download this repository as a ZIP archive and manually place the files in your Magento installation.

1. Click **`Code` → `Download ZIP`** on this repository’s GitHub page.
2. Unzip the archive.
3. Copy the contents of the folder:

    ```
    magento-pgp/app/code/Upc
    ```

   into the corresponding directory of your Magento project:

    ```
    your_magento_project/app/code/Upc
    ```

4. Then run the standard Magento upgrade commands:

    ```bash
    php bin/magento setup:upgrade
    php bin/magento setup:di:compile
    php bin/magento cache:flush
    ```
   
---

## Configuring the module

1. Go to **Admin → Stores → Configuration → Sales → Payment Methods → UPC e-Commerce Connect**.
2. Fill in:
   - **Merchant ID**
   - **Terminal ID**
   - **Payment Gateway Action URL** (example: `https://ecg.test.upc.ua` for test)
3. Set **Test Mode** if you’re on sandbox.
4. Enable **Pre-authorization** if you want initial hold on funds.
5. Set **Sort Order**.
6. Paste your **private keys** and **certificates** (from UPC) in the corresponding fields:
   - use full PEM format, including `-----BEGIN PRIVATE KEY-----` and `-----END PRIVATE KEY-----`
   - same for the certificates: `-----BEGIN CERTIFICATE-----` to `-----END CERTIFICATE-----`
7. For sandbox, enter the **test keys** in separate test fields or leave them empty if not applicable.
8. Provide the Callback URL to the Ukrainian Processing Center to enable online payment notifications (enter your domain) `https://example.com/ecommconnect/webhook/index`

---

## Capturing funds after Pre-authorization

- If **Pre-authorization** is enabled, order will be in `Awaiting Capture` status.
- Admin navigates to **Sales → Orders → Order View**, sees **Capture via UPC** form.
- Enter/verify amount, click **Capture**. Magento will send a server request to UPC and move order to `Processing` after confirmation.

---

## Official UPC documentation
![UPC Logo](https://ecconnect.upc.ua/public/images/newLogo.svg)
- [API Checkout (English)](https://docsecom.atlassian.net/wiki/spaces/DOCEN/pages/49971442/API+Checkout+by+the+payment+page)
