# Day 23 — Client-Side Security Analysis

## 🎯 Objective

Learn how to inspect JavaScript running in a web application and understand how client-side password-strength logic works.

## 🧪 Project Tested

I analyzed the JavaScript bundle of my own password-checker application.

## 🔍 What I Found

The application checks whether a password contains:

* Uppercase letters: `/[A-Z]/`
* Lowercase letters: `/[a-z]/`
* Numbers: `/[0-9]/`
* Special characters: `/[^A-Za-z0-9]/`

These checks are used to calculate the character `poolSize`.

### Pool Size

```text
Lowercase → +26
Uppercase → +26
Numbers   → +10
Special   → +32
```

### Entropy

The application calculates entropy using:

```text
password length × log2(poolSize)
```

## 🔎 Additional Checks

The application also checks for:

* Public/dictionary passwords
* Repeated-character passwords
* Numeric patterns

Example repeated-character detection:

```regex
/^(.)\1+$/
```

This can detect passwords such as:

```text
AAAA
1111
BBBB
```

## 🧠 Important Lesson

The final result is not based only on entropy.

The application checks weakness conditions first:

```text
entropy < 28
OR
dictionary match
OR
repeated characters
OR
numeric pattern
```

If one of these conditions is true, the password can be classified as weak before the higher entropy categories are evaluated.

### Key Takeaway

**First matching condition wins.**

## 🛠️ Tools Used

* Kali Linux
* Terminal
* `grep`
* JavaScript source inspection
* Browser
* My own password-checker application

## 📚 What I Learned

* Basic regex validation
* Boolean `OR (||)`
* Character pools
* Entropy
* Conditional logic
* Condition ordering
* Basic client-side security analysis

## ⚠️ Ethics

Testing was performed on my own application for educational purposes.
