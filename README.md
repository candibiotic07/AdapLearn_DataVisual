# Database Schema Visualizations

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