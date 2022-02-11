# 3.2.1.2 PPM Segments

<!--BREAK-->
### Data Object: PpmAward



#### Access Controls

* Required Role: `erp:reader-refdata`

#### Data Source

* Local Table/View: `PPM_AWARD`
  * Support Tables:
    * `PPM_PROJECT_AWARD`
* Data Origin:
  * System: Oracle BICC
  * Extract Objects:
    * file_fscmtopmodelam_gmsawardam_awardheaderviewpvo-batch316123518-20220126_234329
  * Underlying Database Objects:
    * GMS_AWARD_HEADERS_B
    * GMS_AWARD_HEADERS_TL
    * GMS_AWARD_HEADERS_VL

##### Properties

| Property Name               | Data Type                | Key Field [^2] | Searchable [^1] | Required Role | Notes |
| --------------------------- | ------------------------ | :------------: | :-------------: | ------------- | ----- |
| id                          | Long!                    |       Y        |        Y        |               | Award ID: Unique identifier of the award. |
| name                        | NonEmptyTrimmedString240 |                |        Y        |               | Award Name: Name of the award. |
| description                 | NonEmptyTrimmedString240 |                |                 |               | Description: Brief description of the award. |
| projectId                   | Long!                    |                |        Y        |               | Project ID: Project Identifier for award. |
| endDate                     | LocalDate                |                |                 |               | End Date: End date of the award. |
| closeDate                   | LocalDate                |                |                 |               | Close Date: Date past the end date of the award. Transactions for the award can be entered up to this date. |
| awardOwningOrganizationName | String                   |                |                 |               | Award Owning Organization: An organization that owns awards within an enterprise. An organizing unit in the internal or external structure of your enterprise. Organization structures provide the framework for performing legal reporting, financial control, and management reporting for the award. |
| awardPurpose                | NonEmptyTrimmedString80  |                |                 |               | Purpose: Name of the award purpose. |
| awardType                   | NonEmptyTrimmedString30  |                |        Y        |               | Type: Classification of an award, for example, Federal grants or Private grants. |
| businessUnitName            | NonEmptyTrimmedString100 |                |                 |               | Business Unit: Unit of an enterprise that performs one or many business functions that can be rolled up in a management hierarchy. An award business unit is one within which the award is created. |
| sponsorAwardNumber          | NonEmptyTrimmedString30  |                |        Y        |               | Sponsor Award Number: Award number tracked by the sponsor. |
| lastUpdateDate              | DateTime!                |                |                 |               | The date when the award was last updated. |
| lastUpdatedBy               | ErpUserId                |                |                 |               | The user that last updated the award. |
| awardFundingSource          | [PpmFundingSource!]      |                |                 |               | Award Funding Sources: The Award Funding Sources resource is used to view the attributes used to create or update a funding source for the award. |
| eligibleForUse              | Boolean!                 |                |                 |               | Returns whether this PpmAward is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmAward must:<br/>- Have closeDate after the given accountingDate |

* `eligibleForUse` : `Boolean!`
  * Returns whether this PpmAward is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmAward must:<br/>- Have closeDate after the given accountingDate
  * Arguments:
    * `accountingDate` : `LocalDate`

##### Linked Data Objects

(None)

#### Query Operations

##### `ppmAward`

> Get a single PpmAward by id.  Returns undefined if does not exist

* **Parameters**
  * `id : String!`
* **Returns**
  * `PpmAward`

##### `ppmAwardByName`

> Gets PpmAwards by exact name.  Returns empty list if none are found

* **Parameters**
  * `name : String!`
* **Returns**
  * `[PpmAward!]!`

##### `ppmAwardByProjectId`

> Gets PpmAwards by project.  Returns empty list if none are found

* **Parameters**
  * `projectId : String!`
* **Returns**
  * `[PpmAward!]!`

##### `ppmAwardByProjectNumber`

> Gets PpmAwards by project number.  Returns empty list if none are found

* **Parameters**
  * `projectNumber : PpmProjectNumber!`
* **Returns**
  * `[PpmAward!]!`

##### `ppmAwardSearch`

> Search for PpmAward objects by multiple properties.
> See
> See the PpmAwardFilterInput type for options.

* **Parameters**
  * `filter : PpmAwardFilterInput!`
* **Returns**
  * `PpmAwardSearchResults!`

[^1]: Searchable attributes are available as part of the general search filter input.
[^2]: Key fields are considered unique identifiers for a data type and can be used to retrieve single records via dedicated operations.


<!--BREAK-->
### Data Object: PpmExpenditureType



#### Access Controls

* Required Role: `erp:reader-refdata`

#### Data Source

* Local Table/View: `PPM_EXPENDITURE_TYPE`
* Data Origin:
  * System: Oracle BICC
  * Extract Objects:
    * View Object:file_fscmtopmodelam_pjfsetuptransactionsam_expendituretypeview
  * Underlying Database Objects:
    * PJF_EXP_TYPES_B
    * PJF_EXP_TYPES_TL

##### Properties

| Property Name       | Data Type                 | Key Field [^2] | Searchable [^1] | Required Role | Notes |
| ------------------- | ------------------------- | :------------: | :-------------: | ------------- | ----- |
| id                  | Long!                     |       Y        |        Y        |               | Expenditure Type ID: Unique identifier of the expenditure type. |
| name                | NonEmptyTrimmedString240! |                |        Y        |               | Expenditure Type: Name of the expenditure type. |
| description         | String                    |                |                 |               | Expenditure Type Description: Description of the expenditure type. |
| startDate           | LocalDate                 |                |                 |               | Expenditure Type Start Date: Start date of an expenditure type. |
| endDate             | LocalDate                 |                |                 |               | Expenditure Type End Date: End date of an expenditure type. |
| expenditureCategory | NonEmptyTrimmedString240  |                |                 |               | Expenditure Category: Name of the expenditure category. |
| revenueCategoryCode | NonEmptyTrimmedString30   |                |                 |               | Revenue Category Code: Code of a category grouping of expenditure types by type of revenue. |
| lastUpdateDateTime  | DateTime!                 |                |        Y        |               | The date when the expenditure type was last updated. |
| lastUpdatedBy       | ErpUserId                 |                |                 |               | The user that last updated the expenditure type. |
| eligibleForUse      | Boolean!                  |                |                 |               | Returns whether this PpmExpenditureType is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmExpenditureType must:<br/>- Have a startDate and endDate range which includes the given accoutingDate |

* `eligibleForUse` : `Boolean!`
  * Returns whether this PpmExpenditureType is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmExpenditureType must:<br/>- Have a startDate and endDate range which includes the given accoutingDate
  * Arguments:
    * `accountingDate` : `LocalDate`

##### Linked Data Objects

(None)

#### Query Operations

##### `ppmExpenditureType`

> Get a single PpmExpenditureType by id.  Returns undefined if does not exist.
> 
> This ID is an internal tracking number used by the financial system.  It is only used to link between objects internally.
> Use the ppmExpenditureTypeByName or ppmExpenditureTypeByAccount operations to pull by a unique identifier.

* **Parameters**
  * `id : Long!`
* **Returns**
  * `PpmExpenditureType`

##### `ppmExpenditureTypeByName`

> Gets PpmExpenditureTypes by exact name.  Returns empty list if none are found

* **Parameters**
  * `name : NonEmptyTrimmedString100!`
* **Returns**
  * `PpmExpenditureType!`

##### `ppmExpenditureTypeByAccount`

> Gets PpmExpenditureTypes by the associated GL Account.  Returns undefined if none is found.
> 
> PPM Expense Type names will be the GL Account number plus a description.  This full string must be used in file-based feeds.
> This method will allow you to obtain the exact string (in the name property) that needs to be included.

* **Parameters**
  * `account : ErpAccountCode!`
* **Returns**
  * `PpmExpenditureType`

##### `ppmExpenditureTypeSearch`

> Search for PpmExpenditureType objects by multiple properties.
> See
> See the PpmExpenditureTypeFilterInput type for options.

* **Parameters**
  * `filter : PpmExpenditureTypeFilterInput!`
* **Returns**
  * `PpmExpenditureTypeSearchResults!`

[^1]: Searchable attributes are available as part of the general search filter input.
[^2]: Key fields are considered unique identifiers for a data type and can be used to retrieve single records via dedicated operations.


<!--BREAK-->
### Data Object: PpmFundingSource



#### Access Controls

* Required Role: `erp:reader-refdata`

#### Data Source

* Local Table/View: `PPM_FUNDING_SOURCE`
* Data Origin:
  * System: Oracle BICC
  * Extract Objects:
    * View Object:file_fscmtopmodelam_prjextractam_gmsbiccextractam_fundingsourceextractpvo-batch
  * Underlying Database Objects:
    * GMS_FUNDING_SOURCES_B
    * GMS_FUNDING_SOURCES_TL

##### Properties

| Property Name         | Data Type                 | Key Field [^2] | Searchable [^1] | Required Role | Notes |
| --------------------- | ------------------------- | :------------: | :-------------: | ------------- | ----- |
| id                    | Long!                     |                |        Y        |               | Funding Source ID: The unique identifier of the funding source. |
| name                  | NonEmptyTrimmedString360! |                |        Y        |               | Funding Source Name: The source name of the funding source. |
| fundingSourceNumber   | NonEmptyTrimmedString50!  |                |        Y        |               | Funding Source Number: The number of the funding source. |
| description           | NonEmptyTrimmedString240  |                |                 |               | Funding Source Description: The description of the funding source. |
| fundingSourceFromDate | LocalDate!                |                |                 |               | Funding Source From Date: The date from which the funding source is active. |
| fundingSourceToDate   | LocalDate                 |                |                 |               | Funding Source To Date: The date till which the funding source is active. |
| fundingSourceTypeCode | String                    |                |                 |               | The code of the funding source type. |
| lastUpdateDateTime    | DateTime!                 |                |        Y        |               | The date when the funding source was last updated. |
| lastUpdatedBy         | ErpUserId                 |                |                 |               | The user that last updated the funding source. |
| eligibleForUse        | Boolean!                  |                |                 |               | Returns whether this PpmFundingSource is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmFundingSource must:<br/>- Have a projectStatusCode of ACTIVE<br/>- Not be a templateProject<br/>- Have a fundingSourceFromDate and fundingSourceToDate range which includes the given accountingDate |

* `eligibleForUse` : `Boolean!`
  * Returns whether this PpmFundingSource is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmFundingSource must:<br/>- Have a projectStatusCode of ACTIVE<br/>- Not be a templateProject<br/>- Have a fundingSourceFromDate and fundingSourceToDate range which includes the given accountingDate
  * Arguments:
    * `accountingDate` : `LocalDate`

##### Linked Data Objects

(None)

#### Query Operations

##### `ppmFundingSource`

> Get a single PpmFundingSource by id.  Returns undefined if does not exist

* **Parameters**
  * `id : String!`
* **Returns**
  * `PpmFundingSource`

##### `ppmFundingSourceByNumber`

> Get a single PpmFundingSource by number.  Returns undefined if does not exist

* **Parameters**
  * `fundingSourceNumber : String!`
* **Returns**
  * `PpmFundingSource`

##### `ppmFundingSourceByName`

> Gets PpmFundingSources by exact name.  Returns empty list if none are found

* **Parameters**
  * `name : String!`
* **Returns**
  * `[PpmFundingSource!]!`

##### `ppmFundingSourceSearch`

> Search for PpmFundingSource objects by multiple properties.
> See
> See the PpmFundingSourceFilterInput type for options.

* **Parameters**
  * `filter : PpmFundingSourceFilterInput!`
* **Returns**
  * `PpmFundingSourceSearchResults!`

[^1]: Searchable attributes are available as part of the general search filter input.
[^2]: Key fields are considered unique identifiers for a data type and can be used to retrieve single records via dedicated operations.


<!--BREAK-->
### Data Object: PpmOrganization



#### Access Controls

* Required Role: `erp:reader-refdata`

#### Data Source

* Local Table/View: `PPM_ORGANIZATION`
* Data Origin:
  * System: Oracle BICC
  * Extract Objects:
    * View Object: FscmTopModelAM.file_fscmtopmodelam_organizationam_projectexpenditureorganizationpvo-batch.ProjectView
  * Underlying Database Objects:
    * HR_ORG_UNIT_CLASSIFICATIONS_F
    * HR_ORGANIZATION_UNITS_F_TL

##### Properties

| Property Name      | Data Type                 | Key Field [^2] | Searchable [^1] | Required Role | Notes |
| ------------------ | ------------------------- | :------------: | :-------------: | ------------- | ----- |
| id                 | Long!                     |       Y        |        Y        |               | Organization ID: Unique identifier of the Organization. |
| name               | NonEmptyTrimmedString100! |                |        Y        |               | Organization Name: Name of the Organization |
| effectiveStartDate | LocalDate!                |                |                 |               | Effective Start Date: Start date of Organization |
| effectiveEndDate   | LocalDate                 |                |                 |               | Effective End Date: End date of Organization |
| lastUpdateDateTime | DateTime!                 |                |        Y        |               | The date when the organization was last updated. |
| lastUpdatedBy      | ErpUserId                 |                |                 |               | The user that last updated the organization. |
| eligibleForUse     | Boolean!                  |                |                 |               | Returns whether this PpmOrganization is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmOrganization must:<br/>- Have a effectiveStartDate and effectiveEndDate range which includes the given accountingDate |

* `eligibleForUse` : `Boolean!`
  * Returns whether this PpmOrganization is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmOrganization must:<br/>- Have a effectiveStartDate and effectiveEndDate range which includes the given accountingDate
  * Arguments:
    * `accountingDate` : `LocalDate`

##### Linked Data Objects

(None)

#### Query Operations

##### `ppmOrganization`

> Get a single PpmOrganization by id.  Returns undefined if does not exist

* **Parameters**
  * `id : String!`
* **Returns**
  * `PpmOrganization`

##### `ppmOrganizationByName`

> Gets PpmOrganizations by exact name.  Returns empty list if none are found

* **Parameters**
  * `name : String!`
* **Returns**
  * `PpmOrganization`

##### `ppmOrganizationByDepartment`

> Gets PpmOrganizations by the associated GL Financial Department.  Returns undefined if none is found.
> 
> PPM Expense Organization names will be the GL Financial Department number plus a description.  This full string must be used in file-based feeds.
> This method will allow you to obtain the exact string (in the name property) that needs to be included.

* **Parameters**
  * `department : ErpDepartmentCode!`
* **Returns**
  * `PpmOrganization`

##### `ppmOrganizationSearch`

> Search for PpmOrganization objects by multiple properties.
> See
> See the PpmOrganizationFilterInput type for options.

* **Parameters**
  * `filter : PpmOrganizationFilterInput!`
* **Returns**
  * `PpmOrganizationSearchResults!`

[^1]: Searchable attributes are available as part of the general search filter input.
[^2]: Key fields are considered unique identifiers for a data type and can be used to retrieve single records via dedicated operations.


<!--BREAK-->
### Data Object: PpmProject



#### Access Controls

* Required Role: `erp:reader-refdata`

#### Data Source

* Local Table/View: `PPM_PROJECT`
* Data Origin:
  * System: Oracle BICC
  * Extract Objects:
    * View Object: FscmTopModelAM.PjfProjectAM.ProjectView
  * Underlying Database Objects:
    * FND_CURRENCIES_VL
    * FND_SETID_SETS_VL
    * GL_DAILY_CONVERSION_TYPES
    * HR_ORGANIZATION_INFORMATION_F
    * HR_ORGANIZATION_UNITS_F_TL
    * HR_ORGANIZATION_V
    * PER_PERSON_NAMES_F_V
    * PJC_CINT_RATE_SCH_VL
    * PJF_IND_RATE_SCH_VL
    * PJF_LATESTPROJECTMANAGER_V
    * PJF_PROJECTS_ALL_B
    * PJF_PROJECTS_ALL_VL
    * PJF_PROJECT_STATUSES_VL
    * PJF_PROJECT_TYPES_VL
    * PJF_PROJ_ELEMENTS_VL
    * PJF_TP_SCHEDULES
    * PJF_WORK_TYPES_VL
    * PJO_PROJECT_PROGRESS
    * PJT_PRIMARYPROJMANAGER_V
    * PJT_SCHEDULES_VL
    * XLE_ENTITY_PROFILES

##### Properties

| Property Name              | Data Type                 | Key Field [^2] | Searchable [^1] | Required Role | Notes |
| -------------------------- | ------------------------- | :------------: | :-------------: | ------------- | ----- |
| id                         | Long!                     |       Y        |                 |               | Project ID: Unique identifier of the project. |
| projectNumber              | PpmProjectNumber!         |                |        Y        |               | Project Number: Number of the project that is being created. |
| name                       | NonEmptyTrimmedString240! |                |        Y        |               | Project Name: Name of the project that is being created. |
| description                | String                    |                |                 |               | Project Description: A description about the project. This might include high-level information about the work being performed. |
| projectStartDate           | LocalDate!                |                |        Y        |               | Project Start Date: The date that work or information tracking begins on a project. |
| projectCompletionDate      | LocalDate                 |                |        Y        |               | Project Finish Date: The date that work or information tracking completes for a project. |
| projectStatus              | NonEmptyTrimmedString80!  |                |                 |               | Project Status: An implementation-defined classification of the status of a project. Typical project statuses are Active and Closed. |
| projectStatusCode          | NonEmptyTrimmedString30!  |                |        Y        |               | Project Status Code: The current status set on a project. A project status is an implementation-defined classification of the status of a project. Typical project status codes are ACTIVE and CLOSED. |
| projectOrganizationName    | NonEmptyTrimmedString240  |                |                 |               | Organization: An organizing unit in the internal or external structure of the enterprise. Organization structures provide the framework for performing legal reporting, financial control, and management reporting for the project. |
| legalEntityName            | NonEmptyTrimmedString240  |                |                 |               | Legal Entity: Name of the legal entity associated with the project. A legal entity is a recognized party with given rights and responsibilities by legislation. Legal entities generally have the right to own property, the right to trade, the responsibility to repay debt, and the responsibility to account for themselves to company regulators, taxation authorities, and owners according to rules specified in the relevant legislation. |
| primaryProjectManagerEmail | NonEmptyTrimmedString240  |                |        Y        |               | Project Manager Email: Email of the person who leads the project team and who has the authority and responsibility for meeting the project objectives. |
| primaryProjectManagerName  | NonEmptyTrimmedString240  |                |                 |               | Project Manager: Name of the person who leads the project team and who has the authority and responsibility for meeting project objectives. |
| sourceApplicationCode      | NonEmptyTrimmedString30   |                |                 |               | Source Application: The third-party application from which the project originates. |
| sourceProjectReference     | NonEmptyTrimmedString30   |                |                 |               | Source Reference: The identifier of the project in the external system where it was originally entered. |
| projectCategory            | NonEmptyTrimmedString30   |                |                 |               | TODO |
| sponsoredProject           | Boolean!                  |                |        Y        |               | Sponsored Project Flag: Whether this project is a sponsored project and requires Award and Funding Source segments when assigning costs. |
| billingEnabled             | Boolean!                  |                |        Y        |               | Billing Enabled Flag: If billing is allowed for this project. |
| capitalizationEnabled      | Boolean!                  |                |        Y        |               | Capitalization Enabled Flag: If this is a capital project whose costs may need to be capitalized. |
| templateProject            | Boolean!                  |                |        Y        |               | Template Project Only Flag: If this project is a template for other projects.  Template projects may not have costs submitted against them. |
| lastUpdateDateTime         | DateTime!                 |                |        Y        |               | Timestamp this record was last updated in the financial system. |
| lastUpdateUserId           | ErpUserId                 |                |                 |               | User ID of the person who last updated this record. |
| tasks                      | [PpmTask!]                |                |                 |               | Tasks: The Task resource includes the attributes that are used to store values while creating or updating project tasks. Tasks are units of project work assigned or performed as part of the duties of a resource. Tasks can be a portion of project work to be performed within a defined period by a specific resource or multiple resources.<br/><br/>By default, this will only list tasks which are allowed to be assigned costs.  If you need to see all tasks, set the property argument to false. |
| awards                     | [PpmAward!]               |                |                 |               |  |
| defaultAwardNumber         | PpmAwardNumber            |                |                 |               |  |
| defaultFundingSourceNumber | PpmFundingSourceNumber    |                |                 |               |  |
| eligibleForUse             | Boolean!                  |                |                 |               | Returns whether this PpmProject is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmProject must:<br/>- Have a projectStatusCode of ACTIVE<br/>- Not be a templateProject<br/>- Have a projectStartDate and projectCompletionDate range which includes the given accountingDate |

* `tasks` : `[PpmTask!]`
  * Tasks: The Task resource includes the attributes that are used to store values while creating or updating project tasks. Tasks are units of project work assigned or performed as part of the duties of a resource. Tasks can be a portion of project work to be performed within a defined period by a specific resource or multiple resources.<br/><br/>By default, this will only list tasks which are allowed to be assigned costs.  If you need to see all tasks, set the property argument to false.
  * Arguments:
    * `chargeableOnly` : `Boolean` = true
  * Description of `PpmTask`:
    * Represents a component of work within the project.
* `eligibleForUse` : `Boolean!`
  * Returns whether this PpmProject is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmProject must:<br/>- Have a projectStatusCode of ACTIVE<br/>- Not be a templateProject<br/>- Have a projectStartDate and projectCompletionDate range which includes the given accountingDate
  * Arguments:
    * `accountingDate` : `LocalDate`

##### Linked Data Objects

(None)

#### Query Operations

##### `ppmProject`

> Get a single PpmProject by code.  Returns undefined if does not exist

* **Parameters**
  * `projectId : String!`
* **Returns**
  * `PpmProject`

##### `ppmProjectByNumber`

> Get a single PpmProject by the project number.  Returns undefined if no project with that number is found.

* **Parameters**
  * `projectNumber : String!`
* **Returns**
  * `PpmProject`

##### `ppmProjectByName`

> Gets a list of PpmProjects by exact name.  Returns empty list if none are found.  Project Name should be unique in oracle.

* **Parameters**
  * `projectName : String!`
* **Returns**
  * `[PpmProject!]!`

##### `ppmProjectSearch`

> Search for PpmProject objects by multiple properties.
> See
> See the PpmProjectFilterInput type for options.

* **Parameters**
  * `filter : PpmProjectFilterInput!`
* **Returns**
  * `PpmProjectSearchResults!`

[^1]: Searchable attributes are available as part of the general search filter input.
[^2]: Key fields are considered unique identifiers for a data type and can be used to retrieve single records via dedicated operations.


<!--BREAK-->
### Data Object: PpmTask

Represents a component of work within the project.

#### Access Controls

* Required Role: `erp:reader-refdata`

#### Data Source

* Local Table/View: `PPM_TASK`
* Data Origin:
  * System: Oracle BICC
  * Extract Objects:
    * View Object: file_fscmtopmodelam_prjextractam_pjfbiccextractam_taskstructureextractpvo-batch2130430018-20211110_175451
  * Underlying Database Objects:
    * PJF_TASK_XFACE

##### Properties

| Property Name            | Data Type                 | Key Field [^2] | Searchable [^1] | Required Role | Notes |
| ------------------------ | ------------------------- | :------------: | :-------------: | ------------- | ----- |
| id                       | Long!                     |       Y        |        Y        |               | Task ID: Unique identifier of the project task. |
| taskNumber               | NonEmptyTrimmedString100! |                |        Y        |               | Task Number: The number of a task. |
| name                     | NonEmptyTrimmedString240! |                |        Y        |               | Task Name: The name of the task. A task is a subdivision of the project work. Each project can have a set of top tasks and a hierarchy of subtasks below each top task. |
| description              | String                    |                |                 |               | Task Description: Text description of the project task that is being created. |
| taskStartDate            | LocalDate                 |                |                 |               | Task Start Date: Scheduled start date of the project task. |
| taskFinishDate           | LocalDate                 |                |                 |               | Task Finish Date: Scheduled end date of the project task. |
| billable                 | Boolean!                  |                |        Y        |               | Billable: Indicates that transactions charged to that task can be billed to customers. |
| chargeable               | Boolean!                  |                |        Y        |               | Chargeable: Indicates that something is eligible to be charged to a task. |
| taskLevel                | PositiveInt!              |                |                 |               | Task Level: Indicates level of the task in the WBS. |
| executionDisplaySequence | PositiveInt!              |                |                 |               | Display Sequence: The order in which the task is displayed in the project. |
| lowestLevelTask          | Boolean!                  |                |        Y        |               | Lowest Level Task: Indicates the task is at the lowest level. |
| parentTaskId             | Long                      |                |                 |               | Parent Task ID: Identifier of the parent task of the task. |
| topTaskId                | Long                      |                |                 |               | Top Task ID: Identifier of the top task to which the task rolls up. If the task is a top task, the identifier of the top task is same as the identifier of the task. |
| lastUpdateDateTime       | DateTime!                 |                |        Y        |               | The date when the task was last updated. |
| lastUpdatedBy            | ErpUserId                 |                |                 |               | The user that last updated the task. |
| eligibleForUse           | Boolean!                  |                |                 |               | Returns whether this PpmTask is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmTask must:<br/>- Be chargeable<br/>- Ba a lowestLevelTask<br/>- Have a taskStartDate and taskFinishDate range which includes the given accountingDate |

* `eligibleForUse` : `Boolean!`
  * Returns whether this PpmTask is valid to use on transactional documents for the given accounting date.  If not provided, the date will be defaulted to the current date.<br/><br/>To be eligible for use, the PpmTask must:<br/>- Be chargeable<br/>- Ba a lowestLevelTask<br/>- Have a taskStartDate and taskFinishDate range which includes the given accountingDate
  * Arguments:
    * `accountingDate` : `LocalDate`

##### Linked Data Objects

(None)

#### Query Operations

##### `ppmTask`

> Get a single PpmTask by id.  Returns undefined if does not exist

* **Parameters**
  * `id : Long!`
* **Returns**
  * `PpmTask`

##### `ppmTaskByNumber`

> Get a single PpmTask by number.  Returns undefined if does not exist

* **Parameters**
  * `taskNumber : String!`
* **Returns**
  * `PpmTask`

##### `ppmTaskByName`

> Gets PpmTasks by exact name.  Returns empty list if none are found

* **Parameters**
  * `name : NonEmptyTrimmedString240!`
* **Returns**
  * `[PpmTask!]!`

##### `ppmTaskByProjectId`

> Gets PpmTasks by project.  Returns empty list if none are found

* **Parameters**
  * `projectId : Long!`
* **Returns**
  * `[PpmTask!]!`

##### `ppmTaskByProjectNumber`

> Gets PpmTasks by project.  Returns empty list if none are found

* **Parameters**
  * `projectNumber : PpmProjectNumber!`
* **Returns**
  * `[PpmTask!]!`

##### `ppmTaskSearch`

> Search for PpmTask objects by multiple properties.
> See
> See the PpmTaskFilterInput type for options.

* **Parameters**
  * `filter : PpmTaskFilterInput!`
* **Returns**
  * `PpmTaskSearchResults!`

[^1]: Searchable attributes are available as part of the general search filter input.
[^2]: Key fields are considered unique identifiers for a data type and can be used to retrieve single records via dedicated operations.