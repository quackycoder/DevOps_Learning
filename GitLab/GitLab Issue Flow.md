GitLab Issue Flow

### Introduction
Let’s walk through the location and anatomy of an issue and how to use it to plan projects.

### Step1: Create and Discuss a New Issue
1. List itemTeam creates an issue
  
2. Team applies “Discussion” label
    
3. Team discusses using Comments

### Step2: Code Creation 
    
1. Backend team starts work and developer      starts writing code 
    
2. Developer assigns issue to themselves
    
3. Developer adds “Working on” label

### Commit and Merge Request
    
1. Developer creates Commits

    
1. Developer pushes commits to a feature-      branch

    
1. Developer creates a Merge Request (MR)

    
1. Backend team changes labels to            	“Frontend”

### Deploy to Staging
    
1. Frontend developer starts working on issue

    
1. Developer assigns issue to themselves

    
1. Developer adds “Working on” label 

    
1. Team reviews and refines code

    
1. Team stages code

    
1. Team changes label to “Staging” 

    
1. After successful implementation team changes label to “Ready”

### Ready
    
1. Technical documentation team adds "Docs" label

    
1. Marketing team adds “Marketing" label

    
1. Technical team removes "Docs" label when done

    
1. When done, the marketing team removes “Marketing” label and adds “Production” label

### Deploy to Production
    
1. Release team merges MR and deploys feature to production 

    
1. Release team closes issue

### Summary
This example shows how each change, no matter how small, starts with an issue. Something as small as a discussion can lead to larger beneficial changes in the organization. 
