# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.3] - 2021-04-24 :cookie:
- Adds support for Python 3.10 and PEP 563 (however, it works with `httptools`
  built from its current default branch, because the version of `httptools`
  currently in `PyPi` does not support Python 3.10)
- Fixes bug [#109](https://github.com/Neoteroi/BlackSheep/issues/109) (client
  not handling properly various formats for Cookie time representations)
- Improves a detail in the client session URL handling (doesn't cause exception
  for an empty string URL, defaults to "/")

## [1.0.2] - 2021-04-15 :rocket:
- Applies normalization to return types, when a request handler doesn't return
  an instance of `Response` class, defaulting to a `Response` with JSON body
  in most cases, and plain/text if the request handler returns a string;
  this enables more accurate _automatic_ generation of OpenAPI Documentation
  (see #100)
- Renames `HtmlContent`, `JsonContent`, `FromJson`, and `JsonBinder` classes to
  respect Python naming conventions (to `HTMLContent`, `JSONContent`,
  `FromJSON`, and `JSONBinder`); however, the previous names are kept as
  aliases, for backward compatibility
- Corrects a detail in the `JSONContent` class default dumps function
- Adds support for logging the route pattern for each web request (for logging
  purposes, see issue [#99](https://github.com/Neoteroi/BlackSheep/issues/99))
- Adds support for OpenAPI Docs anonymous access, when a default authentication
  policy requires an authenticated user
- Adds support for [`ReDoc`](https://github.com/Redocly/redoc) UI (see [the
  documentation](https://www.neoteroi.dev/blacksheep/openapi/))

## [1.0.1] - 2021-03-20 :cake:
- Adds a built-in implementation for [sessions](https://www.neoteroi.dev/blacksheep/sessions/)
- Corrects a bug in cookie handling (#37!)
- Fixes #90, i.e. missing CORS response headers when exception are used to
  control the request handler's flow
- Corrects URLs in the README to point to [Neoteroi](https://github.com/Neoteroi),
  also for [Codecov](https://app.codecov.io/gh/Neoteroi/BlackSheep)

## [1.0.0] - 2021-02-25 :hatching_chick:
- Upgrades dependencies
- Improves the internal server error page and the code handling it
- Marks the web framework as stable

## [0.3.2] - 2021-01-24 :grapes:
- Logs handled and unhandled exceptions (fixes: #75)
- Adds support for [Flask Variable Rules syntax](https://flask.palletsprojects.com/en/1.1.x/quickstart/?highlight=routing#variable-rules) (ref. #76) and more granular control on the
  route parameters' patterns when matching web requests
- Adds the missing `html` method to the `Controller` class (#77) - thanks to
  [skivis](https://github.com/Neoteroi/BlackSheep/commits?author=skivis)!
- Deprecates the `ServeFilesOptions` class and reduces verbosity of the
  `Application.serve_files` method (#71)

## [0.3.1] - 2020-12-27 🎄
- Implements an abstraction layer to [handle CORS](https://www.neoteroi.dev/blacksheep/cors/)
- Improves the code API to handle [response cookies](https://www.neoteroi.dev/blacksheep/responses/#setting-cookies)
- Improves the default handling of authorization for request handlers (#69)
- Adds more binders: `FromText`, `FromBytes`, `RequestMethod`, `RequestURL`
- Improves `FromJSON` binder to support returning the dictionary after JSON deserialization
- Improves the default bad request response for invalid dataclass
- Adds two more features to the OpenAPI Documentation:
- - support defining common responses to be shared across all operations
- - support defining servers settings without subclassing `OpenAPIHandler`
- Fixes bugs: #54, #55, #68
- Renames `HttpException` class to `HTTPException` to follow [PEP 8](https://www.python.org/dev/peps/pep-0008/)

## [0.3.0] - 2020-12-16 :gear:
- Builds `wheels` and packs them in the distribution package

## [0.2.9] - 2020-12-12 🏳️
- Corrects inconsistent dependency causing an error in `pip-20.3.1`

## [0.2.8] - 2020-12-10 📜
- Links to the new website with documentation: [https://www.neoteroi.dev/blacksheep/](https://www.neoteroi.dev/blacksheep/)
- Removes links to the GitHub Wiki

## [0.2.7] - 2020-11-28 :octocat:
- Completely migrates to GitHub Workflows
- Corrects a bug in `view` method, preventing the word "name" from being a valid
  model property name
- Improves the `view` method to support built-in dataclasses, Pydantic models,
  and instances of user defined classes using `__dict__`
- Corrects bug in binding of services by name

## [0.2.6] - 2020-10-31 🎃

- Adds support for routes defined using mustaches (not only colon notation)
- Corrects two bugs happening when using `blacksheep` in Windows
- Improves the test suite to be compatible with Windows
- Adds a job running in Windows to the build and validation pipeline
- Adds `after_start` application event, fired when startup has been completed
- Adds `FromCookie` binder
- Adds automatic generation of **OpenAPI Documentation** and serving of
  Swagger UI, supporting [OpenAPI version 3](https://swagger.io/specification/) ✨
- Removes weird handling of DI `Services` and `Container` objects in the
  application
- Adds support for list of items to `BodyBinder`
- Adds `python-dateutil` dependency, and support for `datetime` and `date` to
  binders (i.e. possibility to have these automatically parsed and injected to
  request handlers' calls)
- Raises exception for a `typing.ForwardRef` during handlers normalization

## [0.2.5] - 2020-09-19 💯

- **100% test coverage**, with more than _1000_ tests
- Adds `py.types` file to the distribution package, related to
  [PEP484 stubs files](https://www.python.org/dev/peps/pep-0484/) (.pyi)
- Improves type annotations and work experience with **MyPy** and **Pylance**
- Adds support for specifying route paths when serving static files
- Adds support for serving static files from multiple folders
- Features to serve SPAs that use HTML5 History API for client side routing
- Corrects default headers feature
- Removes the rudimentary and obsolete sync logging middlewares
- Makes Jinja2 a required dependency and removes boilerplate used to make it
  optional
- Corrects default JSON dumps to handle dataclasses in `responses`

## [0.2.4] - 2020-09-08 💎

- Refactors the implementation of `binders` to be always type compliant (breaking change)
- Corrects handling of default parameters for binders
- Handles `UUID` bound parameters to request handlers
- Adds more tests for binders
- Sorts route handlers at application start
- Improves `pyi` and type annotations using recommendations from [Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance)
- Upgrades to `httptools 0.1.*` to match the version used in recent versions of `uvicorn`

## [0.2.3] - 2020-08-22 🐌

- Adds a changelog
- Adds a code of conduct
- Replaces [`aiofiles`](https://github.com/Tinche/aiofiles) with dedicated file handling
- Improves code quality
- Improves code for integration tests
- Fixes bug [#37](https://github.com/Neoteroi/BlackSheep/issues/37)
