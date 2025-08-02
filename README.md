# CST8917 Lab 4: Real-Time Trip Event Analysis

## 📘 Overview

This project demonstrates a real-time trip monitoring solution for a taxi dispatch system. It uses **Azure Event Hub**, **Azure Function**, **Logic Apps**, and **Microsoft Teams Adaptive Cards** to analyze taxi trip data and notify operations teams of any anomalies.

---

## 🧱 Architecture and Workflow

### 🔄 Flow Summary:
1. **Event Hub** receives simulated taxi trip JSON events.
2. **Logic App** triggers on Event Hub batches.
3. **HTTP action** calls an Azure Function to analyze each trip.
4. **For Each loop** processes trip results.
5. **Condition check** identifies if a trip is "interesting".
6. **Microsoft Teams** receives adaptive cards:
   - ✅ Normal trip
   - 🚨 Interesting trip
   - ⚠️ Suspicious vendor activity

---

## 💻 Azure Function Logic

The Azure Function evaluates each trip's metadata and flags based on:
- Long trip (>10 miles)
- Group ride (>4 passengers)
- Cash payment (paymentType == "2")
- Suspicious activity (cash + very short trip)

### 🔍 Output Format:
```json
{
  "vendorID": "V123",
  "tripDistance": 0.9,
  "passengerCount": 5,
  "paymentType": "2",
  "insights": ["GroupRide", "CashPayment", "SuspiciousVendorActivity"],
  "isInteresting": true,
  "summary": "3 flags: GroupRide, CashPayment, SuspiciousVendorActivity"
}
```

---

## 🧪 Testing Workflow

1. Events sent to **Event Hub** via CLI or Python.
2. **Logic App** triggers on event batch.
3. Azure Function analyzes trips and returns list of trip objects.
4. **For each** trip:
   - If `isInteresting == true` → post attention card to Teams.
   - Else → post success card.

---

## 🧠 Lessons Learned

- Event Hub batch triggering integrates smoothly with Logic Apps.
- Azure Function's flexibility allows rich conditional logic.
- Adaptive Cards make alerts actionable and human-readable in Teams.

---

## 📸 Screenshots & Flowchart

- ![Logic App Flow](logic-app-flow.png) *(Add your screenshot here)*

---

## 🔗 Demo Video

[![YouTube Demo](https://img.shields.io/badge/Demo-YouTube-red)](https://www.youtube.com/watch?v=your_demo_link_here)

---

## 📂 Project Contents

| File/Folder | Description |
|-------------|-------------|
| `trip-analyzer-function.py` | Azure Function code |
| `logic-app-workflow.json` | Exported Logic App definition |
| `README.md` | This documentation |
| `trip-samples/` | Sample JSON payloads |
| `screenshots/` | Workflow images |

---

## ✅ Submission Checklist

- [x] Logic App JSON exported
- [x] Function app deployed and tested
- [x] Demo video created and linked
- [x] GitHub repository public and accessible

---

## 🕒 Deadline: Friday, August 1, 2025

Prepared by: **Meet Prajapati**

