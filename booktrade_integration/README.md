# BookTrade API Documentation

**Base URL:** `https://booktrade-backend-nine.vercel.app/api`

**Authentication:** Each request requires an API key passed in the headers as follows:

```json
Authorization: Token {{user_id}}
```

### Table of Contents
1. User Authentication
   - [Send Email OTP](#send-email-otp)
   - [Verify OTP](#verify-otp)
   - [Register User](#register-user)
   - [Login](#login)
   - [Reset Password](#reset-password)
   - [Verify Reset OTP](#verify-reset-otp)
2. Books
   - [Add Book](#add-book)
   - [List Books](#list-books)
   - [Get Book by ID](#get-book-by-id)
   - [Update Book](#update-book)
   - [Delete Book](#delete-book)
3. Exchange Requests
   - [Add Exchange Request](#add-exchange-request)
   - [Get User's Exchange Requests](#get-exchange-requests)

---

## User Authentication

### Send Email OTP

**Endpoint:** `/auth/sendEmailOtp`

**Method:** `POST`

**Description:** Initiates the registration process by sending an OTP to the user's email.

**Request Body:**
```json
{
    "email": "user@example.com"
}
```

**Example Request (cURL):**
```bash
curl -X POST {{root_url}}auth/sendEmailOtp \
     -H "Content-Type: application/json" \
     -d '{"email": "user@example.com"}'
```

---

### Verify OTP

**Endpoint:** `/auth/verifyEmailOtp`

**Method:** `POST`

**Description:** Verifies the OTP sent to the user's email.

**Request Body:**
```json
{
    "uuid": "user-uuid",
    "otp": "123456"
}
```

**Example Request (cURL):**
```bash
curl -X POST {{root_url}}auth/verifyEmailOtp \
     -H "Content-Type: application/json" \
     -d '{"uuid": "user-uuid", "otp": "123456"}'
```

---

### Register User

**Endpoint:** `/auth/registerUser`

**Method:** `POST`

**Description:** Completes the user registration process.

**Request Body:**
```json
{
    "uuid": "user-uuid",
    "username": "newuser",
    "full_name": "Full Name",
    "email": "user@example.com",
    "password": "password123",
    "reading_preferences": "fiction",
    "favorite_genres": "mystery,drama"
}
```

**Example Request (cURL):**
```bash
curl -X POST {{root_url}}auth/registerUser \
     -H "Content-Type: application/json" \
     -d '{...}'
```

---

## Books

### Add Book

**Endpoint:** `/books`

**Method:** `POST`

**Description:** Allows a user to add a new book with various attributes.

**Request Body (multipart/form-data):**
| Parameter          | Type       | Description                     |
|--------------------|------------|---------------------------------|
| title              | `text`     | Title of the book               |
| author             | `text`     | Author of the book              |
| genre              | `text`     | Genre of the book               |
| condition          | `text`     | Condition of the book           |
| availability_status| `text`     | Availability status             |
| latitude           | `text`     | Location latitude               |
| longitude          | `text`     | Location longitude              |
| image              | `file`     | Image file of the book          |

**Example Request (cURL):**
```bash
curl -X POST {{root_url}}books \
     -F "title=Moby Dick" \
     -F "author=Herman Melville" \
     -F "genre=adventure" \
     -F "condition=excellent" \
     -F "availability_status=true" \
     -F "latitude=12.955300" \
     -F "longitude=77.699400" \
     -F "image=@/path/to/image.jpg"
```

---

### List Books

**Endpoint:** `/books`

**Method:** `GET`

**Description:** Retrieves a list of all books.

**Example Request (cURL):**
```bash
curl -X GET {{root_url}}books
```

---

### Get Book by ID

**Endpoint:** `/books/{book_id}`

**Method:** `GET`

**Description:** Retrieves details of a specific book by its ID.

**Example Request (cURL):**
```bash
curl -X GET {{root_url}}books/54ba8bee-ea60-40f5-956c-67f5acace04c
```

---

### Update Book

**Endpoint:** `/books/{book_id}`

**Method:** `PATCH`

**Description:** Allows updating the details of a specific book.

**Request Body:**
```json
{
    "title": "Updated Book Title",
    "author": "Updated Author",
    "genre": "Updated Genre",
    "condition": "Updated Condition"
}
```

**Example Request (cURL):**
```bash
curl -X PATCH {{root_url}}books/54ba8bee-ea60-40f5-956c-67f5acace04c \
     -H "Content-Type: application/json" \
     -d '{"title": "Updated Book Title", "author": "Updated Author", "genre": "Updated Genre", "condition": "Updated Condition"}'
```

---

### Delete Book

**Endpoint:** `/books/{book_id}`

**Method:** `DELETE`

**Description:** Deletes a specific book by its ID.

**Example Request (cURL):**
```bash
curl -X DELETE {{root_url}}books/54ba8bee-ea60-40f5-956c-67f5acace04c
```

---

## Exchange Requests

### Add Exchange Request

**Endpoint:** `/exchange_request`

**Method:** `POST`

**Description:** Creates a new exchange request between users for book trading.

**Request Body:**
```json
{
    "acceptor": "acceptor-uuid",
    "initiator_book_id": "initiator-book-id",
    "acceptor_book_id": "acceptor-book-id",
    "delivery_method": "Courier",
    "exchange_duration": 3
}
```

**Example Request (cURL):**
```bash
curl -X POST {{root_url}}exchange_request \
     -H "Content-Type: application/json" \
     -d '{"acceptor": "acceptor-uuid", "initiator_book_id": "initiator-book-id", "acceptor_book_id": "acceptor-book-id", "delivery_method": "Courier", "exchange_duration": 3}'
```

---
