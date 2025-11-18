# 🛡️ Parameter Tampering and Business Logic Flaw Exploitation on OWASP Juice Shop

This repository contains the report and findings from a security analysis project focused on exploiting vulnerabilities in the **OWASP Juice Shop** web application. The project specifically targeted flaws introduced by **Parameter Tampering** and **weak Business Logic**.

## 📝 Project Overview

The objective was to analyze and exploit critical vulnerabilities in an intentionally insecure e-commerce simulation (OWASP Juice Shop) to confirm the severe risks associated with a lack of server-side validation and proper authorization.

The final output confirms that the application critically fails to implement server-side validation and proper authorization across multiple API endpoints, leading to severe financial, privacy, and integrity risks. Effective mitigation requires adopting a "Never Trust Client Data" approach.

## 🎯 Exploited Challenges (Proof of Concepts)

Five core challenges were successfully exploited, demonstrating various types of parameter manipulation:


**View Basket** - Insecure Direct Object Reference (IDOR) / Broken Access Control - Manipulated the `basket ID` parameter in the request URL (`/rest/basket/6` to `/rest/basket/3`) to access another user's basket details.

**Deluxe Fraud** - Weak Authorization / Price Manipulation - Modified the request payload parameter `paymentMode` from `wallet` to an empty string or `"paid"` in the POST request to obtain a Deluxe Membership without proper payment.

**Forged Feedback** - Unauthorized Action / Broken Access Control - Manipulated the `UserId` parameter in the feedback submission request to post feedback under another user's name.

**Payback Time** - Transaction Logic Flaw / Negative Pricing - Exploited a business logic flaw by modifying the **quantity** parameter to a negative value (e.g., `-100`), resulting in a credit to the account rather than a charge (financial gain).

**Product Tampering** - Unauthorized Data Update - Used a PUT request to inject new HTML content into the product description, changing the hyperlink's `href` attribute.

## ⚙️ Technology and Environment

**Target Application** - OWASP Juice Shop (Intentionally Insecure E-Commerce Simulation)

**Database** - MySQL

**Frameworks** - Angular, Zone.js

**Programming** - TypeScript, Node.js, JavaScript, PHP

**Testing Environment** - Docker Container on Ubuntu Live Server 

**Primary Tool** - Burp Suite (used for intercepting and manipulating HTTP requests)

## 🛠️ General Remediation Recommendations

To mitigate the vulnerabilities demonstrated in this project, applications should adhere to the following principles:

**Never Trust Client Data:** All parameters affecting access control, transactions, and application state must be strictly validated and managed exclusively by the server.

**Server-Side Validation:** Implement rigorous server-side validation for all inputs, especially those related to financial transactions (preventing negative values).

**Robust Access Control (RBAC/ABAC):** Use Role-Based Access Control (RBAC) or Attribute-Based Access Control (ABAC) to ensure a user is authorized for the requested data and action, based on their session, not on user-supplied IDs.

**Secure Payment Logic:** Implement robust checks on the server-side to verify payment details are correct and complete before processing transactions.

**Sanitize All Inputs:** Properly sanitize and validate all user inputs, particularly in fields that allow HTML content (like product descriptions or feedback).
---
