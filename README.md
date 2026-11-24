# qa-test
# QA Portfolio: CyberChair Store Testing

Manual and automated QA testing project for a demo e-commerce landing page (`buggy_shop.html`).

## Tech Stack & Tools
* **Manual Testing:** Chrome DevTools (Console, Elements, Mobile Device Emulation), Boundary Value Analysis (BVA), UI/Layout Testing.
* **Test Automation:** JavaScript, Node.js, Playwright.

## Bug Reports

### 1. Cart total concatenates prices as strings instead of adding numbers
* **Severity:** Critical
* **Environment:** Windows 11, Google Chrome
* **Steps to Reproduce:**
  1. Open `buggy_shop.html`.
  2. Click "Добавить в корзину" (Add to Cart) for the 15000 ₽ chair.
  3. Click "Добавить в корзину" (Add to Cart) for the 20000 ₽ chair.
* **Actual Result:** The total price displays `1500020000 ₽` (string concatenation).
* **Expected Result:** The total price displays the mathematical sum `35000 ₽`.

### 2. Uncaught TypeError when applying a promo code
* **Severity:** Major
* **Environment:** Windows 11, Google Chrome
* **Steps to Reproduce:**
  1. Enter `SALE10` into the promo code input field.
  2. Click the "Применить" (Apply) button.
* **Actual Result:** No discount is applied; Console throws `Uncaught TypeError: Cannot set properties of null (setting 'innerText')` inside `applyPromo()`.
* **Expected Result:** A 10% discount is applied to the total amount without console errors.

### 3. Lack of input validation allows negative product quantities
* **Severity:** Major
* **Environment:** Windows 11, Google Chrome
* **Steps to Reproduce:**
  1. Enter `-3` into the quantity ("Кол-во") field.
  2. Click "Оформить заказ" (Submit Order).
* **Actual Result:** The form submits successfully and displays a refund confirmation for `-3` items.
* **Expected Result:** Negative numbers and zero are blocked by input validation (minimum allowed value is `1`).

### 4. Promotional banner overlaps the submit button on mobile screens
* **Severity:** Blocker (UI/UX)
* **Environment:** Windows 11, Chrome DevTools (viewport width < 500px)
* **Steps to Reproduce:**
  1. Switch to mobile emulation mode (`width < 500px`).
  2. Scroll down to the checkout form.
* **Actual Result:** The fixed bottom promo banner (`z-index: 9999`) covers the "Оформить заказ" button, blocking checkout.
* **Expected Result:** The banner does not overlap interactive elements on mobile viewports.

## How to Run Automated Tests
```bash
npm install
npx playwright test
```

