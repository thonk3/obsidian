This book will walk through a basic issue tracker.
Users will able to create issues with a corresponding description and priority.
Issues can also be marked resolved.

Developed with
- angular and ngrx10
- nodejs 12
- npm 6

 Init new app with
 ```shell
 ng new ngrx-issue-tracker --routing=true
```

the `routing` flag sets ups a separate routing module inside `app-routing.module.ts`
This is for implementing multiple views:
- list of all issues
- detail view
- view to configure the app

> css wont be covered in this book

Jasmine and Karma used for testing

> [!info] complete source code
> https://github.com/nilsmehlhorn/ngrx-issue-tracker

![[Pasted image 20230218154421.png]]

---

next chapter [[NilsNgRx - 3 - Instalation]]