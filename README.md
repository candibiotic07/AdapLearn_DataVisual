# Adaptive Learning System - Data Schema Documentation

This directory contains visual representations of the Adaptive Learning system's database schema and relationships.

## Files Included

1. **database_schema.md** - Entity-Relationship Diagram (ERD) showing database models and their relationships
2. **hierarchical_view.md** - Tree visualization of the hierarchical structure of the system components
3. **data_flow.md** - Flowchart showing the data flow between different actors and components in the system

## System Architecture Overview

The Adaptive Learning system is built on MongoDB (using Mongoose for schema definitions) and is organized into four main modules that work together to create a comprehensive educational platform.

### 1. User Management Module

The User module handles authentication, authorization, and user profiles with a hierarchical organizational structure:

- **User Model**: Central user schema with multiple roles (student, teacher, admin)
  - Student profiles include batch information, admission details, and academic records
  - Teacher profiles include department, designation, and expertise information
  - Admin profiles include management permissions and scope (institute/branch level)

- **Organizational Hierarchy**:
  - Institute → Branch → Batch → Student
  - Institute → Department → Teacher

### 2. Assessment Module

The Assessment module manages all testing-related functionality:

- **Test Model**: Defines test configuration
  - Test metadata (name, duration, start/end times, instructions)
  - Structure (subjects, sections, question distribution)
  - Security settings (password protection, time limits)
  
- **Question Model (QuestionV2)**:
  - Question content (text, options, assets)
  - Metadata (type, difficulty, marks, topics)
  - Answer key and solution information
  
- **Test Submission Model (SubmitTest)**:
  - Student responses to test questions
  - Scoring data (obtained marks, section-wise performance)
  - Analytics information (time taken, attempt patterns)

- **Assessment Content Hierarchy**:
  - Course → Subject → Chapter → Unit → Topic
  - Used for organizing questions and aligning with curriculum

### 3. Assignment Module

The Assignment module handles homework and project-based assessments:

- **Assignment Model**: Defines assigned tasks
  - Assignment details (name, description, deadline)
  - Scoring format (marks or grades)
  - Content references (subject, chapter, topic alignment)
  - Distribution settings (batches assigned to)

- **Assignment Submission Model**:
  - Student work submissions (attachments, text responses)
  - Evaluation data (obtained marks, feedback)
  - Submission metadata (timestamp, status)

### 4. Learning Management System (LMS) Module

The LMS module organizes educational content in a structured manner:

- **LMS Content Hierarchy**:
  - Course → Subject → Chapter → Topic → SubTopic
  - Parallel to assessment hierarchy but focused on learning materials
  
- **Material Model**: Learning resources
  - Content metadata (title, description, type)
  - Storage information (URL, attachments)
  - Classification tags (difficulty, recommended sequence)
  - Association with curriculum points (topic, subtopic)

## Data Relationships and Flow

### Key Relationships

1. **Cross-Module References**:
   - Users reference organizational entities (Institute, Branch, Batch)
   - Tests reference curriculum entities (Course, Subject)
   - Materials reference LMS hierarchy entities (Topic, SubTopic)
   - Assignments reference both curriculum and organizational entities

2. **Submission Workflows**:
   - Student → Test → Test Submission → Analytics
   - Student → Assignment → Assignment Submission → Feedback

3. **Content Organization**:
   - Parallel hierarchies in Assessment (CourseV2, etc.) and LMS (LMSCourse, etc.)
   - Materials linked to specific points in learning hierarchy

### Data Flow Processes

1. **Content Creation & Assignment**:
   - Teachers/Admins create learning materials and assessments
   - Content is organized in hierarchical structures
   - Materials and assessments are assigned to specific batches/students

2. **Learning & Assessment Process**:
   - Students access assigned learning materials
   - Students complete tests and assignments
   - Submissions are recorded and evaluated

3. **Analytics & Adaptation**:
   - Performance data is analyzed
   - Insights inform content adaptation
   - Personalized learning paths are created

## MongoDB Implementation Details

The system uses MongoDB's document-oriented approach with the following patterns:

1. **Reference Documents**: Using ObjectId references between collections
2. **Embedded Documents**: Using nested schemas for related data
3. **Denormalization**: Storing redundant data (e.g., names along with IDs) for performance

Each schema follows consistent patterns with:
- Metadata fields (name, description)
- Reference fields (linking to other documents)
- Content fields (actual educational material)
- Analytics fields (usage statistics, performance metrics)
- Administrative fields (creation, modification timestamps, deletion flags)

## Technical Architecture

The database schemas reflect a modular architecture designed to support:

1. **Scalability**: Independent scaling of different components
2. **Flexibility**: Support for diverse educational content and assessment types
3. **Analytics**: Rich data collection for performance analysis
4. **Personalization**: Data structures enabling adaptive learning paths
5. **Multi-tenancy**: Institution and branch-level isolation of data # Database Schema Visualizations

This directory contains visual representations of the Adaptive Learning system's database schema and relationships.

## Files Included

1. **database_schema.md** - Entity-Relationship Diagram (ERD) showing database models and their relationships
2. **hierarchical_view.md** - Tree visualization of the hierarchical structure of the system components
3. **data_flow.md** - Flowchart showing the data flow between different actors and components in the system

## How to View These Diagrams

These diagrams are written in Mermaid markdown syntax. To view them:

1. **GitHub**: If you push these files to GitHub, they will automatically render the Mermaid diagrams
2. **VS Code**: Install the "Markdown Preview Mermaid Support" extension in VS Code
3. **Online Mermaid Editor**: Copy the content between the mermaid code fences and paste it into [Mermaid Live Editor](https://mermaid.live/)
4. **Browser Extensions**: Various browser extensions can render Mermaid diagrams in markdown files

## System Overview

The Adaptive Learning system has four main components:

1. **User Management** - Handles users, roles, institute hierarchy, and student-teacher relationships
2. **Assessment Module** - Manages tests, questions, and test submissions
3. **Assignment Module** - Handles assignments and student submissions
4. **Learning Management System (LMS)** - Organizes learning content in a hierarchical structure

Each module contains its own data models, but they are interconnected through references (MongoDB ObjectIds) to create a complete educational ecosystem. 
