> The organization_id refers to the unique identifier assigned to each organization within the system. This ID is set arbitrarily at the time of creating the organization and remains constant throughout its lifecycle. The **front-end** should retrieve this id and include it in all relevant API calls. This ensures that all data, actions, and records are correctly associated with the right organization, enabling clear separation and management of information across different clients or business units.

For example, by using a specific organization_id, [[Samuel]] can analyze and report on metrics and information that are relevant only to that organization, ensuring data privacy and contextual accuracy. Similarly, [[Emile]] can generate meeting summaries and follow-ups that are scoped to the correct organization, preventing cross-organization data leakage or confusion.

## How is it generated?

The organization_id is typically generated when a new organization is created in the system. Clerk is tasked with generating the organization_id whenever a new 
organization is created. It is very important that each organization_id is unique to avoid conflicts or data overlap between organizations. This uniqueness allows the system to reliably distinguish between different organizations and maintain data integrity. For testing purposes, the organization_id can be generated manually by [[Clerk]], or by defining a UUID-like string (internal tests tend to be done with the `samla` id).

## How it works with [[MongoDB]]

In MongoDB, each organization's data is stored in a separate database named with its organization_id. When making API calls through [[AWS Lambda]], the organization_id is used to select the correct database for that organization's data. This ensures that data from different organizations stays separate and secure. This field is present in API calls:
- [[get_all_conversations]]