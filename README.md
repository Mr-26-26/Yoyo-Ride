# Yoyo-Ride
import React, { useState, useEffect } from 'react';

const App = () => {
  const [activeTab, setActiveTab] = useState('home');
  const [isMenuOpen, setIsMenuOpen] = useState(false);

  // Mock data for drivers and rides
  const drivers = [
    { id: 1, name: "Carlos", rating: 4.8, location: "Downtown", available: true },
    { id: 2, name: "Ana", rating: 4.9, location: "Uptown", available: false },
    { id: 3, name: "Lucas", rating: 4.7, location: "Midtown", available: true },
  ];

  const rides = [
    { id: 101, passenger: "João", start: "Central Station", end: "Airport", fare: "$15.00" },
    { id: 102, passenger: "Maria", start: "Park Ave", end: "Beach Resort", fare: "$22.00" },
    { id: 103, passenger: "Pedro", start: "North Mall", end: "University", fare: "$18.00" },
  ];

  return (
    <div className="min-h-screen bg-gradient-to-br from-yellow-400 to-yellow-500 text-gray-900">
      {/* Header */}
      <header className="bg-black text-white shadow-lg sticky top-0 z-50">
        <div className="container mx-auto px-4 py-3 flex justify-between items-center">
          <div className="flex items-center space-x-2">
            <svg className="w-8 h-8" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
              <path d="M19 12H5M5 12L9 8M5 12L9 16" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"/>
              <circle cx="18" cy="12" r="2" fill="currentColor"/>
              <circle cx="6" cy="12" r="2" fill="currentColor"/>
            </svg>
            <h1 className="text-xl font-bold">YOYO RIDE</h1>
          </div>

          {/* Desktop Nav */}
          <nav className="hidden md:flex space-x-6">
            {['home', 'services', 'drivers', 'pricing', 'contact'].map((tab) => (
              <button
                key={tab}
                onClick={() => setActiveTab(tab)}
                className={`capitalize hover:text-yellow-400 transition-colors ${activeTab === tab ? 'text-yellow-400' : ''}`}
              >
                {tab}
              </button>
            ))}
          </nav>

          {/* Mobile Menu Button */}
          <button 
            className="md:hidden text-white"
            onClick={() => setIsMenuOpen(!isMenuOpen)}
          >
            <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d={isMenuOpen ? "M6 18L18 6M6 6l12 12" : "M4 6h16M4 12h16M4 18h16"} />
            </svg>
          </button>
        </div>

        {/* Mobile Menu */}
        {isMenuOpen && (
          <div className="md:hidden bg-black bg-opacity-90 p-4 animate-fadeIn">
            <div className="flex flex-col space-y-3">
              {['home', 'services', 'drivers', 'pricing', 'contact'].map((tab) => (
                <button
                  key={tab}
                  onClick={() => {
                    setActiveTab(tab);
                    setIsMenuOpen(false);
                  }}
                  className={`capitalize hover:text-yellow-400 transition-colors ${activeTab === tab ? 'text-yellow-400' : ''}`}
                >
                  {tab}
                </button>
              ))}
            </div>
          </div>
        )}
      </header>

      {/* Hero Section */}
      {activeTab === 'home' && (
        <section className="py-16 md:py-24 px-4 container mx-auto">
          <div className="flex flex-col md:flex-row items-center">
            <div className="md:w-1/2 mb-10 md:mb-0">
              <h2 className="text-3xl md:text-5xl font-bold leading-tight mb-6">
                Chegue onde quiser, rápido e seguro!
              </h2>
              <p className="text-lg md:text-xl mb-8 opacity-90">
                O serviço de transporte mais confiável da cidade. Conectamos você aos melhores motoristas com tecnologia avançada.
              </p>
              <div className="flex flex-wrap gap-4">
                <button className="bg-black text-yellow-400 px-6 py-3 rounded-full font-semibold hover:bg-gray-800 transition-colors transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-yellow-400">
                  Baixar o App
                </button>
                <button className="border-2 border-black text-black bg-transparent px-6 py-3 rounded-full font-semibold hover:bg-black hover:text-yellow-400 transition-colors transform hover:scale-105 focus:outline-none">
                  Cadastre-se como Motorista
                </button>
              </div>
            </div>
            <div className="md:w-1/2 flex justify-center">
              <img src="https://placehold.co/600x400/000000/FFFFFF?text=YOYO+RIDE" alt="YOYO RIDE App Preview" className="rounded-lg shadow-2xl max-w-full h-auto transform rotate-2 hover:rotate-0 transition-transform duration-500" />
            </div>
          </div>
        </section>
      )}

      {/* Services Section */}
      {activeTab === 'services' && (
        <section id="services" className="py-16 px-4 container mx-auto">
          <h2 className="text-3xl md:text-4xl font-bold text-center mb-12">Nossos Serviços</h2>
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8">
            {[
              {
                title: "Viagem por Taxímetro",
                description: "Taxímetro digital que calcula o valor da viagem em tempo real baseado no tempo e distância percorrida.",
                icon: (
                  <svg className="w-12 h-12 mb-4 text-black" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2">
                    <circle cx="12" cy="12" r="10" />
                    <path d="M12 6v6M12 12l4 4" />
                  </svg>
                )
              },
              {
                title: "Viagem por Localização",
                description: "Escolha seu destino usando Google Maps integrado. Receba uma estimativa do custo antes de iniciar a corrida.",
                icon: (
                  <svg className="w-12 h-12 mb-4 text-black" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2">
                    <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5" />
                  </svg>
                )
              },
              {
                title: "Pagamento Integrado",
                description: "Várias opções de pagamento incluindo cartões, PIX (Brasil), dinheiro e carteira digital pré-paga.",
                icon: (
                  <svg className="w-12 h-12 mb-4 text-black" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2">
                    <rect x="1" y="4" width="22" height="16" rx="2" />
                    <path d="M1 10h22" />
                  </svg>
                )
              }
            ].map((service, index) => (
              <div key={index} className="bg-white p-6 rounded-lg shadow-lg hover:shadow-xl transition-shadow transform hover:-translate-y-2 transition-transform">
                <div className="flex flex-col items-center text-center">
                  {service.icon}
                  <h3 className="text-xl font-semibold mb-2">{service.title}</h3>
                  <p className="opacity-80">{service.description}</p>
                </div>
              </div>
            ))}
          </div>
        </section>
      )}

      {/* Drivers Section */}
      {activeTab === 'drivers' && (
        <section id="drivers" className="py-16 px-4 container mx-auto">
          <h2 className="text-3xl md:text-4xl font-bold text-center mb-12">Nossos Motoristas</h2>
          
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            {drivers.map(driver => (
              <div key={driver.id} className="bg-white rounded-lg overflow-hidden shadow-lg hover:shadow-xl transition-shadow">
                <div className="relative h-48 overflow-hidden">
                  <img 
                    src={`https://placehold.co/600x400/000000/FFFFFF?text=${encodeURIComponent(driver.name)}`} 
                    alt={driver.name} 
                    className="w-full h-full object-cover transform hover:scale-110 transition-transform duration-500"
                  />
                  <div className={`absolute top-2 right-2 px-2 py-1 rounded-full text-xs font-bold ${
                    driver.available ? 'bg-green-500 text-white' : 'bg-red-500 text-white'
                  }`}>
                    {driver.available ? 'Disponível' : 'Indisponível'}
                  </div>
                </div>
                <div className="p-6">
                  <div className="flex justify-between items-start">
                    <h3 className="text-xl font-bold">{driver.name}</h3>
                    <div className="flex items-center">
                      <svg className="w-5 h-5 text-yellow-400 mr-1" fill="currentColor" viewBox="0 0 20 20">
                        <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                      </svg>
                      <span>{driver.rating}</span>
                    </div>
                  </div>
                  <p className="text-gray-600 mt-2">Localização: {driver.location}</p>
                  <div className="mt-4 pt-4 border-t">
                    <button className={`w-full py-2 rounded-full font-medium ${
                      driver.available 
                        ? 'bg-yellow-400 hover:bg-yellow-500 text-black' 
                        : 'bg-gray-300 text-gray-500 cursor-not-allowed'
                    }`}>
                      Chamar Motorista
                    </button>
                  </div>
                </div>
              </div>
            ))}
          </div>

          <div className="mt-16 text-center">
            <h3 className="text-2xl font-bold mb-4">Quer ser um motorista YOYO RIDE?</h3>
            <p className="max-w-2xl mx-auto mb-6 text-gray-700">
              Junte-se à nossa rede de motoristas profissionais e aumente seus ganhos. Oferecemos ferramentas modernas, suporte técnico e uma comunidade crescente de usuários.
            </p>
            <button className="bg-black text-yellow-400 px-8 py-3 rounded-full font-semibold hover:bg-gray-800 transition-colors">
              Cadastre-se Agora
            </button>
          </div>
        </section>
      )}

      {/* Pricing Section */}
      {activeTab === 'pricing' && (
        <section id="pricing" className="py-16 px-4 container mx-auto">
          <h2 className="text-3xl md:text-4xl font-bold text-center mb-12">Planos e Preços</h2>
          
          <div className="grid grid-cols-1 md:grid-cols-3 gap-8 max-w-5xl mx-auto">
            {[
              {
                name: "Básico",
                price: "$0",
                features: ["Chamadas por taxímetro", "Pagamento em dinheiro", "Avaliação básica"],
                cta: "Começar agora",
                popular: false
              },
              {
                name: "Premium",
                price: "$9.99/mês",
                features: ["Descontos exclusivos", "Prioridade nas chamadas", "Suporte 24/7", "Carteira digital"],
                cta: "Assinar Premium",
                popular: true
              },
              {
                name: "Motorista Pro",
                price: "$19.99/mês",
                features: ["Visualização de passageiros próximos", "Histórico detalhado", "Suporte técnico especializado", "Análise de rendimento"],
                cta: "Cadastre-se como Pro",
                popular: false
              }
            ].map((plan, index) => (
              <div key={index} className={`bg-white rounded-lg overflow-hidden shadow-lg transition-all ${
                plan.popular ? 'transform scale-105 ring-2 ring-yellow-400' : ''
              }`}>
                <div className="p-6">
                  <h3 className="text-xl font-bold text-center mb-2">{plan.name}</h3>
                  <p className="text-3xl font-bold text-center mb-4">{plan.price}<span className="text-sm font-normal text-gray-500">/mês</span></p>
                  <ul className="mb-6">
                    {plan.features.map((feature, i) => (
                      <li key={i} className="flex items-center mb-2">
                        <svg className="w-5 h-5 text-green-500 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M5 13l4 4L19 7" />
                        </svg>
                        {feature}
                      </li>
                    ))}
                  </ul>
                  <button className={`w-full py-2 rounded-full font-medium ${
                    plan.popular 
                      ? 'bg-yellow-400 hover:bg-yellow-500 text-black' 
                      : 'bg-black hover:bg-gray-800 text-white'
                  }`}>
                    {plan.cta}
                  </button>
                </div>
              </div>
            ))}
          </div>

          <div className="mt-16 bg-white p-8 rounded-lg shadow-lg max-w-4xl mx-auto">
            <h3 className="text-2xl font-bold mb-4 text-center">Histórico de Viagens</h3>
            <div className="overflow-x-auto">
              <table className="w-full table-auto">
                <thead>
                  <tr className="bg-gray-100 text-left">
                    <th className="px-4 py-2">ID</th>
                    <th className="px-4 py-2">Passageiro</th>
                    <th className="px-4 py-2">Origem</th>
                    <th className="px-4 py-2">Destino</th>
                    <th className="px-4 py-2">Valor</th>
                  </tr>
                </thead>
                <tbody>
                  {rides.map(ride => (
                    <tr key={ride.id} className="hover:bg-gray-50 transition-colors">
                      <td className="px-4 py-2">{ride.id}</td>
                      <td className="px-4 py-2">{ride.passenger}</td>
                      <td className="px-4 py-2">{ride.start}</td>
                      <td className="px-4 py-2">{ride.end}</td>
                      <td className="px-4 py-2 font-medium">{ride.fare}</td>
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
        </section>
      )}

      {/* Contact Section */}
      {activeTab === 'contact' && (
        <section id="contact" className="py-16 px-4 container mx-auto">
          <h2 className="text-3xl md:text-4xl font-bold text-center mb-12">Entre em Contato</h2>
          
          <div className="grid grid-cols-1 md:grid-cols-2 gap-12 max-w-5xl mx-auto">
            <div>
              <h3 className="text-xl font-bold mb-4">Informações de Contato</h3>
              <div className="space-y-4">
                <div className="flex items-start">
                  <svg className="w-6 h-6 mr-3 mt-1 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                  </svg>
                  <div>
                    <h4 className="font-semibold">Endereço</h4>
                    <p>Rua Principal, 123 - Centro<br />São Paulo, SP - Brasil</p>
                  </div>
                </div>
                
                <div className="flex items-start">
                  <svg className="w-6 h-6 mr-3 mt-1 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                  </svg>
                  <div>
                    <h4 className="font-semibold">Telefone</h4>
                    <p>+55 (11) 98765-4321</p>
                  </div>
                </div>
                
                <div className="flex items-start">
                  <svg className="w-6 h-6 mr-3 mt-1 text-black" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                  </svg>
                  <div>
                    <h4 className="font-semibold">Email</h4>
                    <p>contato@yoyoride.com.br</p>
                  </div>
                </div>
              </div>
            </div>
            
            <div>
              <h3 className="text-xl font-bold mb-4">Formulário de Contato</h3>
              <form className="space-y-4">
                <div>
                  <label htmlFor="name" className="block mb-1 font-medium">Nome</label>
                  <input type="text" id="name" className="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-400" placeholder="Seu nome" />
                </div>
                <div>
                  <label htmlFor="email" className="block mb-1 font-medium">Email</label>
                  <input type="email" id="email" className="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-400" placeholder="seu@email.com" />
                </div>
                <div>
                  <label htmlFor="message" className="block mb-1 font-medium">Mensagem</label>
                  <textarea id="message" rows="5" className="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-400" placeholder="Sua mensagem..."></textarea>
                </div>
                <button type="submit" className="bg-black text-yellow-400 px-6 py-2 rounded-full font-semibold hover:bg-gray-800 transition-colors">
                  Enviar Mensagem
                </button>
              </form>
            </div>
          </div>
        </section>
      )}

      {/* Footer */}
      <footer className="bg-black text-white py-12 px-4">
        <div className="container mx-auto">
          <div className="grid grid-cols-1 md:grid-cols-4 gap-8">
            <div>
              <div className="flex items-center space-x-2 mb-4">
                <svg className="w-6 h-6" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path d="M19 12H5M5 12L9 8M5 12L9 16" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round"/>
                  <circle cx="18" cy="12" r="2" fill="currentColor"/>
                  <circle cx="6" cy="12" r="2" fill="currentColor"/>
                </svg>
                <h3 className="text-xl font-bold">YOYO RIDE</h3>
              </div>
              <p className="opacity-80">Conectando passageiros aos melhores motoristas com tecnologia avançada e segurança.</p>
            </div>
            
            <div>
              <h4 className="text-lg font-bold mb-4">Empresa</h4>
              <ul className="space-y-2">
                <li><button className="opacity-80 hover:opacity-100 transition-opacity" onClick={() => setActiveTab('home')}>Home</button></li>
                <li><button className="opacity-80 hover:opacity-100 transition-opacity" onClick={() => setActiveTab('about')}>Sobre Nós</button></li>
         
