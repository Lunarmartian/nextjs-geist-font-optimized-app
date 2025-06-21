# Cyber Triage Software - Technical Specification Document

## 1. Introduction
This document specifies the design and implementation plan for a comprehensive Cyber Triage Software platform. The software integrates multiple tools including a workspace, baselining tool, MFT (Master File Table) reader and extractor, user journal extractor and reader into a single unified platform.

## 2. Software Architecture

### 2.1 Overview
The software will follow a modular architecture with the following main components:
- **Workspace Module:** Central hub for managing investigations, case files, and data.
- **Baselining Tool:** Compares system states to identify anomalies.
- **MFT Reader and Extractor:** Parses and extracts data from NTFS Master File Table.
- **User Journal Extractor and Reader:** Extracts and interprets Windows User Journal data.
- **UI Layer:** Modern, responsive interface built with React and Tailwind CSS.
- **Backend Layer:** Node.js server handling file processing, data storage, and API endpoints.

### 2.2 Component Diagram
```
+-------------------+       +-------------------+
|                   |       |                   |
|   User Interface  <-------->  Backend API      |
|  (React + Tailwind)|       |  (Node.js + Express)|
|                   |       |                   |
+-------------------+       +-------------------+
          |                           |
          |                           |
          v                           v
+-------------------+       +-------------------+
| Workspace Module   |       | File Processing   |
| (Case Management)  |       | Modules           |
+-------------------+       +-------------------+
          |                           |
          |                           |
          v                           v
+-------------------+       +-------------------+
| Baselining Tool   |        | MFT Reader &      |
|                   |       | User Journal Tool |
+-------------------+       +-------------------+
```

## 3. Functionality

### 3.1 Workspace Module
- Create, open, and manage investigation cases.
- Store and organize extracted data and reports.
- User authentication and role management (optional for MVP).

### 3.2 Baselining Tool
- Capture system snapshots.
- Compare current system state against baseline.
- Highlight differences and anomalies.

### 3.3 MFT Reader and Extractor
- Parse NTFS Master File Table from disk images or raw files.
- Extract file metadata such as file names, timestamps, and attributes.
- Export extracted data in JSON or CSV format.

### 3.4 User Journal Extractor and Reader
- Extract Windows User Journal entries.
- Parse and display user activity logs.
- Support export and filtering of journal data.

## 4. User Interface Design

### 4.1 General Design Principles
- Clean, modern, and minimalistic UI.
- Responsive layout for desktop and tablets.
- Dark mode support.
- Use Tailwind CSS for styling.
- Use existing UI components for consistency.

### 4.2 Key Screens
- Dashboard: Overview of cases and recent activity.
- Case Workspace: Detailed view of a selected case with tabs for baselining, MFT data, and user journal.
- Baselining Tool: Interface to capture and compare system states.
- MFT Viewer: Table view with sorting and filtering capabilities.
- User Journal Viewer: Timeline or list view of user activities.

## 5. System Requirements and Dependencies

### 5.1 System Requirements
- Operating System: Windows 10/11 or Linux (for backend processing).
- Node.js v16 or higher.
- Sufficient disk space for storing case data and extracted files.

### 5.2 Dependencies
- Frontend:
  - React 18+
  - Tailwind CSS
  - Shadcn UI components (optional)
- Backend:
  - Node.js with Express
  - Libraries for parsing MFT (e.g., `mft-parser` or custom)
  - Libraries for reading Windows User Journal (e.g., `windows-journal-parser` or custom)
  - File upload and processing middleware

## 6. Implementation Steps

1. Setup project repository with frontend and backend structure.
2. Develop Workspace module with case management UI and backend APIs.
3. Implement Baselining tool with snapshot capture and comparison.
4. Develop MFT Reader and Extractor module.
5. Develop User Journal Extractor and Reader module.
6. Integrate all modules into unified UI.
7. Implement export and reporting features.
8. Testing and bug fixing.
9. Prepare deployment scripts and documentation.

## 7. Deployment

- Use Docker for containerized deployment (optional).
- Deploy backend on a Node.js server.
- Serve frontend as a static site or via Node.js server.
- Setup environment variables for configuration.
- Provide scripts for database setup if needed.

## 8. Code Snippets

### 8.1 Example: MFT Parsing (Node.js)
```javascript
const fs = require('fs');
const MFTParser = require('mft-parser');

async function parseMFT(filePath) {
  const buffer = fs.readFileSync(filePath);
  const mft = new MFTParser(buffer);
  const records = mft.parse();
  return records;
}
```

### 8.2 Example: React Component for Case List
```tsx
import React from 'react';

interface Case {
  id: string;
  name: string;
  createdAt: string;
}

const CaseList: React.FC<{ cases: Case[] }> = ({ cases }) => {
  return (
    <div className="p-4">
      <h2 className="text-xl font-bold mb-4">Cases</h2>
      <ul>
        {cases.map((c) => (
          <li key={c.id} className="border-b py-2">
            {c.name} - {new Date(c.createdAt).toLocaleDateString()}
          </li>
        ))}
      </ul>
    </div>
  );
};

export default CaseList;
```

## 9. Diagrams and Illustrations

- Architecture diagram as shown in section 2.2.
- UI wireframes can be created using tools like Figma or Sketch (not included here).

---

This document provides a comprehensive overview and plan for the cyber triage software platform. Upon your confirmation, I can proceed with implementation of the modules step-by-step.
