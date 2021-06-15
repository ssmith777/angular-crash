# AngularCrash

### This is a crash course/example angular app

- Done 6-21 ish Angular Contract :) coming my way
- Jumping from the React world to Angular

Notes: Angular Crash Course

- When do I want to build my own modules & how do I do so?
- Application state ? Do I use redux or does it use its own

Add npm package:

- ng add @fortawesome/angular-fontawesome
- Note: you can do npm install as well, however NG add will install multi packages if they are needed for component you are installing

Http: (HttpClient, HttpHeaders)

- Note: Angular has its own http library it uses
- Steps

  - add import to component class that will make http requests/calls

  ```
    import {HttpClient, HttpHeaders} from '@angular/common/http'
  ```

  - In app.module add import & import to ngModule

  ```
    import { HttpClientModule } from '@angular/common/http';

    @NgModule({imports: [HttpClientModule]})
  ```

  - In constructor of service class add params to constructor parameter declaration

  ```
      constructor(private http: httpClient) {}
  ```

  Examples of Http methods in service class

  ```
  getTasks(): Observable<Task[]> {
    return this.http.get<Task[]>(this.apiUrl);
  }

  deleteTask(task: Task): Observable<Task> {
    const url = `${this.apiUrl}/${task.id}`;
    return this.http.delete<Task>(url);
  }
  ```

  Examples in Component Class calling service methods using HTTP

  ```
  ngOnInit(): void {
    this.taskService.getTasks().subscribe((tasks) => (this.tasks = tasks));
  }

  deleteTask(task: Task) {
    this.taskService
      .deleteTask(task)
      .subscribe(
        () => (this.tasks = this.tasks.filter((t) => t.id != task.id))
      );
  }
  ```

Observables:

- In the service
  - ```
      import { Observable, of } from 'rxjs';
    ```
  - Add class method
    ```
      getTasks(): Observable<Task[]> {
        const tasks = of(TASKS);
        return tasks;
      }
    ```
- In the component consuming the observable
  - Add import to component that is using service (import service)
  - Add this to ngOnInit()
  ```
   ngOnInit(): void {
    this.taskService.getTasks().subscribe((tasks) => (this.tasks = tasks));
  }
  ```
  Create Service:
- ng generate service services/task
- Add method to class
- Add import to component that is using service
- Add params to class constructor
- If adding to init(quick a dirty method)
  ```
    Add service method call in ngOnInit()
    ngOnInit(): void {
      this.tasks = this.taskService.getTasks();
    }
  ```
- With Observable method
  - Add service method call
    ```
    getTasks(): Observable<Task[]> {
      const tasks = of(TASKS);
      return tasks;
    }
    ```

Create a Module:

Create a Component:

```
 ng generate component <folder/file>
```

Create event for component

- In component html, on the html element add
  ```
    (click)="onClick()"
  ```
- In component class file add
  ```
    function onClick() {}
  ```
- Add Output & EventEmitter Class
  - to imports
- Add to Class
  ```
    @Output <btnClick> = new EventEmitter();
  ```
  - In function add
    ```
      this.btnClick.emit();
    ```
  - Note: This just adds an emitter to our function
- Navigate to the components html that is rendering our component above
  ```
  Add (btnClick)="toggleAddTask()"
  ```
- To the component

- Navigate to component class that is rendering this component
  - Add function in class for component
    ```
      toggleAddTask() {}
    ```
