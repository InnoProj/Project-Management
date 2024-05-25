```plantuml

@startuml innP

abstract class Base {
    Id: Guid
    CreatedAt: DateTime
}

enum UserRoleType {
    SuperAdmin
    Admin
    User
}

class User {
    Firstname: string
    Lastname: string
    Birthday: DateOnly
    UserRole: UserRoleType
    AreaCode: int?
    PhoneNumber: string?
    Email: MailAddress
}

class Address {
    Street: string
    HouseNumber: string
    Additional: string
    PostalCode: string
    City: string
    Country : string
}

class Event {
    Title: string
    Description: string
    EventStart: DateTime
    EventEnd: DateTime
    MinParticipants: int
    MaxParticipants: int
    Location: Address
    RegistrationDeadline: DateTime
    PictureBlob : string
}

class ReportedUser {
    IssueDescription: string
    Reason: ReportReason
}

enum ReportReason {
    unangemessene_Sprache
    Keine Rückmeldung
}

class Interest {
    Name: string
}

abstract class Post {
    Message : string
}

class PrivateChatPost {
    
}

class AllChatPost {
    
}

class PrivateChat {

}




class User extends Base
class User extends IdentityUser
class Event extends Base
class Address extends Base
class Post extends Base
class ReportedUser extends Base
class PrivateChatPost extends Post
class AllChatPost extends Post
class PrivateChat extends Base
AllChatPost "0..*" ---o "1" Event : has
User "1" o--- "0..*" Event : creates
Event "0..*" --- "0..*" User : has participants
User "0..*" --- "0..*" User : follows
Event "1" o--- "0..*" Address : has
User "0..*" --- "0..*" Interest : has
Event "0..*" --- "0..*" Interest : has
Post "1" ---o "1" User : has
PrivateChat "1" ---o "1" User : creates
PrivateChat "1" ---o "1" User : participates
PrivateChat "1" ---o "1" PrivateChatPost : has
ReportedUser "1" ---o "1" User : reports
ReportedUser "1" ---o "1" User : is reported
ReportedUser "1" ---o "1" Event : is connected
@enduml
