# Source: https://docs.samply.app/api/files.html

# Files [​](https://docs.samply.app/#files)

Samply offers you the ability to upload & download your files to a project through the API.

First, request an upload URL from an endpoint. Then use that URL to upload a file directly to your project.

You can also skip the documentation and skip directly to [example code](https://docs.samply.app/./files.html#example-upload).

## Request an upload URL [​](https://docs.samply.app/#request-an-upload-url)

First, you'll request an upload URL from a project-specific `/files` endpoint. The file you'll upload will follow the File interface as defined [here](https://developer.mozilla.org/en-US/docs/Web/API/File).

Request type `POST`

Endpoint `/projects/:projectid/files`

### Body [​](https://docs.samply.app/#body)

js

```
{
  name: string,
  mimeType: string,
  size: number | string,
  parentid: string
}
```

---

#### name string

The name parameter on the File.

---

#### mimeType string

The mime type as defined by the type parameter on the File.

---

#### size number | string

The size in bytes as defined by the size parameter on the File.

---

#### parentid string optional

An optional id to specify a stack or folder within the project that this file will be uploaded to.

### Upload URL response [​](https://docs.samply.app/#upload-url-response)

The request will return an object with the following structure.

js

```
{
  boxid: string,
  contentType: string,
  metadata: {
    boxpath: string,
    destination: string,
    projectid: string,
  },
  stackid: string,
  url: string
}
```

---

#### boxid string readonly

The id to the asset you will be uploading.

---

#### contentType string readonly

File content type as returned by the server.

---

#### metadata object readonly

Upload metadata.

###### Child attributes

---

#### boxpath string readonly

Path to box document in the database.

---

#### destination string readonly

Internal file destination indicator.

---

#### projectid string readonly

Project id file will upload to.

---

#### stackid string readonly

Stack id that the file will be uploaded to.

---

#### url string readonly

Upload URL.

## Upload a file [​](https://docs.samply.app/#upload-a-file)

Now that we have our upload URL, our [File](https://developer.mozilla.org/en-US/docs/Web/API/File), and our metadata, it's time to upload the file.

Request type `PUT`

Endpoint is the `url` field returned from the previous request.

Body is the [File](https://developer.mozilla.org/en-US/docs/Web/API/File).

The headers will be populated with fields from the previous response.

A full example is provide below.

## Example upload [​](https://docs.samply.app/#example-upload)

Below is example code for the upload API flow. We receive a file from an `HTMLInputElement`, request an upload URL for that file, then upload the file with a `PUT` request.

js

```
const projectid = "testprojectid"

// File uploaded from HTMLInputElement
const fileInput = document.getElementById("fileInput") as HTMLInputElement;
const files = fileInput.files;
const file = files[0] as File;

// Request upload URL
const response = await fetch(`${baseUrl}/projects/${projectid}/files`, {
  method: "POST",
  body: JSON.stringify({
    name: file.name,
    mimeType: file.type,
    size: file.size,
  }),
  headers: {
    Authorization: `Bearer ${token}`,
    "Content-Type": "application/json",
  },
});
const jsonResponse = await response.json();

// Upload file
const url = jsonResponse.url;
const uploadResponse = await fetch(url, {
  method: "PUT",
  body: file,
  headers: {
    "x-goog-meta-destination": jsonResponse.metadata.destination,
    "x-goog-meta-projectid": jsonResponse.metadata.projectid,
    "x-goog-meta-boxpath": jsonResponse.metadata.boxpath,
    "Content-Type": jsonResponse.contentType,
  },
});
```

## Download a file [​](https://docs.samply.app/#download-a-file)

This endpoint retrieves a download url for a file.

Request type `GET`

Endpoint `/projects/:projectid/files/:fileid/download`

Response

js

```
{
  url: string;
  expires: number;
}
```

## Delete a file [​](https://docs.samply.app/#delete-a-file)

This endpoint deletes a file by id. It returns an empty object and 200 status on successful deletion. Additionally, if the file being deleted is the only version within a stack, that stack will be deleted as well.

Request type `DELETE`

Endpoint `/projects/:projectid/files/:fileid`

## Get a file [​](https://docs.samply.app/#get-a-file)

This endpoint returns a [box object](https://docs.samply.app/#box-object) for a given file, folder, or stack by id.

Request type `GET`

Endpoint `/projects/:projectid/files/:fileid`

## Update a file [​](https://docs.samply.app/#update-a-file)

This endpoint updates an existing file, folder, or stack and returns a [box object](https://docs.samply.app/#box-object).

Request type `POST`

Endpoint `/projects/:projectid/files/:fileid`

### Attributes [​](https://docs.samply.app/#attributes)

js

```
{
  name: string,
  addids: string[],
  removeids: string[],
}
```

---

#### name string optional

The display name of the box.

---

#### addids string array optional

Array of child box ids to add. Applies to folders and stacks.

---

#### removeids string array optional

Array of child box ids to remove. Applies to folders and stacks.

## List all files [​](https://docs.samply.app/#list-all-files)

This endpoint returns an array of all [box objects](https://docs.samply.app/#box-object) within a project, including files, folders, and stacks. Hidden boxes are excluded.

Request type `GET`

Endpoint `/projects/:projectid/all`

## Folders [​](https://docs.samply.app/#folders)

Folders are organizational containers within a project. They can contain files and folders.

### Create a folder [​](https://docs.samply.app/#create-a-folder)

This endpoint creates a folder within a project and returns a [box object](https://docs.samply.app/#box-object) with `object: "folder"`.

Request type `POST`

Endpoint `/projects/:projectid/folders`

### Attributes [​](https://docs.samply.app/#attributes-1)

js

```
{
  name: string,
  color: string,
}
```

---

#### name string

Display name of the folder.

---

#### color string optional

Folder color in hex format (e.g. #ff0000).

### List folders [​](https://docs.samply.app/#list-folders)

This endpoint returns an array of folder [box objects](https://docs.samply.app/#box-object) within a project.

Request type `GET`

Endpoint `/projects/:projectid/folders`

## Stacks [​](https://docs.samply.app/#stacks)

Stacks group multiple versions of a file together. Each child in a stack represents a different version.

### Create a stack [​](https://docs.samply.app/#create-a-stack)

This endpoint creates a stack within a project and returns a [box object](https://docs.samply.app/#box-object) with `object: "stack"`.

Request type `POST`

Endpoint `/projects/:projectid/stacks`

### Attributes [​](https://docs.samply.app/#attributes-2)

js

```
{
  name: string,
  childids: string[],
}
```

---

#### name string

Display name of the stack.

---

#### childids string array

An ordered array of file box ids to group into this stack.

## Box object [​](https://docs.samply.app/#box-object)

Files, folders, and stacks are all represented as box objects.

js

```
{
  id: string,
  object: "file" | "folder" | "stack",
  name: string,
  color: string,
  timeCreated: number,
  children: [
    {
      id: string,
      name: string,
    }
  ],
  duration: number,
}
```

---

#### id string readonly

Box id.

---

#### object 'file' | 'folder' | 'stack' readonly

The type of box.

---

#### name string readonly

Display name.

---

#### color string readonly

Color in hex format.

---

#### timeCreated number readonly

Time created in millis since Unix epoch.

---

#### children array readonly optional

Child boxes. Present on folders and stacks.

###### Child attributes

---

#### id string readonly

Child box id.

---

#### name string readonly

Child label name.

---

#### duration number readonly optional

Duration of the audio file in seconds, rounded to hundredths of a second. Only present on audio file boxes.