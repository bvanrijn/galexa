# galexa
The chat app without a client

## API overview

All paths are relative to `base_url`.  
`base_url` is currently `https://galexa.herokuapp.com`.

## Index or `/`

Get all endpoints.

```
{
    "computer": 0, 
    "endpoints": [
        "/", 
        "/status", 
        "/message/write", 
        "/message/read"
    ], 
    "human": "OK", 
    "time": 1474464099
}
```

## Status or `/status`
**Note**: if you don't receive a reply of any kind within 10 seconds, the server is probably down.

On success:

```
{
    "computer": 0, 
    "human": "OK", 
    "ok": true, 
    "time": 1474462174
}
```

## Write or `/message/write`

Send new message

Example: `GET /message/write?message=hello+world`

```
{
    "computer": 0, 
    "hash": "5eb63bbbe01eeed093cb22bb8f5acdc3", 
    "human": "OK", 
    "length": 11, 
    "message": "hello world", 
    "ok": true, 
    "time_sent": 1474462334
}
````

## Read or `/message/read`

Get all messages

Example: `GET /message/read`

```
[
    {
        "computer": 0, 
        "hash": "6d0007e52f7afb7d5a0650b0ffb8a4d1", 
        "human": "OK", 
        "length": 2, 
        "message": "yo", 
        "ok": true, 
        "time_sent": 1474462408
    },
    {
        "computer": 0, 
        "hash": "5eb63bbbe01eeed093cb22bb8f5acdc3", 
        "human": "OK", 
        "length": 11, 
        "message": "hello world", 
        "ok": true, 
        "time_sent": 1474462268
    }
]
```

## Response format

(This section tries to use [simple words](https://www.xkcd.com/simplewriter/) because it's fun)

The response format is JSON.

The following keys will always be there:

- `computer`: a number that tells computers what's going on. `0` means everything is okay and any other number means something is wrong
- `human`: like `computer`, but for humans. You can show this message to humans if something goes wrong
- `ok`: can be `true` or `false`, _but use `computer` instead_

The following keys might be there, depending on context:

- `hash`: the MD5 hash of a message
- `length`: how long the message is
- `time`: what time it is
- `time_sent`: what time it was when the message was sent
