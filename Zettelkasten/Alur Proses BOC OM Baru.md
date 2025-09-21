- Login
- Home
- Pilih Portal Area
- Pilih Report Category
- Pilih Report Date (default: Hari ini)
- Pilih Start Time (Default Jam dan Menit saat ini)
- Pilih Finish time

```plantuml
@startuml
title BOC OM Use Case Diagram

left to right direction

actor "User" as user
actor "Admin" as admin

rectangle "BOC OM" {
  (Submit Report) as report
  (Review Report) as review
  (Review Manhour) as manhour
  (Edit Report) as edit
  (Sign Report) as sign
  (Generate PDF) as generatepdf
  
  (Manage User) as manageuser
}

user -- report
user -- review
user -- manhour
user -- edit
user -- sign
user -- generatepdf

manageuser -- admin
@enduml
```
