# API Testing Best Practices

REST API testing strategies from 14+ years of enterprise QA experience,
including Oracle Philippines (RGBU) and Vlocity (acquired by Salesforce).

---

## Core API Test Checklist

### ✅ Status Code Validation
- 200 OK — successful GET requests
- 201 Created — successful POST requests
- 400 Bad Request — invalid input data
- 401 Unauthorized — missing/invalid token
- 404 Not Found — resource doesn't exist
- 500 Internal Server Error — server-side failures

### ✅ Response Payload Validation
- Verify all required fields are present
- Check correct data types (string, integer, boolean)
- Validate nested JSON objects and arrays
- Confirm no sensitive data is exposed (passwords, tokens)

### ✅ Authentication Testing
- Valid token → should return 200
- Expired token → should return 401
- Missing token → should return 401
- Invalid token format → should return 400

### ✅ Data Persistence Check
- After POST/PUT → query the database to confirm data was saved correctly
- Verify the response body matches what was stored in the DB

---

## Sample Postman Test Script
```javascript
// Validate status code
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

// Validate response has required fields
pm.test("Response has required fields", function () {
    const json = pm.response.json();
    pm.expect(json).to.have.property("order_id");
    pm.expect(json).to.have.property("status");
    pm.expect(json).to.have.property("total_amount");
});

// Validate data types
pm.test("Total amount is a number", function () {
    const json = pm.response.json();
    pm.expect(json.total_amount).to.be.a("number");
    pm.expect(json.total_amount).to.be.above(0);
});
```

---

## Tools Used
- Postman, Newman (CLI runner)
- GitLab CI / Jenkins for automated API test pipelines
- REST Assured, SoapUI

## Author
Anthony Retardo — Senior QA Engineer | Oracle Philippines (RGBU)  
[LinkedIn](https://www.linkedin.com/in/anthonypretardo/)
