# API Documentation

Base URL: `https://key.getcidapi.com`

## Endpoints

### 1. `/api/ocr` (POST)
**Description:**
Extract text and detect IID from an uploaded image.

**Headers:**
- `Content-Type: application/octet-stream`

**Query Parameters:**
- `api_key` (required): API key to authenticate the request.

**Body:**
- Raw image data.

**Responses:**
- **200:**
  ```json
  {
    "status": "success",
    "result": "<iid_detected>"
  }
  ```
- **400:** Missing API key or invalid/malformed data.
- **403:** Invalid API key.
- **500:** Internal server error.

---

### 2. `/api/get_balance` (GET)
**Description:**
Retrieve the current balance of the user.

**Query Parameters:**
- `api_key` (required): API key to authenticate the request.

**Responses:**
- **200:**
  ```json
  {
    "status": "balance",
    "result": <balance_value>
  }
  ```
- **400:** Missing API key.
- **403:** Invalid API key.
- **402:** Insufficient balance or blocked API key.
- **500:** Internal server error.

---

### 3. `/api/get_cid` (GET)
**Description:**
Check CID using the provided IID.

**Query Parameters:**
- `api_key` (required): API key to authenticate the request.
- `iid` (required): IID to be checked.
- `just_check` (optional): Set to `0` by default.

**Responses:**
- **200:**
  ```json
  {
    "status": "cid",
    "result": "<cid_result>",
    "iid": "<provided_iid>"
  }
  ```
- **400:** Invalid or missing parameters.
- **403:** Invalid API key.
- **402:** Insufficient balance or blocked API key.
- **503:** Service unavailable due to external issues.
- **500:** Internal server error.

---

### 4. `/api/keys_check` (GET)
**Description:**
Check validity of a list of keys.

**Query Parameters:**
- `api_key` (required): API key to authenticate the request.
- `keys` (required): \r\n seperated list of keys to validate.

**Responses:**
- **200:**
  ```json
  {
    "status": "keys",
    "result": {
      "valid_keys": [...],
      "invalid_keys": [...]
    }
  }
  ```
- **400:** Missing API key.
- **403:** Invalid API key.
- **402:** Blocked API key.
- **500:** Internal server error.

---

## Error Handlers

### 1. 404 Not Found
**Response:**
```json
{
  "status": "error",
  "error": "not_found"
}
```

### 2. 500 Internal Server Error
**Response:**
```json
{
  "status": "error",
  "error": "Something went wrong on our end!"
}
```

## Authentication
- Use the `api_key` query parameter in each request to authenticate.
- Invalid or missing API keys will result in a `403` response.

## Notes
- Ensure sufficient balance for API operations. Insufficient balance results in a `402` error.
- The `/api/get_cid` endpoint may become temporarily unavailable due to external dependencies.
