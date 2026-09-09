#  Justification for Architectural Selection

**Architecture Selection Statement:** I chose **Microservices Architecture** for the **Digital Gift Card & Loyalty Point Exchange System**.

* *Reasons:*
  1. **Decoupled Partner API Integrations:** External merchant APIs vary in latency, availability, and response times. Isolating partner integrations inside a dedicated *Partner Adapter Service* prevents external slow downs or downtime from stalling the primary order processing and wallet redemption flows.
  2. **Independent Domain Scalability:** Components like the *Dynamic Conversion Engine* and *Voucher Management* experience intense transaction spikes during promotional events. A microservices architecture allows these high throughput services to scale horizontally on-demand without duplicating the entire backend codebase.

* **Security Advantage:**
  * **Isolated Infection Radius & Encapsulated Fraud Control:** Sensitive security functions ~ such as cryptographic checksum generation and anti fraud voucher locking ~ are isolated within the dedicated *Voucher & Fraud Management Component*. Securing this single component behind strict internal access controls and isolated memory boundaries reduces the attack surface, preventing compromised partner APIs or UI endpoints from altering checksum logic or forging voucher codes.

* **Performance Benefit:**
  * **Parallel Execution & Unblocked Latency (<250 ms Target):** By separating long-running balance syncing from order generation, the system can perform asynchronous, parallel API calls to calculate dynamic conversion rates and lock vouchers concurrently. This decentralized processing ensures redemption transactions routinely meet the strict **<250 ms target** without waiting on synchronous monolithic database locks.

---

# Component Identification

## 1. System Components
* **Order Manager Component** 
  * Coordinates transactions across wallet services, orchestrates gift card voucher issuance, and handles checkout sequences.
* **Payment Service Component**
  * Processes monetary payment gateways, verifies billing information, and updates universal exchange credit balances.
* **Partner Adapter Service Component** 
  * Interacts with external Merchant Partner APIs to fetch point balances, authorize deductions, and validate account credentials.
* **Dynamic Conversion Engine Component** 
  * Evaluates real time exchange rates between merchant loyalty points and universal exchange tokens based on dynamic demand and business rules.
* **Voucher & Fraud Management Component** 
  * Generates single use digital voucher codes with cryptographic checksums and enforces temporary atomic locks to prevent double-spending.

## 2. Component Interfaces
* **`IOrderProcessing`** *(Provided by Order Manager)*
  * Handles checkout requests, initiates gift card issuance, and updates purchase status.
* **`IPaymentGateway`** *(Provided by Payment Service)*
  * Processes payments, verifies billing, and executes balance adjustments.
* **`IPartnerSync`** *(Provided by Partner Adapter Service)*
  * Fetches real time point balances and executes external merchant point debits via HTTPS REST APIs.
* **`IConversionRate`** *(Provided by Dynamic Conversion Engine)*
  * Evaluates and returns real time point to token conversion values on demand.
* **`IVoucherLock`** *(Provided by Voucher & Fraud Management Component)*
  * Creates single use codes with cryptographic checksums and manages atomic locking during redemption.

---

