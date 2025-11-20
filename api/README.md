# Polly Notes API

## Methods

### /notes

#### GET - Runs the lambda list-function

- Expected API input

  - Authorization Header

- Function test event

```json
{
"requestContext": {
  "authorizer": {
    "claims": {
      "cognito:username": "student"}
      }
    }
}
```

- Output returned to client

```json
{
  "isBase64Encoded": false,
  "statusCode": 200,
  "body": "[{\"UserId\": \"student\", \"Note\": \"My note to myself\", \"NoteId\": \"001\"}, {\"UserId\": \"student\", \"Note\": \"My new note to myself\", \"NoteId\": \"002\"}]",
  "headers": {
    "Content-Type": "application/json",
    "Access-Control-Allow-Origin": "*"
  }
}
```

#### POST - Runs the lambda createUpdate-function

- Expected API input

  - Authorization header
  - Request Body with json object string containing a NoteId and note text

- Function test event

```json
{
"requestContext": {
  "authorizer": {
    "claims": {
      "cognito:username": "student"}
      }
    },
"body": "{\"NoteId\":\"999\",\"Note\":\"lambda test note\"}"
}
```
  
- Output returned to client

```json
{
  "isBase64Encoded": false,
  "statusCode": 200,
  "body": "999",
  "headers": {
    "Content-Type": "application/json",
    "Access-Control-Allow-Origin": "*"
  }
}
```

### /notes/search

#### GET - Runs the lambda search-function

- Expected API input

  - Authorization Header
  - A "text" query string parameter with the search tearm

- Function test event

```json
{
"requestContext": {
  "authorizer": {
    "claims": {
      "cognito:username": "student"}
      }
    },
"queryStringParameters": {"text": "new note"}
}
```

- Output returned to client

```json
{
  "isBase64Encoded": false,
  "statusCode": 200,
  "body": "[{\"UserId\": \"student\", \"Note\": \"My new note to myself\", \"NoteId\": \"002\"}]",
  "headers": {
    "Content-Type": "application/json",
    "Access-Control-Allow-Origin": "*"
  }
}

```

### /notes/{id}

#### DELETE - Runs the lambda delete-function

- Expected API input

  - Authorization header
  - Note ID in the request path to delete

- Function test event

```json
{
"requestContext": {
  "authorizer": {
    "claims": {
      "cognito:username": "student"}
      }
    },
"pathParameters": {"id": "999"}
}
```
  
- Output returned to client

```json
Response
{
  "isBase64Encoded": false,
  "statusCode": 200,
  "body": "999",
  "headers": {
    "Content-Type": "application/json",
    "Access-Control-Allow-Origin": "*"
  }
}


```

#### POST - Runs the lambda dictate-function

- Expected API input

  - Authorization header
  - Note ID in the request path to dictate
  - Request Body with json object string containing the polly voice to use

- Function test event

```json
{
"requestContext": {
  "authorizer": {
    "claims": {
      "cognito:username": "student"}
      }
    },
"pathParameters": {"id": "999"},
"body": "{\"voice\":\"Joey\"}"
}
```
  
- Output returned to client

```json
{
  "isBase64Encoded": false,
  "statusCode": 200,
  "body": "\"https://lab-7-pollynotesmp3-1rpbmkboij9mz.s3.amazonaws.com/student/999.mp3?AWSAccessKeyId=AKIAIOSFODNN7EXAMPLE&Signature=LONGSAMPLEKEYTHATHASALONGSTRINGOFCHARACTERS&x-amz-security-token=LONGSAMPLEKEYTHATHASALONGSTRINGOFCHARACTERS&Expires=1619808459\"",
  "headers": {
    "Content-Type": "application/json",
    "Access-Control-Allow-Origin": "*"
  }
}

```
