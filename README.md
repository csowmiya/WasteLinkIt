#  WasteLinkIt

> Smart Plastic Waste Prediction & Trading Platform  
> Built using **Flask + HTML + MongoDB + LSTM**

---

##  Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Architecture](#architecture)
- [Screenshots](#screenshots)
- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

---

##  Introduction

**WasteLinkIt** is a full-stack web platform that helps predict, pre-book, and manage plastic waste in Tamil Nadu using machine learning.  
It enables producers to list available waste and buyers to pre-book or instantly purchase based on **LSTM-powered predictions**.

---

##  Features

-  **ML Predictions**: Predict monthly plastic waste (PET, HDPE, PVC, LDPE, PP, PS) per district
-  **Producer Dashboard**: Add estimates, confirm waste, update logistics
-  **Buyer Dashboard**: Pre-book, instant book, get alerts, track bookings
-  **Email Notifications**: Auto alerts for confirmations and shortages
-  **Unified Booking System**: Both pre-bookings and instant bookings in one place
-  **Chart View**: Line charts and data tables for district & plastic-type filtering

---

##  Architecture

![Image](https://github.com/user-attachments/assets/e4e6e067-2e28-4f8f-b133-2ad6bfd9b2d1)

---

##  Screenshots

HOME PAGE
![Image](https://github.com/user-attachments/assets/29501641-e903-43b9-8f5e-b7b981c78cdb)

PREDICTION GRAPH
![Image](https://github.com/user-attachments/assets/4841c8b5-3a25-445c-a07a-f7e200fa10b4)

PREDICTIONS
![Image](https://github.com/user-attachments/assets/8b571d52-e2a1-42c6-a076-e03c2310ff5e)

SIGN UP PAGE
![Image](https://github.com/user-attachments/assets/2074034e-08e5-4f7a-93aa-7984aa7f543f)

LOGIN PAGE
![Image](https://github.com/user-attachments/assets/ce3c6b78-f82f-42f6-b508-cbc8517b1a93)

PRODUCER DASHBOARD PAGE
![Image](https://github.com/user-attachments/assets/156b5fcf-2a8b-474f-8606-f20d0e994c85)

ESTIMATE WASTE PAGE
![Image](https://github.com/user-attachments/assets/9099d12e-3242-4dda-9157-2d5ab60c0d75)

CONFIRMATION PAGE
![Image](https://github.com/user-attachments/assets/d43e6fd3-01f4-4e0f-ad21-d4de21612bb2)

PRODUCER HISTORY PAGE
![Image](https://github.com/user-attachments/assets/44f756be-018d-4cd7-b852-8616c267bff0)

BUYER DASHBOARD PAGE
![Image](https://github.com/user-attachments/assets/4d0cd8c7-6f31-47a4-91fe-f1c862bec466)

INSTANT BOOKING PAGE
![Image](https://github.com/user-attachments/assets/ef928c58-43f0-4801-b4cc-5f4e62dfc330)

BUYER HISTORY PAGE
![Image](https://github.com/user-attachments/assets/d3fda05b-9074-4526-b05a-5b0b6724ef91)

PRE BOOKING PAGE
![Image](https://github.com/user-attachments/assets/68a7467c-bc74-42eb-bfec-17ffd098a31c)

FILL LOGISTICS PAGE
![Image](https://github.com/user-attachments/assets/cf2371fc-1a95-4aa3-a33f-792525e1bb86)

TRACK LOGISTICS PAGE
![Image](https://github.com/user-attachments/assets/51fa19bf-e3bc-4600-ab2d-8c6c3405ec59)

---

## Installation
### Prerequisites
- Make sure the following tools are installed:

- Python 3.8+

- MongoDB (local or MongoDB Atlas)

- Git

- Web Browser (Chrome, Firefox, etc.)

### Steps

#### 1. Clone the Repository

```bash
git clone https://github.com/csowmiya/WasteLinkIt.git
```
#### 2. Navigate to the Project Directory

```bash
cd WasteLinkIt
```
### 3. Install Dependencies

```bash
pip install -r requirements.txt
```
### 4.Run the Application
``bash
python app.py
``
### 5.Access the Tool: Open a web browser and navigate to http://localhost:5000.

---

## Usage

This section explains how different users interact with the platform and how the plastic waste prediction and trading flow works.

---

### Producer Flow

1. Open the frontend (`index.html`) in a browser.
2. Go to the **Producer Dashboard**.
3. Enter estimated waste quantities by plastic type and district.
4. Later, confirm the actual waste available.
5. View waste history and manage logistics.

---

### Buyer Flow

1. Open the frontend and access the **Buyer Dashboard**.
2. View upcoming predictions for the next 6 months.
3. Choose to:
   - **Pre-book** plastic waste based on forecasted availability.
   - **Instant book** available waste.
4. Receive **email notifications** when:
   - Booking is confirmed.
   - There’s a shortage or mismatch.

---

### Prediction Flow (LSTM)

- Predictions are generated using an LSTM model for each district and plastic type.
- The backend provides this data through `/api/predictions`.
- The frontend displays the predictions in:
  - Interactive line charts
  - Searchable, filterable tables

---

### Data Auto-Update Logic

- Once per month (can be automated), new data is added and predictions are recalculated.
- System forecasts for the **next 6 months** based on latest inputs.

---

### System Overview

- All actions (prebooking, confirmation, instant booking, logistics tracking) are connected to MongoDB.
- A **unified `bookings` collection** is used for easier tracking and dashboard updates.

---

## API Endpoints

---

### Authentication

`POST /login`  
Authenticate user and start a session (producer or buyer)

`GET /logout`  
Logout user and clear the session

---

### Prediction

`GET /api/predictions`  
Get plastic waste predictions by district and plastic type

---

### Producer APIs

`POST /api/estimated-waste`  
Submit estimated waste by plastic type and district

`POST /api/confirm-waste`  
Confirm actual waste available for the current month

`GET /api/producer/history`  
View producer’s waste update history

---

### Buyer APIs

`POST /api/prebook`  
Pre-book plastic waste based on prediction

`POST /api/instant-book`  
Instantly book currently available plastic waste

`GET /api/buyer/history`  
View buyer’s past booking history

---

### Notifications

`POST /api/send-email`  
Send email alert to buyer (for confirmations or shortages)

---

### Example Request

`POST /api/prebook`  
Host: `localhost:5000`  
Content-Type: `application/json`

```json
{
  "buyer_id": "buyer123",
  "district": "Coimbatore",
  "plastic_type": "PET",
  "quantity": 50
}
```
### Example Response

```json
{
  "status": "success",
  "message": "Pre-booking confirmed",
  "booking_id": "64f8a12bc9e2de00123abc45"
}
```
--- 

## Testing

---

### Unit Testing

Tests individual components to ensure they function correctly in isolation.

- Validate ML prediction output using sample inputs
- Test booking logic (pre-book and instant book)
- Test email notification triggers
- Verify session-based login/logout mechanisms

---

### Integration Testing

Verifies the integration between different modules.

- Test frontend → backend API connection using `fetch()`
- Test booking flows between buyers and producers
- Test MongoDB read/write operations for waste and booking data

---

### Running Tests

Use **Postman** to test and validate backend APIs.

- Import the provided Postman collection (if available)
- Run test cases and verify JSON responses

```bash
newman run WasteLinkIt.postman_collection.json -r html,cli
```
---

## License

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.

---

## Contact

For any questions, feedback, or support, feel free to reach out:

**Sowmiya C.**  
 Email: sowmi7810@gmail.com  
 GitHub: [csowmiya](https://github.com/csowmiya)

---


