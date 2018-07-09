# Ruby on Rails Best Practices

* Prefer TDD / Outside-in development to keep test coverage high
  * [This is why](https://www.quora.com/What-are-the-pros-and-cons-of-test-driven-development)
* Do not introduce model callbacks that have external dependencies
  * [This is why](http://samuelmullen.com/2013/05/the-problem-with-rails-callbacks/)
  * Use `FormObject` or `ServiceObject` patterns (some examples [here](http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models/))
* When integrating with external services or libraries, prefer using Facade Pattern (sometimes referred to as Wrapper Pattern)
  * [Some details](https://en.wikipedia.org/wiki/Facade_pattern)
  * It abstracts away communication through API, what makes writing specs easier (no need to use `VCR` that much or at all)
  * It makes interacting with external services and libraries more comprehendable and readable
* Keep your controllers RESTful (implement only default REST actions)
  * [This is why](http://jeromedalbert.com/how-dhh-organizes-his-rails-controllers/)
* Routes 
 * Avoid the `:except` option
 * Use the `:only` option to explicitly show exposed routes
* Use ```raw()``` instead of ```html_safe``` when simply accepting data from field (most likely in views)
* Use ```html_safe``` when building content explicitly (helpers, decorators etc.)
* Do not  perform additional explicit formatting in the view layer - use decorators. So instead of ```for_display(decorated_resource.created_at)``` there should be just ```decorated_resource.created_at```
* In relations, use names retrieved from actual classes, i.e. ```belongs_to :buyer, class_name: User.name```
* [Keep both controllers and models slim] (http://blog.codeclimate.com/blog/2012/10/17/7-ways-to-decompose-fat-activerecord-models) 
* **Follow [Law of Demeter] (http://pl.wikipedia.org/wiki/Prawo_Demeter)**
* **Follow [Single Responsibility Principle] (http://pl.wikipedia.org/wiki/Zasada_jednej_odpowiedzialno%C5%9Bci)**
* Avoid bypassing validations with methods like `save(validate: false)`,
  `update_attribute`, and `toggle`.
* Avoid instantiating more than one object in controllers.
* Don't change a migration after it has been merged into master if the desired
  change can be solved with another migration.
* Don't reference a model class directly from a view.
* If there are default values, set them in migrations.
* Keep `db/schema.rb` or `db/development_structure.sql` under version control.
