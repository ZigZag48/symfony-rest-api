# Symfony 5 REST API skeleton

Symfony 5 + FOSRestBundle + JSON Standard responses + working example

![Travis (.org)](https://img.shields.io/travis/demartis/symfony5-rest-api)
![GitHub last commit](https://img.shields.io/github/last-commit/demartis/symfony5-rest-api.svg)
![GitHub repo size in bytes](https://img.shields.io/github/repo-size/demartis/symfony5-rest-api.svg)
![GitHub language count](https://img.shields.io/github/languages/count/demartis/symfony5-rest-api.svg)
![GitHub top language](https://img.shields.io/github/languages/top/demartis/symfony5-rest-api)
![PHP from Travis config](https://img.shields.io/travis/php-v/demartis/symfony5-rest-api/master)
![GitHub](https://img.shields.io/github/license/demartis/symfony5-rest-api)
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fdemartis%2Fsymfony5-rest-api.svg?type=shield)](https://app.fossa.io/projects/git%2Bgithub.com%2Fdemartis%2Fsymfony5-rest-api?ref=badge_shield)


## Table of Contents
+ [About](#about)
+ [Getting Started](#getting_started)
+ [Contributing](#contributing)



## About <a name = "about"></a>
Symfony 5 skeleton to build REST APIs, inclusive of:

- *FOSRestBundle* (friendsofsymfony/rest-bundle) to simplify the entire process
- *Hateoas Bundle* (willdurand/hateoas-bundle) that specifies relation types for Web links
- *Doctrine*


This project is compliant with:
- [Symfony Best Practices](https://symfony.com/doc/current/best_practices.html)
- [HATEOAS](https://restfulapi.net/hateoas/), [RFC5988 (web links)](https://tools.ietf.org/html/rfc5988), [JSON HAL Model](http://stateless.co/hal_specification.html)
- URIs versioning

### JTTP Coherent output formats
Inspired by [Jsend](https://github.com/omniti-labs/jsend), 
we have set a similar very simple but more coherent and intelligible json format to wrap json responses.

It is called JTTP, and it is compatible with HATEOAS, RFC5988 and HAL standards.
See examples below.

General JTTP output format:

```json
{
  "status": "success|error",
  "code": "HTTP status code",
  "message": "HTTP status message",
  "data|error": {
    "your data": "data or error field only in case of success or error"
  }
}
```

Example - GET resource: GET /v1/books/1
```json
{
    "status": "success",
    "code": 200,
    "message": "OK",
    "data": {
        "id": 1,
        "title": "PHP & MySQL Novice to Ninja",
        "_links": {
            "self": {
                "href": "/v1/books/1"
            }
        }
    }
}

``` 


Example - GET collection: GET /v1/books
```json
{
    "status": "success",
    "code": 200,
    "message": "OK",
    "data": [
        {
            "id": 1,
            "title": "PHP & MySQL Novice to Ninja",
            "_links": {
                "self": {
                    "href": "/v1/books/1"
                }
            }
        },
        {
            "id": 2,
            "title": "Head First PHP & MySQL",
            "pages": 812,
            "_links": {
                "self": {
                    "href": "/v1/books/2"
                }
            }
        }
    ]
}

``` 


Example - error: Resource not found: GET /v1/books/433334
```json
{
    "status": "error",
    "code": 404,
    "message": "Not Found",
    "error": {
        "details": "Resource 433334 not found"
    }
}
```


Example - error: Route not found: GET /wrongroute123
```json
{
  "status": "error",
  "code": "404",
  "message": "Not Found",
  "error": {
    "details": "Resource 433334 not found"
  }
}
```

Example - 500 Internal Server Error
```json
{
    "status": "error",
    "code": 500,
    "message": "Internal Server Error",
    "error": {
        "details": "Notice: Undefined variable: view"
    }
}
```



## Getting Started <a name = "getting_started"></a>

These instructions will get you a copy of the project up and running on your local machine 
for development and testing purposes. 

### Prerequisites

What things you need to install the software and how to install them.
- PHP 7.2.5+
- [composer](https://getcomposer.org/download/)
- [symfony](https://symfony.com/doc/current/setup.html)

### Installing

```bash
git clone https://github.com/demartis/symfony5-rest-api/
cd symfony5-rest-api
cp .env.dist .env
## edit .env if needed
composer install
symfony server:start
```

### Running the example

#### Install database
```bash
php bin/console doctrine:database:create
php bin/console doctrine:migrations:migrate
```

#### Get with Curl

```bash
curl -H 'content-type: application/json' -v -X GET http://127.0.0.1:8000/v1/books
curl -H 'content-type: application/json' -v -X GET http://127.0.0.1:8000/v1/books/2 
```


## Using it as skeleton <a name = "usage"></a>

Add notes about how to use the system.


## Contributing <a name = "contributing"></a>

1. Fork it (<https://github.com/demartis/symfony5-rest-api/fork>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request



## License
[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fdemartis%2Fsymfony5-rest-api.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fdemartis%2Fsymfony5-rest-api?ref=badge_large)