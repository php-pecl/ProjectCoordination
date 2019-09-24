# Introduction

The resource type is a left-over artefact from before PHP had classes.

It was used as a way to represent non-trivial types in PHP userland code. For example a file handle or curl structure.

The problem is that the resource type is a very generic type, which is not very useful. For example if you have a function

```
function foo(resource $bar) {
...
}
```

You could pass in a filehandle, a curl resource or any other resource type, and the parameter type check would pass.

It would be an improvement to PHP if the resource type was removed, by replacing every use of it with a more specific type, which currently would be a class e.g. a Curl object or a FileHandle object.

These replacement classes aren't required to have any methods available on them; it would be fine for them to just be used to define specific types, and isn't required to make them use inheritance.

## BC Impact

The backwards compatibility breaks from the conversion of the resource type to object is considered minimal,
as the BC breaks are limited to code using the ``is_resource()`` and ``get_resource_type()`` functions.
This is due that a resource is produced as a return value from a function and passed as a parameter to all relevant functions.
This means that these changes can occur in between minor version as can be seens with the resource to object migration for the Hash extension in PHP 7.2. [1]

# General plan

* For each of the extensions in PHP src, replace any use of a resource type with a specific class type.

* Contact all known extension maintainers, for who the extension uses resource types and help them move away from resource types.

* Figure out how to mitigate BC breaks for the above.


## PHP core extensions 

### Implementations pending

* **sysvshm** - [WIP PR#3235](https://github.com/php/php-src/pull/3235)

### Still needed
*insert list of php core extensions that need work here*.

## PHP external extensions

*insert list of known non-core extensions that need work here.*

# References

[1] https://www.php.net/manual/en/migration72.incompatible.php#migration72.incompatible.hash-ext-to-objects
