# SQL Injection – Retrieval of Hidden Data

## Platform

PortSwigger Web Security Academy

## Difficulty

Apprentice

## Vulnerability

SQL Injection

## Lab Objective

This lab contains a SQL injection vulnerability in the product category filter.

The application uses a SQL query similar to:

`SELECT * FROM products WHERE category = 'Gifts' AND released = 1`

The objective was to perform a SQL injection attack that causes the application to display one or more unreleased products.

## What I Did

I tested the category parameter in the URL and modified the input to change the logic of the SQL query.

I used the following SQL injection payload in the category parameter:

`' OR 1=1--`

The URL-encoded version of the payload was sent through the product category filter.

## Why It Worked

The original query contains a condition that only displays released products:

`released = 1`

The injected condition `OR 1=1` introduces a condition that is always true.

The `--` characters comment out the remaining part of the SQL query.

As a result, the application's filtering logic was bypassed and unreleased products were displayed.

## Result

The application displayed previously hidden/unreleased products, so the lab was successfully solved.

**Status: Solved ✅**

## What I Learned

* SQL Injection can occur when user input is directly included in a SQL query.
* An attacker can manipulate the logic of a vulnerable query.
* `1=1` is an always-true condition.
* `OR` can introduce an alternative condition.
* `--` can comment out the remaining part of a SQL statement.
* User input should never be trusted or directly concatenated into SQL queries.

## Mitigation

SQL Injection can be prevented by using:

* Parameterized queries / prepared statements
* Proper input validation
* Secure database access practices
* Least-privilege database accounts

## Evidence

(lab-01-solved.png)

## Practice Environment

This lab was completed in the authorized PortSwigger Web Security Academy environment for educational purposes.

