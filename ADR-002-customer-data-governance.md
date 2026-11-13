# ADR-002: Establish controlled customer-data governance across company systems

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Kloud Kart leadership

## Context

Kloud Kart holds customer information across its business systems, including a Marketing customer list of approximately 300,000 people. The company does not have a reliable record of where copies of this information are stored or who is responsible for them.

The company is also dealing with a Data Protection Commission complaint involving a customer's request for deletion and must respond within 90 days. Introducing a read replica and a cloud warehouse could create additional locations containing customer information. Without clear ownership and procedures, the company may struggle to locate, protect or act on customer information when required.

## Decision

Establish a company-wide customer-data governance process that records where customer information is stored, assigns responsibility to the relevant departments and controls who can access it. All known systems and copies must be covered by documented procedures for handling access, retention and deletion requests.

## Alternatives considered

### Alternative A: Allow each department to manage its own customer information

- **How it would work:** Marketing, Finance and Operations would continue managing their own customer-data files and copies. Each department would decide who can access its information and how requests are handled.
- **Why it is attractive:** Departments understand their own work and can manage their information without waiting for a central process. It also avoids the immediate effort of creating a company-wide register and assigning governance responsibilities.
- **Why rejected:** Kloud Kart already does not know where all customer-data copies are stored. Continuing with separate departmental arrangements makes it harder to identify every relevant copy when a customer requests deletion or when the company needs to investigate a complaint. It also makes consistent oversight difficult.

### Alternative B: Keep customer information only in one central system

- **How it would work:** Move all customer information into one central database and require departments to access it from there instead of maintaining separate copies.
- **Why it is attractive:** It could reduce the number of locations containing customer information and make access control and deletion easier to coordinate.
- **Why rejected:** Kloud Kart's departments may still need information in different systems to perform their work. Moving everything into one system would require significant changes to existing processes and would not automatically remove existing copies. The company needs to identify and control its current data locations first rather than assume that centralisation alone solves the problem.

## Consequences

- **What this buys:** Kloud Kart gains a clearer record of where customer information is held, who is responsible for it and how requests are handled. This improves the company's ability to investigate complaints, control access and demonstrate the actions taken when responding to customer requests.

- **What this costs:** Departments must help identify their data locations, maintain accurate records and follow common procedures. Management must assign responsibility and review whether the controls are being followed. The process also takes time away from other departmental work.

- **What it costs the client if I am wrong:** If the register is incomplete or departments fail to report their copies, Kloud Kart could overlook customer information when responding to a deletion request. The company could provide an incomplete response to the Data Protection Commission, face further regulatory consequences and damage customer trust. Nana could also spend more time investigating where information is stored instead of managing Operations.

- **What would make me revisit this:** Revisit the governance arrangement if new systems, departments or countries introduce data locations that the current process cannot adequately track. Reconsider the controls if deletion requests repeatedly reveal unknown copies or if access reviews show that departments cannot manage their responsibilities effectively.

## What this survives

This decision provides a governance process that can cover the production database, read replica, reporting warehouse, Marketing files and future systems introduced during expansion. It does not depend on all customer information being stored in one place. As Kloud Kart grows, new systems and departments must be included in the register and assigned clear responsibility before their customer data is used.