
# HTTP RESPONSE CODES

You may encounter the following response codes. Any unsuccessful response codes will contain more information to help you identify the cause of the problem.

Code | Meaning
-----|--------------------------
200  | The request has succeeded.
201  | The request has been fulfilled and resulted in a new resource being created. The newly created resource can be referenced by the URI(s) returned in the entity of the response, with the most specific URI for the resource given by a Location header field.
404  | Not Found. The requested resource was not found. The response body will explain which resource was not found.
500  | Internal Server Error. The server encountered an error while processing your request and failed. Please report this to the Divido support team.