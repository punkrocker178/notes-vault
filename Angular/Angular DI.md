# Dependency Injection
Dependency provider types:
- `useClass` :  Instantiate with given class when the service is injected
```typescript
providers: [
  { provide: Logger, useClass: ConsoleLogger }
]
```

- useValue:  Binds the service with a specific value. Suitable for mocking data in unit tests
```typescript
providers: [
  { provide: 'API_URL', useValue: 'https://api.example.com' },
  { provide: UserService, useValue: mockedUserServiceSpyObj }
]
```

- `useFactory`: Provide service with it's own dependency through a function.
```typescript
providers: [
  {
    provide: Logger,
    useFactory: (config: ConfigService) => 
      new AdvancedLogger(config.logLevel),
    deps: [ConfigService]
  }
]
```

- `useExisting`: Set multiple token/service name points to a single service (Aliasing)
```typescript
providers: [
  { provide: Logger, useClass: FileLogger },
  { provide: FileLoggerAlias, useExisting: Logger }
]
```

Hierarchical injectors:
![Angular-hierachical-injectors](https://raw.githubusercontent.com/punkrocker178/notes-vault/refs/heads/main/img/hierarchical-injectors.png)

![[Services#Injectable() Decorator]]