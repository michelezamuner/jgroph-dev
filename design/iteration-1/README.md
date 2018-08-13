# Iteration 1

## Business requirements

The application will just display a list of bookmarks data:
- the application is distributed on the Web, as a service
- a list of bookmarks is displayed at the URI `/bookmarks`
- each bookmark contains just an ID and a URL
- bookmarks data is stored in memory on the server
- bookmarks data is a sample, defined in the code

As first iteration, a monolithic application will be enough. The principles of the Clean Architecture will be followed as much as possible.


## Domain

The only domain model currently needed is the Bookmark, representing a link to a resource that is identified by an URL (as such it can be both an online resource, or some file on the local computer, that can be opened in the browser following a `file://` link for example). In addition to the URL, an ID is also defined, to make sure that all Bookmarks are uniquely identified.


## Actors and use cases

At the current moment only one actor is supported by the application, which is the User. Adapters actors that are mapped to User are Web User and API User.


### User

The User uses the features of the application concerning managing Bookmarks: in particular, he can get the pre-defined List of Bookmarks.

```gherkin
Feature: List Bookmarks
    As a User
    I want to get the List of Bookmarks
    In order to see which Bookmarks are available

    Background:
        Given there are bookmarks:
            | ID | URL                           |
            | 1  | https://google.com            |
            | 2  | file:///home/myself/file.html |

    Scenario: Get the List of Bookmarks
        When I get the list of Bookmarks
        Then I get:
            | ID | URL                           |
            | 1  | https://google.com            |
            | 2  | file:///home/myself/file.html |
```


#### Web User

The Web User displays the List of Bookmarks in an HTML page. This is directly mapped to the List Bookmarks use case of User.

```gherkin
Feature: List Bookmarks on Web
    As a Web User
    I want to display the List of Bookmarks
    In order to see which bookmarks are available

    Background:
        Given there are bookmarks:
            | ID | URL                           |
            | 1  | https://google.com            |
            | 2  | file:///home/myself/file.html |

    Scenario: Display the List of Bookmarks
        When I am on "/bookmarks/"
        Then I see an HTML page with links to:
            | Link                          |
            | https://google.com            |
            | file:///home/myself/file.html |
```


#### API User

The API User gets the List of Bookmarks as a JSON response. This is directly mapped to the List Bookmarks use case of User.

```gherkin
Feature: List Bookmarks on API
    As an API User
    I want to get the List of Bookmarks
    In order to perform additional operations with it

    Background:
        Given there are bookmarks:
            | ID | URL                           |
            | 1  | https://google.com            |
            | 2  | file:///home/myself/file.html |

    Scenario:
        When I am on "/bookmarks/"
        Then I see a JSON response containing:
            | JSON Object                                        |
            | {"id": 1, "url": "https://google.com" }            |
            | {"id": 2, "url": "file:///home/myself/file.html" } |
```

![Actors diagram](./usecase.svg)