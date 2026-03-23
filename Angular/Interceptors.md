#HttpClient
# Definition
> Interceptors are middleware that allows common patterns around retrying, caching, logging, and authentication to be abstracted away from individual requests.

`HttpClient` supports functional interceptors and DI-based interceptors

# Functional interceptors
Example of intercepting requests to log data
```typescript
export function loggingInterceptor(
  req: HttpRequest<unknown>,
  next: HttpHandlerFn,
): Observable<HttpEvent<unknown>> {
  console.log(req.url);
  return next(req);
}
```

Usage in application
`withInteceptors` supports an array of interceptors for chaining.
```typescript
bootstrapApplication(App, {
  providers: [provideHttpClient(withInterceptors([loggingInterceptor]))],
});
```

# DI-Based interceptors
To make this work, the interceptor has to implement `HttpInterceptor` interface.
```typescript
@Injectable()
export class LoggingInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    console.log('Request URL: ' + req.url);
    return next.handle(req);
  }
}
```

Usage in application
```typescript
bootstrapApplication(App, {
  providers: [
    provideHttpClient(
      // DI-based interceptors must be explicitly enabled.
      withInterceptorsFromDi(),
    ),
    {provide: HTTP_INTERCEPTORS, useClass: LoggingInterceptor, multi: true},
  ]
});
```

# Chaining interceptors
As mentioned above, a request can have multiple inteceptors chained together with the order based on your specification.
In example, if you have multiple inteceptors setup for the `HttpClient`
```
Request -> A -> B -> C -> backend
```

The order of A, B, C is defined when you setup declare the inteceptors in the array of `withInterceptors`
```
// function based interceptors
withInterceptors([A, B, C])

// DI based interceptors
providers: [
  { provide: HTTP_INTERCEPTORS, useClass: A, multi: true },
  { provide: HTTP_INTERCEPTORS, useClass: B, multi: true },
  { provide: HTTP_INTERCEPTORS, useClass: C, multi: true },
]
```

**Note**: DI-based interceptors run in the order that their providers are registered. In an app with an extensive and hierarchical DI configuration, this order can be very hard to predict.

The order of the response will be
```
backend -> C -> B -> A
```

**Note**: Each interceptor should call  `next(req)` or  `next.handle(req) (DI-based)` for the chain to continue, usually after cloning or modifying the request

# Modifying requests
Most aspects of [`HttpRequest`](https://angular.dev/api/common/http/HttpRequest) and [`HttpResponse`](https://angular.dev/api/common/http/HttpResponse) instances are _immutable_, and interceptors cannot directly modify them. Instead, interceptors apply mutations by cloning these objects using the `.clone()` operation, and specifying which properties should be mutated in the new instance. This might involve performing immutable updates on the value itself (like [`HttpHeaders`](https://angular.dev/api/common/http/HttpHeaders) or [`HttpParams`](https://angular.dev/api/common/http/HttpParams)).

For example, to add a header to a request:
```typescript
const reqWithHeader = req.clone({  headers: req.headers.set('X-New-Header', 'new header value'),});
```

This immutability allows most interceptors to be idempotent if the same [`HttpRequest`](https://angular.dev/api/common/http/HttpRequest) is submitted to the interceptor chain multiple times. This can happen for a few reasons, including when a request is retried after failure.