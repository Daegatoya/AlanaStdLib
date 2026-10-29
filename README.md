# AlanaStdLib v0.2
<img src="alana.png" alt="Alana Logo" width="500">

> Check out the official [Alana website](https://csalana.com)

> Check out the official [Alana runtime](https://github.com/Daegatoya/Alana)
<hr>

**Welcome to AlanaStdLib**, the official standard library made for the [Alana programming language](https://csalana.com).

Currently, the standard library is only available through the official Alana language's download.

## What is currently included in the stdlib
- [x] HTTP POST/GET
- [x] JSON Serialize
- [x] Error Handler

<hr>

## Here is the overview of every currently available libs in stdlib

### HTTP
<details>

| Function | Description | Parameters | Returns |
|------|-------------|-------------|------|
| `HTTP.Get()` | Sends a GET request to an URL | `str url` | A response object |
| `HTTP.Post()` | Sends a POST request to an URL | `str url`, `str body`, `str content type` | A response object |
    
</details>

### Response
<details>

Response is an object type directly included with the HTTP library.

| Function | Description | Parameters | Returns |
|------|-------------|-------------|------|
| `Response.GetStatus()` | Gives you the status of the response | None | The status as a `num` |
| `Response.GetBody()` | Gives you the body of the response | None | The body as a `str` |
| `Response.GetHeader()` | Gives you a header of the response | `str header name` | The header as a `str` |
    
</details>

### JSON
<details>

| Function | Description | Parameters | Returns |
|------|-------------|-------------|------|
| `JSON.Serialize()` | Serializes your value as JSON | `any value to serialize` | The JSON value as a `str` |
    
</details>

### Error
<details>

The `Error` class does not contain any method. Therefore, it works with basic strings or the built-in `error` keyword like so:

```txt
// First case
try;
    showln "Hello";
end;
catch(error);
    throw newobj Error(error);
end;

// Second case
throw newobj Error("Error 1: wrong type");
```
    
</details>

<hr>

**A code using Alana's standard library could look like this:**

```txt
including "stdlib/http.alana";
including "stdlib/json.alana";
including "stdlib/error.alana";

define Http http is newobj Http();
define Json json is newobj Json();

define func Serialize(any value) returning str;
    return call json.Serialize(value);
end;

define func SendRequest(str method, str url, str jsonBody) returning str;
    if method sameas "GET";
        return call http.Get(url).GetBody();
    elseif method sameas "POST";
        return call http.Post(url, jsonBody, "application/json").GetBody();
    else;
        return "";
    end;
end;

define str body is "{
    \"name\": \"John Doe\",
    \"age\": 30,
    \"email\": \"johndoe@example.com\"
}";

define str parsedBody is call Serialize(body);

while true;
    try;
        showln "---- Sending POST Request----";
        showln;
        showln "Press Enter to send a POST request to https://postman-echo.com/post";
        readln;
    
        showln call SendRequest("POST", "https://postman-echo.com/post", parsedBody);
    
        showln "---- Sending GET Request----";
        showln;
        showln "Press Enter to send a GET request to https://postman-echo.com/get";
        readln;
    
        showln call SendRequest("GET", "https://postman-echo.com/get?phrase=HelloWorld", parsedBody);
    end;
    catch(error);
        throw newobj Error(error);
    end;
end;
```

<hr>

This library will obviously keep growing alongside Alana and becoming bigger as I keep adding more stuff to the official language.

Some keywords might change with time, this is truly just the beginning of it.

Stay aware for future updates!

*And don't forget to ⭐ the repo!*

> Copyright © Daegatoya - 2026 | AlanaStdLib v0.1 | Branch of Alana v2.0
