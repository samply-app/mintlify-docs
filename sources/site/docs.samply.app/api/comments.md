# Source: https://docs.samply.app/api/comments.html

# Comments [​](https://docs.samply.app/#comments)

Comments can be read or created for a given file directly through the API. Take advantage of timecoding, completion flags, and replies to organize your workflow and keep feedback in one place.

## Create a comment [​](https://docs.samply.app/#create-a-comment)

This endpoint creates a comment and returns a [comment object](https://docs.samply.app/./comments.html#comment-object). The fileid must be the id of the a specific version. If the fileid is the id of a stack, no comment will be created.

Request type `POST`

Endpoint `/projects/:projectid/files/:fileid/comments`

### Attributes [​](https://docs.samply.app/#attributes)

js

```
{
  completed: boolean,
  message: string,
  parentid: string,
  pinned: boolean,
  audioTimestamp: number,
  audioTimestampEnd: number,
}
```

---

#### message string

Markdown text content of the comment. Best practice is to wrap the message in paragraph tags.

---

#### parentid string optional

Parent comment id if this comment is a reply. Parent comment must not be a reply.

---

#### completed boolean optional

Indicates if the comment is marked complete.

---

#### pinned boolean optional

Indicates if the comment is pinned.

---

#### audioTimestamp number optional

Comment start-time (in seconds). If time is not a range, only this field needs to be set. Replies will not display timecodes.

---

#### audioTimestampEnd number optional

Comment end-time (in seconds). Replies will not display timecodes.

## Update a comment [​](https://docs.samply.app/#update-a-comment)

This endpoint is not yet available. Need it now? Reach out to our lead API engineer at [matt@samplyaudio.com](mailto:matt@samplyaudio.com).

## Get a comment [​](https://docs.samply.app/#get-a-comment)

This endpoint is not yet available. Need it now? Reach out to our lead API engineer at [matt@samplyaudio.com](mailto:matt@samplyaudio.com).

## List comments [​](https://docs.samply.app/#list-comments)

This endpoint lists all comments for a given file and returns an array of [comment objects](https://docs.samply.app/./comments.html#comment-object).

Request type `GET`

Endpoint `/projects/:projectid/files/:fileid/comments`

## Comment object [​](https://docs.samply.app/#comment-object)

All comment actions will return a comment object with the following structure.

### Attributes [​](https://docs.samply.app/#attributes-1)

js

```
{
  audioTimestamp: number;
  audioTimestampEnd: number;
  completed: boolean;
  creator: samply.firestore.UserSnippet;
  id: string;
  isReply: boolean;
  message: string;
  object: "comment";
  parentid: string;
  reactions: {
    [emoji: string]: {
      count: number;
      users: { [uid: string]: samply.firestore.UserSnippet };
    };
  };
  timeCreated: number;
  timeModified: number;
}
```

---

#### audioTimestamp number readonly

Comment start-time (in seconds). If time is not a range, the timestamp will be available in this attribute.

---

#### audioTimestampEnd number readonly

Comment end-time (in seconds).

---

#### completed boolean readonly

Indicates if the comment is marked complete.

---

#### creator object readonly

User who created the comment.

###### Child attributes

---

#### displayName string readonly

Human-readable display name.

---

#### email string readonly

Email address.

---

#### photoURL string readonly

Profile picture URL.

---

#### uid string readonly

User id.

---

#### id string readonly

Comment id.

---

#### isReply boolean readonly

Indicates if the comment is a reply.

---

#### message string readonly

Markdown text content of the comment.

---

#### object string readonly

Object type of returned object. Always 'comment'

---

#### parentid string readonly

Parent comment id if this comment is a reply.

---

#### reactions object readonly

Reactions added to the comment.

###### Child attributes

---

#### emoji object readonly

The emoji object. Keyed on emoji string name. See below for attributes.

---

#### emoji object readonly

Information about emoji reactions to a comment.

###### Child attributes

---

#### count number readonly

Number of times this reaction has been added.

---

#### users object readonly

Map of users who reacted.

---

#### timeCreated number readonly

Time created in millis since Unix epoch.

---

#### timeModified number readonly

Time modified in millis since Unix epoch.