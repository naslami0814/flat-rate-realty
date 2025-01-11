import React, { useState, useEffect } from 'react';
import { Motion, spring } from 'react-motion';
import { ArrowRight, Check, Home, Upload, DollarSign, FileText, ChevronDown } from 'lucide-react';

const App = () => {
  const [isVisible, setIsVisible] = useState(false);
  const [activeSection, setActiveSection] = useState('hero');
  const [showWizard, setShowWizard] = useState(false);

  useEffect(() => {
    setIsVisible(true);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const handleScroll = () => {
    const sections = document.querySelectorAll('section');
    sections.forEach(section => {
      const rect = section.getBoundingClientRect();
      if (rect.top >= 0 && rect.top <= window.innerHeight / 2) {
        setActiveSection(section.id);
      }
    });
  };

  return (
    <div className="min-h-screen bg-white">
      {/* Navigation */}
      <nav className="fixed w-full bg-white/80 backdrop-blur-md z-50 shadow-sm">
        <div className="max-w-7xl mx-auto px-6">
          <div className="flex items-center justify-between h-20">
            <div className="text-2xl font-bold text-blue-600">SimpliClose</div>
            <div className="hidden md:flex items-center space-x-8">
              <a href="#services" className="text-gray-600 hover:text-blue-600 transition-colors">Services</a>
              <a href="#process" className="text-gray-600 hover:text-blue-600 transition-colors">Process</a>
              <a href="#pricing" className="text-gray-600 hover:text-blue-600 transition-colors">Pricing</a>
              <button 
                onClick={() => setShowWizard(true)}
                className="bg-blue-600 text-white px-6 py-2 rounded-full hover:bg-blue-700 transition-all hover:scale-105"
              >
                Get Started
              </button>
            </div>
          </div>
        </div>
      </nav>

      {/* Hero Section */}
      <section id="hero" className="pt-32 pb-20 bg-gradient-to-b from-blue-50 to-white">
        <div className="max-w-7xl mx-auto px-6">
          <div className="grid md:grid-cols-2 gap-12 items-center">
            <div className="space-y-8">
              <h1 className="text-5xl md:text-7xl font-bold leading-tight animate-fade-in">
                Simplify Your Real Estate Journey
              </h1>
              <p className="text-xl text-gray-600 animate-fade-in-delay">
                Professional assistance for buyers and sellers with transparent pricing and seamless process.
              </p>
              <div className="flex space-x-4 animate-fade-in-delay-2">
                <button 
                  onClick={() => setShowWizard(true)}
                  className="bg-blue-600 text-white px-8 py-4 rounded-full hover:bg-blue-700 transition-all hover:scale-105"
                >
                  Get Started
                </button>
                <a href="#process" className="border border-gray-300 px-8 py-4 rounded-full hover:border-blue-600 transition-all hover:scale-105">
                  Learn More
                </a>
              </div>
            </div>
            <div className="hidden md:block animate-float">
              <div className="w-full aspect-square relative">
                {/* Insert the house SVG here */}
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Services Section */}
      <section id="services" className="py-20">
        <div className="max-w-7xl mx-auto px-6">
          <h2 className="text-4xl md:text-5xl font-bold text-center mb-16">Our Services</h2>
          <div className="grid md:grid-cols-3 gap-8">
            {[
              {
                icon: Home,
                title: "Property Listing",
                description: "Professional listing services with maximum exposure"
              },
              {
                icon: FileText,
                title: "Document Handling",
                description: "Comprehensive document preparation and management"
              },
              {
                icon: DollarSign,
                title: "Transaction Support",
                description: "End-to-end transaction coordination and support"
              }
            ].map((service, index) => (
              <div 
                key={index}
                className="p-8 rounded-2xl bg-white shadow-lg hover:shadow-xl transition-all hover:-translate-y-1"
              >
                <service.icon className="w-12 h-12 text-blue-600 mb-6" />
                <h3 className="text-2xl font-bold mb-4">{service.title}</h3>
                <p className="text-gray-600">{service.description}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Process Section */}
      <section id="process" className="py-20 bg-gray-50">
        <div className="max-w-7xl mx-auto px-6">
          <h2 className="text-4xl md:text-5xl font-bold text-center mb-16">How It Works</h2>
          <div className="relative">
            {/* Insert the process SVG here */}
            <div className="grid md:grid-cols-4 gap-8 mt-16">
              {[
                "Choose your package",
                "Upload documents",
                "Review details",
                "Complete transaction"
              ].map((step, index) => (
                <div key={index} className="text-center">
                  <div className="text-xl font-bold mb-2">Step {index + 1}</div>
                  <p className="text-gray-600">{step}</p>
                </div>
              ))}
            </div>
          </div>
        </div>
      </section>

      {/* Pricing Section */}
      <section id="pricing" className="py-20">
        <div className="max-w-7xl mx-auto px-6">
          <h2 className="text-4xl md:text-5xl font-bold text-center mb-16">Simple Pricing</h2>
          <div className="grid md:grid-cols-2 gap-8">
            {[
              {
                title: "Standard Package",
                price: "$3,900",
                description: "For homes under $500,000",
                features: [
                  "Full transaction support",
                  "Document preparation",
                  "Closing coordination",
                  "Digital paperwork"
                ]
              },
              {
                title: "Premium Package",
                price: "Custom",
                description: "For homes over $500,000",
                features: [
                  "Everything in Standard",
                  "Priority support",
                  "Custom marketing plan",
                  "Dedicated agent"
                ]
              }
            ].map((pkg, index) => (
              <div 
                key={index}
                className="p-8 rounded-2xl bg-white shadow-lg hover:shadow-xl transition-all hover:-translate-y-1"
              >
                <h3 className="text-2xl font-bold mb-2">{pkg.title}</h3>
                <div className="text-4xl font-bold text-blue-600 mb-2">{pkg.price}</div>
                <p className="text-gray-600 mb-6">{pkg.description}</p>
                <ul className="space-y-4">
                  {pkg.features.map((feature, i) => (
                    <li key={i} className="flex items-center">
                      <Check className="w-5 h-5 text-blue-600 mr-3" />
                      <span>{feature}</span>
                    </li>
                  ))}
                </ul>
                <button 
                  onClick={() => setShowWizard(true)}
                  className="w-full mt-8 bg-blue-600 text-white px-6 py-3 rounded-full hover:bg-blue-700 transition-all hover:scale-105"
                >
                  Get Started
                </button>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Footer */}
      <footer className="bg-gray-900 text-white py-12">
        <div className="max-w-7xl mx-auto px-6">
          <div className="grid md:grid-cols-4 gap-8">
            <div>
              <div className="text-2xl font-bold mb-4">SimpliClose</div>
              <p className="text-gray-400">Making real estate transactions simple and transparent.</p>
            </div>
            {[
              {
                title: "Services",
                links: ["Buyer Services", "Seller Services", "Pricing"]
              },
              {
                title: "Company",
                links: ["About Us", "Contact", "Careers"]
              },
              {
                title: "Legal",
                links: ["Privacy Policy", "Terms of Service"]
              }
            ].map((section, index) => (
              <div key={index}>
                <h4 className="font-bold mb-4">{section.title}</h4>
                <ul className="space-y-2">
                  {section.links.map((link, i) => (
                    <li key={i}>
                      <a href="#" className="text-gray-400 hover:text-white transition-colors">
                        {link}
                      </a>
                    </li>
                  ))}
                </ul>
              </div>
            ))}
          </div>
        </div>
      </footer>

      {/* CSS Animations */}
      <style jsx>{`
        @keyframes fadeIn {
          from { opacity: 0; transform: translateY(20px); }
          to { opacity: 1; transform: translateY(0); }
        }
        
        @keyframes float {
          0%, 100% { transform: translateY(0px); }
          50% { transform: translateY(-20px); }
        }

        .animate-fade-in {
          animation: fadeIn 1s ease-out forwards;
        }

        .animate-fade-in-delay {
          animation: fadeIn 1s ease-out 0.3s forwards;
          opacity: 0;
        }

        .animate-fade-in-delay-2 {
          animation: fadeIn 1s ease-out 0.6s forwards;
          opacity: 0;
        }

        .animate-float {
          animation: float 6s ease-in-out infinite;
        }
      `}</style>
    </div>
  );
};

export default App;