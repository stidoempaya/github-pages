import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { ShoppingCart, Music } from "lucide-react";

const products = [
  { id: 1, name: "Produit 1", price: "19.99€", image: "/product1.jpg" },
  { id: 2, name: "Produit 2", price: "29.99€", image: "/product2.jpg" },
  { id: 3, name: "Produit 3", price: "39.99€", image: "/product3.jpg" },
];

export default function Home() {
  const [cart, setCart] = useState([]);
  const [audio] = useState(new Audio("/music.mp3"));

  const addToCart = (product) => {
    setCart([...cart, product]);
  };

  const playMusic = () => {
    audio.play();
  };

  return (
    <div className="p-10">
      <div className="relative mb-10">
        <img 
          src="/stido.jpg" 
          alt="Stido Empaya" 
          className="w-full h-64 object-cover rounded-lg shadow-lg"
        />
        <h1 className="absolute inset-0 flex items-center justify-center text-white text-4xl font-bold bg-black bg-opacity-50 rounded-lg">
          Stido Empaya
        </h1>
      </div>
      <Button className="mb-6 flex items-center gap-2" onClick={playMusic}>
        <Music size={18} /> Jouer Musique
      </Button>
      <div className="mb-6 p-4 bg-gray-100 rounded-lg shadow-md">
        <h2 className="text-2xl font-semibold mb-4">Panier</h2>
        {cart.length === 0 ? (
          <p className="text-gray-600">Votre panier est vide.</p>
        ) : (
          <ul>
            {cart.map((item, index) => (
              <li key={index} className="flex justify-between py-2 border-b">
                {item.name} - {item.price}
              </li>
            ))}
          </ul>
        )}
      </div>
      <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
        {products.map((product) => (
          <Card key={product.id} className="p-4 rounded-2xl shadow-lg">
            <img
              src={product.image}
              alt={product.name}
              className="w-full h-40 object-cover rounded-lg"
            />
            <CardContent className="mt-4">
              <h2 className="text-xl font-semibold">{product.name}</h2>
              <p className="text-lg text-gray-600">{product.price}</p>
              <Button 
                className="mt-4 w-full flex items-center gap-2" 
                onClick={() => addToCart(product)}
              >
                <ShoppingCart size={18} /> Ajouter au panier
              </Button>
            </CardContent>
          </Card>
        ))}
      </div>
    </div>
  );
}

