# Getting Started

components: are the directory that use for save components.

## Importing JSON data as a variable

For save json or another data you must create a sources folder within src directory.

```js
import json_data from '/sources/data.json';

console.log(json_data.name);
```

## The useState Hook and conditional classes

**Inline if with logical && operator**
You may embed expressions in JSX by wrapping them in curly braces. This include the JavaScript logical && operator. It can be handly for conditionally including an element.

```js
import {useState} from 'react';

const whatever = () => {
    const [name, setName] = useState(null);

    return (
        <>
            <button onClick={ () => setName("John") }>View Name</button>
            { name != null && <NameParagraph value={name} /> }

            // Infile If-Else with conditional operation.
            { name == "John" ? <JohnGreeting /> : <NormalGreeting />}        
        </>
    );


}
```