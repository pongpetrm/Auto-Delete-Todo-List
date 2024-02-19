# Auto Delete Todo List
# Answer code
```javascript
// This is a JavaScript function that adds two numbers
import React, { useState } from 'react';

const initialData = [
  {
      type: 'Fruit',
      name: 'Apple',
  },
  {
      type: 'Vegetable',
      name: 'Broccoli',
  },
  {
      type: 'Vegetable',
      name: 'Mushroom',
  },
  {
      type: 'Fruit',
      name: 'Banana',
  },
  {
      type: 'Vegetable',
      name: 'Tomato',
  },
  {
      type: 'Fruit',
      name: 'Orange',
  },
  {
      type: 'Fruit',
      name: 'Mango',
  },
  {
      type: 'Fruit',
      name: 'Pineapple',
  },
  {
      type: 'Vegetable',
      name: 'Cucumber',
  },
  {
      type: 'Fruit',
      name: 'Watermelon',
  },
  {
      type: 'Vegetable',
      name: 'Carrot',
  }
];

export default function TodoList() {
    const [todoItems, setTodoItems] = useState(initialData);
    const [fruitItems, setFruitItems] = useState([]);
    const [vegetableItems, setVegetableItems] = useState([]);

    const moveItemToColumn = (item) => {
        if (item.type === 'Fruit') {
            setFruitItems(current => [...current, item]);
        } else if (item.type === 'Vegetable') {
            setVegetableItems(current => [...current, item]);
        }

        setTodoItems(todoItems.filter(todoItem => todoItem !== item));
    };

    const moveItemBackToList = (item) => {
        setTodoItems(current => [...current, item]);
        if (item.type === 'Fruit') {
            setFruitItems(current => [...current].filter(fruitItem => fruitItem !== item));
        } else if (item.type === 'Vegetable') {
            setVegetableItems(current => [...current].filter(vegetableItem => vegetableItem !== item));
        }
    };

    const timeOutInterval = (item) => {
      setTimeout(() => {
        moveItemBackToList(item)
      }, 5000);
    }

    return (
        <div style={{display: 'flex', justifyContent: 'center', padding: 20, height: '80vh'}}>
            <div style={ { display: 'flex', flexDirection: 'column', marginRight: 30 } }>
                {
                  todoItems.map((item, index) => (
                    <button key={index} 
                      style={{minWidth: 200, height: 50, marginBottom: 10, background: 'white', border: '2px solid #eeee', fontWeight: 700, borderRadius: 8}}
                      onClick={() => {
                        moveItemToColumn(item); 
                        timeOutInterval(item);
                      }
                    }>
                      {item.name}
                    </button>
                  ))
                }
            </div>
            <div style={ { height: '100%', border: '2px solid #eeee', marginRight: 10, display: 'flex', flexDirection: 'column', alignItems: 'center', overflow: 'auto' } }>
                <h3 style={{background: '#eef2f3', padding: 5, margin: 0, minWidth: 200, textAlign: 'center', marginBottom: 10}}>
                  Fruits
                </h3>
                { 
                  fruitItems.map((item, index) => (
                    <button 
                      key={index}
                      style={{minWidth: 200, height: 50, marginBottom: 10, background: 'white', border: '2px solid #eeee', fontWeight: 700, borderRadius: 8}}
                    >
                      {item.name}
                    </button>
                  ))
                }
            </div>
            <div style={ { height: '100%', border: '2px solid #eeee', display: 'flex', flexDirection: 'column', alignItems: 'center', overflow: 'auto'} }>
                <h3 style={{background: '#eef2f3', padding: 5, margin: 0, minWidth: 200, textAlign: 'center', marginBottom: 10}}>
                  Vegetables
                </h3>
                { 
                  vegetableItems.map((item, index) => (
                    <button 
                      style={{minWidth: 200, height: 50, marginBottom: 10, background: 'white', border: '2px solid #eeee', fontWeight: 700, borderRadius: 8}}
                      key={index}
                    >
                        {item.name}
                    </button>
                  ))
                }
            </div>
        </div>
    );
}
