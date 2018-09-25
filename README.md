## API Automation Task - Postman test collections

This is the example of Postman test collection that contains request and the response validation. 

#### Setup and structure

First step is to download and install postman client.

Install the command line runner Newman for Postman, using the following command:

`npm install newman --save-dev`

New Workspace is created called API Automation Task, and the new collection API Automation Task.

![capture](https://user-images.githubusercontent.com/10046279/46045510-352b2600-c11e-11e8-892b-7a32ee1b4b41.PNG)

One GET request to the https://jsonplaceholder.typicode.com/users endpoint is created in the collection, and under the tests, three scenarios are written.

First test is to check the status code of the response, using the pm.response object to check if the status is 200.

` 
pm.test("Status code is 200 OK", function () {
    pm.response.to.have.status(200);
});
`

Second test case is verification if the response time is less then 200ms.

`
pm.test(" Validate the response time to be less than 200ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(200);
});
`

Third test case is to iterate over all elements of the json response body  and print out all company names ending in “Group” . First we get the response, and iterate through all the elements, condition is added where is checked if company name from the response is ending with the "Group" using the endsWith() method in javaScript:

`
pm.test(" Print out company names ending in Group", function () {
    pm.response.to.not.be.error;
    pm.response.to.not.have.jsonBody("error");
    var jsonData = pm.response.json();
    for (var i = 0; i < jsonData.length; i++) {
        if(jsonData[i].company.name.endsWith("Group")===true){
            console.log(jsonData[i].company.name)
        }
    }
});
`

If the response is true, then in console the company names are displayed.

#### How to run the collections

Test collection can be run in the Postman client, or using the Newman command line runner.

To run the tests in Postman client, we can open the Collection runner, choose and run the collection we want, in this case it is API Automation Task.

![capture1](https://user-images.githubusercontent.com/10046279/46045522-3d836100-c11e-11e8-8a27-f528b838c590.PNG)

Third test case results can be seen if we open the Postman console:

![capture3](https://user-images.githubusercontent.com/10046279/46045525-41af7e80-c11e-11e8-8e95-0ff8ec64e90e.PNG)

Other option to run the tests is to use the Newman command line runner. If we export our test collection it will be exported in json file, and that will help us to run it using Newman.

In order to run the tests with Newman, following command line needs to be executed:

`newman run postman_collection.json`

In order to use this test collection in Postman, following needs to be executed:

To use this collection in Postman please perform the following steps:

1. Download the postman_collection.json.
2. Import the file in the Postman client.
3. Run the test collection and verify results.
