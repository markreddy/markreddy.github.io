---

title: JSON Data Types
description: "A quick run down of all the JSON data types."
tags: [blog, json, javascript, data, objects]
comments: true
image:
  feature: texture-feature-01.jpg
---

JSON (JavaScript Object Notation) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate. It is based on a subset of the JavaScript Programming Language.  Despite its relationship to JavaScript, it is language-independent, with parsers available for many languages. It has gained much popularity and is implemented in countless hight value, scalable projects worldwide. For those don’t like XML, JSON is an excellent alternative.<br><br>
JSON represents six data types:<br><br>

**Primitive Types**

* String
* Number
* Boolean
* Null

**Structure Type**

* Object
* Array

String: Series of characters (letters, numbers, or symbols); double-quoted UTF-8 with backslash escaping.<br><br>
Number: A number can be an integer, real number, decimal point, with exponent part and prefix minus sign but it does not contain hex and octal forms.<br><br>
Boolean: true or false.<br><br>
Null: empty<br><br>
Array:<br><br>
It represents an ordered sequence of values.  
It is enclosed in square brackets [ ].  
Each value is separated by a comma.  
Array values can be any valid data type.  
Data is retrieved from the array by an index.  
An Array can contain an Object.<br><br>
Object:<br><br>
It is an unordered collection in name/value pairs.  
Each pair is enclosed in curly brackets { }.  
A Name/Value is separated by a colon : .  
A Name is defined in double-quotes and can contain Unicode characters.  
A Value can’t be a function.  
Values can be any data type.  
Object values can retrieved using the . operator with the name.  
We use an eval() JavaScript function to convert JSON text into a JSON object.<br><br>
Example:

{% highlight json %}
{
    "firstName": "John",
    "lastName": "Smith",
    "age": 25,
    "address": {
        "streetAddress": "21 2nd Street",
        "city": "New York",
        "state": "NY",
        "postalCode": 10021
    },
    "phoneNumber": [
        {
            "type": "home",
            "number": "212 555-1234"
        },
        {
            "type": "fax",
            "number": "646 555-4567"
        }
    ]
}
{% endhighlight %}

The above JSON object has string fields for first name and last name, a number field for age, contains an object representing the person’s address, and contains a list (an array) of phone number objects.