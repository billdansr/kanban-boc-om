# Requirements - BOC OM

```plantuml
@startuml
title BOC OM Use Case Diagram

left to right direction

actor "User" as user
actor "Admin" as admin

rectangle "BOC OM" {
  (Login) as login
  (Submit Report) as report
  (Review Report) as review
  (Review Manhour) as manhour
  (Edit Report) as edit
  (Sign Report) as sign
  (Generate PDF) as generatepdf
  
  (Manage User) as manageuser
  
  generatepdf .> review : <<extend>>
}

user -- login
user -- report
user -- review
user -- manhour
user -- edit
user -- sign

admin -- manageuser

note right of login
  Precondition:
  Akun sudah dibuat oleh Admin
end note
@enduml
```

| User class | Use cases                                                                                   |
| ---------- | ------------------------------------------------------------------------------------------- |
| User       | Login, Submit Report, Review Manhour, Edit Report, Sign Report, Review Report, Generate PDF |
| Admin      | Manage User                                                                                 |

## User Stories

- Sebagai user, saya bisa login dengan akun yang dibuat oleh admin
## Acceptance Criteria

- Login valid → masuk home page
- Login invalid → error message
