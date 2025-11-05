# 🐞 EnrichMinion Bug Report

This document lists defects found during manual testing of the **EnrichMinion** web app  
(https://enrichminion.vercel.app).

---

## 📋 Bug Summary

| Bug ID | Title | Severity | Module | Root Cause | Status |
|:-------|:-------|:----------|:---------|:-------------|:---------|
| B-001 | Signup form allows empty fields submission | High | Signup | Frontend (validation missing) | Open |
| B-002 | Invalid email format not blocked during signup | Medium | Signup | Frontend | Open |
| B-003 | Login does not show proper error for wrong credentials | High | Login | Backend (generic error message) | Open |
| B-004 | Logout sometimes does not clear session until page refresh | Medium | Login/Logout | Frontend (state handling) | Open |
| B-005 | File upload accepts non-CSV formats | High | Enrichment | Frontend | Open |
| B-006 | Enrichment API returns 500 error on empty entity array | High | Enrichment | Backend | Open |
| B-007 | Verification module returns inconsistent message text for invalid emails | Medium | Verification | Backend | Open |
| B-008 | UI misalignment on smaller screens | Low | Global UI | Frontend (CSS) | Open |

---

## 🧾 Detailed Bug Descriptions

### **Bug ID:** B-001
**Title:** Signup form allows empty fields submission  
**Severity:** High  
**Steps to Reproduce:**
1. Navigate to the signup page  
2. Leave all fields blank  
3. Click “Sign Up”  
**Expected Result:** Validation messages should prevent submission  
**Actual Result:** Form submits request to server (visible in network tab)  
**Evidence:** Screenshot `signup_empty_submit.png`  
**Root Cause:** Missing required field validation on frontend input elements  
**Component:** Frontend (React validation)  

---

### **Bug ID:** B-002
**Title:** Invalid email format not blocked during signup  
**Severity:** Medium  
**Steps to Reproduce:**
1. Enter `user@invalid` in the email field  
2. Fill other fields correctly  
3. Submit  
**Expected Result:** Client-side error “Enter a valid email”  
**Actual Result:** API called; backend rejects with 400 error  
**Root Cause:** Missing regex validation for email input  
**Component:** Frontend  

---

### **Bug ID:** B-003
**Title:** Login does not show proper error for wrong credentials  
**Severity:** High  
**Steps to Reproduce:**
1. Enter incorrect password for valid email  
2. Submit  
**Expected Result:** User sees “Invalid credentials” or “Wrong password” message  
**Actual Result:** Toast shows generic “Something went wrong”  
**Evidence:** Screenshot `login_error_msg.png`  
**Root Cause:** Backend sends generic 400 without descriptive message  
**Component:** Backend  

---

### **Bug ID:** B-004
**Title:** Logout does not clear session until page refresh  
**Severity:** Medium  
**Steps to Reproduce:**
1. Login  
2. Click Logout  
3. Press Back button  
**Expected Result:** User redirected to login page  
**Actual Result:** Dashboard still accessible until manual refresh  
**Root Cause:** Auth token not cleared from local storage immediately  
**Component:** Frontend  

---

### **Bug ID:** B-005
**Title:** File upload accepts non-CSV formats  
**Severity:** High  
**Steps to Reproduce:**
1. Go to Enrichment page  
2. Upload `.txt` file  
3. Observe upload success message  
**Expected Result:** Should restrict upload to `.csv` only  
**Actual Result:** `.txt` file accepted (processing fails silently)  
**Root Cause:** Missing file type validation in client file input  
**Component:** Frontend  

---

### **Bug ID:** B-006
**Title:** Enrichment API returns 500 error on empty entity array  
**Severity:** High  
**Steps to Reproduce:**
1. Call `/api/enrich` with empty array `[]`  
**Expected Result:** 400 Bad Request with validation message  
**Actual Result:** 500 Internal Server Error  
**Evidence:** Network tab screenshot  
**Root Cause:** Backend null-pointer error when mapping entities  
**Component:** Backend  

---

### **Bug ID:** B-007
**Title:** Verification module returns inconsistent error message  
**Severity:** Medium  
**Steps to Reproduce:**
1. Verify invalid email like `abc@xyz`  
**Expected Result:** “Invalid email address” message consistently shown  
**Actual Result:** Sometimes shows “Verification failed”  
**Root Cause:** Inconsistent backend error response mapping  
**Component:** Backend  

---

### **Bug ID:** B-008
**Title:** UI misalignment on smaller screens  
**Severity:** Low  
**Steps to Reproduce:**
1. Open Enrichment dashboard on 320px width screen (mobile view)  
**Expected Result:** UI adapts to viewport width  
**Actual Result:** Table columns overflow screen; buttons overlap  
**Evidence:** Screenshot `mobile_ui_issue.png`  
**Root Cause:** Missing responsive CSS classes  
**Component:** Frontend  

---

## ✅ Summary

| Category | Count |
|-----------|-------|
| Total Bugs | 8 |
| Frontend Issues | 5 |
| Backend Issues | 3 |

---

**Tested By:** QA Engineer  
**Date:** 05-Nov-2025  
**Environment:** Chrome 141.0, Windows 10, Live URL: https://enrichminion.vercel.app
