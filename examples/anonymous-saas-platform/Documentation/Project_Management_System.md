# Project Management System

**Core system for organizing tasks and team collaboration**

## 📋 Quick Context

**Purpose:** Enables teams to create projects, assign tasks, and track progress

**Key Files:**
- `backend/src/controllers/ProjectController.ts` - Project CRUD operations
- `backend/src/services/TaskService.ts` - Task business logic
- `frontend/src/components/ProjectBoard.tsx` - Main UI component

**Common Issues:**
- Permission checks required for all operations
- Task status transitions must follow workflow rules
- Real-time updates via WebSocket for team sync

---

## 🎯 How It Works

### User Perspective
**What users do:**
1. Create a project with name and description
2. Add team members with specific roles
3. Create tasks within projects
4. Assign tasks to team members
5. Track progress on project board

**What users see:**
- Project dashboard with all projects
- Kanban board for task visualization
- Real-time updates when others make changes
- Activity feed showing team actions

### System Perspective
**Internal workflow:**
1. User creates project → API validates permissions
2. System creates project record → Assigns creator as owner
3. Project appears in user's dashboard → Team members notified
4. Tasks created within project → Status tracking begins

**Data flow:**
```
User Action → Controller → Service Layer → Database → WebSocket Update → UI Refresh
```

---

## 🏗️ Technical Architecture

### Core Components

#### ProjectController
- **Location:** `backend/src/controllers/ProjectController.ts`
- **Responsibility:** Handle HTTP requests for projects
- **Key Methods:**
  - `createProject()` - Creates new project
  - `getProjects()` - Lists user's projects
  - `updateProject()` - Modifies project details
  - `deleteProject()` - Archives project

#### TaskService
- **Location:** `backend/src/services/TaskService.ts`
- **Responsibility:** Business logic for tasks
- **Key Methods:**
  - `assignTask()` - Assigns task with permission check
  - `updateStatus()` - Validates status transitions
  - `notifyAssignee()` - Sends notifications

### Database Schema

**Tables:**
- `projects`
  - Fields: id, name, description, owner_id, team_id, created_at
  - Indexes: owner_id, team_id
  - Relations: belongs to team, has many tasks

- `tasks`
  - Fields: id, title, description, status, assigned_to, project_id
  - Indexes: project_id, assigned_to, status
  - Relations: belongs to project, assigned to user

### API Endpoints

**POST /api/projects**
- **Purpose:** Create new project
- **Auth:** Required (JWT)
- **Request:** `{ name, description, team_id }`
- **Response:** `{ project: {...}, success: true }`
- **Errors:** 401 (unauthorized), 403 (no team access)

---

## 💻 Development Context

### Implementation Patterns
```typescript
// Pattern: Service layer for business logic
class TaskService {
  async assignTask(taskId: string, userId: string, assignerId: string) {
    // 1. Validate permissions
    await this.checkAssignPermission(assignerId, taskId);
    
    // 2. Update task
    const task = await prisma.task.update({
      where: { id: taskId },
      data: { assigned_to: userId }
    });
    
    // 3. Send notification
    await notificationService.notify(userId, `Task assigned: ${task.title}`);
    
    return task;
  }
}
```

### Testing Strategy
**Unit Tests:**
- Location: `backend/src/services/__tests__/TaskService.test.ts`
- Coverage: Business logic, permission checks
- Run: `npm test TaskService`

**Integration Tests:**
- Location: `backend/src/__tests__/integration/projects.test.ts`
- Scenarios: Full CRUD workflows
- Run: `npm test:integration`

---

## 🔒 Security

### Authentication/Authorization
- JWT tokens validated on every request
- Permission model: Owner > Admin > Member
- Task assignment requires admin/owner role

### Input Validation
- Zod schemas for all API inputs
- SQL injection prevention via Prisma ORM
- XSS protection via sanitization

---

## 📊 Performance Considerations

- Database queries optimized with indexes on foreign keys
- WebSocket updates batched to reduce traffic
- Project list paginated (20 per page)

---

**Last Updated:** 2025-10-10
