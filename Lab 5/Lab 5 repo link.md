# Lab 5: Static Code Analysis - Subscription Billing System

## Project repository

[PiyaB06/L5_63_subscription-billing](https://github.com/PiyaB06/L5_63_subscription-billing)

## Project overview

This lab applies static analysis to a small Python subscription-billing system. The program models common SaaS billing operations: starting subscriptions and free trials, applying coupons, calculating invoice totals and upgrade proration, retrying payments, issuing cancellation refunds, generating coupon codes, encrypting card numbers, validating signed webhooks, parsing XML, and rendering HTML invoices.

The aim was not only to make the code pass style checks. The lab used Pylint, Flake8, and Bandit to identify maintainability, correctness, and security concerns, then recorded the findings and updated the implementation.

## Work completed

### 1. Established a baseline and documented findings

The original analysis results recorded in the project were:

- **Pylint:** 4.43/10
- **Bandit:** 1 high-, 1 medium-, and 3 low-severity findings
- **Flake8:** 36 issues

The findings are recorded in the project's [`issues.md`](https://github.com/PiyaB06/L5_63_subscription-billing/blob/main/issues.md). They cover security concerns, potential runtime bugs, naming and documentation conventions, and formatting. The issue list also groups overlapping findings where a single correction addresses more than one tool's warning.

### 2. Addressed security findings

The billing implementation was updated to address the principal security issues identified during analysis:

- **Card encryption:** Replaced the older PyCrypto-style AES import with AES-GCM from the maintained `cryptography` package. A fresh random nonce is used for each encryption, so encrypting the same card number twice produces different ciphertext.
- **Secret handling:** The webhook signing secret and card-encryption key are read from the `WEBHOOK_SECRET` and `CARD_KEY` environment variables rather than embedded as literal values in the source. The program raises an error if a required value is missing.
- **Coupon generation:** Uses Python's `secrets` module to choose characters for generated coupon codes instead of the non-cryptographic `random` module.
- **HTML output:** Escapes the invoice customer name and amount before inserting them into HTML, preventing user-controlled text from being interpreted as markup.
- **Amount validation:** Rejects negative invoice amounts with an explicit `ValueError`, rather than relying on an `assert` that can be disabled when Python runs in optimized mode.
- **Webhook verification:** Compares HMAC signatures with `hmac.compare_digest`, which is designed for safer comparison of secret-derived values.

### 3. Improved code quality and style

The code was also cleaned up to resolve the recorded Pylint and Flake8 findings. This included using snake_case function names, adding module and function docstrings, splitting imports onto separate lines, removing or correcting reported style issues, and wrapping overlong lines. The refund function was simplified to avoid a return in a `finally` block and an uninitialized return value.

### 4. Saved before-and-after reports

The repository contains Pylint, Bandit, and Flake8 report files in the **Before Fix Reports** and **After Fix Reports** folders. The final static summary recorded in the project reports:

| Tool | Before | After |
| ----- | ------ | ----- |
| Pylint | 4.43/10 | 10.00/10 |
| Bandit | 1 high, 1 medium, 3 low | 0 high, 0 medium, 0 low |
| Flake8 | 36 issues | 0 issues |

The analysis reports show that the documented static-analysis targets were met. They are static-analysis results; they do not by themselves demonstrate that every billing calculation behaves correctly for all inputs.

## Remaining behavior to review

The demo output also exposes logic that should be revisited separately from the clean static-analysis results:

- The retry loop reports **4 attempts** even though its message says the maximum is 3. Its loop condition currently allows an extra attempt.
- The cancellation refund demo reports a refund of **999** after 25 of 30 days have been used. The current refund function returns the full plan price instead of calculating a partial refund.

These behaviors are worth correcting and testing before treating the billing calculations as production-ready.

## Reflection

This lab demonstrates that static-analysis tools can find more than formatting problems: they can identify risky security patterns, possible runtime defects, and maintainability issues. It also shows why tool output should be combined with reading and running the program. A clean Pylint, Bandit, or Flake8 report is useful evidence about the checks those tools perform, but it does not guarantee that business rules such as retry limits and refund calculations are correct.
