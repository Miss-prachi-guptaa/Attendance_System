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
