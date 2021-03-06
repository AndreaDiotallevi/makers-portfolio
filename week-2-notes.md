# Week 2 Notes

[Monday](#monday-18th-november-2019) | [Tuesday](#tuesday-19th-november-2019) | [Wednesday](#wednesday-20th-november-2019) | [Thursday](#thursday-21th-november-2019) | [Friday](#friday-22th-november-2019)

By the end of the week all developers can:

- Use all of week 1's skills (don't underestimate the importance of this)
- Break one class into two classes that work together, while maintaining test coverage
- Unit test classes in isolation using mocking
- Explain some basic OO principles and tie them to high level concerns (e.g. ease of change)
- Review another person's code and give them meaningful feedback

## Monday 18th November 2019

- I paired with David on the oystercard challenge and went really well. We both were solving problems very quickly and helped each other, forcing ourselves to follow the correct TDD process.

- Went to my first **process workshop** in the afternoon and funnily enough I got paired with Melvin, my mentor. We both did a 25 minutes session with 5 minutes feedback - me on the 'get middle letter' challenge and Melvin on the 'ten minutes walk' challenge. The feedback was very instructive as well as the following Q&A:

  - Instead of changing screen multiple times, better copy-paste useful information into the code base and split the screen with integrated terminal.

  - I could have worded my solution in a more complete way before jumping into coding the solution.

  - Read carefully about what is requested and how you are supposed to call the method from ```irb``` - ```"string".get_middle``` is different than ```get_middle("string")```.

  - Each test should help towards the correct solution. Therefore, apart from the first trivial test, we shouldn't hard-code the solution, but instead try to improve the code step by step. The order of the tests is important.

## Tuesday 19th November 2019

- Attended a 'feedback workshop' from Dana in the morning and it was very interesting.

- There are 3 types of feedback:

  - Appreciation.

  - Evaluation.

  - Coaching.

- Use the 'ASK' framework when giving feedback:

  - Actionable.

  - Specific.

  - Kind.

- I particularly enjoyed the last part of the workshop, when we had the chance to give our personal feedback to real work examples. I learned the following:

  - Start with "I have noticed..." rather than "You are...".

  - Request, not command.

  - Ask a question to check how the other responds and start from there, instead of going straight to the request.

- I paired with Kealan and it was a lot of fun. In the end he gave me the useful feedback of trying to involve the navigator a bit more with research, regardless if I thought I already knew the answer / syntax, in order to give the other person the opportunity to learn that particular thing as well.

- Received a great feedback from Alice on the video recording during my process workshop yesterday:

  - ANALYSING USER NEEDS:

    - You should spend a bit more time on the instructions and acceptance criteria:

    - You may want to build an input output table to explore the edge cases of the program, and to help you decide which case you should start with.

    - If you look more closely at the acceptance criteria, it's ```get_middle('test')``` not ```'test'.get_middle```.

  - TESTS:

    - You should start with a simpler test case (maybe one or two letters).

    - Each test description should be more specific (prefer ```it returns 'es' when passed 'test'``` to ```it returns the middle characters of a string```).

    - Also, I got very confused later because your test descriptions are reversed. When reading tests results, the test description is giving you context on which is the test that is failing. A wrong description makes it much more difficult to understand what is wrong.

    - Also you need more tests.

  - MODELLING / ALGORITHM DESIGN:

    - Between 8:20 and 9:25, I'm not sure what you were doing, but I guess you were developing the algorithm in your head.

    - Because of your test progression, you are jumping directly from hard coded result to creating the whole algorithm, when you should probably do one thing at a time (like maybe tackle odd number first).

    - Later you looked up "find middle char in string ruby". This is a little bit more specific than I would google. Since you have already found out about round, I would probably already be trying things either in ```irb``` or the code.

    - What I would expect you to google here is "how to get a char from a string by its index" or something along these lines.

  - CODING:

    - 14min - The code you write is complex enough that I would test it in ```irb``` as I go (or add puts and run the tests after every line). This is because debugging is harder when the whole thing has been written, as opposed to when you check that the result is what you expect at every stage.

    - 15:50 - When you fix the bug, there, I think you are missing the point of the error, which does not show the best debugging process.

    - The error was ```undefined method even?` for "test":String```. This should lead you to ask yourself what ```even?``` is defined on. Instead you choose to do things differently, which means you are not learning something new from the error.

    - Again here I would expect you to use ```irb``` a lot more to try things out.

    - 18min - your test descriptions tripped you up there.

  - OVERALL:
  
    - You need to improve your attention to detail, and I would really encourage you to run your code at every step of the process. This may mean going slightly slower, but in the end it would make you a lot faster.

## Wednesday 20th November 2019

- Attented a **workshop on domain models** in the morning with Sophie and it was very informative.

- There are two types of domain models:

  - **Sequence diagram**: the classes are displayed in rectangles at the top and the messages between the objects are shown with arrows. Continuous lines for messages, dotten lines for responses. Better not extend a message through two classes.

  <img src="./img/sequence.png" width="600" height="350" />

  - **Class diagram**: the instance variables and methods are listed in a table for each class.

  <img src="./img/class.png" width="600" height="200" />

- I paired with Sam and it was a great session, with lots of pace, balance and good exchange of different ideas. We learned how to extract a new class from an existing class making sure to keep the functionality. After the pairing he told me I helped him understand the difference between the driver and navigator roles and I was happy about that.

- Went to another process workshop, this time tackling the 'ten minute walk' challenge, with Alastair. I think I approached it more carefully than last time, paying attention to the user needs and starting from simple test cases. I guess the most difficult part this time was how to decide the best order for the test cases, and reach the final code in the most logical way.

## Thursday 21th November 2019

- Studied in the morning important principles of object-oriented programming, like forwarding and dependency injection.

- In object-oriented programming, **forwarding** means that using a member of an object (either a property or a method) results in actually using the corresponding member of a different object: the use is forwarded to another object. Forwarding is used in a number of design patterns, where some members are forwarded to another object, while others are handled by the directly used object. The forwarding object is frequently called a wrapper object, and explicit forwarding members are called wrapper functions.

  ```ruby
  class Diary
    def initialize
      @contents = "Eric Cantona is the best footballer"
    end

    def read
      @contents
    end
  end

  class SecretDiary
    def initialize
      @diary = Diary.new
      @unlocked = false
    end

    def unlock
      @unlocked = true
    end

    def lock
      @unlocked = false
    end

    def read
      return "Go away!" unless @unlocked
      @diary.read
    end
  end
  ```

  See how `SecretDiary` **forwards** methods on to `Diary`. The behaviours of 'locking/unlocking' and 'diary keeping' are now in separate classes. This is a better way of organising our code.

- In software engineering, **dependency injection** is a technique whereby one object supplies the dependencies of another object. A "dependency" is an object that can be used, for example as a service. Instead of a client specifying which service it will use, something tells the client what service to use. The "injection" refers to the passing of a dependency (a service) into the object (a client) that would use it. The service is made part of the client's state. Passing the service to the client, rather than allowing a client to build or find the service, is the fundamental requirement of the pattern.

  ```ruby
  class Greeter
    def initialize(smiley = Smiley.new)
      @smiley = smiley
    end

    def greet
      "Hello #{@smiley.get}"
    end
  end

  class Smiley
    def get
      ":)"
    end
  end
  ```

  Instead of hard coding the dependency, we 'inject' it into the class via the initializer. Dependency injection is a technique for helping you test classes in isolation. It allows a class to use either its real dependency, or a double.

- I paired with Danny and it was very interesting. I liked the fact that he cared about taking good breaks and spend quality time in front of the screen. We also had a nice conversation about how the mind works and the benefits of meditation, which made the session quite unique.

## Friday 22th November 2019

- Was supposed to pair with Hisham, but he was not well.

- It was the first time for me flying solo in the afternoon and I found myself being very concentrated and focused. I worked on the Oystercard challenge and consolidated my understanding of the class extracting process.

- In the morning I studied OOP principles such as:

  - **Law of demeter**: a design guideline for developing software, particularly object-oriented programs. In its general form, the LoD is a specific case of **loose coupling**. The guideline can be summarized in each of the following ways:

    - Each object should have only limited knowledge about other units.

    - Each object should only talk to its friends; don't talk to strangers.

    - Only talk to your immediate friends.

  - **Open closed principle**: tells us that we want our code to be open for extension but closed for modification. The idea is that if we need to add some new functionality then we can do that by extending our code rather than modifying it.

## Saturday-Sunday 23th-24th November 2019

- [Takeway challenge](https://github.com/AndreaDiotallevi/takeaway-challenge/blob/master/MY_README.md) over the weekend. I had fun solving the challenge and learned how to use the Twilio API, test 3rd party dependencies, use environment variables and apply the dependency injection principle.
