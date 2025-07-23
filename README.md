# External REST to Salesforce Contact Integration (Mule 4)

This MuleSoft application receives contact data via an HTTP POST request (external REST client) and creates a corresponding Contact record in Salesforce.

---

## 📌 Features

- Exposes a REST endpoint: `/create-contact`
- Accepts JSON payloads (POST)
- Transforms JSON to Salesforce Contact format
- Creates Contact in Salesforce using Salesforce Connector
- Responds with success or error JSON

---

## 📂 Project Structure

external-rest-to-salesforce/
├── mule-artifact.json        # Project metadata
├── src/
│   └── main/
│       └── mule/
│           └── flow.xml      # Main integration logic
├── README.md
└── pom.xml (optional)
📥 Sample Request
POST http://localhost:8081/create-contact
{
  "firstName": "Alice",
  "lastName": "Smith",
  "email": "alice.smith@example.com",
  "phone": "555-1234"
}

## ✅ Sample Response
{
  "status": "success",
  "message": "Contact created successfully",
  "salesforceResponse": [
    {
      "id": "003XXXXXXXXXXXXXXX",
      "success": true,
      "errors": []
    }
  ]
}

## 🔧 Configuration
Edit the Salesforce Connector in flow.xml:

<salesforce:config name="Salesforce_Config"
                   username="your-username@domain.com"
                   password="yourPasswordAndSecurityToken"
                   doc:name="Salesforce Configuration"/>
🔐 Tip: Use secure properties or Anypoint Secrets Manager for production deployments.

## 🚀 Running the App
Open in Anypoint Studio (Mule 4.3+).

Set port=8081 in listener if needed.

Deploy the application.

Use Postman or cURL to test:

curl -X POST http://localhost:8081/create-contact \
  -H "Content-Type: application/json" \
  -d '{"firstName":"John","lastName":"Doe","email":"john@example.com","phone":"1234567890"}'
