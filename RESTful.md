# RESTful API documentation
by siriuskoan

## bot
Header should contain `Authorization: Bearer <user token>`.
### /status
`GET /status`
Get simplified status

**request**
```
{}
```

**response**
```
{
   "10.1.1.1":"ok",
   "10.1.1.2":"ok",
   "10.1.1.3":"fail",
   "10.1.1.4":"ok"
}
```

`GET /status?mode=verbose`
Get verbose status

**request**
```
{}
```

**response**
```
{
    "10.1.1.1": {
        "status": "ok",
        "uptime": "86400",
        "reconnect_times": "5",
        "role": "client"
    },
    "10.1.1.2": {
        "status": "ok",
        "uptime": "1234",
        "reconnect_times": "10",
        "role": "host"
    }
    "10.1.1.3": {
        "status": "failed",
        "uptime": "0",
        "reconnect_times": "100",
        "role": "client"
    }
}
```

notes:
 - The `reconnect_times` is represented in second.
 - If the `reconnect_times` field is zero and the client is disconnected, it means the client disconnect by himself or herself.

## client
Header should contain `Authorization: Bearer <user token>` except for `/login`
### /login
`POST /login`

**request**
```
{
	"password": "123456",
	"key": "<ssh public key>"
}
```

**response**
```
{
	"status": "ok",
	"token": "<user token>"
}
```

```
{
	"status": "failed",
	"message": "Wrong password"
}
```
The error message can be:
 - Wrong password (*from backend server*)

### /connect
`GET /connect`
Get connection status.

**request**
```
{}
```

**response**
```
{"status": "ok"}
```

```
{"status": "fail", "message": "Invalid token."}
```
The error messages can be:
 - Invalid token. (*from backend server*)
 - Server does not allow new connection now. (*from backend server*)
 - No resources are available. (*from ssh tunnel lib*)

`DELETE /connect`
Tell the server you are disconnecting from the ssh tunnel.

**request**
```
{}
```

**response**
The response is useless.
```
{"status": "ok"}
```

`PUT /connect`
Tell the server you are reconnecting to the ssh tunnel.

**request**
```
{}
```

**response**
```
{"status": "ok"}
```

```
{"status": "fail", "message": "Invalid token."}
```

The error messages are the same as `GET`.

### /host
Header should contain `Authorization: Bearer <user token>`

`POST /host`
Tell the server you want to be the host, if the host has retired, you can be the new host.

**request**
```
{}
```

**response**
```
{"status": "ok"}
```

```
{"status": "failed", "message": "Host is some one else now."}
```

`DELETE /host`
Tell the server you don't want to be the host and allow others to be the new host.

**request**
```
{}
```

**response**
```
{"status": "ok"}
```

```
{"status": "failed", "message": "You are not host."}
```
