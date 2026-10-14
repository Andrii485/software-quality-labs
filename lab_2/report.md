# Лабораторна робота №2

## Проєктування тестів. Checklist, Test Cases та Decision Table

**Виконав:** Бондаренко Андрій\
**Група:** 6.1213-пі-2\
**Дата виконання:** 14.10.2026

## Test Conditions

– TCND-01 - успішна авторізація валідного користувача;\
– TCND-02 - авторізація з неправильним Username;\
– TCND-03 - авторизація з неправильним Password;\
– TCND-04 - авторизація з порожнім Username;\
– TCND-05 - авторизація з порожнім Password;\
– TCND-06 - авторизація заблокованого користувача.


## Checklist

– [ ] Успішна авторизація з валідними даними.\
– [ ] Відмова в аторизації з неправильним Username.\
– [ ] Відмова в авторизації з неправильним Password.\
– [ ] Перевірка порожнього Username.\
– [ ] Перевірка порожнього Password.\
– [ ] Відмова в авторизації заблокованого користувача.


### TC-LOGIN-01 – Успішна авторизація standard_user

**Type:** Positive

**Preconditions:**
– Сторінка Login (https://www.saucedemo.com) відкрита\
– Користувач не авторизований.

**Test Data:**\
– Username: standsrd_user\
– Password: secret_sauce

**Steps:**
1. У поле Username ввести standard_user.
2. У поле "Password" ввести secret_sauce.
3. Натиснути кнопку "Login".

**Expected Result:** Після введення `Username` і правильного пароля та натискання Login користувач успішно авторизується і переходить на сторінку Products (`/inventory.html`).

**Actual Result:** Після введення `Username` і правильного пароля та натискання Login відкрилася сторінка Products (`/inventory.html`).

**Result:** Pass


### TC-LOGIN-02 – Авторизація з неправильним Password

**Type:** Negative

**Preconditions:**
- Відкрита сторінка Login SauceDemo (https://www.saucedemo.com/).
- Користувач не авторизований.

**Test Data:**
- Username: standard_user
- Password: wrong_password

**Steps:**
1. У поле Username ввести standard_user.
2. У поле Password ввести wrong_password.
3. Натиснути кнопку Login.

**Expected Result:**
Після введення standard_user і неправильного пароля та натискання Login авторизація не виконується, користувач залишається на сторінці Login, а система показує повідомлення "Epic sadface: Username and password do not match any user in this service".

**Actual Result:**
Після введення standard_user і неправильного пароля та натискання Login авторизація не виконана, користувач залишився на сторінці Login, з'явилося повідомлення "Epic sadface: Username and password do not match any user in this service".

**Result:** Pass


### TC-LOGIN-03 – Авторизація заблокованого користувача.

**Type:** Negative

**Preconditions:**
- Відкрита сторінка Login SauceDemo (https://www.saucedemo.com/).
- Користувач не авторизований.

**Test Data:**
- Username: locked_out_user
- Password: secret_sauce

**Steps:**
1. У поле Username ввести locked_out_user.
2. У поле Password ввести secret_sauce.
3. Натиснути кнопку Login.

**Expected Result:**
Після введення locked_out_user і правильного пароля та натискання Login вхід до застосунку блокується, відкривається не сторінка Products, а залишається форма входу з повідомленням "Epic sadface: Sorry, this user has been locked out".

**Actual Result:**
Після введення locked_out_user і правильного пароля та натискання Login вхід до застосунку не відбувся, сторінка Products не відкрилася, на формі входу з'явилося повідомлення "Epic sadface: Sorry, this user has been locked out.".

**Result:** Pass


## Decision Table

| Умова / Дія | R1 | R2 | R3 | R4 | R5 |
|-------------|----|----|----|----|----|
| Username входить до списку допустимих? | T | T | F | T | F |
| Password правильний? | T | T | T | F | F |
| Користувач заблокований? | F | T | - | - | - |
| **A1: Products (/inventory.html)** | **X** | | | | |
| **A2: Locked message** | | **X** | | | |
| **A3: Invalid credentials message** | | | **X** | **X** | **X** |

Правила, що залишилися без окремого Test Case: R3. invalid Username + valid Password, R5. invalid Username + invalid Password

## Результати виконання

| Test Case | Type | Result |
| :--- | :--- | :--- |
| TC-LOGIN-01 | Positive | Pass |
| TC-LOGIN-02 | Negative | Pass |
| TC-LOGIN-03 | Negative | Pass |

## Висновок

Під час лабораторної роботи було відпрацьовано підхід до проєктування тестів від вимог: на основі Test Basis визначено Test Conditions, складено checklist і описано три детальні test cases з тестовими даними, кроками та очікуваним результатом. Розглянуто різницю між позитивною та негативною перевіркою на прикладі входу з правильними даними, хибним паролем і заблокованим користувачем. Decision Table дозволила систематизувати комбінації Username, Password і стану блокування та показала, що правила R3 і R5 не покриті окремими test cases. Усі три test cases виконано в SauceDemo, порівняно Expected та Actual Result, результат кожного - Pass.