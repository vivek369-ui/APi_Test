# APi_Test

-----------------------------------------
 
    - Gherkin is a plain-text language with a simple structure. It is designed to be easy to learn by non-programmers, Behat is a tool to test the behavior of your application, described 
       in special language called Gherkin

      1. Features:
                    Feature: Serve coffee
                              In order to earn money
                              Customers should be able to
                              buy coffee at all times
                            
                              Scenario: Buy last coffee
                                Given there are 1 coffees left in the machine
                                And I have deposited 1 dollar
                                When I press the coffee button
                                Then I should be served a coffee

      2.Scenarios:  followed by an optional scenario title. Each feature can have one or more scenarios, and every scenario consists of one or more steps.

                  Scenario: Wilson posts to his own blog
                  Given I am logged in as Wilson
                  When I try to post to "Expensive Therapy"
                  Then I should see "Your article was published."
                
                Scenario: Wilson fails to post to somebody else's blog
                  Given I am logged in as Wilson
                  When I try to post to "Greg's anti-tax rants"
                  Then I should see "Hey! That's not your blog!"

      3.Scenario Outlines: Copying and pasting scenarios to use different values can quickly become tedious and repetitive  

                Scenario Outline: Eating
                Given there are <start> cucumbers
                When I eat <eat> cucumbers
                Then I should have <left> cucumbers
              
                Examples:
                  | start | eat | left |
                  |  12   |  5  |  7   |
                  |  20   |  5  |  15  |
                  
      4.Backgrounds:Backgrounds allows you to add some context to all scenarios in a single feature. A Background is like an untitled scenario, containing a number of steps.

          Feature: Multiple site support
                    Background:
                      Given a global administrator named "Greg"
                      And a blog named "Greg's anti-tax rants"
                      And a customer named "Wilson"
                      And a blog named "Expensive Therapy" owned by "Wilson"
                  
                    Scenario: Wilson posts to his own blog
                      Given I am logged in as Wilson
                      When I try to post to "Expensive Therapy"
                      Then I should see "Your article was published."
                  
                    Scenario: Greg posts to a client's blog
                      Given I am logged in as Greg
                      When I try to post to "Expensive Therapy"
                      Then I should see "Your article was published."

                  
        5.steps: 
                         given() :
                                  we pass Content type , set cookies , add auth , add para , set headers info etc...
                                         body() : here we pass only String data
                                         .contentType(ContentType.JSON) : type of data pass into body (Specify the content type of the request.)
                         when() :
                                 what type of requst we want to send  get, put ,post ,delete,patch
                         then()  :
                                  all validation we have to do in then section status code ,respose body ,cookies ,header
                         log() :
                                    read console data. is used to get all information from response

                                    after log we have to add one method mandatory
                         all() : 
                                  is used to print all data which having with .log()
               
