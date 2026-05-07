1. What problem it solves
Over-fetching (too much data)
Under-fetching (multiple calls)
Multiple endpoints (REST complexity)

👉 GraphQL = one endpoint, client chooses data

2. REST vs GraphQL (must be clear)

REST

Many endpoints (/users, /orders)
Fixed response
Backend controls data

GraphQL

One endpoint (/graphql)
Flexible response
Client controls data
3. Request → Response Flow
Client sends query
GraphQL parses it
Calls resolvers
Fetches data
Returns structured response
4. Operations
Query → read data
Mutation → write data
Subscription → real-time (just know concept)
5. Mindset Shift (important)

👉 REST = “endpoint-based thinking”
👉 GraphQL = “data-based thinking”

⏱️ 20–50 min → Hands-on (just try, no setup needed)

Use any GraphQL playground online (or later local)

Example Query
query {
  user(id: 1) {
    name
    email
  }
}

👉 Observe:

You choose fields
Response matches exactly
Try variations mentally:
Remove email
Add nested object (like orders)
⏱️ 50–60 min → Notes (IMPORTANT)

Write this in your own words:

What is GraphQL
REST vs GraphQL (3 points)
What is Query / Mutation
Why single endpoint matters
🔹 1. What is a Schema?

👉 Schema = Blueprint / contract of GraphQL API

It defines:

What data exists
What operations are allowed
What structure client can request

Example:

type Student {
  id: ID
  name: String
}

Meaning:
👉 “Student object has id and name fields”

🔹 2. type (Object Type)

Equivalent to:

Java class
DTO
Response object

Example:

type Student {
  id: ID
  name: String
  department: String
}

Think:

class Student {
   Long id;
   String name;
   String department;
}
🔹 3. Scalars (Primitive Types)

GraphQL primitive types:

GraphQL	Java Equivalent
String	String
Int	int / Integer
Boolean	boolean
Float	double / float
ID	Long/String/UUID

Example:

type Student {
  id: ID
  age: Int
  active: Boolean
}
🔹 4. What is ID?

👉 Special scalar for unique identifiers

Used for:

Primary keys
UUIDs
Unique references

Example:

id: ID
🔹 5. Nullability (!) ⭐ IMPORTANT
name: String

👉 Optional (can be null)

name: String!

👉 Mandatory (cannot be null)

Think:

@NotNull
private String name;
🔹 6. Lists ([])
students: [Student]

Meaning:
👉 Returns array/list of students

Equivalent:

List<Student>
🔹 7. Query Type

👉 Used for READ operations

Example:

type Query {
  getStudent(id: ID!): Student
}

Meaning:

Client can call getStudent
Must pass id
Returns Student
🔹 8. Mutation Type

👉 Used for WRITE operations

Create
Update
Delete

Example:

type Mutation {
  deleteStudent(id: ID!): String
}
🔹 9. Input Type ⭐ VERY IMPORTANT

Used for request body/input object

Example:

input CreateStudentInput {
  name: String!
  department: String!
}

Equivalent:

class CreateStudentInput {
   String name;
   String department;
}
🔹 10. Why input Exists?

Instead of:

createStudent(name: String, department: String)

We do:

createStudent(input: CreateStudentInput)

Benefits:

Clean structure
Easy to extend
Enterprise-friendly
DTO-style design
🔹 11. Enum

Fixed allowed values

Example:

enum Department {
  CSE
  ECE
  MECH
}

Meaning:
👉 Only these values allowed

🔹 12. Full Small Example
type Student {
  id: ID!
  name: String!
  department: String!
}

input CreateStudentInput {
  name: String!
  department: String!
}

type Query {
  getStudent(id: ID!): Student
  getAllStudents: [Student]
}

type Mutation {
  createStudent(input: CreateStudentInput): Student
  deleteStudent(id: ID!): String
}
🔹 13. Mental Mapping
GraphQL	Java
type	Class/DTO
input	Request DTO
Query	GET
Mutation	POST/PUT/DELETE
Scalar	Primitive
!	@NotNull
[]	List
