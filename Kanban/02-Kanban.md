# Kanban - BOC OM

```mermaid
kanban
  backlog[Backlog]

  todo[To Do]
	  uc04[Edit Report]@{priority: 'Low'}
	  uc05[Sign Report]@{priority: 'Low'}
	  uc07[Review QPI]@{priority: 'High'}
	  uc08[Review Summary]@{priority: 'High'}
	  
  inprogress["In Progress (2)"]
	  uc03["Review Report (Start: 13/10)"]@{priority: 'High'}	
	  uc06["Generate PDF (Start: 13/10)"]@{priority: 'High'}  

  done[Done]
	  uc01["Login (End: 15/09)"]@{priority: 'High'}
	  uc02["Submit Report (End: 13/10)"]@{priority: 'High'}	  
	  uc09["Manage User (End: 25/09)"]@{priority: 'Low'}
	  uc10["Manage Role (End: 06/10)"]@{priority: 'Low'}
	  uc11["Manage Area of Work (End: 01/10)"]@{priority: 'High'}
	  uc12["Manage Equipment Category (End: 01/10)"]@{priority: 'High'}
	  uc13["Manage Functional Location (End: 02/10)"]@{priority: 'High'}
	  uc14["Manage Tank Type (End: 02/10)"]@{priority: 'High'}
	  uc15["Manage Service (End: 02/10)"]@{priority: 'Low'}
	  uc16["Manage Tank Component Group (End: 02/10)"]@{priority: 'High'}
	  uc17["Manage Tank Component (End: 02/10)"]@{priority: 'High'}
	  uc18["Manage Report Category (End: 06/10)"]@{priority: 'High'}
	  uc19["Manage Tank Component Reading (End: 08/10)"]@{priority: 'Low'}
```
