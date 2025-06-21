# APi_Test

-----------------------------------------Gherkin----------------------------------------

	     -Gherkin : 
	    - Gherkin is a plain-text language with a simple structure. It is designed to be easy to learn by non-programmers, Behat is a tool to test the behavior of your application, 
	      described  in special language called Gherkin

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
                                 what type of requst we want to send  get, put(need id) ,post ,delete,patch
                         then()  :
                                  all validation we have to do in then section status code ,respose body ,cookies ,header
                         log() :
                                    read console data. is used to get all information from response

                                    after log we have to add one method mandatory
                         all() : 
                                  is used to print all data which having with .log()


-------------------------------------------------Post ----------------------------------------------------------------

     * from respons capture the ID :
                                        .jsonPath() --> navigate through a JSON object and retrieve specific values, such as strings, numbers, arrays, or nested objects.
	                                       	.getString("name");

     1. post--->  how many way to create requst body
                   -HashMap - org.json - pojo - - external json file
                   1. HashMap -->
                                  HashMap map = new HashMap();
                                 		map.put( "name", "morpheus");
                                 		map.put("job" ,"leader"); 
                                 		String[] data = {"c" ,"c++"};--> if we have json array convert into a java array
                                 		map.put("data", data);--> (java array add as a value)
                                            --> json array name 
                    2. org.json -->   

                                    JSONObject data = new JSONObject();
                                		data.put("name", "morpheus");
                                		data.put("job", "collector");
                                given() 
                                .body(data.toString())-> convert into ToString because data in JSONObject
                                        
                     3. using pojo -->
                                      -create pojo class  
				      
                     4. external json file -->

		               
---------------------------------------------RestAssured---------------------------------------------------------------

	1. path & Query Parameters :
	                          'https://dummyjson.com/RESOURCE/?delay=1000'
	                         ----------------------> ------> ------------------->
	                           domain name             path  ? Query parameters
                           given()
			  .pathParam("data","RESOURCE")
			  .queryParam("delay", 1000)
	                  .when()
	                  .get("https://dummyjson.com/{data}")
		   
	   .pathParam() --> This method allows you to dynamically insert values into the URL
           .QueryParam() --> you can set query parameters at runtime, allowing for more flexible and reusable API calls.
	    

        2. cookies & Header :
	                         - cookies & Header is a part of a response
                                 - capture cookies inforamtion
                                 -  if cookies value keeps changing, means that functionality working find
                                   when()
				         .get("https://www.youtube.com/watch?v=kxPC6wEbbaU&t=906s")
				 .then()
			                 .cookie("YSC","nCzDZPp6TVM").log().all()
				
                 get single cookie  -->      
	                                   Response respons = given()
				          .when()
					  .get("https://www.youtube.com/watch?v=kxPC6wEbbaU&t=906s");
					  
					 String singlecookiesvalue =  respons.getCookie("YSC");
	                                 System.out.println("Single cookie-->"+singlecookiesvalue);
                 get all cookies -->
		                      
                                        Response respons = given()
				          .when()
					  .get("https://www.youtube.com/watch?v=kxPC6wEbbaU&t=906s");
		  
					 Map<String , String> allcookies =  respons.getCookies("YSC");
	                                 System.out.println("all cookie-->"+singlecookiesvalue);
				  
        3. Header  :
                       in header we validate mostly Content-Type ,Content-Encoding, Server
		       		given()
				.when().get("https://www.youtube.com/watch?v=kxPC6wEbbaU&t=906s")
                                .then()
				.header("Content-Type", "text/html; charset=utf-8").header("Content-Encoding", "gzip")
                         - there is 2 type single header its represent only single header  & headers  its represent multiple header
		         - header(name:value)
	4. log  :  
                     Logs everything in the response, including e.g. headers, cookies, body. Pretty-prints the body if content-type is either either XML, JSON or HTML.. 
		       .log().headers()   .log().body()  .log().cookies and much more
	             he log() method is a powerful tool for enhancing visibility and debugging capabilities in API testing, allowing you to monitor both the requests you send and the 
                   responses you receive

------------------------------------------------Parsing JSON Respons Body----------------------------------------------------------

    testNG Asserstion : 
                        
-----------------------------------------------------PostMan-------------------------------------------------------------------------
    
validation we do when get a response :
 
          response Time , size of data , response body , cookies , heaader , states code 
          to test all items we need assertaion(validation point)
          pm --> libray we use provide by postman

20-06-2025 : 
 
	      1. insted of doing Web we directly test the API. direct requst to API and get Response from API 
              and do some validation on response 
              2.                   'https://dummyjson.com/RESOURCE/?delay=1000'
	                         ----------------------> --------------------> ------------------->
	                           domain name          path(end point(never changed))  ? Query parameters
                  Request check -- URL , data , Key , Authentication code
	          Response check --  data response body (json , xml),status code ,coockies ,  header ,time

               cookies : 
                The server sends cookies in the response to:
               🔐 Identify you (session)
               🎯 Track visits
               ⚙️ Save preferences

	     Headers : 
                   Headers are used to give extra information about your API request.
                   Headers are key-value pairs that carry metadata (information about the request).
                   the server so it allows you to access or process your request properly.   
 

                |  Header Key     | Header Value            | What It Means to the Server                         |
		| --------------- | ----------------------- | --------------------------------------------------- |
		| `x-api-key`     | `reqres-free-v1`        | 🔐 "Here is my API key. Please allow me to access." |
		| `Authorization` | `Bearer eyJhbGci...`    | 🔒 "I am a logged-in user. Here is my token."       |
		| `Content-Type`  | `application/json`      | 📤 "I'm sending data in JSON format."               |
		| `Accept`        | `application/json`      | 📥 " Tell Server What Response You Want."           |
		| `User-Agent`    | `PostmanRuntime/7.32.0` | 🧠 "Here’s info about who is making the request."   |

			      The Headers section in Postman is used to:
				Identify yourself (auth keys, tokens)
				Tell the server about the type of data you're sending and receiving
				Provide technical info about your request
     
        Params : 	
               In Postman, the "Params" section is used to add query parameters to your URL.
               These are the values sent in the URL itself, not in headers or the body.

       Authorization:     
                      "Hey, I am a trusted user. Here's my token or key."
                      Authentication ensures that only authorized users can access certain APIs. Examples:
                        API Key
			Bearer Token (OAuth)
			Basic Auth

      we use JS assertion for validation of response : 
                    - In Postman, response validation is done using assertions written in JavaScript under the "Tests" tab( Tests tab write JavaScript code to validate API responses)
                    - The most commonly used type of assertion in Postman is:
                    - for validation of response : use JS , JSON
                    -  in postMan we write script :
                         1 test script ----> in that we do all type of validation, the test tab executed when both request and response completed then the test tab executed.
                         2 pre-request script --> this will executed before sending the requst and after response tests scripts executed.
                                                      pre-request---> Requst --> Response ----> Tests
			Chai.js Assertion Library (BDD style) : 
			--->postman
			pm.test("Status code is 200", function () {
			    pm.response.to.have.status(200);
			});
			
			validating JSON field in response : 
			
			 let jsonData = pm.response.json();
			pm.test("Name should be John", function () {
			    pm.expect(jsonData.data.name).to.eql("John");
			});

  21-06-2025
                     
             variable in postman  : {{URL_GLOBALE}}/api/users?page=2  :
 
             global : accessable in workspace 
            collection : accesable within only coolection 
            Envirment :  if we want to execute evirnment variable we have to switch the particuler evirnment 
            local :  create and accessable only  in request level (pre-request(tab))
            data :  external file csv/text
                     
            API Chaining : we get the response from one AIP, and the same response we will pass as part of a request in the next API  

------------------------------------------------------------Qus-------------------------------------

       ... in api testing mean think is to validate satus code , assertthat , response body  its a end to end api testing.
	Q...DTO : data transfer objcet


 
