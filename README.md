# Snowball Backend Documentation

## Administration Page Table
### GET admin data
+ Endpoint - {BACKEND_IP}/frontend/administration/data

This will return all the data for the administration page.
Input Json

```json
{
  "organization_name": "snowball_crm",
  "offset": 0,
  "limit": 100
}
```

Output Json format [administration.json](JSON-formats%2Foutput%2Fadministration.json)

### Add users/departments record
+ Endpoint - {BACKEND_IP}/frontend/administration/add_record

Input username and department name. If the user and/or department is new, the endpoint will create a new user and/or new department. Return the ids of newly created department/user.

Json format [admin_add_record.json](JSON-formats%2Finput%2Fadmin_add_record.json)

### Update User 
+ Endpoint - {BACKEND_IP}/users/update

User id and department id should exist in the database.

If an existing user needs to add to another department, use this endpoint. 

Json format [update_user.json](JSON-formats%2Finput%2Fupdate_user.json)

Example of updating one user-attribute

```json
{
  "organization_name": "snowball_crm",
  "user_id": 2,
  "department_id": 1,
  "activity_access": [],
  "form_access": [],
  "user_attributes": [
    {
      "attribute_id": 2,
      "attribute_value": "JSON"
    }
  ]
}
```
Example of updating one form_access

```json
{
  "organization_name": "snowball_crm",
  "user_id": 2,
  "user_role": "user",
  "department_id": 1,
  "activity_access": [],
  "form_access": [
    {
      "form_id": 2,
      "is_granted": true
    }
  ],
  "user_attributes": []
}



```

Example of updating one activity_access

```json
{
  "organization_name": "snowball_crm",
  "user_id": 2,
  "user_role": "user",
  "department_id": 1,
  "activity_access": [
    {
      "activity_id": 3,
      "is_granted": false
    }
  ],
  "form_access": [],
  "user_attributes": []
}

```

### Delete user-department row
+ Endpoint - {BACKEND_IP}/frontend/administration/delete_record

Remove row from the administration UI table

Json format 
```json
{
  "organization_name": "snowball_crm",
  "delete_rows": [
    {
      "user_id": 1,
      "department_id": 2
    },
    {
      "user_id": 1,
      "department_id": 2
    }
  ]
}
```
## Department Data Share

### GET data
+ Endpoint - {BACKEND_IP}/departments/data-share/get

Get all the data for the department data share page.

Output JSON format - [department_data_share.json](JSON-formats%2Foutput%2Fdepartment_data_share.json)
```json
{
  "data": {
    "department_name": "Admin",
    "created_on": "2022-12-25T06:41:35",
    "updated_on": "2022-12-25T06:42:27",
    "description": "Administration Department",
    "have_access_to": [
      2,
      3
    ],
    "given_access_to": [
      3
    ],
    "all_users": [
      "Sam Benny"
    ]
  },
  "status": {
    "status_code": 200,
    "status_message": "OK",
    "time_taken": "0.041 sec",
    "api_version": "1.0.0"
  }
}
```

### UPDATE data
+ Endpoint - {BACKEND_IP}/departments/data-share/update

Update the data for the department data share page.

Input JSON format - [dep_data_share_update.json](JSON-formats%2Finput%2Fdep_data_share_update.json)

```json
{
  "organization_name": "snowball_crm",
  "department_id": 1,
  "have_access_to": [
    2,
    3
  ],
  "given_access_to": [
    3
  ]
}
```

### Get department info

+ Endpoint - {BACKEND_IP}/departments/get_info

Get the information about a department given a department id

Input
```json
{
  "department_id": 1,
  "organization_name": "snowball_crm"
}
```

Output
```json
{
  "data": {
    "department_name": "Admin",
    "department_id": 1,
    "department_description": "Administration Department"
  },
  "status": {
    "status_code": 200,
    "status_message": "Department found",
    "time_taken": "0.036 sec",
    "api_version": "1.0.0"
  }
}
```