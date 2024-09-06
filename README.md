{
    "configurations": [

    ]
}import React,
{ useState, useEffect
} from 'react';

const Game = () => {
  const [points, setPoints] = useState(0);
  const [items, setItems] = useState([
    { id: 1, name: 'Item 1', price: 100, owned: 0 },
    { id: 2, name: 'Item 2', price: 200, owned: 0 },
    { id: 3, name: 'Item 3', price: 400, owned: 0 },
    { id: 4, name: 'Item 4', price: 800, owned: 0 },
    { id: 5, name: 'Item 5', price: 1600, owned: 0 },
    { id: 6, name: 'Item 6', price: 3200, owned: 0 },
    { id: 7, name: 'Item 7', price: 6400, owned: 0 },
    { id: 8, name: 'Item 8', price: 12800, owned: 0 },
    { id: 9, name: 'Item 9', price: 25600, owned: 0 },
    { id: 10, name: 'Item 10', price: 51200, owned: 0 },
  ]);

  const handleClick = () => {
    setPoints(prevPoints => prevPoints + 1);
  };

  const buyItem = (id: number) => {
    const item = items.find(item => item.id === id);
    if (item && points >= item.price) {
      setPoints(prevPoints => prevPoints - item.price);
      setItems(prevItems =>
        prevItems.map(i =>
          i.id === id ? { ...i, owned: i.owned + 1 } : i
        )
      );
    }
  };

  return (
    <div style={{ display: 'flex' }}>
      <div style={{ flex: 1 }}>
        <h2>Shop</h2>
        {items.map(item => (
          <div key={item.id}>
            <button onClick={() => buyItem(item.id)} disabled={points < item.price}>
              Buy {item.name} - Price: {item.price} - Owned: {item.owned}
            </button>
          </div>
        ))}
      </div>
      <div style={{ flex: 2, textAlign: 'center' }}>
        <h1>Points: {points}</h1>
        <button onClick={handleClick} style={{ fontSize: '24px', padding: '20px' }}>
          Click me!
        </button>
      </div>
    </div>
  );
};
