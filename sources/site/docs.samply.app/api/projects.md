# Source: https://docs.samply.app/api/projects.html

# Projects [​](https://docs.samply.app/#projects)

Projects contain all the files you work with on Samply. They have a name, artwork, and optionally, collaborators. Anything you upload to Samply will live in a project. And any player you create will be created from files within a project.

## Create a project [​](https://docs.samply.app/#create-a-project)

This endpoint creates a project and returns a [project object](https://docs.samply.app/./projects.html#project-object). As a side effect, this endpoint creates a project-scoped player with your default [player options](https://docs.samply.app/./../sharing.html#link-options). This player contains all the files present in the project.

Request type `POST`

Endpoint `/projects`

### Attributes [​](https://docs.samply.app/#attributes)

js

```
{
  name: string,
  upload: {
    enabled: boolean,
    header: string,
    greeting: string,
    redirect: string
  },
  collaborators: [
    {
      email: string,
      role: "admin" || "editor" || "viewer"
    }
  ],
  sortBy: {
    criterion: "custom" || "name" || "duration" || "size" || "bitDepth" || "sampleRate" || "bitRate" || "channels" || "lufs" || "timeModified" || "timeCreated" || "kind",
    ascending: boolean
  }
}
```

---

#### name string

Human readable title of project.

---

#### upload object optional

Public upload link options.

###### Child attributes

---

#### enabled boolean optional

Enable upload portal.

---

#### header string optional

Upload portal title.

---

#### greeting string optional

Upload portal subheader.

---

#### redirect string optional

Link to redirect user after upload has completed.

---

#### collaborators collaborator array optional

An array of collaborator objects.

---

#### collaborator object optional

The email and permissions for a single collaborator on a project.

###### Child attributes

---

#### email string

User email address.

---

#### role 'admin' | 'editor' | 'viewer'

User permission on a project.

---

#### sortBy object optional

File sort options.

###### Child attributes

---

#### criterion 'custom' | 'name' | 'duration' | 'size' | 'bitDepth' | 'sampleRate' | 'bitRate' | 'channels' | 'lufs' | 'timeModified' | 'timeCreated' | 'kind' optional

Sort criterion for project files.

---

#### ascending boolean optional

Whether to sort in ascending order.

## Update a project [​](https://docs.samply.app/#update-a-project)

This endpoint updates an existing project and returns a [project object](https://docs.samply.app/./projects.html#project-object).

Request type `POST`

Endpoint `/projects/:projectid`

### Attributes [​](https://docs.samply.app/#attributes-1)

js

```
{
  name: string,
  upload: {
    enabled: boolean,
    header: string,
    greeting: string,
    redirect: string
  },
}
```

---

#### name string

Human readable title of project.

---

#### upload object optional

Public upload link options.

###### Child attributes

---

#### enabled boolean optional

Enable upload portal.

---

#### header string optional

Upload portal title.

---

#### greeting string optional

Upload portal subheader.

---

#### redirect string optional

Link to redirect user after upload has completed.

## Get a project [​](https://docs.samply.app/#get-a-project)

This endpoint returns a [project object](https://docs.samply.app/./projects.html#project-object) by id.

Request type `GET`

Endpoint `/projects/:projectid`

## List owned projects [​](https://docs.samply.app/#list-owned-projects)

This endpoints returns an array of all [project objects](https://docs.samply.app/./projects.html#project-object) the caller owns.

Request type `GET`

Endpoint `/projects`

## Project object [​](https://docs.samply.app/#project-object)

All project actions will return a project object with the following structure.

### Attributes [​](https://docs.samply.app/#attributes-2)

js

```
{
  artwork: string,
  color: string,
  creator: {
    displayName: string,
    email: string,
    photoURL: string,
    uid: string,
  },
  id: string,
  name: string,
  object: "project",
  size: 0,
  timeCreated: number,
  timeModified: number,
  upload: {
    enabled: boolean,
    greeting: string,
    header: string,
    redirect: string,
  }
}
```

---

#### artwork string readonly

Download URL to cover artwork.

---

#### color string readonly

Project color in hex format.

---

#### creator object readonly

Project creator.

###### Child attributes

---

#### displayName string readonly

Human-readable display name.

---

#### email string readonly

Email address.

---

#### photoURL string readonly

Download URL to user's profile picture.

---

#### uid string readonly

User's unique id.

---

#### id string readonly

Project id.

---

#### name string readonly

Human readable title of project.

---

#### object project readonly

Object type of returned object.

---

#### size number readonly

Size in bytes of files contained within project.

---

#### timeCreated number readonly

Time created in millis since Unix epoch.

---

#### timeModified number readonly

Time modified in millis since Unix epoch.

---

#### upload object readonly

Public upload link options.

###### Child attributes

---

#### enabled boolean readonly

Enable upload portal.

---

#### header string readonly

Upload portal title.

---

#### greeting string readonly

Upload portal subheader.

---

#### redirect string readonly

Link to redirect user after upload has completed.

---

#### sortBy object readonly

File sort options.

###### Child attributes

---

#### criterion 'custom' | 'name' | 'duration' | 'size' | 'bitDepth' | 'sampleRate' | 'bitRate' | 'channels' | 'lufs' | 'timeModified' | 'timeCreated' | 'kind' readonly

Sort criterion for project files.

---

#### ascending boolean readonly

Whether to sort in ascending order.