# Mutating Data

## How to use useEffect and useCallBack Hooks

**useCallback(fn, [dependencies])**: is a react hook that lets your cache a function definition between re-renders.

```js
import {useState, useEffect, useCallback} from 'react';

export default function whatEverYouWant(){
    const [list, setList] = useState([]);

    // function is caching
    const request = useCallback(() => {
        fetch('API URL')
            .then((response) => response.json())
            .then((data) => {
                setList(data)
            });
    }, []);

    // Trigger request
    useEffect( () => {
        request();

        console.log("Testing number of running");

    }, [request]);

    return (
        <>
            <ul>
                {
                    list.map((item) =>{
                        <li key={item.id}>{item.name}</li>
                    })
                }
            </ul>
        </>
    );
}
```

## Deleting Records

Using parent component function to delete or filter data from child.

```js
import {useState} from 'react';

// Child
const Modality = ({modality, fnDelete}) => {
    return (
        <>
            <div className="card">
                <h4>{modality.title}</h4>
                <p>{modality.description}</p>
                <button className="btn btn-xs btn-danger" onClick={ fnDelete(modality.id) }>Delete!</button>
            </div>
        </>
    );
};

// Parent
const Modalities = () => {
    const [modalities, setModalities] = useState([]);

    const fnDelete = (item) => {
        setModalities(modalities.filter(function(item_v2){
            return item.id != item_v2.id;
        }));
    }

    return (
        <>
            <div className="content">
                {
                    modalities.map(function(item){
                        return <Modality key={item.id} modality={item} fnDelete={fnDelete} />
                    });
                }
            </div>
        </>
    );
};

export {Modalities, Modality};
```

## Searching with a filtered array

Logic to search in array from a parent list

```js
import {useState} from 'react';

export default function Search({q, onChangeQ}){
    return (
        <>
            <label htmlFor="search">Search</label>
            <input type="search" id="search" name="search" value={q} onChange={(e) => onChangeQ(e.target.value)}>
        </>
    );
};

```

```js
import {useState} from 'react';
import Search from './Search.js';

export default function List(){
    const [list, setList] = useState([]);
    const [q, setQ] = useState("");

    // Filtered Data
    const listFiltered = list.filter( (item) => {
        return list.name.toLowerCase().includes(q);
    } );

    return (
        <>
            <Search q={q} onChangeQ={ (txt) => setQ(txt) } />
            
            // List
            {listFiltered.map()}
        </>
    );
}
```