# Angular Interview Questions and Answers

> Based on [roadmap.sh/angular](https://roadmap.sh/angular) and [angular.dev/overview](https://angular.dev/overview)

---

## Table of Contents
1. [Introduction to Angular](#introduction-to-angular)
2. [TypeScript Fundamentals](#typescript-fundamentals)
3. [Components](#components)
4. [Templates and Data Binding](#templates-and-data-binding)
5. [Directives](#directives)
6. [Services and Dependency Injection](#services-and-dependency-injection)
7. [Routing and Navigation](#routing-and-navigation)
8. [Forms](#forms)
9. [HTTP Client](#http-client)
10. [RxJS and Observables](#rxjs-and-observables)
11. [Change Detection](#change-detection)
12. [Modules](#modules)
13. [Pipes](#pipes)
14. [Lifecycle Hooks](#lifecycle-hooks)
15. [Advanced Topics](#advanced-topics)
16. [Performance Optimization](#performance-optimization)
17. [Testing](#testing)
18. [Angular CLI](#angular-cli)
19. [State Management](#state-management)
20. [Security](#security)

---

## Introduction to Angular

### Q1. What is Angular? (Easy)

**Answer:**
Angular is a web framework maintained by Google that empowers developers to build fast, reliable applications. It provides a comprehensive suite of tools, APIs, and libraries to simplify development workflows. Angular is a complete rewrite of AngularJS and uses TypeScript as its primary language. It follows a component-based architecture and supports building single-page applications (SPAs) and progressive web apps (PWAs).

**Key Features:**
- Component-based architecture
- Two-way data binding
- Dependency injection
- Built-in routing
- Forms handling
- HTTP client
- Testing support

---

### Q2. What are the key differences between Angular and AngularJS? (Medium)

**Answer:**
| Feature | AngularJS | Angular |
|---------|-----------|---------|
| Language | JavaScript | TypeScript |
| Architecture | MVC pattern | Component-based |
| Mobile Support | Limited | Excellent (Ionic, NativeScript) |
| Performance | Slower | Faster (AOT compilation) |
| Dependency Injection | Limited | Full-featured hierarchical DI |
| Routing | ngRoute | RouterModule |
| Change Detection | Dirty checking | Zone.js with optimized strategies |
| Bundle Size | Larger | Smaller (tree-shaking) |
| Learning Curve | Easier | Steeper but more powerful |

---

### Q3. What is the current version of Angular, and how is versioning handled? (Easy)

**Answer:**
Angular follows semantic versioning (semver) and releases major versions every 6 months. The current stable version is Angular 17+ (as of 2024). Angular uses a predictable release schedule:
- **Major versions:** Every 6 months with breaking changes
- **Minor versions:** Feature additions (backward compatible)
- **Patch versions:** Bug fixes

Angular also provides migration tools and upgrade guides for moving between versions.

---

## TypeScript Fundamentals

### Q4. Why does Angular use TypeScript instead of JavaScript? (Easy)

**Answer:**
Angular uses TypeScript because it provides:
1. **Static Typing:** Catches errors at compile-time, reducing runtime errors
2. **Better IDE Support:** Enhanced autocomplete, refactoring, and navigation
3. **Improved Maintainability:** Self-documenting code with type annotations
4. **Advanced Features:** Classes, interfaces, decorators, generics, and more
5. **ECMAScript Support:** Access to latest JavaScript features with transpilation
6. **Better Tooling:** Strong integration with development tools

TypeScript compiles to JavaScript, ensuring browser compatibility while providing a better development experience.

---

### Q5. What are Decorators in TypeScript, and how are they used in Angular? (Medium)

**Answer:**
Decorators are special declarations that can be attached to classes, methods, properties, or parameters. In Angular, decorators are used extensively:

```typescript
// Component decorator
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent { }

// Injectable decorator
@Injectable({
  providedIn: 'root'
})
export class UserService { }

// Input and Output decorators
@Input() userName: string;
@Output() userSelected = new EventEmitter();
```

**Common Angular Decorators:**
- `@Component()` - Defines a component
- `@Injectable()` - Marks a class as injectable service
- `@NgModule()` - Defines a module
- `@Directive()` - Defines a directive
- `@Input()` - Marks property as input
- `@Output()` - Marks property as output
- `@Pipe()` - Defines a pipe

---

### Q6. Explain Interfaces and Classes in TypeScript with Angular examples. (Medium)

**Answer:**
**Interfaces** define contracts for objects:
```typescript
interface User {
  id: number;
  name: string;
  email: string;
}

// Usage in component
export class UserComponent {
  user: User = {
    id: 1,
    name: 'John Doe',
    email: 'john@example.com'
  };
}
```

**Classes** are used for components and services:
```typescript
export class UserService {
  private users: User[] = [];
  
  getUsers(): User[] {
    return this.users;
  }
  
  addUser(user: User): void {
    this.users.push(user);
  }
}
```

---

## Components

### Q7. What is a Component in Angular? (Easy)

**Answer:**
A component is a fundamental building block of an Angular application. It controls a portion of the user interface (view) and consists of:

1. **TypeScript Class:** Contains the component's logic and data
2. **HTML Template:** Defines the view structure
3. **CSS Styles:** Component-specific styling
4. **Metadata:** Decorator with configuration

```typescript
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent {
  title = 'User Management';
}
```

**Component Responsibilities:**
- Display data in the view
- Handle user interactions
- Communicate with services
- Manage component state

---

### Q8. How do you create a component using Angular CLI? (Easy)

**Answer:**
```bash
# Basic component
ng generate component user

# With options
ng generate component user --skip-tests --inline-style --inline-template

# Short form
ng g c user

# Generate in specific folder
ng g c features/user/user-profile
```

**Generated Files:**
- `user.component.ts` - Component class
- `user.component.html` - Template
- `user.component.css` - Styles
- `user.component.spec.ts` - Unit tests

---

### Q9. What is the difference between a Component and a Directive? (Medium)

**Answer:**
| Feature | Component | Directive |
|---------|-----------|-----------|
| Template | Has its own template | No template (except structural directives) |
| Purpose | Controls a view | Adds behavior to existing elements |
| Selector | Element selector (e.g., `<app-user>`) | Attribute selector (e.g., `[appHighlight]`) |
| Usage | Reusable UI blocks | Extend HTML functionality |
| Metadata | `@Component()` | `@Directive()` |

**Note:** Components are actually directives with templates. All components are directives, but not all directives are components.

---

### Q10. Explain Component Communication in Angular. (Medium)

**Answer:**
Angular provides several ways for components to communicate:

**1. Parent to Child (Input Binding):**
```typescript
// Parent Component
<app-child [data]="parentData"></app-child>

// Child Component
@Input() data: string;
```

**2. Child to Parent (Output Events):**
```typescript
// Child Component
@Output() dataChanged = new EventEmitter<string>();
this.dataChanged.emit(newData);

// Parent Component
<app-child (dataChanged)="handleDataChange($event)"></app-child>
```

**3. ViewChild/ViewChildren:**
```typescript
// Parent Component
@ViewChild(ChildComponent) child: ChildComponent;
```

**4. Services (Shared State):**
```typescript
// Shared Service
@Injectable({ providedIn: 'root' })
export class DataService {
  private dataSubject = new BehaviorSubject<string>('');
  data$ = this.dataSubject.asObservable();
}
```

**5. Route Parameters:**
```typescript
this.route.params.subscribe(params => {
  const id = params['id'];
});
```

---

## Templates and Data Binding

### Q11. What is Data Binding in Angular? Explain all types. (Easy)

**Answer:**
Data binding is the synchronization between the component (model) and the view (template). Angular supports four types:

**1. Interpolation (`{{ }}`):**
```html
<h1>{{ title }}</h1>
<p>Welcome, {{ user.name }}!</p>
```

**2. Property Binding (`[property]`):**
```html
<img [src]="imageUrl" [alt]="imageAlt">
<button [disabled]="isDisabled">Click</button>
```

**3. Event Binding (`(event)`):**
```html
<button (click)="onClick()">Click Me</button>
<input (keyup)="onKeyUp($event)">
```

**4. Two-Way Binding (`[(ngModel)]`):**
```html
<input [(ngModel)]="userName">
<!-- Equivalent to: -->
<input [value]="userName" (input)="userName = $event.target.value">
```

---

### Q12. What is String Interpolation in Angular? (Easy)

**Answer:**
String interpolation is a one-way data binding technique that embeds expressions into template text using double curly braces `{{ }}`.

```html
<h1>Welcome, {{ userName }}!</h1>
<p>Total: {{ items.length }} items</p>
<p>Price: {{ price | currency }}</p>
<p>Date: {{ currentDate | date:'short' }}</p>
```

**Features:**
- Evaluates expressions and converts to strings
- Can use pipes for transformation
- Automatically updates when data changes
- Supports method calls: `{{ getFullName() }}`

---

### Q13. Explain Property Binding vs Attribute Binding. (Medium)

**Answer:**
**Property Binding** binds to DOM properties (JavaScript object properties):
```html
<!-- Property binding -->
<img [src]="imageUrl">  <!-- Sets the src property -->
<button [disabled]="isDisabled">Click</button>  <!-- Sets disabled property -->
```

**Attribute Binding** binds to HTML attributes (initial values):
```html
<!-- Attribute binding -->
<td [attr.colspan]="columnSpan">Content</td>
<button [attr.aria-label]="buttonLabel">Click</button>
```

**Key Differences:**
- Properties reflect the current state; attributes are initial values
- Properties can be any type; attributes are always strings
- Properties can change; attributes are set once
- Use `[attr.attributeName]` for attribute binding

---

### Q14. What is Two-Way Data Binding, and how does it work? (Medium)

**Answer:**
Two-way data binding combines property binding and event binding to keep the component and view in sync.

```typescript
// Component
export class UserComponent {
  userName = 'John';
}
```

```html
<!-- Template -->
<input [(ngModel)]="userName">
<p>You entered: {{ userName }}</p>
```

**How it works:**
1. `[ngModel]` binds the value from component to input
2. `(ngModelChange)` event updates the component when input changes
3. Changes in either direction update the other

**Note:** Requires `FormsModule` to be imported:
```typescript
import { FormsModule } from '@angular/forms';
```

---

## Directives

### Q15. What are Directives in Angular? (Easy)

**Answer:**
Directives are classes that add behavior to elements in Angular applications. There are three types:

**1. Components:** Directives with templates
```typescript
@Component({ selector: 'app-user', template: '...' })
```

**2. Structural Directives:** Change DOM structure (prefixed with `*`)
- `*ngIf` - Conditionally includes/excludes elements
- `*ngFor` - Repeats elements
- `*ngSwitch` - Conditional rendering

**3. Attribute Directives:** Change appearance or behavior
- `ngClass` - Dynamically add/remove CSS classes
- `ngStyle` - Dynamically set inline styles

---

### Q16. Explain Structural Directives: *ngIf, *ngFor, and *ngSwitch. (Medium)

**Answer:**
**1. *ngIf:**
```html
<div *ngIf="isLoggedIn">Welcome back!</div>
<div *ngIf="user; else noUser">Hello, {{ user.name }}</div>
<ng-template #noUser>Please log in</ng-template>
```

**2. *ngFor:**
```html
<ul>
  <li *ngFor="let user of users; let i = index; let first = first">
    {{ i + 1 }}. {{ user.name }}
  </li>
</ul>

<!-- With trackBy for performance -->
<li *ngFor="let user of users; trackBy: trackByUserId">
  {{ user.name }}
</li>
```

```typescript
trackByUserId(index: number, user: User): number {
  return user.id;
}
```

**3. *ngSwitch:**
```html
<div [ngSwitch]="status">
  <p *ngSwitchCase="'active'">Active</p>
  <p *ngSwitchCase="'inactive'">Inactive</p>
  <p *ngSwitchDefault>Unknown</p>
</div>
```

---

### Q17. How do you create a Custom Directive? (Medium)

**Answer:**
**Attribute Directive Example:**
```typescript
import { Directive, ElementRef, Renderer2, HostListener, Input } from '@angular/core';

@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  @Input() appHighlight: string = 'yellow';
  
  constructor(private el: ElementRef, private renderer: Renderer2) {}
  
  @HostListener('mouseenter') onMouseEnter() {
    this.highlight(this.appHighlight);
  }
  
  @HostListener('mouseleave') onMouseLeave() {
    this.highlight(null);
  }
  
  private highlight(color: string | null) {
    this.renderer.setStyle(this.el.nativeElement, 'background-color', color);
  }
}
```

**Usage:**
```html
<p appHighlight="lightblue">Hover over me!</p>
```

**Structural Directive Example:**
```typescript
@Directive({
  selector: '[appUnless]'
})
export class UnlessDirective {
  private hasView = false;
  
  constructor(
    private templateRef: TemplateRef<any>,
    private viewContainer: ViewContainerRef
  ) {}
  
  @Input() set appUnless(condition: boolean) {
    if (!condition && !this.hasView) {
      this.viewContainer.createEmbeddedView(this.templateRef);
      this.hasView = true;
    } else if (condition && this.hasView) {
      this.viewContainer.clear();
      this.hasView = false;
    }
  }
}
```

---

### Q18. What is the difference between ngClass and ngStyle? (Easy)

**Answer:**
**ngClass** - Dynamically adds/removes CSS classes:
```html
<!-- String -->
<div [ngClass]="'active'">Content</div>

<!-- Array -->
<div [ngClass]="['class1', 'class2']">Content</div>

<!-- Object -->
<div [ngClass]="{ 'active': isActive, 'disabled': isDisabled }">Content</div>

<!-- Method -->
<div [ngClass]="getClasses()">Content</div>
```

**ngStyle** - Dynamically sets inline styles:
```html
<!-- Object -->
<div [ngStyle]="{ 'color': textColor, 'font-size.px': fontSize }">Content</div>

<!-- Method -->
<div [ngStyle]="getStyles()">Content</div>
```

**Key Difference:**
- `ngClass` works with CSS classes (defined in stylesheets)
- `ngStyle` works with inline styles (direct style properties)

---

## Services and Dependency Injection

### Q19. What is a Service in Angular? (Easy)

**Answer:**
A service is a class that encapsulates reusable business logic, data access, or functionality that needs to be shared across multiple components. Services are typically marked with the `@Injectable()` decorator.

```typescript
@Injectable({
  providedIn: 'root'  // Makes it a singleton
})
export class UserService {
  private users: User[] = [];
  
  getUsers(): User[] {
    return this.users;
  }
  
  addUser(user: User): void {
    this.users.push(user);
  }
}
```

**When to use Services:**
- Share data between components
- Handle HTTP requests
- Implement business logic
- Share utility functions
- Manage application state

---

### Q20. What is Dependency Injection (DI) in Angular? (Medium)

**Answer:**
Dependency Injection is a design pattern where a class receives its dependencies from an external source rather than creating them itself. Angular's DI system provides dependencies to classes automatically.

**Benefits:**
- **Modularity:** Components are loosely coupled
- **Testability:** Easy to mock dependencies in tests
- **Maintainability:** Changes in one place affect all dependents
- **Reusability:** Services can be shared across components

**How it works:**
```typescript
// 1. Create a service
@Injectable({ providedIn: 'root' })
export class DataService { }

// 2. Inject into component
export class UserComponent {
  constructor(private dataService: DataService) { }
  
  // Angular automatically provides DataService instance
}
```

---

### Q21. Explain the Hierarchical Dependency Injection System. (Tough)

**Answer:**
Angular's DI system is hierarchical, meaning injectors are organized in a tree structure matching the component tree.

**Injector Hierarchy:**
1. **Root Injector:** Application-wide services (`providedIn: 'root'`)
2. **Module Injector:** Module-level providers
3. **Component Injector:** Component-level providers

```typescript
// Root level (singleton)
@Injectable({ providedIn: 'root' })
export class GlobalService { }

// Module level
@NgModule({
  providers: [ModuleService]
})
export class FeatureModule { }

// Component level
@Component({
  providers: [ComponentService]
})
export class UserComponent { }
```

**Service Resolution:**
- Angular looks for a provider starting from the component's injector
- If not found, it moves up to the parent component's injector
- Continues up to the root injector
- If still not found, throws an error

**Example:**
```typescript
// Parent Component
@Component({
  providers: [SharedService]  // Provides instance for this and child components
})
export class ParentComponent { }

// Child Component
export class ChildComponent {
  constructor(private sharedService: SharedService) {
    // Gets the same instance as parent
  }
}
```

---

### Q22. What are the different ways to provide services in Angular? (Medium)

**Answer:**
**1. Root Level (Recommended):**
```typescript
@Injectable({ providedIn: 'root' })
export class UserService { }
```
- Singleton across the entire application
- Tree-shakeable (removed if unused)

**2. Module Level:**
```typescript
@NgModule({
  providers: [UserService]
})
export class UserModule { }
```
- Available to all components in the module
- Not tree-shakeable

**3. Component Level:**
```typescript
@Component({
  providers: [UserService]
})
export class UserComponent { }
```
- New instance for each component instance
- Available to component and its children

**4. Lazy-loaded Module:**
```typescript
@Injectable()
export class UserService { }

@NgModule({
  providers: [UserService]
})
export class LazyModule { }
```
- Creates a separate instance for the lazy-loaded module

---

## Routing and Navigation

### Q23. What is Angular Router, and how does it work? (Easy)

**Answer:**
Angular Router is a powerful routing library that enables navigation between different views/components in a single-page application (SPA).

**Key Features:**
- Maps URLs to components
- Supports route parameters and query strings
- Provides route guards for authentication/authorization
- Supports lazy loading
- Handles browser history

**Basic Setup:**
```typescript
// app-routing.module.ts
const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'users', component: UserListComponent },
  { path: 'users/:id', component: UserDetailComponent },
  { path: '**', component: PageNotFoundComponent }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

```html
<!-- Template -->
<router-outlet></router-outlet>
<a routerLink="/users">Users</a>
```

---

### Q24. Explain Route Parameters, Query Parameters, and Route Data. (Medium)

**Answer:**
**1. Route Parameters (Required):**
```typescript
// Route definition
{ path: 'users/:id', component: UserDetailComponent }

// Accessing in component
constructor(private route: ActivatedRoute) {}
ngOnInit() {
  const id = this.route.snapshot.paramMap.get('id');
  // Or subscribe to changes
  this.route.paramMap.subscribe(params => {
    const id = params.get('id');
  });
}

// Navigation
this.router.navigate(['/users', userId]);
```

**2. Query Parameters (Optional):**
```typescript
// Navigation with query params
this.router.navigate(['/users'], { 
  queryParams: { page: 1, sort: 'name' } 
});

// Accessing in component
this.route.queryParams.subscribe(params => {
  const page = params['page'];
  const sort = params['sort'];
});
```

**3. Route Data:**
```typescript
// Route definition
{ 
  path: 'users', 
  component: UserComponent,
  data: { title: 'Users', requiresAuth: true }
}

// Accessing in component
this.route.data.subscribe(data => {
  const title = data['title'];
});
```

---

### Q25. What is Lazy Loading, and how do you implement it? (Medium)

**Answer:**
Lazy loading loads feature modules only when needed, reducing the initial bundle size and improving application startup time.

**Implementation:**
```typescript
// app-routing.module.ts
const routes: Routes = [
  {
    path: 'admin',
    loadChildren: () => import('./admin/admin.module').then(m => m.AdminModule)
  },
  {
    path: 'products',
    loadChildren: () => import('./products/products.module').then(m => m.ProductsModule)
  }
];
```

**Feature Module Routing:**
```typescript
// admin-routing.module.ts
const routes: Routes = [
  { path: '', component: AdminDashboardComponent },
  { path: 'users', component: AdminUsersComponent }
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class AdminRoutingModule { }
```

**Benefits:**
- Smaller initial bundle size
- Faster initial load time
- Better code organization
- Modules loaded on-demand

---

### Q26. What are Route Guards, and explain different types. (Medium)

**Answer:**
Route guards control whether a route can be activated or deactivated. They are interfaces that can be implemented as services.

**1. CanActivate:**
```typescript
@Injectable({ providedIn: 'root' })
export class AuthGuard implements CanActivate {
  constructor(private authService: AuthService, private router: Router) {}
  
  canActivate(): boolean {
    if (this.authService.isAuthenticated()) {
      return true;
    }
    this.router.navigate(['/login']);
    return false;
  }
}

// Usage
{ path: 'dashboard', component: DashboardComponent, canActivate: [AuthGuard] }
```

**2. CanActivateChild:**
```typescript
export class AdminGuard implements CanActivateChild {
  canActivateChild(): boolean {
    return this.checkAdminRole();
  }
}
```

**3. CanDeactivate:**
```typescript
export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate> {
  canDeactivate(component: CanComponentDeactivate): boolean {
    return component.canDeactivate ? component.canDeactivate() : true;
  }
}
```

**4. CanLoad:**
```typescript
export class AuthGuard implements CanLoad {
  canLoad(): boolean {
    return this.authService.isAuthenticated();
  }
}
```

**5. Resolve:**
```typescript
@Injectable()
export class UserResolver implements Resolve<User> {
  resolve(): Observable<User> {
    return this.userService.getUser();
  }
}
```

---

### Q27. What is the difference between RouterLink and Router.navigate()? (Easy)

**Answer:**
**RouterLink (Template-based):**
```html
<a routerLink="/users">Users</a>
<a [routerLink]="['/users', userId]">User Details</a>
<a routerLink="/users" [queryParams]="{page: 1}">Users</a>
```

**Router.navigate() (Programmatic):**
```typescript
// In component
constructor(private router: Router) {}

navigateToUsers() {
  this.router.navigate(['/users']);
}

navigateWithParams() {
  this.router.navigate(['/users', userId], {
    queryParams: { page: 1 },
    fragment: 'top'
  });
}
```

**When to use:**
- **RouterLink:** For navigation in templates (links, buttons)
- **Router.navigate():** For programmatic navigation (after form submission, conditional navigation)

---

## Forms

### Q28. What are the two types of forms in Angular? (Easy)

**Answer:**
Angular supports two approaches to handling forms:

**1. Template-Driven Forms:**
- Forms are defined in the template using directives
- Two-way data binding with `[(ngModel)]`
- Simpler for basic forms
- Less testable
- Requires `FormsModule`

**2. Reactive Forms:**
- Forms are defined programmatically in the component
- More powerful and flexible
- Better for complex forms
- More testable
- Requires `ReactiveFormsModule`

---

### Q29. Explain Template-Driven Forms with an example. (Medium)

**Answer:**
```typescript
// Component
export class UserFormComponent {
  user = {
    name: '',
    email: '',
    age: null
  };
  
  onSubmit(form: NgForm) {
    if (form.valid) {
      console.log('Form submitted:', this.user);
    }
  }
}
```

```html
<!-- Template -->
<form #userForm="ngForm" (ngSubmit)="onSubmit(userForm)">
  <div>
    <label>Name:</label>
    <input 
      name="name" 
      [(ngModel)]="user.name" 
      required 
      minlength="3"
      #name="ngModel">
    <div *ngIf="name.invalid && name.touched">
      <span *ngIf="name.errors?.['required']">Name is required</span>
      <span *ngIf="name.errors?.['minlength']">Name must be at least 3 characters</span>
    </div>
  </div>
  
  <div>
    <label>Email:</label>
    <input 
      name="email" 
      type="email" 
      [(ngModel)]="user.email" 
      required
      email
      #email="ngModel">
  </div>
  
  <button type="submit" [disabled]="userForm.invalid">Submit</button>
</form>
```

**Note:** Import `FormsModule` in your module.

---

### Q30. Explain Reactive Forms with an example. (Medium)

**Answer:**
```typescript
// Component
import { FormBuilder, FormGroup, Validators, FormArray } from '@angular/forms';

export class UserFormComponent {
  userForm: FormGroup;
  
  constructor(private fb: FormBuilder) {
    this.userForm = this.fb.group({
      name: ['', [Validators.required, Validators.minLength(3)]],
      email: ['', [Validators.required, Validators.email]],
      age: [null, [Validators.required, Validators.min(18)]],
      address: this.fb.group({
        street: [''],
        city: [''],
        zip: ['']
      }),
      hobbies: this.fb.array([])
    });
  }
  
  get hobbies() {
    return this.userForm.get('hobbies') as FormArray;
  }
  
  addHobby() {
    this.hobbies.push(this.fb.control(''));
  }
  
  onSubmit() {
    if (this.userForm.valid) {
      console.log('Form value:', this.userForm.value);
    } else {
      this.markFormGroupTouched(this.userForm);
    }
  }
  
  markFormGroupTouched(formGroup: FormGroup) {
    Object.keys(formGroup.controls).forEach(key => {
      const control = formGroup.get(key);
      control?.markAsTouched();
    });
  }
}
```

```html
<!-- Template -->
<form [formGroup]="userForm" (ngSubmit)="onSubmit()">
  <div>
    <label>Name:</label>
    <input formControlName="name">
    <div *ngIf="userForm.get('name')?.invalid && userForm.get('name')?.touched">
      <span *ngIf="userForm.get('name')?.errors?.['required']">Required</span>
      <span *ngIf="userForm.get('name')?.errors?.['minlength']">Min 3 chars</span>
    </div>
  </div>
  
  <div formGroupName="address">
    <input formControlName="street" placeholder="Street">
    <input formControlName="city" placeholder="City">
  </div>
  
  <div formArrayName="hobbies">
    <button type="button" (click)="addHobby()">Add Hobby</button>
    <div *ngFor="let hobby of hobbies.controls; let i = index">
      <input [formControlName]="i">
    </div>
  </div>
  
  <button type="submit" [disabled]="userForm.invalid">Submit</button>
</form>
```

---

### Q31. What is the difference between Template-Driven and Reactive Forms? (Medium)

**Answer:**
| Feature | Template-Driven | Reactive |
|---------|----------------|----------|
| **Setup** | Simple, directive-based | Programmatic, FormBuilder |
| **Data Model** | Unstructured | Structured (FormGroup, FormControl) |
| **Validation** | Template-based | Programmatic |
| **Testing** | Harder | Easier |
| **Dynamic Forms** | Difficult | Easy (FormArray) |
| **Custom Validators** | Possible but complex | Straightforward |
| **Value Changes** | Two-way binding | Observable streams |
| **Use Case** | Simple forms | Complex, dynamic forms |

---

### Q32. How do you create Custom Validators? (Medium)

**Answer:**
**Custom Validator Function:**
```typescript
// Validator function
export function forbiddenNameValidator(forbiddenName: RegExp): ValidatorFn {
  return (control: AbstractControl): ValidationErrors | null => {
    const forbidden = forbiddenName.test(control.value);
    return forbidden ? { forbiddenName: { value: control.value } } : null;
  };
}

// Usage in component
this.userForm = this.fb.group({
  name: ['', [
    Validators.required,
    forbiddenNameValidator(/admin/i)
  ]]
});
```

**Custom Validator Class:**
```typescript
@Directive({
  selector: '[appEmailValidator]',
  providers: [{ provide: NG_VALIDATORS, useExisting: EmailValidatorDirective, multi: true }]
})
export class EmailValidatorDirective implements Validator {
  validate(control: AbstractControl): ValidationErrors | null {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    const valid = emailRegex.test(control.value);
    return valid ? null : { invalidEmail: true };
  }
}
```

**Async Validator:**
```typescript
export function uniqueEmailValidator(userService: UserService): AsyncValidatorFn {
  return (control: AbstractControl): Observable<ValidationErrors | null> => {
    return userService.checkEmailExists(control.value).pipe(
      map(exists => exists ? { emailExists: true } : null),
      catchError(() => of(null))
    );
  };
}
```

---

## HTTP Client

### Q33. How do you make HTTP requests in Angular? (Easy)

**Answer:**
Angular provides `HttpClient` service for making HTTP requests.

**Setup:**
```typescript
// Import HttpClientModule in app.module.ts
import { HttpClientModule } from '@angular/common/http';

@NgModule({
  imports: [HttpClientModule]
})
```

**Usage in Service:**
```typescript
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({ providedIn: 'root' })
export class UserService {
  private apiUrl = 'https://api.example.com/users';
  
  constructor(private http: HttpClient) {}
  
  getUsers(): Observable<User[]> {
    return this.http.get<User[]>(this.apiUrl);
  }
  
  getUser(id: number): Observable<User> {
    return this.http.get<User>(`${this.apiUrl}/${id}`);
  }
  
  createUser(user: User): Observable<User> {
    return this.http.post<User>(this.apiUrl, user);
  }
  
  updateUser(id: number, user: User): Observable<User> {
    return this.http.put<User>(`${this.apiUrl}/${id}`, user);
  }
  
  deleteUser(id: number): Observable<void> {
    return this.http.delete<void>(`${this.apiUrl}/${id}`);
  }
}
```

**Usage in Component:**
```typescript
export class UserComponent {
  users: User[] = [];
  
  constructor(private userService: UserService) {}
  
  ngOnInit() {
    this.userService.getUsers().subscribe(
      users => this.users = users,
      error => console.error('Error:', error)
    );
  }
}
```

---

### Q34. What are HTTP Interceptors, and how do you use them? (Medium)

**Answer:**
HTTP Interceptors allow you to intercept and modify HTTP requests and responses globally.

**Creating an Interceptor:**
```typescript
import { Injectable } from '@angular/core';
import { HttpInterceptor, HttpRequest, HttpHandler, HttpEvent } from '@angular/common/http';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    // Get token from storage
    const token = localStorage.getItem('token');
    
    // Clone request and add token
    if (token) {
      const cloned = req.clone({
        setHeaders: {
          Authorization: `Bearer ${token}`
        }
      });
      return next.handle(cloned);
    }
    
    return next.handle(req);
  }
}
```

**Registering Interceptor:**
```typescript
import { HTTP_INTERCEPTORS } from '@angular/common/http';

@NgModule({
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: AuthInterceptor,
      multi: true
    }
  ]
})
export class AppModule { }
```

**Common Use Cases:**
- Adding authentication headers
- Logging requests/responses
- Error handling
- Request/response transformation
- Loading indicators

---

### Q35. How do you handle HTTP errors in Angular? (Medium)

**Answer:**
**1. Using catchError Operator:**
```typescript
import { catchError, throwError } from 'rxjs';

getUsers(): Observable<User[]> {
  return this.http.get<User[]>(this.apiUrl).pipe(
    catchError(error => {
      if (error.status === 404) {
        console.error('Resource not found');
      } else if (error.status === 500) {
        console.error('Server error');
      }
      return throwError(() => error);
    })
  );
}
```

**2. Global Error Handler:**
```typescript
@Injectable()
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: any): void {
    console.error('Global error:', error);
    // Log to error tracking service
  }
}

// Register in app.module.ts
providers: [
  { provide: ErrorHandler, useClass: GlobalErrorHandler }
]
```

**3. HTTP Interceptor for Error Handling:**
```typescript
@Injectable()
export class ErrorInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    return next.handle(req).pipe(
      catchError(error => {
        if (error.status === 401) {
          // Handle unauthorized
          this.router.navigate(['/login']);
        }
        return throwError(() => error);
      })
    );
  }
}
```

---

## RxJS and Observables

### Q36. What are Observables in Angular? (Medium)

**Answer:**
Observables are a key part of Angular's reactive programming model. They represent a stream of data that can be observed over time.

**Key Concepts:**
- **Observable:** A stream of data
- **Observer:** Subscribes to an Observable
- **Subscription:** Connection between Observable and Observer
- **Operators:** Functions to transform, filter, or combine Observables

**Basic Example:**
```typescript
import { Observable } from 'rxjs';

// Creating an Observable
const observable = new Observable(observer => {
  observer.next('Hello');
  observer.next('World');
  observer.complete();
});

// Subscribing
observable.subscribe({
  next: value => console.log(value),
  error: err => console.error(err),
  complete: () => console.log('Done')
});
```

**HTTP Example:**
```typescript
getUsers(): Observable<User[]> {
  return this.http.get<User[]>(this.apiUrl);
}

// Subscribe
this.userService.getUsers().subscribe(users => {
  this.users = users;
});
```

---

### Q37. Explain RxJS Operators: map, filter, switchMap, mergeMap, and catchError. (Medium)

**Answer:**
**1. map - Transform values:**
```typescript
this.http.get<User[]>('/api/users')
  .pipe(
    map(users => users.map(user => ({ ...user, fullName: `${user.firstName} ${user.lastName}` })))
  )
  .subscribe(users => this.users = users);
```

**2. filter - Filter values:**
```typescript
of(1, 2, 3, 4, 5)
  .pipe(filter(x => x % 2 === 0))
  .subscribe(x => console.log(x)); // 2, 4
```

**3. switchMap - Switch to new Observable:**
```typescript
// Cancels previous request when new one comes
this.searchControl.valueChanges
  .pipe(
    debounceTime(300),
    switchMap(query => this.searchService.search(query))
  )
  .subscribe(results => this.results = results);
```

**4. mergeMap - Merge multiple Observables:**
```typescript
// Executes all requests in parallel
this.userIds
  .pipe(
    mergeMap(id => this.userService.getUser(id))
  )
  .subscribe(user => console.log(user));
```

**5. catchError - Handle errors:**
```typescript
this.http.get('/api/users')
  .pipe(
    catchError(error => {
      console.error('Error:', error);
      return of([]); // Return empty array on error
    })
  )
  .subscribe(users => this.users = users);
```

---

### Q38. What is the difference between Observable and Promise? (Medium)

**Answer:**
| Feature | Observable | Promise |
|---------|-------------|---------|
| **Values** | Multiple values over time | Single value |
| **Execution** | Lazy (only when subscribed) | Eager (executes immediately) |
| **Cancellation** | Can be cancelled | Cannot be cancelled |
| **Operators** | Rich operator library (map, filter, etc.) | Limited (then, catch) |
| **Multiple Subscribers** | Each subscription creates new execution | Shares same result |
| **Use Case** | Streams, events, HTTP requests | One-time async operations |

**Example:**
```typescript
// Observable
const obs$ = new Observable(observer => {
  console.log('Executing');
  observer.next('Value');
});
obs$.subscribe(); // Executes
obs$.subscribe(); // Executes again

// Promise
const promise = new Promise(resolve => {
  console.log('Executing');
  resolve('Value');
});
promise.then(); // Executes
promise.then(); // Uses cached result
```

---

### Q39. Explain Subject, BehaviorSubject, and ReplaySubject. (Tough)

**Answer:**
**1. Subject:**
```typescript
import { Subject } from 'rxjs';

const subject = new Subject<string>();

// Subscribers only receive values emitted after subscription
subject.subscribe(value => console.log('Subscriber 1:', value));
subject.next('Hello');
subject.subscribe(value => console.log('Subscriber 2:', value));
subject.next('World');

// Output:
// Subscriber 1: Hello
// Subscriber 1: World
// Subscriber 2: World
```

**2. BehaviorSubject:**
```typescript
import { BehaviorSubject } from 'rxjs';

const behaviorSubject = new BehaviorSubject<string>('Initial');

// New subscribers receive the current value immediately
behaviorSubject.subscribe(value => console.log('Subscriber 1:', value));
behaviorSubject.next('Hello');
behaviorSubject.subscribe(value => console.log('Subscriber 2:', value));

// Output:
// Subscriber 1: Initial
// Subscriber 1: Hello
// Subscriber 2: Hello (receives current value)
```

**3. ReplaySubject:**
```typescript
import { ReplaySubject } from 'rxjs';

const replaySubject = new ReplaySubject<string>(2); // Buffer last 2 values

replaySubject.next('Value 1');
replaySubject.next('Value 2');
replaySubject.next('Value 3');

replaySubject.subscribe(value => console.log('Subscriber:', value));

// Output:
// Subscriber: Value 2
// Subscriber: Value 3
```

**Use Cases:**
- **Subject:** Event emitters, one-time notifications
- **BehaviorSubject:** State management, current value needed
- **ReplaySubject:** Caching recent values for late subscribers

---

## Change Detection

### Q40. What is Change Detection in Angular? (Medium)

**Answer:**
Change Detection is the process by which Angular checks for changes in the component tree and updates the DOM accordingly.

**How it works:**
1. Angular runs change detection when:
   - Component initialization
   - DOM events (click, input, etc.)
   - HTTP requests complete
   - Timers (setTimeout, setInterval)
   - Any asynchronous operation

2. Angular checks all components by default (unless OnPush is used)

3. Updates the DOM if changes are detected

**Change Detection Strategies:**
- **Default:** Checks all components on every change detection cycle
- **OnPush:** Only checks when:
  - Input properties change
  - Events originate from the component
  - Observables emit (with async pipe)
  - Manual trigger

---

### Q41. Explain OnPush Change Detection Strategy. (Medium)

**Answer:**
OnPush change detection strategy improves performance by reducing the number of change detection cycles.

```typescript
@Component({
  selector: 'app-user',
  changeDetection: ChangeDetectionStrategy.OnPush,
  template: '<div>{{ user.name }}</div>'
})
export class UserComponent {
  @Input() user: User;
}
```

**OnPush checks for changes when:**
1. **Input reference changes:**
```typescript
// This triggers change detection
this.user = { ...this.user, name: 'New Name' };

// This does NOT trigger (same reference)
this.user.name = 'New Name';
```

2. **Events from the component:**
```typescript
onClick() {
  // This triggers change detection
  this.count++;
}
```

3. **Observables with async pipe:**
```html
<div>{{ data$ | async }}</div>
```

4. **Manual trigger:**
```typescript
constructor(private cdr: ChangeDetectorRef) {}

updateData() {
  this.data = newData;
  this.cdr.markForCheck(); // Manually trigger
}
```

**Benefits:**
- Better performance
- Predictable updates
- Forces immutable data patterns

---

### Q42. What is Zone.js, and how does it work? (Tough)

**Answer:**
Zone.js is a library that patches asynchronous operations to notify Angular when they complete, triggering change detection.

**How it works:**
1. Zone.js patches browser APIs (setTimeout, Promise, addEventListener, etc.)
2. When these APIs are called, Zone.js wraps them
3. After execution, Zone.js notifies Angular
4. Angular runs change detection

**Example:**
```typescript
// Without Zone.js, Angular wouldn't know about this change
setTimeout(() => {
  this.count++; // Change detection runs automatically
}, 1000);
```

**Running outside Angular Zone:**
```typescript
constructor(private ngZone: NgZone) {}

runOutsideAngular() {
  this.ngZone.runOutsideAngular(() => {
    // This won't trigger change detection
    setInterval(() => {
      // Heavy computation
    }, 100);
  });
}

runInsideAngular() {
  this.ngZone.run(() => {
    // This will trigger change detection
    this.count++;
  });
}
```

---

## Modules

### Q43. What is an NgModule in Angular? (Easy)

**Answer:**
An NgModule is a decorator that marks a class as an Angular module. Modules organize an application into cohesive blocks of functionality.

**Basic Structure:**
```typescript
@NgModule({
  declarations: [UserComponent, UserListComponent], // Components, directives, pipes
  imports: [CommonModule, HttpClientModule],      // Other modules
  providers: [UserService],                        // Services
  exports: [UserComponent],                        // Make available to other modules
  bootstrap: [AppComponent]                        // Root component (AppModule only)
})
export class UserModule { }
```

**Key Properties:**
- **declarations:** Components, directives, pipes that belong to this module
- **imports:** Other modules needed by this module
- **providers:** Services available to this module
- **exports:** Makes declarations available to other modules
- **bootstrap:** Root component (only in AppModule)

---

### Q44. Explain Feature Modules, Shared Modules, and Core Modules. (Medium)

**Answer:**
**1. Feature Modules:**
```typescript
// user.module.ts
@NgModule({
  declarations: [UserComponent, UserListComponent],
  imports: [CommonModule, UserRoutingModule],
  providers: [UserService]
})
export class UserModule { }
```
- Encapsulate a specific feature
- Can be lazy-loaded
- Self-contained functionality

**2. Shared Modules:**
```typescript
// shared.module.ts
@NgModule({
  declarations: [ButtonComponent, CardComponent],
  imports: [CommonModule],
  exports: [ButtonComponent, CardComponent, CommonModule]
})
export class SharedModule { }
```
- Reusable components, directives, pipes
- Imported by feature modules
- Exports common functionality

**3. Core Modules:**
```typescript
// core.module.ts
@NgModule({
  providers: [AuthService, UserService, ApiService]
})
export class CoreModule { }
```
- Singleton services
- Imported once in AppModule
- Application-wide services

---

### Q45. What is the difference between forRoot() and forChild()? (Medium)

**Answer:**
**forRoot()** - Used in the root module to configure a module with providers:
```typescript
// In AppModule
@NgModule({
  imports: [
    RouterModule.forRoot(routes),  // Provides Router service
    HttpClientModule               // Provides HttpClient
  ]
})
export class AppModule { }
```

**forChild()** - Used in feature modules to import routing without creating new service instances:
```typescript
// In FeatureModule
@NgModule({
  imports: [
    RouterModule.forChild(featureRoutes)  // Uses existing Router service
  ]
})
export class FeatureModule { }
```

**Why the difference?**
- Some modules need to provide services only once (Router, HttpClient)
- `forRoot()` creates and provides services
- `forChild()` imports configuration without creating new service instances
- Prevents multiple instances of singleton services

---

## Pipes

### Q46. What are Pipes in Angular? (Easy)

**Answer:**
Pipes are functions that transform input values to a desired output in templates. They are used to format data for display.

**Built-in Pipes:**
```html
<!-- Date Pipe -->
<p>{{ date | date:'short' }}</p>
<p>{{ date | date:'fullDate' }}</p>

<!-- Currency Pipe -->
<p>{{ price | currency:'USD':'symbol' }}</p>

<!-- UpperCase/LowerCase -->
<p>{{ text | uppercase }}</p>
<p>{{ text | lowercase }}</p>

<!-- Decimal Pipe -->
<p>{{ number | number:'1.2-2' }}</p>

<!-- JSON Pipe -->
<pre>{{ object | json }}</pre>

<!-- Async Pipe -->
<div>{{ data$ | async }}</div>
```

**Chaining Pipes:**
```html
<p>{{ date | date:'short' | uppercase }}</p>
```

---

### Q47. How do you create a Custom Pipe? (Medium)

**Answer:**
```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'truncate',
  pure: true  // Default: true (only runs when input changes)
})
export class TruncatePipe implements PipeTransform {
  transform(value: string, limit: number = 20, trail: string = '...'): string {
    if (!value) return '';
    if (value.length <= limit) return value;
    return value.substring(0, limit) + trail;
  }
}
```

**Usage:**
```html
<p>{{ longText | truncate:50 }}</p>
<p>{{ longText | truncate:30:'...' }}</p>
```

**Pure vs Impure Pipes:**
```typescript
@Pipe({
  name: 'filter',
  pure: false  // Runs on every change detection
})
export class FilterPipe implements PipeTransform {
  transform(items: any[], filter: string): any[] {
    // Runs frequently
    return items.filter(item => item.name.includes(filter));
  }
}
```

**Note:** Pure pipes are more performant. Use impure pipes only when necessary.

---

## Lifecycle Hooks

### Q48. Explain Angular Component Lifecycle Hooks. (Medium)

**Answer:**
Lifecycle hooks are special methods that allow you to tap into key moments in a component's lifecycle.

**Hook Order:**
1. **ngOnChanges:** Called when input properties change
2. **ngOnInit:** Called once after first ngOnChanges
3. **ngDoCheck:** Called during every change detection run
4. **ngAfterContentInit:** Called after content projection (ng-content)
5. **ngAfterContentChecked:** Called after projected content is checked
6. **ngAfterViewInit:** Called after component's view is initialized
7. **ngAfterViewChecked:** Called after view is checked
8. **ngOnDestroy:** Called just before component is destroyed

**Example:**
```typescript
export class UserComponent implements OnInit, OnDestroy {
  @Input() userId: number;
  
  ngOnInit() {
    // Initialize component
    // Fetch data
    // Subscribe to observables
    console.log('Component initialized');
  }
  
  ngOnChanges(changes: SimpleChanges) {
    // React to input changes
    if (changes['userId']) {
      this.loadUser(changes['userId'].currentValue);
    }
  }
  
  ngOnDestroy() {
    // Cleanup
    // Unsubscribe from observables
    // Clear timers
    console.log('Component destroyed');
  }
}
```

---

### Q49. When should you use each lifecycle hook? (Medium)

**Answer:**
**ngOnInit:**
- Initialize component
- Fetch initial data
- Subscribe to observables
- Setup component state

**ngOnChanges:**
- React to input property changes
- Compare old and new values
- Update derived state

**ngDoCheck:**
- Custom change detection logic
- Detect changes that Angular doesn't catch
- Use sparingly (performance impact)

**ngAfterContentInit:**
- Access projected content (ng-content)
- Initialize content-related logic

**ngAfterViewInit:**
- Access ViewChild/ViewChildren
- Initialize third-party libraries
- Setup DOM-related logic

**ngOnDestroy:**
- Unsubscribe from observables
- Clear timers/intervals
- Remove event listeners
- Cleanup resources

---

## Advanced Topics

### Q50. What are Angular Signals? (Tough)

**Answer:**
Angular Signals (introduced in Angular 16+) provide a fine-grained reactivity model that simplifies development and improves performance.

**Creating Signals:**
```typescript
import { signal, computed, effect } from '@angular/core';

export class UserComponent {
  // Writable signal
  count = signal(0);
  
  // Computed signal (derived)
  doubleCount = computed(() => this.count() * 2);
  
  // Effect (side effects)
  constructor() {
    effect(() => {
      console.log('Count changed:', this.count());
    });
  }
  
  increment() {
    this.count.update(value => value + 1);
    // Or
    this.count.set(this.count() + 1);
  }
}
```

**In Template:**
```html
<p>Count: {{ count() }}</p>
<p>Double: {{ doubleCount() }}</p>
<button (click)="increment()">Increment</button>
```

**Benefits:**
- Fine-grained reactivity
- Better performance
- Simpler mental model
- Automatic dependency tracking

---

### Q51. What is Angular Universal (SSR)? (Medium)

**Answer:**
Angular Universal is a technology for server-side rendering (SSR) of Angular applications.

**Benefits:**
- **SEO:** Search engines can crawl the content
- **Performance:** Faster initial page load
- **Social Media:** Better preview cards
- **Accessibility:** Works without JavaScript

**Setup:**
```bash
ng add @nguniversal/express-engine
```

**How it works:**
1. Server renders the Angular app
2. Sends HTML to the browser
3. Browser hydrates the app (makes it interactive)

**Usage:**
```typescript
// app.server.module.ts
@NgModule({
  imports: [AppModule, ServerModule],
  bootstrap: [AppComponent]
})
export class AppServerModule { }
```

---

### Q52. Explain Angular's Ahead-of-Time (AOT) Compilation. (Medium)

**Answer:**
AOT compilation converts Angular HTML and TypeScript code into efficient JavaScript code during the build phase, before the browser downloads and runs it.

**Benefits:**
- **Faster Rendering:** No compilation needed in browser
- **Smaller Bundle:** Removes Angular compiler
- **Early Error Detection:** Template errors caught at build time
- **Better Security:** No eval() or Function() calls
- **Tree Shaking:** Removes unused code

**How it works:**
```bash
# Development (JIT - Just in Time)
ng serve

# Production (AOT - Ahead of Time)
ng build --prod
```

**AOT vs JIT:**
| Feature | JIT | AOT |
|---------|-----|-----|
| Compilation | Browser | Build time |
| Bundle Size | Larger | Smaller |
| Startup Time | Slower | Faster |
| Error Detection | Runtime | Build time |

---

### Q53. What is Tree Shaking in Angular? (Medium)

**Answer:**
Tree shaking is the process of removing unused code from the final bundle.

**How Angular enables it:**
1. **ES Modules:** Angular uses ES modules (import/export)
2. **Static Analysis:** Build tools analyze imports
3. **Dead Code Elimination:** Removes unused exports

**Example:**
```typescript
// math.ts
export function add(a: number, b: number) { return a + b; }
export function subtract(a: number, b: number) { return a - b; }

// app.component.ts
import { add } from './math';
// subtract is not imported, so it's removed from bundle
```

**Best Practices:**
- Use ES modules
- Avoid barrel exports when possible
- Use `providedIn: 'root'` for services (tree-shakeable)
- Import only what you need

---

### Q54. What are ViewChild and ContentChild? (Medium)

**Answer:**
**ViewChild** - Accesses child components, directives, or DOM elements in the component's view:

```typescript
import { ViewChild, ElementRef, AfterViewInit } from '@angular/core';

export class ParentComponent implements AfterViewInit {
  @ViewChild(ChildComponent) childComponent: ChildComponent;
  @ViewChild('inputRef') inputElement: ElementRef;
  
  ngAfterViewInit() {
    // Access child component
    this.childComponent.doSomething();
    
    // Access DOM element
    this.inputElement.nativeElement.focus();
  }
}
```

```html
<app-child></app-child>
<input #inputRef type="text">
```

**ContentChild** - Accesses projected content (ng-content):

```typescript
import { ContentChild, AfterContentInit } from '@angular/core';

export class CardComponent implements AfterContentInit {
  @ContentChild('header') header: ElementRef;
  
  ngAfterContentInit() {
    console.log(this.header);
  }
}
```

```html
<app-card>
  <div #header>Header Content</div>
</app-card>
```

**Differences:**
- **ViewChild:** Accesses elements in component's template
- **ContentChild:** Accesses elements projected from parent

---

## Performance Optimization

### Q55. How do you optimize Angular application performance? (Medium)

**Answer:**
**1. OnPush Change Detection:**
```typescript
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush
})
```

**2. Lazy Loading:**
```typescript
{ path: 'feature', loadChildren: () => import('./feature/feature.module') }
```

**3. TrackBy in *ngFor:**
```html
<div *ngFor="let item of items; trackBy: trackById">
```

**4. Pure Pipes:**
```typescript
@Pipe({ name: 'filter', pure: true })
```

**5. Virtual Scrolling:**
```html
<cdk-virtual-scroll-viewport itemSize="50">
  <div *cdkVirtualFor="let item of items">{{ item }}</div>
</cdk-virtual-scroll-viewport>
```

**6. AOT Compilation:**
```bash
ng build --prod
```

**7. Bundle Optimization:**
- Tree shaking
- Code splitting
- Lazy loading modules

**8. Unsubscribe from Observables:**
```typescript
private destroy$ = new Subject();

this.data$.pipe(takeUntil(this.destroy$)).subscribe();

ngOnDestroy() {
  this.destroy$.next();
  this.destroy$.complete();
}
```

---

### Q56. What is the difference between trackBy and OnPush? (Medium)

**Answer:**
**trackBy** - Optimizes *ngFor rendering:
```typescript
trackByUserId(index: number, user: User): number {
  return user.id;
}
```
- Prevents unnecessary DOM manipulation
- Only re-renders changed items
- Used with *ngFor

**OnPush** - Optimizes change detection:
```typescript
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush
})
```
- Reduces change detection cycles
- Only checks component when inputs change
- Used at component level

**Both can be used together for maximum performance.**

---

## Testing

### Q57. How do you test Angular components? (Medium)

**Answer:**
Angular uses Jasmine and Karma for testing.

**Component Test Example:**
```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { UserComponent } from './user.component';

describe('UserComponent', () => {
  let component: UserComponent;
  let fixture: ComponentFixture<UserComponent>;
  
  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [UserComponent],
      imports: [HttpClientTestingModule],
      providers: [UserService]
    }).compileComponents();
    
    fixture = TestBed.createComponent(UserComponent);
    component = fixture.componentInstance;
  });
  
  it('should create', () => {
    expect(component).toBeTruthy();
  });
  
  it('should display user name', () => {
    component.user = { id: 1, name: 'John' };
    fixture.detectChanges();
    
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('h1').textContent).toContain('John');
  });
  
  it('should emit event on click', () => {
    spyOn(component.userSelected, 'emit');
    component.selectUser();
    expect(component.userSelected.emit).toHaveBeenCalled();
  });
});
```

---

### Q58. How do you test Services in Angular? (Medium)

**Answer:**
```typescript
import { TestBed } from '@angular/core/testing';
import { HttpClientTestingModule, HttpTestingController } from '@angular/common/http/testing';
import { UserService } from './user.service';

describe('UserService', () => {
  let service: UserService;
  let httpMock: HttpTestingController;
  
  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule],
      providers: [UserService]
    });
    
    service = TestBed.inject(UserService);
    httpMock = TestBed.inject(HttpTestingController);
  });
  
  afterEach(() => {
    httpMock.verify();
  });
  
  it('should fetch users', () => {
    const mockUsers = [{ id: 1, name: 'John' }];
    
    service.getUsers().subscribe(users => {
      expect(users).toEqual(mockUsers);
    });
    
    const req = httpMock.expectOne('/api/users');
    expect(req.request.method).toBe('GET');
    req.flush(mockUsers);
  });
});
```

---

## Angular CLI

### Q59. What are the most commonly used Angular CLI commands? (Easy)

**Answer:**
```bash
# Create new project
ng new my-app

# Generate component
ng generate component user
ng g c user

# Generate service
ng generate service user
ng g s user

# Generate module
ng generate module user
ng g m user

# Generate directive
ng generate directive highlight
ng g d highlight

# Generate pipe
ng generate pipe truncate
ng g p truncate

# Serve application
ng serve
ng serve --port 4200

# Build application
ng build
ng build --prod

# Run tests
ng test

# Run e2e tests
ng e2e

# Add package
ng add @angular/material

# Update Angular
ng update @angular/core @angular/cli
```

---

### Q60. What is the purpose of angular.json? (Easy)

**Answer:**
`angular.json` is the configuration file for Angular CLI projects. It contains:

- **Project configuration:** Build options, file replacements
- **Architect configurations:** Serve, build, test, e2e
- **Asset paths:** Styles, scripts, assets
- **Environment files:** Development, production
- **Output paths:** Where to build the application

**Key Sections:**
```json
{
  "projects": {
    "my-app": {
      "architect": {
        "build": {
          "options": {
            "outputPath": "dist/my-app",
            "index": "src/index.html",
            "main": "src/main.ts"
          }
        },
        "serve": {
          "options": {
            "port": 4200
          }
        }
      }
    }
  }
}
```

---

## State Management

### Q61. How do you manage state in Angular applications? (Medium)

**Answer:**
**1. Services with RxJS:**
```typescript
@Injectable({ providedIn: 'root' })
export class StateService {
  private stateSubject = new BehaviorSubject<AppState>(initialState);
  state$ = this.stateSubject.asObservable();
  
  updateState(newState: Partial<AppState>) {
    this.stateSubject.next({ ...this.stateSubject.value, ...newState });
  }
}
```

**2. NgRx (Redux pattern):**
```typescript
// Actions
export const loadUsers = createAction('[User] Load Users');
export const loadUsersSuccess = createAction('[User] Load Users Success', props<{ users: User[] }>());

// Reducer
export const userReducer = createReducer(
  initialState,
  on(loadUsersSuccess, (state, { users }) => ({ ...state, users }))
);

// Effects
export class UserEffects {
  loadUsers$ = createEffect(() =>
    this.actions$.pipe(
      ofType(loadUsers),
      switchMap(() => this.userService.getUsers().pipe(
        map(users => loadUsersSuccess({ users }))
      ))
    )
  );
}
```

**3. Signals (Angular 16+):**
```typescript
export class StateService {
  users = signal<User[]>([]);
  selectedUser = signal<User | null>(null);
}
```

---

## Security

### Q62. What security best practices should you follow in Angular? (Medium)

**Answer:**
**1. Sanitize User Input:**
```typescript
import { DomSanitizer } from '@angular/platform-browser';

constructor(private sanitizer: DomSanitizer) {}

getSafeHtml(html: string) {
  return this.sanitizer.sanitize(SecurityContext.HTML, html);
}
```

**2. Use HTTP Interceptors for Authentication:**
```typescript
intercept(req: HttpRequest<any>, next: HttpHandler) {
  const token = this.authService.getToken();
  const cloned = req.clone({
    setHeaders: { Authorization: `Bearer ${token}` }
  });
  return next.handle(cloned);
}
```

**3. Prevent XSS:**
- Angular automatically escapes values in templates
- Use `[innerHTML]` with caution
- Sanitize user input

**4. Use HTTPS:**
- Always use HTTPS in production
- Secure API endpoints

**5. Content Security Policy (CSP):**
```html
<meta http-equiv="Content-Security-Policy" content="default-src 'self'">
```

**6. Avoid eval() and Function():**
- AOT compilation helps prevent this
- Don't use `new Function()` or `eval()`

---

### Q63. How does Angular prevent XSS attacks? (Medium)

**Answer:**
Angular provides built-in protection against Cross-Site Scripting (XSS) attacks:

**1. Automatic Escaping:**
```html
<!-- Safe - Angular escapes this -->
<p>{{ userInput }}</p>
```

**2. Sanitization:**
```typescript
import { DomSanitizer } from '@angular/platform-browser';

constructor(private sanitizer: DomSanitizer) {}

// Sanitize HTML
safeHtml = this.sanitizer.sanitize(SecurityContext.HTML, userHtml);

// Sanitize URL
safeUrl = this.sanitizer.sanitize(SecurityContext.URL, userUrl);
```

**3. Content Security:**
```html
<!-- Dangerous - use with sanitization -->
<div [innerHTML]="safeHtml"></div>
```

**4. Template Security:**
- Templates are compiled securely
- No eval() or Function() in templates
- Expression evaluation is sandboxed

**Best Practices:**
- Always sanitize user input
- Use `[innerHTML]` only when necessary
- Validate and sanitize on the server side too

---

## Miscellaneous

### Q64. What is the difference between ngOnInit and constructor? (Easy)

**Answer:**
**Constructor:**
- Called when the class is instantiated
- Used for dependency injection
- Should not contain initialization logic
- Runs before Angular lifecycle

**ngOnInit:**
- Called after Angular has initialized the component
- First lifecycle hook
- Best place for initialization logic
- Input properties are available

```typescript
export class UserComponent {
  @Input() userId: number;
  
  constructor(private userService: UserService) {
    // Dependencies injected here
    // Input properties NOT available yet
  }
  
  ngOnInit() {
    // Input properties available here
    // Initialize component
    this.loadUser(this.userId);
  }
}
```

---

### Q65. What are Standalone Components? (Medium)

**Answer:**
Standalone components (Angular 14+) are components that don't need to be declared in an NgModule.

```typescript
@Component({
  selector: 'app-user',
  standalone: true,
  imports: [CommonModule, FormsModule],
  template: '<div>{{ user.name }}</div>'
})
export class UserComponent { }
```

**Benefits:**
- Simpler structure
- Better tree-shaking
- Easier lazy loading
- Reduced boilerplate

**Usage:**
```typescript
// Can be imported directly
@Component({
  imports: [UserComponent]
})
export class AppComponent { }
```

---

### Q66. Explain Angular's Dependency Injection Token System. (Tough)

**Answer:**
Angular uses tokens to identify dependencies in the DI system.

**1. Class Token (Default):**
```typescript
@Injectable()
export class UserService { }

// Injection
constructor(private userService: UserService) { }
```

**2. InjectionToken (For Interfaces/Values):**
```typescript
import { InjectionToken } from '@angular/core';

export const API_URL = new InjectionToken<string>('api.url');

// Provide
providers: [
  { provide: API_URL, useValue: 'https://api.example.com' }
]

// Inject
constructor(@Inject(API_URL) private apiUrl: string) { }
```

**3. Factory Provider:**
```typescript
export function userServiceFactory(http: HttpClient): UserService {
  return new UserService(http);
}

providers: [
  {
    provide: UserService,
    useFactory: userServiceFactory,
    deps: [HttpClient]
  }
]
```

**4. Class Provider:**
```typescript
providers: [
  { provide: UserService, useClass: UserService }
]
```

**5. Existing Provider:**
```typescript
providers: [
  { provide: NewService, useExisting: OldService }
]
```

---

### Q67. What is the difference between @Injectable() with and without providedIn? (Medium)

**Answer:**
**Without providedIn:**
```typescript
@Injectable()
export class UserService { }

// Must be provided in module
@NgModule({
  providers: [UserService]
})
```
- Not tree-shakeable
- Must be explicitly provided
- Can create multiple instances

**With providedIn: 'root':**
```typescript
@Injectable({ providedIn: 'root' })
export class UserService { }
```
- Tree-shakeable (removed if unused)
- Singleton across the app
- No need to provide in module
- Recommended approach

**With providedIn: Module:**
```typescript
@Injectable({ providedIn: UserModule })
export class UserService { }
```
- Provided only when UserModule is imported
- Tree-shakeable
- Creates instance per module

---

### Q68. What are Angular Elements? (Medium)

**Answer:**
Angular Elements allows you to package Angular components as custom web elements (Web Components).

**Setup:**
```bash
ng add @angular/elements
```

**Usage:**
```typescript
import { createCustomElement } from '@angular/elements';

export class AppModule {
  constructor(private injector: Injector) {
    const el = createCustomElement(UserComponent, { injector });
    customElements.define('app-user', el);
  }
}
```

**Benefits:**
- Use Angular components in any framework
- Framework-agnostic
- Self-contained
- Can be used in vanilla JavaScript

---

### Q69. Explain Angular's Animation System. (Medium)

**Answer:**
Angular provides a powerful animation system using the `@angular/animations` package.

**Setup:**
```typescript
import { trigger, state, style, transition, animate } from '@angular/animations';

@Component({
  animations: [
    trigger('fadeIn', [
      state('void', style({ opacity: 0 })),
      state('*', style({ opacity: 1 })),
      transition('void => *', animate('300ms')),
      transition('* => void', animate('300ms'))
    ])
  ]
})
```

**Usage:**
```html
<div [@fadeIn]="isVisible">Content</div>
```

**Advanced Example:**
```typescript
trigger('slideInOut', [
  transition(':enter', [
    style({ transform: 'translateX(-100%)' }),
    animate('300ms ease-in', style({ transform: 'translateX(0%)' }))
  ]),
  transition(':leave', [
    animate('300ms ease-in', style({ transform: 'translateX(-100%)' }))
  ])
])
```

---

### Q70. What is the difference between async pipe and subscribe? (Medium)

**Answer:**
**Subscribe (Manual):**
```typescript
export class UserComponent {
  users: User[] = [];
  
  ngOnInit() {
    this.userService.getUsers().subscribe(users => {
      this.users = users;
    });
  }
  
  ngOnDestroy() {
    // Must unsubscribe to prevent memory leaks
  }
}
```

**Async Pipe:**
```html
<div *ngFor="let user of users$ | async">{{ user.name }}</div>
```

```typescript
export class UserComponent {
  users$ = this.userService.getUsers();
  // No need to unsubscribe - async pipe handles it
}
```

**Comparison:**
| Feature | Subscribe | Async Pipe |
|---------|-----------|------------|
| **Unsubscribe** | Manual | Automatic |
| **Memory Leaks** | Risk if not unsubscribed | Safe |
| **Change Detection** | Manual trigger needed | Automatic with OnPush |
| **Multiple Subscriptions** | Possible | One per template |
| **Use Case** | Side effects, complex logic | Display data |

---

## Summary

This comprehensive guide covers Angular interview questions from basic to advanced levels, organized by topics. Each question includes:
- **Difficulty Level:** Easy, Medium, or Tough
- **Detailed Answer:** With code examples and explanations
- **Best Practices:** When applicable
- **Use Cases:** Real-world scenarios

**Key Topics Covered:**
- Core Angular concepts
- TypeScript fundamentals
- Components and templates
- Data binding and directives
- Services and DI
- Routing and navigation
- Forms (Template-driven and Reactive)
- HTTP Client and interceptors
- RxJS and Observables
- Change detection strategies
- Modules and architecture
- Pipes and lifecycle hooks
- Performance optimization
- Testing
- Security
- Advanced features (Signals, SSR, AOT)

**Preparation Tips:**
1. Understand the fundamentals first
2. Practice building small applications
3. Review the official Angular documentation
4. Practice coding examples
5. Understand when to use which feature
6. Be familiar with performance optimization techniques
7. Know testing strategies

Good luck with your Angular interviews! 🚀

