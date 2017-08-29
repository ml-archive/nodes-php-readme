# Getting started
 - [Setup environment](#)
 - [Setup project](#)
 - [Guides](#)

## General

This checklist describes mandatory procedures for every project in development, before they go in production and before an update is deployed to production in general.

Folder structure

- All project specific classes will be in &quot;project&quot;
- Console, which have Commands &amp; Jobs, if you have Commands/Jobs which are not bind to one model, else put them in these folders
- Controllers, have subfolders for Api, Backend &amp; Frontend, each of them can have controllers directly added or have even deeper structure
- Exceptions, if you have global exceptions for your project
- Routes, which have folders for Api, Backend &amp; Frontend, you can add a many subfolders you want in here, they load recursive
- Services, all 3rd party integrations. Create a folder for it, fx Google. If you are doing api calls in your service, use Guzzle. Create clients and models so everything coming in our out of your clients is models
- Support, this is the &quot;others&quot; folder. But all helpers, global contracts, middlewares etc here.
- All folders are plural if it makes sense(Like Laravel does it), Controllers, Models, Routes, Exceptions
- In models each you create a folder in plural for each parent model, a model folder fx Users following folders can be
  - Model and Repository
  - Other 1:1 / 1:n related model folders, fx Tokens,
  - Exceptions, specific exception for this model
  - Observers
  - Transformers
  - Validation, for validators
  - Support, for helpers, DTOs, Requests etc.

Documentation/comments

- All projects should use barryvdh/laravel-ide-helper to have all properties and providers setup for auto-complete
- All function have a docblock with following
  - Description of function if needed
  - @author
  - @access
  - @param (if any)
  - @return
  - @throws (if any)
- Global variables, have a description if needed
- Constants, have a description if needed
- All custom configs have a description
- Comment your code, use it as a break between code groups

Code style/Git/Collaborating with colleagues

- Enforce the code standard PSR-2. This will help others to quickly get an overview of your code.
- Code as strict as possible, since php7 enforce all inputs and return types, and use exceptions for other cases. Use strict model types if you need a specific Id, instead of just accepting integers
- If in doubt use framework specific conventions.
- Keep your git commit messages descriptive.
- Try to keep your git repositories as clean as possible.
- Remember that you&#39;re not the only person to read and understand your work.

Migrations and seeders

- All projects are using migrations and seeders/factories. You should always be able to checkout a project and do &quot;pa migrate:refresh --seed and have it up running

Important requests to 3rd parties

- When the importance of sending a push, charging money or firing important api call triggered by events. Always create datetimes in the table for when it was tried, when it was succeeded, when it was failed and a log. This way you can easy integrate a retry system and you will know if something went wrong, without looking through 100k lines of log.
- example sent\_at, succeeded\_at, failed\_at &amp; log. json\_encode the response of the api call or the exception in.

Models

- Always use following global variables
  - fillable
  - table
  - casts
  - dates
- Consider defining your api fields for select here also, fx as const
- Always set up relations
- Really consider not using hasManyThrough, you always need that pivot model for observers, extra fields etc

Caching strategies

Rules of thumb for considering caching:

- When a response is the same for all users it should be cached.
- When a large portion (~35% of the data) of a response is the same for all users, that portion should be cached.
- When a response rarely changes eg. a user&#39;s settings, caching could be considered.
- Remember to update your cached keys when necessary.
- Remember to clear cache on data changes, use observers for this
- Use the nodes cache pattern, it&#39;s easy for others to check what is cached for how long, and gives some easiness of passing params as cache keys

Queueing

Considerations for Gearman/Beanstalkd queueing routines

- Queue logging.
  - Is logging of the queued element needed?
  - Remember when starting a queue, it&#39;s a different server that means if you just stored an entry which you try to lookup again, it might not have synced to that database server live, you can use the findByIdContinuously(), which will try to look up several times
  - Clean up you queue-log by removing successfully executed entries.
  - Use different queues for, if you have queue tasks taking long time, and tasks which are super important to run fast, a good pattern is to always use \Queue::pushOn(Queues::NAME\_OF\_QUEUE, $job), and keep all your queues in one file as constants
  - failed\_jobs table is ALWAYS added, and retry on queues is default 1

Database

- Select specific columns instead of all (\*).
- Ensure your database changes are aggregated to the production environment.
- Make sure to paginate all responses that has the potential to grow large.
  - Eg. follower lists, posts, likes, etc.
- Use eager loading

Exceptions/Bugsnag

- Bugsnag is a tool to collect exception from staging/live, it&#39;s very powerfull and should be used on all projects
- Not all exceptions should be written to bugsnag. Remember to analyze all thrown exceptions and evaluate if you need this in. Use the dontReport()/report() functions
- Exceptions will get grouped Exception namespace (you can group them by message), but use as many Custom exceptions as possible extending the nodes exception

Test

- All projects will have use phpunit to test (new from 1/6 - 2016)
 - controllers
 - model functions
 - repositories
 - routes
 - services
 - support
 - all project specific which can be tested

Optimization

- Network in request is always bad, if it&#39;s needed consider if it&#39;s possible to cache. If you can put it in a queue, do so, fx for mail/push/sms
- Database queries is often the slowest part of the request. Use &quot;pa debug&quot; to check how many you do, and how big they are. Consider selects, eagerload and cache
- Check bugsnag daily when you have frontend/mobile working, consider setting it up to mail you on new exception during development. It&#39;s cool to fix the bugs before they create the tickets

Process 

- TDD
