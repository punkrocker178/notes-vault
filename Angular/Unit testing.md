## Testing a component

In order to unit test a component, we have to define test cases in `.spec.ts` file.
We should let the `spec` file have the same name as the component we want testing.
Default unit testing tool is `jasmine`

### Preparations for for the testing component

Tested component is initialized and ran in an encapsulated environment (jasmine server) and not related to any modules. Therefore, we have to import/provide nessessary modules/services & other dendencies for the component to run.
The general rule of thumb is to mock the denpendencies as many as possible, as we only need to test our logic within the scope of this component.
Below is the code to setup our test component.

```typescript
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [ HomeComponent ],
      imports: [ 
        CoreModule,
        SharedModule
      ],
      provides: [
        ServiceA,
        { provide: ServiceB: useValue: spyServiceB }
      ]
    })
    .compileComponents();
  });

  beforeEach(() => {
    fixture = TestBed.createComponent(HomeComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });
```

`beforeEach`: is a callback function to let jasmine run this function for every `it` declared.
Then we will call `TestBed.configureTestingModule` to create the testing component for us. The parameter of this function is an object which has the same structure of an Angular module.

### Define a test case

```typescript
it('test case name', () => {
// define mock data
// expect
})
```

Every test case should be defined in a callback function `it` to let jasmine know.
In this callback, we can define our testing logic and make assertion by calling `expect` function.
`expect` function takes in a value need testing, it will then return a `Matcher` object that have many functions (`toBe`, `toEqual`, ...) to compare with the expected value.
