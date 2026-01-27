erDiagram

    USER {
        int user_id PK
        string username
        string password
        string role
        string status
    }

    ADMIN {
        int admin_id PK
        int user_id FK
        string password
        string name
        date dob
    }

    STUDENT {
        int student_id PK
        string name
        string roll_no
        date dob
        string gender
        string email
        string phn
        string address
        int dept_id FK
        int semester
        int fees_id FK
        int user_id FK
        int course_id FK
        int atten_id FK
    }

    FACULTY {
        int faculty_id PK
        string name
        date dob
        string designation
        string email
        string phone
        string address
        date joining_date
        int dept_id FK
        int user_id FK
        int course_id FK
    }

    PARENTS {
        int parents_id PK
        string name
        string email
        string phn
        string relationship
        int student_id FK
        int user_id FK
    }

    LIBRARIAN {
        int librarian_id PK
        string name
        date dob
        string email
        string phn
        date joining_date
        int user_id FK
    }

    COURSE {
        int course_id PK
        string course_name
        int no_of_departments
        int duration
    }

    DEPARTMENT {
        int dept_id PK
        string dept_name
        int no_of_student
        int no_of_faculty
        int course_id FK
    }

    SUBJECT {
        int subject_id PK
        int course_id FK
        string name
        int dept_id FK
        int semester
        int credits
        string syllabus
    }

    TIMETABLE {
        int timetable_id PK
        int dept_id FK
        int faculty_id FK
        int semester
        string days_of_week
        string time_slot
        string classroom
        int subject_id FK
    }

    FACULTY_SCHEDULE {
        int fac_sche_id PK
        int faculty_id FK
        int subject_id FK
        string days_of_week
        int semester
        string time_slot
        string classroom
        int timetable_id FK
    }

    ATTENDANCE {
        int atten_id PK
        int student_id FK
        int subject_id FK
        date date
        int faculty_id FK
        string type
        string status
    }

    FEES {
        int fees_id PK
        int student_id FK
        int semester
        float amount
        string payment_status
        date payment_date
    }

    EXAM {
        int exam_id PK
        int subject_id FK
        string exam_type
        date exam_date
        string exam_time
        int total_marks
        string subject_name
    }

    RESULT {
        int result_id PK
        int exam_id FK
        int student_id FK
        int marks_obtained
    }

    LIBRARY_TRANSACTION {
        int lt_id PK
        string book_title
        int student_id FK
        int librarian_id FK
        date issue_date
        date due_date
        date return_date
        float fine_amt
    }

    USER ||--o| ADMIN : has
    USER ||--o| STUDENT : has
    USER ||--o| FACULTY : has
    USER ||--o| PARENTS : has
    USER ||--o| LIBRARIAN : has

    COURSE ||--o{ DEPARTMENT : contains
    COURSE ||--o{ SUBJECT : offers
    COURSE ||--o{ STUDENT : enrolled_in
    COURSE ||--o{ FACULTY : teaches

    DEPARTMENT ||--o{ STUDENT : has
    DEPARTMENT ||--o{ FACULTY : has
    DEPARTMENT ||--o{ SUBJECT : offers
    DEPARTMENT ||--o{ TIMETABLE : schedules

    FACULTY ||--o{ FACULTY_SCHEDULE : assigned
    FACULTY ||--o{ ATTENDANCE : marks

    STUDENT ||--o{ ATTENDANCE : records
    STUDENT ||--o{ FEES : pays
    STUDENT ||--o{ RESULT : gets
    STUDENT ||--o{ LIBRARY_TRANSACTION : borrows

    SUBJECT ||--o{ ATTENDANCE : tracked_for
    SUBJECT ||--o{ EXAM : evaluated_by
    SUBJECT ||--o{ FACULTY_SCHEDULE : scheduled

    EXAM ||--o{ RESULT : produces
    LIBRARIAN ||--o{ LIBRARY_TRANSACTION : manages
