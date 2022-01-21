#### What is TTD
1. Test-Driven development.
2. Four Steps:
  - Write a failing test
  - Make the test pass
  - Refactor (重構）
  - Repeat
  - ![IMG_A3DBF659B5AF-1](https://user-images.githubusercontent.com/18608853/150532079-46887e2d-c49b-4fef-8303-be5f468bc8ec.jpeg)
  
  
#### What should you test?
1. Do write tests for code that can't be caught in an automated fashion otherwise. This includes code in your classes' methods, custom getters and setters and mostly anything else you write yourself.
2. Don't write tests for generated code. For example, it's not worthwhile to write tests for generated getters and setters. Swift does this very well, and you can trust it works.
3. Don't write tests for issues that can be caught by the compiler.
4. Don't write tests for dependency code, such as first- or third- party frameworks your app uses.
5. Do write tests in order to determine how a framework works.
6. Do write sanity tests that prove third-party code works as you expect. These sort of tests are useful if the library isn't fully stable, or you don't trust it entirely.



#### The TDD Cycle
- Red: Write a failing test, before writing any app code.
- Green: Write the bare minimum code to make the test pass.
- Refactor: Clean up both your app and test code.
- Repeat: Do this cycle again until all features are implemented.
- ![IMG_792058DE8D7B-1](https://user-images.githubusercontent.com/18608853/150534503-287217a8-6026-4f52-8fe2-97fa4550840a.jpeg)
