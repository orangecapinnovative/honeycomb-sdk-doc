# HoneyComb API Body Encryption Guide

This guide explains how to encrypt JSON data using **AES-GCM-256** before sending it to the HoneyComb API.

## How the encryption works
1. The function receives **API Key** and a **JSON data**.
2. It will generate a hash (SHA-256) of API Key into 256-bit key.
3. Generate a **12-byte IV (Initialization Vector)**.
4. Encrypt the **JSON string** using **AES-256-GCM**.
5. Extract the **authentication tag**.
6. Encode the **encrypted data, IV, and authentication tag** in Base64.

## Node.js (TypeScript) Example

```ts
import crypto from "crypto";

// AES GCM 256 encrypt function
const encrypt = (jsonData: object, apiKey: string) => {
  const secretKey = crypto.createHash('sha256').update(apiKey).digest();
  const iv = crypto.randomBytes(12);
  const cipher = crypto.createCipheriv("aes-256-gcm", secretKey, iv);

  const jsonString = JSON.stringify(jsonData);

  // Encrypt thr data then encode it into base64
  let encryptedData = cipher.update(jsonString, "utf8", "base64");
  encryptedData += cipher.final("base64");

  // Get authentication tag
  const authTag = cipher.getAuthTag();

  return {
    encodedData: encryptedData, // already in base64
    authTag: authTag.toString("base64"),
    iv: iv.toString("base64"),
  };
};

// Example usage:
const apiKey = "PASTE_YOUR_API_KEY_HERE"; // Replace with actual API Key
const data = {
  event_name: "purchased",
  reference_number: "TX202501A01",
  total_price: 3950.5,
  items: [
    {
      name: "Hotel Bangkok Stay",
      quantity: 1,
      sku: "hotel_group_001",
      price: 3950.5
    },
  ],
};

try {
  const encrypted = encrypt(data, apiKey);
  console.log(encrypted);
} catch (error) {
  console.error("Encryption Error:", error.message);
}
```

Using the encryption function will get you **encoded data**, **iv**, and **authTag** which are required to send to the HoneyComb API.