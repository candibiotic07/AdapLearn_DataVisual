```mermaid
erDiagram
    %% Organizational Models
    User {
        ObjectId _id
        String username
        String password
        String firstName
        String lastName
        String role
        ObjectId instituteId
        String instituteName
        ObjectId branchId
        String branchName
        ObjectId batchId
        String batchName
        Boolean isActive
        String gender
        String email
        String mobile
    }
    
    %% Assessment Models
    Test {
        ObjectId _id
        String name
        Number duration
        Date startTime
        Date endTime
        Number totalQuestions
        Number totalMarks
        ObjectId courseId
        String courseName
    }
    
    QuestionV2 {
        ObjectId _id
        String type
        String question
        Array options
        Mixed answer
        String difficulty
        ObjectId courseId
        ObjectId subjectId
    }
    
    SubmitTest {
        ObjectId _id
        ObjectId testId
        ObjectId userId
        Array answers
        Number totalMarks
        Number obtainedMarks
    }
    
    %% Curriculum Hierarchy Models
    CourseV2 {
        ObjectId _id
        String name
    }
    
    SubjectV2 {
        ObjectId _id
        String name
        ObjectId courseId
    }
    
    ChapterV2 {
        ObjectId _id
        String name
        ObjectId subjectId
        ObjectId courseId
    }
    
    TopicV2 {
        ObjectId _id
        String name
        ObjectId chapterId
    }
    
    %% Assignment Models
    Assignment {
        ObjectId _id
        String name
        String description
        Date deadLine
        String scoreFormat
        Number totalMarks
        Array batches
        ObjectId courseId
        ObjectId subjectId
        ObjectId chapterId
        ObjectId topicId
    }
    
    AssignmentSubmission {
        ObjectId _id
        ObjectId assignmentId
        ObjectId studentId
        String attachmentUrl
        Number obtainedMarks
        String feedback
    }
    
    %% LMS Models
    LMSCourse {
        ObjectId _id
        String name
    }
    
    LMSSubject {
        ObjectId _id
        String name
        ObjectId courseId
    }
    
    LMSChapter {
        ObjectId _id
        String name
        ObjectId subjectId
        ObjectId courseId
    }
    
    LMSTopic {
        ObjectId _id
        String name
        ObjectId chapterId
        Number sequence
        Number materialCount
    }
    
    LMSSubTopic {
        ObjectId _id
        String name
        ObjectId topicId
        Number sequence
    }
    
    Material {
        ObjectId _id
        String title
        String description
        String type
        String url
        ObjectId courseId
        ObjectId subjectId
        ObjectId chapterId
        ObjectId topicId
        ObjectId subTopicId
    }
    
    %% Organization Hierarchy
    User }|--|| LMSCourse : "enrolls in"
    User }|--|| SubjectV2 : "studies"
    
    %% Assessment Relationships
    Test }|--|{ QuestionV2 : "contains"
    Test }|--|| CourseV2 : "belongs to"
    User }|--|{ SubmitTest : "submits"
    SubmitTest }|--|| Test : "for"
    
    %% Assignment Relationships
    Assignment }|--|| CourseV2 : "belongs to"
    Assignment }|--|| SubjectV2 : "belongs to"
    Assignment }|--|| ChapterV2 : "belongs to"
    Assignment }|--|| TopicV2 : "belongs to"
    User }|--|{ AssignmentSubmission : "submits"
    AssignmentSubmission }|--|| Assignment : "for"
    
    %% Curriculum Hierarchy Relationships
    CourseV2 ||--|{ SubjectV2 : "has"
    SubjectV2 ||--|{ ChapterV2 : "has"
    ChapterV2 ||--|{ TopicV2 : "has"
    
    %% LMS Hierarchy Relationships
    LMSCourse ||--|{ LMSSubject : "has"
    LMSSubject ||--|{ LMSChapter : "has"
    LMSChapter ||--|{ LMSTopic : "has"
    LMSTopic ||--|{ LMSSubTopic : "has"
    LMSTopic ||--|{ Material : "contains"
    LMSSubTopic ||--|{ Material : "contains" 
