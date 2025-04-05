npm create vite@latest my-tailwind-app --template react
cd my-tailwind-app
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init

/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}

@tailwind base;
@tailwind components;
@tailwind utilities;

import { useState } from 'react'
import Header from './components/Header'
import Footer from './components/Footer'
import Navbar from './components/Navbar'

function App() {
  const [activeSection, setActiveSection] = useState('home')

  return (
    <div className="min-h-screen flex flex-col bg-gray-50">
      <Header />
      <Navbar activeSection={activeSection} setActiveSection={setActiveSection} />
      
      <main className="flex-grow container mx-auto px-4 py-8">
        {/* Contenido dinámico */}
      </main>
      
      <Footer />
    </div>
  )
}

export default App



export default function Header() {
  return (
    <header className="bg-blue-600 text-white shadow-md">
      <div className="container mx-auto px-4 py-6">
        <h1 className="text-3xl font-bold">Mi App con Tailwind</h1>
        <p className="text-blue-100 mt-2">Un proyecto moderno con React y Tailwind CSS</p>
      </div>
    </header>
  )
}

export default function Navbar({ activeSection, setActiveSection }) {
  const links = [
    { id: 'home', label: 'Inicio' },
    { id: 'products', label: 'Productos' },
    { id: 'about', label: 'Nosotros' },
    { id: 'contact', label: 'Contacto' },
  ]

  return (
    <nav className="bg-white shadow-sm">
      <div className="container mx-auto px-4">
        <ul className="flex space-x-1">
          {links.map((link) => (
            <li key={link.id}>
              <button
                onClick={() => setActiveSection(link.id)}
                className={`px-4 py-3 text-lg font-medium transition-colors duration-200 ${
                  activeSection === link.id
                    ? 'text-blue-600 border-b-2 border-blue-600'
                    : 'text-gray-600 hover:text-blue-500'
                }`}
              >
                {link.label}
              </button>
            </li>
          ))}
        </ul>
      </div>
    </nav>
  )
}

export default function Footer() {
  return (
    <footer className="bg-gray-800 text-white py-8">
      <div className="container mx-auto px-4">
        <div className="flex flex-col md:flex-row justify-between items-center">
          <div className="mb-4 md:mb-0">
            <h2 className="text-xl font-bold">Mi App</h2>
            <p className="text-gray-400 mt-1">© 2023 Todos los derechos reservados</p>
          </div>
          <div className="flex space-x-4">
            <a href="#" className="hover:text-blue-400 transition-colors">Términos</a>
            <a href="#" className="hover:text-blue-400 transition-colors">Privacidad</a>
            <a href="#" className="hover:text-blue-400 transition-colors">Contacto</a>
          </div>
        </div>
      </div>
    </footer>
  )
}

export default function Card({ item }) {
  return (
    <div className="bg-white rounded-xl shadow-lg overflow-hidden transition-transform duration-300 hover:scale-105 hover:shadow-xl">
      <div className="h-48 bg-gray-200 overflow-hidden">
        <img 
          src={item.image} 
          alt={item.title}
          className="w-full h-full object-cover"
        />
      </div>
      <div className="p-6">
        <h3 className="text-xl font-semibold text-gray-800 mb-2">{item.title}</h3>
        <p className="text-gray-600 mb-4">{item.description}</p>
        <div className="flex justify-between items-center">
          <span className="text-lg font-bold text-blue-600">${item.price}</span>
          <button className="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
            Comprar
          </button>
        </div>
      </div>
    </div>
  )
}

import { useState } from 'react'
import Header from './components/Header'
import Footer from './components/Footer'
import Navbar from './components/Navbar'
import Card from './components/Card'

function App() {
  const [activeSection, setActiveSection] = useState('home')

  // Datos de ejemplo para las cards
  const products = [
    {
      id: 1,
      title: 'Producto 1',
      description: 'Descripción del producto 1 con características destacadas.',
      price: 29.99,
      image: 'https://via.placeholder.com/300'
    },
    {
      id: 2,
      title: 'Producto 2',
      description: 'Descripción del producto 2 con características destacadas.',
      price: 39.99,
      image: 'https://via.placeholder.com/300'
    },
    {
      id: 3,
      title: 'Producto 3',
      description: 'Descripción del producto 3 con características destacadas.',
      price: 49.99,
      image: 'https://via.placeholder.com/300'
    },
    {
      id: 4,
      title: 'Producto 4',
      description: 'Descripción del producto 4 con características destacadas.',
      price: 59.99,
      image: 'https://via.placeholder.com/300'
    },
  ]

  return (
    <div className="min-h-screen flex flex-col bg-gray-50">
      <Header />
      <Navbar activeSection={activeSection} setActiveSection={setActiveSection} />
      
      <main className="flex-grow container mx-auto px-4 py-8">
        {activeSection === 'products' && (
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
            {products.map((product) => (
              <Card key={product.id} item={product} />
            ))}
          </div>
        )}
        
        {activeSection === 'home' && (
          <div className="text-center py-12">
            <h2 className="text-4xl font-bold text-gray-800 mb-6">Bienvenido a nuestra tienda</h2>
            <p className="text-xl text-gray-600 max-w-2xl mx-auto">
              Explora nuestros productos de alta calidad seleccionados especialmente para ti.
            </p>
          </div>
        )}
      </main>
      
      <Footer />
    </div>
  )
}

export default App

