# Cost Control on GCP

## Billing Resource Organization Basics

[Google: Guide to Cloud Billing Resource Organization & Access Management](https://cloud.google.com/billing/docs/onboarding-checklist)

* Billing is based on the Hierarchy

* Sit under organization layer
  * Polices applied to the organization are applied to the billing account
  * the organization can have multiple billing accounts

* Relationship to Projects
  * all projects must be associate to a billing account to create billable resources
  * a billing account can include multiple projects

* account management
  * billing account access control applies to all included projects
  * cost management also applies to all included projects

## Managing Billing Access

## Controlling Billing Access with IAM Roles

* Limit account creation
  * who can create, edit, and delete billing accounts in an organization?

* Limit who can associate billing accounts with projects
  * who can create billable resources?

*IAM* :: Who can do what on which resource.
**IAM** :: Memmber / Role /Resource

### Billing Perspective : Control Access

1. Account Ownership
   * **Billing Account Administrator**
   * Owns the billing account
   * Manges and assigns access to others

2. Account Creation
   * **Billing Account Creator**
   * Creates new billing accounts in the organization
   * cannot assign rights to others

3. Associate Accounts with Projects
   * **Billing Account User**
   * can associate projects with billing accounts
   * prevents unrestricted creation of billable resources
   * Often paired with the **project creator** role

### Best Practices

1. Limit Scope of access -- *principle of least privilege*

2. Assign multiple billing account administrators

## Cost Visibility and Analysis

### Cost Visibility with Billing Reports

* visibility into costs -- 

* how much are we spending

* what are our cost trends

* what are driving the costs

### Export Billing Data into BigQuery

* perform further in-depth analytics of billing data
  * pair with analytics tool like Data studio

1. Create a BigQuery Dataset in advanced -- Requires a **BigQuery User** role in the export project

2. Configure billing export to the above dataset -- requires a **Billing Account Administrator** role.

### Billing Alerts with Budgets

* configure to avoid surprise bills

1. Create a budget -- set the scope to the entire account or limit it by project ID, product or label

2. set alerts thresholds -- configure alerts for reaching different percentages of the monthly budget

## Cost Reduction tools on GCP

* Rightsizing VMs -- new, scope machine type to match resource usage, up or down

* sustained use discounts -- long running compute for 25% of the month auto discounted, discount up to 30% of monthly usage

* committed use discounts -- commit to use a set amount and save up to 70% for 3 year commitment

* preemptible vms -- short lived vms at huge cost savings 

* object-level availability based on access needs -- back ups archives

* lifecycle policies -- for old data, can be moved to lower tier classes for saving

* free tier resources -- low usage of many GCP services is always free