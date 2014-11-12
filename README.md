#xml

Just another Node XML library created as an atempt to make XML serialization as simple and straight forward as JSON serialization

Requires Nodejs http://nodejs.org


##Installing

__From the Command Line__<br />
npm install git+https://github.com/bdunford/xml.git

__package.json as a dependency__<br />
add "helpers": "git+https://github.com/bdunford/xml.git" to dependencies <br />
```json
{
    "name": "your-app",
    "version": "0.0.0",
    "private": true,
    "description": "just another node app",
    "dependencies": {
        "helpers": "git+https://github.com/bdunford/xml.git"
    }
}

```
__Raw__<br />
```git clone https://github.com/bdunford/xml```<br />
Be sure to run npm install from with in the __xml__ directory

##Usage

require xml in your javascript.
```javascript
var xml = require('XML');
```

__stringify__ will serialize an object to an xml string.  Root and child can optionally be passed to specify root and child elements if not part of the object being serialized.
<br />

```javascript
var o = {
    customers: {
        customer: [
            {id: 1, name: "tim"},
            {id: 1, name: "tom"},
            {id: 1, name: "tie"}
        ]
    }
};

xml.stringify(o); /* will return
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<customers>
    <customer><id>1</id><name>tim</name></customer>
    <customer><id>2</id><name>tom</name></customer>
    <customer><id>3</id><name>tie</name></customer>
</customers>'
*/
```

```javascript
var ar = [
    {id: 1, name: "tim"},
    {id: 1, name: "tom"},
    {id: 1, name: "tie"}
];

xml.stringify(ar,'customers'); /* will return
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<customers>
    <customer><id>1</id><name>tim</name></customer>
    <customer><id>2</id><name>tom</name></customer>
    <customer><id>3</id><name>tie</name></customer>
</customers>'
*/
xml.stringify(ar,'root','child'); /* will return
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<root>
    <child><id>1</id><name>tim</name></child>
    <child><id>2</id><name>tom</name></child>
    <child><id>3</id><name>tie</name></child>
</root>'
*/
```

__parse__ will attempt to parse an xml string to object. Parse will also strip root and child tags if stripRoots = true is passed
<br />

```javascript
var xmlString = '
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<customers>
    <customer><id>1</id><name>tim</name></customer>
    <customer><id>2</id><name>tom</name></customer>
    <customer><id>3</id><name>tie</name></customer>
</customers>'

xml.parse(xmlString); /* will return
{
    customers: {
        customer: [
            {id: 1, name: "tim"},
            {id: 1, name: "tom"},
            {id: 1, name: "tie"}
        ]
    }
}
*/
xml.parse(xmlString, true); /* will return
[
    {id: 1, name: "tim"},
    {id: 1, name: "tom"},
    {id: 1, name: "tie"}
]
*/
```
