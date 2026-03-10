# 📝 Printing Quotes API

A RESTful API built with **Express.js** for managing a collection of quotes. It uses `json-server` as a lightweight backend data store and includes input validation via **Joi**.

---

## 🚀 Getting Started

### Prerequisites

- Node.js (v18+)
- npm

### Installation

```bash
npm install
```

### Running the Server

Start `json-server` on port `3000` (required as the data layer):

```bash
npx json-server --watch db.json --port 3000
```

Then start the Express API on port `5000`:

```bash
node index.js
```

The API will be available at: `http://localhost:5000`

---

## 📦 Dependencies

| Package   | Purpose                       |
| --------- | ----------------------------- |
| `express` | Web framework                 |
| `cors`    | Cross-origin resource sharing |
| `joi`     | Request body validation       |

---

## 🔗 Base URL

```
http://localhost:5000
```

---

## 📋 Endpoints

### `GET /`

Health check — confirms the API is running.

**Response:**

```
Printing Quotes API is running...
```

---

### `GET /api/quotes`

Retrieve all quotes.

**Response `200 OK`:**

```json
[
	{
		"id": "1",
		"author": "Mark Twain",
		"quote": "The secret of getting ahead is getting started."
	}
]
```

**Response `500`:**

```json
{ "error": "Failed to fetch quotes" }
```

---

### `POST /api/quotes`

Add a new quote. IDs are auto-generated.

**Request Body:**

```json
{
	"author": "Mark Twain",
	"quote": "The secret of getting ahead is getting started."
}
```

| Field    | Type   | Rules                      |
| -------- | ------ | -------------------------- |
| `author` | string | Required, min 2 characters |
| `quote`  | string | Required, min 5 characters |

**Response `201 Created`:**

```json
{
	"id": "2",
	"author": "Mark Twain",
	"quote": "The secret of getting ahead is getting started."
}
```

**Response `400`:**

```json
{ "error": "\"author\" is required" }
```

---

### `PUT /api/quotes/:id`

Update an existing quote by ID.

**URL Parameter:**

| Param | Type   | Description               |
| ----- | ------ | ------------------------- |
| `id`  | number | ID of the quote to update |

**Request Body:** _(same schema as POST)_

```json
{
	"author": "Winston Churchill",
	"quote": "Success is not final, failure is not fatal."
}
```

**Response `200 OK`:**

```json
{
	"id": "1",
	"author": "Winston Churchill",
	"quote": "Success is not final, failure is not fatal."
}
```

**Response `400`** — Invalid ID format or validation error:

```json
{ "error": "Invalid ID format" }
```

**Response `404`** — Quote not found:

```json
{ "error": "Quote not found" }
```

---

### `DELETE /api/quotes/:id`

Delete a quote by ID.

**URL Parameter:**

| Param | Type   | Description               |
| ----- | ------ | ------------------------- |
| `id`  | number | ID of the quote to delete |

**Response `200 OK`:**

```json
{ "message": "Quote deleted successfully" }
```

**Response `400`** — Invalid ID:

```json
{ "error": "Invalid ID format" }
```

**Response `404`** — Quote not found:

```json
{ "error": "Quote not found" }
```

---

## ✅ Validation Rules

All `POST` and `PUT` requests are validated using **Joi**:

- `author`: required string, minimum **2 characters**
- `quote`: required string, minimum **5 characters**

Invalid requests return a `400` status with a descriptive error message.

---

## 🗂️ Data Format (`db.json`)

The API stores data via `json-server`. Your `db.json` should follow this structure:

```json
{
	"quotes": [
		{
			"id": "1",
			"author": "Author Name",
			"quote": "Quote text here."
		}
	]
}
```

---

## ⚙️ Configuration

| Setting          | Value                          |
| ---------------- | ------------------------------ |
| API Port         | `5000`                         |
| JSON Server Port | `3000`                         |
| JSON Server URL  | `http://localhost:3000/quotes` |
