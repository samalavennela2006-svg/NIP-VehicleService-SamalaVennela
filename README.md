# Vehicle Service Management Application

## Pega National Internship Program (NIP)

A Pega-based Vehicle Service Management Application developed as part of the Pega National Internship Program.

---

## Project Details

| Detail | Information |
|---|---|
| Student Name | Samala Vennela |
| College | ACE Engineering College |
| Course | CSE |
| Project | Vehicle Service Management Application |
| Pega Application | NIP-VehicleService-SamalaVennela |
| Case Type | Vehicle Service Request |
| Platform | Pega Platform |

---

## Project Overview

The Vehicle Service Management Application is designed to manage vehicle service requests from submission to completion.

The application allows a customer to submit a vehicle service request, enables a Service Advisor to inspect the vehicle and generate an estimate, allows the customer to approve or reject the estimate, and automatically routes approved requests to the appropriate technician work queue.

---

## Case Lifecycle

The application follows four main stages:

1. Request Intake
2. Inspection
3. Approval
4. Service Execution

### Workflow

```text
Customer
   ↓
Request Intake
   ↓
Vehicle Inspection
   ↓
Service Estimate
   ↓
Customer Approval
   ↓
Route by Vehicle Type
   ↓
Technician Service Execution
   ↓
Service Completion
   ↓
Customer Notification
   ↓
Resolved-Completed

Main Features
1. Submit Vehicle Service Request

The customer can create a Vehicle Service Request by entering vehicle information and describing the service issue.

The request includes:

Vehicle
Vehicle Type
Issue Description

Required fields are validated before the case can be submitted.

2. Perform Vehicle Inspection

The Service Advisor performs the vehicle inspection and records:

Inspection Notes
Condition Rating

The inspection must be completed before moving forward to estimate generation.

3. Generate Service Estimate

The Service Advisor enters:

Labor Cost
Parts Cost

The application calculates the Total Cost automatically.

Total Cost = Labor Cost + Parts Cost

The calculation is implemented using the CalculateTotalCost Data Transform.

4. Approve Service Estimate

The Approval stage is assigned to the Customer.

The customer can:

Approve the service estimate
Reject the service estimate

Approved requests continue to Service Execution, while rejected requests follow the rejection path.

5. Maintain Vehicle Data

A reusable Vehicle data object was created with the following properties:

Vehicle ID
Model
Type

The Vehicle data object is linked to the Vehicle Service Request case and can be reused across multiple service requests.

6. Review Service Estimate

The customer can review the service estimate before making an approval decision.

The approval screen displays:

Labor Cost
Parts Cost
Total Cost

This provides the customer with visibility into the service estimate before approving or rejecting the request.

7. Automatically Assign Technician

The Service Execution stage contains routing and technician assignment.

The case is automatically routed based on the Vehicle Type.

Heavy vehicles → HeavyVehicleQueue
Other vehicle types → LightVehicleQueue

The application also maintains Assigned Technician and Service Status properties.

8. Notify Service Completion

A Correspondence rule named ServiceCompletionNotification is used to send an email when the service case reaches Resolved-Completed.

The notification includes relevant information such as:

Vehicle ID
Vehicle Model
Service Summary
Total Cost
9. Define Service SLA

A Service Level Agreement is configured for the Vehicle Service Request case.

SLA Configuration	Value
Goal	2 days
Deadline	3 days
Deadline Breach	Urgency increases

The SLA helps ensure that service requests are completed within the defined time period.

10. Route by Vehicle Type

The application uses a Data Transform named RouteByVehicleType to automatically route cases according to Vehicle Type.

Vehicle Type	Work Queue
Heavy	HeavyVehicleQueue
Other Types	LightVehicleQueue

This removes the need for manual queue selection.

Personas

The application uses the following personas:

Customer

The Customer can:

Create a Vehicle Service Request
Review the service estimate
Approve or reject the service estimate
Work Portal

The Work Portal persona covers internal staff roles such as:

Service Advisor
Technician

These users process and complete the service request.

Work Queues
HeavyVehicleQueue

Used when the Vehicle Type is Heavy.

LightVehicleQueue

Used for all other non-heavy vehicle types.

The routing is performed automatically based on the Vehicle Type property.

Rules Created or Modified
Rule Name	Rule Type
CalculateTotalCost	Data Transform
ServiceCompletionNotification	Correspondence (Email)
RouteByVehicleType	Data Transform
Total Cost Calculation

The CalculateTotalCost Data Transform calculates the total service cost.

Properties Used
.LaborCost
.PartsCost
.TotalCost
Formula
.TotalCost = .LaborCost + .PartsCost

The calculation is performed after the Labor Cost and Parts Cost values are entered.

Vehicle-Type Routing

The RouteByVehicleType Data Transform checks the Vehicle Type and routes the case automatically.

If Vehicle Type = Heavy
        ↓
HeavyVehicleQueue

Otherwise
        ↓
LightVehicleQueue

This helps ensure that service requests reach the appropriate team without requiring manual queue selection.

Service Completion Notification

The application contains a Correspondence rule:

ServiceCompletionNotification

The notification is triggered when the case reaches:

Resolved-Completed

The email contains relevant vehicle and service information to keep the customer informed about service completion.

Service Level Agreement

The Vehicle Service Request case has the following SLA configuration:

Goal      : 2 Days
Deadline  : 3 Days

If the deadline is missed, the case urgency is automatically increased.

Design Decisions
1. Data Transform for Total Cost

A Data Transform named CalculateTotalCost is used to calculate Total Cost from Labor Cost and Parts Cost.

This provides explicit control over when the calculation is executed after the cost values are entered.

2. Automatic Vehicle-Type Routing

A Data Transform named RouteByVehicleType automatically routes cases to HeavyVehicleQueue or LightVehicleQueue based on Vehicle Type.

This reduces manual selection and helps ensure that heavy vehicle requests reach the appropriate team.

Case Flow

The complete case flow is:

Customer creates a Vehicle Service Request.
Customer enters Vehicle, Vehicle Type, and Issue Description.
The Service Advisor performs the vehicle inspection.
Inspection Notes and Condition Rating are recorded.
Labor Cost and Parts Cost are entered.
Total Cost is calculated.
Customer reviews the service estimate.
Customer approves or rejects the estimate.
Approved cases move to Service Execution.
The case is routed based on Vehicle Type.
The technician updates the Service Status.
Service is completed.
A completion notification is sent to the customer.
The case reaches Resolved-Completed.
Challenges and Solution

One of the challenges during development was a Failed to find instance error while sending the service completion email.

The Send Email step referenced the correspondence rule using a display name with spaces, while the actual rule identifier was:

ServiceCompletionNotification

The reference was corrected to match the exact rule identifier.

A second issue was related to the development branch and operator access. The fix was merged into the main VehicleS ruleset so that it was available to the required operators.

Project Screenshots

The repository contains screenshots from the completed Pega application.

US-001 — Submit Vehicle Service Request

US-002 — Perform Vehicle Inspection

US-003 — Generate Service Estimate

US-004 — Approve Service Estimate

The submitted project documentation contains additional user-story evidence and implementation details.

User Stories Covered

The project submission covers the following user stories:

ID	User Story
US-001	Submit Vehicle Service Request
US-002	Perform Vehicle Inspection
US-003	Generate Service Estimate
US-004	Approve Service Estimate
US-005	Maintain Vehicle Data
US-006	Review Service Estimate
US-007	Auto Assign Technician
US-008	Notify Service Completion
US-009	Define Service SLA
US-010	Route by Vehicle Type
Project Documentation

The complete project submission document contains:

Project details
User story requirements
Pega screenshots
Application configuration details
Rule information
Case flow
Design decisions
Challenges and solutions
Personas
Work queues

The submitted documentation is included in this repository under the Documentation folder.

Demo

The project demo video will be added here once available.

Demo Video: To be added
Project Status

Completed and submitted as part of the Pega National Internship Program.

The project documentation and available Pega screenshots are included in this repository.

Author

Samala Vennela

ACE EnginMain Features
1. Submit Vehicle Service Request

The customer can create a Vehicle Service Request by entering vehicle information and describing the service issue.

The request includes:

Vehicle
Vehicle Type
Issue Description

Required fields are validated before the case can be submitted.

2. Perform Vehicle Inspection

The Service Advisor performs the vehicle inspection and records:

Inspection Notes
Condition Rating

The inspection must be completed before moving forward to estimate generation.

3. Generate Service Estimate

The Service Advisor enters:

Labor Cost
Parts Cost

The application calculates the Total Cost automatically.

Total Cost = Labor Cost + Parts Cost

The calculation is implemented using the CalculateTotalCost Data Transform.

4. Approve Service Estimate

The Approval stage is assigned to the Customer.

The customer can:

Approve the service estimate
Reject the service estimate

Approved requests continue to Service Execution, while rejected requests follow the rejection path.

5. Maintain Vehicle Data

A reusable Vehicle data object was created with the following properties:

Vehicle ID
Model
Type

The Vehicle data object is linked to the Vehicle Service Request case and can be reused across multiple service requests.

6. Review Service Estimate

The customer can review the service estimate before making an approval decision.

The approval screen displays:

Labor Cost
Parts Cost
Total Cost

This provides the customer with visibility into the service estimate before approving or rejecting the request.

7. Automatically Assign Technician

The Service Execution stage contains routing and technician assignment.

The case is automatically routed based on the Vehicle Type.

Heavy vehicles → HeavyVehicleQueue
Other vehicle types → LightVehicleQueue

The application also maintains Assigned Technician and Service Status properties.

8. Notify Service Completion

A Correspondence rule named ServiceCompletionNotification is used to send an email when the service case reaches Resolved-Completed.

The notification includes relevant information such as:

Vehicle ID
Vehicle Model
Service Summary
Total Cost
9. Define Service SLA

A Service Level Agreement is configured for the Vehicle Service Request case.

SLA Configuration	Value
Goal	2 days
Deadline	3 days
Deadline Breach	Urgency increases

The SLA helps ensure that service requests are completed within the defined time period.

10. Route by Vehicle Type

The application uses a Data Transform named RouteByVehicleType to automatically route cases according to Vehicle Type.

Vehicle Type	Work Queue
Heavy	HeavyVehicleQueue
Other Types	LightVehicleQueue

This removes the need for manual queue selection.

Personas

The application uses the following personas:

Customer

The Customer can:

Create a Vehicle Service Request
Review the service estimate
Approve or reject the service estimate
Work Portal

The Work Portal persona covers internal staff roles such as:

Service Advisor
Technician

These users process and complete the service request.

Work Queues
HeavyVehicleQueue

Used when the Vehicle Type is Heavy.

LightVehicleQueue

Used for all other non-heavy vehicle types.

The routing is performed automatically based on the Vehicle Type property.

Rules Created or Modified
Rule Name	Rule Type
CalculateTotalCost	Data Transform
ServiceCompletionNotification	Correspondence (Email)
RouteByVehicleType	Data Transform
Total Cost Calculation

The CalculateTotalCost Data Transform calculates the total service cost.

Properties Used
.LaborCost
.PartsCost
.TotalCost
Formula
.TotalCost = .LaborCost + .PartsCost

The calculation is performed after the Labor Cost and Parts Cost values are entered.

Vehicle-Type Routing

The RouteByVehicleType Data Transform checks the Vehicle Type and routes the case automatically.

If Vehicle Type = Heavy
        ↓
HeavyVehicleQueue

Otherwise
        ↓
LightVehicleQueue

This helps ensure that service requests reach the appropriate team without requiring manual queue selection.

Service Completion Notification

The application contains a Correspondence rule:

ServiceCompletionNotification

The notification is triggered when the case reaches:

Resolved-Completed

The email contains relevant vehicle and service information to keep the customer informed about service completion.

Service Level Agreement

The Vehicle Service Request case has the following SLA configuration:

Goal      : 2 Days
Deadline  : 3 Days

If the deadline is missed, the case urgency is automatically increased.

Design Decisions
1. Data Transform for Total Cost

A Data Transform named CalculateTotalCost is used to calculate Total Cost from Labor Cost and Parts Cost.

This provides explicit control over when the calculation is executed after the cost values are entered.

2. Automatic Vehicle-Type Routing

A Data Transform named RouteByVehicleType automatically routes cases to HeavyVehicleQueue or LightVehicleQueue based on Vehicle Type.

This reduces manual selection and helps ensure that heavy vehicle requests reach the appropriate team.

Case Flow

The complete case flow is:

Customer creates a Vehicle Service Request.
Customer enters Vehicle, Vehicle Type, and Issue Description.
The Service Advisor performs the vehicle inspection.
Inspection Notes and Condition Rating are recorded.
Labor Cost and Parts Cost are entered.
Total Cost is calculated.
Customer reviews the service estimate.
Customer approves or rejects the estimate.
Approved cases move to Service Execution.
The case is routed based on Vehicle Type.
The technician updates the Service Status.
Service is completed.
A completion notification is sent to the customer.
The case reaches Resolved-Completed.
Challenges and Solution

One of the challenges during development was a Failed to find instance error while sending the service completion email.

The Send Email step referenced the correspondence rule using a display name with spaces, while the actual rule identifier was:

ServiceCompletionNotification

The reference was corrected to match the exact rule identifier.

A second issue was related to the development branch and operator access. The fix was merged into the main VehicleS ruleset so that it was available to the required operators.

Project Screenshots

The repository contains screenshots from the completed Pega application.

US-001 — Submit Vehicle Service Request

US-002 — Perform Vehicle Inspection

US-003 — Generate Service Estimate

US-004 — Approve Service Estimate

The submitted project documentation contains additional user-story evidence and implementation details.

User Stories Covered

The project submission covers the following user stories:

ID	User Story
US-001	Submit Vehicle Service Request
US-002	Perform Vehicle Inspection
US-003	Generate Service Estimate
US-004	Approve Service Estimate
US-005	Maintain Vehicle Data
US-006	Review Service Estimate
US-007	Auto Assign Technician
US-008	Notify Service Completion
US-009	Define Service SLA
US-010	Route by Vehicle Type
Project Documentation

The complete project submission document contains:

Project details
User story requirements
Pega screenshots
Application configuration details
Rule information
Case flow
Design decisions
Challenges and solutions
Personas
Work queues

The submitted documentation is included in this repository under the Documentation folder.

Demo

The project demo video will be added here once available.

Demo Video: To be added
Project Status

Completed and submitted as part of the Pega National Internship Program.

The project documentation and available Pega screenshots are included in this repository.

Author

Samala Vennela

ACE EnginMain Features
1. Submit Vehicle Service Request

The customer can create a Vehicle Service Request by entering vehicle information and describing the service issue.

The request includes:

Vehicle
Vehicle Type
Issue Description

Required fields are validated before the case can be submitted.

2. Perform Vehicle Inspection

The Service Advisor performs the vehicle inspection and records:

Inspection Notes
Condition Rating

The inspection must be completed before moving forward to estimate generation.

3. Generate Service Estimate

The Service Advisor enters:

Labor Cost
Parts Cost

The application calculates the Total Cost automatically.

Total Cost = Labor Cost + Parts Cost

The calculation is implemented using the CalculateTotalCost Data Transform.

4. Approve Service Estimate

The Approval stage is assigned to the Customer.

The customer can:

Approve the service estimate
Reject the service estimate

Approved requests continue to Service Execution, while rejected requests follow the rejection path.

5. Maintain Vehicle Data

A reusable Vehicle data object was created with the following properties:

Vehicle ID
Model
Type

The Vehicle data object is linked to the Vehicle Service Request case and can be reused across multiple service requests.

6. Review Service Estimate

The customer can review the service estimate before making an approval decision.

The approval screen displays:

Labor Cost
Parts Cost
Total Cost

This provides the customer with visibility into the service estimate before approving or rejecting the request.

7. Automatically Assign Technician

The Service Execution stage contains routing and technician assignment.

The case is automatically routed based on the Vehicle Type.

Heavy vehicles → HeavyVehicleQueue
Other vehicle types → LightVehicleQueue

The application also maintains Assigned Technician and Service Status properties.

8. Notify Service Completion

A Correspondence rule named ServiceCompletionNotification is used to send an email when the service case reaches Resolved-Completed.

The notification includes relevant information such as:

Vehicle ID
Vehicle Model
Service Summary
Total Cost
9. Define Service SLA

A Service Level Agreement is configured for the Vehicle Service Request case.

SLA Configuration	Value
Goal	2 days
Deadline	3 days
Deadline Breach	Urgency increases

The SLA helps ensure that service requests are completed within the defined time period.

10. Route by Vehicle Type

The application uses a Data Transform named RouteByVehicleType to automatically route cases according to Vehicle Type.

Vehicle Type	Work Queue
Heavy	HeavyVehicleQueue
Other Types	LightVehicleQueue

This removes the need for manual queue selection.

Personas

The application uses the following personas:

Customer

The Customer can:

Create a Vehicle Service Request
Review the service estimate
Approve or reject the service estimate
Work Portal

The Work Portal persona covers internal staff roles such as:

Service Advisor
Technician

These users process and complete the service request.

Work Queues
HeavyVehicleQueue

Used when the Vehicle Type is Heavy.

LightVehicleQueue

Used for all other non-heavy vehicle types.

The routing is performed automatically based on the Vehicle Type property.

Rules Created or Modified
Rule Name	Rule Type
CalculateTotalCost	Data Transform
ServiceCompletionNotification	Correspondence (Email)
RouteByVehicleType	Data Transform
Total Cost Calculation

The CalculateTotalCost Data Transform calculates the total service cost.

Properties Used
.LaborCost
.PartsCost
.TotalCost
Formula
.TotalCost = .LaborCost + .PartsCost

The calculation is performed after the Labor Cost and Parts Cost values are entered.

Vehicle-Type Routing

The RouteByVehicleType Data Transform checks the Vehicle Type and routes the case automatically.

If Vehicle Type = Heavy
        ↓
HeavyVehicleQueue

Otherwise
        ↓
LightVehicleQueue

This helps ensure that service requests reach the appropriate team without requiring manual queue selection.

Service Completion Notification

The application contains a Correspondence rule:

ServiceCompletionNotification

The notification is triggered when the case reaches:

Resolved-Completed

The email contains relevant vehicle and service information to keep the customer informed about service completion.

Service Level Agreement

The Vehicle Service Request case has the following SLA configuration:

Goal      : 2 Days
Deadline  : 3 Days

If the deadline is missed, the case urgency is automatically increased.

Design Decisions
1. Data Transform for Total Cost

A Data Transform named CalculateTotalCost is used to calculate Total Cost from Labor Cost and Parts Cost.

This provides explicit control over when the calculation is executed after the cost values are entered.

2. Automatic Vehicle-Type Routing

A Data Transform named RouteByVehicleType automatically routes cases to HeavyVehicleQueue or LightVehicleQueue based on Vehicle Type.

This reduces manual selection and helps ensure that heavy vehicle requests reach the appropriate team.

Case Flow

The complete case flow is:

Customer creates a Vehicle Service Request.
Customer enters Vehicle, Vehicle Type, and Issue Description.
The Service Advisor performs the vehicle inspection.
Inspection Notes and Condition Rating are recorded.
Labor Cost and Parts Cost are entered.
Total Cost is calculated.
Customer reviews the service estimate.
Customer approves or rejects the estimate.
Approved cases move to Service Execution.
The case is routed based on Vehicle Type.
The technician updates the Service Status.
Service is completed.
A completion notification is sent to the customer.
The case reaches Resolved-Completed.
Challenges and Solution

One of the challenges during development was a Failed to find instance error while sending the service completion email.

The Send Email step referenced the correspondence rule using a display name with spaces, while the actual rule identifier was:

ServiceCompletionNotification

The reference was corrected to match the exact rule identifier.

A second issue was related to the development branch and operator access. The fix was merged into the main VehicleS ruleset so that it was available to the required operators.

Project Screenshots

The repository contains screenshots from the completed Pega application.

US-001 — Submit Vehicle Service Request

US-002 — Perform Vehicle Inspection

US-003 — Generate Service Estimate

US-004 — Approve Service Estimate

The submitted project documentation contains additional user-story evidence and implementation details.

User Stories Covered

The project submission covers the following user stories:

ID	User Story
US-001	Submit Vehicle Service Request
US-002	Perform Vehicle Inspection
US-003	Generate Service Estimate
US-004	Approve Service Estimate
US-005	Maintain Vehicle Data
US-006	Review Service Estimate
US-007	Auto Assign Technician
US-008	Notify Service Completion
US-009	Define Service SLA
US-010	Route by Vehicle Type
Project Documentation

The complete project submission document contains:

Project details
User story requirements
Pega screenshots
Application configuration details
Rule information
Case flow
Design decisions
Challenges and solutions
Personas
Work queues

The submitted documentation is included in this repository under the Documentation folder.

Demo

The project demo video will be added here once available.

Demo Video: To be added
Project Status

Completed and submitted as part of the Pega National Internship Program.

The project documentation and available Pega screenshots are included in this repository.

Author

Samala Vennela

ACE Engineering College
CSE
