# Comm100 API
# Resource List 
|Name|EndPoint|Note| 
|---|---|---| 
|[Site](#site)| /api/v3/sites|for site|
|[Contact](#contact)| /api/v3/contacts|for contact| 
|[Agent](#agent)| /api/v3/agents|for agent|
|[Role](#role)| /api/v3/roles|for role|
|[Tag](#tag)| /api/v3/tags|for tag|
|[CannedMessage](#cannedMessage)| /api/v3/cannedMessages|for canned message|
|[CannedMessageCategory](#cannedMessageCategory)| /api/v3/cannedMessageCategory|for canned message category|
|[Department](#department)| /api/v3/departments|for department|
|[Attachment](#attachment)| /api/v3/attachments|for attachment|
|[CreditCardMasking](#creditCardMasking)| /api/v3/creditCardMasking|for credit card masking|
|[PasswordPolicy](#passwordPolicy)| /api/v3/passwordPolicies|for password policy|
|[AuditLog](#auditLog)| /api/v3/auditLogs|for audit log|
|[AgentSingleSignOn](#agentSignleSignOn)| /api/v3/agentSignleSignOn|for agent single sign on|
|[Webhook](#webhook)| /api/v3/webhooks|for webhook|

#Site
## Object
### Site
todo



# Contact
## Objects
### Contact
| Name | Type | Description |
| - | - | - |
| `id` | integer | id of contact |
| `name` | string |  the name of the contact |
| `alias` | string |  the alias name of the contact |
| `identities` | [identity](#identity)[] | identity array  |
| `description` | string | a small description of the contact |
| `company` | string | the primary company name which this contact belongs to |
| `title` | string | the title of the contact|
| `phoneNumber` | string | telephone number of the contact|
| `faxNumber` | string | fax number of the contact |
| `address` | string | the address of the contact  |
| `city` | string | the city of the contact  |
| `stateOrProvince` | string | the state or province of the contact |
| `country` | string |  the country of the contact |
| `postalOrZipCode` | string | the postal or zip code of the contact  |
| `createdTime` | datetime | the time the contact was created |
  
### Identity
| Name | Type | Description | 
| - | - | - | 
| `id` | integer | the id of identity |
| `type` | string | `email`, `SSOUserId`, `externalId` |
| `value` | string | the value of one identity, should be unique |

- Note: We currently only allow one for each type.

### Endpoints
#### Get a contact by contact id
`get  /api/v3/contacts/{id}`
- Parameters
    - id: integer, id of the contact
- Response
    - [contact object](#contact)

#### Create a contact
`post  /api/v3/contacts`
- Parameters 

| Name | Type | Description |
| - | - | - |
| `name` | string |  the name of the contact, required |
| `alias` | string |  the alias name of the contact |
| `identities` | [identity](#identity)[] | the array of identities |
| `description` | string | a small description of the contact |
| `company` | string | the primary company name which this contact belongs to |
| `title` | string | the title of the contact |
| `phoneNumber` | string | telephone number of the contact|
| `faxNumber` | string | fax number of the contact |
| `address` | string | the address of the contact  |
| `city` | string | the city of the contact  |
| `stateOrProvince` | string | the state or province of the contact |
| `country` | string |  the country of the contact |
| `postalOrZipCode` | string | the postal or zip Code of the contact  |

- Response
    - contact: [contact object](#contact)

#### Search contacts
- Max 50 contacts are responded for each request.
- `get  /api/v3/contacts`
- Parameters
    - pageIndex, integer, default 1
    - keywords, string, search scope includes: name/identity value/alias 
- Response
    - contacts: [contact object](#contact) list
    - total: int, total number of contacts.
    - previousPage: string, next page uri, the first page return null.
    - nextPage: string, the last page return null.
    - currentPage: string, current page uri.
- Example
    - `get  /api/v3/contacts?keywords=comm100`
- Note
    - Deleted contact will not be included in the results.
    - The query must be URL encoded.
    - Fuzzy search is supported.

#### Update a contact
`put  /api/v3/contacts/{id}`
- Parameters

| Name | Type | Description |
| - | - | - |
| `name` | string |  the name of the contact |
| `alias` | string |  the alias name of the contact |
| `description` | string | a small description of the contact |
| `company` | string | the primary company name which this contact belongs to|
| `title` | string | the title of the contact|
| `phoneNumber` | string | telephone number of the contact|
| `faxNumber` | string | fax number of the contact |
| `address` | string | the address of the contact  |
| `city` | string | the city of the contact  |
| `stateOrProvince` | string | the state or province of the contact |
| `country` | string |  the country of the contact |
| `postalOrZipCode` | string | the postal or zip code of the contact |
| `identities` | [identity](#identity)[] | the array of identities |
- Response
    - contact: [contact object](#contact)

#### Delete a contact
 `delete  /api/v3/contacts/{id}`
- Parameters
    - id: integer, id of the contact
- Response
    - http status code and message

#### Add identity
`post  /api/v3/contacts/{contactId}/identities`
- Parameters
    - contactId: integer, contact id
    - type: string, identity type
    - value: string, identity value
- Response
    - identity: [identity object](#identity)

#### Update identity
`put  /api/v3/contacts/{contactId}/identities/{id}`
- Parameters
    - contactId, integer, contact id
    - id, integer, contact identity id
    - value, string, the value of the identity
- Response
    - identity: [identity object](#identity)

#### Delete identity
 `delete  /api/v3/contacts/{contactId}/identities/{id}`
- Parameters
    - contactId, integer, contact id
    - id, integer, contact identity id
- Response
    - Http status code and message

# Agent
[Reference document](https://www.comm100.com/doc/api/introduction.htm#/Account?id=agent-json-format)
