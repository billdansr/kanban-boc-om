```mermaid
erDiagram
    AspNetUsers ||--o| UserProfile : "has"
    AspNetUsers {
        string Id PK
        string UserName
        string NormalizedUserName
        string Email
        string PasswordHash
    }
    UserProfile {
        int Id PK
        string UserId FK
        string Name
        string NIP
        string Rules
        string Job
        byte[] SampleSignature
    }
```
