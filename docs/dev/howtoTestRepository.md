# Howto Test (in Winery Repository)
In this document the way how tests for the Winery Repository are implemented based on real implemented Example. The Example is Implemented in the Last Chapter its a simple implementation of the `NodeTypeImplementationResourceTest`. 


This test will cover the GET Responses to the Client created by the Backend Implementations, based on the Winery Test Repository.

## Preparations 
In this chapter we will cover how to get the right information to prepare a Test.

### Find class to Test
First of all you should find a Class to test, where you know the logic behind.
If you follow this example, you will test the Response generated by the backend against a local File you created, it will contain the Response we are expecting.

### Download the Winery Test Repository
Based on the Winery test Repository the Responses will be created from the backend. Its available under [Winery Quickstart](http://eclipse.github.io/winery/user/#quickstart)

#### Windows

You will have to check out the Winery repository to `C:\Winery-Repository`
That means you will navigate to your C-Directory with an CMD or Powershell. After that you clone `https://github.com/winery/test-repository.git`

`git clone https://github.com/winery/test-repository.git C:\winery-repository`

Now we have the most recent of the winery repository test data.

#### Unix,Mac,Ubuntu etc.

You will have to check out the Winery repository to `~\Winery-Repository`
That means you will navigate to your Homedirectory with a terminal or your favourite shell. After that you clone `https://github.com/winery/test-repository.git`

`git clone https://github.com/winery/test-repository.git ~/winery-repository`

Now we have the most recent of the Winery repository test data.

### How to get the Right Commit ID for your Test
If you write a new Test you should always base it on the last commit, if you add Files use that commit.
If you want to know which is the latest commit id right now you should get the SHA1 Commit Id.

To get it from your checkout just follow these Steps:

 - Go to the Github Site [Commit overview](https://github.com/winery/test-repository/commits/black)
 - Choose your commit and look at the right side - you will see a short code like `88e5ccd` 
 - Click on the Commit code you want to see
 - On the Right Side you will see the full Commit ID, it starts with the same as the link you clicked before, in this case `88e5ccd6c35aeffdebc19c8dda9cd76f432538f8` (`gitk` can be used, too).

 
 
## Create a new Test
In this chapter we will cover the notation and the Paths you should place the Test Classes you create.

### Create a Test Class
If you want to Test the Class `NodeTypeResource` in the Package `org.eclpse.winery.repository.resources.entitytypes.nodetypes`.
That means we need to create a respective package in the Test Folder of the Project.

We create a new Class for the `NodeTypeResource` Test which we name  `NodeTypeResourceTest` in the Package  `org.eclipse.winery.repository.resources.entitytypes.nodetypes` in the Test Folder located under src/test`

Now that we are Testing a Resource Class we have to add `extends AbstractResourceTest` to the Class definition, this will help us simplifying the Test Classes and only put the tests them self in there.


## Add Test Methods

For basic testing in the repository, we created two Testcases for each type.
```
  @Test
  public void getInstanceXml() throws Exception {
  // Getting Xml from a API, checking if its equal to the expected local file.
  }
  @Test
  public void getServicetemplate() throws Exception {
  // Getting JSON from a API, checking if its equal to the expected local file.
  }
```

These are the two basic methods to test the capability of the API, to serve JSON and XML mime types as response.

## Things to prepare on Test

Before running the Basic Test logic like in the Chapter [Add Test Methods](##Add Test Methods)
you have to get a Github commit-id from the [Test-Repository](https://github.com/winery/test-repository).

In the following example is shown how to get a revision:
```
  @Test
  public void getServicetemplate() throws Exception {
    this.setRevisionTo("c25aa724201824fce6eddcc7c35a666c6e015880");
    // Test Logic 
  }
```
## Implement a Testing Logic

To Test the Logic you can simply implement this two liner Test, it will check out the Revision `c25aa724201824fce6eddcc7c35a666c6e015880` from Github Repository located under [Test-Repository](https://github.com/winery/test-repository).
Afterwards it will send a GET request against the Backend initialized by the GIT-Repository Data. The Response will be tested for equality against a File with the expected Result.
  
If the Result is equal the Test will become marked as successful.  
```
	@Test
 	public void getInstanceXml() throws Exception {
 		this.setRevisionTo("c25aa724201824fce6eddcc7c35a666c6e015880");
 		this.assertGet(INSTANCE_URL, INSTANCE_LOCAL_PATH);
 	}
```
## Run a Test or Test Class

If you want to run a Test you can simply Run it from Menu in your Eclipse or IntelliJ IDE.

## Appendix 

Here we have a simple implementation of the `NodeTypeImplementationResourceTest`. 
````

package org.eclipse.winery.repository.resources.entitytypeimplementations.nodetypeimplementations;

import org.eclipse.winery.repository.resources.AbstractResourceTest;

import org.junit.Test;

public class NodeTypeImplementationResourceTest extends AbstractResourceTest {

	private final String ENTITY_TYPE = "nodetypeimplementations/";
	private final String INSTANCE_XML_PATH = "entityimplementations/" + ENTITY_TYPE + "instance.xml";
	private final String BAOBAB_JSON_PATH = "entityimplementations/" + ENTITY_TYPE + "baobab_inital.json";

	public static final String FOLDERPATH = "http%3A%2F%2Fwinery.opentosca.org%2Ftest%2Fnodetypeimplementations%2Ffruits/baobab_impl";


	private final String INSTANCE_URL = ENTITY_TYPE + FOLDERPATH;

	@Test
	public void getInstanceXml() throws Exception {
		this.setRevisionTo("c25aa724201824fce6eddcc7c35a666c6e015880");
		this.assertGet(testStringConverter(INSTANCE_URL), INSTANCE_XML_PATH);
	}

	@Test
	public void getServicetemplate() throws Exception {
		this.setRevisionTo("c25aa724201824fce6eddcc7c35a666c6e015880");
		this.assertGet(ENTITY_TYPE, BAOBAB_JSON_PATH);
	}
````

## License

Copyright (c) 2013-2017 University of Stuttgart.

All rights reserved. This program and the accompanying materials
are made available under the terms of the [Eclipse Public License v2.0]
and the [Apache License v2.0] which both accompany this distribution.

  [Apache License v2.0]: http://www.apache.org/licenses/LICENSE-2.0.html
  [Eclipse Public License v2.0]: http://www.eclipse.org/legal/epl-v20.html