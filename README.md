# Attendance_System

# Installation

## Requirements

- PHP 8.2+
- Laravel 13
- Composer
- MySQL

---

## Clone

git clone <repository>

---

Install packages

composer install

---

Create environment

cp .env.example .env

---

Generate application key

php artisan key:generate

---

Configure database

DB_CONNECTION=mysql

DB_HOST=127.0.0.1

DB_PORT=3306

DB_DATABASE=attendance_system

DB_USERNAME=root

DB_PASSWORD=

---

Run migrations

php artisan migrate

---

Serve application

php artisan serve



# Database

# Database Changes

No new tables are created.

Only the existing users table is updated.

---

Migration

php artisan migrate

---

Columns Added

face_descriptor

Type:
LONGTEXT

Purpose:
Stores AI-generated face descriptor.

---

is_face_registered

Type:
BOOLEAN

Default:
false

Purpose:
Indicates whether employee has registered face.

---

face_registered_at

Type:
TIMESTAMP

Purpose:
Stores registration date and time.

---

No manual SQL execution is required.

Migration handles all database changes.

# docs/03-API.md

# API Documentation

---

## Register Face

POST

/api/me/register-face

---

Request

Content-Type

multipart/form-data

Body

image : File

---

Success

{
    "success": true,
    "message": "Face registered successfully."
}

---

Already Registered

{
    "success": false,
    "message": "Face already registered."
}

---

Validation Error

{
    "message": "The image field is required."
}


# docs/04-Integration.md

# Integration Guide

This project is designed as a standalone module.

Follow these steps while integrating into an existing HRMS.

---

Step 1

Run migration

php artisan migrate

This adds required face recognition columns.

No existing table is modified manually.

---

Step 2

Copy folders

app/Services

app/Http/Controllers/AttendanceController.php

app/Http/Requests/RegisterFaceRequest.php

routes/api.php

---

Step 3

Update User Model

Add fillable

face_descriptor

is_face_registered

face_registered_at

---

Add cast

'is_face_registered' => 'boolean'

---

Step 4

Replace Authentication

Temporary Development

$user = User::first();

Production

$user = request()->user();

OR

$user = Auth::user();

depending upon existing authentication.

---

Step 5

Configure AI Service

Currently

FaceRecognitionService

returns dummy descriptor.

Replace only this service with actual AI implementation.

No controller changes are required.

No attendance logic changes are required.

---

Step 6

Temporary Storage

Images are stored in

storage/app/temp

and automatically deleted after processing.

---

Step 7

Testing

Import the Postman Collection.

Run

Register Face API

Verify

face_descriptor

is_face_registered

face_registered_at

inside users table.

Integration completed.


#.env

APP_NAME=FaceAttendance

APP_ENV=local

APP_DEBUG=true

DB_CONNECTION=mysql

DB_HOST=127.0.0.1

DB_PORT=3306

DB_DATABASE=attendance_system

DB_USERNAME=root

DB_PASSWORD=

###
Flutter App
      │
      ▼
Register Face API
      │
      ▼
User Table
(face_descriptor)
      │
      ▼
Mark Attendance API
      │
      ▼
Face Verification
      │
      ▼
Attendance Table
(Check-In / Check-Out)

