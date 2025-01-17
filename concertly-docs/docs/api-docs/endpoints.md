---
title: Endpoints
sidebar_position: 2
---

# API Endpoints

A list of all the endpoints in the API

## Authentication

### Register

#### <span style={{color: "#70c895"}}>POST</span>
**Request:**
```http
POST /register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "secure_password123",
  "displayName": "John Doe"
}
```

**Required Fields:**
- `email`: User's email address
- `password`: User's password
- `displayName`: User's display name

**Response:** `201 Created`
```json
{
  "message": "User registered successfully. Please verify your email."
}
```

### Login

#### <span style={{color: "#70c895"}}>POST</span>
**Request:**
```http
POST /login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "secure_password123"
}
```

**Required Fields:**
- `email`: User's email address
- `password`: User's password

**Response:** `200 OK`
```json
{
  "message": "Login successful",
  "access_token": "eyJhbGc..."
}
```

### Delete Account

#### <span style={{color: "#e74d48"}}>DELETE</span>
**Request:**
```http
DELETE /delete-user
```

**Headers:**
| Name | Value | Description |
|------|--------|-------------|
| Authorization | Bearer token | JWT access token obtained from login |

**Response:** `200 OK`
```json
{
  "message": "User deleted successfully"
}
```

## Data management

### Works
Dataset of musical works.

#### <span style={{color: "#73aff8"}}>GET</span>
**Request:**
```http
GET /get-works
```

**Query Parameters:**
- `id`: Query by work id
- `name`: Query by name
- `composer_id`: Query by [composer](/docs/api-docs/endpoints#composers) id

**Response:** `200 OK`
```json
{
  "about": null,
  "composer_id": 1,
  "date": "1885-10-25T12:00:00+00:00",
  "duration_seconds": null,
  "id": 1,
  "mvt1_title": "Allegro non troppo",
  "mvt2_title": "Andante moderato",
  "mvt3_title": "Allegro giocoso",
  "mvt4_title": "Allegro energico e passionato",
  "mvt5_title": null,
  "mvt6_title": null,
  "name": "Symphony No. 4 in E minor",
  "opus_no": "98"
}
```

#### <span style={{color: "#70c895"}}>POST</span>
**Request:**
```http
POST /add-work
Content-Type: application/json

{
  "name": "Symphony No. 5",
  "composer_id": "123",
  "duration_seconds": 1800,
  "opus_no": "67",
  "date": "1808-12-22T00:00:00+00:00",
  "mvt1_title": "Allegro con brio",
  "mvt2_title": "Andante con moto"
}
```

**Required Fields:**
- `name`: The name of the musical work
- `composer_id`: ID of the composer who wrote the work
- `duration_seconds`: Duration of the work in seconds

**Optional Fields:**
- `opus_no`: The opus number of the work
- `date`: ISO 8601 timestamp (e.g., "YYYY-MM-DDTHH:mm:ss+00:00")
- `mvt1_title`: Title of the first movement
- `mvt2_title`: Title of the second movement
- `mvt3_title`: Title of the third movement
- `mvt4_title`: Title of the fourth movement
- `mvt5_title`: Title of the fifth movement
- `mvt6_title`: Title of the sixth movement

**Response:** `201 Created`
```json
{
  "message": "Work added successfully!",
  "work_id": "456"
}
```

### Composers
Dataset of composers.

#### <span style={{color: "#73aff8"}}>GET</span>
**Request:**
```http
GET /get-composers
```

**Query Parameters:**
- `id`: Query by composer id
- `name`: Query by name
- `location_id`: Query by [city](/docs/api-docs/endpoints#cities) id

**Response:** `200 OK`
```json
{
    "birth": "1833-05-07T12:00:00+00:00",
    "death": "1897-04-03T12:00:00+00:00",
    "id": 1,
    "img_url": "https://concertly.s3.eu-north-1.amazonaws.com/composer-images/brahms.png",
    "location_id": 6,
    "name": "Johannes Brahms"
}
```

### Concerts
Dataset of concerts.

#### <span style={{color: "#73aff8"}}>GET</span>
**Request:**
```http
GET /get-concerts
```

**Query Parameters:**
- `id`: Query by concert id
- `venue_id`: Query by venue id
- `title`: Query by title

**Response:** `200 OK`
```json
{
  "date": "2025-01-29T18:30:00+00:00",
  "id": 4,
  "img_url": null,
  "overview": "This is overview text.",
  "title": "Benjamin Grosvenor plays Mozart",
  "venue_id": 1
}
```

### Cities
Dataset of cities.

#### <span style={{color: "#73aff8"}}>GET</span>
**Request:**
```http
GET /get-cities
```

**Query Parameters:**
- None

**Response:** `200 OK`
```json
{
  "country": "United Kingdom",
  "id": 1,
  "name": "London"
}
```

### Venues
Dataset of concert venues.

#### <span style={{color: "#73aff8"}}>GET</span>
**Request:**
```http
GET /get-venues
```

**Query Parameters:**
- `id`: Query by city id
- `name`: Query by venue name

**Response:** `200 OK`
```json
{
  "city_id": 1,
  "id": 1,
  "name": "Royal Festival Hall"
}
```