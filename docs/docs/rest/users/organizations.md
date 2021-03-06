# Organizations

Manage your organization, its children and invitations.

## Get an organization

Return an organization.

`GET /organizations/:id`

### Success response

`HTTP/1.1 200 OK`

  	{
      "url": "/organizations/1/",
      "name": "Example",
      "contact_email": "contact@example.com",
      "settings": {
        "nickname": "",
        "notify_message_status": true,
        "notify_optouts": false,
        "external_optout_message": ""
      },
      "parent": null,
      "can_attach_files": false,
      "can_external_optout": false,
      "_links": {
        "opt_outs": {
          "href": "/organizations/1/opt_outs/"
        },
        "children": {
          "href": "/organizations/1/children/"
        },
       "invite_user": {
          "href": "/organizations/1/invite_user/"
        }
      }
    }

## List your organizations

Return a list of organization with user organization and childrens.

`GET /organizations`

### Success response

`HTTP/1.1 200 OK`

Same as get an [organization](#get-an-organization) section as a list.

## Modify an organization

Update your orgnization or a child one.

`PUT /organizations/:id`

### Success response

Return updated [organization](#get-an-organization).

### Error response

`HTTP/1.1 400 Bad Request`

    {
      "contact_email": [
        "Saisissez une adresse email valable."
      ]
    }

## List organization children

Return list of children organizations.

`GET /organizations/:id/children`

### Success response

Same as get an [organization](#get-an-organization) section as a list.

## Invite a user into an organization

Invite a user into an organization.

`POST /organizations/:id/invite_user`

| Name       | Type     | Description     |
|------------|----------|-----------------|
| identifier | string   | User identifier |

### Success response

`HTTP 201 Created`

    {
      "identifier": "test@example.com"
    }

## List organization opt-outs (todo)

Todo.

## Create child organization

Only organization administrator can create child organization.

`POST /oganizations`

| Name                             | Type     | Description                              |
|----------------------------------|----------|------------------------------------------|
| name                             | string   | Name                                     |
| contact_email                    | string   | Email                                    |
| parent                           | string   | Parent organization URL in case of child |
| settings                         | object   |                                          |
| settings.nickname                | string   | Nickname                                 |
| settings.notify_message_status   | string   | Notify `contact_email` on status changes |
| settings.notify_optouts          | string   | Notify `contact_email` on new opt-out    |
| settings.external_optout_message | string   | Custom external optout message           |

### Success response

`HTTP 201 Created`

    {
      "url": "/organizations/2/",
      "name": "Child organization",
      "contact_email": "contact@example.com",
      "settings": {
        "nickname": "nickname",
        "notify_message_status": false,
        "notify_optouts": false,
        "external_optout_message": "Custom message"
      },
      "parent": "/organizations/1/",
      "can_attach_files": false,
      "can_external_optout": false,
      "_links": {
        "opt_outs": {
          "href": "/organizations/2/opt_outs/"
        },
        "children": {
          "href": "/organizations/2/children/"
        },
        "invite_user": {
          "href": "/organizations/2/invite_user/"
        }
      }
    }
