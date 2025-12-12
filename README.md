# Boi Binimoy 📚🔄
A Flutter-based mobile app for community book lending and borrowing with a structured request–approval–return workflow.

---

## 📌 Project Overview
**Boi Binimoy** helps users share books easily and responsibly. Users can list books with images, browse available books from others, send borrow requests, and complete borrowing only after the owner approves. The system tracks availability in real-time and supports returning books to make them available again.

---

## ✨ Features

### 🔐 Authentication (Firebase)
- Email/Password **Sign Up**
- Email/Password **Login**
- **Logout**
- User profile stored in Firestore (`users` collection)

### 📚 Book Management (Firestore + Cloudinary)
- Add books with:
  - Title
  - Author
  - Description
  - **Multiple images**
- Upload book images to **Cloudinary**
- Store image URLs in **Cloud Firestore**
- View:
  - **Available Books** (excluding your own)
  - **My Books**
- Delete your own books (with confirmation)

### 🔁 Borrow Workflow (Firestore)
- Request to borrow a book (with confirmation)
- Prevent duplicate **pending** requests for the same book by the same user
- Owner can:
  - View pending requests
  - Approve / Reject requests
- If approved:
  - Book becomes **unavailable**
  - Borrower is assigned
- Borrower can:
  - View borrowed books
  - **Return book** (restores availability)

### ⚡ Real-time Updates
- Firestore streams keep UI updated instantly:
  - Requests
  - Book availability
  - Borrowed/returned status

---

## 🧱 Tech Stack
- **Flutter (Dart)**
- **Firebase Authentication**
- **Cloud Firestore**
- **Cloudinary** (image hosting via `cloudinary_public`)
- **Provider** (state management)
- **image_picker** (selecting images)

---

## 📂 Project Structure (Key Files)

### Screens / UI
- `login_screen.dart` — Login UI and validation  
- `signup_screen.dart` — Signup UI and validation  
- `home_screen.dart` — Bottom navigation + Available/My Books/Profile  
- `add_book_screen.dart` — Add book form + image upload  
- `book_detail_screen.dart` — Book details + request to borrow  
- `borrow_requests_dialog.dart` — Owner approves/rejects requests  
- `profile_screen.dart` — Incoming requests, borrowed books, return, logout  

### Services
- `auth_service.dart` — Firebase Authentication operations  
- `firestore_service.dart` — Firestore CRUD + borrow workflow  
- `storage_service.dart` — Cloudinary image upload  

### Provider
- `auth_provider.dart` — Authentication state + user profile data  

### Firebase Setup
- `main.dart` — App entry + Firebase initialization  
- `firebase_options.dart` — Firebase config (generated)

---

## 🔥 Firestore Collections (Schema)

### `users`
Stores user profile data:
- `uid`
- `name`
- `email`
- `phone`
- `createdAt`

### `books`
Stores book details:
- `title`
- `author`
- `description`
- `ownerUid`
- `ownerName`
- `ownerEmail`
- `ownerPhone`
- `imageUrls` (List)
- `isAvailable` (bool)
- `borrowerUid` (nullable)
- `borrowerName` (nullable)
- `createdAt`
- `pendingRequestsCount` (optional)

### `borrow_requests`
Stores borrow request records:
- `bookId`
- `ownerUid`
- `requesterUid`
- `requesterName`
- `requesterEmail`
- `requesterPhone`
- `status` (`pending` / `approved` / `rejected`)
- `createdAt`

---

## ⚙️ Setup & Run Instructions

### 1) Install Flutter
Follow official Flutter setup:
- https://docs.flutter.dev/get-started/install

### 2) Install Dependencies
```bash
flutter pub get
