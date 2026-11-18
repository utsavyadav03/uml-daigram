# Taskflow UML1

> This diagram documents the checked-out Smart Healthcare Resource project, not a Taskflow application.

## Healthcare resource domain class diagram

```mermaid
classDiagram
    class Patient {
        +int patientid
        +String fullname
        +int age
        +String gender
        +String bloodgroup
        +String mobilenumber
        +String email
        +String city
        +String createdat
        +String approve
        +String verificationtoken
        +boolean verified
    }

    class Admin {
        +int adminid
        +String username
        +String password
    }

    class BloodBank {
        +int bloodbankid
        +String bloodbankname
        +String licensenumber
        +String contactperson
        +String mobile
        +String reception
        +String email
        +String address
        +String city
        +double latitude
        +double longitude
        +String approve
        +String createdat
    }

    class BloodRequest {
        +int requestid
        +int patientid
        +int bloodbankid
        +String bloodgroup
        +int requiredunits
        +String hospitalname
        +String requireddate
        +String emergencylevel
        +String requestdate
        +String status
        +String remarks
    }

    class BloodStock {
        +int stockid
        +String bloodgroup
        +int units
        +String updatedat
    }

    class BloodTransaction {
        +int transactionid
        +int requestid
        +int bloodbankid
        +int patientid
        +String bloodgroup
        +int units
        +String transactiontype
        +String patienttype
        +String hospitalname
        +String transactiondate
        +String remarks
    }

    BloodBank "1" --> "0..*" BloodRequest : bloodrequest
    BloodBank "1" --> "0..*" BloodStock : bloodstock
    BloodBank "1" --> "0..*" BloodTransaction : bloodtransaction
    BloodRequest ..> Patient : patientid (stored ID)
    BloodTransaction ..> BloodRequest : requestid (stored ID)
    BloodTransaction ..> Patient : patientid (stored ID)

    note for BloodRequest "patientid and bloodbankid are scalar fields; only the BloodBank collection mapping is declared."
    note for BloodTransaction "requestid, patientid, and bloodbankid are scalar fields, not declared JPA object associations."
    note for Admin "Standalone administrator entity."
```

## Relationship notes

- The three solid associations are represented by `BloodBank`'s `@OneToMany` collections.
- Dashed dependencies show ID values stored by the class; they are not declared JPA object relationships.
- `Admin` is shown as a standalone entity because the model does not declare relationships for it.
