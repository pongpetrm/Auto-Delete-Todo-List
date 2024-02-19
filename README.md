# Auto Delete Todo List
# Answer code
```javascript
import React, { useState } from 'react';

// Initial data constant
const initialData = [
  { type: 'Fruit', name: 'Apple' },
  { type: 'Vegetable', name: 'Broccoli' },
  { type: 'Vegetable', name: 'Mushroom' },
  { type: 'Fruit', name: 'Banana' },
  { type: 'Vegetable', name: 'Tomato' },
  { type: 'Fruit', name: 'Orange' },
  { type: 'Fruit', name: 'Mango' },
  { type: 'Fruit', name: 'Pineapple' },
  { type: 'Vegetable', name: 'Cucumber' },
  { type: 'Fruit', name: 'Watermelon' },
  { type: 'Vegetable', name: 'Carrot' }
];

// Main component
export default function TodoList() {
  // State hooks
  const [todoItems, setTodoItems] = useState(initialData);
  const [fruitItems, setFruitItems] = useState([]);
  const [vegetableItems, setVegetableItems] = useState([]);

  // Move item to respective column
  const moveItemToColumn = (item) => {
    if (item.type === 'Fruit') {
        setFruitItems(prevItems => [...prevItems, item]);
    } else if (item.type === 'Vegetable') {
        setVegetableItems(prevItems => [...prevItems, item]);
    }
    setTodoItems(prevItems => prevItems.filter(todoItem => todoItem !== item));
  };

  // Move item back to the list
  const moveItemBackToList = (item) => {
    setTodoItems(prevItems => [...prevItems, item]);
    if (item.type === 'Fruit') {
        setFruitItems(prevItems => prevItems.filter(fruitItem => fruitItem !== item));
    } else if (item.type === 'Vegetable') {
        setVegetableItems(prevItems => prevItems.filter(vegetableItem => vegetableItem !== item));
    }
  };

  // Timeout function to move item back after a delay
  const timeoutInterval = (item) => {
    setTimeout(() => {
        moveItemBackToList(item);
    }, 5000);
  };

  // JSX rendering
  return (
    <div style={{ display: 'flex', justifyContent: 'center', padding: 20, height: '80vh' }}>
        {/* Todo list */}
        <div style={{ display: 'flex', flexDirection: 'column', marginRight: 30 }}>
            {todoItems.map((item, index) => (
                <button key={index}
                    style={{ minWidth: 200, height: 50, marginBottom: 10, background: 'white', border: '2px solid #eeee', fontWeight: 700, borderRadius: 8 }}
                    onClick={() => {
                        moveItemToColumn(item);
                        timeoutInterval(item);
                    }}
                >
                    {item.name}
                </button>
            ))}
        </div>

        {/* Fruits column */}
        <div style={{ height: '100%', border: '2px solid #eeee', marginRight: 10, display: 'flex', flexDirection: 'column', alignItems: 'center', overflow: 'auto' }}>
            <h3 style={{ background: '#eef2f3', padding: 5, margin: 0, minWidth: 200, textAlign: 'center', marginBottom: 10 }}>Fruits</h3>
            {fruitItems.map((item, index) => (
                <button key={index} style={{ minWidth: 200, height: 50, marginBottom: 10, background: 'white', border: '2px solid #eeee', fontWeight: 700, borderRadius: 8 }}>
                    {item.name}
                </button>
            ))}
        </div>

        {/* Vegetables column */}
        <div style={{ height: '100%', border: '2px solid #eeee', display: 'flex', flexDirection: 'column', alignItems: 'center', overflow: 'auto' }}>
            <h3 style={{ background: '#eef2f3', padding: 5, margin: 0, minWidth: 200, textAlign: 'center', marginBottom: 10 }}>Vegetables</h3>
            {vegetableItems.map((item, index) => (
                <button key={index} style={{ minWidth: 200, height: 50, marginBottom: 10, background: 'white', border: '2px solid #eeee', fontWeight: 700, borderRadius: 8 }}>
                    {item.name}
                </button>
            ))}
        </div>
    </div>
  );
}
