---
id: bryprof9fv7fuqw2fgdqh1s
title: Basics
desc: ""
updated: 1677050281837
created: 1676922484215
---

## Types of testing

**1. [[Unit Testing]]**
In this type we typically test either:

- a class
- a method
- or even one line of code

here we don't have any:

- database calls
- network calls
- or file system calls.

the above calls get mocked with a mocking framework and the responses are staged. we simply test the logic of the method itself while staging its dependencies.

**2. Component Testing:**
This type is not really a separate type , it is a part of the unit testing type but can be separately categorized to differentiate it from Unit Testing.

Here we still don't have database,network or filesystem calls, but we don't just test one unit, we compound multiple unites as a component and test its collective expected behavior.

**3. Integration Testing**
In this type of testing , we test the component and its dependencies. we don't mock the database , network or filesystem calls, we only occasionally do that to isolate the test scope.

**4. End to end testing:**
in this type of testing , we test the whole flow of the system and how it behaves with other systems.

**5. Performance testing**
In this type we test the performance of the application when some defined number of users call the same API or UI and it contains several subtypes:

- Load testing
- spike testing
- stress testing
- smoke testing

#### Testing Pyramid

![Testing Pyramid](https://wpblog.semaphoreci.com/wp-content/uploads/2022/03/pyramid-progression.jpg)

As you can see the lower you go on the pyramid, the less you have to do. Well,, it is not as simple as LESS but it is cheaper to write unit tests that integration or E2E tests. and the lower you go the faster your tests can run.

Integration tests sits at the sweet spot in which the are not that expensive to write and they are not the slowest to run. therefore they can give the most value for your time and mony.
