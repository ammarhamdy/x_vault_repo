

# Users on Android phone

On an Android phone, **“users”** are separate spaces on the same device — similar to having multiple accounts on a computer. 

Each user has its own apps, settings, files, and data.

## Types of Users / Profiles on Android

### 1. Owner (User 0)
- The **main** account on the phone.
- Created when the phone is first set up.
- Has full control: add/remove users, install apps for all users.
### 2. Secondary Users
- Completely separate accounts with their own apps, home screens, settings.
- Like guest accounts on a laptop.
- Don’t share data with the owner.
### 3. Guest User
- Temporary account for lending your phone to someone.
- Clears data when removed.
- Limited access to your apps and data.
### 4. Work Profile (Common on company phones)
- Creates a container managed by your company MDM or Google Workspace.
- Has separate apps with a small briefcase/bag icon.
- Keeps work and personal data separate.
- ADB sees this as another **user ID** (e.g., user 10 or user 150).
### 5. Secure Folder / Dual Apps / Parallel Apps (Samsung, Xiaomi, etc.)
Not official Android “users”, but internally Android treats them as **separate user profiles**.
Examples:
- Samsung Knox “Secure Folder”
- Xiaomi “Dual Apps”
- Oppo “Clone Apps”
Each of these creates another **user ID** (user 150, user 999, etc.), so ADB detects them.


## How to see the users on your device
```
adb shell pm list users
```

## Summary

|User Type|Purpose|Has own apps?|
|---|---|---|
|Owner (0)|Main user|Yes|
|Secondary User|Separate person account|Yes|
|Guest|Temporary login|Yes|
|Work Profile|Company-controlled space|Yes|
|Dual Apps / Secure Folder|Parallel app environments|Yes|