# Payment Refund API Ingestion & Automation

## Overview

This repository demonstrates a repeatable workflow to streamline API discovery, collection generation, and environment setup in Postman for the **Payment Refund API**.  

**Problem:**  
A senior engineer spent 47 minutes integrating the refund API, jumping across 6 systems, hitting 3 dead ends, and relying on a personal workspace example.

**Solution:**  
Automated pipeline using **GitHub Actions** to:  
1. Push OpenAPI spec to Postman API Hub  
2. Generate Postman collection from spec  
3. Set up environments (Dev, QA, UAT, Prod)  
4. Inject JWT authorization for internal calls  
5. Trigger collection tests automatically  

**Outcome:**  
Reduces discovery time from **47 minutes → seconds**, ensures consistent environments, and makes the workflow repeatable across other APIs.

---

## Repository Structure

postman-refund-api-ingestion/ 
	.github/workflows/ 		
		sync-refund-api.yml 	 
	specs/
 		 payment-refund-api-openapi.yaml
	 postman/environments/
 		dev.json
 		qa.json
 		uat.json
 		prod.json
 	README.md
---

## Getting Started

### Prerequisites
- GitHub repository with secrets configured:
  - `POSTMAN_API_KEY`
  - `POSTMAN_SPEC_ID`
  - `POSTMAN_COLLECTION_ID`
  - `BASE_URL_DEV`, `BASE_URL_QA`, `BASE_URL_UAT`, `BASE_URL_PROD`
- Node.js & npm installed (for local CLI testing)
- Postman account with API access

## GitHub Actions Workflow
The workflow triggers on any update to specs/*.yaml or specs/*.json files.
Steps
	1.	Checkout repo
	2.	Update Postman Spec
	3.	Regenerate Collection
	4.	Run Collection Tests against environment (mock or real) 

## Environments

	•	Environments are defined in postman/environments/ with placeholders for:
		◦	Dev
		◦	QA
		◦	UAT
		◦	Prod
	•	Each environment contains a baseUrl variable pointing to the respective mock or real server.
	•	JWT authentication can be implemented in the pre-request scripts; secrets are injected dynamically. 

## ROI calculation

I am assuming each engineer uses all 15 APIs 1 per quarter or 4 times per year. 
•	Pre-automation: 47 min per API
14 engineers × 15 APIs × .7833hr (47 minutes) × $150hr ≈ $24,675 per quarter or $98,700 per year. 

•	Post-automation: < 1 min
14 engineers × 15 APIs × .0167hr (1 minutes) × $150hr ≈ $525 per quarter or $2,100 per year. 

Total amount saved $98,700 - $2,100 = $96,600 per year. 

## Scaling strategy 
	1.	Maintain single source of truth in specs/ folder.
	2.	Generate and update collections automatically via workflow.
	3.	Store environment variables consistently (postman/environments/)
	4.	Establish workspace governance:
		◦	Naming conventions
		◦	Ownership & permissions
	5.	Automate retrieval of updated specs from AWS or GitHub
	6.	Phase rollout:
		◦	Next sprint: 5 APIs
		◦	 Following sprint: 10 APIs
	◦	Remaining 31 APIs: subsequent sprint
	◦	 Target completion: 6 weeks 

## Notes

	•	JWT auth is implemented in pre-request scripts. 
	•	Workflow can run on mock servers for testing before pushing to real environments.
	•	Changes in the spec automatically trigger updates to Postman collections.
	•	The same workflow can be applied to other APIs for repeatable, automated integration. 

Contact / Support
For questions about this repository or workflow, please contact the CSE team - Thomas Power tpower034@gmail.com
—
