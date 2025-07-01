import React, { useState, useRef, useEffect } from 'react';
import { MessageCircle, X, Send, Bot, User, Trash2, Sparkles, Heart, Star, Crown, Zap, Coffee, Award, MapPin, Phone, Clock, ChefHat } from 'lucide-react';
import { useChatbot } from '../context/ChatbotContext';

const Chatbot: React.FC = () => {
  const { mensajes, enviarMensaje, limpiarChat, chatAbierto, setChatAbierto, preguntasFrecuentes } = useChatbot();
  const [inputValue, setInputValue] = useState('');
  const [escribiendo, setEscribiendo] = useState(false);
  const messagesEndRef = useRef<HTMLDivElement>(null);

  // Auto scroll al final
  useEffect(() => {
    messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' });
  }, [mensajes]);

  // Manejar envío de mensaje
  const handleSubmit = (e: React.FormEvent) => {
    e.preventDefault();
    if (inputValue.trim()) {
      setEscribiendo(true);
      enviarMensaje(inputValue.trim());
      setInputValue('');
      setTimeout(() => setEscribiendo(false), 2000);
    }
  };

  // Enviar pregunta frecuente
  const enviarPreguntaFrecuente = (pregunta: string) => {
    setEscribiendo(true);
    enviarMensaje(pregunta);
    setTimeout(() => setEscribiendo(false), 2000);
  };

  // Formatear timestamp
  const formatearHora = (timestamp: Date) => {
    return timestamp.toLocaleTimeString('es-PE', { 
      hour: '2-digit', 
      minute: '2-digit' 
    });
  };

  return (
    <>
      {/* Botón flotante ultra premium */}
      <button
        onClick={() => setChatAbierto(!chatAbierto)}
        className={`fixed bottom-8 right-8 z-50 w-20 h-20 rounded-full shadow-2xl transition-all duration-700 transform hover:scale-110 ${
          chatAbierto 
            ? 'bg-gradient-to-br from-red-500 via-red-600 to-red-700 hover:from-red-600 hover:to-red-800 rotate-180' 
            : 'bg-gradient-to-br from-[#8B4513] via-[#A0522D] to-[#CD853F] hover:from-[#654321] hover:to-[#8B4513] animate-pulse'
        } group overflow-hidden`}
        style={{
          boxShadow: chatAbierto 
            ? '0 25px 50px rgba(239, 68, 68, 0.4), 0 0 30px rgba(239, 68, 68, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.2)' 
            : '0 25px 50px rgba(139, 69, 19, 0.4), 0 0 30px rgba(139, 69, 19, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.2)'
        }}
      >
        {/* Efectos de fondo animados */}
        <div className="absolute inset-0 bg-gradient-to-r from-white/20 via-white/10 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-500 animate-pulse"></div>
        <div className="absolute top-2 right-2 w-3 h-3 bg-white/40 rounded-full animate-ping"></div>
        <div className="absolute bottom-2 left-2 w-2 h-2 bg-white/50 rounded-full animate-bounce"></div>
        <div className="absolute top-1/2 left-1/2 w-8 h-8 border border-white/20 rounded-full transform -translate-x-1/2 -translate-y-1/2 animate-spin-slow"></div>
        
        <div className="relative w-full h-full flex items-center justify-center">
          {chatAbierto ? (
            <X size={32} className="text-white transition-transform duration-500 drop-shadow-lg" />
          ) : (
            <>
              <MessageCircle size={32} className="text-white animate-pulse drop-shadow-lg" />
              <div className="absolute -top-2 -right-2 w-6 h-6 bg-gradient-to-r from-yellow-400 to-orange-400 rounded-full animate-bounce flex items-center justify-center shadow-lg">
                <Sparkles size={12} className="text-white" />
              </div>
            </>
          )}
        </div>
      </button>

      {/* Ventana del chat ultra premium */}
      {chatAbierto && (
        <div className="fixed bottom-32 right-8 z-40 w-96 h-[700px] bg-white/95 backdrop-blur-xl rounded-3xl shadow-2xl border border-white/20 flex flex-col animate-in slide-in-from-bottom-5 duration-700 overflow-hidden"
             style={{ 
               boxShadow: '0 25px 50px rgba(0, 0, 0, 0.25), 0 0 50px rgba(139, 69, 19, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.2)',
               background: 'linear-gradient(135deg, rgba(255, 255, 255, 0.95) 0%, rgba(255, 248, 220, 0.95) 100%)'
             }}>
          
          {/* Header ultra premium con gradiente y efectos */}
          <div className="bg-gradient-to-br from-[#8B4513] via-[#A0522D] to-[#CD853F] text-white p-6 rounded-t-3xl relative overflow-hidden">
            {/* Efectos decorativos del header */}
            <div className="absolute inset-0 opacity-20">
              <div className="absolute top-3 right-6 w-12 h-12 border-2 border-white/30 rounded-full animate-spin-slow"></div>
              <div className="absolute bottom-3 left-6 w-8 h-8 border border-white/30 rounded-full animate-pulse"></div>
              <div className="absolute top-1/2 left-1/2 w-16 h-16 bg-white/10 rounded-full transform -translate-x-1/2 -translate-y-1/2 animate-pulse"></div>
              <div className="absolute top-2 left-2 w-4 h-4 bg-yellow-400/30 rounded-full animate-bounce"></div>
              <div className="absolute bottom-2 right-2 w-6 h-6 bg-white/20 rounded-full animate-float"></div>
            </div>
            
            <div className="flex items-center justify-between relative z-10">
              <div className="flex items-center">
                <div className="relative">
                  <div className="w-16 h-16 bg-white/25 rounded-3xl flex items-center justify-center mr-4 animate-float shadow-xl backdrop-blur-sm border border-white/30">
                    <ChefHat size={32} className="text-white" />
                  </div>
                  <div className="absolute -bottom-1 -right-1 w-6 h-6 bg-gradient-to-r from-green-400 to-emerald-500 rounded-full border-2 border-white animate-pulse flex items-center justify-center shadow-lg">
                    <div className="w-2 h-2 bg-white rounded-full animate-ping"></div>
                  </div>
                  <div className="absolute -top-1 -left-1 w-4 h-4 bg-yellow-400 rounded-full animate-bounce shadow-lg">
                    <Crown size={12} className="text-white p-0.5" />
                  </div>
                </div>
                <div>
                  <h3 className="font-bold text-2xl text-white mb-1 flex items-center">
                    Cuy-Bot 
                    <span className="ml-2 text-2xl animate-bounce">🐹</span>
                  </h3>
                  <p className="text-sm text-white/90 flex items-center font-semibold">
                    <div className="w-2 h-2 bg-green-400 rounded-full mr-2 animate-pulse"></div>
                    En línea • Restaurante Nieves
                  </p>
                  <p className="text-xs text-white/80 font-medium mt-1">
                    🇵🇪 Asistente gastronómico especializado
                  </p>
                </div>
              </div>
              <div className="flex items-center space-x-2">
                <button
                  onClick={limpiarChat}
                  className="p-3 hover:bg-white/20 rounded-2xl transition-all duration-300 hover:scale-110 group backdrop-blur-sm"
                  title="Limpiar chat"
                >
                  <Trash2 size={18} className="group-hover:text-red-200 transition-colors" />
                </button>
                <button
                  onClick={() => setChatAbierto(false)}
                  className="p-3 hover:bg-white/20 rounded-2xl transition-all duration-300 hover:scale-110 backdrop-blur-sm"
                  title="Cerrar chat"
                >
                  <X size={18} />
                </button>
              </div>
            </div>
          </div>

          {/* Mensajes con diseño ultra premium */}
          <div className="flex-1 overflow-y-auto p-6 space-y-6 bg-gradient-to-b from-gray-50 to-white">
            {mensajes.map((mensaje) => (
              <div
                key={mensaje.id}
                className={`flex ${mensaje.esBot ? 'justify-start' : 'justify-end'} animate-in slide-in-from-bottom-2 duration-500`}
              >
                <div className={`max-w-[85%] ${mensaje.esBot ? 'order-2' : 'order-1'}`}>
                  <div
                    className={`p-5 rounded-3xl shadow-lg transition-all duration-300 hover:shadow-xl ${
                      mensaje.esBot
                        ? 'bg-white text-gray-900 border border-gray-200 rounded-bl-lg'
                        : 'bg-gradient-to-br from-[#8B4513] to-[#CD853F] text-white rounded-br-lg'
                    }`}
                    style={{
                      boxShadow: mensaje.esBot 
                        ? '0 10px 25px rgba(0, 0, 0, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.5)'
                        : '0 10px 25px rgba(139, 69, 19, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.2)'
                    }}
                  >
                    <p className="text-sm leading-relaxed whitespace-pre-line font-semibold">{mensaje.texto}</p>
                    <p className={`text-xs mt-3 font-bold ${mensaje.esBot ? 'text-gray-500' : 'text-white/80'}`}>
                      {formatearHora(mensaje.timestamp)}
                    </p>
                  </div>
                </div>
                <div className={`w-12 h-12 rounded-2xl flex items-center justify-center ${mensaje.esBot ? 'order-1 mr-4' : 'order-2 ml-4'} flex-shrink-0`}>
                  {mensaje.esBot ? (
                    <div className="w-12 h-12 bg-gradient-to-br from-[#8B4513] to-[#CD853F] rounded-2xl flex items-center justify-center shadow-xl relative overflow-hidden border border-white/20">
                      <Bot size={20} className="text-white relative z-10" />
                      <div className="absolute inset-0 bg-gradient-to-r from-white/20 to-transparent opacity-0 hover:opacity-100 transition-opacity"></div>
                    </div>
                  ) : (
                    <div className="w-12 h-12 bg-gradient-to-br from-gray-600 to-gray-700 rounded-2xl flex items-center justify-center shadow-xl border border-white/20">
                      <User size={20} className="text-white" />
                    </div>
                  )}
                </div>
              </div>
            ))}
            
            {escribiendo && (
              <div className="flex justify-start animate-in slide-in-from-bottom-2 duration-500">
                <div className="w-12 h-12 bg-gradient-to-br from-[#8B4513] to-[#CD853F] rounded-2xl flex items-center justify-center mr-4 shadow-xl animate-pulse border border-white/20">
                  <Bot size={20} className="text-white" />
                </div>
                <div className="bg-white p-5 rounded-3xl rounded-bl-lg shadow-lg border border-gray-200"
                     style={{ boxShadow: '0 10px 25px rgba(0, 0, 0, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.5)' }}>
                  <div className="flex items-center space-x-2">
                    <div className="flex space-x-1">
                      <div className="w-3 h-3 bg-[#8B4513] rounded-full animate-bounce"></div>
                      <div className="w-3 h-3 bg-[#8B4513] rounded-full animate-bounce" style={{ animationDelay: '0.1s' }}></div>
                      <div className="w-3 h-3 bg-[#8B4513] rounded-full animate-bounce" style={{ animationDelay: '0.2s' }}></div>
                    </div>
                    <span className="text-xs text-gray-700 ml-3 font-bold">Cuy-Bot está escribiendo...</span>
                  </div>
                </div>
              </div>
            )}
            
            <div ref={messagesEndRef} />
          </div>

          {/* Preguntas frecuentes ultra premium */}
          {mensajes.length <= 1 && (
            <div className="p-6 border-t bg-gradient-to-r from-gray-50 to-white">
              <div className="flex items-center mb-4">
                <div className="w-8 h-8 bg-gradient-to-r from-yellow-400 to-orange-400 rounded-full flex items-center justify-center mr-3 shadow-lg animate-pulse">
                  <Star size={16} className="text-white" />
                </div>
                <p className="text-sm text-gray-900 font-black">Preguntas populares:</p>
              </div>
              <div className="space-y-3">
                {preguntasFrecuentes.slice(0, 3).map((faq) => (
                  <button
                    key={faq.id}
                    onClick={() => enviarPreguntaFrecuente(faq.pregunta)}
                    className="w-full text-left text-sm p-4 bg-white hover:bg-gradient-to-r hover:from-[#FFF8DC] hover:to-[#F5DEB3] rounded-2xl transition-all duration-300 border border-gray-200 hover:border-[#8B4513]/30 hover:shadow-lg transform hover:scale-[1.02] group"
                    style={{ boxShadow: '0 4px 6px rgba(0, 0, 0, 0.05)' }}
                  >
                    <div className="flex items-center">
                      <div className="w-3 h-3 bg-gradient-to-r from-[#8B4513] to-[#CD853F] rounded-full mr-3 group-hover:animate-pulse"></div>
                      <span className="text-gray-900 font-bold group-hover:text-[#8B4513] transition-colors">{faq.pregunta}</span>
                    </div>
                  </button>
                ))}
              </div>
            </div>
          )}

          {/* Input ultra premium con diseño sofisticado */}
          <form onSubmit={handleSubmit} className="p-6 border-t bg-white rounded-b-3xl">
            <div className="flex space-x-4">
              <input
                type="text"
                value={inputValue}
                onChange={(e) => setInputValue(e.target.value)}
                placeholder="Escribe tu mensaje..."
                className="flex-1 px-5 py-4 border-2 border-gray-300 rounded-2xl focus:outline-none focus:ring-2 focus:ring-[#8B4513]/30 focus:border-[#8B4513] text-sm bg-gray-50 focus:bg-white transition-all duration-200 text-gray-900 font-semibold placeholder-gray-500"
                style={{ boxShadow: 'inset 0 2px 4px rgba(0, 0, 0, 0.05)' }}
                disabled={escribiendo}
              />
              <button
                type="submit"
                disabled={!inputValue.trim() || escribiendo}
                className="px-6 py-4 bg-gradient-to-r from-[#8B4513] to-[#CD853F] text-white rounded-2xl hover:from-[#654321] hover:to-[#8B4513] disabled:opacity-50 disabled:cursor-not-allowed transition-all duration-300 transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-[#8B4513]/50 shadow-xl hover:shadow-2xl group"
                style={{ boxShadow: '0 10px 25px rgba(139, 69, 19, 0.3)' }}
              >
                <Send size={20} className="group-hover:translate-x-1 transition-transform duration-200" />
              </button>
            </div>
            
            {/* Footer del chat con información del restaurante */}
            <div className="flex items-center justify-center mt-4 space-x-6 text-xs text-gray-600">
              <div className="flex items-center">
                <MapPin size={12} className="mr-1 text-[#8B4513]" />
                <span className="font-bold">Lima, Perú</span>
              </div>
              <div className="flex items-center">
                <Phone size={12} className="mr-1 text-[#8B4513]" />
                <span className="font-bold">992 579 584</span>
              </div>
              <div className="flex items-center">
                <Clock size={12} className="mr-1 text-[#8B4513]" />
                <span className="font-bold">11AM - 10PM</span>
              </div>
            </div>
            
            {/* Indicador de estado con corazón */}
            <div className="flex items-center justify-center mt-3">
              <div className="flex items-center text-xs text-gray-700 bg-gradient-to-r from-red-50 to-pink-50 px-4 py-2 rounded-full border border-red-200 shadow-sm">
                <Heart size={14} className="text-red-400 mr-2 animate-pulse" />
                <span className="font-bold">Hecho con amor peruano</span>
                <Crown size={14} className="text-yellow-500 ml-2 animate-bounce" />
              </div>
            </div>
          </form>
        </div>
      )}
    </>
  );
};

export default Chatbot;
