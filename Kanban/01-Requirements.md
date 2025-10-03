# Requirements - BOC OM

```plantuml
@startuml
title BOC OM Use Case Diagram

left to right direction

actor "User" as user
actor "Admin" as admin

user <|-- admin

rectangle "BOC OM" {
  (Login) as login
  (Submit Report) as report
  (Review Report) as review
  (Edit Report) as edit
  (Sign Report) as sign
  (Generate PDF) as generatepdf
  (Review Quality Performance Indicator) as qpi
  (Review Monthly Summary) as summary
  
  (Manage User) as manageuser
  (Manage Role) as managerole
  (Manage Area of Work) as managearea
  (Manage Equipment Category) as manageequipment
  (Manage Functional Location) as managelocation
  (Manage Tank Type) as managetanktype
  (Manage Service) as manageservice
  (Manage Tank Component Group) as managetankcomponentgroup
  (Manage Tank Component) as managetankcomponent
  (Manage Tank Component Configuration) as managetankcomponentconfiguration
  (Manage Report Category) as managereportcategory
  (Manage Area & Equipment Mappings) as manageareaequipment
  
  generatepdf .> review : <<extend>>
}

user -- login
user -- report
user -- review
user -- edit
user -- sign
user -- qpi
user -- summary

manageuser -- admin
managerole -- admin
managearea -- admin
manageequipment -- admin
managelocation -- admin
managetanktype -- admin
manageservice -- admin
managetankcomponentgroup -- admin
managetankcomponent -- admin
managetankcomponentconfiguration -- admin
managereportcategory -- admin
manageareaequipment -- admin

note right of login
  Precondition:
  Akun sudah dibuat oleh Admin
end note
@enduml
```

| User class | Use cases                                                                                                                                                                                                                                                                                 |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| User       | Login, Submit Report, Edit Report, Sign Report, Review Report, Generate PDF, Review Quality Performance Indicator, Review Monthly Summary                                                                                                                                                 |
| Admin      | Manage User, Manage Role, Manage Area of Work, Manage Equipment Category, Manage Functional Location, Manage Tank Type, Manage Service, Manage Tank Component Group, Manage Tank Component, Manage Tank Component Configuration, Manage Report Category, Manage Area & Equipment Mappings |

## User Stories

- Sebagai user, saya bisa login dengan akun yang dibuat oleh admin
## Acceptance Criteria

- Login valid → masuk home page
- Login invalid → error message

## ERD

```mermaid
---
title: BOC OM (ERD Crow's Foot)
---
erDiagram

IdentityUser ||--o{ ApplicationUser : inherits

AreaOfWork ||--o{ AreaEquipmentCategory : contains
EquipmentCategory ||--o{ AreaEquipmentCategory : contains
FunctionalLocation }o--|| TankType : "has"
FunctionalLocation }o--|| Service : "has"
FunctionalLocation }o--|| AreaEquipmentCategory : "belongs to"

Report ||--|| ReportCategory : "categorized as"
Report ||--|| FunctionalLocation : "at"

ApplicationUser ||--o{ UserReport : "assigned"
Report ||--o{ UserReport : "involves"
UserReport }o--|| UserType : "with role"

TankType ||--o{ TankComponentConfiguration : "configured with"
TankComponentGroup ||--o{ TankComponentConfiguration : "contains"
TankComponent ||--o{ TankComponentConfiguration : "part of"

Report ||--o{ TankComponentGroupRecord : "documents"
TankComponentGroup ||--o{ TankComponentGroupRecord : "instance of"

TankComponentGroupRecord ||--o{ TankComponentRecord : "has"
TankComponent ||--o{ TankComponentRecord : "inspected as"
TankComponentRecord }o--|| TankComponentStatus : "with status"

TankComponentRecord ||--o{ TankComponentReading : "produces"

Report ||--o{ Documentation : "includes"
TankComponentGroup ||--o{ Documentation : "related to"
Documentation }o--|| DocumentationPeriod : "tagged as"

```

## Class Diagram

```mermaid
---
title: BOC OM Class Diagram
---
classDiagram
	class AreaOfWork {
		+int Id
		+string Name
		+ICollection~EquipmentCategory~ EquipmentCategories [Navigation]
	}
	
	class EquipmentCategory {
		+int Id
		+string Name
		+ICollection~FunctionalLocation~ FunctionalLocations
		+int? AreaOfWorkId [FK]
		+AreaOfWork? AreaOfWork [Navigation]
	}
	
	class FunctionalLocation {
		<<abstract>>
		+int Id
		+string Name
		+int? EquipmentCategoryId [FK]
		+EquipmentCategory? EquipmentCategory [Navigation]
		+ICollection~Report~ Reports [Navigation]
	}
	
	class NonTankFunctionalLocation {
		+string? DetailedLocation
		+string? JobDescription
		+ICollection~NonTankDocumentation~ Documentations [Navigation]
	}
	
	class Documentation {
		+int Id
		+string FilePath
	}
	
	class NonTankDocumentation {
		+DocumentationPeriod Period
		+int NonTankFunctionalLocationId [FK]
		+NonTankFunctionalLocation NonTankFunctionalLocation [Navigation]
	}
	
	class TankDocumentation {
		+int TankComponentGroupId [FK]
		+TankComponentGroup TankComponentGroup [Navigation]
	}
	
	class DocumentationPeriod {
		<<enum>>
		BeforeProcess
		DuringProcess
		AfterProcess
	}
	
	class TankFunctionalLocation {
		+int? TankTypeId [FK]
		+TankType? TankType [Navigation]
		+int? ServiceId [FK]
		+Service? Service [Navigation]
	}
	
	class TankType {
		+int Id
		+string Name
		+ICollection~TankComponentGroup~ TankComponentGroups [Navigation]
		+ICollection~TankFunctionalLocation~ TankFunctionalLocations [Navigation]
	}
	
	class TankComponentGroup {
		+int Id
		+TankComponentGroupType Type
		+string? Remarks
		+int? TankTypeId [FK]
		+TankType? TankType [Navigation]
		+ICollection~TankComponent~ TankComponents [Navigation]
		+ICollection~TankDocumentation~ Documentations [Navigation]
	}
	
	class TankComponentGroupType {
		<<enum>>
		MainTank
		TankAccessories
		TankMetering
	}
	
	class TankComponent {
		+int Id
		+string Name
		+Status Status
		+int TankComponentGroupId [FK]
		+TankComponentGroup Group [Navigation]
		+ICollection~TankComponentReading~ Readings [Navigation]
	}
	
	class TankComponentReading {
		+int Id
		+double Value
		+string Unit
		+int TankComponentId [FK]
		+TankComponent TankComponent [Navigation]
	}
	
	class Status {
		<<enum>>
		Normal
		Minor
		Major
		NA
	}
	
	class Service {
		+int Id
		+string Name
		+ICollection~TankFunctionalLocation~ TankFunctionalLocations [Navigation]
	}
	
	class Report {
		+int Id
		+DateTime Date
		+TimeSpan StartTimeOfWork
		+TimeSpan FinishTimeOfWork
		+int FunctionalLocationId [FK]
		+FunctionalLocation FunctionalLocation [Navigation]
		+int ReportCategoryId [FK]
		+ReportCategory ReportCategory [Navigation]
		+ICollection~UserReport~ UserReports [Navigation]
	}
	
	class ReportCategory {
		+int Id
		+string Name
		+ICollection~Report~ Reports [Navigation]
	}
	
	class UserReport {
		+int ReportId [FK]
		+string ApplicationUserId [FK]
		+Report Report [Navigation]
		+ApplicationUser User [Navigation]
		+UserType UserType
	}
	
	class UserType {
		<<enum>>
		Submitter
		Signatory
		Personnel
	}
	
	class IdentityUser {
        +string Id
        +string UserName
        +string NormalizedUserName
        +string Email
        +string NormalizedEmail
        +bool EmailConfirmed
        +string PasswordHash
        +string SecurityStamp
        +string ConcurrencyStamp
        +string PhoneNumber
        +bool PhoneNumberConfirmed
        +bool TwoFactorEnabled
        +DateTimeOffset? LockoutEnd
        +bool LockoutEnabled
        +int AccessFailedCount
    }

    class ApplicationUser {
        +string? Name
        +string? NIP
        +string? Job
        +string? SignatureImagePath
        +ICollection~UserReport~ UserReports
    }
	
	AreaOfWork "0..1" <-- "0..*" EquipmentCategory
	EquipmentCategory "0..1" <-- "0..*" FunctionalLocation
	FunctionalLocation <|-- NonTankFunctionalLocation
	FunctionalLocation <|-- TankFunctionalLocation
	
	Documentation <|-- NonTankDocumentation
	NonTankDocumentation --> DocumentationPeriod
	NonTankFunctionalLocation "1" *-- "0..*" NonTankDocumentation
	
	Documentation <|-- TankDocumentation
	TankComponentGroup "1" *-- "0..*" TankDocumentation
	TankComponentGroup "0..*" --> "0..1" TankType
	TankComponentGroup --> TankComponentGroupType
	TankFunctionalLocation "0..*" --> "0..1" TankType
	TankFunctionalLocation "0..*" --> "0..1" Service
	TankComponentGroup "1" *-- "0..*" TankComponent
	TankComponent "1" *-- "0..*" TankComponentReading
	TankComponent --> Status
	
	Report "0..*" --* "1" FunctionalLocation
	Report "0..*" --* "1" ReportCategory
	Report "1" *-- "0..*" UserReport
	ApplicationUser "1" *-- "0..*" UserReport
	UserReport --> UserType
	IdentityUser <|-- ApplicationUser
```

New

42-T-101G -- Floating Roof
42-T-101A -- Floating Roof
42-T-402B -- Spherical

Floating Roof -- Main Tank
Floating Roof -- Tank Accessories
Floating Roof -- Tank Metering
Spherical -- Main Tank
Spherical -- Tank Accessories
Spherical -- Tank Metering

Visual Plate -- (Floating Roof -- Main Tank)
Manhole -- (Floating Roof -- Main Tank)
Visual Plate -- (Spherical -- Main Tank)
Manhole -- (Spherical -- Main Tank)

```mermaid
---

title: BOC OM

---

classDiagram

direction TB

    class IdentityUser {

        +string Id

        ...

    }

    class ApplicationUser {

        +string? Name

        +string? NIP

        +string? Job

        +string? SignatureImagePath

    }

    class AreaOfWork {

        +int Id

        +string Name

    }

    class EquipmentCategory {

        +int Id

        +string Name

    }

    class FunctionalLocation {

        +int Id

        +string Name

        +int? AreaEquipmentCategoryId

        +int? TankTypeId

        +int? ServiceId

    }

    class TankType {

        +int Id

        +string Name

    }

    class Service {

        +int Id

        +string Name

    }

    class ReportCategory {

        +int Id

        +string Name

    }

    class Report {

        +int Id

        +DateTime ReportDate

        +TimeSpan StartTimeOfWork

        +TimeSpan FinishTimeOfWork

        +string? DetailedLocation

        +string? JobDescription
        
        +int ReportCategoryId
        
        +int FunctionalLocationId

    }

    class TankComponentGroup {

        +int Id

        +string Name

    }

    class TankComponent {

        +int Id

        +string Name

    }

    class TankComponentStatus {

        Normal

        Minor

        Major

        Failure

        NA

    }
    
    class Documentation {
    
	    +int Id
	    
	    +string FilePath
	    
	    +DocumentationPeriod? Period
	    
	    +int ReportId
	    
	    +int? TankComponentGroupId
	    
    }
    
    class DocumentationPeriod {
	    
	    <<enum>>
	    
	    BeforeProcess
	    
	    DuringProcess
	    
	    AfterProcess
	    
    }

    class AreaEquipmentCategory {

        +int Id

        +int AreaOfWorkId

        +int EquipmentCategoryId

    }

    class UserReport {
    
	    +int Id
		
		+UserType UserType

        +int ReportId

        +string ApplicationUserId

    }

    class UserType {

        Submitter

        Signatory

        Personnel

    }

    class TankComponentConfiguration {

        +int Id
        
        +int TankComponentId

        +int TankTypeId

        +int TankComponentGroupId

    }
    
    class TankComponentGroupRecord {
    
	    +int Id
    
	    +string Remarks
	    
	    +int ReportId
	    
	    +int TankComponentGroupId
	    
    }

    class TankComponentRecord {

		+int Id

		+TankComponentStatus Status
		
        +int TankComponentGroupRecordId

        +int TankComponentId

    }

    class TankComponentReading {

        +int Id
        
		+string? Name

        +double Value

        +string Unit

		+int TankComponentRecordId
		
    }

    <<enum>> TankComponentStatus

    <<enum>> UserType

    IdentityUser <|-- ApplicationUser

    AreaOfWork "1" *-- "*" AreaEquipmentCategory

    EquipmentCategory "1" *-- "*" AreaEquipmentCategory

    FunctionalLocation "*" --> "1" TankType

    FunctionalLocation "*" --> "1" Service

    UserReport "*" --* "1" ApplicationUser

    UserReport "*" --* "1" Report

    UserReport --> UserType

    Report "*" --* "1" ReportCategory

    Report "*" --* "1" FunctionalLocation

    TankComponentReading "*" --* "1" TankComponentRecord

    TankComponentConfiguration "*" --* "1" TankType

    TankComponentConfiguration "*" --* "1" TankComponentGroup

    FunctionalLocation "*" --> "1" AreaEquipmentCategory

    TankComponentConfiguration "*" --* "1" TankComponent
    
    TankComponentGroupRecord "*" --* "1" Report
    
    TankComponentGroupRecord "*" --* "1" TankComponentGroup

    TankComponentRecord "*" --* "1" TankComponentGroupRecord

    TankComponentRecord "*" --* "1" TankComponent
    
    TankComponentRecord --> TankComponentStatus
    
    Documentation "*" --* "1" Report
    
    Documentation --> DocumentationPeriod
    
    Documentation "*" --> "1" TankComponentGroup
```


minor
```mermaid
---

title: BOC OM

---

classDiagram

direction TB

    class IdentityUser {

        +string Id

        ...

    }

    class ApplicationUser {

        +string? Name

        +string? NIP

        +string? Job

        +string? SignatureImagePath

    }

    class AreaOfWork {

        +int Id

        +string Name

    }

    class EquipmentCategory {

        +int Id

        +string Name

    }

    class FunctionalLocation {

        +int Id

        +string Name
        
        +int AreaOfWorkId
        
        +int EquipmentCategoryId

        +int? TankTypeId

        +int? ServiceId

    }

    class TankType {

        +int Id

        +string Name

    }

    class Service {

        +int Id

        +string Name

    }

    class ReportCategory {

        +int Id

        +string Name

    }

    class Report {

        +int Id

        +DateTime ReportDate

        +TimeSpan StartTimeOfWork

        +TimeSpan FinishTimeOfWork

        +string? DetailedLocation

        +string? JobDescription
        
        +int ReportCategoryId
        
        +int FunctionalLocationId

    }

    class TankComponentGroup {

        +int Id

        +string Name

    }

    class TankComponent {

        +int Id

        +string Name

    }

    class TankComponentStatus {

        Normal

        Minor

        Major

        Failure

        NA

    }
    
    class Documentation {
    
	    +int Id
	    
	    +string FilePath
	    
	    +DocumentationPeriod? Period
	    
	    +int ReportId
	    
	    +int? TankComponentGroupId
	    
    }
    
    class DocumentationPeriod {
	    
	    <<enum>>
	    
	    BeforeProcess
	    
	    DuringProcess
	    
	    AfterProcess
	    
    }

    class UserReport {
    
	    +int Id
		
		+UserType UserType

        +int ReportId

        +string ApplicationUserId

    }

    class UserType {

        Submitter

        Signatory

        Personnel

    }

    class TankComponentConfiguration {

        +int Id
        
        +int TankComponentId

        +int TankTypeId

        +int TankComponentGroupId

    }
    
    class TankComponentGroupRecord {
    
	    +int Id
    
	    +string Remarks
	    
	    +int ReportId
	    
	    +int TankComponentGroupId
	    
    }

    class TankComponentRecord {

		+int Id

		+TankComponentStatus Status
		
        +int TankComponentGroupRecordId

        +int TankComponentId

    }

    class TankComponentReading {

        +int Id
        
		+string? Name

        +double Value

        +string Unit

		+int TankComponentRecordId
		
    }

    <<enum>> TankComponentStatus

    <<enum>> UserType

    IdentityUser <|-- ApplicationUser
    
    FunctionalLocation "*" --> "1" AreaOfWork
    
    FunctionalLocation "*" --> "1" EquipmentCategory

    FunctionalLocation "*" --> "1" TankType

    FunctionalLocation "*" --> "1" Service

    UserReport "*" --* "1" ApplicationUser

    UserReport "*" --* "1" Report

    UserReport --> UserType

    Report "*" --* "1" ReportCategory

    Report "*" --* "1" FunctionalLocation

    TankComponentReading "*" --* "1" TankComponentRecord

    TankComponentConfiguration "*" --* "1" TankType

    TankComponentConfiguration "*" --* "1" TankComponentGroup

    TankComponentConfiguration "*" --* "1" TankComponent
    
    TankComponentGroupRecord "*" --* "1" Report
    
    TankComponentGroupRecord "*" --* "1" TankComponentGroup

    TankComponentRecord "*" --* "1" TankComponentGroupRecord

    TankComponentRecord "*" --* "1" TankComponent
    
    TankComponentRecord --> TankComponentStatus
    
    Documentation "*" --* "1" Report
    
    Documentation --> DocumentationPeriod
    
    Documentation "*" --> "1" TankComponentGroup
```

Ketika generate form, perlu mengetahui: TankType untuk generate component group yang dalam tiap component group memiliki component masing-masing