# Introducción a React

## ¿Qué es React?
React es una biblioteca JavaScript que permite crear interfaces de usuario (UI) usando componentes reutilizables.
```
const elemento = React.createElement("h1", {}, "Hola Utilapis!");

ReactDOM.render(elemento, document.getElementById('root'));
```

## ¿Cómo funciona React?
React crea un DOM virtual en memoria en lugar de manupular directamente el DOM del navegador. React solo actualiza lo que necesita ser actualizado en el DOM.

```
function tick() {
    const elemento = 
        React.createElement("div", null, 
            React.createElement("h1", null, "La hora es:"),
            React.createElement("h1", null, `${new Date().toISOString()}`)
        );
    ReactDOM.render(elemento, document.getElementById('root'));
}
setInterval(tick, 1000);
```

## JSX - JavaScript XML
JSX permite crear componentes de React usando una sintaxis parecida a HTML. JSX transforma los tags a elementos de React.
 
```
const elemento = <div>Hola Utilapis!</div>;

ReactDOM.render(elemento, document.getElementById('root'));
```

## Componentes
```
// class component
class Persona extends React.Component {
    render() {
        return <h2>Componente Persona</h2>;
    }
}

// function component
function Persona() {
    return <h2>Componente Persona</h2>;
}

ReactDOM.render(<Persona />, document.getElementById('root'));
```

## Props
Son argumentos que se pasan a los componentes.

```
function Persona(props) {
    return <h2>{props.name} - {props.age}</h2>;
}

ReactDOM.render(<Persona name="Juan" age="23" />, document.getElementById('root'));
```

# Hooks (useState, useEffect)
Permite que los componentes basados en funciones puedan usar el estado y la funcionalidad de React.
```
function Persona({name, age, color}) {
  return <h2 style={{background: color}}>{name} - {age}</h2>;
}

function ListaDePersonas() {
const [personas, setPersonas] = React.useState([]);

async function fetchPersonas(results) {
    const response = await fetch(`https://randomuser.me/api/?results=${results}`);
    const data = await response.json();
    
    return data.results.map(persona => {
        const color = '#' + Math.floor(Math.random() * 16777215).toString(16);
        return ({ id: Math.random(), name: persona.name.first, age: persona.dob.age, color: color})
    });
}

async function addPersona() {
    const newPersonas = await fetchPersonas(1);
    setPersonas([...personas, newPersonas[0]]);
}

React.useEffect(async() => {
    const p = await fetchPersonas(10);
    setPersonas(p);
}, []);

return (
    <div>
        {personas?.map(p => <Persona key={p.id} {...p} />)}
        <button onClick={() => addPersona()}>Agregar</button>
    </div>
    );
}

ReactDOM.render(<ListaDePersonas />, document.getElementById('root'));
```

## Crea tu primera aplicacion de react
```
npx create-react-app my-app
cd my-app
npm start
```
